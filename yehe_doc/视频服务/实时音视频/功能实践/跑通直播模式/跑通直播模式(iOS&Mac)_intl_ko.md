## 적용 시나리오
TRTC는 4가지 입장 모드를 지원합니다. 영상 통화(VideoCall), 음성 통화(VoiceCall)는 [통화 모드](https://intl.cloud.tencent.com/document/product/647/35102)라고 부르고, 비디오 ILVB(Live)와 오디오 ILVB(VoiceChatRoom)는 라이브 방송 모드라고 부릅니다.
라이브 방송 모드의 TRTC는 단일 방에 최대 10만 명이 동시에 접속할 수 있으며 300ms 미만의 마이크 연결 딜레이 및 1000ms 미만의 시청 딜레이, 매끄러운 마이크 켜짐/꺼짐 등의 기능을 갖추고 있습니다. 저지연 ILVB, 10만 인터랙션 강의, 화상 소개팅, 온라인 교육, 원격 교육, 초대형 회의 등의 응용 시나리오에 적합합니다.

## 원리 분석
TRTC 클라우드 서비스는 '인터페이스 노드'와 '프록시 노드'라는 두 가지 서버 노드로 구성되어 있습니다.
- **인터페이스 노드**
최고 품질의 회로와 고성능 기기를 사용해 단말기 간의 저지연 마이크 연결 통화 처리에 적합하며, 시간당 단가가 비싼 편입니다.
- **프록시 노드**
일반 회로와 일반 성능 기기를 채택하여 동시 접속에 의한 풀 스트림 시청 수요 처리에 적합하며, 시간당 단가가 저렴한 편입니다.

라이브 방송 모드에서 TRTC는 역할의 개념을 도입했습니다. 사용자는 '호스트'와 '시청자' 역할로 나뉘고, '호스트'는 인터페이스 노드에, '시청자'는 프록시 노드에 할당됩니다. 하나의 방에 들어가는 시청자 수의 최댓값은 10만 명입니다.
'시청자'가 마이크를 켜려면 먼저 역할 전환(switchRole)을 통해 '호스트'가 되어야만 발언할 수 있습니다. 역할 전환의 과정에서 사용자는 프록시 노드에서 인터페이스 노드로 마이그레이션되며, TRTC 고유의 저 딜레이 시청 기술과 매끄러운 마이크 켜짐/꺼짐 전환 기술 덕분에 전체 전환 시간이 대폭 단축되었습니다.

![](https://main.qcloudimg.com/raw/e6a7492c3d0151252f7853373f6bcbbc.png)

## 예시 코드
[Github](https://github.com/tencentyun/TRTCSDK/tree/master/iOS/TRTC-API-Example-OC)에 로그인하여 본 문서와 관련된 예시 코드를 확인할 수 있습니다.
![](https://main.qcloudimg.com/raw/91ba84ef5cee887717ba69e97d939fcd.png)

>?Github 액세스 속도가 느리다면 [TXLiteAVSDK_TRTC_iOS_latest.zip](https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_TRTC_iOS_latest.zip)을 직접 다운로드할 수도 있습니다.


## 작업 단계
[](id:step1)
### 1단계: SDK 통합
아래의 방법 중에서 하나를 택해 **TRTC SDK**를 프로젝트에 통합할 수 있습니다.
#### 방법1: CocoaPods를 사용한 통합
1. **CocoaPods**를 설치합니다. 자세한 작업은 [CocoaPods 공식 홈페이지 설치 설명](https://guides.cocoapods.org/using/getting-started.html)을 참고하십시오.
2. 현재 프로젝트 디렉터리 하위의 `Podfile` 파일을 열고 아래의 내용을 추가합니다.
>?해당 디렉터리 하위에 `Podfile` 파일이 없을 경우, `pod init` 명령어로 먼저 파일을 새로 생성한 다음 아래의 내용을 추가합니다.
>
```
target 'Your Project' do
        pod ’TXLiteAVSDK_TRTC’
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
| Privacy - Camera Usage Description | 카메라 권한을 사용하는 이유를 설명합니다. 예를 들어, 카메라 액세스 권한이 필요한 경우 카메라 활성화 후 비디오 채팅을 해야만 화면이 나타나게 됩니다. |
| Privacy - Microphone Usage Description | 마이크 권한을 사용하는 이유를 설명합니다. 예를 들어, 마이크 액세스 권한이 필요한 경우 마이크 활성화 후 채팅을 해야만 소리가 나게 됩니다. |

[](id:step3)
### 3단계: SDK 인스턴스 초기화 및 이벤트 콜백 수신

1. [sharedInstance()](https://intl.cloud.tencent.com/document/product/647/35119) 인터페이스를 사용해 `TRTCCloud` 인스턴스를 생성합니다.
<dx-codeblock>
::: iOS object-c
// trtcCloud 인스턴스 생성
_trtcCloud = [TRTCCloud sharedInstance];
_trtcCloud.delegate = self;
:::
</dx-codeblock>
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
[enterRoom()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a96152963bf6ac4bc10f1b67155e04f8d) 인터페이스를 호출할 경우, 핵심 매개변수 [TRTCParams](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#interfaceTRTCParams)를 입력해야 합니다. 해당 매개변수가 포함하는 필수 입력 필드는 다음과 같습니다.

| 매개변수 이름 | 필드 유형 | 보충 설명 |입력 예시 |
|---------|---------|---------|---------|
| sdkAppId | 숫자 | 애플리케이션 ID, <a href="https://console.cloud.tencent.com/trtc/app">TRTC 콘솔</a>에서 SDKAppID를 확인할 수 있습니다.|1400000123 |
| userId | 문자열 | 영어 알파벳(a-z, A-Z), 숫자(0-9), 대시부호(-), 언더바(_)만 허용됩니다. | test_user_001 |
| userSig | 문자열 | userId를 기반으로 userSig를 계산할 수 있습니다. 계산 방법은 [UserSig 계산 방법](https://intl.cloud.tencent.com/document/product/647/35166)을 참고하십시오.| eJyrVareCeYrSy1SslI... |
| roomId | 숫자 | 숫자 유형의 방 번호입니다. 문자열 형식의 방 번호를 사용하려면 TRTCParams에서 strRoomId를 사용하십시오. | 29834 |

>! 
>- TRTC에서는 같은 userId 2개로 방에 동시 입장하면 서로 영향을 미칠 수 있으므로 이를 지원하지 않습니다.
>- 각 엔드는 appScene에서 통일되어야 합니다. 그렇지 않으면 예기치 않은 문제가 발생할 수 있습니다.


[](id:step5)
### 5단계: 호스트의 카메라 미리보기 및 마이크 음성 수집 활성화
1. 호스트는 [startLocalPreview()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a3fc1ae11b21944b2f354db258438100e)를 호출하여 로컬 카메라 미리보기를 활성화할 수 있습니다. SDK가 시스템에 카메라 사용 권한을 요청하게 됩니다.
2. 호스트는 [setLocalViewFillMode()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a961596f832657bfca81fd675878a2d15)를 호출하여 로컬 비디오 화면의 표시 모드를 설정할 수 있습니다.
 - Fill 모드는 '채우기'를 의미합니다. 화면은 같은 비율로 확대되거나 잘릴 수 있지만, 검은 부분은 없습니다.
 - Fit 모드는 '맞추기'를 의미합니다. 화면은 해당 콘텐츠가 다 표시되도록 같은 비율로 축소될 수 있고, 검은 부분이 있을 수 있습니다.
3. 호스트는 [setVideoEncoderParam()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a57938e5b62303d705da2ceecf119d74e) 인터페이스를 호출하여 로컬 비디오의 인코딩 매개변수를 설정할 수 있습니다. 해당 매개변수는 방에 있는 다른 사용자가 사용자의 화면을 시청할 때 느끼는 [화질](https://intl.cloud.tencent.com/document/product/647/35153)을 결정합니다.
4. 호스트는 [startLocalAudio()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a3177329bc84e94727a1be97563800beb)를 호출하여 마이크를 활성화합니다. SDK가 시스템에 마이크 사용 권한을 요청하게 됩니다.

<dx-codeblock>
::: iOS object-c
//예시 코드: 로컬 멀티미디어 스트림 배포
[self.trtcCloud startLocalPreview:_isFrontCamera view:self.view];

// 로컬 비디오 인코딩 매개변수 설정
TRTCVideoEncParam *encParams = [TRTCVideoEncParam new];
encParams.videoResolution = TRTCVideoResolution_640_360;
encParams.videoBitrate = 550;
encParams.videoFps = 15;
    
[self.trtcCloud setVideoEncoderParam:encParams];
:::
</dx-codeblock>

[](id:step6)
### 6단계: 호스트의 뷰티 필터 효과 설정

1. 호스트는 [getBeautyManager()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a4fb05ae6b5face276ace62558731280a)를 호출하여 뷰티 필터 설정 인터페이스[TXBeautyManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXBeautyManager__ios.html#interfaceTXBeautyManager)를 획득할 수 있습니다.
2. 호스트는 [setBeautyStyle()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXBeautyManager__ios.html#a8f2378a87c2e79fa3b978078e534ef4a)을 호출하여 뷰티 필터 스타일을 설정할 수 있습니다.
 - Smooth: 매끈하게. SNS 인플루언서 느낌의 뚜렷한 효과를 줍니다.
 - Nature: 내추럴. 피부 보정 알고리즘은 얼굴의 디테일을 더 많이 유지하여 자연스러운 느낌을 줍니다.
 - Pitu: [엔터프라이즈 버전](https://intl.cloud.tencent.com/document/product/647/34615#Enterprise)에서만 지원합니다.
3. 호스트는 [setBeautyLevel()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXBeautyManager__ios.html#af864d9466d5161e1926e47bae0e3f027)을 호출하여 피부 보정 레벨을 설정할 수 있습니다. 일반적으로 5로 설정합니다.
4. 호스트는 [setWhitenessLevel()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXBeautyManager__ios.html#a199b265f6013e0cca0ff99f731d60ff4)을 호출하여 미백 레벨을 설정할 수 있습니다. 일반적으로 5로 설정합니다.
5. iPhone 카메라의 색상 기본값은 노란 편이므로 [setFilter()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a1b0c2a9e82a408881281c7468a74f2c0)를 호출하여 호스트의 미백 특수 효과를 올리길 권장합니다. 미백 특수 효과가 매치되는 필터 파일의 다운로드 주소는 [필터 파일](https://liteav.sdk.qcloud.com/doc/res/trtc/filter/filterPNG.zip)입니다.



[](id:step7)
### 7단계: 호스트의 방 생성 및 푸시 스트리밍 시작
1. 호스트는 [TRTCParams](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#interfaceTRTCParams)에서 필드 `role`을 **`TRTCRoleType.anchor`**로 설정하여 현재 사용자의 역할이 호스트라는 것을 표시합니다.
2. 호스트는 [enterRoom()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a96152963bf6ac4bc10f1b67155e04f8d)을 호출하여 TRTCParams 매개변수 필드 `roomId`의 값이 방 번호인 멀티미디어 방을 생성하고 **`appScene`** 매개변수를 지정할 수 있습니다.
 - TRTCAppScene.LIVE: 비디오 ILVB 모드(이 문서에서 예시에 사용된 모드).
 - TRTCAppScene.voiceChatRoom: 오디오 ILVB 모드.
3. 방 생성에 성공하면 호스트는 멀티미디어 데이터의 인코딩과 전송 프로세스를 시작합니다. 이와 동시에, SDK는 [onEnterRoom(result)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a6960aca54e2eda0f424f4f915908a3c5) 이벤트를 콜백합니다. 매개변수 `result`가 0보다 크면 입장 성공이며, 해당 값은 입장에 걸리는 시간을 밀리초(ms) 단위로 나타냅니다. `result`가 0보다 작으면 입장 실패이며, 해당 값은 입장 실패의 에러 코드입니다.

<dx-codeblock>
::: iOS object-c
- (void)enterRoom() {
    TRTCParams *params = [TRTCParams new];
    params.sdkAppId = SDKAppID;
    params.roomId = _roomId;
    params.userId = _userId;
    params.role = TRTCRoleAnchor;
    params.userSig = [GenerateTestUserSig genTestUserSig:params.userId];
    [self.trtcCloud enterRoom:params appScene:TRTCAppSceneLIVE];
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

[](id:step8)
### 8단계: 시청자의 방 입장 후 라이브 방송 시청
1. 시청자는 [TRTCParams](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#interfaceTRTCParams)의 필드 `role`을 **`TRTCRoleType.audience`**로 설정하여 현재 사용자의 역할이 시청자라는 것을 표시합니다.
2. 시청자는 [enterRoom()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a96152963bf6ac4bc10f1b67155e04f8d)을 호출하여 TRTCParams 매개변수 중 `roomId`가 가리키는 멀티미디어 룸에 입장하고 **`appScene`** 매개변수를 지정할 수 있습니다.
 - TRTCAppScene.LIVE: 비디오 ILVB 모드(이 문서에서 예시에 사용된 모드).
 - TRTCAppScene.voiceChatRoom: 오디오 ILVB 모드.
3. 호스트 화면 시청:
 - 시청자가 사전에 호스트의 userId를 알고 있을 경우, 입장 성공 후 곧바로 호스트 `userId`를 사용해 [startRemoteView(userId, view: view)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#af85283710ba6071e9fd77cc485baed49)를 호출하여 호스트의 화면을 볼 수 있습니다.
 - 시청자는 입장 성공 후 [onUserVideoAvailable()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a533d6ea3982a922dd6c0f3d05af4ce80) 이벤트 공지를 받게 됩니다. 시청자가 사전에 호스트의 userId를 모를 경우, 콜백에서 확인한 호스트 `userId`를 사용해 [startRemoteView(userId, view: view)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#af85283710ba6071e9fd77cc485baed49)를 호출하여 호스트의 화면을 볼 수 있습니다.


[](id:step9)
### 9단계: 시청자와 호스트의 마이크 연결
1. 시청자는 [switch(TRTCRoleType.TRTCRoleAnchor)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a5f4598c59a9c1e66938be9bfbb51589c)를 호출하여 역할을 호스트(TRTCRoleType.TRTCRoleAnchor)로 전환합니다.
2. 시청자는 [startLocalPreview()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a3fc1ae11b21944b2f354db258438100e)를 호출하여 로컬 화면을 활성화할 수 있습니다.
3. 시청자는 [startLocalAudio()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a3177329bc84e94727a1be97563800beb)를 호출하여 마이크 음성 수집을 활성화합니다.

<dx-codeblock>
::: iOS object-c
//예시 코드: 시청자 마이크 켜짐
[self.trtcCloud switchRole:TRTCRoleAnchor];
[self.trtcCloud startLocalAudio:TRTCAudioQualityMusic];
[self.trtcCloud startLocalPreview:_isFrontCamera view:self.view];

//예시 코드: 시청자 마이크 꺼짐
[self.trtcCloud switchRole:TRTCRoleAudience];
[self.trtcCloud stopLocalAudio];
[self.trtcCloud stopLocalPreview];
:::
</dx-codeblock>

[](id:step10)
### 10단계: 호스트 간 크로스 룸 마이크 연결 PK

TRTC에서는 서로 다른 멀티미디어 룸의 두 호스트가 기존의 라이브 룸 시나리오에서 퇴장하지 않고도 '크로스 룸 통화' 기능을 통해 마이크를 연결하여 '크로스 룸 마이크 연결 PK'가 가능합니다.

1. 호스트 A는 [connectOtherRoom()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a062bc48550b479a6b7c1662836b8c4a5) 인터페이스를 호출합니다. 현재 인터페이스 매개변수는 JSON 포맷입니다. 호스트 B의 `roomId`와 `userId`를 {"roomId": "978","userId": "userB"}` 포맷으로 만든 매개변수를 인터페이스 함수에 전달해야 합니다.
2. 크로스 룸에 성공하면 호스트 A는 [onConnectOtherRoom()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a69e5b1d59857956f736c204fe765ea9a) 이벤트 콜백을 받게 됩니다. 이와 동시에 두 라이브 방송 방에 있는 모든 사용자는 [onUserVideoAvailable()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a533d6ea3982a922dd6c0f3d05af4ce80)과 [onUserAudioAvailable()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a8c885eeb269fc3d2e085a5711d4431d5) 이벤트 공지를 받게 됩니다.
 예를 들어, 방 '001'의 호스트 A는 `connectOtherRoom()`을 통해 방 '002'의 호스트 B와 크로스 룸 통화가 연결됩니다. 그 후, 방 '001'의 사용자는 호스트 B의 `onUserVideoAvailable(B, available: true)` 콜백과 `onUserAudioAvailable(B, available: true)` 콜백을 받게 됩니다. 방 '002'의 사용자는 호스트 A의 `onUserVideoAvailable(A, available: true)` 콜백과 `onUserAudioAvailable(A, available: true)` 콜백을 받게 됩니다.
3. 두 방의 사용자는 [startRemoteView(userId, view: view)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#af85283710ba6071e9fd77cc485baed49)를 호출하여 상대 방 호스트의 화면을 볼 수 있게 되고, 소리는 자동으로 재생됩니다.

<dx-codeblock>
::: iOS object-c
//예시 코드: 크로스 룸 마이크 연결 PK
NSMutableDictionary * jsonDict = [[NSMutableDictionary alloc] init];
[jsonDict setObject:@([_otherRoomIdTextField.text intValue]) forKey:@"roomId"];
[jsonDict setObject:_otherUserIdTextField.text forKey:@"userId"];
NSData* jsonData = [NSJSONSerialization dataWithJSONObject:jsonDict options:NSJSONWritingPrettyPrinted error:nil];
NSString* jsonString = [[NSString alloc] initWithData:jsonData encoding:NSUTF8StringEncoding];
[self.trtcCloud connectOtherRoom:jsonString];
:::
</dx-codeblock>

[](id:step11)
### 11단계: 현재 방 퇴장

[exitRoom()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a715f5b669ad1d7587ae19733d66954f3)을 호출하여 퇴장합니다. SDK는 퇴장 시 카메라, 마이크 등 하드웨어 디바이스를 비활성화 및 릴리스해야 합니다. 따라서 퇴장은 금방 완료되는 동작이 아니며, [onExitRoom()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a6a98fcaac43fa754cf9dd80454897bea) 콜백을 받아야만 퇴장이 완료되었다고 할 수 있습니다.

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

