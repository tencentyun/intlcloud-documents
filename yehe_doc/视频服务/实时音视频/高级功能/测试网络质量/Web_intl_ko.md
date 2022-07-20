TRTC는 사용자가 방에 들어가거나 통화에 참여하기 전에 사용자의 네트워크 품질을 확인할 수 있습니다. 네트워크 품질이 만족스럽지 않은 경우 원활한 통화를 위해 더 나은 네트워크 환경으로 이동하도록 안내하는 것이 좋습니다.

본문에서는 [NETWORK_QUALITY](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/module-ClientEvent.html#.NETWORK_QUALITY) 이벤트를 기반으로 호출 전 네트워크 품질을 확인하는 방법을 설명합니다. 통화 중 네트워크 품질을 감지하려면[NETWORK_QUALITY](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/module-ClientEvent.html#.NETWORK_QUALITY) 이벤트를 수신하면 됩니다.

## 구현 프로세스

1. [TRTC.createClient](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#.createClient)를 호출하여 uplinkClient 및 downlinkClient의 두 Client를 생성합니다.
2. 두 명의 Client가 같은 방에 들어가도록 합니다.
3. uplinkClient를 사용하여 스트림을 푸시합니다. [NETWORK_QUALITY](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/module-ClientEvent.html#.NETWORK_QUALITY) 이벤트를 듣고 업스트림 네트워크 품질을 확인하십시오.
4. downlinkClient를 사용하여 스트림을 가져옵니다. [NETWORK_QUALITY](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/module-ClientEvent.html#.NETWORK_QUALITY) 이벤트를 듣고 다운스트림 네트워크 품질을 확인하십시오.
5. 전체 프로세스는 약 15s가 소요되며 평균 네트워크 품질은 결국 업스트림 및 다운스트림 네트워크 품질을 평가하는 데 사용됩니다.

>! 네트워크 품질을 확인하는 과정에는 소정의 [기본 서비스 요금](https://intl.cloud.tencent.com/document/product/647/34610#.E5.9F.BA.E7.A1.80.E6.9C.8D.E5.8A.A1)이 발생합니다. 푸시 해상도가 지정되지 않은 경우 스트림은 기본적으로 640*480 해상도로 푸시됩니다.

## 코드 예시

```js
let uplinkClient = null; // 업스트림 네트워크 품질 확인
let downlinkClient = null; // 다운스트림 네트워크 품질 확인
let localStream = null; // 테스트할 스트림
let testResult = {
  // 업스트림 네트워크 품질 데이터 기록
  uplinkNetworkQualities: [],
  // 다운스트림 네트워크 품질 데이터 기록
  downlinkNetworkQualities: [],
  average: {
    uplinkNetworkQuality: 0,
    downlinkNetworkQuality: 0
  }
}

// 1. 업스트림 네트워크 품질 확인
async function testUplinkNetworkQuality() {
  uplinkClient = TRTC.createClient({
    sdkAppId: 0, // sdkAppId 입력
    userId: 'user_uplink_test',
    userSig: '', // uplink_test의 userSig
    mode: 'rtc'
  });

  localStream = TRTC.createStream({ audio: true, video: true });
  // 필요에 따라 video profile 설정
  localStream.setVideoProfile('480p'); 
  await localStream.initialize();

  uplinkClient.on('network-quality', event => {
    const { uplinkNetworkQuality } = event;
    testResult.uplinkNetworkQualities.push(uplinkNetworkQuality);
  });

  // 테스트를 위한 방으로 들어갑니다. 충돌을 피하기 위해 회의실 ID는 무작위여야 합니다.
  await uplinkClient.join({ roomId: 8080 }); 
  await uplinkClient.publish(localStream);
}

// 2. 다운스트림 네트워크 품질 확인
async function testDownlinkNetworkQuality() {
  downlinkClient = TRTC.createClient({
    sdkAppId: 0, // sdkAppId 입력
    userId: 'user_downlink_test',
    userSig: '', // userSig
    mode: 'rtc'
  });

  downlinkClient.on('stream-added', async event => {
    await downlinkClient.subscribe(event.stream, { audio: true, video: true });
		// 성공적인 구독 후 네트워크 품질 이벤트 수신 시작
    downlinkClient.on('network-quality', event => {
      const { downlinkNetworkQuality } = event;
      testResult.downlinkNetworkQualities.push(downlinkNetworkQuality);
    });
  })
  // 테스트를 위한 방으로 들어갑니다. 충돌을 피하기 위해 회의실 ID는 무작위여야 합니다.
  await downlinkClient.join({ roomId: 8080 });
}

// 3. 점검 시작
testUplinkNetworkQuality();
testDownlinkNetworkQuality();

// 4. 15s 후 점검을 중지하고 평균 네트워크 품질 계산
setTimeout(() => {
  // 평균 업스트림 네트워크 품질 계산
  if (testResult.uplinkNetworkQualities.length > 0) {
    testResult.average.uplinkNetworkQuality = Math.ceil(
      testResult.uplinkNetworkQualities.reduce((value, current) => value + current, 0) / testResult.uplinkNetworkQualities.length
    );
  }

  if (testResult.downlinkNetworkQualities.length > 0) {
    // 평균 다운스트림 네트워크 품질 계산
    testResult.average.downlinkNetworkQuality = Math.ceil(
      testResult.downlinkNetworkQualities.reduce((value, current) => value + current, 0) / testResult.downlinkNetworkQualities.length
    );
  }
    
  // 점검이 종료됩니다. 관련 상태를 지우십시오.
  uplinkClient.leave();
  downlinkClient.leave();
  localStream.close();
}, 15 * 1000);
```

## 결과 분석

위의 단계를 수행한 후 평균 업스트림 및 다운스트림 네트워크 품질을 얻을 수 있습니다. 네트워크 품질의 열거 값은 다음과 같습니다.

| 값 | 설명                                                         |
| :--- | :----------------------------------------------------------- |
| 0    | 알 수 없는 네트워크 품질, 현재 client 인스턴스가 업스트림/다운스트림 연결을 설정하지 않았음을 나타냄     |
| 1    | 우수한 네트워크 품질                                                 |
| 2    | 좋은 네트워크 품질                                                 |
| 3    | 평균 네트워크 품질                                                 |
| 4    | 열악한 네트워크 품질                                                   |
| 5    | 매우 열악한 네트워크 품질                                                 |
| 6    | 네트워크 연결 끊김. 참고: 다운스트림 네트워크 품질이 이 값이면 모든 다운스트림 연결이 끊겼음을 나타냄 |

> 네트워크 품질이 3보다 나쁠 경우 사용자에게 네트워크를 확인하고 더 나은 네트워크 환경으로 이동하라는 메시지를 표시하는 것이 좋습니다. 그렇지 않으면 정상적인 음성/영상 통화 환경이 영향을 받을 수 있습니다. <br>다음 방법을 사용하여 대역폭 소비를 줄일 수도 있습니다.
> - 업스트림 네트워크 품질이 3보다 나쁠 경우 [LocalStream.setVideoProfile()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#setVideoProfile) API를 호출하여 비트레이트를 줄이거나 또는 [LocalStream.muteVideo()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#muteVideo)를 호출하여 업스트림 대역폭 소비를 줄이기 위해 비디오를 비활성화할 수 있습니다.
> - 다운스트림 네트워크 품질이 3보다 낮은 경우 [기본 스트림/서브 스트림 전송 활성화](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-27-advanced-small-stream.html)의 지침에 따라 낮은 품질의 스트림에 가입하거나 오디오만 가입하여 다운스트림 대역폭 소비를 줄일 수 있습니다.

