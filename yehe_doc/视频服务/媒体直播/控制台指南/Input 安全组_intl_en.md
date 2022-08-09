An input security group functions as a virtual firewall that allows you to specify a list of IP addresses (ranges) that can push to an input. It’s an important security method provided by Tencent Cloud.



## Prerequisites
- You have activated [StreamLive](https://intl.cloud.tencent.com/products/mdl). 
- You have logged in to the [StreamLive console](https://console.intl.cloud.tencent.com/mdl/security).

## Managing Input Security Groups
Select **Security Group Management** on the left sidebar. You can view the information of security groups you have created, including their names, status, and IDs. You can also create, edit, and delete a security group on this page. Currently, Tencent Cloud offers five availability zones, namely Mumbai (India), Bangkok (Thailand), Seoul (South Korea), Tokyo (Japan), and Frankfurt (Germany) for you to choose from. If you want to deploy your business in other regions, please [contact us](https://intl.cloud.tencent.com/contact-us).

![](https://qcloudimg.tencent-cloud.cn/raw/fc7c32157eccae3591533e14c511fa8f.png)


### Creating an input security group
A security group helps you ensure the security of an input by checking the validity of IPV4 addresses that push content to it. Click **Create Security Group** in the top left corner and complete the following settings in the pop-up window:
1. **Name**: Enter a name of 1-32 characters. Numbers, letters, and underscores (_) are allowed.
2. **IP Allowlist**: Enter CIDR blocks and separate them with commas or line breaks. If you enter `0.0.0.0/0`, all IP addresses are allowed.
Click **Confirm**.

![](https://qcloudimg.tencent-cloud.cn/raw/4fd4169c10d7b6f968f323822c37301a.png)

### Modifying an input security group
To modify an input security group, find it in the list and click **Edit** in the operation column. Modify its settings in the pop-up window and click **Confirm**.

![](https://qcloudimg.tencent-cloud.cn/raw/6fbf87ce94c7c1cc8e9914c5fb9425ef.png)

### Deleting an input security group
To delete an input security group, find it in the list, click **Delete** in the operation column, and click **Confirm** in the pop-up window.

![](https://qcloudimg.tencent-cloud.cn/raw/b0f08d28e5b0658c04756a179100dad9.png)

>?
>- The status of a security group can be either "idle" or "occupied".
>- "Idle" indicates that a security group is currently not associated with an input and can be edited and deleted.
>- "Occupied" indicates that a security group is currently associated with an input and can only be edited, not deleted.
>- You can create up to five security groups in the console by default. If you want to create more, please [submit a ticket](https://console.cloud.tencent.com/workorder).

