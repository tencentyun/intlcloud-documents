
VPC-CNI component contains three kubernetes cluster components: `tke-eni-agent`, `tke-eni-ipamd` and `tke-eni-ip-scheduler`. Generally, the versions of these components are the same. However, `tke-eni-ip-scheduler` is less modified, so its version may be a little earlier.

## Checking the Component Version

The component version is the image tag. You can check it via the kubernetes API.
```
# Checking the version of tke-eni-agent
kubectl -nkube-system get ds tke-eni-agent -o jsonpath={.spec.template.spec.containers[0].image}
# Checking the version of tke-eni-ipamd
kubectl -nkube-system get deploy tke-eni-ipamd -o jsonpath={.spec.template.spec.containers[0].image}
# Checking the version of tke-eni-ip-scheduler
kubectl -nkube-system get deploy tke-eni-ip-scheduler -o jsonpath={.spec.template.spec.containers[0].image}
```

## Change Records



<table>
<tr>
	<th style="width:13%">Version Number</th><th>Release Date</th><th>Updates</th><th>Impacts</th>
</tr>
<tr>
	<td>v3.3.9</td><td>2021-11-09 </td>
    <td>
<li> Fixed repeat creation of an EIP caused by the network.</li><li> Pods with independent ENIs in non-static IP address mode can be bound to an EIP.</li><li> Optimizes the mechanism of expansion resources for eni-agent to make the management of expansion resources more stable and robust.</li><li> Fixed the issues caused by inconsistency between quota set for the node and the actual quota.</li><li> Optimizes IP garbage collection mechanism for eni-agent. If there is a dirty container in the Pod that is being created, the reclaimed IPs will be allocated to a new container in the Pod.</li><li> Optimizes the calculating method for resources of the used IPs and ENIs in non-static IP address mode. Fixed the issue of inaccurate calculation of resources caused by the Pod status of `Error`, `Evicted` and `Completed` etc.</li>
</td><td>No impact on services</td>
</tr>
<tr>
	<td>v3.3.8</td><td>2021-08-17 </td>
    <td>
<li> `--master` can configure the backend kube-apiserver address without relying on kube-proxy.</li><li> eni-agent supports `--kube-client-qps` and `--kube-client-burst` to configure `QPS` and `Burst` of kube client, and the default values increase to 10 and 20 respectively.</li><li> If eni-agent finds that the updated expansion resources are less than original ones, it will update the latest expansion resources information in the node status to prevent issues caused by async updating of kubelet.</li></td><td>No impact on services</td>
</tr>
<tr>
	<td>v3.3.7</td><td>2021-08-13 </td>
    <td>

<li> eni-ipamd supports `--enable-node-condition` and `--enable-node-taint`. If `eni-ip` or `direct-eni` is missed on the node after enabling, the condition or taints of the node will be set.</li><li> EIP supports parsing new API parameters in json format.</li><li> Fixed the issue where the allocated IPs may be reclaimed improperly by garbage collection of eni-agent in containerd runtime.</li><li> Fixed ipamd panic that may be caused by the EIP API.</li><li> Fixed the issue where an ENI is unbound because `disable-node-eni` annotation is set improperly when the non-static IP mode is upgrading.</li>
</td><td>No impact on services</td>
</tr>
<tr>
	<td>v3.3.6</td><td>2021-07-26 </td>
    <td>
<li> Fixed the issue where the allocated IPs and routes may be reclaimed improperly because of the garbage collection mechanism of eni-agent.</li><li> Fixed the issue where IPs may be released before the Pod when deleting deployment and other upper-layer resources after `--enable-ownerref` is enabled for eni-ipamd.</li>
    </td><td>No impact on services</td>
</tr>
<tr>
	<td>v3.3.5</td><td>2021-07-20 </td>
    <td>
<li> Fixed the issue where locally stored data of the Pod cannot be deleted because of improper deletion of the IPs or ENIs of the Pod with a shared ENI/exclusive ENI in non-static IP address mode.</li><li> Fixed the issue where CNI information of a shared ENI/exclusive ENI does not store and verify ENI information of the Pod in non-static IP address mode.</li>
    </td><td>No impact on services</td>
</tr>
<tr>
	<td>v3.3.4</td><td>2021-07-07 </td>
    <td>
