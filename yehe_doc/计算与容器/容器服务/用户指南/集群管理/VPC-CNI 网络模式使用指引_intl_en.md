## VPC-CNI Introduction
Tencent Kubernetes Engine (TKE) provides the default Global Router network mode, in which, routing can be implemented for container IP addresses (not overlapping with VPC IP ranges) within VPCs based on the global routing capabilities of VPCs. The principle of this mode is that the underlying VPC forwards traffic to the node of the corresponding pod CIDR based on the container IP address, and then the traffic is routed to the pod of the corresponding container IP address through network bridge cbr0, as shown in the figure below:
<img style="width:450px" src="https://main.qcloudimg.com/raw/e94d6f31028d804a346b78be8255a91a.png" data-nonescope="true">
TKE also provides the VPC-CNI network mode. In this mode, an ENI is inserted into each pod, the IP range falls within the VPC IP range, and inter-pod communication is enabled through ENI routing, as shown in the figure below:
<img style="width:450px" src="https://main.qcloudimg.com/raw/24f9223d9cd7c26789f32bc235f56e51.png" data-nonescope="true">

## VPC-CNI Use Cases
Compared with Global Router, the advantages and applicable scenarios of VPC-CNI are as follows:

| Advantage | Applicable Scenario |
|----------------------------------------------------------------|----------------------------------------------------------------|
| Without the need for a network bridge, the network forwarding performance is enhanced by about 10% | This mode is suitable for scenarios with high network latency requirements |
| Support static pod IP addresses | This mode is suitable for scenarios that rely on static container IP addresses, for example, migration from a traditional architecture to a container platform and security policy restrictions on IP addresses |
| Support direct connection between LBs and pods | This mode is suitable for scenarios where direct connection between LBs and pods is desired |

## VPC-CNI Use Limits
- You need to plan a dedicated subnet for containers, and the subnet cannot be shared with other cloud resources, such as CVMs and CLBs.
- Nodes in the cluster must be in the same availability zone as the subnet. If you select an incorrect availability zone when purchasing a node, pods cannot be scheduled.
- The number of pods that can be scheduled in VPC-CNI mode on a node depends on the maximum number of IP addresses that can be bound with the inserted ENIs. Devices with higher configurations allow the insertion of more ENIs. You can view the Allocatable attribute of the node to determine the number of ENIs that can be inserted.


