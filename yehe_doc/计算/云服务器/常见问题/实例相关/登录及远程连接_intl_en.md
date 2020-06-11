### How do I log in to a CVM instance using VNC?

Tencent Cloud allows users to log in to a CVM instance by using the VNC web client. If you do no have a remote login client installed, or cannot log in using the client, the VNC web client is ideal for the situation. You can use the web client to log in remotely, view CVM instance status and perform basic instance management. For more information on detailed instructions, refer to the following articles:
- [Logging in to a Linux Instance Using VNC](https://intl.cloud.tencent.com/document/product/213/32494)
- [Logging in to a Windows Instance Using VNC](https://intl.cloud.tencent.com/document/product/213/32496).

### Why can I not use Internet Explorer 8.0 to log in to my instances?
VNC web client supports Internet Explorer 10 and later. Download the latest version of Internet Explorer.
Tencent Cloud console offers a better experience using Google Chrome. It is recommended that you use Google Chrome.

### How do I enable multi-user remote login on a Windows Server?

Windows Server supports multi-user remote login. For detailed instructions, refer to [Setting up a Windows CVM For Multi-user Remote Login](https://intl.cloud.tencent.com/document/product/213/32497).
If the steps you take do not work, restart the instance and try again.

### Does the console support multi-user login using VNC?
No, it does not. If one user is logged in, other users will not be able to do so.

### How can I log in to an instance running Ubuntu as root?

The default user for Ubuntu is `ubuntu`. `root` is not enabled during the installation process. If necessary, you can enable `root` by following the following instructions:
1. Log in to the CVM instance using `ubuntu`.
2. <span id="Step2"></span>Run the following command to set a password for `root`:
```
sudo passwd root
```
3. Enter a password for `root` and press **Enter**.
4. Enter the password again and press **Enter**.
The following message displays indicating that the password is set successfully:
```
passwd: password updated successfully
```
5. Run the following command to open `sshd_config`:
```
sudo vi /etc/ssh/sshd_config 
```
6. Press **i** to switch to edit mode. Find `#Authentication` and change the value of `PermitRootLogin` to `yes`, as shown in the following figure:
> If `PermitRootLogin` is commented, remove the comment marks (`#`).
> 
![](https://main.qcloudimg.com/raw/359242f7e5df666d43459fe74abce72a.png)
7. Press **Esc** and enter **:wq** to save the file and exit vi.
8. Run the following command to restart the SSH service.
```
sudo service ssh restart
```
9. Refer to [Logging in to a Linux Instance Using the Standard Login Method](https://intl.cloud.tencent.com/document/product/213/5436) on how to use the following information to log in to your CVM instance running Ubuntu.
 - **Username**: root
 - **Password**: the password you set in [Step 2](#Step2).
 A successful login using root is shown in the following figure:
![](https://main.qcloudimg.com/raw/a8a6ec3e2499e08d051c9ee11fdcd85e.png)

### What do I do if I cannot connect (log in) to my CVM instance after restarting it?

This may be caused by high CPU and memory usage of your instance. Refer to the following articles for more information:
- [Failed to Log in to a Linux CVM Due to High CPU and Memory Usage](https://intl.cloud.tencent.com/document/product/213/32387)
- [Failed to Log in to a Windows CVM Due to High CPU and Memory Usage](https://intl.cloud.tencent.com/document/product/213/32405)

### What do I do when I connect to my CVM instance remotely and the connection times out?
Make sure that:
- The instance is running.
- The instance is associated with security groups with the necessary security group rules. For detailed information, refer to [Adding Security Group Rules](https://intl.cloud.tencent.com/document/product/213/34272).
- The instance has SSH or RDP enabled.
- The instance opened the corresponding ports. SSH by default uses port 22 and RDP uses port 3389 by default.

### Why is my remote connection to my Linux instance refused?
Make sure that:
- The instance has SSH or RDP enabled.
- The instance opened the corresponding ports. SSH by default uses port 22 and RDP uses port 3389 by default.

### Why do I get the invalid username or password message when I remotely connect to my Linux instance?
Make sure that:
- You used the correct username. The default user for most Linux distributions is `root`. Ubuntu uses `ubuntu`.
- You entered your password correctly. If you forgot your password, reset it. For details, refer to [Resetting Instance Password](https://intl.cloud.tencent.com/document/product/213/16566).

### Why do I get the invalid username or password message when I remotely connect to my Windows instance?
Make sure that:
- You used the correct username. The default user for Windows is Administrator.
- You entered your password correctly. If you forgot your password, reset it. For details, refer to [Reset Instance Password](https://intl.cloud.tencent.com/document/product/213/16566).
- If you use a user without administrator privilege to log in, that user belongs to the Remote Desktop Users group.

### What do I do if I forgot my CVM instance login password?
You can reset the password. For details, refer to [Reset Instance Password](https://intl.cloud.tencent.com/document/product/213/16566).

### How do I log in to my Linux instance remotely?
- Tencent Cloud recommends [Logging in to a Linux Instance Using Standard Login Mode](https://intl.cloud.tencent.com/document/product/213/5436). You can also:
- [Logging in to a Linux Instance Using Remote Login Software](https://intl.cloud.tencent.com/document/product/213/32502).
- [Logging in to a Linux Instance Using SSH](https://intl.cloud.tencent.com/document/product/213/32501)
- [Log in to a Linux Instance Using VNC](https://intl.cloud.tencent.com/document/product/213/32494)

### What do I do if I cannot connect to my Linux instance?
If you cannot connect to your Linux instance, refer to [Linux Instance Login Failures](https://intl.cloud.tencent.com/document/product/213/32500) for troubleshooting instructions.
If the problem persists, [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=7&source=0&data_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8CVM&step=1).

### What do I do if I cannot connect to my Windows instance?
If you cannot connect to your Windows instance, refer to [CVM Login Failure](https://intl.cloud.tencent.com/document/product/213/10339) for troubleshooting instructions.
If the problem persists, [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=7&source=0&data_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8CVM&step=1).

### What do I do if I find unusual login locations?
If you find logins you do not recognize:
1. Double check the login time from the unusual login location and see if it is from yourself or other administrators.
2. If not, perform the following steps:
 1. [Reset the password](https://intl.cloud.tencent.com/document/product/213/16566) immediately.
 2. Check your instance for viruses or trojans.
 3. Use security groups to [limit logging in to specific IP addresses](https://intl.cloud.tencent.com/document/product/213/32369).



