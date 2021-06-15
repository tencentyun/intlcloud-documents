You need to perform several steps to make a VPN connection effective. Then you can configure the IPsec VPN on the console in a self-service manner. An example is described below.
## Example
Use an IPsec VPN connection to connect subnet A `192.168.1.0/24` in your VPC (TomVPC) in **Guangzhou** to the subnet `10.0.1.0/24` in your IDC. The public IP address of the VPN gateway in your IDC is `202.108.22.5`.
![](https://main.qcloudimg.com/raw/8a2e5c1c1f1a28233b7735f84a525635.png)
## Directions
The flowchart of activating the VPN connection is shown below:
![](https://main.qcloudimg.com/raw/1aa819dbe82889063db1afc22ec7097e.png)
For details about the steps, click the following links:
- [Step 1: Create a VPN Gateway](https://intl.cloud.tencent.com/document/product/1037/32690)
- [Step 2: Create a Customer Gateway](https://intl.cloud.tencent.com/document/product/1037/32691)
- [Step 3: Create a VPN Tunnel](https://intl.cloud.tencent.com/document/product/1037/32692)
- [Step 4: Configure a Local Gateway](https://intl.cloud.tencent.com/document/product/1037/32693)
- [Step 5: Configure a Routing Policy](https://intl.cloud.tencent.com/document/product/1037/32694)
- [Step 6: Activate the VPN Tunnel](https://intl.cloud.tencent.com/document/product/1037/32695)
