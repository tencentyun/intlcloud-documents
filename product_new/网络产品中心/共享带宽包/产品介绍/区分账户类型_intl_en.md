
There are two types of Tencent Cloud BWPs:
## Device Bandwidth Package
Device Bandwidth Package applies to an account that specifies the public network capacity (bandwidth cap) and billing method (bill-by-traffic or bill-by-bandwidth) of a CVM instance when creating it, with public IP address and CLB acting only as public network egress. This kind of BWP is referred to as "Device BWP".
## IP Bandwidth Package
IP Bandwidth Package applies to an account that specifies the public network capacity (bandwidth cap) and billing method (bill-by-traffic or bill-by-bandwidth) of a public IP address when creating it. This kind of BWP is referred to as "IP BWP".

## Differentiating Two Account Types
Log in to [EIP Console](https://console.cloud.tencent.com/cvm/eip):
- If no “Bandwidth” column can be found, the BWP purchased by the account is “Device BWP”. The EIPs are bare IP addresses without public network attributes, and you need to purchase a public network for the backend resources before accessing the public network via a public IP address or CLB. Currently, most customers are using this kind of accounts, as shown in the figure below:
![](https://main.qcloudimg.com/raw/a91a1d2d4e3dfd86755e1103f8c30c23.png)
- If you can find the “Bandwidth” column, the BWP purchased by the account is “IP BWP”.
