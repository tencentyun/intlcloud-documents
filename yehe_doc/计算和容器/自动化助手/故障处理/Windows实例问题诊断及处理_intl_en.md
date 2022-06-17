## Issue Description
After running a TAT check on a Windows instance, you may see the following issues.



## Check Item Categories
<table>
<tr>
<th>Category</th>
<th>Check Items</th>
</tr>
<tr>
<td rowspan=6>OS Environment</td>
<td>
<a href="#OSStatusCheck">Windows OS status</a>
</td>
</tr>
<tr>
<td>
<a href="#memoryLimit">Memory limit</a>
</td>
</tr>
<tr>
<td>
<a href="#CPULimit">CPU limit</a>
</td>
</tr>
<tr>
<td>
<a href="#handleLeak">Handle leak</a>
</td>
</tr>
<tr>
<td>
<a href="#BruteForceAttack">System brute force and attacks</a>
</td>
</tr>
<tr>
<td>
<a href="#environmentVariable">System environment variables</a>
</td>
</tr>
<tr>
<td rowspan=5>System Resource Usage</td>
<td>
<a href="#highMemoryUsage">High memory usage</a>
</td>
</tr>
<tr>
<td>
<a href="#highVirtualMemoryUsage">High virtual memory usage</a>
</td>
</tr>
<tr>
<td>
<a href="#totalCPUusagehigh">High total CPU usage</a>
</td>
</tr>
<tr>
<td>
<a href="#CPUusagehigh">High usage of a single CPU</a>
</td>
</tr>
<tr>
<td>
<a href="#ntfsFileUsageHigh">Large space occupied by metafiles in the NTFS file system</a>
</td>
</tr>
<tr>
<td rowspan=8>Remote Connection</td>
<td>
<a href="#remoteDesktopCheck">Remote Desktop Services (RDS) status</a>
</td>
</tr>
<tr>
<td>
<a href="#remoteDesktopPortCheck">RDS port</a>
</td>
</tr>
<tr>
<td>
<a href="#RDPCconnectionCheck">RDP-TCP connection</a>
</td>
</tr>
<tr>
<td>
<a href="#allowRemoteDesktopConnection">Whether RDS connection is allowed</a>
</td>
</tr>
<tr>
<td>
<a href="#signedCertificateExpiration">RDP self-signed certificate expiration time</a>
</td>
</tr>
<tr>
<td>
<a href="#desktopRoleInstallatAuthorization">RDS role installation and licensing</a>
</td>
</tr>
<tr>
<td>
<a href="#networkAccessAccountCheck">Network access account </a>
</td>
</tr>
<tr>
<td>
<a href="#servicePortFirewallAllowed">Whether an RDS port is allowed in firewall settings</a>
</td>
</tr>
<tr>
<td rowspan=5>Network Configuration</td>
<td>
<a href="#portExhaustionCheck">Port exhaustion</a>
</td>
</tr>
<tr>
<td>
<a href="#timewaitClosewaitConnections">Number of connections in Timewait/Closewait status</a>
</td>
</tr>
<tr>
<td>
<a href="#gatewayStatusCheck">Gateway status</a>
</td>
</tr>
<tr>
<td>
<a href="#MACAddressCheck">MAC address</a>
</td>
</tr>
<tr>
<td>
<a href="#intranetDomainNameResolution">Intranet domain name resolution</a>
</td>
</tr>
</table>


## Identifying and Fixing Issues
You can fix the issues found in checks by following the steps below.

<dx-accordion>
::: Windows OS status
#### Issue description[](id:OSStatusCheck)
The system may have issues like degraded stability, pre-failure, inability to start, and start-up/shut-down related problems, and involve such risks as unexpected restart and crash.    


