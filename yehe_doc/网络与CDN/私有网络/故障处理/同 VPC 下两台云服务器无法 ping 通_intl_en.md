## Problem Description
The ping between two CVM instances in the same VPC fails.

## Possible Causes
+ The access is blocked by the security group.
+ The access is blocked by the network ACL rules of the subnet.
+ There is a container route in a CVM instance.

## Troubleshooting

### Check the security group rules
1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm).
2. Click a CVM instance ID to enter the details page.
3. Click the **Security Group** tab to check whether the ICMP protocol and the inbound and outbound security group rules for the source/destination IPs are allowed.
 + If there is no corresponding protocol rule, or the rule is **Reject**, click **Edit** to modify the security group rule for the protocol, and then ping again to see whether the problem is solved.
 + If the inbound and outbound rules of the security group are correct, proceed to the next step.
	**Reject**:
	![](https://staticintl.cloudcachetci.com/yehe/backend-news/NUQL033_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230330103255.png)
	**Allow**:
	![](https://staticintl.cloudcachetci.com/yehe/backend-news/2yz2526_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230330102955.png)
### Check the network ACL rules associated with subnets
1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm).
2. Click a CVM instance ID to enter the details page.
3. Go to **Instance details** -> **Basic information**, click the subnet ID in **Network information**,
4. Click the **ACL Rule** tab to check the ACL-related settings.
  + An ACL is bound but there is no ICMP rule or ICMP set to **rejected**: Click the ACL ID to enter the ACL page, **allow** the corresponding protocol and source/destination IPs, and move the rule to the first place so that it will be matched first. Then, ping again to see whether the problem is solved, and if not, proceed to the next step.
  + No ACL is bound, or the protocol and IPs are allowed in the ACL: Proceed to the next step.
      
### Checking for container route in CVM instance
1. Go to the [CVM console](https://console.cloud.tencent.com/cvm/instance/index?rid=16), click **Log in** on the right of a CVM instance, enter the password or key as prompted to log in to the instance in the [standard method](https://www.tencentcloud.com/document/product/213/5436), and run `route` to view the internal route table of the system.
    ![](https://qcloudimg.tencent-cloud.cn/raw/3b11c3b313ad0076f3c0d3c80d139701.png)
2. Check whether there is a Docker container route in the system with the same IP range as the subnet of the accessed CVM instance.
  + If yes, this problem is caused by the conflict with the container route. You need to delete the corresponding subnet.
  + If no, [contact us](https://www.tencentcloud.com/contact-sales) for assistance.
