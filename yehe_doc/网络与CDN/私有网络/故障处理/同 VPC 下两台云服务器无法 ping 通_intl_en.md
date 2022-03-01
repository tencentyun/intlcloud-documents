## Error Description
The ping between two CVM instances in the same VPC fails.

## Common Causes
+ The access is blocked by the security group.
+ The access is blocked by the network ACL rules of the subnet.
+ There is a container route in a CVM instance.


## Troubleshooting Procedure

### Check the security group rules
1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm).
2. Click a CVM instance ID to enter the details page.
3. Click the **Security Group** tab to check whether the ICMP protocol and the inbound and outbound security group rules for the source/destination IPs are allowed.
 + If there is no corresponding protocol rule, or the rule is **Reject**, click **Edit** to modify the security group rule for the protocol, and then ping again to see whether the problem is solved.
 + If the inbound and outbound rules of the security group are correct, proceed to the next step.
	**Reject**:
	![]()
	**Allow**:
	![]()
### Check the network ACL rules associated with subnets
1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm).
2. Click a CVM instance ID to enter the details page.
3. Click the **ACL Rule** tab to check whether the subnet is bound to a network ACL, whether there are rules that reject the ICMP protocol, and whether the source/destination IPs are allowed in the inbound and outbound ACL rules.
  + If an ACL is bound and ICMP is **rejected** in the ACL, or there is no ICMP rule in the ACL, then click the ACL ID to enter the ACL page, **allow** the corresponding protocol and source/destination IPs, and move the rule to the first place so that it will be matched first. Then, ping again to see whether the problem is solved, and if not, proceed to the next step.
  + If no ACL is bound, or the ACL rule already allows the corresponding protocol and IPs, proceed to the next step.
      ![]()
	
### Checking for container route in CVM instance
1. Go to the [CVM console](https://console.cloud.tencent.com/cvm/instance/index?rid=16), click **Login** on the right of a CVM instance, enter the password or key as prompted to log in to the instance in the [standard method](https://intl.cloud.tencent.com/document/product/213/5436), and run `route` to view the internal route table of the system.
    ![](https://qcloudimg.tencent-cloud.cn/raw/3b11c3b313ad0076f3c0d3c80d139701.png)
2. Check whether there is a Docker container route in the system with the same IP range as the subnet of the accessed CVM instance.
  + If yes, this problem is caused by the conflict with the container route. You need to delete the corresponding subnet.
  + If no, [contact us](https://intl.cloud.tencent.com/contact-sales) for assistance.
