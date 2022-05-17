## Overview
Remote Desktop Connection is commonly used for file upload to a Windows Lighthouse instance. This document describes how to upload files from a Windows computer to a Windows Lighthouse instance by using Remote Desktop Connection or download files from the instance to a local file system.

## Prerequisites
You have obtained the Lighthouse instance admin account and password.
- The default admin account of a Windows Lighthouse instance is `Administrator`.
- If you forgot the login password, you can [reset it](https://intl.cloud.tencent.com/document/product/1103/41553).

## Directions
>? This document uses a Windows 7 computer as an example. The procedure may vary slightly according to the operating system version.
>
### Obtaining public IP
Log in to the [Lighthouse console](https://console.cloud.tencent.com/lighthouse/instance/index) and get the public IP of the target Lighthouse instance on the **Instances** page.

### Uploading files
1. Press **Windows + R** on the local computer to open the **Run** window.
2. In the **Run** pop-up window, enter **mstsc**, and click **OK** to open the **Remote Desktop Connection** dialog box.
3. In the pop-up dialog box, enter the public IP address of the Lighthouse instance and click **Show Options** as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/4231386f3cbb5398f0169c737522ec3b.png)
4. On the **General** tab, enter the Lighthouse instance public IP address and username "Administrator" as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/c73f97fec591f8c8b91853caf32654f0.png)
5. Select the **Local Resources** tab and click **More**, as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/ea187e8658dc2448748bf12731d251ba.png)
6. In the **Local devices and resources** pop-up window, select the **Drives** module, check a local disk that contains files to upload to the Windows Lighthouse instance, and click **OK** as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/9734f74b2f7fef30ca47775c3e6780d5.png)
7. After the local configuration is completed, click **Connect** to log in to Windows Lighthouse instance remotely.
8. Click <img src="https://main.qcloudimg.com/raw/8a6913dc513bc353c8adee020d3a829f.png" style="margin:-5px 0px"> > **Computer** in the Windows Lighthouse instance, and you can see the local disk mounted as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/8d33784c0b8b4a26f69cac212c2766e4.png)
9. Double-click to open the attached local disk. Copy desired local files to another drive of the Windows Lighthouse instance.
For example, copy the file A from the local drive E to the C drive of the Windows Lighthouse instance.

### Downloading files
To download files from the Windows Lighthouse instance to your computer, you only need to copy desired files from the instance to the attached local disk.

