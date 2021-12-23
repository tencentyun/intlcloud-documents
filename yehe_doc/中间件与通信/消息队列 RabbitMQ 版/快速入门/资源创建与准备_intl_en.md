## Overview

This document describes how to create resources such as cluster, vhost, exchange, and queue in the TDMQ console and what operations you need to perform in the console before running a client.

## Prerequisites

- You have [signed up for a Tencent Cloud account](https://intl.cloud.tencent.com/document/product/378/17985).

## Directions

### Step 1. Create a cluster

1. Log in to the [TDMQ console](https://console.cloud.tencent.com/tdmq), enter the **Cluster Management** page, and select the target region.
2. Click **Create Cluster** and enter the cluster name and remarks.
3. Click **Submit**.
   ![](https://main.qcloudimg.com/raw/f57c3cb1baf598ca8a7de47def4d0981.png)
4. On the **Cluster** list page, click **Access Address** in the **Operation** column of the cluster you just created to get the connection information of the server.
![](https://main.qcloudimg.com/raw/0238d2d64bd896704ebef400fc08a7f1.png)

### Step 2. Create a vhost

1. On the **Cluster** list page, click the ID of the cluster you just created to enter the cluster's basic information page.
2. Select the **Vhost** tab at the top, click **Create**, and enter the vhost information.
   - Vhost Name: enter the vhost name, which cannot be modified after creation and can contain 3–64 letters, digits, hyphens, and underscores.
   - Message TTL: set the retention time of unconsumed messages. Messages will be automatically deleted if not acknowledged after expiration. Value range: 60 seconds–15 days.
   - Remarks: enter the vhost remarks.
3. Click **Submit**.
   ![](https://main.qcloudimg.com/raw/c87ba46c5d7e458f392c41579964be9a.png)

### Step 3. Create a role and configure permissions

1. Select **Role Management** on the left sidebar in the [TDMQ console](https://console.cloud.tencent.com/tdmq) and click **Create** to create a role.
2. On the **Cluster Management** page, click the ID of the cluster you just created to enter the cluster details page.
3. Select the **Vhost** tab at the top and click **Configure Permissions** in the **Operation** column of the vhost you just created.
4. On the **Configure Permissions** page, click **Create** to add production and consumption permissions to the role you just created.
<img src="https://main.qcloudimg.com/raw/515644356c3ec5d005f61ea19fa6e807.png" width="535">


### Step 4. Create an exchange

1. On the **Vhost** list page, select the **Exchange** tab at the top to enter the **Exchange** list page.
2. Select the vhost you just created, click **Create**, enter the exchange name and remarks, and select the exchange type.
   - Direct: a direct exchange will route messages to the queue whose binding key exactly matches the routing key.
   - Fanout: a fanout exchange will route messages to all queues bound to it.
   - Topic: a topic exchange supports multi-condition match and fuzzy match; that is, it will route messages to the queues bound to it by using routing key pattern match and string comparison.
3. Click **Submit**.
   ![](https://main.qcloudimg.com/raw/a05cf17275616133497dd8334e39fd05.png)

### Step 5. Create a queue

1. On the **Exchange** list page, select the **Queue** tab at the top to enter the **Queue** list page.
2. Select the Vhost you just created, click **Create**, and enter the queue name and remarks.
3. Click **Submit**.
   ![](https://main.qcloudimg.com/raw/dfabbd7014042b368168621ff6ebd10e.png)

### Step 6. Create a binding

1. On the **Queue** list page, select the **Binding** tab at the top to enter the **Binding** list page.
2. Select the Vhost you just created and click **Create**.
   Select the exchange you just created as the source exchange, **Queue** as the binding type, and the queue you just created as the binding target.
3. Click **Submit**.
   ![](https://main.qcloudimg.com/raw/27dca8450a4f059179488062738be0ed.png)
