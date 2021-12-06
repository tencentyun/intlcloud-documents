### What should I know about license versions?

The UGSV SDK is available in the Basic Edition and Enterprise Edition. Starting from v4.5, a license is required. The Basic Edition requires only the UGSV license (`TXUgcSDK.licence`), while the Enterprise Edition also requires the Pitu license (`YTFaceSDK.licence`). You can place the licenses into the project directory and rename them accordingly.

Starting from v4.9, the license usage was changed. You can select whether to package the license into the project. When using the license, you need to call the `setLicenceURL:key:` API to set the license URL and key.

>!SDK v4.5-4.7 does not support automatic license renewal, which is supported for v4.9 and later. SDK v4.9 is compatible with the licenses on earlier versions (you cannot pass in `null` for `url` and `key`. If needed, you can pass in a random string for them). However, the licenses on later versions cannot be used on SDK versions earlier than v4.9.



### Can I renew a trial license after it expires?

You can apply for a free trial license which is valid for 14 days and can be renewed for once, making the total trial duration 28 days. You can purchase an official version after the trial license expires. If you have any questions, submit a ticket or [contact sales](https://intl.cloud.tencent.com/contact-us).

>! If you renew a trial license within the first 14 days, the license will expire 28 days after the time of license application; if you renew a trial license that has expired once, the renewed license will expire 14 days after renewal.
>- For example, if you apply for a trial license on `2021-08-12 10:28:41`, it will expire 14 days later, on `2021-08-26 10:28:41`.
>- You can renew the trial license once for free. If you renew it within the first 14 days, it will expire on `2021-09-09 10:28:41`; if you renew it after the first 14 days, for example, on `2021-08-30 22:26:20`, it will expire on `2021-09-13 22:26:20`.



### Can I change the package name for an Android project or the bundle ID for an iOS project if I use a trial license?

Yes. Log in to the [VOD console](https://console.cloud.tencent.com/vod/license/video), select the trial license, and click **Edit** in the top right to make changes.



### Can I use one license for multiple applications at the same time?

Each license can authorize only one `PackageName` and `BundleID` and cannot be used for multiple applications.



### How do I confirm the binding relationship of a license (`PackageName` on Android and `BundleID` on iOS)?

When binding a license, you need to confirm the bundle ID of the application to be launched on App Store or the package name of the application to be launched in an application market on Android.



### What should I do if license verification fails?

Follow these steps to fix the problem:

- Make sure that your license is still valid.
- Make sure the package name in the license info is the same as that in the project package.
- Make sure that the `LicenseUrl` of your license uses the HTTPS protocol.

>? If the problem persists, **reinstall the application** or [submit a ticket](https://console.cloud.tencent.com/workorder/category).


### Can I use the license for Android without entering `BundleID`?

Yes. `BundleID` for iOS is like the `PackageName` for Android. You can enter a random value if you don’t integrate the iOS client.


### Can a UGSV SDK license purchased by an individual be used by an enterprise?

The license can be used by the account that purchased it, with no requirement for individual or enterprise identity verification.
