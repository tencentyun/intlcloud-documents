This file introduces how to create a VPN gateway.
## Directions
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. Click **VPN Connection** > **VPN Gateway** in the left directory to enter the admin page.
3. Choose a region, for example, **Guangzhou**, and click **+Create**.
>? If the **+Create** button is grayed out and “No VPC available” is displayed when the mouse hovers over it, [create a VPC](https://intl.cloud.tencent.com/document/product/215/31805) before creating the VPN gateway. 
>
4. Enter a name for the VPN gateway (for example, TomVPNGw), select the associate network, subordinate network, bandwidth limit, labels, and billing method, and click **Create**. After the VPN gateway is created, the system randomly assigns a public IP address, for example, `203.195.147.82`.
>?
>- 200 MB, 500 MB and 1,000 MB bandwidths are currently only available in North China (Beijing), East China (Shanghai), South China (Guangzhou), Southwest China (Chengdu),  Hong Kong, Macao and Taiwan regions of China(Hong Kong, China), East China (Nanjing) and other availability zones. If needed, please <a href="https://console.cloud.tencent.com/workorder/category">submit a ticket</a>.
>- Only new gateways but not existing gateways are supported on 200 MB, 500 MB and 1,000 MB bandwidths. 
>- If the VPN gateway uses 200 MB, 500 MB, or 1,000 MB bandwidth, AES128+MD5 is recommended for VPN tunnel encryption.
>
![](https://main.qcloudimg.com/raw/990f568ffc28ef1374a578883fea96f5.png)
>?The labels are alternatively configured, please retain the default settings.
