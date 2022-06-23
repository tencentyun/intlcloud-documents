## Vulnerability Details
On October 20, 2020, Tencent Security noticed that Oracle released a [patch update advisory](https://www.oracle.com/security-alerts/cpuoct2020.html). It revealed WebLogic vulnerabilities, among which CVE-2020-14882 and CVE-2020-14883 existed in the WebLogic console, a default component on all WebLogic versions. Attackers can exploit CVE-2020-14882 and CVE-2020-14883 to execute arbitrary code on the server, obtain system permissions, and control the server without authorization, compromising data confidentiality, integrity, and availability.

All Tencent Security services have upgraded rules and vulnerability libraries accordingly to prevent attacks.

To safeguard your business, we recommend you conduct a security inspection in time. If your business is affected, update it to fix the vulnerability promptly and prevent intrusions by attackers.

## Risk Level
High Risk

## Vulnerability Risk
Attackers can exploit the vulnerabilities to control Oracle WebLogic Server, compromising data confidentiality, integrity, and availability.

## Affected Versions
- Oracle WebLogic Server 10.3.6.0.0
- Oracle WebLogic Server 12.1.3.0.0
- Oracle WebLogic Server 12.2.1.3.0
- Oracle WebLogic Server 12.2.1.4.0
- Oracle WebLogic Server 14.1.1.0.0


## Suggestions for Fix
A new version has been officially released to fix the vulnerabilities. Tencent Security recommends you:
- Recommendation solution: [Install the patch](https://www.oracle.com/security-alerts/cpuoct2020.html) in time.
- Use WAF to block similar WebLogic vulnerability attacks.


## References
For more information, see [Oracle Critical Patch Update Advisory - October 2020](https://www.oracle.com/security-alerts/cpuoct2020.html).
