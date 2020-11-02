On September 17, 2020, Tencent Security detected that Microsoft issued a security advisory for a command execution vulnerability in Exchange Server (CVE-2020-16875).
>?Microsoft Exchange Server is an email service program offered by Microsoft Corporation, which provides various features such as mail access, storage, forwarding, voice mail, and mail filtering.
>
The POC of the vulnerability is being circulated on the internet. Tencent Security recommends you upgrade Exchange to the latest version in time and implement asset inspection and protection to avoid attacks by hackers. Tencent Cloud WAF currently supports defense against them. 

## Vulnerability Details


A remote code execution vulnerability exists in Microsoft Exchange server due to improper validation of cmdlet arguments. An attacker who successfully exploited the vulnerability could run arbitrary code in the context of the System user. Exploitation of the vulnerability requires successful authentication by Exchange. As the Exchange service ran with SYSTEM privileges, an attacker could get the highest privileges of the system by exploiting this vulnerability.


## Affected Versions
- Microsoft Exchange Server 2016 Cumulative Update 16
- Microsoft Exchange Server 2016 Cumulative Update 17
- Microsoft Exchange Server 2019 Cumulative Update 5
- Microsoft Exchange Server 2019 Cumulative Update 6

## Suggestions for Fix
According to the vulnerability advisory, Tencent Security recommends you:
- Update to the latest version for fix in time.
- Use WAF to detect and block attacks.

## References
[CVE-2020-16875](https://portal.msrc.microsoft.com/en-US/security-guidance/advisory/CVE-2020-16875) 

