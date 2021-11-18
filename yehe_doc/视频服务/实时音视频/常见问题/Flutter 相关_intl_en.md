[](id:que1)
### The demo is running on two mobile phones, but why can't they display the images of each other?
Make sure that the two mobile phones use different `UserIDs`. With TRTC, you cannot use the same `UserID` on two devices simultaneously unless the `SDKAppIDs` are different.

[](id:que2)
### What firewall restrictions does TRTC face?
The SDK uses the UDP protocol for audio/video transmission and therefore cannot be used in office networks that block UDP. If you encounter such a problem, see [How to Deal with Firewall Restrictions](https://intl.cloud.tencent.com/document/product/647/35164) to troubleshoot the issue.

[](id:que3)
### What should I do if the iOS app crashes when I build and run it?
Check if it is caused by the debug mode issue on iOS 14 and above. For details, see this [Flutter document](https://flutter.cn/docs/development/ios-14#launching-debug-flutter-without-a-host-computer).

[](id:que4)
### What should I do if videos do not show on iOS but do on Android?
Make sure that in `info.plist` of your project, the value of `io.flutter.embedded_views_preview` is `YES`.

[](id:que5)
### What should I do if an error occurs when I run CocoaPods for my iOS project after updating to the latest version of the SDK?
1. Delete `Podfile.lock` in the iOS directory.
2. Run `pod repo update`.
3. Run `pod install`.
4. Run CocoaPods again.

[](id:que6)
### What should I do if Android Studio fails to build my project with the error “Manifest merge failed”?
1. Open `/example/android/app/src/main/AndroidManifest.xml`.
2. Add `xmlns:tools="http://schemas.android.com/tools"` to `manifest`.
3. Add `tools:replace="android:label"` to `application`.

![img](https://main.qcloudimg.com/raw/7a37917112831488423c1744f370c883.png)

[](id:que7)
### What should I do if an error occurs due to the absence of signatures when I debug my project on a real device?
If the error message is as shown below:
![](https://main.qcloudimg.com/raw/809ae94061575b4e670f3a80ac9f3781.png)
1. Purchase an Apple certificate and you will be able to debug on a real device after configuration and signing.
2. Configure in `target > signing & capabilities` after purchase.

[](id:que8)
### Why can’t I find the corresponding file after deleting/adding content in the swift file of the plugin?
In the directory of your main project, run `pod install` in the folder of `/ios`.

[](id:que9)
### What should I do if the error “Info.plist, error: No value at that key path or invalid key path: NSBonjourServices” occurs when I run my project?
Run `flutter clean` and run the project again.

[](id:que10)
### What should I do if an error occurs when I run `pod install`?
If the error message is as shown below:
![](https://main.qcloudimg.com/raw/73db67cfc9e6b934fed947b63c6d2120.png)
According to the message, the error is caused by the absence of `generated.xconfig`, and to fix the problem, you **need to run flutter pub get**.
>? This problem occurs after compilation with Flutter. You won’t run into the problem if you have a new project or have run `flutter clean`.

[](id:que11)
### What should I do if a dependency error occurs when I run my project on iOS?
If the error message is as shown below:
![](https://main.qcloudimg.com/raw/9102b3394560ca9df2f70549baabe3ff.png)
The error may occur because the pods target version fails to meet the requirements of the plugin being depended on. You need to change the target in the pods in question to the specified version.

[](id:que12)
### Does Flutter support custom capturing or rendering?
No, it doesn’t for the time being. For more information on platforms that support custom capturing and rendering, please see [Custom Capturing and Rendering > Supported Platforms](https://intl.cloud.tencent.com/document/product/647/35158).
