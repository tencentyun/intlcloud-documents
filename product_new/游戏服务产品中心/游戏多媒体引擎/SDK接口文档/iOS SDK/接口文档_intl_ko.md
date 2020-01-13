iOS 개발자가 Tencent Cloud GME(Game Multimedia Engine) 제품인 API를 액세스  및 디버깅에 편의를 제공하기 위해  iOS 개발에 적용되는 액세스 기술문서를 소개드립니다.

>이 문서는 GME sdk version:2.5 에 적용됩니다.

## GME 사용 시 중요 사항

|중요 인터페이스     | 인터페이스 의미|
| ------------- |:-------------:|
|InitEngine           |GME 초기화 |
|Poll    |트리거 이벤트 콜백|
|SetDefaultAudienceAudioCategory |백엔드 설정|
|EnterRoom |방 들어가기  |
|EnableMic |마이크 켜기 |
|EnableSpeaker|스피커 켜기 |

>
- GME 를 사용하기 전에 공정에 대한 배치를 진행하십시오, 그렇지 않으면 SDK 효력이 발생하지 않습니다.
- GME 의 인터페이스 호출이 성공적으로 완료된 후의 리턴값은 QAVERror.OK 이며, 수치는 0입니다.
- GME 의 인터페이스 호출은 동일한 스레드 아래 있어야 합니다.
- GME 의 방 추가는 인증이 필요하므로, 인증 내용 관련 문서를 참조하십시오.
- GME 는 주기적인 Poll 인터페이스 트리거 이벤트 콜백이 필요합니다.
- GME 콜백 정보는 콜백된 메시지 목록을 참조하십시오.
- 디바이스의 작동은 방 들어가기 성공 후에 하여야 합니다.
- 에러코드 관련 상세 사항은 [에러코드](https://intl.cloud.tencent.com/document/product/607/15173)를 참조하십시오

## 실시간 음성 채팅 순서도
![](https://main.qcloudimg.com/raw/810d0404638c494d9d5514eb5037cd37.png)


## 초기화 관련 인터페이스
초기화하기 전, SDK가 초기화되지 않은 단계로 인터페이스 Init를 통해 SDK를 초기화해야 실시간 음성 및 오프라인 음성을 사용할 수 있습니다.
사용 중 궁금한 사항은 [일반 문제](https://intl.cloud.tencent.com/document/product/607/30254)를 참조하십시오.

|인터페이스     | 인터페이스 의미   |
| ------------- |:-------------:|
|InitEngine           |GME 초기화 |
|Poll    |트리거 이벤트 콜백|
|Pause   |시스템 일시정지|
|Resume |시스템 복구|
|Uninit    |GME 초기화 취소 |
|SetDefaultAudienceAudioCategory |디바이스 백엔드 소리 재생 설정|

### 단일 항목 획득
음성 기능을 사용할 때는 먼저 ITMGContext 오브젝트를 획득해야 합니다.
####  함수 프로토타입 

```
ITMGContext ITMGDelegate <NSObject>
```



####  예시 코드  

```
ITMGContext* _context = [ITMGContext GetInstance];
_context.TMGDelegate =self;
```

### 메시지 전달
인터페이스 류는 Delegate 방법으로 응용프로그램에 콜백 알림을 보내는데 사용되며, 메시지 유형은 ITMG_MAIN_EVENT_TYPE을 참조하십시오. 메시지 내용은 하나의 사전으로 콜백된 메시지를 수신하는데 사용됩니다.
#### 함수 프로토타입

```
- (void)OnEvent:(ITMG_MAIN_EVENT_TYPE)eventType data:(NSDictionary*)data
```



####  예시 코드  
```
-(void)OnEvent:(ITMG_MAIN_EVENT_TYPE)eventType data:(NSDictionary *)data{
    	NSLog(@"OnEvent:%lu,data:%@",(unsigned long)eventType,data);
		switch (eventType) {
			//eventType 판단
			}
	}
```





### SDK 초기화

파라미터를 획득하려면 [액세스 매뉴얼](https://intl.cloud.tencent.com/document/product/607/10782)을 참조하십시오.
이 인터페이스는 Tencent Cloud 제어 콘솔의 SDKAppID 번호를 파라미터로 사용해야 하며, 여기에 openId를 추가하면 이 openId가 하나의 유일한 사용자로 식별됩니다. 규칙은 App 개발자가 자체 작성하고, App 내에서 중복되지만 않으면 됩니다 (현재는 INT64만 지원합니다).
>SDK 초기기화 후 방에 들어갈 수 있습니다.
>
>####  함수 프로토타입

```
ITMGContext -(int)InitEngine:(NSString*)sdkAppID openID:(NSString*)openId
```

|파라미터     | 유형         |의미|
| ------------- |:-------------:|-------------|
| sdkAppId    |NSString  |Tencent Cloud 콘솔의 sdkAppID 번호|
| openId    |NSString  |OpenID 는 Int64 유형만을 지원하며 (string 으로 전환하여 전송), 10000보다 커야 합니다. 이는 사용자 식별에 사용됩니다 |

####  예시 코드 


```
[[ITMGContext GetInstance] InitEngine:SDKAPPID3RD openID:_openId];
```
### 트리거 이벤트 콜백
update 내부 주기의 Poll 호출을 통해 트리거 이벤트 콜백을 할 수 있습니다.
####  함수 프로토타입

```
ITMGContext -(void)Poll
```
####  예시 코드
```
[[ITMGContext GetInstance] Poll];
```

### 시스템 일시정지
시스템에서 Pause 이벤트가 발생할 경우 엔진에 Pause 진행을 함께 알려야 합니다.
####  함수 프로토타입

```
ITMGContext -(QAVResult)Pause
```

### 시스템 복구
시스템에서 Resume 이벤트가 발생할 경우 엔진에 동시에 Resume를 알려야 합니다. Resume 인터페이스는 실시간 음성만을 복구합니다.
####  함수 프로토타입

```
ITMGContext -(QAVResult)Resume
```



### SDK 초기화 취소
SDK를 초기화 취소하고 미초기화 상태로 들어갑니다. 계정을 바꾸려면 초기화 취소가 필요합니다.
#### 함수 프로토타입

```
ITMGContext -(void)Uninit
```
####  예시 코드
```
[[ITMGContext GetInstance] Uninit];
```



### 벡엔드 소리 재생 설정
백엔드 소리 재생 설정은 방 들어가기 전 호출하십시오.
그리고 애플리케이션 측은 아래 두가지 사항을 주의하십시오:
- 백엔드 닫기 시, 오디오 엔진의 수집과 재생이 일시 중지하지 않습니다 (즉 PauseAudio),
- App 의 Info.plist 중, 적어도 아래 key:Required background modes，string:App plays audio or streams audio/video using AirPlay 을 추가하여야 합니다.

#### 함수 프로토타입
```
ITMGContext -(QAVResult)SetDefaultAudienceAudioCategory:(ITMG_AUDIO_CATEGORY)audioCategory
```

|유형     | 파라미터         |의미|
| ------------- |:-------------:|-------------|
| ITMG_CATEGORY_AMBIENT    |0|벡엔드 닫을 때 소리가 없음 (기본값)|
| ITMG_CATEGORY_PLAYBACK    |1   |백엔드 닫을 때 소리가 있음|

kAudioSessionProperty_AudioCategory의 수정으로 구체적인 실현이 가능하며, 관련 자료는 Apple 공식사이트 상의 문서를 참조하십시오.


#### 예시 코드  
```
[[ITMGContext GetInstance]SetDefaultAudienceAudioCategory:ITMG_CATEGORY_AMBIENT];
```



## 실시간 음성 채팅방 관련 인터페이스
초기화 후, SDK 호출 및 방 들어가기가 진행되어야 실시간 음성 통화가 가능합니다.
궁금한 사항은 [실시간 음성 채팅 관련 문제](https://intl.cloud.tencent.com/document/product/607/30257)를 참조하십시오.

|인터페이스     | 인터페이스 의미   |
| ------------- |:-------------:|
|GenAuthBuffer    |인증 초기화|
|EnterRoom   |방 가입|
|IsRoomEntered   |방 들어가기 여부|
|ExitRoom |방 나가기|
|ChangeRoomType |사용자 방 오디오 유형 수정|
|GetRoomType |사용자 방 오디오 유형 획득|


### 인증 정보
AuthBuffer 생성은 관련 기능의 암호화와 인증에 사용됩니다. 상세 내역은 [인증 보안키](https://intl.cloud.tencent.com/document/product/607/12218)를 참조하십시오.    
오프라인 음성으로 인증을 받으려면 방 번호 파라미터를 null로 채워야 합니다.

#### 함수 프로토타입
```
@interface QAVAuthBuffer : NSObject
+ (NSData*) GenAuthBuffer:(unsigned int)appId roomId:(NSString*)roomId openID:(NSString*)openID key:(NSString*)key;
+ @end
```
|파라미터     | 유형         |의미|
| ------------- |:-------------:|-------------|
| appId    |int   |Tencent Cloud 콘솔의 sdkAppID 번호|
| roomId    |NSString  |방 번호는 최대 127자까지 지원됩니다 (오프라인 음성 방 번호 파라미터는 무조건 null로 채워야 합니다)|
| openID  |NSString    |사용자 식별|
| key    |NSString    |Tencent Cloud [콘솔](https://console.cloud.tencent.com/gamegme) 의 보안키|


####  예시 코드  
```
NSData* authBuffer =   [QAVAuthBuffer GenAuthBuffer:SDKAPPID3RD.intValue roomId:_roomId openID:_openId key:AUTHKEY];
```



### 방 가입
생성된 인증 정보로 방에 들어가면 ITMG_MAIN_EVENT_TYPE_ENTER_ROOM라는 메시지가 콜백됩니다. 가입 방 기본값으로 마이크 및 스피커가 꺼짐 상태로 리턴값이 AV_OK일 때 성공했음을 의미합니다.


####  함수 프로토타입
```
ITMGContext   -(int)EnterRoom:(NSString*) roomId roomType:(int*)roomType authBuffer:(NSData*)authBuffer
```
|파라미터     | 유형         |의미|
| ------------- |:-------------:|-------------|
| roomId |NSString|방 번호는 최대 127자까지 지원합니다|
| roomType |int|방 오디오 유형|
| authBuffer    |NSData    |인증 번호|

오디오 유형과 관련하여 궁금한 사항은 [음질 선택](https://intl.cloud.tencent.com/document/product/607/18522)을 참조하십시오.


####  예시 코드  
```
[[ITMGContext GetInstance] EnterRoom:_roomId roomType:_roomType authBuffer:authBuffer];
```

### 방 가입 이벤트 콜백
방 가입이 완료되면 메시지 ITMG_MAIN_EVENT_TYPE_ENTER_ROOM을 보내 OnEvent 함수에서 판단합니다.

####  예시 코드  
```
-(void)OnEvent:(ITMG_MAIN_EVENT_TYPE)eventType data:(NSDictionary *)data{
    NSLog(@"OnEvent:%lu,data:%@",(unsigned long)eventType,data);
    switch (eventType) {
        case ITMG_MAIN_EVENT_TYPE_ENTER_ROOM:
        {
            int result = ((NSNumber*)[data objectForKey:@"result"]).intValue;
            NSString* error_info = [data objectForKey:@"error_info"];
           	 //방 들어가기 성공 이벤트 수신
        }
            break;
	}
}
```

#### 상세 Data
|메시지     | Data         |예제|
| ------------- |:-------------:|------------- |
| ITMG_MAIN_EVENT_TYPE_ENTER_ROOM    |result; error_info|{"error_info":"","result":0}|


### 방 들어가기 여부 판단
이 인터페이스를 사용하여 방에 들어갔는지 여부를 판단할 수 있으며 리턴값은 bool 유형입니다.
####  함수 프로토타입  
```
ITMGContext -(BOOL)IsRoomEntered
```
####  예시 코드  
```
[[ITMGContext GetInstance] IsRoomEntered];
```

### 방 나가기
이 인터페이스를 사용하여 위치한 방에서 나갈 수 있습니다. 이는 비동기 인터페이스로서, 리턴값이 AV_OK일 때 비동기 딜리버리의 성공을 나타냅니다.

>애플리케이션에서 방 나가기 직후 방 들어가기가 실행되는 작업 환경이 있는 경우 개발자는 인터페이스 호출 프로세스에서 ExitRoom의 콜백 RoomExitComplete 알림을 기다릴 필요가 없습니다. 인터페이스를 직접 호출하면 됩니다.

#### 함수 프로토타입  
```
ITMGContext -(int)ExitRoom
```
####  예시 코드  
```
[[ITMGContext GetInstance] ExitRoom];
```

### 방 나가기 콜백
방 나가기 완료 후 ITMG_MAIN_EVENT_TYPE_EXIT_ROOM 메시지 콜백이 있습니다.
####  예시 코드  
```
-(void)OnEvent:(ITMG_MAIN_EVENT_TYPE)eventType data:(NSDictionary *)data{
    NSLog(@"OnEvent:%lu,data:%@",(unsigned long)eventType,data);
    switch (eventType) {
        case ITMG_MAIN_EVENT_TYPE_EXIT_ROOM：
        {
            //방 나가기 성공 이벤트 수신
        }
            break;
    }
}
```

#### 상세 Data
|메시지     | Data         |예제|
| ------------- |:-------------:|------------- |
| ITMG_MAIN_EVENT_TYPE_EXIT_ROOM    |result; error_info  |{"error_info":"","result":0}|


### 사용자 방 오디오 유형 수정
이 인터페이스는 사용자 방의 오디오 유형을 수정하는 데 사용되며, 결과는 콜백된 이벤트를 참조하십시오. 이벤트 유형은 ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE입니다.

####  함수 프로토타입  
```
ITMGContext GetRoom -(void)ChangeRoomType:(int)nRoomType
```


|파라미터     | 유형         |의미|
| ------------- |:-------------:|-------------|
| nRoomType    |int    |방을 전환하고 싶어하는 유형으로 방 오디오 유형은 EnterRoom 인터페이스 참조|

####  예시 코드  
```
[[[ITMGContext GetInstance]GetRoom ]ChangeRoomType:_roomType];
```


### 사용자 방 오디오 유형 획득
이 인터페이스는 사용자 방의 오디오 유형을 얻는 데 사용됩니다. 리턴 값이 방의 오디오 유형이며, 리턴값이 0인 경우 사용자 룸의 오디오 유형을 얻는 데 오류가 발생했음을 의미하며, 방의 오디오 유형은 EnterRoom 인터페이스를 참조하십시오.

####  함수 프로토타입  
```
ITMGContext GetRoom -(int)GetRoomType
```

####  예시 코드  
```
[[[ITMGContext GetInstance]GetRoom ]GetRoomType];
```


### 방 유형 완성 콜백
방 유형 설정이 완료된 후, 콜백된 사건 소식은 ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE로, 리턴된 파라미터는 result, error_info 및 new_room_type이며, 그 중 new_room_type가 대표되는 메시지는 다음과 같습니다. 이벤트 소식은 OnEvent 함수에서 판단합니다.

|이벤트 유형     | 대표 파라미터   |의미|
| ------------- |:-------------:|-------------|
| ITMG_ROOM_CHANGE_EVENT_ENTERROOM|1 |방에 들어오는 과정에서 가져온 오디오 유형이 방과 일치하지 않음을 나타내는 것이며, 들어온 방 오디오 유형에 따라 수정됨|
| ITMG_ROOM_CHANGE_EVENT_START|2|이미 방에 있는 상황에서 오디오 유형이 변경됨을 나타냄 (예를 들어 ChangeRoomType 인터페이스를 호출한 후 오디오 유형을 변경하는 경우)|
| ITMG_ROOM_CHANGE_EVENT_COMPLETE|3|이미 방에 있는 상황에서 오디오 유형이 변경 완료됨을 뜻함|
| ITMG_ROOM_CHANGE_EVENT_REQUEST|4|방에 멤버가 ChangeRoomType 인터페이스를 호출하여 방 오디오 변경을 요청한 경우 나타남|


####  예시 코드  
```
-(void)OnEvent:(ITMG_MAIN_EVENT_TYPE)eventType data:(NSDictionary *)data {
	NSLog(@"OnEvent:%lu,data:%@",(unsigned long)eventType,data);
    switch (eventType) {
 		case ITMG_MAIN_EVNET_TYPE_USER_UPDATE:
			//처리 진행
	 }
    }
}
```

#### 상세 Data
|메시지     | Data         |예제|
| ------------- |:-------------:|------------- |
| ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE    |result; error_info; new_room_type|{"error_info":"","new_room_type":0,"result":0}|


### 멤버 상태 변화
이 이벤트는 상태 변화가 있어야 알 수 있으며 상태가 변하지 않는 한 알림하지 않습니다. 멤버 상태를 실시간으로 얻으려면 앞에서 알림을 받을 때 캐시하십시오. 이벤트 소식은 ITMG_MAIN_EVNET_TYPE_USER_UPDATE로, 그 중 data는 event_id 및 user_list 두 개의 메시지를 포함하고 있으며, OnEvent 함수에서 본 이벤트 소식을 판단할 수 있습니다.
오디오 이벤트 알림에는 임계 값이 하나 있으며, 이 임계 값을 초과해야 알림이 전송됩니다. 2초 이상 오디오 패키지를 받지 못한 후에야 "멤버가 오디오 패키지 전송을 중지했습니다."라는 메시지를 알립니다.

|event_id     | 의미         |애플리케이션 측 유지보수 내용|
| ------------- |:-------------:|-------------|
|ITMG_EVENT_ID_USER_ENTER    |어떤 멤버가 방에 들어옴|애플리케이션 측 유지보수 멤버 리스트|
|ITMG_EVENT_ID_USER_EXIT    |어떤 멤버가 방을 나감|애플리케이션 측 유지보수 멤버 리스트|
|ITMG_EVENT_ID_USER_HAS_AUDIO    |어떤 멤버가 오디오 패키지 발송함|애플리케이션 측 유지보수 통화 멤버 리스트|
|ITMG_EVENT_ID_USER_NO_AUDIO    |어떤 멤버가 오디오 패키지 발송을 중단함|애플리케이션 측 유지보수 통화 멤버 리스트|

#### 예시 코드  

```
-(void)OnEvent:(ITMG_MAIN_EVENT_TYPE)eventType data:(NSDictionary *)data{
    NSLog(@"OnEvent:%lu,data:%@",(unsigned long)eventType,data);
    switch (eventType) {
        case ITMG_MAIN_EVNET_TYPE_USER_UPDATE:
		{
		//처리 진행
		//개발자는 파라미터를 해석하여 event_id 및 user_list 정보를 얻습니다 
		    switch (eventID)
 		    {
 		    case ITMG_EVENT_ID_USER_ENTER:
  			    //어떤 멤버가 방에 들어왔습니다
  			    break;
 		    case ITMG_EVENT_ID_USER_EXIT:
  			    //어떤 멤버가 방을 나갔습니다
			    break;
		    case ITMG_EVENT_ID_USER_HAS_AUDIO:
			    //어떤 멤버가 오디오 패키지를 발송합니다
			    break;
		    case ITMG_EVENT_ID_USER_NO_AUDIO:
			    //어떤 멤버가 오디오 패키지를 발송 중지했습니다
			    break;
 		    }
		break;
		}
    }
}
```

### 품질 모니터링 이벤트
품질 모니터링 이벤트, 이벤트 소식은 ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_QUALITY로, 리턴된 파라미터는 weight, floss 및 delay로 각각의 의미는 아래와 같습니다. 이벤트 소식은 OnEvent 함수에서 판단됩니다.

|파라미터     | 의미         |
| ------------- |-------------|
|weight    |범위는 1-5이고, 5는 음질 평점이 매우 좋고, 1은 음질 평점이 매우 나빠서 거의 사용할 수 없는 수치입니다. 0은 초기값을 뜻하며, 의미가 없습니다|
|floss    |패킷 손실율|
|delay    |오디오 접촉 지연 시간（ms）|




### 상세 메시지

|메시지     | 메시지 의미   |
| ------------- |:-------------:|
|ITMG_MAIN_EVENT_TYPE_ENTER_ROOM           |오디오방 메시지 들어가기|
|ITMG_MAIN_EVENT_TYPE_EXIT_ROOM             |오디오방 메시지 나가기|
|ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT           |네트워크 등 문제로 방 내 메시지 끊김|
|ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE|방 유형 변화 이벤트|

### 메시지에 대응하는 상세 Data
|메시지     | Data         |예제|
| ------------- |:-------------:|------------- |
| ITMG_MAIN_EVENT_TYPE_ENTER_ROOM    |result; error_info|{"error_info":"","result":0}|
| ITMG_MAIN_EVENT_TYPE_EXIT_ROOM    |result; error_info  |{"error_info":"","result":0}|
| ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT    |result; error_info  |{"error_info":"waiting timeout, please check your network","result":0}|
| ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE    |result; error_info; new_room_type|{"error_info":"","new_room_type":0,"result":0}|


## 실시간 음성 채팅 오디오 인터페이스
SDK를 초기화한 후 방에 들어가야 실시간 음성 채팅 오디오 관련 인터페이스를 호출할 수 있습니다.
사용자가 인터페이스에서 마이크/스피커 열기/닫기 버튼을 클릭할 때 다음과 같은 방식을 권장합니다:
- 대부분의 게임류 App에 EnableMic 및 EnableSpeaker 인터페이스 호출을 추천하는데, 이는 항상 EnableAudioCaptureDevice/EnableAudioSend 와 EnableAudioPlayDevice/EnableAudioRecv 인터페이스를 함께 호출 사용해야 함을 뜻합니다.
- 다른 유형의 모바일 단말기 App의 경우, 예를 들어 소셜 유형 App의 경우, 수집 장비를 열기/닫기 하면 전체 장비(채취 및 재생)가 재시작되며, 만약 이때 App에서 배경 음악이 재생되고 있는 상황이라면 배경 음악의 재생 역시 중단됩니다. 업/다운스트림 제어 방식을 이용하여 마이크의 켜기/끄기 를 작동하면 재생 장치가 중단하지 않습니다. 구체적인 호출 방식은: 방에 들어갈 때는 EnableAudioCaptureDevice(true) && EnableAudioPlayDevice(true) 호출 한 번, 오디오 스티리밍 전송/수신 은 EnableAudioSend/Recv만을 호출하여 제어합니다.
- 수집 또는 재생 장치를 별도로 내보내려면 인터페이스 EnableAudioCaptureDevice 및 EnableAudioPlayDevice를 참조하십시오.
- pause를 사용하여 오디오 엔진을 일시 중지하고 resume을 사용하여 오디오 엔진을 복구합니다.

|인터페이스     | 인터페이스 의미   |
| ------------- |:-------------:|
|EnableMic    |마이크 스위치|
|GetMicState    |마이크 상태 획득|
|EnableAudioCaptureDevice    |수집 장치 스위치|
|IsAudioCaptureDeviceEnabled    |수집 장치 상태 획득|
|EnableAudioSend    |오디오 다운스트림 열기/닫기|
|IsAudioSendEnabled    |오디오 다운스트림 상태 획득|
|GetMicLevel    |실시간 마이크 볼륨 획득|
|GetSendStreamLevel|오디오 다운스트림 실시간 볼륨 획득|
|SetMicVolume    |마이크 볼륨 설정|
|GetMicVolume    |마이크 볼륨 획득|
|EnableSpeaker    |스피커 스위치|
|GetSpeakerState    |스피커 장치 획득|
|EnableAudioPlayDevice    |재생 장치 스위치|
|IsAudioPlayDeviceEnabled    |재생 장치 상태 획득|
|EnableAudioRecv    |오디오 업스트림 열기/닫기|
|IsAudioRecvEnabled    |오디오 업스트림 상태 획득|
|GetSpeakerLevel    |실시간 스피커 볼륨 획득|
|GetRecvStreamLevel|방 내 다른 멤버의 업스트림 실시간 볼륨 획득|
|SetSpeakerVolume    |스피커 볼륨 설정|
|GetSpeakerVolume    |스피커 볼륨 획득|
|EnableLoopBack    |인이어 모니터링 스위치|



### 마이크 켜기 끄기
이 인터페이스는 마이크를 켜기/끄기 위해 사용되며, 방에 들어갈 시 마이크나 스피커의 기본값은 끄기로 되어있습니다.
EnableMic = EnableAudioCaptureDevice + EnableAudioSend.
####  함수 프로토타입  
```
ITMGContext GetAudioCtrl -(QAVResult)EnableMic:(BOOL)enable
```
|파라미터     | 유형         |의미|
| ------------- |:-------------:|-------------|
| isEnabled    |boolean     |마이크를 켜야 할 경우, 파라미터는 YES로 나타나고 마이크를 끄면 NO로 나타납니다|

####  예시 코드  
```
[[[ITMGContext GetInstance] GetAudioCtrl] EnableMic:YES];
```

### 마이크 상태 획득
이 인터페이스는 마이크 상태를 얻는 데 사용되며, 리턴값 0은 마이크가 꺼져있는 상태이고, 리턴값 1은 마이크를 켜기 위한 상태입니다.
####  함수 프로토타입  
```
ITMGContext GetAudioCtrl -(int)GetMicState
```
####  예시 코드  
```
[[[ITMGContext GetInstance] GetAudioCtrl] GetMicState];
```

### 수집 장치 열기 닫기
이 인터페이스는 수집 장치 열기/닫기 에 사용되며, 방에 들어갈 때는 기본값으로 장치가 켜져있지 않습니다.
- 방에 들어온 후에만 이 인터페이스를 호출할 수 있으며, 방 나가기 후는 자동으로 장치가 닫힙니다.
- 모바일 단말기에서 수집 장치를 열면 보통 권한 신청, 볼륨 유형 조정 등의 조작이 수반됩니다.

####  함수 프로토타입  
```
ITMGContext GetAudioCtrl -(QAVResult)EnableAudioCaptureDevice:(BOOL)enabled
```
|파라미터     | 유형         |의미|
| ------------- |:-------------:|-------------|
| enabled    |BOOL     |수집 장치를 켜야 할 경우 파라미터가 YES로 나타나고, 수집 장치를 끄면 NO로 나타납니다|

#### 예시 코드

```
수집 장치 열기
[[[ITMGContext GetInstance]GetAudioCtrl ]EnableAudioCaptureDevice:enabled];
```

### 수집 장치 상태 획득
이 인터페이스는 수집 장치 상태 획득에 사용됩니다.
#### 함수 프로토타입

```
ITMGContext GetAudioCtrl -(BOOL)IsAudioCaptureDeviceEnabled
```
#### 예시 코드

```
BOOL IsAudioCaptureDevice = [[[ITMGContext GetInstance] GetAudioCtrl] IsAudioCaptureDeviceEnabled];
```

### 오디오 다운스트림 열기/닫기
이 인터페이스는 오디오 다운스트림 켜기/끄기 에 사용됩니다. 수집 디바이스가 이미 열려 있다면 채취한 음성 데이터를 보낼 수 있습니다. 수집 디바이스가 켜져 있지 않으면 소리가 나지 않습니다. 수집 디바이스의 켜기 끄기는 인터페이스 EnableAudioCaptureDevice를 참조하십시오.

#### 함수 프로토타입

```
ITMGContext GetAudioCtrl -(QAVResult)EnableAudioSend:(BOOL)enable
```
|파라미터     | 유형         |의미|
| ------------- |:-------------:|-------------|
| enable    |BOOL     |오디오 다운스트림을 켜야 할 경우 파라미터는 YES를 나타내고 오디오 다운스트림을 끄면 NO로 나타납니다|

#### 예시 코드  

```
[[[ITMGContext GetInstance]GetAudioCtrl ]EnableAudioSend:enabled];
```

### 오디오 다운스트림 상태 획득
이 인터페이스는 오디오 다운스트림 상태 획득에 사용됩니다.
#### 함수 프로토타입  
```
ITMGContext GetAudioCtrl -(BOOL)IsAudioSendEnabled
```
####  예시 코드  
```
BOOL IsAudioSend =  [[[ITMGContext GetInstance] GetAudioCtrl] IsAudioSendEnabled];
```

### 마이크 실시간 볼륨 획득
이 인터페이스는 마이크 실시간 볼륨 획득에 사용되며, 리턴값은 int 유형입니다.
####  함수 프로토타입  
```
ITMGContext GetAudioCtrl -(int)GetMicLevel
```
####  예시 코드  
```
[[[ITMGContext GetInstance] GetAudioCtrl] GetMicLevel];
```

### 오디오 다운스트림 실시간 볼륨 획득
이 인터페이스는 오디오 다운스트림 실시간 볼륨 획득에 사용됩니다. 리턴값은 int 유형이며, 값 영역은 0부터 100까지입니다.
####  함수 프로토타입  
```
ITMGContext GetAudioCtrl -(int)GetSendStreamLevel()
```
####  예시 코드  
```
[[[ITMGContext GetInstance] GetAudioCtrl] GetSendStreamLevel];
```

### 마이크 볼륨 설정
이 인터페이스는 마이크의 볼륨을 설정하는 데 사용됩니다. 파라미터 volume 은 마이크의 볼륨을 설정하는데 사용되며 수치가 0일 때 무음을, 수치가 100일 때 볼륨이 더이상 증가하지 않음을 나타내고 기본값은 100입니다.

####  함수 프로토타입  
```
ITMGContext GetAudioCtrl -(QAVResult)SetMicVolume:(int) volume
```
|파라미터     | 유형         |의미|
| ------------- |:-------------:|-------------|
| volume    |int      |볼륨 설정, 범위는 0 부터 200까지|

#### 예시 코드  
```
[[[ITMGContext GetInstance] GetAudioCtrl] SetMicVolume:100];
```
### 마이크 볼륨 획득
이 인터페이스는 마이크 볼륨을 획득하는데 사용됩니다. 리턴값은 int 유형이며, 리턴값 101은 인터페이스 SetMicVolume가 호출되지 않았음을 나타냅니다.

#### 함수 프로토타입  
```
ITMGContext GetAudioCtrl -(int) GetMicVolume
```
####  예시 코드  
```
[[[ITMGContext GetInstance] GetAudioCtrl] GetMicVolume];
```

### 스피커 켜기/끄기
이 인터페이스는 스피커 켜기/끄기 실행에 사용됩니다.
EnableSpeaker = EnableAudioPlayDevice +  EnableAudioRecv.
####  함수 프로토타입  
```
ITMGContext GetAudioCtrl -(void)EnableSpeaker:(BOOL)enable
```
|파라미터     | 유형         |의미|
| ------------- |:-------------:|-------------|
| isEnabled    |boolean       |스피커를 꺼야 할 경우 파라미터가 NO로 나타나며 스피커를 켜면 YES가 나타납니다|

####  예시 코드  
```
[[[ITMGContext GetInstance] GetAudioCtrl] EnableSpeaker:YES];
```

### 스피커 상태 획득
이 인터페이스는 스피커 상태 획득에 사용됩니다. 리턴 값 0은 스피커 상태를 끄기 위해, 리턴 값 1은 스피커 상태를 켜기 위해, 리턴 값 2는 스피커 장비가 작업 중임을 나타냅니다.
####  함수 프로토타입  
```
ITMGContext GetAudioCtrl -(int)GetSpeakerState
```

####  예시 코드  
```
[[[ITMGContext GetInstance] GetAudioCtrl] GetSpeakerState];
```



### 재생 장치 켜기/끄기
이 인터페이스는 재생 장치 켜기/끄기 에 사용됩니다.

#### 함수 프로토타입  
```
ITMGContext GetAudioCtrl -(QAVResult)EnableAudioPlayDevice:(BOOL)enabled
```
|파라미터     | 유형         |의미|
| ------------- |:-------------:|-------------|
| enabled    |BOOL        |재생 장치를 꺼야 할 경우 파라미터가 NO로 나타나며, 재생 기기를 켜면 YES가 나타납니다|

#### 예시 코드  
```
[[[ITMGContext GetInstance]GetAudioCtrl ]EnableAudioPlayDevice:enabled]; 
```

### 재생 장치 상태 획득
이 인터페이스는 재생 장치 상태 획득에 사용됩니다.
#### 함수 프로토타입

```
ITMGContext GetAudioCtrl -(BOOL)IsAudioPlayDeviceEnabled
```
#### 예시 코드  

```
BOOL IsAudioPlayDevice =  [[[ITMGContext GetInstance] GetAudioCtrl] IsAudioPlayDeviceEnabled];
```

### 오디오 업스트림 열기 닫기
이 인터페이스는 오디오 업스트림을 켜기/끄기 에 사용됩니다. 재생 장치가 이미 열려 있다면 방에 있는 다른 사람의 오디오 데이터를 재생합니다. 재생 장치가 켜져 있지 않으면 소리가 나지 않습니다. 재생 장치의 켜기 끄기는 인터페이스 EnableAudioPlayDevice를 참조하십시오.

#### 함수 프로토타입  

```
ITMGContext GetAudioCtrl -(QAVResult)EnableAudioRecv:(BOOL)enabled
```
|파라미터     | 유형         |의미|
| ------------- |:-------------:|-------------|
| enabled    |BOOL     |오디오 다운스트림을 열어야 할 경우, 파라미터는 YES이고, 오디오 다운스트림을 닫으면 NO로 나타납니다|

#### 예시 코드  

```
[[[ITMGContext GetInstance]GetAudioCtrl ]EnableAudioRecv:enabled];
```



### 오디오 업스트림 상태 획득
이 인터페이스는 오디오 업스트림 상태 획득에 사용됩니다.
#### 함수 프로토타입  
```
ITMGAudioCtrl bool IsAudioRecvEnabled()
```

####  예시 코드  
```
BOOL IsAudioRecv = [[[ITMGContext GetInstance] GetAudioCtrl] IsAudioRecvEnabled];
```

### 스피커 실시간 볼륨 획득
이 인터페이스는 스피커 실시간 볼륨 획득에 사용됩니다. 리턴값은 int 유형이며, 스피커 실시간 볼륨을 나타냅니다.
####  함수 프로토타입  
```
ITMGContext GetAudioCtrl -(int)GetSpeakerLevel
```

####  예시 코드  
```
[[[ITMGContext GetInstance] GetAudioCtrl] GetSpeakerLevel];
```

### 방 내 다른 멤버 업스트림 실시간 볼륨 획득
이 인터페이스는 방 내 다른 멤버 업스트림 실시간 볼륨 획득에 사용됩니다. 리턴값은 int 유형이며, 값 영역은 0부터 100까지입니다.
####  함수 프로토타입  
```
ITMGContext GetAudioCtrl -(int)GetRecvStreamLevel:(NSString*) openID 
```

|파라미터     | 유형         |의미|
| ------------- |:-------------:|-------------|
| openID    |NSString       |방 내 다른 멤버의 openId|

####  예시 코드  
```
[[[ITMGContext GetInstance] GetAudioCtrl] GetRecvStreamLevel:(NSString*) openId
```

### 스피커 볼륨 설정
이 인터페이스는 스피커 볼륨 설정에 사용됩니다.
파라미터 volume 은 스피커 볼륨을 설정하는데 사용되며 수치가 0일 때 무음을 표시하고 수치가 100일 때 볼륨이 증가하지 않음을 나타내며 기본값은 100입니다.

####  함수 프로토타입  
```
ITMGContext GetAudioCtrl -(QAVResult)SetSpeakerVolume:(int)vol
```
|파라미터     | 유형         |의미|
| ------------- |:-------------:|-------------|
| vol    |int        |볼륨 설정, 범위 0 부터 200까지|

#### 예시 코드  
```
[[[ITMGContext GetInstance] GetAudioCtrl] SetSpeakerVolume:100];
```

### 스피커 볼륨 획득

이 인터페이스는 스피커 볼륨을 얻는 데 사용됩니다. 리턴 값은 int 유형으로 스피커 볼륨을 의미하며, 리턴 값 101은 인터페이스 SetSpeakerVolume을 호출되지 않았음을 나타냅니다.
Level 은 실시간 볼륨이고 Volume은 스피커 볼륨이며 최종 사운드 볼륨은 Level*Volume%에 해당합니다. 예를 들어: 실시간 볼륨의 수치가 100, Volume의 수치가 60이면, 결과적으로 발생하는 소리의 수치도 60입니다.

####  함수 프로토타입  
```
ITMGContext GetAudioCtrl -(int)GetSpeakerVolume
```
####  예시 코드  
```
[[[ITMGContext GetInstance] GetAudioCtrl] GetSpeakerVolume];
```


### 인이어 모니터링 시작
이 인터페이스는 인이어 모니터링 시작에 사용됩니다.
####  함수 프로토타입  
```
ITMGContext GetAudioCtrl -(QAVResult)EnableLoopBack:(BOOL)enable
```
|파라미터     | 유형         |의미|
| ------------- |:-------------:|-------------|
| enable    |boolean         |설정 시작이 가능한지에 대한 여부|

####  예시 코드  
```
[[[ITMGContext GetInstance] GetAudioCtrl] EnableLoopBack:YES];
```


## 오프라인 음성 채팅 음성을 텍스트로 전환하는 순서도
![](https://main.qcloudimg.com/raw/9ef5e5e4ebc8e63bcd7bfbea6cfb94cc.png)



## 오프라인 음성
초기화 하기 전에 SDK가 초기화되지 않은 단계로 인터페이스 Init를 통해 SDK를 초기화해야 실시간 음성 및 오프라인 음성을 사용할 수 있습니다.
궁금한 사항은 [오프라인 음성 관련 문제](https://intl.cloud.tencent.com/document/product/607/30258)를 참조하십시오.

### 초기화 관련 인터페이스

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
|PauseRecording|녹음 일시중지|
|ResumeRecording|녹음 복구|
|StopRecording    |녹음 중지|
|CancelRecording|녹음 취소|
|GetMicLevel|오프라인 음성 실시간 마이크 볼륨 획득|
|SetMicVolume|오프라인 음성 녹화 볼륨 설정|
|GetMicVolume|오프라인 음성 녹화 볼륨 획득|
|GetSpeakerLevel|오프라인 음성 실시간 스피커 볼륨 획득  |
|SetSpeakerVolume|오프라인 음성 재생 볼륨 설정|
|GetSpeakerVolume|오프라인 음성 재생 볼륨 획득|
|UploadRecordedFile |음성 파일 업로드|
|DownloadRecordedFile|음성 파일 다운로드|
|PlayRecordedFile |음성 재생|
|StopPlayFile|음성 재생 중지|
|GetFileSize |음성 파일의 크기|
|GetVoiceFileDuration|음성 파일의 길이|
|SpeechToText |음성을 텍스트로 인식|

### 인증 초기화
SDK를 초기화한 후에 인증 초기화를 호출합니다. authBuffer 획득은 윗글의 실시간 음성 인증 정보 인터페이스를 참조하십시오.
#### 함수 프로토타입  
```
ITMGContext GetPTT -(QAVResult)ApplyPTTAuthbuffer:(NSData *)authBuffer
```
|파라미터     | 유형         |의미|
| ------------- |:-------------:|-------------|
| authBuffer    |NSData*                    |인증|

#### 예시 코드  
```
[[[ITMGContext GetInstance]GetPTT]ApplyPTTAuthbuffer:(NSData *)authBuffer];
```

### 음성 메시지 최대 길이 제한
음성 메시지의 길이를 제한합니다. 최대 60초까지 지원됩니다.

#### 함수 프로토타입

```
ITMGContext GetPTT -(QAVResult)SetMaxMessageLength:(int)msTime
```
|파라미터     | 유형         |의미|
| ------------- |:-------------:|-------------|
| msTime    |int                    |음성 길이, 단위 ms|

#### 예시 코드  
```
[[[ITMGContext GetInstance]GetPTT]SetMaxMessageLength:(int)msTime];
```


### 녹음 시작
이 인터페이스는 녹음 시작에 사용됩니다. 녹음 파일 업로드 후에야 음성에서 텍스트로 전환하는 등의 작업이 가능합니다.
####  함수 프로토타입  
```
ITMGContext GetPTT -(int)StartRecording:(NSString*)fileDir
```
|파라미터     | 유형         |의미|
| ------------- |:-------------:|-------------|
| fileDir    |NSString                     |저장된 파일 경로|

####  예시 코드  
```
[[[ITMGContext GetInstance]GetPTT]StartRecording:path];
```

### 녹음 시작의 콜백
녹음이 완료된 후 함수 OnEvent를 호출합니다. 이벤트 소식은 ITMG_MAIN_EVNET_TYPE_PTT_RECORD_COMPLETE로 OnEvent 함수에서 이벤트를 판단합니다.
전달된 파라미터는 rusult 와 file_path, 두 가지 정보를 포함하고 있습니다.

#### 에러코드
|에러코드값 |원인  |권장 방안        |
|-----|------|------|
|4097   |파라미터가 비어있음|코드 중 인터페이스 파라미터가 정확한지 점검|
|4098   |초기화 에러|장치가 점유 되어있는지 아니면 권한이 정상인지, 초기화가 정상적인지 점검|
|4099   |녹화 진행 중|정확한 시점에 SDK 녹화 기능을 사용하는지 확인|
|4100   |오디오 데이터 수집 실패|마이크 장치가 정상인지 점검|
|4101   |녹음 시, 녹화 파일 엑세스 에러|파일이 존재하는지, 파일 경로가 합법적인지 확인|
|4102   |마이크 권한 미부여 에러|SDK를 사용하기 위해서는 마이크 권한이 필요합니다. 권한 추가는 엔진 또는 플랫폼의 SDK 공정 배치 문서를 참조하십시오|
|4103   |녹음 시간이 너무 짧음으로 인한 에러|우선 녹음할 때 단위를 ms로 제한하여 파라미터가 올바른지 검사하고, 다음으로 녹음할 때 1,000ms 이상 사용되어야 녹화에 성공할 수 있습니다|
|4104   |녹음 조작 가동 실패|녹음 인터페이스 가동이 이미 호출되어 있는게 아닌지 점검|

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

### 스트리밍 음성 인식 시작
이 인터페이스는 스트리밍 음성 인식을 작동시키는데 사용되며, 동시에 콜백 중에 실시간으로 음성에서 텍스트로 변환시킬 수 있습니다. 지정한 언어를 식별할 수 있으며 음성에서 인식된 정보를 지정 언어로 번역하여 리턴할 수 있습니다.

#### 함수 프로토타입  

```
ITMGContext GetPTT -(void) StartRecordingWithStreamingRecognition(const NSString* filePath)
ITMGContext GetPTT -(void) StartRecordingWithStreamingRecognition(const NSString* filePath,const NSString*speechLanguage,const NSString*translateLanguage)
```
|파라미터     | 유형         |의미|
| ------------- |:-------------:|-------------|
| filePath    |NSString* |보관된 음성 경로|
| speechLanguage    |NSString*                     |지정 텍스트로 식별된 텍스트 파라미터에 관해서는 [음성에서 텍스트로 전환된 텍스트 파라미터 참고 리스트](https://intl.cloud.tencent.com/document/product/607/30260)를 참조하십시오|
| translateLanguage    |NSString*                     |지정 텍스트로 번역된 텍스트 파라미터에 관해서는 [음성에서 텍스트로 전환된 텍스트 파라미터 참고 리스트](https://intl.cloud.tencent.com/document/product/607/30260)를 참조하십시오(이 파라미터는 당분간 사용할 수 없으므로, speechLanguage와 같은 파라미터로 작성하십시오)|

#### 예시 코드  
```
[[[ITMGContext GetInstance] GetPTT] StartRecordingWithStreamingRecognition:recordfilePath  speechLanguage:@"cmn-Hans-CN" translateLanguage:@"cmn-Hans-CN"];
```

### 스트리밍 음성 인식의 시작 콜백
스트리밍 음성 인식이 시작이 완료된 후의 콜백으로 함수 OnEvent를 호출하십시오. 이벤트 소식은 ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_COMPLETE로 OnEvent 함수에서 이벤트 소식을 판단합니다. 전달된 파라미터에는 다음과 같은 네 가지 정보가 포함되어 있습니다.

|메시지 이름     | 의미         |
| ------------- |:-------------:|
| result    |스트리밍 음성 식별에 성공적으로 리턴 코드가 나타났는지에 대한 여부를 판단하는데 사용됨|
| text    |음성에서 텍스트 인식 텍스트로 변환|
| file_path |녹음이 저장된 로컬 주소|
| file_id |녹음의 백그라운드 url 주소|

|에러코드     | 의미         |처리 방식|
| ------------- |:-------------:|:-------------:|
|32775|스트리밍 음성을 텍스트로 변환하는데는 실패했지만 녹음에 성공함|UploadRecordedFile 인터페이스를 호출하여 녹음을 업로드하고, 그 다음SpeechToText 인터페이스를 호출하여 음성을 텍스트로 변환하는 작업을 진행하십시오|
|32777|스트리밍 음성을 텍스트로 변환하는데 실패했지만 녹음과 업로드에 성공함|리턴된 메시지에는 업로드에 성공한 백그라운드 url 주소가 있을 것인데 SpeechToText 인터페이스를 호출하여 음성을 텍스트로 변환하는 작업을 다시 진행하십시오|

#### 예시 코드  
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
### 녹음 일시중지
이 인터페이스는 녹음을 일시 중지하는데 사용됩니다. 녹음을 복원해야 하는 경우 ResumeRecording을 호출하십시오.

#### 함수 프로토타입  
```
ITMGContext GetPTT int PauseRecording()
```
####  예시 코드  
```
[[[ITMGContext GetInstance]GetPTT]PauseRecording;
```

### 녹음 복구
이 인터페이스는 녹음 복구에 사용됩니다.

#### 함수 프로토타입  
```
ITMGContext GetPTT int ResumeRecording()
```
####  예시 코드  
```
[[[ITMGContext GetInstance]GetPTT]ResumeRecording;
```


### 녹음 중지
이 인터페이스는 녹음을 중지하는데 사용됩니다. 이 인터페이스는 비동기 인터페이스이며, 녹음을 중지하면 녹음 완료로 콜백하며, 녹음을 성공한 이후에 만 녹음 파일 사용이 가능합니다.
#### 함수 프로토타입  
```
ITMGContext GetPTT -(QAVResult)StopRecording
```
####  예시 코드  
```
[[[ITMGContext GetInstance]GetPTT]StopRecording];
```



### 녹음 취소
이 인터페이스를 호출하여 녹음을 취소합니다. 취소 후에는 콜백이 없습니다.
#### 함수 프로토타입  
```
ITMGContext GetPTT -(QAVResult)CancelRecording
```
####  예시 코드  
```
[[[ITMGContext GetInstance]GetPTT]CancelRecording];
```

### 오프라인 음성 마이크 실시간 볼륨 획득
이 인터페이스는 마이크 실시간 볼륨 획득에 사용됩니다. 리턴값은 int 유형이며, 값 영역은 0에서 100까지입니다.

#### 함수 프로토타입  
```
ITMGContext GetPTT -(QAVResult)GetMicLevel
```
#### 예시 코드  
```
[[[ITMGContext GetInstance]GetPTT]GetMicLevel];
```

### 오프라인 음성 녹화 볼륨 설정
이 인터페이스는 오프라인 음성 녹화 볼륨 설정에 사용되며, 값 영역은 0에서 100까지입니다.

#### 함수 프로토타입  
```
ITMGContext GetPTT int SetMicVolume:(int) vol
```
#### 예시 코드  
```
[[[ITMGContext GetInstance]GetPTT]SetMicVolume:100];
```

### 오프라인 음성 녹화 볼륨 획득
이 인터페이스는 오프라인 음성 녹화 볼륨을 획득하는데 사용됩니다. 리턴값은 int 유형으로, 값 영역은 0에서 100까지입니다.

#### 함수 프로토타입  
```
ITMGContext GetPTT int GetMicVolume()
```

#### 예시 코드  
```
[[[ITMGContext GetInstance]GetPTT]GetMicVolume];
```


### 스피커 실시간 볼륨 획득
이 인터페이스는 스피커 실시간 볼륨을 획득하는데 사용됩니다. 리턴값은 int 유형으로, 값 영역은 0에서 100까지입니다.

#### 함수 프로토타입  
```
ITMGContext GetPTT -(QAVResult)GetSpeakerLevel
```

#### 예시 코드  
```
[[[ITMGContext GetInstance]GetPTT]GetSpeakerLevel];
```

### 오프라인 재생 볼륨 설정
이 인터페이스는 오프라인 음성 재생 볼륨을 설정하는 데 사용되며, 값 영역은 0에서 100까지입니다.

#### 함수 프로토타입  
```
ITMGContext GetPTT int SetSpeakerVolume:(int) vol
```
#### 예시 코드  
```
[[[ITMGContext GetInstance]GetPTT]SetSpeakerVolume:100];
```

### 오프라인 재생 볼륨 획득
이 인터페이스는 오프라인 음성 재생 볼륨을 얻는 데 사용됩니다. 리턴값은 int 유형이며, 값 영역은 0에서 100까지입니다.

#### 함수 프로토타입  
```
ITMGContext GetPTT int GetSpeakerVolume()
```

#### 예시 코드  
```
[[[ITMGContext GetInstance]GetPTT]GetSpeakerVolume];
```




### 음성 파일 업로드
이 인터페이스는 음성 파일 업로드에 사용됩니다.
#### 함수 프로토타입  
```
ITMGContext GetPTT -(void)UploadRecordedFile:(NSString*)filePath 
```
|파라미터     | 유형         |의미|
| ------------- |:-------------:|-------------|
| filePath    |NSString                      |업로드 된 음성 경로|

#### 예시 코드  
```
[[[ITMGContext GetInstance]GetPTT]UploadRecordedFile:path];
```


### 음성 업로드 완료의 콜백
음성 업로드 완료 후, 이벤트 소식은 ITMG_MAIN_EVNET_TYPE_PTT_UPLOAD_COMPLETE로, OnEvent 함수에서 이벤트 소식을 판단합니다.
#### 에러코드

|에러코드값 |원인  |권장 방안        |
|-----|------|------|
|8193   |파일 업로드 시, 파일 엑세스 에러|파일이 존재하는지와 파일 경로가 합법적인지를 확인|
|8194   |서명 교정 실패 에러|인증 보안키가 올바른 것인지, 초기화 오프라인 음성이 있는지 점검|
|8195   |네트워크 오류|디바이스 네트워크가 외부 네트워크 환경에 제대로 방문할 수 있는지 점검|
|8196   |파라미터 업로드 획득 과정에서의 네트워크 오류|인증이 정확한지 점검하고, 디바이스 네트워크가 외부 네트워크 환경에 제대로 방문할 수 있는지 점검|
|8197   |파라미터 업로드 획득 과정에서 리턴 데이터가 없음|인증이 정확한지 점검하고, 디바이스 네트워크가 외부 네트워크 환경에 제대로 방문할 수 있는지 점검|
|8198   |파라미터 업로드 획득 과정에서 압축 해제 실패|인증이 정확한지 점검하고, 디바이스 네트워크가 외부 네트워크 환경에 제대로 방문할 수 있는지 점검|
|8200   |appinfo 설정 없음|apply 인터페이스가 호출되었는지 확인하거나 인풋 파라미터가 비어있지는 않은지 확인|

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


### 음성 파일 다운로드
이 인터페이스는 음성 파일 다운로드에 사용됩니다.
#### 함수 프로토타입  
```
ITMGContext GetPTT -(void)DownloadRecordedFile:(NSString*)fileId downloadFilePath:(NSString*)downloadFilePath 
```
|파라미터     | 유형         |의미|
| ------------- |:-------------:|-------------|
| fileID    |NSString                      |파일의 url 경로|
| downloadFilePath |NSString                      |파일의 로컬 저장 경로|

####  예시 코드  
```
[[[ITMGContext GetInstance]GetPTT]DownloadRecordedFile:fileIdpath downloadFilePath:path];
```


### 음성 파일 다운로드 완료 콜백
음성 다운로드가 완료된 후, 이벤트 소식은 ITMG_MAIN_EVNET_TYPE_PTT_DOWNLOAD_COMPLETE로, OnEvent 함수에서 이벤트 소식을 판단합니다.
전달된 파라미터에는 result, file_path 와 file_id, 세가지 정보가 포함되어 있습니다.
#### 에러코드

|에러코드값 |원인  |권장 방안        |
|-----|------|------|
|12289  |파일 다운로드 시, 파일 엑세스 에러    |파일 경로가 합법적인지 확인|
|12290  |서명 교정 에러    |인증 보안키가 정확한지와 초기화 오프라인 음성이 있는지 점검|
|12291  |네트워크 저장 시스템 이상    |서버에서 음성 파일 획득 실패한 경우, 인터페이스 파라미터 fileid 올바르게 구성되었는지 검사, 네트워크가 정상인지 검사, cos 파일 저장 없는지 점검|
|12292  |서버 파일 시스템 오류    |디바이스의 네트워크가 외부 네트워크 환경에 제대로 방문할 수 있는지 점검하고, 서버에 이 파일이 있는지 확인|
|12293  |파라미터 다운로드 획득 과정에서 HTTP 네트워크 오류|디바이스의 네트워크가 외부 네트워크 환경에 제대로 방문할 수 있는지 점검|
|12294  |파라미터 다운로드 획득 과정에서 리턴 데이터 없음 |디바이스의 네트워크가 외부 네트워크 환경에 제대로 방문할 수 있는지 점검|
|12295  |파라미터 다운로드 획득 과정에서 압축 해제 실패|디바이스의 네트워크가 외부 네트워크 환경에 제대로 방문할 수 있는지 점검|
|12297  |appinfo 설정 없음|인증 보안키가 올바른 것인지와 초기화 오프라인 음성이 있는지 점검|


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
이 인터페이스는 음성 재생에 사용됩니다.
####  함수 프로토타입  
```
ITMGContext GetPTT -(void)PlayRecordedFile:(NSString*)downloadFilePath
```
|파라미터     | 유형        |의미|
| ------------- |:-------------:|-------------|
| downloadFilePath    |NSString                      |파일 경로|

#### 에러코드

|에러코드값 |원인  |권장 방안        |
|-----|------|------|
|20485  |재생 불가|파일이 있는지, 파일 경로가 합법적인지 확인|

####  예시 코드  
```
[[[ITMGContext GetInstance]GetPTT]PlayRecordedFile:path];
```


### 음성 재생의 콜백
음성 재생의 콜백, 이벤트 소식은 ITMG_MAIN_EVNET_TYPE_PTT_PLAY_COMPLETE로, OnEvent 함수에서 이벤트 소식을 판단합니다.
전달된 파라미터에는 result 와 file_path, 두 가지의 정보가 포함되어 있습니다.

#### 에러코드

|에러코드값 |원인  |권장 방안        |
|-----|------|------|
|20481  |초기화 에러|장치가 점유 되었는지, 아니면 권한이 정상인지, 초기화가 정상적인지 점검|
|20482  |재생 중, 다음 파일을 재생하기 위해 끊는데 실패 (정상 상황에서는 중도 끊기가 가능함)|코드 논리가 맞는지 점검|
|20483  |파라미터 비어있음|코드 중 인터페이스 파라미터가 정확한지 점검|
|20484  |내부 에러|플레이어 초기화 오류, 암호 해독 실패 등의 문제로 이 에러코드가 발생한 경우, 로그 조회와 진단 방법을 결합하여 문제 해결|

#### 예시 코드

```
-(void)OnEvent:(ITMG_MAIN_EVENT_TYPE)eventType data:(NSDictionary *)data{
    NSLog(@"OnEvent:%lu,data:%@",(unsigned long)eventType,data);
    switch (eventType) {
        case ITMG_MAIN_EVNET_TYPE_PTT_PLAY_COMPLETE：
        {
	    //음성 재생의 콜백 
        }
            break;
    }
}
```




### 음성 재생 일시중지
이 인터페이스는 음성 재생 일시중지에 사용됩니다. 음성 재생을 일시중지해도 재생이 완료됨으로 콜백합니다.
####  함수 프로토타입  
```
ITMGContext GetPTT -(int)StopPlayFile
```

####  예시 코드  
```
[[[ITMGContext GetInstance]GetPTT]StopPlayFile];
```



### 음성 파일의 크기 획득
이 인터페이스를 통해 음성 파일의 크기를 알 수 있습니다.
####  함수 프로토타입  
```
ITMGContext GetPTT -(int)GetFileSize:(NSString*)filePath
```
|파라미터     | 유형         |의미|
| ------------- |:-------------:|-------------|
| filePath    |NSString                     |음성 파일의 경로|

####  예시 코드  
```
[[[ITMGContext GetInstance]GetPTT]GetFileSize:path];
```

### 음성 파일 길이 획득
이 인터페이스는 음성 파일의 길이를 획득하는데 사용되며, 단위는 ms입니다.
####  함수 프로토타입  
```
ITMGContext GetPTT -(int)GetVoiceFileDuration:(NSString*)filePath
```
|파라미터     | 유형         |의미|
| ------------- |:-------------:|-------------|
| filePath    |NSString                     |음성 파일의 경로|

####  예시 코드  
```
[[[ITMGContext GetInstance]GetPTT]GetVoiceFileDuration:path];
```


### 지정한 음성 파일을 텍스트로 식별
이 인터페이스는 지정한 음성 파일을 텍스트로 식별하는데 사용됩니다.

#### 함수 프로토타입  
```
ITMGContext GetPTT -(void)SpeechToText:(NSString*)fileID
```
|파라미터     | 유형         |의미|
| ------------- |:-------------:|-------------|
| fileID    |NSString                     |음성 파일 url|

#### 예시 코드  
```
[[[ITMGContext GetInstance]GetPTT]SpeechToText:fileID];
```



### 지정된 음성 파일을 텍스트로 번역 (지정 언어)
이 인터페이스는 지정 언어 식별에 사용할 수 있으며, 음성에서 식별해낸 정보를 지정 언어로 번역하는데 사용할 수도 있습니다.

#### 함수 프로토타입  
```
ITMGContext GetPTT -(void)SpeechToText:(NSString*)fileID (NSString*)speechLanguage (NSString*)translateLanguage
```
|파라미터     | 유형         |의미|
| ------------- |:-------------:|-------------|
| fileID    |NSString*                     |음성 파일 url|
| speechLanguage    |NSString*                     |지정 텍스트의 언어 파라미터를 식별하려면 [음성을 텍스트로 변환된 언어 파라미터 참고 리스트](https://intl.cloud.tencent.com/document/product/607/30260)를 참조하십시오|
| translatelanguage    |NSString*                     |지정 텍스트의 언어 파라미터를 번역하려면 [음성을 텍스트로 변환된 언어 파라미터 참고 리스트](https://intl.cloud.tencent.com/document/product/607/30260)를 참조하십시오(이 파라미터는 일시적으로 유효하지 않으므로, speechLanguage와 일치한 파라미터를 삽입해야 합니다)|

#### 예시 코드  
```
[[[ITMGContext GetInstance]GetPTT]SpeechToText:fileID speechLanguage:"cmn-Hans-CN" translateLanguage:"cmn-Hans-CN"];
```



### 콜백 식별
지정된 음성 파일을 텍스트로 인식된 콜백의 이벤트 소식은 ITMG_MAIN_EVNET_TYPE_PTT_SPEECH2TEXT_COMPLETE로 OnEvent 함수에서 이벤트 소식을 판단합니다.
전달된 파라미터에는 result, file_path 와 text, 이 세가지 정보가 포함되어 있으며, 그 중 text 는 식별된 문자입니다.

#### 에러코드

|에러코드값 |원인  |권장 방안        |
|-----|------|------|
|32769  |내부 오류|로그를 분석을 통해 백그라운드에서 고객에게 잘못 전달한 에러코드를 확인한 뒤, 백그라운드 동료에게 해결을 요청.|
|32770  |네트워크 오류|디바이스 네트워크가 외부 네트워크 환경을 제대로 방문할 수 있는지 점검|
|32772  |롤백 압축 해제 실패|로그를 분석을 통해 백그라운드에서 고객에게 잘못 전달한 에러코드를 확인한 뒤, 백그라운드 동료에게 해결을 요청.|
|32774  |appinfo 설정 없음|인증 보안키가 올바른지, 초기화 오프라인 음성이 있는지 점검|
|32776  |authbuffer 교정 실패|authbuffer 가 올바른지 점검|
|32784  |음성을 텍스트 파라미터로 변환 오류|코드 중 인터페이스 파라미터 fileid 가 비어있는지 점검|
|32785  |음성을 번역된 텍스트로 변환하는데 리턴 오류|오프라인 음성 백그라운드 오류인 경우, 로그를 분석을 통해 백그라운드에서 고객에게 잘못 전달한 에러코드를 확인한 뒤, 백그라운드 동료에게 해결을 요청|

#### 예시 코드

```
-(void)OnEvent:(ITMG_MAIN_EVENT_TYPE)eventType data:(NSDictionary *)data{
    NSLog(@"OnEvent:%lu,data:%@",(unsigned long)eventType,data);
    switch (eventType) {
        case ITMG_MAIN_EVNET_TYPE_PTT_SPEECH2TEXT_COMPLETE：
        {
	    //음성 파일 식별에 성공       
        }
            break;   
    }
}
```



## 고급 API

### 버전 번호 획득
SDK 버전 번호를 획득하여 분석에 사용합니다.
#### 함수 프로토타입
```
ITMGContext  -(NSString*)GetSDKVersion
```
#### 예시 코드  
```
[[ITMGContext GetInstance] GetSDKVersion];
```

### 마이크 권한 점검
마이크 권한 상태 되돌리기.
#### 함수 프로토타입

```
ITMGContext  -(ITMG_RECORD_PERMISSION)CheckMicPermission
```

#### 파라미터 내용

|파라미터|숫자|의미|
|---|---|---|
|ITMG_PERMISSION_GRANTED|0|마이크에 권한이 이미 부여되었습니다|
|ITMG_PERMISSION_Denied|1|마이크 사용이 금지되었습니다|
|ITMG_PERMISSION_NotDetermined|2|사용자에게 권한 신청창이 보여지지 않습니다|
|ITMG_PERMISSION_ERROR|3|인터페이스 호출 에러|

#### 예시 코드  

```
[[ITMGContext GetInstance] CheckMicPermission];
```




### 로그 레벨 인쇄 설정
로그 레벨 인쇄 설정에 사용되며, 기본값 유지를 권장합니다.
#### 함수 프로토타입
```
ITMGContext -(void)SetLogLevel:(ITMG_LOG_LEVEL)levelWrite (ITMG_LOG_LEVEL)levelPrint
```

#### 파라미터 내용

|파라미터|유형|내용|
|---|---|---|
|levelWrite|ITMG_LOG_LEVEL|입력 로그 레벨을 설정하십시오. TMG_LOG_LEVEL_NONE은 사용하지 않음을 의미합니다|
|levelPrint|ITMG_LOG_LEVEL|인쇄 로그 레벨을 설정하십시오. TMG_LOG_LEVEL_NONE은 인쇄하지 않음을 의미합니다|



|ITMG_LOG_LEVEL|내용|
| -------------------------------|----------------------|
|TMG_LOG_LEVEL_NONE=0|로그를 인쇄하지 않습니다|
|TMG_LOG_LEVEL_ERROR=1|로그 인쇄 에러코드(기본값)|
|TMG_LOG_LEVEL_INFO=2|로그 표시 인쇄|
|TMG_LOG_LEVEL_DEBUG=3|개발 디버깅 로그 인쇄|
|TMG_LOG_LEVEL_VERBOSE=4|고빈도 로그 인쇄|

#### 예시 코드  
```
[[ITMGContext GetInstance] SetLogLevel:TMG_LOG_LEVEL_INFO TMG_LOG_LEVEL_INFO];
```



### 로그 경로 인쇄 설정
로그 경로 인쇄 설정에 사용됩니다. 경로 기본값은: Application/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/Documents입니다.
#### 함수 프로토타입
```
ITMGContext -(void)SetLogPath:(NSString*)logDir
```

|파라미터     | 유형         |의미|
| ------------- |:-------------:|-------------|
| logDir    |NSString   |경로|

#### 예시 코드  
```
[[ITMGContext GetInstance] SetLogPath:Path];
```


### 진단 정보 획득
오디오/비디오 통화의 실시간 통화 품질에 대한 정보를 가져옵니다. 이 인터페이스는 주로 실시간 통화 품질, 조사 문제 등을 살펴보는 데 사용되며 업무 측에서는 무시해도 좋습니다.
#### 함수 프로토타입  
```
ITMGContext GetRoom -(NSString*)GetQualityTips
```
#### 예시 코드  
```
[[[ITMGContext GetInstance]GetRoom ] GetQualityTips];
```

### 오디오 데이터 블랙리스트 추가
어떤 ID를 오디오 데이터 블랙리스트에 추가한 경우 리턴값이 0이면 호출이 성공적으로 완료되었음을 나타냅니다.
#### 함수 프로토타입  

```
ITMGContext GetAudioCtrl -(QAVResult)AddAudioBlackList:(NSString*)openID
```
|파라미터     | 유형         |의미|
| ------------- |:-------------:|-------------|
| openId    |NSString      |추가해야 하는 블랙리스트 ID|

#### 예시 코드  

```
[[[ITMGContext GetInstance]GetAudioCtrl ] AddAudioBlackList[id]];
```

### 오디오 데이터 블랙리스트 제거
어떤 ID에서 오디오 데이터 블랙리스트를 제거한 경우 리턴값은 0이면 호출이 성공적으로 완료되었음을 나타냅니다.
#### 함수 프로토타입  

```
ITMGContext GetAudioCtrl -(QAVResult)RemoveAudioBlackList:(NSString*)openID
```
|파라미터     | 유형         |의미|
| ------------- |:-------------:|-------------|
| openId    |NSString      |제거해야 하는 블랙리스트 ID|

#### 예시 코드  

```
[[[ITMGContext GetInstance]GetAudioCtrl ] RemoveAudioBlackList[openId]];
```


## 메시지 콜백

### 메시지 리스트:

|메시지     | 메시지 의미   |
| ------------- |:-------------:|
|ITMG_MAIN_EVENT_TYPE_ENTER_ROOM    |오디오방 메시지 들어가기|
|ITMG_MAIN_EVENT_TYPE_EXIT_ROOM    |오디오방 메시지 나가기|
|ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT|네트워크 등 원인으로 방 내 메시지 끊김|
|ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE|방 유형 변화 이벤트|
|ITMG_MAIN_EVENT_TYPE_ACCOMPANY_FINISH|반주 종료 메시지|
|ITMG_MAIN_EVNET_TYPE_USER_UPDATE|방 멤버 업데이트 메시지|
|ITMG_MAIN_EVNET_TYPE_PTT_RECORD_COMPLETE|PTT 녹음 완료|
|ITMG_MAIN_EVNET_TYPE_PTT_UPLOAD_COMPLETE|PTT 업로드 완료|
|ITMG_MAIN_EVNET_TYPE_PTT_DOWNLOAD_COMPLETE|PTT 다운로드 완료|
|ITMG_MAIN_EVNET_TYPE_PTT_PLAY_COMPLETE|PTT 재생 완료|
|ITMG_MAIN_EVNET_TYPE_PTT_SPEECH2TEXT_COMPLETE|음성을 텍스트로 변환 완료|

### Data 리스트:

|메시지     | Data         |예제|
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
