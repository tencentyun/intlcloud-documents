## Operation Scenarios
When the access address of a database instance needs to be modified, you can adjust the network using the private network translation feature.

>
>- Modifying the private address of an instance is highly risky. Please only do so with caution during off-peak hours. After modification, unless occupied by another service, the original address will remain valid for another 24 hours. Please switch your business configuration as soon as possible.
>- Once selected, a VPC cannot be changed.

## Switching from Basic Network to VPC
An instance can be switched from basic network to VPC. To do so, click **Switch to VPC** in the **Network** section on the instance details page, provided that there is an available IP in the target VPC subnet.


## Changing Private Address
The private address of a TencentDB instance can be changed. You can do so in the **Private IP** section on the instance details page, provided that there is an available IP in the current subnet.
![](https://main.qcloudimg.com/raw/e9b50d4a729e0e8a069e6f2243634181.png)

## Switching Between VPC Subnets
The VPC subnet of an instance can be changed. To do so, click **Change Subnet** in the **Network** section on the instance details page, provided that there is an available IP in the target VPC subnet.
>Because the product supports an intra-city active-active architecture, you are recommended to choose a VPC subnet in the same region as your business server or master node.
>
![](https://main.qcloudimg.com/raw/b2f24c54b12ebdd958d0da3cdf993b5b.png)

