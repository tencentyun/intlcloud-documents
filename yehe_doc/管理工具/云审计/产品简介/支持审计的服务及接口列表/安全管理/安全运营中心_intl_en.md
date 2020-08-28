Security Operation Center (SOC) is a native unified security operation and management platform provided by Tencent Cloud, which has a rich set of features such as automated asset stocktaking, internet attack surface surveying, cloud security configuration risk inspection, compliance risk assessment, traffic threat detection, leakage monitoring, log audit, retrieval, and investigation, security orchestration, automation, and response (SOAR), and security visualization. With the aid of SOC, you can implement a visualized and automated one-stop cloud security operation and management process including pre-event prevention, mid-event monitoring and threat detection, and post-event response and processing.

SOC operations supported by CloudAudit are as shown below:

| Operation Name | Resource Type | Event Name |
|---------------------|------|-------------------------------|
| Manipulating leakage monitoring data            | ssa  | SaDivulgeDataOperate          |
| Deleting monitoring scanning rule policy          | ssa  | SaDivulgeScanRuleDelete       |
| Setting monitoring scanning rule policy for service configured with leakage monitoring    | ssa  | SaDivulgeScanRuleMutate       |
| Deleting the allowlist for service leakage monitoring       | ssa  | SaDivulgeScanWhiteDelete      |
| Setting the allowlist for service leakage monitoring          | ssa  | SaDivulgeScanWhiteMutate      |
| Confirming the SLA protocol for security intelligence and quick leakage scanning | ssa  | SaIntelligenceYdVulScanSlaSet |
| Activating SSA         | ssa  | SaSecProductOpen              |
| Setting weekly security report configuration            | ssa  | SaSecWeeklySetConfig          |
| Reporting user behavior              | ssa  | SaUserBehaviorReport          |
| Customizing user log and name information      | ssa  | SaUserLogoModify              |
