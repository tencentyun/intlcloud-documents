Android 개발자가 Tencent Cloud Game Multimedia Engine(GME) 제품 API를 테스트하고 액세스하는데 도움을 드리고자, Android 개발 매뉴얼 파일을 소개드립니다. 



GME 매뉴얼 파일은 메인 액세스 API만 제공합니다. 더 알아보려면 [관련 API 파일](https://intl.cloud.tencent.com/document/product/607/15210)을 참조해주세요.

|중요 API     | API 의미|
| ------------- |:-------------:|
|Init    |GME 초기화 |
|Poll    |트리거 이벤트 콜백|
|EnterRoom |방 들어가기  |
|EnableMic |마이크 온 |
|EnableSpeaker|스피커 온 |

>
- GME를 사용하기 전에 프로그래밍을 설정해야 SDK가 적용됩니다.
-GME API를 호출하면 리턴값은 QAVError.OK이며, 수치는 0입니다.
-GME API는 같은 스레드에서 호출해야 합니다.
-GME 방에 가입 시 인증이 필요합니다. 파일중 인증 파트 관련 내용을 참조해주세요.
- GME는 주기적으로 Poll API를 호출하여 트리거 이벤트를 콜백해야 합니다.
- GME 콜백 메시지는 콜백 메시지 리스트를 참조해주세요.
- 방에 들어간 후 디바이스를 조작할 수 있습니다.
- 에러코드 상세내역은 [에러코드](https://intl.cloud.tencent.com/document/product/607/15173)를 참조해주세요.

## 액세스 프로세스

### 1. 싱글턴(Singleton) 획득
음성 기능을 적용 시에 우선 ITMGContext 오브젝트를 획득해야 합니다.
####  함수 프로토타입 

```
public static ITMGContext GetInstance(Context context)
```

|파라미터     | 타입         |의미|
| ------------- |:-------------:|-------------|
| context    |Context |애플리케이션 업/다운 텍스트 오브젝트|


####  예시 코드  

```
import com.tencent.TMG.ITMGContext; 
TMGContext.getInstance(this);
```

### 2. SDK 초기화

파라미터를 확인하려면 [액세스 매뉴얼](https://intl.cloud.tencent.com/document/product/607/10782)을 참조해주세요.
이 API는 Tencent Cloud 콘솔의 SDKAppID 계정을 파라라미터로 적용해야 합니다. openId를 추가하면, 이 openId는 1명의 유저에만 적용됩니다. 앱 개발자가 스스로 룰을 정하며, 앱내 중복할 수 없습니다(현재 INT64만 지원합니다).
>SDK를 초기화해야 방에 들어갈 수 있습니다.
####  함수 프로토타입

```
ITMGContext public int Init(String sdkAppId, String openID)
```

|파라미터     | 타입         |의미|
| ------------- |:-------------:|-------------|
| sdkAppId    |String  |Tencent Cloud 콘솔의 sdkAppId 계정|
| openID    |String  |OpenID 오직 Int64 타입(string으로 전환하여 적용)만 지원합니다. 반드시 10000보다 커야 하며 유저를 구분합니다|

####  예시 코드 


```
ITMGContext.GetInstance(this).Init(sdkAppId, openID);
```
### 3. 트리거 이벤트 콜백
update에서 주기적으로 Poll를 호출하여 트리거 이벤트를 콜백합니다

####  함수 프로토타입

```
ITMGContext int Poll()
```
####  예시 코드
```
ITMGContext.GetInstance(this).Poll();
```

### 4. 인증 메시지
AuthBuffer를 생성하여 기능을 암호화하고 인증합니다. 백그라운드 배포 관련 내용은 [인증 보안키](https://intl.cloud.tencent.com/document/product/607/12218)를 참조해주세요.    
오프라인 음성 메시지는 인증을 읽어올 때 방번호는 반드시 null로 입력해야 합니다.

#### 함수 프로토타입
```
AuthBuffer public native byte[] genAuthBuffer(int sdkAppId, String roomId, String identifier, String key)
```
|파라미터     | 타입         |의미|
| ------------- |:-------------:|-------------|
| appId    |int   |Tencent Cloud 콘솔의 sdkAppId 계정|
| roomId    |String   |방번호, 최대 127개 캐릭터를 지원합니다(오프라인 음성 방번호 파라미터는 반드시 null로 입력해야 합니다)|
| openID    |String |유저 표기|
| key    |string |Tencent Cloud [콘솔](https://console.cloud.tencent.com/gamegme) 보안키|


####  예시 코드  
```
import com.tencent.av.sig.AuthBuffer;//헤더파일
byte[] authBuffer=AuthBuffer.getInstance().genAuthBuffer(Integer.parseInt(sdkAppId), strRoomID,identifier, key);
```


### 5. 방 가입
생성한 인증 메시지를 사용하여 방에 들어가면, ITMG_MAIN_EVENT_TYPE_ENTER_ROOM 콜백 메시지를 받습니다. 방에 가입 시 기본적으로 마이크와 스피커를 오픈하지 않습니다. 리턴값이 AV_OK일 경우 성공하였음을 의미합니다. 

####  함수 프로토타입
```
ITMGContext public abstract int EnterRoom(String roomId, int roomType, byte[] authBuffer)
```
|파라미터     | 타입         |의미|
| ------------- |:-------------:|-------------|
| roomId |String|방번호, 최대 127개 캐릭터를 지원합니다|
| roomType |int|방 가청 주파수 타입|
| authBuffer|byte[]|인증코드|

방의 가청 주파수 타입은 [음질 선택](https://intl.cloud.tencent.com/document/product/607/18522)을 참조해주세요.


####  예시 코드  
```
ITMGContext.GetInstance(this).EnterRoom(roomId,roomType, authBuffer);    
```

### 6. 방 가입 이벤트 콜백
방에 가입하면 ITMG_MAIN_EVENT_TYPE_ENTER_ROOM 메시지를 발송하며, OnEvent 함수에서 판단합니다.
콜백 관련 파라미터 코드 설정.

```
private ITMGContext.ITMGDelegate itmgDelegate = null;
itmgDelegate= new ITMGContext.ITMGDelegate() {
            @Override
 			public void OnEvent(ITMGContext.ITMG_MAIN_EVENT_TYPE type, Intent data) {
                }
        };
```
콜백 처리 관련 파라미터 코드.
####  예시 코드  
```
public void OnEvent(ITMGContext.ITMG_MAIN_EVENT_TYPE type, Intent data) {
	if (ITMGContext.ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVENT_TYPE_ENTER_ROOM == type)
        {
           	 //방 들어가기에 성공한 이벤트 수락
        }
	}
```

### 7. 마이크 온/오프
이 API는 마이크를 온/오프합니다. 방에 가입 시 기본적으로 마이크와 스피커를 오프합니다.

####  함수 프로토타입  
```
ITMGContext public void EnableMic(boolean isEnabled)
```
|파라미터     | 타입         |의미|
| ------------- |:-------------:|-------------|
| isEnabled    |boolean     |마이크를 온해야 할 경우, 파라미터는 true로 입력되며, 마이크를 오프하면 파라미터는 false입니다|

####  예시 코드  
```
ITMGContext.GetInstance(this).GetAudioCtrl().EnableMic(true);
```


### 8. 스피커 온/오프
이 API는 스피커를 온/오프합니다.

####  함수 프로토타입  
```
ITMGContext public void EnableSpeaker(boolean isEnabled)
```
|파라미터     | 타입         |의미|
| ------------- |:-------------:|-------------|
| isEnabled    |boolean       |혹 스피커를 오프하려면, 파라미터는 false로 적용됩니다. 혹 스피커를 온하였을 경우, 파라미터는 true입니다|

####  예시 코드  
```
ITMGContext.GetInstance(this).GetAudioCtrl().EnableSpeaker(true);
```

