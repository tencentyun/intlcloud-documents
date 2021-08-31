### What are the differences between Web Application Firewall (WAF) and Tencent Cloud Firewall (CFW)?
Their differences are as follows:
<table>
<thead>
<tr>
<th style ="width:95px;height:45px;position:relative;text-align:left;padding:5px 7px;font-weight:900;" valign="top" rowspan="2"><div style="position:absolute;width:1px;height:130px;top:0;left:0;background-color: #d9d9d9;display:block;transform:rotate(-55deg);transform-origin:top;valign=top;"  ></div>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Product<br><br>Item</th>
<th colspan="2" style ="text-align:center">WAF</th>
<th rowspan="2" style ="text-align:center">CFW</th>
</tr>
<tr>
<th style ="text-align:center">SaaS WAF</th>
<th style ="text-align:center">CLB WAF</th>
</tr>
</thead>
<tbody>
<tr>
<th>Protection Object</th>
<td>Web and API service</td>
<td>Web and API service</td>
<td>Businesses entirely opened to the Internet</td>
</tr>
<tr>
<th>Use Cases</th>
<td>Cybersecurity classified protection, intensifying protection, web and API security protection, application layer protection, and anti-cheating protection.</td>
<td>Cybersecurity classified protection, intensifying protection, web and API security protection, application layer protection, anti-cheating protection, and layer-7 CLB instance application.</td>
<td>Cybersecurity classified protection, intensifying protection, CVM host and web security protection.</td>
</tr>
<tr>
<th>Core Protection Capability</th>
<td><ul><li>Web vulnerability defense, unknown threat defense, and self-service false-negative and false-positive attack processing.</li><li>CC attack defense.</li><li>Bot action management and crawler defense.</li><li>API security and business security protection.</li><li>Anti-leak and anti-tampering.</li></td>
<td><ul><li>Web vulnerability defense, unknown threat defense, and self-service false-negative and false-positive attack processing.</li><li>CC attack defense.</li><li>Bot action management.</li><li>API security and business security protection.</li><li>IPv6 web protection.</li></td>
<td><ul><li>IPS virtual patching, which eliminates the needs for realistic CVM patches and restarting. The basic vulnerability defense for OWASP top 10 attacks is covered.</li><li>Automatic detection for compromised hosts and automatically blocking CVM malicious external connections.</li><li>Domain name-based active external connection control.</li></td>
</tr>
<tr>
<th>Core Strength</th>
<td>The wide scenarios ranging the application needs of users both within and outside Tencent Cloud.</td>
<td>It is a Tencent Cloud native service, which can be connected across regions, eliminating the need to adjust the existing network architecture. Web business forwarding and security protection are separated, therefore WAF service can be easily disconnected during service breakdown to achieve stable and reliable web security protection. It can only be used for businesses within Tencent Cloud.</td>
<td>The Tencent Cloud native firewall can be quickly enabled not affecting the existing businesses. It integrates security capabilities such as IPS, threat intelligence, and vulnerability scanning, etc., which is ideal for cybersecurity classified protection and intensifying protection. It can only be used for businesses within Tencent Cloud.</td>
</tr>
<tr>
<th>Service Selection</th>
<td>For businesses requiring web and API security protection for both Tencent Cloud and local IDCs, we recommend using SaaS WAF.</td>
<td>For businesses using or planning to use layer-7 CLB instances, we recommend using CLB WAF.</td>
<td>For businesses requiring CVM protection, especially the ones with other public network services opened except the web service, we recommend using CFW.</td>
</tr>
</tbody></table>
