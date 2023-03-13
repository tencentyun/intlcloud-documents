This document describes how to create an application and activate the services.

## Creating an Application

[](id:test1)

1. Log in to the [GME console](https://console.intl.cloud.tencent.com/gamegme) and click **Service Management** in the left sidebar to go to the “Service management” page.
2. On this page, click **Create application**.
![](https://qcloudimg.tencent-cloud.cn/raw/f687244df3c633d9a873c58aec4bf864.png)
3. Complete the application information.
  ![](https://qcloudimg.tencent-cloud.cn/raw/7fac1c705952f11b994e4769b964d803.png)
   - Application name: Enter the application name, which will be displayed in the application list.
   - Project: A default project is selected. You can also select a project that you created. For details, see [Project Management - Create project](https://www.tencentcloud.com/zh/document/product/378/34726#.E6.96.B0.E5.BB.BA.E9.A1.B9.E7.9B.AE).
   - Tag: Click **+Add** to add tags. For more information, see [Tag Management](#test).
4. Enable or disable desired services based on your needs.
   - Enable or disable **Real-time Voice Chat**.
    Voice Chat is billed by voice duration. You can enable it as needed.
   ![](https://qcloudimg.tencent-cloud.cn/raw/d8986ba5724ee54e2824d917e74a64d6.png)
   - Enable or disable **Voice Messaging**.
   Voice Messaging is billed by DAU. You can enable it as needed.
   ![](https://qcloudimg.tencent-cloud.cn/raw/54770276d70bdffaee0c5d9f19d5df83.png)
   - Enable or disable **Speech-to-Text**.
   Speech-to-Text is billed by duration. You can enable it as needed.
	![](https://qcloudimg.tencent-cloud.cn/raw/851315bafd172e1c830ead5fbe78a8a7.png)
5. Tick “I have read and agree to GME [Service Level Agreement](https://www.tencentcloud.com/zh/document/product/607/30455) and [SDK Privacy Agreement](https://www.tencentcloud.com/zh/document/product/607/37524)”.
6. Click **OK**.



## Setting an Application

After an application is created, it is displayed in the application list on the “Service management” page. Click **Set** to go to the application details page.
![](https://qcloudimg.tencent-cloud.cn/raw/5030bd1d74a6ee68fb414ca1644037fd.png)

### Modifying application information

1. Click **Modify** to modify the relevant information.
2. After completing the modification, click **Save**.
![](https://qcloudimg.tencent-cloud.cn/raw/4027bcb5db4cdf5c17b07bf305832e69.png)

### Modifying service status

1. Click **Modify** to enable/disable the desired service.
2. After completing the modification, click **Save**.
![](https://qcloudimg.tencent-cloud.cn/raw/e28d05b92ccda7aa011764800a5f3a50.png)

## Key Parameters

In **Authentication info**, you can obtain the AppID and permission key required for the SDK voice services.
![](https://qcloudimg.tencent-cloud.cn/raw/667413c114bec5fc5f73cb0f08c3d472.png)

> ?
- The permission key here will be used as a parameter when accessing the SDK. 
- After you reset the key, it will take effect within 15 minutes to 1 hour. It is not recommended to change it frequently.
- The option of **Reset key** is only available for the account that creates the game, root account, and global collaborators.
- For more information about authentication, see [Authentication Key](https://www.tencentcloud.com/zh/document/product/607/12218).



[](id:test)

## Tag management

When you [create an application](#test1), you can click **+Add** to add an existing tag to the application. If no tags are created, you can create tags by following the steps below:

1. When creating an application, you can click **[Manage Tags](https://console.cloud.tencent.com/tag/taglist)** in the **Application info** section to go to the tag list page.
![](https://qcloudimg.tencent-cloud.cn/raw/2675330a883aefeeaa2c0ad6f374afb7.png)
2. Click **Create tag**, and complete the tag information.
![](https://qcloudimg.tencent-cloud.cn/raw/81a09412f346f0df5f3e5c94dd03f5b0.png)
3. Click **OK**.

## Disabling Services

An existing application cannot be deleted. If you no longer want to use it, disable all services under it. After that, all requests for the application will be failed. To disable a service, log in to the [GME console](https://console.intl.cloud.tencent.com/gamegme), and click **Set** for the desired application to go to the application details page.
![](https://qcloudimg.tencent-cloud.cn/raw/5030bd1d74a6ee68fb414ca1644037fd.png)
Click **Modify** > **Disable** > **Save** for the desired service.
![](https://qcloudimg.tencent-cloud.cn/raw/887c4e50e5f22b32bc08f9f4d712f80c.png)