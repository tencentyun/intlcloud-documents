TencentDB for PostgreSQL supports private and public network addresses. By default, a private network address is provided for you to access your instance over the private network. If you want to enable public network access, you can enable it in the console to build a public network address.

>?
>- Currently, the public network security group feature is available in the Beijing, Shanghai, Guangzhou, and Chengdu regions, so you can enable the public network address in the console.

## Enabling Public Network Address in Console
1. Log in to the [TencentDB for PostgreSQL console](https://console.cloud.tencent.com/postgres) and select the region. In the instance list, click the target instance ID or **Manage** in the **Operation** column to enter the instance management page.
3. On the **Instance Details** page, click **Enable** in **Basic Info** > **Public IPv4 Address**.
![](https://qcloudimg.tencent-cloud.cn/raw/a43ee5972d95fce9c3369cf714f15028.png)
4. In the pop-up window, read the notes and click **OK**.
5. After the instance status is updated to **Running**, you can view the public network address on the instance details page.

### Configure a TencentDB for PostgreSQL security group
1. Log in to the [TencentDB for PostgreSQL console](https://console.cloud.tencent.com/postgres) and select the region. In the instance list, click the target instance ID or **Manage** in the **Operation** column to enter the instance management page.
2. On the instance management page, select the **Security Group** tab, click **Configure Security Group**, configure the security group rule to open all ports, and confirm that the security group allows access from public IPs. For more information on configuration, see [Managing Security Groups](https://intl.cloud.tencent.com/document/product/409/40112).

![](https://qcloudimg.tencent-cloud.cn/raw/5d34fb75a326af1e882f29c1fc967987.png)![](https://qcloudimg.tencent-cloud.cn/raw/789e573631f0eb9806f6e755c6400520.png)

### Check public network connectivity
You can use a client tool to access TencentDB for PostgreSQL. For detailed directions, see [Connecting to PostgreSQL Instances](https://intl.cloud.tencent.com/document/product/409/34626).


