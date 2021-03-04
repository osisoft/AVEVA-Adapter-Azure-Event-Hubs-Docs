---
uid: PIAdapterForAzureEventHubsPerformanceBestPractices
---

# PI Adapter for Azure Event Hubs performance best practices

The performance of an adapter, and PI Adapter for Azure Event Hubs specifically, is dependent upon a number of factors, such as egress limits, data shape, and data selections. Use the following performance guidelines and best practices when setting up an adapter.

## Egress limits

On a virtual machine with 4 GB RAM and 2 vCPUs, a PI Adapter for Azure Event Hubs is capable of sending up to 20,000 events per second to an OCS namespace or PI Web API OMF endpoint.

**Note:** A many-to-one relationship exists between JSON messages sent to Event Hub and time indexed events sent to the data endpoints. For more information, see [Throughput units](#throughput-units).

## Data shape

PI Adapter for Azure Event Hubs assumes a single schema per source Event Hub. When a data selection is assigned a particular Event Hub, it is assumed that all messages received from that Event Hub should be processed for the TimeField and ValueField.

OSIsoft recommends to use larger messages rather than smaller messages for the same amount of data to achieve optimal performance.<br>**Example:** 5000 stream values per message at a 250 ms update rate perform better than 100 streams per message at a 5 ms update rate.

OSIsoft further recommends to use flat data rather than deeply nested data, as they are not as expensive to parse. More complex messages may also require more expensive JSONPath expressions to identify values and timestamps, resulting in lower performance.

### Flat data

```json
{
  "Timestamp": "2020-01-01T00:00:00Z",
  "Events": [
    {
      "Id": "1",
      "Value": 0
    },
    {
      "Id": "2",
      "Value": 0
    }
  ]
}
```

### Nested data

```json
{
    "Timestamp": "2020-01-01T00:00:00Z",
    "L1": {
        "L2": {
            "L3": {
                "L4": [
                  {
                    "Id": "1",
                    "Value": 0
                  },
                  {
                    "Id": "2",
                    "Value": 0
                  }
                ]
            }
        }
    }
}
```

## Data selections

Data selection related to the Event Hubs themselves and the configuration of the ValueField and TimeField parameters highly affect performance of the adapter.

### Event Hub

#### Region

An Event Hub namespace in the same geographic region as the adapter ensures minimal latency due to network communications.

#### Partitions

The OCS SDS service and PI Data Archive can both store sequential data. Out of order data is accepted. However, OSIsoft recommends to order data for optimal performance.

OSIsoft further recommends to use a single partition to preserve messages order even though Azure Event Hubs support multiple partitions for a single Event Hub for parallelism downstream.

#### Throughput units

A single throughput unit for Azure Event Hubs allows for ingress of up to 1MB per second or 1000 events (JSON messages). Each message contains as many individual data endpoint events as are configured in the data selections for that Event Hub.

**Example:** 100 data selections that use Event Hub A and 10 events that are sent to the Event Hub every second results in 1000 events per second sent to the data endpoint.<br>Consider this many-to-one relationship between the events sent to Event Hub and events sent to the data endpoint, when selecting the appropriate throughput units for your Event Hub.

### ValueField and TimeField JSONPath

OSIsoft recommends to use the most direct reference possible to refer to a data item when configuring data selections. Evaluating JSONPath expressions can be expensive.

#### Sample data

```json
{
  "Timestamp": "2020-01-01T00:00:00Z",
  "Events": [
    {
      "Id": "1",
      "Value": 0
    },
    {
      "Id": "2",
      "Value": 0
    }
  ]
}
```

The following data selections retrieve the same value. However, note the differences in both **ValueField** values.

#### Poor performance

This example has a query `$.Events[?(@.Id == "1")].Value` of the events collection.

```json
{
    "Selected": true,
    "Name": null,
    "StreamId": "EventHubs_1",
    "DataFilterId": null,
    "EventHubName": "hub",
    "DeviceId": null,
    "ValueField": "$.Events[?(@.Id == \u00271\u0027)].Value",
    "TimeField": "$.TimeStamp",
    "TimeFormat": null,
    "DataType": "string"
}
```

#### High performance

This example uses a direct reference `$.Events[1].Value` to the index.

```json
{
    "Selected": true,
    "Name": null,
    "StreamId": "EventHubs_1",
    "DataFilterId": null,
    "EventHubName": "hub",
    "DeviceId": null,
    "ValueField": "$.Events[1].Value",
    "TimeField": "$.TimeStamp",
    "TimeFormat": null,
    "DataType": "string"
}
```

### Limitations

As documented in the Known Issues section of the [Release Notes](xref:ReleaseNotes), attempting to configure 10,000 or more streams can result in a timeout.