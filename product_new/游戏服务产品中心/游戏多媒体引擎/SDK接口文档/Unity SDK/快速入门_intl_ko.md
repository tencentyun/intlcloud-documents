		
Unity 개발자가 Tencent Cloud Game Multimedia Enginec(GME) 제품 API를 디버깅하고 액세스하는 편의성을 위해 Unity 개발 맞춤용 액세스 파일을 소개드립니다. 		
		
GME 매뉴얼 파일은 메인 액세스 API만 언급합니다. API 관련 상세내역은 [API 파일](https://intl.cloud.tencent.com/document/product/607/15210)을 참조하십시오.
			
|중요한 API     | API 의미|
| ------------- |:-------------:|
|Init    |GME 초기화 |
|Poll    |트리거 이벤트 콜백|
|EnterRoom |방에 들어가기  |
|EnableMic |마이크 온 |
|EnableSpeaker|스피커 온 |

>
- GME를 사용하기 전에 프로그래밍을 설정해야 SDK가 적용됩니다.
-GME API를 호출하면 리턴값은 QAVError.OK이며, 값은 0입니다.
-GME API는 같은 스레드에서 호출해야 합니다.
-GME 방 가입 전에 인증해야 합니다. 파일중 인증 관련 내용을 참조하십시오.
-GME는 주기적으로 Poll API를 호출하여 트리거 이벤트를 콜백해야 합니다.
-GME 콜백 메시지는 콜백 메시지 리스트를 참조하십시오.
-방에 들어간 후에 디바이스를 조작할 수 있습니다.
- 에러코드 상세내역은 [에러코드](https://intl.cloud.tencent.com/document/product/607/15173)를 참조하십시오

## 쾌속 액세스 프로세스
### 1. SDK를 초기화합니다
파라미터를 획득하려면 [액세스 매뉴얼](https://intl.cloud.tencent.com/document/product/607/10782)을 참조하십시오.
이 인터페이스는 Tencent Cloud 콘솔의 SDKAppID 계정을 파라미터로 적용 및 openId를 추가해야 합니다. 이 openId는 유저당 1개 적용하며, 앱 개발자가 스스로 룰을 정합니다. 앱내 반복할 수 없습니다(현재 INT 64만 지원합니다).
>SDK를 초기화해야 방에 들어갈 수 있습니다.
####  함수 프로토타입

```
ITMGContext Init(string sdkAppID, string openID)
```

|파라미터     | 타입         |의미|
| ------------- |:-------------:|-------------|
| sdkAppId    |String  |Tencent Cloud 콘솔의 sdkAppId 계정|
| openID    |String  |OpenID 오직 Int64타입(string으로 전환하여 입력)만 지원하며, 반드시 10,000보다 커야 합니다. 사용자 표기용|

####  예시 코드 

```
int ret = ITMGContext.GetInstance().Init(str_appId, str_userId);
	if (ret != QAVError.OK) {
		return;
	}
```
### 2. 트리거 이벤트 콜백
update에서 주기적으로 Poll를 호출하면 트리거 이벤트를 콜백합니다.
####  함수 프로토타입

```
ITMGContext public abstract int Poll();
```

### 3. 인증 메시지
AuthBuffer를 생성하여 관련 기능을 암호화하고 인증합니다. 백그라운드 배포 관련 사항은 [인증 보안키](https://intl.cloud.tencent.com/document/product/607/12218)를 참조하십시오.    
오프라인 음성 메시지는 인증을 읽어올 때 방번호 파라미터는 반드시 null로 입력해야 합니다.

#### 함수 프로토타입
```
QAVAuthBuffer GenAuthBuffer(int appId, string roomId, string openId, string key)
```
|파라미터     | 타입         |의미|
| ------------- |:-------------:|-------------|
| appId    |int   |Tencent Cloud 콘솔의 sdkAppId 계정.|
| roomId    |string   |방번호, 최대 127개 캐릭터를 지원합니다(오프라인 음성 방번호의 파라미터는 반드시 null을 입력해야 합니다).|
| openID    |string |유저 표기.|
| key    |string |Tencent Cloud [콘솔](https://console.cloud.tencent.com/gamegme)의 보안키.|


####  예시 코드  
```
byte[] GetAuthBuffer(string appId, string userId, string roomId)
    {
	return QAVAuthBuffer.GenAuthBuffer(int.Parse(appId), roomId, userId, "a495dca2482589e9");
}
```
### 4. 방 가입
생성한 인증 메시지로 방에 들어갑니다. 방에 가입 시 기본적으로 마이크와 스피커를 끕니다.


####  함수 프로토타입
```
ITMGContext EnterRoom(string roomId, int roomType, byte[] authBuffer)
```
|파라미터     | 타입         |의미|
| ------------- |:-------------:|-------------|
| roomId|string    |방번호, 최대 127개 캐릭터를 지원합니다.|
| roomType |ITMGRoomType|방 가청주파수 타입.|
| authBuffer |Byte[] |인증코드.|

방 가청주파수 타입은 [음질 선택](https://intl.cloud.tencent.com/document/product/607/18522)을 참조하십시오.


####  예시 코드  
```
ITMGContext.GetInstance().EnterRoom(roomId, ITMG_ROOM_TYPE_FLUENCY, authBuffer);
```

### 5. 방 가입 이벤트 콜백
방에 가입 시, 위탁 함수를 통해 콜백해야 합니다. 여기에 2종 메시지를 포함합니다: result와 error_info
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
	    ShowWarnning (string.Format("기존 음성 방id:{0}, 다른 단말기에 이 방을 추가하여 통화하세요",roomId));
    }
}
```

### 6. 마이크 온/오프
이 API는 마이크를 온/오프합니다. 방에 가입시 기본적으로 마이크와 스피커를 끕니다.

####  함수 프로토타입  
```
ITMGAudioCtrl EnableMic(bool isEnabled)
```
|파라미터     | 타입         |의미|
| ------------- |:-------------:|-------------|
| isEnabled    |boolean     |마이크를 온하려면, 파라미터는 true로 입력하며, 마이크를 오프할 경우, 파라미터는 false입니다.|

####  예시 코드  
```
마이크 온
ITMGContext.GetInstance().GetAudioCtrl().EnableMic(true);
```


### 7. 스피커 온/오프
이 인터페이스는 스피커를 온/오프합니다.
####  함수 프로토타입  
```
ITMGAudioCtrl EnableSpeaker(bool isEnabled)
```
|파라미터     | 타입         |의미|
| ------------- |:-------------:|-------------|
| isEnabled    |bool        |스피커를 오프하려면, 파라미터는 false로 입력하며, 스피커를 온 할 경우, 파라미터는  true입니다.|

####  예시 코드  
```
스피커 온
ITMGContext.GetInstance().GetAudioCtrl().EnableSpeaker(true);
```

