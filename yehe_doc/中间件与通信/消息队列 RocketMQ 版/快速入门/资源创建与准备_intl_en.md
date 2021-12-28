## Overview

This document describes how to create resources such as cluster and topic in the TDMQ console and what operations you need to perform in the console before running a client.

## Prerequisites

- You have [signed up for a Tencent Cloud account](https://intl.cloud.tencent.com/document/product/378/17985).

## Directions

### Step 1. Create a cluster

1. Log in to the [TDMQ console](https://console.cloud.tencent.com/tdmq), enter the **Cluster Management** page, and select the target region.
2. Click **Create Cluster** to create a cluster.
    ![](https://qcloudimg.tencent-cloud.cn/raw/cdb9f5bf094541056fa892d9da76ca96.png)
3. On the **Cluster** list page, click **Access Address** in the **Operation** column of the cluster you just created to get the connection information of the server.
    ![](https://qcloudimg.tencent-cloud.cn/raw/77687fcea3acf00e964918980a3b60f3.png)

### Step 2. Create a namespace

1. On the **Cluster** list page, click the ID of the cluster created in step 1 to enter the cluster's basic information page.
2. Select the **Namespace** tab at the top and click **Create** to create a namespace.
   ![](https://qcloudimg.tencent-cloud.cn/raw/5a1fdfd089497eced11a3de69e1ca651.png)

### Step 3. Create a role and configure permissions

1. Select **Role Management** on the left sidebar and click **Create** to create a role.
2. On the **Cluster Management** page, click the ID of the cluster you just created to enter the cluster details page.
3. Select the **Namespace** tab at the top and click **Configure Permissions** in the **Operation** column of the namespace you just created.
4. On the **Configure Permissions** page, click **Create** to add production and consumption permissions to the role you just created.
   ![img](https://qcloudimg.tencent-cloud.cn/raw/aea0918d1f2e54ed0ca5f10ab2a94574.png)

### Step 4. Create a topic

1. On the **Namespace** list page, select the **Topic** tab at the top to enter the **Topic** list page.
2. Select the namespace created in step 3 and click **Create** to create a topic.
   ![](https://qcloudimg.tencent-cloud.cn/raw/050d76fe792a2e3609d87c15e5862ca7.png)

### Step 5. Create a group

1. On the **Topic** list page, select the **Group** tab at the top to enter the **Group** list page.
2. Select the namespace you just created and click **Create** to create a group.
   ![](https://qcloudimg.tencent-cloud.cn/raw/abfb914dfe9819ef247ef84cc84551fd.png)
