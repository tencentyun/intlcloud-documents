iOS 개발자가 Tencent Cloud Game Multimedia Engine(GME) 제품 API를 디버깅하고 액세스하는 편의성을 위해, iOS 개발 맞춤용 액세스 파일을 소개드립니다.

GME 매뉴얼 파일은 메인 액세스 API만 제공합니다. 상세내역은 [관련 API 파일](https://intl.cloud.tencent.com/document/product/607/15210)을 참조하십시오.


|메인 API     | API 의미|
| ------------- |:-------------:|
|InitEngine           |GME 초기화 |
|Poll    |트리거 이벤트 콜백|
|SetDefaultAudienceAudioCategory |백그라운드 설정|
|EnterRoom |방 들어가기  |
|EnableMic |마이크 온 |
|EnableSpeaker|스피커 온 |

>
- GME를 사용하기 전에 프로그래밍을 설정해야 SDK가 적용됩니다.
- GME API를 호출하면 리턴값은 QAVError.OK이며, 값은 0입니다.
- GME API는 같은 스레드에서 호출해야 합니다.
- GME 방 가입 전에 인증해야 합니다. 파일중 인증 관련 내용을 참조하십시오.
- GME는 주기적으로 Poll API를 호출하여 트리거 이벤트 콜백합니다.
- GME 콜백 메시지는 콜백 메시지 리스트를 참조하십시오.
- 방에 들어간 후에 디바이스를 조작할 수 있습니다.
- 에러코드 상세내역은 [에러코드](https://intl.cloud.tencent.com/document/product/607/15173)를 참조하십시오


## 액세스 프로세스
### 1. 싱글턴(Singleton) 획득
음성 기능을 사용 시에 우선 ITMGContext 오브젝트를 읽어와야 합니다.

####  함수 프로토타입 

```
ITMGContext ITMGDelegate <NSObject>
```
####  예시 코드  

```
ITMGContext* _context = [ITMGContext GetInstance];
_context.TMGDelegate =self;
```



### 2. SDK 초기화
파라미터를 확인하려면 [액세스 매뉴얼](https://intl.cloud.tencent.com/document/product/607/10782)을 참조하십시오.
이 인터페이스는 Tencent Cloud 콘솔의 SDKAppID 계정을 파라미터로 적용 및 openId를 추가해야 합니다. 이 openId는 사용자당 1개 적용하며, 앱 개발자가 스스로 룰을 정합니다. 앱내 반복할 수 없습니다(현재 INT 64만 지원합니다).
>SDK룰 초기화해야 방에 들어갈 수 있습니다.
>
>####  함수 프로토타입

```
ITMGContext -(int)InitEngine:(NSString*)sdkAppID openID:(NSString*)openID
```

|파라미터     | 타입         |의미|
| ------------- |:-------------:|-------------|
| sdkAppId    |NSString  |Tencent Cloud 콘솔의  sdkAppID 계정|
| openID    |NSString  |OpenID 오직 Int64타입(string으로 전환하여 입력)만 지원하며, 반드시 10000보다 커야 합니다. 사용자 표기용입니다 |

####  예시 코드 


```
[[ITMGContext GetInstance] InitEngine:SDKAPPID3RD openID:_openId];
```
### 3. 트리거 이벤트 콜백
update에서 주기적으로 Poll를 호출하면 트리거 이벤트를 콜백합니다.
####  함수 프로토타입

```
ITMGContext -(void)Poll
```
####  예시 코드
```
[[ITMGContext GetInstance] Poll];
```

### 4. 인증 메시지
AuthBuffer를 생성하여 관련 기능을 암호화하고 인증합니다. 백그라운드 배포 관련 사항은 [인증 보안키](https://intl.cloud.tencent.com/document/product/607/12218)를 참조하십시오.    
오프라인 음성 인증을 읽어오려면 방번호 파라미터는 반드시 null로 입력해야 합니다.

#### 함수 프로토타입
```
@interface QAVAuthBuffer : NSObject
+ (NSData*) GenAuthBuffer:(unsigned int)appId roomId:(NSString*)roomId openID:(NSString*)openID key:(NSString*)key;
+ @end
```
|파라미터     | 타입         |의미|
| ------------- |:-------------:|-------------|
| appId    |int   |Tencent Cloud 콘솔의 sdkAppID 계정|
| roomId    |NSString  |방번호, 최대 127개 캐릭터를 지원합니다(오프라인 음성 방번호 파라미터는 반드시 null를 입력해야 합니다)|
| openID  |NSString    |사용자 표기|
| key    |NSString    |Tencent Cloud [콘솔](https://console.cloud.tencent.com/gamegme) 의 보안키|


####  예시 코드  
```
NSData* authBuffer =   [QAVAuthBuffer GenAuthBuffer:SDKAPPID3RD.intValue roomId:_roomId openID:_openId key:AUTHKEY];
```
### 5. 방 가입
생성한 인증 메시지를 사용하여 방에 가입하면 ITMG_MAIN_EVENT_TYPE_ENTER_ROOM 콜백 메시지를 받습니다. 방에 가입 시 기본적으로 마이크와 스피커를 끄며, 리턴값이 AV_OK일 경우 성공함을 의미합니다.
####  함수 프로토타입
```
ITMGContext   -(int)EnterRoom:(NSString*) roomId roomType:(int*)roomType authBuffer:(NSData*)authBuffer
```
|파라미터     | 타입         |의미|
| ------------- |:-------------:|-------------|
| roomId |NSString|방번호, 최대 127개 캐릭터를 지원합니다|
| roomType |int|방 가청 주파수 타입|
| authBuffer    |NSData    |인증 코드|

방 가청 주파수 타입은 [음질 선택](https://intl.cloud.tencent.com/document/product/607/18522)을 참조하십시오.


####  예시 코드  
```
[[ITMGContext GetInstance] EnterRoom:_roomId roomType:_roomType authBuffer:authBuffer];
```

### 6. 방 가입 이벤트 콜백
방에 가입하면 ITMG_MAIN_EVENT_TYPE_ENTER_ROOM 메시지를 전송하며, OnEvent 함수에서 판단합니다.

```
- (void)OnEvent:(ITMG_MAIN_EVENT_TYPE)eventType data:(NSDictionary*)data
```
콜백하여 관련 참조 코드를 프로세싱합니다.
####  예시 코드  
```
-(void)OnEvent:(ITMG_MAIN_EVENT_TYPE)eventType data:(NSDictionary *)data{
    NSLog(@"OnEvent:%lu,data:%@",(unsigned long)eventType,data);
    switch (eventType) {
        case ITMG_MAIN_EVENT_TYPE_ENTER_ROOM:
        {
            int result = ((NSNumber*)[data objectForKey:@"result"]).intValue;
            NSString* error_info = [data objectForKey:@"error_info"];
           	 //방 가입 성공 이벤트 수신
        }
            break;
	}
}
```

#### 상세 Data
|메시지     | Data         |예시|
| ------------- |:-------------:|------------- |
| ITMG_MAIN_EVENT_TYPE_ENTER_ROOM    |result; error_info|{"error_info":"","result":0}|


### 7. 마이크 온/오프
이 API는 마이크를 온/오프합니다. 방에 가입 시 기본적으로 마이크와 스피커를 끕니다.

####  함수 프로토타입  
```
ITMGContext GetAudioCtrl -(void)EnableMic:(BOOL)enable
```
|파라미터     | 타입         |의미|
| ------------- |:-------------:|-------------|
| isEnabled    |boolean     |혹 마이크를 켜려면 파라미터는 YES로 입력해야 하며, 마이크를 끌 경우, 파라미터는 NO입니다|

####  예시 코드  
```
[[[ITMGContext GetInstance] GetAudioCtrl] EnableMic:YES];
```


### 8. 스피커 온/오프
이 API는 스피커를 온/오프합니다.

####  함수 프로토타입  
```
ITMGContext GetAudioCtrl -(void)EnableSpeaker:(BOOL)enable
```
|파라미터     | 타입         |의미|
| ------------- |:-------------:|-------------|
| isEnabled    |boolean       |혹 스피커를 끄려면 파라미터는 NO로 입력하며, 스피커 켤 경우, 파라미터는 YES입니다|

####  예시 코드  
```
[[[ITMGContext GetInstance] GetAudioCtrl] EnableSpeaker:YES];
```


