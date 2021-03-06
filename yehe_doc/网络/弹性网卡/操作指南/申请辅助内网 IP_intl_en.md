To bind multiple IP addresses to a single ENI, you can apply for secondary private IP addresses for the ENI as follows:
## Step 1. Assign a Private IP
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. Choose **IP and ENI** > **ENI** in the left sidebar to go to the ENI list page.
3. Locate the ENI instance for which you want to request a secondary private IP, and then click on its **ID/Name** to go to its details page.
4. Click the **IPv4 Address Management** tab, and check the primary private IPs that have been bound.
![](https://main.qcloudimg.com/raw/a313d1e3c276e09e0d9231a2ed6205b2.png)
5. Click **Assign Private IP** and select **Auto** or **Enter manually** for **Assign IP** in the pop-up window.
>?If you select **Enter manually**, make sure that the private IP address you enter is within the subnet IP range and is not a reserved IP address of the system.
>For example, if the subnet IP range is `10.0.0.0/24`, the entered private IP address should be within `10.0.0.2 - 10.0.0.254`.
>
![](https://main.qcloudimg.com/raw/587903cea55b559c76e91fa27ee6d768.png)

## Step 2. Configure the Secondary Private IP
Follow the steps below to log in to the CVM that is bound with the ENI and configure the secondary private IP to make it effective:
### Linux CVM instances
1. Run the following command to configure the secondary private IP.
```plaintext
# For example, `ip addr add 10.0.0.2/24 dev eth0`
ip addr add Secondary private IP/CIDR bits dev eth0
```
2. Run the `ip addr` command to view the configured IPs, as shown below.
![](https://main.qcloudimg.com/raw/ddca8a3c87b05bbf5850418824775449.png)
3. Run the following commands to configure policy-based routing.
```plaintext
ip rule add from 10.0.0.2 table 20      //Replace 10.0.0.2 with the secondary private IP you applied for, and 20 with your actual custom route table ID
```
### Windows CVM instances
1. <span id="step1" />Perform the following steps to view the IP address, subnet mask, default gateway, and DNS server of the CVM instance.
 1. On the desktop, select <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin:-3px 0px;width:25px"> in the lower-left corner and click <img src="https://main.qcloudimg.com/raw/f0c84862ef30956c201c3e7c85a26eec.png" style="margin: -3px 0px;"> to open the **Windows PowerShell** window.
```
ipconfig /all
```
 2. Record the IPv4 address, subnet mask, default gateway, and DNS server values that are displayed.
![](https://main.qcloudimg.com/raw/1a4a6f0557ff809a27607fee24549eb3.png)
2. Select **Control Panel** > **Network and Internet** > **Network and Sharing Center**. Click **Ethernet** to modify its information.
![](https://main.qcloudimg.com/raw/56b44bec57750b8e86a9c7f7aba40041.png)
3. In the **Ethernet Status** pop-up window, click **Properties**.
4. In the **Ethernet Properties** pop-up window, select **Internet Protocol Version 4 (TCP/IPv4)** and click **Properties**.
![](https://main.qcloudimg.com/raw/b224af9ef0d18ca24f8e799f9c5023df.png)
5. In the **Internet Protocol Version 4 (TCP/IPv4) Properties** pop-up window, specify the following information:
<table>
<thead>
<tr>
<th>Parameter Name</th>
<th>Parameter Value</th>
</tr>
</thead>
<tbody><tr>
<td>IP address</td>
<td>The IPv4 address obtained in <a href="#step1">step 1</a></td>
</tr>
<tr>
<td>Subnet mask</td>
<td>The subnet mask obtained in <a href="#step1">step 1</a></td>
</tr>
<tr>
<td>Default gateway</td>
<td>The default gateway obtained in <a href="#step1">step 1</a></td>
</tr>
<tr>
<td>Preferred DNS server</td>
<td>The DNS server obtained in <a href="#step1">step 1</a></td>
</tr>
<tr>
<td>Alternate DNS server</td>
<td>The alternate DNS server obtained in <a href="#step1">step 1</a>. If the alternate DNS server is not given, ignore this parameter.</td>
</tr>
</tbody></table>
<img src="https://main.qcloudimg.com/raw/26fca0d8901235e7be62234c3e684e17.png" />
6. Click **Advanced** to configure the secondary private IP address.
7. In the **Advanced TCP/IP Settings** pop-up window, click **Add** under the **IP Addresses** section.
8. In the **TCP/IP Address** pop-up window, enter the secondary private IP and the subnet mask obtained in [step 1](#step1), and click **Add**. 
![](https://main.qcloudimg.com/raw/1fdcb2fa24e45057c5874dfbb20652bc.png)
9. In the **Internet Protocol Version 4 (TCP/IPv4)** pop-up window, click **OK**.
10. In the **Ethernet Properties** pop-up window, click **OK** to complete the configuration.
11. In the **Ethernet Status** pop-up window, click **Details** to view the configured IP addresses.
![](https://main.qcloudimg.com/raw/172cb1189fe0886d6b0b6483a924f8cd.png)

 