<li> Fixed the issue where the component continues trying to unbind the ENI in the condition that the CVM has shut down.</li><li> Fixed the panic caused by the concurrent writes of asynchronous logs.</li><li> Optimizes the ENI synchronization logic in non-static IP address mode to ensure internal data consistency and prevent the ENIs in use from being unbound.</li><li> Fixed the issue where the existing nodes cannot allocate IPs caused by insufficient IPs in the subnet of the cluster upgrading from v3.2 in non-static IP address mode.</li><li> Fixed the issue where the ENI may be incorrectly released when the primary IP of the existing ENI is being used by the Pod.</li>
    </td><td>No impact on services</td>
</tr>
<tr>
	<td>v3.3.3</td><td>2021-06-07 </td>
    <td>
<li> Supports hybrid cloud ipam, and it can work in collaboration with the cilium overlay/underlay mode.</li>
    </td><td>No impact on services</td>
</tr>
</tr>
<tr>
	<td>v3.3.2</td><td>2021-06-01 </td>
    <td>
<li> ip-scheduler supports occupancy caused by insufficiency of default resources, and does not support occupancy caused by insufficiency of IP resources.</li><li> The security group feature logic of the shared ENI is reconstructed. It supports strong synchronization with the security group set on the node to ensure that the binding sequence and priority of security groups is consistent with that in user’s settings.</li><li> Supports the cilium cni-chain mode.</li><li> For eni-agent, `hostPort` field can be configured for the Pod after `--port-mapping` is enabled.</li><li> The annotation `tke.cloud.tencent.com/claim-expired-duration` can be added to the Pods to reclaim static IPs in specific time. The annotation only affects the added Pods.</li>
    </td><td>No impact on services</td>
</tr>
<tr>
	<td>v3.3.1</td><td>2021-05-11 </td>
    <td>
<li> Multiple ENIs can be used in shared ENI non-static IP address mode.</li><li> Tencent Cloud API can call API QPS limits, and the limit for a single cluster is 50 QPS by default (limit by the type of CVM, VPC and TKE).</li><li> Changes of IP quota can be perceived after upgrading of non-static IP address mode.</li><li> The annotation `tke.cloud.tencent.com/desired-route-eni-pod-num` can be added for `node`. The desired number of route-eni ip can be written and the node quota will be adjusted automatically by the component after the writing.</li><li> Fixed the issue of VPC task polling timeout caused by the fact that the VPC task does not exist.</li><li> Fixed the issue of eni-ipamd panic caused by failure of task creation for the ENI.</li><li> Optimizes routing reconciliation logic and only clears the IP routes managed by eni-agent.</li><li> Fixed the issue of exceptional panic occurred at the time of ENI releasing in the independent ENI non-static IP address mode caused by the fact that the ENI has already been released.</li>
    </td><td>No impact on services</td>
</tr>
<tr>
	<td>v3.3.0</td><td>2021-04-13 </td>
    <td>
<li> Supports customized GR mode. Multiple CIDR blocks can be set in a node and a cluster.</li>
    </td><td>No impact on services</td>
</tr>
<tr>
	<td>v3.2.6</td><td>2021-03-31 </td>
    <td>
<li> Reduces the time of retrying for binding an ENI in exclusive ENI mode and improves binding efficiency.</li><li> Reduces failures of concurrent binding and unbinding of ENIs, and improves the efficiency of binding and unbinding through concurrency control.</li><li> Optimizes subnet allocation logic for an ENI in non-static IP address mode. Fixed the issue where some nodes cannot obtain IPs in the condition that IPs are sufficient when the nodes are added concurrently.</li><li> The garbage collection mechanism of eni-agent supports self-awareness of the underlying runtime and supports containerd.</li>
    </td><td>No impact on services</td>
</tr>
<tr>
	<td>v3.2.5</td><td>2021-02-22 </td>
    <td>
<li> dnsConfig is added when eni-ipamd and ip-scheduler are deployed to avoid the issues caused by the DNS that are created by users.</li><li> In the shared ENI static IP address mode, the information of subnetID of the ENI that is bound to each node will be synced to the label of the node, and the key is `tke.cloud.tencent.com/route-eni-subnet-ids`.</li><li> eni-agent will try to obtain the reasons for failures of IP allocation and return them to the CNI plugin to make them reflect in the Pod event.</li><li> A bare Pod can specify an IP through the annotation `tke.cloud.tencent.com/nominated-vpc-ip`.</li><li> eni-agent supports periodic test for the connection with APIServer. It will restart automatically if a timeout occurs.</li><li> Fixed the waste of IPs caused by internal data inconsistency.</li>
    </td><td>No impact on services</td>
</tr>
</table>
