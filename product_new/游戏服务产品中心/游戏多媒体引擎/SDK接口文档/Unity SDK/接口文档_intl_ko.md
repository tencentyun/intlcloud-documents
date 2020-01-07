Unity 개발자가 원활히 테스트하고, Tencent Cloud Game Multimedia Engine(GME) 제품 API를 액세스하는데 도움을 드리고자 Unity 개발 액세스 기술 파일을 안내드립니다.

>이 파일은 GME sdk version：2.5 맞춤용입니다.

## GME 사용 중요사항

|중요 인터페이스     | 인터페이스 의미|
| ------------- |:-------------:|
|Init    |GME 초기화|
|Poll    |이벤트 콜백|
|EnterRoom |방에 들어가기  |
|EnableMic |마이크 온 |
|EnableSpeaker|스피커 온 |

>
- GME를 사용하기 전에 프로그래밍을 설정하지 않으면 SDK는 적용되지 않습니다. 
- GME 인터페이스를 적용하면 리턴값은 QAVError.OK이며, 수치는 0입니다. 
- GME 인터페이스 적용은 같은 스레드에서 진행해야 합니다.
- GME 방에 들어가려면 인증이 필요합니다. 파일중 인증 관련 사항을 참조하십시오.
- GME는 주기적으로 Poll 인터페이스를 호출하여 트리거 이벤트를 콜백해야 합니다.
- GME 콜백 정보는 콜백 메시지 리스트를 참조하십시오.
- 방에 들어간 후 디바이스를 조작해야 합니다. 
- 에러코드 상세내역은 [에러코드](https://intl.cloud.tencent.com/document/product/607/15173)를 참조하십시오.

## 실시간 음성 채팅 프로세스 이미지
![](https://main.qcloudimg.com/raw/810d0404638c494d9d5514eb5037cd37.png)

## 관련 API 초기기화
초기화하기 전에 SDK는 비초기화 상태로 적용되며, Init 인터페이스를 통해 SDK를 초기화해야 실시간 음성 채팅과 오프라인 음성 메시지를 사용할 수 있습니다.
사용문제는 [일반 문제](https://intl.cloud.tencent.com/document/product/607/30254)를 참조하십시오

|인터페이스     | 인터페이스 의미   |
| ------------- |:-------------:|
|Init    |GME 초기화|
|Poll    |트리거 이벤트 콜백|
|Pause   |시스템 일시정지|
|Resume |시스템 복구|
|Uninit    |GME 디이니셜라이제이션(Deinitialization)|

### 인스턴스 획득
ITMGContext 방법으로 Context 인스턴스를 획득하시기 바랍니다. 직접 QAVContext.GetInstance()를 사용하여 인스턴스를 획득하는 것을 금하십시오.

### SDK 초기화

파라미터 획득은 [액세스 매뉴얼](ttps://intl.cloud.tencent.com/document/product/607/10782)을 참조하십시오.
이 API는 Tencent Cloud 콘솔의 SDKAppID 계정을 파라미터로 적용해야 합니다. 추가로 openId가 필요하며, 이 openId는 한 유저의 유일한 인증으로 앱 개발자가 스스로 룰을 확정 및 앱에서 중복하지 말아야 합니다(현재 INT64만 지원합니다).
>SDK를 초기화해야 방에 들어갈 수 있습니다.
>
>####  함수 프로토타입

```
ITMGContext Init(string sdkAppId, string openId)
```

|파라미터     | 타입         |의미|
| ------------- |:-------------:|-------------|
| sdkAppId    |String  |Tencent Cloud 콘솔의 sdkAppId 계정|
| openId    |String  |openId 오직 Int64 타입(string으로 전환하여 추가)만 지원하며, 반드시 10,000보다 커야 합니다. 유저 표기용입니다|

####  예시 코드 


```
int ret = ITMGContext.GetInstance().Init(str_appId, str_openID);
	if (ret != QAVError.OK) {
		return;
	}
```
### 트리거 이벤트 콜백
update 라이프사이클 주기내 Poll를 호출하여 이벤트 콜백을 트리거할 수 있습니다.
####  함수 프로토타입

```
ITMGContext public abstract int Poll();
```
### 시스템 일시정지
시스템에 Pause 이벤트가 발생 시, 동시에 엔진에 Pause를 공지해야 합니다.
####  함수 프로토타입

```
ITMGContext public abstract int Pause()
```

### 시스템 복구
시스템에 Resume 이벤트가 발생 시, 동시에 엔진에 Resume을 공지해야 합니다. Resume 인터페이스는 실시간 음성 채팅만 복구합니다. 
####  함수 프로토타입

```
ITMGContext  public abstract int Resume()
```



### SDK 디이니셜라이제이션(Deinitialization)
SDK 디이니셜라이제이션, 비초기화 상태로 됩니다. 계정을 변경하려면 디이니셜라이제션화해야 합니다. 
#### 함수 프로토타입

```
ITMGContext public abstract int Uninit()
```





## 실시간 음성 채팅방 관련 API
초기화 후에 SDK를 호출하여 방에 들어가야, 실시간 음성 통화가 가능합니다.
사용 문제는 [실시간 음성 채팅 관련 문제](https://intl.cloud.tencent.com/document/product/607/30257)를 참조하십시오.

|API     | API 의미   |
| ------------- |:-------------:|
|GenAuthBuffer    |초기화 인증|
|EnterRoom   |방에 가입하기|
|IsRoomEntered   |방에 들어갔는지 여부|
|ExitRoom |방 나오기|
|ChangeRoomType |유저 방 가청 주파수 타입 변경|
|GetRoomType |유저 방 가청 주파수 타입 획득|


### 인증 메시지
AuthBuffer를 생성하여 기능을 암호화하고 인증합니다. 백그라운드 배포 관련 사항은 [인증 보안키](https://intl.cloud.tencent.com/document/product/607/12218)를 참조하십시오.    
오프라인 음성 메시지를 인증하려면 방번호 파라미터터는 반드시 null로 입력해야 합니다.

#### 함수 프로토타입
```
QAVAuthBuffer GenAuthBuffer(int appId, string roomId, string openId, string key)
```
|파라미터     | 타입         |의미|
| ------------- |:-------------:|-------------|
| appId    |int   |Tencent Cloud의 sdkAppId 계정|
| roomId    |string   |방번호，최대 127개 캐릭터를 지원합니다(오프라인 음성 방번호 파라미터는 반드시 null로 입력해야 합니다)|
| openID    |string |유저 상징 |
| key    |string |Tencent Cloud [콘솔](https://console.cloud.tencent.com/gamegme)의 보안키|


####  예시 코드  
```
byte[] GetAuthBuffer(string appId, string userId, string roomId)
    {
	return QAVAuthBuffer.GenAuthBuffer(int.Parse(appId), roomId,openID, "a495dca2482589e9");
}
```



### 방 가입하기
생성한 인증 메시지로 방에 들어갑니다. 방에 가입하기는 기본적으로 마이크와 스피커를 오픈하지 않습니다.

범위내 음성 액세스 프로세스는 [레인지 음성](https://intl.cloud.tencent.com/document/product/607/17972)을 참조하십시오.


####  함수 프로토타입
```
ITMGContext EnterRoom(string roomId, int roomType, byte[] authBuffer)
```
|파라미터     | 타입         |의미|
| ------------- |:-------------:|-------------|
| roomId|string    |방번호, 최대 127개 캐릭터를 지원합니다|
| roomType |ITMGRoomType|방 가청 주파수 타입|
| authBuffer |Byte[] |인증 코드|

방 가청 주파수 타입은 [음질 선택](ttps://intl.cloud.tencent.com/document/product/607/18522)을 참조하십시오.


####  예시 코드  
```
ITMGContext.GetInstance().EnterRoom(roomId, ITMG_ROOM_TYPE_FLUENCY, authBuffer);
```

### 방 가입 이벤트 콜백
방에 가입하면 위탁(delegate) 함수를 통해 콜백합니다. 여기에 result와 error_info 등 2종 메시지를 포함합니다.

#### 함수 프로토타입
```
위탁 함수: 
public delegate void QAVEnterRoomComplete(int result, string error_info);
이벤트 함수: 
public abstract event QAVEnterRoomComplete OnEnterRoomCompleteEvent;
```

####  예시 코드  
```
이벤트 모니터링: 
ITMGContext.GetInstance().OnEnterRoomCompleteEvent += new QAVEnterRoomComplete(OnEnterRoomComplete);

리스너 처리: 
void OnEnterRoomComplete(int err, string errInfo)
    {
	if (err != 0) {
	    ShowWarnning (string.Format ("join room failed, err:{0}, errInfo:{1}", err, errInfo));
	    return;
	}else{
	    ShowWarnning(string.Format(“기존 음성방id:{0}, 다른 단말기에서 이 방에 가입하여 통화하세요”, roomId));
    }
}
```

### 방에 들어갔는지 여부 판단
이 인터페이스를 호출하여 방에 들어갔는지 여부를 판단할 수 있습니다. 리턴값은 bool 타입입니다.

####  함수 프로토타입  
```
ITMGContext abstract bool IsRoomEntered()
```
####  예시 코드  
```
ITMGContext.GetInstance().IsRoomEntered();
```

### 방 나가기
이 인터페이스를 호출하여 방에서 나갈 수 있습니다. 비동기 인터페이스로, 리턴값은 AV_OK일 경우 비동기 딜리버리하였음을 뜻합니다.

>혹 애플리케이션에 방에서 나간 후 바로 방에 들어오는 솔루션이 있다면, 인터페이스 호출 프로세스에서 개발자는 ExitRoom의 콜백 RoomExitComplete 공지를 대기할 필요가 없으며, 직접 인터페이스를 호출할 수 있습니다

#### 함수 프로토타입  
```
ITMGContext ExitRoom()
```
####  예시 코드  
```
ITMGContext.GetInstance().ExitRoom();
```

### 방 나가기 콜백
방 나가기를 완료한 콜백입니다. 위탁을 통해 메시지를 전송합니다.
#### 함수 프로토타입  
```
위탁 함수: 
ublic delegate void QAVExitRoomComplete();
이벤트 함수: 
public abstract event QAVExitRoomComplete OnExitRoomCompleteEvent; 
```
####  예시 코드  
```
이벤트 모니터링:
ITMGContext.GetInstance().OnExitRoomCompleteEvent += new QAVExitRoomComplete(OnExitRoomComplete);
리스너 처리: 
void OnExitRoomComplete(){
    //방에서 나간 후 처리
}
```

### 유저 방 가청 주파수 타입 획득
이 인터페이스로 유저 방 가청 주파수 타입을 획득할 수 있습니다. 리턴값은 0일 경우 유저 방 가청 주파수 타입을 획득 시에 에러가 나타남을 뜻하며, 방 가청 주파수 타입은 EnterRoom 인터페이스를 참조하십시오.

#### 함수 프로토타입  
```
ITMGContext ITMGRoom public  int GetRoomType()
```

#### 예시 코드  
```
ITMGContext.GetInstance().GetRoom().GetRoomType();
```

### 유저 방 가청 주파수 타입 수정
이 인터페이스는 유저 방 가청 주파수 타입을 수정합니다.
####  함수 프로토타입  
```
ITMGContext ITMGRoom public void ChangeRoomType(ITMGRoomType roomtype)
```


|파라미터     | 타입         |의미|
| ------------- |:-------------:|-------------|
| roomtype    |ITMGRoomType    |원하는 방 변경 타입, 방 가청 주파수 타입은 EnterRoom 인터페이스를 참조하십시오|

####  예시 코드  
```
ITMGContext.GetInstance().GetRoom().ChangeRoomType(ITMG_ROOM_TYPE_FLUENCY);
```



### 방 가청주파수 타입 콜백 수정
스스로 방 타입을 설정합니다. 방 타입을 설정하면 위탁을 통해 수정한 관련 메시지를 전송합니다. 

|리턴 파라미터     | 의미  |
| ------------- |:-------------:|
| result    |0 성공함을 뜻함|
| error_info    |혹 실패하면, 에러 메시지를 전송합니다|

```
위탁 함수: 
public delegate void QAVOnChangeRoomtypeCallback(int result, string error_info);

이벤트 함수:
public abstract event QAVCallback OnChangeRoomtypeCallback; 
```

####  예시 코드  
```
이벤트 모니터링: 
ITMGContext.GetInstance().OnChangeRoomtypeCallback += new QAVOnChangeRoomtypeCallback(OnChangeRoomtypeCallback);
리스너 처리: 
void OnChangeRoomtypeCallback(int result, string error_info){
    //방 타입 설정 완료 후 처리
}
```

### 방 타입 변경 공지
유저가 스스로 방 타입을 수정하거나, 방내 기타 유저가 방 타입을 수정하면, 즉 방 타입이 변경되면 이 콜백함수를 호출합니다. 콜백함수를 통해 서비스측에 방 타입이 변경됨을 알리며, 방 타입을 리턴합니다. EnterRoom 인터페이스를 참조하십시오.
```
위탁 함수: 
public delegate void QAVOnRoomTypeChangedEvent(int roomtype);

이벤트 함수: 
public abstract event QAVOnRoomTypeChangedEvent OnRoomTypeChangedEvent;	
```
####  예시 코드  
```
이벤트 모니터링: 
ITMGContext.GetInstance().OnRoomTypeChangedEvent += new QAVOnRoomTypeChangedEvent(OnRoomTypeChangedEvent);
리스너 처리: 
void OnRoomTypeChangedEvent(int roomtype){
    //방 타입 변경 후 처리
}
```



### 멤버 상태 변화
이 이벤트는 상태 변화시에만 공지하며, 상태 변화가 없을 경우 공지하지 않습니다. 혹 멤버의 상태를 실시간 획득하려면 이전 레이어에서 공지를 받을 때 캐시하십시오. 이벤트 메시지는 ITMG_MAIN_EVNET_TYPE_USER_UPDATE이며, event_id, count 및 openIdList를 포함합니다. OnEvent 함수에서 이벤트 메시지를 판단합니다.
가청 주파수 이벤트 공지는 임계값이 존재합니다. 이 임계값을 초과하면 공지를 발송합니다. 2초 이상 가청 주파수 패킷을 받지 못할 때에만 “멤버가 가청 주파수 패킷 발송을 초과하였습니다”는 메시지를 띄웁니다.

|event_id     | 의미         |응용측 유지 보수 콘텐츠|
| ------------- |:-------------:|-------------|
|ITMG_EVENT_ID_USER_ENTER    |멤버가 방에 들어왔습니다|애플리케이션측 멤버 케어 리스트|
|ITMG_EVENT_ID_USER_EXIT    |멤버가 방을 나갔습니다|애플리케이션측 멤버 케어 리스트|
|ITMG_EVENT_ID_USER_HAS_AUDIO    |멤버가 가청 주파수 패킷을 발송했습니다|애플리케이션측 통화 멤버 케어 리스트|
|ITMG_EVENT_ID_USER_NO_AUDIO    |멤버가 가청 주파수 패킷 발송을 종료했습니다|애플리케이션측 통화 멤버 케어 리스트|

#### 예시 코드
```
위탁 함수:
public delegate void QAVEndpointsUpdateInfo(int eventID, int count, [MarshalAs(UnmanagedType.LPArray, SizeParamIndex = 1)]string[] openIdList);
이벤트 함수:
public abstract event QAVEndpointsUpdateInfo OnEndpointsUpdateInfoEvent;

이벤트 모니터링:
ITMGContext.GetInstance().OnEndpointsUpdateInfoEvent += new QAVEndpointsUpdateInfo(OnEndpointsUpdateInfo);
리스너 처리:
void OnEndpointsUpdateInfo(int eventID, int count, string[] openIdList)
{
    //처리

		    switch (eventID)
 		    {
 		    case ITMG_EVENT_ID_USER_ENTER:
  			    //멤버가 방에 들어왔습니다
  			    break;
 		    case ITMG_EVENT_ID_USER_EXIT:
  			    //멤버가 방을 나갔습니다
			    break;
		    case ITMG_EVENT_ID_USER_HAS_AUDIO:
			    //멤버가 가청 주파수 패킷을 발송했습니다
			    break;
		    case ITMG_EVENT_ID_USER_NO_AUDIO:
			    //멤버가 가청 주파수 패킷 발송을 종료했습니다
			    break;
		  
		    default:
			    break;
 		    }
		break;
}

```


### 품질 모니터링 이벤트
품질 모니터링 이벤트, 이벤트 메시지는 ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_QUALITY이며, 리턴 파라미터는 weight, floss  및 delay입니다. 메시지 의미는 다음과 같으며, OnEvent 함수에서 이벤트 메시지를 판단합니다.

|파라미터     | 의미         |
| ------------- |-------------|
|weight    |범위는 1-5입니다. 수치는 5일 경우 음질이 아주 좋음, 수치는 1일 경우 음질이 아주 차해 사용 불가능함을 뜻하며, 수치 0은 초기값으로 의미가 없습니다.|
|floss    |패킷 손실률|
|delay    |가청 주파수 도착 딜레이 시간(ms)|


## 실시간 음성 채팅 가청 주파서 API
SDK를 초기화하여 방에 들어오면, 방에서 실시간 가청 주파서 음성 관련 인터페이스를 사용할 수 있습니다.
유저 인터페이스를 클릭하여 마이크/스피커 버튼을 온/오프할 때 다음 방식을 권장드립니다: 
- 대부분의 게임류 앱에 대해 EnableMic 및 EnableSpeaker 인터페이스를 호출할것을 권장드립니다. 즉 항상 EnableAudioCaptureDevice/EnableAudioSend 와 EnableAudioPlayDevice/EnableAudioRecv 인터페이스를 동시에 호출합니다;
- 소셜 타입의 앱 등 기타 타입의 모바일 앱의 경우, 수집 디바이스를 오픈하거나 종료하면 전체 디바이스(수집 및 플레이)를 재기동해야 합니다. 혹 이때 앱에서 BGM을 틀고있다면 BMG 재생도 함께 중지합니다. 업/다운 스트리밍 방식으로 마이크 이펙트를 온/오프할 수 있다면, 플레이 디바이스는 정지하지 않습니다. 구체적인 호출방식은: 방에 들어설 때 EnableAudioCaptureDevice(true) && EnableAudioPlayDevice(true)를 1회 호출합니다. 마이크 온/오프를 클릭 시 EnableAudioSend/Recv만 호출하여 가청 주파수 스트리밍 발송/수락을 제어할 수 있습니다.
- 혹 별도로 수집 혹은 플레이 디바이스를 릴리즈하려면, EnableAudioCaptureDevice 및 EnableAudioPlayDevice인터페이스를 참조하십시오.
- pause를 호출하여 가청 주파수 엔진을 일시정지합니다. resume을 호출하여 가청 주파수 엔진을 복구합니다.

|인터페이스     | 인터페이스 의미   |
| ------------- |:-------------:|
|EnableMic    |마이크 온/오프|
|GetMicState    |마이크 상태 획득|
|EnableAudioCaptureDevice    |온/오프 수집 디바이스|
|IsAudioCaptureDeviceEnabled    |수집 디바이스 상태 획득|
|EnableAudioSend    |가청 주파수 업스트리밍 닫기 오픈|
|IsAudioSendEnabled    |가청 주파수 업스트리밍 상태 획득|
|GetMicLevel    |실시간 마이크 사운드 획득|
|GetSendStreamLevel|가청 주파서 업스트리밍 사운드 획득|
|SetMicVolume    |마이크 사운드 설정|
|GetMicVolume    |마이크 사운드 획득|
|EnableSpeaker    |스피커 온/오프|
|GetSpeakerState    |스피커 상태 획득|
|EnableAudioPlayDevice    |온/오프 플레이 디바이스|
|IsAudioPlayDeviceEnabled    |플레이 디바이스 상태 획득|
|EnableAudioRecv    |가청 주파수 다운스트리밍 닫기 오픈|
|IsAudioRecvEnabled    |가청 주파수 다운스트리밍 상태 획득|
|GetSpeakerLevel    |실시간 스피커 사운드 획득|
|GetRecvStreamLevel|방내 기타 멤버 다운스트리밍 실시간 사운드 획득|
|SetSpeakerVolume    |스피커 사운드 설정|
|GetSpeakerVolume    |스피커 사운드 획득|
|EnableLoopBack    |온/오프 루프 백|



### 마이크 닫기 오픈
이 인터페이스는 마이크 닫기를 오픈합니다. 방에 가입하면 기본적으로 마이크와 스피커를 오픈하지 않습니다.
EnableMic = EnableAudioCaptureDevice + EnableAudioSend.
####  함수 프로토타입  
```
ITMGAudioCtrl EnableMic(bool isEnabled)
```
|파라미터     | 타입         |의미|
| ------------- |:-------------:|-------------|
| isEnabled    |boolean     |혹 마이크를 온하면 파라미터는 tru로 입력되며, 마이크를 오프하였을 경우, 파라미터는 false입니다|

#### 예시 코드  
```
마이크 온
ITMGContext.GetInstance().GetAudioCtrl().EnableMic(true);
```

### 마이크 상태 획득
이 인터페이스는 마이크 상태를 읽어옵니다. 리턴값이 0일 경우, 마이크를 오프한 상태이며, 리턴값이 1일 경우 마이크를 온한 상태입니다.
####  함수 프로토타입  
```
ITMGAudioCtrl GetMicState()
```
####  예시 코드  
```
micToggle.isOn = ITMGContext.GetInstance().GetAudioCtrl().GetMicState();
```

### 수집 디바이스 오픈/종료
이 인터페이스는 수집 디바이스를 오픈/종료할 수 있습니다. 방에 가입시 기본적으로 디바이스를 오픈하지 않습니다.
- 오직 방에 들어가야 이 인터페이스를 호출할 수 있스니다. 방에서 나오면 스스로 디바이스를 종료합니다.
- 모바일의 경우, 수집 디바이스를 오픈하면 일반적으로 권한 신청이 따르며, 사운드 타입을 조작할 수 있습니다.

####  함수 프로토타입  
```
ITMGAudioCtrl int EnableAudioPlayDevice(bool isEnabled)
```
|파라미터     | 타입         |의미|
| ------------- |:-------------:|-------------|
| isEnabled    |bool     |수집 디바이스를 오픈해야 하면, 파라미터는 true로 입력하며, 수집 디바이스를 종료할 경우 파라미터는 false입니다|

#### 예시 코드

```
수집 디바이스 오픈
ITMGContext.GetInstance().GetAudioCtrl().EnableAudioCaptureDevice(true);
```

### 수집 디바이스 상태 획득
이 인터페이스는 수집 디바이스 상태를 읽어옵니다.
#### 함수 프로토타입

```
ITMGAudioCtrl bool IsAudioCaptureDeviceEnabled()
```
#### 예시 코드

```
bool IsAudioCaptureDevice = ITMGContext.GetInstance().GetAudioCtrl().IsAudioCaptureDeviceEnabled();
```

### 가청 주파수 업스트리밍 온/오프
이 인터페이스는 가청 주파수 업스트리밍을 온/오프합니다. 혹 수집 디바이스를 온하였을 경우, 수집한 가청 주파수 데이터를 발송하며, 수집 디바이스를 오프하였을 경우, 무음입니다. 수집 디바이스의 온/오프는 EnableAudioCaptureDevice 인터페이스를 참조하십시오.

#### 함수 프로토타입

```
ITMGAudioCtrl int EnableAudioSend(bool isEnabled)
```
|파라미터     | 타입         |의미|
| ------------- |:-------------:|-------------|
| isEnabled    |bool     |가청 주파수 업스트리밍을 오픈하면, 파라미터는 tru로 입력되며, 가청 주파수 업스트리밍을 종료하였을 경우 파라미터는 false입니다|

####  예시 코드  

```
ITMGContext.GetInstance().GetAudioCtrl().EnableAudioSend(true);
```

### 가청 주파수 업스트리밍 상태 획득
이 인터페이스는 가청 주파수 업스트리밍 상태를 읽어옵니다.
#### 함수 프로토타입  
```
ITMGAudioCtrl bool IsAudioSendEnabled()
```
#### 예시 코드  
```
bool IsAudioSend = ITMGContext.GetInstance().GetAudioCtrl().IsAudioSendEnabled();
```

### 마이크 실시간 사운드 획득
이 인터페이스는 마이크 실시간 사운드를 읽어오며, 리턴값은 int 타입입니다.
####  함수 프로토타입  
```
ITMGAudioCtrl int GetMicLevel
```
#### 예시 코드  
```
ITMGContext.GetInstance().GetAudioCtrl().GetMicLevel();
```

### 가청 주파수 업스트리밍 실시간 사운드 획득
이 인터페이스는 가청 주파수 업스트리밍 실시간 사운드를 읽어옵니다. 리턴값은 int 타입이며, 값범위는 0부터 100입니다.
#### 함수 프로토타입  
```
ITMGAudioCtrl int GetSendStreamLevel()
```
####  예시 코드  
```
int Level = ITMGContext.GetInstance().GetAudioCtrl().GetSendStreamLevel();
```

### 마이크 사운드 설정
이 인터페이스는 마이크 사운드를 설정합니다. 파라미터 volume은 마이크 사운드를 설정합니다. 수치가 0일 경우 무음을 뜻하며, 수치가 100일 경우 사운드 비추가 비감소를 뜻하며, 기본값은 100입니다.

#### 함수 프로토타입  
```
ITMGAudioCtrl SetMicVolume(int volume)
```
|파라미터     | 타입         |의미|
| ------------- |:-------------:|-------------|
| volume    |int      |사운드 설정, 범위는 0부터 200|

#### 예시 코드  

```
int micVol = (int)(value * 100);
ITMGContext.GetInstance().GetAudioCtrl().SetMicVolume (micVol);
```
### 마이크 사운드 획득
이 인터페이스는 마이크 사운드를 읽어옵니다. 리턴값은 int 타입 수치이며, 리턴값 101은 SetMicVolume 인터페이스를 호출하지 않음을 뜻합니다.

#### 함수 프로토타입  
```
ITMGAudioCtrl GetMicVolume()
```
#### 예시 코드  
```
ITMGContext.GetInstance().GetAudioCtrl().GetMicVolume();
```

### 스피커 온/오프
이 인터페이스는 스피커를 온/오프합니다.
EnableSpeaker = EnableAudioPlayDevice +  EnableAudioRecv.
#### 함수 프로토타입  
```
ITMGAudioCtrl EnableSpeaker(bool isEnabled)
```
|파라마티     | 타입         |의미|
| ------------- |:-------------:|-------------|
| isEnabled    |bool        |스피커를 오프하려면 파라미터는 false로 입력하며, 스피커를 온할 경우, 파라미터는 true입니다|

#### 예시 코드  
```
스피커 온
ITMGContext.GetInstance().GetAudioCtrl().EnableSpeaker(true);
```

### 스피커 상태 획득
이 인터페이스는 스피커 상태를 획득합니다. 리턴값은 0일 경우 스피커가 오프한 상태이며, 리턴값이 1일 경우 스피커가 온, 리턴값이 2일 경우 스피커 디바이스는 조작중임을 의미합니다. 
#### 함수 프로토타입  
```
ITMGAudioCtrl GetSpeakerState()
```

#### 예시 코드  
```
speakerToggle.isOn = ITMGContext.GetInstance().GetAudioCtrl().GetSpeakerState();
```



### 플레이 디바이스 오픈/종료
이 인터페이스는 플레이 디바이스를 오픈/종료합니다.

#### 함수 프로토타입  
```
ITMGAudioCtrl EnableAudioPlayDevice(bool isEnabled)
```
|파라미터     | 타입         |의미|
| ------------- |:-------------:|-------------|
| isEnabled    |bool        |플레이 디바이스를 종료하려면 파라미터는 false로 입력하며, 디바이스를 오픈할 경우 파라미터는 true입니다|

#### 예시 코드  
```
플레이 디바이스 오픈
ITMGContext.GetInstance().GetAudioCtrl().EnableAudioPlayDevice(true);
```

### 플레이 디바이스 상태를 획득합니다
이 인터페이스는 플레이 디바이스 상태를 읽어옵니다.
#### 함수 프로토타입

```
ITMGAudioCtrl bool IsAudioPlayDeviceEnabled()
```
#### 예시 코드  

```
bool IsAudioPlayDevice = ITMGContext.GetInstance().GetAudioCtrl().IsAudioPlayDeviceEnabled();
```

### 가청 주파수 다운스트리밍 온/오프
이 인터페이스는 가청 주파수 다운스트리밍을 온/오프합니다. 혹 플레이 디바이스를 오픈하였을 경우, 방내 기타 유저의 가청 주파수 데이터를 재생합니다. 혹 플레이 디바이스를 종료하였을 경우, 무음상태가 됩니다. 플레이 디바이스 오픈/종료는 EnableAudioPlayDevice 인터페이스를 참조하십시오.

#### 함수 프로토타입  

```
ITMGAudioCtrl int EnableAudioRecv(bool isEnabled)
```
|파라미터     | 타입         |의미|
| ------------- |:-------------:|-------------|
| isEnabled    |bool     |가청 주파수 다운스트리밍을 오픈하려면 파라미터는 true로 입력하며, 종료할 경우 파라미터는 false입니다|

#### 예시 코드  

```
ITMGContext.GetInstance().GetAudioCtrl().EnableAudioRecv(true);
```



### 가청 주파수 다운스트리밍 획득
이 인터페이스는 가청 주파수 다운스트리밍 상태를 읽어옵니다
#### 함수 프로토타입  
```
ITMGAudioCtrl bool IsAudioRecvEnabled()
```

#### 예시 코드  
```
bool IsAudioRecv = ITMGContext.GetInstance().GetAudioCtrl().IsAudioRecvEnabled();
```

### 스피커 실시간 사운드 획득
이 인터페이스는 스피커 실시간 사운드를 읽어옵니다. 리턴값은 int 타입 수치이며, 스피커 실시간 사운드를 뜻합니다.
#### 함수 프로토타입  
```
ITMGAudioCtrl GetSpeakerLevel()
```

#### 예시 코드  
```
ITMGContext.GetInstance().GetAudioCtrl().GetSpeakerLevel();
```

### 방내 기타 멤버의 다운스트리밍 실시간 사운드 획득
이 인터페이스는 방내 다른 멤버의 다운스트리밍 실시간 사운드를 읽어옵니다. 리턴값은 int 타입이며, 값범위는 0부터 100입니다.
#### 함수 프로토타입  
```
ITMGAudioCtrl int GetRecvStreamLevel(string openId)
```

|파라미터     | 타입         |의미|
| ------------- |:-------------:|-------------|
| openId    |string       |방내 기타 멤버의 openId|

#### 예시 코드  
```
int Level = ITMGContext.GetInstance().GetAudioCtrl().GetRecvStreamLevel(openId);
```

### 스피커 사운드 설정
이 인터페이스는 스피커 사운드를 설정합니다.
파라미터 volume은 스피커 사운드를 설정합니다. 수치가 0일 시 무음을 뜻하며, 수치가 100일 경우 사운드를 증가하지도 줄이지도 않음을 의미합니다. 기본값은 100입니다.

#### 함수 프로토타입  
```
ITMGAudioCtrl SetSpeakerVolume(int volume)
```
|파라미터     | 타입         |의미|
| ------------- |:-------------:|-------------|
| volume    |int        |사운드를 설정합니다. 범위는 0부터 200입니다|

#### 예시 코드  
```
int speVol = (int)(value * 100);
ITMGContext.GetInstance().GetAudioCtrl().SetSpeakerVolume(speVol);
```

### 스피커 사운드 획득

이 인터페이스는 스피커 사운드를 읽어옵니다. 리턴값은 int 타입의 수치이며, 스피커 사운드를 의미합니다. 리턴값 101은 SetSpeakerVolume 인터페이스를 호출하지 않았음을 의미합니다.
Level은 실시간 사운드를, Volume은 스피커 사운드를 뜻하며, 최종 사운드는 Level*Volume%에 대응합니다. 실시간 사운드의 수치가 100일 경우, Volume의 수치는 60이며 최종 사운드는 60입니다. 

#### 함수 프로토타입  
```
ITMGAudioCtrl GetSpeakerVolume()
```
#### 예시 코드  
```
ITMGContext.GetInstance().GetAudioCtrl().GetSpeakerVolume();
```


### 인이어 모니터링 기동
이 인터페이스는 인이어 모니터링을 기동합니다.
#### 함수 프로토타입  
```
ITMGContext GetAudioCtrl EnableLoopBack(bool enable)
```
|파라미터     | 타입         |의미|
| ------------- |:-------------:|-------------|
| enable    |bool         |설정 작동 여부|

####  예시 코드  
```
ITMGContext.GetInstance().GetAudioCtrl().EnableLoopBack(true);
```

### 디바이스 점용, 릴리즈 이벤트 콜백
방에서 디바이스를 점용, 릴리즈 시에 콜백합니다. 위탁을 통해 이벤트 관련 메시지를 전달합니다.

```
위탁 함수: 
public delegate void QAVOnDeviceStateChangedEvent(int deviceType, string deviceId, bool openOrClose);
이벤트 함수: 
public abstract event QAVOnDeviceStateChangedEvent OnDeviceStateChangedEvent;
```

|파라미터     | 타입         |의미|
| ------------- |:-------------:|-------------|
| deviceType    |int       |1 수집 디바이스를 의미, 2 플레이 디바이스를 뜻함|
| deviceId    |string |디바이스 GUID，디바이스를 표기합니다. 오직 Windows와 Mac에 적용합니다|
| openOrClose    |bool  |수집 디바이스/플레이 디바이스 점용 혹은 릴리즈|


|파라미터     | 수치         |의미|
| ------------- |:-------------:|-------------|
| AUDIODEVICE_CAPTURE    |1       |수집 디바이스를 뜻함|
| AUDIODEVICE_PLAYER    |2 |플레이 디바이스 의미|

#### 예시 코드  

```
이벤트 모니터링:
ITMGContext.GetInstance().GetAudioCtrl().OnDeviceStateChangedEvent += new QAVAudioDeviceStateCallback(OnAudioDeviceStateChange);
리스너 처리:
void QAVAudioDeviceStateCallback(int deviceType, string deviceId, bool openOrClose){
    //디바이스 점용과 릴리즈 이벤트 관련 콜백 처리
}
```

## 오프라인 음성 메시지 STT(음성 텍스트 변환) 프로세스
![](https://main.qcloudimg.com/raw/9ef5e5e4ebc8e63bcd7bfbea6cfb94cc.png)



## 오프라인 음성 메시지
초기화하기 전에 SDK는 비초기화 상태이며, Init 인터페이스를 통해 SDK를 초기화해야 실시간 음성 채팅 및 오프라인 음성 메시지를 사용할 수 있습니다.
사용 문제는 [오프라인 음성 메시지 관련 문제](https://intl.cloud.tencent.com/document/product/607/30258)를 참조하십시오.

### 초기화 관련 인터페이스

|인터페이스     |인터페이스 의미   |
| ------------- |:-------------:|
|Init    |GME 초기화|
|Poll    |이벤트 콜백|
|Pause   |시스템 일시정지|
|Resume |시스템 복구|
|Uninit    |GME 초기화 취소 |


### 오프라인 음성 메시지 관련 인터페이스
|인터페이스     | 인터페이스 의미   |
| ------------- |:-------------:|
|ApplyPTTAuthbuffer    |인증 초기화|
|SetMaxMessageLength    |음성 메시지 최대 길이 제한|
|StartRecording|녹음 시작|
|StartRecordingWithStreamingRecognition|스트리밍 녹음 시작|
|PauseRecording|녹음 일시정지|
|ResumeRecording|녹음 복구|
|StopRecording    |녹음 정지|
|CancelRecording|녹음 취소|
|GetMicLevel|오프라인 음성 메시지 실시간 마이크 레벨 획득|
|SetMicVolume|오프라인 음성 메시지 녹화 볼륨 설정|
|GetMicVolume|오프라인 음성 메시지 녹화 볼륨 획득|
|GetSpeakerLevel|오프라인 음성 메시지 실시간 스피커 레벨 획득 |
|SetSpeakerVolume|오프라인 음성 메시지 재생 볼륨 설정|
|GetSpeakerVolume|오프라인 음성 메시지 재생 볼륨 획득|
|UploadRecordedFile |음성 파일 업로드|
|DownloadRecordedFile|음성 파일 다운로드|
|PlayRecordedFile |음성 재생|
|StopPlayFile|음성 재생 중지|
|GetFileSize |음성 파일 크기|
|GetVoiceFileDuration|음성 파일 길이|
|SpeechToText |음성을 텍스트로 인식|

### 인증 초기화
SDK를 초기화한 후에 인증 초기화를 호출하십시오. authBuffer 획득은 윗글의 실시간 음성 채팅 인증 정보 인터페이스를 참조하십시오.
#### 함수 프로토타입  
```
ITMGPTT int ApplyPTTAuthbuffer (byte[] authBuffer)
```
|파라미터     | 유형         |의미|
| ------------- |:-------------:|-------------|
| authBuffer    |byte[]                   |인증|

#### 예시 코드  
```
ITMGContext.GetInstance().GetPttCtrl().ApplyPTTAuthbuffer(authBuffer);
```

### 음성 메시지 최대 길이 제한
음성 메시지 최대 길이를 60초로 제한합니다.

####  함수 프로토타입

```
ITMGPTT int SetMaxMessageLength(int msTime)
```
|파라미터     | 유형         |의미|
| ------------- |:-------------:|-------------|
| msTime    |int                    |음성 메시지 길이, 단위 ms|

#### 예시 코드  
```
ITMGContext.GetInstance().GetPttCtrl().SetMaxMessageLength(60000); 
```


### 녹음 시작
이 인터페이스는 녹음을 시작합니다. 녹음된 파일 업로드가 완료되어야 음성 문자 변환 등 작업을 진행할 수 있습니다.
####  함수 프로토타입  
```
ITMGPTT int StartRecording(string fileDir)
```
|파라미터     | 유형         |의미|
| ------------- |:-------------:|-------------|
| fileDir    |string                      |음성 보관 경로|

####  예시 코드  
```
string recordPath = Application.persistentDataPath + string.Format ("/{0}.silk", sUid++);
int ret = ITMGContext.GetInstance().GetPttCtrl().StartRecording(recordPath);
```

### 녹음 기동 콜백
녹음 완료 시 콜백은 위탁을 통해 메시지를 전송합니다.
#### 함수 프로토타입  
```
위탁 함수: 
public delegate void QAVRecordFileCompleteCallback(int code, string filepath); 
이벤트 함수: 
public abstract event QAVRecordFileCompleteCallback OnRecordFileComplete;
```
|파라미터     | 타입         |의미|
| ------------- |:-------------:|-------------|
| code    |string                      |code가 0일 경우 레코딩 완료|
| filepath    |string                      |레코딩 저장 주소|

#### 에러 코드
|에러코드값 |원인  |제안 방안        |
|-----|------|------|
|4097   |파라미터가 비어있음|코드 중 인터페이스 파라미터가 올바른지 확인하십시오|
|4098   |초기화 오류|디바이스가 점용되었는지, 권한이 정상인지, 초기화가 정상적으로 완료되었는지 점검하십시오|
|4099   |녹화 중|SDK 녹화 기능을 올바른 타이밍에 사용하고 있는지 확인하십시오|
|4100   |오디오 데이터 수집 안됨|마이크 장치가 정상인지 점검하십시오|
|4101   |녹음 시, 파일 액세스 오류|파일이 존재하는지, 파일 경로가 합법적인지 확인하십시오|
|4102   |마이크 권한 미부여|SDK 를 사용하기 위해선 마이크 권한 필요합니다. 권한 추가는 엔진 또는 플랫폼의 SDK 공정 배치 문서를 참조하십시오|
|4103   |녹음 기동이 너무 짧아 오류 발생|우선, 녹음 시 단위는 ms여야 합니다. 파라미터가 올바른지 확인하십시오; 녹음 시간은 1000ms 이상이어야 합니다|
|4104   |녹음 시작 조작 할 수 없음|녹음 시작 인터페이스를 이미 호출한 것이 아닌지 점검하십시오|

####  예시 코드  
```
이벤트 모니터링: 
ITMGContext.GetInstance().GetPttCtrl().OnRecordFileComplete +=  new QAVRecordFileCompleteCallback (OnRecordFileComplete);
리스너 처리: 
void OnRecordFileComplete(int code, string filepath){
    //녹음을 기동한 콜백
}
```

### 스트리밍 음성인식 기동
이 인터페이스는 스트리밍 음성 인식을 기동하는데 사용되며, 동시에 콜백 중에 실시간 음성 문자 변환을 할 수 있습니다. 언어를 지정하여 인식할 수 있으며 음성에서 인식된 정보를 지정된 언어로 번역하여 리턴할 수 있습니다.

#### 함수 프로토타입  

```
ITMGPTT int StartRecordingWithStreamingRecognition(string filePath)
ITMGPTT int StartRecordingWithStreamingRecognition(string filePath, string translateLanguage,string translateLanguage) 
```
|파라미터     | 타입         |의미|
| ------------- |:-------------:|-------------|
| filePath|String|저장한 음성 경로|
| speechLanguage    |String|지정 문자로 인식한 음성 파라미터와 관련하여 [음성 문자 변환된 음성 파라미터 참고 리스트](https://intl.cloud.tencent.com/document/product/607/30260)를 참조하십시오|
| translateLanguage|String|지정 문자로 번역된 음성 파라미터와 관련하여 [음성 문자 변환 음성 파라미터 참고 리스트](https://intl.cloud.tencent.com/document/product/607/30260)를 참조하십시오（이 파라미터는 일시적으로사용이 불가하므로 speechLanguage 와 같은 파라미터를 입력하십시오）|

#### 예시 코드  
```
string recordPath = Application.persistentDataPath + string.Format("/{0}.silk", sUid++);
int ret = ITMGContext.GetInstance().GetPttCtrl().StartRecordingWithStreamingRecognition(recordPath, "cmn-Hans-CN","cmn-Hans-CN");
```

### 스트리밍식 음성 메시지 인식을 기동한 콜백
스트리밍식 음성 메시지 인식을 기동하면 콜백은 위탁을 통해 메시지를 전달합니다.
```
위탁 함수: 
public delegate void QAVStreamingRecognitionCallback(int code, string fileid, string filepath, string result);
이벤트 함수: 
public abstract event QAVStreamingRecognitionCallback OnStreamingSpeechComplete;
```

|메시지 명칭     | 의미         |
| ------------- |:-------------:|
| code    |스트리밍식 음성 인식 성공 여부를 판단하는 리턴코드|
| result    |음성을 텍스트로 변환하여 인식한 텍스트|
| filepath |녹음을 저장한 로컬 주소|
| fileid |백그라운드에 녹음한 url 주소|

|에러코드     | 의미         |처리방식|
| ------------- |:-------------:|:-------------:|
|32775|스트리밍 음성을 텍스트로 변환에는 실패했지만 녹음에는 성공함|UploadRecordedFile 인터페이스를 호출하여 녹음 파일을 업로드 하십시오. 그 후 SpeechToText 인터페이스를 호출하여 음성 문자 변환 작업을 진행하십시오|
|32777|스트리밍 음성 텍스트 변환에는 실패했지만 녹음과 업로드는 성공함|출력된 정보 중 업로드 성공한 백그라운드 url 주소를 사용하여, SpeechToText 인터페이스를 호출한 뒤 음성 문자 변환 작업을 진행하십시오|

#### 예시 코드  
```
이벤트 모니터링:
ITMGContext.GetInstance().GetPttCtrl().OnStreamingSpeechComplete +=new QAVStreamingRecognitionCallback (OnStreamingSpeechComplete);
리스너 처리:
void OnStreamingSpeechComplete(int code, string fileid, string filepath, string result){
    //스트리밍 음성 인식 콜백을 기동합니다
}

```

### 녹음 일시정지
이 인터페이스는 녹음을 일시정지합니다. 녹음을 복구하려면 ResumeRecording 인터페이스를 적용하세요.

#### 함수 프로토타입  
```
ITMGPTT int PauseRecording()
```
####  예시 코드  
```
ITMGContext.GetInstance().GetPttCtrl().PauseRecording();
```

### 녹음 복구
이 인터페이스는 녹음을 복구합니다.

#### 함수 프로토타입  
```
ITMGPTT int ResumeRecording()
```
####  예시 코드  
```
ITMGContext.GetInstance().GetPttCtrl().ResumeRecording();
```


### 녹음 중지
이 인터페이스는 녹음을 중지합니다. 이 인터페이스는 비동기 인터페이스로, 녹음을 중지하면 녹음 완료 콜백이 있으며, 성공한 이후에 녹음 파일 사용이 가능합니다.
#### 함수 프로토타입  
```
ITMGPTT int StopRecording()
```
####  예시 코드  
```
ITMGContext.GetInstance().GetPttCtrl().StopRecording();
```



### 녹음 취소
이 인터페이스는 녹음을 취소합니다. 취소하면 콜백이 없습니다.
#### 함수 프로토타입  
```
ITMGPTT int CancelRecording()
```
####  예시 코드  
```
ITMGContext.GetInstance().GetPttCtrl().CancelRecording();
```

### 오프라인 음성 메시지 마이크 실시간 볼륨 읽어오기
이 인터페이스는 마이크 실시간 볼륨을 읽어옵니다. 리턴값은 int 타입이며, 값범위는 0부터 100입니다.

#### 함수 프로토타입  
```
ITMGPTT int GetMicLevel()
```
#### 예시 코드  
```
ITMGContext.GetInstance().GetPttCtrl().GetMicLevel();
```


### 오프라인 음성 메시지 레코딩 볼륨 설정
이 인터페이스는 오프라인 음성 메시지 레코딩 볼륨을 설정합니다. 값범위는 0부터 100입니다.

#### 함수 프로토타입  
```
ITMGPTT int SetMicVolume(int vol)
```
#### 예시 코드  
```
ITMGContext.GetInstance().GetPttCtrl().SetMicVolume(100);
```

### 오프라인 음성 메시지 레코딩 볼륨 읽어오기
이 인터페이스는 오프라인 음성 메시지 레코딩 볼륨을 읽어옵니다. 리턴값은 int 타입이며, 값범위는 0부터 100입니다.

#### 함수 프로토타입  
```
ITMGPTT int GetMicVolume()
```

#### 예시 코드  
```
ITMGContext.GetInstance().GetPttCtrl().GetMicVolume();
```
### 스피커 실시간 볼륨 읽어오기
이 인터페이스는 스피커 실시간 볼륨을 읽어옵니다. 리턴값은 int 타입이며, 값범위는 0부터 100입니다.

#### 함수 프로토타입  
```
ITMGPTT int GetSpeakerLevel()
```

#### 예시 코드  
```
ITMGContext.GetInstance().GetPttCtrl().GetSpeakerLevel();
```



### 오프라인 음성 메시지 플레이 볼륨 설정
이 인터페이스는 오프라인 음성 메시지 플레이 볼륨을 설정합니다. 값 범위는 0부터 100입니다.

#### 함수 프로토타입  
```
ITMGPTT int SetSpeakerVolume(int vol)
```
#### 예시 코드  
```
ITMGContext.GetInstance().GetPttCtrl().SetSpeakerVolume(100);
```

### 오프라인 음성 메시지 플레이 볼륨 읽어오기
이 인터페이스는 오프라인 음성 메시지 플레이 볼륨을 읽어옵니다. 리턴값은 int 타입이며, 값 범위는 0부터 100입니다.

#### 함수 프로토타입  
```
ITMGPTT int GetSpeakerVolume()
```

#### 예시 코드  
```
ITMGContext.GetInstance().GetPttCtrl().GetSpeakerVolume();
```

### 음성파일 업로드
이 인터페이스는 음성파일을 업로드합니다
#### 함수 프로토타입  
```
ITMGPTT int UploadRecordedFile (string filePath)
```
|파라미터     | 타입         |의미|
| ------------- |:-------------:|-------------|
| filePath    |string                      |업로드한 음성 경로|

#### 예시 코드  
```
ITMGContext.GetInstance().GetPttCtrl().UploadRecordedFile(filePath);
```


### 음성 완료 콜백 업로드
음성 완료 콜백을 업로드하며, 위탁을 통해 메시지를 전달합니다.
#### 함수 프로토타입
```
위탁 함수: 
public delegate void QAVUploadFileCompleteCallback(int code, string filepath, string fileid);
이벤트 함수: 
public abstract event QAVUploadFileCompleteCallback OnUploadFileComplete; 
```
|파라미터     | 타입         |의미|
| ------------- |:-------------:|-------------|
| code    |int                       |code가 0일 경우, 레코딩 완료|
| filepath    |string                      |레코딩 저장 주소|
| fileid    |string                      |파일 url 경로|

#### 에러코드

|에러코드값 |원인  |제안 방안        |
|-----|------|------|
|8193   |파일 업로드 시, 파일 액세스 오류|파일이 존재하는지, 파일 경로가 합법적인지 확인합니다|
|8194   |서명 교정 실패 오류|인증 보안키가 올바른지, 초기화 오프라인 음성 메시지가 있는지 점검합니다|
|8195   |네트워크 오류|디바이스 네트워크가 외부 네트워크에 정상적으로 방문할 수 있는지 점검합니다|
|8196   |업로드된 파라미터 획득 과정에서 네트워크 오류|인증이 올바른지, 디바이스 네트워크가 외부 네트워크에 정상적으로 방문할 수 있는지 점검합니다|
|8197   |업로드 파라미터 획득 중 롤백 데이터가 비어 있음|인증이 올바른지, 디바이스 네트워크가 외부 네트워크에 정상적으로 방문할 수 있는지 점검합니다|
|8198   |업로드 파라미터 획득 중 롤백 데이터 압축해제 실패|인증이 올바른지, 디바이스 네트워크가 외부 네트워크에 정상적으로 방문할 수 있는지 점검합니다|
|8200   |appinfo 설정 안됨|apply 인터페이스가 호출되었는지, 인풋 파라미터가 비어있지는 않은지 점검합니다|

#### 예시 코드
```
이벤트 모니터링: 
ITMGContext.GetInstance().GetPttCtrl().OnUploadFileComplete +=new QAVUploadFileCompleteCallback (OnUploadFileComplete);
리스너 처리: 
void OnUploadFileComplete(int code, string filepath, string fileid){
    //음성 완료 콜백 업로드
}
```


### 음성파일 다운로드
이 인터페이스는 음성파일을 다운로드합니다.
#### 함수 프로토타입  
```
ITMGPTT DownloadRecordedFile (string fileID, string downloadFilePath)
```
|함수     | 타입         |의미|
| ------------- |:-------------:|-------------|
| fileID    |string                       |파일 url 경로|
| downloadFilePath    |string                       |파일 로컬 저장 경로|

####  예시 코드  
```
ITMGContext.GetInstance().GetPttCtrl().DownloadRecordedFile(fileId, filePath);
```


### 음성파일을 다운로드하여 콜백을 완료합니다.
음성파일을 다운로드하여 콜백을 완료합니다. 위탁을 통해 메시지를 전달합니다.
#### 함수 프로토타입  
```
위탁 함수: 
public delegate void QAVDownloadFileCompleteCallback(int code, string filepath, string fileid);
이벤트 함수: 
public abstract event QAVDownloadFileCompleteCallback OnDownloadFileComplete;
```
|파라미터     | 타입         |의미|
| ------------- |:-------------:|-------------|
| code    |int                       |code가 0일 경우, 레코딩 완료|
| filepath    |string                      |레코딩 저장 주소|
| fileid    |string                      |파일 url 경로|

#### 에러 코드

|에러코드값 |원인  |제안 방안        |
|-----|------|------|
|12289  |파일 다운로드 시, 파일 엑세스 오류    |파일 경로가 합법적인지 점검합니다|
|12290  |서명 교정 실패    |인증 보안키가 올바른지, 초기화 오프라인 음성이 있는지 점검합니다|
|12291  |네트워크 스토리지 시스템 이상    |서버가 음성 파일 획득에 실패하였습니다. 인터페이스 파라미터 fileid 가 올바른지, 네트워크가 정상인지, cos 파일이 존재하는지 점검합니다|
|12292  |서버 파일 시스템 오류    |디바이스 네트워크가 외부 네트워크에 정상적으로 방문할 수 있는지, 서버에 파일이 존재하는지 점검합니다|
|12293  |다운로드된 파라미터 획득 과정에서 HTTP 네트워크 오류|디바이스 네트워크가 외부 네트워크에 정상적으로 방문할 수 있는지 점검합니다|
|12294  |다운로드된 파라미터 획득 과정에서 롤백 데이터 비어있음 |디바이스 네트워크가 외부 네트워크에 정상적으로 방문할 수 있는지 점검합니다|
|12295  |다운로드된 파라미터 획득 과정에서 롤백 데이터 압축해제 실패|디바이스 네트워크가 외부 네트워크에 정상적으로 방문할 수 있는지 점검합니다|
|12297  |appinfo 설정 안됨|인증 보안키가 올바른지, 초기화 오프라인 음성 메시지가 있는지 점검합니다|



#### 예시 코드  
```
이벤트 모니터링:  
ITMGContext.GetInstance().GetPttCtrl().OnDownloadFileComplete +=new QAVDownloadFileCompleteCallback(OnDownloadFileComplete);
리스너 처리: 
void OnDownloadFileComplete(int code, string filepath, string fileid){
    //음성파일을 다운로드하여 콜백을 완료합니다
}
```



### 음성 플레이
이 인터페이스는 음성을 플레이합니다.
####  함수 프로토타입  
```
ITMGPTT PlayRecordedFile (string downloadFilePath)
```
|파라미터     | 타입         |의미|
| ------------- |:-------------:|-------------|
| downloadFilePath    |string                       |파일 경로|

####  예시 코드  
```
ITMGContext.GetInstance().GetPttCtrl().PlayRecordedFile(filePath); 
```


### 플레이한 음성 콜백
플레이한 음성을 콜백합니다. 위탁을 통해 메시지를 전달합니다.
#### 함수 프로토타입  
```
위탁 함수:
public delegate void QAVPlayFileCompleteCallback(int code, string filepath);
이벤트 함수: 
public abstract event QAVPlayFileCompleteCallback OnPlayFileComplete;
```
|파라미터     | 타입         |의미|
| ------------- |:-------------:|-------------|
| code    |int                       |code가 0일 경우, 레코딩 완료|
| filepath    |string                      |레코딩 저장 주소|

#### 에러코드

|에러코드값 |원인  |제안 방안        |
|-----|------|------|
|20481  |초기화 오류|디바이스가 점용되었는지, 권한이 정상인지, 초기화가 정상적이었는지 점검합니다|
|20482  |재생 중인 상황에서 중단하고 다음 재생을 시도하였으나 실패함(정상 상황에서는 중단이 가능함)|코드 로직이 올바른지 점검합니다|
|20483  |파라미터 비어있음|코드 중 인터페이스 파라미터가 올바른지 점검합니다|
|20484  |내부 오류|초기화 재생 오류, 암호 해독 실패 등의 문제로 이 에러 코드가 생성됩니다. 로그를 분석하여 해결합니다|


#### 예시 코드  
```
이벤트를 모니터링:  
ITMGContext.GetInstance().GetPttCtrl().OnPlayFileComplete +=new  QAVPlayFileCompleteCallback(OnPlayFileComplete);
리스너 처리:
void OnPlayFileComplete(int code, string filepath){
    //음성 플레이 콜백
}
```




### 음성 플레이 스톱
이 인터페이스로 음성 플레이를 스톱할 수 있습니다. 음성 플레이를 스톱해도 플레이를 완료한 콜백이 있습니다.
####  함수 프로토타입  
```
ITMGPTT int StopPlayFile()
```

#### 예시 코드  
```
ITMGContext.GetInstance().GetPttCtrl().StopPlayFile();
```



### 음성파일 크기를 읽어옵니다
이 인터페이스를 통해 음성파일의 크기를 읽어옵니다.
#### 함수 프로토타입  
```
ITMGPTT GetFileSize(string filePath) 
```
|파라미터     | 타입         |의미|
| ------------- |:-------------:|-------------|
| filePath    |string                      |음성파일 경로|

####  예시 코드  
```
int fileSize = ITMGContext.GetInstance().GetPttCtrl().GetFileSize(filepath);
```

### 음성파일의 시간길이를 읽어옵니다
이 인터페이스는 밀리초 단위로 음성파일의 시간길이를 읽어옵니다.
####  함수 프로토타입  
```
ITMGPTT int GetVoiceFileDuration(string filePath)
```
|파라미터     | 타입         |의미|
| ------------- |:-------------:|-------------|
| filePath    |string                      |음성파일 경로|

####  예시 코드  
```
int fileDuration = ITMGContext.GetInstance().GetPttCtrl().GetVoiceFileDuration(filepath);
```


### 지정 음성파일을 텍스트로 인식합니다
이 인터페이스는 지정 음성파일을 텍스트로 인식합니다.

#### 함수 프로토타입  
```
ITMGPTT int SpeechToText(String fileID)
```
|파라미터     | 타입         |의미|
| ------------- |:-------------:|-------------|
| fileID    |string                      |음성파일 url|

#### 예시 코드  
```
ITMGContext.GetInstance().GetPttCtrl().SpeechToText(fileID);
```



### 지정된 음성 파일을 문자로 번역(지정 언어)
이 인터페이스는 지정 음성을 인식합니다. 또한 음성에서 인식한 정보를 지정 음성으로 번역하여 출력할 수 있습니다.

#### 함수 프로토타입  
```
ITMGPTT int SpeechToText(String fileID,String language)
```
|파라미터     | 타입         |의미|
| ------------- |:-------------:|-------------|
| fileID    |String                     |음성파일 url|
| speechLanguage    |String                 |지정 텍스트를 인식하는 언어 파라미터입니다. 파라미터는 [음성 텍스트 변환 언어 파라미터 참고 리스트](https://intl.cloud.tencent.com/document/product/607/30260)를 참고하십시오 |
| translatelanguage    |String                    |지정 문자로 번역된 음성 파라미터와 관련하여[음성 문자 변환된 음성 파라미터 참고 리스트](https://intl.cloud.tencent.com/document/product/607/30260)를 참조하십시오（이 파라미터는 일시적으로 유효하지 않으므로, 입력 파라미터는 speechLanguage와 일치해야 합니다）|

#### 예시 코드  
```
ITMGContext.GetInstance().GetPttCtrl().SpeechToText(fileID,"cmn-Hans-CN","cmn-Hans-CN");
```



### 콜백 인식
지정 음성파일을 텍스트로 인식하며, 위탁을 통해 메시지를 전달합니다.
#### 함수 프로토타입  
```
위탁 함수:
public delegate void QAVSpeechToTextCallback(int code, string fileid, string result);
이벤트 함수:
public abstract event QAVSpeechToTextCallback OnSpeechToTextComplete;
```
|파라미터     | 타입         |의미|
| ------------- |:-------------:|-------------|
| code    |int                       |code가 0일 경우, 레코딩 완료|
| fileid    |string                      |음성파일 url|
| result    |string                      |변환한 텍스트 결과|

#### 예시 코드
```
이벤트 리스터:
ITMGContext.GetInstance().GetPttCtrl().OnSpeechToTextComplete += new QAVSpeechToTextCallback(OnSpeechToTextComplete);
리스너 처리:
void OnSpeechToTextComplete(int code, string fileid, string result){
    //콜백 인식
}
```



##고급 API

### 버전 번호 획득
SDK 버전 번호를 획득하여 분석합니다.
#### 함수 프로토타입
```
ITMGContext  abstract string GetSDKVersion()
```
#### 예시 코드  
```
ITMGContext.GetInstance().GetSDKVersion();
```





### 프린팅 로그 레벨 설정
프린팅 로그 레벨을 설정합니다. 기본 레벨을 유지하시기를 권장드립니다.
#### 함수 프로토타입
```
ITMGContext  SetLogLevel(ITMG_LOG_LEVEL levelWrite, ITMG_LOG_LEVEL levelPrint)
```

#### 파라미터 의미

|파라미터|타입|의미|
|---|---|---|
|levelWrite|ITMG_LOG_LEVEL|입력 로그 레벨 설정, TMG_LOG_LEVEL_NONE 입력하지 않음을 의미, 디폴트는 TMG_LOG_LEVEL_INFO|
|levelPrint|ITMG_LOG_LEVEL|프린팅 로그 레벨 설정, TMG_LOG_LEVEL_NONE 프린팅하지 않음을 의미, 디폴트는 TMG_LOG_LEVEL_ERROR|



|ITMG_LOG_LEVEL|의미|
| -------------------------------|:-------------:|
|TMG_LOG_LEVEL_NONE=0|로그를 프린팅하지 않음|
|TMG_LOG_LEVEL_ERROR=1|에러 로그 프린팅(디폴트)|
|TMG_LOG_LEVEL_INFO=2|안내 로그 프린팅|
|TMG_LOG_LEVEL_DEBUG=3|개발 테스트 로그 프린팅|
|TMG_LOG_LEVEL_VERBOSE=4|고빈도 로그 프린팅|

#### 예시 코드  
```
ITMGContext.GetInstance().SetLogLevel(TMG_LOG_LEVEL_INFO,TMG_LOG_LEVEL_INFO);
```



### 프린팅 로그 경로 설정
프린팅 로그 경로를 설정합니다.
기본 경로:

|플랫폼     |경로        |
| ------------- |-------------|
|Windows |%appdata%\Tencent\GME\ProcessName|
|iOS    |Application/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/Documents|
|Android|/sdcard/Android/data/xxx.xxx.xxx/files|
|Mac    |/Users/username/Library/Containers/xxx.xxx.xxx/Data/Documents|

#### 함수 프로토타입
```
ITMGContext  SetLogPath(string logDir)
```

|파라미터     | 타입         |의미|
| ------------- |:-------------:|-------------|
| logDir    |NSString   |경로|

#### 예시 코드  
```
ITMGContext.GetInstance().SetLogPath(path);
```


### 진단 정보 획득
오디오 비디오 통화의 실시간 통화 품질에 대한 정보를 획득합니다. 이 인터페이스는 주로 실시간 통화 품질, 배찰 문제 등을 살펴보는 데 사용되며, 업무팀에서는 무시하셔도 무관합니다.
#### 함수 프로토타입  
```
ITMGRoom GetQualityTips()
```
#### 예시 코드  
```
string tips = ITMGContext.GetInstance().GetRoom().GetQualityTips();
```

### 가청주파수 데이터 블랙리스트 추가하기
임의 ID를 가청주파수 데이터 블랙리스트에 추가합니다. 리턴값이 0일 경우 호출 성공하였음을 의미합니다.
#### 함수 프로토타입  

```
ITMGContext ITMGAudioCtrl AddAudioBlackList(String openId)
```
|파라미터     | 타입         |의미|
| ------------- |:-------------:|-------------|
| openId    |NSString      |블랙리스트를 추가해야 할 id|

#### 예시 코드  

```
ITMGContext.GetInstance().GetAudioCtrl ().AddAudioBlackList (id);
```

### 가청주파수 데이터 블랙리스트 제외
임의 ID를 가청주파수 데이터 블랙리스트에서 제외합니다. 리턴값이 0일 경우 호출 성공하였음을 의미합니다.
#### 함수 프로토타입  

```
ITMGContext ITMGAudioCtrl RemoveAudioBlackList(string openId)
```
|파라미터     | 타입         |의미|
| ------------- |:-------------:|-------------|
| openId    |NSString      |블랙리스트를 제외해야 할 id|

#### 예시 코드  

```
ITMGContext.GetInstance().GetAudioCtrl ().RemoveAudioBlackList (id);
```

