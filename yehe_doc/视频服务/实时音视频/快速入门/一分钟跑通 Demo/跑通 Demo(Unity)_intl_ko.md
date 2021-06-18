이 예시 항목은 Unity에 TRTC SDK를 빠르게 통합하여 게임에서 멀티미디어 통화를 구현하는 방법을 소개합니다.

이 예시 항목에는 다음과 같은 기능이 포함됩니다.
- 통화 참여와 통화 종료
- 사용자 정의 비디오 렌더링
- 디바이스 관리, 음악 효과, 음성 효과

>?
>
>- 구체적인 API 기능 매개변수에 대한 설명은 [Unity API 개요](https://cloud.tencent.com/document/product/647/55158)를 참조하십시오.
## 실행 환경 요건
- Unity 권장 버전: 2020.2.1f1c1
- 현재 Android, iOS, Windows, Mac(Mac은 내부 테스트 중) 플랫폼을 지원합니다.
- `Android Build Support`, `iOS Build Support`, `Winodows Build Support`, `MacOs Build Support` 모듈을 포함해야 합니다.
- iOS 개발에 필요한 환경 요건:
  - Xcode 11.0 이상 버전
  - 프로젝트에 유효한 개발자 서명이 설정되어 있는지 확인하십시오.

## 예시 프로그램 실행
[](id:step1)
### 1단계: 새로운 애플리케이션 생성
1. TRTC 콘솔에 로그인한 후, [개발 지원]>[Demo 빠른 실행](https://console.cloud.tencent.com/trtc/quickstart)을 선택합니다.
2. [시작하기]를 클릭하고 애플리케이션 명칭(예: `TestTRTC`)을 입력한 후 [애플리케이션 생성]을 클릭합니다.
![](https://main.qcloudimg.com/raw/9b2db43594f4744b42ef74c94494ea8e.png)

[](id:step2)
### 2단계: SDK와 소스 코드 다운로드
1. 실제 비즈니스 요구사항에 따라 SDK 및 관련 [Demo 소스 코드](https://tccweb-1258344699.cos.ap-nanjing.myqcloud.com/sdk/trtc/unity/TRTCUnitySDK.zip)를 다운로드합니다.
2. 다운로드 완료 후 [다운로드 완료, 다음 단계]를 클릭합니다. 이 프로젝트를 직접 Unity로 열 수 있습니다. SDK 파일을 직접 사용하려면 SDK 패키지에 있는 `TRTCUnitySDK/Assets/TRTCSDK/SDK` 폴더를 프로젝트의 Assets 디렉터리에 복사합니다.
<img src="https://imgcache.qq.com/operation/dianshi/other/unit_down.d5a5ae704fa1a0eec3c01d78fef924dd9e017014.png"/>
3. `Assets/TRTCSDK/Demo/Tools/GenerateTestUserSig.cs` 파일을 찾아 엽니다.
4. `GenerateTestUserSig.cs` 파일에서 관련 매개변수를 설정합니다.
  <ul><li>SDKAPPID: 0으로 기본 설정되어 있습니다. 실제 SDKAppID로 설정하십시오.</li>
  <li>SECRETKEY: 공백으로 기본 설정되어 있습니다. 실제 키 정보로 설정하십시오.</li></ul> 
	<img src="https://imgcache.qq.com/operation/dianshi/other/unity_config.ef41868fb36e8fc3a56652baf46c1f110c9f4a39.png"/>

[](id:step3)
### 3단계: 컴파일 실행
<dx-tabs>
::: Android\s 플랫폼
1. Unity Editor를 설정하고 [File]>[Build Setting]을 클릭하여 Android로 전환합니다.
![](https://imgcache.qq.com/operation/dianshi/other/unnity_android.c411b5d2254a2567d5c00f09845c60b9c3ea43a0.png)
2. Android 기기를 연결하고 [Build And Run]을 클릭하면 Demo가 실행됩니다.
3. 인터페이스 테스트는 enterRoom 호출을 클릭한 후 기타 관련 사항들을 자체 테스트합니다. 데이터 디스플레이 창은 호출이 성공했음을 표시하고 다른 창은 콜백 정보를 표시합니다.
:::
::: iOS\s 플랫폼
1. Unity Editor를 설정하고 [File]>[Build Setting]을 클릭하여 iOS로 전환합니다.
![](https://tccweb-1258344699.cos.ap-nanjing.myqcloud.com/sdk/trtc/unity/ios.png)
2. iPhone 기기를 연결하고 [Build And Run]을 클릭하면 새로운 디렉터리에 저장할 컴파일된 iOS 프로젝트를 선택해야 합니다. 컴파일이 완료되면 새 창에 Xcode 프로젝트가 팝업됩니다.
:::
::: Windows\s 플랫폼
1. Unity Editor를 설정하고 [File]>[Build Setting]을 클릭하면 `PC, Mac & Linux Standalone`, Target Platform으로 전환되어 Windows를 선택합니다.
![](https://main.qcloudimg.com/raw/580764f661c06cf71c4952727c409c5e.png)
2. [Build And Run]을 클릭하면 Demo가 실행됩니다.
:::
::: macOS\s 플랫폼
1. Unity Editor를 설정하고 [File]>[Build Setting]을 클릭하면 `PC, Mac & Linux Standalone`, Target Platform으로 전환되어 macOS를 선택합니다.
![](https://imgcache.qq.com/operation/dianshi/other/macos.f2d60a6ef431222eb4944e95347584a1df2356ea.png)
2. [Build And Run]을 클릭하면 Demo가 실행됩니다.
3. Unity Editor로 시뮬레이터를 실행하려면 `Device Simulator Package`를 설치해야 합니다.
4. [Window]>[General]>[Device Simulator]를 클릭합니다.
![](https://imgcache.qq.com/operation/dianshi/other/sim.8678bc4b6cc328392fa9014105ad58a155b389da.png)
:::
</dx-tabs>


[](id:demo)
## Demo 예시
Demo에는 테스트 및 호출에 참고할 수 있는 온라인 API가 대다수 포함되어 있습니다. API 문서 [SDK API(Unity)](https://cloud.tencent.com/document/product/647/55158)를 참조하십시오.
>? UI에 일부 조정 업데이트가 있을 수 있으니 최신 버전을 기준으로 하십시오.

![](https://imgcache.qq.com/operation/dianshi/other/unity_video.bd36c8bedacb14d718dec8779a8c9c2e6ef4a876.png)
## 디렉터리 구조
```
├─Assets
├── Editor                        // Unity 에디터 스크립트
│   ├── BuildScript.cs            // Unity 에디터 build 메뉴
│   ├── IosPostProcess.cs         // Unity 에디터로 ios 애플리케이션 스크립트 구축
├── Plugins
│   ├── Android                   
│   │   ├── AndroidManifest.xml   //Android 애플리케이션 구성 파일
├── StreamingAssets               // Unity Demo 멀티미디어 스트림 파일
├── TRTCSDK
    ├── Demo                      // Unity 예시 Demo
    ├── SDK                       // TRTC Unity SDK
        ├── Implement             // TRTC Unity SDK 구현
        ├── Include               // TRTC Unity SDK 헤더 파일
        └── Plugins               // TRTC Unity SDK 다양한 플랫폼 기반 구현
            
```
