## Account

Account list information data.

It is referenced by the API DescribeAccounts.

| Name | Type | Description |
|------|------|-------|
| Id | Integer | Unique ID. |
| Uuid | String | Unique Uuid of the HS client. |
| MachineIp | String | Host private IP. |
| MachineName | String | Host name. |
| Username | String | Account name. |
| Groups | String | The group to which the account belongs. |
| Privilege | String | Account type.<br/><li>ORDINARY: Ordinary account</li><li>SUPPER: Super admin account</li> |
| AccountCreateTime | Timestamp | Creation time of the account. |
| LastLoginTime | Timestamp | Last login time of the account. |

## AccountStatistics

Account statistics.

It is referenced by the API DescribeAccountStatistics.

| Name | Type | Description |
|------|------|-------|
| Username | String | User name. |
| MachineNum | Integer | Number of hosts. |

## AgentVul

Vulnerability information of the host.

It is referenced by the API DescribeAgentVuls.

| Name | Type | Description |
|------|------|-------|
| Id | Integer | Vulnerability ID. |
| MachineIp | String | Host IP. |
| VulName | String | Vulnerability name. |
| VulLevel | String | Risk level of the vulnerability.<br/><li>HIGH: High risk</li><li>MIDDLE: Middle risk</li><li>LOW: Low risk</li><li>NOTICE: Notice</li> |
| LastScanTime | Timestamp | Last scan time. |
| Description | String | Vulnerability description. |
| VulId | Integer | Vulnerability type ID. |
| VulStatus | String | Vulnerability status.<br/><li>UN_OPERATED: Pending</li><li>FIXED: Fixed</li> |

## BruteAttack

List of brute force attacks.

It is referenced by the API DescribeBruteAttacks.

| Name | Type | Description |
|------|------|-------|
| Id | Integer | Event ID. |
| MachineIp | String | Host IP. |
| Status | String | Brute force attack event status.<br/><li>BRUTEATTACK_FAIL_ACCOUNT: Brute force attack event - failed (the account already exists)</li><li>BRUTEATTACK_FAIL_NOACCOUNT: Brute force attack event - failed (the account does not exist)</li><li>BRUTEATTACK_SUCCESS: Brute force attack event - successful</li> |
| UserName | String | User name. |
| City | Integer | City ID. |
| Country | Integer | Country ID. |
| Province | Integer | Province ID. |
| SrcIp | String | Source IP. |
| Count | Integer | Number of brute force attack attempts. |
| CreateTime | Timestamp | Time when a brute force attack event occurs. |
| MachineName | String | Host name. |
| Uuid | String | Unique UUID of the HS client. |

## ChargePrepaid

The relevant parameter setting for the prepaid mode. This parameter can specify the purchased usage period, whether to set automatic renewal, and other attributes of the instance purchased on a prepaid basis.

It is referenced by the APIs InquiryPriceOpenProVersionPrepaid, OpenProVersionPrepaid, and RenewProVersion.

| Name | Type | Required | Description |
|------|------|----------|------|
| Period | Integer | Yes | Purchased usage period of an instance (in month). Value range: 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 24, 36. |
| RenewFlag | String | No | Auto renewal flag. Value range:<br/><li>NOTIFY_AND_AUTO_RENEW: Notify expiry and renew automatically</li><li>NOTIFY_AND_MANUAL_RENEW: Notify expiry but not renew automatically</li><li>DISABLE_NOTIFY_AND_MANUAL_RENEW: Neither notify expiry nor renew automatically</li><br/><br/>Default: NOTIFY_AND_MANUAL_RENEW. If this parameter is specified as NOTIFY_AND_AUTO_RENEW, the instance will be automatically renewed on a monthly basis when the account balance is sufficient. |

## Component

Component list data.

It is referenced by the API DescribeComponents.

| Name | Type | Description |
|------|------|-------|
| Id | Integer | Unique ID. |
| Uuid | String | Unique Uuid of the HS client. |
| MachineIp | String | Host private IP. |
| MachineName | String | Host name. |
| ComponentVersion | String | Component version number. |
| ComponentType | String | Component Type.<br/><li>SYSTEM: System component</li><li>WEB: Web component</li> |
| ComponentName | String | Component name. |
| ModifyTime | Timestamp | Update detection time. |

## ComponentStatistics

Component statistics.

It is referenced by the API DescribeComponentStatistics.

