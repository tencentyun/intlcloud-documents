This document describes how to quickly integrate the TRTC SDK for Unreal Engine into your project.

## Environment Requirements
- Unreal Engine 4.27.1 or above
- **Developing for Android:**
  - Android Studio 4.0 or above
  - Visual Studio 2017 15.6 or above
  - A real device for testing
- **Developing for iOS and macOS:**
  - Xcode 11.0 or above
  - OS X 10.11 or above
  - A valid developer signature for your project
- **Developing for Windows:**
    - OS: Windows 7 SP1 or above (64-bit based on x86-64)
    - Disk space: at least 1.64 GB of space after the IDE and relevant tools are installed
    - [Visual Studio 2019](https://visualstudio.microsoft.com/zh-hans/downloads/)

## Integrating the SDK
1. Download the SDK and its [source code](https://github.com/tencentyun/TRTCUnrealEngine). If you have any questions, create an issue [here](https://github.com/tencentyun/TRTCUnrealEngine/issues).
2. Copy the `TRTCSDK` folder to the **Source/[project_name]** directory of your project (**[project_name]** is the name of your project).
3. Add the following function to the **[project_name].Build.cs** file in your project.
```
// Load the TRTC library for different platforms
private void loadTRTCSDK(ReadOnlyTargetRules Target)
{
    string _TRTCSDKPath = Path.GetFullPath(Path.Combine(ModuleDirectory, "TRTCSDK"));
    bEnableUndefinedIdentifierWarnings = false;
    if (Target.Platform == UnrealTargetPlatform.Android)
    {
        // Load the Android header file
        PublicIncludePaths.Add(Path.Combine(_TRTCSDKPath, "include/Android"));
        PrivateDependencyModuleNames.AddRange(new string[] { "Launch" });
        // Load the Android APL file
        AdditionalPropertiesForReceipt.Add(new ReceiptProperty("AndroidPlugin", Path.Combine(ModuleDirectory, "TRTCSDK", "Android", "APL_armv7.xml")));
        
        string Architecture = "armeabi-v7a";
        // string Architecture = "arm64-v8a";
        // string Architecture = "armeabi";
        PublicAdditionalLibraries.Add(Path.Combine(ModuleDirectory,"TRTCSDK", "Android", Architecture, "libtraeimp-rtmp.so"));
        PublicAdditionalLibraries.Add(Path.Combine(ModuleDirectory,"TRTCSDK", "Android", Architecture, "libliteavsdk.so"));
    }else if (Target.Platform == UnrealTargetPlatform.IOS)
    {
        // Load the iOS header file
        PublicIncludePaths.Add(Path.Combine(_TRTCSDKPath, "include/iOS"));
        PublicAdditionalLibraries.AddRange(new string[] {
            "resolv",
            "z",
            "c++",
        });
        PublicFrameworks.AddRange(
            new string[] {
                "CoreML",
                "VideoToolbox",
                "Accelerate",
                "CFNetwork",
                "OpenGLES",
                "AVFoundation",
                "CoreTelephony"
            }
        );
        PublicAdditionalFrameworks.Add(new UEBuildFramework( "TXLiteAVSDK_TRTC",_TRTCSDKPath+"/ios/TXLiteAVSDK_TRTC.framework.zip", ""));
    }else if(Target.Platform == UnrealTargetPlatform.Mac)
    {
        // Load the macOS header file
        PublicIncludePaths.Add(Path.Combine(_TRTCSDKPath, "include/Mac"));
        PublicAdditionalLibraries.AddRange(new string[] {
            "resolv",
            "z",
            "c++",
            "bz2",
        });
        PublicFrameworks.AddRange(
            new string[] {
                "AppKit",
                "IOKit",
                "CoreVideo",
                "CFNetwork",
                "OpenGl",
                "CoreGraphics",
                "Accelerate",
                "CoreFoundation",
                "SystemConfiguration",
                "AudioToolbox",
                "VideoToolbox",
                "CoreTelephony",
                "CoreWLAN",
                "AVFoundation",
                "CoreMedia",
                "CoreAudio",
                "AudioUnit",
                "Accelerate",
            });
        PublicFrameworks.Add(Path.Combine(_TRTCSDKPath, "Mac", "Release","TXLiteAVSDK_TRTC_Mac.framework"));
    }else if (Target.Platform == UnrealTargetPlatform.Win64)
    {
        // Load the 64-bit Windows header file
        PublicIncludePaths.Add(Path.Combine(_TRTCSDKPath, "include/win64"));
        PublicAdditionalLibraries.Add(Path.Combine(_TRTCSDKPath, "win64", "Release","liteav.lib"));
        PublicDelayLoadDLLs.Add(Path.Combine(_TRTCSDKPath, "win64", "Release", "liteav.dll"));
        PublicDelayLoadDLLs.Add(Path.Combine(_TRTCSDKPath, "win64", "Release", "LiteAvAudioHook.dll"));
        PublicDelayLoadDLLs.Add(Path.Combine(_TRTCSDKPath, "win64", "Release", "LiteAvAudioHookService.dll"));
        PublicDelayLoadDLLs.Add(Path.Combine(_TRTCSDKPath, "win64", "Release", "openh264.dll"));
        PublicDelayLoadDLLs.Add(Path.Combine(_TRTCSDKPath, "win64", "Release", "TRAE.dll"));

        RuntimeDependencies.Add("$(BinaryOutputDir)/liteav.dll", Path.Combine(_TRTCSDKPath, "win64", "Release", "liteav.dll"));
        RuntimeDependencies.Add("$(BinaryOutputDir)/LiteAvAudioHook.dll", Path.Combine(_TRTCSDKPath, "win64", "Release", "LiteAvAudioHook.dll"));
        RuntimeDependencies.Add("$(BinaryOutputDir)/LiteAvAudioHookService.dll", Path.Combine(_TRTCSDKPath, "win64", "Release", "LiteAvAudioHookService.dll"));
        RuntimeDependencies.Add("$(BinaryOutputDir)/openh264.dll", Path.Combine(_TRTCSDKPath, "win64", "Release", "openh264.dll"));
        RuntimeDependencies.Add("$(BinaryOutputDir)/TRAE.dll", Path.Combine(_TRTCSDKPath, "win64", "Release", "TRAE.dll"));
    }
}
```
4. Call the function in the **[project_name].Build.cs** file.
![](https://qcloudimg.tencent-cloud.cn/raw/a9b135ffd9e41d9d87fab383ac2d472a.png)
5. You have integrated the TRTC SDK into your project and can now use it in the CPP file.`#include "ITRTCCloud.h"`
```
// Get a TRTC singleton
#if PLATFORM_ANDROID
    if (JNIEnv* Env = FAndroidApplication::GetJavaEnv()) {
        void* activity = (void*) FAndroidApplication::GetGameActivityThis();
        // For Android, pass in the context object
        pTRTCCloud = getTRTCShareInstance(activity);
    }
#else
    pTRTCCloud = getTRTCShareInstance();
#endif
// Register event callbacks
pTRTCCloud->addCallback(this);
// Get the version number
std::string version = pTRTCCloud->getSDKVersion();
// Enter a room
trtc::TRTCParams params;
params.userId = "123";
params.roomId = 110;
params.sdkAppId = SDKAppID;
params.userSig = GenerateTestUserSig().genTestUserSig(params.userId, SDKAppID, SECRETKEY);
pTRTCCloud->enterRoom(params, trtc::TRTCAppSceneVideoCall);
```
## Packaging
<dx-tabs>
::: macOS\s
1. Go to **File > Package Project > Mac**.
2. Configure permissions. Right-click the `xxx.app` file compiled in the previous step and select **Show Package Contents**. 
![](https://qcloudimg.tencent-cloud.cn/raw/3eb106ee3307c206dff5314a43920132.png)
3. Go to **Contents > Info.plist**.
4. Select **Information Property List** and add the following two permissions:
```
<key>NSCameraUsageDescription</key>
<string>Video calls are possible only with camera permission.</string>
<key>NSMicrophoneUsageDescription</key>
<string>Audio calls are possible only with mic access.</string>
```
5. If you use UE4 Editor, add the above permissions to the **UE4Editor.app** file.
:::
::: Windows\s
1. Go to **File > Package Project > Windows > Windows(64-bit)**.
![](https://imgcache.qq.com/operation/dianshi/other/win.ba79ccce59ae58718e6c35c16cdef55531456a70.png)
:::
::: iOS\s
1. The following permissions are required on iOS.
```
Privacy - Camera Usage Description
Privacy - Microphone Usage Description
```
To add the permissions to `info.plist`, go to **Edit > Project Settings > Platforms: iOS** and add  
```
<key>NSCameraUsageDescription</key>
<string>Video calls are possible only with camera permission.</string>
<key>NSMicrophoneUsageDescription</key>
<string>Audio calls are possible only with mic access.</string>
```
to `Additional Plist Data`.
2. Go to **File > Package Project > iOS** to package your project.
:::
:::  Android\s
1. For development and testing, see [Android Quick Start](https://docs.unrealengine.com/4.27/en-US/SharingAndReleasing/Mobile/Android/GettingStarted/).
2. For packaging, see [Packaging Android Projects](https://docs.unrealengine.com/4.27/en-US/SharingAndReleasing/Mobile/Android/PackagingAndroidProject/).
:::
</dx-tabs>

## TRTC Cross-Platform (C++) APIs
[API Documentation (Chinese)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/md_introduction_trtc_zh_Cplusplus_Brief.html)

[API Documentation (English)](https://liteav.sdk.qcloud.com/doc/api/en/md_introduction_trtc_en_Cplusplus_Brief.html)
