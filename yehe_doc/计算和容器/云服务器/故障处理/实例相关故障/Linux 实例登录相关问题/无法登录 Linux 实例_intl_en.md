This document describes how to troubleshoot problems when a Linux instance cannot be connected. It also analyzes the possible causes for the connection failure and provides guidance on troubleshooting, locating, and solving the problem.


## Troubleshooting the Issue
### Using the diagnosis tool
Tencent Cloud provides a diagnosis tool to help you determine whether the problem is due to common bandwidth, firewall, or security group configurations issues. More than 70% of the problems can be located by this tool. You can locate problems that result in login failures based on the detected causes.
1. Click [Self-diagnose](https://console.intl.cloud.tencent.com/workorder/check) to open the self-diagnosis tool.
2. Select the CVM to be diagnosed as prompted and click **Start Detection**.


## Common Causes
The main causes for failing to log in to a Linux instance include the following:
- [SSH key problems](#UseSSHLogin)
- [Password issues](#CryptographicProblem)
- [High bandwidth utilization](#BandwidthUtilization)
- [High server load](#HighServerLoad)
- [Improper security group rules](#SafetyGroupRule)

## Troubleshooting
### Logging in through VNC[](id:VNC)

If you cannot use the standard method (Webshell) or remote login software to log in to a Linux instance, you can use Tencent Cloud VNC to log in and locate the problem causes.
1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/index).
2. On the instance management page, locate the instance you want to access and click **Log In**, as shown in the following figure:
![](https://main.qcloudimg.com/raw/a4cc736f2dc7f13bf39756b8e39532d4.png)
3. In the **Standard Login | Linux Instance** window that pops up, select **Login with VNC**.
<dx-alert infotype="explain" title="">
 If you forget the password for the instance, you can reset it in the console. For more information, see [Resetting Instance Password](https://intl.cloud.tencent.com/document/product/213/16566).
</dx-alert>
4. Enter the username and password to complete the login process.


### SSH key problems[](id:UseSSHLogin)
**Problem**: during [login to a Linux instance using SSH](https://intl.cloud.tencent.com/document/product/213/32501), a message appears indicating that the connection is unavailable or failed.
**Steps**: see [Unable to Use the SSH Method to Log in to a Linux Instance](https://intl.cloud.tencent.com/document/product/213/32486) to perform troubleshooting.

<span id="CryptographicProblem"></span>
### Password issues
**Problem**: the login attempt failed because you forgot the password, entered an incorrect password, or failed to reset your password.
**Solution**: reset the password for this instance in the [CVM console](https://console.cloud.tencent.com/cvm/index) and restart the instance.
**Procedure**: see [Resetting Instance Password](https://intl.cloud.tencent.com/document/product/213/16566) for the detailed procedure.


### High bandwidth utilization[](id:BandwidthUtilization)
**Problem**: the self-diagnosis tool shows that bandwidth utilization is too high.
**Procedure**:
1. Log in to the instance by using [VNC login](#VNC).
2. Check the bandwidth utilization of the instance and perform troubleshooting accordingly. For details, see [Login Failure Due to High Bandwidth Occupation](https://intl.cloud.tencent.com/document/product/213/32542).


### High server load[](id:HighServerLoad)
**Problem**: The self-diagnosis tool or Cloud Monitor shows that server CPU workload is too high, and the system is unable to perform remote connection or access is slow.
**Possible cause**: viruses, trojans, third-party antivirus software, application exceptions, driver exceptions, and automatic updates of software on the backend may lead to high CPU utilization, causing CVM login failures or slow access.
**Procedure**:
1. Log in to the instance by using [VNC login](#VNC).
2. In **Task manager**, find the process with a high load. For details, see [Failed to Log in to a Linux CVM Due to High CPU and Memory Usage](https://intl.cloud.tencent.com/document/product/213/32387).


### Improper security group rules[](id:SafetyGroupRule)
**Problems**: The self-diagnosis tool shows that the security group rule configuration is improper, leading to login failures.
**Procedure**: Troubleshoot with the [security group (port) verification tool](https://console.cloud.tencent.com/vpc/helper).
![](https://main.qcloudimg.com/raw/278c7f0abd9b7224d32fa5402554544a.png)
If the problem is caused by a port issue of the security group, you can use the **Open all ports** function to open all ports.
![](https://main.qcloudimg.com/raw/e4a40dafcc9607ce18ee7001129d9655.png)
To define a custom rule for the security group, see [Adding Security Group Rules](https://intl.cloud.tencent.com/document/product/213/34272).



## Other Solutions
If you still cannot log in to the Linux instance using the preceding troubleshooting methods, save your self-diagnosis results and [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category).
) 进行反馈。
