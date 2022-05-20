This document describes how to create a VPN tunnel.

## Directions
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. Click **VPN Connection** > **VPN Tunnel** in the left sidebar.
3. Choose the region where your VPC is located and your VPC, i.e. **Guangzhou** and `TomVPC` in this example, and click **+New**.
 ![]()
4. Enter a name for the tunnel (for example, TomVPNConn), select the VPN gateway `TomVPNGw` and the customer gateway `TomVPNUserGw`, enter the pre-shared key (for example, `123456`), and click **Next**.
>?The labels are alternatively configured, please retain the default settings.
>
![]()
5. Select the communication mode, and enter an SPD policy to limit the communication between local IP ranges and customer IP ranges. In this example, the local IP range is `192.168.1.0/24` of subnet A, and the customer IP range is `10.0.1.0/24`. Then, click **Next**.
![]()
6. (Optional) Configure IKE parameters. Click **Next** if no advanced configuration is required.
 ![](https://main.qcloudimg.com/raw/4c003c6438a4c8e47e8057113edb1371.png)
7. (Optional) Configure IPsec parameters. Click **Completed** if no configuration is required.
 ![](https://main.qcloudimg.com/raw/3fe3a316218c475f6b5bfcf7a871167a.png)
 8. After the VPN tunnel is successfully created, return to the VPN tunnel list page. Click **More**and choose **Download config file** to complete the download.
 ![](https://main.qcloudimg.com/raw/00575f0bbbfb9aae0442731db89d042c.png)
