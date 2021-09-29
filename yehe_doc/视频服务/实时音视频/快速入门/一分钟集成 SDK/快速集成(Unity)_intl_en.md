This document describes how to quickly integrate TRTC SDK for Unity into your project.

## Environment Requirements
* Unity 2020.2.1f1c1 is recommended.
* Supported platforms: Android, iOS, Windows, macOS (alpha testing)
* Modules required: `Android Build Support`, `iOS Build Support`, `Windows Build Support`, `MacOS Build Support`
- If you are developing for iOS, you also need:
  - Xcode 11.0 or above
  - A valid developer signature for your project

## Integrating SDK
1. Download the SDK and [demo source code](https://github.com/tencentyun/TRTCUnitySDK).
2. Decompress the ZIP file and copy `TRTCUnitySDK/Assets/TRTCSDK/SDK` to the `Assets` directory of your project.

## FAQs
### What should I do if a network access error occurs on Android?
Copy `/Assets/Plugins/AndroidManifest.xml` to the same directory of your project.

### What should I do if the SDK does not have mic or camera access on Android?
You need to add mic and camera permission requests manually when building for Android. For details, see the code below:
```
#if PLATFORM_ANDROID
if (!Permission.HasUserAuthorizedPermission(Permission.Microphone))
 {
     Permission.RequestUserPermission(Permission.Microphone);
 }
 if (!Permission.HasUserAuthorizedPermission(Permission.Camera))
 {
     Permission.RequestUserPermission(Permission.Camera);
 }
 #endif
```  
