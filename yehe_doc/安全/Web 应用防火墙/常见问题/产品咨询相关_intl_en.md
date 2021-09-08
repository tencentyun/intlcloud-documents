### Is WAF available to servers outside Tencent Cloud?
 WAF can be connected with servers in data centers outside Tencent Cloud. WAF protects servers in any public networks, including but not limited to Tencent Cloud, and clouds and IDCs from other vendors. 
>! Domain names connected in the Chinese mainland must be ICP filed as required by the Ministry of Industry and Information Technology of China.

### Does WAF support HTTPS protection?
WAF fully supports HTTPS services. You just need to upload the SSL certificate and private key as instructed or select the Tencent Cloud-hosted certificate to use WAF for HTTPS traffic protection.

### Does the WAF QPS limit apply to the entire instance, or to a single domain name?
The QPS limit in WAF is for the entire instance. For example, if three domain names are protected, the total QPS of the three domain names cannot exceed the limit. If the QPS limit of the purchased instance is exceeded, speed will be limited and packets will be lost.

### Can Anti-DDoS Pro instances be used for WAF?
Yes, you can empower WAF with high DDoS protection capability simply by selecting IPs specified in a WAF instance on the configuration page in the Anti-DDoS Pro console. For more information, please see [Combination of Anti-DDoS Pro and Web Application Firewall](https://intl.cloud.tencent.com/document/product/1029/31768).


### Are there any risks in uploading an SSL certificate’s private key?

An SSL certificate’s private key hosted on Tencent Cloud will enjoy extremely high security, in terms of:

#### Uploading stage
The process from uploading the private key to configuring the certificate on the Tencent Cloud certificate hosting platform is protected with HTTPS, an encrypted communication, and enterprise SSL certificates, ensuring the safety of communication data.
#### Saving stage
1. After uploading, the certificate is stored in the database. The certificate’s private key will be encrypted using the AES CBC mode, which effectively prevents the private key from brute force attacks.
2. The certificate database will be backed up for disaster recovery. For high availability and high security of the certificate data, no external APIs will be used and the data will be protected by STGW.
3. There are multiple backend servers for SSL certificates, which are accessed via a load balancer to ensure API stability.

#### Managing and reading certificates
1. Integrating resource-level Cloud Access Management (CAM), SSL Certificate Service is backed by a well-established access management system that allows you to grant different permissions to your sub-accounts on different certificates to prevent malicious revocation and deletion.
2. The certificate pulling in WAF is protected by STGW. The business pulls the certificate on demand while identifying and authenticating the source of the request to avoid illegal and unnecessary access.

![](https://main.qcloudimg.com/raw/709d8c22cbb0eeab6890737f925f88f6.png)


### Is the SSL mutual authentication supported by both the SaaS WAF and CLB WAF?
It is supported by CLB WAF but not by SaaS WAF.

### What are the differences between WAF and CFW?
The differences are as follows:
<table>
<thead>
<tr>
<th style ="width:95px;height:45px;position:relative;text-align:left;padding:5px 7px;font-weight:900;" valign="top" rowspan="2"><div style="position:absolute;width:1px;height:130px;top:0;left:0;background-color: #d9d9d9;display:block;transform:rotate(-55deg);transform-origin:top;valign=top;"  ></div>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Product<br><br>Item</th>
<th colspan="2" style ="text-align:center">Tencent Cloud WAF</th>
<th rowspan="2" style ="text-align:center">Tencent Cloud CFW</th>
</tr>
<tr>
<th style ="text-align:center">SaaS WAF</th>
<th style ="text-align:center">CLB WAF</th>
</tr>
</thead>
<tbody>
<tr>
<th>Protected Target</th>
<td>Websites and API services.</td>
<td>Websites and API services.</td>
<td>Businesses completely exposed on the internet</td>
</tr>
<tr>
<th>Use Case</th>
<td>It is applicable to those who require multi-level protection or cybersecurity assurance service, particularly for webs, APIs, application layers and anti-cheating behavior.</td>
<td>It is applicable to those who require multi-level protection or cybersecurity assurance service, particularly for webs, APIs, application layers and anti-cheating behavior, and who have used or plan to use layer-7 CLB instances on Tencent Cloud.</td>
<td>It is applicable to those who require multi-level protection or cybersecurity assurance service, or who require protection for CVMs and network.</td>
</tr>
<tr>
<th>Core Protection Capability</th>
<td><ul><li>Web vulnerability and unknown threat prevention, and self-service false negative and false positive handling. </li><li>CC attack protection. </li><li>Bot behavior management and crawling protection. </li><li>API security and business security. </li><li>Leakage and tamper prevention.</li></td>
<td><ul><li>Web vulnerability and unknown threat prevention, and self-service false negative and false positive handling. </li><li>CC attack protection. </li><li>Bot behavior management. </li><li>API security and business security. </li><li>Protected IPv6 access to websites. </li></td>
<td><ul><li>IPS virtual patching (which covers OWASP TOP 10 web vulnerabilities) eliminates the need for CVM to install physical patches or reboots.</li><li>Discovers the overwhelmed CVM and blocks the CVM from malicious external connections automatically.</li><li>Supports controlling external connections proactively based on domain name.</li></td>
</tr>
<tr>
<th>Core Strength</th>
<td>It is applicable to Tencent Cloud and non-Tencent Cloud users.</td>
<td>Cloud-native access ensures the safety, stability and reliability of Tencent Cloud users’ website business with separation between forwarding and security protection via one-click bypass, which is implemented without changing the existing network architecture. Besides, multi-region access is also supported.</td>
<td>The cloud-native firewall can be enabled with one click, without affecting your business. It integrates security capabilities, such as IPS, threat intelligence, and omission scanning, necessary for multi-level protection and cybersecurity assurance scenarios, which is only available to Tencent Cloud users.</td>
</tr>
<tr>
<th>How to Choose</th>
<td>SaaS WAF is recommended for those who require protection for websites and APIs on cloud and in local IDC.</td>
<td>CLB WAF is recommended for those who have used or plan to use layer-7 CLB instances.</td>
<td>CFW is recommended for those who have concerns over the security of CVM (whether it will be overwhelmed), and businesses exposed on the internet that expose public network businesses in addition to web businesses.</td>
</tr>
</tbody></table>


