### What should I know about license versions?

The UGSV SDK is available in the Basic Edition and Enterprise Edition. Starting from v4.5, a license is required. The Basic Edition requires only the UGSV license (`TXUgcSDK.licence`), while the Enterprise Edition also requires the Pitu license (`YTFaceSDK.licence`). You can place the licenses into the project directory and rename them accordingly.

Starting from v4.9, the license usage was changed. You can select whether to package the license into the project. When using the license, you need to call the `setLicenceURL:key:` API to set the license URL and key.

>!SDK v4.5-4.7 does not support automatic license renewal, which is supported for v4.9 and later. SDK v4.9 is compatible with the licenses on earlier versions (you cannot pass in `null` for `url` and `key`. If needed, you can pass in a random string for them). However, the licenses on later versions cannot be used on SDK versions earlier than v4.9.



### Can I renew a trial license after it expires?

You can apply for a free trial license which is valid for 14 days and can be renewed for once, making the total trial duration 28 days. You can purchase an [official version](https://intl.cloud.tencent.com/document/product/266/42077) after the trial license expires.

>! If you renew a trial license within the first 14 days, the license will expire 28 days after the time of license application; if you renew a trial license that has expired once, the renewed license will expire 14 days after renewal.
>- For example, if you apply for a trial license on `2021-08-12 10:28:41`, it will expire 14 days later, on `2021-08-26 10:28:41`.
>- You can renew the trial license once for free. If you renew it within the first 14 days, it will expire on `2021-09-09 10:28:41`; if you renew it after the first 14 days, for example, on `2021-08-30 22:26:20`, it will expire on `2021-09-13 22:26:20`.



### Can I change the package name for an Android project or the bundle ID for an iOS project if I use a trial license?

Yes. Log in to the [VOD console](https://console.cloud.tencent.com/vod/license/video), select the trial license, and click **Edit** in the top right to make changes.



### Can I change the package name for an Android project or the bundle ID for an iOS project if I use an official license?

On the current version, you **cannot** change the package name and bundle ID for an official license. This capability will be available in future versions.



### Can I use one license for multiple applications at the same time?

Each license can authorize only one `PackageName` and `BundleID` and cannot be used for multiple applications.



### How do I confirm the binding relationship of a license (`PackageName` on Android and `BundleID` on iOS)?

When binding a license, you need to confirm the bundle ID of the application to be launched on App Store or the package name of the application to be launched in an application market on Android.



### What should I do if the “license not exist” error occurs when I renew my license?

Log in to the VOD console, click [**UGSV SDK License**](https://console.cloud.tencent.com/vod/license/video), and follow the steps below to troubleshoot the error.

1. Make sure that you are renewing your license as the **Admin**.
   ![img](https://main.qcloudimg.com/raw/446b60171da15bee7b10537ea2f63f32.png)
2. If you operate on a **non-admin** page, please contact the **Admin** to renew the license for you.



### What should I do if I fail to add a license?

Make sure that you are adding the license as the **Admin**.



### What should I do if license verification fails?

Follow these steps to fix the problem:

- Make sure that your license is still valid.
- Make sure the package name in the license info is the same as that in the project package.
- Make sure that the `LicenseUrl` of your license uses the HTTPS protocol.

>? If the problem persists, **reinstall the application** or [submit a ticket](https://console.cloud.tencent.com/workorder/category).



### Can I use the license for Android without entering `BundleID`?

Yes. `BundleID` for iOS is like the `PackageName` for Android. You can enter a random value if you don’t integrate the iOS client.



### 精简版的短视频 SDK，想升级成基础版 License，要怎么操作？

购买点播流量资源包 50TB、200TB 或 1PB 获取基础版 License 使用权。

>? 目前只支持短视频 License 由精简版升级至基础版，升级的 License 为对应的资源包赠送的 License 规格。



### Can a UGSV SDK license purchased by an individual be used by an enterprise?

The license can be used by the account that purchased it, with no requirement for individual or enterprise identity verification.



### I have granted a sub-account full access to CSS and VOD, but why can’t it access the license page of the console?

![img](https://main.qcloudimg.com/raw/7423d2e7912de344052c7891629d528b.png)

We updated APIs along with the new-version SDK licenses. To access the license page of the console with a sub-account, you must use your root account to grant it separate access to licenses.

- If you want to grant your sub-account query permission only, associate the `QcloudVCUBEReadOnlyAccess` policy with it.
- If you want to grant your sub-account all operation permissions, associate the `QcloudVCUBEFullAccess` policy with it.

For more information on how to associate permission policies with users/user groups, please see [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602).

>? All license operations are now independent of CSS and VOD. That means the `QcloudVODFullAccess` and `QcloudLIVEFullAccess` policies no longer apply to license APIs. You must grant access to licenses separately as described above.