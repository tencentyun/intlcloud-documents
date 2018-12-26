## 소개

Tencent Cloud GME SDK의 사용을 환영합니다. H5 개발자가 Tencent Cloud GME 제품 API를 디버깅하고 연결하는 데 도움이 되도록 이 문서에서 H5 개발에 적합한 액세스 기술을 소개합니다.

### GME H5 인터페이스 사용 목차

| 인터페이스           | 인터페이스 의미            |
|--------------|-------------------|
| Init           | 인터페이스 초기화         |
| SetTMGDelegate | 위탁 설정           |
| EnterRoom      | 음성 방 입장       |
| EnableMic      | 수집 장치 켜기 또는 끄기 |
| EnableSpeaker  | 재생 장치 켜기 또는 끄기 |
| SetMicVolume   | 마이크 음량 설정      |
| ExitRoom       | 음성 방 퇴장        |


**설명**

**GME의 인터페이스 호출 성공 후 반환 값은 QAVError.OK이고, 수치는 0입니다.**

**GME가 방을 가입하려면 인증이 필요합니다. 인증 관련 내용을 참조하십시오.**

**방에 입장한 후에 장치에 대한 조작을 실행할 수 있습니다.**


## 초기화 관련 인터페이스
초기화 전에 SDK는 미초기화 단계에 속하고 있습니다. 초기화 인증 후 SDK를 초기화해야 방에 입장할 수 있습니다.

## SDK 초기화
매개변수 획득은 [GME 액세스 가이드].(/GME%20Introduction.md) 문서를 참조하십시오.
해당 API는 Tencent Cloud 콘솔의 SdkAppId 번호를 매개변수로 사용하고 여기에 openId를 더해야 합니다. 해당 openId는 하나의 사용자를 유일하게 식별하는 것으로 규칙은 App 개발자는 자체적으로 제정하고 App 내에서는 중복되지 않으면 됩니다(현재는 INT64만을 지원합니다).
SDK 초기화 후에만 방에 들어갈 수 있습니다.
#### 함수 프로토타입

```
WebGMEAPI.fn.Init = function (document, sdkAppId, openId) {...}
```

|매개변수     |의미|
| ------------- |-------------|
| document    	  |		HTML DOM Document 개체	|
| sdkAppId    		  |Tencent Cloud 콘솔의 SdkAppId 번호	|
| openId    		  |개발자가 정의한 사용자 계정, 사용자를 식별하기 위해 10,000보다 커야 합니다.|

#### 샘플 코드 
```
const cSdkAppId = () => document.getElementById("input-sdkappid").value;
const cOpenID = () => document.getElementById("input-openid").value;
gmeAPI.Init(document, cSdkAppId(), cOpenID());
```

### 콜백 설정
인터페이스 클래스는 Delegate 방법을 사용하여 응용프로그램에 콜백 알림을 발송합니다. 콜백 함수를 SDK에 등록하여 콜백 정보를 수신하는 데 사용됩니다.
콜백 함수를 SDK에 등록하려면 방 입장하기 전에 설정해야 합니다.

#### 함수 프로토타입
```
WebGMEAPI.fn.SetTMGDelegate = function (delegate){...}
```
|매개변수              |의미|
| ------------- |-------------|
| onEvent     |SDK 콜백 이벤트|

#### 샘플 코드  
```
gmeAPI.SetTMGDelegate(onEvent);
```





## 음성 채팅 관련 인터페이스
초기화한 후, SDK를 호출하여 방에 입장해야만 음성 채팅을 진행할 수 있습니다.
인증은 [준비 작업 문서].(./H5%20SDK%20Project%20Configuration.md)를 참조하십시오.

### 방 입장
생성한 인증 정보를 사용해 방에 입장하면 ITMG_MAIN_EVENT_TYPE_ENTER_ROOM이라는 콜백을 받게 됩니다. 방 입장 시 기본적으로 마이크 및 스피커를 켜지 않습니다.
인증은 엔지니어링 구성을 참조하십시오.

#### 함수 프로토타입
```
WebGMEAPI.fn.EnterRoom = function (roomId, roomType, authBuffer) {...}
```
|매개변수     |의미|
| ------------- |-------------|
| roomId 	|방 번호, 최대 127자 지원|
| roomType 	|방 오디오 유형|
| authBuffer	|인증 번호|



|오디오 유형|의미|매개변수|콘솔 추천 샘플링 속도 설정|적용 시나리오|
|-------|---|----|----------------|------|
| ITMG_ROOM_TYPE_FLUENCY			|보통 음질	|1|음질에 대해 특별한 요구가 없을 경우 16K 샘플링 속도라면 충분합니다.					|유창성이 우선이고 지연 시간이 매우 짧은 음성 채팅으로 게임에서 팀 배틀에 사용되고 FPS, MOBA와 같은 게임에 적합합니다.	|					
| ITMG_ROOM_TYPE_STANDARD			|표준 음질	|2|필요한 음질에 따라 16K/48K 샘플링 속도를 선택할 수 있습니다.				|음질이 비교적 좋고 시간 지연이 적당하여 마피아 게임, 보드 게임 등 캐주얼 게임의 실시간 통화 시나리오에 적합합니다.	|						
| ITMG_ROOM_TYPE_HIGHQUALITY		|고음질	|3|최적의 효과를 보증하기 위해서 콘솔에서 48K 샘플링 속도의 고음질 구성을 설정하기를 권장합니다.	|초고음질, 지연시간이 상대적으로 길어서 음악, 댄스 등 게임 및 음성 소셜류 앱에 적용합니다. 음악방송, 온라인 노래방 등 음질 요구가 있는 시나리오에 적용합니다.	|

