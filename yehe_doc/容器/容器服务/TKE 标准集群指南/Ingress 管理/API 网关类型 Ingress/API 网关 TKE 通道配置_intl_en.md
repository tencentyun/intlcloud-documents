## Overview

You can directly access Pods in a TKE cluster through API Gateway without passing through CLB. This document describes how to create a TKE tunnel and configure it as the backend type of an API in the console, so that requests from API Gateway go directly to the corresponding Pod of the TKE tunnel.

**Feature strengths**
- API Gateway is directly connected to the Pods of the TKE cluster, reducing intermediate nodes (such as CLB).
- A TKE tunnel can connect multiple TKE clusters at the same time.

>?TKE tunnels are currently only supported by **dedicated** API Gateway instances.

## Prerequisites
1. You have a dedicated instance.
2. You have an TKE cluster and have obtained its admin role.

## Directions
### Step 1. Create a TKE tunnel

1. Log in to the [API Gateway console](https://console.cloud.tencent.com/apigateway/index).
2. Select **Backend Tunnel** on the left sidebar and click **Create**.
3. On the **Create Backend Tunnel** page, enter the following information: 
   - Backend Tunnel Name: enter a custom name.
   - Tunnel Type: select **TKE tunnel**.
   - VPC: select a VPC.
   - Service List: up to 20 services can be configured in the service list. The weighted round robin algorithm is used to distribute traffic among multiple Pods. The steps to configure a service are as follows:
     1. Enter the weight ratio of each Pod of the service.
     2. Select the cluster. If the cluster has not been authorized, API Gateway will request authorization.
     3. Select a namespace in the cluster.
     4. Select the service and its port.
     5. Advanced options: select additional node labels.
   - Backend Type: select HTTP or HTTPS.
   - Host Header: it is optional and is the value of host in the request header carried in the HTTP/HTTPS request when API Gateway accesses the backend service.
   - Tags: they are optional and manage resources by category in different dimensions.  

### Step 2. Connect the API backend to the TKE tunnel
1. On the [Service](https://console.cloud.tencent.com/apigateway/service) page in the API Gateway console, click the target service ID to enter the API management page.
2. Click **Create** to create a general API.
3. Enter the frontend configuration information and click **Next**.
4. Select **VPC resources** as the backend type, select **TKE tunnel** as the backend tunnel type, and click **Next**.  
5. Set the response result and click **Complete**.

## Network Architecture
After the TKE tunnel is bound to the API, the architecture of the entire network is as follows:

![](https://qcloudimg.tencent-cloud.cn/raw/5268cfc9ad3cd6e0a8616dbf6394c22c.png)

API Gateway directly accesses the Pods in the TKE cluster without passing through CLB. The YAML configuration file of the cluster's httpbin service is as follows, where the `selector` indicates that the Pod with the tag key `app` and tag value `httpbin` is selected as the node of the TKE tunnel. Therefore, Pods on versions 1/2/3 are also nodes of the TKE tunnel.
```yaml
apiVersion: v1
kind: Service
metadata:
  name: httpbin
  labels:
    app: httpbin
    service: httpbin
spec:
  ports:
  - name: http
    port: 8000
    targetPort: 80
  selector:
    app: httpbin
```

 

## Notes

- A TKE tunnel can connect up to 20 TKE services.
- You should have the admin role of the TKE cluster.
- The TKE tunnel and the dedicated API Gateway instance must be in the same region. Currently, API Gateway doesn't support cross-VPC access.
