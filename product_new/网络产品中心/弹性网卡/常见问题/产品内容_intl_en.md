### What is an ENI?
- An ENI is a virtual network interface. You can bind a CVM to an ENI for connecting to a network. An ENI is very useful for configuring management networks and developing highly reliable network solutions.
- An ENI is VPC-, availability zone-, and subnet-specific, and can only be bound to a CVM that resides in the same availability zone as it does. A CVM can be bound with multiple ENIs. The number of ENIs allowed to be bound to a CVM depends on the specification of the CVM.

### What are the differences between a primary ENI and a secondary ENI?
- A primary ENI is assigned by the system to users, and its information cannot be modified.
- A secondary ENI is created by users, and its information can be modified.

### What are the use limits on ENI?
The number of ENIs that can be bound to a CVM and the number of private IP addresses that can be bound to each ENI are subject to the CPU and memory configurations of the CVM. For more information, see [Use Limitations](http://intl.cloud.tencent.com/document/product/576/18527).

### What can I do if an EIP fails to be pinged?
Common causes for failing to ping through an EIP are as follows:

- The EIP is not bound to any Tencent Cloud resource. For the binding method, see [Elastic Public IP Addresses](http://intl.cloud.tencent.com/document/product/213/16586).
- The security policy is invalid. If this is the case, you can check whether the security policy ([Security Groups](http://intl.cloud.tencent.com/document/product/213/12452) or [Network ACL](http://intl.cloud.tencent.com/document/product/215/5132)) is valid.
- Port access is disabled. If the Tencent Cloud resource that is bound to the EIP has a security policy that disables a port, the same port for the EIP is also inaccessible. For example: If the bound resource disables port 8080, port 8080 for the EIP is also inaccessible.
