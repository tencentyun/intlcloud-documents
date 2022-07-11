## Introduction on TEM

Tencent Cloud Elastic Microservice (TEM) is a Serverless platform designed for microservice applications. It perfectly combines serverless and microservice to provide out-of-the-box microservice solutions. TEM embraces the concept of open source, makes it possible to cloudify applications with zero modifications required, offers a wide range of capabilities such as application hosting, service registration and discovery, microservice governance, and multidimensional monitoring, and well supports Eureka and ZooKeeper registries. Moreover, TEM helps you create and manage pay-as-you-go cloud resources without Ops costs. For more information, see [Tencent Cloud Elastic Microservice](https://intl.cloud.tencent.com/document/product/1094).

## Overview

This document describes how to quickly use API Gateway to access a TEM application and manage its APIs. With the combination of API Gateway and TEM, you can enjoy the advanced capabilities of API Gateway such as traffic throttling, authentication, and caching for better business outcomes.
<img src="https://qcloudimg.tencent-cloud.cn/raw/51b9a6d47134c0e83500f05899537d28.png" width="650px">

## Prerequisites

Log in to the [TEM console](https://console.cloud.tencent.com/tem), create an [environment](https://intl.cloud.tencent.com/document/product/1094/40358), and create and deploy an [application](https://intl.cloud.tencent.com/document/product/1094/40362).

## Directions

### Step 1. Configure VPC access for the TEM application

1. Log in to the [TEM console](https://console.cloud.tencent.com/tem), click **Application Management** on the left sidebar, and click the target application to enter the application details page.
2. Click **Edit and update** in the **Access configuration** section to enter the application access configuration page.
3. Select VPC access (layer-4 forwarding), select the subnet, protocol, container port, and application listening port, and click **Submit**. At this point, TEM will automatically create a layer-4 forwarding VPC CLB instance for you.

### Step 2. Create an API Gateway service and bind it to the TEM application[](id:step2)

1. Log in to the [API Gateway console](https://console.cloud.tencent.com/apigateway/service) and click **Service** on the left sidebar to enter the service list page.
2. Select the same region as the TEM application and click **Create** in the top-left corner to create a service.
   When creating the service, you can select the frontend type (HTTP, HTTPS, or HTTP/HTTPS), access mode (VPC or public network), and instance type (shared or dedicated).
>?For more information on the selection of instance type, see [Instance Selection](https://intl.cloud.tencent.com/document/product/628/40305).
>
3. Click the API Gateway service ID to enter the API management page and click **Create API**.
4. In the **Frontend configuration** step, enter the API name, select **HTTP&HTTPS** as the frontend type, **/** as the path, **ANY** as the request method (to include all requests), and **Authentication-free** as the authentication type, and click **Next**.
5. In the **Backend configuration** step, select **VPC resources** as the backend type, select the VPC where the TEM application deployment environment is located, set the backend domain name, select the CLB instance automatically created by the TEM application (named "cls-xxxdefault{TEM application name}"), select the corresponding listener (i.e., the port mapping set in the previous step), and enter `/` as the backend address.
6. At this point, you can see the API you configured and access your TEM application at the default domain name provided by API Gateway.

### Step 3. Access the TEM application through API Gateway

Call the API Gateway API created in [step 2](#step2) to access the TEM application through the API Gateway.
![](https://qcloudimg.tencent-cloud.cn/raw/ace08d2d34747387dc0029a1b71143a0.png)

## Notes

- In order to ensure that applications can access API Gateway in a non-intrusive manner, we recommend you bind an API Gateway service to only one TEM application and keep the frontend address and backend address the same. If they are both `/`, all APIs can be blocked. You can also make separate configurations for some of your application's APIs.
- You can refer to [Plugin Usage](https://intl.cloud.tencent.com/document/product/628/40213) to bind the plugin to the API Gateway API that connects the backend with the TEM.
