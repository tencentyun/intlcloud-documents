This topic describes how to troubleshoot the intrusions into servers running on Linux and provides security optimization suggestions.

## Identifying Causes of Intrusions
### I. Check for hidden accounts and weak passwords
1. Check whether **weak passwords** exist in the server system and application accounts.
  * Description: check the admin account, database account, MySQL account, Tomcat account, and website backend admin account for weak passwords that can be easily cracked by hackers.
  * Solution: Log in to the system or application backend with admin privileges and change the weak passwords to complex passwords.
  * Risk level: high
2. Run the command `last` to view the record of accounts recently logged in to the server and check whether there were logins from suspicious IPs.
  * Description: Attackers or malware often inject hidden accounts into the system to implement privilege elevation or other destructive attacks.
  * Solution: When you find a suspicious user, run the command `usermod -L username` to disable the user or run the command `userdel -r username` to delete the user.
  * Risk level: high
3. Run the command `less /var/log/secure|grep 'Accepted'` to check whether there were successful logins from suspicious IPs.
  * Description: Attackers or malware often inject hidden accounts into the system to implement privilege elevation or other destructive attacks.
  * Solution: Run the command `usermod -L username` to disable the user or run the command `userdel -r username` to delete the user.
  * Risk level: high
4. Check whether the system uses the **default management ports**.
  * Check whether the management ports (for SSH, FTP, MySQL, Redis, etc.) used by the system are the default ones. These default ports can be easily attacked by automated tools.

  * Solutions:
    
      4.1. Change port 22 in the file `/etc/ssh/sshd_config` on the server to a non-default port. You need to restart the SSH service after modification.
