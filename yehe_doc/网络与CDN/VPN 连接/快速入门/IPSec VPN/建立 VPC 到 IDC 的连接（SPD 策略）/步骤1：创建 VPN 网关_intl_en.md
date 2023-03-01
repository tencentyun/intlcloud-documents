This document describes how to create a VPN gateway.

## Directions
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. Select **VPN Connections** > **VPN Gateway** in the left sidebar to enter the admin page.
3. Choose a region, for example, **Guangzhou**, and click **+Create**.
>? If the **+New** button is grayed out and “No VPC available” is displayed when the mouse hovers over it, create a VPC as instructed in [Creating VPCs](https://intl.cloud.tencent.com/document/product/215/31805) before creating the VPN gateway. 
>

4. Enter a name for the VPN gateway, such as TomVPNGw. Select the associate network, subordinate network, bandwidth cap, labels, and billing method, and click **Create**. After the VPN gateway is created, the system randomly assigns a public IP address, such as `203.195.147.82`.
>?
>- 200 Mbps, 500 Mbps, 1,000 Mbps, and 3,000 Mbps bandwidths are available only in the following availability zones: North China (Beijing), East China (Shanghai), South China (Guangzhou), Southwest China (Chengdu), Hong Kong, Macao and Taiwan regions of China( Hong Kong, China), and East China (Nanjing). To use the bandwidths, please <a href="https://console.cloud.tencent.com/workorder/category">submit a ticket</a>.
>- Only new gateways can use 200 Mbps, 500 Mbps, 1,000 Mbps, and 3,000 Mbps bandwidths. Existing gateways cannot use the preceding bandwidths.
>- If the VPN gateway uses the 200 Mbps, 500 Mbps, 1,000 Mbps, or 3,000 Mbps bandwidth, we recommend that you use AES128+MD5 for VPN tunnel encryption.
>

<img src="https://qcloudimg.tencent-cloud.cn/raw/000302a4f734a94744f70bf552308ddc.png" width="70%">

>?The labels are alternatively configured, please retain the default settings.
>

## References
[Step 2: Create a Customer Gateway](https://intl.cloud.tencent.com/document/product/1037/32691)
[Step 3: Create a VPN Tunnel](https://intl.cloud.tencent.com/document/product/1037/32692)
[Step 4: Load the Configuration of the Local Gateway](https://intl.cloud.tencent.com/document/product/1037/32693)
[Step 5: Configure a Routing Table](https://intl.cloud.tencent.com/document/product/1037/32694)
[Step 6: Activate a VPN Tunnel](https://intl.cloud.tencent.com/document/product/1037/32695)
