---
uid: PIAdapterForAzureEventHubsConfigurationExamples
---

# Configuration examples

The following tables provide examples for all configurations available for PI Adapter for Azure Event Hubs.

**Note:** The examples in this topic are using the default port number `5590`. If you selected a different port number, replace it with that value.

## System components configuration

The following JSON is an example of a system components configuration. It contains two instances of the Azure Event Hubs adapter.

```json
[
    {
        "ComponentId": "EventHubs1",
        "ComponentType": "EventHubs"
    },
    {
        "ComponentId": "EventHubs2",
        "ComponentType": "EventHubs"
    },
    {
        "ComponentId": "OmfEgress",
        "ComponentType": "OmfEgress"
    }
]
```

## Adapter configuration

```json
{
    "AzureEventHubs1": {
        "Logging": {
            "logLevel": "Information",
            "logFileSizeLimitBytes": 34636833,
            "logFileCountLimit": 31
        },
        "DataSource": {
            "StreamIdPrefix": "EventHubs1.",
            "DefaultStreamIdPattern": "{EventHubName}.{ValueField}",
            "EventHubNamespaceConnectionString": "<Azure Event Hub Namespace connection string>",
            "BlobStorageConnectionString": "<Azure Storage Account connection string>",
            "ConsumerGroupName": "$Default",
            "CheckpointBlobContainerName": "<checkpoint container>",
            "TimeZone": "America/Los_Angeles"
        },
        "DataSelection": [
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
    },
    "System": {
        "Logging": {
            "logLevel": "Information",
            "logFileSizeLimitBytes": 34636833,
            "logFileCountLimit": 31
        },
        "HealthEndpoints": [
        ],
    "Diagnostics": {
            "enableDiagnostics": true
    },
        "Components": [
            {
                "componentId": "Egress",
                "componentType": "OmfEgress"
            },
            {
                "componentId": "AzureEventHubs1",
                "componentType": "AzureEventHubs"
            }
        ],
    "Buffering": {
            "BufferLocation": "C:/ProgramData/OSIsoft/Adapters/AzureEventHubs/Buffers",
            "MaxBufferSizeMB": -1,
            "EnableBuffering": true
        }
     },
    "OmfEgress": {
        "Logging": {
            "logLevel": "Information",
            "logFileSizeLimitBytes": 34636833,
            "logFileCountLimit": 31
        },
        "DataEndpoints": [
            {
                "id": "WebAPI EndPoint",
                "endpoint": "https://PIWEBAPIServer/piwebapi/omf",
                "userName": "USERNAME",
                "password": "PASSWORD"
            },
            {
                "id": "ADH Endpoint",
                "endpoint": "https://ADHEndpoint/omf",
                "clientId": "CLIENTID",
                "clientSecret": "CLIENTSECRET"
            }
        ]
    }
}
```

## Data source configuration

The following are representations of minimal and complete data source configurations of Azure Event Hubs adapter.

### Minimal data source configuration

```json
{
  "EventHubNamespaceConnectionString": "<Azure Event Hub Namespace connection string>",
  "BlobStorageConnectionString": "<Azure Storage Account connection string>",
  "ConsumerGroupName": "$Default",
  "CheckpointBlobContainerName": "<checkpoint container>"
}
```

### Complete data source configuration

```json
{
  "StreamIdPrefix": "EventHubs1.",
  "DefaultStreamIdPattern": "{EventHubName}.{ValueField}",
  "EventHubNamespaceConnectionString": "<Azure Event Hub Namespace connection string>",
  "BlobStorageConnectionString": "<Azure Storage Account connection string>",
  "ConsumerGroupName": "$Default",
  "CheckpointBlobContainerName": "<checkpoint container>",
  "TimeZone": "America/Los_Angeles"
}
```

## Client settings configuration

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

## Data selection configuration

The following are representations of minimal and complete data selection configurations of Azure Event Hubs adapter.

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
