## Overview

For a service in native LoadBalancer mode, a Cloud Load Balancer (CLB) can be automatically created. It first forwards traffic to a cluster through the Nodeport of the cluster, and then forwards it again through iptable or ipvs. Services in this mode can meet users’ needs in most scenarios, but in the following scenarios, **services in CLB-to-Pod direct access mode** are recommended:

- The source IP needs to be obtained (local forwarding must be enabled for non-direct access mode)
- Higher forwarding performance is required (there are two layers of CLBs when the CLB and service are in non-direct access mode, so performance loss is inevitable).
- Complete health checks and session persistence are required for the Pod layer (there are two layers of CLBs when the CLB and service are in non-direct access mode, so health checks and session persistence are difficult to configure).



> ? Currently, the CLB-to-Pod direct access mode is available for both GlobleRouter and VPC-CNI container network modes. Click the cluster ID in the [cluster list](https://console.cloud.tencent.com/tke2/cluster?rid=1) to go to the cluster details page. In the **Basic Information** page, you can find the container network add-on used by the current cluster.
>


## VPC-CNI Mode

### Use limits

- The Kubernetes version of the cluster must be 1.12 or later.
- The VPC-CNI ENI mode must be enabled for the cluster network mode.
- The workloads used by a service in direct access mode must adopt the VPC-CNI ENI mode.
- The feature limits of a CLB bound to an ENI must be satisfied. For more information, see [Binding an ENI](https://intl.cloud.tencent.com/document/product/214/32520).
- When workloads in CLB-to-Pod direct access mode are updated, a rolling update is performed based on the health check status of the CLB, which will affect the update speed.

### Directions

<dx-tabs>
::: Console operation instructions
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. Go to the "Create a Service" page and configure the service parameters as required by referring to the step of [creating a service in the console](https://intl.cloud.tencent.com/document/product/457/36833).
    Configure some key parameters as follows:
![](https://main.qcloudimg.com/raw/5190f97b699f9d0d856aeb0412a9428f.png)
 - **Service Access**: select **LoadBalancer (public network)** or **LoadBalancer (private network)**.
 - **Network Mode**: **Enable CLB-to-Pod Direct Access**.
 - **Workload Binding**: select **Reference Workload**. In the displayed window, select the backend workload of the VPC-CNI mode.
3. Click **Create Service** to complete creation. 
		

:::
::: YAML operation instructions
The YAML configuration for a service in CLB-to-Pod direct access mode is the same as that for a common service. In this example, the annotation indicates whether to enable the CLB-to-Pod direct access mode.

```
kind: Service
apiVersion: v1
metadata:
    annotations:
  	service.cloud.tencent.com/direct-access: true ##Enable CLB-to-Pod direct access
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

For the CLB configuration, see [Service CLB Configuration](https://intl.cloud.tencent.com/document/product/457/36834). The annotation configuration is as follows:

```
service.cloud.tencent.com/tke-service-config: [tke-service-configName]
```

:::
</dx-tabs>































## GlobalRouter Mode 

### Use limits

- A workload can only run in one network mode. You can choose VPC-CNI ENI mode or GlobalRoute mode for the workloads used by a service in direct access mode.
- It is only available for the bill-by-IP accounts.
- When the CLB-to-Pod direct access mode is used, the network linkage is restricted by the security group of CVM. Please confirm whether the security group configuration opens the corresponding protocol and port. **The port corresponding to the workload on the CVM needs to be opened.**
- After the CLB-to-Pod direct access mode is enabled, the [ReadinessGate](https://intl.cloud.tencent.com/document/product/457/38368) (readiness check) will be enabled by default. It will check whether the traffic from the load balancer is normal during the rolling update of Pod. You also need to configure the correct health check configuration for the application. For details, see [Service CLB Configuration](https://intl.cloud.tencent.com/document/product/457/36834).
- The CLB-to-Pod direct access in Globalrouter mode is in beta test. You can use it through the following two ways:
 -**You can use it via [CCN](https://intl.cloud.tencent.com/document/product/1003).** (recommended). CCN can verify the bound IP address to prevent common IP binding problems such as binding errors and address loopback. The instructions are as follows:
   1. Create a CCN instance. For more information, please see [Creating a CCN Instance](https://intl.cloud.tencent.com/document/product/1003/30062).
   2. Add the VPC where the cluster is located to the created CCN instance.
   3. Register the container network CIDR block of the relevant cluster to the CCN. In the cluster’s **Basic Information** page, enable the **CCN**.
![](https://main.qcloudimg.com/raw/e9c44e7cb6ba38bc1ab34ea1f4d91cef.png)
 - You can [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=350&source=0&data_title=%E5%AE%B9%E5%99%A8%E6%9C%8D%E5%8A%A1%20TKE&step=1) to apply for this feature. **CCN will not verify the IP address in this method** (not recommended).


### Directions

<dx-tabs>
::: Console operation instructions
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. Go to the "Create a Service" page and configure the service parameters as required by referring to the step of [creating a service in the console](https://intl.cloud.tencent.com/document/product/457/36833).
    Configure some key parameters as follows:
![](https://main.qcloudimg.com/raw/5190f97b699f9d0d856aeb0412a9428f.png)
 - **Service Access**: select **LoadBalancer (public network)** or **LoadBalancer (private network)**.
 - **Network Mode**: **Enable CLB-to-Pod Direct Access**.
 - **Workload Binding**: select **Reference Workload**. In the displayed window, select the backend workload of the VPC-CNI mode.
3. Click **Create Service** to complete creation. 
:::
::: YAML operation instructions
The YAML configuration for a service in CLB-to-Pod direct access mode is the same as that for a common service. In this example, the annotation indicates whether to enable the CLB-to-Pod direct access mode.

**Prerequisites**
Add `GlobalRouteDirectAccess: "true"` to the `kube-system/tke-service-controller-config` ConfigMap to enable the direct access capability of GlobalRoute.

```
kind: Service
apiVersion: v1
metadata:
    annotations:
	  service.cloud.tencent.com/direct-access: true ##Enable CLB-to-Pod direct access
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


For the CLB configuration, see [Service CLB Configuration](https://intl.cloud.tencent.com/document/product/457/36834). The annotation configuration is as follows:

```
service.cloud.tencent.com/tke-service-config: [tke-service-configName]
```



:::
</dx-tabs>


