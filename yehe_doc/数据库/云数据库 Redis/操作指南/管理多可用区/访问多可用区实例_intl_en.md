
You can use one VIP to access a multi-AZ deployed TencentDB for Redis instance the same way you access a single-AZ deployed instance.

## Cross-AZ Access
The VIP provided by a TencentDB for Redis instance is accessible region wide. If you access the same VIP in different AZs in the same region, you can access the same instance.

After the failover of Redis service nodes occurs, the service processes associated with the VIP will be automatically updated in the background, so you don't need to change the VIP.

## Viewing Instance VIPs
Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis) and view instance VIPs in the instance list.
![](https://main.qcloudimg.com/raw/3d4787cf07be40f20ca35a050e5424e0.png)
Or, click an instance ID in the instance list and view the instance VIP on the instance details page.
![](https://main.qcloudimg.com/raw/c470985bf8dc39e46f483849202901ba.png)

## Accessing Multi-AZ Deployed Instances
For more information, please see [Connecting to TencentDB for Redis Instances](https://intl.cloud.tencent.com/document/product/239/9897).
