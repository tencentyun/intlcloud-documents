The instance port verification feature can help you detect the port accessibility of a security group associated with CVM instances, locate faults, and improve the user experience.
This feature supports the accessibility detection of common ports and custom ports. See below for the common ports.
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
<td>ICMP protocol</td>
<td>Used to pass control messages such as the ping command. ICMP is a control protocol, and no ports are involved.</td>
</tr>
<tr>
<td>TCP:20</td>
<td rowspan="2">Used to allow uploads and downloads over FTP.</td>
</tr>
<tr>
<td>TCP:21</td>
</tr>
<tr>
<td>TCP:22</td>
<td>Used to allow Linux SSH login.</td>
</tr>
<tr>
<td>TCP:3389</td>
<td>Used to allow Windows remote login.</td>
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
<td>Outbound rules</td>
<td>ALL</td>
<td>Used to allow all outbound traffic for access to external networks.</td>
</tr>
</tbody></table>

## Operation Guide
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc).
2. Click **Diagnostic Tools** > **Port Verification** in the left sidebar to access the management page.
3. Select a region at the top of the page, locate the instance you want to verify in the list, and click **Quick Check**.
4. You can see the port detection details in the pop-up window. Perform the following operations as needed.
   + Uncheck the port that you do not want to detect.
   + Enter custom ports to detect and click **Save**.
      + Protocol: select TCP or UDP.
      + Port: enter one port number to detect, which cannot be the same as a common port. Otherwise, you need to first uncheck the common port before continuing.
      + Direction: select **Inbound** or **Outbound**.
      + IP: enter the source IP for the inbound direction and destination IP for the outbound direction. Enter **ALL** for all source and destination IP addresses.
      + Up to 15 custom ports can be detected.
   
 If you need to detect the outbound traffic towards IP 10.0.1.12 using TCP protocol through port 30, enter the following information in the **Custom port detection** area.

5. After completing the configuration, click **Detect**. The result will be displayed in the **Policy** column.
<p>Assumes that you need to open an <b>Not opened</b> port, for example`TCP:22`, </p>
<p>Then you can add an inbound rule for the security group associated with the instance in the <a href="https://console.cloud.tencent.com/vpc/securitygroup">Security Group console</a> to open port TCP:22. You can select <b>all</b> for <b>Source</b> to allow all IPs, or enter a specific IP (IP range).</p>

## Relevant Information
- For information on security groups, see [Security Group Overview](https://intl.cloud.tencent.com/document/product/215/38750) and [Adding a Security Group Rule](https://intl.cloud.tencent.com/document/product/215/35513).
- For more information on common ports, see [Common Server Ports](https://intl.cloud.tencent.com/document/product/215/35520).
