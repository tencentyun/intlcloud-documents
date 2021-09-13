[](id:que10)
### How to obtain the package name for an Android project?
You can obtain the package name in the `Mainfest.xml` file of your Android project.
```
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
	package="com.huawei.player"
	android:versionCode="20181111"
	android:versionName="1.0">
```

[](id:que11)
### How to obtain the bundle ID for an iOS project?
You can obtain the bundle ID in **General > Identity** in Xcode, as shown below:
![](https://main.qcloudimg.com/raw/56571d560da04bf6563ccae91d32b75a.png)

[](id:que12)
### Can I renew a trial license after it expires?
You can use a trial license for 28 days at most. When it first expires after 14 days, you can renew it for another 14 days. After 28 days, please [purchase a license](https://intl.cloud.tencent.com/document/product/1071/38546).
If you renew a trial license within the first 14 days, the license will expire 28 days after the time of license application; if you renew a trial license that has expired once, the renewed license will expire 14 days after renewal.

- For example, if you apply for a trial license at `2021-08-12 10:28:41`, it will expire 14 days later, at `2021-08-26 10:28:41`.
- You can renew the trial license once for free. If you renew it within the first 14 days, it will expire at `2021-09-09 10:28:41`; if you renew it after the first 14 days, at `2021-08-30 22:26:20`, it will expire at `2021-09-13 22:26:20`.

[](id:que13)
### Can I change the package name for an Android project or the bundle ID for an iOS project if I use a trial license?
Yes, you can.
In the CSS console, go to **MLVB SDK** > [**License Management**](https://console.cloud.tencent.com/live/license) and click **Edit** to change the bundle ID and package name.

[](id:que14)
### Can I change the package name for an Android project or the bundle ID for an iOS project if I use an official license?
No, you can’t.

[](id:que15)
### Can I use a license for multiple applications at the same time?
Each license can be bound to only 1 package name and bundle ID. If you want to use MLVB features in multiple applications, you need to purchase multiple licenses.

[](id:que1)
### Do I have to purchase an MLVB license?
You can use the stream publishing feature of the MLVB SDK only if you have an MLVB license.
>! You cannot unlock MLVB features with a UGSV license.


[](id:que2) 
### Is there a self-help purchase page for MLVB licenses?
No, there isn’t.
With a live publishing license (previously LiteAV_Smart license), you can use the LiteAV_Smart SDK on iOS and Android. With an enterprise edition license, you can use MLVB Enterprise Edition on iOS and Android. To purchase the licenses, please [contact our sales rep](https://intl.cloud.tencent.com/contact-sales).

[](id:que3)
### How does a live publishing license (previously LiteAV_Smart license) differ from an enterprise edition license?
You can use a live publishing license (previously LiteAV_Smart license) to unlock the publishing and playback features of the SDK, as well as basic beauty filters such as skin brightening and skin smoothing.
An enterprise edition license gives you access to additional features including advanced beauty filters (e.g. eye enlarging and face slimming), green screen, animated stickers, AI keying, etc. You can also use makeup and gesture materials to implement more features.

>?
>- You can use a live publishing license (previously LiteAV_Smart license) to unlock the publishing and playback features in all three editions of the MLVB SDK.
>- The advanced beauty filters provided by MLVB Enterprise Edition must be unlocked with an enterprise edition license.


[](id:que4)
### Can I use multiple licenses under the same account?
There is no limit on the number of licenses you use for an account, but to better manage your resources, you are advised to renew an existing license to extend your access to the SDK instead of adding a new license with the same package name.

[](id:que5)
### Can I add multiple licenses with the same package name?
Yes, you can. The validity periods of different licenses are calculated separately. You are not advised to add multiple licenses with the same package name.

[](id:que6)
### Can I modify a license?
You can renew an MLVB license to extend its validity period, but you cannot modify the package name of a license. Before adding a license, please make sure that your package name is not already used by another app in Google Play Store.

[](id:que7)
### I added multiple licenses. Why do they have the same `licenseurl` and `key`?
By default, licenses under the same account are assigned the same `licenseurl` and `key`. This ensures that trial licenses, official licenses, and licenses with different package names can share the API information.

>?You are not advised to commercially launch an app that uses a trial license. You can upgrade to the official version simply by adding an official license. You don’t have to modify the `licenseurl` or `key` in APIs.


[](id:que10)
### I have granted a sub-account full access to CSS and VOD, but why can’t it access the license page of the console?
#### Screenshot:
<img src="https://main.qcloudimg.com/raw/79d4365dcf5723f7a0c1e77c6ffea515.png" width=400px>

#### Analysis:
We updated APIs along with the MLVB SDK licenses. To access the license page of the console with a sub-account, you must use your root account to grant it separate access to licenses.
- If you want to allow your sub-account to query licenses only, associate the QcloudVCUBEReadOnlyAccess policy.
- If you want to give your sub-account full access to licenses, associate the QcloudVCUBEFullAccess policy.

For more information on how to associate permission policies with users/user groups, please see [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602).

>? All license operations are now independent of CSS and VOD. That means the QcloudVODFullAccess and QcloudLIVEFullAccess policies no longer apply to license APIs. You must grant access to licenses separately as described above.
