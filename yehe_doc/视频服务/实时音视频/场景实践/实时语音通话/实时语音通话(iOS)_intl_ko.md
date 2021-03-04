## 효과













빠르게 음성 통화 기능을 실행해야 할 경우, 제공되는 Demo를 수정하여 적용하거나 TRTCCalling 모듈을 사용해 UI 인터페이스를 정의하십시오.

>! 이전에 제공한 TRTCAudioCall 모듈의 구버전은 [모듈 라이브러리](https://github.com/tencentyun/LiteAVClassic)로 이동되었습니다. TRTCCalling 모듈은 IM 신호 인터페이스를 사용하며, 구버전 모듈과는 호환되지 않습니다.

<span id="ui"> </span>

## Demo의 UI 인터페이스 재사용

<span id="ui.step1"></span>

### 1단계: 신규 애플리케이션 생성

1. TRTC 콘솔에 로그인하여 [Development Assistance]>[Demo 빠른 실행](https://console.cloud.tencent.com/trtc/quickstart)을 선택합니다.
2. [시작하기]를 클릭하고 애플리케이션 이름(예: `TestVideoCall`)을 입력한 후 [애플리케이션 생성]을 클릭합니다.

>! 이 기능은 동시에 Tencent Cloud [TRTC](https://intl.cloud.tencent.com/document/product/647/35078) 및 [실시간 통신 IM](https://intl.cloud.tencent.com/document/product/1047)를 기초로 한 PAAS 서비스로, TRTC 활성화 후 동기화해 실시간 IM 서비스를 활성화시킵니다. 실시간 통신 IM은 부가 서비스에 속하며, 자세한 과금 규정은 [실시간 통신 IM 가격 설명](https://intl.cloud.tencent.com/document/product/1047/34350)을 참조하십시오. 



<span id="ui.step2"></span>

### 2단계: SDK와 Demo 소스 코드 다운로드

1. 커서를 상응하는 카드로 이동 후 [Github](https://github.com/tencentyun/TRTCSDK/tree/master/iOS)를 클릭하여 Github(혹은 [ZIP](https://liteavsdk-1252463788.cosgz.myqcloud.com/TXLiteAVSDK_TRTC_iOS_latest.zip) 클릭)로 이동하여 SDK 및 Demo 소스 코드를 다운로드합니다.
   ![](https://main.qcloudimg.com/raw/b0f6f1bd5e0bc083bafddcc7c04a1593.png)
2. 다운로드 완료 후 TRTC 콘솔로 돌아가 [다운로드 완료, 다음 단계]를 클릭하면 SDKAppID와 키 정보를 확인할 수 있습니다.

<span id="ui.step3"></span>

### 3단계: Demo 프로그래밍 파일 설정

1. [2단계](#ui.step2)에서 다운로드한 소스 패키지를 압축 해제합니다.
2. `iOS/TRTCScenesDemo/TXLiteAVDemo/Debug/GenerateTestUserSig.h` 파일을 찾아 열어줍니다.
3. `GenerateTestUserSig.h` 파일에서 관련 매개변수를 설정합니다.
	- SDKAPPID: 0으로 기본 설정되어 있습니다. 실제 SDKAppID로 설정하십시오.
	- SECRETKEY: 공백으로 기본 설정되어 있습니다. 실제 키 정보로 설정하십시오.
![](https://main.qcloudimg.com/raw/87dc814a675692e76145d76aab91b414.png)
4. TRTC 콘솔로 돌아가 [붙여넣기 완료, 다음 단계]를 클릭합니다.
5. [가이드 닫기, 콘솔 관리 애플리케이션 열기]를 클릭합니다.

>!
>본 문서의 UserSig는 클라이언트 코드에서 SECRETKEY를 설정하여 생성합니다. 본 방법에서의 SECRETKEY는 디컴파일로 크래킹되기 쉬워, 일단 키가 유출되면 해커가 Tencent Cloud 트래픽을 도용할 수 있습니다. 따라서 **해당 방법은 로컬 Demo 실행 및 기능 디버깅용으로 적합합니다**.
>정확한 UserSig 발급 방식은 다음과 같습니다. UserSig 계산 코드를 사용자의 서버에 통합하고 App 방향의 인터페이스를 제공합니다. UserSig가 필요할 때 사용자의 App이 비즈니스 서버로 동적 UserSig 획득을 요청합니다. 자세한 내용은 [서버의 UserSig 생성](https://intl.cloud.tencent.com/document/product/647/35166#Server)을 참조하십시오.

<span id="ui.step4"></span>

### 4단계: Demo 실행

Xcode(11.0 버전 이상)를 사용하여 소스 코드 프로그램인 `iOS/TRTCScenesDemo/TXLiteAVDemo.xcworkspace`를 열고 [실행]을 클릭하면 본 Demo 디버깅을 시작할 수 있습니다.

<span id="ui.step5"></span>

### 5단계: Demo 소스 코드 수정

소스코드 폴더 `TRTCCallingDemo`의 2개의 하위 폴더 ui와 model 중 ui 폴더 내용은 모두 인터페이스 코드입니다.

|              파일 혹은 폴더              | 기능 설명                                                 |
| ------------------------------------ | ------------------------------------------------------- |
|  TRTCCallingVideoViewController.swift  | 영상 통화 메인 인터페이스을 표시하고, 이 인터페이스에서 통화 수락과 거절을 완료합니다. |
|  TRTCCallingAudioViewController.swift  | 음성 통화 메인 인터페이스를 표시하고, 이 인터페이스에서 통화 수락과 거절을 완료합니다. |
| TRTCCallingContactViewController.swift | 대화상대 검색 화면 표시에 사용                               |


<span id="model"> </span>

## 사용자 정의 UI 인터페이스 구현

[소스 코드](https://github.com/tencentyun/TRTCSDK/tree/master/iOS/TRTCScenesDemo/TXLiteAVDemo/TRTCCallingDemo) 폴더 `TRTCCallingDemo`에는 두 개의 하위 폴더 ui와 model이 포함되어 있으며, model 폴더에는 Tencent Cloud가 구현한 재사용 가능 오픈 소스 모듈 TRTCCalling이 포함되어 있습니다. `TRTCCalling.h` 파일에서 이 모듈이 제공하는 인터페이스 함수를 볼 수 있습니다.
![](https://main.qcloudimg.com/raw/78cc06cd53538243bc52abc381350c55.jpg)

오픈 소스 컴포넌트 TRTCCalling을 사용해 UI 인터페이스를 실행하고, model 부분을 재사용해 직접 UI 부분을 실행할 수 있습니다.

<span id="model.step1"> </span>

### 1단계: SDK 통합

통화 모듈 TRTCCalling은 TRTC SDK와 IM SDK에 종속되어 있습니다. 아래 절차에 따라 두 가지 SDK를 프로젝트에 통합할 수 있습니다.

- **방법1: cocoapods 라이브러리를 통해 종속**
```
pod 'TXIMSDK_iOS'
pod 'TXLiteAVSDK_TRTC'
```
>? 2개의 SDK 제품의 최신 버전 넘버, [TRTC](https://github.com/tencentyun/TRTCSDK) 및 [실시간 통신 IM](https://github.com/tencentyun/TIMSDK)의 Github 첫 페이지에서 획득할 수 있습니다.
- **방법2: 로컬 종속**
  개발 환경에서 cocoapods 라이브러리 액세스가 느릴 경우, ZIP을 다운로드하고 통합 문서를 따라 수동으로 프로그램에 통합할 수 있습니다.
<table>
<tr><th>SDK</th><th>다운로드 페이지</th><th>통합 가이드</th></tr>
<tr>
<td>TRTC SDK</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34615">DOWNLOAD</a></td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/35093">문서 통합</a></td>
</tr><tr>
<td>IM SDK</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">DOWNLOAD</a></td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/34306">문서 통합</a></td>
</tr></table>

<span id="model.step2"> </span>

### 2단계: 권한 설정

info.plist 파일에 `Privacy - Camera Usage Description`, `Privacy - Microphone Usage Description`을 추가해 카메라 및 마이크 권한을 신청해야 합니다.

<span id="model.step3"> </span>

### 3단계: TRTCCalling 모듈 가져오기

다음 디렉터리의 모든 파일을 프로젝트에 복사합니다.
```
iOS/TRTCSceneDemo/TXLiteAVDemo/TRTCCallingDemo/model 
```

<span id="model.step4"> </span>

### 4단계: 초기화 및 모듈 로그인

1. 푸시 관련 정보 설정
```
[TRTCCalling shareInstance].imBusinessID = your business ID;
[TRTCCalling shareInstance].deviceToken =  deviceToken;
```
2. `login(sdkAppID: UInt32, user: String, userSig: String, success: @escaping (() -> Void), failed: @escaping ((_ code: Int, _ message: String) -> Void))`을 호출해 모듈 로그인을 완료합니다. 그 중 몇몇 주요 매개변수는 다음 표를 참조하십시오.
 <table>
<tr><th>매개변수 이름</th><th>역할</th></tr>
<tr>
<td>sdkAppID</td>
<td><a href="https://console.cloud.tencent.com/trtc/app">TRTC 콘솔</a>에서 SDKAppID를 조회할 수 있습니다.</td>
</tr><tr>
<td>user</td>
<td>현재 사용자의 ID, 문자열 유형은 영어 알파벳(a-z, A-Z), 숫자(0-9), 대시 부호(-), 언더바(_)만 허용됩니다.</td>
</tr><tr>
<td>userSig</td>
<td> <a href="https://intl.cloud.tencent.com/document/product/647/35166">UserSig 계산 방법</a>.</td>
</tr></table>
<pre>
// 로그인
[[TRTCCalling shareInstance] login:SDKAPPID user:userID userSig:userSig success:^{
        NSLog(@"Audio call login success.");
} failed:^(int code, NSString *error) {
        NSLog(@"Audio call login failed.");
}];
</pre>

<span id="model.step5"> </span>
### 5단계: 1v1 통화 구현

1. 발신자가 TRTCCalling을 호출하는 `call(userId, callType)` 방법, `userId` 매개변수는 사용자 ID이며, `callType` 전달 음성 유형 `CallType_Audio`로 음성 통화 요청을 할 수 있습니다.
2. 수신자는 `onInvited` 이벤트를 수신합니다. 이때 `accept`로 통화를 수락할 수 있으며, `reject`로 통화를 거절할 수도 있습니다.
3. 발신자가 `onUserEnter` 콜백을 받는 경우, 수락 측이 통화에 입장했다는 것을 의미합니다.

```Objective-C
// 1. 리스너 콜백
[[TRTCCalling shareInstance] addDelegate:delegate];

//수신/거절
// 이때 B도 IM 시스템에 로그인하면 onInvited(A, null, false) 콜백을 수신합니다.
// TRTCCalling의 accept 방법 호출해 수락 / TRTCCalling의 reject 방법으로 거절할 수 있습니다.
-(void)onInvited:(NSString *)sponsor
         userIds:(NSArray<NSString *> *)userIds
     isFromGroup:(BOOL)isFromGroup
        callType:(CallType)callType {
    [[TRTCCalling shareInstance] accept];
}

// 2. 모듈의 다른 기능 함수를 호출해 통화 혹은 통화 끊기 요청
// 주의: 로그인을 먼저 해야만 정상적인 호출 가능
// 영상 통화 발신
[[TRTCCalling shareInstance] call:@"타깃 사용자" type:CallType_Audio];
// 끊기
[[TRTCCalling shareInstance] hangup];
// 거절
[[TRTCCalling shareInstance] reject];

```

<span id="model.step6"> </span>

### 6단계: 다중 사용자 통화 구현

1. 발신자: 그룹 음성 통화 시 `TRTCCalling `의 `groupCall()` 함수를 호출하고 사용자 목록 (userIdList), 그룹 IM ID(groupId), 통화 유형(callType)에 전달해야 합니다. 그중, userIdList에는 반드시 매개변수를 입력해야 하며, groupId에서는 매개변수를 선택합니다. `callType` 전달 음성 유형 `CallType_Audio` 음성 유형 `CallType_Audio`를 전달하면 그룹 음성 통화를 요청할 수 있습니다.
2. 수신자: `onInvited()` 콜백으로 이 요청을 수락할 수 있습니다.
3. 수신자: 콜백을 수신한 후 `accept()`를 호출해 통화를 수락할 수 있으며, `reject()`로 통화를 거절할 수도 있습니다.
4. 일정 시간(기본30s) 초과 시에도 응답이 없을 경우 수신자는 `onCallingTimeOut()` 콜백을, 발신자는 `onNoResp(String userId)` 콜백을 받게 됩니다. 통화 발신자가 여러 요청의 응답을 받지 못할 경우에는`hangup()`, 수신자들은 `onCallingCancel()` 콜백을 받습니다.
5. 현재 다중 사용자 통화를 나가야 할 경우 `hangup()`을 호출할 수 있습니다.
6. 통화 도중 사용자가 추가되거나 나갈 경우 다른 사용자는 모두 `onUserEnter()` 혹은 `onUserLeave()` 콜백을 받습니다.

```Objective-C
// 앞부분 생략...
// 발신이 필요한 사용자 목록 취합
NSArray *callList = @[];
[callList addObject:@"b"];
[callList addObject:@"c"];
[callList addObject:@"d"];
// 한 IM 그룹에 발송하지 않은 경우, groupId는 비워둘 수 있습니다.
[[TRTCCalling shareInstance] groupCall:callList type:CallType_Video groupID:@""];
```

>?리스너 콜백, 예를 들어 `onReject`, `onCancel` 등 이벤트로 상응하는 UI 알림을 만들 수 있습니다.
><span id="offline"> </span>

### 7단계: 오프라인 통화 구현

>?서비스가 온라인 고객서비스 등 오프라인 수신 기능이 필요 없는 시나리오일 경우, 상술한 [1단계1](#model.step1) - [6단계](#model.step6) 연결을 완료하십시오. 하지만 서비스가 소셜 시나리오일 경우에는 오프라인 수신을 추천합니다.

IM SDK는 오프라인 푸시를 지원합니다. 상응하는 설정을 해야 사용 가능 표준에 도달할 수 있습니다.

1. Apple 푸시 인증서를 신청합니다. 자세한 방법은 [Apple 푸시 인증서 신청](https://intl.cloud.tencent.com/document/product/1047/34346)을 참조하십시오.
2. 백그라운드 및 클라이언트에 오프라인 푸시를 설정합니다.
3. login 함수의 `param.busiId`를 대응되는 ID로 수정합니다.

<span id="api"> </span>

## 모듈 API 리스트

TRTCCalling 모듈의 API 인터페이스 리스트는 다음과 같습니다.

| 인터페이스 함수        | 인터페이스 기능                                                 |
| --------------- | -------------------------------------------------------- |
| addDelegate     | TRTCCalling 프록시 콜백 설정, 사용자는 해당 콜백으로 상태 알림을 받을 수 있습니다. |
| login           | IM 로그인, 모든 기능은 먼저 로그인 한 후 사용할 수 있음                |
| logout          | IM 로그인, 로그인 후 다시 발신 작업을 할 수 없음                        |
| call            | C2C 통화 요청, 요청 수신자는 onInvited 콜백 수신            |
| groupCall       | IM 그룹 통화 요청, 요청 수신자는 onInvited 콜백 수신            |
| accept          | 초대된 사용자 통화 수신                                     |
| reject          | 초대된 사용자 통화 거절                                     |
| hangup          | 통화 종료                                                 |
| startRemoteView | 원격 사용자의 카메라 데이터를 지정한 UIView로 렌더링합니다.             |
| stopRemoteView  | 한 원격 사용자의 카메라 데이터 렌더링을 중지합니다.                         |
| openCamera      | 카메라를 활성화하고 지정 TXCloudVideoView에 렌더링합니다.           |
| closeCamera     | 카메라 끄기                                               |
| switchCamera    | 앞뒤 카메라 변경                                           |
| setMicMute      | mic 음소거 여부                                             |
| setHandsFree    | 핸즈프리 활성화 여부                                             |
