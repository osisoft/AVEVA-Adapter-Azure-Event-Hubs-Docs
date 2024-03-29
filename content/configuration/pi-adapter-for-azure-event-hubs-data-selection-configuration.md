---
uid: PIAdapterForAzureEventHubsDataSelectionConfiguration
---

# Data selection

In addition to the data source configuration, you need to provide a data selection configuration to specify the data you want the adapter to collect from the data sources.

## To configure data selection

Complete the following steps to configure an Azure Event Hubs data selection. Use the `PUT` method in conjunction with the `api/v1/configuration/<ComponentId>/DataSelection` REST endpoint to initialize the configuration.

1. Using a text editor, create an empty text file.

2. Copy and paste an example configuration for an Azure Event Hubs data selection into the file.

    For sample JSON, see [Data selection examples](#data-selection-examples).

3. Update the example JSON parameters for your environment.

    For a table of all available parameters, see [Data selection parameters](#data-selection-parameters).

4. Save the file. For example, as `ConfigureClientSettings.json`.

5. Open a command line session. Change the directory to the location of `ConfigureClientSettings.json`.

6. Enter the following cURL command (which uses the `PUT` method) to initialize the client settings configuration.

    ```bash
    curl -d "@ConfigureClientSettings.json" -H "Content-Type: application/json" -X PUT "http://localhost:5590/api/v1/configuration/AzureEventHubs1/DataSelection"
    ```

    **Notes:**
  
    * If you installed the adapter to listen on a non-default port, update `5590` to the port number you used.
    * If you use a component ID other than `AzureEventHubs1`, update the endpoint with your chosen component ID.
    * For a list of other REST operations you can perform, like updating or deleting a client settings configuration, see [REST URLs](#rest-urls).
    <br/>
    <br/>

## Data selection schema

The full schema definition for the Azure Event Hubs data selection configuration is in the `EventHubs_DataSelection_schema.json` file located in one of the following folders:

* Windows: `%ProgramFiles%\OSIsoft\Adapters\EventHubs\Schemas`
* Linux: `/opt/OSIsoft/Adapters/EventHubs/Schemas`

## Data selection parameters

| Parameter | Required | Type | Description |
|--|:--:|--|--|
| **Selected** | Optional | `boolean` | Selects or clears a measurement. To select an item, set to `true`. To remove an item, leave the field empty or set to `false`.  <br><br>Allowed value: `true` or `false`<br>Default value: `false` |
| **Name** | Optional | `string` | The optional friendly name of the data item collected from the data source <br><br>Allowed value: any string<br>Default value: `null` |
| **StreamId** | Optional | `string` | The custom identifier used to create the streams. If you do not specify the StreamID or define it as `null`, the adapter generates a default **StreamId** based on the measurement configuration. Additionally, within this default **StreamId** value, the text parser replaces any automatically generated special characters with a replacement character. You can override these replacement characters by manually editing the data selection configuration. For more information on character replacement, see [Special characters support](xref:TextParser#special-characters-support).<br><br>A properly configured custom identifier follows the **stream ID rules**:<br><br>Is not case-sensitive<br>Can contain spaces<br>Cannot start with two underscores ("__")<br>Can contain a maximum of 100 characters<br>Cannot start or end with a period<br>Cannot contain consecutive periods<br>Cannot consist of only periods.<br><br>The default ID automatically updates when there are changes to the measurement and follows the format of `<Id>.<ValueField>`.<br><br>**Note:** At time of data egress, the adapter encodes any invalid characters within the **StreamId**. For more information, see [Egress endpoints](xref:EgressEndpointsConfiguration#special-characters-encoding). |
| **DataFilterId** | Optional | `string` | The ID of the data filter <br><br>Allowed value: any string <br>Default value: `null`<br>**Note:** If the specified **DataFilterId** does not exist, unfiltered data is sent until that **DataFilterId** is created. | **DataFilterCache** | Optional | `` | The cache to support data filtering. The cache stores previous and last value. |  |
| **EventHubName** | Required | `string` | The name of the event hub to collect data from <br><br>Allowed value: Maximum of 256 characters per Azure limits<br>Default value: `{EventHubName}` |
| **ValueField** | <sup>1</sup> | `string` | The JSONPath expression<sup>2</sup> to take value from a property |
| **DataFields** | <sup>1</sup> | `string` | A `ComplexTypeMapping` that maps JSONPath expressions of fields to property names. Supported complex data types are `Coordinates` (x, y, and z) or `Geolocation` (latitude and longitude).<br><br>[Complex data type field mapping examples](#complex-data-type-field-mapping-examples)
| **IndexField** | Optional | `string` | The JSONPath expression<sup>2</sup> to take value to use as a timestamp from a property<br>**Note:** The adapter generates a timestamp when `null` is specified. |
| **DeviceId** | Optional | `string` | The device Id associated with the IoT Hub. | <br>If specified, the event is sent only if it originated from the specified device. If omitted, the event is sent to all streams  that match the selection. |
| **DataType** | Required | `string` | The expected data type of the values for the specified field.<br><br>Supported Azure Event Hub data types include: `Boolean`, `Int64`, `Int32`, `Int16`, `UInt64`, `UInt32`, `UInt16`, `Float64`, `Float32`, `Float16`, `Date-Time`, `String`.<br><br>For more information, see <xref:PIAdapterForAzureEventHubsPrinciplesOfOperation>. |
| **IndexFormat** | Optional | `string` | The time format of the timestamp value specified in the IndexField property.<br><br>Allowed value: Any string that can be used as a DateTime format in the .NET `DateTime.TryParseExact()` method, for example `01/30/2021`.<br> For more information, see [Date and time processing](xref:PIAdapterforAzureEventHubsTextParser#date-and-time-processing).<sup>2</sup><br><br>**Note:** If you specify `null`, the adapter parses the timestamp identified in IndexField as a DateTime supporting ISO 8601 formats. |

<sup>1</sup>: `DataFields` and `ValueField` are mutually exclusive. You must define one or the other, but not both.<br>
<sup>2</sup>: JSONPath expressions can be expensive to evaluate. For the best performance, avoid complicated expressions in favor of direct references to data.

## Data selection examples

The following are examples of valid Azure Event Hubs data selection configurations:

### Minimal data selection configuration

```json
[
  {
    "EventHubName" : "SampleEventHubName",
    "ValueField" : "$.TestNode[:1].Value",
    "DataType" : "uint64"
  }
]
```

### Complete data selection configuration

```json
[
  {
    "Selected" : true,
    "Name" : null,
    "StreamId" : "SampleStreamId",
    "DataFilterId" : null,
    "EventHubName" : "SampleEventHubName",
    "ValueField": "$.Events[0].Value",
    "IndexField": "$.TimeStamp",
    "DeviceId" : "EventHub7",
    "DataType" : "uint64",
    "IndexFormat" : null    
  }
]
```

**Note:** Both **ValueField** and **IndexField** require the correct structure of the JSON payload to be specified. The previous examples use the following JSON payload structure:

```json
{
  "TimeStamp": "02/17/2021 12:01:36 AM PST",
  "Events": [
    {
      "Value": "4578",
      "DataType": "int"
    }
  ]
}
```

## Complex data type field mapping examples 

When working with the `DataFields` or `DataType` [data selection parameters](#data-selection-parameters), you can provide complex data types field mappings as JSONPath expressions. PI Adapter for Azure Event Hubs supports the following complex data types: `Coordinates` and `Geolocation`.

### `Coordinates` example

```json
{"X": "$['xValue']", "Y": "$['yValue']", "Z": "$['zValue']"}
```

### `Geolocation` example

```json
{"Latitude": "$['latitudeValue']", "Longitude": "$['longitudeValue']"}
```

## REST URLs

| Relative URL | HTTP verb | Action |
|--|--|--|
| api/v1/configuration/\<ComponentId\>/DataSelection | `GET` | Retrieves the data selection configuration, including all data selection items. |
| api/v1/configuration/\<ComponentId\>/DataSelection | `PUT` | Configures or updates the data selection configuration. The adapter starts collecting data for each data selection item when the following conditions are met:<br/><br/>&bull; The data selection configuration `PUT` request is received.<br/>&bull; A data source configuration is active. |
| api/v1/configuration/\<ComponentId\>/DataSelection | `DELETE` | Deletes the active data selection configuration. The adapter stops collecting data. |
| api/v1/configuration/\<ComponentId\>/DataSelection | `PATCH` | Allows partial updates of configured data selection items.<br/><br/>**Note:** The request must be an array containing one or more data selection items. Each item in the array must include its **StreamId**. |
| api/v1/configuration/\<ComponentId\>/DataSelection/\<StreamId\> | `PUT` | Updates or creates a new data selection item by **StreamId**. For new items, the adapter starts collecting data after the request is received. |
| api/v1/configuration/\<ComponentId\>/DataSelection/\<StreamId\> | `DELETE` | Deletes a data selection item from the configuration by **StreamId**. The adapter stops collecting data for the deleted item. |

**Note:** Replace \<ComponentId\> with the Id of your Azure Event Hubs component, for example AzureEventHubs1.
