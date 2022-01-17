This document describes how to apply for the SDKs of voice services for Tencent Cloud GME.

## Creating Services

<span id="test1"></span>

### Creating an application

1. Log in to the [GME console](https://console.cloud.tencent.com/gamegme) and click **Service Management** on the left sidebar to go to the **Service Management** page.
2. Click **Create Application**, enter the application information, and enable the services as needed.
![](https://main.qcloudimg.com/raw/fe3666053156cd53c29053b851ea5b6f.png)
3. Enter the application information.
![](https://main.qcloudimg.com/raw/0d5da346fcbbad3b938fd86bd707087f.png)
   - Application Name: enter the application name, which will be displayed in the application list.
   - Project: **DEFAULT PROJECT** is selected by default. You can also select the created projects. For how to create a project, see [Project Management](https://intl.cloud.tencent.com/document/product/378/34726).
   - Tag: click **Add** to add tags. For how to create a tag, see [Tag Management](#test).
4. Enable or disable the **Real-time Voice Service**.
 **Real-time Voice Service** is billed by voice duration. You can enable it as needed and purchase in the [Purchase Page](https://intl.cloud.tencent.com/document/product/607/36276).
![](https://main.qcloudimg.com/raw/6360fc755f9b7f3893064b719a71da31.png)
5. Enable or disable the **Speech-to-Text Service**.
You can enable the **Speech-to-Text Service** as needed and select the supported language mode. The two modes have different prices. For details, see [Billing Rules](https://intl.cloud.tencent.com/document/product/607/36276).
![](https://main.qcloudimg.com/raw/09e232363c701db84059b887626aa5ed.png)
7. Click **OK**.



## Service Settings

After being created, the application will be displayed in the application list. Click **Set** on the right side of an application to go to the details page.
![](https://main.qcloudimg.com/raw/2b91bfdb40f81c3a3aed498ce8077961.png)

### Setting application

Click **Modify** in the **Application Info** section to modify the corresponding information.
![](https://main.qcloudimg.com/raw/12391b6b0ca03f79348cd390d749f39e.png)

### Enabling/Disabling service

Click **Modify** in the **Real-time Voice Service** section to enable or disable the service.
![](https://main.qcloudimg.com/raw/fa014623f58740b655c01f2bb726301b.png)


## Key Parameters

In **Authentication Info**, you can obtain the AppID and permission key required for the SDK voice services.
![](https://main.qcloudimg.com/raw/a51de920cec5e748e3fb9b6b42a02a7c.png)

>?
>
>- The permission key here will be used as a parameter when accessing the SDK. 
>- Change of the key on this page takes effect within 15 minutes to 1 hour. It is not recommended to change it frequently.
>- Only the account that creates the game, root account, and global collaborators can **reset the key**.
>- For more information about authentication, see [Authentication Key](https://intl.cloud.tencent.com/document/product/607/12218).

To use the demo, you need to replace the AppID of the Tencent Cloud test account in the corresponding interface of the demo with the AppID you obtained in the console, and change the permission key of voice chat in the GetAuthBuffer function of AVChatViewController.


## API Documentation

Depending on the platform or engine you are using, you can access the SDK by referring to the following documentations:

Documents for Unity:
[Project Configuration](https://intl.cloud.tencent.com/document/product/607/10783)
[API Documentation](https://intl.cloud.tencent.com/document/product/607/15228)

Documents for Unreal Engine:
[Project Configuration](https://intl.cloud.tencent.com/document/product/607/17025)
[API Documentation](https://intl.cloud.tencent.com/document/product/607/15231)

Documents for Cocos2D:
[Project Configuration](https://intl.cloud.tencent.com/document/product/607/15216)
[API Documentation](https://intl.cloud.tencent.com/document/product/607/15218)

Documents for Windows:
[Project Configuration](https://intl.cloud.tencent.com/document/product/607/19068)
[API Documentation](https://intl.cloud.tencent.com/document/product/607/15232)

Documents for iOS:
[Project Configuration](https://intl.cloud.tencent.com/document/product/607/15219)
[API Documentation](https://intl.cloud.tencent.com/document/product/607/15221)

Documents for Android:
[Project Configuration](https://intl.cloud.tencent.com/document/product/607/15203)
[API Documentation](https://intl.cloud.tencent.com/document/product/607/15210)

Documents for Mac:
[Project Configuration](https://intl.cloud.tencent.com/document/product/607/18617)
[API Documentation](https://intl.cloud.tencent.com/document/product/607/18739)

Documents for HTML5:
[Project Configuration](https://intl.cloud.tencent.com/document/product/607/30261)
[API Documentation](https://intl.cloud.tencent.com/document/product/607/30263)

<span id="test"></span>

## Tag Management

If you need to create tags when [creating an application](#test1), you can follow the directions below:

1. In the **Application Info** page when creating an application, you can click [Tag Management](https://console.cloud.tencent.com/tag/taglist) to go to the **Tag List** page.
   ![](https://main.qcloudimg.com/raw/859fdef317b03d96149252ea8a27ee4e.png)
2. Click **Create** and enter the related information in the **Add tag** window.
   ![](https://main.qcloudimg.com/raw/2e09f0b203819f57908ce834c7c5939f.png)
3. Click **OK**.
