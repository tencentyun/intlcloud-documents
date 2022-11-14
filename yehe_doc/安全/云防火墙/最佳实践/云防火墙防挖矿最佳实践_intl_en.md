This topic describes how to use Cloud Firewall to defend against common cryptomining worms and covers attack prevention, detection, and recovery in an actual cloud environment.

## Important notes
Cloud Firewall offers an intrusion defense module to protect against cryptomining worms. The intrusion defense feature is available in Cloud Firewall IPS, Premium, Enterprise, and Ultimate to help users defend against mining attacks. Generally, attackers compromise a server in your private network with Trojans or botnets and exploit your resources to send requests to the Internet. To accurately locate the risky server in the private network, you need the NAT firewall feature. Hence, **we recommend that you purchase Premium, Enterprise, or Ultimate Edition**.

## How do mining worms spread?
In most cases, attackers exploit network vulnerabilities, including general and zero-day/n-day vulnerabilities, to spread mining worms.

### General vulnerabilities
Mining worms often exploit general vulnerabilities in applications or websites, such as code defects, configuration errors, and weak passwords, to continuously scan and attack servers on the Internet. Attacks that exploit general vulnerabilities include SSH/RDP brute-force attacks, command injection, credential stuffing, Webshell communication, and outgoing access to malicious IPs. Typical intrusion methods that exploit general vulnerabilities are listed in the following table:
<table>
<thead>
<tr>
<th>Intrusion type</th>
<th>Malware family</th>
<th>Typical intrusion method</th>
</tr>
</thead>
<tbody><tr>
<td rowspan=11>Brute-force attacks</td>
<td rowspan=11>MyKings<br>MrbMiner<br>LoggerMiner<br>GuardMiner<br>DDG RDPMiner</td>
<td>MongoDB brute-force attack</td>
</tr>
<tr>
 <td>SSH brute-force attack</td>
</tr>
<tr>
 <td>Tomcat brute-force attack</td>
</tr>
<tr>
<td>MySQL brute-force attack</td>
</tr>
<tr>
  <td>PostgreSQL brute-force attack</td>
</tr>
<tr>
  <td>SQL Server brute-force attack</td>
</tr>
<tr>
  <td>FTP brute-force attack</td>
</tr>
<tr>
  <td>RDP brute-force attack</td>
</tr>
<tr>
  <td>SMB brute-force attack</td>
</tr>
<tr>
  <td>Telnet brute-force attack</td>
</tr>
</tbody></table>

### Zero-day/N-day vulnerabilities
When a zero-day or n-day vulnerability is exploited, it can easily lead to large-scale infection before it is fixed and can bring huge damage to your services.
- Common zero-day and n-day vulnerabilities include WebLogic vulnerability, deserialization vulnerability, EternalBlue, and Tomcat remote code execution vulnerability.
- Typical intrusion methods that exploit zero-day/n-day vulnerabilities are listed in the following table:
<table>
<thead>
<tr>
<th>Intrusion type</th>
<th>Malware family</th>
<th>Typical intrusion method</th>
</tr>
</thead>
<tbody><tr>
<td>System vulnerabilities</td>
<td>WannaMine</td>
<td>MS17-010 EternalBlue (CVE-2017-0143)</td>
</tr>
<tr>
<td rowspan=7>Application vulnerabilities</td>
<td rowspan=7>8220Miner<br>BashMiner<br>kworkersMiner<br>TraceMiner<br>CarbonMiner</td>
<td>Confluence remote code execution (CVE-2021-26084)</td>
</tr>
<tr>
<td>Confluence remote command execution (CVE-2019-3396)</td>
</tr>
<tr>
<td>Gitlab exiftool remote command execution (CVE-2021-22205)</td>
</tr>
<tr>
<td>Apache NIFI remote code execution (CVE-2020-9491)</td>
</tr>
<tr>
<td>Yonyou NC Cloud remote code execution (CNVD-2021-30167)</td>
</tr>
<tr>
<td>Docker Remote API unauthorized access (CVE-2019-17671)</td>
</tr>
<tr>
<td>YAPI remote code execution</td>
</tr>
<tr>
<td rowspan=4>Component vulnerabilities</td>
<td rowspan=4>JumaMiner<br>H2Miner<br>tellyouthepass</td>
<td>Log4j2 remote code execution (CVE-2021-44228)</td>
</tr>
<tr>
<td>Jenkins unauthenticated command execution (CVE-2017-1000353)</td>
</tr>
<tr>
<td>WebLogic remote execution (CVE-2021-2109)</td>
</tr>
<tr>
<td>Hadoop Yarn unauthorized access</td>
</tr>
</tbody></table>

## How does Cloud Firewall defend against mining worms?
Cloud Firewall detects incoming and outgoing traffic in real time. Detected malicious traffic is automatically blocked to protect against mining worms. It works in the following two ways:

