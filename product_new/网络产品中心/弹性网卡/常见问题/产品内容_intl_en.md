### What is ENI?
- ENI is a virtual network interface. Users can bind a CVM to an ENI to access the network. It is very useful for configuring management networks and establishing highly reliable network solutions.
- ENI is VPC, availability zone and subnet-specific, and can only be bound to a CVM that resides in the same availability zone as it does. A CVM can be bound with multiple ENIs. The number of ENIs allowed to be bound to a CVM depends on the CVM's specification.

### What is the difference between a primary ENI and a secondary ENI?
- A primary ENI is assigned by the system for users, and the information cannot be modified.
- A secondary ENI is created by users, and the information can be modified.

### What are the use limits of ENI?
The number of ENIs that can be bound to a CVM and the number of private IPs that can be bound to each ENI vary greatly depending on CPU and memory configurations. For more details, please see [Use Limits](http://intl.cloud.tencent.com/document/product/576/18527).

### What can’t I ping an EIP?
Typical reasons are:

- Elastic IP is not bound to any cloud product. For binding methods, please see [Binding EIPs to Cloud Products](http://intl.cloud.tencent.com/document/product/213/16586) for details.
- Security policy is invalid. Users can check whether the security policy ([Security Groups](http://intl.cloud.tencent.com/document/product/213/12452) or [Network ACL](http://intl.cloud.tencent.com/document/product/215/5132)) is effective.
- Port access is disabled. If the cloud product instance bound to an EIP has security policy, but access to the port is disabled, then the port of the EIP is also inaccessible. For example: If port 8080 is inaccessible, then port 8080 of the EIP is also inaccessible.

