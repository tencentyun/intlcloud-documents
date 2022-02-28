TencentDB for PostgreSQL supports private and public network addresses. By default, a private network address is provided for you to access your instance over the private network. If you want to enable public network access, you can enable it in the console or use CLB to bind a public network address.

>?
>- Currently, the public network security group feature is available in the Beijing, Shanghai, Guangzhou, and Chengdu regions, so you can enable the public network address in the console.
>- Instances in other regions may be attacked if public network access is enabled; therefore, proceed with caution. You can use CLB to enable the public network service for such instances, which can be accessed only after security group rules are configured.

## Enabling Public Network Address in Console
1. Log in to the [TencentDB for PostgreSQL console](https://console.cloud.tencent.com/postgres) and select the region. In the instance list, click the target instance ID or **Manage** in the **Operation** column to enter the instance management page.
3. On the **Instance Details** page, click **Enable** in **Basic Info** > **Public IPv4 Address**.
![](https://qcloudimg.tencent-cloud.cn/raw/c2e502e10860d0e760abd0978b73101a.png)
4. In the pop-up window, read the notes and click **OK**.
5. After the instance status is updated to **Running**, you can view the public network address on the instance details page.

## Enabling Public Network Service in CLB
### Step 1. Purchase a CLB instance
>?If you already have a CLB instance in the same region as TencentDB for PostgreSQL, skip this step.
>
>Go to the [CLB purchase page](https://buy.intl.cloud.tencent.com/clb), select the configuration, and click **Buy Now**.
>!
>
>- Region: you need to select the region where the TencentDB for PostgreSQL instance is.
>- Network: you can select the same VPC as the instance or a different VPC.

### Step 2. Configure the CLB instance
#### 2.1 Enable cross-VPC access (you can skip this step if the CLB instance and TencentDB for PostgreSQL instance are in the same VPC)
a. Log in to the [CLB console](https://console.cloud.tencent.com/clb/instance), select the region, and click the target instance ID in the instance list to enter the instance management page.
b. On the **Basic Info** page, click **Configure** in the **Real Server** section.
![](https://qcloudimg.tencent-cloud.cn/raw/8ff86cded677aded4343f4c8ca94bdd3.png)
c. In the pop-up window, click **Submit**.
![](https://qcloudimg.tencent-cloud.cn/raw/ff42f39084a4c37e6558b44e0c645c57.png)

#### 2.2 Configure a public network listener port
a. Log in to the [CLB console](https://console.cloud.tencent.com/clb/instance), select the region, and click the target instance ID in the instance list to enter the instance management page.
b. On the instance management page, select the **Listener Management** tab and click **Create** below **TCP/UDP/TCP SSL Listener**.
![](https://qcloudimg.tencent-cloud.cn/raw/6ec6c16cd556710910349f961ff49799.png)
c. In the pop-up window, complete the settings and click **Submit**.
![](https://qcloudimg.tencent-cloud.cn/raw/71a7693a4494e0f68d6d7fdfec055f35.png)

### Step 3. Bind a TencentDB for PostgreSQL instance
3.1 After creating the listener, click it in **Listener Management** and click **Bind** on the right.
![](https://qcloudimg.tencent-cloud.cn/raw/84dcba3c7ed1ec7b35ab0d63b9ea6895.png)
3.2 In the pop-up window, select **Other Private IPs** as the object type, enter the IP address and port of the TencentDB for PostgreSQL instance, and click **OK**.

>!The login account must be a standard account (bill-by-IP). If binding fails, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.
>
![](https://qcloudimg.tencent-cloud.cn/raw/d1f887acdf59375add6c0d13afd08d90.png)

### Step 4. Configure a TencentDB for PostgreSQL security group
4.1 Log in to the [TencentDB for PostgreSQL console](https://console.cloud.tencent.com/postgres) and select the region. In the instance list, click the target instance ID or **Manage** in the **Operation** column to enter the instance management page.
4.2. On the instance management page, select the **Security Group** tab, click **Configure Security Group**, configure the security group rule to open all ports, and confirm that the security group allows access from public IPs. For more information on configuration, see [Managing Security Groups](https://intl.cloud.tencent.com/document/product/409/40112).
![](https://qcloudimg.tencent-cloud.cn/raw/9e21be547485994b56ee900b9c04fec6.png)

### Step 5. Check public network connectivity
You can use a client tool to access TencentDB for PostgreSQL at the connection address and port of the CLB instance. For detailed directions, see [Connecting to PostgreSQL Instances](https://intl.cloud.tencent.com/document/product/409/34626).


