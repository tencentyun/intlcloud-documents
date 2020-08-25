This document describes how to access the GME SDK.



## Creating Service
#### Creating application
1. Log in to the [GME Console](https://console.cloud.tencent.com/gamegme) and click **Service Management** on the left sidebar.
2. Enter the service management page and click **Create Application**.


#### Entering information
Enter the required information on the page and select the service you need. 
- For billing details, please see [Product Pricing](https://intl.cloud.tencent.com/document/product/607/17808) or consult your Tencent Cloud rep. The settings can be modified afterwards.
- The settings for the voice messaging and speech-to-text service can be modified at any time.

![](https://main.qcloudimg.com/raw/6a7f84cf85f38d6ee87e98feb710ba23.png)

## Setting Service
#### Viewing application
The `AppID` in the list is used as a parameter when accessing the SDK for development.

![](https://main.qcloudimg.com/raw/90dabc58f16597ce5ef934f47d1e6707.png)


#### Setting application
Click **Settings** to enter the application information module and click **Modify** to modify the information as needed.

![](https://main.qcloudimg.com/raw/d915147f17ca0e31fc623c022f3c608b.png)



#### Authentication information

- The permission key in this module is used as a parameter when accessing the SDK. 
- Change of the key on this page takes effect within 15 minutes to 1 hour. You are not recommended to change it frequently.
- Only the account that creates the game, root account, and global collaborators can **reset the key**.
- For more information on how to use authentication, please see [Authentication Key](https://main.qcloudimg.com/raw/973b60c364a7ee43537db2dbdad37494.png).


#### Enabling/Disabling business
You can enable or disable businesses and services here.

![](https://main.qcloudimg.com/raw/90dabc58f16597ce5ef934f47d1e6707.png)



## Downloading SDK 
#### 1. Download address
Please download the relevant demo and SDK in the [SDK Download Guide](https://intl.cloud.tencent.com/document/product/607/18521).

#### 2. Preparations for access
To access the SDK, you need to use the `AppID` and related permission keys provided by Tencent Cloud, i.e., the `AppID` in the application management list and the authentication information in the application settings.

For more information on platform-specific configurations, please see the project configuration document for the platform.

#### 3. Usage tips for official demo
The demo has a Tencent Cloud test account for functionality trial. If you want to use your personal or corporate test account, you need to replace the `AppID` of the Tencent Cloud test account on the corresponding page of the demo with the `AppID` you get in the console and change the permission key of voice chat in the `AVChatViewController-GetAuthBuffer` function.


## API Documentation
You can refer to the following documents for access by platform or engine used:

Documents for Unity:
[Project Configuration](https://intl.cloud.tencent.com/document/product/607/10783)
[API Documentation](https://intl.cloud.tencent.com/document/product/607/15228)

Documents for Unreal Engine:
[Project Configuration](https://intl.cloud.tencent.com/document/product/607/17025)
[API Documentation](https://intl.cloud.tencent.com/document/product/607/15231)

Documents for Cocos2d:
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

Documents for macOS:
[Project Configuration](https://intl.cloud.tencent.com/document/product/607/18617)
[API Documentation](https://intl.cloud.tencent.com/document/product/607/18739)

Documents for HTML5:
[Project Configuration](https://intl.cloud.tencent.com/document/product/607/30261)
[API Documentation](https://intl.cloud.tencent.com/document/product/607/30263)



## Relevant Documents
For more information, please see [Operation Guide](https://intl.cloud.tencent.com/document/product/607/17448).



If you have any questions, please see [General FAQs](https://intl.cloud.tencent.com/document/product/607/30254) and [Error Codes](https://intl.cloud.tencent.com/document/product/607/15173).




