본 문서에서는 화면 공유의 사용 방법을 소개합니다.
>!화면 공유는 Chrome M72+만 지원합니다.

## 화면 공유 스트림 생성과 배포

```
// 화면 공유 스트림 생성
const localStream = TRTC.createStream({ audio: false, screen: true });
// 리스너 화면 공유 중지 이벤트
localStream.on('screen-sharing-stopped', event => {
  console.log('screen sharing was stopped');
});

// 화면 공유 스트림 초기화
localStream.initialize().then(() => {
  console.log('screencast stream init success');
  // 화면 공유 스트림 배포
  client.publish(localStream).then(() => {
    console.log('screen casting');
  });
});
```

## 화면 공유 속성

화면 공유 속성은 해상도, 프레임 레이트, 비트 레이트가 있으며 {@link LocalStream#setScreenProfile setScreenProfile()} 인터페이스에서 속성 Profile을 지정할 수 있습니다. 각 Profile은 한 그룹의 해상도, 프레임 레이트, 비트레이트에 대응되며, 사용자 정의 해상도, 프레임 레이트, 비트레이트를 사용할 수도 있습니다. 화면 공유는 기본적으로 '1080p' Profile을 사용합니다.

- 속성 Profile 지정:
```
const localStream = TRTC.createStream({ audio: false, screen: true });
localStream.setScreenProfile('1080p');
localStream.initialize().then(() => {
  // screencast stream init success
});
```

- 사용자 정의 해상도, 프레임 레이트, 비트 레이트 사용:
```
const localStream = TRTC.createStream({ audio: false, screen: true });
localStream.setScreenProfile({ width: 1920, height: 1080, frameRate: 5, bitrate: 1600 /* kbps */});
localStream.initialize().then(() => {
  // screencast stream init success
});
```

화면 공유 속성 권장 리스트:

| profile | 해상도(너비x높이) | 프레임 레이트(fps) | 비트 레이트(kbps) |
| :------ | :---------------- | :---------- | :---------- |
| 480p    | 640 x 480         | 5           | 900         |
| 480p_2  | 640 x 480         | 30          | 1000        |
| 720p    | 1280 x 720        | 5           | 1200        |
| 720p_2  | 1280 x 720        | 30          | 3000        |
| 1080p   | 1920 x 1080       | 5           | 1600        |
| 1080p_2 | 1920 x 1080       | 30          | 4000        |



## 카메라 비디오와 화면 공유 동시 푸시

한 {@link Client Client}는 최대 동시에 한 채널의 오디오와 한 채널의 비디오를 푸시할 수 있습니다. 동시에 카메라 비디오와 화면 공유를 푸시하고 싶을 경우에는 화면 공유 푸시 전용으로 다른 독립적인 Client를 생성할 수 있습니다.

```
// 독립 사용자의 ID를 사용해 푸시 화면 공유를 진행합니다.
const shareId = 'share-userId';
const shareClient = TRTC.createClient({ mode: 'rtc', sdkAppId, userId, shareId, userSig });

// 해당 shareClient가 기본적으로 원격 스트림을 수락하지 않는다는 의미(화면 공유 스트림만 담당)
shareClient.setDefaultMuteRemoteStreams(true);
shareClient.join({ roomId }).then(() => {
  console.log('shareClient join success');
  // 화면 공유 스트림 생성
  const localStream = TRTC.createStream({ audio: false, screen: true });
  localStream.initialize().then(() => {
    // screencast stream init success
    shareClient.publish(localStream).then(() => {
      console.log('screen casting');
    });
  });
});

// 메인 Client 중 shareId 구독 취소를 지정한 원격 스트림
client.on('stream-added', event => {
  const remoteStream = event.stream;
  const remoteUserId = remoteStream.getUserId();
  if (remoteUserId === shareId) {
    // 자신의 화면 공유 스트림 구독 취소
    client.unsubscribe(remoteStream);
  } else {
    // 기타 일반 원격 스트림 구독
    client.subscribe(remoteStream);
  }
});
```
