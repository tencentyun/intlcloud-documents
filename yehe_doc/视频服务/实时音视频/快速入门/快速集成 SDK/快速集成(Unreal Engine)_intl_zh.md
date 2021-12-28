本文主要介绍如何快速地将腾讯云 TRTC SDK（Unreal Engine）集成到您的项目中，只要按照如下步骤进行配置，就可以完成 SDK 的集成工作。

## 环境要求
- 建议Unreal Engine 4.27.1 及以上版本。
- **Android 端开发：**
  - Android Studio版本4.0及以上版本。
  - Visual Studio 2017 15.6版或更高。
  - 只支持真机调试
- **iOS & macOS 端开发：**
  - Xcode 11.0及以上版本。
  - osx 系统版本要求 10.11 及以上版本
  - 请确保您的项目已设置有效的开发者签名。
- **Windows 开发：**
    - 操作系统：Windows 7 SP1 或更高的版本（基于 x86-64 的 64 位操作系统）。
    - 磁盘空间：除安装 IDE 和一些工具之外还应有至少 1.64 GB 的空间。
    - 安装 [Visual Studio 2019](https://visualstudio.microsoft.com/zh-hans/downloads/)。

## 集成 SDK
1. 下载 SDK 及配套的 [SDK 源码](https://comm.qq.com/sdk/trtc/UE4/TRTCSDK.zip)（有疑问可加入QQ群号：764231117 咨询）。
2. 解压后，把项目中的 `TRTCSDK` 文件夹拷贝到您项目中的 **Source/[project_name]** 目录下，其中 **[project_name]** 表示你项目的名称。
3. 编辑你项目中的 **[project_name].Build.cs**文件。添加下面函数
```
// 加载各个平台TRTC底层库
private void loadTRTCSDK(ReadOnlyTargetRules Target)
{
    string _TRTCSDKPath = Path.GetFullPath(Path.Combine(ModuleDirectory, "TRTCSDK"));
    bEnableUndefinedIdentifierWarnings = false;
    if (Target.Platform == UnrealTargetPlatform.Android)
    {
        // 加载Android头文件
        PublicIncludePaths.Add(Path.Combine(_TRTCSDKPath, "include/Android"));
        PrivateDependencyModuleNames.AddRange(new string[] { "Launch" });
        // 加载Android APL文件
        AdditionalPropertiesForReceipt.Add(new ReceiptProperty("AndroidPlugin", Path.Combine(ModuleDirectory, "TRTCSDK", "Android", "APL_armv7.xml")));
        
        string Architecture = "armeabi-v7a";
        // string Architecture = "arm64-v8a";
        // string Architecture = "armeabi";
        PublicAdditionalLibraries.Add(Path.Combine(ModuleDirectory,"TRTCSDK", "Android", Architecture, "libtraeimp-rtmp.so"));
        PublicAdditionalLibraries.Add(Path.Combine(ModuleDirectory,"TRTCSDK", "Android", Architecture, "libliteavsdk.so"));
    }else if (Target.Platform == UnrealTargetPlatform.IOS)
    {
        // 加载iOS头文件
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
        // 加载MacOs头文件
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
        // 加载Win64头文件
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
4. 在**[project_name].Build.cs**文件调用该函数
![](https://qcloudimg.tencent-cloud.cn/raw/a9b135ffd9e41d9d87fab383ac2d472a.png)
5. 到目前为止你已经集成了TRTC SDK。可在你的cpp 文件中使用TRTC了。`#include "ITRTCCloud.h"`
```
// 获取TRTC单例对象
#if PLATFORM_ANDROID
    if (JNIEnv* Env = FAndroidApplication::GetJavaEnv()) {
        void* activity = (void*) FAndroidApplication::GetGameActivityThis();
        // 安卓这里需要传入当前上下文对象
        pTRTCCloud = getTRTCShareInstance(activity);
    }
#else
    pTRTCCloud = getTRTCShareInstance();
#endif
// 注册事件回调
pTRTCCloud->addCallback(this);
// 获取版本号
std::string version = pTRTCCloud->getSDKVersion();
// 进入房间
trtc::TRTCParams params;
params.userId = "123";
params.roomId = 110;
params.sdkAppId = SDKAppID;
params.userSig = GenerateTestUserSig().genTestUserSig(params.userId, SDKAppID, SECRETKEY);
pTRTCCloud->enterRoom(params, trtc::TRTCAppSceneVideoCall);
```
## 打包
<dx-tabs>
::: macOS\s端
1. File -> Package Project -> Mac
2. 配置权限。右击上一步编译出的 xxx.app 文件 - 选择 "显示包内容" 
![](https://qcloudimg.tencent-cloud.cn/raw/3eb106ee3307c206dff5314a43920132.png)
3. 进入 "Contents->Info.plist"
4. 选择 "Information Property List" 然后添加以下两个权限:
```
<key>NSCameraUsageDescription</key>
<string>授权摄像头权限才能正常视频通话</string>
<key>NSMicrophoneUsageDescription</key>
<string>授权麦克风权限才能正常语音通话</string>
```
5. 如果你现在在UE4的editor运行的话，需要找到 **UE4Editor.app** 文件并且按照上面步骤添加权限。
:::
::: Windows\s端
1. File->Package Project->Windows->Windows(64-bit)
![](https://imgcache.qq.com/operation/dianshi/other/win.ba79ccce59ae58718e6c35c16cdef55531456a70.png)
:::
::: iOS\s端
1. 在 iOS 上也需要以下权限：
```
Privacy - Camera Usage Description
Privacy - Microphone Usage Description
```
为了将上述权限添加到 info.plist 里，你可以在 **Edit->Project Settings->Platforms: iOS** 中，将 
```
<key>NSCameraUsageDescription</key>
<string>授权摄像头权限才能正常视频通话</string>
<key>NSMicrophoneUsageDescription</key>
<string>授权麦克风权限才能正常语音通话</string>
```
添加到 Additional Plist Data 里。
2. 最后打包项目。File -> Package Project -> iOS
:::
::: Android\s端
1.开发调试：详见 [Android快速入门](https://docs.unrealengine.com/4.27/zh-CN/SharingAndReleasing/Mobile/Android/GettingStarted/)
2.打包项目：详见 [打包Android项目](https://docs.unrealengine.com/4.27/zh-CN/SharingAndReleasing/Mobile/Android/PackagingAndroidProject/)
:::
</dx-tabs>

## TRTC全平台 C++ API文档
[中文文档](https://liteav.sdk.qcloud.com/doc/api/zh-cn/md_introduction_trtc_zh_Cplusplus_Brief.html)

[英文文档](https://liteav.sdk.qcloud.com/doc/api/en/md_introduction_trtc_en_Cplusplus_Brief.html)
