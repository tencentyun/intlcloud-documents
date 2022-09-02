This topic describes how to troubleshoot intrusions into servers running on Windows.
## Identifying Causes of Intrusions
### I. Check accounts for weak passwords
1. Check whether weak passwords exist in the server system and application accounts.
 - Description: Check the system admin account, website backend account, database account, and other application accounts (FTP, Tomcat, phpMyAdmin, etc.) for weak passwords.
>?Set a strong account password using 12-16 characters containing uppercase and lowercase letters, special characters, and digits. You can also use a password generator to generate strong passwords.
 - Solution: Please check as needed.
 - Risk level: high
2. Check whether there are any accounts on the server that are not created by the system and you.
 - Description: The names of suspicious accounts created by hackers are generally displayed in the local user group.
 - Solution: Open the Command Prompt window and enter the command `lusrmgr.msc` to check whether there are any new accounts. If new accounts are found in the Administrators group, disable or delete them immediately.
 - Risk level: high
3. Check for hidden account names.
 - Description: To evade inspection, hackers often create hidden accounts on your server that are not visible in the local user group.
 - Solution (you can also check for hidden accounts by downloading the LD_check security tool):
     a. Open the Run window (or press Win + R) on the desktop, and enter `regedit` to open the Registry Editor.
     b. Select HKEY_LOCAL_MACHINE/SAM/SAM. The content of this key is invisible by default. Right-click the key and select **Permissions**.
     c. Select the current user (usually administrator), check **Full Control** for the permissions, click "OK", and close the Registry Editor.
     d. Open the Registry Editor again and select HKEY_LOCAL_MACHINE/SAM/SAM/Domains/Account/Users.
     e. You can see all the user names of the instance under Names. Any account that is not in the list of local accounts can be considered a hidden account. You can delete the user if you confirm it is a non-system user.    
 - Risk level: high

### II. Check for malicious processes and ports
1. Check whether there are malicious processes running in the system background.
 - Description: After intruding into the system, attackers often run malicious processes to communicate with the external network. By analyzing the processes that connect to the external network, you can identify the processes that have intruded into the system.
 - Solution:
     a. Log in to the server and select **Start** > **Run**.
     b. Enter "cmd", and then "netstat –nao" to check whether the server is being listened to by an unauthorized port.
     c. Open the Task Manager and check whether the process corresponding to the PID is a normal process. If not, check the path to the running file via the PID and delete the file. You can also use the Process Explorer provided by Microsoft for troubleshooting.
 - Risk level: high

### III. Check for malicious programs and startup items
1. Check whether unusual startup items exist on the server.
 - Description: After intruding into the system, attackers often put malicious programs in startup items so that they can run upon the system's startup.
 - Solution:
     a. Log in to the server and select **Start** > **All Programs** > **Startup**.
     b. By default, this directory is empty. Check whether there are non-business programs in it.
     c. Select **Start** >**Run**, and enter "msconfig" to check whether startup items with an abnormal name exist. If so, uncheck them and go to the paths displayed in the commands to delete the files.
     d. Select **Start** >**Run**, and enter "regedit" to open the Registry Editor. Check whether the startup items are normal. Especially, check the following three registry entries:
        HKEY_CURRENT_USER\software\micorsoft\windows\currentversion\run
        HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\Run
        HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\Runonce
    Check whether unusual startup items exist on the right of the Registry Editor. If so, delete them. It is recommended to install an anti-virus program for detecting and killing residual viruses and trojans.
 - Risk level: high

2. Check the connected sessions.
 - Description: Check ongoing sessions between the server and other servers on the network or scheduled tasks.
 - Solution:        
     a. Log in to the server and select **Start** > **Run**.
     b. Enter "cmd", and then "netstat -ano" to check the session between the server and other servers on the network, and verify whether the connection is normal. Enter "schtasks", check the scheduled tasks on the server, and verify whether it is a normal scheduled task.
 - Risk level: medium

### IV. Check for third-party software vulnerabilities
If your server runs service applications (WWW, FTP, etc.), configure them to **restrict their permissions and prohibit directory browsing or write access to files**.


## FAQs
### How to restore a compromised website or system 
After a system is intruded, the system files are often modified and replaced. At this point, the system has become untrusted. The best choice is to reinstall the system and install all patches to the new system.

### How to prevent the website or system from being intruded again
1. Change the passwords of all system accounts to **complex passwords** (at least different from those before the intrusion).
2. **Change the default remote desktop port** by following the steps below:
 1. Select **Start** > **Run**, and enter "regedit".
 2. Open the Registry Editor, and go to the following path: HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Terminal Server\Wds\rdpwd\Tds\tcp
 3. KEY_LOCAL_MACHINE\SYSTEM\CurrentContro1Set\Control\Tenninal Server\WinStations\RDP-Tcp
 4. Modify the PortNumber value on the right.
3. Configure the security group firewall to allow only **the specified IPs to access the remote desktop port**.
4. **Back up important business data and files** regularly.
5. **Update the OS and application components (FTP, Struts 2, etc.) regularly ** to prevent vulnerability exploitation.
6. Install **CWPP Agent** and an anti-virus program for regular checkups and scans.