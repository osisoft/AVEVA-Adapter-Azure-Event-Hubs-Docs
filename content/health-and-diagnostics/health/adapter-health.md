---
uid: PIAdapterForAzureEventHubsHealth
---

# Health

AVEVA Adapters produce different kinds of health data that can be egressed to different health endpoints.

## Available health data

The adapter sends dynamic data to configured health endpoints every minute.

The following health data is available:

- [PI Adapter for Azure Event Hubs device status](xref:PIAdapterForAzureEventHubsDeviceStatus)
- [Next Health Message Expected](xref:NextHealthMessageExpected)

## AF structure

With a health endpoint configured to a PI server, you can use PI System Explorer to view the health of a given adapter. The element hierarchy is shown in the following image.

![Health data](../../main/shared-content/images/health-data.png)
