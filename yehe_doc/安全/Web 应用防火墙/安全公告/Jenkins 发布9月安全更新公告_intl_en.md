On September 3, 2020, Tencent Security noticed that Jenkins issued its security advisory for September, which contained 14 CVE vulnerabilities (CVE-2020-2238, CVE-2020-2239, CVE-2020-2240, CVE-2020-2241, CVE-2020-2242, CVE-2020-2243, CVE-2020-2244, CVE-2020-2245, CVE-2020-2246, CVE-2020-2247, CVE-2020-2248, CVE-2020-2249, CVE-2020-2250, and CVE-2020-2251) with 10 plugins affected, including:
- Build Failure Analyzer Plugin
- Cadence vManager Plugin
- database Plugin
- Git Parameter Plugin
- JSGames Plugin
- Klocwork Analysis Plugin
- Parameterized Remote Trigger Plugin
- SoapUI Pro Functional Testing Plugin
- Team Foundation Server Plugin
- Valgrind Plugin

The following vulnerabilities are defined as high for severity:
- CVE-2020-2248 (XSS vulnerability in JSGames Plugin)
- CVE-2020-2247 (XXE vulnerability in Klocwork Analysis Plugin)
- CVE-2020-2246 (XSS vulnerability in Valgrind Plugin)
- CVE-2020-2245 (XXE vulnerability in Valgrind Plugin)
- CVE-2020-2244 (XSS vulnerability in Build Failure Analyzer Plugin)
- CVE-2020-2243 (Stored XSS vulnerability in Cadence vManager Plugin)
- CVE-2020-2240 (CSRF vulnerability in database Plugin)
- CVE-2020-2238 (Stored XSS vulnerability in Git Parameter Plugin)

Jenkins is an open-source automated middleware project based on Java for continuous integration and delivery and is commonly used in the development process. To avoid impact on your business, Tencent Security recommends you conduct a security inspection in time. If your business is affected, please update and fix the vulnerabilities promptly to prevent intrusions by attackers. As some vulnerabilities have no fixes yet, we recommend you use Tencent Cloud WAF for defense.

## Vulnerability Details

- **Stored XSS vulnerability in Git Parameter Plugin (CVE-2020-2238)**
	- Git Parameter Plugin 0.9.12 and earlier does not escape the repository field on the "Build with Parameters" page. This results in a stored cross-site scripting (XSS) vulnerability exploitable by attackers with Job/Configure permission.
	- This vulnerability is fixed on Git Parameter Plugin 0.9.13.
	- Secret stored in plain text by Parameterized Remote Trigger Plugin (CVE-2020-2239).
	- Parameterized Remote Trigger Plugin 3.1.3 and earlier stores a secret in plain text.
- **CSRF vulnerability in database Plugin (CVE-2020-2240)**
	- database Plugin 1.6 and earlier does not require POST requests for the database console, resulting in a cross-site request forgery (CSRF) vulnerability. This vulnerability allows attackers to execute arbitrary SQL scripts.
	- CSRF vulnerability and missing permission checks in database Plugin (CVE-2020-2241 (CSRF), CVE-2020-2242 (permission check)).
	- database Plugin 1.6 and earlier does not perform a permission check in a method implementing form validation. This allows attackers with Overall/Read access to Jenkins to connect to an attacker-specified database server using attacker-specified username and password. Additionally, this form validation method does not require POST requests, resulting in a cross-site request forgery (CSRF) vulnerability.
	- database Plugin 1.7 requires POST requests and Overall/Read permission for the affected form validation method.
- **Stored XSS vulnerability in Cadence vManager Plugin (CVE-2020-2243)**
	- Cadence vManager Plugin 3.0.4 and earlier does not escape build descriptions in tooltips. This results in a stored cross-site scripting (XSS) vulnerability exploitable by attackers with Run/Update permission.
	- Cadence vManager Plugin 3.0.5 removes affected tooltips.
- **XSS vulnerability in Build Failure Analyzer Plugin (CVE-2020-2244)**
	- Build Failure Analyzer Plugin 1.27.0 and earlier does not escape matching text in a form validation response. This results in a cross-site scripting (XSS) vulnerability exploitable by attackers able to provide console output for builds used to test build log indications.
	- Build Failure Analyzer Plugin 1.27.1 escapes matching text in the affected form validation response.
- **XXE vulnerability om Valgrind Plugin (CVE-2020-2245)**
	- Valgrind Plugin 0.28 and earlier does not configure its XML parser to prevent XML external entity (XXE) attacks. This allows a user able to control the input files for the Valgrind plugin parser to have Jenkins parse a crafted file that uses external entities for extraction of secrets from the Jenkins controller or server-side request forgery.  
	- As of publication of this advisory, there is no fix.
- **XSS vulnerability in Valgrind Plugin (CVE-2020-2246)**
	- Valgrind Plugin 0.28 and earlier does not escape content in Valgrind XML reports. This results in a stored cross-site scripting (XSS) vulnerability exploitable by attackers able to control Valgrind XML report contents.
	- As of publication of this advisory, there is no fix.

- **XE vulnerability in Klocwork Analysis Plugin (CVE-2020-2247)**
	- Klocwork Analysis Plugin 2020.2.1 and earlier does not configure its XML parser to prevent XML external entity (XXE) attacks. This allows a user able to control the input files for the Klocwork plugin parser to have Jenkins parse a crafted file that uses external entities for extraction of secrets from the Jenkins controller or server-side request forgery.
	- As of publication of this advisory, there is no fix.
- **Reflected XSS vulnerability in JSGames Plugin (CVE-2020-2248)**
	- JSGames Plugin 0.2 and earlier evaluates part of a URL as code. This results in a reflected cross-site scripting (XSS) vulnerability.
	- As of publication of this advisory, there is no fix.
