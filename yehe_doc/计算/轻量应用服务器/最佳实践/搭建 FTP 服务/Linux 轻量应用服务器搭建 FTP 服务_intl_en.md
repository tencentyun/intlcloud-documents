## Overview
Very Secure FTP Daemon (vsftpd) is the default FTP server for most Linux distributions. This document describes how to use vsftpd to set up the FTP service on a Linux Lighthouse instance on CentOS 7.6 64-bit.

## Software
The following software programs are used to build the FTP service:
- Linux: CentOS 7.6 system image.
- vsftpd: vsftpd 3.0.2.


## Directions
### Step 1. Log in to the Lighthouse instance
You can log in to the Linux instance via [WebShell](https://intl.cloud.tencent.com/document/product/1103/41523) or [other methods](https://intl.cloud.tencent.com/document/product/1103/41388).


### Step 2. Install vsftpd
1. Run the following command to install vsftpd.
```
sudo yum install -y vsftpd
```
2. Run the following command to automatically start vsftpd upon system startup.
```
sudo systemctl enable vsftpd
```
3. Run the following command to start the FTP service.
```
sudo systemctl start vsftpd
```
4. Run the following command to check that the service has been started.
```
sudo netstat -antup | grep ftp
```
If the following information appears, the FTP service has been started.
![](https://main.qcloudimg.com/raw/86f1992cc036513bc475c859cca90663.png)
By default, the anonymous access mode is enabled in vsftpd. You can log in to the FTP server without entering a username or password. However, you do not have permissions to modify or upload files in this login mode.


### Step 3. Configure vsftpd[](id:user)
1. Run the following command to create a user (such as `ftpuser`) for the FTP service:
```
sudo useradd ftpuser
```
2. Run the following command to set the password for `ftpuser`.
```
sudo passwd ftpuser
```
After entering the password, press **Enter** to confirm it. The password is hidden by default.
3. Run the following command to create a file directory (such as `/var/ftp/test`) for the FTP service.
```
sudo mkdir /var/ftp/test
```
4. Run the following command to modify the directory permission.
```
sudo chown -R ftpuser:ftpuser /var/ftp/test
```
5. Run the following command to open the `vsftpd.conf` file.
```
sudo vim /etc/vsftpd/vsftpd.conf
```
6. Press **i** to switch to the edit mode. Select an FTP mode as needed and modify the `vsftpd.conf` configuration file.[](id:config)
<dx-alert infotype="notice" title="">
The FTP server can connect to the client in either active or passive mode for data transmission. Due to the firewall settings of most clients and the fact that the actual IP address cannot be obtained, we recommend that you use the **passive mode** to set up the FTP service. The following modification uses the passive mode as an example. To use the active mode, see [Setting the FTP active mode](#port).
</dx-alert>
 1. Modify the following configuration parameters to set login permissions for anonymous and local users, set the path for storing the exceptional user list, and enable listening on IPv4 sockets.
```
anonymous_enable=NO
local_enable=YES
chroot_local_user=YES
chroot_list_enable=YES
chroot_list_file=/etc/vsftpd/chroot_list
listen=YES
```
  2. Add the pound sign (`#`) at the beginning of the following line to comment out `listen_ipv6=YES` and disable listening on IPv6 sockets.
```
#listen_ipv6=YES
```
  3. Add the following configuration parameters to enable the passive mode, set the directory where local users reside after login, and set the port range for transmitting data by the CVM.
```
local_root=/var/ftp/test
allow_writeable_chroot=YES
pasv_enable=YES
pasv_address=xxx.xx.xxx.xx # Replace xxx.xx.xxx.xx with the public IP address of your Lighthouse instance
pasv_min_port=40000
pasv_max_port=45000
```
7. Press **Esc** and enter **:wq** to save and close the file.
8. Run the following command to create and edit the `chroot_list` file.<span id="create"></span>
```
sudo vim /etc/vsftpd/chroot_list
```
9. Press **i** to enter the edit mode and enter usernames. Note that each username occupies one line. After finishing the configuration, press **Esc** and enter **:wq** to save and close the file.
If you do not need to set exceptional users, skip this step by entering **:wq** to close the file.
10. Run the following command to restart the FTP service.
```
sudo systemctl restart vsftpd
```

### Step 4. Configure the security group
After setting up the FTP service, you need to open the corresponding ports of the Linux Lighthouse instance according to the FTP mode actually used. For more information, see [Adding firewall rules](https://intl.cloud.tencent.com/document/product/1103/41393?has_map=1#.E6.B7.BB.E5.8A.A0.E9.98.B2.E7.81.AB.E5.A2.99.E8.A7.84.E5.88.99).
Most clients convert IP addresses in LANs. If you are using the FTP active mode, ensure that the client has obtained the actual IP address. Otherwise, the client may fail to log in to the FTP server.
- Active mode: Open port 21.
- Passive mode: Open port 21 and all ports ranging from `pasv_min_port` to `pasv_max_port` set in the [configuration file](#config), such as ports 40000 to 45000 in this document.

### Step 5. Verify the FTP service
You can use tools such as the FTP client software, browser, or file manager to verify the FTP server. This document uses the file manager of the client as an example.
1. Open Internet Explorer on the client, choose **Tools** > **Internet Options**, and click the **Advanced** tab. Make the following changes based on the selected FTP mode.
 - Active mode: Deselect **Passive FTP**.
 - Passive mode: Select **Passive FTP**.
2. Open the computer where the client is installed and enter the following path in the search box:
```
ftp://Lighthouse instance public IP:21
```
![](https://qcloudimg.tencent-cloud.cn/raw/da9f2671d485fdcaf14239caf408444f.png)
3. On the login page that appears, enter the username and password set in [Configure vsftpd](#user).
4. You can upload and download files after a successful login.


## Appendix
### Setting FTP active mode[](id:port)
To use the active mode, modify the following configuration parameters and leave others as their defaults:
```
anonymous_enable=NO      # Forbid anonymous users to log in
local_enable=YES         # Allow local users to log in
chroot_local_user=YES    # Restrict all users to access only the root directory
chroot_list_enable=YES   # Enable the exceptional user list
chroot_list_file=/etc/vsftpd/chroot_list  # Specify the user list, in which the listed users are not restricted to access only the root directory
listen=YES               # Enable listening on IPv4 sockets
# Add the pound sign (#) at the beginning of the following line to comment it out
#listen_ipv6=YES         # Disable listening on IPv6 sockets
# Add the following parameters
allow_writeable_chroot=YES
local_root=/var/ftp/test # Set the directory where local users reside after login
```
Press **Esc** and enter **:wq** to save and close the file. After that, proceed to [Step 8](#create) of “Step 3. Configure vsftp”.

### FTP client failure to upload file
#### Problem
In the Linux environment, users encounter the following error message when uploading files with vsftpd.
```
553 Could not create file
```

#### Solution
1. Run the following command to check the disk space utilization of the server.
```
df -h
```
 - If the disk space is insufficient, you cannot upload files. In this case, we recommend you delete some unnecessary large files from the disk.
 - If the disk space is sufficient, proceed to the next step.
2. Run the following command to check whether you have the write permission to the FTP directory.
```
ls -l /home/test      
# Here, `/home/test` indicates the FTP directory. Replace it with your actual FTP directory.
```
 - If `w` is not returned in the result, you don't have the write permission to the directory. In this case, proceed to the next step.
 - If `w` is returned in the result, [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category) for assistance.
3. Run the following command to grant the write permission to the FTP directory.
```
sudo chmod +w /home/test 
# Here, `/home/test` indicates the FTP directory. Replace it with your actual FTP directory.
```
4. Run the following command to check whether the write permission is successfully granted:
```
ls -l /home/test   
# Here, `/home/test` indicates the FTP directory. Replace it with your actual FTP directory.
```

