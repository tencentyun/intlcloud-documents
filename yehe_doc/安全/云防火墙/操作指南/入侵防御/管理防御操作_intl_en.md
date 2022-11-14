This topic describes how to use the Intrusion Protection System (IPS) to identify unknown risks beyond access control rules, monitor the north-south traffic of public IP addresses based on intrusion defense rules, and prevent CVM vulnerabilities from being exposed to the Internet.

## Selecting a protection mode
1. Log in to the [Cloud Firewall console](https://console.cloud.tencent.com/cfw/ips) and click **Intrusion Protection System** in the left navigation pane.
2. On the **Intrusion protection system** page, configure the protection mode in the **Protection mode** module.
Three protection modes are available: **Observe**, **Block**, and **Strict**.
>? The default protection mode is Observe.

 - In the Observe mode, threat intelligence, basic protection, and virtual patching only detect and send alerts against malicious access or network attacks without interrupting the connections.
 - In the Block mode, threat intelligence automatically blocks outbound malicious access, basic protection blocks network attacks that trigger high-confidence rule alerts, and virtual patching blocks all the traffic detected as vulnerability exploits.
 - In the Strict mode, threat intelligence (except for detection of outbound domain names), basic protection, and virtual patching block any detected malicious behaviors that trigger alerts while interrupting the connections. Note that this can cause false positives and is only suggested when the asset is under attack.
![](https://qcloudimg.tencent-cloud.cn/raw/7967386b2f153a4fb05d41b31a333528.png)
3. Click **Advanced settings** on the right side of the **Protection mode** module.
4. In the **Advanced settings** window displayed, configure the protection mode for each asset under **Edge firewall**, **NAT firewall**, and **Inter-VPC firewall** respectively.
![](https://qcloudimg.tencent-cloud.cn/raw/d3dc87ed68d4c82b05a793e29c673003.png)

## IPS overview
1. Log in to the [Cloud Firewall console](https://console.cloud.tencent.com/cfw/ips) and click **Intrusion Protection System** in the left navigation pane.
2. On the right side of the **Intrusion protection system** page, feature updates and feature descriptions are displayed.
	- **Feature updates**: You can view the features of IPS modules.
![](https://qcloudimg.tencent-cloud.cn/raw/d4850a70bcad62cdb61cb7436e1fd83e.png)
	- **Intelligence center**:
	 1. Click **Intelligence center** at the upper right corner of feature updates to view security threat intelligence information.
      2. In the **Intelligence center** window displayed, click an intelligence title to view details about vulnerability description and threat level. You can also scan your assets for the threats reported in the vulnerability intelligence.

## Managing lists
1. Log in to the [Cloud Firewall console](https://console.cloud.tencent.com/cfw/ips) and click **Intrusion Protection System** in the left navigation pane.
2. At the bottom of the **Intrusion protection system** page, you can view the **Blocklist**, **Allowlist**, and **Quarantined list**.

### Blocklist
#### Viewing the blocklist
1. Click **Blocklist** to enter the blocklist.
![](https://qcloudimg.tencent-cloud.cn/raw/c6c68edcef24a5add8f1b40b7b9e8825.png)
2. In the blocklist, you can view the IP addresses marked as "Blocked" in **[Alert Management](https://console.cloud.tencent.com/cfw/warncenter/event)** -> **Attack alerts** and their information. You can also manually add IP addresses to the blocklist.

#### Disabling the blocklist
1. In case of emergency, click ![](https://qcloudimg.tencent-cloud.cn/raw/66a5322882d59d71a354e74385794e09.png) to turn off **Enable blocklist**, and then go to **[Alert Management](https://console.cloud.tencent.com/cfw/warncenter/event)** -> **Blocked attacks** to view all blocking statistics and locate the alert source.
![](https://qcloudimg.tencent-cloud.cn/raw/59bbc31a9996a66d9aab2e853f7aff2c.png)
2. After the fault is located and fixed, click ![](https://qcloudimg.tencent-cloud.cn/raw/ea050a3ce9545e2070d14589e3628d81.png) to turn on **Enable blocklist** again.

#### Managing the effective period in the blocklist
An IP address whose effective period expires will be automatically removed from the blocklist, and traffic of this IP address will not be blocked by the firewall anymore. To prevent risky IP addresses from being automatically removed from the blocklist, you can click **Edit** in the action column on the right side of the blocklist to modify the expiration time for IP addresses.
>? For IP addresses in the blocklist, their inbound or outbound traffic that goes through CFW will be blocked and recorded in **Log Auditing** -> **[Intrusion Defense Logs](https://console.cloud.tencent.com/cfw/ipslog)**.

![](https://qcloudimg.tencent-cloud.cn/raw/7acb4b69b417c7b1d075b2660dbc9f5c.png)

### Allowlist
#### Viewing the allowlist
1. Click **Allowlist** to enter the allowlist.
![](https://qcloudimg.tencent-cloud.cn/raw/279be651a6a4aa1f10776d47ad45834c.png)
2. In the allowlist, you can view the IP addresses marked as "Allowed" in **[Alert Management](https://console.cloud.tencent.com/cfw/warncenter/event)** -> **Attack alerts** and their information. You can also manually add IP addresses to the allowlist.
>! IP addresses in the allowlist will directly bypass the IDPS.

#### Managing the effective period in the allowlist
 An IP address whose effective period expires will be automatically removed from the allowlist, and traffic of this IP address will not bypass CFW IDPS anymore. To prevent trusted IP addresses from being automatically removed from the allowlist, you can click **Edit** in the action column on the right side of the allowlist to modify the expiration time for IP addresses.
![](https://qcloudimg.tencent-cloud.cn/raw/56a0eab9a93919aa8be58b87cf45d34f.png)

### Quarantined list
#### Viewing the quarantined list
1. Click **Quarantined list** to enter the quarantined list.
![](https://qcloudimg.tencent-cloud.cn/raw/fc8d2e5c963e3f2ffdc6bfb50afc47de.png)
2. In the quarantined list, you can view the IP addresses marked as "Quarantined" in **[Alert Management](https://console.cloud.tencent.com/cfw/warncenter/event)** -> **Attack alerts** -> **Server compromised** and their information.
![](https://qcloudimg.tencent-cloud.cn/raw/175c2d589029896ead53bcd416f782d9.png)

#### Viewing rules
IP addresses of compromised servers are quarantined using security groups. Click **View rules** to go to the enterprise security group page and view detailed rule information.
![](https://qcloudimg.tencent-cloud.cn/raw/9713671a32b4a5c0c1a1e7e67f29009b.png)

#### Managing the effective period in the quarantined list
An IP address whose effective period expires will be automatically removed from the quarantined list, and the security group rules of this IP address will be deleted as well. To prevent IP addresses of compromised servers from being automatically removed from the quarantined list, you can click **Edit** in the action column on the right side of the quarantined list to modify the expiration time for IP addresses.

#### Backing up and rolling back rules
Click **Backup rules** to back up existing blocklist and allowlist rules. When the rules are greatly changed, you can click **Roll back** to the right of the backup file to recover the rules.
![](https://qcloudimg.tencent-cloud.cn/raw/e8097476134841049a69045d187491f1.png)
1. On the **Back up and roll up rules** page, click **Create backup**, select **Blocklist** or **Allowlist** from the drop-down list, enter a description, and click **OK** to complete the backup.
![](https://qcloudimg.tencent-cloud.cn/raw/b5654696e906963f0d859118dc337291.png)
2. To roll back rules, click **Roll back** on the right side of the backup list to recover the rules.
![](https://qcloudimg.tencent-cloud.cn/raw/c0a911c407860ae89ddac7c98d47fe92.png)

## More information
For questions about intrusion defense, please see [Intrusion Protection System](https://intl.cloud.tencent.com/document/product/1160/49835).
