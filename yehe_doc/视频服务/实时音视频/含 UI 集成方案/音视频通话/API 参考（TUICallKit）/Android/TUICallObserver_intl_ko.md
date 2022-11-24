## TUICallObserver API

TUICallObserver는 TUICallEngine의 콜백 클래스입니다. 이벤트를 수신하는 데 사용할 수 있습니다.

## 개요

| API                                                          | 설명                       |
| ------------------------------------------------------------ | -------------------------- |
| [onError](#onerror) | 통화 중 오류 발생         |
| [onCallReceived](#oncallreceived) | 통화 수신             |
| [onCallCancelled](#oncallcancelled) | 통화 취소             |
| [onCallBegin](#oncallbegin) | 통화 연결             |
| [onCallEnd](#oncallend) | 통화 종료             |
| [onCallMediaTypeChanged](#oncallmediatypechanged) | 통화 유형 변경 |
| [onUserReject](#onuserreject) | xxxx 사용자 통화 거절    |
| [onUserNoResponse](#onusernoresponse) | xxxx 사용자가 응답하지 않음      |
| [onUserLineBusy](#onuserlinebusy) | xxxx 사용자 통화 중        |
| [onUserJoin](#onuserjoin) | xxxx 사용자가 통화에 참여함    |
| [onUserLeave](#onuserleave) | xxxx 사용자가 통화를 종료함    |
| [onUserVideoAvailable](#onuservideoavailable) | xxx 사용자에게 비디오 스트림이 있는지 여부 |
| [onUserAudioAvailable](#onuseraudioavailable) | xxx 사용자에게 오디오 스트림이 있는지 여부 |
| [onUserVoiceVolumeChanged](#onuservoicevolumechanged) | 모든 사용자의 볼륨 수준 |
| [onUserNetworkQualityChanged](#onusernetworkqualitychanged) | 모든 사용자의 네트워크 품질 |

## 세부 정보

### onError

오류가 발생했습니다.

>? 이 콜백은 SDK에 복구할 수 없는 오류가 발생했음을 나타냅니다. 이러한 오류를 수신해야 하며 필요한 경우 UI 알림을 사용자에게 보내야 합니다.

```java
void onError(int code, String msg);
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형   | 의미     |
| ---- | ------ | -------- |
| code | int    | 오류 코드   |
| msg  | String | 오류 정보 |

### onCallReceived

통화 초대가 수신되었습니다. 이 콜백은 초대받은 사람이 받게됩니다. 이 이벤트를 수신하여 수신 통화 보기 표시 여부를 결정할 수 있습니다.

```java
void onCallReceived(String callerId, List<String> calleeIdList, String groupId, 
                    TUICallDefine.MediaType callMediaType);
```

매개변수는 다음과 같습니다.

| 매개변수          | 유형                    | 의미                                   |
| ------------- | ----------------------- | -------------------------------------- |
| callerId      | String                  | 초대자의 사용자 ID                      |
| calleeIdList  | List                    | 초대받은 사람 목록               |
| groupId       | String                  | 그룹 ID                            |
| callMediaType | TUICallDefine.MediaType | 비디오 또는 오디오일 수 있는 통화 유형 |

### onCallCancelled

초대한 사람이 통화를 취소했거나 시간이 초과되었습니다. 이 콜백은 초대 받은 사람이 받게됩니다. 이 이벤트를 수신하여 부재 중 전화 메시지를 표시할지 여부를 결정할 수 있습니다.

```java
void onCallCancelled(String callerId);
```

매개변수는 다음과 같습니다.

| 매개변수     | 유형   | 의미          |
| -------- | ------ | ------------- |
| callerId | String | 취소 사용자 ID |

### onCallBegin

통화가 연결되었습니다. 이 콜백은 초대자와 초대받은 사람 모두에게 수신됩니다. 이 이벤트를 수신하여 클라우드 녹화, 콘텐츠 조정 또는 기타 작업 시작 여부를 결정할 수 있습니다.

```java
void onCallBegin(TUICommonDefine.RoomId roomId, TUICallDefine.MediaType callMediaType, TUICallDefine.Role callRole);
```

매개변수는 다음과 같습니다.

| 매개변수          | 유형                    | 의미                                                         |
| ------------- | ----------------------- | ------------------------------------------------------------ |
| roomId        | TUICommonDefine.RoomId  | 방 ID. 현재는 숫자로 된 방 ID만 사용할 수 있으며, 문자열 형식의 방 ID는 향후 지원될 예정임 |
| callMediaType | TUICallDefine.MediaType | 비디오 또는 오디오일 수 있는 통화 유형                           |
| callRole      | TUICallDefine.Role      | 호출자 또는 호출 수신자가 될 수 있는 역할                                   |

### onCallEnd

통화가 종료되었습니다. 이 콜백은 초대자와 초대 받은 사람 모두에게 수신됩니다. 이 이벤트를 수신하여 통화 시간 및 통화 유형과 같은 통화 정보를 표시하거나 클라우드 녹음을 중지할 시기를 결정할 수 있습니다.

```java
void onCallEnd(TUICommonDefine.RoomId roomId, TUICallDefine.MediaType callMediaType, TUICallDefine.Role callRole, long totalTime);
```

매개변수는 다음과 같습니다.

| 매개변수          | 유형                    | 의미                                                         |
| ------------- | ----------------------- | ------------------------------------------------------------ |
| roomId        | TUICommonDefine.RoomId  | 방 ID. 현재는 숫자로 된 방 ID만 사용할 수 있으며, 문자열 형식의 방 ID는 향후 지원될 예정임 |
| callMediaType | TUICallDefine.MediaType | 비디오 또는 오디오일 수 있는 통화 유형                           |
| callRole      | TUICallDefine.Role      | 호출자 또는 호출 수신자가 될 수 있는 역할                                   |
| totalTime     | long                    | 통화 시간                                               |

>! 예를 들어 프로세스가 닫힐 때와 같이 오류가 발생하면 클라이언트 측 콜백이 손실되는 경우가 많습니다. 과금 등의 목적으로 통화 시간을 측정해야 하는 경우 REST API를 사용하는 것이 좋습니다.

### onCallMediaTypeChanged

통화 유형이 변경되었습니다.

```java
void onCallMediaTypeChanged(TUICallDefine.MediaType oldCallMediaType,TUICallDefine.MediaType newCallMediaType);
```

매개변수는 다음과 같습니다.

| 매개변수             | 유형                    | 의미         |
| ---------------- | ----------------------- | ------------ |
| oldCallMediaType | TUICallDefine.MediaType | 변경 전 통화 유형 |
| newCallMediaType | TUICallDefine.MediaType | 변경 후 통화 유형 |

### onUserReject

통화가 거절되었습니다. 1v1 통화에서는 초대한 사람만 이 콜백을 받습니다. 그룹 통화에서 모든 초대 대상자가 이 콜백을 받습니다.

```java
void onUserReject(String userId);
```

매개변수는 다음과 같습니다.

| 매개변수   | 유형   | 의미          |
| ------ | ------ | ------------- |
| userId | String | 통화를 거절한 초대받은 사람의 사용자 ID |

### onUserNoResponse

사용자가 응답하지 않습니다.

```java
void onUserNoResponse(String userId);
```

매개변수는 다음과 같습니다.

| 매개변수   | 유형   | 의미            |
| ------ | ------ | --------------- |
| userId | String | 응답하지 않은 초대자의 사용자 ID |

### onUserLineBusy

사용자가 사용 중입니다.

```java
void onUserLineBusy(String userId);
```

매개변수는 다음과 같습니다.

| 매개변수   | 유형   | 의미          |
| ------ | ------ | ------------- |
| userId    | String  | 통화 중인 초대자의 사용자 ID      |

### onUserJoin

사용자가 통화에 참여했습니다.

```java
void onUserJoin(String userId);
```

매개변수는 다음과 같습니다.

| 매개변수   | 유형   | 의미                  |
| ------ | ------ | --------------------- |
| userId | String | 통화에 참여한 사용자의 ID |

### onUserLeave

사용자가 통화를 종료했습니다.

```java
void onUserLeave(String userId);
```

매개변수는 다음과 같습니다.

| 매개변수   | 유형   | 의미                  |
| ------ | ------ | --------------------- |
| userId    | String  | 통화 퇴장 사용자 ID      |

### onUserVideoAvailable

사용자가 비디오를 보내고 있는지 여부입니다.

```java
void onUserVideoAvailable(String userId, boolean isVideoAvailable);
```

매개변수는 다음과 같습니다.

| 매개변수             | 유형    | 의미             |
| ---------------- | ------- | ---------------- |
| userId    | String  | 사용자 ID      |
| isVideoAvailable | boolean | 사용자가 비디오를 가지고 있는지 여부 |

### onUserAudioAvailable

사용자가 오디오를 보내고 있는지 여부입니다.

```java
void onUserAudioAvailable(String userId, boolean isAudioAvailable);
```

매개변수는 다음과 같습니다.

| 매개변수             | 유형    | 의미             |
| ---------------- | ------- | ---------------- |
| userId           | String  | 사용자 ID          |
| isAudioAvailable | boolean | 사용자에게 오디오가 있는지 여부 |

### onUserVoiceVolumeChanged

모든 사용자의 볼륨입니다.

```java
void onUserVoiceVolumeChanged(Map<String, Integer> volumeMap);
```

매개변수는 다음과 같습니다.

| 매개변수      | 유형                 | 의미                                                         |
| --------- | -------------------- | ------------------------------------------------------------ |
| volumeMap | Map< String, Integer> | 각 사용자의 볼륨을 포함하는 볼륨 테이블(`userId`), 값 범위: 0-100 |

### onUserNetworkQualityChanged

모든 사용자의 네트워크 품질입니다.

```java
void onUserNetworkQualityChanged(List<TUICallDefine.NetworkQualityInfo> networkQualityList);
```

매개변수는 다음과 같습니다.

| 매개변수               | 유형 | 의미                                                     |
| ------------------ | ---- | -------------------------------------------------------- |
| networkQualityList | List | 모든 사용자의 현재 네트워크 상태(userId) |
