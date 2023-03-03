1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. Select **VPN Connections** > **VPN Tunnel** in the left sidebar.
3. Choose a region and VPC (**Tokyo** and `VPC1` in this example) and click **+New**.
4. Configure the basic settings of the VPN tunnel.
The basic settings of a VPN tunnel include the tunnel name, region of the gateway, network type, VPN gateway instance, customer gateway instance, pre-shared key, negotiation type, and communication mode. For more information about the parameters, see [Creating a VPN Tunnel](https://intl.cloud.tencent.com/document/product/1037/39635).
In this example, the communication mode is **Destination route**.
5. Configure the advanced settings.
In this step, you can set the advanced parameters, including DPD, health check, IKE, and IPsec. In this example, the default parameter values are used.
>?Make sure that the settings of IKE and IPsec on the cloud side are the same as those on the local side. Otherwise, the tunnel fails due to inconsistent protocol configurations.
>

6. After you created the VPN tunnel successfully, return to the VPN tunnel list page. Click **More** and choose **Download config file** to complete the download.
