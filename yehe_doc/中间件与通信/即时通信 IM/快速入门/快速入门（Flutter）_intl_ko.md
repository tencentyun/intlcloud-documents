본 문서는 Tencent Cloud IM Demo(Flutter)를 빠르게 실행하는 방법을 소개합니다.

## 환경 요건

| 플랫폼 | 버전 |
|---------|---------|
| Flutter | 2.2.0 또는 이후 버전. |
|Android|Android Studio 3.5 및 그 이후 버전. App은 Android 4.1 및 그 이후 버전 디바이스 필요.|
|iOS|Xcode 11.0 및 그 이후 버전. 프로젝트에 유효한 개발자 서명이 설정되어 있는지 확인십시오.|

## 전제 조건

[Tencent Cloud 가입](https://intl.cloud.tencent.com/document/product/378/17985)된 계정이 있고 [실명 인증](https://intl.cloud.tencent.com/document/product/378/3629)이 완료되어야 합니다.

## 작업 단계
[](id:step1)

### 1단계: 애플리케이션 생성
1. [IM 콘솔](https://console.cloud.tencent.com/im)에 로그인합니다.
>?이미 애플리케이션이 있는 경우 SDKAppID를 기록하고 [키 정보 가져오기](#step2)를 합니다.
>동일한 Tencent Cloud 계정으로 최대 300개의 IM 애플리케이션을 만들 수 있습니다. 이미 300개의 애플리케이션이 있는 경우 신규 애플리케이션 생성 전에 사용하지 않는 애플리케이션을 [비활성화 및 삭제](https://intl.cloud.tencent.com/document/product/1047/34540)합니다. **애플리케이션 삭제 후에는 SDKAppID에 해당하는 모든 데이터 및 서비스를 복구할 수 없으므로 주의하시기 바랍니다.**
>
2. **애플리케이션 생성** 클릭하고 **애플리케이션 생성** 대화 상자에 애플리케이션 이름을 입력하고 **확인**을 클릭합니다.
![](https://main.qcloudimg.com/raw/15e61a874a0640d517eeb67e922a14bc.png)
3. SDKAppID 정보를 저장하십시오. 콘솔 전체보기 페이지에서 새로 생성된 애플리케이션의 상태, 서비스 버전, SDKAppID, 생성 시간 및 만료 시간을 확인할 수 있습니다.
    ![](https://main.qcloudimg.com/raw/7954cc2882d050f68cd5d1df2ee776a6.png)
4. 생성된 애플리케이션을 클릭한 후, 왼쪽 사이드바의 **보조 툴**>**UserSig 툴**을 클릭하여, UserID 및 UserSig를 생성하고, 로그인에 사용할 UserSig를 복사합니다.
![](https://main.qcloudimg.com/raw/2286644d987d24caf565142ae30c4392.png)

[](id:step2)
### 2단계: SDK와 소스 코드 다운로드
1. 귀하의 실제 비즈니스 요구사항에 따라, SDK 및 관련 [Demo 소스 코드](https://github.com/tencentyun/TIMSDK/tree/master/Flutter/Demo/im_discuss)를 다운로드합니다.
2. 다운로드 완료 및 디렉터리로 이동: TIMSDK/Flutter/Demo/im_discuss
![](https://qcloudimg.tencent-cloud.cn/raw/8b865854e14e8848b4e8d31d8daf55ac.png)
3. Flutter pub get에 종속성을 설치하고, Demo 프로젝트를 실행한 후, 명령줄에 다음을 입력합니다.
<dx-codeblock>
:::  plaintext
flutter run --dart-define=SDK_APPID=xxxx --dart-define=ISPRODUCT_ENV=false --dart-define=KEY=xxxx
:::
</dx-codeblock>
>?
>-  `--dart-define=SDK_APPID=xxxx` 여기서 `xxxx`는 [1단계](#step1)에서 생성한 SDKAppID로 대체합니다.
>- `--dart-define=ISPRODUCT_ENV=false` 개발 또는 프로덕션 환경을 판단하고 개발 환경이라면 false로 표시해 주십시오.
>-  `--dart-define=KEY=xxxx` 여기서 `xxxx`는 [1단계](#step1)의 키 정보로 대체되어야 합니다.
4. Visual Studio 구성 launch.json을 실행합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/e495955902c8a594085aa045891ffe2a.png)


### 3단계(선택 사항): IDE를 사용하여 디버깅 실행
<dx-tabs>
::: Android 플랫폼[](id:android)
1. Android Studio에서 discuss/andorid 디렉터리를 엽니다.
![](https://qcloudimg.tencent-cloud.cn/raw/6516f9b17c58915c4ebc93c5c8829831.png)
2. Android 에뮬레이터를 실행하고 **Build And Run**을 클릭하면 Demo를 실행할 수 있습니다. 임의의 UserID(숫자, 알파벳 조합)를 입력할 수 있습니다.
>?UI에 일부 조정 업데이트가 있을 수 있으니 최신 버전을 기준으로 하십시오.
:::
::: iOS 플랫폼[](id:ios)
1. Xcode를 열고, discuss/ios/Runner.xcodeproj 파일을 엽니다.
![](https://qcloudimg.tencent-cloud.cn/raw/6d74814ba9bce54c7439e8b3cea53e73.png)
2. iPhone을 연결하고 **Build And Run**을 클릭한 후 iOS 프로젝트 컴파일이 완료되어 Xcode 프로젝트 창이 팝업될 때까지 기다립니다.
3. iOS 프로젝트를 열고, 주 Target의 Signing & Capabilities(Apple 개발자 계정 필요)를 설정하여, iPhone 디바이스에서 프로젝트가 실행될 수 있도록 합니다.
4. 프로젝트를 실행하고, 디바이스에서 Demo 디버깅을 진행합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/3fe6bbac88bb21ad7a7822bb297793b3.png)
:::
</dx-tabs>

## FAQ

### 어떤 플랫폼이 지원됩니까?
현재 iOS, Android 및 Web 세 개의 플랫폼을 모두 지원하며, Windows와 Mac 버전도 개발 중이니 많은 관심 부탁 드립니다.

### Android에서 Build And Run 클릭 후, 사용 가능한 디바이스를 찾을 수 없다는 오류가 보고되면 어떻게 해야 합니까?
디바이스가 다른 리소스에 의해 점유되어 있지 않은지 확인하거나, **Build**를 클릭하여 APK 패키지를 생성한 다음 에뮬레이터로 드래그하여 실행합니다.

### iOS 최초 실행 시 오류가 보고되면 어떻게 합니까?
상기 내용에 따라 설정된 Demo 실행 시 오류가 보고되면, **Product** > **Clean**을 클릭하여 지우고 다시 Build 또는 Xcode를 닫고 재실행 후 다시 Build합니다.

### Flutter 환경 문제
Flutter 환경에 문제가 있는지 알려면 Flutter Doctor를 실행하여 Flutter 환경이 설치되어 있는지 점검하십시오.
