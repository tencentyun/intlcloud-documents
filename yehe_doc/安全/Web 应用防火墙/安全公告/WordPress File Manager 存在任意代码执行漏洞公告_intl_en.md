On September 6, 2020, Tencent Security detected an arbitrary code execution vulnerability in the File Manager plugin of WordPress. Attackers can exploit this vulnerability to upload trojans and run arbitrary commands and malicious scripts on WordPress websites that contain File Manager.

Tencent Security has captured exploitations in the wild (ITW), and Tencent Cloud WAF currently supports defense against them.

## Vulnerability Details
Tencent Security detected an arbitrary code execution vulnerability in the File Manager plugin of WordPress. Attackers can exploit this vulnerability to upload trojans and run arbitrary commands and malicious scripts on WordPress websites that contain File Manager. In the plugin library of wordpress.org, the version 6.8 provided by File Manager before September 1, 2020 is the affected version, which can be used by attackers to damage websites.

File lib/php/\*.php can be by default opened directly, and this file loads lib/php/\*.php which reads POST/GET variables, and then allows executing some internal features, like uploading files. PHP is allowed, thus this leads to unauthenticated arbitrary file upload and remote code execution.


## Affected Versions

WordPress File Manager < 6.9

## Suggestions for Fix
An upgraded plugin has been officially released to fix this vulnerability. Tencent Security recommends you:
- Update WordPress File Manager to v6.9 and above.
- Use WAF to detect and block attacks.



## References
[CVE 2020-25213](https://wpvulndb.com/vulnerabilities/10389) 
