Before creating a VPN tunnel, you need to create a customer gateway:
1. Log in to [Tencent Cloud Console](https://console.cloud.tencent.com/), and click **Products** -> **Virtual Private Cloud** to go to the VPC console.
2. Click **VPN Connection** -> **VPN Tunnel** in the left pane to go to the management page.
3. Choose the region where your VPC is located and your VPC, i.e. **Guangzhou** and `TomVPC` in this example, and click **New**.
 ![](https://main.qcloudimg.com/raw/ad0f45003e1423b7e6bb8da4bd10a26f.png)
4. Enter the name of the tunnel (e.g. TomVPNConn), select the VPN gateway `TomVPNGw` and the customer gateway` TomVPNUserGw`, enter the pre-shared key (e.g. `123456`), and then click **Next**.
 ![](https://main.qcloudimg.com/raw/6264903e7ad42e14e9e437e6658966a2.png)
5. Enter the SPD policy to limit the communication between local IP address ranges and customer IP address ranges. In this example, the local IP address range is `192.168.1.0/24` of the subnet A, and the customer IP address range is` 10.0.1.0/24`. Then, click **Next**.
 ![](https://main.qcloudimg.com/raw/3136826f025a8ce8d3d8dc722d4e0394.png)
6. (Optional) Configure IKE parameters. If you do not need advanced configurations, click **Next**.
 ![](https://main.qcloudimg.com/raw/c370884071d8dd5424be80bbef1e9aec.png)
7. (Optional) Configure IPsec parameters. Click **Finish** if you don't need these parameters.
 ![](https://main.qcloudimg.com/raw/6c67f435c015fb6d2e03ed96dc61b7f7.png)
8. After the customer gateway is successfully created, return to the VPN tunnel list page, and click **Download Profile** to complete the download.
 ![](https://main.qcloudimg.com/raw/3ee49248be8efe8d6910cb85461ef641.png)