### Defense against general vulnerabilities
General vulnerabilities are often exploited to launch RDP/SSH brute-force attacks and system command injection attacks. To protect against such attacks, Cloud Firewall offers a basic protection module for intrusion defense. The basic protection module integrates the intrusion detection rules based on Tencent Cloud's extensive anti-attack experience, covering common network attacks and malicious code, as shown in the image below:
![](https://qcloudimg.tencent-cloud.cn/raw/c8853d75ee5ea29a26fd51040b58bd58.png)

To **enable the basic protection feature to defend against mining worms that exploit general vulnerabilities**:
1. Log in to the [Cloud Firewall console](https://console.cloud.tencent.com/cfw/asset), and then click **Intrusion Protection System** in the left navigation pane.
2. On the Intrusion Defense page, click ![](https://qcloudimg.tencent-cloud.cn/raw/6b585aa1156a486d15c5da8790fd837b.png) to enable threat intelligence and basic protection, and then select "Block" or "Strict" for the protection mode.
>?
>- In observe mode, any mining worms detected are recorded in Alert Management but are not automatically blocked.
>- In block mode, the threat intelligence module can automatically block malicious outgoing requests, and the basic protection module can automatically block traffic that hit the high-confidence preset rules.
>- In strict mode, all detected security events or suspicious IPs are blocked or added to the blocklist by the threat intelligence and basic protection modules.

![](https://qcloudimg.tencent-cloud.cn/raw/62ff635ff3b1f46f4bdb50c9c4fc0463.png)
3. On the [Intrusion Defense Log page](https://console.cloud.tencent.com/cfw/ipslog), you can view the details of intrusion logs.
![](https://qcloudimg.tencent-cloud.cn/raw/27f08ef8581e792a520576fc24d3a833.png)

### Defense against zero-day/n-day vulnerabilities

Some common zero-day/n-day vulnerabilities are likely to be exploited by mining worms if they are not fixed in a timely manner. By obtaining vulnerability intelligence from the Tencent Cloud Threat Intelligence X in real time, Cloud Firewall can promptly detect zero-day/n-day vulnerabilities, obtain the proofs of concept (POCs), and generate a rule base for virtual patching. This way, Cloud Firewall can take actions before hackers do, as shown in the image below:
![](https://qcloudimg.tencent-cloud.cn/raw/c298f0d7e3f306fe728b709d8c25cc81.png)

To **enable virtual patching to defend against mining worms that exploit zero-day/n-day vulnerabilities**:
1. Log in to the [Cloud Firewall console](https://console.cloud.tencent.com/cfw/asset), and then click **Intrusion Protection System** in the left navigation pane.
2. On the Intrusion Defense page, click ![](https://qcloudimg.tencent-cloud.cn/raw/6b585aa1156a486d15c5da8790fd837b.png) to enable virtual patching, and then select the "Block" or "Strict" for the protection mode.
![](https://qcloudimg.tencent-cloud.cn/raw/2fd03d2cb436141de2c1b8c81a0aa93f.png)
3. On the [Intrusion Defense Log page](https://console.cloud.tencent.com/cfw/ipslog), you can view the details of intrusion logs.
![](https://qcloudimg.tencent-cloud.cn/raw/0bdc47a0d342fc93a101539fef69f565.png)

## How does Cloud Firewall detect mining worms?
Tencent Cloud's threat intelligence module detects malicious outgoing traffic in real time. Thanks to the built-in Tencent Security threat intelligence and detection, the module can precisely identify any traffic from malicious IPs and domain names, and automatically update in seconds. Any traffic from or to the assets in the public and private network is monitored by Cloud Firewall. If mining worm attacks are detected, the servers concerned are labeled as compromised, and displayed in the [Alert Management](https://console.cloud.tencent.com/cfw/warncenter).
![](https://qcloudimg.tencent-cloud.cn/raw/13cb16b74fca2a4b5d08f55849648d2c.png)

## How to use Cloud Firewall to quickly recover from cryptomining attacks
If a server is compromised by mining worms, Cloud Firewall can help you quickly locate the infected server, and then remove the mining worms using Cloud Workload Protection Platform. This can prevent hackers from uploading malicious files and avoid information leakage.
- Threats in public network assets can be detected by the CFW edge firewall. Threat Intelligence can immediately locate the infected public asset to block cryptomining requests.
![](https://qcloudimg.tencent-cloud.cn/raw/c712180c33d7e26160a0a4d62c3844b6.png)
- Private network assets cannot access the Internet before their IP addresses are translated. **Cloud Firewall can only locate the NAT public IP addresses**. Hence, if a given private network asset is infected by mining worms, you need to **enable NAT firewall for the private network asset** to see that a request is sent from the NAT public IP to the IP or domain name of a mining pool in Alert Management. With the IP or domain name of the mining pool, you can precisely locate the source server by obtaining the compromised private network asset in the traffic logs of the NAT firewall.
![](https://qcloudimg.tencent-cloud.cn/raw/baaeab179c1b8b67f9d64ed7db658dc0.png)
- Configure access control rules to block malicious requests. If cryptomining is detected on a public network asset by intrusion defense, you can configure blocking rules in [Access control](https://console.cloud.tencent.com/cfw/ac/internet) -> **Edge firewall rules** -> **Outbound rules**.

- If cryptomining is detected on a private network asset, you can configure blocking rules in [Access control](https://console.cloud.tencent.com/cfw/ac/internet) -> **NAT firewall rules** -> **Outbound rules**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/c982d8136185282b51bdca1723af539e.png" style="zoom:67%;" />
