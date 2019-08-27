### My CVM and TencentDB for Redis are deployed in the same region, how to connect to Redis?
In this case, please use the private network for access. For more information on the connection method, see [Connection Guide](https://intl.cloud.tencent.com/document/product/239/9897).

### My CVM and TencentDB for Redis are deployed in different regions, how to connect to Redis?
For communication between basic network and VPC, see [Classiclink](https://intl.cloud.tencent.com/document/product/215/5002).
For communication between VPCs, see [Peering Connection](https://intl.cloud.tencent.com/document/product/215/5000).

### What if my TencentDB for Redis instance is unpingable? 
Redis prohibits `ping` by default. You can use telnet to check connectivity.

### How do I enable access to Redis over a public network? 
TencentDB for Redis does not support public network access for the time being.
If you need to enable public network access, you can use a CVM instance that has a public network connection through the iptable proxy.

### How do I configure password-free login for Redis? 
Currently, password-free login is not supported.

