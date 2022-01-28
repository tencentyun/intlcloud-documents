ここでは、主にTencent Cloud TRTC SDK(Unreal Engine)をプロジェクトに素早く統合する方法をご紹介します。以下の手順に従って設定すれば、SDKの統合作業を完了できます。

## 環境要件
- Unreal Engine 4.27.1およびそれ以降のバージョンを推奨します。
- **Android端末向け開発：**
  - Android Studio 4.0およびそれ以降のバージョン。
  - Visual Studio 2017 15.6以上のバージョン。
  - 実機デバッグのみサポートしています
**iOS & macOS端末向け開発：**
  - Xcode 11.0およびそれ以降のバージョン。
  - osxシステムには10.11およびそれ以降のバージョンが必要です。
  - プロジェクトが有効な開発者による署名を設定済みであることを確認してください。
- **Windows 端末向け開発：**
    - OS:Windows 7 SP1およびそれ以降のバージョン(x86-64に基づく64ビットOS）。
    - ディスク容量：IDEと一部のツールのインストールに必要な容量を除く、少なくとも1.64 GB以上の空き容量を確保するようにしてください。
    - [Visual Studio 2019](https://visualstudio.microsoft.com/zh-hans/downloads/)をインストールします。

## SDKの統合
1. SDKおよび付属する[SDKソースコード](https://comm.qq.com/sdk/trtc/UE4/TRTCSDK.zip)をダウンロードします（ご質問があればQQグループ番号：764231117に参加してお問い合わせください）。
2. 解凍後、プロジェクト内の`TRTCSDK`フォルダを自分のプロジェクトの**Source/[project_name]**ディレクトリ下にコピーします。この中の**[project_name]**にはプロジェクトの名称が入ります。
3. プロジェクトの**[project_name].Build.cs**ファイルを編集し、以下の関数を追加します
```
// 各プラットフォームのTRTC下層データベースをロード
private void loadTRTCSDK(ReadOnlyTargetRules Target)
{
    string _TRTCSDKPath = Path.GetFullPath(Path.Combine(ModuleDirectory, "TRTCSDK"));
    bEnableUndefinedIdentifierWarnings = false;
    if (Target.Platform == UnrealTargetPlatform.Android)
    {
        // Androidヘッダーファイルをロード
        PublicIncludePaths.Add(Path.Combine(_TRTCSDKPath, "include/Android"));
        PrivateDependencyModuleNames.AddRange(new string[] { "Launch" });
        // Android APLファイルをロード
        AdditionalPropertiesForReceipt.Add(new ReceiptProperty("AndroidPlugin", Path.Combine(ModuleDirectory, "TRTCSDK", "Android", "APL_armv7.xml")));
        
        string Architecture = "armeabi-v7a";
        // string Architecture = "arm64-v8a";
        // string Architecture = "armeabi";
        PublicAdditionalLibraries.Add(Path.Combine(ModuleDirectory,"TRTCSDK", "Android", Architecture, "libtraeimp-rtmp.so"));
        PublicAdditionalLibraries.Add(Path.Combine(ModuleDirectory,"TRTCSDK", "Android", Architecture, "libliteavsdk.so"));
    }else if (Target.Platform == UnrealTargetPlatform.IOS)
    {
        // iOSヘッダーファイルをロード
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
        // MacOsヘッダーファイルをロード
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
        // Win64ヘッダーファイルをロード
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
4. **[project_name].Build.cs**ファイルでこの関数を呼び出します
![](https://qcloudimg.tencent-cloud.cn/raw/a9b135ffd9e41d9d87fab383ac2d472a.png)
5. これでTRTC SDKの統合は完了し、cppファイルでTRTCを使用できるようになりました。`#include "ITRTCCloud.h"`
```
// TRTCシングルトンオブジェクトを取得
#if PLATFORM_ANDROID
    if (JNIEnv* Env = FAndroidApplication::GetJavaEnv()) {
        void* activity = (void*) FAndroidApplication::GetGameActivityThis();
        // Androidの場合はここで現在のコンテキストオブジェクトを渡す必要があります
        pTRTCCloud = getTRTCShareInstance(activity);
    }
#else
    pTRTCCloud = getTRTCShareInstance();
#endif
// イベントコールバックを登録
pTRTCCloud->addCallback(this);
// バージョン番号を取得
std::string version = pTRTCCloud->getSDKVersion();
// 入室
trtc::TRTCParams params;
params.userId = "123";
params.roomId = 110;
params.sdkAppId = SDKAppID;
params.userSig = GenerateTestUserSig().genTestUserSig(params.userId, SDKAppID, SECRETKEY);
pTRTCCloud->enterRoom(params, trtc::TRTCAppSceneVideoCall);
```
## パッケージ化
<dx-tabs>
::: macOS\s端末
1. File -> Package Project -> Mac
2. 権限を設定します。前の手順でコンパイルしたxxx.appファイルを右クリックし、「パッケージの内容を表示」を選択します 
![](https://qcloudimg.tencent-cloud.cn/raw/3eb106ee3307c206dff5314a43920132.png)
3. 「Contents->Info.plist」に進みます
4. 「Information Property List」を選択し、次の2つの権限を追加します。
```
<key>NSCameraUsageDescription</key>
<string>通常のビデオ通話が行えるようにカメラを許可します</string>
<key>NSMicrophoneUsageDescription</key>
<string>通常の音声通話が行えるようにマイクの権限を承認します</string>
```
5. UE4のeditorで実行中の場合は、**UE4Editor.app**ファイルを見つけて、上記の手順に従って権限を追加する必要があります。
:::
::: Windows\s端末
1. File->Package Project->Windows->Windows(64-bit)
![](https://imgcache.qq.com/operation/dianshi/other/win.ba79ccce59ae58718e6c35c16cdef55531456a70.png)
:::
::: iOS\s端末
1. iOS上でも次の権限が必要です。
```
Privacy - Camera Usage Description
Privacy - Microphone Usage Description
```
上記の権限をinfo.plistに追加するために、**Edit->Project Settings->Platforms: iOS**で 
```
<key>NSCameraUsageDescription</key>
<string>通常のビデオ通話が行えるようにカメラを許可します</string>
<key>NSMicrophoneUsageDescription</key>
<string>通常の音声通話が行えるようにマイクの権限を承認します</string>
```
上記をAdditional Plist Dataに追加することができます。
2. 最後にプロジェクトをパッケージ化します。File -> Package Project -> iOS
:::
:::  Android\s端末
1. 開発とデバッグ：[Androidクイックスタート](https://docs.unrealengine.com/4.27/zh-CN/SharingAndReleasing/Mobile/Android/GettingStarted/)をご参照ください
2. プロジェクトのパッケージ化：[Androidプロジェクトのパッケージ化](https://docs.unrealengine.com/4.27/zh-CN/SharingAndReleasing/Mobile/Android/PackagingAndroidProject/)をご参照ください
:::
</dx-tabs>

## TRTC全プラットフォーム C++ APIドキュメント
[中国語ドキュメント](https://liteav.sdk.qcloud.com/doc/api/zh-cn/md_introduction_trtc_zh_Cplusplus_Brief.html)

[英語ドキュメント](https://liteav.sdk.qcloud.com/doc/api/en/md_introduction_trtc_en_Cplusplus_Brief.html)
