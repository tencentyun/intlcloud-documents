This document describes how to connect a website application to an Anti-DDoS Advanced instance and verify the forwarding configuration.
>Currently, website businesses support access from only the Beijing, Shanghai, and Guangzhou regions but not regions outside Mainland China.

## Prerequisites
- You need to [purchase an Anti-DDoS Advanced instance](https://intl.cloud.tencent.com/document/product/297/15483) before adding a forwarding rule.
- You need to purchase the domain name resolution product before modifying the DNS information of your business domain name.

## Process
![](https://main.qcloudimg.com/raw/0df61ac0012ebf1123ec9d83fc3438cc.png)

## Directions
<span id="step1"></span>
### Configuring forwarding rule

1. Log in to the [Anti-DDoS Console](https://console.cloud.tencent.com/dayu/bgp_v2) and select **Anti-DDoS Advanced** > **Access Configuration** on the left sidebar.
2. On the access configuration page, click **Website Business**, find and select the target Anti-DDoS Advanced instance, and add the forwarding rule.
	- Add one forwarding rule:
		1. 	Click **Create**.
 
		1. On the **Add forwarding rule** page, configure the following parameters as needed and click **OK**.

Parameter description:
 - Domain Name: enter the website domain name to be protected.
 - Protocol: HTTP and HTTPS are supported. Please choose one based on your actual business needs:
		<table>
			<tr>
				<th>Business Scenario</th>
				<th>Related Operations</th>
			</tr>
			<tr>
				<td>Websites containing only HTTP protocol</td>
				<td>Select **HTTP**.</td>
			</tr>
			<tr>
				<td>Websites containing only HTTPS protocol</td>
				<td><ul><li>Select **HTTPS**.</li>
				        <li>Certificate Source: Tencent Cloud-hosted certificate is selected by default.</li>
				        <li>Certificate: select the corresponding SSL certificate name.</li></td>
			</tr> 
		</table>
  - Forwarding Method: **Forwarding via IP** and **Forwarding via domain name** are supported.
  - Enter the real server IP or domain name according to the **forwarding method**:
			- If **Forwarding via IP** is selected, enter the IP (or IP + port) of the real server. If one website domain name corresponds to multiple real server IPs (or IP + port pairs), you can enter all of them and separate them with carriage return. Up to 16 IPs (or IP + port pairs) are supported.
			- If **Forwarding via domain name** is selected, enter the real server domain name (CNAME) or domain name (CNAME) + port. If one website domain name corresponds to multiple real server domain names (CNAME) or domain name (CNAME) + port pairs, you can enter all of them and separate them with carriage return. Up to 16 domain names (CNAME) or domain name (CNAME) + port pairs are supported.
	- Add forwarding rules in batches:
		1.	 Select **Batch Import** > **Import Forwarding Rules**.
		
		1.	 In the rule input box on the batch import page, paste the rules to be imported.
		
>
>- From left to right, the pasted contents are the domain name, protocol, real server IP (real server domain name is not supported currently), and real server port. The real server IP and real server port are separated with ":", and the rest are separated with space. Only one forwarding rule can be entered per line.
>-  The number of forwarding rules to be added in batches cannot exceed the current available quota.

<span id="step2"></span>
### Opening the intermediate IP range
To prevent service unavailability that occurs when the real server blocks the intermediate IP of Anti-DDoS Advanced, you are recommended to configure whitelist policies for the real server infrastructure, including firewall, web application firewall, intrusion protection system (IPS), and traffic management system, and disable the protection features of the host firewall and other security software programs (such as Safedog) on the real server or set whitelist policies for them, so that the intermediate IP will not be affected by the security policies of the real server.
You can log in to the [Anti-DDoS Console](https://console.cloud.tencent.com/dayu/bgp_v2), select **Anti-DDoS Advanced** > **Resource List** on the left sidebar, find the row of the target Anti-DDoS Advanced instance, and click its **ID/Name** to view its detailed intermediate IP range on the **Basic Information** page that pops up.
<span id="step3"></span>
### Local verification configuration
After the forwarding configuration is completed, the protected IP of Anti-DDoS Advanced will forward the packets from the relevant port to the corresponding real server port based on the forwarding rules.
To ensure the stability of your business, a local test is recommended. The verification method is as follows:
1. Modify your local `hosts` file to forward local requests to the protected website to the protected IP.
   Take Windows as an example:
   1. Open the `hosts` file in `C:\Windows\System32\drivers\etc` on your local compute and add the following content at the end:
   `<Protected IP address> <Domain name of the protected website>`
   For example, if the protected IP is 10.1.1.1 and domain name is [www.qq.com](www.qq.com), then add:
   `10.1.1.1       www.qq.com`
   2. Save the `hosts` file.
2. Run the `ping` command on the protected domain name on the local computer.
   If the resolved IP address is the protected IP bound in the `hosts` file, the forwarding is successful.
> If the resolved IP address is still the real server IP address, try running the `ipconfig/flushdns` command on Windows Command Prompt to clear the local DNS cache.
3. After successfully binding `hosts`, check whether the domain name can be accessed.
   If yes, the configuration has taken effect.

>If the verification still fails with the correct method, please log in to the [Anti-DDoS Console](https://console.cloud.tencent.com/dayu/bgp_v2) and check whether the configuration is correct. If the problem persists after you fix any incorrect configuration items, please contact [Tencent Cloud technical support](https://intl.cloud.tencent.com/contact-sales).

<span id="step4"></span>
### Modifying DNS resolution of business domain name
Before using Anti-DDoS Advanced, you need to configure the A record of your business domain name's DNS with a protected IP, so that all user access requests to your site will pass through Anti-DDoS Advanced first before arriving at the real server (that is, all traffic will be first forwarded to Anti-DDoS Advanced before getting to the real server).
  

