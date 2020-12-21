## Creating a Unified Domain Name
Click **Create** in the **Unified Domain Name** page, select a project in the pop-up window and enter the domain name, IP, or the domain name of the default entry.
![](https://main.qcloudimg.com/raw/ef657658a3746491785734a4b9436efe.png)

## Access Region Settings
Click the target domain name or **Set** on the right of it to enter its settings page. Click **Add Setting Item** and then select the nearest acceleration region and connection in the pop-up window, and finally click **OK**.
![](https://main.qcloudimg.com/raw/9ebb9dbdffbe57a7438b8ce169b9dd1e.png)

## Configuring the Default Entry
After the globally unified domain name access service is enabled, global users can access the origin server through this domain name. You need to manage the access paths for the following users. Otherwise, detours will cause unnecessary network latency and incur unnecessary traffic fees:
- Users in the origin server region: in principle, they can access the origin server directly via the public network to ensure minimum latency, instead of using an acceleration connection.
- Users in regions close to the origin server region or far away from the acceleration connection entry: they can access the origin server directly via the public network with low latency, while connecting to an acceleration connection may not achieve a better result.

In the acceleration region configuration page, a **Default Entry** is provided. After the IP address of the entry is configured, both users in regions covered by the acceleration connection and users in other regions can directly access your origin server using this IP address over the public network.

In the **Unified Domain Name** page, click the target domain name or **Set** on the right of it to enter its settings page. Click the pencil icon next to **Default Entry** to configure the entry.![](https://main.qcloudimg.com/raw/9f2f9980950bdb8b0273c0015b5a777d.png)
