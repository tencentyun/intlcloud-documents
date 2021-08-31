Certificates sold on Tencent Cloud official website are compatible with the mainstream browser versions. See below for the detailed compatibility test report:
|Browser|SecureSite EV|Geotrust EV|SecureSite OV|Geotrust OV|TrustAsia G5 DV|Geotrust DV|
|---|---|---|---|---|---|---|
|IE6 (SHA2 patched)|Supported|Supported|Supported|Supported|Supported|Supported|
|IE (8+)|Supported|Supported|Supported|Supported|Supported|Supported|
|QQ (9.5.1/9.5.2)|CT error|CT error|CT error|CT error|CT error|CT error |
|QQ (7+)|Supported|Supported|Supported|Supported|Supported|Supported|
|Baidu (6+)|Supported|Supported|Supported|Supported|Supported|Supported|
|Maxthon (4.4+)|Supported|Supported|Supported|Supported|Supported|Supported|
|360 (8.1)|Supported|Supported|Supported|Supported|Supported|Supported|
|360 (6+)|Supported|Supported|Supported|Supported|Supported|Supported|
|UC (5+)|Supported|Supported|Supported|Supported|Supported|Supported|
|Sogou (6+)|Supported|Supported|Supported|Supported|Supported|Supported|
|CM (3+)|Supported|Supported|Supported|Supported|Supported|Supported|
|2345 (7.1+)|Supported|Supported|Supported|Supported|Supported|Supported|
|ChromePlus (2+)|Supported|Supported|Supported|Supported|Supported|Supported|
|TheWorld (3.6+)|Supported|Supported|Supported|Supported|Supported|Supported|
|Opera (34+)|Supported|Supported|Supported|Supported|Supported|Supported|
|Safari (5+)|Supported|Supported|Supported|Supported|Supported|Supported|
|Edge|Supported|Supported|Supported|Supported|Supported|Supported|
|Firefox (25+)|Supported|Supported|Supported|Supported|Supported|Supported|
|Chrome (53/54)|CT error|CT error|CT error|CT error|CT error|CT error|
|Chrome (46+)|Supported|Supported|Supported|Supported|Supported|Supported|

>Certificate Transparency (CT) is a policy for Google Chrome to monitor and verify HTTPS certificates. Due to a kernel bug in Chrome 53/54, CT error occurs in all certificates of SecureSite CA issued after June 1, 2016. Chrome handled this problem with automatic patch immediately, and fixed this problem in version 55. This issue doesn’t affect users who can connect to Chrome's server. Since most users in China cannot access Chrome's server, it is recommended to upgrade to version 55+ to solve this problem. And, QQ browser using kernel of Chromium（53/54）version is also affected.
Click [here](https://intl.cloud.tencent.com/document/product/1007/30190) to check specific issues and announcements.
