Cocos2d 개발자가 Tencent Cloud Game Multimedia Engine(GME) 엔진 제품 API를 디버깅 및 액세스하는 편의성을 위해 Cocos2d 개발에 적용된 연동 기술 문서를 소개합니다.

>이 파일은 GME sdk version: 2.5 맞춤용입니다.

## GME 사용 주의사항

|중요 API     | API 의미|
| ------------- |:-------------:|
|Init    |GME 초기화 |
|Poll    |이벤트 콜백 트리거|
|EnterRoom |방 입장  |
|EnableMic |마이크 켜기 |
|EnableSpeaker|스피켜 켜기 |

>
- GME를 사용하기 전에 프로그램을 세팅하지 않으면 SDK가 효력을 발휘하지 않습니다.
- GME의 API 호출 성공 후 리턴값은 AV_OK이고 값은 0입니다.
- GME의 API는 같은 스레드에서 호출해야 합니다.
- GME의 방 입장은 인증이 필요하며, 가이드 중 인증 파트의 내용을 참조하십시오.
- GME는 주기적으로 Poll API를 호출하여 이벤트를 콜백해야 합니다.
- GME 콜백 정보는 콜백 메시지 목록을 참조합니다.
- 디바이스 조작은 방 입장 성공 후에 해야 합니다.
- 오류코드는 [오류코드](https://intl.cloud.tencent.com/document/product/607/15173)를 참조하십시오.

## 실시간 음성 채팅 프로세스
![](https://main.qcloudimg.com/raw/810d0404638c494d9d5514eb5037cd37.png)


## 초기화 관련 API
초기화하기 전에 SDK는 미초기화 단계로, API Init을 통해 SDK를 초기화해야 실시간 음성 및 오프라인 음성을 사용할 수 있습니다.
사용 문제는 [일반 문제](https://intl.cloud.tencent.com/document/product/607/30254)를 참조해주세요.

|API     | API 의미   |
| ------------- |:-------------:|
|Init    |GME 초기화|
|Poll    |이벤트 콜백 트리거|
|Pause   |시스템 일시 정지|
|Resume |시스템 복구|
|Uninit    |GME 초기화 취소 |


### 준비 과정
GME를 액세스하려면 우선 헤더 파일 tmg_sdk.h를 불러와야 하며, 헤더파일류는 ITMG Delegate를 계승하여 메세지를 전달, 콜백합니다.
####  예시 코드  

```
#include "tmg_sdk.h"

class TMGTestScene : public cocos2d::Scene,public ITMGDelegate
{
public:
...
private:
...
｝
```


### 단일항목 설정
EnterRoom 함수 호출에 앞서 ITMGContext를 획득해야 하며, 모든 호출은 ITMGContext에서 시작합니다. 전체 호출은 ITMGDelegate로부터 시작하며, 애플리케이션에 콜백하려면 먼저 설정해야 합니다.
####  예시 코드 
```
ITMGContext* context = ITMGContextGetInstance();
context->SetTMGDelegate(this);
```


### 메세지 전달
API류는 Delegate 메소드를 사용하여 애플리케이션에 리턴 알림을 보내는 데 사용되며, 메세지 유형은 ITMG_MAIN_EVENT_TYPE을 참조하고 data는 Windows 플랫폼의 json 문자열 형식을 참조합니다. 구체적인 key-value는 가이드 설명을 참조하십시오.

####  예시 코드  
```
//함수 구현:
//TMGTestScene.h:
class TMGTestScene : public cocos2d::Scene,public ITMGDelegate
{
public:
	void OnEvent(ITMG_MAIN_EVENT_TYPE eventType, const char* data);
｝

//TMGTestScene.cpp:
void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data){
	//여기에서 eventType에 대한 판단 및 조작
}
```

### SDK 초기화

파라미터 획득은 [액세스 매뉴얼](https://intl.cloud.tencent.com/document/product/607/10782)을 참조하십시오.
이 API는 Tencent Cloud 콘솔의 SDKAppID를 파라미터로 사용해야 하며, 여기에 openId를 추가하면 이 openId가 유일한 사용자 식별자가 되며, 규칙은 현재 App 개발자가 자체 작성하고 App 내에서 중복되지 않으면 됩니다.(현재는 INT64만 지원)
>SDK를 초기화한 후에야 방에 들어갈 수 있습니다.
#### 함수 프로토타입

```
ITMGContext virtual int Init(const char* sdkAppId, const char* openId)
```

|파라미터     | 유형         |의미|
| ------------- |:-------------:|-------------|
| sdkAppId    |char*   |Tencent Cloud 콘솔의 sdkAppId|
| openId    |char*   |openId는 Int64유형만 지원하며(char* 로 전환하여 입력), 10000보다 커야 하고 사용자 식별에 사용됨 |

####  예시 코드 


```
#define SDKAPPID3RD "1400089356"
cosnt char* openId="10001";
ITMGContext* context = ITMGContextGetInstance();
context->Init(SDKAPPID3RD, openId);
```
### 트리거 이벤트 콜백
update에서 주기적으로 Poll 호출을 통해 이벤트 콜백을 촉발할 수 있습니다.
#### 함수 프로토타입

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
//헤드 프로파일 상의 성명
class TMGTestScene : public cocos2d::Scene,public ITMGDelegate
{
void update(float delta); 
}

//코드 구현
void TMGTestScene::update(float delta)
{
    ITMGContextGetInstance()->Poll();
}
```

### 시스템 일시정지
시스템에 Pause 이벤트가 발생할 경우 엔진에 Pause 진행을 함께 알려야 합니다.
#### 함수 프로토타입

```
ITMGContext int Pause()
```

### 시스템 복구
시스템에서 Resume 이벤트가 발생할 경우 엔진에 동시에 Resume을 통지해야 합니다. Resume API는 실시간 음성만 복구합니다.
#### 함수 프로토타입

```
ITMGContext int Resume()
```



### SDK 초기화 취소
SDK 초기화를 취소하고, 초기화되지 않은 상태로 들어갑니다. 계정을 교체하려면 초기화 취소가 필요합니다.
#### 함수 프로토타입

```
ITMGContext int Uninit()
```
####  예시 코드
```
ITMGContext* context = ITMGContextGetInstance();
context->Uninit();
```

## 실시간 음성 채팅 관련 API
초기화 후, SDK 호출 후 방에 입장해야 실시간 음성통화가 가능합니다.
사용상 문제는 [실시간 음성 채팅 관련 문제](https://intl.cloud.tencent.com/document/product/607/30257)를 참조하십시오.

|API     | API 의미   |
| ------------- |:-------------:|
|GenAuthBuffer    |초기화 인증|
|EnterRoom   |방 입장|
|IsRoomEntered   |방에 입장했는지 여부|
|ExitRoom |방 퇴장|
|ChangeRoomType |사용자 방 오디오 유형 수정|
|GetRoomType |사용자 방 오디오 유형 획득|


### 인증 정보
AuthBuffer 를 생성합니다. 관련 기능의 암호화와 인증에 사용되며, 자세한 사항은 관련처의 [인증 보안키](https://intl.cloud.tencent.com/document/product/607/12218)를 참조하십시오.    
오프라인 음성 메시지 인증 획득 시, 방 번호 파라미터는 반드시 null을 입력하세요.

#### 함수 프로토타입
```
int  QAVSDK_AuthBuffer_GenAuthBuffer(unsigned int dwSdkAppID, const char* strRoomID, const char* strOpenID,
	const char* strKey, unsigned char* strAuthBuffer, unsigned int bufferLength);
```
|파라미터     | 유형         |의미|
| ------------- |:-------------:|-------------|
| dwSdkAppID    |int   |Tencent Cloud 콘솔의 sdkAppId 번호|
| strRoomID    |char*     |방 번호는 최대 127자까지 지원합니다（오프라인 음성 메시지 방 번호 파라미터는 반드시 null을 입력하세요）|
| strOpenID  |char*     |사용자 표식|
| strKey    |char*    |Tencent Cloud의 [콘솔](https://console.cloud.tencent.com/gamegme) 보안키|
|strAuthBuffer|char*    |리턴 authbuff|
| bufferLength   |int    |전입된 authbuff 길이, 500 권장|


####  예제 코드  
```
unsigned int bufferLen = 512;
unsigned char retAuthBuff[512] = {0};
QAVSDK_AuthBuffer_GenAuthBuffer(atoi(SDKAPPID3RD), roomId, "10001", AUTHKEY,retAuthBuff,bufferLen);
```



### 방 입장
생성된 인증 정보로 방에 들어가면 ITMG_MAIN_EVENT_TYPE_ENTER_ROOM의 콜백을 수신합니다. 방 입장 시 기본값으로 마이크 및 스피커가 닫힘 상태입니다. 리턴값 AV_OK일 때 성공을 의미합니다.
일반 음성으로 방 입장 시, 업무팀에서 범위 음성에 관한 수요가 없는 경우, 일반 방 입장 인터페이스를 사용하시면 됩니다. 자세한 정보는 [범위 음성](https://intl.cloud.tencent.com/document/product/607/17972)을 참조하십시오.

#### 함수 프로토타입
```
ITMGContext virtual int EnterRoom(const char*  roomID, ITMG_ROOM_TYPE roomType, const char* authBuff, int buffLen)
```
|파라미터     | 유형         |의미|
| ------------- |:-------------:|-------------|
| roomID| char*    |방 번호는 최대 127자까지 지원|
| roomType |ITMG_ROOM_TYPE|방 오디오 유형|
| authBuffer    |char*     |인증 코드|
| buffLen   |int   |인증 코드 길이|

방 오디오 유형과 관련하여 [음질 선택](https://intl.cloud.tencent.com/document/product/607/18522)을 참조하십시오.


####  예제 코드  
```
ITMGContext* context = ITMGContextGetInstance();
context->EnterRoom(roomID, ITMG_ROOM_TYPE_STANDARD, (char*)retAuthBuff,bufferLen);
```

### 방 입장 이벤트 콜백
방 입장 완료 후, 전송되는 메시지는 ITMG_MAIN_EVENT_TYPE_ENTER_ROOM으로, OnEvent 함수에서 판단합니다.

####  예제 코드  
```

void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data){
	switch (eventType) {
            case ITMG_MAIN_EVENT_TYPE_ENTER_ROOM:
		{
		//처리
		break;
		}
	}
}
```

#### 상세 Data
|메시지     | Data         |예제|
| ------------- |:-------------:|-------------|
| ITMG_MAIN_EVENT_TYPE_ENTER_ROOM    |result; error_info|{"error_info":"","result":0}|


### 방 입장 여부 판단
이 인터페이스를 호출하여 방 입장 여부 판단을 할 수 있습니다. 리턴값은 bool 유형입니다.
#### 함수 프로토타입  
```
ITMGContext virtual bool IsRoomEntered()
```
####  예제 코드  
```
ITMGContext* context = ITMGContextGetInstance();
context->IsRoomEntered();
```

### 방 나가기
이 인터페이스를 호출하여 방 나가기를 할 수 있습니다. 이는 비동기 인터페이스로 리턴값이 AV_OK일 때, 비동기 딜리버리의 성공을 나타냅니다.

>애플리케이션에서 체크 아웃 직후 체크 인이 실행되는 작업 환경이 있는 경우 개발자는 인터페이스 호출 프로세스에서 ExitRoom의 콜백 RoomExitComplete 알림을 기다릴 필요가 없습니다. 인터페이스를 직접 호출하면 됩니다.

#### 함수 프로토타입  
```
ITMGContext virtual int ExitRoom()
```
####  예제 코드  
```
ITMGContext* context = ITMGContextGetInstance();
context->ExitRoom();
```

### 방 나가기 콜백
방 나가기 완료 후 콜백이 있습니다. 메시지는  ITMG_MAIN_EVENT_TYPE_EXIT_ROOM입니다.
####  예제 코드  
```
void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data){
	switch (eventType) {
            case ITMG_MAIN_EVENT_TYPE_EXIT_ROOM:
		{
		//처리
		break;
		}
	}
}
```

#### 상세 Data
|메시지     | Data         |예제|
| ------------- |:-------------:|------------- |
| ITMG_MAIN_EVENT_TYPE_EXIT_ROOM    |result; error_info  |{"error_info":"","result":0}|


### 사용자 방 오디오 유형 수정
이 인터페이스는 사용자 방 오디오 유형을 수정하는 데 사용되며, 결과는 이벤트 콜백을 참조하세요. 이벤트 유형은 ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE입니다.
#### 함수 프로토타입  
```
IITMGContext TMGRoom public void ChangeRoomType((ITMG_ROOM_TYPE roomType)
```


|파라미터     | 유형        |의미|
| ------------- |:-------------:|-------------|
| roomType    |ITMG_ROOM_TYPE    |전환하고 싶은 방의 유형, 방 오디오 유형과 관련하여 EnterRoom 인터페이스 참고|

####  예제 코드  
```
ITMGContext* context = ITMGContextGetInstance();
ITMGContextGetInstance()->GetRoom()->ChangeRoomType(ITMG_ROOM_TYPE_FLUENCY);
```


### 사용자 방 오디오 유형 획득
이 인터페이스는 사용자 방의 오디오 유형을 얻는 데 사용되며, 리턴값이 방의 오디오 유형입니다. 리턴값 0은 사용자 방의 오디오 유형을 얻는 데 오류가 발생했음을 의미하며, 방의 오디오 유형은 EnterRoom 인터페이스를 참조합니다.

#### 함수 프로토타입  
```
IITMGContext TMGRoom public  int GetRoomType()
```

####  예제 코드  
```
ITMGContext* context = ITMGContextGetInstance();
ITMGContextGetInstance()->GetRoom()->GetRoomType();
```


### 방 유형 완료 콜백
방 유형 설정 완료 후의 콜백 메시지는 ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE로, 출력된 파라미터는 result, error_info 와 new_room_type입니다. new_room_type 이 의미하는 정보는 아래와 같으며, OnEvent 함수에서 이벤트 메시지를 판단합니다.

|하위 사건 유형     | 파라미터   |의미|
| ------------- |:-------------:|-------------|
| ITMG_ROOM_CHANGE_EVENT_ENTERROOM|1 |방에 들어가기 과정에서 자체 오디오 유형이 방과 일치하지 않음을 나타내는 것으로서, 들어가는 오디오 유형으로 자동 수정됨|
| ITMG_ROOM_CHANGE_EVENT_START|2|이미 방에 위치한 상황에서 오디오 유형은 전환 시작(예를 들어 ChangeRoomType 인터페이스를 호출한 후 오디오 유형을 전환 )|
| ITMG_ROOM_CHANGE_EVENT_COMPLETE|3|이미 방에 위치한 상황에서 오디오 유형의 전환이 완료됨|
| ITMG_ROOM_CHANGE_EVENT_REQUEST|4|방 멤버가 ChangeRoomType 인터페이스를 호출하여, 방 오디오 유형 전환을 요구한 경우|


####  예제 코드  
```
void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data) {
	if (ITMGContext.ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE == type)
        {
		//방 유형 이벤트 처리
	 }
}
```

#### 상세 Data
|메시지     | Data         |예제|
| ------------- |:-------------:|------------- |
| ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE    |result; error_info; new_room_type|{"error_info":"","new_room_type":0,"result":0}|


### 멤버 상태 변화
이 이벤트는 상태 변화가 있어야 알림이 있으며 상태가 변하지 않는 한 알림을 보내지 않습니다. 멤버 상태를 실시간으로 얻으려면 상위에서 알림을 받을 때 캐시하세요. 이벤트 메시지는 ITMG_MAIN_EVNET_TYPE_USER_UPDATE로, 그 중 data는 event_id 및 user_list, 두 가지 정보를 포함하고 있습니다. 본 이벤트 메시지는 OnEvent 함수에서 판단합니다.
오디오 사건 알림에는 임계 값이 하나 있으며, 이 임계 값을 초과해야 알림이 전송됩니다. 2초 이상 오디오 패킷을 받지 못한 후에야 "멤버가 오디오 패킷 전송을 중지했습니다."라는 메시지를 알립니다.

|event_id     | 의미         |애플리케이션 유지 콘텐츠|
| ------------- |:-------------:|-------------|
|ITMG_EVENT_ID_USER_ENTER    |임의 멤버 방 들어오기|애플리케이션 유지 멤버 리스트|
|ITMG_EVENT_ID_USER_EXIT    |임의 멤버 방 나가기|애플리케이션 유지 멤버 리스트|
|ITMG_EVENT_ID_USER_HAS_AUDIO    |어떤 멤버가 오디오 패킷 전송 시작|애플리케이션 유지 통화 멤버 리스트|
|ITMG_EVENT_ID_USER_NO_AUDIO    |어떤 멤버가 오디오 패킷 전송 중지|애플리케이션 유지 통화 멤버 리스트|

####  예제 코드  

```
void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data){
	switch (eventType) {
            case ITMG_MAIN_EVNET_TYPE_USER_UPDATE:
		{
		//처리
		//개발자가 파라미터를 해석하여 eventID 와 user_list 정보를 획득하였습니다
		    switch (eventID)
 		    {
 		    case ITMG_EVENT_ID_USER_ENTER:
  			    //어떤 멤버의 방에 들어왔습니다
  			    break;
 		    case ITMG_EVENT_ID_USER_EXIT:
  			    //어떤 멤버가 방을 나갔습니다
			    break;
		    case ITMG_EVENT_ID_USER_HAS_AUDIO:
			    //어떤 멤버가 오디오 패킷 전송을 시작했습니다
			    break;
		    case ITMG_EVENT_ID_USER_NO_AUDIO:
			    //어떤 멤버가 오디오 패킷 전송을 중지했습니다
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
품질 모니터링 이벤트의 이벤트 메시지는 ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_QUALITY로, 출력 파라미터는 weight, floss  와 delay입니다. 의미하는 정보는 아래와 같으며, OnEvent 함수에서 이벤트 메시지를 판단합니다.

|파라미터     | 의미         |
| ------------- |-------------|
|weight    |범위는 1-5이고, 5는 음질 평점 매우 좋음, 1은 음질 평점이 매우 나쁨으로 거의 사용할 수 없음, 0은 초기값을 의미하지 않으며, 의미가 없습니다|
|floss    |패킷 손실율|
|delay    |오디오 도달 딜레이 시간（ms）|




### 상세 메시지

|메시지     | 메시지 의미   |
| ------------- |:-------------:|
|ITMG_MAIN_EVENT_TYPE_ENTER_ROOM           |오디오/비디오 방 입장 메시지|
|ITMG_MAIN_EVENT_TYPE_EXIT_ROOM             |오디오/비디오 방 나가기 메시지|
|ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT           |네트워크 등 문제로 방 내 메시지 끊김|
|ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE|방 유형 변화 이벤트|

### 메시지에 대응하는 상세 Data

|메시지     | Data         |예제|
| ------------- |:-------------:|------------- |
| ITMG_MAIN_EVENT_TYPE_ENTER_ROOM    |result; error_info|{"error_info":"","result":0}|
 ITMG_MAIN_EVENT_TYPE_EXIT_ROOM    |result; error_info  |{"error_info":"","result":0}|
| ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT    |result; error_info  |{"error_info":"waiting timeout, please check your network","result":0}|
| ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE    |result; error_info; new_room_type|{"error_info":"","new_room_type":0,"result":0}|


## 실시간 음성 메시지 오디오 인터페이스
SDK를 초기화한 후 방에 들어가야 실시간 오디오 채팅 관련 인터페이스를 호출할 수 있습니다.
사용자 인터페이스에서 마이크/스피커 온/오프 버튼을 클릭할 때 다음과 같은 방식이 권장됩니다:
- 대부분의 게임류 App에 EnableMic 및 EnableSpeaker 인터페이스를 권장하는 것은 EnableAudioCaptureDevice/EnableAudioSend 와 EnableAudioPlayDevice/EnableAudioRecv 를 함께 사용해야 한다는 의미입니다.
- 다른 유형의 모바일 App의 경우, 예를 들어 소셜 유형 App의 경우, 수집 디바이스를 켜거나 끄면 전체 장비(수집 및 재생)가 재시작되며, 이때 App에서 배경음악을 재생하고 있다면 배경음악의 재생도 중단됩니다. 업/다운스트리밍을 제어하는 방식으로 마이크 스위치를 작동하며 재생 디바이스가 중단되지 않습니다. 구체적인 호출 방법은: 방에 들어갈 때 EnableAudioCaptureDevice(true) && EnableAudioPlayDevice(true)를 한 번 호출하고, 마이크 스위치를 클릭할 때 EnableAudioSend/Recv 를 호출하여 오디오 스트리밍의 전송/수신을 제어합니다.
- 단독으로 수집 혹은 재생 디바이스를 릴리즈 하시려면, EnableAudioCaptureDevice 및 EnableAudioPlayDevice 인터페이스를 참고하십시오.
- pause 를 호출하여 오디오 엔진 일시중지, resume 를 호출하여 오디오 엔진 복구.



|인터페이스     | 인터페이스 의미   |
| ------------- |:-------------:|
|GetMicListCount           |마이크 디바이스 갯수 획득|
|GetMicList          |마이크 디바이스 세기|
|GetSpeakerListCount          |스피커 디바이스 갯수 획득|
|GetSpeakerList          |스피커 디바이스 세기|
|SelectMic          |마이크 디바이스 선정|
|SelectSpeaker    |스피커 디바이스 선정|
|EnableMic    |마이크 온/오프|
|GetMicState    |마이크 상태 획득|
|EnableAudioCaptureDevice    |수집 디바이스 온/오프|
|IsAudioCaptureDeviceEnabled    |수집 디바이스 상태 획득|
|EnableAudioSend    |오디오 업스트림 열기/닫기|
|IsAudioSendEnabled    |오디오 업스트림 상태 획득|
|GetMicLevel    |실시간 마이크 사운드 획득|
|GetSendStreamLevel|오디오 업스트림 실시간 사운드 획득|
|SetMicVolume    |마이크 사운드 설정|
|GetMicVolume    |마이크 사운드 획득|
|EnableSpeaker    |스피커 온/오프|
|GetSpeakerState    |스피커 상태 획득|
|EnableAudioPlayDevice    |재생 디바이스 온/오프|
|IsAudioPlayDeviceEnabled    |재생 디바이스 상태 획득|
|EnableAudioRecv    |오디오 다운스트림 열기/닫기|
|IsAudioRecvEnabled    |오디오 다운스트림 상태 획득|
|GetSpeakerLevel    |실시간 스피커 사운드 획득|
|GetRecvStreamLevel|방 내 다른 멤버 다운스트림 실시간 사운드 획득|
|SetSpeakerVolume    |스피커 사운드 설정|
|GetSpeakerVolume    |스피커 사운드 획득|
|EnableLoopBack    |인이어 모니터링 온/오프|



### 마이크 디바이스 갯수 획득
이 인터페이스는 마이크 디바이스 갯수 획득에 사용됩니다.
#### 함수 프로토타입  
```
ITMGAudioCtrl virtual int GetMicListCount()
```
####  예제 코드  
```
ITMGContextGetInstance()->GetAudioCtrl()->GetMicListCount();
```

### 마이크 디바이스 세기
이 인터페이스는 마이크 디바이스 세기에 사용됩니다. GetMicListCount 인터페이스와 함께 사용하십시오.

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
| ppDeviceInfoList    |TMGAudioDeviceInfo   |디바이스 리스트|
| nCount    |int     |마이크 디바이스 갯수 획득|

####  예제 코드  

```
ITMGContextGetInstance()->GetAudioCtrl()->GetMicList(ppDeviceInfoList,nCount);
```



### 마이크 디바이스 선정
이 인터페이스는 마이크 디바이스 선정에 사용됩니다. 디버깅하거나 "DEVICEID_DEFAULT"이 수신될 경우 시스템이 기본 디바이스를 선택합니다. 디바이스 ID는 GetMicList 리턴 리스트에서 가져옵니다.

#### 함수 프로토타입  

```
ITMGAudioCtrl virtual int SelectMic(const char* pMicID)
```

|파라미터     | 유형         |의미|
| ------------- |:-------------:|-------------|
| pMicID    |char*      |마이크 디바이스 ID|

####  예제 코드  

```
const char* pMicID ="{0.0.1.00000000}.{7b0b712d-3b46-4f7a-bb83-bf9be4047f0d}";
ITMGContextGetInstance()->GetAudioCtrl()->SelectMic(pMicID);
```

### 마이크 켜기/끄기
이 인터페이스는 마이크 켜기/끄기 에 사용됩니다. 방 입장 시 마이크 및 스피커는 끄기 상태가 기본값입니다.
EnableMic = EnableAudioCaptureDevice + EnableAudioSend.
#### 함수 프로토타입  
```
ITMGAudioCtrl virtual int EnableMic(bool bEnabled)
```
|파라미터     | 유형         |의미|
| ------------- |:-------------:|-------------|
| bEnabled    |bool     |마이크를 켜야 하는 상황이면, 파라미터가 true 이고, 만약 마이크를 꺼야 하는 상황이면, 파라미터가 false 입니다|

####  예제 코드  
```
ITMGContextGetInstance()->GetAudioCtrl()->EnableMic(true);
```

### 마이크 상태 획득
이 인터페이스는 마이크 상태 획득에 사용됩니다. 리턴값 0은 마이크 꺼짐 상태를 의미하며, 1은 켜짐 상태를 의미합니다.
#### 함수 프로토타입  
```
ITMGAudioCtrl virtual int GetMicState()
```
####  예제 코드  
```
ITMGContextGetInstance()->GetAudioCtrl()->GetMicState();
```

### 수집 디바이스 켜기/끄기
이 인터페이스는 수집 디바이스 켜기/끄기 에 사용됩니다. 방 입장 시 디바이스 꺼짐 상태가 기본값입니다.
- 방 들어가기 후에만 이 인터페이스 호출이 가능합니다. 방 나가기 직후 자동으로 디바이스가 꺼집니다.
- 모바일에서, 수집 디바이스를 켜는 경우, 인증 신청, 오디오 유형 조정 등 작업이 요구될 수 있습니다. 

#### 함수 프로토타입  
```
ITMGContext virtual int EnableAudioCaptureDevice(bool enable)
```

|파라미터    | 유형         |의미|
| ------------- |:-------------:|-------------|
| enable    |bool     |수집 디바이스를 켜야 할 경우, 전입된 파라미터는 true이고, 수집 파라미터를 끄면 false 입니다|

####  예제 코드

```
수집 디바이스 열기
ITMGContextGetInstance()->GetAudioCtrl()->EnableAudioCaptureDevice(true);
```

### 수집 디바이스 상태 획득
이 인터페이스는 수집 디바이스 상태 획득에 사용됩니다.
#### 함수 프로토타입

```
ITMGContext virtual bool IsAudioCaptureDeviceEnabled()
```
####  예제 코드

```
ITMGContextGetInstance()->GetAudioCtrl()->IsAudioCaptureDeviceEnabled();
```

### 오디오 업스트림 열기/닫기
이 인터페이스는 오디오 업스트림 열기/닫기 에 사용됩니다. 수집 디바이스가 이미 열려 있다면 수집한 음성 데이터를 보낼 수 있습니다. 수집 디바이스가 켜져 있지 않으면 소리가 나지 않습니다. 수집 디바이스의 열기/닫기 는 인터페이스 EnableAudioCaptureDevice를 참조합니다.

#### 함수 프로토타입

```
ITMGContext  virtual int EnableAudioSend(bool bEnable)
```
|파라미터   | 유형         |의미|
| ------------- |:-------------:|-------------|
| enable    |bool     |오디오 업스트림을 켜야 하는 경우, 전입된 파라미터는 true이고, 오디오 업스티림을 끄면 false 입니다|

####  예제 코드  

```
ITMGContextGetInstance()->GetAudioCtrl()->EnableAudioSend(true);
```

### 오디오 업스트림 상태 획득
이 인터페이스는 오디오 업스트림 상태 획득에 사용됩니다.
#### 함수 프로토타입  
```
ITMGContext virtual bool IsAudioSendEnabled()
```
####  예제 코드  
```
ITMGContextGetInstance()->GetAudioCtrl()->IsAudioSendEnabled();
```

### 마이크 실시간 사운드 획득
이 인터페이스는 마이크 실시간 사운드 획득에 사용되며, 리턴값은 int 유형입니다.
#### 함수 프로토타입  
```
ITMGAudioCtrl virtual int GetMicLevel()
```
####  예제 코드  
```
ITMGContextGetInstance()->GetAudioCtrl()->GetMicLevel();
```

### 오디오 업스트림 실시간 사운드 획득
이 인터페이스는 오디오 업스트림 실시간 사운드 획득에 사용됩니다. 리턴값은 int 유형이며, 값 범위는 0부터 100까지입니다.
#### 함수 프로토타입  
```
ITMGAudioCtrl virtual int GetSendStreamLevel()
```
####  예제 코드  
```
ITMGContextGetInstance()->GetAudioCtrl()->GetSendStreamLevel();
```

### 마이크 사운드 설정
이 인터페이스는 마이크 사운드 설정에 사용됩니다. 파라미터 volume 은 마이크의 사운드를 설정하는데 사용되며 수치가 0일 때 무음을, 수치가 100일 때 볼륨이 더이상 증가하지 않음을 나타냅니다. 기본값은 100입니다.

#### 함수 프로토타입  
```
ITMGAudioCtrl virtual int SetMicVolume(int vol)
```
|파라미터     | 유형         |의미|
| ------------- |:-------------:|-------------|
| vol    |int      |사운드 설정, 범위값 0 부터 200|

####  예제 코드  
```
ITMGContextGetInstance()->GetAudioCtrl()->SetMicVolume(vol);
```
### 마이크 사운드 획득
이 인터페이스는 마이크 사운드 획득에 사용됩니다. 리턴값은 int 유형으로 리턴값 101은 SetMicVolume 인터페이스를 호출한 적 없음을 의미합니다.

#### 함수 프로토타입  
```
ITMGAudioCtrl virtual int GetMicVolume()
```
####  예제 코드  
```
ITMGContextGetInstance()->GetAudioCtrl()->GetMicVolume();
```

### 스피커 디바이스 갯수 획득
이 인터페이스는 스피커 디바이스 갯수 획득에 사용됩니다.

#### 함수 프로토타입  

```
ITMGAudioCtrl virtual int GetSpeakerListCount()
```
####  예제 코드  

```
ITMGContextGetInstance()->GetAudioCtrl()->GetSpeakerListCount();
```

### 스피커 디바이스 세기
이 인터페이스는 스피커 디바이스 세기에 사용됩니다. GetSpeakerListCount 인터페이스와 함께 사용하세요.

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
| ppDeviceInfoList    |TMGAudioDeviceInfo    |디바이스 리스트|
| nCount   |int     |획득한 스피커 디바이스 갯수|

####  예제 코드  
```
ITMGContextGetInstance()->GetAudioCtrl()->GetSpeakerList(ppDeviceInfoList,nCount);
```

### 스피커 디바이스 선정
이 인터페이스는 재생 디바이스를 선택하는 데 사용됩니다. 디버깅하거나 “DEVICEID_DEFAULT”가 전입될 경우, 시스템이 기본 재생 디바이스를 선택합니다. 디바이스 ID는 GetSpeakerList 리턴 리스트에서 가져옵니다.

#### 함수 프로토타입  
```
ITMGAudioCtrl virtual int SelectSpeaker(const char* pSpeakerID)
```

|파라미터     | 유형         |의미|
| ------------- |:-------------:|-------------|
| pSpeakerID    |char*      |스피커 디바이스 ID|

####  예제 코드  
```
const char* pSpeakerID ="{0.0.1.00000000}.{7b0b712d-3b46-4f7a-bb83-bf9be4047f0d}";
ITMGContextGetInstance()->GetAudioCtrl()->SelectSpeaker(pSpeakerID);
```

### 스피커 켜기/끄기
이 인터페이스는 스피커 켜기/끄기 에 사용됩니다.
EnableSpeaker = EnableAudioPlayDevice +  EnableAudioRecv.
#### 함수 프로토타입  
```
ITMGAudioCtrl virtual int EnableSpeaker(bool enabled)
```
|파라미터     | 유형         |의미|
| ------------- |:-------------:|-------------|
| enable   |bool       |스피커를 꺼야 할 경우 전입된 파라미터는 false이고 스피커를 켜면 true입니다|

####  예제 코드  
```
ITMGContextGetInstance()->GetAudioCtrl()->EnableSpeaker(true);
```

### 스피커 상태 획득
이 인터페이스는 스피커 상태 획득에 사용됩니다. 리턴값 0은 스피커 상태를 끄기, 1은 스피커 상태를 켜기, 리턴값 2는 스피커 디바이스가 현재 작업 중임을 의미합니다.
#### 함수 프로토타입  
```
ITMGAudioCtrl virtual int GetSpeakerState()
```

####  예제 코드  
```
ITMGContextGetInstance()->GetAudioCtrl()->GetSpeakerState();
```



### 재생 디바이스 열기/닫기
이 인터페이스는 재생 디바이스 열기/닫기 에 사용됩니다.

#### 함수 프로토타입  
```
ITMGContext virtual int EnableAudioPlayDevice(bool enable) 
```
|파라미터     | 유형         |의미|
| ------------- |:-------------:|-------------|
| enable    |bool        |재생 디바이스를 닫기 해야 하는 경우, 전입 파라미터는 false이고, 재생 디바이스를 열기 하면 true입니다|

####  예제 코드  
```
ITMGContextGetInstance()->GetAudioCtrl()->EnableAudioPlayDevice(true);
```

### 재생 디바이스 상태 획득
이 인터페이스는 재생 디바이스 상태 획득에 사용됩니다.
#### 함수 프로토타입

```
ITMGContext virtual bool IsAudioPlayDeviceEnabled()
```
####  예제 코드  

```
ITMGContextGetInstance()->GetAudioCtrl()->IsAudioPlayDeviceEnabled();
```

### 오디오 다운스트림 열기/닫기
이 인터페이스는 오디오 다운스트림 열기/닫기 에 사용됩니다. 재생 디바이스가 이미 열려 있다면 방에 있는 다른 사람의 오디오 데이터를 재생합니다. 재생 디바이스가 켜져 있지 않으면 소리가 나지 않습니다. 재생 디바이스의 열기/닫기 는 인터페이스 EnableAudioPlayDevice를 참조하십시오.

#### 함수 프로토타입  

```
ITMGContext virtual int EnableAudioRecv(bool enable)
```
|파라미터     | 유형         |의미|
| ------------- |:-------------:|-------------|
| enable    |bool     |오디오 다운스트림이 열기 해야 할 경우 전입된 파라미터는 true이며, 오디오 다운스트림을 닫기 하는 경우 false 입니다|

####  예제 코드  

```
ITMGContextGetInstance()->GetAudioCtrl()->EnableAudioRecv(true);
```



### 오디오 다운스트림 상태 획득
이 인터페이스는 오디오 다온스트림 상태 획득에 사용됩니다.
#### 함수 프로토타입  
```
ITMGContext virtual bool IsAudioRecvEnabled() 
```

####  예제 코드  
```
ITMGContextGetInstance()->GetAudioCtrl()->IsAudioRecvEnabled();
```

### 스피커 실시간 사운드 획득
이 인터페이스는 스피커 실시간 사운드 획득에 사용됩니다. 리턴값은 int 유형이며 스피커 실시간 사운드를 의미합니다.
#### 함수 프로토타입  
```
ITMGAudioCtrl virtual int GetSpeakerLevel()
```

####  예제 코드  
```
ITMGContextGetInstance()->GetAudioCtrl()->GetSpeakerLevel();
```

### 방 내 다른 멤버 다운스트림 실시간 사운드 획득
이 인터페이스는 방 내 다른 멤버 다운스트림 실시간 사운드 획득에 사용됩니다. 리턴값은 int 유형이며, 값 범위는 0부터 100까지입니다.
#### 함수 프로토타입  
```
ITMGAudioCtrl virtual int GetRecvStreamLevel(const char* openId)
```

|파라미터     | 유형         |의미|
| ------------- |:-------------:|-------------|
| openId    |char*       |방 다른 멤버의 openId|


####  예제 코드  
```
iter->second.level = ITMGContextGetInstance()->GetAudioCtrl()->GetRecvStreamLevel(iter->second.openid.c_str());
```

### 스피커 사운드 설정
이 인터페이스는 스피커 사운드 설정에 사용됩니다.
파라미터 volume 은 스피커 사운드를 설정하는데 사용되며, 0일 때 무음을, 100일 때 볼륨이 더이상 증가하지 않음을 나타냅니다. 기본값은 100입니다.

#### 함수 프로토타입  
```
ITMGAudioCtrl virtual int SetSpeakerVolume(int vol)
```
|파라미터     | 유형         |의미|
| ------------- |:-------------:|-------------|
| vol    |int        |사운드 설정, 값 범위 0 부터 200|

####  예제 코드  
```
int vol = 100;
ITMGContextGetInstance()->GetAudioCtrl()->SetSpeakerVolume(vol);
```

### 스피커 사운드 획득

이 인터페이스는 스피커 사운드 획득에 사용됩니다. 리턴값은 int 유형이며, 스피커의 사운드를 의미합니다. 리턴값 101은 SetSpeakerVolume 인터페이스를 호출한 적 없음을 의미합니다.
Level은 실시간 사운드, Volume은 스피커 사운드를 의미하며, 최종 사운드 볼륨은 Level*Volume%에 해당합니다. 예를 들어: 실시간 사운드 수치가 100, Volume의 수치가 60일 경우, 결과적으로 발생하는 소리의 수치는 60이 됩니다.

#### 함수 프로토타입  
```
ITMGAudioCtrl virtual int GetSpeakerVolume()
```
####  예제 코드  
```
ITMGContextGetInstance()->GetAudioCtrl()->GetSpeakerVolume();
```


### 인이어 모니터링 시작
이 인터페이스는 인이어 모니터링 시작에 사용됩니다.
#### 함수 프로토타입  
```
ITMGAudioCtrl virtual int EnableLoopBack(bool enable)
```
|파라미터     | 유형         |의미|
| ------------- |:-------------:|-------------|
| enable    |bool         |설정의 운행 여부|

####  예제 코드  
```
ITMGContextGetInstance()->GetAudioCtrl()->EnableLoopBack(true);
```


## 오프라인 음성 메시지 음성 문자 간 변환 순서도
![](https://main.qcloudimg.com/raw/9ef5e5e4ebc8e63bcd7bfbea6cfb94cc.png)



## 오프라인 음성 메시지
초기화하기 전에 SDK 미초기화 단계로 인터페이스 Init를 통해 SDK를 초기화해야 실시간 음성 및 오프라인 음성 메시지를 사용할 수 있습니다.
궁금한 사항은 [오프라인 음성 메시지 관련 문제](https://intl.cloud.tencent.com/document/product/607/30258)를 참조하십시오.

### 초기화 관련 인터페이스

|인터페이스     | 인터페이스 의미   |
| ------------- |:-------------:|
|Init    |GME 초기화|
|Poll    |트리거 이벤트 콜백|
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
|StopRecording    |녹음 중지|
|CancelRecording|녹음 취소|
|GetMicLevel|오프라인 음성 메시지 실시간 마이크 사운드 획득|
|SetMicVolume|오프라인 음성 메시지 녹화 사운드 설정|
|GetMicVolume|오프라인 음성 메시지 녹화 사운드 획득|
|GetSpeakerLevel|오프라인 음성 메시지 실시간 스피커 사운드 획득  |
|SetSpeakerVolume|오프라인 음성 메시지 재생 사운드 설정|
|GetSpeakerVolume|오프라인 음성 메시지 재생 사운드 획득|
|UploadRecordedFile |음성 파일 업로드|
|DownloadRecordedFile|음성 파일 다운로드|
|PlayRecordedFile |음성 파일 재생|
|StopPlayFile|음성 파일 재생 중지|
|GetFileSize |음성 파일 크기|
|GetVoiceFileDuration|음성 파일 길이|
|SpeechToText |음성을 문자로 인식|

### 인증 초기화
SDK를 초기화한 후에 인증 초기화를 호출합니다. authBuffer 획득은 윗글의 실시간 음성 메시지 인증 정보 인터페이스를 참조하십시오.
#### 함수 프로토타입  
```
ITMGPTT virtual int ApplyPTTAuthbuffer(const char* authBuffer, int authBufferLen)
```
|파라미터     | 유형         |의미|
| ------------- |:-------------:|-------------|
| authBuffer    |char*                    |인증|
| authBufferLen    |int                |인증 길이|

####  예제 코드  
```
ITMGContextGetInstance()->GetPTT()->ApplyPTTAuthbuffer(authBuffer,authBufferLen);
```

### 음성 메시지 최대 길이 제한
음성 메시지의 최대 길이를 60초로 제한합니다.

#### 함수 프로토타입

```
ITMGPTT virtual int SetMaxMessageLength(int msTime)
```
|파라미터     | 유형         |의미|
| ------------- |:-------------:|-------------|
| msTime    |int                    |음성 메시지 길이, 단위 ms|

#### 예제 코드  
```
int msTime = 10;
ITMGContextGetInstance()->GetPTT()->SetMaxMessageLength(msTime);
```


### 녹음 시작
이 인터페이스는 녹음 시작에 사용됩니다. 녹음 파일의 업로드 완료 후에만 음성 문자 간 변환 등 작업을 가능합니다.
#### 함수 프로토타입  
```
ITMGPTT virtual int StartRecording(const char* fileDir)
```
|파라미터     | 유형         |의미|
| ------------- |:-------------:|-------------|
| fileDir    |char*                      |보관된 파일 경로|

####  예제 코드  
```
ITMGContextGetInstance()->GetPTT()->StartRecording(fileDir);
```

### 녹음 시작 콜백
녹음 시작 완료 후의 콜백 메시지는 OnEvent 함수를 호출하여 확인합니다. 이벤트 메시지는 ITMG_MAIN_EVNET_TYPE_PTT_RECORD_COMPLETE로, OnEvent 함수에서 판단합니다.
수신된 파라미터에는 result 와 file_path, 이 두 가지 정보를 포함하고 있습니다.

#### 에러 코드
|에러 코드 |원인  |권장 방안        |
|-----|------|------|
|4097   |파라미터 비어있음|코드 중 인터페이스 파라미터가 올바른지 점검하세요|
|4098   |초기화 오류|디바이스가 점용되었는지, 권한이 올바른지, 초기화가 정상인지를 점검하세요|
|4099   |현재 녹화 중|SDK 녹화 기능이 올바른 타이밍에 사용되고 있는지 확인하세요|
|4100   |오디오 데이터 수집 안됨|마이크 디바이스가 정상인지 점검하세요|
|4101   |녹음 시, 파일 액세스 실패|파일이 존재하는지, 파일 경로가 합법적인지 확인하세요|
|4102   |마이크 권한 미부여 오류|SDK 를 사용하기 위해선 마이크 권한이 필요합니다. 권한 추가와 관련하여 관련 엔진 혹은 플랫폼의 SDK 공정 배치 문서를 참조하십시오|
|4103   |녹음 시간이 너무 짧음으로 인한 오류|우선, 녹음 시간 단위를 ms로 제한하고 있습니다. 파라미터가 올바른지 확인하십시오; 그리고 녹음 시간은 1000ms 이상이어야 녹음 성공으로 간주합니다|
|4104   |녹음 시작 작업 불가|녹음 시작 인터페이스가 이미 호출된 것은 아닌지 점검하세요|

####  예제 코드  
```
void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data){
	switch (eventType) {
		case ITMG_MAIN_EVENT_TYPE_ENTER_ROOM:
		{
		//처리
		break;
	    }
		...
        case ITMG_MAIN_EVNET_TYPE_PTT_RECORD_COMPLETE:
		{
		//처리
		break;
		}
	}
}
```

### 스트리밍 음성 인식 작동
이 인터페이스는 스트리밍 음성 인식을 작동시키는 데 사용되며, 동시에 콜백 중에 실시간 음성 문자 간 변환을 출력할 수 있습니다. 또한 언어를 지정하여 인식할 수 있으며 음성에서 인식된 정보를 지정된 언어로 번역하여 출력할 수 있습니다.

#### 함수 프로토타입  

```
ITMGPTT virtual int StartRecordingWithStreamingRecognition(const char* filePath) 
ITMGPTT virtual int StartRecordingWithStreamingRecognition(const char* filePath,const char* translateLanguage,const char* translateLanguage) 
```
|파라미터    | 유형         |의미|
| ------------- |:-------------:|-------------|
| filePath    |char*|보관된 파일 경로|
| speechLanguage    |char*                     |지정 문자로 인식된 언어 파라미터와 관련하여 [음성 문자 간 변환 언어 파라미터 참고 리스트](https://intl.cloud.tencent.com/document/product/607/30260)를 참조하십시오|
| translateLanguage    |char*                     |지정 문자로 번역된 언어 파라미터와 관련하여 [음성 문자 간 변환 언어 파라미터 참고 리스트](https://intl.cloud.tencent.com/document/product/607/30260)를 참조하십시오（이 파라미터는 일시적으로 사용이 불가합니다. speechLanguage 와 동일한 파라미터를 입력하십시오)|

####  예제 코드  
```
ITMGContextGetInstance()->GetPTT()->StartRecordingWithStreamingRecognition(filePath,"cmn-Hans-CN","cmn-Hans-CN");
```

### 스트리밍 음성 인식 작동 콜백
스트리밍 음성 인식이 완료된 후의 콜백은 함수 OnEvent를 호출할 수 있습니다. 이벤트 메시지는 ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_COMPLETE로, OnEvent 함수에서 판단합니다. 전달된 파라미터에는 다음과 같은 네 가지 정보가 포함되어 있습니다.

|메시지 명칭     | 의미         |
| ------------- |:-------------:|
| result    |스트리밍 음성 인식이 성공적으로 리턴 코드를 보냈는지 판단|
| text    |음성 문자 간 변환 인식 텍스트|
| file_path |녹음 파일이 보관된 로컬 주소|
| file_id |녹음의 백그라운드 url 주소|

#### 에러 코드

|에러 코드     | 의미         |처리 방법|
| ------------- |:-------------:|:-------------:|
|32775|스트리밍 음성 문자 간 변환에 실패하였으나, 녹음에는 성공함|UploadRecordedFile 인터페이스를 호출하여 녹음 파일을 업로드 한 뒤, SpeechToText 인터페이스를 호출하여 음성 문자 간 변환 작업을 진행하세요
|32777|스트리밍 음성 문자 간 변환에 실패하였으나, 녹음과 업로드는 성공함|리턴 정보 중 업로드 성공의 백그라운드 url 주소로 SpeechToText 인터페이스 호출하여 음성 문자 간 변환 작업을 진행하세요
|32786  |스트리밍 음성 문자 간 변환 실패|스트리밍 녹화 상태에서, 스트리밍 녹화 인터페이스 실행 결과가 출력될 때까지 기다리십시오|

####  예제 코드  
```
void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data){
	switch (eventType) {
		case ITMG_MAIN_EVENT_TYPE_ENTER_ROOM:
		{
		//처리
		break;
	    }
		...
        case ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_COMPLETE:
		{
		//처리
		break;
		}
	}
}
```

### 녹음 일시정지
이 인터페이스는 녹음 일시정지에 사용됩니다. 녹음을 복구하려면 ResumeRecording 인터페이스를 호출하세요.

#### 함수 프로토타입  
```
ITMGPTT virtual int PauseRecording()
```
####  예제 코드  
```
ITMGContextGetInstance()->GetPTT()->PauseRecording();
```

### 녹음 복구
이 인터페이스는 녹음 복구에 사용됩니다.

#### 함수 프로토타입  
```
ITMGPTT virtual int ResumeRecording()
```
####  예제 코드  
```
ITMGContextGetInstance()->GetPTT()->ResumeRecording();
```

### 녹음 중지
이 인터페이스는 녹음 중지에 사용됩니다. 이 인터페이스는 비동기 인터페이스로 녹음 중지 후 녹음 완료 콜백이 있으며, 작업이 성공한 뒤에야 녹음 파일 사용이 가능합니다.
#### 함수 프로토타입  
```
ITMGPTT virtual int StopRecording()
```
####  예제 코드  
```
ITMGContextGetInstance()->GetPTT()->StopRecording();
```



### 녹음 취소
이 인터페이스를 호출하여 녹음을 취소합니다. 취소한 뒤에는 콜백이 없습니다.
#### 함수 프로토타입  
```
ITMGPTT virtual int CancelRecording()
```
####  예제 코드  
```
ITMGContextGetInstance()->GetPTT()->CancelRecording();
```

### 오프라인 음성 메시지 마이크 실시간 사운드 획득
이 인터페이스는 오프라인 음성 메시지 마이크 실시간 사운드 획득에 사용됩니다. 리턴값은 int 유형으로 값 범위는 0부터 100까지입니다.

#### 함수 프로토타입  
```
ITMGPTT virtual int GetMicLevel()
```
####  예제 코드  
```
ITMGContextGetInstance()->GetPTT()->GetMicLevel();
```

### 오프라인 음성 메시지 녹화 사운드 설정
이 인터페이스는 오프라인 음성 메시지 녹화 사운드 설정에 사용되며, 값 범위는 0부터 100까지입니다.

#### 함수 프로토타입  
```
ITMGPTT virtual int SetMicVolume(int vol)
```
####  예제 코드  
```
ITMGContextGetInstance()->GetPTT()->SetMicVolume(100);
```

### 오프라인 음성 메시지 녹화 사운드 획득
이 인터페이스는 오프라인 음성 메시지 녹화 사운드 획득에 사용됩니다. 리턴값은 int 유형이며, 값 범위는 0부터 100까지입니다.

#### 함수 프로토타입  
```
ITMGPTT virtual int GetMicVolume()
```

####  예제 코드  
```
ITMGContextGetInstance()->GetPTT()->GetMicVolume();
```


### 스피커 실시간 사운드 획득
이 인터페이스는 스피커 실시간 사운드 획득에 사용됩니다. 리턴값은 int 유형이며, 값 범위는 0부터 100까지입니다.

#### 함수 프로토타입  
```
ITMGPTT virtual int GetSpeakerLevel()
```

####  예제 코드  
```
ITMGContextGetInstance()->GetPTT()->GetSpeakerLevel();
```

### 오프라인 음성 메시지 재생 사운드 설정
이 인터페이스는 오프라인 음성 메시지 재생 사운드 설정에 사용되며, 값 범위는 0부터 100까지입니다.

#### 함수 프로토타입  
```
ITMGPTT virtual int SetSpeakerVolume(int vol)
```
####  예제 코드  
```
ITMGContextGetInstance()->GetPTT()->SetSpeakerVolume(100);
```

### 오프라인 음성 메시지 재생 사운드 획득
이 인터페이스는 오프라인 음성 메시지 재생 사운드 획득에 사용됩니다. 리턴값은 int 유형이며, 값 범위는 0부터 100까지입니다.

#### 함수 프로토타입  
```
ITMGPTT virtual int GetSpeakerVolume()
```

####  예제 코드  
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
| filePath    |char*                       |업로드 파일 경로|

####  예제 코드  
```
ITMGContextGetInstance()->GetPTT()->UploadRecordedFile(filePath);
```


### 음성 파일 업로드 완료 콜백
음성 파일 업로드 완료 후, 이벤트 메시지는 ITMG_MAIN_EVNET_TYPE_PTT_UPLOAD_COMPLETE로, OnEvent 함수에서 이벤트 메시지를 판단합니다.
수신된 파라미터에는 result, file_path 와 file_id, 이 세가지 정보가 포함되어 있습니다.

#### 에러 코드

|에러 코드 |원인  |권장 방안        |
|-----|------|------|
|8193   |파일 업로드 시, 파일 액세스 오류|파일이 존재하는지, 파일 경로가 합법적인지 확인하세요|
|8194   |서명 교정 실패 오류|인증 보안키가 올바른지 오프라인 음성 메시지 초기화가 있는지 점검하세요|
|8195   |네트워크 오류|디바이스 네트워크가 외부 네트워크 환경에 정상적으로 방문할 수 있는지 점검하세요|
|8196   |업로드된 파라미터 획득 과정에서 네트워크 오류|인증이 정확한지, 디바이스 네트워크가 외부 네트워크 환경에 정상적으로 방문할 수 있는지 점검하세요|
|8197   |업로드된 파라미터 획득 과정에서 롤백 데이터 비어있음|인증이 정확한지, 디바이스 네트워크가 외부 네트워크 환경에 정상적으로 방문할 수 있는지 점검하세요|
|8198   |업로드된 파라미터 획득 과정에서 롤백 압축해제 오류|인증이 정확한지, 디바이스 네트워크가 외부 네트워크 환경에 정상적으로 방문할 수 있는지 점검하세요|
|8200   |appinfo 설정 안됨|apply 인터페이스가 호출되었는지, 인풋 파라미터가 비어있지 않은지 점검하세요|

####  예제 코드

```
void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data){
	switch (eventType) {
		case ITMG_MAIN_EVENT_TYPE_ENTER_ROOM:
		{
		//처리
		break;
	    }
		...
        case ITMG_MAIN_EVNET_TYPE_PTT_UPLOAD_COMPLETE:
		{
		//처리
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
| fileId  |char*   |파일 url 경로|
| filePath |char*  |파일 로컬 저장 경로|

####  예제 코드  
```
ITMGContextGetInstance()->GetPTT()->DownloadRecordedFile(fileID,filePath);
```


### 음성 파일 다운로드 완료 콜백
음성 파일 다운로드 완료 후의 이벤트 메시지는 ITMG_MAIN_EVNET_TYPE_PTT_DOWNLOAD_COMPLETE로, OnEvent 함수에서 이벤트 메시지를 판단합니다. 

#### 에러 코드

|에러 코드 |원인  |권장 방안        |
|-----|------|------|
|12289  |파일 다운로드 시, 파일 액세스 오류    |파일 경로가 합법적인지 점검하세요|
|12290  |서명 교정 실패    |인증 보안키가 올바른지, 초기화 오프라인 음성 메시지가 있는지 점검하세요|
|12291  |네트워크 스토리지 시스템 이상    |서버에서 음성 파일 획득에 실패했습니다. 인터페이스 파라미터 fileid 가 올바른지, 네트워크가 정상인지, cos 파일이 존재하는지 점검하세요|
|12292  |서버 파일 시스템 오류    |디바이스 네트워크가 외부 네트워크 환경에 정상적으로 방문할 수 있는지. 서버에 이 파일이 있는지 점검하세요|
|12293  |다운로드된 파라미터 획득 과정에서 HTTP 네트워크 오류|디바이스 네트워크가 외부 네트워크 환경에 정상적으로 방문할 수 있는지 점검하세요|
|12294  |다운로드된 파라미터 획득 과정에서 롤백 데이터 비어있음 |디바이스 네트워크가 외부 네트워크 환경에 정상적으로 방문할 수 있는지 점검하세요|
|12295  |다운로드된 파라미터 획득 과정에서 롤백 데이터 압축해제 실패|디바이스 네트워크가 외부 네트워크 환경에 정상적으로 방문할 수 있는지 점검하세요|
|12297  |appinfo 설정 안됨|인증 보안키가 올바른지, 초기화 오프라인 음성 메시지가 있는지 점검하세요|


####  예제 코드

```
void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data){
	switch (eventType) {
		case ITMG_MAIN_EVENT_TYPE_ENTER_ROOM:
		{
		//처리
		break;
	    }
		...
        case ITMG_MAIN_EVNET_TYPE_PTT_DOWNLOAD_COMPLETE:
		{
		//처리
		break;
		}
	}
}
```



### 음성 파일 재생
이 인터페이스는 음성 파일 재생에 사용됩니다.
#### 함수 프로토타입  
```
ITMGPTT virtual int PlayRecordedFile(const char* filePath)
```
|파라미터     | 유형         |의미|
| ------------- |:-------------:|-------------|
| filePath    |char*                       |파일 경로|

#### 에러 코드

|에러 코드 |원인  |권장 방안        |
|-----|------|------|
|20485  |재생 시작 안됨|파일이 존재하는지, 파일 경로가 합법적인지 확인하세요|

####  예제 코드  
```
ITMGContextGetInstance()->GetPTT()->PlayRecordedFile(filePath);
```


### 음성 파일 재생 콜백
음성 파일 재생 콜백의 이벤트 메시지는 ITMG_MAIN_EVNET_TYPE_PTT_PLAY_COMPLETE로, OnEvent 함수에서 이벤트 메시지에 대해 판단합니다.
수신된 파라미터에는  result 와 file_path, 이 두 가지 정보가 포함되어 있습니다.

#### 에러 코드

|에러 코드 |원인  |권장 방안        |
|-----|------|------|
|20481  |초기화 오류|디바이스가 점용되었는지, 권한이 정상인지, 초기화가 정상인지를 점검하세요|
|20482  |현재 재생 중인 상황에서, 중도 중단하고 다음 재생을 시도하였으나 실패함(정상적으로는 중도 중단이 가능함)|코드 중 로직이 올바른지 점검하세요|
|20483  |파라미터 비어있음|코드 중 인터페이스 파라미터가 올바른지 점검하세요|
|20484  |내부 오류|초기화 재생 장치에 오류가 발생했습니다. 암호 해독 실패 등의 이유로 이 에러코드가 발생하므로 로그 설정을 해결해야 합니다|

####  예제 코드

```
void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data){
	switch (eventType) {
		case ITMG_MAIN_EVENT_TYPE_ENTER_ROOM:
		{
		//처리
		break;
	    }
		...
        case ITMG_MAIN_EVNET_TYPE_PTT_PLAY_COMPLETE:
		{
		//처리
		break;
		}
	}
}
```




### 음성 재생 중지
이 인터페이스는 음성 재생 중지에 사용됩니다. 음성 재생 중지하여도 재생 완료 콜백이 있습니다.
#### 함수 프로토타입  
```
ITMGPTT virtual int StopPlayFile()
```

####  예제 코드  
```
ITMGContextGetInstance()->GetPTT()->StopPlayFile();
```



### 음성 파일 크기 획득
이 인터페이스를 통해 음성 파일 크기 획득을 할 수 있습니다.
#### 함수 프로토타입  
```
ITMGPTT virtual int GetFileSize(const char* filePath)
```
|파라미터     | 유형         |의미|
| ------------- |:-------------:|-------------|
| filePath    |char*                      |음성 파일 경로|

####  예제 코드  
```
ITMGContextGetInstance()->GetPTT()->GetFileSize(filePath);
```

### 음성 파일 길이 획득
이 인터페이스는 음성 파일 길이 획득에 사용되며, 단위는 ms입니다.
#### 함수 프로토타입  
```
ITMGPTT virtual int GetVoiceFileDuration(const char* filePath)
```
|파라미터     | 유형         |의미|
| ------------- |:-------------:|-------------|
| filePath    |char*                      |음성 파일 경로|

####  예제 코드  
```
ITMGContextGetInstance()->GetPTT()->GetVoiceFileDuration(filePath);
```


### 지정한 음성 파일을 텍스트로 식별
이 인터페이스는 지정한 음성 파일을 텍스트로 식별하는데 사용됩니다.

#### 함수 프로토타입  
```
ITMGPTT virtual void SpeechToText(const char* fileID)
```
|파라미터     | 유형         |의미|
| ------------- |:-------------:|-------------|
| fileID    |char*                      |음성 파일 url|

####  예제 코드  
```
ITMGContextGetInstance()->GetPTT()->SpeechToText(fileID);
```



### 지정한 음성 파일을 텍스트로 번역(지정 언어)
이 인터페이스는 지정 언어로 식별이 가능합니다. 또한 음성 속 인식한 정보를 지정 언어로 번역하여 출력할 수 있습니다.

#### 함수 프로토타입  
```
ITMGPTT virtual int SpeechToText(const char* fileID,const char* speechLanguage,const char* translateLanguage)
```
|파라미터     | 유형         |의미|
| ------------- |:-------------:|-------------|
| fileID    |char*                     |음성 파일 url|
| speechLanguage    |char*                     |지정 문자로 식별한 언어 파라미터와 관련하여 [음성 문자 간 변환된 언어 파라미터 참고 리스트](https://intl.cloud.tencent.com/document/product/607/30260)를 참조하십시오|
| translatelanguage    |char*                  |지정 문자로 번역한 언어 파라미터와 관련하여 [음성 문자 간 변환된 언어 파라미터 참고 리스트](https://intl.cloud.tencent.com/document/product/607/30260)를 참조하십시오（이 파라미터는 일시적으로 유효하지 않음으로 speechLanguage 와 일치하는 파라미터로 작성하십시오）|

####  예제 코드  
```
ITMGContextGetInstance()->GetPTT()->SpeechToText(filePath,"cmn-Hans-CN","cmn-Hans-CN");
```



### 인식 콜백
지정한 음성 파일을 텍스트로 인식한 콜백의 이벤트 메시지는 ITMG_MAIN_EVNET_TYPE_PTT_SPEECH2TEXT_COMPLETE로, OnEvent 함수에서 이벤트 메시지에 대해 판단합니다.
수신한 파라미터는 result, file_path 와 text, 이 세 가지 정보가 포함되어 있으며, 그 중 text 가 인식된 텍스트입니다.

#### 에러 코드

|에러코드 |원인  |권장 방안        |
|-----|------|------|
|32769  |내부 오류|로그를 분석한 뒤, 백그라운드에서 클라이언트에게 리턴한 진정한 오류 코드를 얻고, 백그라운드 동료에게 연락하여 해결을 돕습니다.|
|32770  |네트워크 오류|디바이스 네트워크가 외부 네트워크 환경에 정상적으로 방문할 수 있는지 점검합니다|
|32772  |롤백 압축해제 실패|로그를 분석한 뒤, 백그라운드에서 클라이언트에게 리턴한 진정한 오류 코드를 얻고, 백그라운드 동료에게 연락하여 해결을 돕습니다.|
|32774  |appinfo 설정 안됨|인증 보안키가 올바른지, 초기화 오프라인 음성 메시지가 있는지 점검합니다|
|32776  |authbuffer 교정 실패|authbuffer 가 올바른지 점검합니다|
|32784  |음성 문자 간 변환 파라미터 오류|코드 중 인터페이스 파라미터 fileid 가 비어있는지 점검합니다|
|32785  |음성 문자 간 변환 번역 출력 오류|오프라인 음성 메시지 백그라운드 오류로, 로그를 분석한 뒤, 백그라운드에서 클라이언트에게 리턴한 진정한 오류 코드를 얻고, 백그라운드 동료에게 연락하여 해결을 돕습니다|

####  예제 코드

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

## 진단 정보 획득
오디오/비디오 통화의 실시간 통화 품질에 대한 정보를 가져옵니다. 이 인터페이스는 주로 실시간 통화 품질, 배찰 문제 등을 조회하는데 사용되며 업무팀에서는 무시해도 무관합니다.
#### 함수 프로토타입
```
ITMGRoom virtual const char* GetQualityTips()
```
####  예제 코드  
```
ITMGContextGetInstance()->GetRoom()->GetQualityTips();
```


### 버전 번호 획득
#### 함수 프로토타입

```
ITMGContext virtual const char* GetSDKVersion()
```



####  예제 코드  

```
ITMGContextGetInstance()->GetSDKVersion();
```




### 로그 레벨 인쇄 설정
로그 레벨 인쇄 설정에 사용됩니다. 기본값 유지를 권장합니다.
#### 함수 프로토타입
```
ITMGContext int SetLogLevel(ITMG_LOG_LEVEL levelWrite, ITMG_LOG_LEVEL levelPrint)
```

#### 파라미터 내용

|파라미터|유형|내용|
|---|---|---|
|levelWrite|ITMG_LOG_LEVEL|입력 로그 레벨을 설정하십시오. TMG_LOG_LEVEL_NONE은 사용하지 않음을 의미합니다. |
|levelPrint|ITMG_LOG_LEVEL|인쇄 로그 레벨을 설정하십시오. TMG_LOG_LEVEL_NONE은 인쇄하지 않음을 의미합니다.|



|ITMG_LOG_LEVEL|내용|
| -------------------------------|----------------------|
|TMG_LOG_LEVEL_NONE=0|로그를 인쇄하지 않습니다.|
|TMG_LOG_LEVEL_ERROR=1|로그 인쇄 에러코드(기본값)|
|TMG_LOG_LEVEL_INFO=2|로그 표시 인쇄|
|TMG_LOG_LEVEL_DEBUG=3|개발 디버깅 로그 인쇄|
|TMG_LOG_LEVEL_VERBOSE=4|고빈도 로그 인쇄|

####  예제 코드  
```
ITMGContext* context = ITMGContextGetInstance();
context->SetLogLevel(TMG_LOG_LEVEL_INFO,TMG_LOG_LEVEL_INFO);
```



### 로그 경로 인쇄 설정
로그 경로 인쇄 설정에 사용됩니다.
기본 경로는:

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

|파라미터     | 유형         |의미|
| ------------- |:-------------:|-------------|
| logDir    |char*    |경로|

####  예제 코드  

```
cosnt char* logDir = ""//자체 설정 경로

ITMGContext* context = ITMGContextGetInstance();
context->SetLogPath(logDir);
```

## 오디오 데이터 블랙리스트 추가
임의 ID를 오디오 데이터 블랙리스트에 추가합니다. 리턴값 0은 호출 성공을 의미합니다.
#### 함수 프로토타입  

```
ITMGContext ITMGAudioCtrl int AddAudioBlackList(const char* openId)
```
|파라미터     | 유형         |의미|
| ------------- |:-------------:|-------------|
| openId    |char*       |블랙리스트에 추가할 ID|

####  예제 코드  

```
ITMGContextGetInstance()->GetAudioCtrl()->AddAudioBlackList(openId);
```

### 오디오 데이터 블랙리스트에서 제거
임의 ID를 오디오 데이터 블랙리스트에서 제거합니다. 리턴값 0은 호출 성공을 의미합니다.
#### 함수 프로토타입  

```
ITMGContext ITMGAudioCtrl int RemoveAudioBlackList(const char* openId)
```
|파라미터     | 유형         |의미|
| ------------- |:-------------:|-------------|
| openId    |char*       |블랙리스트에서 제거할 ID|

####  예제 코드  

```
ITMGContextGetInstance()->GetAudioCtrl()->RemoveAudioBlackList(openId);
```


## 콜백 메시지

### 메시지 리스트:

|메시지     | 메시지 의미   |
| ------------- |:-------------:|
|ITMG_MAIN_EVENT_TYPE_ENTER_ROOM    |오디오 방 들어가기 메시지|
|ITMG_MAIN_EVENT_TYPE_EXIT_ROOM    |오디오 방 나가기 메시지|
|ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT|네트워크 문제로 방 내 메시지 끊김|
|ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE|방 유형 변화 이벤트|
|ITMG_MAIN_EVENT_TYPE_MIC_NEW_DEVICE    |마이크 디바이스 신규 추가 메시지|
|ITMG_MAIN_EVENT_TYPE_MIC_LOST_DEVICE    |마이크 디바이스 누락 메시지|
|ITMG_MAIN_EVENT_TYPE_SPEAKER_NEW_DEVICE|스피커 디바이스 신규 추가 메시지|
|ITMG_MAIN_EVENT_TYPE_SPEAKER_LOST_DEVICE|스피커 디바이스 누락 메시지|
|ITMG_MAIN_EVENT_TYPE_ACCOMPANY_FINISH|반주 종료 메시지|
|ITMG_MAIN_EVNET_TYPE_USER_UPDATE|방 멤버 업데이트 메시지|
|ITMG_MAIN_EVNET_TYPE_PTT_RECORD_COMPLETE|PTT 녹음 완료|
|ITMG_MAIN_EVNET_TYPE_PTT_UPLOAD_COMPLETE|PTT 업로드 완료|
|ITMG_MAIN_EVNET_TYPE_PTT_DOWNLOAD_COMPLETE|PTT 다운로드 완료|
|ITMG_MAIN_EVNET_TYPE_PTT_PLAY_COMPLETE|PTT 재생 완료|
|ITMG_MAIN_EVNET_TYPE_PTT_SPEECH2TEXT_COMPLETE|음성 문자 간 변환 완료|

### Data 리스트:

|메세지     | Data         |예시|
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
