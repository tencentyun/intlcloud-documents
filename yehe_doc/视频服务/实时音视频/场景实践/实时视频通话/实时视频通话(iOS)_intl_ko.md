## 효과
당사 App를 [다운로드](https://intl.cloud.tencent.com/document/product/647/35076) 및 설치하여 실시간 영상 통화의 효과를 경험할 수 있습니다.



빠른 영상 통화 기능이 필요한 경우, Tencent Cloud가 제공하는 App을 기반으로 설정을 적합하게 수정하거나 TUICalling 컴포넌트를 사용해 사용자 정의 UI 인터페이스를 구현할 수 있습니다.

>! 이전에는 TRTCVideoCall 컴포넌트가 제공되었으나, 구버전 컴포넌트는 [컴포넌트 라이브러리](https://github.com/tencentyun/LiteAVClassic)로 옮겨졌습니다. TUICalling 컴포넌트는 IM 신호 인터페이스를 사용하여 구버전 컴포넌트과 호환되지 않습니다.

[](id:ui)

## App UI 인터페이스 재사용

[](id:ui.step1)
### 1단계: 신규 애플리케이션 생성
1. TRTC 멀티미디어 콘솔에 로그인한 후, [개발 지원] > [Demo 빠른 실행](https://console.cloud.tencent.com/trtc/quickstart)을 선택합니다.
2. 애플리케이션 이름(예: `TestVideoCall`)을 입력한 후 [생성]을 클릭합니다.
3. [다운로드 완료, 다음 단계]를 클릭하여 이 단계를 건너뜁니다.

![](https://main.qcloudimg.com/raw/87dc814a675692e76145d76aab91b414.png)
>!본 기능은 기본 PaaS 서비스인 Tencent Cloud [Tencent Real-Time Communication](https://intl.cloud.tencent.com/document/product/647/35078)과 [Instant Messaging](https://intl.cloud.tencent.com/document/product/1047)을 동시에 사용하였으며, TRTC를 활성화하면 IM 서비스도 동시에 활성화됩니다. IM은 부가 서비스이며, 자세한 과금 규정은 [요금 안내](https://intl.cloud.tencent.com/document/product/1047/34350)를 참고하십시오.


[](id:ui.step2)
### 2단계: App 소스 코드 다운로드
[TUICalling](https://github.com/tencentyun/TUICalling)을 클릭하여 이동하거나, 소스 코드를 Clone 혹은 다운로드 합니다.

[](id:ui.step3)
### 3단계: App 프로그램 파일 설정
1. 설정 변경 페이지로 이동하여 다운로드한 소스 패키지에 따라 해당하는 개발 환경을 선택합니다.
2. `TUICalling/Debug/GenerateTestUserSig.swift` 파일을 찾아 엽니다.
3. `GenerateTestUserSig.swift` 파일에서 관련 매개변수를 설정합니다.
<ul style="margin:0"><li/>SDKAPPID: 0으로 기본 설정되어 있습니다. 실제 SDKAppID로 설정하십시오.
<li/>SECRETKEY: 공백으로 기본 설정되어 있습니다. 실제 키 정보로 설정하십시오.</ul>
![](https://main.qcloudimg.com/raw/87dc814a675692e76145d76aab91b414.png)
4. 붙여넣기 완료 후 [붙여넣기 완료, 다음 단계]를 클릭하면 생성이 완료됩니다.
5. 컴파일 완료 후 [콘솔 개요로 돌아가기]를 클릭합니다.

>!
>- 본 문서의 UserSig는 클라이언트 코드에서 SECRETKEY를 설정하여 생성합니다. 이 방법에서 SECRETKEY는 디컴파일로 크래킹되기 쉬우므로, 키가 유출되면 해커가 귀하의 Tencent Cloud 트래픽을 도용할 수 있습니다. 따라서 **해당 방법은 로컬 App 실행 및 기능 디버깅용으로 적합합니다**.
>- 정확한 UserSig 발급 방식은 다음과 같습니다. UserSig 계산 코드를 귀하의 서버에 통합하고 App 방향의 인터페이스를 제공합니다. UserSig가 필요할 때 귀하의 App이 비즈니스 서버로 동적 UserSig를 요청합니다. 자세한 내용은 [서버의 UserSig 생성](https://intl.cloud.tencent.com/document/product/647/35166)을 참고하십시오.

[](id:ui.step4)
### 4단계: App 실행

Xcode(11.0 및 이후 버전)를 사용하여 소스 코드 프로젝트 `TUICalling/TUICallingApp.xcworkspace`를 열고 [실행]을 클릭하면 App 디버깅이 시작됩니다.

[](id:ui.step5)
### 5단계: App 소스 코드 수정

소스 코드 폴더 `Source`에는 두 개의 하위 폴더 ui와 model이 포함되어 있으며, ui 폴더는 모두 인터페이스 코드입니다.

|              파일 및 폴더              | 기능 설명                                                 |
| ------------------------------------ | ------------------------------------------------------- |
|  TRTCCallingVideoViewController.swift  | 영상 통화의 메인 인터페이스입니다. 통화를 수신하거나 거부합니다. |
|  TRTCCallingAudioViewController.swift  | 음성 통화의 메인 인터페이스입니다. 통화를 수신하거나 거부합니다. |


## 애플리케이션 체험
>! 애플리케이션 체험 시 최소 2대의 디바이스가 필요합니다.

### 사용자 A
1. 다음과 같이 사용자 이름을 입력하고 로그인합니다. **사용자 이름의 고유성을 확보하십시오. 다른 사용자 이름과 중복되어서는 안 됩니다.**
2. 아래 이미지와 같이 전화를 걸 사용자 이름을 입력하고 [검색]을 클릭합니다.
3. [호출]을 클릭하고 [영상 통화]를 선택합니다. (**수신자가 애플리케이션에 남아 있는지 확인하십시오. 그렇지 않으면 통화에 실패할 수 있습니다**).


### 사용자 B
1. 다음과 같이 사용자 이름을 입력하고 로그인합니다. **사용자 이름의 고유성을 확보하십시오. 다른 사용자 이름과 중복되어서는 안 됩니다.**
2. 메인 페이지로 이동하여 전화 수신을 기다립니다.


[](id:model)
## 사용자 정의 UI 인터페이스 구현

[소스 코드](https://github.com/tencentyun/TUICalling) 폴더 `Source`에는 두 개의 하위 폴더 ui와 model이 있으며, model 폴더에는 Tencent Cloud가 구현한 재사용 가능 오픈 소스 컴포넌트 TRTCCalling이 포함되어 있습니다. `TRTCCalling.h` 파일에서 해당 컴포넌트가 제공하는 인터페이스 함수를 확인할 수 있습니다.
![](https://main.qcloudimg.com/raw/9b4087b68541912ce9e7a48955cd48e8.png)

오픈 소스 컴포넌트 TRTCCalling을 사용해 맞춤형 UI 인터페이스를 구현할 수 있습니다. 즉, model 부분만 재사용하여 UI 부분을 자체적으로 구현할 수 있습니다.

[](id:model.step1)
### 1단계: SDK 통합

통화 컴포넌트 TRTCCalling은 TRTC SDK와 IM SDK에 종속되어 있습니다. 아래 단계에 따라 두 가지 SDK를 프로젝트에 통합할 수 있습니다.

- **방법1: cocoapods 라이브러리를 통한 종속**
<dx-codeblock>
::: swift
 pod 'TXIMSDK_iOS'
 pod 'TXLiteAVSDK_TRTC' 
:::
</dx-codeblock>
>?두 SDK 제품의 최신 버전 번호는 [TRTC](https://github.com/tencentyun/TRTCSDK) 및 [IM](https://github.com/tencentyun/TIMSDK)의 Github 첫 페이지에서 획득할 수 있습니다.
- **방법2: 로컬을 통한 종속**
개발 환경에서 cocoapods 라이브러리 액세스가 느릴 경우, ZIP 패키지를 다운로드하고 통합 가이드 문서에 따라 수동으로 프로그램에 통합할 수 있습니다.
<table>
<tr>
<th>SDK</th>
<th>다운로드 페이지</th>
<th>통합 가이드</th>
</tr>
<tr>
<td>TRTC SDK</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34615">DOWNLOAD</a></td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/35092">통합 가이드 문서</a></td>
</tr>
<tr>
<td>IM SDK</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">DOWNLOAD</a></td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/34306">통합 가이드 문서</a></td>
</tr>
</table>

[](id:model.step2)
### 2단계: 권한 설정

info.plist 파일에 `Privacy - Camera Usage Description`, `Privacy - Microphone Usage Description`을 추가해 카메라 및 마이크 권한을 신청해야 합니다.

[](id:model.step3)
### 3단계: TUICalling 컴포넌트 가져오기
**cocoapods를 통해 컴포넌트 가져오기**. 구체적인 단계는 다음과 같습니다.
1. 프로젝트 디렉터리의 `Source`, `Resources`, `TXAppBasic` 폴더 및, `TUICalling.podspec` 파일을 각 프로그램 디렉터리로 복사합니다.
2. `Podfile` 파일에 다음 종속을 추가합니다. 그 다음 `pod install` 명령을 실행하여 가져오기를 완료합니다.
<dx-codeblock>
::: swift
 pod 'TXAppBasic', :path => "TXAppBasic/"
 pod 'TXLiteAVSDK_TRTC'
 pod 'TUICalling', :path => "./", :subspecs => ["TRTC"] 
:::
</dx-codeblock>

[](id:model.step4)
### 4단계: 컴포넌트 초기화 및 로그인

1. 푸시 관련 정보를 설정합니다.
<dx-codeblock>
::: swift
 [TRTCCalling shareInstance].imBusinessID = your business ID;
 [TRTCCalling shareInstance].deviceToken =  deviceToken;
:::
</dx-codeblock>
>? imBusinessID는 [IM 콘솔](https://console.cloud.tencent.com/im)에서 APNs 인증서를 업로드하고, AppDelegate를 통해 Apple 백그라운드에서 콜백을 요청한 후 해당 deviceToken 값을 반환하면 생성됩니다. 구체적인 작업은 [오프라인 푸시](https://intl.cloud.tencent.com/document/product/1047/34347)를 참고하시기 바랍니다.
2. `login(sdkAppID: UInt32, user: String, userSig: String, success: @escaping (() -> Void), failed: @escaping ((_ code: Int, _ message: String) -> Void))`를 호출해 컴포넌트에 로그인합니다. 주요 매개변수는 다음 테이블을 참고하십시오.
<table>
<tr><th>매개변수 이름</th><th>역할</th></tr>
<tr>
<td>sdkAppID</td>
<td><a href="https://console.cloud.tencent.com/trtc/app">TRTC 콘솔</a>에서 SDKAppID를 확인할 수 있습니다.</td>
</tr><tr>
<td>user</td>
<td>현재 사용자 ID이며, 문자열 유형은 영어 알파벳(a-z, A-Z), 숫자(0-9), 대시부호(-), 언더바(_)만 허용됩니다.</td>
</tr><tr>
<td>userSig</td>
<td> <a href="https://intl.cloud.tencent.com/document/product/647/35166">UserSig 계산 방법</a></td>
</tr></table>
<dx-codeblock>
::: Objective-C Objective-C
// 로그인
[[TRTCCalling shareInstance] login:SDKAPPID user:userID userSig:userSig success:^{
        NSLog(@"Video call login success.");
} failed:^(int code, NSString *error) {
        NSLog(@"Video call login failed.");
}];
:::
</dx-codeblock>


[](id:model.step5)
### 5단계: 1대1 통화

1. 발신자: `TRTCCalling`의 `call(userId, callType)`을 호출합니다. `userId`매개변수는 사용자 ID, `callType` 매개변수는 통화 유형입니다. 매개변수를 `CallType_Video`로 전달하면 영상 통화가 요청됩니다.
2. 수신자: 수신자가 로그인 상태인 경우 `onInvited()`라는 콜백을 받게 됩니다. 콜백의 `callType` 매개변수는 발신자가 작성한 통화 유형으로, 이 매개변수를 통해 해당하는 인터페이스를 실행할 수 있습니다. 수신자가 로그인 상태가 아니어도 통화 요청을 받게 하려면 [오프라인 수신](#offline)을 참고하십시오.
3. 수신자: 통화 수신을 원하는 경우 수신자는 `accept()` 함수를 호출할 수 있습니다. 영상 통화인 경우 동시에 `openCamera()` 함수를 호출하여 자신의 로컬 카메라를 활성화할 수 있습니다. 또한 `reject()`를 호출하여 통화를 거부할 수도 있습니다.
4. 멀티미디어 터널이 구축되면 양측은 `onUserVideoAvailable()`이라는 콜백을 받게 되며, 상대의 비디오 화면을 받았다는 의미입니다. 이때 양측의 사용자 모두 `startRemoteView()`를 호출하여 원격 비디오 화면을 볼 수 있습니다. 원격 음성의 기본값은 자동 재생입니다.

<dx-codeblock>
::: Objective-C Objective-C
// 1. 수신 콜백
[[TRTCCalling shareInstance] addDelegate:delegate];

//수신/거부
// 이때 B도 IM 시스템에 로그인하면 onInvited(A, null, false) 콜백을 받게 됩니다.
// TRTCCalling의 accept를 호출해 수신하거나 reject를 호출해 거부할 수 있습니다.
-(void)onInvited:(NSString *)sponsor
         userIds:(NSArray<NSString *> *)userIds
     isFromGroup:(BOOL)isFromGroup
        callType:(CallType)callType {
    [[TRTCCalling shareInstance] accept];
}

// 2. 상대 화면 시청
// A가 카메라를 활성화했기 때문에 B가 통화를 수신하면 onUserVideoAvailable(A, true) 콜백을 받게 됩니다.
- (void)onUserVideoAvailable:(NSString *)uid available:(BOOL)available {
  if (available) {
    UIView* renderView =[[UIView alloc] init];
    [[TRTCCalling shareInstance] startRemoteView:uid view:renderView]; // 즉시 상대의 화면을 볼 수 있습니다.
  } else {
    [[TRTCCalling shareInstance] stopRemoteView:uid]; // 화면 렌더링 중지
  }
}

// 3. 모듈의 다른 기능 함수를 호출해 통화 혹은 통화 끊기 요청
// 주의: 로그인을 해야만 정상적인 호출 가능
// 영상 통화 발신
[[TRTCCalling shareInstance] call:@"타깃 사용자" type:CallType_Video];
// 통화 종료
[[TRTCCalling shareInstance] hangup];
// 거부
[[TRTCCalling shareInstance] reject];
:::
</dx-codeblock>

[](id:model.step6)
### 6단계: 그룹 통화

1. 발신자: 그룹 영상/음성 통화 시 `TRTCCalling`의 `groupCall()` 함수를 호출하고 사용자 목록(userIdList), 그룹 IM ID(groupId), 통화 유형(callType)을 전달해야 합니다. userIdList는 필수 입력 매개변수이며, groupId는 옵션 매개변수입니다. `callType`은 화면 유형 `CallType_Video`입니다.
2. 수신자: `onInvited()`라는 이름의 콜백을 통해 호출 요청을 받을 수 있습니다. 여기서 매개변수 리스트는 발신자가 작성한 것으로, `callType`매개변수는 통화 유형이며 이 매개변수를 통해 해당하는 인터페이스를 실행할 수 있습니다.
3. 수신자: 콜백을 받은 후 `accept()`로 통화를 수신하거나 `reject()`로 거부할 수 있습니다.
4. 일정 시간(기본 30s)이 지나도 응답이 없으면 수신자는 `onCallingTimeOut()` 콜백을, 발신자는 `onNoResp()` 콜백을 받게 됩니다. 다중 수신자가 모두 응답이 없을 경우 발신자는 `hangup()` 콜백을, 모든 수신자는 `onCallingCancel()` 콜백을 받게 됩니다.
5. 그룹 통화를 중단해야 할 경우 `hangup()`을 호출할 수 있습니다.
6. 통화 도중 사용자가 추가되거나 나갈 경우, 다른 사용자는 모두 `onUserEnter()` 또는 `onUserLeave()` 콜백을 받게 됩니다.

>?인터페이스 `groupCall:type:groupID:`의 `groupID` 매개변수는 IM SDK 상의 그룹 ID로, 해당 매개변수를 입력할 경우 통화 요청 메시지 신호가 그룹 ID를 통해 전송됩니다. 해당 메시지 전송 방식은 간단하면서도 신뢰성이 높습니다. 입력하지 않는 경우 `TRTCCalling` 컴포넌트가 개별 발송 방식을 사용하여 일일이 공지합니다.

<dx-codeblock>
::: Objective-C Objective-C
// 앞부분 생략...
// 발신이 필요한 사용자 목록 취합
NSArray *callList = @[];
[callList addObject:@"b"];
[callList addObject:@"c"];
[callList addObject:@"d"];
// 한 IM 그룹에서 발송한 것이 아닌 경우, groupId는 비워둘 수 있습니다.
[[TRTCCalling shareInstance] groupCall:callList type:CallType_Video groupID:@""];

// 카메라 활성화
[[TRTCCalling shareInstance] openCamera:true view:renderView];
:::
</dx-codeblock>

[](id:offline)
### 7단계: 오프라인 수신

>?온라인 고객서비스 등 오프라인 수신 기능이 필요 없는 시나리오인 경우, [1단계](#model.step1)-[6단계](#model.step6)만 진행합니다. 소셜 시나리오에서는 오프라인 수신을 권장합니다.

IM SDK는 오프라인 푸시를 지원합니다. 사용 가능 기준을 충족하려면 해당하는 설정을 완료해야 합니다.

1. Apple 푸시 인증서를 신청합니다. 자세한 방법은 [Apple 푸시 인증서 신청](https://intl.cloud.tencent.com/document/product/1047/34346)을 참고하십시오.
2. 백그라운드 및 클라이언트에 오프라인 푸시를 설정합니다. 자세한 방법은 [오프라인 푸시(iOS)](https://intl.cloud.tencent.com/document/product/1047/34347)를 참고하십시오.
3. login 함수의 `param.busiId`를 해당하는 인증서 ID로 수정합니다.

[](id:api)

## 컴포넌트 API 리스트

TRTCCalling 컴포넌트의 API 인터페이스 리스트는 다음과 같습니다.

| 인터페이스 함수        | 인터페이스 기능                                                 |
| --------------- | -------------------------------------------------------- |
| addDelegate     | TRTCCalling 프록시 콜백을 설정합니다. 해당 콜백으로 상태 공지를 받을 수 있습니다. |
| login           | IM에 로그인합니다. 모든 기능은 먼저 로그인한 후 사용할 수 있습니다.                |
| logout          | IM에서 로그아웃합니다. 로그아웃 후에는 발신 기능을 사용할 수 없습니다.                        |
| call            | C2C 통화에 초대합니다. 초대 받은 사람은 onInvited 콜백을 받게 됩니다.            |
| groupCall       | IM 그룹 통화를 요청합니다. 요청 수신자는 onInvited 콜백을 받게 됩니다.            |
| accept          | 초대된 사용자 통화 수신                                     |
| reject          | 초대된 사용자 통화 거부                                     |
| hangup          | 통화 종료                                                 |
| startRemoteView | 원격 사용자의 카메라 데이터를 지정한 UIView로 렌더링합니다.             |
| stopRemoteView  | 특정 원격 사용자의 카메라 데이터 렌더링을 중지합니다.                         |
| openCamera      | 카메라를 활성화하고 지정한 TXCloudVideoView로 렌더링합니다.           |
| closeCamera     | 카메라 비활성화                                               |
| switchCamera    | 전면/후면 카메라 전환                                           |
| setMicMute      | mic 음소거 여부                                             |
| setHandsFree    | 핸즈프리 활성화 여부                                             |
