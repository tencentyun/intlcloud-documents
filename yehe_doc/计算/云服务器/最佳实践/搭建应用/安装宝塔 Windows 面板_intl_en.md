## Overview
BT panel is easy-to-use, powerful, friendly interactive, and free-of-charge server management software that supports Linux and Windows. It allows you to configure LAMP, LNMP, websites, databases, FTP, and SSL, and easily manage servers with a few clicks via a web client.

This document introduces how to use an image in the Tencent Cloud marketplace to quickly install a BT panel on CVM instances running on Windows.


## Directions

### Installing the BT panel during CVM instance creation


<dx-alert infotype="notice" title="">
If you want to use a purchased CVM instance to install a BT panel, you can [reinstall the system](https://intl.cloud.tencent.com/document/product/213/4933) and select the corresponding image in the image marketplace to complete the environment deployment. CVM instances in some regions outside the Chinese mainland currently do not support system reinstallation via the image marketplace. In such cases, you are advised to use CVM instances in other regions to deploy the environment or go to the [BT panel official website](https://www.bt.cn/) for more installation information.
</dx-alert>

1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/index) and click **Create Instance** on the instance management page.
2. On the model selection page, set parameters as needed. Among the parameters, for **Image**, select **Image Marketplace** and click **Select from image marketplace**, as shown in the figure below:
<dx-alert infotype="notice" title="">
- Some regions outside the Chinese mainland currently do not support CVM instance creation via the image marketplace. If **Image Marketplace** is not displayed under the region you select, select another region that supports the image marketplace.
- You are advised to select an instance whose memory is greater than 2 GB and system disk capacity is greater than 40 GB.
3. In the **Image Marketplace** window, select **Ops Tool**, enter **BT**, and click <img src="https://main.qcloudimg.com/raw/70c20e0ff30f88eef20d6b540d6ef804.png" style="margin:-3px 0px">.
4. Select an image as needed. This document uses **BT Panel for Windows - Official Edition (WAMP/WNMP/Tomcat/Node.js)** as an example. Click **Use for Free**.
5. In the security group associated with the instance, add the inbound rule to open port 8888. For more information, see [Adding Security Group Rules](https://intl.cloud.tencent.com/document/product/213/34272).
Select other configuration such as the storage media and bandwidth as needed, and finally click **Purchase** to complete the BT panel setup.


### Obtaining BT panel login information
1. Log in to the CVM instance. For more information, see [Logging in Using Standard Method (Recommended)](https://intl.cloud.tencent.com/document/product/213/41018).
2. On the desktop, right-click <img src="https://qcloudimg.tencent-cloud.cn/raw/c6e9910fc4f983d45729b4f6924e8273.png" style="margin:-3px 0px"> in the lower-left corner and click **Run** in the pop-up menu.
3. In the command-line interface (CLI), run the following command to obtain the login information:
```
bt default
```
Note down the BT panel address and login information in the command output.


### Logging in to the BT panel
1. On your local computer, open a browser and visit the BT panel address obtained.
```shell
http://CVM public IP:8888/xxxx
```
2. Enter the username and password that you noted down, and click **Log In**.
3. Select **I have read and agreed to Service Agreement** and click **Enter Panel**.
4. Select kits for website installation and deployment as needed.
