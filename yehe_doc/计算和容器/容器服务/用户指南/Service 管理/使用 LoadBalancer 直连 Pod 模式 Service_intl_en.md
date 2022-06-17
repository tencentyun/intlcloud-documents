## Overview

For a service in native LoadBalancer mode, a Cloud Load Balancer (CLB) can be automatically created. It first forwards traffic to a cluster through the Nodeport of the cluster, and then forwards it again through iptable or ipvs. Services in this mode can meet users' needs in most scenarios, but in the following scenarios, **services in CLB-to-Pod direct access mode** are recommended:

- The source IP needs to be obtained (local forwarding must be enabled for non-direct access mode)
- Higher forwarding performance is required (there are two layers of CLBs when the CLB and service are in non-direct access mode, so performance loss is inevitable).
- Complete health checks and session persistence are required for the Pod layer (there are two layers of CLBs when the CLB and service are in non-direct access mode, so health checks and session persistence are difficult to configure).



> ? 
- If your cluster is EKS, it defaults to the CLB-to-Pod direct access mode, and you don't need to do anything.
- Currently, the CLB-to-Pod direct access mode is available for both GlobalRouter and VPC-CNI container network modes. Click the cluster ID in the [cluster list](https://console.cloud.tencent.com/tke2/cluster?rid=1) to go to the cluster details page. On the **Basic Information** page, you can find the container network add-on used by the current cluster.
>


## VPC-CNI Mode

### Use limits

- The Kubernetes version of the cluster must be 1.12 or later.
- The VPC-CNI ENI mode must be enabled for the cluster network mode.
- The workloads used by a service in direct access mode must adopt the VPC-CNI ENI mode.
- Up to 200 workload replicas can be bound to the CLB backend by default. If you need to bind more replicas, [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category) to increase the quota.
- The feature limits of a CLB bound to an ENI must be satisfied. For more information, see [Binding an ENI](https://intl.cloud.tencent.com/document/product/214/32520).
- When workloads in CLB-to-Pod direct access mode are updated, a rolling update is performed based on the health check status of the CLB, which will affect the update speed.
- HostNetwork type workloads are not supported.

### Directions

<dx-tabs>
::: Console
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. Refer to the steps of [Creating a service in the console](https://intl.cloud.tencent.com/document/product/457/36833) to go to the "Create a service" page and set the service parameters as required.
    Some key parameters need to be set as follows:
    ![](https://qcloudimg.tencent-cloud.cn/raw/eb89c97089982a53ceca2db5d43d7dc4.png)
 - **Service access method**: Select **Public network CLB access** or **Private network CLB access**.
 - **Network mode**: Select **Enable CLB-to-Pod direct access**.
 - **Workload binding**: Select **Reference workload**.
3. Click **Create service**. 
		

:::
::: YAML
The YAML configuration for a service in CLB-to-Pod direct access mode is the same as that for a common service. In this example, the annotation indicates whether to enable the CLB-to-Pod direct access mode.

```
kind: Service
apiVersion: v1
metadata:
  annotations:
    service.cloud.tencent.com/direct-access: "true" ##Enable CLB-to-Pod direct access
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

For the CLB configuration, see [TkeServiceConfig](https://intl.cloud.tencent.com/document/product/457/36834). The annotation configuration is as follows:

```
service.cloud.tencent.com/tke-service-config: [tke-service-configName]
```

:::
</dx-tabs>














### Notes

#### Ensuring the availability during rolling update

ReadinessGate, provided by the official Kubernetes, is mainly used to control the status of Pod, and requires the cluster version to be later than 1.12. By default, a Pod has the following conditions: PodScheduled, Initialized, ContainersReady, when these statuses are all Ready, the Pod Ready passes the conditions. However, in the cloud native scenario, the status of Pods needs to be judged in combination with other factors. `ReadinessGate` provides a mechanism that allows you to add a fence for the Pod's status judgment, which is judged and controlled by a third party. In this way, the status of the Pod is associated with the third party.


#### Changes in the rolling update of CLB-to-Pod direct access mode

When users start the rolling update of an app, Kubernetes will perform the rolling update according to the update policy. However, the identification that it uses to judge whether a batch of Pods have started only includes the status of the Pods themselves, and does not consider whether the Pods are configured with health check in the CLB and have passed it. If such Pods cannot be scheduled in time when the access layer components are under high load, the Pods with successful rolling update may not be providing services to external users, thus resulting in service interruption.
In order to associate the backend status of the CLB and rolling update, the TKE access layer components introduced a new feature: `ReadinessGate`, which was introduced in Kubernetes 1.12. Only when the TKE access layer components confirm that the backend binding is successful and the health check is passed, will it configure the state of `ReadinessGate`, so that Pods can reach the Ready state and the rolling update of the entire workload can be facilitated.

#### Using ReadinessGate in a cluster 


Kubernetes clusters provide a service registration mechanism. You only need to register your services to a cluster in the form of `MutatingWebhookConfigurations` resources. When a Pod is created, the cluster will deliver notifications according to the configured callback path. At this time, the pre-creation operation can be performed for the Pod, that is, `ReadinessGate` can be added to the Pod. This callback process must be based on HTTPS. That is, the CA that issues requests needs to be configured in `MutatingWebhookConfigurations`, and a certificate issued by the CA needs to be configured on the server.

#### Disaster recovery of the ReadinessGate mechanism

The service registration or certificates in user clusters may be deleted by users, although these system component resources should not be modified or destroyed by users. However, such problems will inevitably occur because of users' exploration of clusters or maloperations. Therefore, the integrity of the above resources will be checked when the access layer component is started, and the resources will be rebuilt if the integrity is damaged to strengthen the robustness of the system. For more information, see [Pod readiness](https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/#pod-readiness-gate).














## GlobalRouter Mode 

### Use limits

- A workload can only run in one network mode. You can choose VPC-CNI ENI mode or GlobalRoute mode for the workloads used by a service in direct access mode.
- Only bill-by-IP accounts are supported.
- Up to 200 workload replicas can be bound to the CLB backend by default. If you need to bind more replicas, [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category) to increase the quota.
- When the CLB-to-Pod direct access mode is used, the network linkage is restricted by the security group of CVM. Confirm whether the security group configuration opens the corresponding protocol and port. **The port corresponding to the workload on the CVM needs to be opened.**
- After the CLB-to-Pod direct access mode is enabled, the [ReadinessGate](https://intl.cloud.tencent.com/document/product/457/38368) (readiness check) will be enabled by default. It will check whether the traffic from the load balancer is normal during the rolling update of Pod. You also need to configure the correct health check configuration for the application. For details, see [TkeServiceConfig](https://intl.cloud.tencent.com/document/product/457/36834).
- The CLB-to-Pod direct access in Globalrouter mode is in beta test. You can use it through the following two ways:
 - **You can use it via [CCN](https://intl.cloud.tencent.com/zh/document/product/1003).** (recommended). CCN can verify the bound IP address to prevent common IP binding problems such as binding errors and address loopback. The instructions are as follows:
   1. Create a CCN instance. See [Creating a CCN Instance](https://intl.cloud.tencent.com/document/product/1003/30062).
   2. Add the VPC where the cluster is located to the created CCN instance.
   3. Register the container network CIDR block of the relevant cluster to the CCN. On the cluster's **Basic information** page, enable the **CCN**.
 - **You can also [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category) to apply for the CLB-to-Pod direct access.** This method is not recommended as the IP verification feature, which is available in CCN, is not provided in this case.


### Directions

<dx-tabs>
::: Console
**Prerequisites**
<li>Add `GlobalRouteDirectAccess: "true"` to the `kube-system/tke-service-controller-config` ConfigMap to enable the direct access capability of GlobalRoute.</li>
<li>This feature is only available to beta users of CLB SNAT Pro. To become a beta user, <a href="https://console.intl.cloud.tencent.com/workorder/category">submit a ticket</a>.</li>
<br>

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. Refer to the steps of [Creating a service in the console](https://intl.cloud.tencent.com/document/product/457/36833) to go to the "Create a service" page and set the service parameters as required.
    Some key parameters need to be set as follows:
    ![](https://qcloudimg.tencent-cloud.cn/raw/eb89c97089982a53ceca2db5d43d7dc4.png)
 - **Service access method**: Select **Public network CLB access** or **Private network CLB access**.
 - **Network mode**: Select **Enable CLB-to-Pod direct access**.
 - **Workload binding**: Select **Reference workload**.
3. Click **Create service**. 
:::
::: YAML
The YAML configuration for a service in CLB-to-Pod direct access mode is the same as that for a common service. In this example, the annotation indicates whether to enable the CLB-to-Pod direct access mode.

**Prerequisites**
<li>Add `GlobalRouteDirectAccess: "true"` to the `kube-system/tke-service-controller-config` ConfigMap to enable the direct access capability of GlobalRoute.</li>
<li>This feature is only available to beta users of CLB SNAT Pro. To become a beta user, <a href="https://console.intl.cloud.tencent.com/workorder/category">submit a ticket</a>.</li>
<br>

**Enable the direct access mode in the Service's YAML**

```
kind: Service
apiVersion: v1
metadata:
  annotations:
    service.cloud.tencent.com/direct-access: "true" ##Enable CLB-to-Pod direct access
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


For the CLB configuration, see [TkeServiceConfig](https://intl.cloud.tencent.com/document/product/457/36834). The annotation configuration is as follows:

```
service.cloud.tencent.com/tke-service-config: [tke-service-configName]
```



:::
</dx-tabs>

