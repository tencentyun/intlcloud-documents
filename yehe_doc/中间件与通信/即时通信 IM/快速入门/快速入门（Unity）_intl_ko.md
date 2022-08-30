본문은 Tencent Cloud IM Demo(Unity)를 빠르게 실행하는 방법을 소개합니다.

## 환경 요건

| 플랫폼 | 버전 |
|---------|---------|
| Unity | 2019.4.15f1 및 그 이후 버전. |
|Android|Android Studio 3.5 및 그 이후 버전. App은 Android 4.1 및 그 이후 버전 디바이스 필요.|
|iOS|Xcode 11.0 및 그 이후 버전. 프로젝트에 유효한 개발자 서명이 설정되어 있는지 확인십시오.|

## 전제 조건

[Tencent Cloud 가입](https://intl.cloud.tencent.com/document/product/378/17985)된 계정이 있고 [실명 인증](https://intl.cloud.tencent.com/document/product/378/3629)이 완료되어야 합니다.

## 작업 단계


[](id:step1)
### 1단계: IM 애플리케이션 생성
1. [IM 콘솔](https://console.cloud.tencent.com/im)에 로그인합니다.
>?이미 애플리케이션이 있는 경우 SDKAppID를 기록하고 [키 정보 가져오기](#step2)를 합니다.
>동일한 Tencent Cloud 계정으로 최대 300개의 IM 애플리케이션을 만들 수 있습니다. 이미 300개의 애플리케이션이 있는 경우 신규 애플리케이션 생성 전에 사용하지 않는 애플리케이션을 [비활성화 및 삭제](https://intl.cloud.tencent.com/document/product/1047/34540)합니다. **애플리케이션 삭제 후에는 SDKAppID에 해당하는 모든 데이터 및 서비스를 복구할 수 없으므로 주의하시기 바랍니다.**
>
2. **애플리케이션 생성**을 클릭하고 **애플리케이션 생성** 대화 상자에 애플리케이션 이름을 입력한 후 **확인**을 클릭합니다.
![](https://main.qcloudimg.com/raw/15e61a874a0640d517eeb67e922a14bc.png)
3. 왼쪽 사이드바에서 **[보조 툴](https://console.cloud.tencent.com/im/tool-usersig)** > **UserSig Generation & Verification**을 클릭하여 UserID 및 해당 UserSig를 생성하고 서명 정보를 복사하여 [5단계](#step5)에서 사용합니다.
![](https://main.qcloudimg.com/raw/2286644d987d24caf565142ae30c4392.png)

[](id:step2)
### 2단계: Unity 프로젝트 생성
Unity를 사용하여 Unity 프로젝트를 생성합니다. 프로젝트의 위치를 ​​기억하십시오.

[](id:step3)
### 3단계: 종속성 파일 수정
1. IDE(예시: Visual Studio Code)를 통해 프로젝트를 엽니다.
![](https://qcloudimg.tencent-cloud.cn/raw/1a21933037a72a6bd4c8ed14f08c6ca7.png)
2. 디렉터리에 따라 Packages/manifest.json을 찾아 종속성을 다음과 같이 수정합니다.
```json
{
    "dependencies":{
    "com.tencent.imsdk.unity":"https://github.com/TencentCloud/TIMSDK.git#unity" 
  }
}
```

[](id:step4)
### 4단계: 종속성 로딩
Unity Editor에서 프로젝트를 열고 종속성 로딩이 완료되기를 기다렸다가 Tencent Cloud IM이 로딩되었는지 확인합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/d98dfb17bbee6c0319e370de6f2ba9dd.jpg)

[](id:step5)
### 5단계: 스크립트 테스트
1. [테스트 스크립트(TestApi.cs)](https://github.com/TencentCloud/TIMSDK/blob/master/Unity/im_unity_sdk_plus/Assets/Demo/TestApi.cs) 및 [구성 파일(Config.cs)](https://github.com/TencentCloud/TIMSDK/blob/master/Unity/im_unity_sdk_plus/Assets/Demo/Config.cs)을 가져오고, Config.cs 에서 SDKAppID, UserID, UserSig, toUserID 매개변수를 최적화한 후 TestApi.cs를 테스트 시나리오의 Camera에 바인딩합니다.
    ![](https://qcloudimg.tencent-cloud.cn/raw/b4d770775523fdd76b75f1d80f07c925.jpg)

2. Unity Editor 실행 버튼을 클릭하여 시나리오 실행을 시작합니다. Init(SDK 초기화), Login(IM에 로그인) 및 기타 테스트 버튼을 클릭하여 테스트합니다.

  <img src="https://qcloudimg.tencent-cloud.cn/raw/40fb0f381096840418b66b804d403140.png" alt="image-20220616115353114" style="zoom:50%;" />
	
## FAQ

### 어떤 플랫폼이 지원됩니까?
현재 iOS, Android, Windows 및 Mac이 지원됩니다.

### Android에서 Build And Run 클릭 후, 사용 가능한 디바이스를 찾을 수 없다는 오류가 보고되면 어떻게 해야 합니까?
디바이스가 다른 리소스에 의해 점유되어 있지 않은지 확인하거나, Build를 클릭하여 apk 패키지를 생성한 다음 시뮬레이터로 드래그하여 실행합니다.

### iOS 최초 실행 시 오류가 보고되면 어떻게 합니까?
상기 내용에 따라 설정된 Demo 실행 시 오류가 보고되면, **Product**>**Clean**을 클릭하여 지우고 다시 Build하거나, Xcode를 닫고 재실행 후 다시 Build합니다.
### Unity 2019.04 버전이 iOS 플랫폼에서 오류가 보고되면 어떻게 합니까?
Library/PackageCache/com.unity.collab-proxy@1.3.9/Editor/UserInterface/Bootstrap.cs(23,20): error CS0117: 'Collab' does not contain a definition for 'ShowChangesWindow'
Editor 툴바에서 **Window**>**Package Manager**를 클릭하여 Unity Collaborate를 1.2.16으로 다운그레이드합니다.

### Unity 2019.04 버전이 iOS 플랫폼에서 오류가 보고되면 어떻게 합니까?
Library/PackageCache/com.unity.textmeshpro@3.0.1/Scripts/Editor/TMP_PackageUtilities.cs(453,84): error CS0103: The name 'VersionControlSettings' does not exist in the current context
소스 코드를 열고 `|| VersionControlSettings.mode != "Visible Meta Files"` 코드를 삭제합니다.
