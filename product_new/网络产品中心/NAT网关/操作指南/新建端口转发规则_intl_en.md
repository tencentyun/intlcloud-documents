A port forwarding table is a configuration table on a NAT gateway that is used to configure the DNAT feature on the NAT gateway. It maps the **[private IP, protocol and port]** collection of a CVM in the VPC to another **[public IP, protocol and port]** collection in the public network, so that resources on the CVM can be accessed from the public network.
You can create port forwarding rules by completing the steps below.
1. Log in to [Tencent Cloud Console](https://console.cloud.tencent.com/) and choose **Products** > **Virtual Private Cloud* to open the VPC console. Then, click **NAT Gateway** in the left sidebar.
2. In the list, click the ID of the desired NAT gateway to go to its details page. Click **Port Forwarding** tab.
 ![1](https://main.qcloudimg.com/raw/63cc05adc23859e8ce500862d121a483.png)
3. Click **New**, select the protocol, external and internal IP ports, and click **OK**.
 >The internal IP address only supports the private IP address of a CVM within the VPC.
 >
![](https://main.qcloudimg.com/raw/0b25c6a707aaeb6ab122e7e7d418d00e.png)
