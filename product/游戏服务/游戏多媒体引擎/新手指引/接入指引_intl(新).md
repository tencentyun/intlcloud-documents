Thank you for using [Tencent Cloud Game Multimedia Engine (GME) SDK](https://cloud.tencent.com/product/tmg?idx=1). This article describes how to access GME SDK for better developer access.

To use GME, follow the five steps below:
1. [Create a GME service in Tencent Cloud's backend](#.E6.96.B0.E5.BB.BA.E6.9C.8D.E5.8A.A1).
2. [Download the appropriate version of the client SDK](#.E4.B8.8B.E8.BD.BD-sdk).
3. [Port the SDK to the project by following the instructions in the API access document](#.E7.9B.B8.E5.85.B3-sdk-.E6.8A.80.E6.9C.AF.E6.96.87.E6.A1.A3).
4. [View daily operational statistics in the backend](#.E6.8E.A7.E5.88.B6.E5.8F.B0.E7.94.A8.E9.87.8F.E7.BB.9F.E8.AE.A1).
5. [Troubleshoot and give feedback on the special problems during the access process](#.E7.89.B9.E6.AE.8A.E9.97.AE.E9.A2.98.E5.A4.84.E7.90.86).


## Creating a Service
### 1. Create an application
![](https://main.qcloudimg.com/raw/a4b3dbd8aefd9dd032f8c3ce4154b227.png)

### 2. Required information
Enter the required information on the page, and select the services as needed. 
- The billing mode varies with different sound quality options. For more information, see [Purchase Guide](https://cloud.tencent.com/document/product/607/17808) or consult Tencent Cloud's sales rep. The settings can be modified at any time.
- For gaming applications, you need to select the appropriate platform/engine.
- The settings for voice messaging and speech-to-text service can be modified at any time.

![](https://main.qcloudimg.com/raw/bafdd3250004a5d69322beab1d6c25c7.png)


### 3. View an application
The AppID in the list is used as a parameter when accessing the SDK for development.
![](https://main.qcloudimg.com/raw/9e78b27c75b9bfcd2ce02ae1d02b7046.png)


### 4. Application settings
![](https://main.qcloudimg.com/raw/ac27c53e9a07fa819344f668978fe019.png)
In the application information module, click **Modify** to modify the information as needed.

### 5. Authentication information
![](https://main.qcloudimg.com/raw/76b5038763d2aded0be39b0d1bc27efa.png)
- The permission key in this module is used as a parameter when accessing the SDK. 
- Change of the key on this page takes effect within 15 minutes to 1 hour. It is not recommended to change it frequently.
- Key reset is only allowed for the account that creates the game, master account, and global collaborators.
- For more information on authentication, see [GME key documentation](https://cloud.tencent.com/document/product/607/12218).
 ![](https://main.qcloudimg.com/raw/df3f92e2eb50aea9d8dde32f252045f6.png)


### 6. Enable and disable businesses and services
You can enable or disable businesses and services.
![](https://main.qcloudimg.com/raw/a5711820b59c6d4047565562094d1595.png)
![](https://main.qcloudimg.com/raw/ec0f00f1afc229b6db5676772c53edad.png)


## Downloading SDK 
### 1. Download URL
Download the relevant demo and SDK in the [SDK Download Guide](https://cloud.tencent.com/document/product/607/18521).

### 2. Preparations for access
To access the SDK, you need to use the appid and related permission keys provided by Tencent Cloud, which are the AppID in the application management list and the authentication information module in the application settings.

For more information on platform-specific configurations, see the project configuration document for the platform.

### 3. Usage tips for the official demo
You can do a functionality test with a Tencent Cloud test account in the Demo. To use your personal or corporate test account, you need to replace the AppID of the Tencent Cloud test account in the corresponding interface of the demo with the AppID you obtained in the console, and change the permission key of voice chat in the AVChatViewController-GetAuthBuffer function.


## API Documentations
Depending on the platform or engine you are using, you can access the SDK by referring to the following documentations:

Unity related documentations:
[Project Configuration](https://cloud.tencent.com/document/product/607/10783)
[API Documentation](https://cloud.tencent.com/document/product/607/15228)

Unreal Engine related documentations:
[Project Configuration](https://cloud.tencent.com/document/product/607/17025)
[API Documentation](https://cloud.tencent.com/document/product/607/15231)

Cocos2D related documentations:
[Project Configuration](https://cloud.tencent.com/document/product/607/15216)
[API Documentation](https://cloud.tencent.com/document/product/607/15218)

Windows related documentations:
[Project Configuration](https://cloud.tencent.com/document/product/607/19068)
[API Documentation](https://cloud.tencent.com/document/product/607/15232)

iOS related documentations:
[Project Configuration](https://cloud.tencent.com/document/product/607/15219)
[API Documentation](https://cloud.tencent.com/document/product/607/15221)

Android related documentations:
[Project Configuration](https://cloud.tencent.com/document/product/607/15203)
[API Documentation](https://cloud.tencent.com/document/product/607/15210)

Mac related documentations:
[Project Configuration](https://cloud.tencent.com/document/product/607/18617)
[API Documentation](https://cloud.tencent.com/document/product/607/18739)

H5 related documentations:
[Project Configuration](https://cloud.tencent.com/document/product/607/32156)
[API Documentation](https://cloud.tencent.com/document/product/607/32157)



## Console Usage Statistics
[Operation Guide](https://cloud.tencent.com/document/product/607/17448)


## Other Issues
[FAQs](https://cloud.tencent.com/document/product/607/17359)     [Error Codes](https://cloud.tencent.com/document/product/607/15173)

