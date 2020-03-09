Log in to [IM Console](https://console.cloud.tencent.com/im) and click the target app card to go to the app’s basic configuration page. On this page, you can manage the basic configuration of your app according to business needs.

## Changing the Service Version

You can update the service version or configuration of your app by clicking **Upgrade** in the **Service Version** area. For more information, see [Upgrading Apps](https://cloud.tencent.com/document/product/269/32577#.E5.8D.87.E7.BA.A7.E5.BA.94.E7.94.A8).

## Configuring Basic Information
![](https://main.qcloudimg.com/raw/6e02515de636967bfa924a077ed0a5c4.png)
In the **Basic Information** area, you can:
- Edit the app’s basic information, including the name, type, and introduction of the app.
- Disable or delete the app.
- Obtain the key of the app.

### Editing basic information
1. Click **Edit** for **App Information** to edit app settings.
2. You can modify **App name**, **App type**, and **App introduction**.
3. Click **Save**.

### Disabling the app
Note that after the app is disabled, services related to SDKAppID will be unavailable.

1. Click **Disabled** for **Status**.
2. In the "Disable Notification" dialog that appears, click **OK**.

## Deleting the App
You can only delete the app if it is in the **Disabled** state. **Note that after the app is deleted, services related to SDKAppID will be unavailable.**

1. Click **Delete** for **Status**.
2. In the "Deletion Notification" dialog box that appears, click **OK**.

### Obtaining the key
**Keys are sensitive information, and therefore be sure to keep it confidential and prevent it from being leaked.** By default, apps (SDKAppIDs) created before August 15, 2019 use the [ECDSA-SHA256](https://cloud.tencent.com/document/product/269/32688#ECDSA-SHA256) signature algorithm that uses a public key and a private key. You can update to the HMAC-SHA256 signature algorithm if needed.

1. Click **Show key** for **Key**.
2. Click **Copy** to copy and save the key.
  The key can be used to generate UserSig. For more information, see [Generating UserSig](https://cloud.tencent.com/document/product/269/32688).

## Configuring Account Admins
Account admins can call RESTful APIs, dismiss groups, and perform operations on all members. You can directly use the default account admin `administrator`, or manually add new account admins.
![](https://main.qcloudimg.com/raw/19db2d23fd7ae62d0fa95c4e37458387.png)
<span id="AddAdmin"></span>
### Adding account admins
1. Click **Add admin** for **Account Admin**.
2. In the "Add Admin" dialog that appears, click **OK**.
3. Click **Add**.

### Removing admins
1. Click **Remove admin** for **Account Admin**.
2. In the "Remove Admin" dialog that appears, select the admin account that you want to remove.
3. Click **Confirm**.

## Managing offline push certificates

### Adding offline push certificates

1. Click **Add certificate** in the push settings area of the corresponding platform.
2. In the "Add Certificate" dialog that appears, set the parameters as needed.
 - Add Android certificates
 ![](https://main.qcloudimg.com/raw/11842c1b9d44d7a13e53457ebc0d189d.png)
 - Add iOS certificates
 ![](https://main.qcloudimg.com/raw/416ec3e78bf7846fae2276d56df1256d.png)
3. Click **OK** to save the setting.

### Editing offline push certificates
1. Click **Edit** in the certificate area.
2. In the dialog box that appears, modify the parameters as needed and click **OK** to save the settings.

### Deleting offline push certificates
>Note that after certificates are deleted, push notifications cannot be received and data cannot be restored.

1. Click **Delete** in the certificate area.
2. In the confirmation box that appears, click **Confirm**.

## Activating Tencent Real-Time Communication (TRTC)
If you need features such as audio calling, video calling, and interactive live broadcasting in your current IM app, or you need to integrate the IM SDK and the TRTC SDK at the same time, you can activate the [TRTC service](https://cloud.tencent.com/document/product/647) in the **Activate TRTC** area. The system will create a TRTC app in [TRTC Console](https://console.cloud.tencent.com/trtc), which has the same SDKAppID as your current IM app. Both accounts and their authentication information can be reused.

1. Click **Activate Now** in the **Activate TRTC** area.
2. In the "Activate TRTC" dialog that appears, click **OK**.
