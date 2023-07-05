### How do I log in to a CVM instance using VNC?

Tencent Cloud allows users to log in to a CVM instance by using the VNC web client. If you do not have a remote login client installed or cannot log in using the client, you can use a VNC web client to log in to a CVM instance. You can use the web client to log in remotely, view the CVM instance status, and perform basic instance management. For detailed instructions, refer to the following documents:
- [Logging into Linux Instances via VNC](https://intl.cloud.tencent.com/document/product/213/32494)
- [Logging into Windows Instances via VNC](https://intl.cloud.tencent.com/document/product/213/32496)

### How do I enable multi-user remote login on a Windows server?

The Windows server supports multi-user remote login. For detailed configuration directions, refer to [Setting Up Multi-user Remote Login for Windows CVMs](https://intl.cloud.tencent.com/document/product/213/32497).
If you fail to enable multi-user remote login on a Windows server after following the directions in the document above, restart the instance and try logging in again.

### How can I log in to an instance running Ubuntu as root?

The default user for Ubuntu is `ubuntu`. `root` is not enabled during the installation process by default. If necessary, you can enable `root` by following the directions below:
1. Log in to the CVM instance using `ubuntu`.
2. <span id="Step2"></span>Run the following command to set a password for `root`:
```
sudo passwd root
```
3. Enter a password for `root` and press **Enter**.
4. Enter the password again and press **Enter**.
If the following message is displayed, the password was set successfully:
```
passwd: password updated successfully
```
5. Run the following command to open `sshd_config`:
```
sudo vi /etc/ssh/sshd_config 
```
6. Press **i** to switch to the editing mode. Find `#Authentication` and change the value of `PermitRootLogin` to `yes`, as shown in the following figure:
>? If `PermitRootLogin` is commented, remove the comment marks (`#`).
> 
![](https://main.qcloudimg.com/raw/359242f7e5df666d43459fe74abce72a.png)
7. Press **Esc** and enter **:wq** to save the file and exit vi.
8. Run the following command to restart the SSH service.
```
sudo service ssh restart
```
9. Refer to [Logging into Linux Instances Using the Standard Login Method](https://intl.cloud.tencent.com/document/product/213/5436) on how to use the following information to log in to your CVM instance running Ubuntu.
 - **Username**: root
 - **Password**: the password you set in [Step 2](#Step2).
 A successful login using root is shown in the following figure:
![](https://main.qcloudimg.com/raw/a8a6ec3e2499e08d051c9ee11fdcd85e.png)

### What do I do if I cannot connect (log in) to my CVM instance after restarting it?

This problem may have been caused by the high CPU and memory usage of your instance. For more information, please refer to the following documents:
- [Failing to Log in to a Linux CVM Due to High CPU and Memory Usage](https://intl.cloud.tencent.com/document/product/213/32387)
- [Failing to Log in to a Windows CVM Due to High CPU and Memory Usage](https://intl.cloud.tencent.com/document/product/213/32405)

### What do I do when I connect to my CVM instance remotely and the connection times out?
Make sure that:
- The instance is running.
- The instance is associated with security groups with the necessary security group rules. For detailed information, refer to [Adding Security Group Rules](https://intl.cloud.tencent.com/document/product/213/34272).
- The instance has enabled SSH or RDP.
- The instance has opened the corresponding ports. SSH uses port 22 by default and RDP uses port 3389 by default.

### Why is my remote connection to my Linux instance refused?
Make sure that:
- The instance has enabled SSH or RDP.
- The instance has opened the corresponding ports. SSH uses port 22 by default and RDP uses port 3389 by default.

### Why do I get the invalid username or password message when I remotely connect to my Linux instance?
Make sure that:
- You used the correct username. The default username for most Linux distributions is `root`. However, Ubuntu uses `ubuntu`.
- You entered your password correctly. If you forgot your password, reset it. For detailed directions, refer to [Resetting Instance Passwords](https://intl.cloud.tencent.com/document/product/213/16566).

### Why do I get the invalid username or password message when I remotely connect to my Windows instance?
Make sure that:
- You used the correct username. The default username for Windows is `Administrator`.
- You entered your password correctly. If you forgot your password, reset it. For detailed directions, refer to [Resetting Instance Passwords](https://intl.cloud.tencent.com/document/product/213/16566).
- To use a user without administrator privileges to log in, that user needs to belong to the Remote Desktop Users group.

### Does the Console support multi-user login via VNC?
No. If one user has already logged in, other users will not be able to log in.

### What do I do if I forgot my CVM instance login password?
You can reset your password. For detailed directions, refer to [Resetting Instance Passwords](https://intl.cloud.tencent.com/document/product/213/16566).

### Why can’t I use Internet Explorer 8.0 to log in to my instances?
The VNC web client supports Internet Explorer 10 or later. Please download the latest version of Internet Explorer.
In addition, we recommend you use Google Chrome because the Tencent Cloud Console offers a better user experience on Google Chrome than on Internet Explorer.

### How do I log in to my Linux instance remotely?
- Tencent Cloud recommends [logging in to a Linux instance using the standard login mode](https://intl.cloud.tencent.com/document/product/213/5436). You can also:
- [Log in to a Linux instance using remote login software](https://intl.cloud.tencent.com/document/product/213/32502).
- [Log in to a Linux instance using SSH](https://intl.cloud.tencent.com/document/product/213/32501).
- [Log in to a Linux instance using VNC](https://intl.cloud.tencent.com/document/product/213/32494).

### What do I do if I cannot connect to my Linux instance?
If you cannot connect to your Linux instance, refer to [Linux Instance Login Failures](https://intl.cloud.tencent.com/document/product/213/32500) for troubleshooting instructions.
If this problem persists, please [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=7&source=0&data_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8CVM&step=1).

### What do I do if I cannot connect to my Windows instance?
If you cannot connect to your Windows instance, refer to [CVM Login Failure](https://intl.cloud.tencent.com/document/product/213/10339) for troubleshooting instructions.
If this problem persists, please [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=7&source=0&data_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8CVM&step=1).

### What do I do if I find that my CVM instance was logged into from unusual locations?
If you find that your CVM instance was logged into from locations you do not recognize:
1. Double check the login time from the unusual login location and check whether you or other administrators logged in at that time.
2. If no, follow the steps below:
 1. [Reset the password](https://intl.cloud.tencent.com/document/product/213/16566) immediately.
 2. Check your instance for viruses or trojans.
 3. Use security groups to [limit logins to specific IP addresses](https://intl.cloud.tencent.com/document/product/213/32369).



