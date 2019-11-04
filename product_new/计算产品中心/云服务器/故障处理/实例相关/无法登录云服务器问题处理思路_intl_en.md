This document introduces how to determine the reason of the problem where being unable to log into a CVM and locate and troubleshoot the problem. 

## Common Reasons

The following figure shows the primary causes for inability to connect to a CVM instance. If you cannot connect to an instance, it is recommended you use the diagnosis tool, and perform troubleshooting as instructed below.
<img src="https://main.qcloudimg.com/raw/d8e0151489003a251514eebe74dc201a.png" height="310" width="520" />

## Troubleshooting

### Confirming the Instance Type

First, you must understand whether the type of your purchased instance is Windows system instance or Linux system instance. That is, depending on the different instance types, the reason for inability to log in may be different. You can refer to the following documentation to locate and resolve the issue according to the type of your instance:
- [Unable to log into a Windows instance](http://intl.cloud.tencent.com/document/product/213/10339)
- Unable to log into a Linux instance

### Diagnosing the Cause by Using the Diagnosis Tool
Tencent Cloud provides a [Self-Diagnosis Tool](https://console.cloud.tencent.com/workorder/check) and [Port Verification](https://console.cloud.tencent.com/vpc/helper) tool to help you determine the possible causes for the inability to log in. More than 70% of login issues can be located by using this tool.

#### Self-Diagnosis Tool
Problems that can be diagnosed include high bandwidth usage rate, public network bandwidth of 0, high server load, improper security group rules, DDoS attack blocking, security isolation, and account in arrears.

#### Port Verification Tool
Detects security group- and port-related faults. If there is a security group configuration issue, you can use the **Open All Ports** function of the tool to open all the commonly used interfaces of the security group.
If you locate the cause of the issue using the tool, we recommend that you handle the fault according to the corresponding issue cause guidelines.

### Restarting Instance
After the check tool has determined and handled the corresponding fault, or it is still not possible to locate the cause of the inability to log in by using the check tool, you can restart the instance and then connect remotely again to see whether the connection succeeds.
For information about how to restart an instance, see [Restarting an Instance](http://intl.cloud.tencent.com/document/product/213/4928).

### Other Common Causes of Login Issues
If you cannot locate the cause of the issue through the preceding steps, or if when logging in to the CVM you directly receive the following error information, you can refer to the following solutions.

#### Windows Instances
- [Windows instance: Unauthorized for remote desktop service login](https://intl.cloud.tencent.com/document/product/213/32420 )
- [Windows instance: Mac remote login exception](https://intl.cloud.tencent.com/document/product/213/32422)
- [Windows instance: Authentication error](https://intl.cloud.tencent.com/document/product/213/32421)
- [Windows instance: Remote desktop cannot connect to the remote computer](https://intl.cloud.tencent.com/document/product/213/32404)

#### Linux Instances
[Linux instance: Unable to login due to high CPU and memory usage rates](https://intl.cloud.tencent.com/document/product/213/32387)

## Subsequent Operations

If you still cannot log in remotely after following the preceding steps, you can save the related logs and self-check results and [Submit a Ticket](https://console.cloud.tencent.com/workorder/category).
