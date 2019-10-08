## Scenario
This document takes CentOS 7.2 64-bit system as an example to describe how to set up the FTP service on a Linux CVM with vsftpd as the FTP server and FileZilla as the client.

## Directions
### Install vsftpd
1. Log in to the CVM.
2. Execute the following command to install vsftpd.
``` 
yum install vsftpd -y
```

### Start the service
1. Execute the following command to start the service.
```
systemctl start vsftpd
```
2. Execute the following command to confirm whether the service has been started.
```
netstat -tunlp
```
If a message like the following is returned, it means that the vsftpd service has been started successfully.
![](//mc.qcloudimg.com/static/img/6cc74de5689106ce763be98bfe7f5d24/image.png)
3. Execute the following command on other computers connected to the Internet to install the telnet service.
```
yum -y install  telnet
```
4. Execute the following command on other computers that are connected to the Internet to test if the service has been started successfully .
```
telnet + CVM public IP address + 21
```
If a message like the following is returned, it means that the service has been started successful.
![](https://main.qcloudimg.com/raw/c28b93819a8fdd9e121e6b0702d098d4.png)

<span id = "jump">  </span>

### Configure vsftpd
1. Execute the following command to open the vsftpd configuration file.
```
vi /etc/vsftpd/vsftpd.conf
```
2. Press **i** or **Insert** to switch to edit mode and change `anonymous_enable=YES` in the file to `anonymous_enable=NO` as shown below:
![](//mc.qcloudimg.com/static/img/4e7770981eae42e7b16a2a5a7866a6a6/image.png)
3. Press **Esc**, enter **:wq**, save the file and return.

### Add FTP Users
1. Execute the following command to add the user `ftpuser1`.
``` 
useradd -m -d /home/ftpuser1 -s /sbin/nologin ftpuser1
```
2. Execute the following command to set the password for the user `ftpuser1`.
```
passwd ftpuser1
```
The user has been created and the user password has been set successfully as shown below:
![](https://main.qcloudimg.com/raw/eec9ba9d188bf8b82a846fed73e02b52.png)

## FAQs
### FTP client failed to read directory list or connection to server timed out
#### Problem Description
When locally using the FTP client to connect to the server, some users may encounter problems such as connection timeout and failure to read the directory list as shown below:
![](//mc.qcloudimg.com/static/img/eb7beaf8c5a6e683257e94dd754e3f25/image.jpg)
The problem occurs at the PASV command. The reason is that the FTP protocol conflicts with the network architecture of Tencent Cloud. The FTP client uses passive transmission mode by default, so it searches for the server's IP address to connect during the communication process. However, public IP of Tencent Cloud is not directly configured on ENI, so in passive mode the client cannot find a valid IP. The client can only find the private IP of the CVM. Since the private IP cannot communicate directly with the public network, the connection cannot be established.

#### Solution
1. Change the transmission mode of the client to active.
2.  If the network environment of the client requires passive mode, you need to add the following statements to the vsftpd configuration file when [configuring vsftpd](#jump) for the server:
```
pasv_address=XXX.XXX.XXX.XXX     //(Public IP)
pasv_enable=YES
pasv_min_port=1024
pasv_max_port=2048
```

### FTP client failed to upload files
#### Problem Description

In Linux environment, users get the following error message when uploading files with vsftpd.
```
553 Could not create file
```

#### Solution
1. Execute the following command to check the utilization of server disk space.
```
df -h
```
 - If there is not enough disk space, you will not be able to upload files. It is recommended to delete some large files.
 - If there is enough disk space, go to the next step.
2. Execute the following command to check if the FTP directory has the Write permission.
```
ls -l /home/test      
# /home/test is the FTP directory. Change it to your actual FTP directory.
```
 - If there is no `w` in the returned result, it means that the user does not have the permission to write to the directory. Please go to the next step.
 - If there is a `w` in the returned result, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).
3. Execute the following command to add the Write permission to the FTP directory.
```
chmod +w /home/test 
# /home/test is the FTP directory. Change it to your actual FTP directory.
```
4. Execute the following command to check whether the Write permission is added successfully.
```
ls -l /home/test   
# /home/test is the FTP directory. Change it to your actual FTP directory.
``` 




