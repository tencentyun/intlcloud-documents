본문은 Tencent Cloud TRTC SDK(Unreal Engine)를 프로젝트에 빠르게 통합하는 방법을 소개합니다. 아래의 단계에 따라 설정하면 SDK 통합 작업을 완료할 수 있습니다.

## 환경 요건
- Unreal Engine 4.27.1 이상 버전 권장.
- **Android 개발:**
  - Android Studio 4.0 이상 버전.
  - Visual Studio 2017 15.6 이상 버전.
  - 실제 기기 디버깅만 지원
- **iOS & macOS 개발:**
  - Xcode 11.0 이상 버전.
  - osx 시스템 10.11 이상 버전
  - 귀하의 프로젝트에 유효한 개발자 서명이 설정되어 있는지 확인하십시오.
- **Windows 개발:**
    - 운영 체제: Windows 7 SP1 이상(x86-64 기반 64비트 운영 체제).
    - 디스크 공간: IDE 및 일부 툴 설치 외에 최소 1.64GB의 공간 필요.
    - [Visual Studio 2019](https://visualstudio.microsoft.com/zh-hans/downloads/) 설치.

## SDK 통합
1. SDK 및 관련 [SDK 소스 코드](https://comm.qq.com/sdk/trtc/UE4/TRTCSDK.zip)를 다운로드합니다(문의 사항은 QQ 그룹 번호: 764231117 추가 후 상담).
2. 압축 해제 후 프로젝트의 'TRTCSDK' 폴더를 프로젝트의 **Source/[project_name]** 디렉터리에 복사합니다. 여기서 **[project_name]**은 프로젝트 이름입니다.
3. 프로젝트에서 **[project_name].Build.cs** 파일을 편집합니다. 다음 함수를 추가합니다.
```
// 각 플랫폼의 TRTC 기본 라이브러리 로딩
private void loadTRTCSDK(ReadOnlyTargetRules Target)
{
    string _TRTCSDKPath = Path.GetFullPath(Path.Combine(ModuleDirectory, "TRTCSDK"));
    bEnableUndefinedIdentifierWarnings = false;
    if (Target.Platform == UnrealTargetPlatform.Android)
    {
        // Android 헤더 파일 로딩
        PublicIncludePaths.Add(Path.Combine(_TRTCSDKPath, "include/Android"));
        PrivateDependencyModuleNames.AddRange(new string[] { "Launch" });
        // Android APL 파일 로딩
        AdditionalPropertiesForReceipt.Add(new ReceiptProperty("AndroidPlugin", Path.Combine(ModuleDirectory, "TRTCSDK", "Android", "APL_armv7.xml")));
        
        string Architecture = "armeabi-v7a";
        // string Architecture = "arm64-v8a";
        // string Architecture = "armeabi";
        PublicAdditionalLibraries.Add(Path.Combine(ModuleDirectory,"TRTCSDK", "Android", Architecture, "libtraeimp-rtmp.so"));
        PublicAdditionalLibraries.Add(Path.Combine(ModuleDirectory,"TRTCSDK", "Android", Architecture, "libliteavsdk.so"));
    }else if (Target.Platform == UnrealTargetPlatform.IOS)
    {
        // iOS 헤더 파일 로딩
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
        // MacOs 헤더 파일 로딩
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
        // Win64 헤더 파일 로딩
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
4. **[project_name].Build.cs** 파일에서 이 함수 호출
![](https://qcloudimg.tencent-cloud.cn/raw/a9b135ffd9e41d9d87fab383ac2d472a.png)
5. 현재 TRTC SDK가 통합되었으므로 cpp 파일에서 TRTC를 사용할 수 있습니다. `#include "ITRTCCloud.h"`
```
// TRTC 싱글톤 객체 가져오기
#if PLATFORM_ANDROID
    if (JNIEnv* Env = FAndroidApplication::GetJavaEnv()) {
        void* activity = (void*) FAndroidApplication::GetGameActivityThis();
        // 여기에서 Android는 현재 컨텍스트 객체를 전달해야 합니다.
        pTRTCCloud = getTRTCShareInstance(activity);
    }
#else
    pTRTCCloud = getTRTCShareInstance();
#endif
// 이벤트 콜백 가입
pTRTCCloud->addCallback(this);
// 버전 넘버 가져오기
std::string version = pTRTCCloud->getSDKVersion();
// 방 입장
trtc::TRTCParams params;
params.userId = "123";
params.roomId = 110;
params.sdkAppId = SDKAppID;
params.userSig = GenerateTestUserSig().genTestUserSig(params.userId, SDKAppID, SECRETKEY);
pTRTCCloud->enterRoom(params, trtc::TRTCAppSceneVideoCall);
```
## 패키징
<dx-tabs>
::: macOS\s
1. File -> Package Project -> Mac
2. 권한을 설정합니다. 이전 단계에서 컴파일된 xxx.app 파일을 마우스 오른쪽 버튼으로 클릭하고 - ‘패키지 콘텐츠 표시’를 선택합니다. 
![](https://qcloudimg.tencent-cloud.cn/raw/3eb106ee3307c206dff5314a43920132.png)
3. ‘Contents->Info.plist"’로 이동
4. ‘Information Property List’을 선택하고 다음 두 가지 권한을 추가합니다.
```
<key>NSCameraUsageDescription</key>
<string>카메라 권한을 부여해야 정상적으로 영상 통화할 수 있습니다.</string>
<key>NSMicrophoneUsageDescription</key>
<string>마이크 권한을 부여해야 정상적으로 음성 통화할 수 있습니다.</string>
```
5. 현재 UE4 editor에서 실행 중인 경우 **UE4Editor.app** 파일을 찾아 상기 단계에 따라 권한을 추가해야 합니다.
:::
::: Windows\s
1. File->Package Project->Windows->Windows(64-bit)
![](https://imgcache.qq.com/operation/dianshi/other/win.ba79ccce59ae58718e6c35c16cdef55531456a70.png)
:::
::: iOS\s
1. iOS에서도 다음 권한이 필요합니다.
```
Privacy - Camera Usage Description
Privacy - Microphone Usage Description
```
info.plist에 위의 권한을 추가하려면 **Edit->Project Settings->Platforms: iOS**로 이동하여  
```
<key>NSCameraUsageDescription</key>
<string>카메라 권한을 부여해야 정상적으로 영상 통화할 수 있습니다.</string>
<key>NSMicrophoneUsageDescription</key>
<string>마이크 권한을 부여해야 정상적으로 음성 통화할 수 있습니다.</string>
```
Additional Plist Data에 추가합니다.
2. 마지막으로 프로젝트를 패키징합니다. File -> Package Project -> iOS
:::
:::  Android\s
1. 개발 디버깅: 자세한 내용은 [Android 시작하기](https://docs.unrealengine.com/4.27/zh-CN/SharingAndReleasing/Mobile/Android/GettingStarted/) 참고
2. 패키징 프로젝트: 자세한 내용은 [Android 프로젝트 패키징](https://docs.unrealengine.com/4.27/zh-CN/SharingAndReleasing/Mobile/Android/PackagingAndroidProject/) 참고
:::
</dx-tabs>

## TRTC 전체 플랫폼 C++ API 문서
[중국어 문서](https://liteav.sdk.qcloud.com/doc/api/zh-cn/md_introduction_trtc_zh_Cplusplus_Brief.html)

[영어 문서](https://liteav.sdk.qcloud.com/doc/api/en/md_introduction_trtc_en_Cplusplus_Brief.html)
