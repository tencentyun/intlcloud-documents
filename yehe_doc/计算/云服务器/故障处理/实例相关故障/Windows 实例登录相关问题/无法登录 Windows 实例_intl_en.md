

This document describes the possible causes of Windows instance login failures and their troubleshooting methods. 

## Possible Cause
Common login failure reasons:
- [Incorrect password](#CryptographicProblem)
- [High bandwidth utilization](#BandwidthUtilization)
- [High server load](#HighServerLoad)
- [Improper remote port configuration](#RemotePortConfiguration)
- [Improper security group rules](#SafetyGroupRule)
- [Exception caused by the firewall or security software](#LoginSecuritySoftware)
- [Authentication error in access through remote desktop](#AuthenticationError)

## Using Self-Diagnosis Tool

Tencent Cloud provides a self-diagnosis tool to help you determine whether the failure is caused by common problems with the bandwidth, firewall, and security group configurations. 70% of faults can be located with this tool. You can locate the faults that may result in the login failure based on the detected causes.
1. Click [Self-diagnose](https://console.cloud.tencent.com/workorder/check) to open the self-diagnosis tool.
2. Select the target CVM instance as prompted and click **Start Detection**.

If you cannot troubleshoot with the diagnosis tool, we recommend you [log in to the CVM instance via VNC](#VNC) and follow the instructions.


## Troubleshooting[](id:TroubleshootingIdeas)


### Logging in via VNC[](id:VNC)

If you cannot log in to a Windows instance through RDP or remote access software, you can log in through VNC for troubleshooting.
1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/index).
2. On the **Instances** page, select the target instance and click **Log in**.
![](https://main.qcloudimg.com/raw/d9ccf04da21f4ac86d624742c87d5628.png)
3. In the **Standard Login | Windows Instance** pop-up window, click **Login via VNC**.
<dx-alert infotype="explain" title="">
If you forgot the password for the instance, you can reset it in the console. For more information, see [Resetting Instance Password](https://intl.cloud.tencent.com/document/product/213/16566).
</dx-alert>
4. In the login pop-up window, click **Ctrl-Alt-Delete** from the top left list.
![](https://main.qcloudimg.com/raw/5064251ea86085326e86884a1c13ef6b.png)



### Login failure due to password issue[](id:CryptographicProblem)

**Problem**: The login attempt failed because you forgot the password, entered an incorrect password, or failed to reset your password.
**Solution**: Reset the password for this instance in the [CVM console](https://console.cloud.tencent.com/cvm/index) and restart the instance. For more information, see [Resetting Instance Password](https://intl.cloud.tencent.com/document/product/213/16566).



### High bandwidth utilization[](id:BandwidthUtilization)

**Problem**: The self-diagnosis tool shows that bandwidth utilization is too high.
**Procedure**:
1. Log in to the instance by using [VNC login](#VNC).
2. Check the bandwidth utilization of the instance and perform troubleshooting accordingly. For details, see [Login Failure Due to High Bandwidth Occupation](https://intl.cloud.tencent.com/document/product/213/32542).


### High server load[](id:HighServerLoad)

**Problem**: The self-diagnosis tool or Tencent Cloud Observability Platform shows that server CPU workload is too high, and the system is unable to perform remote connection or access is slow.
**Possible cause**: Viruses, trojans, third-party antivirus software, application exceptions, driver exceptions, and automatic updates of software on the backend may lead to high CPU utilization.
**Procedure**:
1. Log in to the instance by using [VNC login](#VNC).
2. In **Task manager**, find the process with high load. For details, see [Failed to log in to a Windows CVM due to high CPU and memory usage](https://intl.cloud.tencent.com/document/product/213/32405).


### Improper remote port configuration[](id:RemotePortConfiguration)

**Problem**: Failed to access the instance remotely, the remote access port is not the default port or has been modified, or port 3389 is not open.
**Diagnosis**: Ping the public IP address of the instance to check network connectivity and run telnet to check whether the port is open.
**Procedure**: See [Remote Login Failure Due to Port Issues](https://intl.cloud.tencent.com/document/product/213/32540) for the detailed procedure.


### Improper security group rules[](id:SafetyGroupRule)

**Problems**: Security group rule configuration is improper, leading to login failures.
**Procedure**: Troubleshoot with the [Port Verification](https://console.cloud.tencent.com/vpc/helper) feature on the VPC console.
<dx-alert infotype="notice" title="">
Open 3389 must be open for remote login.
</dx-alert>
<img src="https://main.qcloudimg.com/raw/bd91ec53dfd0df6bd1127a7f4f9db35c.png"/><br>
To define a custom rule for the security group, see <a href="https://intl.cloud.tencent.com/document/product/213/34272">Adding Security Group Rules</a>.



### Login failure due to firewall or security software[](id:LoginSecuritySoftware)

**Problem**: The login attempt failed due to the CVM firewall or security software.
**Diagnosis**: Log in to a Windows instance through VNC to check whether the login is blocked by the firewall policies or security software installed on the server.
<dx-alert infotype="notice" title="">
This operation involves shutting down the CVM firewall. To perform it, check whether you have the corresponding permission.
</dx-alert>

**Procedure**: Shut down the firewall or the installed security software, and then try to access remotely again. For example, you can shut down the firewall of Windows Server 2016 as follows:
1. Log in to the instance by using [VNC login](#VNC).
2. On the desktop, click <img src="https://main.qcloudimg.com/raw/6e36af2ceb4604b81de13cb42f30e859.png" style="margin:-3px 0px;"> and select **Control Panel**.
3. Click **Windows Defender Firewall**.
4. In the **Windows Defender Firewall** window, click **Turn Windows Firewall on or off** on the left to open **Customize Settings**.
5. Set **Private network settings** and **Public network settings** to **Turn off Windows Firewall** and click **OK**.
6. Restart the instance and try to access remotely again.


### Identity verification error in access through remote desktop[](id:AuthenticationError)

**Problem**: When you tried to log in to a Windows instance through the remote desktop, the prompt stating "Authentication error. Invalid flag is provided to the function." or "Authentication error. The required function is not supported." appears.
**Possible cause**: Microsoft released a security update in March 2018. This update fixes a remote code execution vulnerability in the Credential Security Supporting Program (CredSSP) by correcting how CredSSP validates requests during the authentication process. Both the client and server need to be updated or the preceding error may occur.
**Procedure**: Install the security update (recommended). For details, see [An Authentication Error Occurred when You Tried to Log In to a Windows Instance Remotely](https://intl.cloud.tencent.com/document/product/213/32421).

## Other Solutions
If you still cannot connect to the Windows instance, and [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category) for assistance.
