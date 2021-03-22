---
uid: AdapterHealth1-3
---

# Adapter health

PI Adapters produce different kinds of health data that can be egressed to different health endpoints.

## Available health data

Dynamic data is sent every minute to configured health endpoints. <!--- jokim Mar0322: passive to active voice. who does the sending? --->

The following health data is available:

- [PI Adapter for Azure Event Hubs device status](xref:PIAdapterForAzureEventHubsDeviceStatus)
- [Next Health Message Expected](xref:NextHealthMessageExpected1-3)

## AF structure

With a health endpoint configured to a PI server, you can use PI System Explorer to view the health of a given adapter. The element hierarchy is shown in the following image.

![Health data](../../main/v1.3/images/health-data.png)
