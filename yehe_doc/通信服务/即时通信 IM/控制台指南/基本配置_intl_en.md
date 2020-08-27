Log in to the [IM Console](https://console.cloud.tencent.com/im) and click the target app card to go to the app’s basic configuration page. You can manage basic configuration for your app according to business needs.

## Changing the Version

You can click **Update** in the **Version** area to update the version or configuration of your app. For more information, see [Updating Apps](https://intl.cloud.tencent.com/document/product/1047/34577).

## Configuring Basic Information
![](https://main.qcloudimg.com/raw/867f34d67ddcca7de31ff17327dee744.png)
In the **Basic Info** area, you can:

- Edit the app’s basic information, including the name, type, and introduction of your app.
- Disable/Delete your app.
- Get the key of your app.

### Editing basic information
1. Click **Edit** to the right of **Application Info** to edit app settings.
2. You can modify **Application Name**, **Application Type**, and **Application Intro**.
3. Click **Save**.

### Disabling and deleting an app
>You can create up to 100 IM apps under a Tencent Cloud account. If you have reached that limit, [disable and delete] an unwanted app before creating a new one.
>**Only apps in **Disabled** status can be deleted. Once an app is deleted, all the data and services associated with the SDKAppID are removed and cannot be recovered, so proceed with caution.**



**Trial Edition**
- Trial Edition apps can be manually disabled.
 In the **Basic Info** area, click **Disable** next to **Status**. In the pop-up dialog box, click **OK**.
- Trial Edition apps can be manually deleted.
 In the **Basic Info** area, click **Delete** next to **Status**. In the pop-up dialog box, click **OK**.

**Pro Edition/Flagship Edition**
- Apps that have been in arrears for seven days will be automatically **Disabled**. To delete such disabled apps, please [contact us](https://console.cloud.tencent.com/workorder/category).
- Apps become **Expired** after the refund and **Disabled** after seven days. To delete such disabled apps, please [contact us](https://console.cloud.tencent.com/workorder/category).

**TRTC Trial**
Once a TRTC trial app is disabled by the TRTC administrator, you can [contact us](https://console.cloud.tencent.com/workorder/category) to disable and delete the app.


### Obtaining a key
**Keys are sensitive information, so be sure to keep it confidential and prevent it from being leaked.** By default, apps (SDKAppIDs) created before August 15, 2019 use the [ECDSA-SHA256](https://intl.cloud.tencent.com/document/product/1047/34385) signature algorithm that uses a public key and a private key. You can choose to update to the HMAC-SHA256 signature algorithm.

1. Click **Display key** to the right of **Key**.
2. Click **Copy** to copy and save the key information.
    The key can be used to generate UserSig. For more information, see [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385).

## Configuring Account Admins
Account administrators can call RESTful APIs, disband groups, and perform operations on all members. You can use the default `administrator` or manually add account administrators.  Each application can have 5 account administrators.
![](https://main.qcloudimg.com/raw/9cf8914c53cb998fd7ee619ef30836a9.jpg)
<span id="AddAdmin"></span>

### Adding an admin
1. Click **Add Admin** to the right of **Account Admin**.
2. In the Add Admin dialog that pops up, enter a name for the account admin.
3. Click **Add**.

### Removing an admin
1. Click **Remove Administrator** to the right of **Account Admin**.
2. In the Remove Administrator dialog that pops up, check the admin account you want to remove.
3. Click **Remove**.

## Managing Offline Push Certificates

### Adding an offline push certificate

1. Click **Add Certificate** in the push settings area of the corresponding platform.
2. In the Add Certificate dialog that pops up, set the parameters as needed.
 - Add Android certificate
 ![](https://main.qcloudimg.com/raw/7821c57eef8b7a63019df23eb347720f.jpg)
 - Add iOS certificate
 ![](https://main.qcloudimg.com/raw/dc629d1f3ae746e699919930b1f99024.png)
3. Click **Confirm** to save the configuration.

### Editing an offline push certificate
1. Click **Edit** in the certificate area.
2. In the dialog box that pops up, modify the parameters as needed and click **Confirm** to save the configuration.

### Deleting an offline push certificate
> Once the certificate is deleted, push messages are no longer delivered. Deleted certificates cannot be restored. Proceed with caution.

1. Click **Delete** in the certificate area.
2. In the confirmation box that pops up, click **Confirm**.

## Activating Tencent Real-Time Communication (TRTC)
If you need features such as audio calling, video calling, and interactive live broadcasting in your current IM app, or you need to integrate the IM SDK and TRTC SDK at the same time, you can activate the [TRTC service](https://intl.cloud.tencent.com/document/product/647) in the **Activate TRTC** area. The system will create a TRTC app in the [TRTC Console](https://console.cloud.tencent.com/trtc), which has the same SDKAppID as your current IM app. The two accounts and their authentications can be reused.

1. Click **Activate Now** in the **Activate TRTC** area.
2. In the Activate TRTC dialog that pops up, click **OK**.
