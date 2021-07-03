---
uid: PIAdapterAzureEventHubsDataSourceDiscover
---

# Azure Event Hubs data source discovery

When running a discovery against an Azure Event Hub namespace defined within your [Data source configuration](xref:PIAdapterForAzureEventHubsDataSourceConfiguration), you can specify query parameters to narrows the scope of the discovery, targeting specific event hubs within the namespace. When the discovery completes, you can add the discovered items to the data selection.

## Azure Event Hubs query string

Azure Event Hubs query strings must includes one or more `EventHubName`, along with a `WaitTime` that specifies how long the query runs.

```text
EventHubNames=<EVENT_HUB_1>,<EVENT_HUB_2>;WaitTime=<DAYS>.<HOURS>:<MINUTES>:<SECONDS>
```

Within the discovery request JSON payload, enter the Azure Event Hubs query using the `query` parameter, as shown in the [query examples](#query-examples) below. For more information on using the query parameter during API requests to the `api/v1/configuration/<componentId>/discoveries` endpoint, see <xref:DiscoveryConfiguration>.


## Query parameters

When including a query within your discovery, you can provide the parameters in the table that follows. Separate the `EventHubNames` and `WaitTime` parameters with a semicolon (`;`).

String item | Required | Description
--|--|--
`EventHubNames` | Required | Specifies one or more event hub as query targets during discovery. Discovery looks for the specified event hubs within the namespace set in the [Data source configuration](xref:PIAdapterForAzureEventHubsDataSourceConfiguration) using the `EventHubNamespaceConnectionString` parmeter.<br><br>&bull; When querying for more than one event hub, seperate each event hub with a comma (`,`).<br>&bull; The maximum number of event hubs that you can query is **ten**, as Microsoft Azure limits each namespace to ten event hubs.
`WaitTime` | Optional | Specifies the duration of the discovery. If you omit the `WaitTime` parameter, discovery defaults to one minute: `0.00:01:00`.<br><br>&bull; **Minimum value:** 30 seconds (`0.00:00:30`)<br>&bull; **Maximum value:** 7 days (`7.00:00:00`). This maximum is limited by Azure Event Hubs, as it retains messages for seven days.<br><br>**Note:** Discoveries with `WaitTimes` outside of the minimum and maximum values are considered invalid and will fail with the following message:<br><br>`Discovery operation failed: Exception type: ArgumentException. Message: Wait Time must be between 30 seconds and 7 days`. 

## Query examples

The following section contain several examples of Azure Event Hub queries. When creating a discovery request, include the Azure Event Hub query within the [request payload](xref:DiscoveryConfiguration#)

### [Example 1: Single event hub](#tab/example-1)

This Azure Event Hubs query example discovers a single event hub.

```json
{
    "query": "EventHubNames=event-hub-1;WaitTime=0.00:00:30"
}
```

### [Example 2: Multiple event hubs](#tab/example-2)

This Azure Event Hubs query example discovers multiple event hubs.

```json
{
    "query": "EventHubNames=event-hub-1,event-hub-2;WaitTime=0.00:00:30"
}
```

### [Example 3: No WaitTime](#tab/example-3)

This Azure Event Hubs query example discovers multiple event hubs, but omits the `WaitTime` parameter. Without a specified `WaitTime`, the discovery defaults to a `WaitTime` of one minute.

```json
{
    "query": "EventHubNames=event-hub-1,event-hub-2"
}
```

***

## Query results

After your submit a discovery request and the discovery completes, you can view its results and use them to create a [Data selection configuration](xref:PIAdapterForAzureEventHubsDataSelectionConfiguration). The discovery results includes a data selection configuration for each stream it finds for an event hub. For example, the following discovery results include a configuration for two streams found for `"eventHubName":"event-hub-1"`: `"streamId": "event-hub-1.$.PumpTemperature"` and `"streamId": "event-hub-1.$.TimeStamp"`.

```json
[
    {​​​
        "eventHubName": "event-hub-1",
        "deviceId": null,
        "valueField": "$.PumpTemperature",
        "timeField": null,
        "timeFormat": null,
        "dataType": "Single",
        "selected": false,
        "name": null,
        "streamId": "event-hub-1.$.PumpTemperature",
        "dataFilterId": null
    }​​​,
    {​​​
        "eventHubName": "event-hub-1",
        "deviceId": null,
        "valueField": "$.TimeStamp",
        "timeField": null,
        "timeFormat": null,
        "dataType": "DateTime",
        "selected": false,
        "name": null,
        "streamId": "event-hub-1.$.TimeStamp",
        "dataFilterId": null
    }​​​
]
```

### Combining query results into a valid data selection configuration 

After viewing the results of a discovery, you can manually combine them into a single valid data selection configuration. In the example below, the two data selection configurations above are combined into single configuration. Notice that `timeField` has been updated to `$.TimeStamp`.

After creating a valid data selection configuration, you can upload it by performing a `PUT` against the `api/v1/configuration/<ComponentId>/DataSelection` endpoint. For more information, see <xref:PIAdapterForAzureEventHubsDataSelectionConfiguration>.


```json
[
    {
        "eventHubName": "event-hub-1",
        "deviceId": null,
        "valueField": "$.PumpTemperature",
        "timeField": "$.TimeStamp",
        "timeFormat": null,
        "dataType": "Single",
        "selected": true,
        "name": null,
        "streamId": "event-hub-1.$.PumpTemperature",
        "dataFilterId": null
    }
]
```

### Additional considerations for `query` and `autoselect`

When you use the `query` parameter within a discovery request, OSIsoft recommends setting the [autoSelect](xref:DiscoveryConfiguration#) parameter to `false` for most use cases. OSIsoft makes this recomendation because the data selection configuration that discovery returns is not suitable for a production environment without manually editing its settings, most notably the `TimeField` setting. `"autoSelect" = true` should only be used for data sources with simple data structures, as it automatically applies the discovery results as the active [Data selection configuration](xref:PIAdapterForAzureEventHubsDataSelectionConfiguration).
