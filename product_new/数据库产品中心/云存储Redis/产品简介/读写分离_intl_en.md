TencentDB for Redis supports read-write separation for business scenarios with more reads but less writes, which can well cope with read requests concentrating on frequently read data. It supports up to 1-master 5-slave mode to offer 5x read performance.

## How It Works

#### Redis Cluster Edition
- **Read-write separation principle**: Redis Cluster Edition implements automatic read-write separation at the Proxy layer.
- **Read-write separation weight**: After read-write separation is enabled, Proxy will enable access by directing write requests to the master node only and distributing read requests evenly on slave nodes.
![](https://main.qcloudimg.com/raw/b37d95b6fe281bb77d2a22af2daf5a9f.png)

## Read-write Separate Billing
After read-write separation is enabled, certain fees will be charged for the read-only replicas. For more information, see [Product Pricing](http://intl.cloud.tencent.com/document/product/239/9894).




