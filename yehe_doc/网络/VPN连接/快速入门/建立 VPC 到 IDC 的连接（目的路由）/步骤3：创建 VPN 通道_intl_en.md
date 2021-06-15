1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. Click **VPN Connection** > **VPN Tunnel** on the left sidebar to go to the management page.
3. Choose a region and VPC (**Tokyo** and **VPC1** in this example) and click **+New**.
4. Enter the tunnel name (e.g. **tunnel1**). Choose the VPN gateway **VPN1** and the customer gateway **UserGw1**, enter the pre-shared key (e.g. **123456**), and click **Next**.
>?Health check is optional and is disabled by default. If it is enabled, please enter the VPN gateway IP address (an available IP not included in the primary CIDR block of the VPC), and the customer gateway IP (an available IP in the IDC IP range). 
5. On the **SPD Policy** page, configure both the VPN gateway and customer gateway IP as **0.0.0.0/0**, and click **Next**.
6. (Optional) Configure IKE parameters. Click **Next** if no advanced configuration is required.
7. (Optional) Configure IPsec parameters. Click **Complete** if no configuration is required.
8. After the VPN tunnel is successfully created, return to the VPN tunnel list page. Click **More**and choose **Download config file** to complete the download.
   
