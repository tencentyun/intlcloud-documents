## TUICallEngine API

TUICallEngine은 **UI 요소를 포함하지 않는** 음성/영상 통화 컴포넌트입니다.

## API 개요

| API                                                          | 설명                                |
| ------------------------------------------------------------ | ----------------------------------- |
| [createInstance](#createinstance) | TUICallEngine 인스턴스 생성(싱글톤 모드) |
| [destroyInstance](#destroyinstance) | TUICallEngine 인스턴스 종료(싱글톤 모드) |
| [on](#on)    | 이벤트 수신                            |
| [off](#off)  | 이벤트 수신 중지                        |
| [login](#login) | 로그인                            |
| [logout](#logout) | 로그아웃                            |
| [setSelfInfo](#setselfInfo) | 대화명 및 프로필 사진 설정                  |
| [call](#call) | C2C 통화하기                         |
| [groupCall](#groupcall) | 그룹 통화 하기                        |
| [accept](#accept) | 통화 수락                            |
| [reject](#reject) | 통화 거절                            |
| [hangup](#hangup) | 통화 종료                            |
| [switchCallMediaType](#switchcallmediatype) | 통화 유형 변경                    |
| [startRemoteView](#startremoteview) | 원격 비디오 렌더링 시작                    |
| [stopRemoteView](#stopremoteview) | 원격 비디오 렌더링 중지                    |
| [startLocalView](#startlocalview) | 로컬 비디오 렌더링 시작                    |
| [stopLocalView](#stoplocalview) | 로컬 비디오 렌더링 중지       |
| [openCamera](#opencamera) | 카메라 켜기                          |
| [closeCamara](#closecamara) | 카메라 끄기                          |
| [openMicrophone](#openmicrophone) | 마이크 켜기                          |
| [closeMicrophone](#closemicrophone) | 마이크 끄기                          |
| [setVideoQuality](#setvideoquality) | 비디오 품질 설정                        |
| [getDeviceList](#getdevicelist) | 장치 목록 가져오기                        |
| [switchDevice](#switchdevice) | 다른 카메라/마이크로 변경              |

## API 세부정보

### createInstance

이 API는 TUICallEngine 싱글톤을 생성하는 데 사용됩니다.



```swift
const tuiCallEngine = TUICallEngine.createInstance({
    SDKAppID: 0, // 0을 IM 애플리케이션의 SDKAppID로 대체
    tim: tim         // 이미 TIM 인스턴스가 있는 경우 이 tim 매개변수를 사용하여 TIM 인스턴스의 고유성 보장
});
```

**매개변수는 다음과 같습니다:**

| 매개변수     |  유형   | 의미                  |
| -------- | ------ | --------------------- |
| SDKAppID | Number | IM 애플리케이션의 SDKAppID |
| tim      | Any    | TIM 인스턴스(선택 사항)      |

### destroyInstance

이 API는 TUICallEngine 싱글톤을 종료하는 데 사용됩니다.



```swift
tuiCallEngine.destroyInstance().then(() => {
    //success
}).catch(error => {
    console.warn('destroyInstance error:', error);
});
```

### on

이 API는 이벤트를 수신하는 데 사용됩니다.



```swift
let onError = function(error) {
    console.log(error);
};
tuiCallEngine.on(TUICallEvent.ERROR, onError, this);
```

**매개변수는 다음과 같습니다:**

| 매개변수     | 유형     | 의미                         |
| --------- | -------- | ---------------------------- |
| eventName | String   | 이벤트 이름                       |
| callback  | function | 이벤트 콜백                 |
| context   | Any      | callback이 실행될 것으로 예상되는 컨텍스트 |

### off

이 API는 이벤트 수신을 중지하는 데 사용됩니다.



```swift
let onError = function(error) {
    console.log(error);
};
tuiCallEngine.off(TUICallEvent.ERROR, onError, this);
```

**매개변수는 다음과 같습니다:**

| 매개변수     | 유형     | 의미                         |
| --------- | -------- | ---------------------------- |
| eventName | String   | 이벤트 이름                       |
| callback  | function | 이벤트 콜백                 |
| context   | Any      | callback이 실행될 것으로 예상되는 컨텍스트 |

### login

인터페이스 로그인에 사용됩니다.



```swift
let promise = tuiCallEngine.login({userID: 'your userID', userSig: 'your userSig'});
promise.then(() => {
    //success
}).catch(error => {
    console.warn('login error:', error);
});
```

**매개변수는 다음과 같습니다:**

| 매개변수    | 유형   | 의미                                                         |
| ------- | ------ | ------------------------------------------------------------ |
| userID  | String | 현재의 사용자 ID. 영어 알파벳(a-z, A-Z), 숫자(0-9), 하이픈(-), 언더바(_)의 문자열로 구성 |
| userSig | String | Tencent Cloud가 설계한 일종의 보안 서명입니다. 가져오는 방법은 [UserSig 계산 방법](https://www.tencentcloud.com/document/product/647/35166)을 참고하십시오. |

### logout

인터페이스 로그아웃에 사용됩니다.



```swift
let promise = tuiCallEngine.logout();
promise.then(() => {
    //success
}).catch(error => {
    console.warn('logout error:', error);
});
```

### setSelfInfo

이 API는 대화명과 프로필 사진을 설정하는 데 사용됩니다.



```swift
let promise = tuiCallEngine.setSelfInfo({
    nickName: 'video', 
    avatar:'http(s)://url/to/image.jpg'
});
promise.then(() => {
    //success
}).catch(error => {
    console.warn('setSelfInfo error:', error);
});
```

**매개변수는 다음과 같습니다:**

| 매개변수     | 유형   | 의미     |
| -------- | ------ | -------- |
| nickName | String | 대화명     |
| avatar   | String | 프로필 사진의 URL |

### call

이 API는 C2C 통화를 수행하는 데 사용됩니다. 초대받은 사람은 TUICallEvent.INVITED 콜백을 수신합니다.

>! Android 및 iOS에서 오프라인 알림이 지원됩니다. Web에서는 지원되지 않습니다.



```javascript
let promise = tuiCallEngine.call({
    userID: 'user1', 
    type: 1, 
});
promise.then(() => {
    //success
}).catch(error => {
    console.warn('call error:', error);
});
```

**매개변수는 다음과 같습니다:**

| 매개변수   | 유형   | 의미                            |
| ------ | ------ | ------------------------------- |
| userID          | String | 초대된 사용자의 userID  |
| type   | Number | 0-알 수 없음, 1-음성 통화, 2-영상 통화 |

### groupCall

이 API는 그룹 통화를 하는 데 사용됩니다. 초대받은 사람은 'EVENT.INVITED' 콜백을 받게 됩니다.

>! Android 및 iOS에서 오프라인 알림이 지원됩니다. Web에서는 지원되지 않습니다.



```javascript
let promise = tuiCallEngine.groupCall({
    userIDList: ['user1', 'user2'], 
    type: 1, 
    groupID: 'IM 그룹 ID', 
});
promise.then(() => {
    //success
}).catch(error => {
    console.warn('groupCall error:', error);
});
```

**매개변수는 다음과 같습니다:**

| 매개변수                                                         | 유형   | 의미                                                    |
| ------------------------------------------------------------ | ------ | ------------------------------------------------------- |
| userIDList                                                   | Array  | 통화할 사용자의 ID                                                |
| type                                                         | Number | 0: 알 수 없음; 1: 음성 통화; 2: 영상 통화                         |
| groupID                                                      | String | IM 그룹 ID                                                 |
| timeout                                                      | String | 타임 아웃 시간(선택 사항)                                          |
| roomID                                                       | String | 방 ID(선택 사항)                                           |
| [offlinePushInfo](#offlinePushInfo) | Object | 사용자 정의 오프라인 알림. 이 매개변수는 선택 사항이며 tsignaling 0.8.0 이상에서만 유효함 |

#### offlinePushInfo

| 매개변수                 | 유형   | 의미                                                   |
| -------------------- | ------ | ------------------------------------------------------- |
| title                | string | 오프라인 알림의 제목(선택 사항)                                    |
| description          | string | 오프라인 알림 콘텐츠(선택 사항)                                    |
| androidOPPOChannelID | string | OPPO 8.0 이상(선택 사항)의 오프라인 알림에 대한 채널 ID |
| extension            | string | 통과 콘텐츠. 이 매개변수는 선택 사항이며 tsignaling 0.9.0 이상에서만 유효    |

### accept

이 API는 `TUICallEvent.INVITED` 콜백을 수신한 후 통화를 수락하는 데 사용됩니다.



```javascript
tuiCallEngine.on(TUICallEvent.INVITED, () => {
    tuiCallEngine.accept().promise.then(() => {
        //success
    }).catch(error => {
        console.warn('accept error:', error);
    });
});
```

### reject

이 API는 `TUICallEvent.INVITED` 콜백을 수신한 후 통화를 거부하는 데 사용됩니다.



```javascript
tuiCallEngine.on(TUICallEvent.INVITED, () => {
    tuiCallEngine.reject().then(() => {
        //success
    }).catch(error => {
        console.warn('reject error:', error);
    });
});
```

### hangup

이 API는 통화를 종료하는 데 사용됩니다.

통화 중인 경우 이 API로 통화를 종료할 수 있습니다.

통화에 아직 응답하지 않은 상태인 경우 이 API로 통화를 취소할 수 있습니다.



```javascript
tuiCallEngine.hangup().then(() => {
     //success
 }).catch(error => {
        console.warn('hangup error:', error);
 });
```

### switchCallMediaType

이 API는 통화 유형을 변경하는 데 사용됩니다.

이 API는 1v1 통화에만 작동합니다.

ERROR 콜백 전환 실패. code: 60001



```javascript
// 1 음성 통화; 2 영상 통화
tuiCallEngine.switchCallMediaType(2).then(() => {
  //success
}).catch(error => {
  console.warn('switchCallMediaType error:', error);
});
```

**매개변수는 다음과 같습니다:**

| 매개변수         | 유형   | 의미                   |
| ------------ | ------ | ---------------------- |
| newMediaType | Number | 1-음성 통화, 2-영상 통화 |

### startRemoteView

이 API는 원격 비디오 렌더링을 시작하는 데 사용됩니다.



```javascript
let promise = tuiCallEngine.startRemoteView({
    userID: 'user1', 
    videoViewDomID: 'video_1',
});
promise.then(() => {
    //success
}).catch(error => {
    console.warn('startRemoteView error:', error);
});
```

**매개변수는 다음과 같습니다:**

| 매개변수           | 유형   | 의미                               |
| -------------- | ------ | ---------------------------------- |
| userID           | String  | 사용자 ID                            |
| videoViewDomID | String | 사용자의 데이터를 이 dom id 노드로 렌더링 |

### stopRemoteView

이 API는 원격 비디오 렌더링을 중지하는 데 사용됩니다.



```javascript
tuiCallEngine.stopRemoteView({userID: 'user1'});
```

**매개변수는 다음과 같습니다:**

| 매개변수   | 유형   | 의미   |
| ------ | ------ | ------ |
| userID | String | 사용자 id |

### startLocalView

이 API는 로컬 비디오 렌더링을 시작하는 데 사용됩니다.



```javascript
let promise = tuiCallEngine.startLocalView({
    userID: 'user1', 
    videoViewDomID: 'video_1'
});
promise.then(() => {
    //success
}).catch(error => {
    console.warn('startLocalView error:', error);
});
```

**매개변수는 다음과 같습니다:**

| 매개변수           | 유형   | 의미                               |
| -------------- | ------ | ---------------------------------- |
| userID         | String | 사용자 ID                            |
| videoViewDomID | String | 사용자의 데이터를 이 dom id 노드로 렌더링 |

### stopLocalView

이 API는 로컬 비디오 렌더링을 중지하는 데 사용됩니다.



```javascript
let promise = tuiCallEngine.stopLocalView({userID: 'user1'});
promise.then(() => {
    //success
}).catch(error => {
    console.warn('stopLocalView error:', error)
});
```

**매개변수는 다음과 같습니다:**

| 매개변수   | 유형   | 의미    |
| ------ | ------ | ------- |
| userID         | String | 사용자 ID    |

### openCamera

이 API는 카메라를 켜는 데 사용됩니다.



```javascript
tuiCallEngine.openCamera().then(() => {
    //success
}).catch(error => {
    console.warn('openCamera error:', error);
});
```

### closeCamara

이 API는 카메라를 끄는 데 사용



```javascript
tuiCallEngine.closeCamera().then(() => {
    //success
}).catch(error => {
    console.warn('closeCamara error:', error);
});
```

### openMicrophone

이 API는 마이크를 켜는 데 사용됩니다.



```javascript
tuiCallEngine.openMicrophone().then(() => {
    //success
}).catch(error => {
    console.warn('openMicrophone error:', error);
});
```

### closeMicrophone

이 API는 마이크를 끄는 데 사용됩니다.



```javascript
tuiCallEngine.closeMicrophone().then(() => {
    //success
}).catch(error => {
    console.warn('closeMicrophone error:', error);
});
```

### setVideoQuality

이 API는 비디오 품질을 설정하는 데 사용됩니다.



```javascript
const profile = '720p';
tuiCallEngine.setVideoQuality(profile).then(() => {
    //success
}).catch(error => {
    console.warn('setVideoQuality error:', error)
});    // 비디오 품질을 720p로 설정     
```

**매개변수는 다음과 같습니다:**

| 비디오 Profile | 해상도(W x H) |
| ------------ | ----------------- |
| 480p         | 640 × 480         |
| 720p         | 1280 × 720        |
| 1080p        | 1920 × 1080       |

### getDeviceList

이 API는 장치 목록을 가져오는 데 사용됩니다.



```javascript
tuiCallEngine.getDeviceList("camera").then((devices) => {
    console.log(devices);
}).catch(error => {
    console.warn('getDeviceList error:', error);
});
```

**매개변수는 다음과 같습니다:**

| 매개변수       | 유형   | 의미                                  |
| ---------- | ------ | ------------------------------------- |
| deviceType | String | 장치 유형. 'camera'-카메라, 'microphones'-마이크 |

### switchDevice

이 API는 다른 카메라나 마이크로 변경하는 데 사용됩니다.



```javascript
let promsie = tuiCallEngine.switchDevice({
    deviceType: 'video', 
    deviceId: cameras[0].deviceId
});
promise.then(() => {
    //success
}).catch(error => {
    console.warn('switchDevice error:', error)
});
```

**매개변수는 다음과 같습니다:**

| 매개변수       | 유형   | 의미                                                         |
| ---------- | ------ | ------------------------------------------------------------ |
| deviceType | String | 장치 유형, 'video' 카메라 'audio' 마이크               |
| deviceId   | String | 변경할 장치의 ID, getCameras()를 사용하여 카메라 ID를 가져오고, getMicrophones()를 사용하여 마이크 ID 가져오기 |

 