| Name | Type | Description |
|------|------|-------|
| Id | Integer | Component ID. |
| MachineNum | Integer | Number of hosts. |
| ComponentName | String | Component name. |
| ComponentType | String | Component Type.<br/><li>WEB: Web component</li><li>SYSTEM: System component</li> |
| Description | String | Component description. |

## Filter

Key-value pair filters for conditional filtering queries, such as filtering ID, name, status.

If more than one Filter exists, the logical relation between these Filters is "AND".
If there are multiple Values for one Filter, the logical relation between these Values under the same Filter is "OR".

* The number of Filters is limited to 5.
* If there are multiple Values for one Filter, the maximum number of Values is 5.


It is referenced by the following APIs: DescribeAccountStatistics, DescribeAccounts, DescribeAgentVuls, DescribeBruteAttacks, DescribeComponentStatistics, DescribeComponents, DescribeHistoryAccounts, DescribeImpactedHosts, DescribeMachines, DescribeMaliciousRequests, DescribeMalwares, DescribeNonlocalLoginPlaces, DescribeOpenPortStatistics, DescribeOpenPorts, DescribeProcessStatistics, DescribeProcesses, DescribeVuls.

| Name | Type | Required | Description |
|------|------|----------|------|
| Name | String | Yes | The name of the filter key. |
| Values | Array of String | Yes | One or more filter values. |

## HistoryAccount

Update history data of the account.

It is referenced by the API DescribeHistoryAccounts.

| Name | Type | Description |
|------|------|-------|
| Id | Integer | Unique ID. |
| Uuid | String | Unique Uuid of the HS client. |
| MachineIp | String | Host private IP. |
| MachineName | String | Host name. |
| Username | String | Account name. |
| ModifyType | String | Type of account change.<br/><li>CREATE: Created</li><li>MODIFY: Modified</li><li>DELETE: Deleted</li> |
| ModifyTime | Timestamp | Time of account change. |

## ImpactedHost

Information of the affected host.

It is referenced by the API DescribeImpactedHosts.

| Name | Type | Description |
|------|------|-------|
| Id | Integer | Vulnerability ID. |
| MachineIp | String | Host IP. |
| MachineName | String | Host name. |
| LastScanTime | Timestamp | Last detection time. |
| VulStatus | String | Vulnerability status.<br/><li>UN_OPERATED: Pending</li><li>SCANING: Scanning</li><li>FIXED: Fixed</li> |
| Uuid | String | Unique UUID of the HS client. |
| Description | String | Vulnerability description. |
| VulId | Integer | Vulnerability type ID. |

## Machine

Host list.

It is referenced by the API DescribeMachines.

| Name | Type | Description |
|------|------|-------|
| MachineName | String | Host name. |
| MachineOs | String | Host OS. |
| MachineStatus | String | Host status.<br/><li>OFFLINE: Offline</li><li>ONLINE: Online</li> |
| Uuid | String | Unique Uuid of the HS client. An empty character is returned if the client is offline for a long period of time. |
| Quuid | String | Unique Uuid of a CVM or BM. |
| VulNum | Integer | Number of vulnerabilities. 0 is returned for non-pro version. |
| MachineIp | String | Host IP. |
| IsProVersion | Boolean | Indicates whether it is HS Pro.<br/><li>true: Yes</li><li>false: No</li> |
| MachineWanIp | String | Host public IP. |
| PayMode | String | Billing mode.<br/><li>POSTPAY: Postpaid</li><li>PREPAY: Prepaid</li> |

## MaliciousRequest

Malicious request data.

It is referenced by the API DescribeMaliciousRequests.

| Name | Type | Description |
|------|------|-------|
| Id | Integer | Record ID. |
| Uuid | String | UUID of the HS client. |
| MachineIp | String | Host private IP. |
| MachineName | String | Host name. |
| Domain | String | Malicious request domain name. |
| Count | Integer | Number of malicious requests. |
| ProcessName | String | Process name. |
| Status | String | Record status.<br/><li>UN_OPERATED: Pending</li><li>TRUSTED: Trusted</li><li>UN_TRUSTED: Untrusted</li> |
| Description | String | Description of malicious request domain name. |
| Reference | String | Reference URL. |
| CreateTime | Timestamp | Time when a malicious request is found. |
| MergeTime | Timestamp | Time when records are merged. |
| ProcessMd5 | String | Process MD5<br/> value. |
| CmdLine | String | Command line. |
| Pid | Integer | Process PID. |

