## Scenario
This document uses FileZilla as an example to describe how to set up the FTP service on a Windows CVM. You can also get images from the service marketplace to skip the installation and configuration part. For details, please go to [Cloud Marketplace] (https://market.cloud.tencent.com/list?cid=64).

## Downloading File
 FileZilla is a fast, reliable, cross-platform software which supports FTP, FTPS and SFTP. It has a graphical user interface (GUI) and many features. It is easy to use and supports multiple protocols.
 Click [here](https://filezilla-project.org/download.php?type=server) to download FileZilla Server for Windows. Click [here](https://filezilla-project.org/download.php?type=client) to download FileZilla Client for Windows.

## Directions

1. Log in to the CVM.
2. Download and run the FileZilla Server installer.
3. Read the license agreement and click **I Agree**.
4. Select the type of install (use the default) and click **Next** as shown below:
![](https://main.qcloudimg.com/raw/8d17fe17de20eb21f7cc8bc58d821037.png)
5. Select the install location and click **Next**.
6. <span id="step2">Select the startup mode of FileZilla Server, choose the port, and click **Next** as shown below:</span>
Normally you can select the default startup mode and a port that is not occupied.
 ![](https://main.qcloudimg.com/raw/c97294110f187db619e50097bb614f0e.png)
7. Click **Install** and start FileZilla Server.
8. In the pop-up window, fill in the following information and click **Connect** to connect to FileZilla server as shown below:
![](https://main.qcloudimg.com/raw/05393c6c6519c9d052dc87f6ff09af4c.png)
 - Host: enter 127.0.0.1
 - Port: fill in the port you configure in [Step 6] (#step2) such as 14147.
9. In the FileZilla Server window, click <img src="https://main.qcloudimg.com/raw/6eaffea83cd46f08300a27dcdf1c62a1.png" style="margin: 0;"> to open the Users window.
10. In the Users window, click **Add**, and you will see an Add User Account dialog box as shown below:
![](https://main.qcloudimg.com/raw/2ed9ccaeee7a4a4b3278f50d5c8b30ff.png)
11. Enter a user name in the dialogue box and click **OK**.
For example, you can enter “tencent-qcloud”.
12. In the User window, select **Password**, set a password for the new user, and click **OK** as shown below:
![](https://main.qcloudimg.com/raw/4d0b34e03796e5e1aca0c9ac97d60c14.png)
13. In the pop-up window, click **OK**.
14. In the Shared folders column, click **Add** to add a user directory as shown below:
![](https://main.qcloudimg.com/raw/e5b0accf2129a6f54278487a6aa2a8ba.png)
15. Select the FTP resource directory and click **OK** as shown below:
For example, select the Tencent-Qcloud directory as the FTP resource directory and place a `Welcome to Tencent Cloud Server.txt` file in the directory for [Testing the FTP Service](#checkFTPService).
![](//mc.qcloudimg.com/static/img/abfe5bdfd1011f723b4e5d75e4b3de36/image.jpg)
16. In the Shared Folders column, set the permissions for user's operations on the FTP resource directory as shown below:
![](https://main.qcloudimg.com/raw/fe1b57c00ef8e91461a814d94bec2238.png)
17. Click **OK** to complete the setup of the FileZilla FTP service.

<sapn id="checkFTPService"></span>
## Testing the FTP Service

1. On your local PC, install and open the FileZilla client.
2. Enter the public IP address of the CVM, the FTP username and the password, and click **Quickconnect**. You will be able to see the directory the FileZilla server shares with the user and the "Welcome to Tencent Cloud Server.txt" file placed in the directory. See the figure below:
![](https://main.qcloudimg.com/raw/ff94910a171be385bf8aaa7059f9c560.jpg)
3. Switch to the FileZilla server and you will be able to monitor the connection with the FileZilla client as shown below:
![](https://main.qcloudimg.com/raw/7856575e8d7a57e1c72ad5a867ac46b8.jpg)



