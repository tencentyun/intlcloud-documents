이 예시 항목은 Unity에 TRTC SDK를 빠르게 통합하여 게임에서 멀티미디어 통화를 구현하는 방법을 소개합니다.

이 예시 항목에는 다음과 같은 기능이 포함됩니다.
- 통화 참여와 통화 종료
- 사용자 정의 비디오 렌더링
- 디바이스 관리, 음악 효과, 음성 효과

>?
>
>- 구체적인 API 기능 매개변수에 대한 설명은 [Unity API 개요](https://intl.cloud.tencent.com/zh/document/product/647/40139)를 참조하십시오.
- Unity 권장 버전: 2020.2.1f1c1
- 현재 Android, iOS, Windows, Mac(Mac은 알파 테스트 중) 플랫폼을 지원합니다.
- `Android Build Support`, `iOS Build Support`, `Winodows Build Support`, `MacOs Build Support` 모듈을 포함해야 합니다.
- iOS 개발에 필요한 환경 요건:
  - Xcode 11.0 이상 버전
  - 프로젝트에 유효한 개발자 서명이 설정되어 있는지 확인하십시오.

## 예시 프로그램 실행
[](id:step1)
### 1단계: 새로운 애플리케이션 생성
1. TRTC 콘솔에 로그인한 후 [개발 지원] > [Demo 빠른 실행](https://console.cloud.tencent.com/trtc/quickstart)을 선택합니다.
2. [시작하기]를 클릭하고 애플리케이션 이름(예시: `TestTRTC`)을 입력한 후 [애플리케이션 생성]을 클릭합니다.
![](https://main.qcloudimg.com/raw/7178fb5203b8c1ad9eb4a3b7a3c008d7.png)

[](id:step2)
### 2단계: SDK와 소스 코드 다운로드
1. 실제 비즈니스 요구사항에 따라 SDK 및 관련 [Demo 소스 코드](https://tccweb-1258344699.cos.ap-nanjing.myqcloud.com/sdk/trtc/unity/TRTCUnitySDK.zip)를 다운로드합니다.
2. 다운로드 완료 후 [다운로드 완료, 다음 단계]를 클릭합니다. 이 프로젝트를 직접 Unity로 열 수 있습니다. SDK 파일을 직접 사용하려면 SDK 패키지에 있는 `TRTCUnitySDK/Assets/TRTCSDK/SDK` 폴더를 프로젝트의 Assets 디렉터리에 복사합니다.

3. `Assets/TRTCSDK/Demo/Tools/GenerateTestUserSig.cs` 파일을 찾아 엽니다.
4. `GenerateTestUserSig.cs` 파일에서 관련 매개변수를 설정합니다.
  <ul><li>SDKAPPID: 0으로 기본 설정되어 있습니다. 실제 SDKAppID로 설정하십시오.</li>
  <li>SECRETKEY: 공백으로 기본 설정되어 있습니다. 실제 키 정보로 설정하십시오.</li></ul> 
	<img src="https://main.qcloudimg.com/raw/4dad4541a4a0d400441e9cd75c07ba1e.png"/>

[](id:step3)
### 3단계: 컴파일 실행
<dx-tabs>
::: Android\s 플랫폼
1. Unity Editor를 설정하고 [File]>[Build Setting]을 클릭하여 Android로 전환합니다.
![](https://main.qcloudimg.com/raw/4464eb891829e3505a59c8ec00cc2414.png)
2. Android 기기를 연결하고 [Build And Run]을 클릭하면 Demo가 실행됩니다.
3. 인터페이스 테스트는 enterRoom 호출을 클릭한 후 기타 관련 사항들을 자체 테스트해야 합니다. 데이터 디스플레이 창은 호출 완료를, 다른 창은 콜백 정보를 표시합니다.
:::
::: iOS\s 플랫폼
1. Unity Editor를 설정하고 [File]>[Build Setting]을 클릭하여 iOS로 전환합니다.
![](https://main.qcloudimg.com/raw/3a0ef43000fe53e8e7ff58b6cc243785.png)
2. iPhone 기기를 연결하고 [Build And Run]을 클릭하면 컴파일된 iOS 프로젝트를 저장할 새 디렉터리를 선택해야 합니다. 컴파일이 완료되면 새 창에 Xcode 프로젝트가 팝업됩니다.
:::
::: Windows\s 플랫폼
1. Unity Editor를 설정하고 [File]>[Build Setting]을 클릭하면 `PC, Mac & Linux Standalone`으로 전환됩니다. Target Platform은 Windows를 선택합니다.
![](https://main.qcloudimg.com/raw/580764f661c06cf71c4952727c409c5e.png)
2. [Build And Run]을 클릭하면 Demo가 실행됩니다.
:::
::: macOS\s 플랫폼
1. Unity Editor를 설정하고 [File]>[Build Setting]을 클릭하면 `PC, Mac & Linux Standalone`으로 전환됩니다. Target Platform은 macOS를 선택합니다.
![](https://main.qcloudimg.com/raw/6f3f9c21aa9eeadd7a4e3be377b2a6b3.png)
2. [Build And Run]을 클릭하면 Demo가 실행됩니다.
3. Unity Editor 시뮬레이터를 실행하려면 먼저 `Device Simulator Package`를 설치해야 합니다.
4. [Window]>[General]>[Device Simulator] 클릭
![](https://main.qcloudimg.com/raw/79f707b89553528956a888f48b4d4d6d.png)
:::
</dx-tabs>


[](id:demo)
## Demo 예시
Demo에는 이미 런칭된 API가 대다수 포함되어 있습니다. 테스트 및 호출 참고용으로 사용할 수 있습니다. API 문서 [SDK API(Unity)](https://intl.cloud.tencent.com/zh/document/product/647/40139)를 참조하십시오.
>? UI에 일부 조정 업데이트가 있을 수 있으니 최신 버전을 기준으로 하십시오.

![](https://main.qcloudimg.com/raw/2ce3ab51c6fdc843c1e8b086b55840c0.png)

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
