## Overview

This document describes how to create resources such as cluster and topic in the TDMQ for Pulsar console and what operations you need to perform in the console before running a client.

## Directions

### Step 1. Create a cluster and configure the network

1. Log in to the [TDMQ for Pulsar console](https://console.cloud.tencent.com/tdmq), enter the **Cluster Management** page, and select the target region.
2. Click **Create Cluster** to create a cluster.
3. Click **Access Address** in the **Operation** column of the created cluster.
     ![](https://qcloudimg.tencent-cloud.cn/raw/72d7e1f59410ced5ab00403406f29727.png) 
    You can get the access address in the following ways:
   <dx-tabs>
   ::: Clusters\son\sv2.7.1\sor\sabove
   You can directly get the access address as shown below:
      ![](https://qcloudimg.tencent-cloud.cn/raw/cba9bfef826619335cf9ba9c4c8b0e5a.png)
   :::
   ::: Clusters\son\sv2.6.1
   On the access point list page, click **Create** to create a VPC access point (in the same VPC as the resource on which the client runs) .
   :::
   </dx-tabs>

> ?For more information on clusters, see [Cluster Management](https://intl.cloud.tencent.com/document/product/1110/42928).

### Step 2. Create a namespace

> ?If your cluster version is 2.6.1, you can directly use the automatically created default namespace. For more information on namespaces, see [Namespace](https://intl.cloud.tencent.com/document/product/1110/42929).

On the **[Namespace](https://console.cloud.tencent.com/tdmq/env)** page in the console, select the region and the cluster just created and click **Create** to create a namespace.

![](https://qcloudimg.tencent-cloud.cn/raw/9f9eefdc535750ff0bca2d7720fcb5b1.png)

### Step 3. Create a role and configure permissions

1. On the **[Role Management](https://console.cloud.tencent.com/tdmq/role)** page in the console, select the region and the cluster just created and click **Create** to enter the **Create Role** page.
2. Enter the role name and remarks and click **Submit**.
3. Enter the **[Namespace](https://console.cloud.tencent.com/tdmq/env)** page and click **Configure Permission** in the **Operation** column of the namespace just created to open its permission list.
4. On the **Configure Permissions** page, click **Add Role**, add the role just created, and assign the production and consumption permissions.
   ![](https://qcloudimg.tencent-cloud.cn/raw/2ff48a2715937e0436c101e4f631be95.png)
5. If the following is displayed, the permissions are configured successfully.
   ![](https://qcloudimg.tencent-cloud.cn/raw/4b756a7bf60bb50036805b9890fa4b1d.png)



### Step 4. Create a topic and subscription

1. On the **[Topic Management](https://console.cloud.tencent.com/tdmq/topic)** page, select the target region, cluster, and namespace and click **Create** to create a topic.
2. Click **Create Subscription** in the **Operation** column to create a subscription for the topic just created.
3. Click **More** > **View subscription** in the **Operation** column to view the subscription just created.
   ![](https://qcloudimg.tencent-cloud.cn/raw/cbab46518844a44584530d2536d16ff6.png)
