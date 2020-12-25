## Overview
Very Secure FTP Daemon (vsftpd) is the default FTP server for most Linux distributions. This document describes how to use the vsftpd software to build the FTP service on the CentOS 7.6 64-bit CVM.

## Software
The following software is used to build the FTP service.
- Linux operating system: this document uses the public image CentOS 7.6 as an example.
- Vsftpd: this document uses vsftpd 3.0.2 as an example.


## Directions
### Step 1: log in to the CVM
See [Logging in to Linux Instance Using Standard Login Method](https://intl.cloud.tencent.com/document/product/213/5436). You can also use other login methods that you are more comfortable with:
- [Logging in to Linux Instances via Remote Login Tools](https://intl.cloud.tencent.com/document/product/213/32502).
- [Logging into Linux Instance via SSH Key](https://intl.cloud.tencent.com/document/product/213/32501)

### Step 2: install vsftpd
1. Run the following command to install vsftpd:
```
yum install -y vsftpd
```
2. Run the following command to enable vsftpd autostart.
```
systemctl enable vsftpd
```
3. Run the following command to start the FTP service:
```
systemctl start vsftpd
```
4. Run the following command to check that the service has been started:
```
netstat -antup | grep ftp
```
If the following appears, the FTP service has been successfully started.
![](https://main.qcloudimg.com/raw/2a7abf80253a8469c9340878d89b452a.png)
By default, vsftpd has enabled the anonymous access mode. This mode allows you to log in to the FTP server without entering a username or password, but you cannot modify or upload files.


### Step 3: configure vsftpd<span id="user"></span>
1. Run the following command to create a Linux user (such as ftpuser) for the FTP service:
```
useradd ftpuser
```
2. Run the following command to set the password for ftpuser:
```
passwd ftpuser
```
After entering the password, press **Enter**. The password you entered will not be displayed by default. This document uses the password `tf7295TFY` as an example.
3. Run the following command to create a file directory (such as `/var/ftp/test`) for the FTP service:
```
mkdir /var/ftp/test
```
4. Run the following command to modify the directory permission:
```
chown -R ftpuser:ftpuser /var/ftp/test
```
5. Run the following command to open the `vsftpd.conf` file:
```
vim /etc/vsftpd/vsftpd.conf
```
6. Press **i** to switch to the edit mode. Select an FTP mode as needed and modify the `vsftpd.conf` configuration file.<span id="config"></span>
>! The FTP server can connect to the client in active or passive mode for data transmission. Due to the firewall settings of most clients and unobtainable real IPs, we recommend you to use the FTP **passive mode** as instructed below. To use the active mode, go to [Setting the FTP active mode](#port).
>
 1. Modify the following configuration parameters, set the login permissions for anonymous users and local users, set the path for storing the exceptional user list, and enable listening on IPv4 sockets.
```
anonymous_enable=NO
local_enable=YES
chroot_local_user=YES
chroot_list_enable=YES
chroot_list_file=/etc/vsftpd/chroot_list
listen=YES
```
  2. Add the pound sign (#) at the beginning of the following line to comment out `listen_ipv6=YES` and disable listening on IPv6 sockets.
```
#listen_ipv6=YES
```
  3. Add the following configuration parameters, enable the passive mode, set the working directory for local users after login, and set the port range that the CVM can use to transmit data.
```
local_root=/var/ftp/test
allow_writeable_chroot=YES
pasv_enable=YES
pasv_address=xxx.xx.xxx.xx # Replace xxx.xx.xxx.xx with the public IP address of your Linux CVM
pasv_min_port=40000
pasv_max_port=45000
```
7. Press **Esc** and enter **:wq** to save and close the file.
8. Run the following command to create and edit the `chroot_list` file.<span id="create"></span>
```
vim /etc/vsftpd/chroot_list
```
9. Press **i** to enter the edit mode. Enter one username per line. After the configuration is completed, press **Esc** and enter **:wq** to save and close the file.
If you do not need to set exceptional users, skip this step and directly enter **:wq** to close the file.
10. Run the following command to restart the FTP service:
```
systemctl restart vsftpd
```

### Step 4: configure security groups
After building the FTP service, configure **inbound rules** for the Linux CVM based on the actually used FTP mode. For more information, see [Adding Security Group Rules](https://intl.cloud.tencent.com/document/product/213/34272).
Most clients convert IP addresses in LANs. If you are using the FTP active mode, ensure that the client has obtained the real IP address. Otherwise, the client may fail to log in to the FTP server.
- Active mode: open the port 21.
- Passive mode: open the ports 21 and all ports ranging from `pasv_min_port` to `pasv_max_port` set in the [configuration file](#config), such as the ports 40000-45000 in this document.

### Step 5: verify the FTP service
You can use tools such as the FTP client software, browser, or file manager to verify the FTP server. This document uses the file manager of the client as an example.
1. Open an Internet Explorer on the client, choose **Tools** > **Internet Options**, and click the **Advanced** tab to modify the configuration based on the selected FTP mode.
 - Active mode: deselect **Passive FTP**.
 - Passive mode: select **Passive FTP**.
2. Open the PC where the client is installed, type the following address in the address box of the browser, and press **Enter**, as shown below:
```
ftp://CVM public IP address:21
```
![](https://main.qcloudimg.com/raw/40cef1738cb1d2fad07d2ef219822d2f.png)
3. In the pop-up window, enter the username and password configured in [Step 3](#user).
In this document, the username is `ftpuser`, and the password is `tf7295TFY`.
4. You can upload and download files after a successful login.


## Appendix
### Setting the FTP active mode<span id="port"></span>
To use the active mode, modify the following configurations and keep the default values for other configurations:
```
anonymous_enable=NO      # Forbid anonymous users to log in
local_enable=YES         # Allow local users to log in
chroot_local_user=YES    # Restrict all users to access only the root directory
chroot_list_enable=YES   # Enable the exceptional user list
chroot_list_file=/etc/vsftpd/chroot_list  # Specify the user list, in which the listed users are not restricted to access only the root directory
listen=YES               # Enable listening on IPv4 sockets
# Add the pound sign (#) at the beginning of the following line to comment out the following parameter
#listen_ipv6=YES         # Disable listening on IPv6 sockets
# Add the following parameters
allow_writeable_chroot=YES
local_root=/var/ftp/test # Set the working directory for local users after login
```
Press **Esc**and enter **:wq** to save and close the file. Go to [Step 8](#create) to configure vsftpd.

### Failing to upload files from an FTP client
#### Issue
The following error message is displayed when a file is uploaded over vsftpd to a Linux server.
```
553 Could not create file
```

#### Solution
1. Run the following command to check disk usage of the server.
```
df -h
```
 - If the disk space is insufficient, you cannot upload files. In this case, we recommend that you delete some unnecessary large files from the disk.
 - If the disk space is sufficient, go to the next step.
2. Run the following command to check whether you have the write permission to the FTP directory:
```
ls -l /home/test      
# Change `/home/test` to your actual FTP directory.
```
 - If `w` is not returned in the result, you do not have the write permission to the directory. In this case, go to the next step.
 - If `w` is returned in the result, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for further troubleshooting.
3. Run the following command to grant the write permission to the FTP directory
```
chmod +w /home/test 
# Change `/home/test` to your actual FTP directory.
```
4. Run the following command to check whether the write permission is successfully granted:
```
ls -l /home/test   
# Change `/home/test` to your actual FTP directory.
```
