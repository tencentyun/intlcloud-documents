A security group is a stateful virtual firewall capable of filtering. As an important means of network security isolation provided by Tencent Cloud, it is used to manage the security verification of inputs.

### Selecting a security group region

Currently, Tencent Cloud StreamLive is available in four AZs: Mumbai (India), Bangkok (Thailand), Seoul (Korea), and Tokyo (Japan). If you need to deploy StreamLive in other AZs, please [contact us](https://intl.cloud.tencent.com/contact-sales).
![](https://qcloudimg.tencent-cloud.cn/raw/c099c3984d22fca6227e14123d9e2c17.jpg)

### Creating a security group

A security group is used to verify the validity of an input source's IPv4 address, which makes the input of StreamLive channels more secure.

Choose **Security Group Management** on the left sidebar and click **Create Security Group**. Enter a name, and add IPs to the allowlist (the IPs must be in CIDR block format, separated with commas or line breaks). Then, click **Confirm** to complete the creation.

![img](https://main.qcloudimg.com/raw/e5c7365ba3724802b2013b3c25cdc07b.png)

>?
> - The status of a security group can be either **Idle** or **Occupied**.
> - **Idle** indicates that a security group is currently not associated with an input and can be edited and deleted.
> - **Occupied** indicates that a security group is currently associated with an input and can only be edited, not deleted.
>- You can create up to 5 security groups in the console by default. Please [submit a ticket](https://console.cloud.tencent.com/workorder) if you need more security groups.
