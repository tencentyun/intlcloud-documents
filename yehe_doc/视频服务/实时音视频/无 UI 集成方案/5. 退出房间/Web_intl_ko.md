본 문서는 TRTC 방 퇴장 방법과 어떤 경우에 사용자가 강제 퇴장 당할 수 있는지 설명합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/ea39f08a98dc41195ae63a6ecae803b8.png)

TRTC Web SDK를 사용하다 보면 종종 다음과 같은 객체를 접하게 됩니다.
- Client 객체는 로컬 클라이언트를 말합니다. [Client](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html) 타입으로 통화방 추가, 로컬 스트림 배포, 원격 스트림 구독 등 기능을 제공합니다.
- Stream 객체는 멀티미디어 스트림 객체를 말하며, 로컬 멀티미디어 스트림 객체 [LocalStream](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html)와 원격 멀티미디어 스트림 객체 [RemoteStream](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/RemoteStream.html)로 나뉩니다. Stream 타입은 오디오 및 비디오의 재생과 관련한 멀티미디어 스트림 객체 행위를 지원합니다.

[](id:step1)
## 1단계: 방 입장
Client 객체를 생성하고 방에 입장합니다. 자세한 안내는 [방 입장](https://intl.cloud.tencent.com/document/product/647/48424)을 참고하십시오.

[](id:step2)
## 2단계: 방 퇴장

통화 종료 시 [Client.leave()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#leave)를 호출하여 영상 통화방에서 퇴장하면 모든 영상 통화 세션이 종료됩니다.

```javascript
await client.leave(); 
```

[](id:step3)
## 3단계: 강제 퇴장
다음과 같은 경우 사용자는 [`CLIENT_BANNED`](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/module-ClientEvent.html#.CLIENT_BANNED) 콜백을 받게 되며 이는 방 강제 퇴장을 나타냅니다.

```javascript
client.on('client-banned', error => {
  console.error('client-banned observed: ' + error.message);
  // client-banned observed: client was banned because of duplicated userId joining the room.
  // client-banned observed: client was banned because of you got banned by account admin
});
```

- **사례1: 동일한 아이디의 사용자가 방에 입장**
방에 동일한 userId를 가진 앵커가 2개 있는 경우 먼저 방에 입장한 사용자가 방에서 퇴장됩니다.
예시: 사용자 A가 먼저 방에 들어가고 사용자 B가 동일한 사용자 ID로 같은 방에 들어갔다고 가정합니다. 사용자 A는 방에서 퇴장됩니다.
동일한 방에 동일한 ID를 가진 두 명의 사용자가 있으면 오류가 발생할 수 있으며 허용되지 않습니다.

- **사례2: 사용자 강제 퇴장 또는 방 해산을 위해 서버측 API가 호출됨**
[RemoveUser](https://intl.cloud.tencent.com/document/product/647/34268) | [RemoveUserByStrRoomId](https://intl.cloud.tencent.com/document/product/647/39630)를 호출하여 TRTC 룸에서 사용자를 제거합니다. 사용자는 [`CLIENT_BANNED`](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/module-ClientEvent.html#.CLIENT_BANNED) 콜백을 받게 됩니다. [DismissRoom](https://intl.cloud.tencent.com/document/product/647/34269) | [DismissRoomByStrRoomId](https://intl.cloud.tencent.com/document/product/647/39631)를 호출하여 TRTC 룸을 닫으면 룸의 모든 사용자는 [`CLIENT_BANNED`](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/module-ClientEvent.html#.CLIENT_BANNED) 콜백을 받게 됩니다.
