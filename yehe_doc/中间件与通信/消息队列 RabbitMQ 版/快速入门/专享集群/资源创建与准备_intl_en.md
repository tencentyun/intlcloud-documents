## Overview

This document describes how to create an exclusive cluster in the TDMQ console and create resources such as vhosts, exchanges, and queues in the open-source RabbitMQ console. This helps you prepare the resources required to run a client.

## Directions

### Step 1. Create a cluster

1. Log in to the [TDMQ console](https://console.cloud.tencent.com/tdmq).
2. Select **RabbitMQ** > **Cluster** on the left sidebar and click **Create Cluster** to enter the purchase page.
3. On the purchase page, select the target instance specification and click **Buy Now**.
4. Click the cluster ID to enter the **Basic Info** page and get the server connection information in the **Network Info** section.
   ![](https://qcloudimg.tencent-cloud.cn/raw/04d5cad31290beb1445625c8bf373031.png)



### Step 2. Create a vhost

1. Click the ID of the cluster just created to enter the **Basic Info** page.
2. In the **Network Info** section, log in to the RabbitMQ console by using the access address, username, and password displayed in the **Web Console** section.
3. Select the **Admin** > **Virtual Hosts** tab and create a vhost.
   ![](https://qcloudimg.tencent-cloud.cn/raw/b2c8ec0857bb5bdaf9adafa286adfc54.png)



### Step 3. Create and authorize a user

1. Select the **Admin** > **Users** tab and create a user.
   ![](https://qcloudimg.tencent-cloud.cn/raw/22bbaa24d4ef45d2654a47340dcae2d5.png)
2. Click the name of the created user to enter the authorization page.
   ![](https://qcloudimg.tencent-cloud.cn/raw/3abc8b667f6dc235f6798424602b5819.png)
3. Grant the created user the access to the created vhost.
   ![](https://qcloudimg.tencent-cloud.cn/raw/b6480d63c579de5e05a84c1e96afe474.png)



### Step 4. Create an exchange

Select **Exchanges** at the top of the page, click **Add a new exchange**, select the created vhost, and enter the exchange name to create an exchange.

![](https://qcloudimg.tencent-cloud.cn/raw/96a030e68d04ba789864445825679e5b.png)



### Step 5. Create a queue

Select the **Queues** tab at the top of the page, click **Add a new queue**, select the created vhost, and enter the queue name to create a queue.

![](https://qcloudimg.tencent-cloud.cn/raw/c1c3fc32b12ceccd020e83a7837fdf4a.png)



### Step 6. Bind a routing

1. On the **Queues** tab, click the name of the created queue to enter the details page.
   ![](https://qcloudimg.tencent-cloud.cn/raw/57b820d50ca66cf84c3c99692bee2a6b.png)
2. Create a routing in the **Bindings** section.
   ![](https://qcloudimg.tencent-cloud.cn/raw/293c5b9f7a4f1a286af2d59c09e8123b.png)

