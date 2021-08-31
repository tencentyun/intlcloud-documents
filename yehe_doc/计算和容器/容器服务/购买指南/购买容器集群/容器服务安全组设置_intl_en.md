Security is always of utmost importance. Tencent Cloud prioritizes security in product design and strictly requires that all products are fully isolated. The Tencent Cloud classic network provides multiple layers of security protection. Tencent Kubernetes Engine (TKE) also pays special attention to security. TKE selects [VPC](https://intl.cloud.tencent.com/document/product/215/535) with richer network features as the underlying network. This document describes the best practice of using security groups in TKE, helping you select the most appropriate security group policy.

## Security Group
A security group is a virtual firewall for stateful data packet filtering. As an important network isolation approach provided by Tencent Cloud, a security group is used to set network access control of one or more Cloud Virtual Machine (CVMs). For more information on security groups, please see [Security Groups](https://intl.cloud.tencent.com/document/product/213/12452).

## How to Select a Security Group for TKE
- In a container cluster, service pods are distributed on different nodes. We recommend that you bind all CVM instances in one cluster to the same security group and do not add non-clustered CVMs to a security group for a cluster.
- A security group only grants the minimum permission externally.
- You must enable the following rules for using TKE:
 - Open the container pod network and the cluster node network to the Internet.
 When a node receives a service access request, the node forwards the request to a service pod according to the iptables rule configured by the kube-proxy module. If the service pod is on another node, cross-node access occurs. For example, the destination IP addresses of the access request include the IP address of the service pod, IP addresses of other nodes in the cluster, and the IP address of the cluster’s cbr0 bridge on the node. In this case, the container pod network and the cluster node network on the peer node must be open to the Internet.
 - If clusters in the same VPC need to communicate with each other, you must open the container networks and node networks of the corresponding clusters to the Internet.
 - Open port 22 to the Internet if SSH login is required.
 - Open ports 30000 to 32768 on nodes to the Internet.
 In the access path, you must use a load balancer to forward data packets to NodeIP:NodePort of the container cluster. NodeIP is the CVM instance IP of any node in the cluster. NodePort is assigned by the container cluster by default when the service is created. NodePort ranges from 30000 to 32768.
 The following figure uses service access from the public network as an example.
![Public network access through CLB](https://main.qcloudimg.com/raw/0a237626a95174fd851052f49a0ff5b3.png)

## Default Security Group Rules for TKE
### Default security group rules for node
Some ports must be opened to the Internet to ensure normal communication between cluster nodes. To avoid cluster creation failures due to binding to invalid security groups, TKE provides default security group rules, as described in the following table.
> ! If the current default security group cannot meet your service requirements and you have created a cluster bound to this security group, you can view and modify the security group rules for the cluster. For more information, please see [Managing Security Group Rules](https://intl.cloud.tencent.com/document/product/213/34275).

#### Inbound rules
| Protocol | Port Number | Source IP Address | Rule | Description |
|:--------:|:---------:|:-------:|:-------:|:--------:|
| All | All | CIDR of the container network | Allow | Enable the communication between pods in the container network. |
| All | All | CIDR of the cluster network | Allow | Enable the communication between nodes in the cluster network. |
| TCP | 22 | 0.0.0.0/0 | Allow | Open the SSH login port to the Internet. |
| TCP | 30000 to 32768 | 0.0.0.0/0 | Allow | Enable the communication between master and worker nodes. |
| UDP | 30000 to 32768 | 0.0.0.0/0 | Allow | Enable the communication between master and worker nodes. |
| ICMP | - | 0.0.0.0/0 | Allow | Enable the support for Internet Control Message Protocol (ICMP) and ping operations. |

#### Outbound rules

| Protocol | Port Number | Source IP Address | Rule |
|:--------:|:---------:|:-------:|:-------:|
| All | All | 0.0.0.0/0 | Allow |

>?
> - To customize outbound rules, you need to open the node IP range and container IP range.
> - If you configure this rule for container nodes, the services in the cluster can be accessed using different access methods.
> - For more information on how to access a service in a cluster, please see "Service Access" in [Overview](https://intl.cloud.tencent.com/document/product/457/36832).

### Default security group rules for self-deployed cluster Master
When a self-deployed cluster is created, the TKE default security group will be bound to the Master model by default to reduce the risk that the Master and Node cannot communicate normally and the Service cannot be accessed normally after the cluster is created. The default security group configuration rules are as follows:
>?The permission to create a security group is same as the permission configured in TKE **Service Authorization**. For more information, see [Description of Role Permissions Related to Service Authorization](https://intl.cloud.tencent.com/document/product/457/37808)

#### Inbound rules
<table>
<thead>
<tr>
<th>Protocol</th>
<th>Port</th>
<th style="width:13%">IP Range</th>
<th>Rule</th>
<th style="width:25%">Description</th>
</tr>
</thead>
<tbody><tr>
<td>ICMP</td>
<td>ALL</td>
<td>0.0.0.0/0</td>
<td>Allow</td>
<td>Ping is supported.</td>
</tr>
<tr>
<td>TCP</td>
<td>30000 - 32768</td>
<td>Cluster network CIDR</td>
<td>Allow</td>
<td>Enable the communication between Master and Worker nodes.</td>
</tr>
<tr>
<td>UDP</td>
<td>30000 - 32768</td>
<td>Cluster network CIDR</td>
<td>Allow</td>
<td>Enable the communication between Master and Worker nodes.</td>
</tr>
<tr>
<td>TCP</td>
<td>60001,60002,10250,2380,2379,53,17443,<br>50055,443,61678</td>
<td>Cluster network CIDR</td>
<td>Allow</td>
<td>Enable the communication of API Server.</td>
</tr>
<tr>
<td>TCP</td>
<td>60001,60002,10250,2380,2379,53,17443</td>
<td>Container network CIDR</td>
<td>Allow</td>
<td>Enable the communication of API Server.</td>
</tr>
<tr>
<td>TCP</td>
<td>30000 - 32768</td>
<td>Container network CIDR</td>
<td>Allow</td>
<td>Enable the communication of Service.</td>
</tr>
<tr>
<td>UDP</td>
<td>30000 - 32768</td>
<td>Container network CIDR</td>
<td>Allow</td>
<td>Enable the communication of Service.</td>
</tr>
<tr>
<td>UDP</td>
<td>53</td>
<td>Container network CIDR</td>
<td>Allow</td>
<td>Enable the communication of CoreDNS.</td>
</tr>
<tr>
<td>UDP</td>
<td>53</td>
<td>Cluster network CIDR</td>
<td>Allow</td>
<td>Enable the communication of CoreDNS.</td>
</tr>
</tbody></table>

#### Outbound rules

| Protocol | Port Number | Source IP Address | Rule |
|:--------:|:---------:|:-------:|:-------:|
| All | All | 0.0.0.0/0 | Allow |