## VPC-CNI Directions
Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
<span id="VPC-CNI"></span>
### Enabling VPC-CNI
TKE provides two methods to enable VPC-CNI:
- Method 1: when creating a cluster, select the VPC-CNI network plug-in, as shown in the figure below:
![](https://main.qcloudimg.com/raw/f85f024cd4ae534685a7b3127c58f360.png)
>! When using [Method 1](#VPC-CNI) to enable VPC-CNI, choose **Advanced Settings** > **Configure IP Repossession Policy**.

- Method 2: when creating a cluster, select the Global Router network plug-in. On the basic information page of the cluster, enable the VPC-CNI mode (by default, both modes are enabled), as shown in the figure below:   
![](https://main.qcloudimg.com/raw/e01e2d163cca413ed7d9acc2d7ce0b60.png)
In static-IP scenarios, after enabling VPC-CNI, you need to configure the IP repossession policy, which specifies how long after pods are terminated their IP addresses are returned. Pods with non-static IP addresses are not affected by these settings because their IP addresses are immediately released upon pod termination, as shown in the figure below:<br>
<img style="width:350px" src="https://main.qcloudimg.com/raw/2b682377dab2503431213171de61b258.png" data-nonescope="true">



### Using VPC-CNI
>! 
To use VPC-CNI, ensure that rp_filter is disabled. The following shows a sample code:
``` bash
sysctl -w net.ipv4.conf.all.rp_filter=0
sysctl -w net.ipv4.conf.default.rp_filter=0
```
The `tke-cni-agent` component automatically configures the node kernel parameters. If you manually configure the kernel parameters and enable rp_filter, network connection will fail.
>
>- If you use [Method 1](#VPC-CNI) to enable VPC-CNI and create a workload in the console or by using YAML, the pods all use ENIs by default.   
>- If you use [Method 2](#VPC-CNI) to enable VPC-CNI (both Global Router and VPC-CNI are enabled), the pods do not use ENIs by default. In this case, take note of the following items:
  - When you create a workload in the console, VPC-CNI supports only the StatefulSet type. Choose **Advanced Settings** > **Use VPC-CNI Mode**, as shown in the figure below:
    <img style="width:450px" src="https://main.qcloudimg.com/raw/7f910787d72379ca5d00b090391e6e73.png" data-nonescope="true">
  - VPC-CNI supports any type of workload created using YAML. In this case, you only need to add an annotation, namely `tke.cloud.tencent.com/networks: "tke-route-eni"`, for pods and add requests and limits for one of the containers, such as `tke.cloud.tencent.com/eni-ip: "1"`. The following shows a sample code:
   ``` yaml
   apiVersion: apps/v1
   kind: Deployment
   metadata:
     name: nginx
     labels:
       app: nginx
   spec:
     replicas: 1
     selector:
       matchLabels:
         app: nginx
     template:
       metadata:
         annotations:
           tke.cloud.tencent.com/networks: "tke-route-eni"
         labels:
           app: nginx
       spec:
         containers:
           - name: nginx
             image: nginx
             resources:
               requests:
                 tke.cloud.tencent.com/eni-ip: "1"
               limits:
                 tke.cloud.tencent.com/eni-ip: "1"
   ```


### Static pod IP addresses 

The static IP feature is only applicable to StatefulSet-type workloads. You can enable static IP addresses by using the following two methods:
- Method 1: when creating a workload in the console, enable static IP addresses, as shown in the figure below:
    <img style="width:450px" src="https://main.qcloudimg.com/raw/266ca1346994c7f84ee27de9c09a0169.png" data-nonescope="true">
- Method 2: when creating a workload by using YAML, add an annotation, namely `tke.cloud.tencent.com/vpc-ip-claim-delete-policy: Never`, for the StatefulSet. The following shows a sample code:
   ``` yaml
   apiVersion: apps/v1beta1
   kind: StatefulSet
   metadata:
     name: busybox
   spec:
     serviceName: "busybox"
     replicas: 1
     template:
       metadata:
         annotations:
           tke.cloud.tencent.com/networks: tke-route-eni
           tke.cloud.tencent.com/vpc-ip-claim-delete-policy: Never
         labels:
           app: busybox
       spec:
         terminationGracePeriodSeconds: 0
         containers:
         - name: busybox
           image: busybox
           command: ["sleep", "10000000000"]
           resources:
             requests:
               tke.cloud.tencent.com/eni-ip: "1"
             limits:
               tke.cloud.tencent.com/eni-ip: "1"
   ```


### Modifying the IP repossession policy 

If you configure the IP repossession policy when enabling VPC-CNI, you can modify the policy later by manually modifying the launch parameter of the ipamd component, namely `kubectl -n kube-system edit deployments.v1.apps tke-eni-ipamd`. The following shows a sample code:
``` yaml
    spec:
      containers:
      - args:
        - --clusterid
        - cls-kjqul1ir
        - --claim-expired-duration
        - 10m0s
```
>! Change `--claim-expired-duration` to the specified value.

### Expanding the IP capacity

If the number of subnet IP addresses for VPC-CNI is insufficient, you can manually modify the configuration of the ipamd component to add subnets. To do this, edit configmap of `tke-eni-ipamd` under the `kube-system` namespace, namely `kubectl -n kube-system edit configmap tke-eni-ipamd`. The following shows a sample code:
``` yaml
apiVersion: v1
kind: ConfigMap
metadata:
  namespace: kube-system
  name: tke-eni-ipamd
data:
  TKE_ENI_IPAMD_SUBNET_ID: subnet-4k3fdq3f:subnet-aa7clla5
  TKE_ENI_IPAMD_VPC_ID: vpc-409o11tu
```
>!
>- Add the IDs of the subnets to be added to `TKE_ENI_IPAMD_SUBNET_ID` and separate them with colons (`:`). Note that the subnets to be added must be empty, that is, they do not contain any cloud resources such as CVMs and CLBs. Otherwise, a conflict will occur.
>- If a configuration exists for TKE_ENI_IPAMD_ZONE, ignore it. This configuration has been discarded.
>- After modifying the configuration of the ipamd component, you must run the following command to delete and rebuild the ipamd pod so that the modification can take effect:
  ```
  kubectl -nkube-system get po -ocustom-columns=Name:.metadata.name | grep ipamd | kubectl -nkube-system delete po
  ```



## References
- [How to Choose a TKE Network Mode](https://intl.cloud.tencent.com/document/product/457/35248)
- [GlobalRouter VPC-CNI Mode Description](https://intl.cloud.tencent.com/document/product/457/35250)
- [Managing StatefulSets with Static Pod IP Addresses](https://intl.cloud.tencent.com/document/product/457/35249)
