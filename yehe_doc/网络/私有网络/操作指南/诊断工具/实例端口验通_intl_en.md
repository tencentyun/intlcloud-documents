The instance port verification feature can help you detect the accessibility of security group ports of CVM instances, locate faults, and enhance the user experience.
The following ports can be verified:
 <table>
<thead>
<tr>
<th>Rule type</th>
<th>Port</th>
<th>Note</th>
</tr>
</thead>
<tbody>
<tr>
<td rowspan="7">Inbound rules</td>
<td>TCP:3389</td>
<td>Used to permit Windows remote login.</td>
</tr>
<tr>
<td>TCP:22</td>
<td>Used to permit Linux SSH login.</td>
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
<td rowspan="2">Used to permit uploads and downloads over FTP.</td>
</tr>
<tr>
<td>TCP:20</td>
</tr>
<tr>
<td>ICMP protocol</td>
<td>Used to provide website HTTP service.</td>
</tr>
<tr>
<td>Outbound rules</td>
<td>ALL</td>
<td>Used to permit all outbound traffic for access to external networks.</td>
</tr>
</tbody></table>

## Operation Guide
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc).
2. Click **Diagnostic Tools** -> **Instance Port Verification** in the directory on the left to enter the management page.
3. Select **Region** at the top of the page and, in the displayed list, find the instance to be verified and click **Quick Check** in the same row.
![](https://main.qcloudimg.com/raw/04780280964c1d63698423b22ce764f5.png)
4. You can see the port verification details in the pop-up window. To open ports that are not open to the Internet, click **Open All Ports**.
>? **Open All Ports** will open all listed ports. If you only need to open certain ports (such as `TCP:22`), add an inbound rule on the [Security Group Console](https://console.cloud.tencent.com/vpc/securitygroup) to open port `TCP:22`. For more information, see [Adding Security Group Rules](https://intl.cloud.tencent.com/document/product/215/35513).

![](https://main.qcloudimg.com/raw/b7f208cca3943ecefacd791f30533911.png)
