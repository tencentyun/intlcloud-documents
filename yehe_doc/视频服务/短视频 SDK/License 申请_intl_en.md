## Applying for a Trial License
**You can apply for a Basic Edition trial license (14-day validity period) to explore the SDK. Each account is eligible for two applications. See below for detailed instructions.**
1. Go to the Tencent Cloud website, log in to the [VOD console](https://console.cloud.tencent.com/vod/license), click **Edit**, and enter the information as required. For **Package Name**, enter the package name of your Android app, and for **Bundle ID**, enter the Bundle ID of your iOS app.
2. After adding a trial license successfully, you will be able to view the information of the license. Note the **Key** and **LicenseUrl**, which you must pass in when initializing the SDK.
For the full version, please contact [Tencent Cloud sales](https://intl.cloud.tencent.com/contact-us) to purchase a license.


[](id:use)
## Using a License
Call the following method to configure your license before using the APIs of the SDK.

- Recommended configuration for iOS: add the following in `[AppDelegate application:didFinishLaunchingWithOptions:]`:
```
[TXUGCBase setLicenceURL:LicenceUrl key:Key];
```
- Recommended configuration for Android: add the following in `application`:
```
TXUGCBase.getInstance().setLicence(context, LicenceUrl, Key);
```

[](id:check)
## Viewing License Information
After the license is successfully configured, you can call the below method to view the license information. Please note that it may take a while for the configuration to be completed. The exact time needed depends on your network conditions.

- iOS:
```
NSLog(@"%@", [TXUGCBase getLicenceInfo]);
```
- Android:
```
TXUGCBase.getInstance().getLicenceInfo(context);
```

[](id:faq)
## FAQs

1. **Can I extend the validity period of a trial license when it expires?**
You can use a trial license for 28 days at most and cannot extend the period. Please purchase an official license after your trial license expires.
2. **Can I change the `PackageName` (for Android) or `BundleID` (for iOS) of a trial license?**
Yes, you can. In the trial license information page of the console, click *Edit* on the right to modify the information.
3. **Can I use the same license for multiple apps?**
   Each license can authorize only one `PackageName` and `BundleID` and cannot be used for multiple apps.
