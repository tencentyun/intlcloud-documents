## Overview

To deploy applications in Tencent Kubernetes Engine (TKE) and use static pod IP addresses, you can use StatefulSets with static IP addresses. Pods created by this type of StatefulSet are assigned with an IP in an actual VPC through ENIs. TKE's VPC-CNI plugin assigns IP addresses. The IP addresses remain unchanged after pods are restarted or migrated.
By using StatefulSets with static IP addresses, you can:
- Authorize based on source IP addresses.
- Review processes based on IP addresses.
- Query logs based on pod IP addresses.

>! When StatefulSets with static IP addresses are used, the static IP addresses survive only within the lifecycle of their StatefulSets.

## Prerequisites

You have enabled the VPC-CNI mode for your cluster. For more information, please see [Enabling VPC-CNI for a Cluster](https://intl.cloud.tencent.com/document/product/457/35250).

## Directions

### Using the console
1. Log in to the [TKE console](https://console.qcloud.com/tke2) and click **Cluster** to go to the [cluster](https://console.qcloud.com/tke2/cluster?rid=1) management page.
2. Select the ID or name of the cluster that you want to view to go to the cluster management page.
3. Choose **Workload** > **StatefulSet** to go to the cluster management page of **StatefulSet**.
4. Click **Create** to view **Number of Pods**, as shown below.
![](https://main.qcloudimg.com/raw/0ebc313ec37d0f4dc6506ecbcecd3fc7.png)
5. Click **Advanced Settings** and set StatefulSet parameters as needed. The key parameters are as follows:
   ![Create StatefulSet](https://main.qcloudimg.com/raw/fa66910444475fcab224844c200a217c.png)
 - Network mode: select **Enable VPC-CNI mode**.
 - IP address range: currently, only the **Random** value is supported.
 - Static pod IP: select **Enable**.

### YAML sample

```yaml
apiVersion: apps/v1
kind: StatefulSet
metadata:
  annotations:
    tke.cloud.tencent.com/enable-static-ip: "true"
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
- metadata.annotations: to create StatefulSets with static IP addresses, you need to set annotations, that is, `tke.cloud.tencent.com/enable-static-ip`.
- spec.template.annotations: to create pods in VPC-CNI mode, you need to set annotations, that is, `tke.cloud.tencent.com/networks`.
	- The default value is `Immediate`. After a pod is terminated, the associated IP address is also terminated.
	- To use a static IP address, set it to `Never`. After a pod is terminated, the associated IP address will be retained. When a pod with the same name as the terminated pod is pulled the next time, the original IP address is used.
- spec.template.spec.containers.0.resources: to create pods in VPC-CNI mode, you need to add limits on "requests" and "limits", that is, `tke.cloud.tencent.com/eni-ip`.

