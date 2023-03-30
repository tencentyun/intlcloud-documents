TencentDB for SQL Server supports VPC.

## Network restrictions
- The networks of different regions are fully isolated. Tencent Cloud services in different regions **cannot communicate via a private network by default**.
- Tencent Cloud services in different VPCs can communicate with each other over [Cloud Connect Network](https://www.tencentcloud.com/document/product/1003), which is fast and stable.
- [Cloud Load Balancer](https://www.tencentcloud.com/document/product/214) currently supports intra-region traffic forwarding by default. If [cross-region binding](https://intl.cloud.tencent.com/document/product/214/38441) is enabled, cross-region binding of CLB and TencentDB instances is supported.
Currently, TencentDB for SQL Server doesn't support public IP. If you need to use a public IP, you can use the port mapping feature of SSH2 to connect to, configure, and manage an instance from the internet. For more information, see [Connecting to TencentDB for SQL Server Instance from Local System](https://intl.cloud.tencent.com/document/product/238/11627).
> When you purchase TencentDB for SQL Server, we recommend that you select the same region as your CVM instance to reduce access delay.


## Network connectivity test
The network connectivity test tool provided on the [TencentDB for SQL Server purchase page](https://buy.cloud.tencent.com/sqlserver#/) can be used to check whether there are CVM instances in the selected region/AZ and network type that can communicate with TencentDB for SQL Server over the private network.
![](https://main.qcloudimg.com/raw/d1bca3859d60633ed0fb5669c88daf13.png)
Click **View Details** to view the information of eligible CVM instances, including ID/instance name, AZ, configuration (CPU, memory, disk, and network), and primary IP address. You can also use the search feature to quickly filter CVM instances that can communicate with TencentDB for SQL Server over the private network.
![](https://main.qcloudimg.com/raw/8c76d06d19734b7fe8f85ba2f14b64a1.png)
