---
uid: AzureEventHubsConfiguration
---

# Configuration

PI Adapter for Azure Event Hubs provides configuration of data source and data selection.

The examples in the configuration topics use `curl`, a commonly available tool on both Windows and Linux. You can configure the adapter with any programming language or tool that supports making REST calls or with the EdgeCmd utility. For more information, see the [EdgeCmd utility documentation](https://osisoft.github.io/Edgecmd-Docs/content/edgecmd-utility.html). To validate successful configurations, you can perform data retrieval (`GET` commands) with a browser, if available, on your device.

For more information on PI Adapter configuration tools, see [Configuration tools](xref:ConfigurationTools).

## Quick start

This Quick Start guides you through setup of each configuration file available for PI Adapter for Azure Event Hubs. As you complete each step, perform each required configuration to establish a data flow from a data source to one or more endpoints. Some configurations are optional.

**Important:** If you want to complete the optional configurations, complete those tasks before the required tasks.

1. Configure one or more Azure Event Hubs system components.

    See <xref:SystemComponentsConfiguration>.

2. Configure an Azure Event Hubs data source for each Azure Event Hubs device.

    See <xref:PIAdapterForAzureEventHubsDataSourceConfiguration>.

3. **Optional**: Configure client settings.

    See <xref:PIAdapterForAzureEventHubsClientSettingsConfiguration>.

4. Configure an Azure Event Hubs data selection for each Azure Event Hubs data source.

    See <xref:PIAdapterForAzureEventHubsDataSelectionConfiguration>.

5. **Optional**: Configure data filters and if there is a proxy between the adapter and your egress endpoints, define it.

    See the following topics:

    - <xref:DataFiltersConfiguration>
    - <xref:ConfigureANetworkProxy>

6. Configure one or more egress endpoints.

    See <xref:EgressEndpointsConfiguration>.

7. **Optional**: Configure health endpoints, general (diagnostics and metadata), buffering, and logging. See the following topics:

    - <xref:HealthEndpointConfiguration>
    - <xref:GeneralConfiguration>
    - <xref:BufferingConfiguration>
    - <xref:LoggingConfiguration>
