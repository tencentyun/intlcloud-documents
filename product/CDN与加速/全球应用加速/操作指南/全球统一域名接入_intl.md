Generally, multiple acceleration connections are created for the same origin server to cover users in different acceleration regions. To allow users in multiple regions to access the origin server using the same domain name, you can configure DNS to enable nearby access through a unified domain name.

If you have activated the connection group service, you can activate the globally unified domain name access service for your connection group. You will get a unified domain name, and adjust the acceleration regions covered by each connection on the configuration page, so users can access the origin server region through the connection or public network.
## Activating globally unified domain name access
In connection group list, click the ID or name of a connection group to enter its details page, and click **Global Unified Domain Name Access** on the top:
- Read the service description thoroughly and click **Activate Service**.
![](https://main.qcloudimg.com/raw/153e67534e7a49bce047209f07486ef8.png)

- After the service is activated, the system will configure acceleration regions covered by each acceleration connection in the connection group. In principle, an acceleration region should be close to the entry or with low access latency to the entry over the public network.
![](https://main.qcloudimg.com/raw/2c114cd64be71a6ee2ccd281ee8b599d.png)

## Configuring an acceleration region
After the globally unified domain name service is activated, the system will configure default acceleration regions for each of your connections. You can also click **Modify** in the operation column to add/delete acceleration regions covered by a connection for more accurate coverage.
![](https://main.qcloudimg.com/raw/2fed708fb9f360ba9b63983b8444b6e9.png)
Click **OK** after making the adjustment.

## Configuring the default entry
After the globally unified domain name access service is activated, global users can access the origin server through this domain name. You need to manage the access paths for the following users, otherwise there will be unnecessary network latency caused by detours and unnecessary traffic fees incurred therefrom:

- **Users in the origin server region**: in principle, users in the origin server region can access the origin server directly via the public network to ensure minimum latency, instead of using an acceleration connection.
- **Users in regions close to the origin server region or far away from the acceleration connection entry**: users in these regions can access the origin server directly via the public network with low latency, while connecting to an acceleration connection may not achieve a better result.

On the acceleration region configuration page, "Default Entry" is provided. When you configure the IP address of the entry, both users in regions covered by the acceleration connection and users in other regions can directly access your origin server using this IP address over the public network.

Click **Create** or **Modify** to the right of "Default Entry", and enter an IP address in the pop-up dialog box:
![](https://main.qcloudimg.com/raw/79702e1970c9fa9b763f9da93356f213.png)

Click **OK** after entering the IP address.
>After returning to the details page, click **Save** and the change will take effect.
![](https://main.qcloudimg.com/raw/8af4dd0cd137597641a2b40a245af25f.png)


