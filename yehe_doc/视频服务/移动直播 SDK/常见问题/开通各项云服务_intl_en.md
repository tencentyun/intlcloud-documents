[](id:LVB)
## Cloud Streaming Services (CSS) 
[](id:LVB_OPEN)
### How to activate CSS?
Go to the [CSS console](https://console.cloud.tencent.com/live), on the service activation page, read the agreement, check **Agree**, and click **Apply for Activation**.
![](https://main.qcloudimg.com/raw/6e3a5b7794e6dacdd77a9ce818c56e21.png)

[](id:LVB_PUSH_SECRECT)
### How do I enable hotlink protection keys?
Hotlink protection keys are a security mechanism that ensures only your app users can publish streams. You can change your hotlink protection settings anytime on the [Domain Management](https://console.cloud.tencent.com/live/domainmanage) page of the CSS console. For details, please see [Playback Authentication Settings](https://intl.cloud.tencent.com/document/product/267/31060).

[](id:LVB_API_SECRECT)
### How to obtain authentication keys for API calls?

For your backend server to call [cloud APIs](https://intl.cloud.tencent.com/document/product/267/30760) of CSS, it will need authentication keys to verify the legitimacy of the calls. For details on how to obtain authentication keys for API calls, please see [Signature v3](https://intl.cloud.tencent.com/document/product/267/37447).

[](id:LVB_EVENT_URL)
### How to configure a URL for event callbacks?
Tencent Cloud allows you to register callbacks for some live streaming events. It sends notifications to the URL you specify using the HTTP POST method. For how to configure a URL for event callbacks, please see [CSS Callback](https://intl.cloud.tencent.com/document/product/267/31074).

## Video on Demand (VOD)
### How to activate VOD?
Go to the [VOD console](https://console.cloud.tencent.com/vod/overview) to activate VOD. The service is charged daily by default.

### How do I query my VOD `APPID`?
Each Tencent Cloud account is assigned a unique `APPID`, which you can view in [Account Information](https://console.cloud.tencent.com/developer) of the Account Center.

[](id:IM)
## Instant Messaging (IM)
[](id:IM_OPEN)
### How to activate IM?
Go to the [IM console](https://console.cloud.tencent.com/im).
The IM application list of a newly verified account is empty. To create an application, click **Create Application**, fill in the information, and click **Confirm**.

>! You can also create an IM application in the CSS console. Log in to the CSS console, go to **MLVB SDK** > [**Application Management**](https://console.cloud.tencent.com/live/license/appmanage), click **Create Application**, enter an application name and description, and click **Confirm**.

[](id:IM_SDKAPPID)
### What is `SDKAppID`?
`SDKAppID` is a number,  that represents a product under your account. If you have multiple products, each product will have a `SDKAPPID`.

[](id:IM_ADMIN)
 ### What is administrator?
IM provides a series of [RESTful APIs](https://intl.cloud.tencent.com/document/product/1047/34621) that allows your backend server to use IM features directly, for example, to create a group, send system messages, and remove a user from a group. However, the RESTful APIs can only be called by an administrator. That is to say, you need a username that is `Administrator` and its corresponding password (`UserSig`). For more information, please see [RESTful API Overview](https://intl.cloud.tencent.com/document/product/1047/34620).


>? `UserSig` is the password needed to log in to IM. For details on how to obtain it, please see [Obtaining a Key](https://intl.cloud.tencent.com/document/product/1047/34385#obtaining-a-key).


## Cloud Object Storage (COS)
### How to activate COS?
All Tencent Cloud accounts can use the COS service after verification. Go to the [COS console](https://console.cloud.tencent.com/cos), click **Bucket List** > **Create Bucket**, fill in the information, and click **Create** to create a bucket.


### What is bucket?
Put simply, buckets function as **disk partitions**. When you pay for Tencent Cloud’s COS service, it’s like purchasing a hard disk. It’s a common practice to partition and format a disk before using it to store data. When you create a bucket in COS, it’s like creating a hard disk partition.

### How do I query `BucketName`?
`BucketName` is the name you give to a bucket during creation.

### How do I query `AppID`, `SecretId`, or `SecretKey`?
To view the information, on the [key management](https://console.cloud.tencent.com/cos5/key) page of the COS console, click **Cloud API Key**.
In COS, `APPID` is bound to `SecretId` and `SecretKey`. They are required to call COS APIs. COS is a cloud service with high security requirements, so unless a correct key is passed in, an API request will be rejected by Tencent Cloud.

## Cloud Virtual Machine (CVM, optional)
You can use your own server to deploy backend scripts for your project, but we recommend Tencent Cloud CVM for greater expertise and reliability. Please note that Tencent Cloud's distributed cloud databases can only be accessed via Tencent Cloud’s CVMs.
Log in to the [CVM console](https://console.cloud.tencent.com/cvm/overview), select **Instances** on the left sidebar, and click **Create** to go to the CVM purchase page.

>? For CVM image, we suggest that you select a Linux image with Nginx + PHP + MySQL from the image market.

Complete the subsequent steps as prompted. The CVM becomes available after the image is installed.

## TencentDB for MySQL (optional)
### How to activate TencentDB for MySQL?
Please see [Purchase Methods](https://intl.cloud.tencent.com/document/product/236/5160).

### How to use a database?
Please refer to:
- [Initializing MySQL Instance](https://intl.cloud.tencent.com/document/product/236/3128)
- [Connecting to MySQL Instance](https://intl.cloud.tencent.com/document/product/236/37788)
- [Instance Management Page](https://intl.cloud.tencent.com/document/product/236/31898)
