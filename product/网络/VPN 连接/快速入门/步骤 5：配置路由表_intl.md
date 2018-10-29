After the completion of Step 4, we have successfully configured a VPN tunnel. However, a route table should be configured to route the traffic of the subnet A to the VPN gateway before the IP address ranges in the subnet A can communicate with those in your IDC.
1. Log in to [Tencent Cloud Console](https://console.cloud.tencent.com/), and click **Products** -> **Virtual Private Cloud** to go to the VPC console.
2. In the left pane, click **Subnets**. Choose the region where your VPC is located and your VPC, i.e. **Guangzhou** and `TomVPC` in this example, and click the ID of the route table associated with the subnet A to go to the details page.
 ![](https://main.qcloudimg.com/raw/cdd9d95137ac9cee7f0c381d43395d73.png)
3. Click **+ New routing policies**
 ![](https://main.qcloudimg.com/raw/6b649b540f6e982b5a332051b1df2582.png)
4. In the pop-up box, enter the destination IP address range (`10.0.1.0/24`), select **VPN Gateway** for the next hop type, and then select the newly created VPN gateway `TomVPNGw`.
 ![](https://main.qcloudimg.com/raw/e0d5d841e0fca5cd1c4cdeeeefd5e23a.png)
5. Click **OK**.
