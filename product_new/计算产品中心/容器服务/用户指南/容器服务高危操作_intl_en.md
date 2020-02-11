When deploying or running business, you may trigger high-risk operations at different levels, leading to service failures to different degrees. To help you estimate and avoid operational risks, this document describes the consequences of the high-risk operations and corresponding solutions. Below you can find the high-risk operations you may trigger when dealing with clusters, networking and load balancing, logs, and cloud disks.

## Clusters

<table>
	<tr>
	<th>Category</th>
	<th>High-risk Operation</th>
	<th>Consequence</th>
	<th>Solution</th>
	</tr>
	<tr>
	<td rowspan=8>Master and etcd nodes</td>
	<td>Modifying the security groups of nodes in a cluster</td>
	<td>Master node may become unavailable</td>
	<td>Configure security groups as recommended by Tencent Cloud</td>
	</tr>
	<tr>
	<td>Node expires or is terminated</td>
	<td>The master node becomes unavailable</td>
	<td>Unrecoverable</td>
	</tr>
	<tr>
	<td>Reinstalling operating system</td>
	<td> Master components get deleted</td>
	<td>Unrecoverable</td>
	</tr>
	<tr>
	<td>Upgrading master or etcd component version on your own</td>
	<td>Cluster may become unavailable</td>
	<td>Roll back to the original version</td>
	</tr>
	<tr>
	<td>Deleting or formatting core directory data such as node <code>/etc/kubernetes</code></td>
	<td>The master node becomes unavailable</td>
	<td>Unrecoverable</td>
	</tr>
	<tr>
	<td>Changing node IP </td>
	<td>The master node becomes unavailable</td>
	<td>Change back to the old IP </td>
	</tr>
	<tr>
	<td>Modifying parameters of core components, e.g. etcd, kube-apiserver, docker, etc., on your own</td>
	<td>Master node may become unavailable</td>
	<td>Configure parameters as recommended by Tencent Cloud</td>
	</tr>
	<tr>
	<td>Changing master or etcd certificate on your own</td>
	<td>Cluster may become unavailable</td>
	<td>Unrecoverable</td>
	</tr>
	<tr>
	<td rowspan=7>Worker node</td>
	<td>Modifying the security groups of nodes in a cluster</td>
	<td>Nodes may become unavailable</td>
	<td>Configure security groups as recommended by Tencent Cloud</td>
	</tr>
	<tr>
	<td>Node expires or is terminated</td>
	<td>The node becomes unavailable</td>
	<td>Unrecoverable</td>
	</tr>
	<tr>
	<td>Reinstalling operating system</td>
	<td>Node components get deleted</td>
	<td>Remove the node and add it back to the cluster</td>
	</tr>
	<tr>
	<td>Upgrading node component version on your own</td>
	<td>Node may become unavailable</td>
	<td>Roll back to the original version</td>
	</tr>
	<tr>
	<td>Changing node IP </td>
	<td>Node becomes unavailable</td>
	<td>Change back to the old IP </td>
	</tr>
	<tr>
	<td>Modifying parameters of core components, e.g. etcd, kube-apiserver, docker, etc., on your own</td>
	<td>Node may become unavailable</td>
	<td>Configure parameters as recommended by Tencent Cloud</td>
	</tr>
	<tr>
	<td>Modifying operating system configuration</td>
	<td>Node may become unavailable</td>
	<td>Try to restore the configurations or delete the node and purchase a new one</td>
	</tr>
	<tr>
	<td>Others</td>
	<td>Modifying permissions in CAM</td>
	<td>Some cluster resources, such as cloud load balancers, may not be able to be created</td>
	<td>Restore the permissions</td>
	</tr>	
</table>

## Networking and Load Balancing

<table>
	<tr>
	<th>High-risk Operation</th>
	<th>Consequence</th>
	<th>Solution</th>
	</tr>
  <tr>
	<td>Modifying kernel parameters <code>net.ipv4.ip_forward=0</code></td>
	<td>Network not connected</td>
	<td>Modify kernel parameters to <code>net.ipv4.ip_forward=1</code></td>
	</tr>
	<tr>
	<td>Modifying kernel parameter <code>net.ipv4.tcp_tw_recycle = 1</code> </td>
	<td>NAT exception</td>
	<td>Modify kernel parameter <code>net.ipv4.tcp_tw_recycle = 0</code></td>
	</tr>
	<tr>
	<td>Container CIDR’s UDP port 53 is not opened to the Internet in the security group configuration of the node</td>
	<td>In-cluster DNS cannot work normally</td>
	<td>Configure security groups as recommended by Tencent Cloud</td>
	</tr>
	<tr>
	<td>Modifying or deleting LB tags added in TKE</td>
	<td>A new LB is purchased </td>
	<td>Restore the LB tags</td>
	</tr>
	<tr>
	<td>Creating custom listeners in TKE-managed LB through LB console</td>
	<td rowspan=4>Modification gets reset by TKE</td>
	<td>Automatically create listeners through service YAML</td>
	</tr>
	<tr>
	<td>Binding custom backend rs in TKE-managed LB through LB console</td>
	<td>Prohibit manual binding of backend rs </td>
	</tr>
	<tr>
	<td>Modifying certificate of TKE-managed LB through LB console</td>
	<td>Automatically manage certificate through ingress YAML</td>
	</tr>
	<tr>
	<td>Modifying TKE-managed LB listener name through LB console</td>
	<td>Prohibit modification of TKE-managed LB listener name</td>
	</tr>
</table>

## Logs
<table>
	<tr>
	<th>High-risk Operation</th>
	<th>Consequence</th>
	<th>Solution</th>
	</tr>
	<tr>
	<td>Deleting the <code>/tmp/ccs-log-collector/pos</code> directory of the host</td>
	<td>Log gets collected again</td>
	<td>None</td>
	</tr>
	<tr>
	<td>Deleting the <code>/tmp/ccs-log-collector/buffer</code> directory of the host</td>
	<td>Log gets lost</td>
	<td>None</td>
	</tr>
</table>

## Cloud Disks

<table>
	<tr>
	<th width="24%">High-risk Operation</th>
	<th>Consequence</th>
	<th width="25%">Solution</th>
	<th>Notes</th>
	</tr>
	<tr>
	<td>Manually unmounting cloud disks through console</td>
	<td>Writing to Pod reports IO errors </td>
	<td>Delete the mount directory of the node and reschedule the Pod</td>
	<td>Files in Pod record where they are collected</td>
	</tr>	
	<tr>
	<td>Unmounting disk mounting path on the node</td>
	<td>Pod gets written to the local disk</td>
	<td>Re-mount the corresponding directory onto Pod</td>
	<td>Buffer contains log cache file</td>
	</tr>	
	<tr>
	<td>Directly operating CBS block device on the node</td>
	<td>Pod gets written to the local disk</td>
	<td>None</td>
	<td>None</td>
	</tr>
</table>

