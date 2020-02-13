This document describes possible causes of Linux instance login failures and troubleshooting methods, helping you detect, locate and resolve problems.

## Possible Causes
The primary causes of Linux instance login failures include:
- [SSH key problems](#UseSSHLogin)
- [Password Problems](#CryptographicProblem)
- [Bandwidth utilization too high](#BandwidthUtilization)
- [Server workload too high](#HighServerLoad)
- [Remote port configuration exception](#RemotePortConfiguration)
- [Incorrect security group rules](#SafetyGroupRule)

If your problem cannot be checked using the self-diagnose tool, we recommend you [log in to the CVM via VNC](#VNC) and troubleshoot step by step.

## Troubleshooting
### Logging in via VNC
<span id="VNC"></span>
If you cannot use the standard method (Webshell) or remote login software to log into a Linux instance, you can use Tencent Cloud VNC to log in and locate the problem causes.
1. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/index).
2. In the instance management page, select the instance to be logged in to and click **Log In**. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/a4cc736f2dc7f13bf39756b8e39532d4.png)
3. In the **Log into Linux instance** window that pops up, select **Alternative login methods (VNC)**, and click **Log In Now**.
> During login, if you forget the password of this instance, you can reset it in the console. For more information, see [Reset Instance Password](http://intl.cloud.tencent.com/document/product/213/16566).
>
4. Enter the username and password in the dialog box that pops up to complete the login process.

<span id="UseSSHLogin"></span>
### Login failures due to SSH problems
**Problem**: [When using SSH to log in to a Linux instance](https://intl.cloud.tencent.com/document/product/213/32501), the prompt says unable to connect or connection failed.
**Troubleshooting**: Refer to [Unable to use the SSH method to log in to a Linux instance](https://intl.cloud.tencent.com/document/product/213/32486) for troubleshooting.

<span id="CryptographicProblem"></span>
### Login failures due to password problems
**Problem**: You forget the password, enter it incorrectly or password reset failed resulting in login failures.
**Troubleshooting**: Reset the password for this instance in the [Tencent Cloud Console](https://console.cloud.tencent.com/cvm/index), and restart the instance.
**Steps**: For information about how to reset the password of an instance, see [Reset Instance Password](http://intl.cloud.tencent.com/document/product/213/16566).

<span id="BandwidthUtilization"></span>
### Bandwidth utilization too high
**Problem**: The self-diagnosis tool shows that bandwidth utilization is too high.
**Steps**:
1. Log in to the instance via [VNC Login](#VNC).
2. Refer to [Login failure due to high bandwidth usage](https://intl.cloud.tencent.com/document/product/213/32542) to view the bandwidth usage of the instance and how to fix the problem.

<span id="HighServerLoad"></span>
### Server workload too high
**Problem**: The self-diagnosis tool or Cloud Monitor shows that server CPU workload is too high, and the system is unable to perform remote connection or access is slow.
**Possible Causes**: Viruses, Trojans, third-party anti-virus software, application exceptions, driver exceptions, and software backend automatic updates may lead to high CPU usage rate, causing CVM login failures or slow access.
**Steps**:
1. Log in to the instance via [VNC Login](#VNC).
2. Refer to [Linux instance: login failure due to high CPU and memory usage rate](https://intl.cloud.tencent.com/document/product/213/32387). In **Task Manager**, locate the high load process.


<span id="RemotePortConfiguration"></span>
### Remote port configuration exception
**Problems**: The remote port cannot connect, remote access port is not the default port or has been modified, or port 22 is not open.
**Diagnosis**: Whether the public IP of the instance can be pinged, use the `telnet` command to check whether the port is open.
**Solutions**: For specific information about this operation, see [Remote connect failures due to port problems](https://intl.cloud.tencent.com/document/product/213/32540).

<span id="SafetyGroupRule"></span>
### Improper security group rules
**Problems**: The self-diagnosis tool shows that the security group rule configuration is improper, leading to login failures.
**Steps**: Check by using the [port verification tool](https://console.cloud.tencent.com/vpc/helper).
![](https://main.qcloudimg.com/raw/278c7f0abd9b7224d32fa5402554544a.png)
If the problem is caused by security group configurations, you can use the **Open All Tools** to open all ports.
![](https://main.qcloudimg.com/raw/e4a40dafcc9607ce18ee7001129d9655.png)
If you need to customize security group rules, see [Security Group Operations](http://intl.cloud.tencent.com/document/product/213/18197) for reconfiguration.



## Other Solutions
If you still cannot log into the Linux instance using above-mentioned troubleshooting methods, please save your self-diagnosis results and [Submit Ticket](https://console.cloud.tencent.com/workorder/category).
