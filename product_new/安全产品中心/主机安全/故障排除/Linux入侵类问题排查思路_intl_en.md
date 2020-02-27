## Finding Causes of Intrusions
### 1. Check for hidden accounts and weak passwords
1. Check whether there are **weak passwords** in the server system and application accounts:
 * Description: check the admin account, database account, MySQL account, Tomcat account, and website backend admin account for weak passwords that can be easily cracked by hackers.
  * Solution: log in to the system or application backend with admin privileges and change the weak passwords to complex passwords.
   * Risk level: high
2. Run the `last` command to view the record of accounts that recently logged in to the server and check whether there were logins from suspicious IPs.
    * Description: attackers or malware often inject hidden accounts into the system to implement privilege elevation or other destructive attacks.
    * Solution: when you find a suspicious user, run the `usermod -L username` command to disable the user or run the `userdel -r username` command to delete the user.
    * Risk level: high
3. Run the `less /var/log/secure|grep 'Accepted'` command to check whether there were successful logins from suspicious IPs.
    * Description: attackers or malware often inject hidden accounts into the system to implement privilege elevation or other destructive attacks.
    * Solution: when you find a suspicious user, run the `usermod -L username` command to disable the user or the `userdel -r username` command to delete the user.
    * Risk level: high
4. Check whether the system uses the **default management ports**:
    * Check whether the management ports (for SSH, FTP, MySQL, Redis, etc.) used by the system are the default ones. These default ports can be easily intruded by automated tools.
    * Solutions:
        1. Change port 22 in the `/etc/ssh/sshd_config` file on the server to a non-default port. You need to restart the SSH service after modification.
        2. Run `/etc/init.d/sshd restart` (on CentOS) or `/etc/init.d/ssh restart` (on Debian or Ubuntu) to restart the server to make the configuration take effect.
        3. Change the default listener ports 21, 3306, and 6379 in the configuration files of FTP, MySQL, and Redis to other ports.
        4. Deny remote login IPs by editing the `/etc/hosts.deny` and `/etc/hosts.allow` files.
    * Risk level: high
5. Check the `/etc/passwd` file to see whether there were unauthorized account logins.
    * Description: attackers or malware often inject hidden accounts into the system to implement privilege elevation or other destructive attacks.
    * Solution: when you find a suspicious user, run the `usermod -L username` command to disable the user or the `userdel -r username` command to delete the user.
    * Risk level: medium

### 2. Check for malicious processes and unauthorized ports
1. Run `netstat –antlp` to check whether the server is being listened to by an unauthorized port and check the corresponding PID.
 * Check the server for malicious processes, which often open listener ports and connect to external controllers.
 * Solutions:
      1. If you find an unauthorized process, run `ls -l /proc/$PID/exe` or `file /proc/$PID/exe` ($PID is the corresponding PID) to check the path to the process file corresponding to the PID.
      2. If it is a malicious process, delete the corresponding file.
   * Risk level: high
2. Run the `ps -ef` and `top` commands to check whether there are exceptional processes.
    * Description: run the commands above. If you find an unauthorized processes with a constantly changing name that occupies a great amount of CPU or memory resources, it may be a malicious program.
    * Solution: after confirming that the process is malicious, run the `kill -9 process name` command to end the process or use a firewall to prevent network connection by the process.
    * Risk level: high


### 3. Check malicious programs and suspicious startup items
1. Run the `chkconfig --list` and `cat /etc/rc.local` commands to check whether there are suspicious startup services in the startup items.
    * Description: malicious programs are often added to the system startup items so that they can run again after the system is restarted.
    * Solution: if you find a malicious process, run the `chkconfig service name off` command to close it. Plus, check whether there are suspicious items in `/etc/rc.local`, and if yes, comment them out.
    * Risk level: high
2. Go to the cron file directory and check whether there are illegal scheduled task scripts.
    * Description: check `/etc/crontab`, `/etc/cron.d`, `/etc/cron.daily`, `cron.hourly/`, `cron.monthly`, and `cron.weekly/` for suspicious scripts and programs.
    * Solution: if you find a scheduled task that you do not know, you can locate its script to confirm whether it is a normal service script, and if not, directly comment out the task content or delete the script.
    * Risk level: high

