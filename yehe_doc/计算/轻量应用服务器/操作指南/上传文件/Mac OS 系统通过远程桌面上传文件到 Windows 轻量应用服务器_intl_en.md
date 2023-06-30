## Overview
Microsoft Remote Desktop (MRD) is a remote desktop software developed by Microsoft. This document describes how to use it on macOS to upload files to a Lighthouse instance with Windows Server 2012 R2 installed. 

## Prerequisites
- You have downloaded and installed MRD on your local computer. Go to [Microsoft Remote Desktop for Mac Beta](https://install.appcenter.ms/orgs/rdmacios-k2vy/apps/microsoft-remote-desktop-for-mac/distribution_groups/all-users-of-microsoft-remote-desktop-for-mac) to download and install it.
- MRD supports macOS 10.10 and later versions. Make sure your operating system is compatible.
- You have obtained the Lighthouse instance admin account and password.
	- The default admin account of a Windows Lighthouse instance is `Administrator`.
	- If you forgot the login password, you can [reset it](https://intl.cloud.tencent.com/document/product/1103/41553).

## Directions
### Obtaining public IP
Log in to the [Lighthouse console](https://console.cloud.tencent.com/lighthouse/instance/index) and get the public IP of the target Lighthouse instance on the **Instances** page.

### Uploading files
1. Start MRD and click **Add Desktop**, as shown below:
![](https://main.qcloudimg.com/raw/e69528d10e9a17dfa26119a090766c49.png)
2. In the **Add Desktop** pop-up window, follow the steps illustrated in the following image to select a folder to upload and establish a connection with your Windows instance.
![](https://main.qcloudimg.com/raw/fc241ce8e4744bde57476ea823fcef72.png)
  1. In the **PC name** text field, enter the public IP address of your Lighthouse instance.
  2. Click **Folders** to redirect to the folder list.
  3. Click <img src="https://main.qcloudimg.com/raw/89e7a3ff040849307cd1eb8bd878a2db.png" style="margin:-3px 0px"> in the lower-left corner and select the folder to be uploaded in the pop-up window.
  4. Check your list of folders to upload and click **Add**.
  5. Retain the default settings for the other options and establish the connection.
Your entry has now been saved, as shown below:
![](https://main.qcloudimg.com/raw/1c0eff28aa68a7f02e8f295917bb603b.png)
4. Double-click the new entry. Enter your username and password for the Lighthouse instance and click **Continue**.
5. In the pop-up window, click **Continue** to establish the connection, as shown below:
![](https://main.qcloudimg.com/raw/61b3d9566365183fcc1d92c2f6bc2e7b.png)
If the connection is successful, the following page will appear:
![](https://qcloudimg.tencent-cloud.cn/raw/09da9b26eb5ec4475ffe266e2761cf03.png)
7. Click <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin:-3px 0px"> in the lower-left corner and select **My Computer** to see a list of shared folders as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/30eb7cddd803d656e926130bae920f51.png)
8. Double-click a shared folder to open it. Copy desired local files to another drive of the Windows Lighthouse instance.
For example, copy the file A from the folder to the C drive of the Windows Lighthouse instance.

### Downloading files
To download files from the Windows Lighthouse instance to your computer, you only need to copy desired files from the instance to a shared folder.

