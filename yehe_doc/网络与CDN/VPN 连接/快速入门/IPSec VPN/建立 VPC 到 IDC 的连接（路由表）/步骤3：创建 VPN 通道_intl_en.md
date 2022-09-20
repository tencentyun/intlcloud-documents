1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. Click **VPN Connection** > **VPN Tunnel** in the left sidebar.
3. Choose a region and VPC (**Tokyo** and `VPC1` in this example) and click **+New**.
4. Enter the tunnel name (e.g. tunnel1). Choose the VPN gateway VPN1 and the customer gateway `UserGw1`, enter the pre-shared key (e.g. `123456`), and click **Next**.
>?Whether to enable the health check is optional. If it is enabled, please enter the local IP address and customer IP address. The former is the IP address available other than the primary CIDR block of the VPC, and the latter is the IP address available in the IDC. The health check is not enabled by default.
>
![]()
5. Select the destination route as the communication mode, and click **Next**.
![]()
6. (Optional) Configure IKE parameters. Click **Next** if no advanced configuration is required.
7. (Optional) Configure IPsec parameters. Click **Completed** if no configuration is required.
8. After you created the VPN tunnel successfully, return to the VPN tunnel list page. Click **More**and choose **Download config file** to complete the download.
 ![]()
