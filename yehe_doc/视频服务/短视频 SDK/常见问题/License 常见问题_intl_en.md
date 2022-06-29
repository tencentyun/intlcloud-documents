[](id:que0)
### What should I know about license versions?
The UGSV SDK is available in Lite edition and Basic edition. Starting from v4.5, a UGSV license (`TXUgcSDK.licence`) is required for the Basic edition. You need to put the license in your project directory and rename it.

Starting from v4.9, you can select whether to package the license into your project. When using the license, you need to call `setLicenceURL:` and `key:` to set the license URL and key.

>! Automatic license renewal is supported only since v4.9. It’s not supported in v4.5-4.7. You cannot use new licenses for versions earlier than v4.9, but you can use legacy licenses for v4.9. Note that you cannot pass in `null` as the URL or key. Set them to random values.

[](id:que1)

### Can I extend the validity period of a trial license?

A free trial license is valid for 14 days and can be renewed once, making the total trial duration 28 days. After your trial license expires, please purchase a license. To learn more, submit a ticket or [contact sales](https://intl.cloud.tencent.com/contact-us).

>! If you renew a trial license within the first 14 days, the license will expire 28 days after the time of license application; if you renew a trial license that has expired once, the renewed license will expire 14 days after renewal.
>- For example, if you apply for a trial license at 11:34:55 on May 25, 2022, it will expire 14 days later at 00:00:00 on June 9, 2022.
>- You can renew the trial license once for free. If you renew it within the first 14 days, it will expire at 10:28:41 on June 23, 2022; if you renew it after the first 14 days, for example, at 22:26:20 on July 3, 2022, it will expire at 00:00:00 on July 18, 2022.


[](id:que2)
### Can I change the Android package name or iOS bundle ID bound to my trial license?
Yes. Log in to the [VOD console](https://console.cloud.tencent.com/vod/license/video), find your trial license, and click **Edit** to change the information.

[](id:que3)
### Can I change the Android package name or iOS bundle ID bound to an official license?
You cannot change the package name or bundle ID bound to an official license. Before adding a license, make sure that your package name or bundle ID is not already used by another app.

[](id:que4)
### Can I use one license for multiple applications at the same time?
You can bind each license to only one package name and one bundle ID.

[](id:que5)
### How do I know what package name (for Android) or bundle ID (for iOS) to bind to a license?
When binding a license, make sure you enter the same bundle ID or package name as that of the app you launch in the App Store or Google Play Store.

[](id:que6)
### What should I do if the “license not exist” error occurs when I renew my license?
Go to the [UGSV SDK License](https://console.cloud.tencent.com/vod/license/video) page of the VOD console.
1. Check whether you are renewing your license as the **Admin**.
2. If not, contact the **Admin** to renew the license for you.

[](id:que7)
### What should I do if I fail to add a license?
Make sure that you are adding the license as the **Admin**.

[](id:que8)
### What should I do if license verification fails?
Check the following:
- Whether your license is valid
- Whether the package name bound to the license is the same as that of your project
- Whether the `LicenseUrl` of your license uses the HTTPS protocol

>? If the problem persists, **reinstall the app** or [submit a ticket](https://console.cloud.tencent.com/workorder/category). 


[](id:que9)
### If I don’t bind a bundle ID, can I use a license for my Android project?
Yes, you can. A bundle ID is for an iOS project and a package name for an Android project. You can enter a random value for bundle ID if you don’t use the SDK in an iOS project.



[](id:que11)

### Can a UGSV SDK license purchased by a personal account be used by a business account?
A license can only be used by the account that purchased it, regardless of whether the account is verified as an individual or corporate entity.



[](id:que13)

### Why can’t I receive notifications about license expiration?
Go to [Message Subscription](https://console.cloud.tencent.com/message/subscription) and subscribe to RT-Cube notifications. You can specify how to receive the notifications (for example, via **Message Center**, **Email**, or **SMS**). The system will send you notifications 30 days, 15 days, 7 days, and 1 day before your UGSV license expires.
