---
uid: PIAdapterForAzureEventHubsPerformanceBestPractices
---

# Performance best practices

The performance of an adapter, PI Adapter for Azure Event Hubs, specifically, depends upon a number of factors, like egress limits, data shape, and data selections. Use the following performance guidelines and best practices when you set up an adapter.

**Note:** A many-to-one relationship exists between JSON messages sent to Event Hub and time indexed events sent to the data endpoints. For more information, see [Throughput units](#throughput-units).

## Data shape

PI Adapter for Azure Event Hubs assumes a single schema per source Event Hub. When a data selection is assigned a particular Event Hub, it is assumed that all messages received from that Event Hub should be processed for the `IndexField` and `ValueField`.

OSIsoft recommends using larger messages rather than smaller messages for the same amount of data to achieve optimal performance.

**Example:** 5000 stream values per message at a 250 ms update rate perform better than 100 streams per message at a 5 ms update rate.

OSIsoft also recommends that you use flat data rather than deeply nested data as they are not as expensive to parse. More complex messages may also require more expensive JSONPath expressions to identify values and timestamps, which results in lower performance.

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

Data selection related to the Event Hubs and the configuration of the `ValueField` and `IndexField` parameters highly affect performance of the adapter.

### Event Hub

#### Region

An Event Hub namespace in the same geographic region as the adapter ensures minimal latency due to network communications.

#### Partitions

The ADH SDS service and PI Data Archive can both store sequential data. Out of order data is accepted; however, OSIsoft recommends to order your data for optimal performance.

OSIsoft further recommends that you use a single partition to preserve message order even though Azure Event Hubs support multiple partitions for a single Event Hub for parallelism downstream.

#### Throughput units

A single throughput unit for Azure Event Hubs allows for ingress of up to 1MB per second or 1000 events (JSON messages). Each message contains as many individual data endpoint events as are configured in the data selections for that Event Hub.

**Example:** 100 data selections that use Event Hub A and 10 events that are sent to the Event Hub every second results in 1000 events per second sent to the data endpoint.

Consider this many-to-one relationship between the events sent to Event Hub and events sent to the data endpoint when you select the appropriate throughput units for your Event Hub.

### ValueField and IndexField JSONPath

OSIsoft recommends that you use the most direct reference possible to refer to a data item when you configure data selections. Evaluating JSONPath expressions can be expensive.

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

The following data selections retrieve the same value; however, note the differences in both `ValueField` values.

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
    "IndexField": "$.TimeStamp",
    "IndexFormat": null,
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
    "IndexField": "$.TimeStamp",
    "IndexFormat": null,
    "DataType": "string"
}
```

