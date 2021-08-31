## Overview

When you use a hybrid cloud architecture, your business may be deployed in both public and private clouds, but a unified access layer is required, which serves as the ingress and egress of traffic and supports the processing of all non-business features such as authentication and traffic throttling.

An API Gateway dedicated instance runs in a VPC and supports forwarding client requests to various services deployed in the VPC or local IDC or on the public network. It is deeply integrated with common backend services to provide a productized connection method. Therefore, it is very suitable as a unified access layer in complex network environments. This document describes how to connect to backend resources in an IDC by using an API Gateway dedicated instance.

## Scheme Advantages

![](https://main.qcloudimg.com/raw/2adf52e12df99cc9d0eecc998c8b6ecc.png)

- The API Gateway dedicated instance can forward requests to the backend resources deployed in the VPC and local IDC and on the public network at the same time, seamlessly connecting the cloud and local systems and enabling smooth cloudification.
- The rich features provided by API Gateway can also be used, such as IP access control, traffic throttling, and log monitoring.
- Resources on the private network can be interconnected with each other through CCN, fine-grained routing is supported to guarantee the quality, and diversified tiered pricing is supported to reduce the costs.

## Directions

### Step 1. Create a CCN instance and associate it with a network instance[](id:Step-1)

1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc).
2. On the left sidebar, click **Cloud Connect Network** to enter the CCN management page.
3. Click **+ New**.
4. In the pop-up window, enter the name and description of the CCN instance and select the billing mode, service level, and bandwidth limit mode.
5. Associate the IDC's Direct Connect gateway with the VPC.
	 ![](https://main.qcloudimg.com/raw/7063ae428f1bb924e9eeb5a999a67eab.png)

### Step 2. Purchase an API Gateway dedicated instance

1. Log in to the [API Gateway console](https://console.cloud.tencent.com/apigateway) and select **Instance** on the left sidebar.
2. Click **Create** to enter the API Gateway dedicated instance purchase page.
3. Select and enter the instance configuration information.
>!The VPC configuration of the dedicated instance should be the same as that of the VPC instance associated with the CCN instance created in [step 1](#Step-1).
>
4. Click **Buy Now** and make the payment.

### Step 3. Create a service and API under the instance

1. Log in to the [API Gateway console](https://console.cloud.tencent.com/apigateway) and select **Service** on the left sidebar.
2. Click **Create** and select **Dedicated** as the instance type.
3. In the pop-up window for instance selection, select the dedicated instance purchased in step 1 and click **Submit**.
4. Click the name of the created service in the service list to enter its API management page.
5. Click **Create** to enter the API creation page and set the configuration items. Select public URL/IP as the API backend type, enter the IDC's private IP, port, and path to be bound as the backend address, and click **Submit**.
6. Request the created API, and you will see that the backend resources in the IDC can be accessed through API Gateway.
