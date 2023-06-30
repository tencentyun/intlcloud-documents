## Overview
WinSCP is an open-source graphical SFTP client that uses SSH in Windows environment and supports SCP protocol. Its main feature is to copy files securely between the local and remote computers. Unlike uploading codes via FTP, you can directly use your CVM account in WinSCP to access the CVM without any additional configuration.

## Prerequisites
WinSCP has been downloaded and installed on the local computer. [Download the latest WinSCP](http://winscp.net/eng/docs/lang:chs).

## Directions

### Logging in to WinSCP

1. Open WinSCP, and the "WinSCP Login" box pops up.
2. Configure the following parameters:
 - **Protocol**: either SFTP or SCP.
 - **Host Name**: Public IP of the CVM. Log in to [CVM console](https://console.cloud.tencent.com/cvm) to view the Public IP of the CVM.
 - **Port**: 22 by default.
 - **Username**: Username for logging in to the CVM.
 <dx-alert infotype="explain" title="">
  The default admin username is `root` for Linux instances and `ubuntu` for Ubuntu instances. If you use Ubuntu, configure as instructed in [How can I log in to an instance running Ubuntu as root?](https://intl.cloud.tencent.com/document/product/213/17278) and then log in as `root`.
 </dx-alert>
 - **Password**: Password of the username.
	 - If you choose to log in with a random password, you can obtain the password at the [Message Center](https://console.cloud.tencent.com/message).
	 - If you forgot your password, please [reset the instance password](https://intl.cloud.tencent.com/document/product/213/16566).
3. Click **Log In** to enter the "WinSCP" file transfer page.

### Uploading files
1. In the right pane of the "WinSCP" file transfer page, select the directory where the files are to be stored on the server, such as `/user`.
2. In the left pane, select the directory where the files are stored on the local computer, such as `F:\SSL certificate\ Nginx`, and then select the files to be transferred.
3. In the left menu, click **Upload**.
4. In the "Upload" box that pops up, confirm the files to be uploaded and the remote directories, and click **OK** to upload the files from the local computer to the CVM.

### Downloading files
1. In the left pane of the "WinSCP" file transfer page, select the local computer directory to store the downloaded files, such as "F:\SSL certificate\ Nginx".
2. In the right pane, select the directory where the files locate, such as `/user`, and then select the file to be transferred.
3. In the right menu, click **Download**.
4. In the "Download" box that pops up, confirm the files to be downloaded and the remote directories, and click **OK** to download the files from the CVM to the local computer.



