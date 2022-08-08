본문은 영상 통화 또는 라이브 스트리밍 세션의 이미지 화질을 설정하는 방법을 설명합니다. 더 나은 사용자 경험을 제공하기 위해 비디오 화질 및 원활성에 대한 요구 사항에 따라 속성을 설정할 수 있습니다.
비디오 속성에는 해상도, 프레임 레이트 및 비트 레이트가 포함됩니다.

## 구현 방식

Stream 객체의 `{@link LocalStream#setVideoProfile setVideoProfile()}`을 호출하여 비디오 속성을 설정할 수 있습니다.

- 권장 해상도, 프레임 레이트 및 비트 레이트 집합에 해당하는 미리 정의된 Profile 사용.
```
const localStream = TRTC.createStream({ userId, audio: true, video: true });
// Profile을 ‘480p’로 설정
localStream.setVideoProfile('480p');

localStream.initialize().then(() => {
  console.log('local stream init success');
  localStream.play('local_stream');
});
```

- 사용자 정의 해상도, 프레임 레이트, 비트 레이트 지정
```
const localStream = TRTC.createStream({ userId, audio: true, video: true });
// 해상도, 프레임 레이트 및 비트 레이트 값 지정
localStream.setVideoProfile({ width: 640, height: 480, frameRate: 15, bitrate: 900 /* kpbs */});

localStream.initialize().then(() => {
  console.log('local stream init success');
  localStream.play('local_stream');
});
```

> !
> - v4.8.4 이상 버전에서는 `{@link LocalStream#setVideoProfile setVideoProfile()}`을 호출하여 통화 중 실시간으로 비디오 설정을 변경할 수 있습니다. 자세한 내용은 `{@link LocalStream#setVideoProfile setVideoProfile()}` API 설명을 참고하십시오
> - v4.8.4 이전 버전에서는 `{@link LocalStream#setVideoProfile setVideoProfile()}`을 호출하여 로컬 스트림을 초기화하기 전에 `{@link LocalStream#initialize initialize()}`를 호출해야 합니다. 통화 중에는 영상 설정을 변경할 수 없습니다.

## 비디오 Profile

| 비디오 profile | 해상도(너비 × 높이) | 프레임 레이트(fps) | 비트 레이트(kbps) |
| :----------- | :---------------- | :---------- | :----------- |
| 120p         | 160 × 120         | 15          | 200          |
| 180p         | 320 × 180         | 15          | 350          |
| 240p         | 320 × 240         | 15          | 400          |
| 360p         | 640 × 360         | 15          | 800          |
| 480p         | 640 × 480         | 15          | 900          |
| 720p         | 1280 × 720        | 15          | 1500         |
| 1080p        | 1920 × 1080       | 15          | 2000         |
| 1440p        | 2560 × 1440       | 30          | 4860         |
| 4K           | 3840 × 2160       | 30          | 9000         |

Profile의 목표 해상도는 장치 및 브라우저 제한으로 인해 구현이 불가능할 수도 있습니다. 이 경우 브라우저는 목표에 최대한 가깝게 해상도를 조정합니다.
