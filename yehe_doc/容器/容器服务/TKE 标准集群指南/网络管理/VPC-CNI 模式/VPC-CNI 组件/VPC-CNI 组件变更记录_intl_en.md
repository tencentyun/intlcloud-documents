
The VPC-CNI component contains three Kubernetes cluster components: `tke-eni-agent`, `tke-eni-ipamd`, and `tke-eni-ip-scheduler`. Generally, their versions are the same. However, `tke-eni-ip-scheduler` is less modified, so its version may be a little earlier.

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
	<td>v3.4.7</td><td>2022-09-07 </td>
    <td>
<li>Supports the preferential scheduling policy of ip-scheduler, where Pods with static IP addresses are preferentially scheduled to the ENIs matching the subnet.</li><li> eni-ipamd supports the dry run to sync existing custom resources (CRs) and promptly discover change exceptions.</li><li>Optimizes the polling logic for ENI-IP address binding to reduce the errors caused by ENIs/IP addresses that are being bound.</li><li>Fixed the occasional issue where internally allocated IP addresses are leaked when shared ENIs are released in non-static IP address mode.</li>
    </td><td>No impact on services</td>
</tr>
<tr>
	<td>v3.4.6</td><td>2022-07-26 </td>
    <td>
<li>Supports the native node pool.</li>
    </td><td>No impact on services</td>
</tr>
<tr>
	<td>v3.4.5</td><td>2022-06-28 </td>
    <td>
<li>The non-static IP address mode of shared ENIs supports IPv4/IPv6 dual-stack. In dual-stack mode, each Pod will be allocated an IPv6 IP address and an IPv4 IP address.</li><li>Fixed the issue where the EIP becomes invalid due to `nodeLost` on super nodes. After the fix, the EIP will be bound again.</li>
    </td><td>No impact on services</td>
</tr>
<tr>
	<td>v3.4.4</td><td>2022-06-06 </td>
    <td>
<li>By default, the EIP is tagged with `tke-clusterId` and `tke-created-eip` and inherits the TKE cluster's tag.</li><li>Supports unbinding ENIs in instances that have been shut down.</li><li>Optimizes ip-scheduler and fixed the issue of slow start due to too many subnets.</li>
    </td><td>No impact on services</td>
</tr>
<tr>
	<td>v3.4.3</td><td>2022-04-13 </td>
    <td>
<li>eni-ipamd and ip-scheduler support disabling subnets. Disabled subnets can be allocated only to specified objects by setting the `--only-nominated-eni-subnets` startup parameter.</li><li> The static IP address mode supports specifying subnets for Pods through the `tke.cloud.tencent.com/nominated-eni-subnets` annotation. Multiple subnets need to be separated by comma.</li><li> eni-agent supports protecting key kernel parameters of the system and adopting new TLinux features to prevent kernel parameters (`rp_filter`and `ip_forward`) from being modified.</li><li> Fixed the occasional issue where the eni-ip resource of the node fails to be registered due to kubelet restart during node initialization in shared ENI mode.</li><li>Fixed the issue where the IP garbage collection mechanism fails due to dockershim or containerd restart during container running.</li>
    </td><td>No impact on services</td>
</tr>
<tr>
	<td>v3.4.2</td><td>2022-03-04 </td>
    <td>
<li>The non-static IP address mode supports specifying the ENI and subnet of the node.</li><li>eni-agent supports automatically setting `ip_forward` and `rp_filter` kernel parameters on schedule to avoid network failures due to their changes.</li><li> Optimizes the scheduling performance. In shared ENI mode, if an ENI is being bound, the polling wait occurs to reduce scheduling failures.</li><li> Fixed the occasional issue where eni-ip extension resources are lost due to high node loads.</li><li>Attempts to delete and recreate the ENI and IP address that are pending for a long time; fixed the issue where the ENI and IP address become unavailable for a long time due to underlying failures.</li>
    </td><td>No impact on services</td>
</tr>
<tr>
	<td>v3.4.1</td><td>2022-01-21 </td>
    <td>
<li>Supports scheduling Pods to TKE Serverless nodes and maintaining the IP address in static IP address mode.</li><li> Supports specifying the EIP through the `tke.cloud.tencent.com/eip-id-list` annotation.</li><li> Supports binding dedicated ENIs to security groups in non-static IP address mode.</li><li> Upgrades the CRD API to v1 and supports Kubernetes 1.22.</li><li>Fixed the occasional issue where the IP status is not synced in static IP address mode.</li>
    </td><td>No impact on services</td>
</tr>
<tr>
	<td>v3.4.0</td><td>2021-12-08 </td>
    <td>
<li> Supports static IP addresses with multiple ENIs.</li><li> Supports underlay connection in and off the hybrid cloud and elastic Pod deployment.</li><li> Fixed the issue of incorrect CNI data plane settings due to occasional CNI concurrency in the same Pod.</li>
</td><td>No impact on services</td>
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
