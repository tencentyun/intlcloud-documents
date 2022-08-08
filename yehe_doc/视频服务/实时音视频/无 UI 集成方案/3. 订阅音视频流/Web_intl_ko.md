본 문서는 방에 있는 다른 사용자의 오디오/비디오 스트림을 구독하는 방법, 즉 다른 사용자의 오디오/비디오를 재생하는 방법을 설명합니다. 편의상 이 문서에서는 ‘방에 있는 다른 사용자’를 ‘원격 사용자’라고 합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/c8ae41656c97fe546b9c4b0b857b0746.png)

TRTC Web SDK를 사용하다 보면 종종 다음과 같은 객체를 접하게 됩니다.
- Client 객체는 로컬 클라이언트를 말합니다. [Client](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html) 타입으로 통화방 추가, 로컬 스트림 배포, 원격 스트림 구독 등 기능을 제공합니다.
- Stream 객체는 멀티미디어 스트림 객체를 말하며, 로컬 멀티미디어 스트림 객체 [LocalStream](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html)와 원격 멀티미디어 스트림 객체 [RemoteStream](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/RemoteStream.html)로 나뉩니다. Stream 타입은 오디오 및 비디오의 재생과 관련한 멀티미디어 스트림 객체 행위를 지원합니다.

## 1단계: Client 객체 생성
[방 입장-1단계](https://cloud.tencent.com/document/product/647/74636#step1) 문서를 참고하여 client를 생성할 수 있습니다.

Client를 생성할 때 구독 모드를 지정할 수 있습니다. TRTC는 두 가지 구독 모드를 제공합니다.
 - 자동 구독, stream-added 알림을 수신하면 SDK가 원격 스트림 수신 및 디코딩을 시작합니다. SDK의 기본 모드입니다.
 - 수동 구독, 화면 공유 client는 스트림을 게시만 하고 스트림을 수신하지 않습니다. 따라서 화면 공유 client의 경우 수동 구독 모드를 사용하십시오.

```javascript
const client = TRTC.createClient({
  ...,
  autoSubscribe: false // 기본값은 true(자동 구독)
});
```

## 2단계: 새로운 원격 스트림 수신 및 구독
[Client.on('stream-added')](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/module-Event.html#.STREAM_ADDED) 이벤트를 수신하여 방에서 원격 스트림을 얻을 수 있습니다. 이 이벤트를 수신하면 원격 스트림을 구독할 수 있고 이벤트 콜백에서 [Client.subscribe()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#subscribe)를 통해 원격 멀티미디어 스트림을 구독합니다.

```javascript
client.on('stream-added', event => {
  const remoteStream = event.stream;
  console.log('원격 스트림 추가: ' + remoteStream.getId());
  //원격 스트림 구독
  client.subscribe(remoteStream);
});
```
>!
>- 방에서 사용 가능한 모든 스트림에 대한 알림을 받으려면 방 입장 전에 [Client.on('stream-added')](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/module-Event.html#.STREAM_ADDED)을 등록해야 합니다.
>- 원격 스트림 퇴장 등 다른 이벤트는 [API 소개 문서](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/module-Event.html)에서 확인할 수 있습니다.


## 3단계: 구독 성공 이벤트 수신 및 원격 스트림 재생
원격 스트림에 대한 성공적인 구독을 나타내는 콜백에서 [Stream.play()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Stream.html#play)를 호출하여 스트림을 재생합니다. 'play' 메소드가 div 요소 ID 또는 HTMLDivElement 객체를 API에 전달하면 SDK가 div 요소에 멀티미디어 태그를 생성하고 스트림을 재생합니다.

'play' API의 매개변수에 대한 자세한 내용은 [Stream.play()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Stream.html#play)를 참고하십시오. 

```javascript
client.on('stream-subscribed', event => {
  const remoteStream = event.stream;
  console.log('원격 스트림 구독 성공:' + remoteStream.getId());
  // 원격 스트림 재생
  remoteStream.play('remote-stream-' + remoteStream.getId());
});
```
브라우저의 [자동 재생 정책](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-21-advanced-auto-play-policy.html)으로 인해 'play' 호출 시 PLAY_NOT_ALLOWED 오류가 발생할 수 있습니다. 이러한 경우 SDK는 사용자에게 팝업 창을 표시합니다. 사용자의 허가를 받은 후 SDK는 API를 호출하여 재생을 재개합니다.

또한 고유한 사용자 상호 작용 논리를 구현하고 사용자의 클릭/탭 이벤트 후 [Stream.resume()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Stream.html#resume)을 호출하여 재생을 재개할 수 있습니다. 이러한 경우 [TRTC.createClient()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#createClient) 의 enableAutoPlayDialog 매개변수를 false로 설정해야 합니다.

```javascript
client.on('stream-subscribed', event => {
  const remoteStream = event.stream;
  console.log('원격 스트림 구독 성공:' + remoteStream.getId());
  // remoteStream의 0x4043 error를 수신
  remoteStream.on('error', error => {
    const errorCode = error.getCode();
    if (errorCode === 0x4043) {
      // PLAY_NOT_ALLOWED 오류가 발생하면 UI에 창을 표시하고 사용자의 클릭/탭 이벤트 후 stream.resume을 호출하여 재생 재개
      // remoteStream.resume()
    }
  });
  // 원격 스트림 재생
  remoteStream.play('remote-stream-' + remoteStream.getId());
});
```

## 4단계: 영상 통화방 입장
Client.join()을 호출하여 방에 입장합니다. 자세한 안내는 [방 입장-2단계](https://cloud.tencent.com/document/product/647/74636#step2)를 참고하십시오.

## 완전한 코드

```javascript

const client = TRTC.createClient({
  mode: 'rtc',
  sdkAppId,
  userId,
  userSig
});

client.on('stream-added', event => {
  const remoteStream = event.stream;
  console.log('원격 스트림 추가: ' + remoteStream.getId());
  //원격 스트림 구독
  client.subscribe(remoteStream);
});

client.on('stream-subscribed', event => {
  const remoteStream = event.stream;
  console.log('원격 스트림 구독 성공:' + remoteStream.getId());
  // remoteStream의 0x4043 error 수신
  remoteStream.on('error', error => {
    const errorCode = error.getCode();
    if (errorCode === 0x4043) {
      // PLAY_NOT_ALLOWED 오류가 발생하면 UI에 창을 표시하고 사용자의 클릭/탭 이벤트 후 stream.resume을 호출하여 재생을 재개
      // remoteStream.resume()
    }
  });
  // 원격 스트림 재생
  remoteStream.play('remote-stream-' + remoteStream.getId());
});

try {
  await client.join({ roomId });
  console.log('입장 성공');
} catch (error) {
  console.error('입장 실패, 나중에 다시 시도하십시오' + error);
}
```