## Overview

For a service in native LoadBalancer mode, a Cloud Load Balancer (CLB) can be automatically created. It first forwards traffic to a cluster through the Nodeport of the cluster, and then forwards it again through iptable or ipvs. Services in this mode can meet users’ needs in most scenarios, but in the following scenarios, **services in direct pod connection mode** are recommended:

- The source IP address needs to be obtained (local forwarding must be enabled for the non-direct connection mode)
- Higher forwarding performance is required (there are two layers of CLBs when the CLB and service are in non-direct connection mode, so performance loss is inevitable.)
- Complete health checks and session persistence are required for the pod layer (there are two layers of CLBs when the CLB and service are in non-direct connection mode, so health checks and session persistence are difficult to configure.)

## Use Limits

- The Kubernetes version of the cluster must be 1.12 or later.
- The VPC-CNI ENI mode must be enabled for the cluster network mode.
- The workloads used by a service in direct connection mode must adopt the VPC-CNI ENI mode.
- The feature limits of a CLB bound to an ENI must be satisfied. For more information, see [Binding an ENI](https://intl.cloud.tencent.com/document/product/214/32520).
- When workloads in direct pod connection mode are updated, a rolling update is performed based on the health check status of the CLB, affecting the update speed.

## Directions

### Console operation instructions

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. Go to the "Create a Service" page and configure the service parameters as required by referring to the step of [Creating a Service in the Console](https://intl.cloud.tencent.com/document/product/457/36833).
Configure some key parameters as follows:
![](https://main.qcloudimg.com/raw/1e52f535cd9eb5712ddf6c4760952e70.png)
	- **Service Access Mode**: select **Provide Public Network Access** or **VPC Private Network Access**.
	- **Network Mode**: select **Direct CLB-Pod Connection Mode**.
	- **Workload Binding**: select **Import Workload**. In the window that appears, select the backend workload of the VPC-CNI mode.
3. Click **Create a Service** to complete the creation.

### YAML operation instructions

#### YAML example
The YAML configuration for a service in direct pod connection mode is the same as that for a common service. In this example, the annotation indicates whether to enable the direct pod connection mode.
```
kind: Service
apiVersion: v1
metadata:
  annotations:
	service.cloud.tencent.com/direct-access: true ##Enable the direct pod connection mode
  name: my-service
spec:
  selector:
    app: MyApp
  ports:
  - protocol: TCP
    port: 80
    targetPort: 9376
  type: LoadBalancer
```



#### Annotation extension
For the CLB configuration, see [CLB Configuration](https://intl.cloud.tencent.com/document/product/457/36834). The annotation configuration is as follows:
```
service.cloud.tencent.com/tke-service-config: [tke-service-configName]
```
