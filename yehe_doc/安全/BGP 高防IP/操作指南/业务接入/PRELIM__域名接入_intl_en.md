

## Operation Directions
1. Log in to the [Anti-DDoS console](https://console.cloud.tencent.com/ddos/antiddos-advanced/access/l7), click **Anti-DDoS Advanced (New)** -> **Application Accessing** on the left sidebar, and open the **Access via domain names** tab.
![](https://main.qcloudimg.com/raw/01495e735af641b8a8f0af4d36c1ef18.png)
2. Click **Add Domain Name** to fill in the configuration fields in the pop-up window.
>?For accessing via domain names, only the forwarding ports 80 and 443 are supported. To use other ports, please configure port forwarding. For more information, please see [Port Connection](https://intl.cloud.tencent.com/document/product/297/37221).
>
![](https://main.qcloudimg.com/raw/21d74e651807145a4a67c9a538f769db.png)
Parameter description:
 - Associated protecting IP: search to enter the IP or name.
 - Domain name: enter the domain name to be protected.
 - Protocol: HTTP and HTTPS are supported, you can tick one as needed.
		<table>
			<tr>
				<th>Scenario</th>
				<th>Operation</th>
			</tr>
			<tr>
				<td>Websites with HTTP only</td>
				<td>Tick **HTTP**.</td>
			</tr>
			<tr>
				<td>Websites with HTTPS only</td>
				<td><ul><li>Tick **HTTPS**.</li>
				        <li>Certificate source: the Tencent Cloud hosted certificate is selected by default.</li>
				        <li>Certificate: select the corresponding SSL certificate.</li></td>
			</tr> 
		</table>
  - Forwarding can be performed via IPs or domain names.
    - If you select **Forwarding via IP**, enter the real server IP (or IP + port). If a domain name corresponds to multiple real server IPs (or multiple pairs of IP + port), you can enter all of them and separate them with carriage return. Up to 16 entries are supported.
    - If you select **Forwarding via domain name**, enter the forwarding domain name (CNAME) or domain name (CNAME) + port. If a domain name corresponds to multiple real server domain names (CNAME) or multiple pairs of domain name (CNAME) + port, you can enter all of them and separate them with carriage return. Up to 16 entries are supported.
3. After completing the configuration, click **OK**.

