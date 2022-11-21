>? **We made some changes to the `TUICallEngine` APIs in the latest version (v1.1.0.103) of the SDK.**
>- If an Android project build error occurs due to the Maven update mechanism, try troubleshooting the issue using the following two methods:
	  - Update `TUICallKit` to the latest version.
	  - Specify the version of the `tuicallengine` dependency in `tuicallkit/build.gradle`: `com.tencent.liteav.tuikit:tuicallengine:1.0.0.53`.
>- If an iOS project build error occurs when you execute `pod update`, try troubleshooting the issue using the following two methods:
	  - Update `TUICallKit` to the latest version.
	  - Add `pod 'TUICallEngine', '1.0.0.53'` to `Podfile`.

### Version 1.1.0.103 Released on September 30, 2022
- Android & iOS: Optimized the feature of inviting new members to the current group call.
- Android & iOS: Optimized the call process to avoid the charging of recording, moderation, and other fees before a call is answered.
- Android & iOS: Added support for custom offline notifications.
- Android & iOS: Changed the parameters of some **TUICallEngine** APIs. For details, see [call()](https://www.tencentcloud.com/document/product/647/51006#call), [groupCall()](https://www.tencentcloud.com/document/product/647/51006#groupcall), [inviteUser()](https://www.tencentcloud.com/document/product/647/51006#inviteuser), and [onCallReceived()](https://www.tencentcloud.com/document/product/647/51007#oncallreceived).
- Android & iOS: Fixed occasional callback errors during a group call.
- Android & iOS: Fixed the status abnormal issue caused by repeated login or expired `UserSig`.
- iOS: Fixed the issue where, when a mixed-language `TUICallKit` project is built with Objective-C and Swift, an error occurs when `init` is called.
- Android: Fixed the issue where an error occurs when the floating window feature is integrated for a Kotlin project.

### Version 1.0.0.53 Released on August 15, 2022

#### First release: 
- Android & iOS: Supports one-to-one and group audio/video calls.
- Android & iOS: Supports offline call push for mainstream devices on the market.
- Android & iOS: Supports custom profile photos and aliases.
- Android & iOS: Supports floating call windows.
- Android & iOS: Supports custom ringtones.
- Android & iOS: Supports receiving calls when the user is logged in on multiple platforms.