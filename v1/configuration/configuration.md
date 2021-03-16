---
uid: AzureEventHubsConfiguration
---

# Configuration

PI Adapter for Azure Event Hubs provides configuration of data source and data selection.

The examples in the configuration topics use `curl`, a commonly available tool on both Windows and Linux. You can configure the adapter with any programming language or tool that supports making REST calls or with the EdgeCmd utility. For more information, see the [EdgeCmd utility documentation](https://osisoft.github.io/Edgecmd-Docs/V1.2/edgecmd-utility.html). To validate successful configurations, you can perform data retrieval (`GET` commands) with a browser, if available, on your device.

For more information on PI Adapter configuration tools, see [Configuration tools](xref:ConfigurationTools).

## Quick start

Complete the following steps to establish a data flow from a Azure Event Hubs data source device to a data endpoint.

1. Configure one or several Azure Event Hubs system components.<br>See [System components configuration](xref:SystemComponentsConfiguration1-3#configure-system-components).

2. Configure a Azure Event Hubs data source for each Azure Event Hubs device.<br>See [PI Adapter for Azure Event Hubs data source configuration](xref:PIAdapterForAzureEventHubsDataSourceConfiguration#configure-azure-event-hubs-data-source).

3. Configure a Azure Event Hubs data selection for each Azure Event Hubs data source.<br>See [PI Adapter for Azure Event Hubs data selection configuration](xref:PIAdapterForAzureEventHubsDataSelectionConfiguration#configure-azure-event-hubs-data-selection).

4. Configure one or several egress endpoints.<br>See [Egress endpoints configuration](xref:EgressEndpointsConfiguration).
