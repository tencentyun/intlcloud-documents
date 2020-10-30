

 An input security group is used to verify the validity of the input source's IPv4 address, which makes the input of MediaLive channels more secure.

Add a CIDR block separated by comma or newline to a new input security group.
![](https://main.qcloudimg.com/raw/fa4a607b8f856c0733fef5d5ff1f4ea0.jpg)

>!
The status of the security group can be either "idle" or "occupied". The former means that the security group is currently not associated and can be edited and deleted, while the latter indicates that the security group is currently associated with a channel input and can be edited but not deleted.
>- you can create up to 5 security groups in the console by default. If you need more security groups, please submit a ticket for assistance.(https://console.cloud.tencent.com/workorder/category)
