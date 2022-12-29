## Environment Requirements

- Flutter 2.0 or later
- Developing for Android:
  - Android Studio 3.5 or later
  - Devices with Android 4.1 or later
- Developing for iOS:
  - Xcode 11.0 or later
  - OS X 10.11 or later.
  - A valid developer signature for your project

## SDK Download

You can download the Player SDK for Flutter [here](https://github.com/LiteAVSDK/Player_Flutter).

## Quick Integration

### Adding the following dependencies to the `pubspec.yaml` of your project

You can integrate `LiteAVSDK_Player` or `LiteAVSDK_Professional` as needed.

1. Integrate the latest version of `LiteAVSDK_Player` (which is integrated by default) and add the following configuration to `pubspec.yaml`:
```yaml
super_player:
  git:
    url: https://github.com/LiteAVSDK/Player_Flutter
    path: Flutter
```
To integrate the latest version of `LiteAVSDK_Professional`, change the configuration in `pubspec.yaml` as follows:
```yaml
super_player:
  git:
    url: https://github.com/LiteAVSDK/Player_Flutter
    path: Flutter
    ref: Professional
```
To integrate a specified version of the player SDK, specify the corresponding version through the `tag` that `ref` depends on as follows:
```yaml
super_player:
  git:
    url: https://github.com/LiteAVSDK/Player_Flutter
    path: Flutter
    ref: release_player_v1.0.6 

# `release_player_v1.0.6` indicates to integrate TXLiteAVSDK_Player_10.6.0.11182 for Android or TXLiteAVSDK_Player_10.6.11821 for iOS.
```

For more archived tags, see [Release List](https://github.com/LiteAVSDK/Player_Flutter/releases).

2. After the integration, you can obtain the Flutter dependencies through the UI that comes with the code editor or by directly running the following command:

```yaml
flutter packages get
```

3. During use, you can run the following command to update existing Flutter dependencies:

```dart
flutter pub upgrade
```

### Adding native configuration

#### Android configuration
1. Add the following configuration to `AndroidManifest.xml`.
```xml
<!--network permission-->
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
<!--storage-->
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
```

2. Make sure that the `build.gradle` in the Android directory uses `mavenCenter` and can successfully download dependencies.
```groovy
repositories {
  mavenCentral()
}
```

3. To update the dependency version of the native SDK, manually delete the `build` folder in the Android directory or run the following command to force a refresh.
```shell
./gradlew build
```

4. To use the picture-in-picture feature of Android, integrate `FTXFlutterPipActivity.java` in the `android` directory in the `example` component.


#### iOS configuration

Note: **iOS currently does not support project running and debugging in simulators; therefore, we recommend you develop and debug your project on a real device**.

1. Add the following configuration to the `Info.plist` file of iOS:
```xml
<key>NSAppTransportSecurity</key>
<dict>
    <key>NSAllowsArbitraryLoads</key>
    <true/>
</dict>
```
2. iOS natively uses `pod` for dependency. Edit the `podfile` file and specify your player SDK edition. `TXLiteAVSDK_Player` is integrated by default.
```xml
pod 'TXLiteAVSDK_Player'	        // Player Edition
```
 Integrate `LiteAVSDK_Professional`:
```
pod 'TXLiteAVSDK_Professional' 	// Professional Edition
```

If you do not specify the edition, the latest version of `TXLiteAVSDK_Player` will be installed.

3. In some cases such as new version release, you need to forcibly update the iOS player dependencies by running the following command in the iOS directory:
```shell
rm -rf Pods
rm -rf Podfile.lock
pod update
```

## Integrating the Video Playback License
If you have obtained a license, you can view the license URL and key in the [RT-Cube console](https://www.tencentcloud.com/account/login).

If you don't have the required license yet, you can get it as instructed in [Adding and Renewing a License](https://www.tencentcloud.com/document/product/266/51098).

Before you integrate the player, you need to [sign up for a Tencent Cloud account](https://www.tencentcloud.com/account/login), apply for the video playback license, and configure the license as follows (we recommend you do this when the application is launched):

If you don’t configure a license, errors may occur during playback.
```dart
String licenceURL = ""; // The license URL obtained
String licenceKey = ""; // The license key obtained
SuperPlayerPlugin.setGlobalLicense(licenceURL, licenceKey);
```

## Custom Development

The Flutter plugin of the Player SDK is based on the system’s native player capabilities. You can use either of the following methods for custom development:

- Use the VOD playback API class `TXVodPlayerController` or live playback API class `TXLivePlayerController` for custom development. You can refer to the demos we provide (`DemoTXVodPlayer` and `DemoTXLivePlayer` in `example`).

- The player component `SuperPlayerController` encapsulates VOD playback and live playback capabilities and includes basic UI elements.

  You can copy the code of the player component (in `example/lib/superplayer`) to your project for custom development.

## FAQs

1. Errors about missing APIs such as `No visible @interface for 'TXLivePlayer' declares the selector 'startLivePlay:type:'` occur on iOS.
Run the following command to update the iOS SDK:
```shell
rm -rf Pods
rm -rf Podfile.lock
pod update
```

2. SDK or symbol conflicts occur when `tencent_trtc_cloud` and Flutter player are integrated at the same time.

   Common exception log: `java. lang.RuntimeException: Duplicate class com.tencent.liteav.TXLiteAVCode found in modules classes.jar`

   In this case, you need to integrate the Professional version of the Flutter player, so that `tencent_trtc_cloud` and the Flutter player both depend on the same version of `LiteAVSDK_Professional`.

   For example, to depend on `TXLiteAVSDK_Professional_10.3.0.11196` for Android or `TXLiteAVSDK_Professional to 10.3.12231` for iOS, the dependency declaration is as follows:
   ```xml
   tencent_trtc_cloud: 2.3.8
   
   super_player:
     git:
       url: https://github.com/LiteAVSDK/Player_Flutter
       path: Flutter
       ref: release_pro_v1.0.3.11196_12231
   ```
3. When multiple player instances need to be used at the same time, the video image gets blurry when videos are frequently switched.
	When each player component container is terminated, call the `dispose` method of the player to release the player.
4. Other common issues with Flutter dependencies:
 - Run the `flutter doctor` command to check the runtime environment until "No issues found!" is displayed.
 - Run `flutter pub get` to ensure that all dependent components have been updated successfully.

## More

You can try out all the features by running the example in the project.

The player SDK website provides demos for iOS, Android, and web. Click [here](https://www.tencentcloud.com/document/product/266/42091) to use them.

