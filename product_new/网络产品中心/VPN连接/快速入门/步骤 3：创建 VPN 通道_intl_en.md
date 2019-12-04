Before creating a VPN tunnel, you need to create a customer gateway.
1. Log in to [Tencent Cloud Console](https://console.cloud.tencent.com/) and choose **Products** > **Virtual Private Cloud** to access the VPC console.
2. In the left sidebar, choose **VPN Connection** > **VPN Tunnel** to go to the management page.
3. Select the region where your VPC is located and your VPC, and click **+ New**.
4. Enter a name for the tunnel (for example, TomVPNConn), select the VPN gateway `TomVPNGw` and the customer gateway `TomVPNUserGw`, enter the pre-shared key (for example, `123456`), and click **Next**.
 ![](https://main.qcloudimg.com/raw/16563ad3fdf63ce147bd2ffa35e5d014.png)
5. Enter an SPD policy to limit the communication between local IP ranges and customer IP ranges. In this example, the local IP range is `192.168.1.0/24` of subnet A, and the customer IP range is `10.0.1.0/24`. Then, click **Next**.
 ![](https://main.qcloudimg.com/raw/ee39d49c99ab4cd5883af7d2adb71788.png)
6. (Optional) Configure IKE parameters. Click **Next** if no advanced configuration is required.
 ![](https://main.qcloudimg.com/raw/4c003c6438a4c8e47e8057113edb1371.png)
7. (Optional) Configure IPsec parameters. Click **Complete** if no configuration is required.
 ![](https://main.qcloudimg.com/raw/3fe3a316218c475f6b5bfcf7a871167a.png)
8. After the VPN tunnel is successfully created, return to the VPN tunnel list page and click **Download config file** to complete the download.
 ![](https://main.qcloudimg.com/raw/00575f0bbbfb9aae0442731db89d042c.png)
