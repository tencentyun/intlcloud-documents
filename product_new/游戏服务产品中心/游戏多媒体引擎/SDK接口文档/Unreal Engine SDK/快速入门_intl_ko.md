unreal 개발자가 Tencent Cloud Game Multimedia Engine(GME) 제품 API를 디버깅하고 액세스하는 편의성을 위해 unreal 개발 맞춤용 액세스 파일을 소개드립니다.


GME 액세스 파일은 가장 중요한 액세스 API만 제공합니다. API 관련 더 알아보려면 [관련 API 파일](https://intl.cloud.tencent.com/document/product/607/15210)을 참조하십시오.


|메인 API     | API 의미|
| ------------- |:-------------:|
|Init    |GME 초기화 |
|Poll    |트리거 이벤트 콜백|
|EnterRoom |방에 들어가기  |
|EnableMic |마이크 온 |
|EnableSpeaker|스피커 온 |

>
- GME를 사용하기 전에 프로그래밍을 설정해야 SDK가 적용됩니다.
- GME API를 호출하면 리턴값은 QAVError.OK이며, 값은 0입니다.
- GME API는 같은 스레드에서 호출해야 합니다.
- GME 방 가입 전에 인증해야 합니다. 파일중 인증 관련 내용을 참조하십시오.
- GME는 주기적으로 Poll API를 호출하여 트리거 이벤트를 콜백해야 합니다.
- GME 콜백 메시지는 콜백 메시지 리스트를 참조하십시오.
- 방에 들어간 후에 디바이스를 조작할 수 있습니다.
- 에러코드 상세내역은 [에러코드](https://intl.cloud.tencent.com/document/product/607/15173)를 참조하십시오


## 쾌속 액세스 프로세스
### 1. 싱글턴(singleton) 획득
음성 기능을 사용 시, 우선 ITMGContext 오브젝트를 읽어와야 합니다.

#### 예시 코드  

```
ITMGContext* context = ITMGContextGetInstance();
context->SetTMGDelegate(this);
```



### 2. SDK 초기화
파라미터를 읽어오려면 [액세스 매뉴얼](https://intl.cloud.tencent.com/document/product/607/10782)을 참조하십시오.
이 인터페이스는 Tencent Cloud 콘솔의 SDKAppID 계정을 파라미터로 적용 및 openId를 추가해야 합니다. 이 openId는 유저당 1개 적용하며, 앱 개발자가 스스로 룰을 정합니다. 앱내 반복할 수 없습니다(현재 INT 64만 지원합니다).
>SDK를 초기화해야 방에 들어갈 수 있습니다.
####  함수 프로토타입

```
ITMGContext virtual int Init(const char* sdkAppId, const char* openID)
```

|파라미터     | 타입         |의미|
| ------------- |:-------------:|-------------|
| sdkAppId    |char*   |Tencent Cloud 콘솔의  sdkAppId 계정|
| openID    |char*   |openID 오직 Int64타입(string으로 전환하여 입력)만 지원하며, 반드시 10,000보다 커야 합니다. 사용자 표기용|

####  예시 코드 


```
std::string appid = TCHAR_TO_UTF8(CurrentWidget->editAppID->GetText().ToString().operator*());
std::string userId = TCHAR_TO_UTF8(CurrentWidget->editUserID->GetText().ToString().operator*());
ITMGContextGetInstance()->Init(appid.c_str(), userId.c_str());
```
### 3. 트리거 이벤트 콜백
Tick에서 주기적으로 Poll를 호출하여 트리거 이벤트를 콜백합니다.
#### 함수 프로토타입

```
class ITMGContext {
protected:
    virtual ~ITMGContext() {}
    
public:    	
	virtual void Poll()= 0;
}
```
#### 예시 코드
```
//헤더파일 성명
virtual void Tick(float DeltaSeconds);

//코드 구현
void AUEDemoLevelScriptActor::Tick(float DeltaSeconds) 
{   
ITMGContextGetInstance()->Poll();
}
```


### 4. 인증 메시지
AuthBuffer를 생성하여 관련 기능을 암호화하고 인증합니다. 백그라운드 배포 관련 사항은 [인증 보안키](https://intl.cloud.tencent.com/document/product/607/12218)를 참조하십시오.  
오프라인 음성 메시지는 인증을 읽어올 때 방번호 파라미터는 반드시 null을 입력해야 합니다.
#### 함수 프로토타입
```
int  QAVSDK_AuthBuffer_GenAuthBuffer(unsigned int dwSdkAppID, const char* strRoomID, const char* strOpenID,
	const char* strKey, unsigned char* strAuthBuffer, unsigned int bufferLength);
```
|파라미터     | 타입         |의미|
| ------------- |:-------------:|-------------|
| dwSdkAppID    |int   |Tencent Cloud 콘솔의  sdkAppId 계정|
| strRoomID    |char*     |방번호, 최대 127개 캐릭터를 지원합니다(오프라인 음성 방번호는 반드시 null을 입력해야 합니다)|
| strOpenID  |char*     |사용자 표기|
| strKey    |char*    |Tencent Cloud [콘솔](https://console.cloud.tencent.com/gamegme)의 보안키|
|strAuthBuffer|char*    |리턴한 authbuff|
| bufferLength   |int    |입력한 authbuff 길이, 500으로 권장드립니다|



#### 예시 코드  
```
unsigned int bufferLen = 512;
unsigned char retAuthBuff[512] = {0};
QAVSDK_AuthBuffer_GenAuthBuffer(atoi(SDKAPPID3RD), roomId, "10001", AUTHKEY,retAuthBuff,bufferLen);
```


### 5. 방 가입
생성한 인증 메시지를 사용하여 방에 가입하면 ITMG_MAIN_EVENT_TYPE_ENTER_ROOM 콜백 메시지를 받습니다. 방에 가입시 기본적으로 마이크와 스피커를 끄며, 리턴값이 AV_OK일 경우 성공함을 의미합니다.
- 방 가입 시에 기본적으로 마이크와 스피커를 끕니다.
- EnterRoom API를 호출하기 전에 우선 Init API를 호출해야 합니다.

####  함수 프로토타입
```
ITMGContext virtual int EnterRoom(const char*  roomId, ITMG_ROOM_TYPE roomType, const char* authBuff, int buffLen)//일반적인 방 들어가기 API
```
|파라미터     | 타입         |의미|
| ------------- |:-------------:|-------------|
| roomId| char*    |방번호, 최대 127개 캐릭터를 지원합니다|
| roomType |ITMG_ROOM_TYPE|방 가청주파수 타입|
| authBuffer    |char*     |인증코드|
| buffLen   |int   |인증코드 길이|

방 가청주파수 타입은 음질 선택](https://intl.cloud.tencent.com/document/product/607/18522).을 참조하십시오


####  예시 코드  
```
ITMGContext* context = ITMGContextGetInstance();
context->EnterRoom(roomId, ITMG_ROOM_TYPE_STANDARD, (char*)retAuthBuff,bufferLen);
```

### 6. 방 가입 이벤트 콜백
방에 가입 시, ITMG_MAIN_EVENT_TYPE_ENTER_ROOM 메시지를 발송하며, OnEvent 함수에서 판단합니다.

####  예시 코드  
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

### 7. 마이크 온/오프
이 API는 마이크를 온/오프합니다. 방에 가입시 기본적으로 마이크와 스피커를 끕니다.

####  함수 프로토타입  
```
ITMGAudioCtrl virtual void EnableMic(bool bEnabled)
```
|파라미터     | 타입         |의미|
| ------------- |:-------------:|-------------|
| bEnabled    |bool     |마이크를 온하려면, 파라미터는 true로 입력되며, 마이크를 오프할 경우, 파라미터는 false입니다|

####  예시 코드  
```
ITMGContextGetInstance()->GetAudioCtrl()->EnableMic(true);
```


### 8. 스피커 온/오프
이 API는 스피커를 온/오프합니다.

####  함수 프로토타입  
```
ITMGAudioCtrl virtual void EnableSpeaker(bool enabled)
```
|파라미터     | 타입         |의미|
| ------------- |:-------------:|-------------|
| enable   |bool       |스피커를 오프하려면 파라미터는 false로 입력되며, 스피커를 온 할 경우, 파라미터는 true입니다|

####  예시 코드  
```
ITMGContextGetInstance()->GetAudioCtrl()->EnableSpeaker(true);
```



