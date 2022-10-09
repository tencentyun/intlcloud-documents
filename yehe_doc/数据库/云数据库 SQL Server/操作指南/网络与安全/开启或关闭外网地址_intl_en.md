## Overview
TencentDB for SQL Server supports private and public network addresses. By default, a private network address is provided for you to access your instance over the private network. If you want to access your instance at its public network address, you need to enable the public network address, which can be disabled as needed.

## Notes
- After enabling the public network address, you can access your TencentDB for SQL Server instance by using the system-assigned domain name and port. It takes about five minutes for the configuration to take effect.
- After the public network access is enabled, it will be controlled by the security group policy. You should configure the database access source in the security group's inbound rules and open the protocol ports (both the private network port (1433 by default) and public network port) as instructed in [Configuring Security Group](https://intl.cloud.tencent.com/document/product/238/35789).
- Enabling the public network address will expose your database services to the public network, which may lead to database intrusions or attacks. We recommend you use the private network to connect to the database in the production environment, as public network access may become unavailable due to uncontrollable factors, such as DDoS attacks and large traffic surges.
- Accessing an instance at the public network address will undermine the security of the instance, and service availability will not be guaranteed by SLA. Therefore, we recommend you access your instance at the public network address only when developing, testing, or managing databases. To make transfer faster and ensure a higher security level, use the private network address for database connection. Do not use the public network to sustain the business load, and if you need this, we recommend you [enable public network access through CLB](https://www.tencentcloud.com/document/product/238/48066).
- Currently, enabling the public network address and the public network traffic generated subsequently are free of charge, but the stability of the public network bandwidth and traffic cannot be guaranteed.
- The instance service downtime caused by public network errors won't be counted into the "Single Instance Service Downtime" in TencentDB for SQL Server Service Level Agreement (SLA).

## Prerequisites
- The network of the instance is a VPC.
- The instance is in Guangzhou, Shanghai, Beijing, Chengdu, or Chongqing region.

## Private/Public network address description

| Address Type | Description |
|---------|---------|
| Private network address | <li>A private network address is an IP address that cannot be accessed by an external device on the internet. It is the implementation form of the Tencent Cloud private network service.<li>A private network address is provided by the system by default and cannot be disabled. You can switch the network type though.<li>If your CVM and TencentDB for SQL Server instances are in the same VPC or classic network in the same region under the same Tencent Cloud root account, they can be interconnected over the private network, and there is no need to enable the public network address.<li>It is highly secure. |
| Public network address | <li>A public network address is a non-reserved address on the internet.<li>A public network address needs to be manually enabled and can be disabled when no longer needed.<li>As a public network address lowers the instance's security level, it should be used with caution.<li>A device not in Tencent Cloud can access a TencentDB for SQL Server instance at its public network address.</li>|

## Enabling the public network address
1. Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver).
2. Select the region and click the ID or **Manage** in the **Operation** column of the target instance in the instance list.
3. On the **Instance Details** tab, click **Enable** in **Basic Info** > **Public Network Address**.
![](https://qcloudimg.tencent-cloud.cn/raw/14537eedf3016656d5d6dee1c392342b.png)
4. In the **Enabling public network** window, read the note, indicate your consent, and click **OK** (before the public network address is enabled, a note will be displayed depending on whether a security group is configured).
>!After the public network address is enabled, it can be viewed in **Basic Info**. The public network access can be toggled off. When it is enabled again, the public network address corresponding to the domain name remains the same.
>
 - If your instance is bound to a security group, and no high-risk policy is involved, the public network address can be enabled.
 - If your instance is bound to a security group, but there is a high-risk inbound rule such as `0.0.0.0/0` or `::/0`, a note will be displayed as follows:
 ![](https://qcloudimg.tencent-cloud.cn/raw/ece84f46b9da7d1691c585a8f17eb636.png) 
 - If your instance is not bound to a security group, enabling public network access will lead to a high risk, and a note will be displayed as follows:
 ![](https://qcloudimg.tencent-cloud.cn/raw/7f21811e96a0bb1c85d40dcb8fd8c152.png)
5. After the instance status becomes **Running**, you can view the public network address on the instance details page.

## Disabling the public network address
1. Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver).
2. Select the region and click the ID or **Manage** in the **Operation** column of the target instance in the instance list.
3. On the **Instance Details** tab, click **Disable** in **Basic Info** > **Public Network Address**.
4. In the **Disabling public network** pop-up window, click **OK**.
>!After it is disabled, you can no longer use the domain name and port to access TencentDB for SQL Server over the public network. To minimize potential losses, make sure that no public address is used in your system before disabling it.