## Malware

Trojan-related information.

It is referenced by the API DescribeMalwares.

| Name | Type | Description |
|------|------|-------|
| Id | Integer | Event ID. |
| MachineIp | String | Host IP. |
| Status | String | Current status of Trojan.<br/><li>UN_OPERATED: Unprocessed</li><li>SEGREGATED: Isolated</li><li>TRUSTED: Trusted</li><li>SEPARATING: Isolating</li><li>RECOVERING: Recovering</li> |
| FilePath | String | Path of Trojan. |
| Description | String | Trojan description. |
| MachineName | String | Host name. |
| FileCreateTime | Timestamp | Creation time of the Trojan file. |
| ModifyTime | Timestamp | Modification time of the Trojan file. |
| Uuid | String | Unique UUID of the HS client. |

## NonLocalLoginPlace

Remote login.

It is referenced by the API DescribeNonlocalLoginPlaces.

| Name | Type | Description |
|------|------|-------|
| Id | Integer | Event ID. |
| MachineIp | String | Host IP. |
| Status | String | Login status.<br/><li>NON_LOCAL_LOGIN: Remote login</li><li>NORMAL_LOGIN: Intended login</li> |
| UserName | String | User name. |
| City | Integer | City ID. |
| Country | Integer | Country ID. |
| Province | Integer | Province ID. |
| SrcIp | String | Login IP. |
| MachineName | String | Host name. |
| LoginTime | Timestamp | Login time. |
| Uuid | String | Unique Uuid of the HS client. |

## OpenPort

Port list.

It is referenced by the API DescribeOpenPorts.

| Name | Type | Description |
|------|------|-------|
| Id | Integer | Unique ID. |
| Uuid | String | Unique UUID of the HS client. |
| Port | Integer | Open port. |
| MachineIp | String | Host IP. |
| MachineName | String | Host name. |
| ProcessName | String | Process name corresponding to the port. |
| Pid | Integer | Process Pid corresponding to the port. |
| CreateTime | Timestamp | Creation time of the record. |
| ModifyTime | Timestamp | Update time of the record. |

## OpenPortStatistics

Port statistics list.

It is referenced by the API DescribeOpenPortStatistics.

| Name | Type | Description |
|------|------|-------|
| Port | Integer | Port. |
| MachineNum | Integer | Number of hosts. |

## Place

Login location Information.

It is referenced by the API: CreateUsualLoginPlaces.

| Name | Type | Required | Description |
|------|------|----------|------|
| CityId | Integer | Yes | City ID. |
| ProvinceId | Integer | Yes | Province ID. |
| CountryId | Integer | Yes | Country ID. Only Mainland China is supported: 1. |

## ProVersionMachine

Information of a host with HS Pro activated.

It is referenced by the APIs InquiryPriceOpenProVersionPrepaid and OpenProVersionPrepaid.

| Name | Type | Required | Description |
|------|------|----------|------|
| MachineType | String | Yes | Host type.<br/><li>CVM: Cloud virtual machine</li><li>BM: Cloud physical machine</li> |
| MachineRegion | String | Yes | Region where the host locates.<br/>Such as: ap-guangzhou and ap-beijing. |
| Quuid | String | Yes | Unique Uuid of the host.<br/>InstanceId for CPMs, and Uuid for CVMs. |

## Process

Process information data.

It is referenced by the API DescribeProcesses.

| Name | Type | Description |
|------|------|-------|
| Id | Integer | Unique ID. |
| Uuid | String | Unique UUID of the HS client. |
| MachineIp | String | Host private IP. |
| MachineName | String | Host name. |
| Pid | Integer | Process Pid. |
| Ppid | Integer | Process Ppid. |
| ProcessName | String | Process name. |
| UserName | String | Process user name. |
| Platform | String | Platform.<br/><li>WIN32: Windows 32-bit</li><li>WIN64: Windows 64-bit</li><li>LINUX32: Linux 32-bit</li><li>LINUX64: Linux 64-bit</li> |
| FullPath | String | Process path. |
| CreateTime | Timestamp | Creation time. |

## ProcessStatistics

Process statistics.

It is referenced by the API DescribeProcessStatistics.

| Name | Type | Description |
|------|------|-------|
| ProcessName | String | Process name. |
| MachineNum | Integer | Number of hosts. |

## SecurityDynamic

