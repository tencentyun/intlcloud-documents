## Overview

This document describes how to create resources such as cluster, vhost, exchange, and queue in the TDMQ console and what operations you need to perform in the console before running a client.





## Prerequisites

- You have [signed up for a Tencent Cloud account](https://intl.cloud.tencent.com/document/product/378/17985).

## Directions

### Step 1. Create a cluster

1. Log in to the [TDMQ console](https://console.cloud.tencent.com/tdmq), enter the **Cluster** page, and select the target region.
2. Click **Create Cluster** and enter the cluster name and description.
3. Click **Submit**.
   ![](https://qcloudimg.tencent-cloud.cn/raw/6f32ba4d48604459759c3e234cafb7e0.png)
4. On the **Cluster** list page, click **Access Address** in the **Operation** column of the cluster you just created to get the connection information of the server.
![](https://qcloudimg.tencent-cloud.cn/raw/27d49fe8aef1e4f9401ff17e35d6a56f.png)

### Step 2. Create a vhost

1. On the **Cluster** list page, click the ID of the cluster you just created to enter the cluster's basic information page.
2. Select the **Vhost** tab at the top, click **Create**, and enter the vhost information.
   - Vhost Name: Enter the vhost name, which cannot be modified after creation and can contain 3–64 letters, digits, "-", and "_".
   - Message TTL: Set the retention time of unconsumed messages. Messages will be automatically deleted if not acknowledged after expiration. Value range: 60 seconds–15 days.
   - Remarks: Enter the vhost remarks.
3. Click **Submit**.
   ![](https://qcloudimg.tencent-cloud.cn/raw/e6dd389c40c696a4e81f571d38b41655.png)

### Step 3. Create a role and configure permissions

1. Select **Role Management** on the left sidebar in the [TDMQ console](https://console.cloud.tencent.com/tdmq) and click **Create** to create a role.
2. On the **Cluster** page, click the ID of the cluster you just created to enter the cluster details page.
3. Select the **Vhost** tab at the top and click **Configure Permissions** in the **Operation** column of the vhost you just created.
4. On the **Configure Permission** page, click **Add Role** to add production and consumption permissions to the role you just created.
    <img src="https://qcloudimg.tencent-cloud.cn/raw/27f5ba2394ed0306e82310fb344321a7.png" width="535">


### Step 4. Create an exchange

1. On the **Vhost** list page, select the **Exchange** tab at the top to enter the **Exchange** list page.
2. Select the vhost you just created, click **Create**, enter the exchange name and description, and select the route type.
   - Direct: A direct exchange will route messages to the queue whose binding key exactly matches the routing key.
   - Fanout: A fanout exchange will route messages to all queues bound to it.
   - Topic: A topic exchange supports multi-condition match and fuzzy match; that is, it will route messages to the queues bound to it by using routing key pattern match and string comparison.
   - X-delayed-message: By declaring this exchange type, you can customize the header attribute **x-delay** of the message to specify the time period for delayed message delivery in milliseconds. The message will be delivered to the corresponding queue based on the routing rule after the time period defined in **x-delay** elapses. The routing rule is subject to the route type specified in **x-delayed-type**.
3. Click **Submit**.
   ![](https://qcloudimg.tencent-cloud.cn/raw/f1c98dd23bceef637c707c846f359d14.png)

### Step 5. Create a queue

1. On the **Exchange** list page, select the **Queue** tab at the top to enter the **Queue** list page.
2. Select the Vhost you just created, click **Create**, and enter the queue name, remarks, and dead letter exchange.
3. Click **Submit**.
   ![](https://qcloudimg.tencent-cloud.cn/raw/fb820128e02ce7f7a79fb0ab2285fee8.png)

### Step 6. Create a routing

1. On the **Queue** list page, select the **Routing** tab at the top to enter the **Routing** list page.
2. Select the Vhost you just created and click **Create**.
   Select the exchange you just created as the source exchange, **Queue** as the binding type, and the queue you just created as the binding target.
3. Click **Submit**.
   ![](https://qcloudimg.tencent-cloud.cn/raw/e5614e3c31c35f170e3f59f36c3c6a86.png)
