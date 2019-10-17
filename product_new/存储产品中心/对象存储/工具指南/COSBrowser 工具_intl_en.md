## Feature Description
COSBrowser is a COS client tool that allows you to easily upload, download, and manage data through GUIs.

>- COSBrowser Desktop Edition (Windows/macOS/Linux) uses the system-configured proxy to connect to the internet. Please make sure that your proxy is configured properly or disable the proxy configuration if it fails to connect to the internet. To query the details, go to "Internet Options" on Windows, "Network Preferences" on macOS, or System Settings > Network > Network Proxy on Linux.
>- If you upload a file through this tool, an existing file with the same name will be overwritten. Detection of filename duplication is not supported.

## Download Links

| OS | System Requirements | Download Address |
|:---|:---|:---|
|Windows desktop version| Above Windows 7 32/64-bit or Windows Server 2008 R2 64-bit |[Windows](https://cos5.cloud.tencent.com/cosbrowser/releases/cosbrowser-setup-latest.exe)|
|macOS desktop version| Above macOS 10.13 |[macOS](https://cos5.cloud.tencent.com/cosbrowser/releases/cosbrowser-latest.dmg)|
|Linux desktop verison| GUI- and AppImage-enabled version |[Linux](https://cos5.cloud.tencent.com/cosbrowser/releases/cosbrowser-latest-linux.zip)|
|Android mobile version| Above Android 4.4 |[Android](https://sj.qq.com/myapp/detail.htm?apkName=com.qcloud.cos.client)|
|iOS desktop version Above iOS 11 |[iOS](https://apps.apple.com/cn/app/id1469323992)|

## Desktop Version

> COSBrowser Desktop Edition supports Windows, macOS, and Linux.

#### Software UI

![COSBrowser Desktop Edition](https://main.qcloudimg.com/raw/6b36f6090281ac7925544ac42bbef55c.png)

#### Login Instructions

  - **TencentCloud API key (SecretId/SecretKey)**: You can log in using your TencentCloud API key (SecretId and SecretKey; project key is not supported), which can be obtained on the [API Key Management](https://console.cloud.tencent.com/cam/capi) page in the CAM Console. After login, the key will be saved in **Historical Keys**.
  - **Historical Keys**: Click **Historical Keys** to view and use the TencentCloud API keys that have been successfully used to log in on the current computer.

## Mobile Version

#### Software UI

![COSBrowser Mobile Version](https://main.qcloudimg.com/raw/8cde524816485071348ff3d7aaca863f.png)

#### Login Instructions

COSBrowser Mobile Version supports the following two login methods:
  - **Login with WeChat**: If your Tencent Cloud account was created through WeChat, you can use your WeChat account to quickly log in to COSBrowser.
  - **Login with permanent key**: You can log in using your TencentCloud API key (SecretId and SecretKey; project key is not supported), which can be obtained on the [API Key Management](https://console.cloud.tencent.com/cam/capi) page in the CAM Console. After successful login, the account will keep logged in permanently.

> If your Tencent Cloud account was created with a QQ account, you can also use the login with WeChat method by selecting login with QQ on the redirected WeChat Mini Program screen.

## Directions

The following takes a Windows PC as an example, and the steps for other desktop and mobile operation systems are similar.

### Managing a File/Folder
#### Creating a Folder
1. Log in to COSBrowser. In the bucket module on the left, click a bucket to select it.
2. Click **Create a Folder**.
3. Enter the folder name and confirm.
>- The folder name can contain up to 255 digits, letters, and visible characters.
>- The folder name cannot contain special characters such as `\ / : * ? " | < >`.
>- `..` cannot be used as the folder name.
>- The folder cannot be renamed, so name it carefully.

#### Uploading a File/Folder
In the specified bucket or directory, click **Upload File** or **Upload Folder** and select the file or folder to be uploaded.
> COSBrowser Mobile Version only supports uploading images and videos.

#### Downloading a File/Folder
1. In the specified bucket or directory, select the file or folder to be downloaded.
2. Click **Download** to download them in the default download method.
3. You can also select **Advanced Download** to configure the download options.
![Download a folder](https://main.qcloudimg.com/raw/e57f4a12cfce6c97ddc5c27d8f25cf4b.jpg)
> COSBrowser Mobile Version does not have **Advanced Download** mode and does not support downloading folders.

#### Copying and Pasting a File/Folder
1. In the specified bucket or directory, select the file or folder to be copied and click **Copy**.
2. In the bucket or directory where you want to paste the file or folder, click **Paste**.
>- Copy-and-paste is not supported between public cloud regions and finance cloud regions.
>- If the source address and destination address of the file to be copied are the same, the file with the same name will be renamed by default; if the addresses are different, the file with the same name will be overwritten.
>- COSBrowser Mobile Version does not support copying and pasting folders.

#### Renaming a File
1. In the specified bucket or directory, select the file to be renamed and click **Rename**.
2. Enter a new file name.
> Folders cannot be renamed.

#### Deleting a File/Folder
In the specified bucket or directory, select the file or folder to be deleted and click **Delete**.
>? You can select multiple files/folders and delete them in batches.

### More Operations
#### General Settings
Select **Settings** > **General** to enter the COSBrowser settings page where you can modify the general configurations, such as language, server domain name, and use of HTTPS.

#### Upload/Download Parameter Configuration
- File concurrence: This sets the number of concurrent tasks for file upload/download. Excessive tasks will enter the waiting queue and be executed after the first tasks are completed.
- Part concurrence: This sets the number of parts for file upload/download.
- Retries on failure: This sets the number of retries on failure for file upload/download.

## Change Log

Desktop Version change log: [changelog](https://github.com/tencentyun/cosbrowser/blob/master/changelog.md)
Mobile Version change log: [changelog_mobile](https://github.com/tencentyun/cosbrowser/blob/master/changelog_mobile.md)

## Feedback and Suggestions

If you have any questions or suggestions during the use of COSBrowser, please feel free to give us your feedback:
- Desktop Version: [issues](https://github.com/tencentyun/cosbrowser/issues)
- Mobile Version: [issues_mobile](https://support.qq.com/embed/phone/67467)

