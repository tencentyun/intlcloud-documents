The [ACL Rule](https://www.tencentcloud.com/document/product/215/31850) is an optional security layer which operates at subnet level. It is used to control the inbound and outbound data streams of subnets, which can be accurate to the protocol and port granularity, to achieve fine-control of subnet traffic. You can associate the same network ACL to subnets which require the same level of network traffic control.
This document describes how to bind, unbind, and change ACL rules in the VPC console.

## How It Works
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc).
2. Click **Subnet** on the left sidebar to access the subnet management page.
3. Click a subnet ID to go to its details page. You can bind, unbind, and change ACL rules on the following tabs:
    + In the **Associate ACL** field under the **Basic information** tab
    
    <img src="https://staticintl.cloudcachetci.com/yehe/backend-news/QU8E337_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230406171900.png" width="50%" />
    + Under the **ACL rules** tab
    
     <img src="https://staticintl.cloudcachetci.com/yehe/backend-news/e5Du001_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230406172142.png" width="50%" />
4. Perform the following operations based on the business needs. The following screenshots take the operations in **ACL Rules** as an example.
  + If the current subnet is not bound to an ACL rule, you can click **Bind** to select an appropriate ACL rule, and click **OK** to complete the binding. The binding will take effect immediately. The inbound and outbound traffic of the subnet is allowed only when the rule is **Allow**.
    <img src="https://staticintl.cloudcachetci.com/yehe/backend-news/HYHk340_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230406172316.png" width="50%" /> 
  + If the ACL rule bound to the current subnet does not meet network flow requirements, you can click **Change** to change the ACL rule, which will take effect immediately.
  
	<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/EDr8528_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230406173010.png" width="80%" />
  + If the current subnet is bound to an ACL rule, but you no longer need to control the inbound and outbound traffic of the subnet, you can click **Unbind** to unbind the ACL rule. The unbinding will take effect immediately and this will cause the lifting of the ACL rule restriction on the inbound and outbound traffic of the subnet.
	<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/2KsW035_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230406173542.png" width="70%" /> 
