## Issue Description
Two VPCs are connected over CCN, but a ping failure occurs.
>? 
>+ You can test network connectivity in one of the following methods:
>  + ping command: Run the "ping  **peer IP**" command to test whether the source server and the target server are connected.
>   + telnet command: Run the "telnet **peer IP** **peer port number**" command to test whether the port of the specified target server is reachable.
>+ As ping is forbidden for TencentDB and CFS/ES clusters by default, we recommend you use telnet to test the connectivity.
>+ As the virtual IP (VIP) of a private network CLB instance can be pinged only from a client in the same VPC, you cannot ping the peer VIP to test the connectivity of the network connected over CCN; instead, you can ping the peer CVM or telnet the CLB service port.


## Possible Causes
- A Docker container is installed in the CVM instance, and there is a container route.
- Subnet IP ranges conflict, causing the route to fail.
- The security group rule does not allow access.
- The subnet ACL rule does not allow access.
- The firewall is enabled in the CVM instance.


## Troubleshooting

### Step 1. Check for any Docker route in the CVM instances at both sides of the communication
1. Go to the [CVM console](https://console.cloud.tencent.com/cvm/instance/index?rid=16), click **Login** on the right of a CVM instance, enter the password or key as prompted to log in to the instance in the [standard method](https://intl.cloud.tencent.com/document/product/213/5436), and run `route` to view the internal route table of the system.
2. Check whether there is a Docker container route in the system with the same IP range as the subnet of the peer CVM instance.
  + If so, the container route will conflict with the VPC route. In this case, the system will select the container route preferably, leading to inaccessibility to the peer. You need to use a subnet with another IP range or modify the container IP range, and then ping again to test whether the problem is solved. If not, go to [step 2](#step2).
  + If there is no container route, go to [step 2](#step2).
 ![](https://qcloudimg.tencent-cloud.cn/raw/d539f8bd7364e7bd6edd0b0521be3a00.png)

### Step 2. Determine whether the route failed due to the conflict between two VPC subnet IP ranges[](id:step2)
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/ccn) and click **CCN** to enter the CCN console.
2. Click a CCN instance ID to enter the details page.
3. Click the **Route Table** tab to check the route status.
  + If there is an **Invalid** route; that is, if there are two routes to the same destination as shown below, thereby causing the [route conflict](https://intl.cloud.tencent.com/document/product/1003/30052), delete or disable the route with the conflicting IP range according to the actual situation, enable the route that you need for communication, and then ping again to test whether the problem is solved. If not, go to [step 3](#step3).
  + If there is no invalid route, go to [step 3](#step3).
    ![]()

### Step 3. Check whether the security group rules of the CVM instances at both sides of the communication allow access[](id:step3)
1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm).
2. Click the CVM instance ID to enter the details page.
3. Click the **Security Group** tab to check whether the ICMP protocol and the inbound and outbound security group rules for the source/destination IPs are allowed.
 + If there is no protocol rule, or the rule is **Rejected**, click **Edit** to modify the security group rule for the protocol, and then ping again to see whether the problem is solved. If not, go to [step 4](#step4).
 + If the inbound and outbound rules of the security group are correct, go to [step 4](#step4).
	**Rejected**:
	![]()
	**Allowed**:
	![]()

### Step 4. Check whether the ACL rules associated with the subnets at both sides of the communication allow access[](id:step4)
1. On the CVM instance details page, click the subnet ID of the CVM instance to enter the subnet details page.
<img src="" width="60%">
2. Click the **ACL Rule** tab to check whether the subnet is bound to a network ACL, whether there are rules that reject the ICMP protocol, and whether the source/destination IPs are allowed in the inbound and outbound ACL rules.
  +  If no ACL is bound, go to [step 5](#step5).
  + If an ACL is bound, and the ACL rule already allows the protocol and IPs, go to [step 5](#step5).
  + If an ACL is bound and ICMP is **Rejected** in the ACL, or there is no ICMP rule in the ACL, then click the ACL ID to enter the ACL page, **allow** the protocol and source/destination IPs, and then ping again to test whether the problem is solved. If not, go to [step 5](#step5).
>?You can also disassociate ACL rules if you do not need them to control subnet traffic. Evaluate the impact before you disassociate them.
>
 ![]()


### Step 5. Check whether the firewall is enabled in the CVM instances at both sides of the communication[](id:step5)
Confirm whether the firewall is enabled in the CVM instance and make sure that it will not block the communication traffic; otherwise, remove the firewall.
>?
>- For more information on how to remove a firewall, see [Firewall](https://intl.cloud.tencent.com/document/product/213/17403).
>- If the problem persists, record it and [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.
>
