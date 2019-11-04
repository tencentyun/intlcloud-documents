This document introduces how to determine the reason of the problems where being unable to log into Linux instance, and lists the common reason.

## Common Reasons
The primary reasons for inability to connect to a Linux instance include:
- [SSH key problems](#UseSSHLogin)
- [Password problems](#CryptographicProblem)
- [Bandwidth utilization too high](#BandwidthUtilization)
- [Server workload too high](#HighServerLoad)
- [Remote port configuration exception](#RemotePortConfiguration)
- [Incorrect security group rules](#SafetyGroupRule)

## Troubleshooting
### Logging in Through VNC
<span id="VNC"></span>
If you cannot use the standard method (Webshell) or remote login software to log into a Linux instance, you can use the Tencent Cloud VNC method to log in, to help you locate the cause of the fault.
1. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/index).
2. In the instance management page, select the instance to be logged in to and click **Log In**. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/a4cc736f2dc7f13bf39756b8e39532d4.png)
3. In the **Log Into Linux Instance** window that pops up, select **Other Methods (VNC)**, and click **Log In Now**.
>? In the login process, if you forget the password, you can reset the password for this instance in the console. For more information, see [Resetting an Instance Password](http://intl.cloud.tencent.com/document/product/213/16566).
>
4. Enter the username and password in the dialog box that pops up to complete the login process.

<span id="UseSSHLogin"></span>
### SSH Problem Causing Inability to Log in
**Problem**: [When using SSH to log in to a Linux instance], there is a prompt that it is unable to connect, or that connection failed.
**Troubleshooting**: Refer to [Unable to use the SSH method to log in to a Linux instance]

<span id="CryptographicProblem"></span>
### Unable to Login Due to Password Problems
**Problem**: The password is entered incorrectly, the password is forgotten, or the password reset failed leading to unsuccessful log in.
**Troubleshooting**: Reset the password for this instance in the [Tencent Cloud Console](https://console.cloud.tencent.com/cvm/index), and restart the instance.
**Procedure**: For information about how to reset the password of an instance, see [Resetting the Password of an Instance](http://intl.cloud.tencent.com/document/product/213/16566).

<span id="BandwidthUtilization"></span>
### Bandwidth Utilization Too High
**Problem**: After diagnosing with the self-diagnosis tool, it prompts that the problem occurs because the bandwidth utilization is too high.
**Steps**:
1. Using [VNC Login](#VNC), log in to the instance.
2. Refer to [Login Failure due to High Bandwidth Usage] for viewing the bandwidth usage of the instance and how to fix the problem.

<span id="HighServerLoad"></span>
### Server Workload Too High
**Problem**: Using the self-check tool or Cloud Monitor, you find that the server CPU load is too high, causing the system to be unable to perform remote connection or access to have a lot of stutter.
**Possible Reasons**: Viruses and Trojans, third-party anti-virus software, application exceptions, driver exceptions, and software backend automatic updates, can all lead the CPU usage rate to be high, causing an inability to log into the CVM or slow access issues.
**Procedure**:
1. Using [VNC Login](#VNC), log in to the instance.
2. Refer to [Linux Instance: High CPU and Memory Usage Rate Causing Login Failure]. In **Task Manager**, locate the high load process.


<span id="RemotePortConfiguration"></span>
### Remote Port Configuration Exception
**Problem Description**: The remote port cannot connect, remote access port is not the default port, has been modified, or port 22 is not open.
**Location**: Whether the public IP of the instance can be pinged, use the `telnet` command to check whether the port is open.
**Procedure**: For specific information about this operation, see [Unable to Login Due to Port Problems].

<span id="SafetyGroupRule"></span>
### Improper Security Group Rules
**Problem Description**: By using the Diagnosis tool, you discover that the security group rule configuration is improper, leading to an inability to log in.
**Procedure**: Check by using the [Port Verification Tool](https://console.cloud.tencent.com/vpc/helper).
![](https://main.qcloudimg.com/raw/278c7f0abd9b7224d32fa5402554544a.png)
If the problem is caused by security group configurations, you can use the **Open All Ports** to open all ports.
![](https://main.qcloudimg.com/raw/e4a40dafcc9607ce18ee7001129d9655.png)
If you need to customize  security group rules, see [Security Group Operations](http://intl.cloud.tencent.com/document/product/213/18197).



## Other Solutions
After the preceding troubleshooting, if you are still unable to log in to the Linux instance, please save your self-diagnosis results, and [Submit a Ticket](https://console.cloud.tencent.com/workorder/category).
