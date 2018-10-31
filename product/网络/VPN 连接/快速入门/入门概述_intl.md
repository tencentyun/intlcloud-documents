You need to complete several steps to make the VPN connection effective, and then you can fully customize an IPsec VPN in the console, which will be illustrated below.
## Example
Through an IPsec VPN connection, connect the subnet A `192.168.1.0/24` in your VPC ("TomVPC") in **Guangzhou** with the subnet `10.0.1.0/24` in your IDC, and the public IP of the VPN gateway in your IDC is `202.108.22.5`.
![](//mc.qcloudimg.com/static/img/0cfc46cf11e4d53164219b1c386509a1/1.png)
## Description
The process to activate a VPN connection is depicted in the following figure:
![](https://main.qcloudimg.com/raw/8f017e7278462b27bf2aae995e6c280a.png)
Please refer to the following steps to proceed:
- [Step 1: Create a VPN Gateway](/document/product/554/18989)
- [Step 2: Create a Customer Gateway](/document/product/554/18990)
- [Step 3: Create a VPN tunnel](/document/product/554/18991)
- [Step 4: Load Configurations into Local Gateway](/document/product/554/18992)
- [Step 5: Configure the Route Table](/document/product/554/18993)
- [Step 6: Activate the VPN tunnel](/document/product/554/18994)

