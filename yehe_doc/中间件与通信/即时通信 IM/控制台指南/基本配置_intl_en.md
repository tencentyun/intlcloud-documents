Log in to the [IM console](https://console.cloud.tencent.com/im) and click the target app card to go to the basic configuration page of the app. On the page, you can manage the basic configuration of the app based on your business needs.



## Standard Billing Plan Information
![](https://main.qcloudimg.com/raw/97daad91ef3deb7e9e1f5cbfb210b7ad.png)  
In the **Standard Billing Plan** section, you can see the standard billing plan information of the app and perform the following operations:

- Upgrade the standard billing plan of the app.
- Disable/Delete the app.

### Upgrading the standard billing plan
You can click **Upgrade Plan** in the **Standard Billing Plan** section to update the plan edition or configuration of your app. For more information, see [Upgrading an App](https://intl.cloud.tencent.com/document/product/1047/34577).

### Disabling/Deleting an app
>?You can create up to 300 IM apps under a Tencent Cloud account. If you have reached that limit, [disable and delete] an unwanted app before creating a new one.
>**Only apps in "Disabled" status can be deleted. Once an app is deleted, all the data and services associated with the SDKAppID are removed and cannot be recovered, so proceed with caution.**


**Free Edition Apps**
- Free Edition apps can be manually disabled.
 In the **Basic Info** area, click **Disable** next to **Status**. In the pop-up dialog box, click **OK**.
- Free Edition apps can be manually deleted.
 In the **Basic Info** area, click **Delete** next to **Status**. In the pop-up dialog box, click **OK**.

**Pro and Ultimate Edition Apps**
- Apps that have overdue payments for seven days will be automatically **Disabled**. To delete such disabled apps, [contact us](https://console.cloud.tencent.com/workorder/category).
- Apps become **Expired** after refund, and **Disabled** after seven days. To delete such disabled apps, [contact us](https://console.cloud.tencent.com/workorder/category).

**TRTC Trial Edition Apps**
Once a TRTC trial app is disabled by the TRTC administrator, you can [contact us](https://console.cloud.tencent.com/workorder/category) to disable and delete the app.

## Configuring App Information
![](https://main.qcloudimg.com/raw/867f34d67ddcca7de31ff17327dee744.png)
In the **Basic Info** section, you can:
Edit the basic information of your app, including the app name, type, and introduction.

### Editing basic information
1. Click **Edit** on the right of **Basic Info** to edit the app settings.
2. You can modify the app name, type, and introduction.
3. Click **Save**.

## Configuring Basic Information
![](https://main.qcloudimg.com/raw/935f6fbdcd16ac4cbcb7ff7d53d7bfe5.png)
In the **Basic Information** section, you can:
Obtain the key of the app.

### Obtaining a key
**Keys are sensitive information. Be sure to keep them confidential and prevent them from being leaked.** By default, apps (SDKAppIDs) created before August 15, 2019 use the [ECDSA-SHA256](https://intl.cloud.tencent.com/document/product/1047/34385) signature algorithm that uses a public key and a private key. You can choose to update to the HMAC-SHA256 signature algorithm.

1. Click **Display key** to the right of **Key**.
2. Click **Copy** to copy and save the key information.
    The key can be used to generate UserSig. For more information, see [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385).

## Configuring Account Admins
Account admins can call RESTful APIs, disband groups, and perform operations on all members. You can use the default account admin `administrator` or manually add a new account admin. Each app supports up to 10 account admins.
![](https://main.qcloudimg.com/raw/9cf8914c53cb998fd7ee619ef30836a9.jpg)
[](id:AddAdmin)

### Adding an admin
1. Click **Add Admin** to the right of **Account Administrator**.
2. In the **Add Admin** dialog that pops up, enter a name for the account admin.
3. Click **Add**.

### Deleting an admin
1. Click **Delete** on the right of the target admin.
2. Click **Confirm** in the pop-up dialog box.

## Managing Offline Push Certificates

### Adding an offline push certificate

1. Click **Add Certificate** in the push settings area of the corresponding platform.
2. In the **Add Certificate** dialog that pops up, set the parameters as needed.
 - Adding an Android certificate
![](https://main.qcloudimg.com/raw/7821c57eef8b7a63019df23eb347720f.jpg)
 - Adding an iOS certificate
 ![](https://main.qcloudimg.com/raw/dc629d1f3ae746e699919930b1f99024.png)
3. Click **Confirm** to save the configuration.

### Editing an offline push certificate
1. Click **Edit** in the certificate area.
2. In the dialog box that pops up, modify the parameters as needed and click **Confirm** to save the configuration.

### Deleting an offline push certificate
>!Once the certificate is deleted, push messages are no longer delivered. Deleted certificates cannot be restored. Proceed with caution.

1. Click **Delete** in the certificate area.
2. In the pop-up dialog box, click **Confirm**.

## Configuring Tags 
### Editing tags

1. Click **Edit** on the right of **Tag Configuration**.
2. In the pop-up dialog, you can add or delete a tag.
![](https://main.qcloudimg.com/raw/0fd92ff5708ea939777cd6916d311f60.png)

## TRTC

### Activate the Video Calls Service

To implement features such as audio/video call and interactive live streaming in the current IM application, click **Activate** in the top-right corner of the **TRTC** section to quickly activate [TRTC](https://www.tencentcloud.com/document/product/647?lang=en&pg=). The system will create a TRTC application in the [TRTC console](https://console.cloud.tencent.com/trtc), which has the same `SDKAppID` as your current IM application. The two can use the same accounts and authentications.

After activation, you can click **View application** in the top-right corner of the **TRTC** section to view your TRTC application in the TRTC console.

### Managing audio/video call feature

IM and TRTC jointly provide the audio/video call capability as described in [Billing Overview](https://www.tencentcloud.com/document/product/1047/34349) for audio/video call business scenarios, so you can better use audio/video services at lower costs by quickly integrating relevant capabilities. You can click **Activate now** in the **TRTC** section and then manage the feature.

The directions are as follows:

1. Log in to the [IM console](https://console.cloud.tencent.com/im) and click the target application card to go to the basic configuration page.

2. In the bottom-right corner of the page, click **Audio/Video call capability - free trial** in the **TRTC** section. In the **Activate free trial of audio/video call feature** pop-up window, click **Activate Now** to activate the **60-day free trial** of TUICallKit.

3. In the feature section, you can click <img src="https://qcloudimg.tencent-cloud.cn/raw/26be00c9c3f48ae0c7031b89d1f3d3d9.png" style="zoom:35%;" /> to view the details of the free trial of the audio/video call capability.
