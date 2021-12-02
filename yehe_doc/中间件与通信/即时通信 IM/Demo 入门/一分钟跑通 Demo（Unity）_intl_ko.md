본문은 Tencent Cloud IM Demo(Unity)를 빠르게 실행하는 방법을 소개합니다.

## 환경 요건

| 플랫폼 | 버전 |
|---------|---------|
| Unity | 2019.4.15f1 및 그 이후 버전. |
|Android|Android Studio 3.5 및 그 이후 버전. App은 Android 4.1 및 그 이후 버전 디바이스 필요.|
|iOS|Xcode 11.0 및 그 이후 버전. 프로젝트에 유효한 개발자 서명이 설정되어 있는지 확인십시오.|

## 전제 조건

[Tencent Cloud 가입](https://intl.cloud.tencent.com/document/product/378/17985)된 계정이 있고 [실명 인증](https://intl.cloud.tencent.com/document/product/378/3629)이 완료되어야 합니다.

## 작업 절차
[](id:step1)
## 1단계: 애플리케이션 생성
1. [IM 콘솔](https://console.cloud.tencent.com/im)에 로그인합니다.
 >? 이미 애플리케이션이 있는 경우 SDKAppID를 기록하고 [키 정보 가져오기](#step2)를 합니다.
 >동일한 Tencent Cloud 계정으로 최대 300개의 IM 애플리케이션을 만들 수 있습니다. 이미 300개의 애플리케이션이 있는 경우 신규 애플리케이션 생성 전에 사용하지 않는 애플리케이션을 ​​[비활성화 및 삭제](https://intl.cloud.tencent.com/document/product/1047/34540)합니다. **애플리케이션 삭제 후에는 SDKAppID에 해당하는 모든 데이터 및 서비스를 복구할 수 없으므로 주의하시기 바랍니다. **
 >
2. [신규 애플리케이션 생성]을 클릭하고 [애플리케이션 생성] 대화 상자에 애플리케이션 이름을 입력한 후 [확인]을 클릭합니다.
![](https://main.qcloudimg.com/raw/15e61a874a0640d517eeb67e922a14bc.png)
3. SDKAppID 정보를 저장하십시오. 콘솔 전체보기 페이지에서 새로 생성된 애플리케이션의 상태, 서비스 버전, SDKAppID, 생성 시간 및 만료 시간을 확인할 수 있습니다.
    ![](https://main.qcloudimg.com/raw/7954cc2882d050f68cd5d1df2ee776a6.png)
4. 생성된 애플리케이션을 클릭한 후, 왼쪽 메뉴의 [보조 툴]>[UserSig 툴]을 클릭하여, UserID 및 UserSig를 생성하고, 로그인에 사용할 UserSig를 복사합니다.
![](https://main.qcloudimg.com/raw/2286644d987d24caf565142ae30c4392.png)

[](id:step2)
## 2단계: SDK 및 소스 코드 다운로드
1. 실제 비즈니스 요구사항에 따라 SDK 및 관련 [Demo 소스 코드](https://intl.cloud.tencent.com/document/product/1047/33996)를 다운로드합니다.
2. 다운로드 후, Package를 더블클릭하여 열고, 패키지의 리소스를 전체 선택하여 현재의 Unity 프로젝트로 가져오기 합니다.
![](https://main.qcloudimg.com/raw/c338ce838fff81841f85b06fd3dc5c6c.png)
3. Assets/TIMCloud/Demo/ExampleEntry.cs 소스 코드를 열고, [1단계](#step1)에서 얻은 SDKAppID, UserID, UserSig를 아래 그림의 붉은색 박스에 입력한 후, Config.key가 있는 행을 주석 처리합니다.
![](https://main.qcloudimg.com/raw/e31692ae98503221f45ece41039ead92.png)
4. ExampleEntry.cs 주석으로 userSig 로직을 동적으로 가져옵니다(동적으로 가져오기 설정이 약간 더 복잡하기 때문에 추후에 별도로 설정해도 됩니다).
![](https://main.qcloudimg.com/raw/7a8ac734ac60a73caf6139fc0d1d250f.png)

## 3단계: 패키지 실행
### Android 플랫폼
1. Unity Editor를 설정하고 [File]>[Build Setting]을 클릭하여 Android로 전환합니다.
![](https://main.qcloudimg.com/raw/d913d32e36aa01ff93acf0316d4f103f.png)
2. Android 시뮬레이터를 실행하고, [Build And Run]을 클릭하면 Demo가 실행됩니다.

>- Demo에는 이미 런칭된 모든 API가 포함되어 있으며, 테스트 및 호출 레퍼런스로 사용할 수 있습니다. API 문서 [SDK API(Unity)](https://intl.cloud.tencent.com/document/product/1047/40125)를 참고하십시오.
> - UI에 일부 변동이 있을 수 있으니 최신 버전을 기준으로 하십시오.
>
![](https://main.qcloudimg.com/raw/e6f3583d0b807af62a27ee753cfa3b53.png)
3. 인터페이스를 테스트하려면 첫 번째 줄의 두 번째 입력창에 UserID를 추가한 다음, initSDK와 login를 호출하면, 데이터 표시창에 호출 완료가 표시되고, 다른 인터페이스도 호출해볼 수 있습니다.

### iOS 플랫폼
1. Unity Editor를 설정하고 [File]>[Build Setting]을 클릭하여 iOS로 전환합니다.
![](https://main.qcloudimg.com/raw/3982b96c4f9e76107bb4aadac33a5de5.png)
2. iPhone 디바이스 연결 및 [Build And Run] 클릭 후, 컴파일된 iOS 프로젝트를 저장할 새로운 디렉터리를 선택합니다. 컴파일이 완료되면 새 창에 Xcode 프로젝트가 팝업됩니다.
3. iOS 프로젝트를 열고, 주 Target의 Signing & Capabilities(Apple 개발자 계정 필요)를 설정하여, iPhone 디바이스에서 프로젝트가 실행될 수 있도록 합니다.
4. 프로젝트를 실행하고, 디바이스에서 Demo 디버깅을 진행합니다.

## FAQ

### 어떤 플랫폼이 지원됩니까?
현재 iOS와 Android 플랫폼을 모두 지원하며, Windows와 Mac 버전도 개발 중이니 많은 관심 부탁드립니다.

### Android에서 Build And Run 클릭 후, 사용 가능한 디바이스를 찾을 수 없다는 오류가 보고되면 어떻게 해야 합니까?
디바이스가 다른 리소스에 의해 점유되어 있지 않은지 확인하거나, Build를 클릭하여 apk 패키지를 생성한 다음 시뮬레이터로 드래그하여 실행합니다.

### iOS 최초 실행 시 오류가 보고되면 어떻게 합니까?
상기 내용에 따라 설정된 Demo 실행 시 오류가 보고되면, [Product]> [Clean]을 클릭하여 지우고 다시 Build하거나, Xcode를 닫고 재실행 후 다시 Build합니다.
### Unity 2019.04 버전이 iOS 플랫폼에서 오류가 보고되면 어떻게 합니까?
Library/PackageCache/com.unity.collab-proxy@1.3.9/Editor/UserInterface/Bootstrap.cs(23,20): error CS0117: 'Collab' does not contain a definition for 'ShowChangesWindow'
Editor 툴바에서 [Window]>[Package Manager]를 클릭하여 Unity Collaborate를 1.2.16으로 다운그레이드합니다.

### Unity 2019.04 버전이 iOS 플랫폼에서 오류가 보고되면 어떻게 합니까?
Library/PackageCache/com.unity.textmeshpro@3.0.1/Scripts/Editor/TMP_PackageUtilities.cs(453,84): error CS0103: The name 'VersionControlSettings' does not exist in the current context
소스 코드를 열고 `|| VersionControlSettings.mode != "Visible Meta Files"` 코드를 삭제합니다.
