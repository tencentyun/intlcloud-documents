## Filter
Filter of the descriptor key-value pair for conditional filtering queries such as filtering ID, name and status.

If there are multiple filters, the relationship among them is logical AND.
If there are multiple values ​​in the same filter, the relationship among the values ​​is logical OR.

Referenced by: DescribeMonitors, DescribeSites, DescribeVuls.

| Name | Type | Required | Description |
|------|------|----------|------|
| Name | String | Yes | Name of the filter key. |
| Values | Array of String | Yes | One or more filter values. |

## Monitor

Basic data of the monitoring task.

Referenced by: DescribeMonitors.

| Name | Type | Description |
|------|------|-------|
| Appid | Integer | Cloud user's appid. |
| Id | Integer | Monitoring task ID. |
| Name | String | Monitoring task name. |
| MonitorStatus | Integer | Monitoring status: 1 - monitoring, 2 - monitoring paused. |
| ScannerType | String | Monitoring mode; normal - normal scan, deep - deep scan. |
| Crontab | Integer | Scanning cycle in hours, i.e. executed every X hour(s). |
| IncludedVulsTypes | String | Specified scan type with 3 digits indicating web vulnerability scan, system vulnerability scan and system port scan sequentially. |
| RateLimit | Integer | Rate limit, i.e. sending X HTTP request(s) per second. |
| FirstScanStartTime | Timestamp | Start time of the first scan. |
| ScanStatus | Integer | Scan status: 0 - to be scanned (no scan results); 1 - scanning (scanning in progress); 2 - scanned (with scan results and not scanning); 3 - scan completed and waiting for result synchronization. |
| LastScanFinishTime | Timestamp | Completion time of the last scan. |
| CurrentScanStartTime | Timestamp | Start time of the current scan; if scan completed, start time of the last scan. |
| CreatedAt | Timestamp | Created time. |
| UpdatedAt | Timestamp | Updated time. |

## MonitorMiniSite

Website information in the monitoring task.

Referenced by: DescribeMonitors, DescribeVulsNumber.

| Name | Type | Description |
|------|------|-------|
| SiteId | Integer | Website ID. |
| Url | String | Website URL. |

## MonitorsDetail

Monitoring task details.

Referenced by: DescribeMonitors.

