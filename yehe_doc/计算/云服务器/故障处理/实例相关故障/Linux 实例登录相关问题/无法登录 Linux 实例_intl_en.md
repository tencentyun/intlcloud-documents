
This document describes possible causes of Linux instance login failures and troubleshooting methods, helping you detect, locate and resolve problems.


## Troubleshooting the Issue
### Using the Diagnosis Tool
Tencent Cloud provides a diagnosis tool to help you determine whether the problem is due to common bandwidth, firewall, or security group configurations issues. More than 70% of the problems can be located by this tool. You can locate problems that result in login failures based on the detected causes.
1. Click [Self-diagnose](https://console.cloud.tencent.com/workorder/check) to open the self-diagnosis tool.
2. Select the target CVM instance as prompted and click **Start Detection**.


### Using TAT to send commands
You can use TAT to send commands to an instance for troubleshooting and problem locating. The directions are as follows:
1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/index) and click the target instance ID in the instance list.
2. On the instance details page, select the **Run Commands** tab and click **Execute command**.
3. In the **Execute command** pop-up window, select a command as needed. Click **Execute command** and view the result.
For example, enter `df -TH` and click **Execute command** to view the result of an instance without logging in to it.
For more information, see [TencentCloud Automation Tools](https://intl.cloud.tencent.com/document/product/1147).


<dx-alert infotype="explain" title="">
If you cannot troubleshoot with the diagnosis tool, we recommend you [log in to the CVM instance via VNC](#VNC) and follow the instructions.
</dx-alert>




## Possible Cause
Common login failure reasons:
- [SSH key problems](#UseSSHLogin)
- [Password issues](#CryptographicProblem)
- [High bandwidth utilization](#BandwidthUtilization)
- [High server load](#HighServerLoad)
- [Improper security group rules](#SafetyGroupRule)

## Troubleshooting
### Logging in via VNC[](id:VNC)

If you cannot log in to the Linux instance by using Orcaterm or remote login software, you can try log in with VNC for troubleshooting.
1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/index).
2. On the **Instances** page, select the target instance and click **Log in**.
![](https://main.qcloudimg.com/raw/a4cc736f2dc7f13bf39756b8e39532d4.png)
3. In the **Standard Login | Linux Instance** window that pops up, select **Login via VNC**.
<dx-alert infotype="explain" title="">
 If you forgot the password for the instance, you can reset it in the console. For more information, see [Resetting Instance Password](https://intl.cloud.tencent.com/document/product/213/16566).
</dx-alert>
4. Enter the username and password to login.


### Login failure due to SSH issue[](id:UseSSHLogin)
**Problem**: During [login to a Linux instance using SSH](https://intl.cloud.tencent.com/document/product/213/32501), a message appears indicating that the connection is unavailable or failed.
**Steps**: See [Unable to Use the SSH Method to Log in to a Linux Instance](https://intl.cloud.tencent.com/document/product/213/32486) to perform troubleshooting.


### Login failure due to password issue[](id:CryptographicProblem)
**Problem**: The login attempt failed because you forgot the password, entered an incorrect password, or failed to reset your password.
**Solution**: Reset the password for this instance in the [CVM console](https://console.cloud.tencent.com/cvm/index) and restart the instance.
**Procedure**: See [Resetting Instance Password](https://intl.cloud.tencent.com/document/product/213/16566) for the detailed procedure.


### High bandwidth utilization[](id:BandwidthUtilization)
**Problem**: The self-diagnosis tool shows that bandwidth utilization is too high.
**Procedure**:
1. Log in to the instance by using [VNC login](#VNC).
2. Check the bandwidth utilization of the instance and perform troubleshooting accordingly. For details, see [Login Failure Due to High Bandwidth Occupation](https://intl.cloud.tencent.com/document/product/213/32542).


### High instance load[](id:HighServerLoad)
**Problem**: The self-diagnosis tool or Tencent Cloud Observability Platform shows that server CPU workload is too high, and the system is unable to perform remote connection or access is slow.
**Possible cause**: Viruses, trojans, third-party antivirus software, application exceptions, driver exceptions, and automatic updates of software on the backend may lead to high CPU utilization, causing CVM login failures or slow access.
**Procedure**:
1. Log in to the instance by using [VNC login](#VNC).
2. In **Task manager**, find the process with a high load. For more information, see [Failing to log in to a Linux CVM due to high CPU and memory usage](https://intl.cloud.tencent.com/document/product/213/32387).


### Improper security group rules[](id:SafetyGroupRule)
**Problems**: The self-diagnosis tool shows that the security group rule configuration is improper, leading to login failures.
**Procedure**: Troubleshoot with the [security group (port) verification tool](https://console.cloud.tencent.com/vpc/helper).
![](https://main.qcloudimg.com/raw/278c7f0abd9b7224d32fa5402554544a.png)
If the problem is caused by a port issue of the security group, you can use the **Open all ports** feature to open all ports.
![](https://main.qcloudimg.com/raw/e4a40dafcc9607ce18ee7001129d9655.png)
To define a custom rule for the security group, see [Adding Security Group Rules](https://intl.cloud.tencent.com/document/product/213/34272).



## Other Solutions
If you still cannot connect to the Linux instance, save your self-diagnosis results and [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category) for assistance.
