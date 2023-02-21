본문은 Unity 음성 채팅 기능을 위해 Tencent Cloud Game Multimedia Engine(GME) 클라이언트 API에 액세스하고 디버깅하는 방법을 설명합니다.

## GME 사용을 위한 주요 고려 사항

GME는 Init 및 Poll과 같은 핵심 API에 의존하는 실시간 음성, 음성 메시지 및 음성 텍스트 변환 서비스를 제공합니다.

#### 주요 사항

- [서비스 활성화](https://intl.cloud.tencent.com/document/product/607/10782)에 설명된 대로 GME 애플리케이션을 생성하고 SDK의 AppID 및 Key를 가져옵니다.
- [서비스 활성화](https://intl.cloud.tencent.com/document/product/607/10782)에 설명된 대로 **GME의 실시간 음성, 음성 메시지 및 음성 텍스트 변환 서비스**를 활성화했습니다.
- GME를 사용하기 전에 프로젝트를 구성하십시오. 그렇지 않으면 SDK가 적용되지 않습니다.
- GME API가 성공적으로 호출되면 QAVError.OK가 0 값으로 반환됩니다.
- GME API는 동일한 스레드에서 호출되어야 합니다.
- GME가 이벤트 콜백을 트리거하려면 Poll API를 주기적으로 호출해야 합니다.
- 자세한 에러 코드는 <dx-tag-link link="https://cloud.tencent.com/document/product/607/15173" tag="ErrorCode">에러 코드</dx-tag-link>를 참고하십시오.
- GME는 Unity-WebGL 플랫폼에서 간단한 음성 채팅 기능만 지원합니다. 자세한 내용은 [H5 Project Configuration](https://intl.cloud.tencent.com/document/product/607/30261)을 참고하십시오.

## SDK에 연결

### 중요 단계

SDK 연결 관련 주요 프로세스는 다음과 같습니다.

<img src="https://qcloudimg.tencent-cloud.cn/raw/c8758a24fe68fc084b8d12b09de5e27a.jpg"  width="70%" /></img>

<dx-steps>
-<dx-tag-link link="#Init" tag="API: Init">GME 초기화</dx-tag-link>
-<dx-tag-link link="#Poll" tag="API: Poll">이벤트 콜백을 트리거하기 위해 주기적으로 Poll 호출</dx-tag-link>
-<dx-tag-link link="#EnterRoom" tag="API: EnterRoom">음성 채팅방 입장</dx-tag-link>
-<dx-tag-link  tag="콜백: QAVEnterRoomComplete">방 입장 콜백 처리</dx-tag-link>
-<dx-tag-link link="#EnableMic" tag="API: EnableMic">마이크 활성화</dx-tag-link>
-<dx-tag-link link="#EnableSpeaker" tag="API: EnableSpeaker">스피커 활성화</dx-tag-link>
-<dx-tag-link link="#ExitRoom" tag="API: ExitRoom">음성 채팅방 퇴장</dx-tag-link>
-<dx-tag-link link="#UnInit" tag="API: UnInit">GME 초기화 해제</dx-tag-link>
</dx-steps>

### C# 클래스

| 클래스                  |        설명        |
| ------------------- | :----------------: |
| ITMGContext         |      주요 API      |
| ITMGRoom            |    방 API    |
| ITMGRoomManager     |    방 관리 API    |
| ITMGAudioCtrl       |    오디오 API    |
| ITMGAudioEffectCtrl | 음향 효과 및 반주 API |

## 주요 API

| API   |   설명   |
| ------ | :----------: |
| Init   |  GME 초기화  |
| Poll   | 이벤트 콜백 트리거 |
| Pause  |   시스템 정지   |
| Resume |   시스템 복구   |
| Uninit | GME 초기화 해제 |

### 헤더 파일 가져오기

```
using GME;
```

### 인스턴스 가져오기

QAVContext.GetInstance() 대신 ITMGContext 메소드를 사용하여 Context 인스턴스를 가져옵니다.

[](id:Init)
### SDK 초기화

실시간 음성, 음성 메시지, 음성 텍스트 변환 서비스를 사용하려면 먼저 **Init API를 통해 SDK를 초기화해야 합니다**. Init API는 다른 API와 동일한 스레드에서 호출해야 합니다. 기본 스레드에서 모든 API를 호출하는 것이 좋습니다.

#### API 프로토타입

```
//class ITMGContext
public abstract int Init(string sdkAppID, string openID);
```

| 매개변수     |  유형  | 설명                                                         |
| -------- | :----: | ------------------------------------------------------------ |
| sdkAppId | string | [서비스 활성화](https://intl.cloud.tencent.com/document/product/607/10782#.E9.87.8D.E7.82.B9.E5.8F.82.E6.95.B0)의 지침에 따라 얻을 수 있는 [GME 콘솔](https://console.cloud.tencent.com/gamegme)에서 제공되는 AppID입니다. |
| openID   | string | openID는 Int64 타입만 가능하며 문자열로 변환되어 전달됩니다. 해당 규칙을 사용자 정의할 수 있으며 App에서 고유해야 합니다. Openid를 문자열로 전달하기 위해서는 [Submit Ticket](https://console.cloud.tencent.com/workorder/category?level1_id=438&level2_id=445&source=0&data_title=%E6%B8%B8%E6%88%8F%E5%A4%9A%E5%AA%92%E4%BD%93%E5%BC%95%E6%93%8EGME&step=1)하여 신청하십시오.|

#### 반환된 값

|반환 값                          | 설명                                          |
| ------------------------------- | --------------------------------------------- |
| QAVError.OK= 0                  | SDK 초기화 성공                               |
| AV_ERR_SDK_NOT_FULL_UPDATE=7015 | SDK 파일이 완전한지 확인합니다. 삭제한 후 SDK를 다시 가져오는 것이 좋습니다. |

<dx-alert infotype="notice" title="7015 에러 코드에 대한 참고 사항">

- 7015 에러 코드는 md5로 판단됩니다. 통합 중에 이 오류가 보고되면 메시지에 따라 SDK 파일의 무결성과 버전을 확인하십시오.
- 반환 값 AV_ERR_SDK_NOT_FULL_UPDATE는 사전 **알림일 뿐**이며 초기화 실패를 일으키지는 않습니다.
- 타사 강화, Unity 패키징 메커니즘 및 기타 요인으로 인해 라이브러리 파일의 md5가 영향을 받아 오판이 발생할 수 있습니다. **정식 출시를 위한 로직에서는 이 오류를 무시**하고 UI에 표시하지 않도록 하십시오.
  </dx-alert>

#### 예시 코드 

```
int ret = ITMGContext.GetInstance().Init(sdkAppId, openID);
// 반환된 값으로 초기화 성공 여부 판단
if (ret != QAVError.OK)
    {
        Debug.Log("SDK 초기화 실패:"+ret);
        return;
    }
```

[](id:Poll)
### 이벤트 콜백 트리거

이벤트 콜백은 update에서 Poll API를 주기적으로 호출하여 트리거할 수 있습니다. Poll API는 GME의 메시지 펌프이며 GME가 이벤트 콜백을 트리거하도록 주기적으로 호출해야 합니다. 그렇지 않으면 전체 SDK 서비스가 비정상적으로 실행됩니다. 자세한 내용은 [SDK 다운로드 가이드](https://intl.cloud.tencent.com/document/product/607/18521)의 EnginePollHelper 파일을 참고하십시오.

<dx-alert infotype="alarm" title="주기적으로 Poll API 호출">
비정상적인 API 콜백을 방지하기 위해 Poll API는 주기적으로 메인 스레드에서 호출되어야 합니다.
</dx-alert>

#### API 프로토타입

```
ITMGContext public abstract int Poll();
```

#### 예시 코드

```
public void Update()
    {
        ITMGContext.GetInstance().Poll();
    }
```

### 시스템 일시 중지

시스템에서 Pause 이벤트가 발생하면 엔진에도 일시 중지를 알려야 합니다. 예를 들어 애플리케이션이 백그라운드로 전환되고(OnApplicationPause, isPause=True) 방에서 오디오를 재생하기 위해 백그라운드가 필요하지 않은 경우 Pause API를 호출하여 GME 서비스를 일시 중지하십시오.

#### API 프로토타입

```
ITMGContext public abstract int Pause()
```

### 시스템 복구

시스템에서 Resume 이벤트가 발생하면 엔진에도 Resume에 대해 알려야 합니다. Resume API는 음성 채팅 복구만 지원합니다.

#### API 프로토타입

```
ITMGContext  public abstract int Resume()
```

[](id:UnInit)
### SDK 초기화 해제

이 API는 SDK 초기화 해제를 통해 초기화를 해제하는 데 사용됩니다. **게임 비즈니스 계정이 openid에 바인딩되어 있는 경우 게임 계정을 전환하려면 GME를 초기화 해제한 다음 새 openid를 사용하여 다시 초기화해야 합니다**.

#### API 프로토타입

```
ITMGContext public abstract int Uninit()
```

## 음성 채팅방 API

음성 채팅을 시작하기 전에 초기화하고 SDK를 호출하여 방에 입장해야 합니다.
서비스 이용 중 궁금하신 사항은 [음성 채팅 FAQ](https://intl.cloud.tencent.com/document/product/607/39524)를 참고하십시오.

![](https://qcloudimg.tencent-cloud.cn/raw/02f98895d0b7bfe1bac774d5983289c1.jpg)

| API           |       설명       |
| ------------- | :------------------: |
| GenAuthBuffer |     로컬 인증 키 계산     |
| EnterRoom     |       방 입장       |
| ExitRoom      |       방 퇴장       |
| IsRoomEntered | 방 입장 성공 여부 판단 |
| SwitchRoom    |     방을 빠르게 전환     |

### 로컬 인증 키 계산

관련 기능의 암호화 및 인증을 위해 AuthBuffer를 생성합니다. 프로덕션 환경에서 릴리스하려면 [Authentication Key](https://intl.cloud.tencent.com/document/product/607/12218)에 설명된 대로 백엔드 배포 키를 사용하십시오.    

#### API 프로토타입

```
QAVAuthBuffer GenAuthBuffer(int appId, string roomId, string openId, string key)
```

| 매개변수   |  유형  | 설명                                                         |
| ------ | :----: | ------------------------------------------------------------ |
| appId  |  int   | Tencent Cloud 콘솔의 AppID입니다.                              |
| roomId | string | 최대 127자의 방 ID입니다.                                    |
| openId | string | Init 시 openID와 동일한 사용자 ID입니다.                       |
| key    | string | Tencent Cloud [콘솔](https://console.cloud.tencent.com/gamegme)의 권한 키입니다. |

#### 예시 코드  

```
public static byte[] GetAuthBuffer(string AppID, string RoomID,string OpenId, string AuthKey){
        return QAVAuthBuffer.GenAuthBuffer(int.Parse(AppID), RoomID, OpenId, AuthKey);
}

```

#### WebGL 측 적응
- WebGL 플랫폼에서 로컬 인증 함수를 호출한 후 인증 값은 js 코드에 저장되며 인증된 authBuffer는 C# 레이어로 반환되지 않습니다. 사용자가 로컬 인증을 위해 GetAuthBuffer를 호출한 후, 방 입장 시 호출되는 인증 키 값은 빈칸 또는 아무 값이나 채우면 됩니다.
- 백그라운드 컴퓨팅 인증 체계를 사용하는 경우 GetAuthBuffer API를 호출할 필요가 없습니다.


[](id:EnterRoom)
### 방 입장

생성된 인증 정보로 방에 입장하기 위해 사용하는 API입니다. 방 입장 후 마이크와 스피커는 기본적으로 활성화되지 않습니다.

<dx-alert infotype="alarm" title="주의">
- 방 입장 콜백 result가 0이면 방 입장 성공입니다. EnterRoom API에서 0이 반환된다고 해서 반드시 방 입장이 성공한 것은 아닙니다.
- 방의 오디오 유형은 방에 들어오는 첫 번째 사용자에 의해 결정됩니다. 이후 방에 있는 구성원이 방 유형을 변경하면 모든 구성원에게 적용됩니다. 예를 들어, 처음 방에 입장한 사용자가 원활 음질을 사용하고 두 번째 입장한 사용자가 HD 음질을 사용했다면 두 번째 사용자의 방 오디오 유형은 원활 음질로 변경됩니다. 방의 구성원이 ChangeRoomType API를 호출한 후에만 방의 오디오 유형이 변경됩니다.
</dx-alert>

#### API 프로토타입

```
ITMGContext EnterRoom(string roomId, int roomType, byte[] authBuffer)

```

| 매개변수       |     유형     | 의미                                       |
| ---------- | :----------: | ------------------------------------------ |
| roomId     |    string    | 최대 127자의 방 ID입니다                    |
| roomType   | ITMGRoomType | 객실 유형. 게임의 경우 ITMG_ROOM_TYPE_FLUENCY를 선택하는 것이 좋습니다. 방 오디오 종류에 대한 자세한 내용은 [Sound Quality](https://intl.cloud.tencent.com/document/product/607/18522)를 참고하십시오.|
| authBuffer |    Byte[]    | 인증 키                                     |

#### 예시 코드  

```
ITMGContext.GetInstance().EnterRoom(strRoomId, ITMGRoomType.ITMG_ROOM_TYPE_FLUENCY, byteAuthbuffer);

```

#### 방 입장 콜백

사용자가 방에 들어가면 방 입장 결과가 다시 호출되어 처리를 위해 들을 수 있습니다. 성공적인 콜백은 방 입장이 성공적이며 **과금**이 시작됨을 의미합니다.

<dx-fold-block title="과금 참고">
[구매 가이드](https://intl.cloud.tencent.com/document/product/607/50009)
[과금](https://intl.cloud.tencent.com/document/product/607/30255)
[음성 채팅 사용 시 클라이언트가 서버와 연결이 끊긴 경우에도 계속 과금됩니까?](https://intl.cloud.tencent.com/document/product/607/30255#.E4.BD.BF.E7.94.A8.E5.AE.9E.E6.97.B6.E8.AF.AD.E9.9F.B3.E5.90.8E.EF.BC.8C.E5.A6.82.E6.9E.9C.E5.AE.A2.E6.88.B7.E7.AB.AF.E6.8E.89.E7.BA.BF.E4.BA.86.EF.BC.8C.E6.98.AF.E5.90.A6.E8.BF.98.E4.BC.9A.E7.BB.A7.E7.BB.AD.E8.AE.A1.E8.B4.B9.EF.BC.9F)
</dx-fold-block>

#### API 프로토타입

```
public delegate void QAVEnterRoomComplete(int result, string error_info);
public abstract event QAVEnterRoomComplete OnEnterRoomCompleteEvent;
```

#### 예시 코드  

```
//이벤트 수신:
ITMGContext.GetInstance().OnEnterRoomCompleteEvent += new QAVEnterRoomComplete(OnEnterRoomComplete);

//수신된 이벤트 처리:
void OnEnterRoomComplete(int err, string errInfo)
    {
	if (err != 0) {
  			ShowLoginPanel("에러 코드:" + err + " 에러 메시지:" + errInfo);
            return;
	}else{
		//방 입장 성공
    }
}
```

#### Data 상세정보

| 메시지                                 |        Data        | 샘플                                                         |
| ------------------------------------ | :----------------: | ------------------------------------------------------------ |
| ITMG_MAIN_EVENT_TYPE_ENTER_ROOM      | result; error_info | {"error_info":"","result":0}                                 |
| ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT | result; error_info | {"error_info":"waiting timeout, please check your network","result":0} |

네트워크 연결이 끊어지면 연결 끊김 콜백 알림 `ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT`가 발생합니다. 이때 SDK는 자동으로 다시 연결되며 콜백은 `ITMG_MAIN_EVENT_TYPE_RECONNECT_START`입니다. 재연결에 성공하면 `ITMG_MAIN_EVENT_TYPE_RECONNECT_SUCCESS` 콜백이 발생합니다.

#### 에러 코드

| 에러 코드 값 | 원인 및 제안 솔루션                                               |
| -------- | ------------------------------------------------------------ |
| 7006     | 인증 실패 원인: <li>AppID가 존재하지 않거나 올바르지 않습니다 <li>authbuff를 인증하는 동안 오류가 발생했습니다 <li>인증이 만료되었습니다 <li>OpenId가 사양을 충족하지 않습니다 |
| 7007     | 이미 다른 방에 있습니다                                               |
| 1001     | 사용자는 이미 방에 들어가는 과정에 있었지만 이 작업을 반복했습니다. 방 입장 콜백이 반환될 때까지 방 입장 API를 호출하지 않는 것이 좋습니다. |
| 1003     | 사용자가 이미 방에 있었고 방 입장 API를 다시 호출했습니다                       |
| 1101     | SDK가 초기화되었는지, openId가 규칙을 준수하는지, API가 동일한 스레드에서 호출되는지, Poll API가 정상적으로 호출되는지 확인하십시오 |

[](id:ExitRoom)	
### 방 퇴장

이 API는 현재 방을 나가는 데 사용되며, 비동기 API입니다. 반환된 값 AV_OK는 성공적인 비동기 전달을 나타냅니다. 애플리케이션에서 방 퇴장 직후에 방 입장이 수행되는 시나리오가 있는 경우 API 호출 중에 ExitRoom API에서 RoomExitComplete 콜백 알림을 기다릴 필요가 없습니다. 대신 EnterRoom API를 직접 호출할 수 있습니다.

#### API 프로토타입  

```
ITMGContext ExitRoom()
```

#### 예시 코드  

```
ITMGContext.GetInstance().ExitRoom();
```

#### 방 퇴장 콜백

룸 퇴장 후 메시지를 전달하기 위해 델리게이트 함수를 통해 콜백이 실행됩니다.

#### API 프로토타입  

```
ublic delegate void QAVExitRoomComplete();
public abstract event QAVExitRoomComplete OnExitRoomCompleteEvent; 
```

#### 예시 코드  

```
이벤트 수신:
ITMGContext.GetInstance().OnExitRoomCompleteEvent += new QAVExitRoomComplete(OnExitRoomComplete);
수신된 이벤트 처리:
void OnExitRoomComplete(){
    //방 퇴장 후 콜백 전송
}
```

### 사용자의 방 입장 여부 판단

이 API는 사용자가 방에 들어왔는지 여부를 확인하는 데 사용됩니다. bool 유형의 값이 반환됩니다. 방 입장 중에는 이 API를 호출하지 마십시오.

#### API 프로토타입  

```
ITMGContext abstract bool IsRoomEntered()
```

#### 예시 코드  

```
ITMGContext.GetInstance().IsRoomEntered();
```

### 방 전환

사용자는 이 API를 호출하여 방 입장 후 빠르게 음성 채팅방을 전환할 수 있습니다. 방이 전환된 후 장치는 재설정되지 않습니다. 즉, 이 방에서 마이크가 이미 활성화된 경우 방이 전환된 후에도 마이크는 계속 활성화됩니다.
신속하게 방을 전환하기 위한 콜백은 ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVENT_TYPE_SWITCH_ROOM이며 필드는 error_info 및 result입니다.

#### API 프로토타입

```
public abstract int SwitchRoom(string targetRoomID, byte[] authBuffer);
```

#### 유형 설명

| 매개변수         | 유형   | 설명                           |
| ------------ | ------ | ------------------------------ |
| targetRoomID | String | 입장할 방 ID               |
| authBuffer   | byte[] | 입장할 방의 ID로 새로운 인증 생성 |

## 방 상태 유지 보수

이 섹션의 API는 말하는 구성원과 방 입장/퇴장 구성원을 표시하고 비즈니스 레이어에서 방의 구성원을 음소거하는 데 사용됩니다.

![](https://main.qcloudimg.com/raw/33eecfcd9e18a361aa0b732ffd0fb7dd.png)

| API/알림                        |       설명       |
| -------------------------------- | :--------------: |
| ITMG_MAIN_EVNET_TYPE_USER_UPDATE | 구성원 상태가 변경되었습니다 |
| AddAudioBlackList                | 방에 있는 구성원을 음소거합니다 |
| RemoveAudioBlackList             |     음소거를 해제합니다     |

### 구성원 방 입장 및 발언 상태 알림 이벤트

- 이 이벤트는 방에서 발언하는 사용자를 가져와 UI에 사용자를 표시하며, 누군가의 방 입장/퇴장 시 알림을 보내는 데 사용됩니다.
- 이 이벤트에 대한 알림은 상태가 변경될 때만 전송됩니다. 구성원 상태를 실시간으로 가져오려면 비즈니스 레이어에서 알림을 받을 때 캐시합니다. event_id, count 및 openIdList가 포함된 이벤트 메시지 ITMG_MAIN_EVNET_TYPE_USER_UPDATE가 반환되며 이는 OnEvent 알림에서 판단됩니다.
- EVENT_ID_ENDPOINT_NO_AUDIO 오디오 이벤트 알림은 임계값을 초과한 경우에만 전송됩니다. 즉, 방에 있는 다른 구성원은 로컬 클라이언트가 2초 동안 음성을 캡처하지 않은 후에만 로컬 사용자가 발언을 중지했다는 알림을 받을 수 있습니다.
- 오디오 이벤트는 구성원의 발언 상태만 반환하고 특정 볼륨 수준은 반환하지 않습니다. 방에 있는 구성원의 특정 볼륨 수준이 필요한 경우 GetVolumeById API를 사용할 수 있습니다.

| event_id                    |                         설명                          | 유지 보수         |
| --------------------------- | :---------------------------------------------------: | ---------------------- |
| EVENT_ID_ENDPOINT_ENTER     |         방에 입장하는 구성원의 openid를 반환합니다         | 구성원 목록     |
| EVENT_ID_ENDPOINT_EXIT      |         방을 나가는 구성원의 openid를 반환합니다         | 구성원 목록     |
| EVENT_ID_ENDPOINT_HAS_AUDIO |     방에서 오디오 패킷을 보내는 구성원의 openid를 반환합니다. 이 이벤트는 사용자가 말하고 있는지 여부를 확인하고 성문 효과를 표시하는 데 사용할 수 있습니다.     | 채팅 구성원 목록 |
| EVENT_ID_ENDPOINT_NO_AUDIO  | 방에서 오디오 패킷 전송을 중지하는 구성원의 openid를 반환합니다 | 채팅 구성원 목록 |

#### 예시 코드

```
public delegate void QAVEndpointsUpdateInfo(int eventID, int count, [MarshalAs(UnmanagedType.LPArray, SizeParamIndex = 1)]string[] openIdList);
public abstract event QAVEndpointsUpdateInfo OnEndpointsUpdateInfoEvent;

//이벤트 수신:
ITMGContext.GetInstance().OnEndpointsUpdateInfoEvent += new QAVEndpointsUpdateInfo(OnEndpointsUpdateInfo);
//수신된 이벤트 처리:
void OnEndpointsUpdateInfo(int eventID, int count, string[] openIdList)
{
				//프로세스
		    switch (eventID)
 		    {
 		    case EVENT_ID_ENDPOINT_ENTER:
  			    //구성원 방 입장
  			    break;
 		    case EVENT_ID_ENDPOINT_EXIT:
  			    //구성원 방 퇴장
			    break;
		    case EVENT_ID_ENDPOINT_HAS_AUDIO:
			    //구성원 오디오 패키지 발송
			    break;
		    case EVENT_ID_ENDPOINT_NO_AUDIO:
			    //구성원 오디오 패키지 발송 중단
			    break;
		  
		    default:
			    break;
 		    }
		break;
}
```

### 방에 있는 구성원 음소거

이 API는 오디오 데이터 블록리스트에 ID를 추가하는 데 사용됩니다. 이 작업은 누군가의 오디오를 차단하지만 다른 장치에는 영향을 주지 않고 로컬 장치에만 적용됩니다. 반환된 값 0은 호출이 성공했음을 나타냅니다. 사용자 A, B, C가 모두 방에서 마이크를 사용하여 말하고 있다고 가정합니다. 

- A가 C를 차단하면 A는 B만 들을 수 있습니다.
- B가 A도 C도 차단하지 않으면 B는 둘 다 들을 수 있습니다.
- C가 A도 B도 차단하지 않으면 C는 둘 다 들을 수 있습니다.

이 API는 방에서 사용자가 음소거된 시나리오에 적합합니다.

#### API 프로토타입  

```
ITMGContext ITMGAudioCtrl AddAudioBlackList(String openId)
```

| 매개변수   |  유형  | 설명                      |
| ------ | :----: | ------------------------- |
| openId | String | 블록리스트에 추가할 사용자 openid |

#### 예시 코드  

```
ITMGContext.GetInstance().GetAudioCtrl ().AddAudioBlackList (openId);
```

### 음소거 해제

이 API는 오디오 데이터 블록리스트에서 ID를 제거하는 데 사용됩니다. 반환된 값 0은 호출이 성공했음을 나타냅니다.

#### API 프로토타입  

```
ITMGContext ITMGAudioCtrl RemoveAudioBlackList(string openId)
```

| 매개변수   |  유형  | 설명                      |
| ------ | :----: | ------------------------- |
| openId | String | 블록리스트에서 삭제할 사용자 openid |

#### 예시 코드  

```
ITMGContext.GetInstance().GetAudioCtrl ().RemoveAudioBlackList (openId);
```



## 음성 채팅 캡처 API

- 음성 채팅 API는 SDK 초기화 및 방 입장 후에만 호출할 수 있습니다.
- 사용자가 UI에서 마이크 또는 스피커 활성화/비활성화 버튼을 클릭할 때 EnableMic 또는 EnableSpeaker API를 호출하는 것이 좋습니다.
- 사용자가 UI에서 마이크 버튼을 눌렀다가 놓아 말을 멈출 수 있도록 하려면 방 입장 중에 EnableAudioCaptureDevice를 한 번 호출하고 EnableAudioSend를 호출하여 사용자가 버튼을 누른 상태에서 말할 수 있도록 하는 것이 좋습니다.

| API                        |       설명       |
| --------------------------- | :------------------: |
| EnableMic                   |      마이크 활성화/비활성화      |
| GetMicState                 |    마이크 상태 가져오기    |
| EnableAudioCaptureDevice    |     캡처 장치 활성화/비활성화     |
| IsAudioCaptureDeviceEnabled |   캡처 장치 상태 가져오기   |
| EnableAudioSend             |   오디오 업스트림 활성화/비활성화   |
| IsAudioSendEnabled          |   오디오 업스트림 상태 가져오기   |
| GetMicLevel                 |  실시간 마이크 볼륨 레벨 가져오기  |
| GetSendStreamLevel          | 실시간 오디오 업스트림 볼륨 가져오기 |
| SetMicVolume                |    마이크 볼륨 레벨 설정    |
| GetMicVolume                |    마이크 볼륨 레벨 가져오기    |


[](id:EnableMic)	
### 마이크 활성화 또는 비활성화

이 API는 마이크를 활성화/비활성화하는 데 사용됩니다. 방 입장 후 마이크와 스피커는 기본적으로 활성화되지 않습니다. **EnableMic = EnableAudioCaptureDevice + EnableAudioSend**

#### API 프로토타입  

```
ITMGAudioCtrl EnableMic(bool isEnabled)
```

| 매개변수      |  유형   | 설명                                                         |
| --------- | :-----: | ------------------------------------------------------------ |
| isEnabled | boolean | 마이크를 활성화하려면 이 매개변수를 true로 설정하십시오. 그렇지 않으면 false로 설정하십시오. |

#### 예시 코드  

```
//마이크 활성화
ITMGContext.GetInstance().GetAudioCtrl().EnableMic(true);
```

### 마이크 상태 가져오기

이 API는 마이크 상태를 가져오는 데 사용됩니다. 반환 값 0은 마이크가 꺼져 있음을 나타내고 1은 켜져 있음을 나타냅니다.

#### API 프로토타입  

```
ITMGAudioCtrl GetMicState()
```

#### 예시 코드  

```
micToggle.isOn = ITMGContext.GetInstance().GetAudioCtrl().GetMicState();
```

### 캡처 장치 활성화 또는 비활성화

이 API는 캡처 장치를 활성화/비활성화하는 데 사용됩니다. 방 입장 후 장치는 기본적으로 활성화되지 않습니다.

- 이 API는 방 입장 후에만 호출할 수 있습니다. 방에서 나가면 장치가 자동으로 비활성화됩니다.
- 권한 적용 및 볼륨 유형 조정과 같은 작업은 일반적으로 모바일 장치에서 캡처 장치가 활성화된 경우에 수행됩니다.

#### API 프로토타입  

```
ITMGAudioCtrl int EnableAudioCaptureDevice(bool isEnabled)
```

| 매개변수      | 유형 | 설명                                                         |
| --------- | :--: | ------------------------------------------------------------ |
| isEnabled | bool | 캡처 장치를 활성화하려면 이 매개변수를 true로 설정하십시오. 그렇지 않으면 false로 설정하십시오. |

#### 예시 코드

```
//캡처 장치 활성화
ITMGContext.GetInstance().GetAudioCtrl().EnableAudioCaptureDevice(true);
```

### 캡처 장치 상태 가져오기

이 API는 캡처 장치의 상태를 가져오는 데 사용됩니다.

#### API 프로토타입

```
ITMGAudioCtrl bool IsAudioCaptureDeviceEnabled()
```

#### 예시 코드

```
bool IsAudioCaptureDevice = ITMGContext.GetInstance().GetAudioCtrl().IsAudioCaptureDeviceEnabled();
```

### 오디오 업스트림 활성화 또는 비활성화

이 API는 오디오 업스트림을 활성화/비활성화하는 데 사용됩니다. 캡처 장치가 이미 활성화된 경우 캡처된 오디오 데이터를 보냅니다. 그렇지 않으면 음소거 상태로 유지됩니다. 캡처 장치를 활성화/비활성화하는 방법에 대한 자세한 내용은 EnableAudioCaptureDevice API를 참고하십시오.

#### API 프로토타입

```
ITMGAudioCtrl int EnableAudioSend(bool isEnabled)
```

| 매개변수      |  유형  | 설명                                                         |
| --------- | :--: | ------------------------------------------------------------ |
| isEnabled    |bool     |오디오 업스트림을 활성화하려면 이 매개변수를 true로 설정하십시오. 그렇지 않으면 false로 설정하십시오. |

#### 예시 코드  

```
ITMGContext.GetInstance().GetAudioCtrl().EnableAudioSend(true);
```

### 오디오 업스트림 상태 가져오기

이 API는 오디오 업스트림 상태를 가져오는 데 사용됩니다.

#### API 프로토타입  

```
ITMGAudioCtrl bool IsAudioSendEnabled()
```

#### 예시 코드  

```
bool IsAudioSend = ITMGContext.GetInstance().GetAudioCtrl().IsAudioSendEnabled();
```

### 실시간 마이크 볼륨 가져오기

이 API는 실시간 마이크 볼륨을 가져오는 데 사용됩니다. 0 - 100 범위의 int 유형 값이 반환됩니다. 이 API는 20ms마다 한 번씩 호출하는 것이 좋습니다.

 

#### API 프로토타입  

```
ITMGAudioCtrl int GetMicLevel
```

#### 예시 코드  

```
ITMGContext.GetInstance().GetAudioCtrl().GetMicLevel();
```

### 실시간 오디오 업스트림 볼륨 가져오기

이 API는 로컬 실시간 오디오 업스트림 볼륨을 가져오는 데 사용됩니다. 0 - 100 범위의 int 유형 값이 반환됩니다.

 

#### API 프로토타입  

```
ITMGAudioCtrl int GetSendStreamLevel()
```

#### 예시 코드  

```
int Level = ITMGContext.GetInstance().GetAudioCtrl().GetSendStreamLevel();
```

### 마이크 소프트웨어 볼륨 설정

이 API는 마이크 볼륨 레벨을 설정하는 데 사용됩니다. 해당 매개변수는 volume이며, 이는 캡처된 사운드에 대한 감쇠 또는 이득과 같습니다.

 

#### API 프로토타입  

```
ITMGAudioCtrl SetMicVolume(int volume)
```

| 매개변수   |  유형  | 설명                                                         |
| ------ | :--: | ------------------------------------------------------------ |
| volume | int  | 값 범위: 0–200. 기본값: 100. 0은 오디오가 음소거됨을 나타내고 100은 볼륨 레벨이 변경되지 않음을 나타냅니다. |

#### 예시 코드  

```
int micVol = (int)(value * 100);
ITMGContext.GetInstance().GetAudioCtrl().SetMicVolume (micVol);
```

### 마이크 소프트웨어 볼륨 가져오기

이 API는 마이크 볼륨을 가져오는 데 사용됩니다. int 값이 반환됩니다. 값 101은 API SetMicVolume이 호출되지 않았음을 나타냅니다.

 

#### API 프로토타입  

```
ITMGAudioCtrl GetMicVolume()
```

#### 예시 코드  

```
ITMGContext.GetInstance().GetAudioCtrl().GetMicVolume();
```

## 음성 채팅 재생 API

| API                     |            설명            |
| ------------------------ | :----------------------------: |
| EnableSpeaker            |           스피커 활성화/비활성화           |
| GetSpeakerState          |         스피커 상태 가져오기         |
| EnableAudioPlayDevice    |          재생 장치 활성화/비활성화          |
| IsAudioPlayDeviceEnabled |        재생 장치 상태 가져오기        |
| EnableAudioRecv          |        오디오 다운스트림 활성화/비활성화        |
| IsAudioRecvEnabled       |        오디오 다운스트림 상태 가져오기        |
| GetSpeakerLevel          |       실시간 스피커 볼륨 레벨 가져오기       |
| GetRecvStreamLevel       | 방에 있는 다른 구성원의 실시간 다운스트림 오디오 볼륨 레벨 가져오기 |
| SetSpeakerVolume         |         스피커 볼륨 레벨 설정         |
| GetSpeakerVolume         |         스피커 볼륨 레벨 가져오기         |


[](id:EnableSpeaker)	
### 스피커 활성화 또는 비활성화

이 API는 스피커를 활성화/비활성화하는 데 사용됩니다. **EnableSpeaker = EnableAudioPlayDevice +  EnableAudioRecv**

#### API 프로토타입  

```
ITMGAudioCtrl EnableSpeaker(bool isEnabled)
```

| 매개변수      |  유형  | 설명                                                         |
| --------- | :--: | ------------------------------------------------------------ |
| isEnabled | bool | 스피커를 비활성화하려면 이 매개변수를 false로 설정하십시오. 그렇지 않으면 true로 설정하십시오. |

#### 예시 코드  

```
//스피커 활성화
ITMGContext.GetInstance().GetAudioCtrl().EnableSpeaker(true);
```

### 스피커 상태 가져오기

이 API는 스피커 상태를 가져오는 데 사용됩니다. 0은 스피커가 꺼져 있음을 나타내고 1은 켜져 있음을 나타냅니다.

#### API 프로토타입  

```
ITMGAudioCtrl GetSpeakerState()
```

#### 예시 코드  

```
speakerToggle.isOn = ITMGContext.GetInstance().GetAudioCtrl().GetSpeakerState();
```



### 재생 장치 활성화 또는 비활성화

이 API는 재생 장치를 활성화/비활성화하는 데 사용됩니다.

#### API 프로토타입  

```
ITMGAudioCtrl EnableAudioPlayDevice(bool isEnabled)
```

| 매개변수      |  유형  | 설명                                                         |
| --------- | :--: | ------------------------------------------------------------ |
| isEnabled | bool | 재생 장치를 비활성화하려면 이 매개변수를 false로 설정하십시오. 그렇지 않으면 true로 설정하십시오. |

#### 예시 코드  

```
ITMGContext.GetInstance().GetAudioCtrl().EnableAudioPlayDevice(true);
```

### 재생 장치 상태 가져오기

이 API는 재생 장치의 상태를 가져오는 데 사용됩니다.

#### API 프로토타입

```
ITMGAudioCtrl bool IsAudioPlayDeviceEnabled()
```

#### 예시 코드  

```
bool IsAudioPlayDevice = ITMGContext.GetInstance().GetAudioCtrl().IsAudioPlayDeviceEnabled();
```

### 오디오 다운스트림 활성화 또는 비활성화

이 API는 오디오 다운스트림을 활성화/비활성화하는 데 사용됩니다. 재생 장치가 이미 활성화된 경우 방에 있는 다른 구성원의 오디오 데이터를 재생합니다. 그렇지 않으면 음소거 상태로 유지됩니다. 재생 장치를 활성화/비활성화하는 방법에 대한 자세한 내용은 EnableAudioPlayDevice API를 참고하십시오.

#### API 프로토타입  

```
ITMGAudioCtrl int EnableAudioRecv(bool isEnabled)
```

| 매개변수      |  유형  | 설명                                                         |
| --------- | :--: | ------------------------------------------------------------ |
| isEnabled | bool | 오디오 다운스트림을 활성화하려면 이 매개변수를 true로 설정하십시오. 그렇지 않으면 false로 설정하십시오. |

#### 예시 코드  

```
ITMGContext.GetInstance().GetAudioCtrl().EnableAudioRecv(true);
```



### 오디오 다운스트림 상태 가져오기

이 API는 오디오 다운스트림 상태를 가져오는 데 사용됩니다.

#### API 프로토타입  

```
ITMGAudioCtrl bool IsAudioRecvEnabled()
```

#### 예시 코드  

```
bool IsAudioRecv = ITMGContext.GetInstance().GetAudioCtrl().IsAudioRecvEnabled();
```

### 실시간 스피커 볼륨 가져오기

이 API는 실시간 스피커 볼륨을 가져오는 데 사용됩니다. 볼륨을 나타내기 위해 int 유형 값이 반환됩니다. 이 API는 20ms마다 한 번씩 호출하는 것이 좋습니다.

#### API 프로토타입  

```
ITMGAudioCtrl GetSpeakerLevel()
```

#### 예시 코드  

```
ITMGContext.GetInstance().GetAudioCtrl().GetSpeakerLevel();
```

### 방에 있는 다른 구성원의 실시간 다운스트림 오디오 레벨 가져오기

이 API는 방에 있는 다른 구성원의 실시간 오디오 다운스트림 볼륨을 가져오는 데 사용됩니다. int 유형 값이 반환됩니다. 값 범위: 0 - 200.

#### API 프로토타입  

```
ITMGAudioCtrl int GetRecvStreamLevel(string openId)
```

| 매개변수   |  유형  | 의미                  |
| ------ | :----: | --------------------- |
| openId | string | 방에 있는 다른 구성원의 openId |

#### 예시 코드  

```
int Level = ITMGContext.GetInstance().GetAudioCtrl().GetRecvStreamLevel(openId);
```

### 스피커 볼륨 설정

이 API는 스피커 볼륨을 설정하는 데 사용됩니다.

#### API 프로토타입  

```
ITMGAudioCtrl SetSpeakerVolume(int volume)
```

| 매개변수   |  유형  | 설명                                                         |
| ------ | :--: | ------------------------------------------------------------ |
| volume | int  | 값 범위: 0 – 200. 기본값: 100. 0은 오디오가 음소거됨을 나타내고 100은 볼륨 레벨이 변경되지 않음을 나타냅니다. |

#### 예시 코드  

```
int speVol = (int)(value * 100);
ITMGContext.GetInstance().GetAudioCtrl().SetSpeakerVolume(speVol);
```

### 스피커 볼륨 가져오기

이 API는 스피커 볼륨을 가져오는 데 사용됩니다. 볼륨을 나타내기 위해 int 유형 값이 반환됩니다. 101은 SetSpeakerVolume API가 호출되지 않았음을 나타냅니다.
Level은 실시간 Volume을 나타내고 Volume 은 스피커 볼륨을 나타냅니다. 최종 볼륨 = Level × Volume %. 예를 들어 레벨이 100이고 Volume이 60이면 최종 볼륨은 60입니다.

#### API 프로토타입  

```
ITMGAudioCtrl GetSpeakerVolume()
```

#### 예시 코드  

```
ITMGContext.GetInstance().GetAudioCtrl().GetSpeakerVolume();
```

## 장치 선택 API

장치 선택 API는 PC에서만 사용할 수 있습니다.

| API                        |       설명       |
| --------------------------- | :------------------: |
| GetMicListCount             |       마이크 수 가져오기       |
| GetMicList                  |         마이크 목록         |
| GetSpeakerListCount         |       스피커 수 가져오기       |
| GetSpeakerList              |         스피커 목록         |
| SelectMic                   |         마이크 선택         |
| SelectSpeaker               |         스피커 선택         |

### 마이크 수 가져오기

이 API는 마이크 수를 가져오는 데 사용됩니다.

#### 함수 프로토타입  

```
public abstract int GetMicListCount()

```

#### 예시 코드  

```
ITMGContext.GetInstance().GetAudioCtrl().GetMicListCount();
```

### 마이크 열거

이 API는 마이크를 열거하기 위해 GetMicListCount API와 함께 사용됩니다.

#### 함수 프로토타입 

```
public abstract int GetMicList(out List<TMGAudioDeviceInfo> devicesInfo, int count)

```

| 매개변수             |        유형        | 설명                 |
| ---------------- | :----------------: | -------------------- |
| ppDeviceInfoList | TMGAudioDeviceInfo | 장치 목록             |
| count           |        int         | 마이크의 수 |

| TMGAudioDeviceInfo 매개변수             |        유형        | 설명                 |
| ---------------- | :----------------: | ------------------- |
| m_strDeviceID | string | 장치 이름|
| m_strDeviceID | string |장치 ID |

#### 예시 코드  

```
ITMGContext.GetInstance().GetAudioCtrl().GetMicList(devicesInfo,count);
```



### 마이크 선택

이 API는 마이크를 선택하는 데 사용됩니다. 이 API가 호출되지 않거나 DEVICEID_DEFAULT가 전달되면 기본 마이크가 선택됩니다.
GetMicList API에서 반환되는 0번째 장치 id는 통화 장치의 기본 장치입니다. 선택된 통화 장치가 있으면 서비스에서 유지합니다. 만약 통화 장치의 플러그가 뽑히면 통화 장치가 다시 기본 장치로 변경됩니다.

#### 함수 프로토타입  

```
public abstract int SelectMic(string micID);
```

| 매개변수   | 유형  | 설명          |
| ------ | :---: | ------------- |
| pMicID | string | GetMicList에서 반환된 목록의 마이크 ID입니다. |

#### 예시 코드  

```
string deviceID = DEVICE_ID_DEFAULT;
                if (index != 0)
                {
                    deviceID = listMicInfo[index - 1].m_strDeviceID;
                }
                ITMGContext.GetInstance().GetAudioCtrl().SelectMic(deviceID);
                selectedMicID = deviceID;
```

이 API는 스피커 수를 가져오는 데 사용됩니다.

#### 함수 프로토타입  

```
public abstract int GetSpeakerListCount();

```

#### 예시 코드  

```
ITMGContext.GetInstance().GetAudioCtrl().GetSpeakerListCount();

```

### 스피커 열거

이 API는 GetSpeakerListCount API와 함께 스피커를 열거하는 데 사용됩니다.

#### 함수 프로토타입  

```
public abstract int GetSpeakerList(out List<TMGAudioDeviceInfo> devicesInfo, int count)
```

| 매개변수             |        유형        | 설명                 |
| ---------------- | :----------------: | -------------------- |
| ppDeviceInfoList | TMGAudioDeviceInfo | 장치 목록             |
| count           |        int         | 스피커 수 |

| TMGAudioDeviceInfo 매개변수             |        유형        | 설명                 |
| ---------------- | :----------------: | ------------------- |
| m_strDeviceID | string | 장치 이름|
| m_strDeviceID | string |장치 ID |

#### 예시 코드  

```
int speakerCount = ITMGContext.GetInstance().GetAudioCtrl().GetSpeakerListCount();
Debug.LogFormat("speakerCount = {0}", speakerCount);
if (speakerCount > 0)
	{
		int ret = ITMGContext.GetInstance().GetAudioCtrl().GetSpeakerList(out listSpeakerInfo, speakerCount);
		Debug.LogFormat("GetSpeakerList ret = {0}", ret);
		if (ret != 0)
		{
			listSpeakerInfo = null;
		}
	}
}
```

### 스피커 선택

이 API는 재생 장치를 선택하는 데 사용됩니다. 이 API가 호출되지 않거나 "DEVICEID_DEFAULT"가 전달되면 기본 재생 장치가 선택됩니다.

#### 함수 프로토타입  

```
public abstract int SelectSpeaker(string speaker);

```

| 매개변수       | 유형  | 설명          |
| ---------- | :---: | ------------- |
| speaker | string | GetSpeakerList에 의해 반환된 목록의 스피커 ID입니다. |

#### 예시 코드  

```
speakerDropdown = transform.Find("DevicePanel/SpeakerSelect").GetComponent<Dropdown>();
        if (speakerDropdown != null)
        {
            speakerDropdown.onValueChanged.AddListener(delegate (int index)
            {
                string deviceID = DEVICE_ID_DEFAULT;
                if (index != 0)
                {
                    deviceID = listSpeakerInfo[index - 1].m_strDeviceID;
                }
                ITMGContext.GetInstance().GetAudioCtrl().SelectSpeaker(deviceID);
                selectedSpeakerID = deviceID;
            });
        }
```


## 고급 API

### 인이어 모니터링 활성화

이 API는 인이어 모니터링을 활성화하는 데 사용됩니다. 자신의 목소리를 듣기 전에 EnableLoopBack+EnableSpeaker를 호출해야 합니다.

#### API 프로토타입  

```
ITMGContext GetAudioCtrl EnableLoopBack(bool enable)
```

| 매개변수    | 유형   | 의미      |
| ------ | :--: | ------------ |
| enable | bool | 사용 여부를 지정합니다 |

#### 예시 코드  

```
ITMGContext.GetInstance().GetAudioCtrl().EnableLoopBack(true);
```

### 장치 사용 및 릴리스에 대한 콜백

방에서 장치를 사용하거나 해제한 후에 이벤트 메시지를 전달하기 위해 델리게이트 함수를 통해 콜백이 실행됩니다.

```
public delegate void QAVOnDeviceStateChangedEvent(int deviceType, string deviceId, bool openOrClose);
public abstract event QAVOnDeviceStateChangedEvent OnDeviceStateChangedEvent;
```

| 매개변수        |  유형  | 설명                                                  |
| ----------- | :----: | ----------------------------------------------------- |
| deviceType  |  int   | <li>1: 캡처 장치<li>2: 재생 장치                  |
| deviceId    | string | 장치를 식별하는 데 사용되는 장치 GUID는 Windows 및 Mac에만 적용됩니다 |
| openOrClose |  bool  | 캡처/재생 장치 점유 또는 릴리스                         |

#### 예시 코드  

```
이벤트 수신:
ITMGContext.GetInstance().GetAudioCtrl().OnDeviceStateChangedEvent += new QAVAudioDeviceStateCallback(OnAudioDeviceStateChange);
수신된 이벤트 처리:
void QAVAudioDeviceStateCallback(int deviceType, string deviceId, bool openOrClose){
    //장치 점유 및 릴리스에 대한 콜백
}
```

### 사용자 방 오디오 유형 가져오기

이 API는 사용자의 방 오디오 유형을 가져오는 데 사용됩니다. 반환되는 값은 방 오디오 유형입니다. 값 0은 사용자의 방 오디오 유형을 가져오는 동안 오류가 발생했음을 나타냅니다. 방 오디오 유형에 대해서는 EnterRoom API를 참고하십시오.

#### API 프로토타입  

```
ITMGContext ITMGRoom public  int GetRoomType()
```

#### 예시 코드  

```
ITMGContext.GetInstance().GetRoom().GetRoomType();
```

### 방 유형 변경

이 API는 사용자의 방 오디오 유형을 수정하는 데 사용됩니다. 결과는 콜백 이벤트를 참고하십시오. 이벤트 유형은 ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE입니다. 방의 오디오 유형은 방에 들어오는 첫 번째 사용자에 의해 결정됩니다. 이후 방에 있는 구성원이 방 유형을 변경하면 모든 구성원에게 적용됩니다.
#### API 프로토타입  

```
ITMGContext ITMGRoom public int ChangeRoomType(ITMGRoomType roomtype)
```

| 매개변수     |     유형     | 설명                                                  |
| -------- | :----------: | ----------------------------------------------------- |
| roomtype | ITMGRoomType | 전환할 방 유형입니다. 방 오디오 유형에 대해서는 EnterRoom API를 참고하십시오.  |

#### 예시 코드  

```
ITMGContext.GetInstance().GetRoom().ChangeRoomType(ITMG_ROOM_TYPE_FLUENCY);
```

#### 콜백 이벤트

방 유형을 설정합니다. 방 유형이 설정되면 델리게이트 함수를 통해 콜백을 실행하여 수정이 완료되었음을 알리는 메시지를 전달합니다.

| 반환된 매개변수 |            설명            |
| ---------- | :------------------------: |
| roomtype   | 업데이트된 roomtype 반환 |

```
public abstract event QAVCallback OnChangeRoomtypeCallback;
public abstract event QAVOnRoomTypeChangedEvent OnRoomTypeChangedEvent;
```

#### 예시 코드  

```
//이벤트 수신:
ITMGContext.GetInstance ().OnRoomTypeChangedEvent += new QAVOnRoomTypeChangedEvent (OnRoomTypeChangedEvent);
//수신된 이벤트 처리:
void OnRoomTypeChangedEvent(int roomtype)
{
        ShowWarnning (string.Format ("RoomTypeChanged current:{0}",roomtype));
}
```

#### 방 유형 변경 알림

방 유형이 귀하 또는 방의 다른 사용자에 의해 변경되면 이 알림 이벤트는 비즈니스 레이어에 방 유형 변경을 알리는 데 사용됩니다. 반환되는 값은 방 유형입니다. 자세한 내용은 EnterRoom API를 참고하십시오.

```
public delegate void QAVOnRoomTypeChangedEvent(int roomtype);
public abstract event QAVOnRoomTypeChangedEvent OnRoomTypeChangedEvent;	
```

#### 예시 코드  

```
//이벤트 수신:
ITMGContext.GetInstance().OnRoomTypeChangedEvent += new QAVOnRoomTypeChangedEvent(OnRoomTypeChangedEvent);
//수신된 이벤트 처리:
void OnRoomTypeChangedEvent(int roomtype){
    //방 유형 변경 후 콜백 전송
}
```



### 방 통화 품질 모니터링 이벤트

네트워크 품질을 수신하는 데 사용되는 품질 모니터링 이벤트입니다. 네트워크 상태가 좋지 않으면 비즈니스 레이어에서 UI를 통해 네트워크를 전환하도록 요청합니다. 이 이벤트는 방 입장 후 2초마다 한 번씩 발생하며 메시지는 ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_QUALITY입니다. 반환된 매개변수에는 weight, loss 및 delay가 포함되며 아래에 자세히 설명되어 있습니다.

| 매개변수   | 유형   | 의미                                                         |
| ------ | ------ | ------------------------------------------------------------ |
| weight | int    | 값 범위: 1 - 50. 50은 우수한 음질을 나타내고, 1은 매우 열악한(거의 사용할 수 없는) 음질을 나타내며, 0은 초기 의미 없는 값을 나타냅니다. 일반적으로 값이 30 미만이면 비즈니스 레이어에서 사용자에게 네트워크 상태가 좋지 않음을 알리고 네트워크 전환을 권장합니다. |
| loss   | double | 업스트림 패킷 손실률.|
| delay  | int    | 음성 채팅 지연(ms).                                     |




### 버전 번호 가져오기

이 API는 분석을 위한 SDK 버전 번호를 가져오는 데 사용됩니다.

#### API 프로토타입

```
ITMGContext  abstract string GetSDKVersion()
```

#### 예시 코드  

```
ITMGContext.GetInstance().GetSDKVersion();
```



### 로그 출력 레벨 설정

이 API는 출력할 로그의 수준을 설정하는 데 사용되며 초기화 전에 호출해야 합니다. 기본 수준을 유지하는 것이 좋습니다.

#### API 프로토타입

```
ITMGContext  SetLogLevel(ITMG_LOG_LEVEL levelWrite, ITMG_LOG_LEVEL levelPrint)
```

#### 매개변수 설명

| 매개변수       | 유형           | 설명                                                         |
| ---------- | -------------- | ------------------------------------------------------------ |
| levelWrite | ITMG_LOG_LEVEL | 기록할 로그 수준을 설정합니다. TMG_LOG_LEVEL_NONE은 쓰지 않음을 나타냅니다. 기본값: TMG_LOG_LEVEL_INFO |
| levelPrint | ITMG_LOG_LEVEL | 출력할 로그의 수준을 설정합니다. TMG_LOG_LEVEL_NONE은 인쇄하지 않음을 나타냅니다. 기본값: TMG_LOG_LEVEL_ERROR |

ITMG_LOG_LEVEL은 아래와 같습니다.

| ITMG_LOG_LEVEL        | 설명                 |
| --------------------- | -------------------- |
| TMG_LOG_LEVEL_NONE    | 로그를 출력하지 않음           |
| TMG_LOG_LEVEL_ERROR   | 에러 로그 출력(기본값) |
| TMG_LOG_LEVEL_INFO    | 정보 로그 출력         |
| TMG_LOG_LEVEL_DEBUG   | 디버그 로그 출력     |
| TMG_LOG_LEVEL_VERBOSE | 고빈도 로그 출력         |

#### 예시 코드  

```
ITMGContext.GetInstance().SetLogLevel(TMG_LOG_LEVEL_INFO,TMG_LOG_LEVEL_INFO);
```



### 로그 출력 경로 설정

이 API는 로그 출력 경로를 설정하는 데 사용됩니다. 기본 경로는 다음과 같습니다. Init 전에 호출해야 합니다.

| 플랫폼    | 경로                                                         |
| ------- | ------------------------------------------------------------ |
| Windows | %appdata%\Tencent\GME\ProcessName                            |
| iOS     | Application/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/Documents   |
| Android | /sdcard/Android/data/xxx.xxx.xxx/files                       |
| Mac     | /Users/username/Library/Containers/xxx.xxx.xxx/Data/Documents |

#### API 프로토타입

```
ITMGContext  SetLogPath(string logDir)

```

| 매개변수   |  유형  | 설명 |
| ------ | :----: | ---- |
| logDir | String | 경로 |

#### 예시 코드  

```
ITMGContext.GetInstance().SetLogPath(path);

```

### 진단 메시지 가져오기

이 API는 실시간 음성/화상 통화 품질에 대한 정보를 얻는 데 사용되며, 주로 실시간 통화 품질을 보고 문제를 해결하는 데 사용되며 비즈니스 측면에서는 무시할 수 있습니다.

#### API 프로토타입  

```
ITMGRoom GetQualityTips()
```

#### 예시 코드  

```
string tips = ITMGContext.GetInstance().GetRoom().GetQualityTips();

```
