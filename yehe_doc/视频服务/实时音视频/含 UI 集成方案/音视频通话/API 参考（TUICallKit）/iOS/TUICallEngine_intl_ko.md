## TUICallEngine API

TUICallEngine은 **UI 요소를 포함하지 않는** 오디오/비디오 통화 컴포넌트입니다. TUICallKit이 요구 사항을 충족하지 않는 경우 TUICallEngine의 API를 사용하여 프로젝트를 사용자 정의할 수 있습니다.

## API 개요

| API                                                          | 설명                                                        |
| ------------------------------------------------------------ | ----------------------------------------------------------- |
| [createInstance](#createinstance) | TUICallEngine 인스턴스 생성(싱글톤 모드)                         |
| [destroyInstance](#destroyinstance) | TUICallEngine 인스턴스 종료(싱글톤 모드)                         |
| [init](#init) | 기본 음성/영상 통화 기능을 인증함                                |
| [addObserver](#addobserver) | 이벤트 리스너 등록                                                |
| [removeObserver](#removeobserver) | 이벤트 리스너 등록 취소                                                |
| [call](#call) | 1v1 통화 걸기                                               |
| [groupCall](#groupcall) | 그룹 통화 걸기                                                |
| [accept](#accept) | 통화 수락                                                    |
| [reject](#reject) | 통화 거절                                                    |
| [hangup](#hangup) | 통화 종료                                                    |
| [ignore](#ignore) | 통화 무시                                                    |
| [inviteUser](#inviteuser) | 현재 그룹 통화에 사용자 초대                                |
| [joinInGroupCall](#joiningroupcall) | 그룹 통화에 참여                                    |
| [switchCallMediaType](#switchcallmediatype) | 통화 유형 변경. 예를 들어, 화상 통화에서 음성 통화로 전환.                    |
| [startRemoteView](#startremoteview) | 원격 사용자의 비디오 스트림 구독                                      |
| [stopRemoteView](#stopremoteview) | 원격 사용자의 비디오 스트림 구독 취소                                      |
| [openCamera](#opencamera) | 카메라 켜기                                                  |
| [closeCamera](#closecamera) | 카메라 끄기                                                  |
| [switchCamera](#switchcamera) | 전면 및 후면 카메라 전환                                              |
| [openMicrophone](#openmicrophone) | 마이크 켜기                                                  |
| [closeMicrophone](#closemicrophone) | 마이크 끄기                                                  |
| [selectAudioPlaybackDevice](#selectaudioplaybackdevice) | 오디오 재생 장치(핸드셋 또는 스피커) 선택                             |
| [setSelfInfo](#setselfinfo) | 대화명 및 프로필 사진 설정                                        |
| [enableMultiDeviceAbility](#enablemultideviceability) | TUICallEngine에 대한 다중 장치 로그인 활성화 여부 설정(프리미엄 패키지에서 지원) |

## API 세부 정보

### createInstance

이 API는 TUICallEngine 싱글톤을 생성하는 데 사용됩니다.

```objectivec
- (TUICallEngine *)createInstance;
```

### destroyInstance

이 API는 TUICallEngine 싱글톤을 종료하는 데 사용됩니다.

```objectivec
- (void)destroyInstance;
```

### init

이 API는 TUICallEngine을 초기화하는 데 사용됩니다. 다른 API를 호출하기 전에 통화 서비스를 인증하고 다른 필수 작업을 수행하기 위해 호출합니다.

```objectivec
- (void)init:(NSString *)sdkAppID userId:(NSString *)userId userSig:(NSString *)userSig succ:(TUICallSucc)succ fail:(TUICallFail)fail;
```

매개변수는 다음과 같습니다.

| 매개변수     | 유형               | 의미                                                         |
| -------- | ------------------ | ------------------------------------------------------------ |
| sdkAppID | int                | **TRTC 콘솔** > [**애플리케이션 관리**](https://console.tencentcloud.com/trtc/app) > **애플리케이션 정보**에서 SDKAppID 확인 |
| userId   | String         | 현재 사용자의 ID, 문자열 유형은 영어 알파벳(a-z, A-Z), 숫자(0-9), 하이픈(-), 언더바(_)만 허용 |
| userSig  | String             | Tencent Cloud의 독점 보안 서명. 계산 및 사용 방법은 [UserSig](https://www.tencentcloud.com/document/product/647/35166) 참고 |
| callback | TUIDefine.Callback | 초기화 콜백. `onSuccess`는 초기화가 성공했음을 표시                        |

### addObserver

이 API는 'TUICallObserver' 이벤트를 수신할 이벤트 리스너를 등록하는 데 사용됩니다.

```objectivec
- (void)addObserver:(id<TUICallObserver>)observer;
```

### removeObserver

이 API는 이벤트 리스너를 등록 해제하는 데 사용됩니다.

```objectivec
- (void)removeObserver:(id<TUICallObserver>)observer;
```

### call

이 API는 (1v1) 통화를 수행하는 데 사용됩니다.

```objectivec
- (void)call:(TUIRoomId *)roomId userId:(NSString *)userId callMediaType:(TUICallMediaType)callMediaType params:(TUICallParams *)params succ:(TUICallSucc)succ fail:(TUICallFail)fail
```

매개변수는 다음과 같습니다.

| 매개변수          | 유형             | 의미                                                         |
| ------------- | ---------------- | ------------------------------------------------------------ |
| roomId        | TUIRoomId        | 방 ID. 현재는 숫자로 된 방 ID만 사용할 수 있으며, 문자열 형식의 방 ID는 향후 지원될 예정임 |
| userId        | NSString         | 대상 userId                                            |
| callMediaType | TUICallMediaType | 비디오 또는 오디오일 수 있는 통화 유형                       |
| params        | TUICallParams    | 추가 매개변수. 예를 들어 오프라인 알림을 사용자 정의하는 데 사용할 수 있음                   |

### groupCall

이 API는 그룹 통화를 하는 데 사용됩니다. 그룹 통화를 하기 전에 IM 그룹을 생성해야 합니다.

```objectivec
- (void)groupCall:(TUIRoomId *)roomId groupId:(NSString *)groupId userIdList:(NSArray <NSString *> *)userIdList callMediaType:(TUICallMediaType)callMediaType params:(TUICallParams *)params succ:(TUICallSucc)succ fail:(TUICallFail)fail
```

| 매개변수          | 유형             | 의미                                                         |
| ------------- | ---------------- | ------------------------------------------------------------ |
| roomId        | TUIRoomId        | 방 ID. 현재는 숫자로 된 방 ID만 사용할 수 있으며, 문자열 형식의 방 ID는 향후 지원될 예정임 |
| groupId       | NSString         | 그룹 ID                                          |
| userIdList    | NSArray          | 대상 userId                                       |
| callMediaType | TUICallMediaType | 비디오 또는 오디오일 수 있는 통화 유형                       |
| params        | TUICallParams    | 추가 매개변수. 예를 들어 오프라인 알림을 사용자 지정하는 데 사용할 수 있음                   |

### accept

이 API는 통화를 수락하는 데 사용됩니다. 'onCallReceived()' 콜백을 수신한 후 이 API를 호출하여 통화를 수락할 수 있습니다.

```objectivec
- (void)accept:(TUICallSucc)succ fail:(TUICallFail)fail;
```

### reject

이 API는 통화를 거절하는 데 사용됩니다. 'onCallReceived()' 콜백을 수신한 후 이 API를 호출하여 통화를 거절할 수 있습니다.

```objectivec
- (void)reject:(TUICallSucc)succ fail:(TUICallFail)fail;
```

### ignore

이 API는 통화를 무시하는 데 사용됩니다. 'onCallReceived()'를 수신한 후 이 API를 호출하여 통화를 무시할 수 있습니다. 호출자는 'onUserLineBusy' 콜백을 수신합니다. 프로젝트에 라이브 스트리밍 또는 회의가 포함된 경우 이 API를 사용하여 ‘회의 중’ 또는 ‘방송 중’ 기능을 구현할 수도 있습니다.

```objectivec
- (void)ignore:(TUICallSucc)succ fail:(TUICallFail)fail;
```

### hangup

이 API는 통화를 종료하는 데 사용됩니다.

```objectivec
- (void)hangup:(TUICallSucc)succ fail:(TUICallFail)fail;
```

### inviteUser

이 API는 그룹 통화 참가자가 사용자를 통화에 초대하는 데 사용합니다.

```objectivec
- (void)inviteUser:(NSArray<NSString *> *)userIdList params:(TUICallParams *)params succ:(void(^)(NSArray <NSString *> *userIdList))succ fail:(TUICallFail)fail
```

| 매개변수       | 유형          | 의미                                       |
| ---------- | ------------- | ------------------------------------------ |
| userIdList | NSArray       | 대상 userId                     |
| params     | TUICallParams | 추가 매개변수. 예를 들어 오프라인 알림을 사용자 지정하는 데 사용할 수 있음. |

### joinInGroupCall

이 API는 그룹 구성원이 그룹 통화에 참여하는 데 사용됩니다.

```objectivec
- (void)joinInGroupCall:(TUIRoomId *)roomId groupId:(NSString *)groupId callMediaType:(TUICallMediaType)callMediaType succ:(TUICallSucc)succ fail:(TUICallFail)fail;
```

| 매개변수          | 유형             | 의미                                                         |
| ------------- | ---------------- | ------------------------------------------------------------ |
| roomId        | TUIRoomId        | 방 ID. 현재는 숫자로 된 방 ID만 사용할 수 있으며, 문자열 형식의 방 ID는 향후 지원될 예정임 |
| groupId       | NSString         | 그룹 ID                                          |
| callMediaType | TUICallMediaType | 비디오 또는 오디오일 수 있는 통화 유형                       |

### switchCallMediaType

이 API는 그룹 구성원이 그룹 통화에 참여하는 데 사용합니다.

```objectivec
- (void)switchCallMediaType:(TUICallMediaType)newType;
```

| 매개변수          | 유형             | 의미                                   |
| ------------- | ---------------- | -------------------------------------- |
| callMediaType | TUICallMediaType | 비디오 또는 오디오일 수 있는 통화 유형 |

### startRemoteView

이 API는 원격 비디오를 표시하도록 View 객체를 설정하는 데 사용됩니다.

```objectivec
- (void)startRemoteView:(NSString *)userId videoView:(TUIVideoView *)videoView onPlaying:(void(^)(NSString *userId))onPlaying onLoading:(void(^)(NSString *userId))onLoading onError:(void(^)(NSString *userId, int code, NSString *errMsg))onError;
```

| 매개변수      | 유형         | 의미              |
| --------- | ------------ | ----------------- |
| userId    | NSString     | 대상 userId |
| videoView | TUIVideoView | 렌더링할 뷰      |

### stopRemoteview

이 API는 원격 사용자의 비디오 스트림 구독을 취소하는 데 사용됩니다.

```objectivec
- (void)stopRemoteView:(NSString *)userId;
```

| 매개변수   | 유형     | 의미              |
| ------ | -------- | ----------------- |
| userId | NSString | 대상 userId |

### openCamera

카메라 활성화

```objectivec
- (void)openCamera:(TUICallCamera)camera videoView:(TUIVideoView *)videoView succ:(TUICallSucc)succ fail:(TUICallFail)fail;
```

| 매개변수      | 유형          | 의미             |
| --------- | ------------- | ---------------- |
| camera    | TUICallCamera | 전면 또는 후면 카메라 사용 여부 |
| videoView | TUIVideoView  | 렌더링할 뷰     |

### closeCamera

이 API는 카메라를 끄는 데 사용됩니다.

```objectivec
- (void)closeCamera;
```

### switchCamera

이 API는 전면 및 후면 카메라 간에 전환하는 데 사용됩니다.

```objectivec
- (void)switchCamera:(TUICallCamera)camera;
```

| 매개변수   |  유형          | 의미             |
| ------ | ------------- | ---------------- |
| camera | TUICallCamera | 전면 또는 후면 카메라 사용 여부 |

### openMicrophone

이 API는 마이크를 켜는 데 사용됩니다.

```objectivec
- (void)openMicrophone:(TUICallSucc)succ fail:(TUICallFail)fail;
```

### closeMicrophone

이 API는 마이크를 끄는 데 사용됩니다.

```objectivec
- (void)closeMicrophone;
```

### selectAudioPlaybackDevice

이 API는 오디오 재생 장치(리시버 또는 스피커)를 선택하는 데 사용됩니다. 통화 시나리오에서 이 API를 사용하여 핸즈프리 모드를 켜고 끌 수 있습니다.

```objectivec
- (void)selectAudioPlaybackDevice:(TUIAudioPlaybackDevice)device;
```

| 매개변수   |  유형                   | 의미        |
| ------ | ---------------------- | ----------- |
| device | TUIAudioPlaybackDevice | 스피커 또는 핸드셋 |

### setSelfInfo

이 API는 대화명과 프로필 사진을 설정하는 데 사용됩니다. 대화명은 500바이트를 초과할 수 없으며 프로필 사진은 URL로 지정됩니다.

```objectivec
- (void)setSelfInfo:(NSString * _Nullable)nickName avatar:(NSString * _Nullable)avatar succ:(TUICallSucc)succ fail:(TUICallFail)fail;
```

### enableMultiDeviceAbility

이 API는 `TUICallEngine`에 대한 다중 장치 로그인 활성화 여부를 설정하는 데 사용됩니다(프리미엄 패키지에서 지원).

```objectivec
- (void)enableMultiDeviceAbility:(BOOL)enable succ:(TUICallSucc)succ fail:(TUICallFail)fail;
```