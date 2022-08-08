본 문서는 TRTC 방에 들어가는 방법을 설명합니다. 오디오/비디오 방에 입장한 후에만 사용자는 방에 있는 다른 사용자의 오디오/비디오 스트림을 구독하거나 사용자 자신의 오디오/비디오 스트림을 다른 사용자에게 게시할 수 있습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/d7353029f13bf9950d4ada0b05de7077.png)

TRTC Web SDK를 사용하다 보면 종종 다음과 같은 객체를 접하게 됩니다.
- Client 객체는 로컬 클라이언트를 말합니다. [Client](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html) 타입으로 통화방 입장, 로컬 스트림 배포, 원격 스트림 구독 등 기능을 제공합니다.
- Stream 객체는 멀티미디어 스트림 객체를 말하며, 로컬 멀티미디어 스트림 객체 [LocalStream](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html)와 원격 멀티미디어 스트림 객체 [RemoteStream](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/RemoteStream.html)로 나뉩니다. Stream 타입은 오디오 및 비디오의 재생과 관련한 멀티미디어 스트림 객체 행위를 지원합니다.

[](id:step1)
## 1단계: Client 객체 생성
[TRTC.createClient()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#createClient)로 [Client](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html) 객체를 생성합니다. 주요 매개변수는 다음과 같습니다.

| 매개변수 | 필드 의미 | 보충 설명 | 데이터 유형 | 샘플 값 | 기본값 | 비고 |
|---------|---------|---------|---------|---------|---------|---------|
| mode | 응용 시나리오 | 'rtc'모드는 일대일 음성/화상 통화 또는 최대 300명이 참여할 수 있는 회의에 적합합니다.<br> `live`는 최대 10만 명까지 실시간 스트리밍할 수 있습니다. | string | rtc | rtc | -|
| sdkAppId | 애플리케이션 ID | <a href="https://console.cloud.tencent.com/trtc/app">TRTC 콘솔</a>에서 sdkAppId를 볼 수 있습니다. 아직 애플리케이션이 없다면 ‘애플리케이션 생성’을 클릭하여 애플리케이션을 생성합니다.| number | 1400000123 | 없음 |필수 |
| userId | 사용자 ID | 사용자 이름. 영어 대문자 및 소문자(a-z, A-Z), 숫자(0-9), 밑줄 및 하이픈만 포함할 수 있습니다.<br> **참고:** TRTC에서 사용자는 동일한 사용자 ID를 사용하여 두 개의 다른 장치에서 동시에 같은 방에 들어갈 수 없습니다. | string | ‘denny’ 또는 ‘123321’| 없음 |필수 |
| userSig | 방에 들어가기 위해 필요한 인증 티켓 | 계산 방법은 [UserSig 계산 및 사용 방법](https://intl.cloud.tencent.com/document/product/647/35166)을 참고하십시오. | 문자열 | eJyrVareCeYrSy1SslI... | 없음 |필수 |
| useStringRoomId | 문자열 유형의 방 ID 사용 여부 | string 유형의 roomId 사용 여부를 지정합니다.|boolean| true | false | - |

자세한 매개변수 설명은 [TRTC.createClient()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#createClient)를 참고하십시오. 

```javascript
// 실시간 통화 모드에서 클라이언트 객체 생성
const client = TRTC.createClient({
  mode: 'rtc',
  sdkAppId,
  userId,
  userSig
});

// 라이브 스트리밍 모드에서 클라이언트 객체 생성
const client = TRTC.createClient({
  mode: 'live',
  sdkAppId,
  userId,
  userSig
});
```

[](id:step2)
## 2단계: 영상 통화방 입장

[Client.join()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#join)을 호출하여 음성/영상 통화방에 입장합니다. 주요 매개변수는 다음과 같습니다.

| 매개변수 | 필드 의미 | 보충 설명 | 데이터 유형 | 샘플 값 | 기본값 | 비고 |
|---------|---------|---------|---------|---------|---------|---------|
| roomId | 방 ID | 데이터 유형은 기본적으로 number입니다. string 유형의 roomId를 사용하려면 createClient()의 useStringRoomId 매개변수를 true로 설정합니다.<br> - number roomId는 [1에서 4294967294] 사이의 정수여야 합니다.<br> - roomId가 string 유형일 때 64바이트 미만의 다음 문자 세트만 지원됩니다: <br> 영문 대문자 및 소문자(a-zA-Z); 숫자(0-9); 스페이스, !, #, $, %, &, (,), +, -, :, ;, <, =, ., >, ?, @, [,], ^, _, {,}, \|, ~, |   number / string  | 3364 또는 class-room | 없음 | 필수 |
| role | 사용자 역할 | 이 매개변수는 모드가 `live`로 설정된 경우에만 필요합니다. 현재 지원되는 두 가지 역할: `anchor` 앵커, `audience` 시청자 | string | anchor |  audience | - |

자세한 매개변수 설명은 [Client.join()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#join)을 참고하십시오. 

```javascript
// Promise 구문 사용
client
  .join({ roomId })
  .then(() => {
    console.log('입장 성공');
  })
  .catch(error => {
    console.error('입장 실패, 나중에 다시 시도하십시오' + error);
  });

// async/await 구문을 사용하는 것이 좋습니다.
try {
  await client.join({ roomId });
  console.log('입장 성공');
} catch (error) {
  console.error('입장 실패, 나중에 다시 시도하십시오' + error);
}

// 앵커 역할로 방 입장
try {
  await client.join({ 
    roomId,
    role: 'anchor' 
  });
  console.log('입장 성공');
} catch (error) {
  console.error('입장 실패, 나중에 다시 시도하십시오' + error);
}
```
