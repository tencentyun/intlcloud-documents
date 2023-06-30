## Overview
OrcaTerm is a login method recommended by Tencent Cloud. You can use it to directly log in to a Linux instance quickly. It has the following strengths:
- Supports copy and paste.
- Supports scrolling with mouse wheel.



<dx-alert infotype="explain" title="">
- When you create a Linux Lighthouse instance, it will be bound to a key by default. The username of the key is `lighthouse`, which has the root privileges.
- When you use OrcaTerm to log in to a Linux instance, the system will use the key of the `lighthouse` username for login by default.
</dx-alert>



## Supported Systems
Windows, Linux, or macOS.

## Prerequisites

- Before login, confirm that the firewall of the instance has passed port 22 (which has been enabled by default when the instance was created).

## Directions

1. Log in to the [Lighthouse console](https://console.cloud.tencent.com/lighthouse/instance/index).
2. Find the target instance in the server list and select a login method as desired.
 - Click **Log in** in the instance card in the server list.
![](https://qcloudimg.tencent-cloud.cn/raw/11148d430192dcc14bb2f55d039d32d5.png)
 - Click the instance card to enter the instance details page and click **Log In** in **Remote Login** or in the top-right corner of the page.
![](https://qcloudimg.tencent-cloud.cn/raw/0b01ce7d78e8660187e59c04267d7594.png)
 - For an instance created by using an [application image](https://intl.cloud.tencent.com/document/product/1103/41261), select **Pre-installed application** on the instance details page and click **Log in** in the top-right corner of the page.
   ![](https://qcloudimg.tencent-cloud.cn/raw/455852974d4bcfff9140c23ff54f493d.png)
   The page for successful login is as shown below:
   ![](https://qcloudimg.tencent-cloud.cn/raw/5b277158fec90436320b61bbc393233a.png)
    - After successful login, you can set up low-load lightweight applications with a moderate number of access requests, such as small and middle-sized websites, web applications, blogs, forums, mini games, ecommerce, cloud storage, image hosting, and cloud-based development, testing, and learning environments as instructed in [Best Practices](https://www.tencentcloud.com/document/product/1103/41255).
    - The WebShell UI has a variety of features. You can use the virtual keyboard on the mobile client to change the OrcaTerm appearance, upload/download files, start self-service instance detection, enable multi-session, split the screen, and get the prompts as instructed in [More OrcaTerm features](#OrcaTermWork).

## Related Operations
### Enabling/Disabling OrcaTerm-based quick login


<dx-alert infotype="explain" title="">
After a Lighthouse instance is created successfully, the OrcaTerm-based quick login feature will be enabled by default. You can disable or enable it again in the following steps:
</dx-alert>


1. Log in to the [Lighthouse console](https://console.cloud.tencent.com/lighthouse/instance/index).
2. Find the target instance in the server list and enter the instance details page.
3. In **Quick login** in **Remote login**, you can **enable** or **disable** OrcaTerm-based quick login as needed:
 - **Close**: If you don't need to use quick login, you can disable it.
<dx-alert infotype="notice" title="">
- After quick login is disabled, you can still use the local SSH client to remotely log in to the instance. You can also enable quick login again.
- After quick login is disabled, the public key (stored under the `lighthouse` user of the operating system by default) of the default system key won't be deleted at the same time. You can delete the public key by yourself. However, if it is deleted, quick login will not take effect after being enabled again.
</dx-alert>
 - **Enable**: After quick login is enabled, you can use the default system key to quickly log in to the instance through OrcaTerm in a browser.
<dx-alert infotype="notice" title="">
Confirm that the public key (stored under the `lighthouse` user of the operating system by default) of the default system private key is not deleted; otherwise, the quick login feature won't work after being enabled.
</dx-alert>



### More OrcaTerm features[](id:OrcaTermWork)

OrcaTerm offers a variety of features to ensure a satisfactory user experience.

OrcaTerm features are described as follows:
<dx-accordion>
::: Multiple keyboard shortcuts[](id:hotKey)

OrcaTerm supports multiple keyboard shortcuts, which can be viewed on the UI as instructed below:
1. Log in to the instance as instructed in [Logging in to Linux Instance via OrcaTerm](https://intl.cloud.tencent.com/document/product/1103/41523).
2. On the OrcaTerm UI, open the **Keyboard shortcuts** window to view the supported shortcuts.
  - If your local computer uses macOS: Press `⌘ + /`.
  - If your local computer uses Windows: Press `Ctrl + /`.
    


:::
::: Viewing instance monitoring data[](id:monitoringData)

You can view the instance monitoring data in real time on the OrcaTerm UI as instructed below. Currently, the data is refreshed once every 10 seconds.

1. Log in to the instance as instructed in [Logging in to Linux Instance via OrcaTerm](https://intl.cloud.tencent.com/document/product/1103/41523).
2. At the bottom of the OrcaTerm UI, view the instance monitoring data.



:::
::: Changing the username[](id:modifyUsername)

You can specify the user to log in via OrcaTerm as instructed below:

1. Log in to the instance as instructed in [Logging in to Linux Instance via OrcaTerm](https://intl.cloud.tencent.com/document/product/1103/41523).
2. In the **Log in** pop-up window, the default username is `lighthouse`, which can be changed as needed.

3. Then click **Log in**



:::
::: Quickly installing TencentCloud Automation Tools[](id:installTAT)


You need to use TencentCloud Automation Tools to implement quick passwordless login via OrcaTerm. If the tool is not installed for your instance, you can install it upon login as instructed below:

1. Log in to the instance as instructed in [Logging in to Linux Instance via OrcaTerm](https://intl.cloud.tencent.com/document/product/1103/41523).
2. In the **Log in** pop-up window, select the installation method as needed if you are prompted that TencentCloud Automation Tools is not installed for your instance.
   - **Quick installation (reboot required)**: Read the notes, select **Installation requires your agreement to a forced shutdown**, and click **Quickly install TencentCloud Automation Tools**.
   - **Manual installation (no reboot required)**: Perform the installation as instructed in [Installing TAT Agent](https://intl.cloud.tencent.com/document/product/1147/46042).
3. After the installation is completed, the instance can be quickly logged in to via OrcaTerm.

:::
::: Using the command block mode[](id:block)

You can use the command block mode on the OrcaTerm UI. After the mode is enabled, every executed command will be displayed as a module for easy use of OrcaTerm. You can also disable the mode as needed as instructed below:

1. Log in to the instance as instructed in [Logging in to Linux Instance via OrcaTerm](https://intl.cloud.tencent.com/document/product/1103/41523).
2. On the OrcaTerm UI, enable or disable the command line mode.
  - **Enable the command line mode**: Select <img src="https://qcloudimg.tencent-cloud.cn/raw/2a7a6b5795be349496600bda16a038c6.png" style="margin:-3px 0px"> on the toolbar of the OrcaTerm UI to enable the command block mode. After it is enabled, a command will be executed as follows:
![](https://qcloudimg.tencent-cloud.cn/raw/2b3752cb5644e4e06af15d037a7992cb.png)
  - **Disable the command line mode**: Select <img src="https://qcloudimg.tencent-cloud.cn/raw/bb5426e4e2012fc77ff78561de913e15.png" style="margin:-3px 0px"> on the toolbar of the OrcaTerm UI to disable the command block mode. After it is disabled, a command will be executed as follows:
![](https://qcloudimg.tencent-cloud.cn/raw/5862c7588022194f1a855f26e87b6f86.png)
<dx-alert infotype="explain" title="">
If the command block mode is disabled and enabled again, you need to reconnect to OrcaTerm.
</dx-alert>



:::
::: Viewing the release note[](id:changelogs)
You can view the latest release note of OrcaTerm, including the new features, bugfixes, and features coming soon, as instructed below:

1. Log in to the instance as instructed in [Logging in to Linux Instance via OrcaTerm](https://intl.cloud.tencent.com/document/product/1103/41523).
2. Select <img src="https://qcloudimg.tencent-cloud.cn/raw/4796538ba87024b0a264e8d512c4544b.png" style="margin:-3px 0px"> in the bottom-right corner of the OrcaTerm UI.
3. View the latest release note in the pop-up window.

:::
::: Selecting an instance to log in[](id:choose)
You can select any instance to log in on the OrcaTerm UI as instructed below:

1. Log in to the instance as instructed in [Logging in to Linux Instance via OrcaTerm](https://intl.cloud.tencent.com/document/product/1103/41523).
2. Select <img src="https://qcloudimg.tencent-cloud.cn/raw/5bb1db36d10fd49f34ecc27eda0e306a.png" style="margin:-3px 0px"> on the toolbar of the OrcaTerm UI.
3. For the first time, the **Select the instance to be displayed** window will pop up. Select the target instance and click **OK**.
4. Select <img src="https://qcloudimg.tencent-cloud.cn/raw/5bb1db36d10fd49f34ecc27eda0e306a.png" style="margin:-3px 0px"> > **Add instance** to add instances as needed.
<dx-alert infotype="explain" title="">
Currently, up to ten instances can be added.
</dx-alert>
5. After the instances are added successfully, you can select any instance to log in.



:::
::: Uploading/Downloading files[](id:updownload)



You can upload local files to the instance or download files from the instance to your local file system as instructed below:

1. Log in to the instance as instructed in [Logging in to Linux Instance via OrcaTerm](https://intl.cloud.tencent.com/document/product/1103/41523).
2. Select <img src="https://qcloudimg.tencent-cloud.cn/raw/81fbdd2c2b7cb70f17c508073496f58e.png" style="margin:-3px 0px"> on the toolbar of the OrcaTerm UI.
3. In the pop-up menu, select **Upload** or **Download**.
   The detailed steps are as follows:
    - **Upload a file**:
       1. In the **Select the file and directory for upload** pop-up window, select **Local upload** or **Upload via URL** as needed.
       2. If you select **Local upload**, click **Click to upload** and then select a local file. If you select **Upload via URL**, enter the file URL in **URL**.
       4. Select the target upload directory and click **OK**.
       <dx-alert infotype="explain" title="">
       Currently, files can be uploaded only to the `home > lighthouse` directory.
        </dx-alert>
       Click <img src="https://qcloudimg.tencent-cloud.cn/raw/a78e204de7cde3473482732c8b9fef98.png" style="margin:-3px 0px"> in the bottom-right corner of the page and view the operation result in the pop-up window. If the file is uploaded successfully, the result will be displayed.
    - **Download a file**:
       1. In the **Download file** pop-up window, open the directories and select the target file.
       2. Click **OK** and select the local directory in the pop-up window.
       3. Click <img src="https://qcloudimg.tencent-cloud.cn/raw/a78e204de7cde3473482732c8b9fef98.png" style="margin:-3px 0px"> in the bottom-right corner of the page and view the operation result in the pop-up window. If the file is downloaded successfully, the result will be displayed.

:::
::: Using self-service instance detection[](id:selfCheck)

If you encounter any problem when logging in to or using the instance, you can perform self-service instance detection as instructed below:

1. Log in to the instance as instructed in [Logging in to Linux Instance via OrcaTerm](https://intl.cloud.tencent.com/document/product/1103/41523).
2. Select <img src="https://qcloudimg.tencent-cloud.cn/raw/2d3d7e693d09bb8a58d58557e4f25ff4.png" style="margin:-3px 0px"> on the toolbar of the OrcaTerm UI.
3. In the **Self-service instance detection** pop-up window, click **OK**.


:::
::: Enabling the multi-tag window[](id:multilabel)

You can open multiple instance connection pages in the form of tags on the OrcaTerm UI as instructed below:

1. Log in to the instance as instructed in [Logging in to Linux Instance via OrcaTerm](https://intl.cloud.tencent.com/document/product/1103/41523).
2. Select <img src="https://qcloudimg.tencent-cloud.cn/raw/fc93655617db690aecdc7b1cea0baf39.png" style="margin:-3px 0px"> at the top of the OrcaTerm UI.
3. You can see that the `(1) instance ID` tag has been created.
<dx-alert infotype="explain" title="">
- Up to five tags can be opened at the same time.
- A tag will be named in the format of `(Incrementing number) instance ID`.
</dx-alert> <img src="https://qcloudimg.tencent-cloud.cn/raw/b978c74d0b6c127e0948de0a39716dc4.png"/>


:::
::: Enabling screen splitting[](id:splitScreen)

You can split the screen on the OrcaTerm UI to view and execute multiple operation tasks at the same time as instructed below:

1. Log in to the instance as instructed in [Logging in to Linux Instance via OrcaTerm](https://intl.cloud.tencent.com/document/product/1103/41523).
2. Select <img src="https://qcloudimg.tencent-cloud.cn/raw/bf17a1103ce6fa76150df87768987f79.png" style="margin:-3px 0px"> at the top of the OrcaTerm UI.
3. You can see that the screen has been split into three sections named in the format of `(Incrementing number) instance ID`:
<dx-alert infotype="explain" title="">
- The screen can be split into up to four sections.
- A section will be named in the format of `(Incrementing number) instance ID`.
</dx-alert> <img src="https://qcloudimg.tencent-cloud.cn/raw/4d4b2c02d5173c92fe189c358c71a29f.png"/>


:::
::: Changing the skin[](id:changeAppearance)

You can change the text size, font, and color on the WedShell UI as instructed below:

1. Log in to the instance as instructed in [Logging in to Linux Instance via OrcaTerm](https://intl.cloud.tencent.com/document/product/1103/41523).
2. Select <img src="https://qcloudimg.tencent-cloud.cn/raw/183be38a53180ccd705dddbb859820e3.png" style="margin:-3px 0px"> on the toolbar of the OrcaTerm UI.
3. In the pop-up window, change the text size, font, or color of the OrcaTerm as you like.

:::
</dx-accordion>





