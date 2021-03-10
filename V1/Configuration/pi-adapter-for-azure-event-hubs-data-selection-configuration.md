---
uid: PIAdapterForAzureEventHubsDataSelectionConfiguration
---

# PI Adapter for Azure Event Hubs data selection configuration

In addition to the data source configuration, you need to provide a data selection configuration to specify the data you want the adapter to collect from the data sources.

## Configure Azure Event Hubs data selection

Complete the following steps to configure an Azure Event Hubs data selection. Use the `PUT` method in conjunction with the `api/v1/configuration/<ComponentId>/DataSelection` REST endpoint to initialize the configuration.

1. Using a text editor, create an empty text file.

2. Copy and paste an example configuration for an Azure Event Hubs data selection into the file.

    For sample JSON, see [Azure Event Hubs data selection examples](#azure-event-hubs-data-selection-examples).

3. Update the example JSON parameters for your environment.

    For a table of all available parameters, see [Azure Event Hubs data selection parameters](#azure-event-hubs-data-selection-parameters).

4. Save the file. For example, as `ConfigureDataSource.json`.

5. Open a command line session. Change directory to the location of `ConfigureDataSource.json`.

6. Enter the following cURL command (which uses the `PUT` method) to initialize the data source configuration.

    ```bash
    curl -d "@ConfigureDataSource.json" -H "Content-Type: application/json" -X PUT "http://localhost:5590/api/v1/configuration/AzureEventHubs1/DataSelection"
    ```

    **Notes:**
  
    * If you installed the adapter to listen on a non-default port, update `5590` to the port number in use.
    * If you use a component ID other than `AzureEventHubs1`, update the endpoint with your chosen component ID.
    * For a list of other REST operations you can perform, like updating or deleting a data source configuration, see [REST URLs](#rest-urls).
    <br/>
    <br/>

7. Configure data selection.

## Azure Event Hubs data selection schema

The full schema definition for the Azure Event Hubs data selection configuration is in the `EventHubs_DataSelection_schema.json` file located in one of the following folders:

Windows: `%ProgramFiles%\OSIsoft\Adapters\EventHubs\Schemas`

Linux: `/opt/OSIsoft/Adapters/EventHubs/Schemas`

## Azure Event Hubs data selection parameters

| Parameter        | Required | Type      | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
|------------------|----------|-----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Selected**     | Optional | `boolean` | Selects or clears a measurement. To select an item, set to `true`. To remove an item, leave the field empty or set to `false`.  <br><br>Allowed value: `true` or `false`<br>Default value: `false`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| **Name**         | Optional | `string`  | The optional friendly name of the data item collected from the data source. <br><br>Allowed value: any string<br>Default value: `null`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| **StreamId**     | Optional | `string`  | The custom stream ID that is used to create the streams. If you do not specify the StreamID, the adapter generates a default stream ID based on the measurement configuration. A properly configured custom stream ID follows these rules:<br><br>Is not case-sensitive.<br>Can contain spaces.<br>Cannot start with two underscores ("__").<br>Can contain a maximum of 100 characters.<br>Cannot use the following characters:<br> `/` `:` `?` `#` `[` `]` `@` `!` `$` `&` `'` `(` `)` `\` `*` `+` `,` `;` `=` `%` `<` `>` or the vertical bar<br>Cannot start or end with a period.<br>Cannot contain consecutive periods.<br>Cannot consist of only periods.<br><br>The default ID automatically updates when there are changes to the measurement and follows the format of `<Id>.<ValueField>` |
| **DataFilterId** | Optional | `string`  | The ID of the data filter. <br><br>Allowed value: any string <br>Default value: `null`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | **DataFilterCache** | Optional | `` | The cache to support data filtering. The cache stores previous and last value. |  |
| **EventHubName** | Required | `string`  | The name of the event hub to collect data from. <br><br>Allowed value: Maximum of 256 characters per Azure limits<br>Default value: `{EventHubName}`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| **ValueField**   | Required | `string`  | The JsonPath expression<sup>1</sup>  to take value from a property.<br><br>Allowed value: cannot be `null`, empty, or whitespace.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| **TimeField**    | Optional | `string`  | The JsonPath expression<sup>1</sup> to take value to use as a timestamp from a property.<br>**Note:** The adapter generates a timestamp when `null` is specified.<br><br>Allowed value: cannot be `null`, empty, or whitespace.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| **DeviceId**     | Optional | `string`  | The device Id associated with the IoT Hub.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    | <br>If specified, the event is sent only if it originated from the specified device. If omitted, the event is sent to all streams  that match the selection. |
| **DataType**     | Required | `string`  | The expected data type of the values for the specified field. <br><br>Allowed value: OMF supported data types                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| **TimeFormat** | Optional | `string` | The time format of the timestamp value specified in the TimeField property<br><br>Allowed value: Any string that can be used as a DateTime format in the .NET `DateTime.TryParseExact()`method, for example `01/30/2021`.<br> For more information, see [DateTime.TryParseExact Method](https://docs.microsoft.com/en-us/dotnet/api/system.datetime.tryparseexact?view=net-5.0)<sup>1</sup><br><br>**Note:** Specify `Adapter` to have the adapter supply the timestamp and ignore the TimeField. If you specify `null`, the adapter parses the timestamp identified in TimeField as a DateTime supporting ISO 8601 formats.

<sup>1</sup> **Note:** JsonPath expressions can be expensive to evaluate. For best performance, avoid complicated expressions in favor of direct references to data.

## Azure Event Hubs data selection examples

The following are examples of valid Azure Event Hubs data selection configurations<sup>1</sup>:

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
    "TimeField": "$.TimeStamp",
    "DeviceId" : "EventHub7",
    "DataType" : "uint64",
    "TimeFormat" : null    
  }
]
```

<sup>1</sup> **Note:** Both **ValueField** and **TimeField** require the correct structure of the JSON payload to be specified, in other words, what the data source returns. The previous examples use the following JSON payload structure:

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

## REST URLs

| Relative URL | HTTP verb | Action |
| ------------ | --------- | ------ |
| api/v1/configuration/_ComponentId_/DataSelection  | GET | Retrieves the Azure Event Hubs data selection configuration |
| api/v1/configuration/_ComponentId_/DataSelection  | PUT | Configures or updates the Azure Event Hubs data selection configuration |
| api/v1/configuration/_ComponentId_/DataSelection | DELETE | Deletes the Azure Event Hubs data selection configuration |
| api/v1/configuration/_ComponentId_/DataSelection | PATCH | Allows partial updating of configured data selection items. <br>**Note:** The request must be an array containing one or more data selection items. Each data selection item in the array must include its *StreamId*. |
| api/v1/configuration/_ComponentId_/DataSelection/_StreamId_ | PUT | Updates or creates a new data selection with the specified *StreamId*|
| api/v1/configuration/_ComponentId_/DataSelection/_StreamId_ | DELETE | Deletes a specific data selection item of the Azure Event Hubs data selection configuration |

**Note:** Replace _ComponentId_ with the Id of your Azure Event Hubs component, for example AzureEventHubs1.
