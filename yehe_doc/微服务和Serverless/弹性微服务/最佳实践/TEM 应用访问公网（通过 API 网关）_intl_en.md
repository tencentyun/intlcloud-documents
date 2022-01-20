
## Overview

Applications running on TEM usually need to access the public network for business and other reasons. In many cases, these requests are all HTTP/HTTPS requests. You can use API Gateway to easily access HTTP/HTTPS requests from the public network through simple configuration.
>? If your access to the public network does not only include HTTP/HTTPS, refer to [Public Network Access of TEM Applications](https://intl.cloud.tencent.com/zh/document/product/1094/41888) to configure a NAT gateway for implementation.

## Prerequisites

Create an [environment](https://intl.cloud.tencent.com/document/product/1094/40358) and create and deploy an [application](https://intl.cloud.tencent.com/document/product/1094/40362).

## Directions

### Step 1. Associate public network HTTP/HTTPS requests in API Gateway

1. Log in to the [API Gateway console](https://console.cloud.tencent.com/apigateway) and click **Service** on the left sidebar to enter the service list page.
2. Select the same region as the TEM application and click **Create** in the top-left corner to create a service.
    When creating the service, you can select the frontend type (HTTP, HTTPS, or HTTP/HTTPS), access mode (VPC), and instance type (shared).
    <img src = "https://qcloudimg.tencent-cloud.cn/raw/5f95e38cc91b5a4854c2048a93a7fe06.png" style="width: 100%">  
3. Click the API Gateway service ID to enter the API management page and click **Create API**.
4. In the **Frontend Configuration** step, enter the API name, select **HTTP&amp;HTTPS** as the frontend type, **/** as the path, **ANY** as the request method (to include all requests), and **No authentication** as the authentication type, and click **Next**.
![](https://qcloudimg.tencent-cloud.cn/raw/a945e3e3bd7d60383c47be24b7d884a5.png)
5. In the **Backend Configuration** step, select **Public URL/IP** as the backend type, configure the public domain name and path you need to access (Tencent Cloud official website is used as an example here), and click **Next**.
![](https://qcloudimg.tencent-cloud.cn/raw/b695295cda52de71705b973c2de5a6ab.png)
6. Set the return type of the application (which is HTML here), select **JSON** as the RESTful service, and click **Complete** to publish the service.

### Step 2. Verify public network request connectivity

1. Go to the API Gateway service's basic configuration page and copy its VPC access address.
![](https://qcloudimg.tencent-cloud.cn/raw/c7132945c851609b3c559295a9968925.png)
2. Open the deployed TEM application page, enter the webshell of the application instance, and visit the API Gateway VPC access address to verify the network connectivity.
![](https://qcloudimg.tencent-cloud.cn/raw/8bd3f68e322495c0416c68cdbccecf23.png)
