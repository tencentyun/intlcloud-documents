
A [security group](https://cloud.tencent.com/document/product/213/12452) is a stateful virtual firewall capable of filtering. As an important means for network security isolation provided by Tencent Cloud, it can be used to set network access controls for one or more TencentDB instances. Instances with the same network security isolation demands in one region can be put into the same security group, which is a logical group. TencentDB and CVM share the security group list and are matched with each other within the security group based on rules. For more information on rules and restrictions, please see Security Group Description.

>?As TDSQL-A for PostgreSQL does not have active outbound traffic, outbound rules are not applicable to it.

## Configuring Security Group
1. Log in to the [TDSQL-A for PostgreSQL](https://console.cloud.tencent.com/tdsqla/tdapg) console and click an instance ID in the instance list to enter the instance management page.
2. On the instance management page, select the **Security Group** tab and click **Configure Security Group**.
![](https://main.qcloudimg.com/raw/cae61babfb1e6fc68b6d884a874720b0.png)
3. In the pop-up window, select the security group to be bound and click **OK**.
![](https://main.qcloudimg.com/raw/8e5b230fa3bd2417d6dc304fbadaea7f.png)
4. After the security group is successfully configured, you can view its information at the bottom of the **Security Group** tab.

## Deleting Security Group
1. Log in to the [TDSQL-A for PostgreSQL](https://console.cloud.tencent.com/tdsqla/tdapg) console and click an instance ID in the instance list to enter the instance management page.
2. On the instance management page, select the **Security Group** tab, and click <img src="https://main.qcloudimg.com/raw/5ee603dd3dcf82d92cf230cb64ddbe8e.png"  style="margin:0;"> in the **Operation** column to delete a security group. The corresponding rules will be deleted at the same time.
![](https://main.qcloudimg.com/raw/2a467f8f3c74c7eb6a95d39d22f124c6.png)
