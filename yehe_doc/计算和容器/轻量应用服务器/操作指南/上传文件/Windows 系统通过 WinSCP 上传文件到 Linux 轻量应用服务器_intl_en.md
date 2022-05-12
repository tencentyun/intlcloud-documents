## Overview
WinSCP is an open-source graphical SFTP client that uses SSH in Windows environment and supports SCP protocol. Its main feature is to copy files securely between the local and remote computers. Unlike uploading codes via FTP, you can directly use your instance account in WinSCP to access the instance without any additional configuration.

## Prerequisites
- WinSCP has been downloaded and installed on the local computer. [Download the latest WinSCP](http://winscp.net/eng/docs/lang:chs).
- You have obtained the Lighthouse instance admin account and password.
 - The default admin username of a Linux Lighthouse instance is `root`, and that of an Ubuntu instance is `ubuntu`. You can also customize the username.
 - If you forgot your password, you can [reset it](https://intl.cloud.tencent.com/document/product/1103/41553).

## Directions

### Logging in to WinSCP

1. Open WinSCP, and the "WinSCP Login" box pops up, as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/91c1ef2566ea60df7d9cee3f36b3e8b0.png)
2. Configure the following parameters:
 - **Protocol**: Either SFTP or SCP.
 - **Hostname**: Lighthouse instance public IP, which can be viewed in the [Lighthouse console](https://console.cloud.tencent.com/lighthouse/instance/index).
 - **Port**: 22 by default.
 - **Username**: Lighthouse instance system username.
 - **Password**: Password of the Lighthouse instance system username.
3. Click **Login** to enter the **WinSCP** file transfer window as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/ff4497378f2faf81816ce2f34ce75fd1.png)

### Uploading files
1. In the right pane of the "WinSCP" file transfer interface, select the directory where the files are to be stored on the server, such as "/user".
2. In the left pane, select the directory where the files are stored on the local computer, such as `F:\SSL certificate\Nginx`, and then select the files to be transferred.
3. In the left menu, click **Upload** as shown below:
![Upload](https://qcloudimg.tencent-cloud.cn/raw/94607a5024f8900e92f26403e5f68c6c.png)
4. In the "Upload" box that pops up, confirm the files to be uploaded and the remote directories, and click **OK** to upload the files from the local computer to the Lighthouse instance.

### Downloading files
1. In the left pane of the "WinSCP" file transfer page, select the local computer directory to store the downloaded files, such as "F:\SSL certificate\Nginx".
2. In the right pane, select the directory where the files locate, such as `/user`, and then select the file to be transferred.
3. In the right menu, click **Download** as shown below:
![Download](https://qcloudimg.tencent-cloud.cn/raw/71b400fac63f032c582183c76d188f42.png)
4. In the "Download" box that pops up, confirm the files to be downloaded and the remote directories, and click **OK** to download the files from the Lighthouse instance to the local computer.



