macOS 개발자가 Tencent Cloud GME(Game Multimedia Engine) 제품 API를 디버깅하고 연동하는 편의성을 위해 macOS 개발맞춤용 액세스 가이드를 소개합니다.

>이 문서는 GME sdk version：2.5  맞춤용입니다.

## GME 사용 시 주의할 점

|중요 API     | API 의미|
| ------------- |:-------------:|
|InitEngine           |GME 초기화 |
|Poll    |트리거 이벤트 콜백|
|EnterRoom |방 입장  |
|EnableMic |마이크 활성화 |
|EnableSpeaker|스피커 활성화 |

>
- GME 사용 전 프로그래밍을 설정하지 않으면 SDK가 적용되지 않습니다.
- GME의 API 호출 성공 후 리턴값은 QAVError.OK이며, 값은 0입니다.
- GME API 호출은 동일한 스레드에 있어야 합니다.
- GME 방 추가에는 인증이 필요하며, 가이드 중 인증 파트 내용을 참조하십시오.
- GME는 주기적으로 Poll API 트리거 콜백 이벤트를 호출해야 합니다.
- GME 콜백 정보는 콜백 정보 리스트를 참조하십시오.
- 디바이스 조작은 방 진입 성공 후에 해야합니다.
- 에러코드는 [에러코드](https://intl.cloud.tencent.com/document/product/607/15173)를 참조하십시오.

## 실시간 음성 채팅 순서도
![](https://main.qcloudimg.com/raw/810d0404638c494d9d5514eb5037cd37.png)


## 초기화 관련 인터페이스
초기화 전, SDK는 미초기화 단계이며, Init API를 통해 SDK를 초기화해야 실시간 음성채팅 및 오프라인 음성을 사용할 수 있습니다.
사용 문제는 [일반적인 문제](https://intl.cloud.tencent.com/document/product/607/30254)를 참조하십시오.

|인터페이스     | API 의미   |
| ------------- |:-------------:|
|InitEngine           |GME 초기화|
|Poll    |트리거 이벤트 콜백|
|Pause   |시스템 정지|
|Resume |시스템 복구|
|Uninit    |GME 초기화 취소 |

### 단일 항목 획득
음성 기능 사용 시, ITMGContext 객체를 먼저 획득해야 합니다.
####  함수 프로토타입 

```
ITMGContext ITMGDelegate <NSObject>
```



####  예시 코드  

```
ITMGContext* _context = [ITMGContext GetInstance];
_context.TMGDelegate =self;
```

### 메세지 전달
API류는 Delegate 방법으로 어플리케이션에 리턴 알림을 보내며, 메시지 유형은 ITMG_MAIN_EVENT_TYPE을 참조하며, 메시지 내용은 하나의 사전으로, 리턴된 메시지를 수신하는 데 사용됩니다.
#### 함수 프로토타입

```
- (void)OnEvent:(ITMG_MAIN_EVENT_TYPE)eventType data:(NSDictionary*)data
```



####  예시 코드  
```
-(void)OnEvent:(ITMG_MAIN_EVENT_TYPE)eventType data:(NSDictionary *)data{
    	NSLog(@"OnEvent:%lu,data:%@",(unsigned long)eventType,data);
		switch (eventType) {
			//eventType에 대한 판단
			}
	}
```





### SDK초기화

파라미터 획득은 [액세스 매뉴얼](https://intl.cloud.tencent.com/document/product/607/10782)을 참조하십시오.
이 API는 Tencent Cloud 제어 콘솔의 SDKAppID 를 파라미터로 사용해야 합니다. 여기에 openId를 추가하며 이 openId가 유일한 식별자입니다. 규칙은 App 개발자가 자체 작성하고 App 내에 중복하지 말아야 합니다(현재 INT64만 지원합니다).
>SDK초기화 후 방에 들어갈 수 있습니다.
>
>####  함수 프로토타입

```
ITMGContext -(int)InitEngine:(NSString*)sdkAppID openID:(NSString*)openId
```

|파라미터     | 타입         |의미|
| ------------- |:-------------:|-------------|
| sdkAppId    |NSString  |Tencent Cloud 제어 콘솔의 sdkAppId|
| openId    |NSString  |openId Int64 유형만 지원(string 전환 후 입력), 10000보다 커야하며, 사용자 식별에 사용|

####  예시 코드 


```
[[ITMGContext GetInstance] InitEngine:SDKAPPID3RD openID:_openId];
```
### 트리거 이벤트 콜백
update에 주기적인 Poll 호출을 통해 트리거 이벤트 콜백할 수 있습니다.
####  함수 프로토타입

```
ITMGContext -(void)Poll
```
####  예시 코드
```
[[ITMGContext GetInstance] Poll];
```

### 시스템 정지
시스템에 Pause 이벤트 발생시, 엔진에도 알려 Pause해야 합니다.
####  함수 프로토타입

```
ITMGContext -(QAVResult)Pause
```

### 시스템 복구
시스템에 Resume 이벤트 발생 시, 엔진에도 알려 Resume해야 합니다. Resume API는 실시간 음성채팅 복구만 합니다.
####  함수 프로토타입

```
ITMGContext -(QAVResult)Resume
```



### SDK 초기화 취소
SDK초기화 취소는 초기화 전 상태로 만듦니다. 계정 전환을 하려면 초기화 취소를 해야 합니다.
#### 함수 프로토타입

```
ITMGContext -(void)Uninit
```
####  예시 코드
```
[[ITMGContext GetInstance] Uninit];
```


## 실시간 음성 채팅 방 관련 API
초기화 후, SDK가 방 진입 호출 후 방에 들어가야 실시간 음성 채팅 통화를 할 수 있습니다.
사용 문제는 [실시간 음성 채팅 관련 문제](https://intl.cloud.tencent.com/document/product/607/30257)를 참조하십시오.

|API     | API 의미   |
| ------------- |:-------------:|
|GenAuthBuffer    |인증 초기화|
|EnterRoom   |방 입장|
|IsRoomEntered   |방 입장 여부|
|ExitRoom |방 퇴장|
|ChangeRoomType |사용자 방 오디오 유형 수정|
|GetRoomType |사용자 방 오디오 유형 획득|


### 인증 정보
AuthBuffer 생성은 관련 기능의 암호화와 인증에 사용되며, 관련 백엔드 배포는 [인증 키](https://intl.cloud.tencent.com/document/product/607/12218)를 참조하십시오.    
오프라인 음성 인증 획득 시, 방 번호 파라미터는 null이어야 합니다.

#### 함수 프로토타입
```
@interface QAVAuthBuffer : NSObject
+ (NSData*) GenAuthBuffer:(unsigned int)appId roomId:(NSString*)roomId openID:(NSString*)openID key:(NSString*)key;
+ @end
```
|파라미터     | 타입         |의미|
| ------------- |:-------------:|-------------|
| appId    |int   |Tencent Cloud 제어 콘솔의 sdkAppId|
| roomId    |NSString  |방번호, 최대 127바이트(오프라인 음성 방번호 파라미터는 null이어야 함)|
| openID  |NSString    |사용자 식별자|
| key    |NSString    |Tencent Cloud [제어 콘솔](https://console.cloud.tencent.com/gamegme) 의 키|


####  예시 코드  
```
NSData* authBuffer =   [QAVAuthBuffer GenAuthBuffer:SDKAPPID3RD.intValue roomId:_roomId openID:_openId key:AUTHKEY];
```



### 방 입장
생성된 인증 정보로 방에 진입하며, 수신 정보는 ITMG_MAIN_EVENT_TYPE_ENTER_ROOM의 콜백입니다. 진입한 방은 마이크와 스피커 끔 상태가 디폴트이며, 리턴값이 AV_OK 일 경우 성공입니다.


####  함수 프로토타입
```
ITMGContext   -(int)EnterRoom:(NSString*) roomId roomType:(int*)roomType authBuffer:(NSData*)authBuffer
```
|파라미터     | 타입         |의미|
| ------------- |:-------------:|-------------|
| roomId |NSString|방번호, 최대 127바이트까지 지원|
| roomType |int|방 오디오 유형|
| authBuffer    |NSData    |인증 코드|

방 오디오 유형은 [음질 선택](https://intl.cloud.tencent.com/document/product/607/18522)을 참조하십시오.


####  예시 코드  
```
[[ITMGContext GetInstance] EnterRoom:_roomId roomType:_roomType authBuffer:authBuffer];
```

### 방 입장 이벤트 콜백
방 입장 후 ITMG_MAIN_EVENT_TYPE_ENTER_ROOM 정보를 발송하며, OnEvent 함수에서 판단합니다.

####  예시 코드  
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

#### Data 상세정보
|메세지     | Data         |예시|
| ------------- |:-------------:|------------- |
| ITMG_MAIN_EVENT_TYPE_ENTER_ROOM    |result; error_info|{"error_info":"","result":0}|


### 방 입장 여부 판단
이 API호출을 통해 방 입장 여부 판단이 가능하며, 리턴값은 bool 유형 입니다.
####  함수 프로토타입  
```
ITMGContext -(BOOL)IsRoomEntered
```
####  예시 코드  
```
[[ITMGContext GetInstance] IsRoomEntered];
```

### 방 퇴장
이 API 호출을 통해 방 퇴장을 할 수 있습니다. 비동기화 API로 리턴값이 AV_OK일 경우 비동기화 발신 성공을 의미합니다.

>어플리케이션에서 방 퇴장 후 바로 입장하는 경우, API호출 프로세스 상, 개발자는 ExitRoom의 RoomExitComplete 리턴 알림을 기다릴 필요가 없으며, API를 바로 호출하기만 하면 됩니다.

#### 함수 프로토타입  
```
ITMGContext -(int)ExitRoom
```
####  예시 코드  
```
[[ITMGContext GetInstance] ExitRoom];
```

### 방 퇴장 콜백
방 퇴장 후 콜백이 있으며, 메세지는 ITMG_MAIN_EVENT_TYPE_EXIT_ROOM 입니다.
####  예시 코드  
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

#### Data 상세 정보
|메세지     | Data         |예시|
| ------------- |:-------------:|------------- |
| ITMG_MAIN_EVENT_TYPE_EXIT_ROOM    |result; error_info  |{"error_info":"","result":0}|


### 사용자 방 오디오 유형 수정
이 API는 사용자 방 오디오 유형 수정에 사용되며, 결과는 콜백 이벤트를 참고하며, 이벤트 유형은 ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE 입니다.
####  함수 프로토타입  
```
ITMGContext GetRoom -(void)ChangeRoomType:(int)nRoomType
```


|파라미터     | 타입         |의미|
| ------------- |:-------------:|-------------|
| nRoomType    |int    |희망하는 방 전환 유형, 방 오디오 유형은 EnterRoom API를 참고|

####  예시 코드  
```
[[[ITMGContext GetInstance]GetRoom ]ChangeRoomType:_roomType];
```


### 사용자 방 오디오 유형 획득
이 API는 사용자 방 오디오 유형 획득에 사용되며, 리턴값은 방 오디오 유형입니다. 리턴값이 0일 경우 사용자 방 오디오 유형 획득에 오류가 있음을 나타내며, 방 오디오 유형은 EnterRoom API를 참조하십시오.

####  함수 프로토타입  
```
ITMGContext GetRoom -(int)GetRoomType
```

####  예시 코드  
```
[[[ITMGContext GetInstance]GetRoom ]GetRoomType];
```


### 방 유형 완료 콜백
방 유형 세팅 완료 후, 콜백 이벤트 정보는 ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE로 리턴 파라미터는 result, error_info 및 new_room_type이며, new_room_type이 의미하는 정보는 아래와 같으며, OnEvent 함수 중 이벤트 정보에 대한 판단을 합니다.

|이벤트 서브 유형     | 대표 파라미터   |의미|
| ------------- |:-------------:|-------------|
| ITMG_ROOM_CHANGE_EVENT_ENTERROOM|1 |방에 진입하는 과정 중, 자체 오디오 유형과 방이 부합하지 않으며, 진입하려는 방 오디오 유형으로 수정되었음을 나타냄|
| ITMG_ROOM_CHANGE_EVENT_START|2|이미 방에 있으며 오디오 유형 변경 시작을 나타냄(예를 들어 ChangeRoomType API호출 후 오디오 유형 변경)|
| ITMG_ROOM_CHANGE_EVENT_COMPLETE|3|이미 방에 있으며, 오디오 유형 변경 완료를 나타냄|
| ITMG_ROOM_CHANGE_EVENT_REQUEST|4|방의 구성원이 ChangeRoomType API를 호출하여 방 오디오 유형 변경을 요청하는 것을 나타냄|


####  예시 코드  
```
-(void)OnEvent:(ITMG_MAIN_EVENT_TYPE)eventType data:(NSDictionary *)data {
	NSLog(@"OnEvent:%lu,data:%@",(unsigned long)eventType,data);
    switch (eventType) {
 		case ITMG_MAIN_EVNET_TYPE_USER_UPDATE:
			//처리하기
	 }
    }
}
```

#### Data 상세정보
|메세지     | Data         |예시|
| ------------- |:-------------:|------------- |
| ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE    |result; error_info; new_room_type|{"error_info":"","new_room_type":0,"result":0}|


### 구성원 상태 변화
해당 이벤트는 상태 변화시에만 알림을 보내며, 상태 변화가 없을 경우 알리지 않습니다. 실시간으로 구성원 상태를 획득해야 하는 경우 상단 레이어에서 알림을 받았을 때 캐시를 남겨야 하며, 이벤트 정보는 ITMG_MAIN_EVNET_TYPE_USER_UPDATE, 그 중 data가 포함하는 정보는 event_id와 user_list 두가지이며, OnEvent함수 중 해당 이벤트 정보에 대해 판단하게 됩니다.
오디오 이벤트 알림은 하나의 임계값이 있으며, 이 값을 초과하는 경우에만 알림을 발송합니다. 2초 초과후에도 오디오패키지를 받지 못한 경우 “구성원이 오디오패키지 발송을 중단했습니다”라는 알림을 보냅니다.

|event_id     | 의미         |어플리케이션측 관리 내용|
| ------------- |:-------------:|-------------|
|ITMG_EVENT_ID_USER_ENTER    |구성원 방 입장|어플리케이션측 관리 구성원 리스트|
|ITMG_EVENT_ID_USER_EXIT    |구성원 방 퇴장|어플리케이션측 관리 구성원 리스트|
|ITMG_EVENT_ID_USER_HAS_AUDIO    |구성원 오디오 패키지 발송|어플리케이션측 관리 통화 구성원 리스트|
|ITMG_EVENT_ID_USER_NO_AUDIO    |구성원 오디오 패키지 발송 중단|어플리케이션측 관리 통화 구성원 리스트|

#### 예시 코드  

```
-(void)OnEvent:(ITMG_MAIN_EVENT_TYPE)eventType data:(NSDictionary *)data{
    NSLog(@"OnEvent:%lu,data:%@",(unsigned long)eventType,data);
    switch (eventType) {
        case ITMG_MAIN_EVNET_TYPE_USER_UPDATE:
		{
		//프로세싱
		//개발자는 해당 파라미터를 해석하여 event_id 및 user_list 정보를 획득합니다.
		    switch (eventID)
 		    {
 		    case ITMG_EVENT_ID_USER_ENTER:
  			    //구성원 방 입장
  			    break;
 		    case ITMG_EVENT_ID_USER_EXIT:
  			    //구성원 방 퇴장
			    break;
		    case ITMG_EVENT_ID_USER_HAS_AUDIO:
			    //구성원 오디오 패키지 발송
			    break;
		    case ITMG_EVENT_ID_USER_NO_AUDIO:
			    //구성원 오디오 패키지 발송 중단
			    break;
 		    }
		break;
		}
    }
}
```

## 퀄리티 모니터링 이벤트
퀄리티 모미터링 이벤트, 이벤트 정보는 ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_QUALITY이며, 리턴 파라미터는 weight, floss  및 delay입니다. 나타내는 정보는 아래와 같으며, OnEvent 함수에서 해당 이벤트 정보에 대한 판단을 하게 됩니다.

|파라미터     | 의미         |
| ------------- |-------------|
|weight    |범위는 1-5이며, 값이 5이면 음질 평점 좋음, 1이면 음질 평점이 낮아 거의 사용할 수 없음을 나타내며, 0은 초기값으로 의미 없음|
|floss    |패킷 손실율|
|delay    |오디오 지연 시간(ms)|




### 메세지 상세 정보

|메세지     | 의미   
| ------------- |:-------------:|
|ITMG_MAIN_EVENT_TYPE_ENTER_ROOM           |비디오 방 입장 메세지|
|ITMG_MAIN_EVENT_TYPE_EXIT_ROOM             |비디오 방 퇴장 메세지|
|ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT           |방이 네트워크 등 이유로 연결이 끊김|
|ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE|방 유형 변화 이벤트|

### 메세지에 해당하는 Data 상세 정보
|메세지     | Data         |예시|
| ------------- |:-------------:|------------- |
| ITMG_MAIN_EVENT_TYPE_ENTER_ROOM    |result; error_info|{"error_info":"","result":0}|
| ITMG_MAIN_EVENT_TYPE_EXIT_ROOM    |result; error_info  |{"error_info":"","result":0}|
| ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT    |result; error_info  |{"error_info":"waiting timeout, please check your network","result":0}|
| ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE    |result; error_info; new_room_type|{"error_info":"","new_room_type":0,"result":0}|


## 실시간 음성 채팅 오디오 API
SDK 초기화 후 방에 진입해야 실시간 음성 채팅 관련 API 호출 가능합니다.
사용자 인터페이스에서 마이크/스피커 열기/닫기를 클릭할 때, 아래와 같은 방식을 권장합니다:
- 대부분의 게임류 App는 EnableMic 및 EnableSpeaker API 호출을 권장하며, 매번 EnableAudioCaptureDevice/EnableAudioSend와 EnableAudioPlayDevice/EnableAudioRecv API를 호출하는 것과 같습니다;
- 소셜 App와 같은 기타 유형 모바일 App은 열기 혹은 닫기 시 전체 디바이스가 (캡쳐 및 재생)가 재시작되며, 이때 App가 배경음악을 재생하고 있다면 배경음악 재생도 중단됩니다. 마이크 전원효과는 상하행 컨트롤 방식으로 구현하며, 디바이스 재생을 중단하지 않습니다. 구체적인 호출 방식은, 방 입장시 EnableAudioCaptureDevice(true) && EnableAudioPlayDevice(true)를 한번 호출하며, 마이크 전원 클릭 시 EnableAudioSend/Recv만 호출하는 방식으로 오디오 송/수신을 컨트롤 합니다.
- 단독으로 캡쳐 혹은 디바이스 재생을 릴리즈 하고자 할때 EnableAudioCaptureDevice 및 EnableAudioPlayDevice API를 참고하면 됩니다.
- pause 호출로 오디오 엔진을 중단하며, resume 호출로 오디오 엔진을 복구합니다.

|API     | API 의미   |
| ------------- |:-------------:|
|EnableMic    |마이크 전원|
|GetMicState    |마이크 상태 획득|
|EnableAudioCaptureDevice    |디바이스 캡쳐 전원|
|IsAudioCaptureDeviceEnabled    |디바이스 캡쳐 상태 획득|
|EnableAudioSend    |오디오 다운 스트림 끄기 활성화|
|IsAudioSendEnabled    |오디오 다운 스트림 상태 획득|
|GetMicLevel    |실시간 마이크 음량 획득|
|GetSendStreamLevel|오디오 다운 스트림 실시간 음량 획득|
|SetMicVolume    |마이크 음량 설정|
|GetMicVolume    |마이크 음량 획득|
|EnableSpeaker    |스피커 전원|
|GetSpeakerState    |스피커 상태 획득|
|EnableAudioPlayDevice    |재생 디바이스 전원|
|IsAudioPlayDeviceEnabled    |재생 디바이스 상태 획득|
|EnableAudioRecv    |오디오 업스트림 끄기 활성화|
|IsAudioRecvEnabled    |오디오 업스트림 상태 획득|
|GetSpeakerLevel    |실시간 스피커 음량 획득|
|GetRecvStreamLevel|방 내 기타 구성원 업스트림 실시간 음량 획득|
|SetSpeakerVolume    |스피커 음량 설정|
|GetSpeakerVolume    |스피커 음량 획득|
|EnableLoopBack    |인이어 모니터링 전원|



### 마이크 끄기 활성화
이 API는 마이크 끄기 활성화에 사용됩니다. 방 입장 시 마이크와 스피커 끔 상태가 디폴트 입니다.
EnableMic = EnableAudioCaptureDevice + EnableAudioSend.
####  함수 프로토타입  
```
ITMGContext GetAudioCtrl -(QAVResult)EnableMic:(BOOL)enable
```
|파라미터     | 타입         |의미|
| ------------- |:-------------:|-------------|
| isEnabled    |boolean     |마이크가 켜져있어야 하는 경우 입력되는 파라미터는 YES이고 마이크가 꺼져있으면 NO|

####  예시 코드  
```
[[[ITMGContext GetInstance] GetAudioCtrl] EnableMic:YES];
```

### 마이크 상태 획득
이 API는 마이크 상태 획득에 사용되며, 리턴값이 0일 경우 마이크 꺼짐 상태, 1일경우 마이크 겨짐 상태입니다.
####  함수 프로토타입  
```
ITMGContext GetAudioCtrl -(int)GetMicState
```
####  예시 코드  
```
[[[ITMGContext GetInstance] GetAudioCtrl] GetMicState];
```

### 디바이스 캡쳐 끄기 활성화
이 API는 디바이스 캡쳐 온오프에 사용됩니다. 방 입장시 꺼짐 상태가 디폴드값입니다.
- 방 입장후에만 이 API를 호출할 수 있으며, 퇴장시 자동으로 디바이스를 끕니다.
- 모바일에서 디바이스 캡쳐를 켜면 일반적으로 권한 신청을 하며, 음량유형 조정등 조작입니다.

####  함수 프로토타입  
```
ITMGContext GetAudioCtrl -(QAVResult)EnableAudioCaptureDevice:(BOOL)enabled
```
|파라미터     | 타입         |의미|
| ------------- |:-------------:|-------------|
| enabled    |BOOL     |디바이스 캡쳐를 켜야 하는 경우, 전송되는 파라미터는 YES, 끄면 NO|

#### 예시 코드

```
디바이스 캡쳐 켜기
[[[ITMGContext GetInstance]GetAudioCtrl ]EnableAudioCaptureDevice:enabled];
```

### 디바이스 캡쳐 상태 획득
이 API는 디바이스 캡쳐 상태 획득에 사용됩니다.
#### 함수 프로토타입

```
ITMGContext GetAudioCtrl -(BOOL)IsAudioCaptureDeviceEnabled
```
#### 예시 코드

```
BOOL IsAudioCaptureDevice = [[[ITMGContext GetInstance] GetAudioCtrl] IsAudioCaptureDeviceEnabled];
```

### 오디오 다운스트림 끄기 활성화
이 API는 오디오 다운스트림 온오프에 사용됩니다. 디바이스 캡쳐가 이미 켜져있다면 캡쳐한 오디오 데이터를 전송합니다. 디바이스 캡쳐가 꺼져있다면 소리가 없는 상태입니다. 디바이스 캡쳐의 온오프는 EnableAudioCaptureDevice API입니다.

#### 함수 프로토타입

```
ITMGContext GetAudioCtrl -(QAVResult)EnableAudioSend:(BOOL)enable
```
|파라미터     | 타입         |의미|
| ------------- |:-------------:|-------------|
| enable    |BOOL     |오디오 업스트림을 켜야한다면 파라미터는 YES, 오디오 다운스트림 끔은 NO|

#### 예시 코드  

```
[[[ITMGContext GetInstance]GetAudioCtrl ]EnableAudioSend:enabled];
```

### 오디오 다운스트림 상태 획득
이 API는 오디오 다운스트림 상태 획득에 사용됩니다.
#### 함수 프로토타입  
```
ITMGContext GetAudioCtrl -(BOOL)IsAudioSendEnabled
```
####  예시 코드  
```
BOOL IsAudioSend =  [[[ITMGContext GetInstance] GetAudioCtrl] IsAudioSendEnabled];
```

### 마이크 실시간 음량 획득
이 API는 마이크 실시간 음량 획득에 사용되며, 리턴값은 int유형입니다.
####  함수 프로토타입  
```
ITMGContext GetAudioCtrl -(int)GetMicLevel
```
####  예시 코드  
```
[[[ITMGContext GetInstance] GetAudioCtrl] GetMicLevel];
```

### 오디오 다운스트림 실시간 음량 획득
이 API는 오디오 다운스트림 실시간 음량에 사용되며 리턴값은 int유형, 값 범위는 0에서 100입니다.
####  함수 프로토타입  
```
ITMGContext GetAudioCtrl -(int)GetSendStreamLevel()
```
####  예시 코드  
```
[[[ITMGContext GetInstance] GetAudioCtrl] GetSendStreamLevel];
```

### 마이크 음량 설정
이 API는 마이크 음량 설정에 사용됩니다. 파라미터 volume은 마이크 음량 설정에 사용되며, 값이 0일 경우 무음, 값이 100일 경우 음량 변화 없음이며, 디폴트값은 100입니다.

####  함수 프로토타입  
```
ITMGContext GetAudioCtrl -(QAVResult)SetMicVolume:(int) volume
```
|파라미터     | 타입         |의미|
| ------------- |:-------------:|-------------|
| volume    |int      |음량 설정, 범위 0에서 200|

#### 예시 코드  
```
[[[ITMGContext GetInstance] GetAudioCtrl] SetMicVolume:100];
```
### 마이크 음량 획득
이 API는 마이크 음량 획득에 사용됩니다. 리턴값은 int유형이며, 리턴값이 101일 경우 SetMicVolume API를 호출한 적이 없음을 의미합니다.

#### 함수 프로토타입  
```
ITMGContext GetAudioCtrl -(int) GetMicVolume
```
####  예시 코드  
```
[[[ITMGContext GetInstance] GetAudioCtrl] GetMicVolume];
```

### 스피커 켜기/끄기
이 API는 스피커 켜기/끄기에 사용됩니다.
EnableSpeaker = EnableAudioPlayDevice +  EnableAudioRecv.
####  함수 프로토타입  
```
ITMGContext GetAudioCtrl -(void)EnableSpeaker:(BOOL)enable
```
|파라미터     | 타입         |의미|
| ------------- |:-------------:|-------------|
| isEnabled    |boolean       |스피커를 꺼야 하는 경우 파라미터 NO전송, 켜야하는 경우 YES|

####  예시 코드  
```
[[[ITMGContext GetInstance] GetAudioCtrl] EnableSpeaker:YES];
```

### 스피커 상태 획득
이 API는 스피커 상태 획득에 사용됩니다. 리턴값이 0일 경우 스피터 꺼짐 상태, 리턴값이 1일 경우 스피커 켜짐 상태, 리턴값이 2일 경우 스피커 디바이스 조작중입니다.
####  함수 프로토타입  
```
ITMGContext GetAudioCtrl -(int)GetSpeakerState
```

####  예시 코드  
```
[[[ITMGContext GetInstance] GetAudioCtrl] GetSpeakerState];
```



### 재생 디바이스 켜기/끄기
이 API는 재생 디바이스 켜기/끄기에 사용됩니다.

#### 함수 프로토타입  
```
ITMGContext GetAudioCtrl -(QAVResult)EnableAudioPlayDevice:(BOOL)enabled
```
|파라미터     | 타입         |의미|
| ------------- |:-------------:|-------------|
| enabled    |BOOL        |재생 디바이스를 꺼야 하는 경우, NO전송, 재생 디바이스를 켜야하는 경우 YES전송|

#### 예시 코드  
```
[[[ITMGContext GetInstance]GetAudioCtrl ]EnableAudioPlayDevice:enabled];
```

### 재생 디바이스 상태 획득
이 API는 재생 디바이스 상태 획득에 사용됩니다.
#### 함수 프로토타입

```
ITMGContext GetAudioCtrl -(BOOL)IsAudioPlayDeviceEnabled
```
#### 예시 코드  

```
BOOL IsAudioPlayDevice =  [[[ITMGContext GetInstance] GetAudioCtrl] IsAudioPlayDeviceEnabled];
```

### 오디오 업스트림 끄기 온오프
이 API는 오디오 업스트림 온오프에 사용됩니다. 재생 디바이스가 켜져있다면 방의 다른사람의 오디오 데이터를 재생하게됩니다. 재생 디바이스가 켜져있지 않다면, 아무소리도 나지 않습니다. 재생 디바이스의 온오프는 EnableAudioPlayDevice API를 확인하면 됩니다.

#### 함수 프로토타입  

```
ITMGContext GetAudioCtrl -(QAVResult)EnableAudioRecv:(BOOL)enabled
```
|파라미터     | 타입         |의미|
| ------------- |:-------------:|-------------|
| enabled    |BOOL     |오디오 업스트림을 켜려고 한다면 파라미터 YES전송, 오디오 업스트림을 끄려한다면 파라미터는 NO|

#### 예시 코드  

```
[[[ITMGContext GetInstance]GetAudioCtrl ]EnableAudioRecv:enabled];
```



### 오디오 업스트림 상태 획득
이 API는 오디오 업스트림 상태 획득에 사용됩니다.
#### 함수 프로토타입  
```
ITMGAudioCtrl bool IsAudioRecvEnabled()
```

####  예시 코드  
```
BOOL IsAudioRecv = [[[ITMGContext GetInstance] GetAudioCtrl] IsAudioRecvEnabled];
```

### 스피커 실시간 음량 획득
이 API는 스피커 실시간 음량 획득에 사용됩니다. 리턴값은 int유형이며, 스피커 실시간 음량을 나타냅니다.
####  함수 프로토타입  
```
ITMGContext GetAudioCtrl -(int)GetSpeakerLevel
```

####  예시 코드  
```
[[[ITMGContext GetInstance] GetAudioCtrl] GetSpeakerLevel];
```

### 방안의 기타 구성원 업스트림 실시간 음량 획득
이 API는 방안의 기타 구성원의 업스트림 실시간 음량 획득에 사용되며, 리턴값은 int유형, 값 범위는 0에서 100입니다.
####  함수 프로토타입  
```
ITMGContext GetAudioCtrl -(int)GetRecvStreamLevel:(NSString*) openID 
```

|파라미터     | 타입         |의미|
| ------------- |:-------------:|-------------|
| openID    |NSString       |방 기타 구성원의 openId|

####  예시 코드  
```
[[[ITMGContext GetInstance] GetAudioCtrl] GetRecvStreamLevel:(NSString*) openId
```

### 스피커 음량 설정
이 API는 스피커 음량 설정에 사용됩니다.
파라미터 volume은 스피커 음량 설정에 사용되며, 값이 0인 경우 무음, 값이 100인 경우 음량 변화 없음, 디폴트는 100입니다.

####  함수 프로토타입  
```
ITMGContext GetAudioCtrl -(QAVResult)SetSpeakerVolume:(int)vol
```
|파라미터     | 타입         |의미|
| ------------- |:-------------:|-------------|
| vol    |int        |음량 설정, 범위는 0에서 200|

#### 예시 코드  
```
[[[ITMGContext GetInstance] GetAudioCtrl] SetSpeakerVolume:100];
```

### 스피커 음량 획득

이 API는 스피커 음량 획득에 사용됩니다. 리턴값은 int유형, 스피커 음량을 의미하며, 리턴값이 101일 경우 SetSpeakerVolume API를 호출한 적이 없음을 의미합니다.
Level은 실시간 음량이며, Volume은 스피커 음량, 최종 사운드 음량은 Level*Volume%라고 할 수 있습니다. 예시: 실시간 음량값 100, Volume 60인 경우, 최종 사운드 값은 60입니다.

####  함수 프로토타입  
```
ITMGContext GetAudioCtrl -(int)GetSpeakerVolume
```
####  예시 코드  
```
[[[ITMGContext GetInstance] GetAudioCtrl] GetSpeakerVolume];
```


### 인이어 모니터링 활성화
이 API는 인이어 모니터링 활성화에 사용됩니다.
####  함수 프로토타입  
```
ITMGContext GetAudioCtrl -(QAVResult)EnableLoopBack:(BOOL)enable
```
|파라미터     | 타입         |의미|
| ------------- |:-------------:|-------------|
| enable    |boolean         |설정 활성화 여부|

####  예시 코드  
```
[[[ITMGContext GetInstance] GetAudioCtrl] EnableLoopBack:YES];
```


## 오프라인 음성 텍스트 변환 프로세스
![](https://main.qcloudimg.com/raw/9ef5e5e4ebc8e63bcd7bfbea6cfb94cc.png)



## 오프라인 음성
초기화 전, SDK는 미초기화 상태이며, Init API를 통해 SDK 를 초기화해야 실시간 음성 채팅 및 오프라인 음성을 사용할 수 있습니다.
사용 문제는 [오프라인 음성 관련 문제](https://intl.cloud.tencent.com/document/product/607/30258)를 참조하십시오.

### 관련 API초기화

|API     | API 의미   |
| ------------- |:-------------:|
|Init    |GME 초기화|
|Poll    |트리거 이벤트 콜백|
|Pause   |시스템 정지|
|Resume |시스템 복구|
|Uninit    |GME 초기화 취소 |


### 오프라인 음성 관련 API
|API     | API 의미   |
| ------------- |:-------------:|
|ApplyPTTAuthbuffer    |인증 초기화|
|SetMaxMessageLength    |음성 메세지 최대 시간 제한|
|StartRecording|녹음 시작|
|StartRecordingWithStreamingRecognition|스트리밍 녹음 시작|
|PauseRecording|녹음 일시정지|
|ResumeRecording|녹음 복구|
|StopRecording    |녹음 정지|
|CancelRecording|녹음 취소|
|GetMicLevel|오프라인 음성 실시간 마이크 음량 획득|
|SetMicVolume|오프라인 음성 녹음 음량 설정|
|GetMicVolume|오프라인 음성 녹음 음량 획득|
|GetSpeakerLevel|오프라인 음성 실시간 스피커 음량 획득  |
|SetSpeakerVolume|오프라인 음성 재생 음량 설정|
|GetSpeakerVolume|오프라인 음성 재생 음량 획득|
|UploadRecordedFile |음성 파일 업로드|
|DownloadRecordedFile|음성 파일 다운로드|
|PlayRecordedFile |음성 재생|
|StopPlayFile|음성 재생 정지|
|GetFileSize |음성 파일 사이즈|
|GetVoiceFileDuration|음성 파일 시간|
|SpeechToText |음성을 텍스트로 식별|

### 인증 초기화
SDK초기화 후 인증 초기화 호출을 하며, authBuffer의 획득은 실시간 음성 인증 정보 API를 확인하면 됩니다.
#### 함수 프로토타입  
```
ITMGContext GetPTT -(QAVResult)ApplyPTTAuthbuffer:(NSData *)authBuffer
```
|파라미터     | 타입         |의미|
| ------------- |:-------------:|-------------|
| authBuffer    |NSData*                    |인증|

#### 예시 코드  
```
[[[ITMGContext GetInstance]GetPTT]ApplyPTTAuthbuffer:(NSData *)authBuffer];
```

### 최대 보이스 메세지 시간 제한
최대 보이스 메세지 길이 제한은 60초까지 지원합니다.

#### 함수 프로토타입

```
ITMGContext GetPTT -(QAVResult)SetMaxMessageLength:(int)msTime
```
|파라미터     | 타입         |의미|
| ------------- |:-------------:|-------------|
| msTime    |int                    |보이스 시간, 단위 ms|

#### 예시 코드  
```
[[[ITMGContext GetInstance]GetPTT]SetMaxMessageLength:(int)msTime];
```


### 녹음 활성화
이 API는 녹음 활성화에 사용됩니다. 녹음 파일을 업로드해야 녹음 파일을 텍스트로 변환하는 등의 작업이 가능합니다.
####  함수 프로토타입  
```
ITMGContext GetPTT -(int)StartRecording:(NSString*)fileDir
```
|파라미터     | 타입         |의미|
| ------------- |:-------------:|-------------|
| fileDir    |NSString                     |음성 저장 경로|

####  예시 코드  
```
[[[ITMGContext GetInstance]GetPTT]StartRecording:path];
```

### 녹음 콜백 활성화
녹음이 완료된 후 세션용 함수 OnEvent를 작동, 이벤트 메세지는 ITMG_MAIN_EVNET_TYPE_PTT_RECORD_COMPLETE, OnEvent 함수에서 이벤트를 판단합니다
전달된 파라미터에는 두 가지 정보가 포함되어 있으며, 하나는 result이고 다른 하나는 file_path입니다.

#### 오류코드
|오류코드 값 |원인  |권장 방안        |
|-----|------|------|
|4097   |파라미터가 빈 값|코드 중 API 파라미터가 정확한지 검사|
|4098   |초기화 오류|디바이스가 사용중인지 검사, 혹은 권한 정상 여부, 초기화 정상 여부 확인|
|4099   |녹음 중|정확한 시기에 SDK녹음 기증을 사용한 것인지 확인|
|4100   |캡쳐한 오디오 데이터 없음|마이크 디바이스 정상 여부 확인|
|4101   |녹음시 녹음 파일 접근 오류|파일 존재 확인, 파일 경로 정확성|
|4102   |마이크 권한 오류|SDK를 사용하려면 마이크 권한이 필요하며 권한 추가는 엔진 또는 플랫폼에 대응하는 SDK 세팅 문서를 참조하십시오|
|4103   |녹음 시간이 너무 짧은 오류|우선, 녹음시간 제한 단위는 밀리초이며, 파라미터가 올바른지 검사합니다. 녹음할 때 1,000밀리초 이상 걸려야 녹음에 성공할 수 있습니다.|
|4104   |녹음 조작 활성화하지 않음|녹음 활성화 API 호출 했는지 여부 검사|

####  예시 코드  
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

### 스트림 음성 인식(ASR) 활성화
이 API는 스트림 음성인식(ASR)활성화에 사용되며, 동시에 콜백 중 실시간 음성 텍스트 변환 리턴이 있고, 지정한 음성을 식별할 수 있습니다. 또한 음성에서 식별한 정보를 지정한 언어로 번역하여 리턴 가능합니다.

#### 함수 프로토타입  

```
ITMGContext GetPTT -(void) StartRecordingWithStreamingRecognition(const NSString* filePath)
ITMGContext GetPTT -(void) StartRecordingWithStreamingRecognition(const NSString* filePath,const NSString*speechLanguage,const NSString*translateLanguage)
```
|파라미터     | 타입         |의미|
| ------------- |:-------------:|-------------|
| filePath    |NSString* |음성 저장 경로|
| speechLanguage    |NSString*                     |지정한 텍스트로 식별하는 언어 파라미터입니다. 파라미터는 [음성 텍스트 변환의 언어 파라미터 리스트](https://intl.cloud.tencent.com/document/product/607/30260)를 참조하십시오|
| translateLanguage    |NSString*                     |지정한 텍스트로 번역하는 언어 파라미터입니다. 파라미터는 [음성 텍스트 변환의 언어 파라미터 리스트](https://intl.cloud.tencent.com/document/product/607/30260)를 참조하십시오(이 파라미터는 현재 사용불가하며 speechLanguage와 동일한 파라미터를 입력하십시오)|

#### 예시 코드  
```
[[[ITMGContext GetInstance] GetPTT] StartRecordingWithStreamingRecognition:recordfilePath  speechLanguage:@"cmn-Hans-CN" translateLanguage:@"cmn-Hans-CN"];
```

### 스트림 음성 인식(ASR) 콜백 활성화
스트림 음성 인식이 완료된 후의 세션용 함수 OnEvent, 이벤트 정보는 ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_COMPLETE에서 판단합니다. 전달된 파라미터에는 다음과 같은 네 가지 정보가 포함되어 있습니다.

|정보 명칭     | 의미         |
| ------------- |:-------------:|
| result    |스트림 음성인식 성공 판단에 사용되는 리턴코드|
| text    |음성 텍스트 변환으로 식별된 텍스트|
| file_path |녹음이 저장된 로컬 주소|
| file_id |백엔드의 녹음 url주소|

|오류 코드     | 의미         |처리방식|
| ------------- |:-------------:|:-------------:|
|32775|스트림 음성 텍스트 변환 실패, 단 녹음은 성공|UploadRecordedFile API 호출로 녹음 업로드 후 SpeechToText API 호출로 음성 텍스트 변환 작업|
|32777|스트림 음성 텍스트 변환 실패, 단 녹음은 성공, 업로드 성공|리턴 정보에 업로드에 성공한 백엔드 url주소가 있으며, SpeechToText API 호출로 음성 텍스트 변환 작업|

#### 예시 코드  
```
-(void)OnEvent:(ITMG_MAIN_EVENT_TYPE)eventType data:(NSDictionary *)data{
    NSLog(@"OnEvent:%lu,data:%@",(unsigned long)eventType,data);
    switch (eventType) {
        case ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_COMPLETE：
        {
	    //스트림 음성 인식(ASR) 콜백 활성화
        }
            break;
    }
}
```
### 녹음 일시정지
이 API는 녹음 일시정지에 사용됩니다. 녹음 복구를 해야하는 경우 ResumeRecording API를 호출하면 됩니다.

#### 함수 프로토타입  
```
ITMGContext GetPTT int PauseRecording()
```
####  예시 코드  
```
[[[ITMGContext GetInstance]GetPTT]PauseRecording;
```

### 녹음 복구
이 API는 녹음 복구에 사용됩니다.

#### 함수 프로토타입  
```
ITMGContext GetPTT int ResumeRecording()
```
####  예시 코드  
```
[[[ITMGContext GetInstance]GetPTT]ResumeRecording;
```


### 녹음 정지
이 API는 녹음 정지에 사용됩니다. 비동기 API로 녹음 정지 후 녹은 완료 콜백이 있으며, 성공 후 녹음 파일을 사용할 수 있습니다.
#### 함수 프로토타입  
```
ITMGContext GetPTT -(QAVResult)StopRecording
```
####  예시 코드  
```
[[[ITMGContext GetInstance]GetPTT]StopRecording];
```



### 녹음 취소
이 API는 녹음 취소에 사용됩니다. 취소 후 콜백이 없습니다.
#### 함수 프로토타입  
```
ITMGContext GetPTT -(QAVResult)CancelRecording
```
####  예시 코드  
```
[[[ITMGContext GetInstance]GetPTT]CancelRecording];
```

### 오프라인 음성 마이크 실시간 음량 획득
이 API는 마이크 실시간 음량 획득에 사용되며, 리턴값은 int유형, 범위는 0에서 100입니다.

#### 함수 프로토타입  
```
ITMGContext GetPTT -(QAVResult)GetMicLevel
```
#### 예시 코드  
```
[[[ITMGContext GetInstance]GetPTT]GetMicLevel];
```

### 오프라인 음성 녹음 음량 설정
이 API는 오프라인 음성 녹음 음량 설정에 사용되며, 값은 0에서 100입니다.

#### 함수 프로토타입  
```
ITMGContext GetPTT int SetMicVolume:(int) vol
```
#### 예시 코드  
```
[[[ITMGContext GetInstance]GetPTT]SetMicVolume:100];
```

### 오프라인 음성 녹음 음량 획득
이 API는 오프라인 음성 녹음 음량 획득에 사용됩니다. 리턴값은 int유형이며, 값은 0에서 100입니다.

#### 함수 프로토타입  
```
ITMGContext GetPTT int GetMicVolume()
```

#### 예시 코드  
```
[[[ITMGContext GetInstance]GetPTT]GetMicVolume];
```


### 스피커 실시간 음량 획득
이 API는 스피커 실시간 음량 획득에 사용됩니다. 리턴값은 int유형이며, 값은 0에서 100입니다.

#### 함수 프로토타입  
```
ITMGContext GetPTT -(QAVResult)GetSpeakerLevel
```

#### 예시 코드  
```
[[[ITMGContext GetInstance]GetPTT]GetSpeakerLevel];
```

### 오프라인 음성 재생 음량 설정
이 API는 오프라인 음성 재생 음량 설정에 사용되며, 값은 0에서 100입니다.

#### 함수 프로토타입  
```
ITMGContext GetPTT int SetSpeakerVolume:(int) vol
```
#### 예시 코드  
```
[[[ITMGContext GetInstance]GetPTT]SetSpeakerVolume:100];
```

### 오프라인 음성 재생 음량 획득
이 API는 오프라인 음성 재생 음량 획득에 사용됩니다. 리턴값은 int유형이며, 값은 0에서 100입니다.

#### 함수 프로토타입  
```
ITMGContext GetPTT int GetSpeakerVolume()
```

#### 예시 코드  
```
[[[ITMGContext GetInstance]GetPTT]GetSpeakerVolume];
```




### 음성 파일 업로드
이 API는 음성파일 업로드에 사용됩니다.
#### 함수 프로토타입  
```
ITMGContext GetPTT -(void)UploadRecordedFile:(NSString*)filePath 
```
|파라미터     | 타입         |의미|
| ------------- |:-------------:|-------------|
| filePath    |NSString                      |업로드한 음성 경로|

#### 예시 코드  
```
[[[ITMGContext GetInstance]GetPTT]UploadRecordedFile:path];
```


### 음성 업로드 완료 콜백
음성 업로드 완료 후, 이벤트 정보는 ITMG_MAIN_EVNET_TYPE_PTT_UPLOAD_COMPLETE, OnEvent함수에서 해당 이벤트에 대한 판단을 합니다.
#### 오류코드

|오류코드 값 |원인  |권장 방안        |
|-----|------|------|
|8193   |파일 업로드시, 파일 접근 오류|파일 존재 확인, 파일 경로 정확성 확인|
|8194   |서명 교정 실패 오류|인증 키가 정확한지 점검하고, 초기화된 오프라인 음성이 있는지 점검|
|8195   |네트워크 오류|네크워크가 정상적으로 외부 망을 방문할 수 있는지 점검|
|8196   |업로드 파라미터 획득 중 네트워크 실패|인증이 정확한지 점검하고 디바이스 네트워크가 외부 망을 방문할 수 있는지 점검|
|8197   |업로드 파라미터 획득 중 롤백 데이터가 비어 있음|인증이 정확한지 점검하고 디바이스 네트워크가 외부 망을 방문할 수 있는지 점검|
|8198   |업로드 파라미터 획득 중 롤백 해제 실패|인증이 정확한지 점검하고 디바이스 네트워크가 외부 망을 방문할 수 있는지 점검|
|8200   |appinfo 설정 안함|apply API가 호출되었는지 점검하거나 파라미터가 비어있는지 점검|

#### 예시 코드

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


### 음성파일 다운로드
이 API는 음성파일 다운로드에 사용됩니다.
#### 함수 프로토타입  
```
ITMGContext GetPTT -(void)DownloadRecordedFile:(NSString*)fileId downloadFilePath:(NSString*)downloadFilePath 
```
|파라미터     | 타입         |의미|
| ------------- |:-------------:|-------------|
| fileID    |NSString                      |파일 url 경로|
| downloadFilePath |NSString                      |파일의 로컬 저장 경로|

####  예시 코드  
```
[[[ITMGContext GetInstance]GetPTT]DownloadRecordedFile:fileIdpath downloadFilePath:path];
```


### 음성파일 다운로드 완료 콜백
음성파일 다운로드가 완료 후, 이벤트 정보는 ITMG_MAIN_EVNET_TYPE_PTT_DOWNLOAD_COMPLETE로 OnEvent 함수에서 이벤트 정보를 판단합니다.
전달된 파라미터는 3개의 정보를 포함하고 있습니다, result, file_path 및 file_id.
#### 오류코드

|오류코드 값 |원인  |권장 방안        |
|-----|------|------|
|12289  |파일 다운로드시 파일 접근 오류   |파일 경로가 올바른지 점검|
|12290  |서명 교정 실패    |인증키가 올바른지 점검하고 오프라인 음성 초기화 여부 점검|
|12291  |네크워크 저장 시스템 이상    |서버에서 음성 파일 획득 실패, API함수 fileid가 올바른지 점검하고 네트워크 환경, cos파일 존재여부 점검|
|12292  |서버 문서 시스템 오류    |디바이스 네트워크가 외부 망에 방문할 수 있는지를 점검하고 서버상에 해당 파일이 있는지 확인|
|12293  |다운로드 파라미터를 얻는 중 HTTP 네트워크 실패|디바이스 네트워크가 외부 망에 방문할 수 있는지를 점검|
|12294  |다운로드 파라미터를 얻는 중 롤백 데이터가 빈값 |디바이스 네트워크가 외부 망에 방문할 수 있는지를 점검|
|12295  |다운로드 파라미터를 얻는 중 롤백 해제 실패|디바이스 네트워크가 외부 망에 방문할 수 있는지를 점검|
|12297  |appinfo설정 안함|인증키가 올바른지 점검하고 오프라인 음성 초기화 여부 점검|


#### 예시 코드

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
이 API는 음성 재생에 사용됩니다.
####  함수 프로토타입  
```
ITMGContext GetPTT -(void)PlayRecordedFile:(NSString*)downloadFilePath
```
|파라미터     | 타입         |의미|
| ------------- |:-------------:|-------------|
| downloadFilePath    |NSString                      |파일 경로|

#### 오류코드

|오류코드 값 |원인  |권장 방안        |
|-----|------|------|
|20485  |재생 미시작|파일 존재여부 확인, 문서 경로가 올바른지 확인|

####  예시 코드  
```
[[[ITMGContext GetInstance]GetPTT]PlayRecordedFile:path];
```


### 음성 재생 콜백
음성 재생 콜백으로, 이벤트 정보는 ITMG_MAIN_EVNET_TYPE_PTT_PLAY_COMPLETE, OnEvent함수에서 해당 이벤트 정보를 판단합니다.
전달된 파라미터는 2가지 정보가 포함되어 있으며, 하나는 result, 다른 하나는 file_path입니다.

#### 오류코드

|오류코드 값 |원인  |권장 방안        |
|-----|------|------|
|20481  |초기화 오류|장치가 사용중인지, 또는 권한이 정상인지, 초기화가 정상인지 점검|
|20482  |재생 중, 차단 시도 및 다음 파일 재생에 실패했습니다(정상적으로는 차단 가능)|코드 알고리즘이 정상인지 확인|
|20483  |파라미터가 빈값|코드의 API 파라미터가 정확한지 확인|
|20484  |내부 오류|플레이어 초기화 오류, 해시 실패 등의 문제가 이 오류를 야기, 로그를 통해 문제 확인 필요|

#### 예시 코드

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




### 음성 재생 정지
이 API는 음성 재생 정지에 사용됩니다. 음성재생 정지에는 재생 완료 콜백이 있을 수 있습니다.
####  함수 프로토타입  
```
ITMGContext GetPTT -(int)StopPlayFile
```

####  예시 코드  
```
[[[ITMGContext GetInstance]GetPTT]StopPlayFile];
```



### 음성 파일 사이즈 획득
이 API를 통해 음성 파일 사이즈를 획득할 수 있습니다.
####  함수 프로토타입  
```
ITMGContext GetPTT -(int)GetFileSize:(NSString*)filePath
```
|파라미터     | 타입         |의미|
| ------------- |:-------------:|-------------|
| filePath    |NSString                     |음성 파일 경로|

####  예시 코드  
```
[[[ITMGContext GetInstance]GetPTT]GetFileSize:path];
```

### 음성 파일 시간 획득
이 API는 음성파일 시간 획득에 사용되며, 단위는 ms입니다.
####  함수 프로토타입  
```
ITMGContext GetPTT -(int)GetVoiceFileDuration:(NSString*)filePath
```
|파라미터     | 타입         |의미|
| ------------- |:-------------:|-------------|
| filePath    |NSString                     |음성 파일 경로|

####  예시 코드  
```
[[[ITMGContext GetInstance]GetPTT]GetVoiceFileDuration:path];
```


### 지정한 음성 파일을 텍스트로 식별
이 API는 지정한 음성 파일을 텍스트로 식별하는데 사용됩니다.

#### 함수 프로토타입  
```
ITMGContext GetPTT -(void)SpeechToText:(NSString*)fileID
```
|파라미터     | 타입         |의미|
| ------------- |:-------------:|-------------|
| fileID    |NSString                     |음성 파일 url|

#### 예시 코드  
```
[[[ITMGContext GetInstance]GetPTT]SpeechToText:fileID];
```



### 지정한 음성 파일을 텍스트로 번역(지정한 언어)
이 API는 지정한 음성 식별을 할 수 있으며, 음성중 식별한 정보를 지정한 언어로 번역하여 리턴할 수 있습니다.

#### 함수 프로토타입  
```
ITMGContext GetPTT -(void)SpeechToText:(NSString*)fileID (NSString*)speechLanguage (NSString*)translateLanguage
```
|파라미터     | 타입         |의미|
| ------------- |:-------------:|-------------|
| fileID    |NSString                     |음성 파일 url|
| speechLanguage    |NSString*                     |지정한 텍스트를 식별하는 언어 파라미터, [음성 텍스타 변환의 언어 파라미터 리스트]를(https://intl.cloud.tencent.com/document/product/607/30260)참고하십시오|
| translatelanguage    |NSString*                     |지정 텍스트로 번역한 언어 파라미터, [음성 텍스트 변환의 언어 파라미터 리스트](https://intl.cloud.tencent.com/document/product/607/30260)를 참고하십시오(이 파라미터는 현재 무효하며, 입력한 파라미터는 speechLanguage와 일치해야 합니다)|

#### 예시 코드  
```
[[[ITMGContext GetInstance]GetPTT]SpeechToText:fileID speechLanguage:"cmn-Hans-CN" translateLanguage:"cmn-Hans-CN"];
```



### 식별 콜백
지정한 음성 파일을 텍스트로 인식한 콜백, 이벤트 정보는 ITMG_MAIN_EVNET_TYPE_PTT_SPEECH2TEXT_COMPLETE. OnEvent 함수에서 판단합니다.
전달된 파라미터에 포함된 3가지 정보, result, file_path 및 text, 그 중 text가 식별된 텍스트 입니다.

#### 오류코드

|오류코드 값 |원인  |권장 방안        |
|-----|------|------|
|32769  |내부 오류|로그 분석, 백엔드에서 클라이언트로 리턴한 오류코드 획득 후 백엔드 담당자와 해결|
|32770  |네트워크 실패|디바이스 네트워크가 외부 망을 방문할 수 있는지 점검|
|32772  |롤백 해제 실패|로그 분석, 백엔드에서 클라이언트로 리턴한 오류코드 획득 후 백엔드 담당자와 해결|
|32774  |appinfo 세팅 안함|인증키가 정확한지 확인, 오프라인 음성 초기화 여부 확인|
|32776  |authbuffer 교정 실패|authbuffer 가 정확한지 확인|
|32784  |음성 텍스트 변환 파라미터 오류|코드 중 fileid API 파라미터가 비어있는지 확인|
|32785  |음성 텍스트 변환 번역 리턴 오류|오프라인 음성 백엔드 오류, 로그 분석, 백엔드에서 클라이언트로 리턴한 오류코드 획득 후 백엔드 담당자와 해결|

#### 예시 코드

```
-(void)OnEvent:(ITMG_MAIN_EVENT_TYPE)eventType data:(NSDictionary *)data{
    NSLog(@"OnEvent:%lu,data:%@",(unsigned long)eventType,data);
    switch (eventType) {
        case ITMG_MAIN_EVNET_TYPE_PTT_SPEECH2TEXT_COMPLETE：
        {
	    //음성 파일 식별 성공       
        }
            break;   
    }
}
```



## 고급 API

### 버전 번호 획득
SDK버전 번호 획득, 분석에 사용됩니다.
#### 함수 프로토타입
```
ITMGContext  -(NSString*)GetSDKVersion
```
#### 예시 코드  
```
[[ITMGContext GetInstance] GetSDKVersion];
```

### 로그 출력 레벨 설정
로그 출력 레벨 설정에 사용되며, 디폴트값 유지를 권장합니다.
#### 함수 프로토타입
```
ITMGContext -(void)SetLogLevel:(ITMG_LOG_LEVEL)levelWrite (ITMG_LOG_LEVEL)levelPrint
```

#### 파라미터의미

|파라미터|타입|의미|
|---|---|---|
|levelWrite|ITMG_LOG_LEVEL|로그 입력 레벨 설정, TMG_LOG_LEVEL_NONE 는 입력하지 않음을 뜻함|
|levelPrint|ITMG_LOG_LEVEL|로그 출력 레벨 설정, TMG_LOG_LEVEL_NONE 는 출력 하지 않음을 뜻함|



|ITMG_LOG_LEVEL|의미|
| -------------------------------|----------------------|
|TMG_LOG_LEVEL_NONE=0|로그 출력하지 않음|
|TMG_LOG_LEVEL_ERROR=1|오류 로그 출력(디폴트)|
|TMG_LOG_LEVEL_INFO=2|안내 로그 출력|
|TMG_LOG_LEVEL_DEBUG=3|개발 디버깅 로그 출력|
|TMG_LOG_LEVEL_VERBOSE=4|고빈도 로그 출력|

#### 예시 코드  
```
[[ITMGContext GetInstance] SetLogLevel:TMG_LOG_LEVEL_INFO TMG_LOG_LEVEL_INFO];
```



### 로그 출력 경로 설정
로그 출력 경로 설정에 사용됩니다. 디폴트 경로는 /Users/username/Library/Containers/xxx.xxx.xxx/Data/Documents 입니다.
#### 함수 프로토타입
```
ITMGContext -(void)SetLogPath:(NSString*)logDir
```

|파라미터     | 타입         |의미|
| ------------- |:-------------:|-------------|
| logDir    |NSString   |경로|

#### 예시 코드  
```
[[ITMGContext GetInstance] SetLogPath:Path];
```


### 진단 정보 획득
보이스 비디오 통화 실시간 통화 품질 관련 정보 획득입니다. 해당 API는 주로 실시간 통화 품질 확인 및 문제 확인에 사용되며, 서비스측은 무시해도 됩니다.
#### 함수 프로토타입  
```
ITMGContext GetRoom -(NSString*)GetQualityTips
```
#### 예시 코드  
```
[[[ITMGContext GetInstance]GetRoom ] GetQualityTips];
```

### 오디오 데이터 블랙리스트 추가
특정 ID를 오디오 데이터 블랙리스트에 추가합니다. 리턴값이 0이면 호출 성공을 의미합니다.
#### 함수 프로토타입  

```
ITMGContext GetAudioCtrl -(QAVResult)AddAudioBlackList:(NSString*)openID
```
|파라미터     | 타입         |의미|
| ------------- |:-------------:|-------------|
| openId    |NSString      |블랙리스트에 추가할 ID|

#### 예시 코드  

```
[[[ITMGContext GetInstance]GetAudioCtrl ] AddAudioBlackList[id]];
```

### 오디오 데이터 블랙리스트 제거
특정 ID를 오디오 데이터 블랙리스트에서 제거합니다. 리턴값이 0이면 호출 성공을 의미합니다.
#### 함수 프로토타입  

```
ITMGContext GetAudioCtrl -(QAVResult)RemoveAudioBlackList:(NSString*)openID
```
|파라미터     | 타입         |의미|
| ------------- |:-------------:|-------------|
| openId    |NSString      |블랙리스트에서 제거할 ID|

#### 예시 코드  

```
[[[ITMGContext GetInstance]GetAudioCtrl ] RemoveAudioBlackList[openId]];
```


## 콜백 정보

### 메세지 리스트

|메세지     | 메세지 의미   |
| ------------- |:-------------:|
|ITMG_MAIN_EVENT_TYPE_ENTER_ROOM    |오디오 방 입장 메세지|
|ITMG_MAIN_EVENT_TYPE_EXIT_ROOM    |오디오 방 퇴장 메세지|
|ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT|네트워크 등의 원인으로 방 연결 끊김|
|ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE|방 타입 변경 이벤트|
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
