This document describes how to determine possible causes of instance login failures after you purchase Cloud Virtual Machine (CVM) instances, helping you locate and resolve CVM login failures.

## Possible Causes

The following figure shows the primary causes of CVM instance login failures and their probabilities. If you cannot connect to an instance, we recommended you use the diagnosis tool and perform troubleshooting as instructed below.
<img src="https://main.qcloudimg.com/raw/d8e0151489003a251514eebe74dc201a.png" height="310" width="520" />

## Troubleshooting

### Confirming the instance type

You must first determine whether your purchased instance is a Windows system instance or Linux system instance. The causes of login failures vary by instance types. According to your purchased instance type, refer to the following documentation to locate and resolve the issue.
- [Unable to log into a Windows instance](http://intl.cloud.tencent.com/document/product/213/10339)
- [Unable to log into a Linux instance](https://intl.cloud.tencent.com/document/product/213/32500)

### Using the diagnosis tool to locate the causes
Tencent Cloud provides [Port Verification](https://console.cloud.tencent.com/vpc/helper) to help you determine possible causes of login failures. More than 70% of login issues can be checked and located by this tool.

#### Self-Diagnosis Tool
Problems that can be diagnosed include high bandwidth usage rate, zero public network bandwidth, high server workload, improper security group rules, DDoS attack blocking, security isolation, and account in arrears.

#### Port Verification Tool
This tool can diagnose security group- and port-related problems. If there is a security group configuration issue, you can use **Open All Ports** function of the tool to open all commonly used interfaces of the security group.
If you locate the cause of the issue using the tool, we recommend you follow the corresponding issue guidelines to resolve it.

### Restarting Instance
After the diagnosis tool has located and managed the corresponding issue, or it is still not possible to locate the cause of the login failure using the diagnosis tool, you can restart the instance and connect remotely again to see whether the connection succeeds.
For information about how to restart an instance, see [Restart Instance](http://intl.cloud.tencent.com/document/product/213/4928).

### Other common causes of login failures
If you cannot locate the cause of the issue following the above-mentioned steps, or you receive the following error messages when logging in to the CVM, refer to the following solutions.

#### Windows Instances
- [Windows instance: Unauthorized to log in via remote desktop service](https://intl.cloud.tencent.com/document/product/213/32420)
- [Windows instance: Mac remote login exception](https://intl.cloud.tencent.com/document/product/213/32422)
- [Windows instance: Authentication error](https://intl.cloud.tencent.com/document/product/213/32421)
- [Windows instance: Remote desktop cannot connect to the remote computer](https://intl.cloud.tencent.com/document/product/213/32404)

#### Linux Instances
[Linux instance: Unable to login due to high CPU and memory usage rates](https://intl.cloud.tencent.com/document/product/213/32387)

## Subsequent Operations

If you still cannot log in remotely following the above-mentioned steps, save the related logs and self-diagnosis results, then [Submit Ticket](https://console.cloud.tencent.com/workorder/category).
