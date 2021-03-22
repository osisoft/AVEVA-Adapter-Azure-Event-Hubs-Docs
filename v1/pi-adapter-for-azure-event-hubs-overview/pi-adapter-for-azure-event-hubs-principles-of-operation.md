---
uid: PIAdapterForAzureEventHubsPrinciplesOfOperation
---

# PI Adapter for Azure Event Hubs principles of operation

This adapter's operations focus on data collection and stream creation.

## Adapter configuration

For the Azure Event Hubs adapter to start data collection, configure the following: <!--- jokim Mar0322: configure the following items --->

- Data source: Provide the data source from which the adapter should collect data. <!--- jokim Mar0322: remove periods in a bulleted list --->
- Data selection: Select Azure Event Hubs items to which the adapter should subscribe for data.
- Logging: Set up the logging attributes to manage the adapter logging behavior.

For more details, see [PI Adapter for Azure Event Hubs data source configuration](xref:PIAdapterForAzureEventHubsDataSourceConfiguration) and [PI Adapter for Azure Event Hubs data selection configuration](xref:PIAdapterForAzureEventHubsDataSelectionConfiguration).

## Connection

The adapter communicates with the Azure Event Hubs platform using the [AMQP (Advanced Message Queueing Protocol)](https://www.amqp.org/about/what). Alternatively, the adapter can connect using AMQP over WebSockets using HTTPS protocol with corresponding adapter configuration. A Shared Access Signature (SAS) is required for the adapter to authenticate with the Azure Event Hub namespace, which is supplied by a valid connection string in the adapter's data source configuration.

For more information, see [PI Adapter for Azure Event Hubs data source configuration](xref:PIAdapterForAzureEventHubsDataSourceConfiguration).

## Data collection

After data source and data selection items are configured, the adapter establishes a connection to each event hub within the event hub namespace for all event hubs specified in data selection items. Once a connection is established, the adapter begins consuming events from the event hubs and processes the events as soon as they are published by an event producer and become available to consumers.

For more information see [PI Adapter for Azure Event Hubs data selection configuration](xref:PIAdapterForAzureEventHubsDataSelectionConfiguration).

### Data types

The following table lists Azure Event Hubs variable types that the adapter collects data from and types of streams that will be created.<!--- jokim Mar0322: ...and types of streams created... --->

| Event Hubs data type | Stream data type |
|------------------|------------------|
| Boolean          | Boolean          |
| Int16            | Int16            |
| UInt16           | UInt16           |
| Int32            | Int32            |
| UInt32           | UInt32           |
| Int64            | Int64            |
| UInt64           | UInt64           |
| Float            | Float32          |
| Double           | Float64          |
| DateTime         | DateTime         |
| String           | String           |

## Stream creation

The Azure Event Hubs adapter creates a stream value with two properties for each selected Azure Event Hubs item. The properties are described in the following table.

| Property name | Data type | Description |
|---------------|-----------|-------------|
| `Timestamp`   | String    | The response time of the stream data from the Azure Event Hubs device |
| `Value`       | Specified by the data selection | The value of the stream data from the Azure Event Hubs device |

Certain metadata are sent with each stream created. <!--- jokim Mar0322: passive->active voice pls --->The following metadata are common for every adapter type:

- **ComponentId**: Specifies the data source, for example, _EventHubs1_
- **ComponentType**: Specifies the type of adapter, for example, _EventHubs_

Metadata specific to the Azure Event Hubs adapter are: <!--- jokim Mar0322: ...are as follows: --->

- **EventHubName**: Contains the Azure Event Hub name configured in the data selection item.
- **DeviceId**: Contains the Device Id configured in the data selection item (IoT Hub integration only).

**Note:** A configured metadata level allows you to set the amount of metadata for the adapter. Specify the metadata level in [General configuration](xref:GeneralConfiguration). For the Azure Event Hubs adapter, the following metadata is sent for the individual level: <!--- jokim Mar0322: "Azure Event Hubs send the following metadata for the individual level"? --->

- `None`: No metadata
- `Low`: AdapterType (ComponentType) and DataSource (ComponentId)
- `Medium`: AdapterType (ComponentType), DataSource (ComponentId), EventHubName, and DeviceId

Each stream created for the selected measurement has a unique identifier (stream ID). If you specify a custom stream ID for the measurement in the data selection configuration, the adapter uses that stream ID to create the stream. Otherwise, the adapter constructs the stream ID using the following format:

```code
<Id>.<ValueField>
```

**Note:** Naming convention is affected by `StreamIdPrefix` and `DefaultStreamIdPattern` settings in the data source configuration. For more information, see [PI Adapter for Azure Event Hubs data source configuration](xref:PIAdapterForAzureEventHubsDataSourceConfiguration).
