## TUICallObserver API

TUICallObserver는 TUICallEngine의 콜백 클래스입니다. 이벤트를 수신하는 데 사용할 수 있습니다.

## 개요

| API                                                          | 설명                       |
| ------------------------------------------------------------ | -------------------------- |
| [onError](#onerror) | 통화 중 오류 발생         |
| [onCallReceived](#oncallreceived) | 통화 초대를 받음             |
| [onCallCancelled](#oncallcancelled) | 통화가 취소됨             |
| [onCallBegin](#oncallbegin) | 통화가 연결됨             |
| [onCallEnd](#oncallend) | 통화가 종료됨             |
| [onCallMediaTypeChanged](#oncallmediatypechanged) | 통화 유형이 변경됨 |
| [onUserReject](#onuserreject) | xxxx 사용자가 통화를 거절함    |
| [onUserNoResponse](#onusernoresponse) | xxxx 사용자가 응답하지 않음      |
| [onUserLineBusy](#onuserlinebusy) | xxxx 사용자가 통화 중임        |
| [onUserJoin](#onuserjoin) | xxxx 사용자가 통화에 참여함    |
| [onUserLeave](#onuserleave) | xxxx 사용자가 통화를 종료함    |
| [onUserVideoAvailable](#onuservideoavailable) | xxx 사용자가 비디오 스트림이 있는지 여부 |
| [onUserAudioAvailable](#onuseraudioavailable) | xxx 사용자에게 오디오 스트림이 있는지 여부 |
| [onUserVoiceVolumeChanged](#onuservoicevolumechanged) | 모든 사용자의 볼륨 수준 |
| [onUserNetworkQualityChanged](#onusernetworkqualitychanged) | 모든 사용자의 네트워크 품질 |

## 세부 정보

### onError

오류가 발생했습니다.

>? 이 콜백은 SDK에 복구할 수 없는 오류가 발생했음을 나타냅니다. 이러한 오류를 수신해야 하며 필요한 경우 UI 알림을 사용자에게 보내야 합니다.

```objc
- (void)onError:(int)code message:(NSString * _Nullable)message;
```

매개변수는 다음과 같습니다.

| 매개변수    | 유형     | 의미     |
| ------- | -------- | -------- |
| code    | int    | 오류 코드   |
| message | NSString  | 오류 정보 |

### onCallReceived

통화 초대가 수신되었습니다. 이 콜백은 초대받은 사람이 받았습니다. 이 이벤트를 수신하여 수신 통화 보기 표시 여부를 결정할 수 있습니다.

```objc
- (void)onCallReceived:(NSString *)callerId calleeIdList:(NSArray<NSString *> *)calleeIdList groupId:(NSString * _Nullable)groupId callMediaType:(TUICallMediaType)callMediaType
```

매개변수는 다음과 같습니다.

| 매개변수          | 유형             | 의미                                   |
| ------------- | ---------------- | -------------------------------------- |
| callerId      | NSString         | 초대자의 사용자 ID                      |
| calleeIdList  | NSArray          | 초대받은 사람 목록               |
| groupId       | NSString         | 그룹 ID                            |
| callMediaType | TUICallMediaType | 비디오 또는 오디오일 수 있는 통화 유형 |

### onCallCancelled

초대한 사람이 통화를 취소했거나 시간이 초과되었습니다. 이 콜백은 초대받은 사람이 받았습니다. 이 이벤트를 수신하여 부재중 전화 메시지를 표시할지 여부를 결정할 수 있습니다.

```objc
- (void)onCallCancelled:(NSString *)callerId;
```

매개변수는 다음과 같습니다.

| 매개변수     | 유형     | 의미          |
| -------- | -------- | ------------- |
| callerId | NSString | 초대자의 사용자 ID |

### onCallBegin

통화가 연결되었습니다. 이 콜백은 초대자와 초대받은 사람 모두에게 수신됩니다. 이 이벤트를 수신하여 클라우드 녹화, 콘텐츠 조정 또는 기타 작업 시작 여부를 결정할 수 있습니다.

```swift
- (void)onCallBegin:(TUIRoomId *)roomId callMediaType:(TUICallMediaType)callMediaType callRole:(TUICallRole)callRole;
```

매개변수는 다음과 같습니다.

| 매개변수          | 유형             | 의미                                                         |
| ------------- | ---------------- | ------------------------------------------------------------ |
| roomId        | TUIRoomId        | 방 ID. 현재는 숫자로 된 방 ID만 사용할 수 있으며, 문자열 형식의 방 ID는 향후 지원될 예정임 |
| callMediaType | TUICallMediaType | 비디오 또는 오디오일 수 있는 통화 유형                           |
| callRole      | TUICallRole      | 호출자 또는 호출 수신자가 될 수 있는 역할                                   |

### onCallEnd

통화가 종료되었습니다. 이 콜백은 초대자와 초대받은 사람 모두에게 수신됩니다. 이 이벤트를 수신하여 통화 시간 및 통화 유형과 같은 통화 정보를 표시하거나 클라우드 녹음을 중지할 시기를 결정할 수 있습니다.

```swift
- (void)onCallEnd:(TUIRoomId *)roomId callMediaType:(TUICallMediaType)callMediaType callRole:(TUICallRole)callRole totalTime:(float)totalTime;
```

매개변수는 다음과 같습니다.

| 매개변수          | 유형             | 의미                                                         |
| ------------- | ---------------- | ------------------------------------------------------------ |
| roomId        | TUIRoomId        | 방 ID. 현재는 숫자로 된 방 ID만 사용할 수 있으며, 문자열 형식의 방 ID는 향후 지원될 예정임 |
| callMediaType | TUICallMediaType | 비디오 또는 오디오일 수 있는 통화 유형                           |
| callRole      | TUICallRole      | 호출자 또는 호출 수신자가 될 수 있는 역할                                   |
| totalTime     | float            | 통화 시간                                               |

>! 예를 들어 프로세스가 닫힐 때와 같이 오류가 발생하면 클라이언트 측 콜백이 손실되는 경우가 많습니다. 과금 등의 목적으로 통화 시간을 측정해야 하는 경우 REST API를 사용하는 것이 좋습니다.

### onCallMediaTypeChanged

통화 유형이 변경되었습니다.

```swift
- (void)onCallMediaTypeChanged:(TUICallMediaType)oldCallMediaType newCallMediaType:(TUICallMediaType)newCallMediaType;
```

매개변수는 다음과 같습니다.

| 매개변수             | 유형             | 의미         |
| ---------------- | ---------------- | ------------ |
| oldCallMediaType | TUICallMediaType | 변경 전의 통화 유형 |
| newCallMediaType | TUICallMediaType | 변경 후의 호출 유형 |

### onUserReject

통화가 거절되었습니다. 1v1 통화에서는 초대한 사람만 이 콜백을 받습니다. 그룹 통화에서 모든 초대 대상자는 이 콜백을 받습니다.

```swift
- (void)onUserReject:(NSString *)userId;
```

매개변수는 다음과 같습니다.

| 매개변수   | 유형     | 의미          |
| ------ | -------- | ------------- |
| userId | NSString | 통화를 거절한 사용자의 ID |

### onUserNoResponse

사용자가 응답하지 않았습니다.

```swift
- (void)onUserNoResponse:(NSString *)userId;
```

매개변수는 다음과 같습니다.

| 매개변수   | 유형     | 의미            |
| ------ | -------- | --------------- |
| userId | NSString | 응답하지 않은 사용자의 ID |

### onUserLineBusy

통화 중입니다.

```swift
- (void)onUserLineBusy:(NSString *)userId;
```

### onUserJoin

사용자가 통화에 참여했습니다.

```swift
- (void)onUserJoin:(NSString *)userId;
```

### onUserLeave

사용자가 통화를 종료했습니다.

```swift
- (void)onUserLeave:(NSString *)userId;
```

### onUserAudioAvailable

사용자가 오디오를 보내고 있는지 여부입니다.

```swift
- (void)onUserAudioAvailable:(NSString *)userId isAudioAvailable:(BOOL)isAudioAvailable;
```

매개변수는 다음과 같습니다.

| 매개변수             | 유형     | 의미             |
| ---------------- | -------- | ---------------- |
| userId           | NSString | 사용자 ID          |
| isAudioAvailable | BOOL     | 사용자에게 오디오가 있는지 여부 |

### onUserVideoAvailable

사용자가 비디오를 보내고 있는지 여부입니다.

```swift
- (void)onUserVideoAvailable:(NSString *)userId isVideoAvailable:(BOOL)isVideoAvailable;
```

매개변수는 다음과 같습니다.

| 매개변수             | 유형     | 의미             |
| ---------------- | -------- | ---------------- |
| userId           | NSString | 사용자 ID      |
| isVideoAvailable | BOOL     | 사용자에게 비디오가 있는지 여부 |

### onUserVoiceVolumeChanged

모든 사용자의 볼륨입니다.

```swift
- (void)onUserVoiceVolumeChanged:(NSDictionary <NSString *, NSNumber *> *)volumeMap;
```

매개변수는 다음과 같습니다.

| 매개변수      | 유형                                  | 의미                                                         |
| --------- | ------------------------------------- | ------------------------------------------------------------ |
| volumeMap | NSDictionary <NSString *, NSNumber *> | 각 사용자의 볼륨을 포함하는 볼륨 테이블(userId). 값 범위: 0-100 |
| volumeMap | NSDictionary                          | 각 사용자의 볼륨을 포함하는 볼륨 테이블(userId). 값 범위: 0-100 |

### onUserNetworkQualityChanged

모든 사용자의 네트워크 품질입니다.

```swift
- (void)onUserNetworkQualityChanged:(NSArray<TUINetworkQualityInfo *> *)networkQualityList;
```

매개변수는 다음과 같습니다.

| 매개변수               | 유형    | 의미                                                     |
| ------------------ | ------- | -------------------------------------------------------- |
| networkQualityList | NSArray | 모든 사용자의 현재 네트워크 상태(userId) |