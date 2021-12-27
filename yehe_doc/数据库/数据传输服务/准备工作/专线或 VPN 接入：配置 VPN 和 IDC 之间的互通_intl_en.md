## Overview
If the access type is VPN gateway, you need to create a VPC and VPN and establish a tunnel between the VPN and IDC for interconnection.

In this scenario, your VPC is "TomVPC", your subnet is "subnet A", and the IP range of “subnet A” is `192.168.1.0/24`. The created VPN gateway is "TomVPNGW", the public IP of the VPN gateway is `203.195.147.82`, the subnet IP range of your IDC is `10.0.1.0/24`, the public IP of the VPN gateway in your IDC is `202.108.22.5`, and the IP address of the source database server is `10.0.1.8`.

![](https://qcloudimg.tencent-cloud.cn/raw/86936527e538a841b69bb703ac8a0837.png)

## Directions
Configure as instructed in [Overview](https://intl.cloud.tencent.com/document/product/1037/32689).

## Subsequent Steps
1. After the VPN is connected to your IDC, on the [DTS task page](https://console.cloud.tencent.com/dts/migration), select **VPN Access**.
<table>
<thead><tr><th><strong>Parameter</strong></th><th><strong>Description</strong></th><th><strong>Sample Value</strong></th></tr></thead>
<tbody><tr>
<td>VPN Gateway</td>
<td>Name of the VPN gateway created in the VPC.</td>
<td>TomVPNGW</td></tr>
<tr>
<td>VPC</td>
<td>Name of your VPC.</td>
<td>TomVPC</td></tr>
<tr>
<td>Subnet</td>
<td>Name of the subnet of your VPC.</td>
<td>Subnet A</td></tr>
<tr>
<td>Host Address</td>
<td>IP address of the source database server.</td>
<td>10.0.1.8</td></tr>
<tr>
<td>Port</td>
<td>Port used by the source database. Below are the default ports for common databases (if they are modified, enter the actual ports): <br><ul><li>MySQL: 3306</li><li>SQL Server: 1433</li><li>PostgreSQL: 5432</li><li>MongoDB: 27017</li><li>Redis: 6379</li></ul></td>
<td>3306</td></tr>
</tbody></table>
2. Click **Test Connectivity**. If the test fails, troubleshoot as follows:
   - The Telnet test fails.
     In the created VPC ("TomVPC" in this example), purchase a CVM instance and ping the source database server address from it:
      - If the address is unpingable:
        - [The source database has a security group or firewall configured](https://intl.cloud.tencent.com/document/product/571/42552).
        - [The SNAT IP address is blocked in the source database](https://intl.cloud.tencent.com/document/product/571/42552).
        - The port settings of the source database are incorrect.     
      - If the address is pingable:
        [Submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.
   - The Telnet test is passed, but the database connection fails.
     - The migration account is not properly authorized. Authorize it again as instructed in the corresponding scenario in [data migration](https://intl.cloud.tencent.com/document/product/571/42645) and [data sync](https://intl.cloud.tencent.com/document/product/571/42624).
     - The account or password is incorrect.
     

 

 
