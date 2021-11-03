본 문서에서는 화면 공유의 사용 방법을 소개합니다.
>!화면 공유는 Chrome M72+만 지원합니다.

## 화면 공유 스트림 생성과 배포

<dx-codeblock>
::: 화면 공유 스트림 
// 화면 공유 스트림 생성
const localStream = TRTC.createStream({ audio: false, screen: true });
// 화면 공유 중지 이벤트 수신
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
:::
</dx-codeblock>

## 화면 공유 속성

화면 공유 속성은 해상도, 프레임 레이트, 비트 레이트가 있으며 {@link LocalStream#setScreenProfile setScreenProfile()} 인터페이스에서 속성 Profile을 지정할 수 있습니다. 각 Profile은 한 그룹의 해상도, 프레임 레이트, 비트레이트에 대응되며, 사용자 정의 해상도, 프레임 레이트, 비트레이트를 사용할 수도 있습니다. 화면 공유는 기본적으로 '1080p' Profile을 사용합니다.

- 속성 Profile 지정:
<dx-codeblock>
::: Profile 
const localStream = TRTC.createStream({ audio: false, screen: true });
localStream.setScreenProfile('1080p');
localStream.initialize().then(() => {
		// screencast stream init success
});
:::
</dx-codeblock>
- 사용자 정의 해상도, 프레임 레이트, 비트 레이트 사용:
<dx-codeblock>
::: 사용자 정의 해상도 
const localStream = TRTC.createStream({ audio: false, screen: true });
localStream.setScreenProfile({ width: 1920, height: 1080, frameRate: 5, bitrate: 1600 /* kbps */});
localStream.initialize().then(() => {
		// screencast stream init success
});
:::
</dx-codeblock>

화면 공유 속성 권장 리스트:

| profile | 해상도(너비 × 높이) | 프레임 레이트(fps) | 비트 레이트(kbps) |
| :------ | :---------------- | :---------- | :---------- |
| 480p    | 640 × 480         | 5           | 900         |
| 480p_2  | 640 × 480         | 30          | 1000        |
| 720p    | 1280 × 720        | 5           | 1200        |
| 720p_2  | 1280 × 720        | 30          | 3000        |
| 1080p   | 1920 × 1080       | 5           | 1600        |
| 1080p_2 | 1920 × 1080       | 30          | 4000        |



## 카메라 영상과 화면 공유 동시 푸시

한 {@link Client Client}는 최대 동시에 한 채널의 오디오와 한 채널의 비디오를 푸시할 수 있습니다. 동시에 카메라 비디오와 화면 공유를 푸시하고 싶을 경우에는 화면 공유 푸시 전용으로 다른 독립적인 Client를 생성할 수 있습니다.


<dx-codeblock>
::: client 
// 독립적인 사용자 ID를 사용하여 푸시 화면 공유
const shareId = 'share-userId';
const shareClient = TRTC.createClient({ mode: 'rtc', sdkAppId, userId, shareId, userSig });

// 이 shareClient가 원격 스트림을 수신하지 않도록 지정(화면 공유 스트림 전송만 담당) 
shareClient.on('stream-added', event => {
  const remoteStream = event.stream;
  shareClient.unsubscribe(remoteStream);
});
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
:::
</dx-codeblock>
