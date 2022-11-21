## TUICallKit API

TUICallKit은 **UI 요소를 포함**하는 음성/영상 통화 컴포넌트입니다. API를 사용하여 WeChat과 유사한 음성/영상 통화 애플리케이션을 빠르게 구현할 수 있습니다. 통합에 대한 지침은 [TUICallKit 통합](https://www.tencentcloud.com/document/product/647/50992)을 참고하십시오.

## API 개요

| API                                             | 설명                                                         |
| ------------------------------------------------------------ | -------------------------------- |
| [createInstance](#createinstance) | TUICallKit 인스턴스 생성(싱글톤 모드) |
| [setSelfInfo](#setselfinfo) | 대화명 및 프로필 사진 설정             |
| [call](#call) | 1v1 전화 걸기                    |
| [groupCall](#groupcall) | 그룹 전화 걸기                     |
| [joinInGroupCall](#joiningroupcall) | 그룹 통화에 참여         |
| [setCallingBell](#setcallingbell) | 벨소리 설정               |
| [enableMuteMode](#enablemutemode) | 음소거 모드를 켤지 여부 설정                |
| [enableFloatWindow](#enablefloatwindow) | 플로팅 창 활성화 여부 설정              |

## API 세부 정보

### createInstance

이 API는 TUICallKit 싱글톤을 생성하는 데 사용됩니다.

```objectivec
- (instancetype)createInstance;
```

### setSelfInfo

이 API는 대화명과 프로필 사진을 설정하는 데 사용됩니다. 대화명은 500바이트를 초과할 수 없으며 프로필 사진은 URL로 지정됩니다.

```objectivec
- (void)setSelfInfo:(NSString * _Nullable)nickname avatar:(NSString * _Nullable)avatar succ:(TUICallSucc)succ fail:(TUICallFail)fail
```

| 매개변수     | 유형     | 의미           |
| -------- | -------- | -------------- |
| nickName | NSString | 대화명 |
| avatar   | NSString | 프로필 사진 |

### call

이 API는 (1v1) 통화를 수행하는 데 사용됩니다.

```objectivec
- (void)call:(NSString *)userId callMediaType:(TUICallMediaType)callMediaType;
```

매개변수는 다음과 같습니다.

| 매개변수          | 유형             | 의미                                   |
| ------------- | ---------------- | -------------------------------------- |
| userId        | NSString         | 대상 userId                      |
| callMediaType | TUICallMediaType | 비디오 또는 오디오일 수 있는 통화 유형 |

### groupCall

이 API는 그룹 통화를 하는 데 사용됩니다. 그룹 통화를 하기 전에 IM 그룹을 생성해야 합니다.

```objectivec
- (void)groupCall:(NSString *)groupId userIdList:(NSArray<NSString *> *)userIdList callMediaType:(TUICallMediaType)callMediaType;
```

| 매개변수          | 유형             | 의미                                   |
| ------------- | ---------------- | -------------------------------------- |
| groupId       | NSString         | 그룹 ID                    |
| userIdList    | NSArray          | 대상 userId                 |
| callMediaType | TUICallMediaType | 비디오 또는 오디오일 수 있는 통화 유형 |

### joinInGroupCall

이 API는 그룹 통화를 하는 데 사용됩니다. 그룹 통화를 하기 전에 IM 그룹을 생성해야 합니다.

```objectivec
- (void)joinInGroupCall:(TUIRoomId *)roomId groupId:(NSString *)groupId callMediaType:(TUICallMediaType)callMediaType;
```

| 매개변수          | 유형             | 의미                                                         |
| ------------- | ---------------- | ------------------------------------------------------------ |
| roomId        | TUIRoomId        | 방 ID, 현재는 숫자 방 ID만 사용할 수 있으며, 앞으로는 문자열 형식의 방 ID가 지원될 예정임 |
| groupId       | NSString         | 그룹 ID                                          |
| callMediaType | TUICallMediaType | 비디오 또는 오디오일 수 있는 통화 유형                       |

### setCallingBell

이 API는 벨소리를 설정하는 데 사용됩니다. `filePath`는 액세스 가능한 로컬 파일 URL이어야 합니다.

벨소리는 장치와 연결되어 있으며 사용자에 따라 변경되지 않습니다.

벨소리를 재설정하려면 `filePath`에 빈 문자열을 전달하십시오.

```objectivec
- (void)setCallingBell:(NSString *)filePath;
```

### enableMuteMode

이 API는 음소거 모드를 켤지 여부를 설정하는 데 사용됩니다.

```objc
- (void)enableMuteMode:(BOOL)enable;
```

### enableFloatWindow

이 API는 플로팅 창 활성화 여부를 설정하는 데 사용됩니다. 기본값은 'false'이며 통화 보기의 왼쪽 상단 모서리에 있는 플로팅 창 버튼이 숨겨져 있습니다. true로 설정하면 버튼이 표시됩니다.

```objc
- (void)enableFloatWindow:(BOOL)enable;
```