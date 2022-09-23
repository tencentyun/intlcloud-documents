

## Retention and Reclamation of Static IP Address

In static IP address mode, after a Pod that uses the VPC-CNI mode is created, the network component will create a CRD object with the same name `VpcIPClaim` in the same namespace for the Pod. This object describes the Pod's requirements for IP. The network component will then create a CRD object `VpcIP` based on this object and associate it with the corresponding `VpcIPClaim`. `VpcIP` is named after the actual IP address, indicating that the actual IP address is occupied.

You can run the following command to view the usage of the IP in the container subnet used by the cluster.

```
kubectl get vip
```

For Pods with non-static IP addresses, the `VpcIPClaim` will be terminated upon Pod termination, and then the `VpcIP` will be terminated and reclaimed. For Pods with static IP addresses, the `VpcIPClaim` is still retained after the Pod is terminated, and so is the `VpcIP`. After the Pod with the same name is started, it uses the `VpcIP` associated with the `VpcIPClaim` of the same name to implement the IP address retention.

As the network component will search for available IPs based on the information of `VpcIP` when assigning IP within the cluster, the static IP address needs to be reclaimed in time if it is not used to avoid IP waste and no IP available (the current default policy is never to reclaim). This document introduces IP reclamation methods for reclamation after expiration, manual reclamation, and cascading reclamation.

### Reclamation after expiration (by default)
On [Creating a Cluster](https://intl.cloud.tencent.com/document/product/457/30637) page, select **VPC-CNI** for **Container Network Add-on** and check **Enable Support** for **Static Pod IP**.
Set **IP Reclaiming Policy** in **Advanced Settings**. You can set how many seconds after the Pod is terminated to reclaim the static IP address.

### Manual reclamation
For IP addresses that need to be reclaimed urgently, you need to ensure that the IP to reclaim is occupied by which Pod, find the namespace and name of the corresponding Pod, and run the following command to manually reclaim.
>! Please make sure that the Pod corresponding to the reclaimed IP has been terminated, otherwise the Pod network will become unavailable.
>
```
kubectl delete vipc <podname> -n <namespace>
```


### Cascading reclamation
Currently, the static IP address is bound to a Pod, regardless of the specific workload (e.g., Deployment, Statefulset). After the Pod is terminated, it is uncertain when to reclaim the static IP address. TKE has implemented that the static IP address was deleted once the workload to which the Pod belongs was deleted.

The following steps describes how to enable cascading reclamation:
1. Modify the existing **tke-eni-ipamd deployment: `kubectl edit deploy tke-eni-ipamd -n kube-system`**.
2. Run the following command to add the launch parameter to `spec.template.spec.containers[0].args`.

```yaml
- --enable-ownerref
```
After modification, ipamd will automatically restart and take effect. After ipamd takes effect, the new workloads can implement the cascading deletion of the static IP address, which is not supported for the existing Workload.

## Characteristics

### Pod IP in shared ENI mode is automatically associated with EIP

Currently, the static IP address mode that shares ENI supports Pod IP automatically associate with EIP by default.
See the following Yaml example to associate with EIP:
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
        tke.cloud.tencent.com/eip-attributes: ""
        tke.cloud.tencent.com/eip-claim-delete-policy: "Never"
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
            tke.cloud.tencent.com/eip: "1"
          requests:
            tke.cloud.tencent.com/eni-ip: "1"
            tke.cloud.tencent.com/eip: "1"
```

- **spec.template.annotations: tke.cloud.tencent.com/eip-attributes: ""** indicates that the Pod of the Workload needs to associate with EIP.
- **spec.template.annotations: tke.cloud.tencent.com/eip-claim-delete-policy: "Never"** indicates that the EIP of the Pod for Workload is also a static IP address, and it cannot be changed after the Pod is terminated. If it is not a static IP address, do not add the annotation.
- **spec.template.spec.containers.0.resources**: Pod that associates with EIP. You need to add limits on “requests” and “limits”, that is, `tke.cloud.tencent.com/eip`, so that the scheduler can ensure that the nodes scheduled by the Pod still have EIP resources available.
>! The EIP resources that each node can bind to are subject to the relevant quota restrictions and the bound number of CVMs.
The maximum number of EIPs that each node can bind to is **the bound number of CVMs - 1**.


## FAQs

### Nodes cannot be assigned to ENI, and Pod cannot be scheduled normally (in shared ENI mode)

When the node is added to the cluster, ipamd will try to bind an ENI to the node from the subnet in the same AZ as the node (the subnet configured for ipamd). If ipamd is abnormal or no subnet with the same AZ as the node is configured for ipamd, ipamd will be unable to assign a secondary ENI to the node. In addition, if the number of secondary ENIs used by the current VPC exceeds the upper limit, the node cannot be assigned a secondary ENI.
Run the following command for troubleshooting:
```shell
kubectl get event
```

- If “ENILimit” is displayed in the event, it is a quota problem. You can increase the quota of ENIs for the VPC.

- If the following information is displayed in the event, it indicates that the IPs in the subnet are insufficient.

  ![](https://main.qcloudimg.com/raw/3a7b70c880ddd7d48e8404a47ac6c14d.png)

Run the following command to get the usage number of IPs for the current subnet.

```shell
kubectl get vip | wc -l
```

If the number of subnet IPs is sufficient, but there are still problems, it may be related to the underlying soft limits. The analysis is as follows:
Take a high-spec model (the ENI associated with each node can assign an additional 29 IPs) and the configured subnet is `/23` as an example. When the cluster has 17 nodes, in theory, IP resources that are available for these nodes are 17 * (29 + 1), which have exceeded 500, and the subnet of `/23` can be filled. At this time, ipamd will no longer assign ENIs to the new node. To solve this problem, you can add some subnets. The ENIs can be created in the new subnets and bound to the new nodes. Although the new nodes can join the cluster, the Pod will not schedule the nodes that are not bound to the ENIs.
If there are no restrictions, more nodes there are, the less IPs that can be assigned to Pod. The ENI itself will occupy a primary IP, which cannot be assigned to Pod. Therefore, when a node is added, there will be one less IP that the subnet can assign to the Pod. In extreme cases, the secondary ENIs assigned to the nodes are concentrated in a subnet, which will limit the size of the Pod in the entire cluster. This situation can only be restored by draining the legacy nodes, adding the subnets, and then adding the node to the cluster.


### The ENI cannot be assigned to the node, and it prompts that the number of ENIs exceeds the limit
#### Error description
The ENI configured for the node cannot be bound to, and the “nec” fails to associate with “vip attach”. When you check “nec”, you find that the “nec status” associated with the node is empty.
Run the following command to check “nec”.
```shell
kubectl get nec -o yaml
```

When the “nec status” associated with the node is empty, the returned result is as shown in the figure below:
![](https://main.qcloudimg.com/raw/8af59f6b986e844e7aa6dd776f9a0bc0.png)

Run the following command to check the VIP associated with “nec”:
```shell
kubectl get vip -oyaml
```

If the command returns successfully, there will be an error that the VIP status is Attaching, as shown in the figure below:
![](https://main.qcloudimg.com/raw/a46a0ec8be41d520038269c43f823d1c.png)

#### Solutions
Currently, ENI supports that one VPC can bind up to 50 ENIs. Please [submit a ticket](https://console.cloud.tencent.com/workorder/category) to apply to increase this quota. The quota takes effect based on regions.
