The offline call push feature enables your application to receive audio/video calls even if it runs in the background or is offline. `TUICallKit` uses the Apple Push Notification service (APNs) provided by Apple to push message notifications.

## Step 1. Configure offline push

1. **Apply for an APNs certificate** as instructed in step 1 in [APNs](https://www.tencentcloud.com/document/product/1047/39157#.E6.AD.A5.E9.AA.A41.EF.BC.9A.E7.94.B3.E8.AF.B7-apns-.E8.AF.81.E4.B9.A6).

2. **Configure in the IM console** as instructed in step 2 in [APNs](https://www.tencentcloud.com/document/product/1047/39157#.E6.AD.A5.E9.AA.A42.EF.BC.9A.E4.B8.8A.E4.BC.A0.E8.AF.81.E4.B9.A6.E5.88.B0.E6.8E.A7.E5.88.B6.E5.8F.B0).

3. **Get `deviceToken` from Apple every time the user logs in to the application** as instructed in step 3 in [APNs](https://www.tencentcloud.com/document/product/1047/39157#.E6.AD.A5.E9.AA.A43.EF.BC.9Aapp-.E5.90.91.E8.8B.B9.E6.9E.9C.E5.90.8E.E5.8F.B0.E8.AF.B7.E6.B1.82-devicetoken).

4. **Upload `deviceToken` to Tencent Cloud after logging in to the IM SDK** as instructed in step 4 in [APNs](https://www.tencentcloud.com/document/product/1047/39157#.E6.AD.A5.E9.AA.A44.EF.BC.9A.E7.99.BB.E5.BD.95-im-sdk-.E5.90.8E.E4.B8.8A.E4.BC.A0-devicetoken-.E5.88.B0.E8.85.BE.E8.AE.AF.E4.BA.91).

>? You can ignore other steps in [APNs](https://www.tencentcloud.com/document/product/1047/39157), as `TUICallKit` has completed the subsequent steps.

## Step 2. Configure the project

To add the required permissions to your application, enable the push notification feature in your Xcode project.

Open the project in **Xcode**, select your **project** and **target**, click **+** on the **Signing & Capabilities** tab, and select **Push Notifications** to add this permission. The result is as shown below:

![](https://qcloudimg.tencent-cloud.cn/image/document/954340261de64a1aab536cf8744d6136.png)

After completing the above steps, you can run your project to try out the offline call push feature of `TUICallKit`.

## FAQs 

### 1. What should I do if push messages cannot be received and the backend reports the "bad devicetoken" error?

For Apple devices, `deviceToken` is related to the current compilation environment. If the certificate ID used to upload `deviceToken` to Tencent Cloud after logging in to the IM SDK is inconsistent with the environment token, the error will be reported.

If the compilation environment is `Release`, the `- application:didRegisterForRemoteNotificationsWithDeviceToken:` callback returns the release environment token. In this case, `businessID` must be set to the certificate ID of the production environment.

If the compilation environment is `Debug`, the `- application:didRegisterForRemoteNotificationsWithDeviceToken:` callback returns the development environment token. In this case, `businessID` must be set to the certificate ID of the development environment.

```objectivec
V2TIMAPNSConfig *confg = [[V2TIMAPNSConfig alloc] init];
/* You need to register a developer certificate with Apple, download and generate the certificate (P12 file) in their developer accounts, and upload the generated P12 file to the Tencent certificate console. The console will automatically generate a certificate ID and pass it to the `businessID` parameter.*/
// Push certificate ID
confg.businessID = sdkBusiId;
confg.token = self.deviceToken;
[[V2TIMManager sharedInstance] setAPNS:confg succ:^{

} fail:^(int code, NSString *msg) {

}];
```

### 2. What should I do if `deviceToken` is not returned for registration occasionally or APNs' request for token fails in the iOS development environment?

This problem is caused by instability of APNs. You can fix it in the following ways:

1. Insert a SIM card into the phone and use the 4G network.

2. Uninstall and reinstall the application, restart the application, or shut down and restart the phone.

3. Use a package for the production environment.

4. Use another iPhone.
