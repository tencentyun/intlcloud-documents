본문에서는 React Native용 IM(Instant Messaging) Demo를 빠르게 실행하는 방법을 소개합니다.

## 환경 요건

|              | 버전                                                         |
| ------------ | ------------------------------------------------------------ |
| React Native | 0.63.4 이후 버전                                             |
| Android      | Android Studio 3.5 및 그 이후 버전. App은 Android 4.1 및 그 이후 버전 디바이스가 필요합니다. |
| iOS          | Xcode 11.0 이후 버전, 프로젝트에 대한 유효한 개발자 서명이 설정되어 있는지 확인하십시오. |

## 전제 조건

[Signing Up](https://intl.cloud.tencent.com/document/product/378/17985)된 계정이 있고 [Identity Verification](https://intl.cloud.tencent.com/document/product/378/3629)이 완료되어야 합니다.

## 파트1: 테스트 사용자 생성

[IM 콘솔](https://console.cloud.tencent.com/im)에서 애플리케이션을 선택하고 왼쪽 사이드바에서 **보조 툴**->**UserSig Generation & Verification**을 클릭하여 두 개의 UserID와 해당 UserSig를 생성하고 `UserID`, `서명(Key)`, `UserSig`를 복사하여 이후 로그인에 사용합니다.

> ? 이 계정은 개발 및 테스트 전용입니다. 애플리케이션 런칭 전에 올바른 `UserSig` 배포 방식은 서버에서 생성하여, App 지향 인터페이스를 제공하는 것입니다. `UserSig`가 필요할 때, App은 비즈니스 서버에 동적 `UserSig` 가져오기 요청을 발송합니다. 자세한 내용은 [서버의 UserSig 생성](https://intl.cloud.tencent.com/document/product/1047/34385)을 참고하십시오.

![](https://main.qcloudimg.com/raw/2286644d987d24caf565142ae30c4392.png)

[](id:part2)

## 파트2: React Native SDK 통합

### 전제 조건

React Native 프로젝트를 생성했거나 또는 기반으로 할 수 있는 React Native 프로젝트가 있습니다.

### 액세스 단계

#### IM SDK 설치
다음 명령을 사용하여 최신 버전의 React Naitve IM SDK를 설치합니다. 명령 라인에서 실행:
```shell
// npm
npm install react-native-tim-js

// yarn
yarn add react-native-tim-js
```

#### SDK 초기화 완료
'initSDK'를 호출하여 SDK 초기화를 완료하십시오. `sdkAppID`를 전달합니다.
```javascript
import { TencentImSDKPlugin, LogLevelEnum } from 'react-native-tim-js';

TencentImSDKPlugin.v2TIMManager.initSDK(
    sdkAppID: 0, // Replace 0 with the SDKAppID of your IM application when integrating
    loglevel: LogLevelEnum.V2TIM_LOG_DEBUG, // Log
    listener: V2TimSDKListener(),
);
```

이 단계에서는 주로 네트워크 상태 및 사용자 정보 변경 등 IM SDK에 대한 일부 리스너를 마운트할 수 있습니다. 자세한 내용은 [이 문서](https://comm.qq.com/im/doc/RN/zh/Interface/Listener/V2TimSDKListener.html)를 참고하십시오.

#### 테스트 계정에 로그인
1. 이제 처음에 콘솔에서 생성된 테스트 계정을 사용하여 로그인 인증을 완료할 수 있습니다.
2. 'TencentImSDKPlugin.v2TIMManager.login' 메소드를 호출하여 테스트 계정에 로그인합니다. 반환값 'res.code'가 0이면 로그인이 성공한 것입니다.
```javascript
import { TencentImSDKPlugin } from 'react-native-tim-js';
 const res = await TencentImSDKPlugin.v2TIMManager.login(
    userID: userID,
    userSig: userSig,
  );
```
> ? 이 계정은 개발 테스트 전용입니다. 애플리케이션이 런칭되기 전에 정확한 `UserSig` 발급 방식은 다음과 같습니다. `UserSig` 계산 코드를 귀하의 서버에 통합하고 App 방향의 인터페이스를 제공합니다. `UserSig`가 필요할 때 귀하의 App이 비즈니스 서버로 동적 `UserSig`를 요청합니다. 자세한 내용은 [서버의 UserSig 생성](https://intl.cloud.tencent.com/document/product/1047/34385)을 참고하십시오.

#### 메시지 발송

다음은 문자 메시지 발송 예이며 프로세스는 다음과 같습니다.
1. `createTextMessage(String)`를 호출하여 문자 메시지를 생성합니다.
2. 반환 값에 따라 메시지 ID를 가져옵니다.
3. `sendMessage()`를 호출하여 해당 ID로 메시지를 발송합니다. `receiver`는 이전에 생성한 다른 테스트 계정 ID로 입력할 수 있습니다. 하나의 채팅 메시지를 발송할 때 `groupID`를 입력할 필요가 없습니다.

코드 예시:

```javascript
import { TencentImSDKPlugin } from 'react-native-tim-js';

const createMessage =
      await TencentImSDKPlugin.v2TIMManager
          .getMessageManager()
          .createTextMessage("The text to create");

const id = createMessage.data!.id!; // The message creation ID

const res = await TencentImSDKPlugin.v2TIMManager
      .getMessageManager()
      .sendMessage(
          id: id, // Pass in the message creation ID to
          receiver: "The userID of the destination user",
          groupID: "The groupID of the destination group",
          );
```

> ?만약 sdkAppID가 낯선 사람에게 메시지를 보낼 수 없기 때문에 전송에 실패한다면, 테스트용으로 콘솔에서 활성화할 수 있습니다.
>
> [이 링크를 클릭](https://console.cloud.tencent.com/im/login-message)하여, 친구 관계망 확인을 비활성화하십시오.

#### 대화 목록 가져오기

이전 단계에서 테스트 메시지를 보내면 다른 테스트 계정에 로그인하여 대화 목록을 가져올 수 있습니다.

대화 목록을 가져오는 방법은 두 가지입니다.

1. 장기간 연결 콜백을 수신하여 대화 목록을 실시간으로 업데이트합니다.
2. API를 요청하여 페이징에 따라 대화 목록을 한번에 가져옵니다.

일반 응용 시나리오는 다음과 같습니다.

응용 프로그램을 실행한 후 바로 대화 목록을 가져온 다음 장기간 연결을 수신하여 대화 목록의 변경 사항을 실시간으로 업데이트합니다.

##### 일회성 요청 대화 목록

대화 목록을 가져오려면 현재 위치를 기록하고 'nextSeq'를 유지해야 합니다.

```typescript
import { useState } from "react";
import { TencentImSDKPlugin } from "react-native-tim-js";

const [nextSeq, setNextSeq] = useState<string>("0");

const getConversationList = async () => {
  const count = 10;
  const res = await TencentImSDKPlugin.v2TIMManager
    .getConversationManager()
    .getConversationList(count, nextSeq);
  setNextSeq(res.data?.nextSeq ?? "0");
};
```

이제 이전 단계에서 다른 테스트 계정을 사용하여 보낸 메시지의 대화를 볼 수 있습니다.

##### 긴 링크에서 실시간으로 대화 목록 가져오기

이 단계에서는 SDK에 리스너를 마운트한 다음 콜백 이벤트를 처리하고 UI를 업데이트해야 합니다.

1. 리스너 마운트.
```javascript
import { TencentImSDKPlugin } from "react-native-tim-js";

const addConversationListener = () => {
  TencentImSDKPlugin.v2TIMManager
    .getConversationManager()
    .addConversationListener({
      onNewConversation: (conversationList) => {
        // new conversation created callback
        _onConversationListChanged(conversationList);
      },
      onConversationChanged: (conversationList) => {
        // conversation changed callback
        _onConversationListChanged(conversationList);
      },
    });
};
```

2. 콜백 이벤트를 처리하고 최신 대화 목록을 인터페이스에 표시합니다.
```javascript
const _onConversationListChanged = (list) => {
  // you can use conversation list to update UI
};
```

#### 메시지 수신

Tencent Cloud IM React Native SDK를 통해 메시지를 수신하는 방법에는 두 가지가 있습니다:

1. 장기간 연결 콜백을 수신하고, 실시간으로 메시지 변경 사항을 가져오고, 렌더링 메시지 기록 목록을 업데이트합니다.
2. API를 요청하여 페이징에 따라 메시지 기록를 한번에 가져옵니다.

일반 응용 시나리오는 다음과 같습니다.

1. 인터페이스는 새로운 대화가 시작되면 먼저 일정량의 메시지 기록을 한꺼번에 요청하여 메시지 기록 목록을 보여 줍니다.
2. 긴 링크를 수신하여 실시간으로 새로운 메시지를 수신하여 메시지 기록 목록에 추가합니다.

##### 일회성 요청 메시지 기록 리스트

페이지당 풀링하는 메시지의 수는 너무 크면 안 됩니다. 그렇지 않으면 풀링 속도에 영향을 줄 수 있습니다. 약 20으로 설정하는 것이 좋습니다.

다음 요청 시 현재 페이지 수를 동적으로 기록해야 합니다.

예시 코드는 다음과 같습니다.

```javascript
import { TencentImSDKPlugin } from "react-native-tim-js";

const getGroupHistoryMessageList = async () => {
  const groupID = "";
  const count = 20;
  const lastMsgID = "";
  const res = await TencentImSDKPlugin.v2TIMManager
    .getMessageManager()
    .getGroupHistoryMessageList(groupID, count, lastMsgID);
  const msgList = res.data ?? [];
  // here you can use msgList to render your message list
};
```

##### 긴 링크를 통해 실시간으로 새 메시지 가져오기

메시지 기록 리스트가 초기화되면 `V2TimAdvancedMsgListener.onRecvNewMessage`라는 긴 링크에서 새 메시지가 나타납니다.

`onRecvNewMessage` 콜백이 트리거된 후, 필요에 따라 새 메시지를 메시지 기록 리스트에 추가할 수 있습니다.

바인딩 리스너의 예시 코드는 다음과 같습니다.

```javascript
import { TencentImSDKPlugin } from "react-native-tim-js";

const adVancesMsgListener = {
  onRecvNewMessage: (newMsg) => {
    _onReceiveNewMsg(newMsg);
    /// ... other listeners related to message
  },
};

const addAdvancedMsgListener = () => {
  TencentImSDKPlugin.v2TIMManager
    .getMessageManager()
    .addAdvancedMsgListener(adVancesMsgListener);
};
```

이제 IM 모듈 개발을 완료했으며, 메시지를 주고받거나 다른 대화에 들어갈 수 있습니다.
그룹, 사용자 프로필, 관계망, 오프라인 푸시, 로컬 검색 등 관련 기능을 계속 개발할 수 있습니다. 자세한 내용은 [SDK API 문서](https://comm.qq.com/im/doc/RN/zh/)를 참고하십시오.

## FAQ

#### demo 실행 시 `Undefined symbols for architecture x86_64 [duplicate]`를 해결하는 방법은 무엇입니까?

[문서](https://stackoverflow.com/questions/71933392/react-native-ios-undefined-symbols-for-architecture-x86-64)를 참고하십시오.

#### demo 실행 시 `Failed to resolve: react-native-0.71.0-rc.0-debug`를 해결하는 방법은 무엇입니까?

[문서](https://blog.csdn.net/weixin_44132277/article/details/127731985)를 참고하십시오.
