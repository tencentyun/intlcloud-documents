Security is a matter of utmost importance. Tencent Cloud considers security as a top priority in product design and requires all its products to be fully isolated and provides multiple layers of security protection with its basic network. TKE is a typical example. It uses [VPC](https://intl.cloud.tencent.com/document/product/215/535) as the underlying network of container services. This document describes the best practice of using security groups in TKE to help you select the most appropriate security group policy.

## Security Groups
A security group is a virtual firewall that can filter stateful packets. As an important network security isolation means provided by Tencent Cloud, it can be used to configure network access control for one or more CVM instances. For more information, see [Security Groups](https://intl.cloud.tencent.com/document/product/213/12452).

## Principles on Security Group Selection for TKE
- Service pods are distributed on different nodes in a cluster. We recommend that you bind all CVM instances in the same cluster to a single security group and do not add other instances to the security group.
- The security group grants only the minimum permission externally.
- The following TKE rules are enabled:
 - Open the container pod network and cluster node network to the Internet.
 After a service access request reaches a node, the request is forwarded to a random pod of the service based on the iptables rule configured by the kube-proxy module. As a service pod may be on another node, cross-node access occurs in this case. For example, the destination IP addresses of the access request include the IP address of the service pod, IP addresses of other nodes in the cluster, and IP address of the cluster cbr0 bridge on the node. This requires the peer node to allow access requests from the container pod network and cluster node network.
 - Open the corresponding container network and node network of the cluster to the Internet if different clusters in the same VPC instance need to communicate with one another.
 - Open port 22 for login attempts over SSH, if required.
 - Open ports 30000-32768 on a node to the Internet.
 In the access route, data packets need to be forwarded to NodeIP: NodePort of the container cluster through CLB. Here, NodeIP indicates the CVM instance IP address of a random node in the cluster, and NodePort indicates the default port assigned by the container cluster when the service is created. The value range of NodePort is between 30000 and 32768.
 The following figure illustrates this process by using public network access as an example.
![Public network access through CLB](https://main.qcloudimg.com/raw/0a237626a95174fd851052f49a0ff5b3.png)

## Default Security Group Rules of TKE
Some ports need to be opened to ensure normal communication between cluster nodes. To avoid cluster creation failures resulting from binding invalid security groups, TKE provides default security group rules, as described in the following table.
> If the current default security group cannot meet the service requirements, and you have created a cluster that is bound to this security group, you can view and modify the security group rules of the cluster by referring to [Managing Security Group Rules](https://intl.cloud.tencent.com/document/product/213/34826).

#### Inbound policies
| Protocol Rule | Port | Source | Policy | Remarks |
|:--------:|:---------:|:-------:|:-------:|:--------:|
| ALL | ALL | Container network CIDR | Allow | Allow communication between pods within the container network |
| ALL | ALL | Cluster network CIDR | Allow | Allow communication between nodes within the cluster network |
| TCP | 22 | 0.0.0.0/0 | Allow | Open port 22 for login attempts over SSH |
| TCP | 30000-32768 | 0.0.0.0/0 | Allow | Allow communication between the master and worker nodes |
| UDP | 30000-32768 | 0.0.0.0/0 | Allow | Allow communication between the master and worker nodes |
| ICMP | - | 0.0.0.0/0 | Allow | Enable ICMP to support pings |

#### Outbound policies

| Protocol Rule | Port | Source | Policy |
|:--------:|:---------:|:-------:|:-------:|
| ALL | ALL | 0.0.0.0/0 | Allow |

>
>- Configuring this policy for container nodes makes services in the cluster accessible through different access means.
>- For more information on how to access services in a cluster, see the Service Management [Introduction](https://intl.cloud.tencent.com/document/product/457/30672).
