## Overview

CKafka transfers data over the private network by default. To access over the public network, you need to activate a public network route separately. For detailed directions, please see [Adding Routing Policy](https://intl.cloud.tencent.com/document/product/597/32555). Currently, 3 Mbps public network bandwidth is provided free of charge by default.

CKafka Pro Edition supports increasing the public network bandwidth to up to 198 Mbps for a fee. For the specific prices, please see [Billing Overview](https://intl.cloud.tencent.com/document/product/597/11745).

This document describes how to upgrade, adjust, and delete the public network bandwidth in the CKafka console.

## Directions

### Upgrading public network bandwidth

1. Log in to the [CKafka console](https://console.cloud.tencent.com/ckafka).
2. Click **Instance List** on the left sidebar and click the **ID/Name** of the target instance to enter the basic information page.
3. On the instance basic information page, click **Add a routing policy** in the **Access Mode** module.
4. In the pop-up window, select **Public domain name access** as the route type, select the public network bandwidth you need, and click **Submit**.

![](https://main.qcloudimg.com/raw/5e4e665632e7ebd5a78931e87819b5d8.png)

### Adjusting public network bandwidth

1. Log in to the [CKafka console](https://console.cloud.tencent.com/ckafka).
2. Click **Instance List** on the left sidebar and click the **ID/Name** of the target instance to enter the basic information page.
3. On the instance's basic information page, click the edit icon next to the public network bandwidth in the configuration information module.
   ![](https://main.qcloudimg.com/raw/e831bfe8a42bb3e1e9dee069a85155b7.png)
4. Modify the public network bandwidth in the pop-up window and click **Submit**.
>?Public network bandwidth is billed by hour. If it is changed multiple times within one hour, fees will be charged based on the highest bandwidth value.
>
![](https://main.qcloudimg.com/raw/d26c1378a4ce18e0356a780e2f921717.png)

### Deleting public network route

1. Log in to the [CKafka console](https://console.cloud.tencent.com/ckafka).
2. Click **Instance List** on the left sidebar and click the **ID/Name** of the target instance to enter the basic information page.
3. In the access mode module, click **Delete** in the **Operation** column for the public network route you want to delete and select the execution time in the pop-up window.
>?Deleting the public network route will result in load balancing. Please do so with caution.
>
![](https://main.qcloudimg.com/raw/0b39161d566885348c433b8e65696278.png)
   - Immediately: the public network route will be deleted immediately.
   - Custom time: you can select any time within the next 24 hours for scheduled deletion. The public network route will enter the state of waiting for deletion, and the scheduled deletion time can be modified in the **Operation** column.
![](https://main.qcloudimg.com/raw/30008f4c164cd70fcfab68cd8f6b50ff.png)

   
