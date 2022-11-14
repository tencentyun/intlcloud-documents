
### What kind of traffic will be checked by the Intrusion Prevention System (IPS)?
Traffic going through the edge firewall and NAT firewall will be checked by the Intrusion Prevention System.

### What will be blocked in the Block mode?	
In the Block mode, CFW will perform blocking in the following conditions:
- Threat intelligence: Network attacks or malicious access with high confidence, as well as malicious outbound access can be automatically blocked.
- Basic protection: Malicious behaviors that hit high-confidence rules are automatically blocked, and security event alerts are generated when other rules are hit.
- Virtual patching: Virtual patching support automatic blocking of all traffic detected as vulnerability exploits.

### How to manually block risks in the alert list? Can I manually add IP addresses for blocking?
For risks with frequent alerts or high risk levels, you can perform manual blocking. Besides, you can import IP addresses to be blocked to the blocklist of IPS. In case of access with any of these IP addresses, it will be directly blocked by CFW.

###What requests are blocked automatically in Block mode? Why do alerts still appear when Block mode is enabled?
- In the Block mode, CFW will automatically block risks with high confidence and IP addresses in the blocklist.
- Alerts will be generated for risks with low confidence. You can manually block the alert IP addresses in Alert Management.

### How are malicious IP addresses blocked in Strict mode?
In the Strict mode, threat intelligence, base protection, and virtual patching are all in Global Block mode. All IP addresses that generate alerts will be blocked. For risks with high confidence and IP addresses in the blocklist, blocking will be triggered upon initial access. For other malicious IP addresses, an alert will be generated upon initial access, and blocking will be triggered upon access for twice.

### Why are malicious IP addresses not blocked?
Intrusion defense of CFW is performed on sessions. Only sessions with attack characteristics will be blocked. If an IP address is not added to the blocklist, its sessions will not be blocked.

### When will the Block mode be enabled?	
Generally, if services remain unchanged after switching from Observe mode to Block mode for 1 to 2 days, the Block mode will be enabled.

### Will the Block mode affect services after it is enabled? Are the blocking policies precise?
IPS only set rules with high precision to the Block mode. False positives are never found for virtual patching. If any problem occurs after the Block mode is enabled, feel free to contact us for help.

### Will the communication between cloud intranet addresses be affected after the CFW Block mode is enabled?	
No. After the Block mode is enabled, only Internet traffic of cloud services will be affected, and communication between cloud intranet addresses will not be affected.


### What should I do if an IP address is incorrectly blocked by IPS?
1. Log in to the [Cloud Firewall console](https://console.cloud.tencent.com/cfw), select **Log auditing** -> **Intrusion defense logs**, and then you can check the blocking history of the source or destination IP address.
2. In case of emergency, enter the **[IPS](https://console.cloud.tencent.com/cfw/ips)** menu to turn off "Enable blocklist", and then go to **[Alert management](https://console.cloud.tencent.com/cfw/warncenter)** -> **Blocked statistics** to view all blocking statistics and locate the blocking source.
3. After the fault is located and fixed, you can turn on "Enable blocklist" to enable it again.

### What can I do in case of incorrect interception or access failure?
- Check whether the firewall for the public IP address is disabled. In this case, traffic does not go through CFW.
- Modify the IPS to Observe mode.
- Configure the CFW policy to "Any", which means that the public IP address is allowed to pass.

>?If none of the above works, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) to contact us.

### Why is an IP address missing in the configured blocklist?
1. An IP address whose effective period expires will be automatically removed from the blocklist, and the access of this IP address will not be blocked by the firewall anymore.
2. To prevent risky IP addresses from being automatically removed from the blocklist, you can click **Edit** in the action column on the right side of the blocklist to modify the expiration time for IP addresses.

### Will IP addresses in the ignored list be blocked?
IP addresses in the ignored list will directly bypass the IDPS.

### How can I make specified detection rules ignored for an IP address?
Currently, it is not supported to make specified detection rules ignored.

### In what case will DNS traffic bypass CFW?
- Tencent Cloud CVM may use the DNS service developed by Tencent, and generated DNS messages will not go across the edge. In this case, alerts and logs will be generated for such domain names.
- To enable a specified CVM to normally use domain name detection and alert features of CFW, you can manually modify the resolution address under /etc/resolv.conf to 8.8.8.8.

### What is the relationship between Intrusion Protection System and access control?
- CFW judgment order: **Blocklist** -> **Access control** -> **Ignored list** -> **Intrusion Protection System**
- Intrusion Protection System takes effect only for assets with firewall enabled. For assets without protection enabled, their traffic will not go through CFW.