| Name | Type | Description |
|------|------|-------|
| Progress | Integer | The average scan progress of the list of the websites included in the monitoring task. |
| PageCount | Integer | Total number of pages scanned. |
| Basic | [Monitor](#Monitor) | Basic information of the monitoring task. |
| Sites | Array of [MonitorMiniSite](#MonitorMiniSite) | List of the websites included in the monitoring task. |
| SiteNumber | Integer | Number of the websites included in the monitoring task. |
| ImpactSites | Array of [MonitorMiniSite](#MonitorMiniSite) | List of the websites included in the monitoring task that are threatened by vulnerabilities. |
| ImpactSiteNumber | Integer | Number of the websites included in the monitoring task that are threatened by vulnerabilities. |
| VulsHighNumber | Integer | Number of high-risk vulnerabilities. |
| VulsMiddleNumber | Integer | Number of medium-risk vulnerabilities. |
| VulsLowNumber | Integer | Number of low-risk vulnerabilities. |
| VulsNoticeNumber | Integer | Number of notices. |

## Site

Website data

Referenced by: DescribeSites.

| Name | Type | Description |
|------|------|-------|
| Progress | Integer | Scan progress, a percentile integer |
| Appid | Integer | Cloud user's appid. |
| Uin | String | Cloud user's ID. |
| NeedLogin | Integer | Whether the website requires login for scan: 0 - unknown, -1 - not required, 1- required. |
| LoginCookie | String | Cookie after login. |
| LoginCookieValid | Integer | Whether the cookie after login is valid: 0 - invalid, 1 - valid. |
| LoginCheckUrl | String | The URL used to test whether the cookie is valid. |
| LoginCheckKw | String | The keyword used to test whether the cookie is valid. |
| ScanDisallow | String | Directory keywords that prevent scanner from scanning. |
| UserAgent | String | ID of the client accessing the website. |
| Id | Integer | Website ID. |
| MonitorId | Integer | Monitoring task ID; if 0, no monitoring task is added. |
| Url | String | Website URL. |
| Name | String | Website name. |
| VerifyStatus | Integer | Verification status: 0 - not verified; 1 - verified; 2 - verification failed and to be verified again. |
| MonitorStatus | Integer | Monitoring status: 0 - not monitored; 1 - monitoring; 2 - monitoring paused. |
| ScanStatus | Integer | Scan status: 0 - to be scanned (no scan results); 1 - scanning (scanning in progress); 2 - scanned (with scan results and not scanning); 3 - scan completed and waiting for result synchronization. |
| LastScanTaskId | Integer | ID of the last AIScanner scan task; pay attention to cancellations. |
| LastScanStartTime | Timestamp | Start time of the last scan. |
| LastScanFinishTime | Timestamp | Completion time of the last scan. |
| LastScanCancelTime | Timestamp | Time of the last cancellation; if canceled, result of the last scan. |
| LastScanPageCount | Integer | Number of pages scanned during last scan. |
| LastScanScannerType | String | normal - normal scan; deep - deep scan. |
| LastScanVulsHighNum | Integer | Number of high-risk vulnerabilities during last scan. |
| LastScanVulsMiddleNum | Integer | Number of medium-risk vulnerabilities during last scan. |
| LastScanVulsLowNum | Integer | Number of low-risk vulnerabilities during last scan. |
| LastScanVulsNoticeNum | Integer | Number of notices during last scan. |
| CreatedAt | Timestamp | Added time of the record. |
| UpdatedAt | Timestamp | Last modified time of the record. |
| LastScanRateLimit | Integer | Rate limit, i.e. sending X HTTP request(s) per second. |
| LastScanVulsNum | Integer | Total number of vulnerabilities during last scan. |
| LastScanNoticeNum | Integer | Total number of notices during last scan.

## SitesVerification

Website verification data.

Referenced by: DescribeSitesVerification.

| Name | Type | Description |
|------|------|-------|
| Id | Integer | ID. |
| Appid | Integer | Cloud user's appid |
| VerifyUrl | String | URL used to verify the website, i.e. visiting this URL to obtain the verification data. |
| VerifyFileUrl | String | URL used to obtain the verification file. |
| Domain | String | Root domain name. |
| TxtName | String | Name of the TXT domain name verification. |
| TxtText | String | Text of the TXT domain name verification. |
| ValidTo | Timestamp | Verification expiry date, i.e. valid before this date. |
| VerifyStatus | Integer | Verification status: 0 - not verified; 1 - verified; 2 - verification failed and to be verified again. |
| CreatedAt | Timestamp | Created time. |
| UpdatedAt | Timestamp | Updated time. |

## Vul

Vulnerability data.

Referenced by: DescribeVuls.

| Name | Type | Description |
|------|------|-------|
| IsReported | Integer | Whether a false positive has been added; 0 - no, 1 - yes. |
| Appid | Integer | Cloud user's appid. |
| Uin | String | Cloud user's ID. |
| Id | Integer | Vulnerability ID. |
| SiteId | Integer | Website ID. |
| TaskId | Integer | Scan task ID of the scan engine. |
| Level | String | Vulnerability level: high, medium, low, notice. |
| Name | String | Vulnerability name. |
| Url | String | URL containing the vulnerability. |
| Html | String | URL/details. |
| Nickname | String | Vulnerability type. |
| Harm | String | Harm description. |
| Describe | String | Vulnerability description. |
| Solution | String | Solution. |
| From | String | Vulnerability reference. |
| Parameter | String | The vulnerability is exploited through this parameter. |
| CreatedAt | Timestamp | Created time. |
| UpdatedAt | Timestamp | Updated time. |

## VulsTimeline

User vulnerability statistics over time.

Referenced by: DescribeVulsNumberTimeline.

| Name | Type | Description |
|------|------|-------|
| Id | Integer | ID. |
| Appid | Integer | Cloud user's appid. |
| Date | Timestamp | Date. |
| PageCount | Integer | Total number of pages scanned. |
| SiteNum | Integer | Total number of websites verified. |
| ImpactSiteNum | Integer | Total number of websites affected. |
| VulsHighNum | Integer | Total number of high-risk vulnerabilities. |
| VulsMiddleNum | Integer | Total number of medium-risk vulnerabilities. |
| VulsLowNum | Integer | Total number of low-risk vulnerabilities. |
| VulsNoticeNum | Integer | Total number of risk notices. |
| CreatedAt | Timestamp | Added time of the record. |
| UpdatedAt | Timestamp | Last modified time of the record. |


