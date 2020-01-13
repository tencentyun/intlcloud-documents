H5 개발자가 Tencent Cloud GME(Game Multimedia Engine) 제품 API를 디버깅하고 액세스하는 편의성을 위해 H5 개발 맞춤용 액세스 기술 파일을 소개드립니다.


| API           | API 의미            |
|--------------|-------------------|
| Init           | API 초기화         |
| SetTMGDelegate | 위탁 설정           |
| EnterRoom      | 음성 방에 들어가기       |
| EnableMic      | 수집 디바이스 오픈 혹은 종료 |
| EnableSpeaker  | 플레이 디바이스 오픈 혹은 종료 |
| SetMicVolume   | 마이크 볼륨 설정      |
| ExitRoom       | 음성 방 나가기        |


>
- GME API를 호출하면 리턴값은 QAVError.OK이며, 수치는 0입니다. 
-GME 방에 가입하기 전에 인증해야 합니다. 문서의 인증 관련 내용을 참조하십시오.
- 방에 들어간 후에 디바이스를 조작할 수 있습니다.


## 초기화 관련 API
초기화하기 전에 SDK는 비초기화 상태로, 초기화를 인증하여 SDK를 초기화한 후에 방에 들어갈 수 있습니다.

### SDK 초기화
파라미터 획득은 [액세스 매뉴얼](https://intl.cloud.tencent.com/document/product/607/10782)을 참조하십시오.
이 인터페이스는 Tencent Cloud 콘솔의 SDKAppID 계정을 파라미터로 적용 및 openId를 추가해야 합니다. 이 openId는 사용자당 1개 적용하며, 앱 개발자가 스스로 룰을 정합니다. 앱내 반복할 수 없습니다(현재 INT 64만 지원합니다).

>SDK를 초기화해야 방에 들어갈 수 있습니다.

### 함수 프로토타입

```
WebGMEAPI.fn.Init = function (document, SdkAppId, openId) {...}
```

|파라미터     |의미|
| ------------- |-------------|
| document      |HTML DOM Document 오브젝트|
| SdkAppId      |Tencent Cloud 콘솔의 SdkAppId 계정|
| openId      |사용자 계정, 개발자가 정의하며, 반드시 10000보다 커야 합니다. 사용자 표기용.|

### 예시 코드 
```
const cSdkAppId = () => document.getElementById("input-SdkAppId").value;
const cOpenID = () => document.getElementById("input-OpenID").value;
gmeAPI.Init(document, cSdkAppId(), cOpenID());
```

### 콜백 설정
API류는 Delegate 방법으로 애플리케이션에 콜백 공지를 전송합니다. 콜백 함수를 SDK에 등록하여 콜백 메시지를 수락합니다. 콜백 함수를 SDK에 등록하려면 방에 들어가기 전에 설정해야 합니다.


#### 함수 프로토타입
```
WebGMEAPI.fn.SetTMGDelegate = function (delegate){...}
```
|파라미터              |의미|
| ------------- |-------------|
| onEvent     |SDK 콜백 이벤트|

#### 예시 코드  
```
gmeAPI.SetTMGDelegate(onEvent);
```





## 실시간 음성 관련 API
초기화를 하고나면 SDK를 호출하여 방에 들어가야 실시간 음성 통화가 가능합니다.


### 방 가입
생성한 인증 메시지로 방에 들어가면 ITMG_MAIN_EVENT_TYPE_ENTER_ROOM 콜백 메시지를 받습니다. 방에 가입 시 기본적으로 마이크와 스피커를 끕니다.


#### 함수 프로토타입
```
WebGMEAPI.fn.EnterRoom = function (roomId, roomType, authBuffer) {...}
```
|파라미터     |의미|
| ------------- |-------------|
| roomId |룸 ID, chleo 127개 캐릭터를 지원합니다|
| roomType |방 가청주파수 타입|
| authBuffer|인증코드, 획득 방법은 [프로그래밍 설정](https://intl.cloud.tencent.com/document/product/607/10783)을 참조하십시오.



#### 예시 코드  
```
 function bindButtonEvents() {
        $("#start_btn").click(function () {
            console.log('start!');
            //스텝1, AuthBuffer를 읽어옵니다
            var FetchSigCgi = 'http://134.175.146.244:10005/';
            $.ajax({
                type: "POST",
                url: FetchSigCgi,
                dataType: 'json',
                data: {
                    sdkappid: cSdkAppId(),
                    id: cRoomNum(),
                    openid: cOpenID(),
                },
                success: function (json) {
                    //스텝2, AuthBuffer를 읽어오는데 성공합니다
                    if (json && json.errorCode === 0) {
                        let userSig = json.userSig;
                        gmeAPI.Init(document, cSdkAppId(), cOpenID());
                        gmeAPI.SetTMGDelegate(onEvent);
                        gmeAPI.EnterRoom(cRoomNum(), 1, userSig);
                    } else {
                        console.error(json);
                    }
                },
                error: function (err) {
                    console.error(err);
                }
            });
        });
```

### 이벤트 콜백
방에 가입 시 ITMG_MAIN_EVENT_TYPE_ENTER_ROOM 메시지를 발송하며, OnEvent 함수에서 판단합니다.

#### 예시 코드  
```
 onEvent = function (eventType, result) {
         if (eventType === gmeAPI.event.ITMG_MAIN_EVENT_TYPE_ENTER_ROOM)
        {
            //방 들어가기
        }
        else if (eventType === gmeAPI.event.ITMG_MAIN_EVNET_TYPE_USER_UPDATE)
        {
            app._data.downStreamInfoList = result.PeerInfo;//수신한 다운스트리밍 메시지는 하기 리스트를 참조하십시오
            app._data.brSend = result.UploadBRSend;//음성 데이터 부호율 업로드
            app._data.rtt = result.UploadRTT;//RTT 업로드
        }
        else if (eventType === gmeAPI.event.ITMG_MAIN_EVENT_TYPE_EXIT_ROOM)
        {
            //방 나가기
        }
        else if (eventType === gmeAPI.event.ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT)
        {
            //방 연결 끊김
        }
    };
```


수신 다운스트리밍 메시지는 다음 downStreamInfoList과 같습니다: 

|파라미터      |의미|
| ------------- |------------|
| brRecv      |수신 부호율|
| delay      |수신 딜레이|
| jitterBufferMs      |지터 딜레이|
| jitterReceived      |jitter 수락|


### 방 로그아웃
이 API로 방에서 나갈 수 있습니다. 이는 비동기화 인터페이스로, 방에서 나갈 경우 콜백이 있으며, 리턴값은 AV_OK일 경우, 비동기화 딜리버리가 성공하였음을 의미합니다.
#### 함수 프로토타입  
```
WebGMEAPI.fn.ExitRoom = function (){...}
```
#### 예시 코드  
```
gmeAPI.ExitRoom();
```

### 마이크 온/오프
이 API는 마이크를 온/오프합니다. 방에 가입 시에 기본적으로 마이크와 스피커를 끕니다.

#### 함수 프로토타입  
```
WebGMEAPI.fn.EnableMic = function (bEnable) {...}
```
|파라미터      |의미|
| ------------- |------------|
| isEnabled      |마이크를 온하려면 파라미터는 true로 입력하며, 마이크를 오프할 경우 파라미터는 false입니다|

#### 예시 코드  
```
gmeAPI.EnableMic(false);
```



### 마이크 볼륨 설정
이 API는 마이크 볼륨을 설정합니다. 파라미터 volume은 마이크 볼륨을 설정하며, 수치가 0일 경우 무음, 수치가 100일 경우 볼륨 그대로 유지를 의미하며, 기본값은 100입니다.

#### 함수 프로토타입  
```
WebGMEAPI.fn.SetMicVolume = function (volume){...}
```
|파라미터     |의미|
| -------------|-------------|
| volume    |볼륨 설정, 범위는0-100|

#### 예시 코드  
```
gmeAPI.SetMicVolume(100);
```


### 스피커 온/오프
이 API는 스피커를 온/오프합니다.
#### 함수 프로토타입  
```
WebGMEAPI.fn.EnableSpeaker = function (bEnable){...}
```
|파라미터     |의미|
| ------------- |------------|
| isEnabled           |혹 스피커를 끄려면, 파라미터는 false로 입력하며, 스피커를 켤 경우 파라미터는 true입니다|

#### 예시 코드  
```
gmeAPI.EnableSpeaker(true);
```
