Before creating a VPN tunnel, you need to create a customer gateway.
1. Log in to [Tencent Cloud Console](https://console.cloud.tencent.com/) and choose **Products** > **Virtual Private Cloud** to access the VPC console.
2. In the left sidebar, choose **VPN Connection** > **VPN Tunnel** to go to the management page.
3. Select the region where your VPC is located and your VPC, and click **+ New**.
4. Enter a name for the tunnel (for example, TomVPNConn), select the VPN gateway `TomVPNGw` and the customer gateway `TomVPNUserGw`, enter the pre-shared key (for example, `123456`), and click **Next**.
 ![](https://main.qcloudimg.com/raw/6264903e7ad42e14e9e437e6658966a2.png)
5. Enter an SPD policy to limit the communication between local IP ranges and customer IP ranges. In this example, the local IP range is `192.168.1.0/24` of subnet A, and the customer IP range is `10.0.1.0/24`. Then, click **Next**.
 ![](https://main.qcloudimg.com/raw/3136826f025a8ce8d3d8dc722d4e0394.png)
6. (Optional) Configure IKE parameters. Click **Next** if no advanced configuration is required.
 ![](https://main.qcloudimg.com/raw/c370884071d8dd5424be80bbef1e9aec.png)
7. (Optional) Configure IPsec parameters. Click **Complete** if no configuration is required.
 ![](https://main.qcloudimg.com/raw/6c67f435c015fb6d2e03ed96dc61b7f7.png)
8. After the VPN tunnel is successfully created, return to the VPN tunnel list page and click **Download config file** to complete the download.
 ![](https://main.qcloudimg.com/raw/3ee49248be8efe8d6910cb85461ef641.png)