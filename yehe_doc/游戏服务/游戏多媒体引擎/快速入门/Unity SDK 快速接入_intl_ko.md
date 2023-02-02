본문에서는 Unity 프로젝트 개발자가 GME(Game Multimedia Engine)용 API를 쉽게 디버깅하고 통합할 수 있도록 자세한 설명을 제공합니다.

이 문서는 API 디버깅 및 통합을 위해 GME를 시작하는 데 도움이 되는 기본 API만 제공합니다.

## GME 사용 시 주의할 점

GME는 실시간 음성 채팅 서비스와 음성 메시지 및 음성-텍스트 변환 서비스의 두 가지 서비스를 제공하며 둘 다 Init 및 Poll과 같은 주요 API에 의존합니다.

<dx-alert infotype="notice" title="Init API 정보">
실시간 음성 채팅과 음성 메시지 서비스를 동시에 사용해야 하는 경우 **Init API를 한 번만 호출하면 됩니다**.
</dx-alert>

### API 호출 순서도

![image](https://qcloudimg.tencent-cloud.cn/raw/c8758a24fe68fc084b8d12b09de5e27a.jpg)

### 액세스 단계

#### SDK 통합

SDK를 프로젝트에 통합하려면 [Integrating SDK](https://intl.cloud.tencent.com/document/product/607/10783)를 참고하십시오.

#### 주요 API

- <dx-tag-link link="#Init" tag="API: Init">GME 초기화</dx-tag-link>
- <dx-tag-link link="#Poll" tag="API: Poll">이벤트 콜백을 트리거하기 위해 주기적으로 Poll 호출</dx-tag-link>
- <dx-tag-link link="#Complete" tag="수신: QAVEnterRoomComplete">방 입/퇴장 알림 수신</dx-tag-link>

#### 실시간 음성 채팅

<dx-steps>
-<dx-tag-link link="#EnterRoom" tag="API: EnterRoom">음성 채팅방 입장</dx-tag-link>
-<dx-tag-link link="#EnableMic" tag="API: EnableMic">마이크 활성화 또는 비활성화</dx-tag-link>
-<dx-tag-link link="#EnableSpeaker" tag="API: EnableSpeaker">스피커 활성화 또는 비활성화</dx-tag-link>
-<dx-tag-link link="#ExitRoom" tag="API: ExitRoom">음성 채팅방 퇴장</dx-tag-link>
</dx-steps>

#### 음성 메시지

<dx-steps>
-<dx-tag-link link="#ApplyPtt" tag="API: ApplyPTTAuthbuffer">인증 초기화</dx-tag-link>
-<dx-tag-link link="#StartRWSR" tag="API: StartRecordingWithStreamingRecognition">스트리밍 음성 인식 시작</dx-tag-link>
-<dx-tag-link link="#Stop" tag="API: StopRecording">녹화 중지</dx-tag-link>
</dx-steps>

- <dx-tag-link link="#Init" tag="API: UnInit">GME 초기화 해제</dx-tag-link>

## 주요 API 액세스

### 1. SDK 다운로드 

SDK 다운로드 가이드 페이지에서 적절한 <dx-tag-link link="https://intl.cloud.tencent.com/document/product/607/18521" tag="DownLoad">클라이언트 SDK</dx-tag-link>를 다운로드합니다.

### 2. 헤더 파일 가져오기

```
using GME;
```

### 3. Context 인스턴스 가져오기

QAVContext.GetInstance() 대신 ITMGContext 메소드를 사용하여 Context 인스턴스를 가져옵니다.

#### 예시 코드  

```
int ret = ITMGContext.GetInstance().Init(sdkAppId, openID);
```

### [4. SDK 초기화](id:Init)

실시간 음성, 음성 메시지, 음성 텍스트 변환 서비스를 사용하려면 먼저 **Init API를 통해 SDK를 초기화해야 합니다**. Init API는 다른 API와 동일한 스레드에서 호출해야 합니다. 기본 스레드에서 모든 API를 호출하는 것이 좋습니다.

#### API 프로토타입

```
//class ITMGContext
public abstract int Init(string sdkAppID, string openID);
```

| 매개변수     | 유형  | 설명                                                         |
| -------- | :----: | ------------------------------------------------------------ |
| sdkAppId | string | [GME 콘솔](https://console.cloud.tencent.com/gamegme)에서 제공되는 AppID는 [서비스 활성화](https://intl.cloud.tencent.com/document/product/607/10782)에 안내된 대로 얻을 수 있습니다. |
| openID   | string | openID는 Int64 유형만 가능하며 문자열로 변환되어 전달됩니다. 해당 규칙을 사용자 정의할 수 있으며 App에서 고유해야 합니다. Openid를 문자열로 전달하려면 [Submit Ticket](https://console.cloud.tencent.com/workorder/category?level1_id=438&level2_id=445&source=0&data_title=%E6%B8%B8%E6%88%8F%E5%A4%9A%E5%AA%92%E4%BD%93%E5%BC%95%E6%93%8EGME&step=1)하여 신청하십시오.|

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

### [5. 이벤트 콜백 트리거](id:Poll)

이벤트 콜백은 update에서 Poll API를 주기적으로 호출하여 트리거할 수 있습니다. Poll API는 GME의 메시지 펌프이며 GME가 이벤트 콜백을 트리거하도록 주기적으로 호출해야 합니다. 그렇지 않으면 전체 SDK 서비스가 비정상적으로 실행됩니다. 자세한 내용은 [SDK 다운로드 가이드](https://intl.cloud.tencent.com/document/product/607/18521)의 EnginePollHelper 파일을 참고하십시오.

#### 예시 코드

```
public void Update()
  {
      ITMGContext.GetInstance().Poll();
  }
```

### [6. 방 입/퇴장 알림 수신](id:Complete)

#### 방 입장 알림

```
//위임 함수: 
public delegate void QAVEnterRoomComplete(int result, string error_info);
//이벤트 트리거 함수: 
public abstract event QAVEnterRoomComplete OnEnterRoomCompleteEvent;
```

#### 방 퇴장 알림

```
위임 함수: 
ublic delegate void QAVExitRoomComplete();
이벤트 트리거 함수: 
public abstract event QAVExitRoomComplete OnExitRoomCompleteEvent;
```

### 7. 로컬 인증 키 계산

관련 기능의 암호화 및 인증을 위해 AuthBuffer를 생성합니다. 프로덕션 환경에서 릴리스하려면 [Authentication Key](https://intl.cloud.tencent.com/document/product/607/12218)에 설명된 대로 백엔드 배포 키를 사용하십시오.    

#### API 프로토타입

```
QAVAuthBuffer GenAuthBuffer(int appId, string roomId, string openId, string key)
```

| 매개변수   | 유형  | 설명                                                         |
| ------ | :----: | ------------------------------------------------------------ |
| appId  |  int   | Tencent Cloud 콘솔의 AppId.                              |
| roomId | string | 방 ID, 최대 127자 지원(음성 메시지의 경우 null 입력).   |
| openId | string | 사용자 ID. Init 시 openId와 동일.                       |
| key    | string | Tencent Cloud [콘솔](https://console.cloud.tencent.com/gamegme)의 권한 키. |

#### 예시 코드  

```
public static byte[] GetAuthBuffer(string AppID, string RoomID,string OpenId, string AuthKey){
    return QAVAuthBuffer.GenAuthBuffer(int.Parse(AppID), RoomID, OpenId, AuthKey);
}

```

## 실시간 음성 채팅 액세스

### [1. 방 입장](id:EnterRoom)

생성된 인증 정보로 방에 입장하기 위해 사용하는 API입니다. 방 입장 후 마이크와 스피커는 기본적으로 활성화되지 않습니다. 반환된 AV_OK 값은 API 호출은 성공했지만 방 입장은 성공하지 못했다는 의미입니다.

#### API 프로토타입

```
ITMGContext EnterRoom(string roomId, int roomType, byte[] authBuffer)
```

| 매개변수     |  유형  | 설명                    |
| ---------- | :----: | ----------------------- |
| roomId     | String | 방 ID, 최대 127자 지원 |
| roomType   | ITMGRoomType | ITMGRoomType.ITMG_ROOM_TYPE_FLUENCY 입력 |
| authBuffer | byte[] | 인증 코드                  |

#### 예시 코드  

```
ITMGContext.GetInstance().EnterRoom(strRoomId, ITMGRoomType.ITMG_ROOM_TYPE_FLUENCY, byteAuthbuffer);
```

#### 방 입장 콜백

사용자가 방에 들어가면 방 입장 결과가 다시 호출되어 처리를 위해 들을 수 있습니다. 성공적인 콜백은 방 입장이 성공적이며 **과금**이 시작됨을 의미합니다.

<dx-fold-block title="과금 참고">
[Purchase Guide](https://intl.cloud.tencent.com/document/product/607/50009)
[Billing](https://intl.cloud.tencent.com/document/product/607/30255)
[음성 채팅 사용 시 클라이언트가 서버와 연결이 끊긴 경우에도 계속 과금됩니까?](https://intl.cloud.tencent.com/document/product/607/30255#.E4.BD.BF.E7.94.A8.E5.AE.9E.E6.97.B6.E8.AF.AD.E9.9F.B3.E5.90.8E.EF.BC.8C.E5.A6.82.E6.9E.9C.E5.AE.A2.E6.88.B7.E7.AB.AF.E6.8E.89.E7.BA.BF.E4.BA.86.EF.BC.8C.E6.98.AF.E5.90.A6.E8.BF.98.E4.BC.9A.E7.BB.A7.E7.BB.AD.E8.AE.A1.E8.B4.B9.EF.BC.9F)
</dx-fold-block>

- **예시 코드**  
  콜백 처리를 위한 예시 코드입니다.
```
//이벤트 수신:
ITMGContext.GetInstance().OnEnterRoomCompleteEvent += new QAVEnterRoomComplete(OnEnterRoomComplete);
//수신된 이벤트 처리:
void OnEnterRoomComplete(int err, string errInfo)
{
  if (err != 0) {
    ShowLoginPanel("에러 코드:" + err + " 에러 메시지:" + errInfo);
    return;
  }
  else{
	//방 입장 성공
  }
}
```

- **에러 코드**
<table>
<thead>
<tr>
<th>에러 코드 값</th>
<th>원인 및 권장 방안</th>
</tr>
</thead>
<tbody><tr>
<td>7006</td>
<td>인증 실패. 가능한 원인들: <ul><li>AppID 가 존재하지 않거나 올바르지 않음</li><li>authbuff를 인증하는 동안 오류 발생</li><li>인증 만료 </li><li>openId 사양 불충족</li></ul></td>
</tr>
<tr>
<td>7007</td>
<td>이미 다른 방에 있음</td>
</tr>
<tr>
<td>1001</td>
<td>사용자는 이미 방에 들어가는 과정에 있었지만 이 작업을 반복했습니다. 방 입장 콜백이 반환될 때까지 방 입장 API를 호출하지 않는 것이 좋습니다.</td>
</tr>
<tr>
<td>1003</td>
<td>사용자가 이미 방에 있었고 API를 입력하는 방을 다시 호출함</td>
</tr>
<tr>
<td>1101</td>
<td>SDK가 초기화되었는지, openId가 규칙을 준수하는지, API가 동일한 스레드에서 호출되는지, Poll API가 정상적으로 호출되는지 확인</td>
</tr>
</tbody></table>





### [2. 마이크 활성화 또는 비활성화](id:EnableMic)

이 API는 마이크를 활성화/비활성화하는 데 사용됩니다. 방 입장 후 마이크와 스피커는 기본적으로 활성화되어 있지 않습니다.

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
  }
  else{
	//방 입장 성공
	//마이크 활성화
    ITMGContext.GetInstance().GetAudioCtrl().EnableMic(true);
  }
}
```

### [3. 스피커 활성화 또는 비활성화](id:EnableSpeaker)

이 API는 스피커를 활성화/비활성화하는 데 사용됩니다.

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
  }
  else{
	//방 입장 성공
    //스피커 활성화
    ITMGContext.GetInstance().GetAudioCtrl().EnableSpeaker(true);
  }
}
```

### [4. 방 퇴장](id:ExitRoom)

이 API는 현재 방을 나가기 위해 호출됩니다. 종료를 위해 콜백을 기다리고 처리해야 합니다.

#### 예시 코드  

```
ITMGContext.GetInstance().ExitRoom();
```

#### 방 퇴장 콜백

사용자가 방을 나가면 콜백이 반환됩니다. 예시 코드는 아래와 같습니다.

```
이벤트 수신:
ITMGContext.GetInstance().OnExitRoomCompleteEvent += new QAVExitRoomComplete(OnExitRoomComplete);
수신된 이벤트 처리:
void OnExitRoomComplete(){
//방 퇴장 후 콜백 전송
}
```



## 음성 메시지 액세스

### [1. 인증 초기화](id:ApplyPtt)

SDK 초기화 후 인증 초기화를 호출합니다. authBuffer를 얻는 방법에 대한 자세한 내용은 genAuthBuffer(실시간 음성 채팅 인증 정보 API)를 참고하십시오.

#### API 프로토타입  

```
ITMGPTT int ApplyPTTAuthbuffer (byte[] authBuffer)
```

| 매개변수       |  유형  | 설명                    |
| ---------- | :----: | ---- |
| authBuffer | String | 인증 |

#### 예시 코드  

```
UserConfig.SetAppID(transform.Find ("appId").GetComponent<InputField> ().text);
UserConfig.SetUserID(transform.Find ("userId").GetComponent<InputField> ().text);
UserConfig.SetAuthKey(transform.Find("authKey").GetComponent<InputField>().text);
byte[] authBuffer = UserConfig.GetAuthBuffer(UserConfig.GetAppID(), UserConfig.GetUserID(), null,UserConfig.GetAuthKey());
ITMGContext.GetInstance ().GetPttCtrl ().ApplyPTTAuthbuffer(authBuffer);
```

### [2. 스트리밍 음성 인식 시작](id:StartRWSR)

이 API는 스트리밍 음성 인식을 시작하는 데 사용됩니다. 음성-텍스트로 변환에서 얻은 텍스트는 콜백에서 실시간으로 반환됩니다. **녹음을 중지하려면 StopRecording을 호출합니다**. 녹음이 중지된 후 콜백이 반환됩니다.

#### API 프로토타입  

```
ITMGPTT int StartRecordingWithStreamingRecognition(string filePath)
```

| 매개변수              |  유형  | 설명                                                         |
| ----------------- | :----: | ------------------------------------------------------------ |
| filePath          | String | 저장된 오디오 파일의 경로                                               |


#### 예시 코드  

```
string recordPath = Application.persistentDataPath + string.Format("/{0}.silk", sUid++);
int ret = ITMGContext.GetInstance().GetPttCtrl().StartRecordingWithStreamingRecognition(recordPath);
```

#### 스트리밍 음성 인식 콜백

스트리밍 음성 인식이 시작된 후 OnStreamingSpeechComplete 또는 OnStreamingSpeechisRunning 알림에서 콜백 메시지를 수신해야 합니다. 자세한 내용은 아래와 같습니다.

- `OnStreamingSpeechComplete`은 녹화가 중지되고 인식이 완료된 후 텍스트를 반환합니다. 이는 음성 단락 이후에 인식된 텍스트를 반환하는 것과 같습니다.
- `OnStreamingSpeechisRunning`은 녹음 중 실시간으로 인식된 텍스트를 반환합니다. 이는 말하는 동안 인식된 텍스트를 반환하는 것과 같습니다.

이벤트 메시지는 실제 필요에 따라 OnEvent 함수에서 식별됩니다. 전달된 매개변수에는 다음 네 가지 메시지가 포함됩니다.

| 메시지 이름  |                    설명                     |
| --------- | :-----------------------------------------: |
| result    |    스트리밍 음성 인식 성공 여부를 판단하기 위한 반환 코드     |
| text      |            음성에서 변환된 텍스트             |
| file_path |             저장된 녹음 파일의 로컬 경로              |
| file_id   | 90일 동안 보관되는 녹음 파일의 백엔드 url 주소 |

- **예시 코드**  
```
//이벤트 수신:
ITMGContext.GetInstance().GetPttCtrl().OnStreamingSpeechComplete +=new QAVStreamingRecognitionCallback (OnStreamingSpeechComplete);
ITMGContext.GetInstance().GetPttCtrl().OnStreamingSpeechisRunning += new QAVStreamingRecognitionCallback (OnStreamingRecisRunning);
//수신된 이벤트 처리:
void OnStreamingSpeechComplete(int code, string fileid, string filepath, string result){
    //스트리밍 음성 인식을 위한 콜백
}
void OnStreamingRecisRunning(int code, string fileid, string filePath, string result){
    if (code == 0)
    {
        setBtnText(mStreamBtn, "스트리밍");
        InputField field = transform.Find("recordFilePath").GetComponent<InputField>();
        field.text = filePath;
            field = transform.Find("downloadUrl").GetComponent<InputField>();
        field.text = "Stream is Running";
            field = transform.Find("convertTextResult").GetComponent<InputField>();
        field.text = result;
        showWarningText("녹화 중");
    }    
}
```

- **에러 코드**
<table>
<thead>
<tr>
<th>에러 코드</th>
<th align="center">설명</th>
<th align="center">제안된 솔루션</th>
</tr>
</thead>
<tbody><tr>
<td>32775</td>
<td align="center">스트리밍 음성을 텍스트로 변환하는 데 실패했지만 녹음은 성공함</td>
<td align="center">UploadRecordedFile API를 호출하여 녹음 파일을 업로드한 다음 SpeechToText API를 호출하여 음성을 텍스트로 변환</td>
</tr>
<tr>
<td>32777</td>
<td align="center">스트리밍 음성을 텍스트로 변환하는 데 실패했지만 녹음 및 업로드는 성공함</td>
<td align="center">반환된 메시지에는 업로드 성공 후 백엔드 url이 포함되어 있으며, SpeechToText API를 호출하여 음성을 텍스트로 변환</td>
</tr>
<tr>
<td>32786</td>
<td align="center">스트리밍 음성-텍스트 변환 실패</td>
<td align="center">스트리밍 녹화 중 스트리밍 녹화 API의 실행 결과가 반환될 때까지 기다리십시오</td>
</tr>
</tbody></table>



### [3. 녹음 중지](id:Stop)

이 API는 녹음을 중지하는 데 사용됩니다. 비동기식이며 녹음이 중지된 후 녹음 완료에 대한 콜백이 반환됩니다. 녹음 파일은 녹음이 성공한 후에만 사용할 수 있습니다.

#### API 프로토타입  

```
ITMGPTT int StopRecording()
```

#### 예시 코드  

```
ITMGContext.GetInstance().GetPttCtrl().StopRecording();
```
