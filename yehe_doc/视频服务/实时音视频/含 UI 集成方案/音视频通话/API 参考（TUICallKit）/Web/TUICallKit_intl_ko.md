## TUICallKit API

TUICallKit API는 **UI 요소를 포함**하는 음성/영상 통화 컴포넌트입니다. API를 사용하여 WeChat과 유사한 음성/영상 통화 애플리케이션을 빠르게 구현할 수 있습니다. 통합에 대한 지침은 [TUICallKit 통합](https://www.tencentcloud.com/document/product/647/50993)을 참고하십시오.

## API 개요

| API                                                          | 설명                                |
| ------------------------------------------------------------ | ----------------------------------- |
| [init](#init) | TUICallKit 초기화                   |
| [call](#call) | 1v1 통화 걸기                       |
| [groupCall](#groupcall) | 그룹 통화 걸기                        |
| [destroyed](#destroyed) | TUICallKit 종료 |

## API 세부 정보

### init

이 API는 TUICallKit을 초기화하는 데 사용됩니다. call과 groupCall보다 먼저 호출되어야 합니다.

```javascript
import { TUICallKitServer } from "./src/components/TUICallKit/Web";
TUICallKitServer.init({
  SDKAppID,
  userID, 
  userSig,
  tim, 
});
```

매개변수는 다음과 같습니다.

| 매개변수     | 유형   | 의미                                                         |
| -------- | ------ | ------------------------------------------------------------ |
| SDKAppID | Number | IM 애플리케이션의 SDKAppID                                        |
| userID   | String | 현재 사용자 ID, 영어 알파벳(a-z, A-Z), 숫자(0-9), 하이픈(-), 언더바(_)의 문자열로 구성 |
| userSig  | String | Tencent Cloud의 독점 보안 서명. 획득 방법은 [UserSig](https://www.tencentcloud.com/document/product/647/35166) 참고 |
| TIM 인스턴스 | Any    | 이미 TIM 인스턴스가 있는 경우 이 tim 매개변수(선택 사항)를 사용하여 TIM 인스턴스의 고유성을 보장할 수 있음 |

### call

이 API는 (1v1) 통화를 수행하는 데 사용됩니다.


```javascript
import { TUICallKitServer } from "./src/components/TUICallKit/Web";
TUICallKitServer.call({
  userID: 'jack',
  type: 1,
});
```

매개변수는 다음과 같습니다.

| 매개변수   | 유형   | 의미                                                   |
| ------ | ------ | ------------------------------------------------------ |
| userID | String | 호출할 userId                                      |
| type   | Number | 통화 유형, 음성 통화(type = 1), 영상 통화(type = 2) |

### groupCall

이 API는 그룹 통화를 하는 데 사용됩니다.

```javascript
import { TUICallKitServer } from "./src/components/TUICallKit/Web";
TUICallKitServer.groupCall({
  userIDList: ['jack', 'tom'],
  groupID: 'xxx',
  type: 1,
});
```

매개변수는 다음과 같습니다.

| 매개변수       | 유형          | 의미                                                   |
| ---------- | ------------- | ------------------------------------------------------ |
| userIDList | Array<String> | 호출할 사용자의 ID                                       |
| groupID    | String        | 그룹 ID                                             |
| type       | Number        | 통화 유형, 음성 통화(type = 1), 영상 통화(type = 2) |


### destroyed

이 API는 TUICallKit을 종료하는 데 사용됩니다.

```javascript
import { TUICallKitServer } from "./src/components/TUICallKit/Web";
TUICallKitServer.destroyed();
```
