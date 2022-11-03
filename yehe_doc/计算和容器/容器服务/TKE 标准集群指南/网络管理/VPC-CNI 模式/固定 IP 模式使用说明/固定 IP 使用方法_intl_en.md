
## Overview 

This mode is suitable for scenarios that rely on static container IP addresses, for example, migrating a traditional architecture to a container platform and performing security policy restrictions on IP addresses. The static IP address mode is not recommended for services without IP address limits.

## Features and Limitations

- The static IP address is achieved by retaining the associated IP address when the Pod is terminated, or keeping the IP unchanged when the Pod is migrated.
- Pods in a cluster can be in different subnets, but Pods with static IP addresses cannot be scheduled across node availability zones and across subnets.
- The IP address of Pod can automatically associate with EIP, thus Pod can be accessed via internet.
- For the static IP addresses with shared ENI, when the Pod with static IP address is terminated, its IP address is only retained in the cluster. If other clusters or services (such as CVM, CDB, CLB) use the same subnet, the retained static IP address may be occupied, and the Pod will be unable to obtain the IP address when it being restarted. **Please ensure that the container subnet of this mode is exclusively used.**

## How to Use

You can enable the static IP address using either of the following methods:
- Select VPC-CNI with static IP address when creating a cluster
- Enable VPC-CNI with static IP address for GlobalRouter mode


### Selecting static IP address of VPC-CNI mode when creating a cluster
>? If you use this method to enable VPC-CNI, when you create a workload on the console or through YAML, all Pods will use ENIs by default.
>
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and select **Cluster** on the left sidebar.
2. On the "Cluster management" page, click **Create** above the cluster list.
3. On "Create Cluster" page, select **VPC-CNI** for **Container Network Add-on**.
4. Select **VPC-CNI** for "Container Network Add-on". Check **Enable Support** for **Static Pod IP**, as shown in the figure below:
![](https://qcloudimg.tencent-cloud.cn/raw/6ec7190975269a84f2fcecb41a842f78.png)


### Enabling VPC-CNI with static IP address for GlobalRouter mode
#### Enabling VPC-CNI for the existing clusters
>?
>- Enable VPC-CNI Mode with static IP address for GlobalRouter, that is, when creating a cluster, you select the Global Router network add-on, and then enable the VPC-CNI mode (both modes can be used at the same time by default) on the basic information page of the cluster.
>- If you use this method to enable VPC-CNI, the Pods cannot use ENIs by default.
>
1. Log in to the [TKE console](https://console.qcloud.com/tke2) and select **Cluster** on the left sidebar.
2. On "Cluster Management" page, select the ID of the cluster for which VPC-CNI needs to be enabled and go to its details page.
3. On the cluster details page, click **Basic Information** on the left.
4. In the **Node and Network Information** section, enable **VPC-CNI mode**.
5. In the pop-up window, select **Enable Support**, confirm the IP address reclaim policy, and select the subnet as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/22d8257099799f8a527d07eeefcb5602.png)
>! 
>- For scenarios that use static IP addresses, when enabling VPC-CNI, you need to set the IP reclaiming policy to specify when to reclaim the IP addresses after Pods are terminated.
>- Pods with non-static IP addresses are not affected by these settings because their IP addresses are immediately released upon Pod termination. These IP addresses are not returned to the VPC, but returned to the IP address pool managed by the container.
6. Click **Submit** to enable VPC-CNI mode for the cluster.


#### Creating StatefulSets with static Pod IP addresses
In GlobalRouter mode with VPC-CNI enabled, if you have applications to deploy in TKE, which need to use the static Pod IP addresses, you can create a StatefulSets with static IP addresses. Pod created by this type of StatefulSet are assigned with an actual IP address in the VPC through an ENI. The IP addresses are assigned by TKE VPC-CNI add-on. So that when the Pod is restarted or migrated, the IP address can be unchanged.

By using StatefulSets with static IP addresses, you can:
- Authorize based on source IP addresses.
- Review processes based on IP addresses.
- Query logs based on Pod IP addresses.

>!When StatefulSets with static IP addresses are used, the static IP addresses survive only within the lifecycle of their StatefulSets.
>
You can create the static IP address using either of the following methods:
- Creating StatefulSets with Static IP Addresses via TKE console
  1. Log in to the [TKE console](https://console.qcloud.com/tke2) and select **Cluster** on the left sidebar.
  2. Select a cluster ID that needs to use the static IP address and go to its management page.
  3. Choose **Workload** > **StatefulSet** to go to the cluster management page for StatefulSet.
  4. Click **Create** and view **Number of Instances**, as shown in the figure below.
      ![](https://main.qcloudimg.com/raw/0ce9969c685d732aed4103f91e8ffe41.png)
  5. Click **Advanced Settings** and set **StatefulSet** parameters as needed. The key parameters are as follows:
      ![](https://main.qcloudimg.com/raw/ce1bb9d7f0df7b07db6a7d66da115eb8.png)
   - Network mode: select **Enable VPC-CNI mode**.
      - IP address range: currently, only the **Random** value is supported.
      - Static pod IP: select **Enable**.

- Creating via YAML
```yaml
apiVersion: apps/v1
kind: StatefulSet
metadata:
  labels:
    k8s-app: busybox
  name: busybox
  namespace: default
spec:
  replicas: 3
  selector:
    matchLabels:
      k8s-app: busybox
      qcloud-app: busybox
  serviceName: ""
  template:
    metadata:
      annotations:
        tke.cloud.tencent.com/networks: "tke-route-eni"
        tke.cloud.tencent.com/vpc-ip-claim-delete-policy: Never
      creationTimestamp: null
      labels:
        k8s-app: busybox
        qcloud-app: busybox
    spec:
      containers:
      - args:
        - "10000000000"
        command:
        - sleep
        image: busybox
        imagePullPolicy: Always
        name: busybox
        resources:
          limits:
            tke.cloud.tencent.com/eni-ip: "1"
          requests:
            tke.cloud.tencent.com/eni-ip: "1" 
```
  - spec.template.annotations: `tke.cloud.tencent.com/networks: "tke-route-eni"` indicates that the Pod uses the VPC-CNI mode with shared ENI. If you use the VPC-CNI mode with independent ENI, please modify the value to `"tke-direct-eni"`.
  - spec.template.annotations: to create Pods in VPC-CNI mode, you need to set the annotation `tke.cloud.tencent.com/vpc-ip-claim-delete-policy`. Its default value is “Immediate”, that is, when a Pod is terminated, the associated IP address is also terminated. To use a static IP address, set it to “Never”, that is, a Pod is terminated, but the associated IP address will be retained. When a Pod with the same name as the terminated Pod is pulled the next time, the original IP address is used.
  - spec.template.spec.containers.0.resources: to create Pods with shared ENI in VPC-CNI mode, you need to add "requests" and "limits", that is, `tke.cloud.tencent.com/eni-ip`. If you are using the VPC-CNI mode with independent ENI, add `tke.cloud.tencent.com/direct-eni`.