>! When you change the port, you need to edit the security group configuration of the server on the [CVM Console](https://console.intl.cloud.tencent.com/cvm/instance/index?rid=1) to allow the corresponding port in its inbound rule. For more information, see [Adding Security Group Rules](https://www.tencentcloud.com/document/product/215/35513).

​      4.2. Run `/etc/init.d/sshd restart` (on CentOS) or `/etc/init.d/ssh restart` (on Debian or Ubuntu) to restart the server to make the updated configuration take effect.
​      4.3. Change the default listener ports 21, 3306, and 6379 in the configuration files of FTP, MySQL, and Reids to other ports.
​      4.4. Deny remote login IPs by editing the files `/etc/hosts.deny` and `/etc/hosts.allow`.

 * Risk level: high
5. Check the `/etc/passwd` file for unauthorized account logins.
  * Description: Attackers or malware often inject hidden accounts into the system to implement privilege elevation or other destructive attacks.
  * Solution: Run the command `usermod -L username` to disable the user or run the command `userdel -r username` to delete the user.
  * Risk level: medium

### II. Check for malicious processes and unauthorized ports
1. Run `netstat –antlp` to check whether the server is being listened to by an unauthorized port and check the corresponding PID.
 * Check the server for malicious processes, which often open listener ports and connect to external controllers.
 * Solutions:
      a. If you find an unauthorized process, run `ls -l /proc/$PID/exe` or `file /proc/$PID/exe` ($PID is the PID) to check the path to the process file identified by the PID.
      b. If it is a malicious process, delete its file.
   * Risk level: high
1. Run the commands `ps -ef` and `top` to check for unusual processes.
    * Description: If you find an unauthorized process with a constantly changing name that occupies a great amount of CPU or memory resources, it may be a malicious program.
    * Solution: After confirming that the process is malicious, run the command `kill -9 process name` to end the process or use a firewall rule to prevent network connection by the process.
    * Risk level: high


### III. Check for malicious programs and suspicious startup items
1. Run the commands `chkconfig --list` and `cat /etc/rc.local` to check whether suspicious startup services exist in the startup items.
    * Description: Malicious programs are often added to the system startup items so that they can run again after the system is restarted.
    * Solution: If you find a malicious process, run the command `chkconfig service name off` to close it. At the same time, check whether there are suspicious items in `/etc/rc.local`. If so, comment them out.
    * Risk level: high
2. Go to the cron file directory and check whether illegal scheduled task scripts exist.
    * Description: Check `/etc/crontab`, `/etc/cron.d`, `/etc/cron.daily`, `cron.hourly/`, `cron.monthly`, and `cron.weekly/` for suspicious scripts and programs.
    * Solution: If you find an unknown scheduled task, you can locate its script to verify whether it is a normal service script. If not, directly comment out the task content or delete the script.
    * Risk level: high

### IV. Check for third-party software vulnerabilities
1. If your server runs web or database application services, restrict the application accounts' write access to the file system and try to use non-root accounts for running them.
    * Description: Using a non-root account to run an application can guarantee that the attacker cannot remotely control the server immediately after the application is compromised, reducing the potential losses caused by the attack.
    * Solutions:
      a. Go to the web service's root directory or database configuration directory;
      b. Run the commands `chown -R apache:apache /var/www/xxxx` and `chmod -R 750 file1.txt` to configure the website access permissions.
    * Risk level: medium
    * <a href=#ex>Reference example</a>
2. Upgrade applications to fix vulnerabilities
 * Description: If a server is intruded, the reason may be that the software applications used by the system are older with more unfixed vulnerabilities, which could be exploited.
 * Solution: For typical vulnerabilities such as ImageMagick, openssl, and glibc, you can directly upgrade the applications to fix them through apt-get/yum or other methods according to the security notices released by Tencent Cloud.
  * Risk level: high

<a id="ex"></a>
**Below is an example of file permission for a website directory:**
**Scenarios:**
The user and user group running on the HTTP server is "www", the website user is "centos", and the root directory of the website is `/home/centos/web`.
**Steps:**
1. Run the following command to set the owner of the website directory and files to "centos" and the owner group to "www":
```
 chown -R centos:www /home/centos/web
```
2. Set the website directory permission to 750, which grants the user "centos" read/write access to the directory. The user "centos" can create files in any directory. The user group has read and execute permissions so that the users in it can access the directory. Other users have no permission at all.
```
find -type d -exec chmod 750 {} \;
```
3. Set the website file permission to 640, which means that only the user "centos" has permission to change the website files. The HTTP server only has permission to read files but cannot modify files, and other users have no permission at all.
```
find -not -type d -exec chmod 640 {} \;
```
4. Set the permission for certain directories requiring write permission to 770. For example, some cache directories of the website need to grant the HTTP service write permission, such as the `/data/` directory of Discuz x2.
```
find data -type d -exec chmod 770 {} \;
```

## Security Optimization Suggestions
- It’s recommended to log in using SSH keys to reduce the risk of brute force attacks.
- Change port 22 in the file `/etc/ssh/sshd_config` on the server to a non-default port. Then you need to restart the SSH service using the following command:
```
/etc/init.d/sshd restart (on CentOS) or /etc/init.d/ssh restart (on Debian or Ubuntu)
```
>! When you change the port, you need to edit the security group configuration of the server on the [CVM Console](https://console.intl.cloud.tencent.com/cvm/instance/index?rid=1) to allow the corresponding port in its inbound rule. For more information, see [Adding Security Group Rules](https://www.tencentcloud.com/document/product/215/35513).

- If you do need to use an SSH password, choose a strong one.
 * For application management backends (website, middleware, Tomcat, etc.), remote SSH, remote desktop, and databases, always use complex and different passwords.
 * See below for examples of strong passwords (spaces are allowed):
       `1qtwo-threeMiles3c45jia`
       ` caser, lanqiu streets`
 * See below for the examples of weak passwords:
        Company name + date (coca-cola2016xxxx)
        Common phrases (Iamagoodboy)
- Run the following command to check which ports on the server are opened to the Internet and close ports not used for your business.
```
netstat -antp
```
- Use the **Tencent Cloud security group firewall** to allow only specified IPs to access the management features. Or, restrict the IPs by editing the files `/etc/hosts.deny` and `/etc/hosts.allow`.
- Avoid running applications with the **root** privileges.
  For example, for Apache, Redis, MySQL, and Nginx, do not run them with the root privileges.
- Fix system privilege elevation vulnerabilities and **program vulnerabilities** running under the root privileges to prevent malware from gaining root privileges to embed backdoors.
    * Update the OS and applications used in a timely manner, such as Struts 2, Nginx, ImageMagick, and Java.
    * Disable remote management of applications such as Redis and NTP. If there is no need for remote management, you can disable the external listener ports or configuration.
- **Back up** your CVM business data regularly.
    * Perform off-site or cloud backup of important business data to ensure that the data can be recovered after the CVM instances are compromised.
    * In addition to the "home" and "root" directories, also back up the "/etc" and "/var/log" directories.
- Install Tencent Cloud's **CWPP Agent** so that you can keep track of risks after an attack.
