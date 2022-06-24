This document describes how to configure protection rules in Web Application Firewall (WAF) to defend against web attacks.

## Overview
WAF uses a regex-based rule protection engine and a machine learning-based AI protection engine to defend against web vulnerabilities and unknown threats.

WAF's rule protection engine provides expert rule sets based on Tencent Security's accumulated web threat intelligence to automatically prevent OWASP top 10 attacks. Currently, it can defend against 17 categories of common web attacks, such as SQL injections, XSS attacks, malicious scanning, command injection attacks, web application vulnerabilities, WebShell uploads, non-compliant protocols, and trojans.

WAF's rule protection engine supports rule level configuration. You can set the rule protection level according to your actual business needs and enable or disable rule sets, individual rules, and preset rules. You can also use the allowlist of specified URLs and rule IDs to process false positives.

## Directions
### Viewing the rule category
1. Log in to the [WAF console](https://console.cloud.tencent.com/guanjia/tea-service) and select **Service Management** > **Web Rule Library** on the left sidebar.
2. On the **Protection rules** tab, you can view the descriptions and rule updates of the attack categories that WAF currently can defend against.
![](https://qcloudimg.tencent-cloud.cn/raw/b69e92fce90b3eb7c85ca0f960978174.png)

Attack categories that WAF currently can defend against include:
<table>
<thead>
<tr>
<th>Attack Category</th>
<th>Attack Description</th>
</tr>
</thead>
<tbody><tr>
<td>SQL injection attack</td>
<td>In the implementation of websites, the input parameters are not strictly filtered, resulting in the unauthorized acquisition of SQL database content.</td>
</tr>
<tr>
<td>XSS attack</td>
<td>XSS vulnerabilities occur when the application's new webpage contains untrusted data or data that is not properly validated or escaped, or when an existing webpage is updated using a browser API that can create HTML or JavaScript. XSS enables attackers to execute scripts in victims' browsers, hijack user sessions, destroy websites, or redirect users to malicious sites.</td>
</tr>
<tr>
<td>Malicious scanning</td>
<td>WAF can detect whether the website has been maliciously scanned.</td>
</tr>
<tr>
<td>Unauthorized access to core files</td>
<td>WAF can detect whether certain configuration files, database files, and parameter data are downloadable at will.</td>
</tr>
<tr>
<td>Open-source component vulnerability exploiting</td>
<td>Attacks caused by vulnerabilities in common open-source web components.</td>
</tr>
<tr>
<td>Command injection attack</td>
<td>This is a type of injection attacks, such as shell command injections, PHP code injections, and Java code injections, which can cause websites to execute the injected code if successfully exploited by attackers.</td>
</tr>
<tr>
<td>Web application vulnerability exploiting</td>
<td>Web application security (security of Java, ActiveX, PHP, and ASP code running on the web server).</td>
</tr>
<tr>
<td>XXE attack</td>
<td>If the XML processor has external entity references in the XML file, attackers can use external entities to steal internal files and shared files that use the URI file processor, monitor internal scanning ports, execute remote code, and implement denial of service attacks.</td>
</tr>
<tr>
<td>Trojan horse attack</td>
<td>WAF can detect the communication with the control terminal during or after trojan upload.</td>
</tr>
<tr>
<td>File upload attack</td>
<td>After a malicious script disguised as a file with a normal extension is uploaded, attackers can execute it through the local file inclusion vulnerability.</td>
</tr>
<tr>
<td>Other vulnerability exploiting</td>
<td>Attacks caused by the security configuration or vulnerabilities of the web server itself and other software.</td>
</tr>
<tr>
<td>Non-compliant protocol</td>
<td>Exceptions with HTTP protocol and header parameters.</td>
</tr>
</tbody></table>

3. You can view the rule updates on the right of the **Protection rules** tab. For more security notifications, please see [Security Advisory](https://intl.cloud.tencent.com/document/product/627/38433).

### Rule management
1. Log in to the [WAF console](https://console.cloud.tencent.com/guanjia/tea-baseconfig) and select **Configuration Center** > **Basic Security** on the left sidebar.
2. On the page that appears, click **Web security**. On the **Rule engine** tab, you can enable individual rules based on domain names. All rules are enabled by default.
![](https://qcloudimg.tencent-cloud.cn/raw/ed81f20dcbd89a6e34a2444258948088.png)
3. You can search in the rule set by specifying the rule level, defense level, rule ID, attack category, or CVE number to view specific rules and perform operations.
>? The level "Strict" covers rules of the level "Normal" and "Loose", and "Normal" covers "Loose".

![](https://qcloudimg.tencent-cloud.cn/raw/756d827ea0ce084e865b1481e371935e.png)

### Rule allowlist and false positive processing
1. Log in to the [WAF console](https://console.cloud.tencent.com/guanjia/tea-baseconfig) and select **Configuration Center** > **Basic Security** on the left sidebar.
2. On the basic security page, click **Web security**. On the "Rule engine" tab, you can add domain name URLs and rule IDs to the allowlist and process false positives.
3. On the **Rule engine** tab, select the target rule, click **Add to allowlist**, and the custom rule adding window will pop up.
![](https://qcloudimg.tencent-cloud.cn/raw/94f94ceba414af3823eb067171396768.png)
4. In the pop-up window, configure relevant parameters and click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/6ca91f5a136aa91641a1a0c1a2e1a383.png)

**Field description**
 - Rule ID: ID of the rule that needs to be allowed. You can add one rule ID for each policy.
 - Match method: Match method of the URL to be allowed. You can select "Exact match" (default value), "Prefix match", or "Suffix match".
 - URL: URL path to be allowed. The URL must be unique under one domain name.
 - Enable allowlist: It controls whether to enable allowlist, which is disabled by default.
5. After the allowlist is configured, click **View allowlist** to view the allowed rules and perform relevant operations.
![](https://qcloudimg.tencent-cloud.cn/raw/507835ea0c14702e56b9674cf1d879f6.png)

**Field description:**
 - **Rule ID:** ID of the rule added to the allowlist, which can be obtained through attack logs or rule management.
 - **Match method:** Match method of the URL to be allowed. You can select "Exact match" (default value), "Prefix match", or "Suffix match".
 - **URL:** URL path to be allowed. The URL must be unique under one domain name.
 - **Enable allowlist:** It controls whether to enable allowlist.
 - **Last modified:** The last time the rule was added or modified.
 - **Operation:** It allows you to edit or delete a rule.
       - Click **Edit**, modify relevant parameters, and click **OK**.
       - Click **Delete** and confirm the deletion.
