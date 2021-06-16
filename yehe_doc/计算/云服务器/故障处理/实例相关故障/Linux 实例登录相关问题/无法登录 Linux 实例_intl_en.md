This document describes the possible causes of Linux instance login failures and troubleshooting methods, helping you detect, locate, and resolve problems.

## Possible Causes
The primary causes of Linux instance login failures include:
- [SSH key problems](#UseSSHLogin)
- [Password problems](#CryptographicProblem)
- [Excessive bandwidth utilization](#BandwidthUtilization)
- [High server load](#HighServerLoad)
- [Incorrect security group rules](#SafetyGroupRule)


If you cannot check your problem by using the self-diagnose tool, we recommend that you [log in to the CVM through VNC](#VNC) and troubleshoot step by step.

## Troubleshooting
### Logging in by using VNC
<span id="VNC"></span>
If you cannot use the standard method (Webshell) or remote login software to log in to a Linux instance, you can use Tencent Cloud VNC to log in and locate the problem causes.
1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/index).
2. On the instance management page, select the instance to access and click **Log In**, as shown in the following figure:
![](https://main.qcloudimg.com/raw/a4cc736f2dc7f13bf39756b8e39532d4.png)
3. In the "Log in to Linux Instance" window that appears, select **Alternative login methods (VNC)** and click **Log In Now**.
> During login, if you forget the password of this instance, you can reset it in the console. For more information, see [Resetting the Instance Password](http://intl.cloud.tencent.com/document/product/213/16566).
>
4. Enter the username and password in the dialog box that appears to complete the login process.

<span id="UseSSHLogin"></span>
### SSH problems
**Problem**: during [login to a Linux instance by using SSH](https://intl.cloud.tencent.com/document/product/213/32501), a message indicating that the connection is unavailable or failed appears.
**Steps**: see [Unable to Log In to a Linux Instance by Using SSH](https://intl.cloud.tencent.com/document/product/213/32486) for troubleshooting.

<span id="CryptographicProblem"></span>
### Password problems
**Problem**: unable to log in because you forget the password, enter it incorrectly, or fail to reset it.
**Solution**: reset the password of this instance in the [Tencent Cloud console](https://console.cloud.tencent.com/cvm/index), and restart the instance.
**Steps**: for information on how to reset the password of an instance, see [Resetting the Instance Password](http://intl.cloud.tencent.com/document/product/213/16566).

<span id="BandwidthUtilization"></span>
### Excessive bandwidth utilization
**Problem**: the self-diagnosis tool shows that bandwidth utilization is too high.
**Steps**:
1. Log in to the instance by using [VNC](#VNC).
2. Check the bandwidth utilization of the instance and troubleshoot accordingly. For details, see [Unable to Log In Due to High Bandwidth Utilization](https://intl.cloud.tencent.com/document/product/213/32542).

<span id="HighServerLoad"></span>
### High server load
**Problem**: Cloud Monitor shows that load of the server CPU is high, and the system cannot be accessed remotely or access is slow.
**Possible Causes**: viruses, trojans, third-party anti-virus software, application exceptions, driver exceptions, and software backend automatic updates may lead to high CPU usage, causing CVM login failures or slow access.
**Steps**:
1. Log in to the instance by using [VNC](#VNC).
2. In "Task manager", find the process with a high load. For details, see [Unable to Log In Due to High CPU and Memory Usage](https://intl.cloud.tencent.com/document/product/213/32387).

<span id="SafetyGroupRule"></span>
### Incorrect security group rules
**Problem**: unable to log in due to incorrect security group rules.
**Steps**: troubleshoot by using the [port verification tool for security groups](https://console.cloud.tencent.com/vpc/helper).
![](https://main.qcloudimg.com/raw/278c7f0abd9b7224d32fa5402554544a.png)
If the problem is caused by the incorrect security group port configuration, you can use **Open All Tools** to open all ports.
![](https://main.qcloudimg.com/raw/e4a40dafcc9607ce18ee7001129d9655.png)
If you need to define a custom rule for the security group, see [Adding Rules to Security Groups](https://intl.cloud.tencent.com/document/product/213/34272) for information on how to reconfigure security group rules.



## Other Solutions
If you still cannot log in to the Linux instance after trying the preceding troubleshooting methods, save your self-diagnosis results and [submit a ticket](https://console.cloud.tencent.com/workorder/category).
