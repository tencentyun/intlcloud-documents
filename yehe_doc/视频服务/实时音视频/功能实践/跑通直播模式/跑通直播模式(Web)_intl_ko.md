본문은 시청자로서 라이브 룸에 입장해 마이크 연결 인터랙션을 시작하는 시나리오를 소개합니다. 호스트로서 라이브 방송을 진행하는 시나리오는 TRTC 통화 시나리오와 동일하게 [TRTC 통화](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-11-basic-video-call.html)를 참고하십시오.

## 1단계: Client 객체 생성 

[TRTC.createClient()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#.createClient)를 통해 [Client](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html) 객체를 생성합니다. 매개변수 설정은 다음과 같습니다.

- `mode`: 대화형 라이브 방송 모드. 설정값: `live`
- `sdkAppId`: Tencent Cloud에 신청한 sdkAppId
- `userId`: 사용자 ID
- `userSig`: 사용자 서명

<dx-codeblock>
::: javascript javascript
const client = TRTC.createClient({
  mode: 'live',
  sdkAppId,
  userId,
  userSig
});
:::
</dx-codeblock>

## 2단계: 시청자로서 라이브 방송 방 입장

[Client.join()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#join)을 호출하여 멀티미디어 통화 방에 입장합니다. 매개변수 설정은 다음과 같습니다.

- `roomId`: 방 ID
- `role`: 사용자 역할
  - `anchor`: 호스트. 호스트에게는 로컬 스트림 배포와 원격 스트림 수락 권한이 있습니다. 기본값은 호스트 역할입니다.
  - `audience`: 시청자. 시청자에게는 원격 스트림 수락 권한만 있고, 로컬 스트림 배포 권한은 없습니다. 시청자가 호스트와 마이크 연결로 인터랙션하려면 [Client.switchRole()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#switchRole)을 통해 역할을 `anchor` 호스트로 전환한 후 로컬 스트림을 배포해야 합니다.

<dx-codeblock>
::: javascript javascript
// 시청자 역할로 입장 후 시청
client
  .join({ roomId, role: 'audience' })
  .catch(error => {
    console.error('입장 실패' + error);
  })
  .then(() => {
    console.log('입장 성공');
  });
:::
</dx-codeblock>

## 3단계: 라이브 방송 시청
1. 원격 스트림은 리스너를 통해 `client.on('stream-added')`이벤트를 획득합니다. 해당 이벤트를 받은 후 [Client.subscribe()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#subscribe)를 통해 원격 멀티미디어 스트림을 구독합니다.
>?[Client.join()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#join) 방 입장 전 `client.on('stream-added')` 이벤트를 등록하면 원격 사용자의 입장 알림을 놓치지 않을 수 있습니다.

<dx-codeblock>
::: javascript javascript
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
:::
</dx-codeblock>
2. 원격 스트리밍 구독 성공 이벤트 콜백에서 [Stream.play()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Stream.html#play)를 호출하여 인터넷 홈페이지에서 멀티미디어를 재생합니다. `play` 방법은 div 요소 ID를 매개변수로 받습니다. SDK 내부에서는 해당 div 요소 하위에서 상응하는 멀티미디어 태그를 자동으로 생성하고 그 위에서 멀티미디어를 재생합니다.
<dx-codeblock>
::: javascript javascript
client.on('stream-subscribed', event => {
    const remoteStream = event.stream;
    console.log('원격 스트림 구독 성공:' + remoteStream.getId());
    // 원격 스트림 재생
    remoteStream.play('remote_stream-' + remoteStream.getId());
});
:::
</dx-codeblock>

## 4단계: 호스트와의 마이크 연결 인터랙션

### 4.1단계: 역할 전환

[Client.switchRole()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#switchRole)을 사용해 `anchor` 호스트 역할로 전환합니다.
<dx-codeblock>
::: javascript javascript
client
  .switchRole('anchor')
  .catch(error => {
    console.error('역할 전환 실패 ' + error);
  })
  .then(() => {
    // 역할 전환 성공, 현재 호스트 역할
  });
:::
</dx-codeblock>

### 4.2단계: 마이크 연결 인터랙션

1. [TRTC.createStream()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#.createStream)을 사용해 로컬 멀티미디어 스트림을 생성합니다. 아래의 인스턴스는 카메라 및 마이크에서 수집한 멀티미디어 스트림입니다. 매개변수 설정은 다음과 같습니다.
 - `userId`: 로컬 스트림 소속 사용자 ID
 - `audio`: 오디오 활성화 여부
 - `video`: 비디오 활성화 여부

 ```javascript
const localStream = TRTC.createStream({ userId, audio: true, video: true });
 ```
2. [LocalStream.initialize()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#initialize)를 호출하여 로컬 멀티미디어 스트림을 초기화합니다.
<dx-codeblock>
::: javascript javascript
localStream
    .initialize()
    .catch(error => {
    console.error('로컬 스트림 초기화 실패 ' + error);
    })
    .then(() => {
    console.log('로컬 스트림 초기화 성공');
    });
:::
</dx-codeblock>
3. 로컬 스트림 초기화에 성공하면 로컬 스트림이 재생됩니다.
<dx-codeblock>
::: javascript javascript
localStream
    .initialize()
    .catch(error => {
    console.error('로컬 스트림 초기화 실패 ' + error);
    })
    .then(() => {
    console.log('로컬 스트림 초기화 성공');
    localStream.play('local_stream');
    });
:::
</dx-codeblock>
4. 로컬 스트림 초기화 성공 후, [Client.publish()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#publish)를 호출하여 로컬 스트림을 배포하고 시청자와 마이크 연결 인터랙션을 시작합니다.
<dx-codeblock>
::: javascript javascript
client
    .publish(localStream)
    .catch(error => {
    console.error('로컬 스트리밍 배포 실패 ' + error);
    })
    .then(() => {
    console.error('로컬 스트리밍 배포 성공' + error);
    });
:::
</dx-codeblock>

## 5단계: 라이브 방송 방 종료

라이브 방송 종료 시 [Client.leave()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#leave)를 호출하여 라이브 방송 방을 종료하면 라이브 세션 전체가 종료됩니다.
<dx-codeblock>
::: javascript javascript
client
  .leave()
  .catch(error => {
    console.error('퇴장 실패 ' + error);
  })
  .then(() => {
    // 퇴장 성공
  });
:::
</dx-codeblock>

>! appScene의 값은 각 클라이언트에서 동일해야 합니다. 그렇지 않을 경우 예상치 못한 문제가 발생할 수 있습니다.
