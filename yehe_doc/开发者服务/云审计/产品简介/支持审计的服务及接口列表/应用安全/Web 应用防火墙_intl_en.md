Tencent Cloud Web Application Firewall (WAF) is an AI-based one-stop solution for preventing web business operation risks. Based on Tencent Cloud's security big data detection capabilities and 19 years of experience in web security protection gained from Tencent's businesses, WAF protects website system and business security comprehensively through multi-dimensional protection policies such as web intrusion prevention, zero-day vulnerability patching and fixing, malicious access blocking, and cloud backup anti-tampering.

WAF operations supported by CloudAudit are as shown below:

| Operation Name | Resource Type | Event Name |
|---------------------|------|--------------------------------|
| Getting bot switch in Bot_V2    | waf  | BotV2GetSwitchStat             |
| Querying WAF CC protection policy V2   | waf  | DescirbeCCRule                 |
| Getting access log cursor            | waf  | DescribeAccessCursor           |
| Querying access log download task          | waf  | DescribeAccessDownloadRecords  |
| Querying the number of access logs matching search condition     | waf  | DescribeAccessLogCount         |
| Querying access log              | waf  | DescribeAccessLogs             |
| Querying WAF IP status      | waf  | DescribeActionedIp             |
| Getting AI model status            | waf  | DescribeAIModelStatus          |
| Verifying whether the request is an attack in the WAF AI engine          | waf  | DescribeAIVerifyResult         |
| Getting anti-tampering URL            | waf  | DescribeAntiFakeUrl            |
| Getting the list of information leakage prevention rules         | waf  | DescribeAntiInfoLeakRules      |
| Getting region-specific blocking configuration            | waf  | DescribeAreaBanAreas           |
| Getting the list of regions supported by WAF region blocking    | waf  | DescribeAreaBanSupportAreas    |
| Getting attack log details            | waf  | DescribeAttackDetail           |
| Querying the download record of attack log         | waf  | DescribeAttackDownloadRecords  |
| Querying the number of attack logs            | waf  | DescribeAttackLogCount         |
| Querying city distribution of attacks               | waf  | DescribeAttackWorldMap         |
| Getting bot action statistics in Bot_V2  | waf  | DescribeBotActionStat          |
| Getting domain name bot statistics in Bot_V2    | waf  | DescribeBotAggregateDomainStat |
| Getting bot details               | waf  | DescribeBotRecordDetail        |
| Getting bot record access details in Bot_V2  | waf  | DescribeBotRecordItems         |
| Getting bot record access trend          | waf  | DescribeBotRecordPoints        |
| Getting bot statistics by geographic location in Bot_V2   | waf  | DescribeBotRegionsStat         |
| Getting bot traffic statistics in Bot_V2     | waf  | DescribeBotStatisticPoints     |
| Getting bot switch in Bot_V2     | waf  | DescribeBotStatus              |
| Getting the bots in TCB type in Bot_V2 | waf  | DescribeBotTCBRecords          |
| Getting TCB rule in Bot_V2    | waf  | DescribeBotTCBRule             |
| Getting bot type statistics in Bot_V2     | waf  | DescribeBotTypeStat            |
| Getting bots in UB type in Bot_V2 | waf  | DescribeBotUBRecords           |
| Getting custom UCB policy in Bot_V2 | waf  | DescribeBotUCBFeatureRule      |
| Getting preset UCB policy in Bot_V2  | waf  | DescribeBotUCBPreinstallRule   |
| Getting bots in UCB type in Bot_V2 | waf  | DescribeBotUCBRecords          |
| Querying automatic CC blocking status on the WAF backend | waf  | DescribeCCAutoStatus           |
| Querying log service usage status          | waf  | DescribeCLS                    |
| Querying custom payload list      | waf  | DescribeCustomPayloads         |
| Getting the data of the number of hijacked users in DNS hijacking detection | waf  | DescribeDNSDetectDataChart     |
| DNS hijacking - Getting map data       | waf  | DescribeDNSDetectDataMap       |
| Getting the domain name list of DNS hijacking detection      | waf  | DescribeDNSDetectDomainList    |
| Getting the hijacking record of DNS hijacking detection      | waf  | DescribeDNSDetectHijackData    |
| Querying WAF IP blocklist/allowlist        | waf  | DescribeIpAccessControl        |
| Querying WAF IP blocking status        | waf  | DescribeIpHitItems             |
| Querying the overview of business and attack trends         | waf  | DescribePeakPoints             |
| Querying the overview of business and attack peaks         | waf  | DescribePeakValue              |
| Getting product information            | waf  | DescribeProductInfo            |
| Getting the total number of requests in specified period        | waf  | DescribeRequestCount           |
| Querying WAF session definition        | waf  | DescribeSession                |
| Querying user information              | waf  | DescribeSpartUserInfo          |
| Pulling attack type statistics          | waf  | DescribeStatisticTypes         |
| Downloading access logs in batches            | waf  | ExportAccessLogs               |
| Querying WAF price            | waf  | InquiryPriceWafInstance        |
| Log usage              | waf  | WafClsOverview                 |
| Downloading query logs              | waf  | WafDownloadlogs                |
| Querying download record              | waf  | WafDownloadRecords             |
| Querying AI model status            | waf  | WafGetAIModelStatus            |
| Verifying WAF AI with online attack          | waf  | WafGetAIVerifyResult           |
| Querying custom payload list      | waf  | WafGetCustomPayloads           |
| Getting non-standard port              | waf  | WafGetPort                     |
| General WAF API             | waf  | WafInterface                   |
| Querying all logs              | waf  | WafSearchLogs                  |
