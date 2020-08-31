By using the instance port verification feature, you can check the accessibility of the security group ports of CVM instances, locate faults, and enhance user experience.
The following ports can be verified:
 <table>
<thead>
<tr>
<th>Rule Type</th>
<th>Port</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td rowspan="7">Inbound rule</td>
<td>TCP: 3389</td>
<td>It is used to permit Windows remote login.</td>
</tr>
<tr>
<td>TCP: 22</td>
<td>It is used to permit Linux SSH login.</td>
</tr>
<tr>
<td>TCP: 443</td>
<td>It is used to provide website HTTPS service.</td>
</tr>
<tr>
<td>TCP: 80</td>
<td>It is used to provide website HTTP service.</td>
</tr>
<tr>
<td>TCP: 21</td>
<td rowspan="2">It is used to permit the upload and download features for FTP service.</td>
</tr>
<tr>
<td>TCP: 20</td>
</tr>
<tr>
<td>ICMP protocol</td>
<td>It is used to provide website HTTP service.</td>
</tr>
<tr>
<td>Outbound rule</td>
<td>All</td>
<td>It is used to permit all outbound traffic for accessing external networks.</td>
</tr>
</tbody></table>

## Operation Instructions
1. Log in to [VPC Console](https://console.cloud.tencent.com/vpc).
2. Click **Diagnostic Tools** > **Instance Port Verification** in the left sidebar to enter the management page.
3. In the row of the instance that you want to verify, click **Quick Check**.
![](https://main.qcloudimg.com/raw/04780280964c1d63698423b22ce764f5.png)
4. In the pop-up window, you can see the details of the port verification. To open ports that are not open to the Internet, click **Open All Ports**.
>**Open All Ports** will open all listed ports. To open certain ports, add rules in [Security Group Console](https://console.cloud.tencent.com/vpc/securitygroup).
>
![](https://main.qcloudimg.com/raw/b7f208cca3943ecefacd791f30533911.png)

## Relevant Information
- For more information about the common server ports, see [Common Server Ports](https://intl.cloud.tencent.com/document/product/215/35520).