- **Credentials stored in plain text by Team Foundation Server Plugin (CVE-2020-2249)**
	Team Foundation Server Plugin 5.157.1 and earlier stores a webhook secret unencrypted in its global configuration file hudson.plugins.tfs.TeamPluginGlobalConfig.xml on the Jenkins controller as part of its configuration. This secret can be viewed by attackers with access to the Jenkins controller file system.
- **Passwords stored in plain text by SoapUI Pro Functional Testing Plugin (CVE-2020-2250)**
	SoapUI Pro Functional Testing Plugin 1.3 and earlier stores project passwords unencrypted in job config.xml files as part of its configuration. These project passwords can be viewed by attackers with Extended Read permission or access to the Jenkins controller file system. SoapUI Pro Functional Testing Plugin 1.4 stores project passwords encrypted once affected job configurations are saved again.
- **Passwords transmitted in plain text by SoapUI Pro Functional Testing Plugin (CVE-2020-2251)**
	- SoapUI Pro Functional Testing Plugin stores project passwords in job config.xml files on the Jenkins controller as part of its configuration.
	- While these passwords are stored encrypted on disk since SoapUI Pro Functional Testing Plugin 1.4, they are transmitted in plain text as part of the global configuration form by SoapUI Pro Functional Testing Plugin 1.5 and earlier. These passwords can be viewed by attackers with Extended Read permission.
	- This only affects Jenkins before 2.236, including 2.235.x LTS, as Jenkins 2.236 introduces a security hardening that transparently encrypts and decrypts data used for a Jenkins password form field.
	- As of publication of this advisory, there is no fix.

## Severity
- CVE-2020-2249: low
- CVE-2020-2239: low
- CVE-2020-2241: medium
- CVE-2020-2242: medium
- CVE-2020-2250: medium
- CVE-2020-2251: medium
- CVE-2020-2240: high
- CVE-2020-2247: high
- CVE-2020-2248: high
- CVE-2020-2246: high
- CVE-2020-2245: high
- CVE-2020-2243: high
- CVE-2020-2238: high
- CVE-2020-2244: high

## Affected Versions
- Build Failure Analyzer Plugin <= 1.27.0
- Cadence vManager Plugin <= 3.0.4
- database Plugin <= 1.6
- Git Parameter Plugin <= 0.9.12
- JSGames Plugin <= 0.2
- Klocwork Analysis Plugin <= 2020.2.1
- Parameterized Remote Trigger Plugin <= 3.1.3
- SoapUI Pro Functional Testing Plugin <= 1.3
- SoapUI Pro Functional Testing Plugin <= 1.5
- Team Foundation Server Plugin <= 5.157.1
- Valgrind Plugin <= 0.28

## Fixed Versions
- Build Failure Analyzer Plugin should be updated to version 1.27.1
- Cadence vManager Plugin should be updated to version 3.0.5
- database Plugin should be updated to version 1.7
- Git Parameter Plugin should be updated to version 0.9.13
- Parameterized Remote Trigger Plugin should be updated to version 3.1.4
- SoapUI Pro Functional Testing Plugin should be updated to version 1.4

## Versions to Be Fixed
- JSGames Plugin
- Klocwork Analysis Plugin
- SoapUI Pro Functional Testing Plugin
- Team Foundation Server Plugin
- Valgrind Plugin


## Suggestions for Fix
Certain upgraded plugins have been officially released to fix these vulnerabilities; however, as some of them have no fix yet, Tencent Security recommends you:
- Update the corresponding Jenkins plugins (as the plain text storage vulnerability is a local vulnerability, you need to wait for the plugin update).
- Restrain exposing Jenkins to the public network due to its sensitivity. If there is a need for public network access, you can configure an access policy such as [IP allowlist](https://intl.cloud.tencent.com/document/product/627/35646) in WAF.
- Use WAF to detect and block network-based attacks through the vulnerabilities in the Jenkins Security Advisory for September.

WAF supports detection of and defense against all the vulnerabilities contained in the Jenkins Security Advisory for September.


## References
 The official advisory is as follows:
- [Jenkins Security Advisory 2020-09-01](https://www.jenkins.io/security/advisory/2020-09-01/) 
- [CVE-2020-2238](https://nvd.nist.gov/vuln/detail/CVE-2020-2238)
- [CVE-2020-2239](https://nvd.nist.gov/vuln/detail/CVE-2020-2239)
- [CVE-2020-2240](https://nvd.nist.gov/vuln/detail/CVE-2020-2240)
- [CVE-2020-2241](https://nvd.nist.gov/vuln/detail/CVE-2020-2241)
- [CVE-2020-2242](https://nvd.nist.gov/vuln/detail/CVE-2020-2242)
- [CVE-2020-2243](https://nvd.nist.gov/vuln/detail/CVE-2020-2243)
- [CVE-2020-2244](https://nvd.nist.gov/vuln/detail/CVE-2020-2244)
- [CVE-2020-2245](https://nvd.nist.gov/vuln/detail/CVE-2020-2245)
- [CVE-2020-2246](https://nvd.nist.gov/vuln/detail/CVE-2020-2246)
- [CVE-2020-2247](https://nvd.nist.gov/vuln/detail/CVE-2020-2247)
- [CVE-2020-2248](https://nvd.nist.gov/vuln/detail/CVE-2020-2248)
- [CVE-2020-2249](https://nvd.nist.gov/vuln/detail/CVE-2020-2249)
- [CVE-2020-2250](https://nvd.nist.gov/vuln/detail/CVE-2020-2250)
- [CVE-2020-2251](https://nvd.nist.gov/vuln/detail/CVE-2020-2251)




