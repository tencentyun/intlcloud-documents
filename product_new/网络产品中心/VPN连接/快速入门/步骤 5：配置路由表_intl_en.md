After you complete Step 4, the VPN tunnel is successfully configured. Next, you need to configure a route table to route the traffic of subnet A to the VPN gateway so that the IP range in subnet A can communicate with the IP range in the IDC.
1. Log in to [Tencent Cloud Console](https://console.cloud.tencent.com/) and choose **Products** > **Virtual Private Cloud** to access the VPC console.
2. Click **Subnet** in the left sidebar, select the region of you VPC, and click the ID of the route table associated with subnet A to go to the details page.
3. Click **+ New Routing Policies**.
4. In the pop-up box, enter the destination IP range (`10.0.1.0/24`), select **VPN Gateway** as the next hop type, and select the new VPN gateway `TomVPNGw` as the next hop.
 ![](https://main.qcloudimg.com/raw/e0d5d841e0fca5cd1c4cdeeeefd5e23a.png)
5. Click **OK**.