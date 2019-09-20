### What is an ENI?
- ENI is a virtual network interface. Users can bind the CVM to the ENI for the connection to network. It is very useful for configuring management networks and establishing highly reliable network solutions.
- An ENI is VPC, availability zone and subnet-specific, and can only be bound to a CVM that resides in the same availability zone as it. A CVM can be bound with multiple ENIs. The maximum number of ENIs allowed to be bound to a CVM depends on the CVM's specification.

### What’s the difference between a Primary ENI and a Secondary ENI?
- A primary ENI is assigned by the system for user, and the information cannot be modified.
- A secondary ENI is created by user, and the information can be modified.

### What are the user limits on ENI?
The maximum number of ENIs that can be bound to a CVM and that of private IPs that can be bound to each ENI vary greatly with CPU and memory configurations. For more details, please see [Use Limits](http://intl.cloud.tencent.com/document/product/576/18527).

### What to do if I cannot ping a EIP?
Typically, the reasons are:

- The elastic IP is not bound to any cloud product. For binding methods, please see [Binding EIPs to Cloud Products](http://intl.cloud.tencent.com/document/product/213/16586) for details.
- Security policy is invalid. Users can check whether the security policy ([Security Groups](http://intl.cloud.tencent.com/document/product/213/12452) or [Network ACL](http://intl.cloud.tencent.com/document/product/215/5132)) has taken effect.
- Port access is disabled. Even if the bound cloud product has a security policy, but the access to the port is disabled, the port of the EIP is also inaccessible. For example: If the port 8080 is inaccessible, the port 8080 of the EIP is inaccessible either.

