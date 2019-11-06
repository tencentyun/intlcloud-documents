
This document introduces how to troubleshoot the problem where unable to connect remotely to a CVM due to security group configuration issues.

## Diagnostic Tool

You can use the [Port Verification](https://console.cloud.tencent.com/vpc/helper) to check whether the problem is caused by security group configurations.
1. Log in to the [Port Verification](https://console.cloud.tencent.com/vpc/helper).
2. In the **Port Verification** page, select the instance to check and click **Quick Check**. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/a792a1692e0a21b3f9dfe111d4b86789.png)
If the check shows that the instance has ports that are not open to the Internet, you can use the **Open All Ports** function to open all the commonly used ports of the CVM to the Internet, and then try to remotely connect again.
<img src="https://main.qcloudimg.com/raw/a743739b5885874c15a6b5c7869f5acd.png" height="400" width="420">


## Modifying Security Group Configurations

If you do not want to use the **Open All Ports** function to open all the commonly used ports of the CVM to the Internet, or you need a custom remote login port, you can also use the custom configuration of the inbound and outbound rules of the security group to resolve the inability to log in issue. For more information, see [Modifying Security Group Rules](https://cloud.tencent.com/document/product/213/18197#.E4.BF.AE.E6.94.B9.E5.AE.89.E5.85.A8.E7.BB.84.E8.A7.84.E5.88.99).
