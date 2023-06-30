## Overview
Microsoft Remote Desktop (MRD) is a remote desktop software developed by Microsoft. This document describes how to use it on MacOS to upload files to a Tencent Cloud CVM with Windows Server 2012 R2 installed. 

## Prerequisites
- You have downloaded and installed MRD on your local computer. The following operations use Microsoft Remote Desktop for Mac as an example. Microsoft stopped providing a link to download the Remote Desktop client in 2017. Currently, its subsidiary HockeyApp is responsible for releasing the beta client. Go to [Microsoft Remote Desktop Beta](https://install.appcenter.ms/orgs/rdmacios-k2vy/apps/microsoft-remote-desktop-for-mac/distribution_groups/all-users-of-microsoft-remote-desktop-for-mac) to download a Beta version.
- MRD supports MacOS 10.10 and later versions. Make sure your operating system is compatible.
- You have purchased a Windows CVM.

## Directions
### Obtaining a public IP
Log in to the [CVM console](https://console.cloud.tencent.com/cvm/index), navigate to the **Instances** page, and record the public IP of the CVM to which you want to upload files, as shown below:
![](https://main.qcloudimg.com/raw/59ce52615c467ad80bc4220425bf2b80.png)

### Uploading files
1. Start MRD and click **Add Desktop**, as shown below:
![](https://main.qcloudimg.com/raw/e69528d10e9a17dfa26119a090766c49.png)
2. In the **Add Desktop** pop-up window, follow the steps below to select the folder to upload and establish a connection with your Windows CVM.
![](https://main.qcloudimg.com/raw/fc241ce8e4744bde57476ea823fcef72.png)
  1. In the **PC name** text field, enter the public IP address of your CVM.
  2. Click **Folders** to redirect to the folder list.
  3. Click <img src="https://main.qcloudimg.com/raw/89e7a3ff040849307cd1eb8bd878a2db.png" style="margin:-3px 0px"> in the lower-left corner and select the folder to be uploaded in the pop-up window.
  4. Check your list of folders to upload and click **Add**.
  5. Retain the default settings for the other options and establish the connection.
Your entry has now been saved, as shown below:
![](https://main.qcloudimg.com/raw/1c0eff28aa68a7f02e8f295917bb603b.png)
4. Double-click the new entry. Input your username and password for CVM and click **Continue**.
>?
>- The default account for the Windows CVM is `Administrator`.
>- If you use a system default password to log in to the instance, go to the [Message Center](https://console.cloud.tencent.com/message) to obtain the password first.
>- If you have forgotten your password, please [reset the instance password](http://intl.cloud.tencent.com/document/product/213/16566).
>
5. In the pop-up window, click **Continue** to establish the connection, as shown below:
![](https://main.qcloudimg.com/raw/61b3d9566365183fcc1d92c2f6bc2e7b.png)
If the connection is successful, the following page will appear:
![](https://main.qcloudimg.com/raw/5a524210acd13624af7263b6de3aea54.png)
6. Click <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin:-3px 0px"> in the lower-left corner and select **My Computer** to see a list of shared folders.
7. Double click a shared folder to open it. Copy desired local files to another drive of the Windows CVM.
For example, copy the A file under the folder to the C drive of Windows CVM.

### Downloading files
To download files from the Windows CVM to your computer, you only need to copy desired files from the CVM to a shared folder.