- 음량 유형 또는 시나리오에 특별한 요구가 있는 경우 고객 서비스에 연락하십시오.
콘솔 샘플링 속도 설정은 게임 음성 효과에 직접 영향을 줄 수 있으므로 [콘솔](https://console.cloud.tencent.com/gamegme)에서 샘플링 속도 설정이 항목 사용 시나리오에 적합한지 다시 확인하십시오.


#### 샘플 코드  
```
 function bindButtonEvents() {
        $("#start_btn").click(function () {
            console.log('start!');
            //1. AuthBuffer 획득
            var FetchSigCgi = 'http://134.175.146.244:10005/';
            $.ajax({
                type: "POST",
                url: FetchSigCgi,
                dataType: 'json',
                data: {
                    sdkappid: cSdkAppId(),
                    roomid: cRoomNum(),
                    openid: cOpenID(),
                },
                success: function (json) {
                    //2. AuthBuffer 획득 성공
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
방 가입 완료 후 메시지 ITMG_MAIN_EVENT_TYPE_ENTER_ROOM을 발송하고, OnEvent 함수에서 판단합니다.

#### 샘플 코드  
```
 onEvent = function (eventType, result) {
         if (eventType === gmeAPI.event.ITMG_MAIN_EVENT_TYPE_ENTER_ROOM)
        {
            //방 입장 성공
        }
        else if (eventType === gmeAPI.event.ITMG_MAIN_EVNET_TYPE_USER_UPDATE)
        {
            app._data.downStreamInfoList = result.PeerInfo;//수신된 피어 정보는 아래 표를 참조하십시오.
            app._data.brSend = result.UploadBRSend;//업로드 비트 전송률
            app._data.rtt = result.UploadRTT;//업로드 RTT
        }
        else if (eventType === gmeAPI.event.ITMG_MAIN_EVENT_TYPE_EXIT_ROOM)
        {
            //방 퇴장 성공
        }
        else if (eventType === gmeAPI.event.ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT)
        {
            //방 연결 끊김
        }
    };
```


수신된 피어의 정보는 다음과 같습니다. downStreamInfoList: 

|매개변수      |의미|
| ------------- |------------|
| brRecv      |수신된 비트 전송률|
| delay      |수신 지연|
| jitterBufferMs      |지터 지연|
| jitterReceived      |지터 받기|


### 방 퇴장
해당 인터페이스를 호출하여 방에서 퇴장할 수 있습니다. 이것은 비동기 인터페이스이며 퇴장 후 콜백이 있고 반환 값은 AV_OK라면 비동기 전달이 성공했음을 의미합니다.
#### 함수 프로토타입  
```
WebGMEAPI.fn.ExitRoom = function (){...}
```
#### 샘플 코드  
```
gmeAPI.ExitRoom();
```

### 마이크 켜기/끄기
이 인터페이스는 마이크 켜기/끄기에 사용됩니다. 방 가입 시 기본적으로 마이크 및 스피커를 켜지 않습니다.

#### 함수 프로토타입  
```
WebGMEAPI.fn.EnableMic = function (bEnable) {...}
```
|매개변수      |의미|
| ------------- |------------|
| isEnabled      |마이크를 켜야 하는 경우 매개변수 TRUE를 가져오고, 마이크를 꺼야 하는 경우 매개변수 FALSE를 가져옵니다.|

#### 샘플 코드  
```
gmeAPI.EnableMic(false);
```



### 마이크 음량 설정
이 인터페이스는 마이크의 음량 설정에 사용됩니다. 매개변수 volume은 마이크의 음량 설정에 사용되며, 값이 0이면 무성임을 의미하고, 값이 100이면 음량이 커지지도 작아지지도 않음을 의미합니다. 기본값은 100입니다.

#### 함수 프로토타입  
```
WebGMEAPI.fn.SetMicVolume = function (volume){...}
```
|매개변수     |의미|
| -------------|-------------|
| volume    |음량 설정, 범위: 0~100|

#### 샘플 코드  
```
gmeAPI.SetMicVolume(100);
```


### 스피커 켜기/끄기
이 인터페이스는 스피커 켜기/끄기에 사용됩니다.
#### 함수 프로토타입  
```
WebGMEAPI.fn.EnableSpeaker = function (bEnable){...}
```
|매개변수              |의미|
| ------------- |------------|
| isEnabled           |스피커를 꺼야 하는 경우 매개변수 FALSE를 가져오고, 스피커를 켜야 하는 경우 매개변수 TRUE를 가져옵니다.|

#### 샘플 코드  
```
gmeAPI.EnableSpeaker(true);
```

