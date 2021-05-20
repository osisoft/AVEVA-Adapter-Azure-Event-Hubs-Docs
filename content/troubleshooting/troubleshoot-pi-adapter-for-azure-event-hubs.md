---
uid: TroubleshootPIAdapterForAzureEventHubs
---

# Troubleshoot PI Adapter for Azure Event Hubs

PI Adapter for Azure Event Hubs provides troubleshooting features that enable you to verify adapter configuration, confirm connectivity, and view message logs. If you are unable to resolve issues with the adapter or need additional guidance, contact OSIsoft Technical Support through the [OSIsoft Customer Portal](https://my.osisoft.com/).

## Check configurations

Incorrect configurations can interrupt data flow and cause errors in values and ranges. Perform the following steps to confirm correct configuration for your adapter.

1. If the adapter is failing to collect any data, navigate to <xref:PIAdapterForAzureEventHubsDataSourceConfiguration> and verify that the following parameter values are correct.

    | Parameter                             | Description |
    |---------------------------------------|-------------|
    | **StreamIdPrefix**                    | If you have recently updated this prefix setting, you must [restart the adapter](xref:StartAndStopAnAdapter) for the change to take effect. |
    | **EventHubNamespaceConnectionString** | Verify that the string is entered correctly. If the string is entered incorrectly, the adapter cannot connect to the AEH namespace. |
    | **ConsumerGroupName**                 | Verify that the group name is entered correctly. If the group name is entered incorrectly, the adapter cannot read the event stream. |
    | **BlobStorageConnectionString**       | Verify that the string is entered correctly. If the string is entered incorrectly, the adapter cannot perform checkpointing, which disrupts data collection. |
    | **CheckpointBlobContainerName**       | Verify that the container name is entered correctly. If the name is entered incorrectly, the adapter cannot perform checkpointing, which disrupts data collection. |

2. If specific data streams or sub-streams are not updating, navigate to <xref:PIAdapterForAzureEventHubsDataSelectionConfiguration> and verify that the following data selection items are correct:

    | Parameter           | Description |
    |---------------------|-------------|
    | **StreamId**        | If you using a custom stream ID that is not being generated, verify that it follows the [stream ID rules](xref:PIAdapterForAzureEventHubsDataSelectionConfiguration#data-selection-parameters). If the custom stream ID does not follow the rules, the adapter generates a default stream ID based on the measurement configuration. |
    | **EventHubName**    | The event hub name is valid. If the name is invalid, the adapter cannot collect data. |
    | **ValueField**      | The JSONPath expression is valid. With an invalid JSONPath expression, the adapter cannot extract a data value from the AEH payload. |
    | **TimeField**       | The JSONPath expression is valid. With an invalid JSONPath expression, the adapter cannot extract a timestamp from the AEH payload. |
    | **DataType**        | The correct data type is referenced. An incorrect data type causes data conversion to fail. |
    | **TimeFormat**      | The correct time format is referenced. A time format that does not match the value from **TimeField** means that the adapter cannot convert timestamp from the AEH payload. |

3. If the adapter is performing suboptimal, navigate to <xref:PIAdapterForAzureEventHubsClientSettingsConfiguration> and review the configuration for any custom values that override default settings. Default client settings fit most use cases, so customized settings are more likely to cause issues.

4. Navigate to <xref:EgressEndpointsConfiguration>. For each configured endpoint, verify that the **Endpoint** and authentication properties are correct.

    * For a PI server or EDS endpoint, verify **UserName** and **Password**.
    * For an OCS endpoint, verify **ClientId** and **ClientSecret**.

## Check connectivity

Perform the following steps to verify active connections to the data source and egress endpoints.

1. Based on your egress endpoints, verify that data values are updating.

    * For PI Server, send a request to the PI Web API to verify that PI point values are updating. Use Postman or a Web browser to send the request. For more information, see [PI Web API Reference](https://techsupport.osisoft.com/Documentation/PI-Web-API/help/controllers/point.html).

        Alternatively, use any PI Client software to read point values from the PI Data Archive directly.

    * For OCS, view the OCS portal to verify that data streams are updating. For more information, see [Getting started with trend data](https://ocs-docs.osisoft.com/Content_Portal/Quickstarts/Getting-Started-Trend.html).

        Alternatively, you can use Postman to send an API request to verify data streams. For more information, see [API calls for reading data](https://ocs-docs.osisoft.com/Content_Portal/Documentation/SequentialDataStore/Reading_Data_API.html).

2. If configured, use a health endpoint to determine the status of the adapter.

    For more information, see [Health and diagnostics](xref:HealthAndDiagnostics).

## Check logs

Perform the following steps to view the adapter and endpoint logs to isolate issues for resolution.

1. Navigate to the logs directory:

   * Windows: `%ProgramData%\OSIsoft\Adapters\BACnet\Logs`
   * Linux: `/usr/share/OSIsoft/Adapters/BACnet/Logs`

2. Optional: Change the log level of the adapter to receive more information and context.

    For more information, see [Logging configuration](xref:LoggingConfiguration).
