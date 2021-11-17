## Overview

As a new type of cloud integration service, [Tencent Cloud Enterprise Integration Service (EIS)](https://cloud.tencent.com/product/eis) connects different systems or businesses in and outside enterprises to the same platform and implements various features such as resource integration, data orchestration, and business connection between systems by reusing best practices and quickly building system integration models, which meet enterprises' requirements for a lightweight, all-around, and flexible integrated system.

Currently, EIS has been fully connected to EventBridge. You can configure a SaaS connector to receive and consume the events of third-party SaaS services from EIS for linkage between cloud events and SaaS businesses. This document describes how to create a SaaS connector and the SaaS connector data structure.


## Prerequisites

You have [created an event bus](https://intl.cloud.tencent.com/document/product/1108/42285).



## Directions

### Creating event bus and connector
1. Log in to the [EventBridge console](https://console.cloud.tencent.com/eb/) and select **Event Bus** on the left sidebar.
2. In the **Event Bus** list, select the event bus for which you want to configure a SaaS connector.
3. Click **Add** in the connector configuration section on the **Event Bus Details** page 
4. Here, select **SaaS** for **Connector Type** 
5. Enter the [EIS console](https://console.cloud.tencent.com/eis/project).
<dx-alert infotype="notice" title="">
If you use a sub-account, you need to have the admin permissions to perform more operations. Please configure the permissions in **Member Management** in the **EIS console**.
</dx-alert>
6. On the integration project list page, click a project name to enter the project details page.
7. On the **Application Management** tab, select **Add Application** or **Import Application** 
8. On the **Application Management** list page, click an application name to enter the application details page.
9. Select the corresponding flow to enter the flow details page 
10. On the flow details page, click **Create Connector** and select **EventBridge** > **Event Delivery**.
11. Set the default and connector configurations as prompted and click **Save**.
<dx-tabs>
::: Default configuration
In **Edit Connector Configuration**, enter the configuration information.
:::
::: Connector configuration
In **Edit Connector Configuration**, enter the configuration information.
- **Event Bus ID**: enter your delivery event bus.
- **Event List**: select the message content to be sent to the specified event bus.
:::
</dx-tabs>
12. Click **Publish**.

### Creating event rule
1. Log in to the [EventBridge console](https://console.cloud.tencent.com/eb/) and select **Event Rule** on the left sidebar.
2. On the **Event Rule** page, select a region and event bus and click **Create Event Rule**.
3. Enter the relevant information as prompted 
Here, select **SaaS event delivery** for **Tencent Cloud Service Type** and configure the event target.
4. Click **OK** to complete connector creation and match rule settings. Then, all SaaS events from EIS can be processed and consumed through EventBridge.

     


#### SaaS connector data structure description

```json
{      
    "specversion": "0",      
    "id": "13a3f42d-7258-4ada-da6d-023a333b4662",  
    "type": "adapter:eis",  
    "source": "eis.cloud.tencent",
    "subjuect":"qcs::eis:${region}:uin/${uin}:application/${projectId}/${applicationId}",  
    "time": "1615430559146",  
    "region": "ap-guangzhou",  
    "datacontenttype": "application/json;charset=utf-8",  
    "resource": [    "qcs::eb:ap-guangzhou:uid1250000000:eventbusid/eventruleid"  ],  
    "data": {
          "payload": "test_value" 
           } 
}
```

Some parameters in `data` are completely subject to the event content delivered by EIS. You can specify the content to be delivered in the `data` field based on your actual business needs.
