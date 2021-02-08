[](id:que1)
### Do I have to purchase an MLVB license?
You can use the stream pushing feature of the MLVB SDK only if you have an MLVB license.
>! You cannot UGSV licenses to access MLVB features.


[](id:que2)
### Is there a purchase page for MLVB licenses?
No, there isn’t.
Please [contact Tencent Cloud sales] to apply for a license for the Basic or Enterprise Edition SDK.

[](id:que3)
### How does an MLVB Basic Edition license differ from an MLVB Enterprise Edition license?
With an MLVB Basic Edition license, you can use the stream pushing and playback features of the SDK, as well as basic beauty filters such as skin brightening and skin smoothing.
An MLVB Enterprise Edition license offers additional features including advanced beauty filters (e.g. eye enlarging and face slimming), green screen, animated stickers, AI keying, etc. You can also use makeup and gesture materials to explore more features.

>?
>- You can use a Basic Edition license to unlock the stream pushing and playback features in all three editions of the SDK.
>- The advanced beauty filters in the Enterprise Edition SDK must be unlocked using an Enterprise Edition license.


[](id:que4)
### Can I use multiple licenses for the same account?
There is no limit on the number of licenses you use for an account, but to better manage your resources, you are advised to renew an existing license to extend your access to the SDK instead of adding a new license with the same package name.

[](id:que5)
### Can I add multiple licenses with the same package name?
Yes, you can, but the validity periods of different licenses are calculated separately. You are not advised to add multiple licenses with the same package name.

[](id:que6)
### Can I modify a license?
You can renew an MLVB license to extend its validity period, but you cannot modify the package name of a license. Before adding a license, please make sure that your package name is not already used by another app in Google Play Store.

[](id:que7)
### I added multiple licenses. Why do they have the same `licenseurl` and `key`?
By default, licenses under the same account are assigned the same `licenseurl` and `key`. This ensures that trial licenses, official licenses, and licenses with different package names can share the API information.

>?You are not advised to launch an app that uses a trial license. You can upgrade to the official version simply by adding an official license, without the need to modify the `licenseurl` or `key` in the API.


