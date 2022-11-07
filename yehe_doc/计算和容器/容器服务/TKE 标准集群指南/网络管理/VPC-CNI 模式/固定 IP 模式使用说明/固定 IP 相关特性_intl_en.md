

## Retaining and Reclaiming a Static IP Address

In static IP address mode, after a Pod in VPC-CNI mode is created and used, the network component will create the CRD object `VpcIPClaim` with the same name as the Pod in the same namespace. This object describes the Pod's requirements for the IP address. The network component will then create the CRD object `VpcIP` based on the object and associate it with the corresponding `VpcIPClaim`. `VpcIP` is the name of the actual IP address, indicating that an actual IP address is occupied.

You can run the following command to view IP address usage in the container subnet of the cluster:

```
kubectl get vip
```

For a Pod to which a non-static IP address is bound, `VpcIPClaim` will be terminated and `VpcIP` will be terminated and reclaimed after the Pod is terminated. For a Pod to which a static IP address is bound, `VpcIPClaim` and `VpcIP` will be retained after the Pod is terminated. After the Pod with the same name is started, it will use the `VpcIP` associated with the `VpcIPClaim` with the same name, so as to retain the IP address.

As the network component will look for available IP addresses based on `VpcIP` during IP address allocation in the cluster, static IP addresses need to be reclaimed promptly if not used (the current default policy indicates never to reclaim); otherwise, IP addresses will be wasted, and no IP addresses will be available. This document describes reclaiming after expiration, manual reclaiming, and cascade reclaiming of an IP address.

### Reclaiming after expiration (by default)
On the [**Create Cluster**](https://intl.cloud.tencent.com/document/product/457/30637) page, select **VPC-CNI** for **Container Network Add-on** and **Enable Support** for **Static Pod IP**.
![](https://qcloudimg.tencent-cloud.cn/raw/6ec7190975269a84f2fcecb41a842f78.png)
Set **IP Reclaiming Policy** in **Advanced Settings**. You can set how many seconds after the Pod is terminated to reclaim the static IP address.
![](https://main.qcloudimg.com/raw/85c8ec1b5306333ad9d7af4b3301abab.png)

### Manual reclaiming
For an IP address that urgently needs to be reclaimed, you need to find its Pod and namespace before running the following command to manually reclaim it:
>! You must make sure that the Pod of the IP address to be reclaimed has been terminated; otherwise, the Pod network will become unavailable.
>
```
kubectl delete vipc <podname> -n <namespace>
```


### Cascade reclaiming
Currently, the static IP address is tightly bound to the Pod, regardless of the specific workload (e.g., Deployment and StatefulSet). After the Pod is terminated, it is uncertain when to reclaim the static IP address. TKE has implemented deletion of the static IP address immediately after the workload of the Pod is deleted.

You can enable cascade reclaiming by the following steps:
1. **Run the command `kubectl edit deploy tke-eni-ipamd -n kube-system` to modify the existing tke-eni-ipamd deployment**.
2. Run the following command to add the launch parameter to `spec.template.spec.containers[0].args`.
```yaml
- --enable-ownerref
```
After the modification, IPAMD will automatically restart and take effect. Then, cascade deletion of the static IP address will apply to new workloads but not existing ones.


## FAQs

### What should I do if the EIP cannot be bound and Pods cannot be scheduled to a node in shared ENI mode?

After a node is added to a cluster, IPAMD will try binding an EIP from the subnet in the same AZ as the node (the subnet configured for IPAMD) to the node. If IPAMD becomes abnormal or it is not configured with a subnet in the same AZ as the node, IPAMD cannot allocate a secondary ENI to the node. In addition, if the current VPC uses more secondary ENIs than the upper limit, no secondary ENIs can be allocated to the node.
Run the following command for troubleshooting:
```shell
kubectl get event
```

- If `event` displays `ENILimit`, the quota is not appropriate. You can fix the problem by increasing the quota of ENIs for the VPC.
- Check whether the container subnet in the AZ of the node has sufficient IP addresses, and if not, add some.




### What should I do if the prompt says that the number of ENIs exceeds the upper limit and no ENIs can be allocated for the node?
#### Symptom
The ENIs configured for the node cannot be bound, and the VIP associated with `nec` failed to be attached. View `nec`, and you can see that its status is empty.
Run the following command to view `nec`:
```shell
kubectl get nec -o yaml
```

If the `nec` status of the node is empty, the returned result will be as shown below:
![](https://main.qcloudimg.com/raw/8af59f6b986e844e7aa6dd776f9a0bc0.png)

Run the following command to view the VIP associated with `nec`:
```shell
kubectl get vip -oyaml
```

If the command returns a success result, the VIP status is `Attaching`. The error message is as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/06375d489d671d5d5ddbd93d588e05e7.png)

#### Solution
Currently, up to 1,000 ENIs can be bound to a VPC. To increase the quota, [submit a ticket](https://console.tencentcloud.com/workorder/category) for application. The quota will take effect by region.

