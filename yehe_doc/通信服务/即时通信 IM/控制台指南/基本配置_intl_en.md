Log in to the [IM console](https://console.cloud.tencent.com/im) and click the desired app to enter the app configuration page. You can manage basic configurations of your app using this page.

## Changing Version

You can click **Update** in the **Version** area to update the version or configuration of your app. For more information, refer to [Updating Apps](https://intl.cloud.tencent.com/document/product/1047/34577).

## Configuring Basic Information
![](https://main.qcloudimg.com/raw/6e02515de636967bfa924a077ed0a5c4.png)
In the **Basic Info** area, you can:
- Edit the app's basic information, including the name, type, and introduction.
- Disable or delete the app.
- Obtain the app key.

### Editing basic information
1. Click **Edit** next to **App Information** to edit app settings.
2. You can modify **Application Name**, **Application Type**, and **Application Intro**.
3. Click **Save**.

### Disabling or deleting an app
> A Tencent Cloud account can create up to 100 IM apps. To create more than 100 apps, disable and delete an app first.

Once an app is disabled, the services associated with its SDKAppID will be unavailable. **Only disabled apps can be deleted. Once an app (along with its SDKAppID) is deleted, the service it provides and all its data are lost. Proceed with caution.**

**Trial Edition Apps**
- Trial apps can be manually disabled.
 In the **Basic Information** area, click **Disable** next to **Status**. In the pop-up dialog box, click **OK**.
- Trial apps can be manually deleted.
 In the **Basic Information** area, click **Delete** next to **Status**. In the pop-up dialog box, click **OK**.

**Pro and Flagship Edition Apps**
- Apps that have been in arrears for seven days will be automatically **Disabled**. To delete such disabled apps, [contact us](https://console.cloud.tencent.com/workorder/category).
- Apps become **Expired** after refund and **Disabled** after seven days. To delete such disabled apps, [contact us](https://console.cloud.tencent.com/workorder/category).

**TRTC Trial Edition Apps**
Once a TRTC trial app is disabled by the TRTC administrator, you can [contact us](https://console.cloud.tencent.com/workorder/category) to disable and delete the app.


### Obtaining a key
**Keys are sensitive information. Keep it confidential and do not leak it.** Apps (SDKAppIDs) created before August 15, 2019 used the [ECDSA-SHA256](https://intl.cloud.tencent.com/document/product/1047/34385) signature algorithm by default, which uses a public key and a private key. You can update them to use the HMAC-SHA256 signature algorithm.

1. Click **Display key** next to **Key**.
2. Click **Copy** to copy and store the key information.
    The key can be used to generate UserSig. For more information, refer to [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385).

## Configuring Account Administrators
Account administrators can call RESTful APIs, disband groups, and perform operations on all members. You can use the default account administrator `administrator` or manually add a new account administrator.
![](https://main.qcloudimg.com/raw/19db2d23fd7ae62d0fa95c4e37458387.png)
<span id="AddAdmin"></span>
### Adding account administrators
1. Click **Add Administrator** next to **Account Administrator**.
2. In the pop-up Add Administrator dialog box, enter the administrator account name.
3. Click **Add**.

### Removing administrators
1. Click **Remove Administrators** next to **Account Administrator**.
2. In the pop-up Remove Administrator dialog box, select the administrator account you want to remove.
3. Click **Confirm**.

## Managing Offline Push Certificates

### Adding offline push certificates

1. Click **Add certificate** in the push settings area of the corresponding platform.
2. In the pop-up Add Certificate dialog box, configure related parameters.
 - Adding Android certificates
 ![](https://main.qcloudimg.com/raw/11842c1b9d44d7a13e53457ebc0d189d.png)
 - Adding iOS certificates
 ![](https://main.qcloudimg.com/raw/416ec3e78bf7846fae2276d56df1256d.png)
3. Click **OK** to save the configuration.

### Editing offline push certificates
1. Click **Edit** in the certificate area.
2. In the pop-up dialog box, modify related parameters and click **OK** to save the configuration.

### Deleting offline push certificates
> Once the certificate is deleted, push messages are no longer delivered. Deleted certificates cannot be restored. Proceed with caution.

1. Click **Delete** in the certificate area.
2. In the pop-up confirmation box, click **OK**.

## Enabling Tencent Real-Time Communication (TRTC)
If you need features such as audio calls, video calls, and interactive live broadcasting in your IM app, or need to integrate the IM SDK and TRTC SDK at the same time, enable [TRTC](https://intl.cloud.tencent.com/document/product/1047) in the **Tencent Real-Time Communication (TRTC)**. The system will create a TRTC app in the [TRTC console](https://console.cloud.tencent.com/trtc), which has the same SDKAppID as your current IM app. The two apps use the same account and authentication.

1. Click **Activate** in the **Tencent Real-Time Communication (TRTC)** area.
2. In the pop-up Tencent Real-Time Communication (TRTC) dialog box, click **OK**.
