Tencent Cloud IM은 HBuilderX에서 Android 및 iOS를 컴파일하기 위해 Web IM SDK 기반 애플리케이션을 공식 출시했으며 멀티 단말 패키징을 구현할 수 있습니다.

## 온라인 고객서비스 시나리오
고객 서비스 그룹 예시, 친구 기본 템플릿 예시가 제공되며, 다음과 같은 온라인 고객서비스 시나리오 기능이 포함됩니다.
- 문자 메시지, 이미지 메시지, 음성 메시지, 비디오 메시지 등의 일반적인 메시지 전송을 지원합니다.
- 일반적인 용어, 주문, 서비스 평가 등의 사용자 정의 메시지를 지원합니다.
- 그룹 채팅 세션 생성, 그룹 구성원 관리 등을 지원합니다.


## 작업 단계
### 1단계: uni-app 계정 등록 및 생성
1. app 개발 환경을 구축하려면 [HBuilderX 편집기](https://www.dcloud.io/hbuilderx.html)를 다운로드하십시오.
>!현재 프로젝트에서 사용 중인 HBuilderX의 최신 버전입니다. 이전에 HBuilderX를 다운로드한 적이 있다면 최신 버전으로 업데이트하여 통합 개발 환경을 보장하십시오.
2. [DCloud 개발자 센터](https://dev.dcloud.net.cn/) 가입 후 HBuilderX 편집기에 로그인합니다.

### 2단계: 애플리케이션 생성
1. [IM 콘솔](https://console.cloud.tencent.com/im)에 로그인합니다.
>?
>- 이미 애플리케이션이 있는 경우 SDKAppID를 기록하고 [키 정보 가져오기](#step2)를 합니다.
>- 동일한 Tencent Cloud 계정으로 최대 300개의 IM 애플리케이션을 만들 수 있습니다. 이미 300개의 애플리케이션이 있는 경우 신규 애플리케이션 생성 전에 사용하지 않는 애플리케이션을 [비활성화 및 삭제](https://intl.cloud.tencent.com/document/product/1047/34540)합니다. **애플리케이션 삭제 후에는 SDKAppID에 해당하는 모든 데이터 및 서비스를 복구할 수 없으므로 주의하시기 바랍니다.**
>
2. **애플리케이션 생성** 클릭하고  **애플리케이션 생성** 대화 상자에 애플리케이션 이름을 입력하고 **확인**을 클릭합니다.
![](https://main.qcloudimg.com/raw/15e61a874a0640d517eeb67e922a14bc.png)
3. SDKAppID 정보를 저장하십시오. 콘솔 전체보기 페이지에서 새로 생성된 애플리케이션의 상태, 서비스 버전, SDKAppID, 생성 시간 및 만료 시간을 확인할 수 있습니다.
    ![](https://main.qcloudimg.com/raw/7954cc2882d050f68cd5d1df2ee776a6.png)
4. 생성된 애플리케이션을 클릭한 후, 왼쪽 메뉴의 **보조 툴**>**UserSig 툴**을 클릭하여, UserID 및 UserSig를 생성하고, 로그인에 사용할 UserSig를 복사합니다.
![](https://main.qcloudimg.com/raw/2286644d987d24caf565142ae30c4392.png)
>!키 정보가 유출되지 않도록 잘 보관하십시오.

### 3단계: uni-app 소스 코드 다운로드 및 설정
1. 실제 비즈니스 요구사항에 따라 SDK 및 관련 [Demo 소스 코드](https://intl.cloud.tencent.com/document/product/1047/33996)를 다운로드합니다.
```javascript
# 명령 라인 실행
git clone https://github.com/tencentyun/TIMSDK.git

# uni-app TUIKit 프로젝트 진입
cd TIMSDK/uni-app/TUIKit
```
2. uni-app의 TUIKit 프로그래밍 파일을 자신의 HBuilderX 프로그램(버전 3.2.11.20211021-alpha)으로 가져옵니다. 공식 홈페이지 [uni-app 개발](https://uniapp.dcloud.io/quickstart-hx)을 참고하십시오.
3. GenerateTestUserSig 파일에서 관련 매개변수를 설정합니다.
- `debug/GenerateTestUserSig.js` 파일을 찾아 엽니다.
- `GenerateTestUserSig.js` 파일에서 관련 매개변수를 설정합니다.
  <ul><li>SDKAPPID: 0으로 기본 설정되어 있으며 실제 SDKAppID로 설정하십시오.</li>
  <li>SECRETKEY: 공백으로 기본 설정되어 있으며 실제 키 정보로 설정하십시오.</li></ul> 
  

>! 
>- 본 문서의 `UserSig`는 클라이언트 코드에서 `SECRETKEY`를 설정하여 생성합니다. 이 방법에서 `SECRETKEY`는 디컴파일로 크래킹되기 쉬우므로, 키가 유출되면 해커가 귀하의 Tencent Cloud 트래픽을 도용할 수 있습니다. 따라서 **해당 방법은 로컬 uni-app 실행 및 기능 디버깅용으로 적합합니다**.
>- 정확한 `UserSig` 발급 방식은 다음과 같습니다. `UserSig` 계산 코드를 귀하의 서버에 통합하고 App 방향의 인터페이스를 제공합니다. `UserSig`가 필요할 때 귀하의 App이 비즈니스 서버로 동적 `UserSig`를 요청합니다. 자세한 내용은 [서버의 UserSig 생성](https://intl.cloud.tencent.com/document/product/647/35166)을 참고하십시오.

###  4단계: 컴파일 실행
공식 [uni-app 실행](https://uniapp.dcloud.io/quickstart-hx?id=%e8%bf%90%e8%a1%8cuni-app)을 참고하십시오.

###  5단계: 패키징 배포

 공식 [uni-app 패키징](https://uniapp.dcloud.io/quickstart-hx?id=%e5%8f%91%e5%b8%83uni-app)을 참고하십시오.
- 네이티브 App - 클라우드 패키징: **HBuilderX 편집기** > **배포** > **네이티브 App** - **클라우드 패키징** (app 아이콘, 실행 페이지 등의 세부 설정은 manifest.json에서 설정 가능)
- 네이티브 App - 오프라인 패키징: **HBuilderX 편집기** > **배포** > 로컬 패키징된 App 리소스 생성 (자세한 패키징 방안은 iOS, Android 로컬 패키징 가이드 참고)

## FAQ
[](id:Q1)
### 1. uni-app은 Android, iOS를 동시에 지원하는데 어떤 IM SDK를 선택해야 합니까?
`tim-wx-sdk` 를 선택하여 npm으로 설치하거나 정적으로 가져오십시오.
```javascript
    // v2.11.2부터 SDK는 WebSocket을 지원하므로 통합을 권장합니다. v2.10.2 이하 버전은 HTTP를 사용합니다.
	npm install tim-wx-sdk@2.15.0 --save
	import TIM from 'tim-wx-sdk';
	// SDK 인스턴스를 생성합니다. `TIM.create()` 메소드는 동일한 `SDKAppID`에 대해 동일한 인스턴스만 반환합니다.
	uni.$TUIKit = TIM.create({
		SDKAppID: 0  // 액세스 시 0이 IM 애플리케이션의 SDKAppID로 대체됩니다.
	});
	
	// SDK 로그 출력 레벨을 설정합니다. 자세한 레벨은 setLogLevel 인터페이스 설명을 참고하십시오.
	uni.$TUIKit.setLogLevel(0); // 일반 레벨. 로그량이 많을 경우, 통합 시 사용을 권장합니다.
	// uni.$TUIKit.setLogLevel(1); // release 레벨. SDK는 주요 정보를 출력하므로 프로덕션 환경에서 사용하십시오.
```
프로젝트에 관계망 기능이 필요한 경우 `tim-wx-friendship.js`를 사용하십시오.
```javascript
	import TIM from 'tim-wx-sdk/tim-wx-friendship.js';
```
>?
>- **Uni-app이 tim을 더 잘 사용하고, 빠른 문제 진단 및 해결을 위해 Uni.$TUIKit 이름을 수정하지 마십시오. 만약 tim을 이미 통합했다면 uni.tim을 Uni.$TUIKit으로 수정하십시오.**
>- IM SDK를 [2.15.0](https://intl.cloud.tencent.com/document/product/1047/34281)으로 업그레이드하십시오. 이 버전은 iOS 음성 재생을 지원합니다.
>- 동기화 종속성 프로세스 중 문제가 발생하면 npm 소스를 전환하고 다시 시도하십시오.
```javascript
	cnpm 소스 전환
	>npm config set registry http://r.cnpmjs.org/
	>
	>
```

[](id:Q2)
### 2. 이미지, 비디오 및 음성 메시지와 같은 리치 미디어 메시지를 업로드하는 방법은 무엇입니까?
`cos-wx-sdk-v5`를 사용하십시오.
```javascript
    // 이미지, 음성, 비디오 등 메시지를 보내려면 cos-wx-sdk-v5 업로드 플러그 인이 필요합니다.
	npm install cos-wx-sdk-v5@0.7.11 --save
	import COS from "cos-wx-sdk-v5";
	// COS SDK 플러그 인 가입
	uni.$TUIKit.registerPlugin({
		'cos-wx-sdk': COS
	});
```

[](id:Q3)
### 3. uni-app  패키징 iOS 음성 메시지를 재생할 수 없는 경우 어떻게 해야 합니까?
  IM SDK를 [2.15.0](https://intl.cloud.tencent.com/document/product/1047/34281)으로 업그레이드하십시오. 이 버전은 iOS 음성 메시지 재생을 지원합니다.

[](id:Q4)
### 4. uni-app  패키징 app 음성 메시지 발송 시 오류가 발생하면 어떻게 해야 합니까?
   Uni-app 패키징 app은 `recorderManager.onStop`의 콜백에 `duration`과 `fileSize`가 없으므로 사용자가 스스로 duration과 fileSize를 추가해야 합니다.
- **로컬 타이머를 통해 시간을 기록하여 duration을 계산합니다.**
- **파일 크기의 로컬 계산. fileSize = (오디오 비트 레이트) x 시간 길이(단위: 초) / 8, 대략적인 추정치.**
자세한 코드는 [uni-app TUIKit](https://github.com/tencentyun/TIMSDK/tree/master/uni-app)를 참고하십시오.
>!
>
>- 음성 메시지 객체는 'duration' 및 'fileSize'를 포함해야 합니다. 'fileSize'가 없으면 음성 메시지 지속 시간은 잘못된 숫자의 문자열입니다.

[](id:Q5)
### 5. video 메시지 레벨이 높아서 슬라이드할 수 없으면 어떻게 해야 합니까?
 본 프로젝트에서는 `video`를 직접 렌더링하지 않고 대신 비디오 이미지를 사용하여, 재생 중 렌더링 방식으로 인해 레벨이 과도하게 높아지는 문제를 피할 수 있습니다.
 자세한 코드는 [uni-app TUIKit](https://github.com/tencentyun/TIMSDK/tree/master/uni-app)를 참고하십시오.
>!공식 [네이티브 컴포넌트 설명](https://uniapp.dcloud.io/component/native-component)을 참고하십시오.

[](id:Q6)

### 6. 디바이스 미리보기 시 시스템 오류가 보고되는데, 용량이 너무 크면 어떻게 해야 하나요?
실행 시 코드 압축을 선택하여 미니프로그램 에뮬레이터 실행>실행 시 코드 압축 여부를 확인하십시오.

[](id:Q7)



## 기술 컨설팅
자세한 내용은 [고객센터](https://intl.cloud.tencent.com/zh/contact-us)를 참고하십시오.

## 참고 문서

- [SDK API 매뉴얼](https://web.sdk.qcloud.com/im/doc/zh-cn/SDK.html)
- [SDK 업데이트 로그](https://intl.cloud.tencent.com/document/product/1047/34281)
- [uni-app TUIKit 소스 코드](https://github.com/tencentyun/TIMSDK/tree/master/uni-app)
- [uni-app TUIKit 소스 코드 빠른 통합](https://intl.cloud.tencent.com/document/product/1047/43893)