Security event message data.

It is referenced by the API DescribeSecurityDynamics.

| Name | Type | Description |
|------|------|-------|
| Uuid | String | UUID of the HS client. |
| EventTime | Timestamp | Time when a security event occurs. |
| EventType | String | Security event type.<br/><li>MALWARE: Trojan event</li><li>NON_LOCAL_LOGIN: Remote login</li><li>BRUTEATTACK_SUCCESS: Brute force attack succeeded</li><li>VUL: Vulnerability</li><li>BASELINE: Security baseline</li> |
| Message | String | Security event message. |

## SecurityTrend

Security trend statistics.

It is referenced by the API DescribeSecurityTrends.

| Name | Type | Description |
|------|------|-------|
| Date | Date | Event time. |
| EventNum | Integer | Number of events. |

## UsualPlace

Common login location.

It is referenced by the API DescribeUsualLoginPlaces.

| Name | Type | Description |
|------|------|-------|
| Id | Integer | ID. |
| Uuid | String | Unique UUID of the HS client. |
| CountryId | Integer | Country ID. |
| ProvinceId | Integer | Province ID. |
| CityId | Integer | City ID. |

## Vul

Vulnerability list data.

It is referenced by the API DescribeVuls.

| Name | Type | Description |
|------|------|-------|
| VulId | Integer | Vulnerability type ID. |
| VulName | String | Vulnerability name. |
| VulLevel | String | Risk level of the vulnerability.<br/>HIGH: High risk<br/>MIDDLE: Middle risk<br/>LOW: Low risk<br/>NOTICE: Notice |
| LastScanTime | Timestamp | Last scan time. |
| ImpactedHostNum | Integer | Number of affected hosts. |
| VulStatus | String | Vulnerability status.<br/>* UN_OPERATED: Pending<br/>* FIXED: Fixed |

## WeeklyReport

Weekly report list.

It is referenced by the API DescribeWeeklyReports.

| Name | Type | Description |
|------|------|-------|
| BeginDate | Date | Start time of the weekly report. |
| EndDate | Date | End time of the weekly report. |

## WeeklyReportBruteAttack

Brute force attack data in the weekly report of HS Pro.

It is referenced by the API DescribeWeeklyReportBruteAttacks.

| Name | Type | Description |
|------|------|-------|
| MachineIp | String | Host IP. |
| UserName | String | Attacked user name. |
| SrcIp | String | Source IP. |
| Count | Integer | Number of attempts. |
| AttackTime | Timestamp | Attack time. |

## WeeklyReportMalware

Trojan data in the weekly report of HS Pro.

It is referenced by the API DescribeWeeklyReportMalwares.

| Name | Type | Description |
|------|------|-------|
| MachineIp | String | Host IP. |
| FilePath | String | Path of the Trojan file. |
| Md5 | String | MD5 value of the Trojan file. |
| FindTime | Timestamp | Time when the Trojan is detected. |
| Status | String | Current status of Trojan.<br/><li>UN_OPERATED: Unprocessed</li><li>SEGREGATED: Isolated</li><li>TRUSTED: Trusted</li><li>SEPARATING: Isolating</li><li>RECOVERING: Recovering</li> |

## WeeklyReportNonlocalLoginPlace

Remote login data in the weekly report of HS Pro.

It is referenced by the API DescribeWeeklyReportNonlocalLoginPlaces.

| Name | Type | Description |
|------|------|-------|
| MachineIp | String | Host IP. |
| Username | String | User name. |
| SrcIp | String | Source IP. |
| Country | Integer | Country ID. |
| Province | Integer | Province ID. |
| City | Integer | City ID. |
| LoginTime | Timestamp | Login time. |

## WeeklyReportVul

Vulnerability data in the weekly report of HS Pro.

It is referenced by the API DescribeWeeklyReportVuls.

| Name | Type | Description |
|------|------|-------|
| MachineIp | String | Host private IP. |
| VulName | String | Vulnerability name. |
| VulType | String | Vulnerability type.<br/><li> WEB: Web vulnerability</li><li> SYSTEM: System component vulnerability</li><li> BASELINE: Security baseline</li> |
| Description | String | Vulnerability description. |
| VulStatus | String | Vulnerability status.<br/><li>UN_OPERATED: Pending</li><li>SCANING: Scanning</li><li>FIXED: Fixed</li> |
| LastScanTime | Timestamp | Last scan time. |


