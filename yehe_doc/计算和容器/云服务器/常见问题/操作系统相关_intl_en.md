### Why an error occurs when I execute an update on Ubuntu OS?

**Possible reasons**:
Tencent Cloud Ubuntu system source is synced with the official source at 00:00, 08:00 and 16:00 every day (UTC+8). If you run the `apt-get update` and `apt-get install` commands just before and after the time points, the apt verification will be failed and an error will occur.

**Solution**:
Run the `apt-get clean all` command to purge cache before you run the `apt-get update` command.



### How do I change the owners and owner groups of directories and files on a Linux instance?
If the file or directory permissions are incorrectly configured on the Web server, a 403 error will occur when you access a website hosted on the instance. Therefore, before you adjust a file or directory, you must confirm the identity under which the file or directory process is running.
- You can run the `ps` and `grep` commands to query the identities under which the file or directory process is running.
- You can run the `ls –l` command to query the owners and owner groups of files and directories.
- You can run the `chown` command to modify the permissions. For example, you can run the `chown -R www.www /tencentcloud/www/user/` command to change the owners and owner groups of all files and directories under the `/tencentcloud/www/user` directory to account “www”.


### Do Linux instances support GUI?
Yes. For directions on building GUI on a Linux instance, see [Building a Visual Ubuntu Desktop](https://intl.cloud.tencent.com/document/product/213/37500).


### How can I activate the operating system of a Windows CVM instance?
You can refer to [Activating Windows with slmgr Command](https://intl.cloud.tencent.com/document/product/213/2757) or [Windows Server System Activation](https://intl.cloud.tencent.com/document/product/213/46346) for directions.



### Why do I need to boot into the single-user mode on a Linux instance, and how to do this?
Linux's users sometimes need to boot into the single-user mode to perform special operations, such as password management, sshd repair, or maintenance before disk attaching. For directions, see [Booting into Linux Single User Mode](https://intl.cloud.tencent.com/document/product/213/34819).


### How can I check the login logs of a CVM instance?
For more information, see [Getting Instance Login Logs](https://www.tencentcloud.com/document/product/213/47384).
