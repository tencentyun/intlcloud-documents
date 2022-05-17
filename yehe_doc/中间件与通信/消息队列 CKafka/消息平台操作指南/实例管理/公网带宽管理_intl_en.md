## Overview

CKafka transfers data over the private network by default. To access over the public network, you need to activate a public network route separately. For detailed directions, see [Adding Routing Policy](https://intl.cloud.tencent.com/document/product/597/32555). Currently, public network bandwidth of 3 Mbps is provided free of charge by default.

CKafka Pro Edition supports increasing the public network bandwidth for a fee. For the specific prices, see [Billing Overview](https://intl.cloud.tencent.com/document/product/597/11745).


This document describes how to upgrade, adjust, and delete the public network bandwidth in the CKafka console.

## Directions

CKafka adjusted the purchase entry and mode of public network bandwidth on January 7, 2022. After then, new users can purchase a public network bandwidth during instance purchase, and existing instances continue to be billed by the hourly bandwidth, which can be upgraded.

You can click the following tags to view the purchase methods and relevant operations for old and new instances.

<dx-tabs>

::: Public network bandwidth management (new)

### Purchasing public network bandwidth
1. Log in to the [CKafka console](https://console.cloud.tencent.com/ckafka).
2. Click **Instance List** on the left sidebar and click **Create** to enter the purchase page.
3. On the purchase page, set the instance information and select the public network bandwidth based on your actual needs.
   - Billing Mode: **monthly bandwidth** and **hourly bandwidth** are supported. Currently, you cannot switch the billing mode of the public network bandwidth. For billing details, see [Billing Overview](https://intl.cloud.tencent.com/document/product/597/11745#prices).
   - Bandwidth Size: Select the desired public network bandwidth size. CKafka provides 3 Mbps public network bandwidth free of charge by default. You can purchase more as needed.
4. Click **Buy Now**.


### Upgrading public network bandwidth

<dx-alert infotype="explain"> 
Currently, the public network bandwidth can only be upgraded but not downgraded. Therefore, make your purchase with caution.
</dx-alert>

1. Log in to the [CKafka console](https://console.cloud.tencent.com/ckafka).
2. Click **Instance List** on the left sidebar and click the **ID/Name** of the target instance to enter the basic information page.
3. On the instance's basic information page, click **Upgrade** next to the public network bandwidth in the **Configuration Information** module.
4. Modify the public network bandwidth in the pop-up window and click **Submit**.



### Unsubscribing from public network bandwidth
<dx-alert infotype="explain">
<li>
 Currently, only the public network bandwidth **billed by hour** can be unsubscribed from, while that **billed by month** cannot (which can be terminated together with the instance though).
</li>
<li>
You can unsubscribe from the public network bandwidth only when there is no public network route in your instance; therefore, you need to delete public network routes first before proceeding.
</li>
</dx-alert>

1. Log in to the [CKafka console](https://console.cloud.tencent.com/ckafka).
2. Click **Instance List** on the left sidebar and click the **ID/Name** of the target instance to enter the basic information page.
3. On the instance's basic information page, click **Unsubscribe** next to the public network bandwidth in the **Configuration Information** module.
4. Click **Submit** in the pop-up window. After unsubscription, the bandwidth will stop being billed.
   



### Deleting public network route

1. Log in to the [CKafka console](https://console.cloud.tencent.com/ckafka).
2. Click **Instance List** on the left sidebar and click the **ID/Name** of the target instance to enter the basic information page.
3. In the access mode module, click **Delete** in the **Operation** column for the public network route you want to delete and select the execution time in the pop-up window.
  - Immediately: The public network route will be deleted immediately.
  - Custom time: You can select any time within the next 24 hours for scheduled deletion. The public network route will enter the state of waiting for deletion, and the scheduled deletion time can be modified in the **Operation** column.
 
 
<dx-alert infotype="explain" title="">
Deleting the public network route will result in load balancing. Do so with caution.
</dx-alert>




:::

::: Public network bandwidth management (old)

### Upgrading public network bandwidth

1. Log in to the [CKafka console](https://console.cloud.tencent.com/ckafka).
2. Click **Instance List** on the left sidebar and click the **ID/Name** of the target instance to enter the basic information page.
3. On the instance basic information page, click **Add a routing policy** in the **Access Mode** module.
4. In the pop-up window, select **Public domain name access** as the route type, select the public network bandwidth you need, and click **Submit**.



### Adjusting public network bandwidth

1. Log in to the [CKafka console](https://console.cloud.tencent.com/ckafka).
2. Click **Instance List** on the left sidebar and click the **ID/Name** of the target instance to enter the basic information page.
3. On the instance's basic information page, click the edit icon next to the public network bandwidth in the configuration information module.
4. Modify the public network bandwidth in the pop-up window and click **Submit**.

<dx-alert infotype="explain">
Public network bandwidth is billed by hour. If it is changed multiple times within one hour, fees will be charged based on the highest bandwidth value.
</dx-alert>

   

### Deleting public network route

1. Log in to the [CKafka console](https://console.cloud.tencent.com/ckafka).
2. Click **Instance List** on the left sidebar and click the **ID/Name** of the target instance to enter the basic information page.
3. In the access mode module, click **Delete** in the **Operation** column for the public network route you want to delete and select the execution time in the pop-up window.
   - Immediately: The public network route will be deleted immediately.
   - Custom time: You can select any time within the next 24 hours for scheduled deletion. The public network route will enter the state of waiting for deletion, and the scheduled deletion time can be modified in the **Operation** column.
		 
<dx-alert infotype="explain" title="">
Deleting the public network route will result in load balancing. Do so with caution.
</dx-alert>



:::
</dx-tabs>
