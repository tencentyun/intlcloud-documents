Enterprise security group is a new security group control plane that replaces the security group administration interface in the CVM console. The configuration logic of security groups has been redesigned and a centralized access control administration page has been maintained, which improves the user experience of security groups. CFW provides five-tuple-based rule configuration and automatically publishes security group rules through intelligent transformation algorithms, which simplifies the configuration of security groups.
![](https://qcloudimg.tencent-cloud.cn/raw/9c7dcade591d0cec16ea8246f39b25f9.jpg)

## Features
-	It simplifies the configuration of security groups based on the 5-tuple rules.
-	It supports inter-VPC, inter-subnet, and direct connect access control.
-	It provides access control logs of security groups for easy backtracking of blocking and routine troubleshooting.
-	It requires no change in the network architecture, and has no impact on network stability and network performance.

## Restrictions
Enterprise security group is developed based on the underlying architecture of the CVM security group, and thus is restricted by the underlying functional implementation and resource quotas of the security group.

## Rules
### Rule composition
- Access source and access destination: Depending on the inbound or outbound direction, they can be IPs, CIDR blocks, instances, subnets, or private networks.
- Destination port: The destination port number. Not required when the protocol type is ICMP or ANY.
- Protocol type: 	TCP, UDP, and ICMP are supported. ANY indicates all supported protocols.
- Policy: the operation performed after the rule is hit.
	- Allow: Allow the matched traffic but do not record access control logs.
	- Block: Block the matched traffic and record access control logs.

### Rule priorities
The security group rules are prioritized in a way that the rule at the top of the list has the highest priority while the rule at the bottom has the lowest priority.
The rule with the highest priority is evaluated first. If a given rule is matched, rules with lower priorities will not be evaluated.
The inbound and outbound rules are in different lists and independent of each other.

## Auto two-way publishing
Enterprise security group provides the "Auto two-way publishing" feature to improve the configuration efficiency of security groups. This eliminates the need to configure two identical rules in both directions to block or allow traffic between private networks, thus reducing the workload of rule configuration.

When the access source address is an instance, subnet, or private network address, an identical outbound rule (with the highest priority) can be automatically configured using "Auto two-way publishing".
>! It only applies to communication between private networks.

For example, there are two instances, instance 1 and instance 2, and their IP address is IP1 and IP2, respectively.
If you have configured a "deny all" policy for the security group for instances 1 and 2, respectively, and want to allow the access from instance 1 to instance 2, you need to manually configure two security group rules:
- Instance 1: Allow IP2 in the outbound direction.
- Instance 2: Allow IP1 in the inbound direction.


## Logs
### Security group blocking logs
The [security group blocking logs](https://console.cloud.tencent.com/cfw/log/secgroup) record the implementation of all blocking policies for enterprise security groups. This is only available to [specified models](https://intl.cloud.tencent.com/document/product/682/18934).
### Enterprise security group operation logs
The [enterprise security group operation logs](https://console.cloud.tencent.com/cfw/operatelog/safe) record the operations performed by an account on the "Enterprise security groups" page.

