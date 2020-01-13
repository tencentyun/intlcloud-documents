Windows 개발자가 Tencent Cloud GME(Game Multimedia Engine) 제품 API를 액세스하고 디버깅하는 편의성을 위해 Windows 개발용 액세스 기술 파일을 소개드립니다. 

>이 파일은 GME sdk version：2.5에 해당합니다.

## GME 사용 시 중요 사항

|메인 API     | API 의미|
| ------------- |:-------------:|
|Init    |GME 초기화|
|Poll    |트리거 이벤트 콜백|
|EnterRoom |방에 들어가기  |
|EnableMic |마이크 온 |
|EnableSpeaker|스피커 온 |

>
- GME를 사용하기 전에 프로그래밍을 설정해야 SDK가 적용됩니다.
- GME API를 호출하면 리턴값은 AV_OK이며, 수치는 0입니다.
-GME 스레드는 같은 스레드에서 호출해야 합니다.
- GME 방 가입 시 인증이 필요합니다. 파일중 인증 파트 관련 내용을 참조하십시오.
- GME는 주기적으로 Poll API를 호출하여 트리거 이벤트를 콜백해야 합니다.
- GME 콜백 메시지는 콜백 메시지 리스트를 참조하십시오.
- 방에 들어간 후 디바이스를 조작할 수 있습니다.
- 에러코드 상세내역은 [에러코드](https://intl.cloud.tencent.com/document/product/607/15173)를 참조하십시오.

## 실시간 음성 프로세스 
![](https://main.qcloudimg.com/raw/810d0404638c494d9d5514eb5037cd37.png)


## 초기화 관련 API
초기화하기 전에 SDK는 비초기화 상태이며, Init API를 통해 SDK를 초기화해야 실시간/오프라인 음성을 사용할 수 있습니다.
사용 문제는 [일반 문제](https://intl.cloud.tencent.com/document/product/607/30254)를 참조하십시오.

|API     | API 의미   |
| ------------- |:-------------:|
|Init    |GME 초기화|
|Poll    |트리거 이벤트 콜백|
|Pause   |시스템 일시 정지|
|Resume |시스템 복구|
|Uninit    |GME 반초기화(Deinitialization) |


### 싱글턴(singleton) 획득
GME SDK는 싱글턴 형태로 제공됩니다. 전체 호출은 ITMGContext로부터 시작하며, ITMGDelegate 콜백을 통해 애플리케이션에 백패스합니다. 반드시 가장 먼저 설정해야 합니다.    
#### 함수 프로토타입 

```
QAVSDK_API ITMGContext* QAVSDK_CALL ITMGContextGetInstance();
```
#### 예시 코드  

```
ITMGContext* m_pTmgContext;
m_pTmgContext = ITMGContextGetInstance();
```


### 메시지 전달
인터페이스는 Delegate 방법을 적용하여 애플리케이션에 콜백 공지를 전송합니다. 메시지 타입은 ITMG_MAIN_EVENT_TYPE을 참조하십시오. Windows 플랫폼에서 data는 json 스트링 포멧이며, 구체적인 key-value는 설명 파일을 참조하십시오.

#### 예시 코드  
```
//함수 구현: 
class Callback : public SetTMGDelegate 
{
	virtual void OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data)
	{
  		switch(eventType)
  		{
   			//메시지 타입 판단 및 프로세싱
  		}
 	}
}

Callback*  p = new Callback ();
m_pTmgContext->SetTMGDelegate(p);
```

##SDK 초기화

파라미터를 읽어오려면 [액세스 매뉴얼](https://intl.cloud.tencent.com/document/product/607/10782)을 참조하십시오.
이 인터페이스는 Tencent Cloud 콘솔의 SDKAppID 계정을 파라미터로 적용 및 openId를 추가해야 합니다. 해당 openId는 1개당 사용자 한명에 적용하며, 앱 개발자가 스스로 룰을 정합니다. 앱에서 반복하지 말아야 합니다.(현재 INT64만 지원합니다).
>SDK 초기화 후 체크인 가능.
>
>####  함수 프로토타입

```
ITMGContext virtual int Init(const char* sdkAppId, const char* openId)
```

|파라미터     | 유형         |의미|
| ------------- |:-------------:|-------------|
| sdkAppId    |char*   |텐센트 클라우드 콘솔로부터의 sdkAppId 번호|
| openId    |char*   |openId 는 Int64 유형만을 지원하고 (char* 로 전환 후 전달), 10000보다 무조건 커야 하며 사용자 식별에 사용됩니다 |

####  예시 코드 


```
#define SDKAPPID3RD "1400089356"
cosnt char* openId="10001";
ITMGContext* context = ITMGContextGetInstance();
context->Init(SDKAPPID3RD, openId);
```
### 트리거 이벤트 콜백
update에서 주기의 Poll 조정을 통해 트리거 이벤트를 콜백할 수 있습니다.
####  함수 프로토타입

```
class ITMGContext {
protected:
    virtual ~ITMGContext() {}
    
public:    	
	virtual void Poll()= 0;
}

```
####  예시 코드
```
//최고 문서 중의 선언

//코드 실현
void TMGTestScene::update(float delta)
{
    ITMGContextGetInstance()->Poll();
}
```

### 시스템 일시정지
시스템에 Pause 사건이 발생할 경우 엔진에 Pause 진행을 함께 알려야 합니다.
####  함수 프로토타입

```
ITMGContext int Pause()
```

### 시스템 복구
시스템에서 Resume 사건이 발생할 경우 엔진에 동시에 Resume을 알려야 합니다. Resume 인터페이스는 실시간 음성만 복구합니다.
####  함수 프로토타입

```
ITMGContext int Resume()
```



### SDK 초기화 취소
SDK를 초기화 취소하고 초기화되지 않은 상태로 들어갑니다. 계정을 전환하기 위해서는 초기화 취소가 필요합니다.
####  함수 프로토타입

```
ITMGContext int Uninit()
```
####  예시 코드
```
ITMGContext* context = ITMGContextGetInstance();
context->Uninit();
```

## 실시간 음성 채팅룸 관련 인터페이스
초기화 후, SDK 조정과 방에 옮겨 들어가야 실시간 음성 채팅 통화가 가능합니다.
궁금한 사항은 [실시간 음성 채팅 관련 문제](https://intl.cloud.tencent.com/document/product/607/30257)를 참조하십시오.

|인터페이스     | 인터페이스 의미   |
| ------------- |:-------------:|
|GenAuthBuffer    |초기화 인증|
|EnterRoom   |방 추가|
|IsRoomEntered   |방에 들어갔는지 여부|
|ExitRoom |방 나가기|
|ChangeRoomType |방 사용자 오디오 타입 수정|
|GetRoomType |방 사용자 오디오 타입 획득|


### 인증 정보
AuthBuffer 생성하고, 기능의 암호화와 인증 상세 내역은 백그라운드에서 배포한 [인증 보안키](https://intl.cloud.tencent.com/document/product/607/12218)를 참조하십시오.    
오프라인 음성으로 인증을 받으려면 룸 번호 파라미터를 null로 채워야 합니다.

#### 함수 프로토타입
```
int  QAVSDK_AuthBuffer_GenAuthBuffer(unsigned int dwSdkAppID, const char* strRoomID, const char* strOpenID,
	const char* strKey, unsigned char* strAuthBuffer, unsigned int bufferLength);
```
|파라미터     | 유형         |의미|
| ------------- |:-------------:|-------------|
| dwSdkAppID    |int   |텐센트 클라우드 콘솔로부터의 sdkAppId 번호|
| strRoomID    |char*     |방 번호는 최대 127개 문자까지 지원됩니다 (오프라인 음성방 번호 파라미터는 반드시 null이어야 합니다)|
| strOpenID  |char*     |사용자 표식|
| strKey    |char*    |텐센트 클라우드[콘솔](https://console.cloud.tencent.com/gamegme) 의 보안키|
|strAuthBuffer|char*    |리턴한 authbuff|
| bufferLength   |int    |전달된 authbuff 의 길이로 500을 추천합니다|


####  예시 코드  
```
unsigned int bufferLen = 512;
unsigned char retAuthBuff[512] = {0};
QAVSDK_AuthBuffer_GenAuthBuffer(atoi(SDKAPPID3RD), roomId, "10001", AUTHKEY,retAuthBuff,bufferLen);
```



### 방 추가
생성된 인증 정보로 방에 들어가면 ITMG_MAIN_EVENT_TYPE_ENTER_ROOM의 콜백이 수신됩니다. 방 가입 시 기본값으로 마이크 및 스피커가 켜져있지 않습니다. 리턴 값이 AV_OK일 때 성공을 의미합니다.
일반 음성으로 방에 들어오고 범위 음성에 관한 수요 신청이 없는 경우 일반 방 들어가기 인터페이스를 사용합니다. 자세한 정보는 [범위 음성](https://intl.cloud.tencent.com/document/product/607/17972)을 참조하십시오.

####  함수 프로토타입
```
ITMGContext virtual int EnterRoom(const char*  roomID, ITMG_ROOM_TYPE roomType, const char* authBuff, int buffLen)
```
|파라미터     | 유형         |의미|
| ------------- |:-------------:|-------------|
| roomID| char*    |방 번호는 최대 127 글자까지 지원됩니다|
| roomType |ITMG_ROOM_TYPE|방 오디오 유형|
| authBuffer    |char*     |인증번호|
| buffLen   |int   |인증번호 길이|

방 오디오 유형과 관련하여 [음질 선택](https://intl.cloud.tencent.com/document/product/607/18522)을 참조하십시오.


####  예시 코드  
```
ITMGContext* context = ITMGContextGetInstance();
context->EnterRoom(roomID, ITMG_ROOM_TYPE_STANDARD, (char*)retAuthBuff,bufferLen);
```

### 방 가입 이벤트의 콜백
방 가입이 완료되면 메시지 ITMG_MAIN_EVENT_TYPE_ENTER_ROOM 가 발송됩니다. OnEvent 함수에서 판단을 진행합니다.

####  예시 코드  
```

void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data){
	switch (eventType) {
            case ITMG_MAIN_EVENT_TYPE_ENTER_ROOM:
		{
		//처리 진행
		break;
		}
	}
}
```

#### 상세 Data
|메시지     | Data         |예제|
| ------------- |:-------------:|-------------|
| ITMG_MAIN_EVENT_TYPE_ENTER_ROOM    |result; error_info|{"error_info":"","result":0}|


### 방에 들어왔는지 판단하기
인터페이스를 사용하여 방에 이미 들어갔는지 여부를 판단할 수 있으며 리턴값은 bool 유형입니다.
####  함수 프로토타입  
```
ITMGContext virtual bool IsRoomEntered()
```
####  예시 코드  
```
ITMGContext* context = ITMGContextGetInstance();
context->IsRoomEntered();
```

### 방 나가기
인터페이스를 사용하여 위치한 방에서 나갈 수 있습니다. 이것은 비동기 인터페이스로서, 리턴 값이 AV_OK일 때 비동기 전송의 성공을 나타냅니다.

>애플리케이션에서 체크 아웃 직후 체크인이 실행되는 작업 환경이 있는 경우 개발자는 인터페이스 호출 프로세스에서 ExitRoom의 콜백 RoomExitComplete 알림을 기다릴 필요가 없습니다. 인터페이스를 직접 호출하면 됩니다.

#### 함수 프로토타입  
```
ITMGContext virtual int ExitRoom()
```
####  예시 코드  
```
ITMGContext* context = ITMGContextGetInstance();
context->ExitRoom();
```

### 방 나가기 콜백
방 나가기가 완료되면 세션이 종료되며, 메시지는 ITMG_MAIN_EVENT_TYPE_EXIT_ROOM입니다.
####  예시 코드  
```
void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data){
	switch (eventType) {
            case ITMG_MAIN_EVENT_TYPE_EXIT_ROOM:
		{
		//처리 진행
		break;
		}
	}
}
```

#### 상세 Data
|메시지     | Data         |예제|
| ------------- |:-------------:|------------- |
| ITMG_MAIN_EVENT_TYPE_EXIT_ROOM    |result; error_info  |{"error_info":"","result":0}|


### 방 사용자 오디오 유형 수정
인터페이스는 사용자 방의 오디오 유형을 수정하는 데 사용되며, 그 결과 리턴 이벤트를 참조하며, 이벤트 유형은 ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE입니다.
####  함수 프로토타입  
```
IITMGContext TMGRoom public void ChangeRoomType((ITMG_ROOM_TYPE roomType)
```


|파라미터     | 유형         |의미|
| ------------- |:-------------:|-------------|
| roomType    |ITMG_ROOM_TYPE    |방 바꾸기를 원하는 경우, 방 오디오 유형은 EnterRoom 인터페이스를 참조하십시오|

####  예시 코드  
```
ITMGContext* context = ITMGContextGetInstance();
ITMGContextGetInstance()->GetRoom()->ChangeRoomType(ITMG_ROOM_TYPE_FLUENCY);
```


### 사용자 방 오디오 유형 획득
인터페이스는 사용자 룸의 오디오 유형을 얻는 데 사용되며, 리턴 값이 방의 오디오 유형이며, 리턴 값이 0인 경우 사용자 방의 오디오 유형을 얻는 데 오류가 발생했음을 의미하며, 방의 오디오 유형은 EnterRoom 인터페이스를 참조합니다.

####  함수 프로토타입  
```
IITMGContext TMGRoom public  int GetRoomType()
```

####  예시 코드  
```
ITMGContext* context = ITMGContextGetInstance();
ITMGContextGetInstance()->GetRoom()->GetRoomType();
```


### 방 유형 콜백 완성
방 유형 설정이 완료된 후, 리턴된 이벤트 메시지는 ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE로, 리턴된 파라미터는 result, error_info 및 new_room_type, new_room_type 가 대표하는 정보는 다음과 같이 OnEvent 함수에서 이벤트 메시지를 판단합니다.

|하위 이벤트 유형     | 대표 파라미터   |의미|
| ------------- |:-------------:|-------------|
| ITMG_ROOM_CHANGE_EVENT_ENTERROOM|1 |이것은 방 들어가기 과정에서 가지고 있는 오디오 유형과 방 유형이 적합하지 않은 경우, 들어간 방의 오디오 유형으로 자동 수정됨을 뜻하는 것입니다|
| ITMG_ROOM_CHANGE_EVENT_START|2|이것은 이미 방에 위치한 경우에서 오디오 유형의 전환이 발생했을 시 나옵니다 (예를 들어 ChangeRoomType 인터페이스 조정 후 오디오 유형을 바꿨을 때)|
| ITMG_ROOM_CHANGE_EVENT_COMPLETE|3|이것은 이미 방에 위치한 경우에서 오디오 유형의 전환이 완료되었을 때 나옵니다|
| ITMG_ROOM_CHANGE_EVENT_REQUEST|4|이것은 방 팀원의 ChangeRoomType 인터페이스 조정 후, 방 오디오 유형 전환을 요청할 시 나옵니다|


####  예시 코드  
```
void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data) {
	if (ITMGContext.ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE == type)
        {
		//방 유형 이벤트 처리 진행
	 }
}
```

#### 상세 Data
|메시지     | Data         |예제|
| ------------- |:-------------:|------------- |
| ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE    |result; error_info; new_room_type|{"error_info":"","new_room_type":0,"result":0}|


### 멤버 상태 변화
이 이벤트는 상태 변화가 있어야 알 수 있으며 상태가 변하지 않는 한 알림이 없습니다. 멤버 상태를 실시간으로 얻으려면 위에서 알림을 받을 때 캐시하십시요. 이벤트 소식은 ITMG_MAIN_EVNET_TYPE_USER_UPDATE이며, 여기 data에는 두 개의 메시지가 포함되며 event_id 및 user_list, OnEvent 함수에서 이벤트 소식을 판단합니다.
오디오 이벤트 알림에는 임계 값이 하나 있으며, 이 임계 값을 초과해야 알림이 전송됩니다. 2초 이상 오디오 패키지를 받지 못한 후에야 "한 멤버가 오디오 패키지 전송을 중지했습니다."라는 메시지 알림이 뜹니다.

|event_id     | 의미         |애플리케이션 유지 콘텐츠|
| ------------- |:-------------:|-------------|
|ITMG_EVENT_ID_USER_ENTER    |멤버 방 들어오기|애플리케이션 유지 멤버 리스트|
|ITMG_EVENT_ID_USER_EXIT    |멤버 방 나가기|애플리케이션 유지 멤버 리스트|
|ITMG_EVENT_ID_USER_HAS_AUDIO    |멤버 오디오 패키지 발송|애플리케이션 유지 통화 멤버 리스트|
|ITMG_EVENT_ID_USER_NO_AUDIO    |멤버 오디오 패키지 전송 중지|애플리케이션 유지 통화 멤버 리스트|

#### 예시 코드  

```
void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data){
	switch (eventType) {
            case ITMG_MAIN_EVNET_TYPE_USER_UPDATE:
		{
		//처리 진행
		//개발자는 파라미터를 해석하여 eventID 및 user_list 정보를 얻습니다 
		    switch (eventID)
 		    {
 		    case ITMG_EVENT_ID_USER_ENTER:
  			    //한 멤버가 방에 들어왔습니다
  			    break;
 		    case ITMG_EVENT_ID_USER_EXIT:
  			    //한 멤버가 방을 나갔습니다
			    break;
		    case ITMG_EVENT_ID_USER_HAS_AUDIO:
			    //한 멤버가 오디오 패키지를 보냈습니다
			    break;
		    case ITMG_EVENT_ID_USER_NO_AUDIO:
			    //한 멤버가 오디오 패키지 전송을 중지했습니다
			    break;
 		    default:
			    break;
		    }
		break;
		}
	}
}
```

### 품질 모니터링 이벤트
품질 모니터링 이벤트, 이벤트 소식은 ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_QUALITY로, 리턴 파라미터는 weight, floss 및 delay로 대표하는 정보는 아래와 같으며, OnEvent 함수에서 이벤트 소식을 판단합니다.

|파라미터     | 의미         |
| ------------- |-------------|
|weight    |범위는 1-5이고, 5는 음질 평점이 매우 좋은 것, 수치는 1은 음질 평점이 매우 나빠서 거의 사용할 수 없는 정도를 뜻합니다. 0은 초기값을 의미하며, 무의미합니다|
|floss    |패킷 손실율|
|delay    |오디오 접촉 지연 시간 (ms)|




### 상세 메시지

|메시지     | 메시지 의미   |
| ------------- |:-------------:|
|ITMG_MAIN_EVENT_TYPE_ENTER_ROOM           |오디오/비디오방 들어가기 메시지|
|ITMG_MAIN_EVENT_TYPE_EXIT_ROOM             |오디오/비디오방 나가기 메시지|
|ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT           |네트워크 등의 이유로 끊긴 메시지|
|ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE|방 유형 변화 이벤트|

### 메시지가 대응하는 상세 Data
|메시지     | Data         |예제|
| ------------- |:-------------:|------------- |
| ITMG_MAIN_EVENT_TYPE_ENTER_ROOM    |result; error_info|{"error_info":"","result":0}|
| ITMG_MAIN_EVENT_TYPE_EXIT_ROOM    |result; error_info  |{"error_info":"","result":0}|
| ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT    |result; error_info  |{"error_info":"waiting timeout, please check your network","result":0}|
| ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE    |result; error_info; new_room_type|{"error_info":"","new_room_type":0,"result":0}|


## 실시간 음성 채팅 오디오 인터페이스
SDK를 초기화한 후 방에 들어가야 실시간 음성 음성 관련 인터페이스를 호출할 수 있습니다.
사용자 인터페이스에서 마이크/스피커 켜기/끄기 버튼을 클릭할 때 다음과 같은 방식을 권장합니다:
- 대부분의 게임류 App에 대해 EnableMic 및 EnableSpeaker 인터페이스를 추천하기 때문에 이는 항상 EnableAudioCaptureDevice/EnableAudioSend를 함께 사용해야 하는 것을 의미합니다.
- 다른 유형의 모바일 App의 경우, 예를 들어 소셜 유형 App의 경우, 채취 장치를 켜거나 끄면 전체 장치(채취 및 재생)가 재시작되며, 이때 App에서 bgm을 재생하고 있다면 배경음악의 재생도 중단됩니다. 스위치 마이크는 위아래 행을 제어하는 방식으로 작동하며 재생을 중단하지 않습니다. 세부 호출은 방에 들어갈 때 EnableAudioCaptureDevice(true) && EnableAudioPlayDevice(true) 한 번, 스위치 마이크를 클릭할 때 EnableAudioSend/Recv만을 사용하여 오디오 스트림이 송신/수신되는지 여부를 제어합니다.
- 채취 또는 재생 장비를 별도로 내보내려면 인터페이스 EnableAudioCaptureDevice 및 EnableAudioPlayDevice를 참조하십시오.
- pause를 사용하여 오디오 엔진을 일시 중지하고 resume을 사용하여 오디오 엔진을 복구합니다.



|인터페이스     | 인터페이스 의미   |
| ------------- |:-------------:|
|GetMicListCount           |마이크 획득 장치 수|
|GetMicList          |기거 마이크 장비|
|GetSpeakerListCount          |스피커 획득 장치 수|
|GetSpeakerList          |기거 스피커 장치|
|SelectMic          |마이크 장비 선정|
|SelectSpeaker    |스피커 장비 선정|
|EnableMic    |마이크 온|
|GetMicState    |마이크 상태 획득|
|EnableAudioCaptureDevice    |채집 장치 온|
|IsAudioCaptureDeviceEnabled    |채집 장치 상태 획득|
|EnableAudioSend    |오디오 다운스트림 닫기 열기|
|IsAudioSendEnabled    |오디오 다운스트림 상태 획득|
|GetMicLevel    |실시간 마이크 음량 획득|
|GetSendStreamLevel|오디오 다운스트림 실시간 음량 획득|
|SetMicVolume    |마이크 음량 설정|
|GetMicVolume    |마이크 음량 획득|
|EnableSpeaker    |스피커 스위치|
|GetSpeakerState    |스피커 상태 획득|
|EnableAudioPlayDevice    |재생 디바이스 스위치|
|IsAudioPlayDeviceEnabled    |재생 디바이스 상태 획득|
|EnableAudioRecv    |오디오 업스트림 닫기 열기|
|IsAudioRecvEnabled    |오디오 업스트림 상태 획득|
|GetSpeakerLevel    |실시간 스피커 음량 획득|
|GetRecvStreamLevel|방 멤버 업스트림 실시간 음량 획득|
|SetSpeakerVolume    |스피커 음량 설정|
|GetSpeakerVolume    |스피커 음량 획득|
|EnableLoopBack    |인이어 모니터링 스위치|



### 획득한 마이크 장치 수
이 인터페이스는 마이크 장치 수를 얻는 데 사용됩니다.
#### 함수 프로토타입  
```
ITMGAudioCtrl virtual int GetMicListCount()
```
#### 예시 코드  
```
ITMGContextGetInstance()->GetAudioCtrl()->GetMicListCount();
```

### 기거 마이크 장치
이 인터페이스는 마이크 장비를 트리거하는데 사용됩니다. GetMicListCount 인터페이스에 맞춰 사용합니다.

#### 함수 프로토타입 
```
ITMGAudioCtrl virtual int GetMicList(TMGAudioDeviceInfo* ppDeviceInfoList, int nCount)

class TMGAudioDeviceInfo
{
public:
	const char* pDeviceID;
	const char* pDeviceName;
};
```
|파라미터     | 유형         |의미|
| ------------- |:-------------:|-------------|
| ppDeviceInfoList    |TMGAudioDeviceInfo   |장치 리스트|
| nCount    |int     |획득한 마이크 장치 수|

#### 예시 코드  

```
ITMGContextGetInstance()->GetAudioCtrl()->GetMicList(ppDeviceInfoList,nCount);
```



### 마이크 장치 선택
이 인터페이스는 마이크 장치를 선택하기 위해 사용됩니다. 디버깅하거나 디버깅하지 않을 경우 시스템 랜덤으로 장치를 선택합니다. 장치 ID는 GetMicList 리턴 리스트에서 가져옵니다.

#### 함수 프로토타입  

```
ITMGAudioCtrl virtual int SelectMic(const char* pMicID)
```

|파라미터     | 유형         |의미|
| ------------- |:-------------:|-------------|
| pMicID    |char*      |마이크 장치 ID|

#### 예시 코드  

```
const char* pMicID ="{0.0.1.00000000}.{7b0b712d-3b46-4f7a-bb83-bf9be4047f0d}";
ITMGContextGetInstance()->GetAudioCtrl()->SelectMic(pMicID);
```

### 마이크 닫기 실행
이 인터페이스는 마이크 닫기를 시작하는 데 사용됩니다. 방 추가 시 마이크 및 스피커가 켜져있지 않습니다.
EnableMic = EnableAudioCaptureDevice + EnableAudioSend.
####  함수 프로토타입  
```
ITMGAudioCtrl virtual int EnableMic(bool bEnabled)
```
|파라미터     | 유형         |의미|
| ------------- |:-------------:|-------------|
| bEnabled    |bool     |마이크를 켜야 할 경우 true로 전해지고, 마이크를 끄면 false로 파라미터가 전달됩니다|

####  예시 코드  
```
ITMGContextGetInstance()->GetAudioCtrl()->EnableMic(true);
```

### 마이크 상태 획득
이 인터페이스는 마이크 상태를 얻는 데 사용되며, 리턴 값 0은 마이크 끄기 상태이고, 리턴 값 1은 마이크를 켜기 위한 상태입니다.
####  함수 프로토타입  
```
ITMGAudioCtrl virtual int GetMicState()
```
####  예시 코드  
```
ITMGContextGetInstance()->GetAudioCtrl()->GetMicState();
```

### 채집 장치 닫기 실행
이 인터페이스는 채취 장비를 켜기/끄기 위해 사용됩니다. 방 추가 시 장비를 열지 않는 것이 기본값으로 정해져 있습니다.
- 방에 들어온 후에만 이 인터페이스를 사용할 수 있으며, 방 나가기 후 자동으로 장치를 잠급니다.
- 모바일 단말기에서 수집설비를 열면 일반적으로 권한신청, 볼륨타임조정 등의 조작이 수반됩니다.

####  함수 프로토타입  
```
ITMGContext virtual int EnableAudioCaptureDevice(bool enable)
```

|파라미터     | 유형         |의미|
| ------------- |:-------------:|-------------|
| enable    |bool     |채집 장치를 켜야 할 경우 true로 전해지고, 수집 장치를 끄면 false로 파라미터가 전달됩니다|

#### 예시 코드

```
채집 장치 열기
ITMGContextGetInstance()->GetAudioCtrl()->EnableAudioCaptureDevice(true);
```

### 채집 장치 상태 획득
이 인터페이스는 채집 장치 상태 획득하는 데 사용됩니다.
#### 함수 프로토타입

```
ITMGContext virtual bool IsAudioCaptureDeviceEnabled()
```
#### 예시 코드

```
ITMGContextGetInstance()->GetAudioCtrl()->IsAudioCaptureDeviceEnabled();
```

### 오디오 다운스트림 닫기 열기
이 인터페이스는 오디오 다운스트림을 켜기/끄기 하는데 사용됩니다. 채집 장치가 이미 켜져 있다면 채취한 음성 데이터를 발송합니다. 채집 장치가 켜져 있는 상황이 아니라면 소리가 나지 않습니다. 채집 장치의 켜기 끄기는 인터페이스 EnableAudioCaptureDevice를 참조합니다.

#### 함수 프로토타입

```
ITMGContext  virtual int EnableAudioSend(bool bEnable)
```
|파라미터     | 유형         |의미|
| ------------- |:-------------:|-------------|
| enable    |bool     |다운스트림을 켜야 할 경우 true로 전해지고, 다운스트림을 끄면 false로 파라미터가 전달됩니다|

#### 예시 코드  

```
ITMGContextGetInstance()->GetAudioCtrl()->EnableAudioSend(true);
```

### 오디오 다운스트림 상태 획득
이 인터페이스는 오디오 다운스트림 상태 획득에 사용됩니다.
#### 함수 프로토타입  
```
ITMGContext virtual bool IsAudioSendEnabled()
```
####  예시 코드  
```
ITMGContextGetInstance()->GetAudioCtrl()->IsAudioSendEnabled();
```

### 마이크 실시간 음량 획득
이 인터페이스는 마이크 실시간 음량 획득에 사용되며, 리턴값은 int 유형입니다.
####  함수 프로토타입  
```
ITMGAudioCtrl virtual int GetMicLevel()
```
####  예시 코드  
```
ITMGContextGetInstance()->GetAudioCtrl()->GetMicLevel();
```

### 오디오 다운스트림 실시간 음량 획득
이 인터페이스는 오디오 다운스트림 실시간 음량 획득에 사용되며, 리턴값은 int 유형으로 0부터 100 사이 범위값을 가지고 있습니다.
####  함수 프로토타입  
```
ITMGAudioCtrl virtual int GetSendStreamLevel()
```
#### 예시 코드  
```
ITMGContextGetInstance()->GetAudioCtrl()->GetSendStreamLevel();
```

### 마이크의 음량 설정
이 인터페이스는 마이크의 볼륨을 설정하는 데 사용됩니다. 파라미터 volume 은 마이크의 볼륨을 설정하는데 사용되며 수치가 0일 때 무음을 표시하고 수치가 100일 때 볼륨이 더이상 증가하지 않고 암묵적으로 수치가 100임을 나타냅니다.

####  함수 프로토타입  
```
ITMGAudioCtrl virtual int SetMicVolume(int vol)
```
|파라미터     | 유형         |의미|
| ------------- |:-------------:|-------------|
| vol    |int      |음량 설정, 범위 0 부터 200|

#### 예시 코드  
```
ITMGContextGetInstance()->GetAudioCtrl()->SetMicVolume(vol);
```
### 마이크의 음량 획득
이 인터페이스는 마이크 음량을 획득하는데 사용됩니다. 리턴값은 하나의 int 유형이며, 리턴값은 101이 인터페이스 SetMicVolume을 로드하지 않았음을 나타냅니다.

#### 함수 프로토타입  
```
ITMGAudioCtrl virtual int GetMicVolume()
```
####  예시 코드  
```
ITMGContextGetInstance()->GetAudioCtrl()->GetMicVolume();
```

### 획득한 스피커 장치 수
이 인터페이스는 스피커 장치 수 획득에 사용됩니다.

#### 함수 프로토타입  

```
ITMGAudioCtrl virtual int GetSpeakerListCount()
```
#### 예시 코드  

```
ITMGContextGetInstance()->GetAudioCtrl()->GetSpeakerListCount();
```

### 기거 스피커 장치
이 인터페이스는 기거 스피커 장치에 사용됩니다. GetSpeakerListCount 인터페이스에 맞춰 사용합니다.

#### 함수 프로토타입  
```
ITMGAudioCtrl virtual int GetSpeakerList(TMGAudioDeviceInfo* ppDeviceInfoList, int nCount)

class TMGAudioDeviceInfo
{
public:
	const char* pDeviceID;
	const char* pDeviceName;
};
```

|파라미터     | 유형         |의미|
| ------------- |:-------------:|-------------|
| ppDeviceInfoList    |TMGAudioDeviceInfo    |장치 리스트|
| nCount   |int     |획득한 스피커 장치 수|

#### 예시 코드  
```
ITMGContextGetInstance()->GetAudioCtrl()->GetSpeakerList(ppDeviceInfoList,nCount);
```

### 스피커 장치 선택
이 인터페이스는 재생 장치를 선택하는 데 사용됩니다. 디버깅하거나 디버깅하지 않을 경우 시스템 랜덤으로 재생 장비를 선택합니다. 장치 ID는 GetSpeakerList 리턴 리스트에서 가져옵니다.

#### 함수 프로토타입  
```
ITMGAudioCtrl virtual int SelectSpeaker(const char* pSpeakerID)
```

|파라미터     | 유형         |의미|
| ------------- |:-------------:|-------------|
| pSpeakerID    |char*      |스피커 장치 ID|

#### 예시 코드  
```
const char* pSpeakerID ="{0.0.1.00000000}.{7b0b712d-3b46-4f7a-bb83-bf9be4047f0d}";
ITMGContextGetInstance()->GetAudioCtrl()->SelectSpeaker(pSpeakerID);
```

### 스피커 닫기 진행
이 인터페이스는 스피커 닫기 시작하는데 사용됩니다.
EnableSpeaker = EnableAudioPlayDevice +  EnableAudioRecv.
####  함수 프로토타입  
```
ITMGAudioCtrl virtual int EnableSpeaker(bool enabled)
```
|파라미터     | 유형         |의미|
| ------------- |:-------------:|-------------|
| enable   |bool       |스피커를 꺼야 할 경우 false로 전해지고, 스피커를 켜면 true로 파라미터가 전달됩니다|

####  예시 코드  
```
ITMGContextGetInstance()->GetAudioCtrl()->EnableSpeaker(true);
```

### 스피커 상태 획득
이 인터페이스는 스피커 상태 획득에 사용됩니다. 리턴 값 0은 스피커 상태를 끄기 위해, 리턴 값 1은 스피커 상태를 켜기 위해, 리턴 값 2는 스피커 장비를 위해 조작 중입니다.
####  함수 프로토타입  
```
ITMGAudioCtrl virtual int GetSpeakerState()
```

####  예시 코드  
```
ITMGContextGetInstance()->GetAudioCtrl()->GetSpeakerState();
```



### 재생 장치 닫기 진행
이 인터페이스는 재생 장치 닫기 진행에 사용됩니다.

#### 함수 프로토타입  
```
ITMGContext virtual int EnableAudioPlayDevice(bool enable) 
```
|파라미터     | 유형         |의미|
| ------------- |:-------------:|-------------|
| enable    |bool        |재생 장치를 꺼야 할 경우 false로 전해지고, 재생 장치를 켜면 true로 파라미터가 전달됩니다|

#### 예시 코드  
```
ITMGContextGetInstance()->GetAudioCtrl()->EnableAudioPlayDevice(true);
```

### 재생 장치 상태 획득
이 인터페이스는 재생 장치 상태 획득에 사용됩니다.
#### 함수 프로토타입

```
ITMGContext virtual bool IsAudioPlayDeviceEnabled()
```
#### 예시 코드  

```
ITMGContextGetInstance()->GetAudioCtrl()->IsAudioPlayDeviceEnabled();
```

### 오디오 업스트림 닫기 열기
이 인터페이스는 오디오 업스트림을 켜기/끄기 하는데 사용됩니다. 재생 장치가 이미 열려 있다면 방에 있는 다른 사람의 오디오 데이터를 재생합니다. 재생 장치가 켜져 있지 않으면 계속해서 무음입니다. 재생 장치의 켜기 끄기는 인터페이스 EnableAudioPlayDevice를 참조합니다.

#### 함수 프로토타입  

```
ITMGContext virtual int EnableAudioRecv(bool enable)
```
|파라미터     | 유형         |의미|
| ------------- |:-------------:|-------------|
| enable    |bool     |오디오 업스트림을 켜야 할 경우 true로 전해지고, 오디오 업스트림을 끄면 false로 파라미터가 전달됩니다|

#### 예시 코드  

```
ITMGContextGetInstance()->GetAudioCtrl()->EnableAudioRecv(true);
```



### 오디오 업스트림 상태 획득
이 인터페이스는 오디오 업스트림 상태 획득에 사용됩니다.
#### 함수 프로토타입  
```
ITMGContext virtual bool IsAudioRecvEnabled() 
```

####  예시 코드  
```
ITMGContextGetInstance()->GetAudioCtrl()->IsAudioRecvEnabled();
```

### 스피커 실시간 음량 획득
이 인터페이스는 스피커 실시간 음량 획득에 사용되며 리턴값은 int 유형 수치로 스피커 실시간 음량을 나타냅니다.
####  함수 프로토타입  
```
TMGAudioCtrl virtual int GetSpeakerLevel()
```

####  예시 코드  
```
ITMGContextGetInstance()->GetAudioCtrl()->GetSpeakerLevel();
```

### 방 내 다른 멤버 업스트림 실시간 음량 획득
이 인터페이스는 방 내 다른 멤버 업스트림 실시간 음량 획득에 사용되며 리턴값은 int 유형으로 0부터 100까지의 범위값을 가지고 있습니다.
####  함수 프로토타입  
```
ITMGAudioCtrl virtual int GetRecvStreamLevel(const char* openId)
```

|파라미터     | 유형         |의미|
| ------------- |:-------------:|-------------|
| openId    |char*       |방 다른 멤버의 openId|

####  예시 코드  
```
iter->second.level = ITMGContextGetInstance()->GetAudioCtrl()->GetRecvStreamLevel(iter->second.openid.c_str());
```

### 스피커의 음량 설정
이 인터페이스는 스피커의 음량 설정에 사용됩니다.
파라미터 volume 은 스피커 음령을 설정하는데 사용되며 수치가 0일 때 무음을 표시하고 수치가 100일 때 볼륨이 증가하지 않음을 나타내며 암묵적인 수치는 100입니다.

####  함수 프로토타입  
```
ITMGAudioCtrl virtual int SetSpeakerVolume(int vol)
```
|파라미터     | 유형         |의미|
| ------------- |:-------------:|-------------|
| vol    |int        |음량 설정, 0 부터 200|

#### 예시 코드  
```
int vol = 100;
ITMGContextGetInstance()->GetAudioCtrl()->SetSpeakerVolume(vol);
```

### 스피커의 음량 획득

이 인터페이스는 스피커 음량을 획득하는데 사용됩니다. 리턴 값은 int 유형 수치로 스피커 음량을 의미하며, 리턴 값은 101이 인터페이스 SetSpeakerVolume을 로드하지 않았음을 나타냅니다.
Level은 실시간 음량이고 Volume은 스피커 음량이며 최종 사운드 볼륨은 Level*Volume%에 해당합니다. 예를 들어: 실시간 음량의 수치가 100, Volume의 수치가 60이면, 그러면 결과적으로 발생하는 소리의 수치도 60이 됩니다.

####  함수 프로토타입  
```
ITMGAudioCtrl virtual int GetSpeakerVolume()
```
####  예시 코드  
```
ITMGContextGetInstance()->GetAudioCtrl()->GetSpeakerVolume();
```


### 인이어 모니터링 시작
이 인터페이스는 인이어 모니터링 시작에 사용됩니다.
####  함수 프로토타입  
```
ITMGAudioCtrl virtual int EnableLoopBack(bool enable)
```
|파라미터     | 유형         |의미|
| ------------- |:-------------:|-------------|
| enable    |bool         |설정 시작 여부|

####  예시 코드  
```
ITMGContextGetInstance()->GetAudioCtrl()->EnableLoopBack(true);
```


## 오프라인 음성 채팅의 음성 텍스트 전환 순서도
![](https://main.qcloudimg.com/raw/9ef5e5e4ebc8e63bcd7bfbea6cfb94cc.png)



## 오프라인 음성 채팅
초기화하기 전에 SDK가 초기화되지 않은 단계로 인터페이스 Init를 통해 SDK를 초기화해야 실시간 음성 및 오프라인 음성을 사용할 수 있습니다.
사용 시 문제가 있다면 [오프라인 음성 관련 문제](https://intl.cloud.tencent.com/document/product/607/30258)를 참조하십시오.

### 관련 인터페이스 초기화

|인터페이스     | 인터페이스 의미   |
| ------------- |:-------------:|
|Init    |GME 초기화|
|Poll    |트리거 이벤트 콜백|
|Pause   |시스템 일시정지|
|Resume |시스템 복구|
|Uninit    |GME 초기화 취소 |


### 오프라인 음성 관련 인터페이스
|인터페이스     | 인터페이스 의미   |
| ------------- |:-------------:|
|ApplyPTTAuthbuffer    |인증 초기화|
|SetMaxMessageLength    |음성 메시지 최대 길이 제한|
|StartRecording|녹음 시작|
|StartRecordingWithStreamingRecognition|스트리밍 녹음 시작|
|PauseRecording|녹음 일시정지|
|ResumeRecording|녹음 복구|
|StopRecording    |녹음 중지|
|CancelRecording|녹음 취소|
|GetMicLevel|오프라인 실시간 마이크 음량 획득|
|SetMicVolume|오프라인 음성 레코딩 음량 설정|
|GetMicVolume|오프라인 음성 레코딩 음량 획득|
|GetSpeakerLevel|오프라인 음성 실시간 스피커 음량 획득  |
|SetSpeakerVolume|오프라인 음성 재생 음량 설정|
|GetSpeakerVolume|오프라인 음성 재생 음량 획득|
|UploadRecordedFile |음성 파일 업로드|
|DownloadRecordedFile|음성 파일 다운로드|
|PlayRecordedFile |음성 재생|
|StopPlayFile|음성 재생 중지|
|GetFileSize |음성 파일의 크기|
|GetVoiceFileDuration|음성 파일의 길이|
|SpeechToText |음성을 텍스트로 식별|

### 인증 초기화
DK를 초기화한 후에 인증 초기화를 호출하시고, authBuffer의 획득은 윗글의 실시간 음성 인증 정보 인터페이스를 참조합니다.
#### 함수 프로토타입  
```
ITMGPTT virtual int ApplyPTTAuthbuffer(const char* authBuffer, int authBufferLen)
```
|파라미터     | 유형         |의미|
| ------------- |:-------------:|-------------|
| authBuffer    |char*                    |인증|
| authBufferLen    |int                |인증 길이|

#### 예시 코드  
```
ITMGContextGetInstance()->GetPTT()->ApplyPTTAuthbuffer(authBuffer,authBufferLen);
```

### 음성 메시지 최대 길이 제한
최대 음성 메시지의 길이를 제한하고 최대 60초까지 지원합니다.

####  함수 프로토타입

```
ITMGPTT virtual int SetMaxMessageLength(int msTime)
```
|파라미터     | 유형         |의미|
| ------------- |:-------------:|-------------|
| msTime    |int                    |음성 메시지 길이, 단위 ms|

#### 예시 코드  
```
int msTime = 10;
ITMGContextGetInstance()->GetPTT()->SetMaxMessageLength(msTime);
```


### 녹음 시작
이 인터페이스는 녹음을 작동하기 위해 사용되며 녹음파일을 업로드 후에야 음성 텍스트 간 전환 등 작업이 가능합니다.
####  함수 프로토타입  
```
ITMGPTT virtual int StartRecording(const char* fileDir)
```
|파라미터     | 유형         |의미|
| ------------- |:-------------:|-------------|
| fileDir    |char*                      |보관된 음성 경로|

####  예시 코드  
```
ITMGContextGetInstance()->GetPTT()->StartRecording(fileDir);
```

### 녹음의 콜백 시작
녹음이 완료된 후의 콜백은 함수 OnEvent를 작동할 수 있으며 이벤트 소식은 ITMG_MAIN_EVNET_TYPE_PTT_RECORD_COMPLETE입니다. OnEvent 함수에서 이벤트 소식을 판단합니다.
전달된 파라미터에는 result 와 file_path, 이 두 가지의 정보가 포함되어 있습니다.

#### 에러코드
|에러코드값 |원인  |권장방안        |
|-----|------|------|
|4097   |파라미터가 없음|코드 중 인터페이스 파라미터가 정확한지 검토|
|4098   |초기화 에러|장치가 점유 되었는지, 또는 권한이 정상인지, 초기화가 정상인지를 점검|
|4099   |현재 레코딩 중|SDK 녹화 기능을 올바른 시기에 사용할 수 있도록 보장|
|4100   |오디오 데이터 수집 안됨|마이크 장치가 정상인지 점검|
|4101   |녹음 시, 레코딩 파일 엑세스 에러|파일이 존재하는지, 파일이 합법적인 루트로 존재하는 것인지 확인|
|4102   |마이크 라이센스 미부여로 인한 에러|SDK를 사용하려면 마이크 권한이 필요하며 권한 추가는 엔진 또는 플랫폼에 대응하는 SDK 엔지니어링 배치 문서를 참조하십시오|
|4103   |녹음 시간이 너무 짧음으로 인한 에러|우선 녹음할 때 단위를 ms로 제한하여 파라미터가 올바른지 검사하고, 그 다음, 녹음할 때 1,000ms 이상 지속되어야 녹화에 성공할 수 있습니다|
|4104   |녹음 조작이 작동하지 않음|녹음 인터페이스가 조정되어 있는지 점검|

####  예시 코드  
```
void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data){
	switch (eventType) {
		case ITMG_MAIN_EVENT_TYPE_ENTER_ROOM:
		{
		//처리 진행
		break;
	    }
		...
        case ITMG_MAIN_EVNET_TYPE_PTT_RECORD_COMPLETE:
		{
		//처리 진행
		break;
		}
	}
}
```

### 스트리밍 음성 인식 시작
이 인터페이스는 스트리밍 음성 인식을 작동시키는 데 사용되며, 동시에 세션 중에 실시간 음성을 텍스트로 전환하여 되돌아올 수 있으며, 언어를 지정하여 인식할 수 있고 음성에서 인식된 정보를 지정된 언어로 번역하여 돌아올 수도 있습니다.

#### 함수 프로토타입  

```
ITMGPTT virtual int StartRecordingWithStreamingRecognition(const char* filePath) 
ITMGPTT virtual int StartRecordingWithStreamingRecognition(const char* filePath,const char* translateLanguage,const char* translateLanguage) 
```
|파라미터     | 유형         |의미|
| ------------- |:-------------:|-------------|
| filePath    |char*|보관된 음성 경로|
| speechLanguage    |char*                     |지정된 언어로 식별된 텍스트 파라미터와 관련하여 [음성을 텍스트로 변환한 언어 파라미터 참조 리스트](https://intl.cloud.tencent.com/document/product/607/30260)를 참조하십시오|
| translateLanguage    |char*                     |지정된 언어로 번역된 텍스트 파라미터와 관련하여 [음성을 텍스트로 변환한 언어 파라미터 참조 리스트](https://intl.cloud.tencent.com/document/product/607/30260)를 참조하십시오(이 파라미터는 당분간 사용할 수 없으므로, speechLanguage와 같은 파라미터를 작성하십시오)|

#### 예시 코드  
```
ITMGContextGetInstance()->GetPTT()->StartRecordingWithStreamingRecognition(filePath,"cmn-Hans-CN","cmn-Hans-CN");
```

### 스트리밍 음성 인식의 콜백 시작
스트리밍 음성 인식이 완료된 후의 콜백에선 함수 OnEvent를 통하여 조정할 수 있습니다. 이벤트 소식은 ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_COMPLETE으로, OnEvent 함수에서 이벤트 소식을 판단합니다. 전달된 파라미터에는 다음과 같은 네 가지 정보가 포함되어 있습니다.

|소식 이름     | 의미         |
| ------------- |:-------------:|
| result    |스트리밍 음성 인식이 성공적이었는지 여부를 판단하는 데 사용되는 리턴코드|
| text    |음성 텍스트 간 전환 인식 텍스트|
| file_path |녹음이 저장된 주소|
| file_id |녹음이 저장된 백그라운드 url 주소|

#### 에러코드

|에러코드     | 의미         |처리방법|
| ------------- |:-------------:|:-------------:|
|32775|스트리밍 음성을 텍스트로 변환하는데는 실패했지만, 녹음 성공| UploadRecordedFile 인터페이스로 녹음을 업로드하고 SpeechToText 인터페이스로 음성을 텍스트로 변환 작업 호출 |
|32777|스트리밍 음성을 텍스트로 변환하는데는 실패했지만 녹음은 성공하며, 업로드도 성공|되돌아온 메시지에는 업로드에 성공한 백그라운드 url 주소가 있으므로 SpeechToText 인터페이스로 음성을 텍스트로 변환하는 작업을 진행|
|32786  |스트리밍 음성을 텍스트로 변환에 실패|스트리밍 녹화 상태에서, 스트리밍 녹화 인터페이스 실행 결과가 다시 되돌아 올 때까지 기다리십시오|

#### 예시 코드  
```
void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data){
	switch (eventType) {
		case ITMG_MAIN_EVENT_TYPE_ENTER_ROOM:
		{
		//처리 진행
		break;
	    }
		...
        case ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_COMPLETE:
		{
		//처리 진행
		break;
		}
	}
}
```

### 녹음 일시중지
이 인터페이스는 녹음을 일시 중지하는 데 사용됩니다. 레코딩을 복원해야 하는 경우 ResumeRecording을 호출하십시오.

#### 함수 프로토타입  
```
ITMGPTT virtual int PauseRecording()
```
####  예시 코드  
```
ITMGContextGetInstance()->GetPTT()->PauseRecording();
```

### 녹음 복구
이 인터페이스는 녹음 복구에 사용됩니다.

#### 함수 프로토타입  
```
ITMGPTT virtual int ResumeRecording()
```
####  예시 코드  
```
ITMGContextGetInstance()->GetPTT()->ResumeRecording();
```

### 녹음 중지
이 인터페이스는 녹음을 중지하는 데 사용됩니다. 이 인터페이스는 비동기 인터페이스이며, 녹음을 중지하면 녹음이 완료되어 세션이 완료되고 성공한 이후에만 녹음 파일이 사용이 가능합니다.
#### 함수 프로토타입  
```
ITMGPTT virtual int StopRecording()
```
####  예시 코드  
```
ITMGContextGetInstance()->GetPTT()->StopRecording();
```



### 녹음 취소
이 인터페이스는 녹음 취소에 사용되며 취소한 후에는 돌이킬 수 없습니다.
#### 함수 프로토타입  
```
ITMGPTT virtual int CancelRecording()
```
####  예시 코드  
```
ITMGContextGetInstance()->GetPTT()->CancelRecording();
```

### 오프라인 음성 마이크 실시간 음량 획득
이 인터페이스는 마이크의 실시간 음량을 얻는 데 사용되며, 리턴값은 int 유형이며, 값 영역은 0에서 100까지입니다.

#### 함수 프로토타입  
```
ITMGPTT virtual int GetMicLevel()
```
#### 예시 코드  
```
ITMGContextGetInstance()->GetPTT()->GetMicLevel();
```

### 오프라인 음성 레코딩 음량 설정
이 인터페이스는 오프라인 음성 녹화 음량을 설정하는 데 사용되며, 값 영역은 0에서 100까지입니다.

#### 함수 프로토타입  
```
ITMGPTT virtual int SetMicVolume(int vol)
```
#### 예시 코드  
```
ITMGContextGetInstance()->GetPTT()->SetMicVolume(100);
```

### 오프라인 음성 레코딩 음량 획득
이 인터페이스는 오프라인 음성 녹화 음량을 얻는 데 사용됩니다. 리턴값은 int 유형이며, 값 영역은 0에서 100까지입니다.

#### 함수 프로토타입  
```
ITMGPTT virtual int GetMicVolume()
```

#### 예시 코드  
```
ITMGContextGetInstance()->GetPTT()->GetMicVolume();
```


### 스피커 실시시간 음량 획득
이 인터페이스는 스피커 실시간 음량을 얻는 데 사용됩니다. 리턴값은 int 유형이며, 값 영역은 0에서 100까지입니다.

#### 함수 프로토타입  
```
ITMGPTT virtual int GetSpeakerLevel()
```

#### 예시 코드  
```
ITMGContextGetInstance()->GetPTT()->GetSpeakerLevel();
```

### 오프라인 음성 재생 음량 설정
이 인터페이스는 오프라인 음성 재생 음향을 설정하는 데 사용되며, 값 영역은 0에서 100까지입니다.

#### 함수 프로토타입  
```
ITMGPTT virtual int SetSpeakerVolume(int vol)
```
#### 예시 코드  
```
ITMGContextGetInstance()->GetPTT()->SetSpeakerVolume(100);
```

### 오프라인 음성 재생 음량 획득
이 인터페이스는 오프라인 음성 재생 볼륨을 설정하는 데 사용됩니다. 리턴값은 int 유형이며 값 영역은 0에서 100까지입니다.

#### 함수 프로토타입  
```
ITMGPTT virtual int GetSpeakerVolume()
```

#### 예시 코드  
```
ITMGContextGetInstance()->GetPTT()->GetSpeakerVolume();
```




### 음성 파일 업로드
이 인터페이스는 음성 파일 업로드에 사용됩니다.
#### 함수 프로토타입  
```
ITMGPTT virtual int UploadRecordedFile(const char* filePath)
```
|파라미터     | 유형         |의미|
| ------------- |:-------------:|-------------|
| filePath    |char*                       |음성 업로드 경로|

#### 예시 코드  
```
ITMGContextGetInstance()->GetPTT()->UploadRecordedFile(filePath);
```


### 음성 업로드 완료의 콜백
음성 업로드가 완료되면 이벤트 소식은 ITMG_MAIN_EVNET_TYPE_PTT_UPLOAD_COMPLETE로 OnEvent 함수에서 이벤트 소식을 판단합니다.
전달된 파라미터에는 result, file_path 와 file_id, 이 세가지의 정보가 포함되어 있습니다.

#### 에러코드

|에러코드값 |원인  |권장 방안        |
|-----|------|------|
|8193   |파일 업로드 시, 파일 엑세스 에러|파일이 확실히 존재하는지, 그리고 합법적인 경로로 만들어진 파일인지 확인|
|8194   |서명 교정 실패 오류|인증 비밀키가 정확한지 점검하고, 초기화된 오프라인 음성이 있는지 점검한다|
|8195   |네트워크 에러|디바이스 네트워크가 외부 네트워크 환경을 제대로 방문할 수 있는지 점검|
|8196   |업로드된 파라미터 획득 과정에서의 네트워크 에러|인증이 올바른지 점검하고, 디바이스 네트워크가 외부 네트워크 환경에 제대로 접근할 수 있는지 점검|
|8197   |업로드된 파라미터 획득 과정에서의 롤백 데이터가 비어있음|인증이 올바른지 점검하고, 디바이스 네트워크가 외부 네트워크 환경에 제대로 접근할 수 있는지 점검|
|8198   |업로드된 파라미터 획득 과정에서의 로딩 오류|인증이 올바른지 점검하고, 디바이스 네트워크가 외부 네트워크 환경에 제대로 접근할 수 있는지 점검|
|8200   |appinfo 설정 안됨|apply 인터페이스가 사용되고 있는지, 또는 인풋 파라미터가 비어 있는지 검사|

#### 예시 코드

```
void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data){
	switch (eventType) {
		case ITMG_MAIN_EVENT_TYPE_ENTER_ROOM:
		{
		//처리 진행
		break;
	    }
		...
        case ITMG_MAIN_EVNET_TYPE_PTT_UPLOAD_COMPLETE:
		{
		//처리 진행
		break;
		}
	}
}
```


### 음성 파일 다운로드
이 인터페이스는 음성 파일 다운로드에 사용됩니다.
#### 함수 프로토타입  
```
ITMGPTT virtual int DownloadRecordedFile(const char* fileId, const char* filePath) 
```
|파라미터     | 유형         |의미|
| ------------- |:-------------:|-------------|
| fileId  |char*   |파일의 url 경로|
| filePath |char*  |파일의 드라이브 저장 경로|

####  예시 코드  
```
ITMGContextGetInstance()->GetPTT()->DownloadRecordedFile(fileID,filePath);
```


### 음성 파일 다운로드 완료 콜백
음성 다운로드가 완료되면 이벤트 소식은 ITMG_MAIN_EVNET_TYPE_PTT_DOWNLOAD_COMPLETE로 OnEvent 함수에서 이벤트 소식을 판단합니다.

#### 에러코드

|에러코드값 |원인  |권장 방안        |
|-----|------|------|
|12289  |파일 다운로드 시, 파일 엑세스 에러    |파일 경로가 합법적인지 검사|
|12290  |서명 교정 에러    |맞는 인증 보안키인지 확인하고, 초기화된 오프라인 음성이 있는지 확인|
|12291  |네트워크 스토리지 시스템 이상    |서버에서 음성 파일 획득 실패인 경우, 인터페이스 파라미터 fileid 올바르게 구성되었는지 검사하고, 네트워크가 정상인지 확인, cos 파일 존재 여부 점검|
|12292  |서버 파일 시스템 오류    |디바이스 네트워크가 외부 네트워크 환경에 제대로 접근할 수 있는지 점검하고, 서버에 이 파일이 있는지 점검|
|12293  |다운로드된 파라미터를 획득하는 과정에서 HTTP 네트워크 에러 |디바이스 네트워크가 외부 네트워크 환경을 제대로 방문할 수 있는지 점검|
|12294  |다운로드된 파라미터 획득하는 과정에서 반환 데이터가 없음 |디바이스 네트워크가 외부 네트워크 환경을 제대로 방문할 수 있는지 점검|
|12295  |다운로드된 파라미터 획득하는 과정에서 압축 해제 오류|디바이스 네트워크가 외부 네트워크 환경을 제대로 방문할 수 있는지 점검|
|12297  |appinfo 설정 안됨|는 인증 보안키인지 확인하고, 초기화된 오프라인 음성이 있는지 확인|


#### 예시 코드

```
void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data){
	switch (eventType) {
		case ITMG_MAIN_EVENT_TYPE_ENTER_ROOM:
		{
		//처리 진행
		break;
	    }
		...
        case ITMG_MAIN_EVNET_TYPE_PTT_DOWNLOAD_COMPLETE:
		{
		//처리 진행
		break;
		}
	}
}
```



### 음성 재생
이 인터페이스는 음성 재생에 사용됩니다.
#### 함수 프로토타입  
```
ITMGPTT virtual int PlayRecordedFile(const char* filePath)
```
|파라미터     | 유형         |의미|
| ------------- |:-------------:|-------------|
| filePath    |char*                       |파일의 경로|

#### 에러코드

|에러코드값 |원인  |권장 방안        |
|-----|------|------|
|20485  |재생 미시작|파일의 존재 확보, 파일 경로의 합법성 검토|

####  예시 코드  
```
ITMGContextGetInstance()->GetPTT()->PlayRecordedFile(filePath);
```


### 음성 재생의 콜백
음성 재생의 콜백의 이벤트 소식은 ITMG_MAIN_EVNET_TYPE_PTT_PLAY_COMPLETE로 OnEvent 함수에서 이벤트 소식을 판단합니다.
전송된 파라미터에는 result, file_path, 이 두 개의 정보가 포함되어 있습니다.

#### 에러코드

|에러코드값 |원인  |권장 방안        |
|-----|------|------|
|20481  |초기화 에러|장치가 점유 되었는지, 또는 권한이 정상인지, 초기화가 정상인지 점검|
|20482  |현재 재생 중인 상황에서 끊거나 다음 파일을 재생하면 실패하는 오류 (정상적으론 재생 중단이 가능함)|코드 배열 논리가 올바른지 점검|
|20483  |파라미터 없음|코드 중 인터페이스 파라미터가 올바른지 점검|
|20484  |내부 오류|초기화 플레이어 오류, 암호 해독 실패 등의 문제로 인해 본 에러코드가 발생한 경우 로그 조회하여 문제 찾기|

#### 예시 코드

```
void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data){
	switch (eventType) {
		case ITMG_MAIN_EVENT_TYPE_ENTER_ROOM:
		{
		//처리 진행
		break;
	    }
		...
        case ITMG_MAIN_EVNET_TYPE_PTT_PLAY_COMPLETE:
		{
		//처리 진행
		break;
		}
	}
}
```




### 음성 재생 일시중지
이 인터페이스는 음성 재생 일시중지에 사용되며, 일시중지 되어도 끝까지 들을 수 있습니다.
####  함수 프로토타입  
```
ITMGPTT virtual int StopPlayFile()
```

####  예시 코드  
```
ITMGContextGetInstance()->GetPTT()->StopPlayFile();
```



### 획득한 음성 파일의 크기
이 인터페이스를 통하여 획득한 음성 파일의 크기를 알 수 있습니다.
####  함수 프로토타입  
```
ITMGPTT virtual int GetFileSize(const char* filePath)
```
|파라미터     | 유형         |의미|
| ------------- |:-------------:|-------------|
| filePath    |char*                      |음성 파일의 경로|

####  예시 코드  
```
ITMGContextGetInstance()->GetPTT()->GetFileSize(filePath);
```

### 획득한 음성 파일의 길이
이 인터페이스를 사용하여 음성 파일의 길이를 알 수 있으며, 단위는 ms입니다.
####  함수 프로토타입  
```
ITMGPTT virtual int GetVoiceFileDuration(const char* filePath)
```
|파라미터     | 유형         |의미|
| ------------- |:-------------:|-------------|
| filePath    |char*                      |음성 파일의 경로|

####  예시 코드  
```
ITMGContextGetInstance()->GetPTT()->GetVoiceFileDuration(filePath);
```


### 지정된 음성 파일을 텍스트로 식별
이 인터페이스는 지정된 음성 파일을 문자로 식별하는 데 사용됩니다.

#### 함수 프로토타입  
```
ITMGPTT virtual void SpeechToText(const char* fileID)
```
|파라미터     | 유형         |의미|
| ------------- |:-------------:|-------------|
| fileID    |char*                      |음성 파일 url|

#### 예시 코드  
```
ITMGContextGetInstance()->GetPTT()->SpeechToText(fileID);
```



### 지정된 음성 파일을 텍스트로 번역 (지정 언어)
이 인터페이스는 언어를 지정하여 식별할 수도 있고 음성에서 인식된 정보를 지정된 언어로 번역하여 보여줄 수도 있습니다.

#### 함수 프로토타입  
```
ITMGPTT virtual int SpeechToText(const char* fileID,const char* speechLanguage,const char* translateLanguage)
```
|파라미터     | 유형         |의미|
| ------------- |:-------------:|-------------|
| fileID    |char*                     |음성 파일 url|
| speechLanguage    |char*                     |지정된 텍스트의 언어 파라미터를 식별하려면 [음성을 텍스트로 전환한 언어 파라미터 참조 리스트](https://intl.cloud.tencent.com/document/product/607/30260)를 참조하십시오|
| translatelanguage    |char*                  |지정된 텍스트의 언어 파라미터를 번역하려면 [음성을 텍스트로 전환한 언어 파라미터 참조 리스트](https://intl.cloud.tencent.com/document/product/607/30260)를 참조하십시오(이 파라미터는 일시적으로 유효하지 않으므로, 인풋 파라미터는 speechLanguage와 일치해야 합니다)|

#### 예시 코드  
```
ITMGContextGetInstance()->GetPTT()->SpeechToText(filePath,"cmn-Hans-CN","cmn-Hans-CN");
```



### 인식 콜백 
지정한 음성 파일을 문자 콜백으로 인식, 이벤트 소식은 ITMG_MAIN_EVNET_TYPE_PTT_SPEECH2TEXT_COMPLETE 으로, OnEvent 함수에서 이벤트 소식을 판단합니다.
전달된 파라미터 패키지에는 result, file_path 와 text와 같은 세가지 정보가 포함되어 있으며, 그 중 text 가 인식된 글자입니다.

#### 에러코드

|에러코드 값 |원인  |권장방안        |
|-----|------|------|
|32769 |내부 오류|로그를 분석하여 백그라운드에서 클라이언트에게 리턴되는 진정한 에러코드를 획득하고, 백그라운드 동료에게 연락하여 해결을 돕습니다.|
|32770 |네트워크 실패|디바이스의 네트워크가 외부망 환경에 정상적으로 액세스 가능한지 점검|
|32772  |패킷 리턴, 패킷 압축 실패|로그를 분석합니다. 백그라운드에서 클라이언트에 리턴한 에러코드를 획득하여 백그라운드 담당자에게 연락하면 문제 해결을 지원드립니다.|
|32774  |appinfo를 설정하지 않음|인증 보안키가 정확한지 체크, 오프라인 음성을 초기화하였는지 체크|
|32776  |authbuffer 검증 실패|authbuffer가 정확한지 검증|
|32784  |음성 텍스트 변환 파라미터 에러|코드의 API 파라미터 fileid가 비었는지 체크|
|32785  |음성 텍스트 변환 번역 리턴 에러|오프라인 음성 백그라운드 에러, 로그를 분석하고 백그라운드에서 클라이언트에 리턴한 에러코드를 획득하세요. 백그라운드 담당자와 연락하면 해결 관련 지원드립니다|

#### 예시 코드

```
void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data){
	switch (eventType) {
		case ITMG_MAIN_EVENT_TYPE_ENTER_ROOM:
		{
		//처리
		break;
	    }
		...
        case ITMG_MAIN_EVNET_TYPE_PTT_SPEECH2TEXT_COMPLETE:
		{
		//처리
		break;
		}
	}
}
```



## 고급 API

### 진단 메시지 획득
오디오/비디오 통화의 실시간 통화 퀄리티 관련 메시지를 읽어옵니다. 이 API는 실시간 통화 퀄리티를 조회하고 문제를 체크하며, 업무측에서 무시해주시면 됩니다.
#### 함수 프로토타입
```
ITMGRoom virtual const char* GetQualityTips()
```
#### 예시 코드  
```
ITMGContextGetInstance()->GetRoom()->GetQualityTips();
```


### 버전 번호 획득
#### 함수 프로토타입

```
ITMGContext virtual const char* GetSDKVersion()
```



#### 예시 코드  

```
ITMGContextGetInstance()->GetSDKVersion();
```




### 프린팅 로그 레벨 설정
프린팅 로그 레벨을 설정합니다. 기본 레벨을 유지하시기를 추천드립니다.
#### 함수 프로토타입
```
ITMGContext int SetLogLevel(ITMG_LOG_LEVEL levelWrite, ITMG_LOG_LEVEL levelPrint)
```

#### 파라미터 의미

|파라미터|타입|의미|
|---|---|---|
|levelWrite|ITMG_LOG_LEVEL|입력 로그 레벨 설정, TMG_LOG_LEVEL_NONE 입력하지 않음을 의미|
|levelPrint|ITMG_LOG_LEVEL|프린팅 로그 레벨 설정, TMG_LOG_LEVEL_NONE 프린팅하지 않음을 의미|



|ITMG_LOG_LEVEL|의미|
| -------------------------------|----------------------|
|TMG_LOG_LEVEL_NONE=0|로그를 프린팅하지 않음|
|TMG_LOG_LEVEL_ERROR=1|에러 로그 프린팅(디폴트)|
|TMG_LOG_LEVEL_INFO=2|안내 로그 프린팅|
|TMG_LOG_LEVEL_DEBUG=3|개발 테스트 로그 프린팅|
|TMG_LOG_LEVEL_VERBOSE=4|고주파 로그 프린팅|

#### 예시 코드  
```
ITMGContext* context = ITMGContextGetInstance();
context->SetLogLevel(TMG_LOG_LEVEL_INFO,TMG_LOG_LEVEL_INFO);
```



## 프린팅 로그 경로 설정
프린팅 로그 경로를 설정합니다.
디폴트 경로: 

|플랫폼     |경로        |
| ------------- |:-------------:|
|Windows |%appdata%\Tencent\GME\ProcessName|
|iOS    |Application/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/Documents|
|Android|/sdcard/Android/data/xxx.xxx.xxx/files|
|Mac    |/Users/username/Library/Containers/xxx.xxx.xxx/Data/Documents|

#### 함수 프로토타입
```
ITMGContext virtual int SetLogPath(const char* logDir) 
```

|파라미터     | 타입         |의미|
| ------------- |:-------------:|-------------|
| logDir    |char*    |경로|

#### 예시 코드  

```
cosnt char* logDir = ""//스스로 경로 설정

ITMGContext* context = ITMGContextGetInstance();
context->SetLogPath(logDir);
```

### 가청주파서 데이터 블랙리스트 추가
임의 ID를 가청주파수 데이터 블랙리스트에 추가합니다. 리턴값 0은 호출 성공하였음을 의미합니다.
#### 함수 프로토타입  

```
ITMGContext ITMGAudioCtrl int AddAudioBlackList(const char* openId)
```
|파라미터     | 타입         |의미|
| ------------- |:-------------:|-------------|
| openId    |char*       |블랙리스트를 추가할  ID|

#### 예시 코드  

```
ITMGContextGetInstance()->GetAudioCtrl()->AddAudioBlackList(openId);
```

### 가청주파수 데이터 블랙리스트에서 제외
임의 ID를 가청주파수 데이터 블랙리스트에서 제외합니다. 리턴값 0은 호출 성공하였음을 의미합니다.
#### 함수 프로토타입  

```
ITMGContext ITMGAudioCtrl int RemoveAudioBlackList(const char* openId)
```
|파라미터     | 타입         |의미|
| ------------- |:-------------:|-------------|
| openId    |char*       |블랙리스테에서 제외할 ID|

#### 예시 코드  

```
ITMGContextGetInstance()->GetAudioCtrl()->RemoveAudioBlackList(openId);
```


## 콜백 메시지

### 메시지 리스트:

|메시지     | 메시지가 대표하는 의미   |
| ------------- |:-------------:|
|ITMG_MAIN_EVENT_TYPE_ENTER_ROOM    |가청주파수 방 로그인 메시지|
|ITMG_MAIN_EVENT_TYPE_EXIT_ROOM    |가청주파수 방 로그아웃 메시지|
|ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT|네트워크 등 이유로 방 메시지가 끊김|
|ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE|방 타입 변경 이벤트|
|ITMG_MAIN_EVENT_TYPE_MIC_NEW_DEVICE    |마이크 디바이스 신규 추가 메시지|
|ITMG_MAIN_EVENT_TYPE_MIC_LOST_DEVICE    |마이크 디바이스 로스 메시지|
|ITMG_MAIN_EVENT_TYPE_SPEAKER_NEW_DEVICE|디바이스 신규 추가 메시지|
|ITMG_MAIN_EVENT_TYPE_SPEAKER_LOST_DEVICE|스피커 디바이스 로스 메시지|
|ITMG_MAIN_EVENT_TYPE_ACCOMPANY_FINISH|반주 종료 메시지|
|ITMG_MAIN_EVNET_TYPE_USER_UPDATE|방 멤버 업데이트 메시지|
|ITMG_MAIN_EVNET_TYPE_PTT_RECORD_COMPLETE|PTT 녹음 완료|
|ITMG_MAIN_EVNET_TYPE_PTT_UPLOAD_COMPLETE|PTT 업로드 완료|
|ITMG_MAIN_EVNET_TYPE_PTT_DOWNLOAD_COMPLETE|PTT 다운로드 완료|
|ITMG_MAIN_EVNET_TYPE_PTT_PLAY_COMPLETE|PTT 플레이 완료|
|ITMG_MAIN_EVNET_TYPE_PTT_SPEECH2TEXT_COMPLETE|음성 텍스트 변환 완료|

### Data 리스트: 

|메시지     | Data         |예시|
| ------------- |:-------------:|------------- |
| ITMG_MAIN_EVENT_TYPE_ENTER_ROOM    |result; error_info|{"error_info":"","result":0}|
| ITMG_MAIN_EVENT_TYPE_EXIT_ROOM    |result; error_info  |{"error_info":"","result":0}|
| ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT    |result; error_info  |{"error_info":"waiting timeout, please check your network","result":0}|
| ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE    |result; error_info; sub_event_type; new_room_type|{"error_info":"","new_room_type":0,"result":0}|
| ITMG_MAIN_EVENT_TYPE_SPEAKER_NEW_DEVICE|result; error_info  |{"deviceID":"{0.0.0.00000000}.{a4f1e8be-49fa-43e2-b8cf-dd00542b47ae}","deviceName":"스피커 (Realtek High Definition Audio)","error_info":"","isNewDevice":true,"isUsedDevice":false,"result":0}|
| ITMG_MAIN_EVENT_TYPE_SPEAKER_LOST_DEVICE    |result; error_info  |{"deviceID":"{0.0.0.00000000}.{a4f1e8be-49fa-43e2-b8cf-dd00542b47ae}","deviceName":"스피커 (Realtek High Definition Audio)","error_info":"","isNewDevice":false,"isUsedDevice":false,"result":0}|
| ITMG_MAIN_EVENT_TYPE_MIC_NEW_DEVICE    |result; error_info  |{"deviceID":"{0.0.1.00000000}.{5fdf1a5b-f42d-4ab2-890a-7e454093f229}","deviceName":"마이크 (Realtek High Definition Audio)","error_info":"","isNewDevice":true,"isUsedDevice":true,"result":0}|
| ITMG_MAIN_EVENT_TYPE_MIC_LOST_DEVICE    |result; error_info |{"deviceID":"{0.0.1.00000000}.{5fdf1a5b-f42d-4ab2-890a-7e454093f229}","deviceName":"마이크 (Realtek High Definition Audio)","error_info":"","isNewDevice":false,"isUsedDevice":true,"result":0}|
| ITMG_MAIN_EVNET_TYPE_USER_UPDATE    |user_list;  event_id|{"event_id":1,"user_list":["0"]}|
| ITMG_MAIN_EVNET_TYPE_PTT_RECORD_COMPLETE |result; file_path  |{"file_path":"","result":0}|
| ITMG_MAIN_EVNET_TYPE_PTT_UPLOAD_COMPLETE |result; file_path;file_id  |{"file_id":"","file_path":"","result":0}|
| ITMG_MAIN_EVNET_TYPE_PTT_DOWNLOAD_COMPLETE|result; file_path;file_id  |{"file_id":"","file_path":"","result":0}|
| ITMG_MAIN_EVNET_TYPE_PTT_PLAY_COMPLETE |result; file_path  |{"file_path":"","result":0}|
| ITMG_MAIN_EVNET_TYPE_PTT_SPEECH2TEXT_COMPLETE|result; text;file_id|{"file_id":"","text":"","result":0}|
| ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_COMPLETE|result; file_path; text;file_id|{"file_id":"","file_path":","text":"","result":0}|
