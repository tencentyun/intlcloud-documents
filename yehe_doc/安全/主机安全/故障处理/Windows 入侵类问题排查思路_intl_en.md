This document will instruct you to troubleshoot intrusions on Windows.
## Finding Causes of Intrusions
### 1. Check accounts and weak passwords
1. Check whether there are weak passwords in the existing server system and application accounts:
 - Description: check system admin account, website backend account, database account, and other application accounts (FTP, Tomcat, phpMyAdmin, etc.) for weak passwords.
 >?Set a strong account password using 12-16 characters containing uppercase and lowercase letters, special characters, and digits. You can also use a password generator to automatically generate strong passwords.
 - Solution: do so based on the actual situation.
 - Risk level: high
2. Check whether there are any accounts on the server that are not created by the system and you.
 - Description: names of suspicious accounts created by hackers are generally displayed in the local user group.
 - Solution: open the Command Prompt window and enter the `lusrmgr.msc` command to see whether there are any new accounts. If there are new accounts in the Administrators group, disable or delete them immediately.
 - Risk level: high
3. Check whether there are hidden account names.
 - Description: hackers often create hidden users on your server to evade inspection. Hidden accounts are not visible in the local user group.
 - Solution (you can also check whether there are hidden accounts by downloading the LD_check security tool):
     a. Open the Run window (or press Win + R) on the desktop and enter `regedit` to open the Registry Editor.
     b. Select HKEY_LOCAL_MACHINE/SAM/SAM. The content of this key is invisible by default. Right-click the key and select **Permissions**.
     c. Select the current user (usually administrator), check **Full Control** for the permissions, click OK, and close the Registry Editor.
     d. Open the registry editor again to select HKEY_LOCAL_MACHINE/SAM/SAM/Domains/Account/Users.
     e. Under the Names entry, you can see all the usernames on the instance. If there is an account that is not in the local account group, it is a hidden account. After confirming that it is not a system user, delete it.    
 - Risk level: high

### 2. Check malicious processes and ports
1. Check whether there are malicious processes running in the system background.
 - Description: after intruding the system, attackers often run malicious processes to communicate with external services. By analyzing the outbound processes, the intrusion control processes can be identified.
 - Solution:
     a. Log in to the server and click **Start** > **Run**.
     b. Enter `cmd` and enter `netstat –nao` to check whether the server is being listened to by an unauthorized port.
     c. Open the Task Manager and check whether the process corresponding to the PID is a normal process, and if not, use the PID to view the path to the running file and delete it. You can also use the official Process Explorer tool provided by Microsoft for troubleshooting.
 - Risk level: high

### 3. Check malicious programs and startup items
1. Check whether there are abnormal startup items on the server.
 - Description: after intruding the system, attackers often put malicious programs in startup items so that they can run at system startup.
 - Solution:
     a. Log in to the server and select **Start** > **All Programs** > **Startup**.
     b. By default, this directory is empty. Check whether there are non-business programs in it.
     c. Select **Start** > **Run**, and enter `msconfig` to see whether there are startup items with abnormal names, and if yes, uncheck them and go to the paths displayed in the commands to delete the files.
     d. Select **Start** > **Run** and enter `regedit` to open the Registry Editor. Check whether the startup items are normal. Especially, check the following three registry entries:
        HKEY_CURRENT_USER\software\micorsoft\windows\currentversion\run
        HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\Run
        HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\Runonce
    Check whether there are any abnormal startup items on the right of the Registry Editor, and if yes, delete them. It is recommended to install an anti-virus program for detecting and killing residual viruses and trojans.
 - Risk level: high

2. View the connected sessions.
 - Description: check ongoing sessions between your computer and other computers on the network or scheduled tasks.
 - Solution:        
     a. Log in to the server and click **Start** > **Run**.
     b. Enter `cmd` and then enter `netstat -ano` to check ongoing sessions between your computer and other computers on the network and confirm whether they are normal. Enter `schtasks` to check scheduled tasks on your computer and confirm whether they are normal.
 - Risk level: medium

### 4. Check third-party software vulnerabilities
1. If your server runs service applications (WWW, FTP, etc.), configure them to **restrict their permissions and prohibit directory browsing or file write**.
2. [Activate Web Application Firewall (WAF)](https://console.cloud.tencent.com/guanjia/instance/domain) to view the WAF attack logs.

## FAQs
### How to restore a website or system
After the system is intruded, the system files are often modified and replaced. At this point, the system has become untrusted, and the best choice is to reinstall the system and install all patches to the new system.

### How to prevent the website or system from being intruded again
1. Change the passwords of all system accounts to **complex passwords** (at least different from those before the intrusion).
2. **Change the default remote desktop port** in the following steps:
 i. Select **Start** > **Run** and enter `regedit`.
 ii. Open the Registry Editor and go to the following path: HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Terminal Server\Wds\rdpwd\Tds\tcp
 iii. KEY_LOCAL_MACHINE\SYSTEM\CurrentContro1Set\Control\Tenninal Server\WinStations\RDP-Tcp
 iv. Modify the `PortNumber` value on the right.
3. Configure the security group firewall to allow only **the specified IPs to access the remote desktop port**.
4. **Back up important business data and files** on a regular basis.
5. **Update the OS and application components (FTP, Struts 2, etc.) on a regular basis** to prevent vulnerability exploitation.
6. Install **CWP Agent** and an anti-virus program for regular checkups and scans.
