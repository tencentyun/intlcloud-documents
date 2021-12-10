## Creating Unified Domain Name

1. Log in to the [GAAP console](https://console.cloud.tencent.com/gaap), enter the **Unified Domain Name** page, and click **Create**.
2. Configure the information of the **new unified domain name**.
![](https://main.qcloudimg.com/raw/ef657658a3746491785734a4b9436efe.png)
- Project: the project to which the unified domain name belongs. It can be changed later.
- Domain Name: it consists of up to 30 characters.
- Default Entry: the access address for regions without acceleration, which is typically the IP address of the origin server.

> ! The number of unified domain names is 5 by default. If you need more, contact your Tencent Cloud rep.

## Configuring Access Region

1. Enter the **[Unified Domain Name](https://console.cloud.tencent.com/gaap/domain)** page and click the specified domain name or **Set** to proceed to the next page.
    ![](https://qcloudimg.tencent-cloud.cn/raw/2be645caa6cbc7d1c0f6016e7ac70fec.png)
   - Domain Name: the domain name used for client access.
   - Default Entry: the access address for regions without acceleration, which is typically the IP address of the origin server.
   - Number of Connections: number of connections under the unified domain name.
   - Status: the unified domain name can work properly only in **Enabled** status.
2. Click **Add Settings** to pop up the **Adding Settings** window, select the acceleration region from the list as well as the access node, and click **OK** for them to take effect as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/1d5e8a5fb087abcd21c2ce17a94c12ef.png)

## Configuring Default Entry

After the globally unified domain name access service is activated, to avoid unnecessary network latency caused by detours and additional traffic fees, you need to configure the access path for users in the following types:

1. Users in or close to the origin region: they generally can access the origin server directly over the public network instead of using an acceleration connection.
2. Users far away from the acceleration connection entry region: they generally access the origin server directly over the public network. Accessing over an acceleration connection does not have an ideal acceleration effect.

On the **[Unified Domain Name](https://console.cloud.tencent.com/gaap/domain)** page, click the specified domain name or **Set** to proceed to the next page. Then, click the **Edit** icon on the right of the **Default Entry** at the top to configure the **Default Entry**.
After you configure the IP address of the entry, users in regions without acceleration will access your origin server directly at this IP over the public network.
![](https://qcloudimg.tencent-cloud.cn/raw/c549724b7ac191aa4b45ca7d97144ce0.png)
![](https://qcloudimg.tencent-cloud.cn/raw/3aa59862dd00d759ee4933d8cf7b2a34.png)

