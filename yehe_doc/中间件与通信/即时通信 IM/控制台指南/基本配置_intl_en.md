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


**Trial Edition Apps**
- Trial Edition apps can be manually disabled.
 In the **Basic Info** area, click **Disable** next to **Status**. In the pop-up dialog box, click **OK**.
- Trial Edition apps can be manually deleted.
 In the **Basic Info** area, click **Delete** next to **Status**. In the pop-up dialog box, click **OK**.

**Pro and Flagship Edition Apps**
- Apps that have overdue payments for seven days will be automatically **Disabled**. To delete such disabled apps, [contact us](https://console.cloud.tencent.com/workorder/category).
- Apps become **Expired** after refund and **Disabled** after seven days. To delete such disabled apps, [contact us](https://console.cloud.tencent.com/workorder/category).

**TRTC Trial Edition Apps**
Once a TRTC trial app is disabled by the TRTC administrator, you can [contact us](https://console.cloud.tencent.com/workorder/category) to disable and delete the app.

## Configuring App Information
![](https://main.qcloudimg.com/raw/867f34d67ddcca7de31ff17327dee744.png)
In the **App Information** section, you can:
Edit the basic information of your app, including the app name, type, and introduction.

### Editing basic information
1. Click **Edit** on the right of **App Information** to edit the app settings.
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
    The key can be used to generate UserSig. For more information, please see [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385).

## Configuring Account Admins
Account admins can call RESTful APIs, disband groups, and perform operations on all members. You can use the default account admin `administrator` or manually add a new account admin. Each app supports up to 10 account admins.
![](https://main.qcloudimg.com/raw/9cf8914c53cb998fd7ee619ef30836a9.jpg)
[](id:AddAdmin)

###  Adding an admin
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
 - Adding a TPNS certificate
 ![](https://main.qcloudimg.com/raw/454f5fbbcc9b4e5587c7ecbc3b587e6b.png)
3. Click **Confirm** to save the configuration.

### Editing an offline push certificate
1. Click **Edit** in the certificate area.
2. In the dialog box that pops up, modify the parameters as needed and click **Confirm** to save the configuration.

### Deleting an offline push certificate
>!Once the certificate is deleted, push messages are no longer delivered. Deleted certificates cannot be restored. Proceed with caution.

1. Click **Delete** in the certificate area.
2. In the pop-up dialog box, click **Confirm**.

## Tag Configuration
### Editing tags

1. Click **Edit** on the right of **Tag Configuration**.
2. In the pop-up dialog, you can add or delete a tag.
![](https://main.qcloudimg.com/raw/0fd92ff5708ea939777cd6916d311f60.png)

## Activating Tencent Real-Time Communication (TRTC)
If you need features such as audio calling, video calling, and interactive live streaming in your current IM app, or you need to integrate the IM SDK and TRTC SDK at the same time, you can activate [TRTC](https://intl.cloud.tencent.com/document/product/647) in the **Activate Tencent Real-Time Communication (TRTC)** area. The system will create a TRTC app in the [TRTC console](https://console.cloud.tencent.com/trtc), which has the same SDKAppID as your current IM app. The two accounts and their authentications can be reused.

1. Click **Activate** in the **Activate Tencent Real-Time Communication (TRTC)** area.
2. Click **Confirm** in the pop-up dialog box.

## Activating TPNS
You can activate TPNS for the current IM app in the [TPNS console](https://console.cloud.tencent.com/tpns). TPNS is a paid service. For its pricing, see [Billing Overview](https://intl.cloud.tencent.com/document/product/1024/36877).

You can see [Creating Products and Applications](https://intl.cloud.tencent.com/document/product/1024/32603) to create a TPNS app and enter relevant information in TPNS Push in the IM console.
>?After enabled, TPNS Push cannot be used concurrently with Native Offline Push.
