## Overview

This document describes how to create resources such as cluster and topic in the TDMQ console and what operations you need to perform in the console before running a client.

## Prerequisites

- You have [signed up for a Tencent Cloud account](https://intl.cloud.tencent.com/document/product/378/17985).

## Directions

### Step 1. Create a cluster

1. Log in to the [TDMQ console](https://console.cloud.tencent.com/tdmq), enter the **Cluster Management** page, and select the target region.
2. Click **Create Cluster** to create a cluster.
   ![](https://main.qcloudimg.com/raw/a6f5d8605fab1db0b4dd7adb56b11a4b.png)
3. On the **Cluster** list page, click **Access Address** in the **Operation** column of the cluster you just created to get the connection information of the server.
   ![](https://main.qcloudimg.com/raw/352ce691aed50b3de6f05b0414ef0512.png)

### Step 2. Create a namespace

1. On the **Cluster** list page, click the ID of the cluster created in step 1 to enter the cluster's basic information page.
2. Select the **Namespace** tab at the top and click **Create** to create a namespace.
   ![](https://main.qcloudimg.com/raw/8e415d23147c2dc28bb8a68120dc7cbf.png)

### Step 3. Create a role and configure permissions

1. Select **Role Management** on the left sidebar and click **Create** to create a role.
2. On the **Cluster Management** page, click the ID of the cluster you just created to enter the cluster details page.
3. Select the **Namespace** tab at the top and click **Configure Permissions** in the **Operation** column of the namespace you just created.
4. On the **Configure Permissions** page, click **Create** to add production and consumption permissions to the role you just created.
   ![img](https://main.qcloudimg.com/raw/515644356c3ec5d005f61ea19fa6e807.png)

### Step 4. Create a topic

1. On the **Namespace** list page, select the **Topic** tab at the top to enter the **Topic** list page.
2. Select the namespace created in step 3 and click **Create** to create a topic.
   ![](https://main.qcloudimg.com/raw/39a7f3e824d13f6de028eb9ffe46ca93.png)

### Step 5. Create a group

1. On the **Topic** list page, select the **Group** tab at the top to enter the **Group** list page.
2. Select the namespace you just created and click **Create** to create a group.
   ![](https://main.qcloudimg.com/raw/ce5a7784b059465f0dde65b17efd3329.png)
