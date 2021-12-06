### Can I initiate network connections in my function code?

Yes. You can use general programming language and operating system features, such as initiating TCP and UDP connections. Through relevant language libraries, you can also perform operations such as connecting to databases and accessing APIs.

### My TencentDB for Redis instance only supports private network access. How do I connect SCF to it?

You can [deploy a function to a VPC](https://intl.cloud.tencent.com/document/product/583/19703) through which SCF can access resources in the private network.

### After SCF is deployed to a VPC, how do I configure public network access?

There are several ways for a VPC to access the public network. For more information, see the [NAT Gateway documentation](https://intl.cloud.tencent.com/document/product/1015).

### Is the IP used for SCF to access the public network random or fixed?

It is random by default. You can also set a fixed public IP. For more information, please see [Fixed Public Outbound IP](https://intl.cloud.tencent.com/document/product/583/38106).

