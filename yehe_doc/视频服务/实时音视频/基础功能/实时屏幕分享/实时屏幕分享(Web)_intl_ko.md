TRTC Web SDK 화면 공유 지원은 [브라우저 지원 상황](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-05-info-browser.html)을 확인하십시오. SDK는 [TRTC.isScreenShareSupported](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/TRTC.html#.isScreenShareSupported) 인터페이스를 제공하여 현재 브라우저의 화면 공유 지원 여부를 판단합니다.
본 문에서는 다음과 같은 다양한 시나리오를 통해 구현 프로세스를 소개합니다.

> !
> - Web은 현재 서브스트림 배포를 지원하지 않습니다. 화면 공유 배포는 메인 스트림을 통해 구현됩니다. 원격 화면 공유 스트림 출처가 Web 사용자인 경우 [RemoteStream.getType()](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/RemoteStream.html#getType)의 반환 값은 'main'이며 일반적으로 userId는 Web에서 화면 공유 스트림을 식별하는 데 사용됩니다.
> - Native(iOS, Android, Mac, Windows 등)는 서브스트림 배포를 지원하며 화면 공유 배포는 서브스트림 배포를 통해 구현됩니다. 원격 화면 공유 스트림 출처가 Native 사용자인 경우 [RemoteStream.getType()](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/RemoteStream.html#getType)의 반환 값은 'auxiliary'입니다.

## 화면 공유 스트림 생성과 배포
>!아래의 순서를 정확히 따라 화면 공유 스트림 코드를 생성 및 배포하십시오.

### 1단계: 화면 공유를 담당하는 클라이언트 객체 생성
일반적으로 userId에 'share_'를 접두사로 붙여 이를 화면 공유 클라이언트 객체로 식별하는 것이 좋습니다.

<dx-codeblock>
:::javascript
const shareClient = TRTC.createClient({
  mode: 'rtc',
  sdkAppId,
  userId, // 예시: ‘share_teacher’
  userSig
});
// 클라이언트 객체 방 입장
try {
  await shareClient.join({ roomId });
  // ShareClient join room success
} catch (error) {
  // ShareClient join room failed
}

:::
</dx-codeblock>

### 2단계: 화면 공유 스트림 생성
화면 공유 스트림에는 비디오 스트림과 오디오 스트림이 포함됩니다. 오디오 스트림은 마이크 오디오 또는 시스템 오디오로 분류됩니다.
<dx-codeblock>
:::javascript
// Good 정확한 사용법
// 화면 비디오 스트림만 캡처
const shareStream = TRTC.createStream({ audio: false, screen: true, userId });
// or 마이크 오디오 및 화면 비디오 스트림 캡처
const shareStream = TRTC.createStream({ audio: true, screen: true, userId });
// or 시스템 오디오 및 화면 비디오 스트림 캡처
const shareStream = TRTC.createStream({ screenAudio: true, screen: true, userId });

// Bad 오류 사용법
const shareStream = TRTC.createStream({ camera: true, screen: true });
// or
const shareStream = TRTC.createStream({ camera: true, screenAudio: true });

:::
</dx-codeblock>

>! 
>- audio와 screenAudio 속성은 동시에 true로 설정할 수 없으며, camera와 screenAudio 속성도 동시에 true로 설정할 수 없습니다. screenAudio에 대한 자세한 정보는 본 문의 Part 5에서 소개됩니다.
>- camera와 screen 속성은 동시에 true로 설정할 수 없습니다.

### 3단계: 화면 공유 스트림 초기화
초기화 시 브라우저는 사용자에게 화면 공유 콘텐츠 및 권한을 요청합니다. 사용자가 권한 부여를 거부하거나 시스템이 브라우저 화면 공유 권한을 부여하지 않으면 코드는 'NotReadableError' 또는 'NotAllowedError' 오류를 캐치합니다. 이 때 사용자가 브라우저 설정 또는 시스템 설정을 수행하여 화면 공유 권한을 활성화하도록 안내해야 합니다.
<dx-codeblock>
:::javascript
try {
  await shareStream.initialize();
} catch (error) {
  // 화면 공유 스트림 초기화 실패 시 사용자에게 알리고 후속 방 입장 배포 프로세스 중지
  switch (error.name) {
    case 'NotReadableError':
      // 시스템에서 현재 브라우저가 화면 내용을 가져올 수 있도록 사용자에게 알림
      return;
    case 'NotAllowedError':
      if (error.message.includes('Permission denied by system')) {
        // 시스템에서 현재 브라우저가 화면 내용을 가져올 수 있도록 사용자에게 알림
      } else {
        // 사용자가 화면 공유를 거부/취소
      }
      return;
    default:
      // 화면 공유 스트림을 초기화할 때 알 수 없는 오류가 발생했으며 사용자에게 다시 시도하라는 메시지가 표시됨
      return;
  }
}
:::
</dx-codeblock>

### 4단계: 화면 공유 스트림 배포
첫 번째 단계에서 생성한 클라이언트 객체를 통해 배포합니다. 배포가 성공한 후 원격 화면 공유 스트림을 수신할 수 있습니다.
<dx-codeblock>
:::javascript
try {
  await shareClient.publish(shareStream);
} catch (error) {
  // ShareClient failed to publish local stream
}
:::
</dx-codeblock>

### 완전한 코드
<dx-codeblock>
:::javascript
const shareClient = TRTC.createClient({
  mode: 'rtc',
  sdkAppId,
  userId, // 예시: ‘share_teacher’
  userSig
});
// 클라이언트 객체 방 입장
try {
  await shareClient.join({ roomId });
  // ShareClient join room success
} catch (error) {
  // ShareClient join room failed
}
// 화면 비디오 스트림만 캡처
const shareStream = TRTC.createStream({ audio: false, screen: true, userId });
// or 마이크 오디오 및 화면 비디오 스트림 캡처
// const shareStream = TRTC.createStream({ audio: true, screen: true, userId });
// or 시스템 오디오 및 화면 비디오 스트림 캡처
// const shareStream = TRTC.createStream({ screenAudio: true, screen: true, userId });
try {
  await shareStream.initialize();
} catch (error) {
  // 화면 공유 스트림 초기화 실패 시 사용자에게 알리고 후속 방 입장 배포 프로세스 중지
  switch (error.name) {
    case 'NotReadableError':
      // 시스템에서 현재 브라우저가 화면 내용을 가져올 수 있도록 사용자에게 알림
      return;
    case 'NotAllowedError':
      if (error.message.includes('Permission denied by system')) {
        // 시스템에서 현재 브라우저가 화면 내용을 가져올 수 있도록 사용자에게 알림
      } else {
        // 사용자가 화면 공유를 거부/취소
      }
      return;
    default:
      // 화면 공유 스트림을 초기화할 때 알 수 없는 오류가 발생했으며 사용자에게 다시 시도하라는 메시지 표시됨
      return;
  }
}
try {
  await shareClient.publish(shareStream);
} catch (error) {
  // ShareClient failed to publish local stream
}
:::
</dx-codeblock>

## 화면 공유 매개변수 설정
설정할 수 있는 매개변수는 해상도, 프레임 레이트 및 비트 레이트를 포함하며, 필요에 따라 [setScreenProfile()](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#setScreenProfile) 인터페이스를 통해 profile을 지정할 수 있으며, 각 profile은 해상도, 프레임 레이트 및 비트 레이트에 해당합니다. SDK는 기본적으로 '1080p' 설정을 사용합니다.

<dx-codeblock>
:::javascript
const shareStream = TRTC.createStream({ audio: false, screen: true, userId });
// setScreenProfile()은 initialize() 전에 호출되어야 합니다.
shareStream.setScreenProfile('1080p');
await shareStream.initialize();
:::
</dx-codeblock>

또는 사용자 정의 해상도, 프레임 레이트, 비트 레이트 사용:

<dx-codeblock>
:::javascript
const shareStream = TRTC.createStream({ audio: false, screen: true, userId });
// setScreenProfile()은 initialize() 전에 호출되어야 합니다.
shareStream.setScreenProfile({ width: 1920, height: 1080, frameRate: 5, bitrate: 1600 /* kbps */});
await shareStream.initialize();
:::
</dx-codeblock>
화면 공유 속성 권장 리스트:

| profile | 해상도(너비x높이) | 프레임 레이트(fps) | 비트 레이트(kbps) |
|:--------|:----------------|:----------|:------------|
| 480p    | 640 x 480         | 5           | 900         |
| 480p_2  | 640 x 480         | 30          | 1000        |
| 720p    | 1280 x 720        | 5           | 1200        |
| 720p_2  | 1280 x 720        | 30          | 3000        |
| 1080p   | 1920 x 1080       | 5           | 1600        |
| 1080p_2 | 1920 x 1080       | 30          | 4000        |

>! 너무 높은 매개변수를 설정하면 예상치 못한 문제가 발생할 수 있으므로 권장 매개변수에 따라 설정하는 것이 좋습니다.

## 화면 공유 종료

<dx-codeblock>
:::javascript
// 화면 공유 클라이언트 배포 스트림 취소
await shareClient.unpublish(shareStream);
// 화면 공유 스트림 비활성화
shareStream.close();
// 화면 공유 클라이언트 방 퇴장
await shareClient.leave();

// 상기 세 단계는 선택사항이며 시나리오의 필요에 따라 필요한 코드를 실행할 수 있습니다. 일반적으로 방 입장 여부와 스트림 해제 여부에 대한 판단을 추가해야 합니다. 자세한 내용은 코드 예시는 [demo 소스 코드](https://github.com/LiteAVSDK/TRTC_Web/blob/main/base-js/js/share-client.js)를 참고하십시오.
:::
</dx-codeblock>

또한 사용자는 브라우저와 함께 제공되는 버튼을 통해 화면 공유를 중지할 수도 있으므로 화면 공유 스트림은 화면 공유 중지 이벤트를 수신하고 이에 따라 처리해야 합니다.


<dx-codeblock>
:::javascript
// 화면 공유 스트림의 화면 공유 중지 이벤트 수신
shareStream.on('screen-sharing-stopped', event => {
  // 화면 공유 클라이언트의 스트림 푸시 중지
  await shareClient.unpublish(shareStream);
  // 화면 공유 스트림 비활성화
  shareStream.close();
  // 화면 공유 클라이언트 방 퇴장
  await shareClient.leave();
});
:::
</dx-codeblock>

## 카메라 영상과 화면 공유 동시 배포
클라이언트는 동시에 하나의 오디오와 하나의 비디오만 배포할 수 있습니다. 카메라 영상과 화면 공유를 동시에 배포하려면 두 개의 Client를 생성하고 ‘각각의 역할을 수행’하도록 해야 합니다.
예를 들어 다음과 같이 두 개의 Client 생성:
- **클라이언트**: 로컬 멀티미디어 스트림 배포 및 shareClient를 제외한 모든 원격 스트림 구독을 담당합니다.
- **shareClient**: 화면 공유 스트림 게시를 담당하고 원격 스트림을 구독하지 않습니다.

>! 
>- 화면 공유를 담당하는 shareClient는 자동 구독을 비활성화해야 합니다. 그렇지 않으면 원격 스트림에 대한 반복 구독이 발생합니다. [API 설명](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/TRTC.html#createClient)을 참고하십시오.
>- 로컬 멀티미디어 스트림 배포를 담당하는 client는 shareClient에서 배포한 스트림의 구독을 취소해야 합니다. 그렇지 않으면 스스로 구독하는 상황이 발생합니다.

예시 코드:
<dx-codeblock>
:::javascript
const client = TRTC.createClient({ mode: 'rtc', sdkAppId, userId, userSig });
// 원격 스트림에 대한 자동 구독을 비활성화하려면 shareClient를 설정해야 합니다. 즉: autoSubscribe: false
const shareClient = TRTC.createClient({ mode: 'rtc', sdkAppId, `share_${userId}`, userSig, autoSubscribe: false,});

// 로컬 멀티미디어 스트림 배포를 담당하는 client는 shareClient에서 배포한 스트림의 구독을 취소해야 합니다.
client.on('stream-added', event => {
  const remoteStream = event.stream;
  const remoteUserId = remoteStream.getUserId();
  if (remoteUserId === `share_${userId}`) {
    // 자신의 화면 공유 스트림 구독 취소
    client.unsubscribe(remoteStream);
  } else {
    // 기타 일반 원격 스트림 구독
    client.subscribe(remoteStream);
  }
});

await client.join({ roomId });
await shareClient.join({ roomId });

const localStream = TRTC.createStream({ audio: true, video: true, userId }); 
const shareStream = TRTC.createStream({ audio: false, screen: true, userId });

// ... 초기화 및 관련 코드 배포를 생략하고 필요에 따라 스트림을 배포합니다.

:::
</dx-codeblock>

## 화면 공유 시스템 오디오 수집

**시스템 오디오 수집은 Chrome M74+만 지원하며, Windows 및 Chrome OS에서는 전체 시스템 오디오를 캡처할 수 있습니다. Linux 및 Mac에서는 탭의 오디오만 캡처할 수 있습니다. 그 외의 Chrome 버전, 기타 시스템 및 브라우저는 지원되지 않습니다.**

<dx-codeblock>
:::javascript
// 화면 공유 스트림 screenAudio 생성 시 true로 설정하십시오. 시스템 및 마이크 볼륨 동시 수집을 지원하지 않으며, audio 속성을 동시에 true로 설정하지 마십시오.
const shareStream = TRTC.createStream({ screenAudio: true, screen: true, userId });
await shareStream.initialize();
...
:::
</dx-codeblock>

팝업 창에서 '오디오 공유'를 선택하면 배포된 stream에 시스템 사운드가 전달됩니다.
