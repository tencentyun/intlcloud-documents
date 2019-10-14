## Scenario
This document uses FileZilla as an example to describe how to set up the FTP service on a Windows CVM. You can also get images from the service marketplace to skip the installation and configuration part. For details, please go to [Cloud Marketplace](https://market.cloud.tencent.com/list?cid=64).

## Downloading File
 FileZilla is a fast, reliable, cross-platform software which supports FTP, FTPS and SFTP. It has a graphical user interface (GUI) and many features. It is easy to use and supports multiple protocols.
 Click [here](https://filezilla-project.org/download.php?type=server) to download FileZilla Server for Windows. Click [here](https://filezilla-project.org/download.php?type=client) to download FileZilla Client for Windows.

## Directions

1. Log in to the CVM.
2. Download and run the FileZilla Server installer.
3. Read the license agreement and click **I Agree**.
4. Select the type of install (use the default) and click **Next** as shown below:
![](https://main.qcloudimg.com/raw/96537179989adaae28ed43987910763d.png)
5. Select the install location and click **Next**.
6. <span id="step2">Select the startup mode of FileZilla Server, choose the port, and click **Next** as shown below:</span>
Normally you can select the default startup mode and a port that is not occupied.
 ![](https://main.qcloudimg.com/raw/9336caf9f56b4cd84be68b0bf108bb9b.png)
7. Click **Install** and start FileZilla Server.
8. In the pop-up window, fill in the following information and click **Connect** to connect to FileZilla server as shown below:
![](https://main.qcloudimg.com/raw/70e43cd78e7b52b2a3f7db51341fc011.png)
 - Host: enter 127.0.0.1
 - Port: fill in the port you configure in [Step 6] (#step2) such as 14147.
9. In the FileZilla Server window, click <img src="https://main.qcloudimg.com/raw/6eaffea83cd46f08300a27dcdf1c62a1.png" style="margin: 0;"> to open the Users window.
10. In the Users window, click **Add**, and you will see an Add User Account dialog box as shown below:
![](https://main.qcloudimg.com/raw/192ce19ec011d7b4848146a3a4b6a1e6.png)
11. Enter a user name in the dialogue box and click **OK**.
For example, you can enter “tencent-qcloud”.
12. In the User window, select **Password**, set a password for the new user, and click **OK** as shown below:
![](https://main.qcloudimg.com/raw/b456b2cddb1a44806d0a2c1fc5377c6a.png)
13. In the pop-up window, click **OK**.
14. In the Shared folders column, click **Add** to add a user directory as shown below:
![](https://main.qcloudimg.com/raw/567e7c0bec0d9d69749835767cc6697d.png)
15. Select the FTP resource directory and click **OK** as shown below:
For example, select the Tencent-Qcloud directory as the FTP resource directory and place a `Welcome to Tencent Cloud Server.txt` file in the directory for [Testing the FTP Service](#checkFTPService).
![](https://main.qcloudimg.com/raw/1df0c3ea3d63a1dcb671137b0b475f41.png)
16. In the Shared Folders column, set the permissions for user's operations on the FTP resource directory as shown below:
![](https://main.qcloudimg.com/raw/43fae3ae7e4e0f7d63259d1068351cd2.png)
17. Click **OK** to complete the setup of the FileZilla FTP service.

<sapn id="checkFTPService"></span>
## Testing the FTP Service

1. On your local PC, install and open the FileZilla client.
2. Enter the public IP address of the CVM, the FTP username and the password, and click **Quickconnect**. You will be able to see the directory the FileZilla server shares with the user and the "Welcome to Tencent Cloud Server.txt" file placed in the directory. See the figure below:
![](https://main.qcloudimg.com/raw/875b51c3d89cc358e492a240caac1ce2.png)
3. Switch to the FileZilla server and you will be able to monitor the connection with the FileZilla client as shown below:
![](https://main.qcloudimg.com/raw/c2b9042feeded36ac872db7f9aee8062.png)



