본 문서는 앵커가 오디오/비디오 스트림을 게시하는 방법을 설명합니다. ‘게시’는 마이크와 카메라를 켜서 오디오를 듣고 비디오를 방의 다른 사용자에게 표시하는 것을 의미합니다.

![](https://qcloudimg.tencent-cloud.cn/raw/3f49218df6a0cc1a106f9a61c23fdb98.png)

TRTC Web SDK를 사용하다 보면 종종 다음과 같은 객체를 접하게 됩니다.
- Client 객체는 로컬 클라이언트를 말합니다. [Client](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html) 타입으로 통화방 추가, 로컬 스트림 배포, 원격 스트림 구독 등 기능을 제공합니다.
- Stream 객체는 멀티미디어 스트림 객체를 말하며, 로컬 멀티미디어 스트림 객체 [LocalStream](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html)과 원격 멀티미디어 스트림 객체 [RemoteStream](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/RemoteStream.html)으로 나뉩니다. Stream 타입은 오디오 및 비디오의 재생과 관련한 멀티미디어 스트림 객체 행위를 지원합니다.

[](id:step1)
## 1단계: 방 입장
Client 객체를 만들고 방에 입장합니다. 자세한 안내는 [방 입장](https://intl.cloud.tencent.com/document/product/647/48424)을 참고하십시오.


[](id:step2)
## 2단계: 로컬 스트림 생성
[TRTC.createStream()](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/TRTC.html#createStream)을 호출하여 로컬 멀티미디어 스트림을 생성합니다. 매개변수 설정:

| 매개변수 | 설명 | 참고 | 데이터 유형 | 예시 | 기본값 |
|---------|---------|---------|---------|---------|---------|
| userId | 사용자 ID | 이 매개변수는 필수이며 Client를 생성할 때 전달한 userId와 동일해야 합니다 | string | “denny” 또는 “123321”| - |
| audio | 오디오 캡처 여부 | 이 매개변수는 필수입니다. 마이크에서 오디오를 캡처할지 선택합니다 | boolean | true |  - |
| video | 비디오 캡처 여부 | 이 매개변수는 필수입니다. 카메라에서 비디오를 캡처할지 선택합니다 | boolean | true |  - |

매개변수에 대한 자세한 내용은 [TRTC.createStream()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#createStream)을 참고하십시오. 

```javascript
const localStream = TRTC.createStream({ userId, audio: true, video: true });
```

로컬 스트림을 게시하기 전에 [LocalStream.initialize()](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#initialize)를 호출하여 스트림을 초기화합니다.
초기화하는 동안 SDK는 카메라와 마이크를 사용할 수 있는 권한을 요청합니다. 브라우저에서 요청하면 권한을 허용합니다.

초기화 성공 콜백에서 [LocalStream.play()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#play)를 호출하여 멀티미디어를 로컬에서 재생합니다.

```javascript
// Promise 구문 사용
localStream
  .initialize()
  .then(() => {
    console.log('로컬 스트림 초기화 성공');
    localStream.play('local_stream');
  })
  .catch(error => {
    console.error('로컬 스트림 초기화 실패 ' + error);
  });

// async/await 구문 사용 권장
try {
  await localStream.initialize();
  localStream.play('local_stream');
  console.log('로컬 스트림 초기화 성공');
} catch (error) {
  console.error('로컬 스트림 초기화 실패 ' + error);
}
```


[](id:step3)
## 3단계: 로컬 스트림 게시
로컬 스트림이 초기화된 후, [Client.publish()](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#publish)를 호출하여 게시합니다.
```javascript
// Promise 구문 사용
client
  .publish(localStream)
  .then(() => {
    console.error('로컬 스트림 배포 성공' + error);
  })
  .catch(error => {
    console.error('로컬 스트림 배포 실패 ' + error);
  });

// async/await 구문 사용 권장
try {
  await client.publish(localStream);
  console.error('로컬 스트림 배포 성공' + error);
} catch (error) {
  console.error('로컬 스트림 배포 실패 ' + error);
}
```

## 완전한 코드
```javascript
const client = TRTC.createClient({
  mode: 'rtc',
  sdkAppId,
  userId,
  userSig
});
const localStream = TRTC.createStream({ userId, audio: true, video: true });

try {
  await client.join({ roomId });
  console.log('입장 성공');
} catch (error) {
  console.error('입장 실패, 나중에 다시 시도하십시오' + error);
}

try {
  await localStream.initialize();
  localStream.play('local_stream');
  console.log('로컬 스트림 초기화 성공');
} catch (error) {
  console.error('로컬 스트림 초기화 실패 ' + error);
}

try {
  await client.publish(localStream);
  console.error('로컬 스트림 배포 성공' + error);
} catch (error) {
  console.error('로컬 스트림 배포 실패 ' + error);
}
```