1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. Click **VPN Connections** > **VPN Gateway** in the left directory to enter the admin page.
3. Choose a region (**Tokyo** in this example), and click **+New**.
>? If the **+New** button is grayed out and “No VPC available” is displayed when the mouse hovers over it, create a VPC as instructed in [Creating VPCs](https://intl.cloud.tencent.com/document/product/215/31805) before creating the VPN gateway. 
>
![](https://qcloudimg.tencent-cloud.cn/raw/e2a11579b443c9e5affdb0c842da5103.png)
4. In the pop-up dialog box, enter the VPN gateway name (such as VPN1), choose VPC as the associated network, choose VPC1 as the network it belongs to, and select the bandwidth cap and billing method.
>?
>- 200 MB, 500 MB and 1,000 MB bandwidths are currently only available in North China (Beijing), East China (Shanghai), South China (Guangzhou), Southwest China (Chengdu),  Hong Kong, Macao and Taiwan regions of China (Hong Kong, China), East China (Nanjing) and other availability zones. To use them, please <a href="https://console.cloud.tencent.com/workorder/category">submit a ticket</a>.
>- Only new gateways but not existing gateways are supported on 200 MB, 500 MB and 1,000 MB bandwidths.
>- If the VPN gateway uses 200 MB, 500 MB, or 1,000 MB bandwidth, AES128+MD5 is recommended for VPN tunnel encryption.
>
![](https://qcloudimg.tencent-cloud.cn/raw/de9c596b396c72604f643b4dc88fc47c.png)
5. Click **Create**. After the VPN gateway is created, the system randomly assigns it a public IP address such as `119.29.147.109`.
    ![](https://qcloudimg.tencent-cloud.cn/raw/10ddbbb6350f585850445fcf73a86ec2.png)
