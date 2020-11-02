On September 11, 2020, Tencent Security detected an SQL injection vulnerability in Yonyou GRP-U8 internal control and management software for government affairs. Attackers can use a carefully constructed payload to perform SQL injection attacks in order to get sensitive database information.

Exploitations in the wild (ITW) have been detected, and Tencent Cloud WAF supports defense against them. 

## Vulnerability Details

Attackers can use a carefully constructed payload to perform SQL injection attacks in order to get sensitive database information, and Tencent Cloud WAF currently supports defense against them. 

## Affected Versions

Yonyou GRP-U8 internal control and management software for government affairs.

## Suggestions for Fix
According to the vulnerability advisory, there is currently no official update. Tencent Security recommends you:
- Restrain exposing the software to the public network due to its sensitivity or use an allowlist policy.
- Use WAF to detect and block attacks.



## References
-  [CNVD-2020-49261](https://www.cnvd.org.cn/flaw/show/CNVD-2020-49261)  
-  [Yonyou Gov website](http://shyy.chinaetax.com.cn/)
