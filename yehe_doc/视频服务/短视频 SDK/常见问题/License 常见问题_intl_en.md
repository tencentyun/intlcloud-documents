[](id:que0)
### What should I know about license versions?
The UGSV SDK is available in the Basic Edition and Enterprise Edition. Starting from v4.5, a license is required. The Basic Edition requires only the UGSV license (`TXUgcSDK.licence`), while the Enterprise Edition also requires the Pitu license (`YTFaceSDK.licence`). You can place the licenses into the project directory and rename them accordingly.

Starting from v4.9, the license usage was changed. You can select whether to package the license into the project. When using the license, you need to call the `setLicenceURL:key:` API to set the license URL and key.
>!Automatic license renewal is supported only since v4.9 and not in v4.5-4.7. You can use legacy licenses for v4.9 (pass in a random non-null string for `url` and `key`), but you cannot use new licenses for versions before v4.9.


[](id:que1)
### Can I extend the validity period of the trial license?

A free trial license is valid for 14 days and can be renewed once, making the total trial duration 28 days. After your trial license expires, please purchase a license. To learn more, submit a ticket or [contact sales](https://intl.cloud.tencent.com/contact-us).

>! If you renew a trial license within the first 14 days, the license will expire 28 days after the time of license application; if you renew a trial license that has expired once, the renewed license will expire 14 days after renewal.
>- For example, if you apply for a trial license on `2021-08-12 10:28:41`, it will expire 14 days later, on `2021-08-26 10:28:41`.
>- You can renew the trial license once for free. If you renew it within the first 14 days, it will expire on `2021-09-09 10:28:41`; if you renew it after the first 14 days, for example, on `2021-08-30 22:26:20`, it will expire on `2021-09-13 22:26:20`.


[](id:que2)
### Can I change the Android package name or iOS bundle ID bound to my trial license?
Yes. Log in to the [VOD console](https://console.cloud.tencent.com/vod/license/video), select the trial license, and click **Edit** in the top right to make changes.

[](id:que3)
### Can I change the Android package name or iOS bundle ID bound to an official license?
In the current version, you **cannot** change the package name or bundle ID for an official license, but we may support this in future versions.

[](id:que4)

### Can I use one license for multiple applications at the same time?
Each license can authorize only one `PackageName` and `BundleID` and cannot be used for multiple applications.

[](id:que5)
### How do I confirm the binding relationship of a license (`PackageName` on Android and `BundleID` on iOS)?
When binding a license, you need to confirm the bundle ID of the application to be launched on App Store or the package name of the application to be launched in an application market on Android.

[](id:que6)
### What should I do if the “license not exist” error occurs when I renew my license?
Log in to the VOD console, click [**UGSV SDK License**](https://console.cloud.tencent.com/vod/license/video), and follow the steps below to troubleshoot the error.
1. Make sure that you are renewing your license as the **Admin**.
2. If you operate on a **non-admin** page, please contact the **Admin** to renew the license for you.

[](id:que7)
### What should I do if I fail to add a license?
Make sure that you are adding the license as the **Admin**.

[](id:que8)
### What should I do if license verification fails?
Follow these steps to fix the problem:
- Make sure that your license is still valid.
- Make sure the package name in the license info is the same as that in the project package.
- Make sure that the `LicenseUrl` of your license uses the HTTPS protocol.

>? If the problem persists, **reinstall the application** or [submit a ticket](https://console.cloud.tencent.com/workorder/category). 


[](id:que9)
### Can I use a license only for Android without specifying `BundleID`?
Yes. `BundleID` for iOS is like `PackageName` for Android. You can enter a random value for `BundleID` if you don’t need to integrate the SDK into an iOS project.

[](id:que10)
### How do I upgrade the SDK from Lite Edition to Basic Edition?
Purchase a 50 TB, 200 TB, or 1 PB VOD traffic package.
>? You can only upgrade from Lite Edition to Basic Edition currently. The type of license used for the Basic Edition after the upgrade depends on the package purchased.

[](id:que11)
### Can a UGSV SDK license purchased by an individual be used by an enterprise?
A license can be used by the account that purchased it, regardless of whether the account is verified as an individual or corporate entity.



#### Analysis:
We updated APIs along with the new-version SDK licenses. To access the license page of the console with a sub-account, you must use your root account to grant it separate access to licenses.
- If you want to grant your sub-account query permission only, associate the `QcloudVCUBEReadOnlyAccess` policy with it.
- If you want to grant your sub-account all operation permissions, associate the `QcloudVCUBEFullAccess` policy with it.

For more information on how to associate permission policies with users/user groups, please see [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602).

>? All license operations are now independent of CSS and VOD. That means the `QcloudVODFullAccess` and `QcloudLIVEFullAccess` policies no longer apply to license APIs. You must grant access to licenses separately as described above.

[](id:que13)
### Why can’t I receive notifications about license expiration, etc.?
To receive notifications about UGSV licenses, subscribe to RT-Cube in [Message Subscription](https://console.cloud.tencent.com/message/subscription) and choose how you want to receive the notifications (via **Message Center**, **Email**, **SMS**, etc.). The system will send you notifications 30 days, 15 days, 7 days, and 1 day before your UGSV license expires.
