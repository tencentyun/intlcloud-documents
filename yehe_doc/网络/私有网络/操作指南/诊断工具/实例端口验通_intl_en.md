The instance port verification feature can help you detect the port accessibility of a security group associated with CVM instances, locate faults, and improve the user experience.
The following ports can be verified:
 <table>
<thead>
<tr>
<th>Rule</th>
<th>Port</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td rowspan="7">Inbound rules</td>
<td>TCP:3389</td>
<td>Used to allow Windows remote login.</td>
</tr>
<tr>
<td>TCP:22</td>
<td>Used to allow Linux SSH login.</td>
</tr>
<tr>
<td>TCP:443</td>
<td>Used to provide website HTTPS service.</td>
</tr>
<tr>
<td>TCP:80</td>
<td>Used to provide website HTTP service.</td>
</tr>
<tr>
<td>TCP:21</td>
<td rowspan="2">Used to allow uploads and downloads over FTP.</td>
</tr>
<tr>
<td>TCP:20</td>
</tr>
<tr>
<td>ICMP protocol</td>
<td>Used to provide website HTTP service. ICMP is a control protocol, and no ports are involved.</td>
</tr>
<tr>
<td>Outbound rules</td>
<td>ALL</td>
<td>Used to allow all outbound traffic for access to external networks.</td>
</tr>
</tbody></table>

## Operations Guide
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc).
2. Click **Diagnostic Tools** > **Port Verification** in the left sidebar to access the management page.
3. Select a region at the top of the page, locate the instance to be verified in the list, and click **Quick Check**.
![](https://main.qcloudimg.com/raw/04780280964c1d63698423b22ce764f5.png)
4. You can see the port verification details in the pop-up window. To open ports that are not open to the Internet, click **Open all ports**.
![](https://main.qcloudimg.com/raw/b7f208cca3943ecefacd791f30533911.png)
If you only need to open certain ports (such as `TCP:22`), add an inbound rule on the [Security Group console](https://console.cloud.tencent.com/vpc/securitygroup) to open port TCP:22. You can also select **all** for **Source** to open all IPs, or enter a specific IP (IP range), as shown below:
![](https://main.qcloudimg.com/raw/6780b4df05168e19718ffe6c699c5159.png)

## Relevant Information
- For information on security groups, see [Security Group Overview](https://intl.cloud.tencent.com/document/product/215/38750) and [Adding a Security Group Rule](https://intl.cloud.tencent.com/document/product/215/35513).
- For more information about ports, see [Common Server Ports](https://intl.cloud.tencent.com/document/product/215/35520).
