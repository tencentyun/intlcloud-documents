The [ACL Rule](https://intl.cloud.tencent.com/document/product/215/31850) is an optional security layer which operates at subnet level. It is used to control the inbound and outbound data streams of subnets, which can be accurate to the protocol and port granularity, to achieve fine-control of subnet traffic. You can associate the same network ACL to subnets which require the same level of network traffic control.
This section describes how to bind, unbind, and change ACL rules via the VPC console.

## Directions
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc).
2. Select **Subnet** in the left sidebar to go to the subnet management page.
3. Click a subnet ID to go to its details page. You can perform the binding, unbinding, or changing of ACL in the following pages.
    + In the **Associate ACL** field under the **Basic Information** tab
    <img src="https://main.qcloudimg.com/raw/fe87d689ee1fa4f6b87e6dfa7ed6f644.png" width="50%" />
    + Under the **ACL Rules** tab
     <img src="https://main.qcloudimg.com/raw/01505eca4a05bf829b2deb29f0db2231.png" width="50%" />
4. Perform the following operations based on the business needs. The following screenshots take the operations in **ACL Rules** as an example.
  + If the current subnet is not bound with ACL rule, you can click **Bind** to select an appropriate ACL rule, and click **OK** to complete the binding. The binding will take effect immediately. At this time, only the inbound and outbound traffic of the subnet that the rule is **Allow** can pass through.
  <img src="https://main.qcloudimg.com/raw/0bad22697aa3af3b36e866be781027ec.png" width="50%" />
 + If the ACL rule bound to the current subnet does not meet network flow requirements, you can click **Change** to change the ACL rule, which will take effect immediately.
	<img src="https://main.qcloudimg.com/raw/b3b3d8815e2053a0b703f4a03f372aba.png" width="80%" />
 + If the current subnet is bound with a ACL rule, but you no longer need to control the inbound and outbound traffic of the subnet, you can click **Unbind** to unbind the ACL rule. The unbinding will take effect immediately and this will cause the lifting of the ACL rule restriction on the inbound and outbound traffic of the subnet.
	<img src="https://main.qcloudimg.com/raw/c3e375dca8a91f35cfe7f1087817db8a.png" width="80%" />
    	 
