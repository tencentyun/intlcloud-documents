This document describes how to quickly run the demo for the TRTC Flutter SDK.

>! Currently, screen sharing and device selection are not supported on Windows or macOS.

## Environment Requirements
- Flutter 2.0 or later
- **Developing for Android:**
  - Android Studio 3.5 or later
  - Devices with Android 4.1 or later
- **Developing for iOS and macOS:**
  - Xcode 11.0 or later
  - OS X 10.11 or later
  - A valid developer signature for your project
- **Developing for Windows:**
    - OS: Windows 7 SP1 or later (64-bit based on x86-64)
    - Disk space: At least 1.64 GB of space after the IDE and relevant tools are installed
    - [Visual Studio 2019](https://visualstudio.microsoft.com/zh-hans/downloads/)

## Prerequisites
You have [signed up for a Tencent Cloud account](https://intl.cloud.tencent.com) .

## Directions
[](id:step1)
### Step 1. Create an application
1. In the TRTC console, click **Development Assistance** > **[Demo Quick Run](https://console.cloud.tencent.com/trtc/quickstart)**.
2. Select **New** and enter an application name such as `TestTRTC`. If you have already created an application, select **Existing**.
3. Add or edit tags according to your needs and click **Create**.
![](https://qcloudimg.tencent-cloud.cn/raw/7d1d1940f02ee954c369b5f749e0c663.png)
>?
>- An application name can contain up to 15 characters. Only digits, letters, Chinese characters, and underscores are allowed.
>- Tags are used to identify and organize your Tencent Cloud resources. For example, an enterprise may have multiple business units, each of which has one or more TRTC applications. In this case, the enterprise can tag TRTC applications to mark out the unit information. Tags are optional and can be added or edited according to your actual business needs.

[](id:step2)
### Step 2. Download the SDK and demo source code
1. Download the SDK and [demo source code](https://github.com/LiteAVSDK/TRTC_Flutter/tree/master/TRTC-Simple-Demo) for the platform you are developing for.
2. Click **Next**.
![](https://main.qcloudimg.com/raw/9f4c878c0a150d496786574cae2e89f9.png)


[](id:step3)
### Step 3. Configure the demo project file
1. In the **Modify Configuration** step, select your platform.
2. Find and open the `TRTC-Simple-Demo/lib/debug/GenerateTestUserSig.dart` file.
3. Set parameters in `GenerateTestUserSig.dart` as follows.
<ul><li/>SDKAPPID: A placeholder by default. Set it to the actual `SDKAppID`.
	<li>`SECRETKEY`: A placeholder by default. Set it to the actual secret key.</ul>
<img src="https://qcloudimg.tencent-cloud.cn/raw/e210b7b71cf273de59d6e2df917101e4.png">

4. Click **Next** to complete the creation.
5. After compilation, click **Return to Overview Page**.

>?
>- In this document, the method to obtain `UserSig` is to configure the secret key in the client code. In this method, the secret key is vulnerable to decompilation and reverse engineering. Once your secret key is leaked, attackers can steal your Tencent Cloud traffic. Therefore, **this method is only suitable for locally running a demo project and debugging**.
>- The best practice is to integrate the calculation code of `UserSig` into your server and provide an application-oriented API. When `UserSig` is needed, your application can send a request to your server for a dynamic `UserSig`. For more information, see [How do I calculate `UserSig` during production?](https://intl.cloud.tencent.com/document/product/647/35166).

[](id:step4)
### Step 4. Compile and run the demo
1. Run `flutter pub get`.
2. Compile, run, and test the project.
<dx-tabs>
:::  Android
1. Run `flutter run`.
2. Open the demo project with Android Studio (3.5 or later), and click **Run**.
:::
::: iOS
1. Go to the iOS directory and run `pod install`.
2. Open `/ios` in the source code directory with Xcode (11.0 or later). Compile and run the demo project.
:::
::: Windows
1. Run `flutter config --enable-windows-desktop`.
2. Run `flutter run -d windows`.
:::
::: macOS
1. Run `flutter config --enable-macos-desktop`.
2. Go to the `macos` directory and run `pod install`.
3. Run `flutter run -d macos`.
:::
</dx-tabs>

## FAQs
### How do I view TRTC logs?
TRTC logs are compressed and encrypted by default with the `.xlog` extension. You can view them via the following paths:
- **iOS**: `Documents/log` of the application sandbox
- **Android**:
	- 6.7 and earlier: `/sdcard/log/tencent/liteav`
	- 6.8 and later: `/sdcard/Android/data/package name/files/log/tencent/liteav/`

### What should I do if videos show on Android but not on iOS?
Make sure that in `info.plist` of your project, the value of `io.flutter.embedded_views_preview` is `YES`. 

### What should I do if the "Manifest merge failed" error occurs in Android Studio?
Open `/example/android/app/src/main/AndroidManifest.xml`.
    
1. Add `xmlns:tools="http://schemas.android.com/tools"` to `manifest`.
2. Add `tools:replace="android:label"` to `application`.
![Illustration](https://main.qcloudimg.com/raw/7a37917112831488423c1744f370c883.png)

>? For more FAQs, see [Flutter](https://intl.cloud.tencent.com/document/product/647/39242).

