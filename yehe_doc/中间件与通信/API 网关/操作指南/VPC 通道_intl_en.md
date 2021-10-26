## Overview

A VPC upstream is to open the services deployed in the VPC for external access through API Gateway. It provides load balancing capabilities and can connect to multiple services in the VPC at the same time.

## Solution Strengths

- There is no need to purchase private network CLBs. With VPC upstreams, you can use API Gateway alone to open services in the VPC for external access. The VPC upstream feature itself is free of charge, resulting in low costs.
- VPC subnets are used for communication, resulting in low network latency and high performance.

## Prerequisites

- You have purchased a [dedicated API Gateway instance](https://intl.cloud.tencent.com/document/product/628/40305).
- You have created VPC resources such as [CVMs](https://console.cloud.tencent.com/cvm).

>!Currently, VPC upstreams support only APIs mounted under dedicated instances but not shared instances.


## Directions

### Step 1: create a VPC upstream

1. Log in to the [API Gateway console](https://console.cloud.tencent.com/apigateway).
2. In the left sidebar, click **VPC Upstreams**. The VPC upstream list page is displayed.
3. Click **Create** in the top-left corner to create a VPC upstream.

| Parameter | Required | Description |
| ------------ | -------- | ------------------------------------------------------------ |
| Upstream Name | No       | Name of the VPC upstream. An upstream name can contain up to 50 characters out of a-z, A-Z, 0-9, and _.      |
| VPC     | Yes       | VPC of the backend resource to be connected.                               |
| Description         | No       | Remarks of the VPC upstream.                                      |
| Load Balancing Algorithm | No       | Only the weighted polling algorithm is supported currently.                                       |
| Protocol         | Yes       | Protocol for API Gateway to interact with backend resources. HTTP and HTTPS are supported.        |
| Host Header  | No       | Request header Host of backend requests, usually the backend service domain name and port number.     |
| Node List     | Yes       | List of backend nodes to which API Gateway forwards messages. A list can contain up to 200 nodes. You need to set the node address, port number, and weight for each node. |
| Retry Attempts     | Yes       | Number of retry attempts for a failed node request of API Gateway. The default value is 5. Enter an integer ranging from 1 to 100. |

![](https://qcloudimg.tencent-cloud.cn/raw/616613c74e0b9fa196f8258642accd60.png)

### Step 2: create an API for the backend to connect to resources in the VPC and associate it with the VPC upstream

1. Log in to the [API Gateway console](https://console.cloud.tencent.com/apigateway/index?rid=1) and click **Service** in the left sidebar.
2. In the service list, click a service name **mounted under a dedicated instance** to view the service details.
3. In the service details, click the **Manage API** tab and choose to create a **General API** based on the backend business type.
4. Click **Create**, configure the API frontend, and click **Next**.
5. In **Backend Configuration**, set **Backend Type** to **VPC resources**, set **Connection Mode** to **VPC Upstream**, and select the VPC upstream created in step 1.
6. Complete the rest configuration.

### Step 3: call the API

Call the API created in step 2. The API can be called successfully.

## Notes

- On the **Associated APIs** tab on the VPC upstream details page, you can view the APIs that use the current VPC channel as the backend. You need to delete these APIs before deleting the VPC upstream to avoid affecting API calling.
- A dedicated instance runs in a VPC. If the VPC where the dedicated instance resides is inconsistent with the VPC connected to the VPC upstream, connect the two VPCs via [Cloud Connect Network](https://console.cloud.tencent.com/vpc/ccn) to avoid affecting API calling.
