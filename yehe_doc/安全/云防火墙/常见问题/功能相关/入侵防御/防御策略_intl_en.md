
### What kind of traffic will be automatically blocked in Block mode of threat intelligence?	
After the Block mode of threat intelligence is enabled, the NAT edge firewall will automatically block outbound threat intelligence alerts, and edge firewall and inbound traffic will be observed.

### What kind of traffic will be automatically blocked in Block mode of virtual patching?	
After the Block mode of virtual patching is enabled, the edge firewall will automatically identify vulnerability exploits and attacks of all network perimeter traffic. Connections that generate alerts will be automatically blocked.

### What is the difference between IPS virtual patching and patches of other host security products?
- Patches on a host are generally officially released, which may take several weeks or months. Some patches also require a CVM restart.
- IPS virtual patching of CFW takes only few hours to update without the need to change or restart services. This is implemented by updating prevention rules of IPS in real time based on vulnerability exploit characteristics.
- CFW IPS virtual patching and host security products such as CWPP, an optimal combination for host security protection, work together to systematically protect networks and hosts.

### Do I still need to make a fix on my host after virtual patching is used?
Yes. Virtual patching protects the forefront of your network, and you still need to thoroughly fix vulnerabilities for most secure protection.

### How are threat levels of intrusion defense rules defined?
- The threat levels for basic defense and virtual patching are defined based on the threats they may cause.
The threat levels for threat intelligence are defined based on the threat level of historical attacks initiated by a specific IP address or domain name.

### How does the CFW threat intelligence package update mechanism work?
There are two kinds of threat intelligence packages: high-precision package and prioritized protection package. Their features are as follows:
- For high-precision packages, a complete false positive removal process is available.
- Prioritized protection packages are only used in Strict mode for non-real IP addresses, and are disabled in Block or Observe mode by default.

### Can shiro vulnerabilities be identify for intrusion defense virtual patching?
Yes, but not all scenarios can be covered, since some traffic is encrypted.

### What vulnerabilities can be prevented by CFW?
For vulnerabilities that can be prevented by CFW, go to [**Intrusion defense**](https://console.cloud.tencent.com/cfw/ips) -> **Intelligence center**.

### How CFW determine a web attack?
Attack characteristics will be introduced during scanning and sniffing of external hackers. For example, once CFW detects the attack characteristics of the weblogic vulnerability, it will regard it as an attempted attack.

### What protocol types are supported for brute force prevention?
The following protocol types are supported: MySQL, Oracle, SSH, Redis, MongoDB, IMAP, POP3, FTP, SMTP, SQLServer, and RDP.

### How to deal with existing mining attacks?
- If you have not purchased Tencent CWPP, you can manually kill the virus without the need of reinstallation. The server is infected if mining works.
- If you have purchased Tencent CWPP, you can directly clear the threat.
