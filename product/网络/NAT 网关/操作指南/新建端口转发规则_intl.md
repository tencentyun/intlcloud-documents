Port forwarding table is a configuration table on an NAT gateway and is used to configure the DNAT feature on the NAT gateway. It maps the **[private IP, protocol and port]** of a CVM in the VPC to a **[public IP, protocol and port]** in the public network, so that the resources on the CVM can be accessed from the public network.
You can create port forwarding rules by following the steps below.
1. Log in to [Tencent Cloud Console](https://console.cloud.tencent.com/), select **Products** -> **Virtual Private Cloud** to go to the VPC console, and then click **NAT Gateway** on the left pane.
2. In the list page, select the NAT gateway to be modified to go to its details page, and click **Port Forwarding** in the tab.
 ![1](https://main.qcloudimg.com/raw/63cc05adc23859e8ce500862d121a483.png)
3. Click **New**, select the protocol, external IP port and internal IP port, and then click **OK**.
 >**Note:**
 >The internal IP only supports the private IP of the CVM within the VPC.

 ![2](https://main.qcloudimg.com/raw/cd128b49e9a1e9bf81da3cd23ecef4d3.png)

