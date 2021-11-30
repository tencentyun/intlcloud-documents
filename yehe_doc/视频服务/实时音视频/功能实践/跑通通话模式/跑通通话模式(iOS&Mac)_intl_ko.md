## 적용 시나리오
TRTC는 4가지 입장 모드를 지원합니다. 그중 영상 통화(VideoCall)와 음성 통화(VoiceCall)는 통화 모드라고 부르고, 비디오 ILVB(Live)와 음성 ILVB(VoiceChatRoom)는 [라이브 방송 모드](https://intl.cloud.tencent.com/document/product/647/35107)라고 부릅니다.
통화 모드의 TRTC는 단일 방에 최대 300명이 동시에 접속할 수 있으며 최대 50명이 동시에 발언할 수 있습니다. 일대일 영상 통화, 300명 화상 회의, 온라인 진료, 원격 면접, 화상 고객서비스, 온라인 마피아 게임 등의 응용 시나리오에 적합합니다.

## 원리 분석
TRTC 클라우드 서비스는 '인터페이스 노드'와 '프록시 노드'라는 두 가지 서버 노드로 구성되어 있습니다.
-   **인터페이스 노드**
최고 품질의 회로와 고성능 기기를 사용해 단말기 간의 저지연 마이크 연결 통화 처리에 적합하며, 시간당 단가가 비싼 편입니다.
-   **프록시 노드**
일반 회로와 일반 성능 기기를 채택하여 동시 접속에 의한 풀 스트림 시청 수요 처리에 적합하며, 시간당 단가가 저렴한 편입니다.

통화 모드에서는 TRTC 방에 있는 모든 사용자가 인터페이스 노드에 할당되므로, 모두가 '호스트'인 셈입니다. 모든 사용자가 언제든지 발언(최고 업스트림 동시 접속 제한은 50회선)할 수 있어 온라인 회의와 같은 시나리오에 적합합니다. 단, 한 개 방의 인원은 300명으로 제한됩니다.
![](https://main.qcloudimg.com/raw/e6a7492c3d0151252f7853373f6bcbbc.png)

## 예시 코드
[Github](https://github.com/tencentyun/TRTCSDK/tree/master/iOS/TRTC-API-Example-OC)에 로그인하여 본문과 관련된 예시 코드를 확인할 수 있습니다.
![](https://main.qcloudimg.com/raw/468128bcaf078183eed097f7ee5f9c21.png)

>?Github 액세스 속도가 느리다면 [TXLiteAVSDK_TRTC_iOS_latest.zip](https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_TRTC_iOS_latest.zip)을 직접 다운로드할 수도 있습니다.

## 작업 단계
[](id:step1)
### 1단계: SDK 통합
아래의 방법 중에서 하나를 택해 **TRTC SDK**를 프로젝트에 통합할 수 있습니다.
#### 방법1: CocoaPods로 통합
1. [CocoaPods 공식 홈페이지 설치 가이드](https://guides.cocoapods.org/using/getting-started.html)를 참고해 **CocoaPods**를 설치합니다.
2. 현재 프로젝트의 루트 디렉터리에서 'Podfile' 파일을 연 뒤 다음 내용을 추가합니다.
>?해당 디렉터리 하위에 `Podfile` 파일이 없을 경우, `pod init` 명령어로 먼저 파일을 새로 생성한 다음 아래의 내용을 추가합니다.
>
```
target 'Your Project' do
        pod 'TXLiteAVSDK_TRTC'
end
```
3. 다음 명령어를 실행하여 **TRTC SDK**를 설치합니다.
```
pod install
```
설치에 성공하면 현재 프로젝트의 디렉터리 하위에 **xcworkspace** 파일이 하나 생성됩니다.
4. 새로 생성된 **xcworkspace** 파일을 엽니다.

#### 방법2: ZIP 패키지를 다운로드하여 수동으로 통합
현재 CocoaPods 환경 설치를 원하지 않거나, 설치되었지만 CocoaPods 라이브러리 액세스가 느릴 경우 [ZIP 압축 패키지](https://intl.cloud.tencent.com/document/product/647/34615)를 다운로드하고 [빠른 통합(iOS)](https://intl.cloud.tencent.com/document/product/647/35092)을 참고하여 SDK를 프로세스에 통합할 수 있습니다.

[](id:step2)
### 2단계: 미디어 디바이스 권한 추가
`Info.plist` 파일에 카메라 및 마이크 신청 권한을 추가합니다.

| Key | Value |
|---------|---------|
| Privacy - Camera Usage Description | 카메라 권한을 사용하는 이유를 설명합니다. 예를 들어, 카메라 액세스 권한이 필요한 경우 카메라 활성화 후 비디오 채팅을 해야만 화면이 나타나게 됩니다.|
| Privacy - Microphone Usage Description | 마이크 권한을 사용하는 이유를 설명합니다. 예를 들어, 마이크 액세스 권한이 필요한 경우 마이크 활성화 후 채팅을 해야만 소리가 나게 됩니다. |

[](id:step3)
### 3단계: SDK 인스턴스 초기화 및 이벤트 콜백 수신

1. [sharedInstance()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#ab6884975e069628328d05cf0e2c3dc67) 인터페이스를 사용하여 `TRTCCloud` 인스턴스를 생성합니다.
```
// trtcCloud 인스턴스 생성
_trtcCloud = [TRTCCloud sharedInstance];
_trtcCloud.delegate = self;
```
2. `delegate` 속성을 설정하고 이벤트 콜백을 등록한 다음, 관련 이벤트와 오류 공지를 리슨합니다.
<dx-codeblock>
::: iOS object-c
// 오류 공지를 수신하여 사용자에게 공지해야 함
- (void)onError:(TXLiteAVError)errCode errMsg:(NSString *)errMsg extInfo:(NSDictionary *)extInfo {
    if (ERR_ROOM_ENTER_FAIL == errCode) {
        [self toastTip:@"방 입장 실패"];
        [self.trtcCloud exitRoom];
    }
}
:::
</dx-codeblock>

[](id:step4)
### 4단계: 입장 매개변수 TRTCParams 어셈블리
[enterRoom()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a96152963bf6ac4bc10f1b67155e04f8d) 인터페이스 호출 시 핵심 매개변수 [TRTCParams](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#interfaceTRTCParams)를 입력해야 합니다. 해당 매개변수에 포함되어 있는 필수 입력 필드는 다음과 같습니다.

| 매개변수 이름 | 필드 유형 | 보충 설명 |입력 예시 |
|---------|---------|---------|---------|
| sdkAppId | 숫자 | 애플리케이션 ID, <a href="https://console.cloud.tencent.com/trtc/app">TRTC 콘솔</a>에서 SDKAppID를 확인할 수 있습니다.|1400000123 |
| userId | 문자열 | 영어 알파벳(a-z, A-Z), 숫자(0-9), 대시부호(-), 언더바(_)만 허용됩니다. | test_user_001 |
| userSig | 문자열 | userId를 기반으로 userSig를 계산할 수 있습니다. 계산 방법은 [UserSig 계산 방법](https://intl.cloud.tencent.com/document/product/647/35166)을 참고하십시오. | eJyrVareCeYrSy1SslI... |
| roomId | 숫자 | 숫자 유형의 방 번호입니다. 문자열 형식의 방 번호를 사용하려면 TRTCParams의 strRoomId를 사용하십시오. | 29834 |

>! TRTC에서는 상호 간섭이 일어나는 상황을 방지하기 위해 같은 userId 2개의 동시 입장을 지원하지 않습니다.

[](id:step5)
### 5단계: 방 생성 및 입장
1. [enterRoom()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a96152963bf6ac4bc10f1b67155e04f8d)을 호출하여 TRTCParams 매개변수 'roomId'가 지정한 멀티미디어 방에 들어갈 수 있습니다. 해당 방이 존재하지 않는 경우 SDK는 필드 'roomId'를 방 번호로 하는 신규 방을 자동 생성합니다.
2. 응용 시나리오에 따라 적합한 **'appScene'** 매개변수를 설정하십시오. 잘못된 매개변수를 사용하는 경우 랙이 발생하거나 화면 해상도가 떨어질 수 있습니다.
 - 영상 통화는 'TRTCAppScene.videoCall'로 설정하십시오.
 - 음성 통화는 'TRTCAppScene.audioCall'로 설정하십시오.
3. 방에 입장하면 SDK는 'onEnterRoom(result)' 이벤트를 콜백합니다. 매개변수 'result'가 0보다 크면 방 입장 성공을 뜻하며, 세부 값은 방 입장 소요 시간으로, 단위는 밀리세컨드(ms)입니다. 'result'가 0보다 작으면 방 입장 실패를 뜻하며, 세부 값은 방 입장 실패 에러 코드입니다.

<dx-codeblock>
::: iOS object-c
- (void)enterRoom() {
    TRTCParams *params = [TRTCParams new];
    params.sdkAppId = SDKAppID;
    params.roomId = _roomId;
    params.userId = _userId;
    params.role = TRTCRoleAnchor;
    params.userSig = [GenerateTestUserSig genTestUserSig:params.userId];
    [self.trtcCloud enterRoom:params appScene:TRTCAppSceneVideoCall];
}

- (void)onEnterRoom:(NSInteger)result {
    if (result > 0) {
        [self toastTip:@"방 입장 성공"];
    } else {
        [self toastTip:@"방 입장 실패"];
    }
}
:::
</dx-codeblock>

>! 
>- 방 입장에 실패하면 SDK는 동시에 'onError' 이벤트를 콜백하며, 'errCode'([에러 코드](https://intl.cloud.tencent.com/document/product/647/35124)), 'errMsg'(에러 원인), 'extraInfo'(보관 매개변수)를 반환합니다.
>- 이미 방에 입장한 경우 `exitRoom()`을 호출하여 해당 방에서 퇴장해야만 다른 방에 들어갈 수 있습니다.
>- 각 엔드는 appScene에서 통일되어야 합니다. 그렇지 않으면 예기치 않은 문제가 발생할 수 있습니다.

[](id:step6)
### 6단계: 원격 멀티미디어 스트림 구독
SDK는 자동 구독 및 수동 구독 기능을 지원합니다.

#### 자동 구독 모드(기본값)
자동 구독 모드에서 특정 방에 입장하면 SDK가 방에 입장한 다른 사용자의 오디오 스트림을 자동 수신하여 '바로 재생' 수준으로 재생합니다.
1. 같은 방에 입장한 사용자가 오디오 데이터를 업스트림하면 [onUserAudioAvailable()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a8c885eeb269fc3d2e085a5711d4431d5) 이벤트가 공지되고, SDK는 원격 사용자의 음성을 자동 재생합니다.
2. [muteRemoteAudio(userId, mute: true)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#afede3cc79a8d68994857b410fb5572d2)를 이용하여 특정 userId의 오디오 데이터를 차단할 수 있으며, [muteAllRemoteAudio(true)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a75148bf8a322c852965fe774cbc7dd14)를 통해 모든 원격 사용자의 오디오 데이터를 차단할 수 있습니다. 차단이 완료되면 SDK는 차단 대상 사용자의 오디오 데이터를 불러오지 않습니다.
3. 같은 방에 입장한 사용자가 비디오 데이터를 업스트림하면 (https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a533d6ea3982a922dd6c0f3d05af4ce80) 이벤트가 수신됩니다. 단, 이 때 SDK는 비디오 데이터 명령어 처리 방법을 수신하지 못해 비디오 데이터를 자동 처리하지 않습니다. [startRemoteView(userId, view: view)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#af85283710ba6071e9fd77cc485baed49)를 호출하여 원격 사용자의 비디오 데이터와 `view` 표시를 연결합니다.
4. [setRemoteViewFillMode()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#afda6658d1bf7dc9bc1445838b95d21ff)를 통해 비디오 화면의 표시 모드를 지정합니다.
 - Fill 모드: 확대 화면을 뜻하며, 검은 여백 없이 화면을 일정 비율로 확대 및 편집할 수 있습니다.
 - Fit 모드: 축소 화면을 뜻하며, 일정 비율로 화면을 축소할 수 있습니다. 콘텐츠가 전부 표시되지만 검은 여백도 발생합니다.
5. [stopRemoteView(userId)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a2b7e96e4b527798507ff743c61a6a066)를 이용하여 특정 userId의 비디오 데이터를 차단할 수 있으며, [stopAllRemoteView()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#aaa75cd1b98c226bb7b8a19412b204d2b)를 통해 모든 원격 사용자의 비디오 데이터를 차단할 수 있습니다. 차단이 완료되면 SDK는 차단 대상 원격 사용자의 비디오 데이터를 불러오지 않습니다.

<dx-codeblock>
::: iOS object-c
// 인스턴스 코드: 구독 통지(또는 구독 취소)한 원격 사용자의 비디오 화면
- (void)onUserVideoAvailable:(NSString *)userId available:(BOOL)available {
    UIView* remoteView = remoteViewDic[userId];
    if (available)  {
        [_trtcCloud startRemoteView:userId streamType:TRTCVideoStreamTypeSmall view:remoteView];
    } else {
        [_trtcCloud stopRemoteView:userId streamType:TRTCVideoStreamTypeSmall];
    }
}
:::
</dx-codeblock>

>? 'onUserVideoAvailable()' 이벤트 콜백이 발생한 뒤 즉시 'startRemoteView()'를 호출하여 비디오 스트림을 구독하지 않으면 SDK는 5초 이내에 원격 비디오 데이터의 수신을 중지합니다.

#### 수동 구독 모드
[setDefaultStreamRecvMode()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#ada2e2155e0e7c3001c6bb6dca1d93048) 인터페이스를 이용해 SDK를 수동 구독 모드로 설정할 수 있습니다. 수동 구독 모드에서 SDK는 같은 방에 입장한 사용자의 멀티미디어 데이터를 자동 수신하지 않습니다. API 함수를 이용해 직접 트리거해야 합니다.

1. **방 입장 이전에** [setDefaultStreamRecvMode(false, video: false)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#ada2e2155e0e7c3001c6bb6dca1d93048) 인터페이스를 호출하면 SDK가 수동 구독 모드로 설정됩니다.
2. 같은 방에 입장한 사용자가 오디오 데이터를 업스트림하면 [onUserAudioAvailable()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a8c885eeb269fc3d2e085a5711d4431d5) 이벤트가 수신됩니다. 이때 [muteRemoteAudio(userId, mute: false)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#afede3cc79a8d68994857b410fb5572d2)를 호출하여 해당 사용자의 오디오 데이터를 수동 구독해야 SDK가 해당 사용자의 오디오 데이터를 수신한 뒤 디코딩하여 재생합니다.
3. 같은 방에 입장한 사용자가 비디오 데이터를 업스트림하면 [onUserVideoAvailable()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a533d6ea3982a922dd6c0f3d05af4ce80) 이벤트가 수신됩니다. 이 때 [startRemoteView(userId, view: view)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#af85283710ba6071e9fd77cc485baed49)를 호출하여 해당 사용자의 비디오 데이터를 수동 구독해야 SDK가 해당 사용자의 비디오 데이터를 수신한 뒤 디코딩하여 재생합니다.

[](id:step7)
### 7단계: 로컬의 멀티미디어 스트림 배포
1. [startLocalAudio()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a3177329bc84e94727a1be97563800beb)를 호출하여 마이크 수집을 활성화하고 수집된 오디오를 인코딩 및 발송합니다.
2. [startLocalPreview()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a3fc1ae11b21944b2f354db258438100e)를 호출하면 로컬 카메라가 실행되고, 수집한 화면을 인코딩한 뒤 송신할 수 있습니다.
3. [setLocalViewFillMode()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a961596f832657bfca81fd675878a2d15)를 호출하면 로컬 비디오 화면의 표시 모드를 설정할 수 있습니다.
 - Fill 모드는 '채우기'를 의미합니다. 화면은 같은 비율로 확대되거나 잘릴 수 있지만, 검은 부분은 없습니다.
 - Fit 모드는 '맞추기'를 의미합니다. 화면은 해당 콘텐츠가 다 표시되도록 같은 비율로 축소될 수 있고, 검은 부분이 있을 수 있습니다.
4. [setVideoEncoderParam()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a57938e5b62303d705da2ceecf119d74e) 인터페이스를 호출하면 로컬 비디오의 코드 매개변수를 설정할 수 있습니다. 해당 매개변수는 같은 방 사용자가 시청하는 화면의 [화질](https://intl.cloud.tencent.com/document/product/647/35153)을 결정합니다.

<dx-codeblock>
::: iOS object-c
//예시 코드: 로컬 멀티미디어 스트림 배포
[self.trtcCloud startLocalPreview:_isFrontCamera view:self.view];
[self.trtcCloud startLocalAudio:TRTCAudioQualityMusic];
:::
</dx-codeblock>

>! Mac 버전의 SDK는 카메라와 마이크의 기본값이 설정되어 있습니다. [setCurrentCameraDevice()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#aae9955bb39985586f7faba841d2692fc)와 [setCurrentMicDevice()](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a5141fec83e7f071e913bfc539c193ac6)를 통해 카메라와 마이크 설정을 변경할 수 있습니다.

[](id:step8)
### 8단계: 현재 방에서 퇴장하기

[exitRoom()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a715f5b669ad1d7587ae19733d66954f3)을 호출하여 퇴장합니다. 퇴장 시 SDK에서 카메라, 마이크 등 하드웨어 기기를 비활성화 및 릴리스해야 합니다. 따라서 퇴장은 금방 완료되지 않으며, [onExitRoom()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a6a98fcaac43fa754cf9dd80454897bea) 콜백을 수신해야 완료됩니다.

<dx-codeblock>
::: iOS object-c
// 퇴장 호출 후 onExitRoom 이벤트 콜백 대기
[self.trtcCloud exitRoom];

- (void)onExitRoom:(NSInteger)reason {
    NSLog(@"방 퇴장: reason: %ld", reason)
}
:::
</dx-codeblock>

>! 애플리케이션에서 여러 개의 멀티미디어 SDK가 동시에 통합되었을 경우, `onExitRoom` 콜백을 받은 후 다른 멀티미디어 SDK를 재실행하십시오. 그렇지 않으면 하드웨어 점유율 문제가 나타날 수 있습니다.
