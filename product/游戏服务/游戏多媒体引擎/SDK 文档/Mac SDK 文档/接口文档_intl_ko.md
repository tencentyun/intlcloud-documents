Mac 개발자가 Tencent Cloud GME API를 디버깅하고 연결하는 데 도움이 되도록 여기에 Mac 개발에 적합한 액세스 기술 문서를 소개합니다.

>?이 문서에 해당하는 GME SDK 버전은 2.4입니다.

## 사용 프로세스도
### 음성 채팅 프로세스도
![](https://main.qcloudimg.com/raw/bf2993148e4783caf331e6ffd5cec661.png)

### 오프라인 음성의 문자로 전환 프로세스도
![](https://main.qcloudimg.com/raw/4c875d05cd2b4eaefba676d2e4fc031d.png)

### GME 사용 중요사항

|중요 API     | API 의미|
| ------------- |:-------------:|
|InitEngine    				       	|GME 초기화 	|
|Poll    		|이벤트 콜백 트리거	|
|EnterRoom	 	|방 입장  		|
|EnableMic	 	|마이크 켜기 	|
|EnableSpeaker		|스피커 켜기 	|

>**설명: **
- GME의 API 호출이 성공한 후 반환 값은 QAVError.OK이고 수치는 0입니다.
- GME의 API는 같은 스레드에서 호출되어야 합니다.
- GME가 방을 가입하려면 인증이 필요합니다. 인증 관련 내용을 참조하십시오.
- GME는 Poll API를 주기적으로 호출하여 이벤트 콜백을 트리거해야 합니다.
- GME 콜백 메시지는 콜백 메시지 리스트를 참조하십시오.
- 방에 입장한 후에 장치에 대한 조작을 실행할 수 있습니다.

## 초기화 관련 API
초기화 전에 SDK는 미초기화 단계에 속하고 있습니다. 초기화 인증 후 SDK를 초기화해야 방에 입장할 수 있습니다.

|API     | API 의미   |
| ------------- |:-------------:|
|InitEngine    				       	|GME 초기화 	|
|Poll    	|이벤트 콜백 트리거	|
|Pause   	|시스템 일시 중지	|
|Resume 	|시스템 다시 시작	|
|Uninit    	|GME 반초기화 	|

### 싱글 인스턴스 획득
음성 기능 사용 시 먼저 ITMGContext 개체를 획득해야 합니다.
#### 함수 프로토타입

```
ITMGContext ITMGDelegate <NSObject>
```
#### 샘플 코드  

```
ITMGContext* _context = [ITMGContext GetInstance];
_context.TMGDelegate =self;
```

### 메시지 전송
Delegate 방법을 채택한 API는 응용프로그램에 콜백 알림을 발송하는 데 사용됩니다. 메시지 유형은 ITMG_MAIN_EVENT_TYPE를 참조하며, 메시지 내용은 사전 한 개입니다. 이벤트 유형에 따라 메시지 내용도 달라집니다.
#### 함수 프로토타입

```
- (void)OnEvent:(ITMG_MAIN_EVENT_TYPE)eventType data:(NSDictionary*)data
```
#### 샘플 코드

```
-(void)OnEvent:(ITMG_MAIN_EVENT_TYPE)eventType data:(NSDictionary *)data{
    	NSLog(@"OnEvent:%lu,data:%@",(unsigned long)eventType,data);
		switch (eventType) {
			//EventType에 대해 판단
			}
	}
```


### SDK 초기화
매개변수 획득에 대한 정보는 [액세스 가이드](https://cloud.tencent.com/document/product/607/10782)를 참조하십시오.
해당 API는 Tencent Cloud 콘솔의 SdkAppId 번호를 매개변수로 사용하고 여기에 openId를 더해야 합니다. 해당 openId는 하나의 사용자를 유일하게 식별하는 것으로 규칙은 App 개발자가 자체적으로 제정하고 App 내에서 중복되지 않으면 됩니다(현재는 INT64만을 지원합니다).
SDK 초기화 후에만 방에 들어갈 수 있습니다.
#### 함수 프로토타입

```
ITMGContext -(void)InitEngine:(NSString*)sdkAppID openID:(NSString*)openID
```

|매개변수     | 유형         |의미|
| ------------- |:-------------:|-------------|
| sdkAppId    	|NSString  |Tencent Cloud 콘솔의 sdkAppID 번호				|
| OpenID    		|NSString  |OpenID는 Int64 유형(string으로 전환 후 가져오기)만 지원하고 반드시 10000보다 크며 사용자 ID 식별에 사용합니다. |

#### 샘플 코드  

```
[[ITMGContext GetInstance] InitEngine:SDKAPPID3RD openID:_openId];
```


### 이벤트 콜백 트리거
update에서의 주기적인 Poll 호출을 통해 이벤트 콜백을 트리거할 수 있습니다.
#### 함수 프로토타입

```
ITMGContext -(void)Poll
```
#### 샘플 코드
```
[[ITMGContext GetInstance] Poll];
```



### 시스템 일시 중지
시스템에 일시 중지가 발생하는 동시에 엔진에 Pause 진행을 알려야 합니다.
#### 함수 프로토타입

```
ITMGContext -(QAVResult)Pause
```

### 시스템 복원
시스템 이벤트가 다시 시작되면 엔진에도 동시에 Resume 진행을 알려야 합니다.
#### 함수 프로토타입

```
ITMGContext -(QAVResult)Resume
```


### SDK 반초기화
SDK 반초기화, 미초기화 상태에 들어갑니다. 계정을 변경할 경우 반초기화를 진행해야 합니다.
#### 함수 프로토타입

```
ITMGContext -(void)Uninit
```
#### 샘플 코드
```
[[ITMGContext GetInstance] Uninit];
```


## 음성 채팅 방 관련 API
초기화 후, SDK로 방 입장을 호출하여 방에 입장해야만 음성 채팅 통화를 진행할 수 있습니다.

|API     | API 의미   |
| ------------- |:-------------:|
|GenAuthBuffer    	|인증 초기화|
|EnterRoom   		|방 가입|
|IsRoomEntered   	|방 입장 여부|
|ExitRoom 			|방 퇴장|
|ChangeRoomType 	|사용자 방 오디오 유형 수정|
|GetRoomType 		|사용자 방 오디오 유형 획득|



### 인증 정보
AuthBuffer를 생성하고 관련 기능의 암호화와 인증에 사용됩니다. 백 엔드 배포에 대한 세부 정보는 [인증 키](https://cloud.tencent.com/document/product/607/12218)를 참조하십시오. 오프라인 음성이 인증을 획득할 때, 방 번호 매개변수는 null을 입력해야 합니다.
해당 API 반환 값은 NSData 유형입니다.
#### 함수 프로토타입

```
@interface QAVAuthBuffer : NSObject
+ (NSData*) GenAuthBuffer:(unsigned int)appId roomId:(NSString*)roomId openID:(NSString*)openID key:(NSString*)key;
+ @end
```

|매개변수     | 유형         |의미|
| ------------- |:-------------:|-------------|
| appId    		|int   		|Tencent Cloud 콘솔의 sdkAppID 번호		|
| roomId    		|NSString  	|방 번호, 최대 127자 지원(오프라인 음성 방 번호 매개변수를 null을 입력해야 함)	|
| openID  		|NSString    	|사용자 ID								|
| key    			|NSString    	|Tencent Cloud [콘솔](https://console.cloud.tencent.com/gamegme)의 키					|



#### 샘플 코드  

```
NSData* authBuffer =   [QAVAuthBuffer GenAuthBuffer:SDKAPPID3RD.intValue roomId:_roomId openID:_openId key:AUTHKEY];
```

### 방 입장
생성한 인증 정보를 사용해 방에 입장하면 ITMG_MAIN_EVENT_TYPE_ENTER_ROOM이라는 콜백을 받게 됩니다. 방 가입 시 기본적으로 마이크 및 스피커를 켜지 않습니다. 반환 값은 AV_OK라면 성공했음을 의미합니다.


#### 함수 프로토타입

```
ITMGContext   -(int)EnterRoom:(NSString*) roomId roomType:(int*)roomType authBuffer:(NSData*)authBuffer
```
|매개변수     | 유형         |의미|
| ------------- |:-------------:|-------------|
| RoomID 	|NSString		|방 번호, 최대 127자 지원|
| roomType 		|int			|방 오디오 유형		|
| authBuffer    	|NSData    	|인증 번호						|

방 오디오 유형은 [음질 선택](https://cloud.tencent.com/document/product/607/18522)을 참조하십시오.

#### 샘플 코드  

```
[[ITMGContext GetInstance] EnterRoom:_roomId roomType:_roomType authBuffer:authBuffer];
```

### 방 가입 이벤트의 콜백
방 가입 완료 후 메시지 ITMG_MAIN_EVENT_TYPE_ENTER_ROOM을 발송하고, OnEvent 함수에서 판단합니다.
#### 샘플 코드

```
-(void)OnEvent:(ITMG_MAIN_EVENT_TYPE)eventType data:(NSDictionary *)data{
    NSLog(@"OnEvent:%lu,data:%@",(unsigned long)eventType,data);
    switch (eventType) {
        case ITMG_MAIN_EVENT_TYPE_ENTER_ROOM:
        {
            int result = ((NSNumber*)[data objectForKey:@"result"]).intValue;
            NSString* error_info = [data objectForKey:@"error_info"];
            //방 입장 성공 이벤트 수신
        }
            break;
     }
}
```

### 방 입장 여부 판단
해당 API를 호출하여 방 입장 여부를 판단할 수 있으며 반환 값은 BOOL 유형입니다.
#### 함수 프로토타입  

```
ITMGContext -(BOOL)IsRoomEntered
```
#### 샘플 코드  

```
[[ITMGContext GetInstance] IsRoomEntered];
```

### 방 퇴장
해당 API를 호출하여 방에서 퇴장할 수 있습니다. 이것은 비동기 API이며 반환 값은 AV_OK라면 비동기 전달이 성공했음을 의미합니다.

> 만약 응용프로그램 중 방 퇴장 후 즉시 입장하는 상황이 발생할 경우 API 호출 과정에서 개발자는 ExitRoom의 콜백 RoomExitComplete 알림을 기다릴 필요가 없으며 바로 API를 호출하면 됩니다.

#### 함수 프로토타입  

```
ITMGContext -(int)ExitRoom
```
#### 샘플 코드

```
[[ITMGContext GetInstance] ExitRoom];
```

### 방 퇴장 콜백
방 퇴장 완료 후 콜백이 있으며 메시지는 ITMG_MAIN_EVENT_TYPE_EXIT_ROOM입니다.

#### 샘플 코드  

```
-(void)OnEvent:(ITMG_MAIN_EVENT_TYPE)eventType data:(NSDictionary *)data{
    NSLog(@"OnEvent:%lu,data:%@",(unsigned long)eventType,data);
    switch (eventType) {
        case ITMG_MAIN_EVENT_TYPE_EXIT_ROOM：
        {
    //방 퇴장 성공 이벤트 수신
        }
            break;
    }
}
```



### 사용자 방 오디오 유형 수정
이 API는 사용자 방 오디오 유형을 수정하는 데 사용됩니다. 그 결과는 콜백 이벤트를 참조하십시오. 이벤트 유형은 ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE입니다.

#### 함수 프로토타입  
```
ITMGContext GetRoom -(void)ChangeRoomType:(int)nRoomType
```
|매개변수     | 유형         |의미|
| ------------- |:-------------:|-------------|
| nRoomType    |int    |전환하려는 방 유형, 방 오디오 유형은 EnterRoom API를 참조하십시오.|

#### 샘플 코드

```
[[[ITMGContext GetInstance]GetRoom ]ChangeRoomType:_roomType];
```

### 사용자 방 오디오 유형 획득
이 API는 사용자 방 오디오 유형을 획득하는 데 사용되며, 반환 값은 방 오디오 유형입니다. 반환 값이 0이면 사용자 방 오디오 유형에 오류가 발생하였음을 의미합니다. 방 오디오 유형은 EnterRoom API를 참조하십시오.

#### 함수 프로토타입  
```
ITMGContext GetRoom -(int)GetRoomType
```


#### 샘플 코드

```
[[[ITMGContext GetInstance]GetRoom ]GetRoomType];
```

### 방 유형을 설정한 후 콜백
방 유형 설정 완료 후 콜백 이벤트 메시지는 ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE이며, 반환한 매개변수는 result, error_info 및 new_room_type이고, new_room_type가 의미하는 정보는 다음과 같습니다. OnEvent 함수에서 이벤트 메시지에 대해 판단합니다.

|이벤트 서브 유형     | 매개변수 표시 값   |의미|
| ------------- |:-------------:|-------------|
| ITMG_ROOM_CHANGE_EVENT_ENTERROOM		|1 	|방 입장 과정에서 자체 보유한 오디오 유형이 방과 부합하지 않아 입장한 방의 오디오 유형으로 수정되었음을 의미합니다.	|
| ITMG_ROOM_CHANGE_EVENT_START			|2	|이미 방 안에 있고 오디오 유형 전환이 시작되었음을 의미합니다(예를 들어, ChangeRoomType API 호출 후 오디오 유형 전환).|
| ITMG_ROOM_CHANGE_EVENT_COMPLETE		|3	|이미 방 안에 있고 오디오 유형 전환이 완료되었음을 의미합니다.|
| ITMG_ROOM_CHANGE_EVENT_REQUEST			|4	|방 멤버가 ChangeRoomType API를 호출하여 방 오디오 유형 전환을 요청하였음을 의미합니다.|


#### 샘플 코드  
```
-(void)OnEvent:(ITMG_MAIN_EVENT_TYPE)eventType data:(NSDictionary *)data {
	NSLog(@"OnEvent:%lu,data:%@",(unsigned long)eventType,data);
    switch (eventType) {
 		case ITMG_MAIN_EVNET_TYPE_USER_UPDATE:
			//처리
	 }
    }
}
```


### 멤버 상태 변화
이 이벤트는 상태 변화 시에만 알리며 상태 변화가 없을 경우 알리지 않습니다. 멤버 상태를 실시간으로 획득하려면 상위 레이어에서 알림을 수신하였을 때 캐시를 하십시오. 이벤트 메시지는 ITMG_MAIN_EVNET_TYPE_USER_UPDATE이고 event_ID 및 user_list 두 개 정보를 포함하며 OnEvent 함수에서 이벤트 메시지를 판단합니다.
오디오 이벤트의 알림에는 임계값이 있습니다. 이 임계값을 초과해야 알림이 발송됩니다. 2초 이후에도 오디오 패킷을 수신하지 못해야 "어떤 멤버가 오디오 패킷 발송을 중지합니다."라는 메시지가 발송됩니다.

|event_id     | 의미         |관리 내용|
| ------------- |:-------------:|-------------|
|ITMG_EVENT_ID_USER_ENTER    				|멤버 방 입장			|앱에 멤버 리스트 관리		|
|ITMG_EVENT_ID_USER_EXIT    				|멤버 방 퇴장			|앱에 멤버 리스트 관리		|
|ITMG_EVENT_ID_USER_HAS_AUDIO    		|멤버 오디오 패킷 발송		|앱에 통화 멤버 리스트 관리	|
|ITMG_EVENT_ID_USER_NO_AUDIO    			|멤버 오디오 패킷 발송 중지	|앱에 통화 멤버 리스트 관리	|

#### 샘플 코드  

```
-(void)OnEvent:(ITMG_MAIN_EVENT_TYPE)eventType data:(NSDictionary *)data{
    NSLog(@"OnEvent:%lu,data:%@",(unsigned long)eventType,data);
    switch (eventType) {
        case ITMG_MAIN_EVNET_TYPE_USER_UPDATE:
		{
		//처리
		//개발자가 매개변수를 해석하여 메시지 event_ID 및 user_list 획득
		    switch (eventID)
 		    {
 		    case ITMG_EVENT_ID_USER_ENTER:
  			    //멤버 방 입장
  			    break;
 		    case ITMG_EVENT_ID_USER_EXIT:
  			    //멤버 방 퇴장
			    break;
		    case ITMG_EVENT_ID_USER_HAS_AUDIO:
			    //멤버 오디오 패킷 발송
			    break;
		    case ITMG_EVENT_ID_USER_NO_AUDIO:
			    //멤버 오디오 패킷 발송 중지
			    break;
 		    }
		break;
		}
    }
}
```

### 품질 모니터링 이벤트
품질 모니터링 이벤트, 이벤트 메시지는 ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_QUALITY이며, 반환한 매개변수는 weight, floss 및 delay이고 의미하는 정보는 다음과 같습니다. OnEvent 함수에서 이벤트 메시지에 대해 판단합니다.

|매개변수     | 의미         |
| ------------- |-------------|
|weight    				|범위는 1 ~ 50으로 50이면 음질이 매우 우수하며, 1이면 음질이 아주 떨어져 거의 사용할 수 없습니다. 0은 초기값으로 의미가 없습니다.|
|floss    				|패킷 손실률|
|delay    		|오디오 리치 지연 시간(ms)|


### 메시지 세부 정보

|메시지     | 메시지 의미   
| ------------- |:-------------:|
|ITMG_MAIN_EVENT_TYPE_ENTER_ROOM    				       |오디오/비디오 방 입장 메시지|
|ITMG_MAIN_EVENT_TYPE_EXIT_ROOM    				         	|오디오/비디오 방 퇴장 메시지|
|ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT    		       |네트워크 등 원인으로 방 연결이 끊김 메시지|
|ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE				|방 유형 변화 이벤트|

### 메시지에 해당 데이터 세부 정보
|메시지     | Data         |예|
| ------------- |:-------------:|------------- |
| ITMG_MAIN_EVENT_TYPE_ENTER_ROOM    				|result; error_info					|{"error_info":"","result":0}|
| ITMG_MAIN_EVENT_TYPE_EXIT_ROOM    				|result; error_info  					|{"error_info":"","result":0}|
| ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT    		|result; error_info  					|{"error_info":"waiting timeout, please check your network","result":0}|
| ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE    		|result; error_info; new_room_type	|{"error_info":"","new_room_type":0,"result":0}|


## 음성 채팅 오디오 API
SDK 초기화 후 방에 입장해야 방에서 실시간 오디오 음성 관련 API를 호출할 수 있습니다.
호출 시나리오 예시:

사용자가 인터페이스에서 마이크/스피커 켜기/끄기 버튼을 클릭할 때 다음 방식을 채택하길 권합니다.
- 대부분의 게임 앱의 경우, EnableMic 및 EnbaleSpeaker API를 호출하는 것을 권장합니다. 즉, EnableAudioCaptureDevice/EnableAudioSend 및 EnableAudioPlayDevice/EnableAudioRecv API를 동시에 호출해야 합니다.
- 소셜 앱과 같은 다른 유형의 모바일 앱은 캡처 장치를 시작/종료하면 전체 장치(캡처 및 재생)가 다시 시작됩니다. 이때 앱이 배경 음악을 재생 중이라면 그 음악은 재생이 중단됩니다. 업/다운스트림에 대한 제어를 통해 마이크 켜기/끄기를 진행하면 재생 장치가 중단되지 않습니다. 구체적인 호출 방식은 다음과 같습니다. 방에 입장할 때 EnableAudioCaptureDevice(true) && EnabledAudioPlayDevice(true)를 1회 호출하고, 마이크 켜기/끄기를 클릭할 때 EnableAudioSend/Recv만 호출하여 오디오 발송/수신 여부를 제어합니다.
- 단독으로 캡처를 릴리스하거나 장치를 재생하려면 API EnableAudioCaptureDevice 및 EnableAudioPlayDevice를 참조하십시오.
- Pause를 호출하여 오디오 엔진을 일시 중지하고 resume을 호출하여 오디오 엔진을 복원합니다.


### 소셜 앱 호출 프로세스도
![](https://main.qcloudimg.com/raw/53598680491501ab5a144e87ba932ccc.png)


|API     | API 의미   |
| ------------- |:-------------:|
|EnableMic    						|마이크 켜기/끄기|
|GetMicState    						|마이크 상태 획득|
|EnableAudioCaptureDevice    		|캡처 장치 켜기/끄기		|
|IsAudioCaptureDeviceEnabled    	|캡처 장치 상태 획득	|
|EnableAudioSend    				|오디오 업스트림 시작/종료	|
|IsAudioSendEnabled    				|오디오 업스트림 상태 획득	|
|GetMicLevel    						|실시간 마이크 음량 획득	|
|SetMicVolume    					|마이크 음량 설정		|
|GetMicVolume    					|마이크 음량 획득		|
|EnableSpeaker    					|스피커 켜기/끄기|
|GetSpeakerState    					|스피커 상태 획득|
|EnableAudioPlayDevice    			|재생 장치 켜기/끄기		|
|IsAudioPlayDeviceEnabled    		|재생 장치 상태 획득	|
|EnableAudioRecv    					|오디오 다운스트림 시작/종료	|
|IsAudioRecvEnabled    				|오디오 다운스트림 상태 획득	|
|GetSpeakerLevel    					|실시간 스피커 음량 획득	|
|SetSpeakerVolume    				|스피커 음량 설정		|
|GetSpeakerVolume    				|스피커 음량 획득		|
|EnableLoopBack    					|인이어 켜기/끄기			|



### 마이크 켜기/끄기
이 API는 마이크 켜기/끄기에 사용됩니다. 방 가입 시 기본적으로 마이크 및 스피커를 켜지 않습니다.
EnableMic = EnableAudioCaptureDevice + EnableAudioSend.
#### 함수 프로토타입  

```
ITMGContext GetAudioCtrl -(void)EnableMic:(BOOL)enable
```
|매개변수     | 유형         |의미|
| ------------- |:-------------:|-------------|
| isEnabled    |boolean     |마이크를 시작해야 하는 경우 매개변수 YES를 가져오고, 마이크를 종료해야 하는 경우 매개변수 NO를 가져옵니다.|

#### 샘플 코드  

```
[[[ITMGContext GetInstance] GetAudioCtrl] EnableMic:YES];
```

### 마이크 상태 획득
이 API는 마이크 상태를 획득하는 데에 사용됩니다. 반환 값 0은 마이크가 꺼져 있음을 의미하며, 반환 값 1은 마이크가 켜져 있음을 의미합니다.
#### 함수 프로토타입  

```
ITMGContext GetAudioCtrl -(int)GetMicState
```
#### 샘플 코드  

```
[[[ITMGContext GetInstance] GetAudioCtrl] GetMicState];
```

### 캡처 장치 켜기/끄기
해당 API는 캡처 장치 켜기/끄기에 사용합니다. 방 입장 시 기본적으로 장치를 켜지 않습니다.
- 방에 입장한 후에야 해당 API를 호출할 수 있고 방을 나가면 자동으로 장치를 끕니다.
- 모바일에서 캡처 장치 켜는 동시에 일반적으로 권한 신청, 음량 유형 조정 등을 조작이 수반됩니다.

#### 함수 프로토타입  

```
ITMGContext GetAudioCtrl -(QAVResult)EnableAudioCaptureDevice:(BOOL)enabled
```
|매개변수     | 유형         |의미|
| ------------- |:-------------:|-------------|
| enabled    |BOOL     |캡처 장치를 켜야 하는 경우 매개변수 YES를 가져오고, 캡처 장치를 종료해야 하는 경우 NO를 가져옵니다.|

#### 샘플 코드  

```
캡처 장치 켜기
[[[ITMGContext GetInstance]GetAudioCtrl ]EnableAudioCaptureDevice:enabled];
```

### 캡처 장치 상태 획득
이 API는 캡처 장치 상태 획득에 사용됩니다.
#### 함수 프로토타입

```
ITMGContext GetAudioCtrl -(BOOL)IsAudioCaptureDeviceEnabled
```
#### 샘플 코드

```
BOOL IsAudioCaptureDevice = [[[ITMGContext GetInstance] GetAudioCtrl] IsAudioCaptureDeviceEnabled];
```

### 오디오 업스트림 시작/종료
이 API는 오디오 업스트림 시작/종료에 사용됩니다. 캡처 장치가 이미 시작된 경우, 캡처한 오디오 데이터를 전송합니다. 캡처 장치가 시작되지 않은 경우 여전히 무성입니다. 캡처 장치의 켜기/끄기는 API EnableAudioCaptureDevice를 참조하십시오.

#### 함수 프로토타입

```
ITMGContext GetAudioCtrl -(QAVResult)EnableAudioSend:(BOOL)enable
```
|매개변수     | 유형         |의미|
| ------------- |:-------------:|-------------|
| enable    |BOOL     |오디오 업스트림을 시작해야 하는 경우 매개변수 YES를 가져오고, 오디오 업스트림을 종료해야 하는 경우 매개변수 NO를 가져옵니다.|

#### 샘플 코드  

```
[[[ITMGContext GetInstance]GetAudioCtrl ]EnableAudioSend:enabled];
```

### 오디오 업스트림 상태 획득
이 API는 오디오 업스트림 상태 획득에 사용됩니다.
#### 함수 프로토타입  

```
ITMGContext GetAudioCtrl -(BOOL)IsAudioSendEnabled
```
#### 샘플 코드  

```
BOOL IsAudioSend =  [[[ITMGContext GetInstance] GetAudioCtrl] IsAudioSendEnabled];
```

### 마이크 실시간 음량 획득
이 API는 마이크 실시간 음량 획득에 사용되며 반환 값은 int 유형입니다.
#### 함수 프로토타입  

```
ITMGContext GetAudioCtrl -(int)GetMicLevel
```
#### 샘플 코드  
```
[[[ITMGContext GetInstance] GetAudioCtrl] GetMicLevel];
```

### 마이크 음량 설정
이 API는 마이크 음량 설정에 사용됩니다. 매개변수 volume은 마이크의 음량 설정에 사용되며, 값이 0이면 무성임을 의미하고, 값이 100이면 음량이 커지지도 작아지지도 않음을 의미합니다. 기본값은 100입니다.

#### 함수 프로토타입

```
ITMGContext GetAudioCtrl -(QAVResult)SetMicVolume:(int) volume
```
|매개변수     | 유형         |의미|
| ------------- |:-------------:|-------------|
| volume    |int        |음량 설정, 범위: 0 ~ 200|

#### 샘플 코드  

```
[[[ITMGContext GetInstance] GetAudioCtrl] SetMicVolume:100];
```

###  마이크 음량 획득
이 API는 마이크 음량 획득에 사용됩니다. 반환 값은 int 유형이며 반환 값 101은 API SetMicVolume을 호출한 적이 없음을 의미합니다.

#### 함수 프로토타입  

```
ITMGContext GetAudioCtrl -(int) GetMicVolume
```
#### 샘플 코드  

```
[[[ITMGContext GetInstance] GetAudioCtrl] GetMicVolume];
```

### 스피커 켜기/끄기
이 API는 스피커 켜기/끄기에 사용됩니다.
EnableSpeaker = EnableAudioPlayDevice +  EnableAudioRecv.
#### 함수 프로토타입  

```
ITMGContext GetAudioCtrl -(void)EnableSpeaker:(BOOL)enable
```
|매개변수     | 유형         |의미|
| ------------- |:-------------:|-------------|
| isEnabled    |boolean       |스피커를 꺼야 하는 경우 매개변수 NO를 가져오고, 스피커를 켜야 하는 경우 매개변수 YES를 가져옵니다.|

#### 샘플 코드  

```
[[[ITMGContext GetInstance] GetAudioCtrl] EnableSpeaker:YES];
```

### 스피커 상태 획득
이 API는 스피커 상태 획득에 사용됩니다. 반환 값 0은 스피커가 꺼져 있음을 의미하며, 반환 값 1은 스피커가 켜져 있음을 의미하며, 반환 값 2는 스피커가 실행 중임을 의미합니다.
#### 함수 프로토타입  

```
ITMGContext GetAudioCtrl -(int)GetSpeakerState
```

#### 샘플 코드  

```
[[[ITMGContext GetInstance] GetAudioCtrl] GetSpeakerState];
```

### 재생 장치 켜기/끄기
이 API는 재생 장치 켜기/끄기에 사용됩니다.
#### 함수 프로토타입  

```
ITMGContext GetAudioCtrl -(QAVResult)EnableAudioPlayDevice:(BOOL)enabled
```
|매개변수     | 유형         |의미|
| ------------- |:-------------:|-------------|
| enabled    |BOOL        |재생 장치를 꺼야 하는 경우 매개변수 NO를 가져오고, 재생 장치를 켜야 하는 경우 매개변수 YES를 가져옵니다.|

#### 샘플 코드

```
재생 장치 켜기
[[[ITMGContext GetInstance]GetAudioCtrl ]EnableAudioPlayDevice:enabled];
```


### 재생 장치 상태 획득
이 API는 재생 장치 상태 획득에 사용됩니다.
#### 함수 프로토타입

```
ITMGContext GetAudioCtrl -(BOOL)IsAudioPlayDeviceEnabled
```
#### 샘플 코드  

```
BOOL IsAudioPlayDevice =  [[[ITMGContext GetInstance] GetAudioCtrl] IsAudioPlayDeviceEnabled];
```

### 오디오 다운스트림 시작/종료
이 API는 오디오 다운스트림 시작/종료에 사용됩니다. 재생 장치가 이미 켜져 있는 경우 방의 다른 사람의 오디오 데이터를 재생합니다. 재생 장치가 켜지지 않은 경우 여전히 무성입니다. 재생 장치의 켜기/끄기는 API EnableAudioPlayDevice를 참조하십시오.

#### 함수 프로토타입  

```
ITMGContext GetAudioCtrl -(QAVResult)EnableAudioRecv:(BOOL)enabled
```
|매개변수     | 유형         |의미|
| ------------- |:-------------:|-------------|
| enabled    |BOOL     |오디오 다운스트림을 시작해야 하는 경우 매개변수 YES를 가져오고, 오디오 다운스트림을 종료해야 하는 경우 매개변수 NO를 가져옵니다.|

#### 샘플 코드  

```
[[[ITMGContext GetInstance]GetAudioCtrl ]EnableAudioRecv:enabled];
```

### 오디오 다운스트림 상태 획득
이 API는 오디오 다운스트림 상태 획득에 사용됩니다.
#### 함수 프로토타입  

```
ITMGAudioCtrl bool IsAudioRecvEnabled()
```

#### 샘플 코드  

```
BOOL IsAudioRecv = [[[ITMGContext GetInstance] GetAudioCtrl] IsAudioRecvEnabled];
```

### 스피커 실시간 음량 획득
이 API는 스피커 실시간 음량 획득에 사용됩니다. 반환 값은 int 유형이며, 스피커 실시간 음량을 나타냅니다.
#### 함수 프로토타입  

```
ITMGContext GetAudioCtrl -(int)GetSpeakerLevel
```

#### 샘플 코드  

```
[[[ITMGContext GetInstance] GetAudioCtrl] GetSpeakerLevel];
```

### 스피커 음량 설정
이 API는 스피커의 음량 설정에 사용됩니다.
매개변수 volume은 스피커의 음량 설정에 사용되며, 값이 0이면 무성임을, 값이 100이면 음량이 커지지도 작아지지도 않음을 의미합니다. 기본값은 100입니다.

#### 함수 프로토타입  

```
ITMGContext GetAudioCtrl -(QAVResult)SetSpeakerVolume:(int)vol
```
|매개변수     | 유형         |의미|
| ------------- |:-------------:|-------------|
| vol    |int      |음량 설정, 범위: 0 ~ 200|

#### 샘플 코드  

```
[[[ITMGContext GetInstance] GetAudioCtrl] SetSpeakerVolume:100];
```

### 스피커 음량 획득
이 API는 스피커 음량 획득에 사용됩니다. 반환 값은 int 유형이며 스피커의 음량을 의미합니다. 반환 값 101은 API SetSpeakerVolume을 호출한 적이 없음을 의미합니다.
Level은 실시간 음량이고, Volume은 스피커의 음량으로 최종 음량은 Level*Volume%입니다. 예: 실시간 음량 값이 100이고, Volume 값이 60이라면 최종 음량 값은 역시 60이 됩니다.

#### 함수 프로토타입  

```
ITMGContext GetAudioCtrl -(int)GetSpeakerVolume
```
#### 샘플 코드  

```
[[[ITMGContext GetInstance] GetAudioCtrl] GetSpeakerVolume];
```


### 인이어 시동
이 API는 인이어 시동에 사용됩니다.
#### 함수 프로토타입  

```
ITMGContext GetAudioCtrl -(QAVResult)EnableLoopBack:(BOOL)enable
```
|매개변수     | 유형         |의미|
| ------------- |:-------------:|-------------|
| enable    |boolean         |시동 여부 설정|

#### 샘플 코드  

```
[[[ITMGContext GetInstance] GetAudioCtrl] EnableLoopBack:YES];
```


## 음성 채팅 반주 관련 API
|API     | API 의미   |
| ------------- |:-------------:|
|StartAccompany    				       |반주 재생 시작|
|StopAccompany    				   	|반주 재생 중지|
|IsAccompanyPlayEnd				|반주 재생 완료 여부|
|PauseAccompany    					|반주 재생 일시 중지|
|ResumeAccompany					|반주 다시 재생|
|SetAccompanyVolume 				|반주 음량 설정|
|GetAccompanyVolume				|반주 재생 음량 획득|
|SetAccompanyFileCurrentPlayedTimeByMs 				|재생 진도 설정|


### 반주 재생 시작
이 API를 호출하여 반주 재생을 시작합니다. M4A, WAV, MP3 모두 3가지 형식을 지원합니다. 이 API를 호출하면 음량이 리셋됩니다.
#### 함수 프로토타입  

```
ITMGContext GetAudioEffectCtrl -(QAVAccResult)StartAccompany:(NSString*)filePath loopBack:(BOOL)loopBack loopCount:(int)loopCount
```
|매개변수     | 유형         |의미|
| ------------- |:-------------:|-------------|
| filePath    	|NSString    		|반주 재생 경로											|
| loopBack  	|boolean         	|믹스하여 발송 여부, 일반적으로 YES로 설정하며 다른 사람도 반주를 들을 수 있습니다	|
| loopCount	|int          		|순환 횟수, -1은 무한 순환을 의미합니다.				|

#### 샘플 코드  

```
[[[ITMGContext GetInstance] GetAudioEffectCtrl] StartAccompany:path loopBack:isLoopBack loopCount:loopCount];
```

### 반주 재생 콜백
반주 재생 완료 후, 콜백 함수는 OnEvent를 호출합니다. 이벤트 메시지는 ITMG_MAIN_EVENT_TYPE_ACCOMPANY_FINISH이며 OnEvent 함수에서 이벤트 메시지를 판단합니다.
#### 샘플 코드  

```
-(void)OnEvent:(ITMG_MAIN_EVENT_TYPE)eventType data:(NSDictionary *)data{
    NSLog(@"OnEvent:%lu,data:%@",(unsigned long)eventType,data);
    switch (eventType) {
        case ITMG_MAIN_EVENT_TYPE_ACCOMPANY_FINISH：
        {
	    //반주 재생 이벤트 콜백
        }
            break;
    }
}
```

### 반주 재생 중지
이 API를 호출하여 반주 재생을 중지합니다.
#### 함수 프로토타입  

```
ITMGContext GetAudioEffectCtrl -(QAVAccResult)StopAccompany:(int)duckerTime
```
|매개변수     | 유형         |의미|
| ------------- |:-------------:|-------------|
| duckerTimeMs    |int             |페이드아웃 시간|

#### 샘플 코드  

```
[[[ITMGContext GetInstance] GetAudioEffectCtrl] StopAccompany:duckerTime];
```

### 반주 재생 완료 여부
재생이 완료되었다면 반환 값은 YES, 재생이 완료되지 않았다면 반환 값은 NO입니다.
#### 함수 프로토타입  

```
ITMGContext GetAudioEffectCtrl -(bool)IsAccompanyPlayEnd
```
#### 샘플 코드  

```
[[[ITMGContext GetInstance] GetAudioEffectCtrl] IsAccompanyPlayEnd];
```

### 반주 재생 일시 중지
이 API를 호출하여 반주 재생을 일시 중지합니다.
#### 함수 프로토타입  

```
ITMGContext GetAudioEffectCtrl -(QAVAccResult)PauseAccompany
```
#### 샘플 코드  

```
[[[ITMGContext GetInstance] GetAudioEffectCtrl] PauseAccompany];
```

### 반주 다시 재생
이 API는 반주를 다시 재생하는 데 사용됩니다.
#### 함수 프로토타입  

```
GetAudioEffectCtrl -(QAVAccResult)ResumeAccompany
```
#### 샘플 코드  

```
[[[ITMGContext GetInstance] GetAudioEffectCtrl] ResumeAccompany];
```

### 반주 음량 설정
반주 음량을 설정하는 데 사용되고 가능한 범위는 0 ~200입니다. 기본값은 100입니다. 100보다 큰 값은 "볼륨 높이기"를 의미하고 100보다 작은 값은 "볼륨 줄이기"를 의미합니다.
#### 함수 프로토타입  

```
ITMGContext GetAudioEffectCtrl -(QAVAccResult)SetAccompanyVolume:(int)vol
```
|매개변수     | 유형         |의미|
| ------------- |:-------------:|-------------|
| vol    |int             |음량 값|

#### 샘플 코드  

```
[[[ITMGContext GetInstance] GetAudioEffectCtrl] SetAccompanyVolume:volume];
```

### 반주 재생 음량 획득
이 API는 반주 음량 획득에 사용됩니다.
#### 함수 프로토타입  

```
ITMGContext GetAudioEffectCtrl -(int)GetAccompanyVolume
```
#### 샘플 코드  

```
[[[ITMGContext GetInstance] GetAudioEffectCtrl] GetAccompanyVolume];
```

### 반주 재생 진도 획득
다음 2개의 API는 반주 재생 진도 획득에 사용됩니다. 주의사항: Current / Total = 현재 순환 횟수, Current % Total = 현재 순환 재생 위치입니다.
#### 함수 프로토타입  

```
ITMGContext GetAudioEffectCtrl -(int)GetAccompanyFileTotalTimeByMs
ITMGContext GetAudioEffectCtrl -(int)GetAccompanyFileCurrentPlayedTimeByMs
```
#### 샘플 코드  

```
[[[ITMGContext GetInstance] GetAudioEffectCtrl] GetAccompanyFileTotalTimeByMs];
[[[ITMGContext GetInstance] GetAudioEffectCtrl] GetAccompanyFileCurrentPlayedTimeByMs];
```

### 재생 진도 설정
이 API는 재생 진도 설정에 사용됩니다.
#### 함수 프로토타입  

```
ITMGContext GetAudioEffectCtrl -(QAVAccResult)SetAccompanyFileCurrentPlayedTimeByMs:(uint) time
```
|매개변수     | 유형         |의미|
| ------------- |:-------------:|-------------|
| time    |uint                |재생 진도, 단위: 밀리초|

#### 샘플 코드  

```
[[[ITMGContext GetInstance] GetAudioEffectCtrl] SetAccompanyFileCurrentPlayedTimeByMs:time];
```

## 음성 채팅 효과음 관련 API
|API     | API 의미   |
| ------------- |:-------------:|
|PlayEffect    		|효과음 재생|
|PauseEffect    	|효과음 재생 일시 중지|
|PauseAllEffects	|모든 효과음 일시 중지|
|ResumeEffect    	|효과음 다시 재생|
|ResumeAllEffects	|모든 효과음 다시 재생|
|StopEffect 		|효과음 재생 중지|
|StopAllEffects		|모든 효과음 재생 중지|
|SetVoiceType 		|변성 효과|
|SetKaraokeType 		|노래방 효과음|
|GetEffectsVolume	|효과음 재생 음량 획득|
|SetEffectsVolume 	|효과음 재생 음량 설정|


### 효과음 재생
이 API는 효과음 재생에 사용됩니다. 매개변수에서의 효과음 ID는 앱에서 관리해야 하며, ID는 1차의 독립 재생 이벤트를 의미합니다. 후속적으로 이 ID에 의해 이번 재생을 제어할 수 있습니다. 파일은 M4A, WAV, MP3 모두 3가지 형식을 지원합니다.
#### 함수 프로토타입  

```
ITMGContext GetAudioEffectCtrl -(QAVResult)PlayEffect:(int)soundId filePath:(NSString*)filePath loop:(BOOL)loop
```
|매개변수     | 유형         |의미|
| ------------- |:-------------:|-------------|
| soundId  	|int           	|효과음 ID			|
| filePath    	|NSString    	|효과음 경로		|
| loop    		|boolean  	|중복 재생 여부	|

#### 샘플 코드  

```
[[[ITMGContext GetInstance] GetAudioEffectCtrl] PlayEffect:soundId filePath:path loop:isLoop];
```

### 효과음 재생 일시 중지
이 API는 효과음 재생 일시 중지에 사용됩니다.
#### 함수 프로토타입  

```
ITMGContext GetAudioEffectCtrl -(QAVResult)PauseEffect:(int)soundId
```
|매개변수     | 유형         |의미|
| ------------- |:-------------:|-------------|
| soundID    |int                    |효과음 ID|

#### 샘플 코드  

```
[[[ITMGContext GetInstance] GetAudioEffectCtrl] PauseEffect:soundId];
```

### 모든 효과음 일시 중지
이 API를 호출하여 모든 효과음을 일시 중지합니다.
#### 함수 프로토타입  

```
ITMGContext GetAudioEffectCtrl -(QAVResult)PauseAllEffects
```
#### 샘플 코드  

```
[[[ITMGContext GetInstance] GetAudioEffectCtrl] PauseAllEffects];
```

### 효과음 다시 재생
이 API는 효과음 다시 재생에 사용됩니다.
#### 함수 프로토타입  

```
ITMGContext GetAudioEffectCtrl -(QAVResult)ResumeEffect:(int)soundId
```
|매개변수     | 유형         |의미|
| ------------- |:-------------:|-------------|
| soundID    |int                    |효과음 ID|

#### 샘플 코드  

```
[[[ITMGContext GetInstance] GetAudioEffectCtrl] ResumeEffect:soundId];
```

### 모든 효과음 다시 재생
이 API를 호출하여 모든 효과음을 다시 재생합니다.
#### 함수 프로토타입  

```
ITMGContext GetAudioEffectCtrl -(QAVResult)ResumeAllEffects
```
#### 샘플 코드  

```
[[[ITMGContext GetInstance] GetAudioEffectCtrl] ResumeAllEffects];
```

### 효과음 재생 중지
이 API는 효과음 재생 중지에 사용됩니다.
#### 함수 프로토타입  

```
ITMGContext GetAudioEffectCtrl -(QAVResult)StopEffect:(int)soundId
```
|매개변수     | 유형         |의미|
| ------------- |:-------------:|-------------|
| soundID    |int                    |효과음 ID|

#### 샘플 코드  

```
[[[ITMGContext GetInstance] GetAudioEffectCtrl] StopEffect:soundId];
```

### 모든 효과음 재생 중지
이 API를 호출하여 모든 효과음 재생을 중지합니다.
#### 함수 프로토타입  

```
ITMGContext GetAudioEffectCtrl -(QAVResult)StopAllEffects
```
#### 샘플 코드  

```
[[[ITMGContext GetInstance] GetAudioEffectCtrl] StopAllEffects];
```

### 변성 효과
이 API를 호출하여 변성 효과를 설정합니다.
#### 함수 프로토타입  

```
ITMGContext GetAudioEffectCtrl -(QAVResult)SetVoiceType:(ITMG_VOICE_TYPE) type
```
|매개변수     | 유형         |의미|
| ------------- |:-------------:|-------------|
| type    |int                    |로컬 오디오 변성 유형|




|유형 매개변수     |매개변수 표시 값|의미|
| ------------- |-------------|------------- |
| ITMG_VOICE_TYPE_ORIGINAL_SOUND  		|0	|오리지날			|
| ITMG_VOICE_TYPE_LOLITA    				|1	|여자애			|
| ITMG_VOICE_TYPE_UNCLE  				|2	|아저씨			|
| ITMG_VOICE_TYPE_INTANGIBLE    			|3	|고유함			|
| ITMG_VOICE_TYPE_DEAD_FATBOY  			|4	|뚱뚱보			|
| ITMG_VOICE_TYPE_HEAVY_MENTA			|5	|헤비 멘탈			|
| ITMG_VOICE_TYPE_DIALECT 				|6	|외국인			|
| ITMG_VOICE_TYPE_INFLUENZA 				|7	|독감			|
| ITMG_VOICE_TYPE_CAGED_ANIMAL 			|8	|야수			|
| ITMG_VOICE_TYPE_HEAVY_MACHINE		|9	|무거운 기계			|
| ITMG_VOICE_TYPE_STRONG_CURRENT		|10	|강한 전류			|
| ITMG_VOICE_TYPE_KINDER_GARTEN			|11	|유치원생			|
| ITMG_VOICE_TYPE_HUANG 					|12	|미니언즈			|


#### 샘플 코드  

```
[[[ITMGContext GetInstance] GetAudioEffectCtrl] SetVoiceType:0];
```

### 노래방 효과음
이 API를 호출하여 노래방 효과음을 설정합니다.
####  함수 프로토타입  
```
ITMGContext GetAudioEffectCtrl -(QAVResult)SetKaraokeType:(ITMG_KARAOKE_TYPE) type
```
|매개변수     | 유형         |의미|
| ------------- |:-------------:|-------------|
| type    |int                    |로컬 오디오 변성 유형|


|유형 매개변수     |매개변수 표시 값|의미|
| ------------- |-------------|------------- |
|ITMG_KARAOKE_TYPE_ORIGINAL 		|0	|오리지날			|
|ITMG_KARAOKE_TYPE_POP 				|1	|팝			|
|ITMG_KARAOKE_TYPE_ROCK 			|2	|락			|
|ITMG_KARAOKE_TYPE_RB 				|3	|힙합			|
|ITMG_KARAOKE_TYPE_DANCE 			|4	|댄스곡			|
|ITMG_KARAOKE_TYPE_HEAVEN 			|5	|고유함			|
|ITMG_KARAOKE_TYPE_TTS 				|6	|음성 합성		|

#### 샘플 코드  
```
[[[ITMGContext GetInstance] GetAudioEffectCtrl] SetKaraokeType:0];
```

### 효과음 재생 음량 획득
효과음 재생 음량을 획득하는 데 사용되고 선형 음량입니다. 기본값은 100입니다. 100보다 큰 값은 "볼륨 높이기"를 의미하고 100보다 작은 값은 "볼륨 줄이기"를 의미합니다.
#### 함수 프로토타입  

```
ITMGContext GetAudioEffectCtrl -(int)GetEffectsVolume
```
#### 샘플 코드  

```
[[[ITMGContext GetInstance] GetAudioEffectCtrl] GetEffectsVolume];
```

### 효과음 재생 음량 설정
이 API를 호출하여 효과음 재생 음량을 설정합니다.
#### 함수 프로토타입  

```
ITMGContext GetAudioEffectCtrl -(QAVResult)SetEffectsVolume:(int)volume
```
|매개변수     | 유형         |의미|
| ------------- |:-------------:|-------------|
| volume    |int                    |음량 값|

#### 샘플 코드  

```
[[[ITMGContext GetInstance] GetAudioEffectCtrl] SetEffectsVolume:(int)Volume];
```

## 오프라인 음성
오프라인 음성 및 문자 전환 기능을 사용하려면 우선 SDK를 초기화해야 합니다.

|API     | API 의미   |
| ------------- |:-------------:|
|ApplyPTTAuthbuffer    |인증 초기화	|
|SetMaxMessageLength    |최대 음성 메시지 시간 제한	|
|StartRecording		|녹음 시작		|
|StartRecordingWithStreamingRecognition		|스트리밍 녹음 시작		|
|StopRecording    	|녹음 중지		|
|CancelRecording	|녹음 취소		|
|GetMicLevel |오프라인 음성의 실시간 마이크 음량 획득	|
|GetSpeakerLevel | 오프라인 음성의 실시간 스피커 음량 획득	|
|UploadRecordedFile 	|음성 파일 업로드		|
|DownloadRecordedFile	|음성 파일 다운로드		|
|PlayRecordedFile 	|음성 재생		|
|StopPlayFile		|음성 재생 중지		|
|GetFileSize 		|음성 파일 크기		|
|GetVoiceFileDuration	|음성 파일 시간		|
|SpeechToText 		|음성을 문자로 인식		|



### 인증 초기화
SDK 초기화 후 인증 초기화를 호출하여 authBuffer를 획득하려면 상기 음성 채팅 인증 정보 API를 참조하십시오.
#### 함수 프로토타입  
```
ITMGContext GetPTT -(QAVResult)ApplyPTTAuthbuffer:(NSData *)authBuffer
```
|매개변수     | 유형         |의미|
| ------------- |:-------------:|-------------|
| authBuffer    |NSData*                    |인증|

#### 샘플 코드  
```
[[[ITMGContext GetInstance]GetPTT]ApplyPTTAuthbuffer:(NSData *)authBuffer];
```

### 최대 음성 메시지 시간 제한
최대 음성 메시지 길이를 60초로 제한합니다.

#### 함수 프로토타입  

```
ITMGContext GetPTT -(void)SetMaxMessageLength:(int)msTime
```
|매개변수     | 유형         |의미|
| ------------- |:-------------:|-------------|
| msTime    |int                    |음성 시간, 단위: 밀리초|

#### 샘플 코드  

```
[[[ITMGContext GetInstance]GetPTT]SetMaxMessageLength:(int)msTime];
```

### 녹음 시작
이 API는 녹음 시작에 사용됩니다. 녹음 파일을 업로드해야 음성을 문자로 전환 등 조작을 진행할 수 있습니다.
#### 함수 프로토타입  

```
ITMGContext GetPTT -(void)StartRecording:(NSString*)fileDir
```
|매개변수     | 유형         |의미|
| ------------- |:-------------:|-------------|
| fileDir    |NSString                     |음성 저장 경로|

#### 샘플 코드  

```
[[[ITMGContext GetInstance]GetPTT]StartRecording:path];
```

### 녹음 시작 콜백
녹음 시작 완료 후 콜백 함수는 OnEvent를 호출합니다. 이벤트 메시지는 ITMG_MAIN_EVNET_TYPE_PTT_RECORD_COMPLETE이며 OnEvent 함수에서 이벤트 메시지를 판단합니다.

#### 샘플 코드  

```
-(void)OnEvent:(ITMG_MAIN_EVENT_TYPE)eventType data:(NSDictionary *)data{
    NSLog(@"OnEvent:%lu,data:%@",(unsigned long)eventType,data);
    switch (eventType) {
        case ITMG_MAIN_EVNET_TYPE_PTT_RECORD_COMPLETE：
        {
	    //녹음 콜백
        }
            break;
    }
}
```


### 스트리밍 음성 인식 시작
이 API는 스트리밍 음성 인식 시작에 사용되며, 동시에 콜백 과정에서 실시간으로 음성을 문자로 전환하여 반환할 수 있으며, 언어를 지정하여 인식할 수 있고 인식한 정보를 지정한 언어로 번역하여 반환할 수도 있습니다.


#### 함수 프로토타입  

```
ITMGContext GetPTT int StartRecordingWithStreamingRecognition(const NSString* filePath)
ITMGContext GetPTT int StartRecordingWithStreamingRecognition(const NSString* filePath,const NSString*speechLanguage,const NSString*translateLanguage)
```
|매개변수     | 유형         |의미|
| ------------- |:-------------:|-------------|
| filePath    	|NSString*	|저장한 음성 경로	|
| speechLanguage    |NSString*                     |지정한 문자로 식별하는 언어 매개변수, 세부 정보는 [음성을 문자로 전환하는 언어 매개변수 참고리스트](https://cloud.tencent.com/document/product/607/30282)를 참조하십시오.|
| translateLanguage    |NSString*                     |지정한 문자로 번역하는 언어 매개변수, 세부 정보는 [음성을 문자로 전환하는 언어 매개변수 참고리스트](https://cloud.tencent.com/document/product/607/30282)를 참조하십시오. (이 매개변수는 잠시 사용 불가하고 speechLanguage와 동일한 매개변수를 입력해 주십시오)|

#### 샘플 코드  
```
[[[ITMGContext GetInstance] GetPTT] StartRecordingWithStreamingRecognition:recordfilePath  speechLanguage:@"cmn-Hans-CN" translateLanguage:@"cmn-Hans-CN"];
```


### 스트리밍 음성 인식 시작의 콜백
스트리밍 음성 인식 시작 완료 후 콜백은 함수 OnEvent를 호출합니다. 이벤트 메시지는 ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_COMPLETE이며 OnEvent 함수에서 이벤트 메시지를 판단합니다. 전달하는 매개변수는 아래 네가지 정보를 포함합니다.

|메시지 이름     | 의미         |
| ------------- |:-------------:|
| result    	|스트리밍 음성 인식 성공 여부를 판단하는 반환 코드			|
| text    		|음성을 문자로 전환하여 인식한 텍스트	|
| file_path 	|녹음 저장 로컬 주소		|
| file_id 		|녹음의 백 엔드 URL 주소	|

|오류 코드     | 의미         |처리 방식|
| ------------- |:-------------:|:-------------:|
|32775	|스트리밍 음성을 문자로 전환에 실패했지만, 녹음이 성공했습니다.	|UploadRecordedFile API를 호출하여 녹음을 업로드하고 SpeechToText API를 호출하여 음성을 문자로 전환합니다.
|32777	|스트리밍 음성을 문자로 전환에 실패했지만, 녹음이 성공했고, 업로드도 성공했습니다.	|반환한 정보에 업로드가 성공한 백 엔드 URL 주소가 있으며, SpeechToText API를 호출하여 음성을 문자로 전환합니다.

#### 샘플 코드  
```
-(void)OnEvent:(ITMG_MAIN_EVENT_TYPE)eventType data:(NSDictionary *)data{
    NSLog(@"OnEvent:%lu,data:%@",(unsigned long)eventType,data);
    switch (eventType) {
        case ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_COMPLETE：
        {
	    //스트리밍 음성 인식의 콜백
        }
            break;
    }
}

```

### 녹음 중지
이 API는 녹음을 중지하는 데 사용되며 비동기 API입니다. 녹음 후 콜백이 반환됩니다. 녹음이 완료되면 녹음 파일을 사용할 수 있습니다.
#### 함수 프로토타입  

```
ITMGContext GetPTT -(QAVResult)StopRecording
```
#### 샘플 코드  

```
[[[ITMGContext GetInstance]GetPTT]StopRecording];
```

### 녹음 취소
이 API를 호출하여 녹음을 취소합니다. 취소 후 콜백이 없습니다.
#### 함수 프로토타입  

```
ITMGContext GetPTT -(QAVResult)CancelRecording
```
#### 샘플 코드  

```
[[[ITMGContext GetInstance]GetPTT]CancelRecording];
```

### 오프라인 음성 마이크 실시간 음량 획득
이 API는 마이크 실시간 음량 획득에 사용되며 반환 값은 int 유형입니다. 값 범위는 0 ~ 100입니다.

#### 함수 프로토타입  
```
ITMGContext GetPTT -(QAVResult)GetMicLevel
```
#### 샘플 코드  
```
[[[ITMGContext GetInstance]GetPTT]GetMicLevel];
```


### 스피커 실시간 음량 획득
이 API는 스피커 실시간 음량 획득에 사용되며 반환 값은 int 유형입니다. 값 범위는 0 ~ 100입니다.

#### 함수 프로토타입  
```
ITMGContext GetPTT -(QAVResult)GetSpeakerLevel
```

#### 샘플 코드  
```
[[[ITMGContext GetInstance]GetPTT]GetSpeakerLevel];
```




### 음성 파일 업로드
이 API는 음성 파일울 업로드하는 데 사용됩니다.
#### 함수 프로토타입  

```
ITMGContext GetPTT -(void)UploadRecordedFile:(NSString*)filePath
```
|매개변수     | 유형         |의미|
| ------------- |:-------------:|-------------|
| filePath    |NSString                      |음성 업로드 경로|

#### 샘플 코드  

```
[[[ITMGContext GetInstance]GetPTT]UploadRecordedFile:path];
```

### 음성 업로드 완료 콜백
음성 업로드 완료 후, 이벤트 메시지는 ITMG_MAIN_EVNET_TYPE_PTT_UPLOAD_COMPLETE이며 OnEvent 함수에서 이벤트 메시지를 판단합니다.
```
-(void)OnEvent:(ITMG_MAIN_EVENT_TYPE)eventType data:(NSDictionary *)data{
    NSLog(@"OnEvent:%lu,data:%@",(unsigned long)eventType,data);
    switch (eventType) {
        case ITMG_MAIN_EVNET_TYPE_PTT_UPLOAD_COMPLETE：
        {
	    //음성 업로드 성공
        }
            break;
    }
}
```

### 음성 파일 다운로드
이 API는 음성 파일을 다운로드하는 데 사용됩니다.
#### 함수 프로토타입  

```
ITMGContext GetPTT -(void)DownloadRecordedFile:(NSString*)fileId downloadFilePath:(NSString*)downloadFilePath
```

|매개변수     | 유형         |의미|
| ------------- |:-------------:|-------------|
| fileID    			|NSString                      |파일의 URL 경로		|
| downloadFilePath 	|NSString                      |파일의 로컬 저장 경로	|

#### 샘플 코드  

```
[[[ITMGContext GetInstance]GetPTT]DownloadRecordedFile:fileIdpath downloadFilePath:path];
```

### 음성 파일의 다운로드가 완료되면 콜백이 실행됩니다.
음성 다운로드 완료 후, 이벤트 메시지는 ITMG_MAIN_EVNET_TYPE_PTT_DOWNLOAD_COMPLETE이며 OnEvent 함수에서 이벤트 메시지를 판단합니다.
```
-(void)OnEvent:(ITMG_MAIN_EVENT_TYPE)eventType data:(NSDictionary *)data{
    NSLog(@"OnEvent:%lu,data:%@",(unsigned long)eventType,data);
    switch (eventType) {
        case ITMG_MAIN_EVNET_TYPE_PTT_DOWNLOAD_COMPLETE：
        {
	    //다운로드 성공   
        }
            break;
    }
}
```

### 음성 재생
이 API는 음성을 재생하는 데 사용됩니다.
#### 함수 프로토타입  

```
ITMGContext GetPTT -(void)PlayRecordedFile:(NSString*)downloadFilePath
```
|매개변수     | 유형         |의미|
| ------------- |:-------------:|-------------|
| downloadFilePath    |NSString                      |파일의 경로|

#### 샘플 코드  

```
[[[ITMGContext GetInstance]GetPTT]PlayRecordedFile:path];
```

### 음성 재생 콜백
음성 재생 콜백, 이벤트 메시지는 ITMG_MAIN_EVNET_TYPE_PTT_PLAY_COMPLETE이며 OnEvent 함수에서 이벤트 메시지를 판단합니다.
```
-(void)OnEvent:(ITMG_MAIN_EVENT_TYPE)eventType data:(NSDictionary *)data{
    NSLog(@"OnEvent:%lu,data:%@",(unsigned long)eventType,data);
    switch (eventType) {
        case ITMG_MAIN_EVNET_TYPE_PTT_PLAY_COMPLETE：
        {
	    //음성 재생 콜백
        }
            break;
    }
}
```

### 음성 재생 중지
이 API는 음성 재생 중지에 사용됩니다.
#### 함수 프로토타입  

```
ITMGContext GetPTT -(int)StopPlayFile
```
#### 샘플 코드  

```
[[[ITMGContext GetInstance]GetPTT]StopPlayFile];
```

### 음성 파일 크기 획득
이 API를 통해 음성 파일 크기를 획득할 수 있습니다.
#### 함수 프로토타입  

```
ITMGContext GetPTT -(int)GetFileSize:(NSString*)filePath
```
|매개변수     | 유형         |의미|
| ------------- |:-------------:|-------------|
| filePath    |NSString                     |음성 파일 경로|

#### 샘플 코드  

```
[[[ITMGContext GetInstance]GetPTT]GetFileSize:path];
```

### 음성 파일 시간 획득
이 API는 음성 파일 시간 획득에 사용되며 단위는 밀리초입니다.
#### 함수 프로토타입  

```
ITMGContext GetPTT -(int)GetVoiceFileDuration:(NSString*)filePath
```
|매개변수     | 유형         |의미|
| ------------- |:-------------:|-------------|
| filePath    |NSString                     |음성 파일 경로|

#### 샘플 코드  

```
[[[ITMGContext GetInstance]GetPTT]GetVoiceFileDuration:path];
```

### 지정한 음성 파일을 문자로 식별
이 API는 지정한 음성 파일을 문자로 식별하는 데 사용됩니다.
#### 함수 프로토타입  

```
ITMGContext GetPTT -(void)SpeechToText:(NSString*)fileID
```
|매개변수     | 유형         |의미|
| ------------- |:-------------:|-------------|
| fileID    |NSString                     |음성 파일 URL|

#### 샘플 코드  

```
[[[ITMGContext GetInstance]GetPTT]SpeechToText:fileID];
```

### 지정한 음성 파일을 문자로 번역(지정한 언어)
이 API는 지정한 음성 파일을 지정한 언어의 문자로 번역하는 데 사용됩니다.


####  함수 프로토타입  
```
ITMGContext GetPTT -(void)SpeechToText:(NSString*)fileID (NSString*)speechLanguage (NSString*)translateLanguage
```
|매개변수     | 유형         |의미|
| ------------- |:-------------:|-------------|
| fileID    |NSString                     |음성 파일 URL|
| speechLanguage    |NSString*                     |지정한 문자로 식별하는 언어 매개변수, 세부 정보는 [음성을 문자로 전환하는 언어 매개변수 참고 리스트](https://cloud.tencent.com/document/product/607/30282)를 참조하십시오.|
| translatelanguage    |NSString*                     |지정한 문자로 번역하는 언어 매개변수, 세부 정보는 [음성을 문자로 전환하는 언어 매개변수 참고리스트](https://cloud.tencent.com/document/product/607/30282)를 참조하십시오(이 매개변수는 잠시 사용 불가하고 speechLanguage와 동일한 매개변수를 입력해 주십시오).|

####  샘플 코드  
```
[[[ITMGContext GetInstance]GetPTT]SpeechToText:fileID speechLanguage:"cmn-Hans-CN" translateLanguage:"cmn-Hans-CN"];
```



### 식별 콜백
지정한 음성 파일을 문자로 식별한 콜백, 이벤트 메시지는 ITMG_MAIN_EVNET_TYPE_PTT_SPEECH2TEXT_COMPLETE이며 OnEvent 함수에서 이벤트 메시지를 판단합니다.
```
-(void)OnEvent:(ITMG_MAIN_EVENT_TYPE)eventType data:(NSDictionary *)data{
    NSLog(@"OnEvent:%lu,data:%@",(unsigned long)eventType,data);
    switch (eventType) {
        case ITMG_MAIN_EVNET_TYPE_PTT_SPEECH2TEXT_COMPLETE：
        {
	    //음성 파일 인식 성공       
        }
            break;   
    }
}
```
## 고급 API

### 버전 번호 획득
SDK 버전 번호 획득, 분석에 사용됩니다.
#### 함수 프로토타입

```
ITMGContext  -(NSString*)GetSDKVersion
```
#### 샘플 코드  

```
[[ITMGContext GetInstance] GetSDKVersion];
```

### 로그 인쇄 등급 설정
로그 인쇄 등급 설정에 사용됩니다. 기본 등급 유지를 권장합니다.
#### 함수 프로토타입
```
ITMGContext -(void)SetLogLevel:(ITMG_LOG_LEVEL)levelWrite (ITMG_LOG_LEVEL)levelPrint
```



#### 매개변수 의미

|매개변수|유형|의미|
|---|---|---|
|levelWrite|ITMG_LOG_LEVEL| 쓰기 로그의 등급 설정, TMG_LOG_LEVEL_NONE은 쓰지 않음을 의미합니다|
|levelPrint|ITMG_LOG_LEVEL| 인쇄 로그의 등급 설정, TMG_LOG_LEVEL_NONE은 인쇄하지 않음을 의미합니다|




|ITMG_LOG_LEVEL|의미|
| -------------------------------|:-------------:|
|TMG_LOG_LEVEL_NONE=0		|로그 인쇄하지 않음			|
|TMG_LOG_LEVEL_ERROR=1		|오류 로그 인쇄(기본값)	|
|TMG_LOG_LEVEL_INFO=2			|알림 로그 인쇄		|
|TMG_LOG_LEVEL_DEBUG=3		|개발 디버깅 로그 인쇄	|
|TMG_LOG_LEVEL_VERBOSE=4		|고빈도 로그 인쇄		|

#### 샘플 코드  
```
[[ITMGContext GetInstance] SetLogLevel:TMG_LOG_LEVEL_NONE YES YES];
```

### 로그 인쇄 경로 설정
로그 인쇄 경로 설정에 사용됩니다. 기본 경로는 /Users/username/Library/Containers/xxx.xxx.xxx/Data/Documents입니다.
#### 함수 프로토타입
```
ITMGContext -(void)SetLogPath:(NSString*)logDir
```

|매개변수     | 유형         |의미|
| ------------- |:-------------:|-------------|
| logDir    		|NSString   		|경로|

#### 샘플 코드  
```
[[ITMGContext GetInstance] SetLogPath:Path];
```


### 진단 정보 획득
실시간 영상/음성 통화 품질 관련 정보를 획득합니다. 해당 API는 주로 실시간 통화 품질을 확인하고 문제점을 해결하는 데 사용되므로 비즈니스 측에서는 무시할 수 있습니다.
#### 함수 프로토타입  

```
ITMGContext GetRoom -(NSString*)GetQualityTips
```
#### 샘플 코드  

```
[[[ITMGContext GetInstance]GetRoom ] GetQualityTips];
```

### 오디오 데이터 블랙리스트에 추가
어느 ID 하나를 오디오 데이터 블랙리스트에 추가합니다. 반환 값이 0이면 호출 성공을 의미합니다.
#### 함수 프로토타입  

```
ITMGContext GetAudioCtrl -(QAVResult)AddAudioBlackList:(NSString*)openID
```
|매개변수     | 유형         |의미|
| ------------- |:-------------:|-------------|
| openID    |NSString      |블랙리스트에 추가할 ID|

#### 샘플 코드  

```
[[[ITMGContext GetInstance]GetAudioCtrl ] AddAudioBlackList[id]];
```

### 오디오 데이터 블랙리스트에서 제거
어느 ID 하나를 오디오 데이터 블랙리스트에서 제거합니다. 반환 값이 0이면 호출 성공을 의미합니다.
#### 함수 프로토타입  

```
ITMGContext GetAudioCtrl -(QAVResult)RemoveAudioBlackList:(NSString*)openID
```
|매개변수     | 유형         |의미|
| ------------- |:-------------:|-------------|
| openID    |NSString      |블랙리스트에서 제거할 ID|

#### 샘플 코드  

```
[[[ITMGContext GetInstance]GetAudioCtrl ] RemoveAudioBlackList[openId]];
```
## 콜백 메시지

#### 메시지 리스트:

|메시지     | 메시지 의미   
| ------------- |:-------------:|
|ITMG_MAIN_EVENT_TYPE_ENTER_ROOM    		|오디오 방 입장 메시지		|
|ITMG_MAIN_EVENT_TYPE_EXIT_ROOM    		|오디오 방 퇴장 메시지		|
|ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT		|네트워크 등 원인으로 방 연결이 끊김 메시지	|
|ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE		|방 유형 변화 이벤트		|
|ITMG_MAIN_EVENT_TYPE_ACCOMPANY_FINISH		|반주 종료 메시지			|
|ITMG_MAIN_EVNET_TYPE_USER_UPDATE		|방 멤버 변경 메시지		|
|ITMG_MAIN_EVNET_TYPE_PTT_RECORD_COMPLETE	|PTT 녹음 완료			|
|ITMG_MAIN_EVNET_TYPE_PTT_UPLOAD_COMPLETE	|PTT 업로드 완료			|
|ITMG_MAIN_EVNET_TYPE_PTT_DOWNLOAD_COMPLETE	|PTT 다운로드 완료			|
|ITMG_MAIN_EVNET_TYPE_PTT_PLAY_COMPLETE		|PTT 재생 완료			|
|ITMG_MAIN_EVNET_TYPE_PTT_SPEECH2TEXT_COMPLETE	|음성을 문자로 전환 완료			|

#### 데이터 리스트:

|메시지     | Data         |예|
| ------------- |:-------------:|------------- |
| ITMG_MAIN_EVENT_TYPE_ENTER_ROOM    		|result; error_info			|{"error_info":"","result":0}|
| ITMG_MAIN_EVENT_TYPE_EXIT_ROOM    		|result; error_info  			|{"error_info":"","result":0}|
| ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT    	|result; error_info  			|{"error_info":"waiting timeout, please check your network","result":0}|
| ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE    	|result; error_info; sub_event_type; new_room_type	|{"error_info":"","new_room_type":0,"result":0}|
| ITMG_MAIN_EVENT_TYPE_SPEAKER_NEW_DEVICE	|result; error_info  			|{"deviceID":"{0.0.0.00000000}.{a4f1e8be-49fa-43e2-b8cf-dd00542b47ae}","deviceName":"스피커(Realtek High Definition Audio)","error_info":"","isNewDevice":true,"isUsedDevice":false,"result":0}|
| ITMG_MAIN_EVENT_TYPE_SPEAKER_LOST_DEVICE    	|result; error_info  			|{"deviceID":"{0.0.0.00000000}.{a4f1e8be-49fa-43e2-b8cf-dd00542b47ae}","deviceName":"스피커 (Realtek High Definition Audio)","error_info":"","isNewDevice":false,"isUsedDevice":false,"result":0}|
| ITMG_MAIN_EVENT_TYPE_MIC_NEW_DEVICE    	|result; error_info  			|{"deviceID":"{0.0.1.00000000}.{5fdf1a5b-f42d-4ab2-890a-7e454093f229}","deviceName":"마이크 (Realtek High Definition Audio)","error_info":"","isNewDevice":true,"isUsedDevice":true,"result":0}|
| ITMG_MAIN_EVENT_TYPE_MIC_LOST_DEVICE    	|result; error_info 			|{"deviceID":"{0.0.1.00000000}.{5fdf1a5b-f42d-4ab2-890a-7e454093f229}","deviceName":"마이크 (Realtek High Definition Audio)","error_info":"","isNewDevice":false,"isUsedDevice":true,"result":0}|
| ITMG_MAIN_EVNET_TYPE_USER_UPDATE    		|user_list;  event_id			|{"event_id":1,"user_list":["0"]}|
| ITMG_MAIN_EVNET_TYPE_PTT_RECORD_COMPLETE 	|result; file_path  			|{"file_path":"","result":0}|
| ITMG_MAIN_EVNET_TYPE_PTT_UPLOAD_COMPLETE 	|result; file_path;file_id  		|{"file_id":"","file_path":"","result":0}|
| ITMG_MAIN_EVNET_TYPE_PTT_DOWNLOAD_COMPLETE	|result; file_path;file_id  		|{"file_id":"","file_path":"","result":0}|
| ITMG_MAIN_EVNET_TYPE_PTT_PLAY_COMPLETE 	|result; file_path  			|{"file_path":"","result":0}|
| ITMG_MAIN_EVNET_TYPE_PTT_SPEECH2TEXT_COMPLETE	|result; text;file_id		|{"file_id":"","text":"","result":0}|
| ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_COMPLETE	|result; file_path; text;file_id		|{"file_id":"","file_path":","text":"","result":0}|
