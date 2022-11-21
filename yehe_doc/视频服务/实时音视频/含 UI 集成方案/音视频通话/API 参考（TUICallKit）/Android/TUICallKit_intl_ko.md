## TUICallKit API

TUICallKit은 **UI 요소를 포함**하는 음성/영상 통화 컴포넌트입니다. API를 사용하여 WeChat과 유사한 음성/영상 통화 애플리케이션을 빠르게 구현할 수 있습니다. 통합에 대한 지침은 [TUICallKit 통합](https://www.tencentcloud.com/document/product/647/50991)을 참고하십시오.

## API 개요

| API                                             | 설명                                                         |
| ------------------------------------------------------------ | -------------------------------- |
| [createInstance](#createinstance) | TUICallKit 인스턴스 생성(싱글톤 모드) |
| [setSelfInfo](#setselfinfo) | 대화명 및 프로필 사진 설정             |
| [call](#call) | 1v1 통화 호출                    |
| [groupCall](#groupcall) | 그룹 통화 호출                     |
| [joinInGroupCall](#joiningroupcall) | 그룹 통화 참여         |
| [setCallingBell](#setcallingbell) | 벨소리 설정               |
| [enableMuteMode](#enablemutemode) | 음소거 모드 활성화 여부 설정                |
| [enableFloatWindow](#enablefloatwindow) | 플로팅 창 활성화 여부 설정              |

## API 세부 정보

### createInstance

이 API는 TUICallKit 싱글톤을 생성하는 데 사용됩니다.

```java
TUICallKit createInstance(Context context)
```

### setSelfInfo

이 API는 대화명과 프로필 사진을 설정하는 데 사용됩니다. 대화명은 500바이트를 초과할 수 없으며 프로필 사진은 URL로 지정됩니다.

```java
void setSelfInfo(String nickname, String avatar, TUICommonDefine.Callback callback)
```

매개변수는 다음과 같습니다.

| 매개변수     | 유형   | 의미           |
| -------- | ------ | -------------- |
| nickname | String | 대화명 |
| avatar   | String | 프로필 사진 |

### call

이 API는 (1v1) 통화를 수행하는 데 사용됩니다.

```java
 void call(String userId, TUICallDefine.MediaType callMediaType)
```

매개변수는 다음과 같습니다.

| 매개변수          | 유형                    | 의미                                   |
| ------------- | ----------------------- | -------------------------------------- |
| userId        | String                  | 대상 userId                      |
| callMediaType | TUICallDefine.MediaType | 비디오 또는 오디오일 수 있는 통화 유형 |

### groupCall

이 API는 그룹 통화에 참여하는 데 사용됩니다.

>! 그룹 통화를 하기 전에 먼저 IM 그룹을 생성해야 합니다.

```java
void groupCall(String groupId, List<String> userIdList, TUICallDefine.MediaType callMediaType) {
```

매개변수는 다음과 같습니다.

| 매개변수          | 유형                    | 의미                                   |
| ------------- | ----------------------- | -------------------------------------- |
| groupId       | String                  | 그룹 ID                    |
| userIdList    | List                    | 대상 userId                 |
| callMediaType | TUICallDefine.MediaType | 비디오 또는 오디오일 수 있는 통화 유형 |

### joinInGroupCall

이 API는 그룹 통화에 참여하는 데 사용됩니다.

>! 그룹 통화를 하기 전에 먼저 IM 그룹을 생성해야 합니다.

```java
void joinInGroupCall(TUICommonDefine.RoomId roomId, String groupId, TUICallDefine.MediaType callMediaType, TUICommonDefine.Callback callback);
```

매개변수는 다음과 같습니다.

| 매개변수          | 유형                    | 의미                                                         |
| ------------- | ----------------------- | ------------------------------------------------------------ |
| roomId        | TUICommonDefine.RoomId  | 방 ID. 현재는 숫자로 된 방 ID만 사용할 수 있으며, 문자열 형식의 방 ID는 향후 지원될 예정임 |
| groupId       | String                  | 그룹 ID                                          |
| callMediaType | TUICallDefine.MediaType | 비디오 또는 오디오일 수 있는 통화 유형                       |

### setCallingBell

이 API는 벨소리를 설정하는 데 사용됩니다. filePath는 액세스 가능한 로컬 파일 URL이어야 합니다.

벨소리 세트는 장치와 연결되어 있으며 사용자에 따라 변경되지 않습니다.

벨소리를 재설정하려면 `filePath`에 빈 문자열을 전달하십시오.

```java
void setCallingBell(String filePath);
```

### enableMuteMode

이 API는 음소거 모드를 켤지 여부를 설정하는 데 사용됩니다.

```java
void enableMuteMode(boolean enable);
```

### enableFloatWindow

이 API는 플로팅 창 활성화 여부를 설정하는 데 사용됩니다.

기본값은 'false'이며 통화 보기의 왼쪽 상단 모서리에 있는 플로팅 창 버튼이 숨겨져 있습니다. true로 설정하면 버튼이 표시됩니다.

```java
void enableFloatWindow(boolean enable);
```