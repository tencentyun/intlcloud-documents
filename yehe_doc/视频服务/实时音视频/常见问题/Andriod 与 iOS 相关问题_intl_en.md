[](id:que1)
### What system volume types does TRTC support on mobile devices (Android and iOS)?
It supports two system volume types, i.e., call volume and media volume.
- Call volume is designed for call scenarios. It uses phones’ built-in acoustic echo cancellation (AEC) technique and offers lower audio quality than media volume does. In the call volume mode, the volume cannot be turned to 0 with the volume buttons, but the mics of Bluetooth earphones can be used for audio capture.
- Media volume is designed for music scenarios. It offers higher sound quality than call volume does. In the media volume mode, the volume can be turned to 0 with the volume buttons, and if you want to enable the AEC feature, the SDK will use its built-in acoustic processing algorithm to process the audio. With media volume, only the mics on phones can be used to capture audio.

[](id:que2)
### How do I set the resolution for push to 1080p in the SDK on mobile devices?
1080p is defined as `114` in `TX_Enum_Type_VideoResolution`. Just set the resolution by passing in the enumerated value.

[](id:que4)
### How do I implement the screen sharing feature in TRTC on mobile devices?	
- **Android**: version 7.2 and above support screen sharing. For detailed instructions on how to implement the feature, see [Real-Time Screen Sharing (Android)](https://intl.cloud.tencent.com/document/product/647/37337).
- **iOS**: version 7.2 and above support in-app screen sharing, and version 7.6 and above support both system-level and in-app screen sharing. For detailed instructions on how to implement the feature, see [Real-Time Screen Sharing (iOS)](https://intl.cloud.tencent.com/document/product/647/37338).



[](id:que5)
### Does TRTC support the 64-bit arm64-v8a architecture on Android?
TRTC has supported the arm64-v8a ABI since version 6.3.


[](id:que7)
### Does TRTC support Swift integration on iOS?
Yes. Just integrate the SDK in the same steps as you do a third-party library or by following the steps in [Demo Quick Start (iOS & macOS)](https://intl.cloud.tencent.com/document/product/647/35086).


[](id:que9)
### Can I run the TRTC SDK in the background on iOS?
Yes, you can. To run the SDK in the background, select the project, set **Background Modes** under **Capabilities** to **ON**, and check **Audio, AirPlay and Picture in Picture**, as shown below:
![](https://main.qcloudimg.com/raw/d960dfec88388936abce2d4cb77ac766.jpg)

[](id:que10)
### Can I listen for room exit by remote users on iOS?
You can use [onRemoteUserLeaveRoom](http://doc.qcloudtrtc.com/group__TRTCCloudDelegate__ios.html#afa7d16e1e4c66d938fc2bc69f3e34c28) to listen for room exit events. With this API, callbacks are triggered only if all users under the `VideoCall` mode or anchors under the `Live` mode leave the room. 

[](id:que11)
### How do I make a video call with the phone screen locked?
For how to implement features including offline answering, see [Real-Time Voice Call (Android) - Answer a call offline](https://intl.cloud.tencent.com/document/product/647/36068)

[](id:que12)
### Can Android and web users call each other?
Yes. They just need to use the same [SDKAppID](https://console.cloud.tencent.com/trtc/app) and enter the same room. For more information, see the documents below:
- [Demo Quick Start (Android)](https://intl.cloud.tencent.com/document/product/647/35084)
- [Demo Quick Start (Desktop Browser)](https://intl.cloud.tencent.com/document/product/647/35607)

[](id:que13)
### Can both anchors and viewers initiate co-anchoring during live streaming?
Yes. Both anchors and viewers can initiate a co-anchoring request using the same logic. For more information, please see [Demo Quick Start (Android)](https://intl.cloud.tencenxt.com/document/product/647/35108).

[](id:que14)

 

[](id:que15)
### Can I create N TRTC objects and log in to N rooms with N user IDs on the same page?
Yes. It is possible for a user to enter multiple rooms since [version 7.6](https://intl.cloud.tencent.com/document/product/647/34615).

[](id:que16_flutter)
### The demo is running on two mobile phones, but why can't they display the images of each other?
Please make sure that the two mobile phones use different user IDs when running the demo, as TRTC does not support the use of the same user ID on two devices simultaneously unless different SDKAppIDs are used.

[](id:que17_flutter)
### What firewall restrictions does TRTC face?
The SDK uses the UDP protocol for audio/video transmission and therefore cannot be used in office networks that block UDP. If you encounter such a problem, see [How to Deal with Firewall Restrictions](https://intl.cloud.tencent.com/document/product/647/35164) to troubleshoot the issue.

[](id:que18_flutter)
### What should I if the iOS app crashes when I build and run it?
Check if it is caused by the debug mode issue on iOS 14 and above. For details, see this [Flutter document](https://flutter.cn/docs/development/ios-14#launching-debug-flutter-without-a-host-computer).

[](id:que19_flutter)
### What should I do if videos do not show on iOS but do on Android?
Make sure that in `info.plist` of your project, the value of `io.flutter.embedded_views_preview` is `YES`.

[](id:que20_flutter)
### What should I do if an error occurs when I run CocoaPods on iOS after updating to the latest version of the SDK?
1. Delete `Podfile.lock` in the iOS directory.
2. Run `pod repo update`.
3. Run `pod install`.
4. Run CocoaPods again.

[](id:que21_flutter)
### What should I do if Android Studio fails to build my project with the error “Manifest merge failed”?
1. Open `/example/android/app/src/main/AndroidManifest.xml`.
2. Add `xmlns:tools="http://schemas.android.com/tools"` to manifest.
3. Add `tools:replace="android:label"` to application.

![img](https://main.qcloudimg.com/raw/7a37917112831488423c1744f370c883.png)

[](id:que22_flutter)
### What should I do if an error occurs due to the absence of signatures when I debug my project on a real device?
The error message is as shown in the figure:
![](https://main.qcloudimg.com/raw/809ae94061575b4e670f3a80ac9f3781.png)
1. Purchase an Apple certificate and you will be able to debug on a real device after configuration and signing.
2. Configure in `target > signing & capabilities` after purchase.

[](id:que23_flutter)
### Why can’t I find the corresponding file after deleting/adding content in the swift file of the plugin?
In the directory of your main project, run `pod install` in the folder of `/ios`.

[](id:que24_flutter)
### What should I do if the error “Info.plist, error: No value at that key path or invalid key path: NSBonjourServices” occurs when I run my project?
Run `flutter clean` and run the project again.

[](id:que25_flutter)
### What should I do if an error occurs when I run pod install?
The error message is as shown in the figure:
![](https://main.qcloudimg.com/raw/73db67cfc9e6b934fed947b63c6d2120.png)
According to the message, the error is caused by the absence of `generated.xconfig`, and to fix the problem, you **need to run flutter pub get**.
>? This problem occurs after compilation with Flutter. You won’t run into the problem if you have a new project or have run `flutter clean`.

[](id:que26_flutter)
### What should I do if a dependency error occurs when I run my project on iOS?
The error message is as shown in the figure:
![](https://main.qcloudimg.com/raw/9102b3394560ca9df2f70549baabe3ff.png)
The error may occur because the pods target version fails to meet the requirements of the plugin being depended on. You need to change the target in the pods in question to the specified version.












