This document describes how to quickly integrate the Tencent Cloud IM SDK (Flutter) to your projects.

## Environment Requirements

| Platform | Version | 
|---------|---------|
| Flutter | 2.2.0 or later| 
| Android | Android Studio 3.5 or later; devices with Android 4.1 or later for apps |
| iOS | Xcode 11.0 or later. For testing with a real device, ensure that your project has a valid developer signature. |


## Integrating the IM SDK
You can directly integrate the IM SDK for Flutter through [pub add](https://pub.dev/packages/tencent_im_sdk_plugin), or write the IM SDK into `pubspec.yaml`.


### Installing the IM SDK via `flutter pub add`
Enter the following command in the terminal window (the Flutter environment is ready):
```
flutter pub add tencent_im_sdk_plugin
```

### Writing the IM SDK into `pubspec.yaml`
```
dependencies:
  tencent_im_sdk_plugin: ^3.8.2
```
Here, your editor may automatically run `flutter pub get`. If not, enter the command `flutter pub get`.


### Importing and initializing the SDK
```
import 'package:tencent_im_sdk_plugin/tencent_im_sdk_plugin.dart';

```


## FAQs

### What should I do if `flutter pub get/add` fails?
Configure Flutter to use a mirror site as instructed in [Flutter](https://flutter.cn/community/china).


