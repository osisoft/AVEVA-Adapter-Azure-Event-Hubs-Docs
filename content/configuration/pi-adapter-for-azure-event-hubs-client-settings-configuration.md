---
uid: PIAdapterForAzureEventHubsClientSettingsConfiguration
---

# Client settings

The client settings configuration is automatically generated when you add a new data source. If you experience problems with timeouts or when Azure Event Hubs limits are exceeded in terms of browse or subscription operation, you can change the client settings configuration.

## Configure client settings

Complete the following steps to configure Azure Event Hubs client settings. Use the `PUT` method in conjunction with the `api/v1/configuration/<ComponentId>/ClientSettings` REST endpoint to initialize the configuration.

1. Using a text editor, create an empty text file.

2. Copy and paste an example configuration for Azure Event Hubs client settings into the file.

    For sample JSON, see [Client settings example](#client-settings-example).

3. Update the example JSON parameters for your environment.

    For a table of all available parameters, see [Client settings parameters](#client-settings-parameters).

4. Save the file. For example, as `ConfigureClientSettings.json`.

5. Open a command line session. Change the directory to the location of `ConfigureClientSettings.json`.

6. Enter the following cURL command (which uses the `PUT` method) to initialize the client settings configuration.

    ```bash
    curl -d "@ConfigureClientSettings.json" -H "Content-Type: application/json" -X PUT "http://localhost:5590/api/v1/configuration/AzureEventHubs1/ClientSettings"
    ```

    **Notes:**
  
    * If you installed the adapter to listen on a non-default port, update `5590` to the port number you used.
    * If you use a component ID other than `AzureEventHubs1`, update the endpoint with your chosen component ID.
    * For a list of other REST operations you can perform, like updating or deleting a client settings configuration, see [REST URLs](#rest-urls).
    <br/>
    <br/>

## Client settings schema

The full schema definition for the Azure Event Hubs client settings configuration is in the `EventHubs_ClientSettings_schema.json` file located in one of the following folders:

* Windows: `%ProgramFiles%\OSIsoft\Adapters\EventHubs\Schemas`
* Linux: `/opt/OSIsoft/Adapters/EventHubs/Schemas`

## Client settings parameters

The following parameters are available for configuring Azure Event Hubs client settings:

| Parameter                | Required | Type       | Description |
|--------------------------|----------|------------|-------------|
| **MaxInternalQueueSize** | Optional | `integer`  |  Specifies maximum number of value updates that can be held by the adapter in memory<br><br>Allowed value: > `1000`<br>Default value: `500000`           |
| **InternalQueuePollingIntervalInMs** | Optional | `string`<br>(time-span) | Specified interval at which data is removed from internal queue <br><br>Allowed value: Between `1` and `60000` milliseconds<br>Default value: `0:00:00.05` |
| **TrackLastEnqueuedEventProperties** | Optional | `boolean` | Indicates if the user should request information on the last enqueued event on the partition associated with a given event and track that  information as events are received <br><br>Allowed value: `true` or `false` <br>Default value: `false`|
| **CacheEventCount** | Optional | `integer` | The maximum amount of events read from the Event Hubs service and held in a local memory cache when reading is active and events are emitted to an enumerator for processing<br><br>Default value: `100` |
|**PrefetchCount** | Optional | `integer` | The number of events requested from the Event Hubs service and staged locally regardless of whether a reader is active. **PrefetchCount** is intended to maximize throughput by buffering service operations. <br><br>Allowed value: Must be greater than `2` times the **CacheEventCount**.<br>Default value: `300`|
| **BatchSizeForCheckpoint** | Optional | `integer`| The number of events processed to trigger a checkpoint operation<br><br>Default value: `500` |
| **CheckpointingTimeoutSeconds** | Optional | `integer`| The timeout in seconds for the checkpoint operation<br><br>Default value: `60` |
| **DeviceIdSystemPropertyName** | Optional | `string` | The name of the system property for the device id.<br><br>Default value: `iothub-connection-device-id` |
| **EventHubTransportType** | Optional | `enum` | Identifies the protocol used internally by the client<br><br>Allowed values: `AmqpTcp` and `AmqpWebSockets`<br>Default value: `AmqpTcp`|
| **EventHubLoadBalancingStrategy** | Optional | `enum` | The load balancing strategy used by the internal Event Hub client used by the adapter. For more information, see Microsoft's [LoadBalancingStrategy Enum](https://docs.microsoft.com/en-us/dotnet/api/azure.messaging.eventhubs.processor.loadbalancingstrategy?view=azure-dotnet).<br><br>**Note:** This setting is irrelevant when you use the recommended Event Hub configuration (single partition).<br><br>Allowed values: `Balanced` or `Greedy`<br>Default value: `Greedy` |
| **EventProcessorClientMaximumRetries** | Optional | `integer` | The maximum amount of retries that the EventProcessorClient makes in case of client failures <br><br>Default value: `5` |
| **EventProcessorClientMaximumDelayInMin** | Optional |`integer` | The maximum delay for the timeout operation in minutes<br><br>Default value: `5`|

## Client settings example

```json
{
   "MaxInternalQueueSize" : 500000,
   "InternalQueuePollingIntervalInMs" : "0:00:00.05",
   "TrackLastEnqueuedEventProperties" : false,
   "CacheEventCount" : 100,
   "PrefetchCount" : 300,
   "BatchSizeForCheckpoint" : 500,
   "CheckpointingTimeoutSeconds" : 60,
   "DeviceIdSystemPropertyName" : "iothub-connection-device-id",
   "EventHubTransportType" : "AmqpTcp",
   "EventHubLoadBalancingStrategy": "Greedy",
   "EventProcessorClientMaximumRetries" : 5,
   "EventProcessorClientMaximumDelayInMin" : 5 
}
```

## REST URLs

| Relative URL | HTTP verb | Action |
| ------------ | --------- | ------ |
| api/v1/configuration/_ComponentId_/ClientSettings  | GET | Retrieves the Azure Event Hubs client settings configuration |
| api/v1/configuration/_ComponentId_/ClientSettings  | PUT | Configures or updates the Azure Event Hubs client settings configuration |
| api/v1/configuration/_ComponentId_/ClientSettings | DELETE | Deletes the Azure Event Hubs client settings configuration |
| api/v1/configuration/_ComponentId_/ClientSettings | PATCH | Allows partial updating of configured client settings fields |

**Note:** Replace _ComponentId_ with the Id of your Azure Event Hubs component, for example AzureEventHubs1.
