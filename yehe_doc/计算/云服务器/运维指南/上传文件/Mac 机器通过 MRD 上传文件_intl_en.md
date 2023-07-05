## Scenario
Microsoft Remote Desktop (MRD) is a remote desktop software by Microsoft. This article describes how to use it on MacOS to upload files to a CVM with Windows Server 2012 R2 installed. 


## Prerequisites
- Download and install [Microsoft Remote Desktop for Mac](https://www.techspot.com/downloads/4698-microsoft-remote-desktop-for-mac.html).
- MRD supports MacOS 10.10 and above. Make sure you have a compatible OS.
- Purchased a Windows CVM.


## Directions
### Obtaining a CVM Public IP
Log in to [CVM Console](https://console.cloud.tencent.com/cvm/index) and note down the public IP address of your CVM instance on the instance list page, as shown in the following image:
![](https://main.qcloudimg.com/raw/59ce52615c467ad80bc4220425bf2b80.png)


### Uploading Files
1. Start MRD and click **Add Desktop**, as shown in the following image:
![](https://main.qcloudimg.com/raw/e69528d10e9a17dfa26119a090766c49.png)
2. The **Add Desktop** window appears. Follow the steps illustrated in the following image to select a folder to upload and establish a connection with your Windows CVM:
![](https://main.qcloudimg.com/raw/fc241ce8e4744bde57476ea823fcef72.png)
  1. In the **PC name** text field, input your CVM’s public IP.
  2. Click **Folders** to switch to the folder list view.
  3. Click <img src="https://main.qcloudimg.com/raw/89e7a3ff040849307cd1eb8bd878a2db.png" style="margin:-3px 0px">. In the pop-up window, select the folder to be uploaded. 
  4. After you finish, check your list of folders to upload and click **Add**.
  5. Leave other options as default and complete the process.
Your entry is saved, as shown in the following image:
![](https://main.qcloudimg.com/raw/1c0eff28aa68a7f02e8f295917bb603b.png)
4. Double click the newly added entry. Input your username and password for CVM and click **Continue**.
>
>- The default account for the Windows CVM is `Administrator`.
>- If you choose to log in with random password, please check it in the [Message Center](https://console.cloud.tencent.com/message).
>- If you have forgotten your password, please [reset the instance password](http://intl.cloud.tencent.com/document/product/213/16566).
>
5. Click **Continue** to establish the connection, as shown in the following image:
![](https://main.qcloudimg.com/raw/61b3d9566365183fcc1d92c2f6bc2e7b.png)
If the connection is successful, then the following page appears:
![](https://main.qcloudimg.com/raw/3d36c84ef12110a81879377f56a7e26c.png)
7. In the bottom-left corner, click <img src="https://main.qcloudimg.com/raw/20fd46098cf037eb003dc41f1f913313.png" style="margin:-3px 0px;"/> then **My Computer** to see a list of shared folders.
8. Double click a shared folder to open it. Copy desired local files to another drive on the Windows CVM to complete upload.
For example, copy **a.txt** to the C drive on Windows CVM.

### Downloading Files
To download files from the Windows CVM to your computer, copy desired files from the CVM to a shared folder.


