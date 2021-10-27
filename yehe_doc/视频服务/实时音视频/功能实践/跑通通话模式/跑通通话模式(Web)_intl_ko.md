본문은 실시간 음성/영상 통화 기능을 구현하는 방법에 대한 TRTC Web SDK의 기본 워크플로를 설명합니다.

TRTC Web SDK를 사용하다 보면 종종 다음과 같은 객체를 접하게 됩니다.
- Client 객체는 로컬 클라이언트를 말합니다. [Client](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html) 타입으로 통화방 추가, 로컬 스트림 배포, 원격 스트림 구독 등 기능을 제공합니다.
- Stream 객체는 멀티미디어 스트림 객체를 말하며, 로컬 멀티미디어 스트림 객체[LocalStream](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html)와 원격 멀티미디어 스트림 객체[RemoteStream](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/RemoteStream.html)로 나뉩니다. Stream 타입은 오디오 및 비디오의 재생과 관련한 멀티미디어 스트림 객체 행위를 지원합니다.

기본 영상 통화를 위한 API 호출 방법은 다음과 같습니다.
![](https://main.qcloudimg.com/raw/9f246e5a88e5a8176290eb6070a0ecb6.jpg)

## 1단계: Client 객체 생성

[TRTC.createClient()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#.createClient)로 [Client](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html) 객체를 생성합니다. 매개변수 설정 방법은 다음과 같습니다.
- 'mode': TRTC 통화 모드를 'rtc'로 설정
- 'sdkAppId': Tencent Cloud에서 신청한 sdkAppId
- 'userId': 사용자 ID
- 'userSig': 사용자 서명으로, 계산 방법은 [UserSig 계산 방법](https://intl.cloud.tencent.com/document/product/647/35166) 참고

```javascript
const client = TRTC.createClient({
  mode: 'rtc',
  sdkAppId,
  userId,
  userSig
});
```

## 2단계: 영상 통화방 입장

[Client.join()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#join)을 호출하여 음성 및 영상 통화방에 입장합니다.
매개변수 'roomId': 방 ID

```javascript
client
  .join({ roomId })
  .catch(error => {
    console.error('입장 실패' + error);
  })
  .then(() => {
    console.log('방 입장 성공');
  });
```

## 3단계: 로컬 스트림 배포 및 원격 스트림 구독

1. [TRTC.createStream()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#.createStream)을 사용해 로컬 멀티미디어 스트림을 생성합니다.
 아래의 인스턴스는 카메라 및 마이크에서 수집한 멀티미디어 스트림입니다. 매개변수 설정은 다음과 같습니다.
 - 'userId': 로컬 스트림 소속 사용자 ID
 - 'audio': 오디오 활성화 여부
 - `video`: 비디오 활성화 여부

 ```javascript
const localStream = TRTC.createStream({ userId, audio: true, video: true });
 ```

2. [LocalStream.initialize()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#initialize)를 호출하여 로컬 멀티미디어 스트림을 초기화합니다.
```javascript
localStream
  .initialize()
  .catch(error => {
    console.error('로컬 스트림 초기화 실패 ' + error);
  })
  .then(() => {
    console.log('로컬 스트림 초기화 성공');
  });
```

3. 로컬 스트림을 초기화 성공 후, [Client.publish()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#publish)를 호출하여 로컬 스트림을 배포합니다.
```javascript
client
  .publish(localStream)
  .catch(error => {
    console.error('로컬 스트리밍 배포 실패 ' + error);
  })
  .then(() => {
    console.error('로컬 스트리밍 배포 성공' + error);
  });
```

4. 원격 스트림은 이벤트 리슨[Client.on('stream-added')](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/module-Event.html#.STREAM_ADDED)을 통해 해당 이벤트를 획득한 뒤 [Client.subscribe()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#subscribe)를 통해 원격 멀티미디어 스트림을 구독합니다.
>?
>- [Client.join()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#join)에서 방에 입장하기 전 원격 사용자의 방 입장 알림을 놓치지 않도록 [Client.on('stream-added')](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/module-Event.html#.STREAM_ADDED) 이벤트를 등록하십시오.
>- 원격 스트림 퇴장 등 다른 이벤트는 [API 소개 문서](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/module-Event.html)에서 확인할 수 있습니다.
```javascript
client.on('stream-added', event => {
  const remoteStream = event.stream;
  console.log('원격 스트림 추가: ' + remoteStream.getId());
  //원격 스트림 구독
  client.subscribe(remoteStream);
});
client.on('stream-subscribed', event => {
  const remoteStream = event.stream;
  console.log('원격 스트림 구독 성공:' + remoteStream.getId());
  // 원격 스트림 재생
  remoteStream.play('remote_stream-' + remoteStream.getId());
});
```

5. 로컬 스트림 초기화 성공 후 콜백이나 원격 스트림의 구독 이벤트 콜백 시, [Stream.play()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Stream.html#play)를 호출하여 웹 페이지에서 멀티미디어를 재생합니다. 'play' 시 div 요소의 ID를 매개변수로 받으면 SDK에서 div 요소 하위에 멀티미디어 태그를 자동 생성한 뒤 멀티미디어를 재생합니다.
 - 로컬 스트림 초기화 성공 시 로컬 스트림 재생
```javascript
localStream
  .initialize()
  .catch(error => {
    console.error('로컬 스트림 초기화 실패 ' + error);
  })
  .then(() => {
    console.log('로컬 스트림 초기화 성공');
    localStream.play('local_stream');
  });
```
 - 원격 스트림 구독 성공 시 원격 스트림 재생
```javascript
client.on('stream-subscribed', event => {
  const remoteStream = event.stream;
  console.log('원격 스트림 구독 성공:' + remoteStream.getId());
  // 원격 스트림 재생
  remoteStream.play('remote_stream-' + remoteStream.getId());
});
```

## 4단계: 영상 통화방 퇴장

통화 종료 시 [Client.leave()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#leave)를 호출하여 영상 통화방에서 퇴장하면 모든 영상 통화 세션이 종료됩니다.

```javascript
client
.leave()
.then(() => {
  // 방 퇴장 후에도 client.join 호출로 방에 다시 입장하여 새 통화를 할 수 있음
})
.catch(error => {
  console.error('방 퇴장 실패 ' + error);
  // 복구가 불가능한 오류, 페이지 새로고침
});
```

>! 각 엔드는 appScene에서 통일되어야 합니다. 그렇지 않으면 예기치 않은 문제가 발생할 수 있습니다.
