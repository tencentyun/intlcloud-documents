This document describes the possible causes of Windows instance login failures and their troubleshooting methods. You can follow the instructions to identify the cause of your problem and learn how to fix it.

## Possible Causes
Failure to log into a Windows instance may be the result of:
- [Password issues](#CryptographicProblem)
- [High bandwidth utilization](#BandwidthUtilization)
- [High server load](#HighServerLoad)
- [Improper remote port configuration](#RemotePortConfiguration)
- [Improper security group rules](#SafetyGroupRule)
- [Exception caused by the firewall or security software](#LoginSecuritySoftware)
- [Authentication error during access through the remote desktop](#AuthenticationError)

If you cannot troubleshoot with a diagnosis tool, we recommend that you [log in through VNC](#VNC) and follow the instructions on the CVM.

<span id="TroubleshootingIdeas"></span>
## Troubleshooting

<span id="VNC"></span>
### Logging in through VNC

If you cannot log in to a Windows instance through RDP or remote access software, you can log in through VNC instead, which helps you identify the cause of the problem.
1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/index).
2. On the instance management page, select the instance to access and click **Log In**, as shown in the following figure:
![](https://main.qcloudimg.com/raw/d9ccf04da21f4ac86d624742c87d5628.png)
3. In the **Log into Windows instance** window that appears, select **Alternative methods (VNC)** and click **Log In Now**.
> If you forget the password for the instance, you can reset it in the console. For more information, see [Resetting the Instance Password](https://intl.cloud.tencent.com/document/product/213/16566).
>
4. In the login window that appears, select **Send CtrlAltDel** in the upper-left corner, and press **Ctrl-Alt-Delete** to open the system login window, as shown in the following figure:
![](https://main.qcloudimg.com/raw/5064251ea86085326e86884a1c13ef6b.png)


<span id="CryptographicProblem"></span>
### Password issues

**Problem**: the login attempt failed because you forgot the password, entered an incorrect password, or failed to reset your password.
**Procedure**: reset the password for this instance in the [CVM Console](https://console.cloud.tencent.com/cvm/index) and restart the instance. For more information, see [Resetting Instance Password](https://intl.cloud.tencent.com/document/product/213/16566).

<span id="BandwidthUtilization"></span>
### High bandwidth utilization

**Procedure**:
1. Log in to the instance by using [VNC login](#VNC).
2. Check the bandwidth utilization of the instance and troubleshoot accordingly. For details, see [Login Failure Due to High Bandwidth Occupation](https://intl.cloud.tencent.com/document/product/213/32542).

<span id="HighServerLoad"></span>
### High server load

**Problem**: Cloud Monitor shows a high load on the server’s CPU, and the system cannot be accessed remotely or access is slow.
**Possible cause**: viruses, trojans, third-party antivirus software, application exceptions, driver exceptions, and automatic updates of software on the backend may lead to high CPU utilization, causing CVM login failures or slow access.
**Procedure**:
1. Log in to the instance by using [VNC login](#VNC).
2. In **Task Manager**, locate the process that causes the high load. For details, see [Failed to Log In to a Windows CVM Due to High CPU and Memory Usage](https://intl.cloud.tencent.com/document/product/213/32405).

<span id="RemotePortConfiguration"></span>
### Improper remote port configuration

**Problem**: the remote access attempt to an instance failed, the remote access port is not the default port or has been modified, or port 3389 is not open.
**Diagnosis**: ping the public IP address of the instance to check network connectivity and run telnet to check whether the port is open.
**Procedure**: See [Remote Login Failure Due to Port Issues](https://intl.cloud.tencent.com/document/product/213/32540) for the detailed procedure.

<span id="SafetyGroupRule"></span>
### Improper security group rules

**Procedure**: Troubleshoot with the [security group (port) verification tool](https://console.cloud.tencent.com/vpc/helper).
> For a remotely logged-in Windows instance, you need to open port 3389.
> 
![](https://main.qcloudimg.com/raw/27b5aa974a2263719574dfc3bb7c0c6d.png)
If the problem is caused by a port issue of the security group, you can use the **Open all ports** function to open all ports.
![](https://main.qcloudimg.com/raw/bd91ec53dfd0df6bd1127a7f4f9db35c.png)
To define a custom rule for the security group, see [Adding Rules for a Security Group](https://intl.cloud.tencent.com/document/product/213/34272).


<span id="LoginSecuritySoftware"></span>
### Exception caused by the firewall or security software

**Problem**: the login attempt failed due to the CVM firewall or security software.
**Diagnosis**: log in to a Windows instance through VNC to check whether the firewall is enabled and whether security software such as 360 Total Security or security dongles are installed on the server.
> This operation involves shutting down the CVM firewall. To perform it, check that you have the corresponding permission.
>
**Procedure**: shut down the firewall or the installed security software, and then try to access remotely again. For example, you can shut down the firewall of Windows Server 2016 as follows:
1. Log in to the instance by using [VNC login](#VNC).
2. On the desktop of the operating system, click <img src="https://main.qcloudimg.com/raw/6e36af2ceb4604b81de13cb42f30e859.png" style="margin: 0;"> and choose **Control Panel**.
3. In the **Control Panel** window, click **Windows Firewall**.
4. In the **Windows Firewall** window, click **Enable or Disable Windows Firewall** on the left to open **Custom Settings**.
5. Set **Private Network Settings** and **Public Network Settings** to **Disable Windows Firewall**, and then click **OK**.
6. Restart the instance and try to access remotely again.

<span id="AuthenticationError"></span>
### Authentication error during access through the remote desktop

**Problem**: when you tried to log in to a Windows instance through the remote desktop, the prompt stating "Authentication error. Invalid flag is provided to the function." or "Authentication error. The required function is not supported." appears.
**Possible cause**: Microsoft released a security update in March 2018. This update fixes a remote code execution vulnerability in the Credential Security Supporting Program (CredSSP) by correcting how CredSSP validates requests during the authentication process. Both the client and server need to be updated or the preceding error may occur.
**Procedure**: install the security update (recommended). For details, see [An Authentication Error Occurred when You Tried to Log In to a Windows Instance Remotely](https://intl.cloud.tencent.com/document/product/213/32421).

## Other Solutions
After trying the preceding methods, if you still cannot log in to the Window instance, please save your self-diagnosis results and [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.