### 4. Check for third-party software vulnerabilities
1. If your server runs web or database application services, limit the application accounts' write access to the file system and try to use non-root accounts for running them.
    * Description: using a non-root account to run an application can guarantee that the attacker cannot remotely control the server immediately after the application is compromised, reducing the potential losses caused by attacks.
    * Solutions:
      1. Enter the web service's root directory or database configuration directory;
      2. Run the `chown -R apache:apache /var/www/xxxx` and `chmod -R 750 file1.txt` commands to configure website access permissions.
    * Risk level: medium
    * <a href=#ex>Reference example</a>
2. Upgrade applications to repair vulnerabilities
 * Description: if a server is intruded, the reason may be that the software applications used by the system are older with more unfixed vulnerabilities which could be exploited.
 * Solution: for typical vulnerabilities such as ImageMagick, openssl, and glibc, you can directly upgrade the applications to repair them through apt-get/yum or other methods according to the security notices released by Tencent Cloud.
  * Risk level: high

<a id="ex"></a>
**Below is a reference example of file permission of a website directory:**
**Scenario:**
Assume that the HTTP server runs user and user group “www”, the website user is “centos”, and the root directory of the website is `/home/centos/web`.
**Steps:**
1. Run the following command to set the owner of the website directory and files to “centos” and the owner group to “www”:
```
 chown -R centos:www /home/centos/web
```
2. Set the website directory permission to 750, which grants the user “centos” read/write permission to the directory. The user “centos” can create files in any directory. The user group has read and execute permissions so that the users in it can access the directory. Other users have no permissions at all.
```
find -type d -exec chmod 750 {} \;
```
3. Set the website file permission to 640. 640 means that only the centos user has permission to change the website files, the HTTP server only has permission to read files but cannot modify files, and other users have no permissions at all.
```
find -not -type d -exec chmod 640 {} \;
```
4. Set the permission for certain directories requiring write permission to 770. For example, some cache directories of the website need to grant the HTTP service write permission, such as the `/data/` directory of Discuz x2.
```
find data -type d -exec chmod 770 {} \;
```

## Security Optimization Suggestions
1. It’s recommended to log in using SSH keys to reduce the risk of brute force attacks.
2. Change port 22 in the `/etc/ssh/sshd_config` file on the server to a non-default port. You need to restart the SSH service after modification by running the following command:
```
/etc/init.d/sshd restart (on CentOS) or /etc/init.d/ssh restart (on Debian or Ubuntu)
```
3. If you do need to use password login, choose a strong password.
 * For application management backends (website, middleware, Tomcat, etc.), remote SSH, remote desktop, and databases, always use complex and different passwords.
 * See below for the examples of strong passwords (spaces are allowed):
       `1qtwo-threeMiles3c45jia`
       ` caser, lanqiu streets`
 * See below for the examples of weak passwords:
        Company name + date (coca-cola2016xxxx)
        Common phrases (Iamagoodboy)
4. Run the following command to check which ports on the server are opened to the internet and close ports not used for your business.
```
netstat -anltp
```
5. Use the **Tencent Cloud security group firewall** to allow only specified IPs to access the management features. Or, limit the IPs by editing the `/etc/hosts.deny` and `/etc/hosts.allow` files.
6. Prevent running applications with the **root** privileges.
  For example, for Apache, Redis, MySQL, and Nginx, do not run them with the root privileges.
7. Repair system privilege elevation vulnerabilities and **program vulnerabilities** running under the root privileges to prevent malware from gaining root privileges to embed backdoors.
    * Update the OS and applications used in a timely manner, such as Struts 2, Nginx, ImageMagick, Java,
    * Disable remote management of applications such as Redis and NTP. If there is no need for remote management, you can disable the external listener ports or configuration.
8. Regularly **back up** your CVM business data.
    * Perform off-site or cloud backup of important business data to ensure that the data can be recovered after the CVM instances are compromised.
    * In addition to the “home” and “root” directories, you should also back up the “/etc” and “/var/log” directories.
9. Install the **CWP Agent** so that you can understand the risk situation after an attack.
