---
uid: PIAdapterForAzureEventHubsDeviceStatus
---

# PI Adapter for Azure Event Hubs device status

The PI Adapter for Azure Event Hubs device status indicates the health of the Azure Event Hubs component and if it is currently communicating properly with the data source. This time-series data is stored within a PI point or OCS stream, depending on the endpoint type. During healthy steady-state operation, a value of `Good` is expected.

| Property                          | Type                                 | Description                    |
|-----------------------------------|--------------------------------------|--------------------------------|
| **Time**                        | `string`                               | Timestamp of the event        |
| **DeviceStatus**                | `string`                               | The value of the `DeviceStatus` |

The adapter supports the following statuses:

| Status            | Meaning                                                                                       |
|-------------------|-----------------------------------------------------------------------------------------------|
| `Starting`        | The component is starting up and is not yet connected to the data source.                     |
| `ConnectedNoData` | Connectivity to Event Hubs is confirmed but no events have been received yet                  |
| `Good`            | Connectivity to Event Hubs is confirmed and event was received                                |
| `DeviceInError`   | The adapter failed to connect to Azure Event Hubs, or the connection was interrupted          |
| `Shutdown`        | Connectivity to Event Hubs is being closed                                                    |
| `NotConfigured`   | The adapter configuration does not have any data selection items defined with Event Hub names |

For more information on health data supported by the adapter, see [Adapter health](xref:AdapterHealth1-3).