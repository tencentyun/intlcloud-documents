Tencent Cloud Web Application Firewall (WAF) is an AI-based one-stop web business risk prevention solution. Backed by Tencent Cloud's security big data detection capabilities and 19 years of experience in internal web business protection, it comprehensively protects the security of website systems and businesses through defense policies in multiple dimensions, including web intrusion prevention, zero-day vulnerability patch, malicious access penalty, and cloud backup for anti-tampering.

The following table lists the WAF operations supported by CloudAudit:

| Operation | Resource Type | Event Name |
|---------------------|------|--------------------------------|
| Add anti-tampering URL | waf | AddAntiFakeUrl |
| Add information leakage prevention rule | waf | AddAntiInfoLeakRules |
| Add API rule | waf | AddApiRule |
| Add banned region | waf | AddAreaBanAreas |
| Add custom blocking page | waf | AddBlockPage |
| Add custom payload | waf | AddCustomPayload |
| Add custom policy | waf | AddCustomRule |
| Add domain name rule allowlist | waf | AddDomainWhiteRule |
| Add Sparta protected domain name | waf | AddSpartaProtection |
| Apply custom blocking page to domain name | waf | ApplyBlockPage |
| Copy Bot_V2 TCB policy domain name | waf | CopyBotTCBRule |
| Copy Bot_V2 UCB custom policy | waf | CopyBotUCBFeatureRules |
| Copy Bot_V2 UCB preset policy | waf | CopyBotUCBPreinstallRule |
| Add WAF Sparta cache path | waf | CreateCachePath |
| Create postpaid CLS instance | waf | CreateClsForAfterpay |
| Copy region ban to another domain name | waf | CreateCopyAreaBan |
| Copy custom rule to another domain name | waf | CreateCopyCustomRule |
| Add domain name for DNS hijacking detection | waf | CreateDNSDetectDomain |
| Add protected domain name | waf | CreateHost |
| Create business allowlist | waf | CreateWhiteList |
| Delete anti-tampering URL | waf | DeleteAntiFakeUrl |
| Delete information leakage prevention rule | waf | DeleteAntiInfoLeakRule |
| Delete attack log download task record | waf | DeleteAttackDownloadRecord |
| Delete custom blocking page | waf | DeleteBlockPage |
| Delete WAF CC V2 rule | waf | DeleteCCRule |
| Delete WAF Sparta cache path | waf | DeleteCachePath |
| Delete custom payload | waf | DeleteCustomPayloads |
| Delete custom rule | waf | DeleteCustomRule |
| Delete domain name under DNS hijacking detection | waf | DeleteDNSDetectDomain |
| Delete domain name rule allowlist | waf | DeleteDomainWhiteRules |
| Delete access log download record | waf | DeleteDownloadRecord |
| Delete CLB-WAF protected domain name | waf | DeleteHost |
| Delete WAF IP blocklist/allowlist | waf | DeleteIpAccessControl |
| Delete session settings for CC attack | waf | DeleteSession |
| Delete WAF Sparta protected domain name | waf | DeleteSpartaProtection |
| Delete business allowlist | waf | DeleteWhiteList |
| Refresh anti-tampering URL | waf | FreshAntiFakeUrl |
| Manually import API rule | waf | ImportApiRules |
| Train model | waf | ModifyAIModelai |
| Edit anti-tampering URL | waf | ModifyAntiFakeUrl |
| Enable or disable anti-tampering | waf | ModifyAntiFakeUrlStatus |
| Enable or disable information leakage prevention rule | waf | ModifyAntiInfoLeakRuleStatus |
| Edit information leakage prevention rule | waf | ModifyAntiInfoLeakRules |
| Modify region information in region ban | waf | ModifyAreaBanAreas|
| Modify region ban status | waf | ModifyAreaBanStatus |
| Enable or disable Bot_V2 bot | waf | ModifyBotStatus |
| Update Bot_V2 TCB policy | waf | ModifyBotTCBRule |
| Update Bot_V2 UCB preset rule | waf | ModifyBotUCBPreinstallRule |
| Cache WAF Sparta cache path | waf | ModifyCachePath |
| Edit custom rule | waf | ModifyCustomRule |
| Enable or disable custom policy | waf | ModifyCustomRuleStatus |
| Edit domain name for DNS hijacking detection | waf | ModifyDNSDetectDomain |
| Modify rule | waf | ModifyDomainWhiteRule |
| Enable or disable access log for domain name list | waf | ModifyDomainsCLSStatus |
| Enable or disable WAF for domain name list | waf | ModifyDomainsStatus |
| Edit protected domain name | waf | ModifyHost |
| Enable or disable access log for domain name | waf | ModifyHostAccessLogStatus |
| Set the traffic mode of protected domain name | waf | ModifyHostFlowMode |
| Set the protection status of protected domain name | waf | ModifyHostMode |
| Enable or disable WAF for protected domain name | waf | ModifyHostStatus |
| Enable or disable QPS elastic billing for instance | waf | ModifyInstanceElasticMode |
| Enable or disable auto-renewal for instance | waf | ModifyInstanceRenewFlag |
| Update frontend defense rule | waf | ModifyJsInjectRule |
| Update the status of frontend defense rule | waf | ModifyJsInjectRuleStatus |
| Set auto-renewal for package | waf | ModifyPackageRenew |
| Change protection level | waf | ModifyProtectionLevel |
| Enable or disable WAF Sparta | waf | ModifyProtectionStatuswaf |
| Enable or disable auto-renewal for WAF version | waf | ModifySpartaPackageRenewSparta |
| Modify domain name configuration | waf | ModifySpartaProtection |
| Set WAF protection status | waf | ModifySpartaProtectionMode |
| Set webshell status | waf | ModifyWebshellStatus |
| Update business allowlist | waf | ModifyWhiteList |
| Create attack log search and download task | waf | PostAttackDownloadTask |
| Refresh the result of integration check | waf | RefreshAccessCheckResult |
| Enable or disable API rule | waf | SwitchApiRules |
| Enable or disable domain name rule | waf | SwitchDomainRules |
| Enable or disable domain name allowlist | waf | SwitchDomainWhiteRules |
| Enable or disable elastic QPS | waf | SwitchElasticMode |
| Update Bot_V2 UCB policy | waf | UpsertBotUCBFeatureRule |
| Update WAF Sparta automatic CC blocking status | waf | UpsertCCAutoStatus |
| Upsert WAF CC V2 | waf | UpsertCCRule |
| Specify whether to pass through client IP and port | waf | UpsertClientMsg |
| Upsert WAF IP blocklist/allowlist | waf | UpsertIpAccessControl |
| Upsert session definition | waf | UpsertSessionWaf |
| Query download record | waf | WafDownloadRecords |
| Download query log | waf | WafDownloadlogs |
