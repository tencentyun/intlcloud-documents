

 An input security group is used to verify the input source's IPv4 address, making the input of MediaLive channels more secure.

Add a CIDR block to a new input security group. Separate the CIDR block by a comma or newline.
![](https://main.qcloudimg.com/raw/fa4a607b8f856c0733fef5d5ff1f4ea0.jpg)

>!
The status of the security group can be either "idle" or "occupied". The former means that the security group is currently not associated and can be edited and deleted. The latter indicates that the security group is currently associated with a channel input and can only be edited, not deleted.
>- You can create up to 5 security groups in the console by default. Please [submit a ticket](https://console.cloud.tencent.com/workorder/category) if you need more security groups.