#### Solution
1. Back up data by creating snapshots or other means to ensure data security. For more information, see [Creating Snapshots](https://intl.cloud.tencent.com/document/product/362/5755).
2. Restart the instance through the console. For more information, see [Restarting Instances](https://intl.cloud.tencent.com/document/product/213/4928).
3. Run TAT again to check whether the issue is fixed. If the issue persists, try the following solutions:
   - Reinstall the instance system through the console. For more information, see [Reinstalling System](https://intl.cloud.tencent.com/document/product/213/4933).
   - Restore the instance quickly by rolling back snapshots. For more information, see [Rolling Back Snapshots](https://intl.cloud.tencent.com/document/product/362/5756). For snapshot-related issues, see [Snapshot FAQs](https://intl.cloud.tencent.com/document/product/362/17820).

:::
::: Memory limit
#### Issue description[](id:memoryLimit)
 Memory underutilization occurs on the Windows operating system. Memory bottlenecks may exist, preventing the system from maximizing its performance.


#### Solution
1. Log in to the instance. For more information, see [Logging in Using Standard Method (Recommended)](https://intl.cloud.tencent.com/document/product/213/41018).
2. Right-click in the lower left corner of the operating system's desktop <img src="https://qcloudimg.tencent-cloud.cn/raw/0cfefcbe7474bf6b532a589c53314d5b.png" style="margin:-3px 0px">, and select <b>Windows PowerShell (Admin)</b> from the pop-up menu.
3. Enter `resmon` in the powershell window, and press **Enter** to open the **Resource Monitor** window.
4. In the **Resource Monitor** window, select the **Memory** tab, and check if the **Hardware Reserved** is greater than 512 MB. 
	
   - A value less than 512 MB indicates a normal state.
   - If the value is greater than 512 MB, perform the following steps to fix the issue:
   1. Enter `msconfig` in the powershell window, and press **Enter** to open the "System Configuration" window.
   2. In the "System Configuration" window, select the **Boot** tab, and then click **Advanced Options**. 
  
	 3. In the "Boot Advanced Options" pop-up, deselect "Maximum Memory". 
	
	 4. Click **OK**.
	 5. Right-click in the lower left corner of the operating system's desktop, <img src="https://qcloudimg.tencent-cloud.cn/raw/0cfefcbe7474bf6b532a589c53314d5b.png" style="margin:-3px 0px">, and select **Settings**.
	 6. Select **Update & Security** in the "Settings" window, and click **Activate** on the left.
	 7. Check if the system is activated.
	    - If yes, proceed with the next step.
	    - If not, activate it by following the steps described in [System Activation](https://intl.cloud.tencent.com/document/product/213/2757).
	 8. Restart the instance through the console to make the settings take effect. For more information, see [Restarting Instances](https://intl.cloud.tencent.com/document/product/213/4928).


:::
::: CPU limit
#### Issue description[](id:CPULimit)[](id:CPULimit)

CPU underutilization occurs on the Windows operating system. CPU bottlenecks may exist, preventing the system from maximizing its performance.


#### Solution
1. Log in to the instance. For more information, see [Logging in Using Standard Method (Recommended)](https://intl.cloud.tencent.com/document/product/213/41018).
2. Right-click in the lower left corner of the operating system's desktop, <img src="https://qcloudimg.tencent-cloud.cn/raw/0cfefcbe7474bf6b532a589c53314d5b.png" style="margin:-3px 0px">, and select <b>Windows PowerShell (Admin)</b> from the pop-up menu.
3. Enter `msconfig` in the powershell window, and press **Enter** to open the "System Configuration" window.
4. In the "System Configuration" window, select the **Boot** tab, and then click **Advanced Options**. 

5. In the "Boot Advanced Options" pop-up, deselect "Number of Processors". 

6. Restart the instance through the console to make the settings take effect. For more information, see [Restarting Instances](https://intl.cloud.tencent.com/document/product/213/4928).


:::
:::Handle leak
#### Issue description[](id:handleLeak)
Handle leak can cause a waste of system resources, and even failures of the system, such as stutters, login failure, and service errors.



#### Solution
1. Log in to the instance. For more information, see [Logging in Using Standard Method (Recommended)](https://intl.cloud.tencent.com/document/product/213/41018).
If you are unable to log in to the instance, please [restart the instance](https://intl.cloud.tencent.com/document/product/213/4928).
2. Right-click in the lower left corner of the operating system's desktop, <img src="https://qcloudimg.tencent-cloud.cn/raw/0cfefcbe7474bf6b532a589c53314d5b.png" style="margin:-3px 0px">, and select <b>Windows PowerShell (Admin)</b> from the pop-up menu.
3. Enter `taskmgr.exe` in the powershell window, and press **Enter** to open the "Task Manager" window.
4. In the "Task Manager" window, select **Details** and click the **Performance** tab. You can check the total number of handles.

5. Select the **Details** tab, right-click the first row of the details, and then click **Select Column** in the pop-up menu.
6. In the "Select Column" pop-up window, select "Handle", and then click **OK**.
7. Click **Handle** in the first row to sort processes by the number of handles in descending order. 

8. Right-click the process with the most handles, and select **Create Dump File** from the pop-up menu.
9. Click **OK** in the "Dump Process" pop-up window.
10. Update system patches, install antivirus software, and perform virus scans as needed.


:::
::: System brute force and attacks
#### Issue description[](id:BruteForceAttack)
Brute force and attacks can cause system stutters or even a system crash. This can affect the normal operation of services or even lead to data loss.


#### Solution
Set the security group policy reasonably through the console by only allowing necessary IPs and ports and denying others by default. For more information, see [Security Group Overview](https://intl.cloud.tencent.com/document/product/215/38750).


:::
::: System environment variables
#### Issue description[](id:environmentVariable)
Issues related to environment variables can cause the failure of some commands (you are prompted that the command does not exist, or an exception occurs after the command is executed, such as a window that keeps popping up.)


#### Solution
1. Log in to the instance. For more information, see [Logging in Using Standard Method (Recommended)](https://intl.cloud.tencent.com/document/product/213/41018).
2. Right-click in the lower left corner of the operating system's desktop, <img src="https://qcloudimg.tencent-cloud.cn/raw/0cfefcbe7474bf6b532a589c53314d5b.png" style="margin:-3px 0px">, and select <b>Windows PowerShell (Admin)</b> from the pop-up menu.
3. Enter `sysdm.cpl` in the powershell window, and press **Enter** to open the "System Properties" window.
4. In the "System Properties" window, select the **Advanced** tab, and click **Environment Variables**.

5. Double-click `Path` in "System Variables" to check the environment variables.
	Make sure the following 4 environment variables exist, are in the correct order, and are placed at the top. If you have other custom environment variables, put them at the bottom. 
	
	If any issue occurs with your environment variables, fix it:
	- `%SystemRoot%\system32`
	- `%SystemRoot%`
	- `%SystemRoot%\System32\Wbem`
	- `%SYSTEMROOT%\System32\WindowsPowerShell\v1.0\`


:::
::: High memory usage
#### Issue description[](id:highMemoryUsage)
High memory usage can degrade system performance, and insufficient available memory can cause system stutters.



#### Solution
1. Log in to the instance. For more information, see [Logging in Using Standard Method (Recommended)](https://intl.cloud.tencent.com/document/product/213/41018).
If you cannot log in to your CVM due to high memory usage, please refer to [Failed to log in to a Windows CVM due to high CPU and memory usage](https://intl.cloud.tencent.com/document/product/213/32405) for troubleshooting.
2. Identify the process with the highest memory usage by viewing the check results or "Task Manager". The following are the steps for identifying the process in "Task Manager". 
   1. Right-click in the lower left corner of the operating system's desktop,<img src="https://qcloudimg.tencent-cloud.cn/raw/0cfefcbe7474bf6b532a589c53314d5b.png" style="margin:-3px 0px">, and select <b>Windows PowerShell (Admin)</b> from the pop-up menu.
   2. Enter `resmon` in the powershell window, and press **Enter** to open "Resource Monitor".
   3. In "Resource Monitor", verify whether the process with the highest memory usage is running normally. 
   	
	    If the business is checked out：
		 - If the identified process is necessary for your business, upgrade your instance configuration by referring to [Changing Instance Configuration](https://intl.cloud.tencent.com/document/product/213/2178).
		 - If the process is not for your business, it is recommended to update system patches, install antivirus software, or perform virus scans as needed.



:::
::: High virtual memory usage
#### Issue description[](id:highVirtualMemoryUsage)
Long-term insufficient virtual memory can lead to problems such as Windows activation registry corruption, restricted memory, or restricted login.


#### Solution
1. Log in to the instance. For more information, see [Logging in Using Standard Method (Recommended)](https://intl.cloud.tencent.com/document/product/213/41018).
2. Right-click in the lower left corner of the operating system's desktop, <img src="https://qcloudimg.tencent-cloud.cn/raw/0cfefcbe7474bf6b532a589c53314d5b.png" style="margin:-3px 0px">, and select <b>Windows PowerShell (Admin)</b> from the pop-up menu.
3. Enter `sysdm.cpl` in the powershell window, and press **Enter** to open the "System Properties" window.
4. In the "System Properties" pop-up window, click **Settings** under "Performance". 
5. In the "Performance Options" pop-up window, select the **Advanced** tab, and click **Change**. 
6. In the "Virtual Memory" pop-up window, set the following options. 
    1. Deselect "Automatically manage paging file size for all drives".
    2. Select a drive with sufficient disk space to host the paging file on this drive. Drive C is selected in this example.
    3. Select "Custom Size" and set the paging file size.
    4. Click **Settings**.
    5. Click **OK**.
<dx-alert infotype="explain" title="">
Since virtual memory depends on physical memory and free drive space, it is recommended to change the instance resource configuration to increase physical memory. For more information, see [Changing Instance Configuration](https://intl.cloud.tencent.com/document/product/213/2178).
</dx-alert>


:::
::: High total CPU usage
#### Issue description[](id:totalCPUusagehigh)
Excessive CPU usage can cause degraded system performance, and insufficient available CPU resources may lead to instance stutters or even your failure to log in to the instance.


#### Solution
1. Log in to the instance. For more information, see [Logging in Using Standard Method (Recommended)](https://intl.cloud.tencent.com/document/product/213/41018).
If you cannot log in to your CVM due to high memory usage, please refer to [Failed to log in to a Windows CVM due to high CPU and memory usage](https://intl.cloud.tencent.com/document/product/213/32405) for troubleshooting.
2. Identify the process with the highest CPU usage by viewing the check results, "Task Manager", or "Resource Monitor". The following are the steps for identifying the process in "Resource Monitor".
   1. Right-click in the lower left corner of the operating system's desktop,<img src="https://qcloudimg.tencent-cloud.cn/raw/0cfefcbe7474bf6b532a589c53314d5b.png" style="margin:-3px 0px">, and select <b>Windows PowerShell (Admin)</b> from the pop-up menu.
   3. Enter `resmon` in the powershell window, and press **Enter** to open "Resource Monitor".
   3. In "Resource Monitor", select the **CPU** tab to verify whether the process with the highest CPU usage is running normally. 
	    If the business is checked out：
		 - If the identified process is necessary for your business, upgrade your instance configuration by referring to [Changing Instance Configuration](https://intl.cloud.tencent.com/document/product/213/2178).
		 - If the process is not for your business, it is recommended to update system patches, install antivirus software, or perform virus scans as needed.


:::
::: High usage of a single CPU
#### Issue description[](id:CPUusagehigh)
If the usage of a single logical CPU is too high, but that of other logical CPUs is low, this can lead to an uneven distribution of CPU resources and the inability to maximize the system performance.



#### Solution
1. Identify the process with the highest CPU usage of a single CPU from the check results.
2. Verify whether the process is running normally.
   - If yes, ignore it.
   - If not, it is recommended to optimize the CPU usage of the abnormal process (unless the high CPU usage is for a specific purpose), or contact the program manufacturer for optimization and adaptation.


:::
::: Large space occupied by metafiles in NTFS file system
#### Issue description[](id:ntfsFileUsageHigh)
The large total size of metafiles hidden in the NTFS file system can lead to insufficient system space.



#### Solution
This issue is caused by an excessive number of metafiles. If the issue occurs occasionally, it is recommended to back up your data and then format the drive. If the issue occurs frequently, please check whether the program generates an excessive number of files, and then optimize the program.



:::
::: Remote Desktop Services (RDS) status
#### Issue description[](id:remoteDesktopCheck)
RDS has an abnormal status, which results in the failure to log in to the CVM remotely (you can only log in through VNC).


#### Solution
1. [Log in to the Windows instance using VNC](https://intl.cloud.tencent.com/document/product/213/32496).
2. Right-click in the lower left corner of the operating system's desktop, <img src="https://qcloudimg.tencent-cloud.cn/raw/0cfefcbe7474bf6b532a589c53314d5b.png" style="margin:-3px 0px">, and select <b>Windows PowerShell (Admin)</b> from the pop-up menu.
3. Execute the following command in the powershell window to start the service.
```
Get-Service termservice |Start-Service -Verbose
```
   - Normally, the returned result is as follows:
![](https://qcloudimg.tencent-cloud.cn/raw/c362638db2ec00bd33440253cfd5f5b7.png)
   - If the restart of the service gets stuck, perform the following steps.
   1. Execute the following command to obtain the PID.
```
sc.exe queryex termservice
```
As shown in the figure below, the PID value is 800.
![](https://qcloudimg.tencent-cloud.cn/raw/94369868c25e7bb96866e8a28fd578f3.png)
   2. Execute the following command to forcibly end the process by using the obtained PID.
```
taskkill.exe /f /pid "PID number"
```
Execute the following command with the PID 800:
```
taskkill.exe /f /pid 800
```
   3. Execute the following command to start up Remote Desktop Services.
```
Start-Service TermService
```



:::
::: RDS port
#### Issue description[](id:remoteDesktopPortCheck)
The RDS port is not listened. You are unable to log in to the CVM remotely, and can only log in through VNC.



#### Solution

<dx-alert infotype="explain" title="">
Check whether the problem is fixed after performing each step. If not, proceed with the next step.
</dx-alert>



1. **Execute a command**
   1. [Log in to the Windows instance using VNC](https://intl.cloud.tencent.com/document/product/213/32496).
   2. Right-click in the lower left corner of the operating system's desktop, <img src="https://qcloudimg.tencent-cloud.cn/raw/0cfefcbe7474bf6b532a589c53314d5b.png" style="margin:-3px 0px">, and select <b>Windows PowerShell (Admin)</b> from the pop-up menu.
   3. Execute the following command in the powershell window.
```
Set-ItemProperty 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp\' -Name fEnableWinStation -Value "1" -Force
```
2. **Check if the system is activated.**
    1. Right-click in the lower left corner of the operating system's desktop, <img src="https://qcloudimg.tencent-cloud.cn/raw/0cfefcbe7474bf6b532a589c53314d5b.png" style="margin:-3px 0px">, and select **Settings**.
    2. Select **Update & Security** in the "Settings" window, and click **Activate** on the left.
    3. Check whether the system is activated. If not, activate it by following the steps described in [System Activation](https://intl.cloud.tencent.com/document/product/213/2757).
3. **Reset WinSock**
    1. Execute the following command to reset WinSock.
```
netsh.exe winsock reset
```
    2. After executing the command, restart the instance make the settings take effect. For more information, see [Restarting Instances](https://intl.cloud.tencent.com/document/product/213/4928).
4. **Fixing multi-user login remote**
   If you have installed Remote Desktop Services for multi-user login, it is recommended to uninstall it, and then install it again after troubleshooting.
   By following the steps below, export and back up the registry file of the abnormal instance, and then import the registry file of a normal instance to the abnormal instance.  
   1. Right-click in the lower left corner of the operating system's desktop,<img src="https://qcloudimg.tencent-cloud.cn/raw/0cfefcbe7474bf6b532a589c53314d5b.png" style="margin:-3px 0px">, and select <b>Windows PowerShell (Admin)</b> from the pop-up menu.
   2. Enter `regedit` in the powershell window, and press **Enter** to open "Registry Editor".
   3. In the file tree on the left of the "Registry Editor", locate the `WinStations` file under the path **HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations**.
   4. Right-click the `WinStations` file, and select **Export** from the pop-up menu. As shown in the figure below:
	 5. Set a name for the exported file in the pop-up window, such as `WinStations.reg` in this example.
   6. Click **OK**, and then view the exported file `WinStations.reg` in the specified location.
   7. After backup, export the registry file `WinStations` of the normal instance, and then import it to the abnormal instance. Double-click the `WinStations.reg` file to be imported, and click **Yes** in the pop-up window to import it.



:::
::: RDP-TCP connection
#### Issue description[](id:RDPCconnectionCheck)
The RDS port is not listened. You are unable to log in to the CVM remotely, and can only log in through VNC.

#### Solution
 1. [Log in to the Windows instance using VNC](https://intl.cloud.tencent.com/document/product/213/32496).
 2. Right-click in the lower left corner of the operating system's desktop, <img src="https://qcloudimg.tencent-cloud.cn/raw/0cfefcbe7474bf6b532a589c53314d5b.png" style="margin:-3px 0px">, and select <b>Windows PowerShell (Admin)</b> from the pop-up menu.
 3. Execute the following command in the powershell window.
```
Set-ItemProperty 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp\' -Name fEnableWinStation -Value "1" -Force
```


:::
::: Whether RDS connection is allowed
#### Issue description[](id:allowRemoteDesktopConnection)
You are unable to log in to the CVM remotely, and can only log in through VNC.

#### Solution
 1. [Log in to the Windows instance using VNC](https://intl.cloud.tencent.com/document/product/213/32496).
 2. Right-click in the lower left corner of the operating system's desktop, <img src="https://qcloudimg.tencent-cloud.cn/raw/0cfefcbe7474bf6b532a589c53314d5b.png" style="margin:-3px 0px">, and select <b>Windows PowerShell (Admin)</b> from the pop-up menu.
 3. Execute the following command in the powershell window.
```
Set-ItemProperty 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\' -Name "fDenyTSConnections" -Value 0 -Force
```


:::
::: RDP self-signed certificate expiration time
#### Issue description[](id:signedCertificateExpiration)
You are unable to log in to the CVM remotely, and can only log in through VNC.

#### Solution
 1. [Log in to the Windows instance using VNC](https://intl.cloud.tencent.com/document/product/213/32496).
 2. Right-click in the lower left corner of the operating system's desktop, <img src="https://qcloudimg.tencent-cloud.cn/raw/0cfefcbe7474bf6b532a589c53314d5b.png" style="margin:-3px 0px">, and select <b>Windows PowerShell (Admin)</b> from the pop-up menu.
 3. Execute the following commands in the powershell window.
```shell
Remove-Item -Path 'Cert:\LocalMachine\Remote Desktop\*' -Force -ErrorAction SilentlyContinue
```
```
Restart-Service TermService -Force
```

:::
::: RDS role installation and licensing
#### Issue description[](id:desktopRoleInstallatAuthorization)
Your failure to import the License within the 120-day period results in the failure of remote login (you can only log in through VNC).

#### Solution
The Microsoft system allows up to 2 accounts to log in concurrently by default. If multi-user remote login is not required, you're recommended to uninstall the RDS roles to quickly fix the issue. If multi-user remote login is required, contact Microsoft to purchase RDS CALs (Client Access Licenses). For more information, see [Setting Up Windows CVM for Multi-User Remote Login](https://intl.cloud.tencent.com/document/product/213/32497).

Perform the following steps:

 1. [Log in to the Windows instance using VNC](https://intl.cloud.tencent.com/document/product/213/32496).
 2. Right-click in the lower left corner of the operating system's desktop, <img src="https://qcloudimg.tencent-cloud.cn/raw/0cfefcbe7474bf6b532a589c53314d5b.png" style="margin:-3px 0px">, and select <b>Windows PowerShell (Admin)</b> from the pop-up menu.
 3. Execute the following commands in the powershell window to uninstall roles.
```shell
Remove-WindowsFeature Remote-Desktop-Services
```
4. Restart the instance to make the settings take effect. For more information, see [Restarting Instances](https://intl.cloud.tencent.com/document/product/213/4928).

:::
::: Network access account
#### Issue description[](id:networkAccessAccountCheck)
You are unable to log in to the CVM remotely, and can only log in through VNC.



#### Solution
 1. [Log in to the Windows instance using VNC](https://intl.cloud.tencent.com/document/product/213/32496).
 2. Right-click in the lower left corner of the operating system's desktop, <img src="https://qcloudimg.tencent-cloud.cn/raw/0cfefcbe7474bf6b532a589c53314d5b.png" style="margin:-3px 0px">, and select <b>Windows PowerShell (Admin)</b> from the pop-up menu.
 3. Execute the following commands in the powershell window.
```shell
Set-ItemProperty HKLM:\SYSTEM\CurrentControlSet\Control\Lsa -Name forceguest -Value 0 -Force
```

:::
::: Whether RDS port is allowed in firewall settings
#### Issue description[](id:servicePortFirewallAllowed)
The RDS port is blocked in the Windows CVM's firewall settings. As a result, you are unable to log in to the CVM remotely, and can only log in through VNC.



#### Solution
1. [Log in to the Windows instance using VNC](https://intl.cloud.tencent.com/document/product/213/32496).
2. Right-click in the lower left corner of the operating system's desktop, <img src="https://qcloudimg.tencent-cloud.cn/raw/0cfefcbe7474bf6b532a589c53314d5b.png" style="margin:-3px 0px">, and select <b>Windows PowerShell (Admin)</b> from the pop-up menu.
3. Enter `wf` in the powershell window, and press **Enter** to open the "Windows Firewall with Advanced Security" window.
4. In the "Windows Firewall with Advanced Security" window, click **Windows Firewall Properties** in "Overview". As shown in the figure below:
5. In "Local Computer" > "Properties", switch to **"Domain Profile", "Private Profile", and "Public Profile"** respectively, and set "Firewall State" to "Off".
6. Click **OK** to save the settings.
After turning off the instance's firewall, allow the RDS port of the instance by configuring the security group in the console. For more information, see [Adding Security Group Rules](https://intl.cloud.tencent.com/document/product/213/34272).



:::
::: Port exhaustion
#### Issue description[](id:portExhaustionCheck)
 The port exhaustion causes the network disconnection problem.



#### Solution
 1. [Log in to the Windows instance using VNC](https://intl.cloud.tencent.com/document/product/213/32496).
 2. Right-click in the lower left corner of the operating system's desktop, <img src="https://qcloudimg.tencent-cloud.cn/raw/0cfefcbe7474bf6b532a589c53314d5b.png" style="margin:-3px 0px">, and select <b>Windows PowerShell (Admin)</b> from the pop-up menu.
 3. In the powershell window, you can choose to use the following methods as needed:
    - Increase the number of ports. This can return the business to normal quickly without having to restart the instance.
```
netsh int ipv4 set dynamicport tcp start=10000 num=55536
```
```
netsh int ipv4 set dynamicport udp start=10000 num=55536
```
    - Speed up the release of ports while increasing the number of ports This method is recommended, but a restart of the instance is required.
```
Set-ItemProperty HKLM:\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters\ -Name TcpTimedWaitDelay -Value 30 -Force
```


:::
::: Number of connections in Timewait/Closewait status
#### Issue description[](id:timewaitClosewaitConnections)
A large number of connections in Timewait/Closewait status may lead to your inability to log in remotely, or even port exhaustion and network disconnection.



#### Solution
1. [Log in to the Windows instance using VNC](https://intl.cloud.tencent.com/document/product/213/32496).
2. Right-click in the lower left corner of the operating system's desktop, <img src="https://qcloudimg.tencent-cloud.cn/raw/0cfefcbe7474bf6b532a589c53314d5b.png" style="margin:-3px 0px">, and select <b>Windows PowerShell (Admin)</b> from the pop-up menu.
3. Execute the following command in the powershell window to speed up the release of ports.
```
Set-ItemProperty HKLM:\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters\ -Name TcpTimedWaitDelay -Value 30 -Force
```
It is recommended to use a security group to only allow necessary IPs and port numbers for filtering out malicious requests. At the same time, replace the default service ports with too many connections in wait status as needed, for example, the default port 3389 for Remote Desktop Services.

:::
::: Gateway status
#### Issue description[](id:gatewayStatusCheck)
A gateway issue may cause network disconnection.



#### Solution
1. [Log in to the Windows instance using VNC](https://intl.cloud.tencent.com/document/product/213/32496).
2. Right-click in the lower left corner of the operating system's desktop, <img src="https://qcloudimg.tencent-cloud.cn/raw/0cfefcbe7474bf6b532a589c53314d5b.png" style="margin:-3px 0px">, and select <b>Windows PowerShell (Admin)</b> from the pop-up menu.
3. Enter `ncpa.cpl` in the powershell window, and press **Enter** to open the "Network Connection" window.
4. In the "Network Connection" window, restart the NIC:
    - Right-click the NIC, and select **Disable** from the pop-up menu.
    - Right-click again, select **Enable** to try a quick fix.
5. If the problem persists, verify whether the NIC obtains an IP address automatically. If not, it is recommended to set it to "Obtain an IP address automatically". The steps are as follows:
   1. Right-click the NIC in the "Network Connection" window, and select **Properties** from the pop-up menu.
   2.Select "Internet Protocol Version 4 (TCP/IPv4)" in the "Ethernet X Properties" pop-up window, and then click **Properties**.
   3. In the "Internet Protocol Version 4 (TCP/IPv4)" pop-up window, select "Obtain an IP address automatically".
   4. Click **OK**, and then check the gateway status again.


:::
:::MAC address
#### Issue description[](id:MACAddressCheck)
An abnormal MAC address may cause network disconnection.



#### Solution
1. [Log in to the Windows instance using VNC](https://intl.cloud.tencent.com/document/product/213/32496).
2. Right-click in the lower left corner of the operating system's desktop, <img src="https://qcloudimg.tencent-cloud.cn/raw/0cfefcbe7474bf6b532a589c53314d5b.png" style="margin:-3px 0px">, and select <b>Windows PowerShell (Admin)</b> from the pop-up menu.
3. Enter `ncpa.cpl` in the powershell window, and press **Enter** to open the "Network Connection" window.
4 Right-click the NIC in the "Network Connection" window, and select **Properties** from the pop-up menu.
5. In the **Ethernet X Properties** pop-up window, click **Configuration**.
6. In the "Tencent VirtIO Ethernet Adapter Properties" pop-up window, select the **Advanced** tab, select **Assign MAC** in "Properties", and set it to "Absent". 
7. Click **OK** to save the settings.
8. In the "Network Connection" window, restart the NIC:
    - Right-click the NIC, and select **Disable** from the pop-up menu.
    - Right-click again, and select **Enable**.



:::
::: Intranet domain name resolution
#### Issue description[](id:intranetDomainNameResolution)
The nslookup and ping commands fail to query DNS data for an intranet, resulting the inability to activate the system and sync time.



#### Solution
1. [Log in to the Windows instance using VNC](https://intl.cloud.tencent.com/document/product/213/32496).
2. Right-click in the lower left corner of the operating system's desktop, <img src="https://qcloudimg.tencent-cloud.cn/raw/0cfefcbe7474bf6b532a589c53314d5b.png" style="margin:-3px 0px">, and select <b>Windows PowerShell (Admin)</b> from the pop-up menu.
3. Enter `ncpa.cpl` in the powershell window, and press **Enter** to open the "Network Connection" window.
4 Right-click the NIC in the "Network Connection" window, and select **Properties** from the pop-up menu.
5.Select "Internet Protocol Version 4 (TCP/IPv4)" in the "Ethernet X Properties" pop-up window, and then click **Properties**.
6. In the "Internet Protocol Version 4 (TCP/IPv4)" pop-up window:
    - It is recommended to select "Obtain DNS server address automatically", or add CVM default DNS addresses (generally, add `183.60.83.19` and `183.60.82.98` for a private network).
    - If the instance is a domain environment, click **Advanced**. Then in the "Advanced TCP/IP Settings" window, it is recommended to place the CVM default DNS addresses after the domain DNS.
7. Execute the following command in the powershell window to check the persistent route.
```
route print
```
If the route information in the returned result does not start with 169.254.0.0, execute the following command to add it.
```
route add 169.254.0.0 mask 255.255.128.0 $Gateway -p
```
<dx-alert infotype="notice" title="">
Replace `$Gateway` with your actual gateway address.
</dx-alert>
:::
</dx-accordion>



