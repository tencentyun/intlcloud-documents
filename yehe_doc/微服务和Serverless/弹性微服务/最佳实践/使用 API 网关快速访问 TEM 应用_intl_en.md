## API Gateway Overview

API Gateway is an API hosting service launched by Tencent Cloud, which supports the management of APIs throughout their lifecycle from creation, maintenance, launch, and operation to deactivation. For more information, see [API Gateway product documentation](https://intl.cloud.tencent.com/zh/document/product/628).

## Overview

This document describes how to quickly use API Gateway to access a TEM application and manage its APIs. With the combination of API Gateway and TEM, you can enjoy the advanced capabilities of API Gateway such as traffic throttling, authentication, and caching for better business outcomes.
<img src="https://qcloudimg.tencent-cloud.cn/raw/a353d0a3340323f948920a02a71ec0ab.png">

## Prerequisites

Log in to the [TEM console](https://console.cloud.tencent.com/tem), create an [environment](https://intl.cloud.tencent.com/document/product/1094/40358), and create and deploy an [application](https://intl.cloud.tencent.com/document/product/1094/40362).

## Directions

### Step 1. Configure VPC access for the TEM application

1. Log in to the [TEM console](https://console.cloud.tencent.com/tem), click **Application Management** on the left sidebar, and click the target application to enter the application details page .
2. Click **Edit and Update** in the **Access Configuration** section to enter the application access configuration page.
3. Select VPC access (layer-4 forwarding), select the subnet, protocol, container port, and application listening port, and click **Submit**. At this point, TEM will automatically create a layer-4 forwarding VPC CLB instance for you.


### Step 2. Create an API Gateway service and bind it to the TEM application[](id:step2)

1. Log in to the [API Gateway console](https://console.cloud.tencent.com/apigateway/service) and click **Service** on the left sidebar to enter the service list page.
2. Select the same region as the TEM application and click **Create** in the top-left corner to create a service.
   When creating the service, you can select the frontend type (HTTP, HTTPS, or HTTP/HTTPS), access mode (VPC or public network), and instance type (shared or dedicated).
	 <img src="https://qcloudimg.tencent-cloud.cn/raw/5f95e38cc91b5a4854c2048a93a7fe06.png">
3. Click the API Gateway service ID to enter the API management page and click **Create API**.
4. In the **Frontend Configuration** step, enter the API name, select **HTTP&HTTPS** as the frontend type, **/** as the path, **ANY** as the request method (to include all requests), and **Authentication-free** as the authentication type, and click **Next**.
   ![](https://qcloudimg.tencent-cloud.cn/raw/a945e3e3bd7d60383c47be24b7d884a5.png)
5. In the **Backend Configuration** step, select **VPC resource** as the backend type, select the VPC where the TEM application deployment environment is located, set the backend domain name, select the CLB instance automatically created by the TEM application (named "cls-xxxdefault{TEM application name}"), select the corresponding listener (i.e., the port mapping set in the previous step), and enter `/` as the backend address.
   ![](https://qcloudimg.tencent-cloud.cn/raw/37a8a5b7bc18613de223419c978b7f8e.png)
6. At this point, you can see the API you configured and access your TEM application at the default domain name provided by API Gateway.


### Step 3. Access the TEM application through API Gateway

Call the API Gateway API created in [step 2](#step2) to access the TEM application through API Gateway.
   ![](https://main.qcloudimg.com/raw/70ca90f3a189c79f09f0c8e334507b22.png)

## Notes

- In order to ensure that applications can access API Gateway in a non-intrusive manner, we recommend you bind an API Gateway service to only one TEM application and keep the frontend address and backend address the same. If they are both `/`, all APIs can be blocked. You can also make separate configurations for some of your application's APIs.
- You can refer to [Overview](https://intl.cloud.tencent.com/zh/document/product/628/40214) to bind the plugin to the API Gateway API with a TEM backend and then enjoy advanced features provided by API Gateway.
