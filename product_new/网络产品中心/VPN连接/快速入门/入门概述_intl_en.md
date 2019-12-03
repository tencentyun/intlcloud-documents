You need to perform several steps to make a VPN connection effective. Then you can configure the IPsec VPN on the console in a self-service manner. An example is described below.
## Example
Use an IPsec VPN connection to connect subnet A `192.168.1.0/24` in your VPC (TomVPC) in **Guangzhou** to the subnet `10.0.1.0/24` in your IDC. The public IP address of the VPN gateway in your IDC is `202.108.22.5`.
![](//mc.qcloudimg.com/static/img/0cfc46cf11e4d53164219b1c386509a1/1.png)
## Directions
The flowchart of activating the VPN connection is shown below:
![](https://main.qcloudimg.com/raw/8f017e7278462b27bf2aae995e6c280a.png)
For details about the steps, click the following links:
- [Step 1: Create a VPN gateway](https://cloud.tencent.com/document/product/554/18989)
- [Step 2: Create a customer gateway](https://cloud.tencent.com/document/product/554/18990)
- [Step 3: Create a VPN tunnel](https://cloud.tencent.com/document/product/554/18991)
- [Step 4: Configure a local gateway](https://cloud.tencent.com/document/product/554/18992)
- [Step 5: Configure a route table](https://cloud.tencent.com/document/product/554/18993)
- [Step 6: Activate the VPN tunnel](https://cloud.tencent.com/document/product/554/18994)
