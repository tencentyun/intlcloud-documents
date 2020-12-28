
## Overview

This mode is suitable for scenarios that rely on static container IP addresses. For example, migration from a traditional architecture to a container platform and security policy restrictions on IP addresses. It is not recommended to use the static IP address mode for services without IP limits.

## Features and Limitations

- It supports that after a pod is terminated, the associated IP address will be retained, and the IP addresses remain unchanged after pods are migrated, so as to implement the static IP address.
- It supports multiple subnets but does not support cross-subnet scheduling of Pod with static IP address, so Pod with static IP address does not support cross-AZ scheduling.
- It supports that Pod IP is automatically associated with EIP IP, thus Pod can be accessed via internet.
- In the static IP address mode with shared ENI, after the Pod with static IP address is terminated, its IP is only retained in the cluster. If other clusters or services (such as CVM, CDB, CLB) use the same subnet, the retained static IP address may be occupied, and the Pod will be unable to obtain the IP when restarting. **Please ensure that the container subnet of this mode is exclusively used.**

## Usage

You can enable the static IP address using either of the following methods:
- Select VPC-CNI mode with static IP address when creating a cluster
- GlobalRouter VPC-CNI Mode with static IP address


### Selecting VPC-CNI mode with static IP address when creating a cluster
>? If you use this method to enable VPC-CNI and create a workload on the console or using YAML, the pods all use ENIs by default.

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **Cluster** in the left sidebar.
2. On the "Cluster Management" page, click **Create** above the cluster list.
3. On **Create Cluster** page, select **VPC-CNI** for **Container Network Add-on**.
4. Check **Enable Support** for **Static Pod IP**.


### GlobalRouter VPC-CNI Mode with static IP address
#### Enabling VPC-CNI for the existing clusters
>?
>- GlobalRouter VPC-CNI Mode with static IP address, that is, when creating a cluster, select the Global Router network plug-in. On the basic information page of the cluster, enable the VPC-CNI mode (by default, both modes are enabled).
>- If you use this method to enable VPC-CNI, the pods do not use ENIs by default.

1. Log in to the [TKE console](https://console.qcloud.com/tke2) and select **Cluster** in the left sidebar.
2. On **Cluster Management** page, select a cluster ID that needs to enable VPC-CNI and go to its details page.
3. On the cluster details page, click **Basic Information** on the left.
4. In the **Node and Network Information** section, enable **VPC-CNI mode**.
5. Select the subnet and set the **IP Reclaiming Policy** in the pop-up window.

>! 
>- In static-IP scenarios, after enabling VPC-CNI, you need to set the IP reclaiming policy, which specifies how long after pods are terminated their IP addresses are returned.
>- Pods with non-static IP addresses are not affected by these settings because their IP addresses are immediately released upon pod termination.
6. Click **Submit**.


#### Creating StatefulSets with Static Pod IP Addresses
In GlobalRouter VPC-CNI Mode, to deploy applications in TKE and use static pod IP addresses, you can use StatefulSets with static IP addresses. Pods created by this type of StatefulSet are assigned with an IP in an actual VPC through ENIs. TKE's VPC-CNI plugin assigns IP addresses. The IP addresses remain unchanged after pods are restarted or migrated.

By using StatefulSets with static IP addresses, you can:
- Authorize based on source IP addresses.
- Review processes based on IP addresses.
- Query logs based on pod IP addresses.

>! When StatefulSets with static IP addresses are used, the static IP addresses survive only within the lifecycle of their StatefulSets.

You can create the static IP address using either of the following methods:
- Creating StatefulSets with Static IP Addresses on TKE console
 1. Log in to the [TKE console](https://console.qcloud.com/tke2) and select **Cluster** in the left sidebar.
 2. Select a cluster ID that needs to use the static IP address and go to its management page.
 3. Choose **Workload** > **StatefulSet** to go to the cluster management page of **StatefulSet**.
  4. Click **Create** to view **Number of Pods**.
  5. Click **Advanced Settings** and set StatefulSet parameters as needed. 
   - Network mode: select **Use VPC-CNI mode**.
      - IP address range: currently, only the **Random** value is supported.
      - Static pod IP: select **Enable**.

- Creating using YAML
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
 - spec.template.annotations: `tke.cloud.tencent.com/networks: "tke-route-eni"` indicates that the Pod uses the VPC-CNI mode with shared ENI. If you are using the VPC-CNI mode with independent ENI, please modify the value to `"tke-direct-eni"`.
 - spec.template.annotations: to create pods in VPC-CNI mode, you need to set annotations, that is, `tke.cloud.tencent.com/vpc-ip-claim-delete-policy`. The default value is “Immediate”. After a pod is terminated, the associated IP address is also terminated. To use a static IP address, set it to “Never”. After a pod is terminated, the associated IP address will be retained. When a pod with the same name as the terminated pod is pulled the next time, the original IP address is used.
 - spec.template.spec.containers.0.resources: to create pods in VPC-CNI mode with shared ENI, you need to add limits on "requests" and "limits", that is, `tke.cloud.tencent.com/eni-ip`. If you are using the VPC-CNI mode with independent ENI, add `tke.cloud.tencent.com/direct-eni`.
