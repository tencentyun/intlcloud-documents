
This document describes how to troubleshoot the problem where you are unable to connect remotely to a CVM due to security group configuration issues.

## Diagnostic Tool

You can use [Port Verification](https://console.cloud.tencent.com/vpc/helper) to check whether the problem is caused by security group configurations.
1. Log in to the [Port Verification](https://console.cloud.tencent.com/vpc/helper).
2. In the **Port Verification** page, select the instance to check and click **Quick Check**. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/a792a1692e0a21b3f9dfe111d4b86789.png)
If the check shows that the instance has ports that are not open, you can select **Open all ports** to open all commonly used ports of the CVM to the Internet, and try to log in remotely again.

<img src="https://main.qcloudimg.com/raw/a743739b5885874c15a6b5c7869f5acd.png" height="400" width="420">


## Modifying security group configurations

If you do not want to use **Open all ports** to open all commonly used ports of the CVM to the Internet, or you need to customize the remote login port, you can use custom configuration of the inbound and outbound rules of the security group to resolve remote login failures. For more information, see [Modifying Security Group Rules](https://intl.cloud.tencent.com/document/product/213/34825).
