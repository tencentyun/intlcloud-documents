WordPress is a blogging platform developed with PHP. You can use it as a content management system, or use it to create websites on services that support PHP and MySQL databases.

This document describes how to use the `tutum/wordpress` image to create a publicly accessible WordPress website.

>**Note:**
>The created WordPress with single pod is for testing purpose only. The image includes all operating environments for WordPress, allowing you to pull and create the service directly. However, using WordPress with single pod cannot ensure persistent data storage, so it is recommended that you use the self-built MySQL or Tencent Cloud CDB to store your data. For more information, please see [WordPress with CDB](https://intl.cloud.tencent.com/document/product/457/7447).

## Prerequisites
You need to create a cluster first. For more information on how to create a cluster, please see [Basic Operations of Cluster](https://intl.cloud.tencent.com/document/product/457/9091).

## Procedure
1. Log in to the [Tencent Cloud TKE console](https://console.cloud.tencent.com/ccs).
2. Click **Service** in the left navigation bar, and click **+ New** in the service list page.
![](https://main.qcloudimg.com/raw/8356f5ad7e4ce21d9cb71758bc9e4c5f.png)
3. Configure basic service information.
 - **Service Name**: The name of the service to be created, which is comprised of lowercase letters, numbers and "-". It starts with a lowercase letter and ends with a lowercase letter or a number.
 - **Region**: Select the closest region based on your location.
 - **Cluster**: Select a cluster to run your service. You need to select a running cluster with available CVMs in it.
 - **Service description**: Information of the created service. This information is displayed on the **Service Information** page.
![](https://main.qcloudimg.com/raw/73687fc0802c6424dc67938b8314f9fb.png)
4. Image configuration.
 - **Name**: Enter the name of the running container (here is WordPress).
 - **Image**: Enter `tutum/wordpress`.
 - **Version (Tag)**: Enter "latest".
![](https://main.qcloudimg.com/raw/32772dc0702d2a2d201e1f15d784a0ba.png)
5. Configure port mapping. Set both container port and service port to 80.
![](https://main.qcloudimg.com/raw/c4aaf83d20d944d83c407bfb7d1c6af7.png)
6. Click **Create Service** to complete the creation of the WordPress service.
>**Note**: Keep default settings for other options.

## Accessing WordPress Service
1. Click **Service Information** on the service page to check the load balancer IP.
![](https://main.qcloudimg.com/raw/2dcc23110a59e265e58bde07ede14d92.png) 
2. Enter the IP in the browser to access the service.
![Alt text](https://main.qcloudimg.com/raw/3d3c21421cb2b1688853ae7deba3de8f.png)


