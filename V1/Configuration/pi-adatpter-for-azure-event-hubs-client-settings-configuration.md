---
uid: PIAdapterForAzureEventHubsClientSettingsConfiguration
---

# PI Adapter for Azure Event Hubs client settings configuration

The client settings configuration is automatically generated when a new data source is added. If you experience problems with timeouts or when Azure Event Hubs limits are exceeded in terms of browse or subscription operation, you can change the client settings configuration.

## Configure Azure Event Hubs client settings

Complete the following steps to configure the Azure Event Hubs client settings:

1. Using any text editor, create a file that contains the Azure Event Hubs client settings in the JSON format.
    - For content structure, see [Azure Event Hubs client settings example](#azure-event-hubs-client-settings-example).
    - For all available parameters, see [Azure Event Hubs client settings](#azure-event-hubs-client-settings-parameters).
2. Save the file. For example, `ConfigureClientSettings.json`.
3. Use any of the [Configuration tools](xref:ConfigurationTools) capable of making HTTP requests to run a `PUT` command to its appropriate endpoint:

    **Note:** The following example uses AzureEventHubs1 as the adapter component name. For more information on how to add a component, see [System components configuration](xref:SystemComponentsConfiguration).
  
    `5590` is the default port number. If you selected a different port number, replace it with that value.

    **PUT** endpoint: `http://localhost:5590/api/v1/configuration/<componentId>/ClientSettings/`

      Example using `curl`:

    ```bash
    curl -d "@ConfigureClientSettings.json" -H "Content-Type: application/json" -X PUT "http://localhost:5590/api/v1/configuration/AzureEventHubs1/ClientSettings"
    ```

    **Note:** Run this command from the same directory where the file is located.

## Azure Event Hubs client settings schema

The full schema definition for the Azure Event Hubs client settings configuration is in the `AzureEventHubs_ClientSettings_schema.json` file located in one of the following folders:

Windows: `%ProgramFiles%\OSIsoft\Adapters\AzureEventHubs\Schemas`

Linux: `/opt/OSIsoft/Adapters/AzureEventHubs/Schemas`

## Azure Event Hubs client settings parameters

The following parameters are available for configuring Azure Event Hubs client settings:

| Parameter                | Required | Type       | Description |
|--------------------------|----------|------------|-------------|
| **MaxInternalQueueSize** | Optional | `integer`  |  Specifies maximum number of value updates that can be held by the adapter in memory.<br><br>Allowed value: > `1000`<br>Default value: `500000`           |
| **InternalQueuePollingIntervalInMs** | Optional | `integer` | Specified interval at which data is removed from internal queue. <br><br>Allowed value: Between `1` and `60000` milliseconds<br>Default value: `100` |
| **NumOfParallelQueueReaders** | Optional | `integer` | The number of concurrent internal queue readers.<br>Allowed value: Between `1` and the number of processors times 2.<br>Default value: `100` |
| **TrackLastEnqueuedEventProperties** | | `boolean` | Indicates if the user should request information on the last enqueued event on the partition associated with a given event, and track that  information as events are received. <br><br>Allowed value: `true` or `false` <br>Default value: `false`|
| **CacheEventCount** | | `integer` | The maximum amount of events read from the Event Hubs service and held in a local memory cache when reading is active and events are emitted to an enumerator for processing.<br><br>Default value: `100` |
|**PrefetchCount** | | `integer` | The number of events requested from the Event Hubs service and staged locally regardless of whether a reader is active. **PrefetchCount** is intended to maximize throughput by buffering service operations. <br><br>Allowed value: Must be greater than `2` times the **CacheEventCount**.|
| **BatchSizeForCheckpoint** | | `integer`| The number of events processed to trigger a checkpoint operation.<br><br>Default value: `50` |
| **CheckpointTimeoutSeconds** | | `integer`| The timeout in seconds for the checkpoint operation.<br><br>Default value: `60` |
| **EventHubTransportType** | | `enum` | Identifies the protocol used internally by the client. Allowed values: `AmqpTcp` and `AmqpWebSockets`<br>Default value: `AmqpTcp`|
| **DeviceIdSystemPropertyName** | Optional | `string` | The name of the system property for the device id.<br><br>Default value: `iothub-connection-device-id` |

## Azure Event Hubs client settings example

```json
{
   "MaxInternalQueueSize" : 500000,
   "InternalQueuePollingIntervalInMs" : 100,
   "NumOfParallelQueueReaders" : 100,
   "TrackLastEnqueuedEventProperties" : false,
   "CacheEventCount" : 100,
   "PrefetchCount" : 300,
   "BatchSizeForCheckpoint" : 50,
   "CheckpointTimeoutSeconds" : 60,
   "EventHubTransportType" : "AmqpTcp",
   "DeviceIdSystemPropertyName" : "iothub-connection-device-id"
}
```

## REST URLs

| Relative URL | HTTP verb | Action |
| ------------ | --------- | ------ |
| api/v1/configuration/_ComponentId_/ClientSettings  | GET | Retrieves the Azure Event Hubs client settings configuration |
| api/v1/configuration/_ComponentId_/ClientSettings  | PUT | Configures or updates the Azure Event Hubs client settings  configuration |
| api/v1/configuration/_ComponentId_/ClientSettings | DELETE | Deletes the Azure Event Hubs client settings  configuration |
| api/v1/configuration/_ComponentId_/ClientSettings | PATCH | Allows partial updating of configured client settings fields. |

**Note:** Replace _ComponentId_ with the Id of your Azure Event Hubs component, for example AzureEventHubs1.
