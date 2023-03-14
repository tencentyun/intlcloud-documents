본문은 Unity 음성 메시지 및 음성-텍스트 변환 서비스용 GME(Game Multimedia Engine) 클라이언트 API를 통합하고 디버깅하는 방법을 설명합니다.

## GME 사용을 위한 주요 고려 사항

GME는 Init 및 Poll과 같은 핵심 API에 의존하는 실시간 음성, 음성 메시지 및 음성 텍스트 변환 서비스를 제공합니다.

#### 주요 사항
- [서비스 활성화](https://intl.cloud.tencent.com/document/product/607/10782)에 설명된 대로 GME 애플리케이션을 생성하고 SDK의 AppID 및 Key를 가져옵니다.

- [서비스 활성화](https://intl.cloud.tencent.com/document/product/607/10782)에 설명된 대로 **GME의 실시간 음성, 음성 메시지 및 음성 텍스트 변환 서비스**를 활성화했습니다.

- GME를 사용하기 전에 프로젝트를 구성하십시오. 그렇지 않으면 SDK가 적용되지 않습니다.

- GME API가 성공적으로 호출되면 QAVError.OK가 0 값으로 반환됩니다.

- GME API는 동일한 스레드에서 호출되어야 합니다.

- GME가 이벤트 콜백을 트리거하려면 Poll API를 주기적으로 호출해야 합니다.

- 자세한 에러 코드는 [에러 코드](https://intl.cloud.tencent.com/document/product/607/33223)를 참고하십시오.
  

   >!
   > 
   > 음성-텍스트 변환 API는 기본 빈도 제한이 있습니다. 한도 내 과금 방식은 [구매 가이드](https://intl.cloud.tencent.com/document/product/607/50009)를 참고하십시오. 한도를 늘리고 싶거나 빈도 초과 시 과금 방식에 대해 자세히 알아보려면 비즈니스 매니저에게 문의하거나 [티켓 제출](https://console.cloud.tencent.com/workorder/category?level1_id=438&level2_id=445&source=0&data_title=%E6%B8%B8%E6%88%8F%E5%A4%9A%E5%AA%92%E4%BD%93%E5%BC%95%E6%93%8EGME&step=1)하시기 바랍니다.
   >   - 음성 메시지 비스트리밍 텍스트 변환 API **SpeechToText()**: 단일 계정 기본 동시 연결 수는 10개 입니다
   >   - 음성 메시지 스트리밍 텍스트 변환 API **StartRecordingWithStreamingRecognition()**: 단일 계정 기본 동시 연결 수는 50개 입니다
   >   - 실시간 음성 채팅 스트리밍 텍스트 변환 API **StartRealTimeASR()**: 단일 계정 기본 동시 연결 수는 50개 입니다


## SDK에 연결

### 중요 단계

SDK 연결 관련 주요 프로세스는 다음과 같습니다.

![](https://qcloudimg.tencent-cloud.cn/raw/c8758a24fe68fc084b8d12b09de5e27a.jpg)
1. [GME 초기화](https://write.woa.com/document/102980915702525952)

2. [주기적 Poll 호출을 통해 콜백 트리거하기](https://write.woa.com/document/102980915702525952)

3. [인증 초기화](https://write.woa.com/document/102980915702525952)

4. [스트리밍 음성 인식 시작](https://write.woa.com/document/102980915702525952)

5. [녹음 중지](https://write.woa.com/document/102980915702525952)

6. [GME 초기화 해제](https://write.woa.com/document/102980915702525952)


### C# 클래스
<table>
<tr>
<td rowspan="1" colSpan="1" >클래스</td>
<td rowspan="1" colSpan="1" >설명</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >ITMGContext</td>
<td rowspan="1" colSpan="1" >핵심 API</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >ITMGPTT</td>
<td rowspan="1" colSpan="1" >음성 메시지 및 음성-텍스트 변환 API</td>
</tr>
</table>


## 주요 API
<table>
<tr>
<td rowspan="1" colSpan="1" >API</td>
<td rowspan="1" colSpan="1" >설명</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >Init</td>
<td rowspan="1" colSpan="1" >GME 초기화</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >Poll</td>
<td rowspan="1" colSpan="1" >이벤트 콜백 트리거</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >Pause</td>
<td rowspan="1" colSpan="1" >시스템 일시 중지</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >Resume</td>
<td rowspan="1" colSpan="1" >시스템 재개</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >Uninit</td>
<td rowspan="1" colSpan="1" >GME 초기화 해제</td>
</tr>
</table>


### 헤더 파일 가져오기
``` bash
using TencentMobileGaming;
```

### 인스턴스 가져오기

QAVContext.GetInstance() 대신 ITMGContext 메소드를 사용하여 Context 인스턴스를 가져옵니다.

### SDK 초기화

실시간 음성, 음성 메시지, 음성 텍스트 변환 서비스를 사용하려면 먼저 **Init API를 통해 SDK를 초기화해야 합니다**. Init API는 다른 API와 동일한 스레드에서 호출해야 합니다. 기본 스레드에서 모든 API를 호출하는 것이 좋습니다.

#### API 프로토타입
``` bash
//class ITMGContext
public abstract int Init(string sdkAppID, string openID);
```
<table>
<tr>
<td rowspan="1" colSpan="1" >매개변수</td>
<td rowspan="1" colSpan="1" >유형</td>
<td rowspan="1" colSpan="1" >설명</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >sdkAppId</td>
<td rowspan="1" colSpan="1" >string</td>
<td rowspan="1" colSpan="1" ><a href="https://console.cloud.tencent.com/gamegme">GME 콘솔에서 제공되는 AppID는 <a href="https://intl.cloud.tencent.com/document/product/607/10782#.E9.87.8D.E7.82.B9.E5.8F.82.E6.95.B0">서비스 활성화</a>의 안내에 따라 얻을 수 있습니다.</td>
<tr>
<td rowspan="1" colSpan="1" >openID</td>
<td rowspan="1" colSpan="1" >string</td>
<td rowspan="1" colSpan="1" >openID는 Int64 유형만 가능하며 문자열로 변환되어 전달됩니다. 해당 규칙을 사용자 정의할 수 있으며 App에서 고유해야 합니다. openID를 문자열로 전달하기 위해서는 <a href="https://console.cloud.tencent.com/workorder/category?level1_id=438&level2_id=445&source=0&data_title=%E6%B8%B8%E6%88%8F%E5%A4%9A%E5%AA%92%E4%BD%93%E5%BC%95%E6%93%8EGME&step=1">티켓 제출</a>하여 신청하십시오.</td>
</tr>
</table>


#### 반환된 값
<table>
<tr>
<td rowspan="1" colSpan="1" >반환된 값</td>
<td rowspan="1" colSpan="1" >설명</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >QAVError.OK= 0</td>
<td rowspan="1" colSpan="1" >SDK 초기화 성공</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >AV_ERR_SDK_NOT_FULL_UPDATE=7015</td>
<td rowspan="1" colSpan="1" >SDK 파일이 완전한지 확인합니다. 삭제한 후 SDK를 다시 가져오는 것이 좋습니다.</td>
</tr>
</table>


>!**7015 오류 메시지**
> 
> - 7015 에러 코드는 md5로 판단됩니다. 통합 중에 이 오류가 보고되면 메시지에 따라 SDK 파일의 무결성과 버전을 확인하십시오.
> - 반환 값 AV_ERR_SDK_NOT_FULL_UPDATE는 사전 **알림일 뿐**이며 초기화 실패를 일으키지는 않습니다.
> - 타사 강화, Unity 패키징 메커니즘 및 기타 요인으로 인해 라이브러리 파일의 md5가 영향을 받아 오판이 발생할 수 있습니다. **정식 출시를 위한 로직에서는 이 오류를 무시**하고 UI에 표시하지 않도록 하십시오.


#### 예시 코드
``` bash
int ret = ITMGContext.GetInstance().Init(sdkAppId, openID);
// 반환된 값으로 초기화 성공 여부 판단
if (ret != QAVError.OK)
    {
        Debug.Log("SDK 초기화 실패:"+ret);
        return;
    }
```

### 이벤트 콜백 트리거

이벤트 콜백은 update에서 Poll API를 주기적으로 호출하여 트리거할 수 있습니다. Poll API는 GME의 메시지 펌프이며 GME가 이벤트 콜백을 트리거하도록 주기적으로 호출해야 합니다. 그렇지 않으면 전체 SDK 서비스가 비정상적으로 실행됩니다. 자세한 내용은 [SDK 다운로드 가이드](https://intl.cloud.tencent.com/document/product/607/18521)의 EnginePollHelper 파일을 참고하십시오.

>!
> 
> 비정상적인 API 콜백을 방지하기 위해 Poll API는 주기적으로 메인 스레드에서 호출되어야 합니다.
> 


#### API 프로토타입
``` bash
ITMGContext public abstract int Poll();
```

#### 예시 코드
``` bash
public void Update()
    {
        ITMGContext.GetInstance().Poll();
    }
```

### 시스템 일시 중지

시스템에서 Pause 이벤트가 발생하면 엔진에도 일시 중지를 알려야 합니다. 예를 들어 애플리케이션이 백그라운드로 전환되고(OnApplicationPause, isPause=True) 방에서 오디오를 재생하기 위해 백그라운드가 필요하지 않은 경우 Pause API를 호출하여 GME 서비스를 일시 중지하십시오.

#### API 프로토타입
``` bash
ITMGContext public abstract int Pause()
```

### 시스템 복구

시스템에서 Resume 이벤트가 발생하면 엔진에도 Resume에 대해 알려야 합니다. Resume API는 음성 채팅 복구만 지원합니다.

#### API 프로토타입
``` bash
ITMGContext  public abstract int Resume()
```

### SDK 초기화 해제

이 API는 SDK 초기화 해제를 통해 초기화를 해제하는 데 사용됩니다. **게임 비즈니스 계정이 openid에 바인딩되어 있는 경우 게임 계정을 전환하려면 GME를 초기화 해제한 다음 새 openid를 사용하여 다시 초기화해야 합니다**.

#### API 프로토타입
``` bash
ITMGContext public abstract int Uninit()
```

## 음성 메시지 서비스 및 음성-텍스트 변환 서비스

>?
> 
> - 음성-텍스트 변환 서비스는 빠른 녹음 파일 텍스트 변환 및 음성 메시지 스트리밍 텍스트 변환으로 구성됩니다.
> - 음성 메시지 서비스 이용 시 음성 채팅방에 입장할 필요가 없습니다.
> - 음성 메시지의 기본 녹음 시간은 1 - 58초입니다. 최대 녹음 시간을 10초로 수정하는 등 녹음 시간을 사용자 지정하려면 초기화 후 SetMaxMessageLength API를 호출하여 설정합니다.


### 음성 메시지 서비스 사용

![](https://qcloudimg.tencent-cloud.cn/raw/24c16c71cb2fcc6cf170a6b481067564.jpg)

### 텍스트 변환 서비스 사용

![](https://qcloudimg.tencent-cloud.cn/raw/8269f413756379d574a2969ac8da0158.jpg)
<table>
<tr>
<td rowspan="1" colSpan="1" >API</td>
<td rowspan="1" colSpan="1" >설명</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >GenAuthBuffer</td>
<td rowspan="1" colSpan="1" >로컬 인증 키 생성</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >ApplyPTTAuthbuffer</td>
<td rowspan="1" colSpan="1" >인증 초기화</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >SetMaxMessageLength</td>
<td rowspan="1" colSpan="1" >음성 메시지의 최대 길이 지정</td>
</tr>
</table>


### 로컬 인증 키 생성

관련 기능의 암호화 및 인증을 위해 AuthBuffer를 생성합니다. 프로덕션 환경에서 릴리스하려면 [인증 키](https://intl.cloud.tencent.com/document/product/607/12218)에 설명된 대로 백엔드 배포 키를 사용하십시오.    

#### API 프로토타입
``` bash
QAVAuthBuffer GenAuthBuffer(int appId, string roomId, string openId, string key)
```
<table>
<tr>
<td rowspan="1" colSpan="1" >매개변수</td>
<td rowspan="1" colSpan="1" >유형</td>
<td rowspan="1" colSpan="1" >설명</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >appId</td>
<td rowspan="1" colSpan="1" >int</td>
<td rowspan="1" colSpan="1" >Tencent Cloud 콘솔의 AppId.</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >roomId</td>
<td rowspan="1" colSpan="1" >string</td>
<td rowspan="1" colSpan="1" >null 또는 빈 문자열 입력.</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >openId</td>
<td rowspan="1" colSpan="1" >string</td>
<td rowspan="1" colSpan="1" >Init 시 OpenId와 동일한 사용자 ID.</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >key</td>
<td rowspan="1" colSpan="1" >string</td>
<td rowspan="1" colSpan="1" >Tencent Cloud <a href="https://console.cloud.tencent.com/gamegme">콘솔</a>의 권한 키.</td>
</tr>
</table>


### 애플리케이션 인증

인증 정보가 생성되면 SDK에 인증이 할당됩니다.  

#### API 프로토타입
``` bash
ITMGPTT int ApplyPTTAuthbuffer (byte[] authBuffer)
```
<table>
<tr>
<td rowspan="1" colSpan="1" >매개변수</td>
<td rowspan="1" colSpan="1" >유형</td>
<td rowspan="1" colSpan="1" >설명</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >authBuffer</td>
<td rowspan="1" colSpan="1" >byte[]</td>
<td rowspan="1" colSpan="1" >인증</td>
</tr>
</table>


#### 예시 코드
``` bash
UserConfig.SetAppID(transform.Find ("appId").GetComponent<InputField> ().text);
UserConfig.SetUserID(transform.Find ("userId").GetComponent<InputField> ().text);
UserConfig.SetAuthKey(transform.Find("authKey").GetComponent<InputField>().text);
byte[] authBuffer = UserConfig.GetAuthBuffer(UserConfig.GetAppID(), UserConfig.GetUserID(), null,UserConfig.GetAuthKey());
ITMGContext.GetInstance ().GetPttCtrl ().ApplyPTTAuthbuffer(authBuffer);
```

### 음성 메시지의 최대 길이 지정

이 API는 음성 메시지의 최대 길이(최대 58초)를 지정하는 데 사용됩니다.

#### API 프로토타입
``` bash
ITMGPTT int SetMaxMessageLength(int msTime)
```
<table>
<tr>
<td rowspan="1" colSpan="1" >매개변수</td>
<td rowspan="1" colSpan="1" >유형</td>
<td rowspan="1" colSpan="1" >설명</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >msTime</td>
<td rowspan="1" colSpan="1" >int</td>
<td rowspan="1" colSpan="1" >오디오 길이(ms), 값 범위: 1000 < msTime < = 58000</td>
</tr>
</table>


#### 예시 코드
``` bash
ITMGContext.GetInstance().GetPttCtrl().SetMaxMessageLength(58000); 
```

## 스트리밍 음성 인식

### 음성 메시지 및 음성-텍스트 변환 API
<table>
<tr>
<td rowspan="1" colSpan="1" >API</td>
<td rowspan="1" colSpan="1" >설명</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >StartRecordingWithStreamingRecognition</td>
<td rowspan="1" colSpan="1" >스트리밍 녹음 시작</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >StopRecording</td>
<td rowspan="1" colSpan="1" >녹음 중지</td>
</tr>
</table>




### 스트리밍 음성 인식 시작

이 API는 스트리밍 음성 인식을 시작하는 데 사용됩니다. 음성-텍스트 변환된 텍스트는 콜백에서 실시간으로 반환됩니다. 인식할 언어를 지정하거나 음성에서 인식된 정보를 지정된 언어로 번역하여 반환할 수 있습니다. **녹음을 중지하려면** [녹음 중지](https://write.woa.com/document/102980915702525952)**를 호출합니다.**

#### API 프로토타입
``` bash
ITMGPTT int StartRecordingWithStreamingRecognition(string filePath)
ITMGPTT int StartRecordingWithStreamingRecognition(string filePath, string speechLanguage,string translateLanguage) 
```
<table>
<tr>
<td rowspan="1" colSpan="1" >매개변수</td>
<td rowspan="1" colSpan="1" >유형</td>
<td rowspan="1" colSpan="1" >설명</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >filePath</td>
<td rowspan="1" colSpan="1" >String</td>
<td rowspan="1" colSpan="1" >저장된 오디오 파일의 경로</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >speechLanguage</td>
<td rowspan="1" colSpan="1" >String</td>
<td rowspan="1" colSpan="1" >언어 매개변수를 지정하여 해당 언어로 텍스트 변환을 진행합니다. 매개변수는 <a href="https://intl.cloud.tencent.com/document/product/607/30260">Language Parameter Reference List</a>를 참고하십시오.</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >translateLanguage</td>
<td rowspan="1" colSpan="1" >String</td>
<td rowspan="1" colSpan="1" >언어 매개변수를 지정하여 해당 언어로 번역합니다. 매개변수는 <a href="https://intl.cloud.tencent.com/document/product/607/30260">Language Parameter Reference List</a>를 참고하십시오.</td>
</tr>
</table>


#### 예시 코드
``` bash
string recordPath = Application.persistentDataPath + string.Format("/{0}.silk", sUid++);
int ret = ITMGContext.GetInstance().GetPttCtrl().StartRecordingWithStreamingRecognition(recordPath, "cmn-Hans-CN","cmn-Hans-CN");
```

>!
> 
>  번역은 추가 요금이 발생합니다. 자세한 내용은 [구매 가이드](https://intl.cloud.tencent.com/document/product/607/50009)를 참고하십시오.
> 


### 스트리밍 음성 인식 콜백

스트리밍 음성 인식이 시작된 후 OnStreamingSpeechComplete 또는 OnStreamingSpeechisRunning 알림에서 콜백 메시지를 수신해야 합니다. 자세한 내용은 아래와 같습니다.
- `OnStreamingSpeechComplete`은 녹음이 중지되고 인식이 완료된 후 텍스트를 반환합니다. 이는 음성 단락 이후에 인식된 텍스트를 반환하는 것과 같습니다.

- `OnStreamingSpeechisRunning`은 녹음 중 실시간으로 인식된 텍스트를 반환합니다. 이는 말하는 동안 인식된 텍스트를 반환하는 것과 같습니다.


   이벤트 메시지는 실제 필요에 따라 OnEvent 알림에서 식별됩니다. 전달된 매개변수에는 다음 네 가지 메시지가 포함됩니다.

<table>
<tr>
<td rowspan="1" colSpan="1" >메시지 이름</td>
<td rowspan="1" colSpan="1" >설명</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >result</td>
<td rowspan="1" colSpan="1" >스트리밍 음성 인식 성공 여부를 나타내는 반환 코드</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >text</td>
<td rowspan="1" colSpan="1" >음성-텍스트 변환에서 인식된 텍스트</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >file_path</td>
<td rowspan="1" colSpan="1" >저장된 녹음 파일의 로컬 경로</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >file_id</td>
<td rowspan="1" colSpan="1" >파일 url 경로, 녹음 파일은 서버에 90일 동안 보관됨</td>
</tr>
</table>


   >!
   > 
   > file_id는 `ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_IS_RUNNING` 메시지 수신 시 비어 있습니다.
   > 


#### 에러 코드
<table>
<tr>
<td rowspan="1" colSpan="1" >에러 코드</td>
<td rowspan="1" colSpan="1" >설명</td>
<td rowspan="1" colSpan="1" >솔루션 제안</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >32775</td>
<td rowspan="1" colSpan="1" >스트리밍 음성-텍스트 변환에 실패했지만 녹음은 성공함</td>
<td rowspan="1" colSpan="1" >UploadRecordedFile API를 호출하여 녹음 파일을 업로드한 다음 SpeechToText API를 호출하여 음성-텍스트 변환을 수행합니다</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >32777</td>
<td rowspan="1" colSpan="1" >스트리밍 음성-텍스트 변환에 실패했지만 녹음 및 업로드는 성공함</td>
<td rowspan="1" colSpan="1" >반환된 메시지에는 성공적인 업로드 후 백엔드 URL이 포함되어 있습니다. SpeechToText API를 호출하여 음성을 텍스트로 변환합니다.</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >32786</td>
<td rowspan="1" colSpan="1" >스트리밍 음성-텍스트 변환 실패</td>
<td rowspan="1" colSpan="1" >스트리밍 녹음 중에는 스트리밍 녹음 API의 실행 결과가 반환될 때까지 기다립니다</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >32787</td>
<td rowspan="1" colSpan="1" >음성-텍스트 변환에 성공했지만 텍스트 번역 서비스가 활성화되지 않음</td>
<td rowspan="1" colSpan="1" >콘솔에서 텍스트 번역 서비스를 활성화해야 합니다</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >32788</td>
<td rowspan="1" colSpan="1" >음성-텍스트 변환에 성공했지만 텍스트 번역 서비스의 언어 매개변수가 잘못됨</td>
<td rowspan="1" colSpan="1" >전달된 매개변수를 확인하십시오</td>
</tr>
</table>


오류 코드 4098이 보고되면 해결 방법은 [FAQ](https://intl.cloud.tencent.com/document/product/607/39716)를 참고하십시오.

#### 예시 코드
``` bash
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
                        showWarningText("녹음 중");
                    }	
}
```

## 음성 메시지 녹음

**녹음 프로세스는 다음과 같습니다. 녹음 시작 > 녹음 중지 > 녹음 콜백 반환 > 다음 녹음 시작.**

### 음성 메시지 및 음성-텍스트 변환 API
<table>
<tr>
<td rowspan="1" colSpan="1" >API</td>
<td rowspan="1" colSpan="1" >설명</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >StartRecording</td>
<td rowspan="1" colSpan="1" >녹음 시작</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >PauseRecording</td>
<td rowspan="1" colSpan="1" >녹음 일시 중지</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >ResumeRecording</td>
<td rowspan="1" colSpan="1" >녹음 재개</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >StopRecording</td>
<td rowspan="1" colSpan="1" >녹음 중지</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >CancelRecording</td>
<td rowspan="1" colSpan="1" >녹음 취소</td>
</tr>
</table>


### 녹음 시작

이 API는 녹음을 시작하는 데 사용됩니다.

#### API 프로토타입
``` bash
ITMGPTT int StartRecording(string fileDir)
```
<table>
<tr>
<td rowspan="1" colSpan="1" >매개변수</td>
<td rowspan="1" colSpan="1" >유형</td>
<td rowspan="1" colSpan="1" >설명</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >fileDir</td>
<td rowspan="1" colSpan="1" >string</td>
<td rowspan="1" colSpan="1" >저장된 오디오 파일의 경로</td>
</tr>
</table>


#### 예시 코드
``` bash
string recordPath = Application.persistentDataPath + string.Format ("/{0}.silk", sUid++);
int ret = ITMGContext.GetInstance().GetPttCtrl().StartRecording(recordPath);
```



### 녹음 정지

이 API는 녹음을 중지하는 데 사용됩니다. 비동기식이며 녹음이 중지된 후 녹음 완료에 대한 콜백이 반환됩니다. 녹음 파일은 녹음이 성공한 후에만 사용할 수 있습니다.

#### API 프로토타입
``` bash
ITMGPTT int StopRecording()
```

#### 예시 코드
``` bash
ITMGContext.GetInstance().GetPttCtrl().StopRecording();
```

### 녹음 시작 콜백

녹음이 완료되면 메시지를 전달하기 위해 델리게이트 함수를 통해 콜백이 실행됩니다.

**녹음을 중지하려면 StopRecording을 호출합니다**. 녹음 시작 콜백은 녹음이 중지된 후에 반환됩니다.

#### API 프로토타입
``` bash
public delegate void QAVRecordFileCompleteCallback(int code, string filepath); 
public abstract event QAVRecordFileCompleteCallback OnRecordFileComplete;
```
<table>
<tr>
<td rowspan="1" colSpan="1" >매개변수</td>
<td rowspan="1" colSpan="1" >유형</td>
<td rowspan="1" colSpan="1" >설명</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >code</td>
<td rowspan="1" colSpan="1" >string</td>
<td rowspan="1" colSpan="1" >0: 녹음 완료</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >filepath</td>
<td rowspan="1" colSpan="1" >string</td>
<td rowspan="1" colSpan="1" >저장된 녹음 파일의 경로로, 액세스할 수 있어야 하며 fileid일 수 없음</td>
</tr>
</table>


#### 에러 코드
<table>
<tr>
<td rowspan="1" colSpan="1" >에러 코드 값</td>
<td rowspan="1" colSpan="1" >원인</td>
<td rowspan="1" colSpan="1" >솔루션 제안</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >4097</td>
<td rowspan="1" colSpan="1" >매개변수가 비어 있음</td>
<td rowspan="1" colSpan="1" >코드의 API 매개변수가 올바른지 확인하십시오</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >4098</td>
<td rowspan="1" colSpan="1" >초기화 오류</td>
<td rowspan="1" colSpan="1" >디바이스가 사용 중인지, 권한이 정상인지, 초기화가 정상인지 확인하십시오</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >4099</td>
<td rowspan="1" colSpan="1" >녹음 중</td>
<td rowspan="1" colSpan="1" >SDK 녹음 기능이 적시에 사용되는지 확인하십시오</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >4100</td>
<td rowspan="1" colSpan="1" >오디오 데이터가 캡처되지 않음</td>
<td rowspan="1" colSpan="1" >마이크가 제대로 작동하는지 확인하십시오</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >4101</td>
<td rowspan="1" colSpan="1" >녹음 중 파일에 액세스하는 동안 오류 발생</td>
<td rowspan="1" colSpan="1" >파일의 존재와 파일 경로의 유효성을 확인하십시오</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >4102</td>
<td rowspan="1" colSpan="1" >마이크가 인증되지 않음</td>
<td rowspan="1" colSpan="1" >SDK를 사용하기 위해서는 마이크 권한이 필요합니다. 권한을 추가하려면 해당 엔진 또는 플랫폼에 대한 SDK 프로젝트 구성 문서를 참고하십시오.</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >4103</td>
<td rowspan="1" colSpan="1" >녹음 시간이 너무 짧음</td>
<td rowspan="1" colSpan="1" >녹음 시간은 ms 단위로 1000ms보다 길어야 합니다</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >4104</td>
<td rowspan="1" colSpan="1" >녹음 작업이 시작되지 않음</td>
<td rowspan="1" colSpan="1" >녹음 시작 API가 호출되었는지 확인합니다</td>
</tr>
</table>


#### 예시 코드
``` bash
//이벤트 수신
ITMGContext.GetInstance().GetPttCtrl().OnRecordFileComplete +=  new QAVRecordFileCompleteCallback (OnRecordFileComplete);
//수신한 이벤트 처리
void OnRecordFileComplete(int code, string filepath){
    //녹음 시작 콜백
}
```

### 녹음 일시정지

이 API는 녹음을 일시 중지하는 데 사용됩니다. 녹음을 재개하려면 ResumeRecording API를 호출하십시오.

#### API 프로토타입
``` bash
ITMGPTT int PauseRecording()
```

#### 예시 코드
``` bash
ITMGContext.GetInstance().GetPttCtrl().PauseRecording();
```

### 녹음 재개

이 API는 녹음을 재개하는 데 사용됩니다.

#### API 프로토타입
``` bash
ITMGPTT int ResumeRecording()
```

#### 예시 코드
``` bash
ITMGContext.GetInstance().GetPttCtrl().ResumeRecording();
```

### 녹음 취소

이 API는 녹음 취소에 사용됩니다. **취소 후 콜백이 없습니다**.

#### API 프로토타입
``` bash
ITMGPTT int CancelRecording()
```

#### 예시 코드
``` bash
ITMGContext.GetInstance().GetPttCtrl().CancelRecording();
```

## 음성 메시지 업로드, 다운로드 및 재생
<table>
<tr>
<td rowspan="1" colSpan="1" >API</td>
<td rowspan="1" colSpan="1" >설명</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >UploadRecordedFile</td>
<td rowspan="1" colSpan="1" >오디오 파일 업로드</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >DownloadRecordedFile</td>
<td rowspan="1" colSpan="1" >오디오 파일 다운로드</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >PlayRecordedFile</td>
<td rowspan="1" colSpan="1" >오디오 파일 재생</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >StopPlayFile</td>
<td rowspan="1" colSpan="1" >오디오 파일 재생 중지</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >GetFileSize</td>
<td rowspan="1" colSpan="1" >오디오 파일 크기 가져오기</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >GetVoiceFileDuration</td>
<td rowspan="1" colSpan="1" >오디오 파일 길이 가져오기</td>
</tr>
</table>


### 오디오 파일 업로드

이 API는 오디오 파일을 업로드하는 데 사용됩니다.

#### API 프로토타입
``` bash
ITMGPTT int UploadRecordedFile (string filePath)
```
<table>
<tr>
<td rowspan="1" colSpan="1" >매개변수</td>
<td rowspan="1" colSpan="1" >유형</td>
<td rowspan="1" colSpan="1" >설명</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >filePath</td>
<td rowspan="1" colSpan="1" >String</td>
<td rowspan="1" colSpan="1" >로컬 경로인 업로드된 오디오 파일의 경로</td>
</tr>
</table>


#### 예시 코드
``` bash
ITMGContext.GetInstance().GetPttCtrl().UploadRecordedFile(filePath);
```

### 오디오 파일 업로드 완료 콜백

오디오 파일 업로드가 완료되면 메시지를 전달하기 위해 델리게이트 함수를 통해 콜백이 실행됩니다.

#### API 프로토타입
``` bash
public delegate void QAVUploadFileCompleteCallback(int code, string filepath, string fileid);
public abstract event QAVUploadFileCompleteCallback OnUploadFileComplete; 
```
<table>
<tr>
<td rowspan="1" colSpan="1" >매개변수</td>
<td rowspan="1" colSpan="1" >유형</td>
<td rowspan="1" colSpan="1" >설명</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >code</td>
<td rowspan="1" colSpan="1" >int</td>
<td rowspan="1" colSpan="1" >0: 녹음 완료</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >filepath</td>
<td rowspan="1" colSpan="1" >string</td>
<td rowspan="1" colSpan="1" >저장된 녹음 파일의 경로</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >fileid</td>
<td rowspan="1" colSpan="1" >string</td>
<td rowspan="1" colSpan="1" >파일 url 경로</td>
</tr>
</table>


#### 에러 코드
<table>
<tr>
<td rowspan="1" colSpan="1" >에러 코드 값</td>
<td rowspan="1" colSpan="1" >원인</td>
<td rowspan="1" colSpan="1" >솔루션 제안</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >8193</td>
<td rowspan="1" colSpan="1" >업로드 중에 파일에 액세스하는 동안 오류 발생</td>
<td rowspan="1" colSpan="1" >파일의 존재와 파일 경로의 유효성을 확인하십시오</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >8194</td>
<td rowspan="1" colSpan="1" >서명 확인 실패</td>
<td rowspan="1" colSpan="1" >인증키가 정확한지, 음성 메시지 및 음성 변환 기능이 초기화 되었는지 확인하십시오</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >8195</td>
<td rowspan="1" colSpan="1" >네트워크 오류 발생</td>
<td rowspan="1" colSpan="1" >장치가 인터넷에 액세스할 수 있는지 확인하십시오</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >8196</td>
<td rowspan="1" colSpan="1" >업로드 매개변수를 가져오는 동안 네트워크 실패</td>
<td rowspan="1" colSpan="1" >인증이 올바른지, 장치 네트워크가 정상적으로 인터넷에 액세스할 수 있는지 확인하십시오</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >8197</td>
<td rowspan="1" colSpan="1" >업로드 매개변수를 가져오는 과정에서 반환된 패킷이 비어 있음</td>
<td rowspan="1" colSpan="1" >인증이 올바른지, 장치 네트워크가 정상적으로 인터넷에 액세스할 수 있는지 확인하십시오</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >8198</td>
<td rowspan="1" colSpan="1" >업로드 매개변수를 가져오는 과정에서 반환된 패킷 디코딩 실패</td>
<td rowspan="1" colSpan="1" >인증이 올바른지, 장치 네트워크가 정상적으로 인터넷에 액세스할 수 있는지 확인하십시오</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >8200</td>
<td rowspan="1" colSpan="1" >appinfo가 설정되지 않음</td>
<td rowspan="1" colSpan="1" >apply API가 호출되었는지 또는 입력 매개변수가 비어 있는지 확인하십시오</td>
</tr>
</table>


#### 예시 코드
``` bash
//이벤트 수신
ITMGContext.GetInstance().GetPttCtrl().OnUploadFileComplete +=new QAVUploadFileCompleteCallback (OnUploadFileComplete);
//수신한 이벤트 처리
void OnUploadFileComplete(int code, string filepath, string fileid){
    //오디오 파일 업로드 완료 콜백
}
```

### 오디오 파일 다운로드

이 API는 오디오 파일을 다운로드하는 데 사용됩니다.

#### API 프로토타입
``` bash
ITMGPTT DownloadRecordedFile (string fileID, string downloadFilePath)
```
<table>
<tr>
<td rowspan="1" colSpan="1" >매개변수</td>
<td rowspan="1" colSpan="1" >유형</td>
<td rowspan="1" colSpan="1" >설명</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >fileID</td>
<td rowspan="1" colSpan="1" >String</td>
<td rowspan="1" colSpan="1" >파일 url 경로</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >downloadFilePath</td>
<td rowspan="1" colSpan="1" >String</td>
<td rowspan="1" colSpan="1" >파일의 로컬 저장 경로로, 액세스할 수 있어야 하며 fileid일 수 없음</td>
</tr>
</table>


#### 예시 코드
``` bash
ITMGContext.GetInstance().GetPttCtrl().DownloadRecordedFile(fileId, filePath);
```

### 오디오 파일 다운로드 완료 콜백

오디오 파일 다운로드가 완료되면 메시지를 전달하기 위해 델리게이트 함수를 통해 콜백이 실행됩니다.

#### API 프로토타입
``` bash
public delegate void QAVDownloadFileCompleteCallback(int code, string filepath, string fileid);
public abstract event QAVDownloadFileCompleteCallback OnDownloadFileComplete;
```
<table>
<tr>
<td rowspan="1" colSpan="1" >매개변수</td>
<td rowspan="1" colSpan="1" >유형</td>
<td rowspan="1" colSpan="1" >설명</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >code</td>
<td rowspan="1" colSpan="1" >int</td>
<td rowspan="1" colSpan="1" >0: 녹음 완료</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >filepath</td>
<td rowspan="1" colSpan="1" >String</td>
<td rowspan="1" colSpan="1" >저장된 녹음 파일의 경로</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >fileid</td>
<td rowspan="1" colSpan="1" >String</td>
<td rowspan="1" colSpan="1" >파일 url 경로, 녹음 파일은 서버에 90일 동안 보관됨</td>
</tr>
</table>


#### 에러 코드
<table>
<tr>
<td rowspan="1" colSpan="1" >에러 코드 값</td>
<td rowspan="1" colSpan="1" >원인</td>
<td rowspan="1" colSpan="1" >솔루션 제안</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >12289</td>
<td rowspan="1" colSpan="1" >다운로드 중 파일에 액세스하는 동안 오류 발생</td>
<td rowspan="1" colSpan="1" >파일 경로가 유효한지 확인하십시오</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >12290</td>
<td rowspan="1" colSpan="1" >서명 확인 실패</td>
<td rowspan="1" colSpan="1" >인증키가 정확한지, 음성 메시지 및 음성 변환 기능이 초기화 되었는지 확인하십시오</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >12291</td>
<td rowspan="1" colSpan="1" >네트워크 스토리지 시스템 예외</td>
<td rowspan="1" colSpan="1" >서버가 오디오 파일을 가져오지 못했습니다. API 매개변수 fileid가 올바른지, 네트워크가 정상인지, COS에 파일이 존재하는지 확인하십시오.</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >12292</td>
<td rowspan="1" colSpan="1" >서버 파일 시스템 오류</td>
<td rowspan="1" colSpan="1" >장치가 인터넷에 액세스할 수 있는지와 파일이 서버에 존재하는지 확인하십시오</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >12293</td>
<td rowspan="1" colSpan="1" >다운로드 매개변수를 가져오는 과정에서 HTTP 네트워크 실패</td>
<td rowspan="1" colSpan="1" >장치가 인터넷에 액세스할 수 있는지 확인하십시오</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >12294</td>
<td rowspan="1" colSpan="1" >다운로드 매개변수를 가져오는 과정에서 반환된 패킷이 비어 있음</td>
<td rowspan="1" colSpan="1" >장치가 인터넷에 액세스할 수 있는지 확인하십시오</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >12295</td>
<td rowspan="1" colSpan="1" >다운로드 매개변수를 가져오는 과정에서 반환된 패킷 디코딩 실패</td>
<td rowspan="1" colSpan="1" >장치가 인터넷에 액세스할 수 있는지 확인하십시오</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >12297</td>
<td rowspan="1" colSpan="1" >appinfo가 설정되지 않음</td>
<td rowspan="1" colSpan="1" >인증키가 정확한지, 음성 메시지 및 음성 변환 기능이 초기화 되었는지 확인하십시오</td>
</tr>
</table>


#### 예시 코드
``` bash
//이벤트 수신
ITMGContext.GetInstance().GetPttCtrl().OnDownloadFileComplete +=new QAVDownloadFileCompleteCallback(OnDownloadFileComplete);
//수신한 이벤트 처리
void OnDownloadFileComplete(int code, string filepath, string fileid){
    //오디오 파일 다운로드 완료 콜백
}
```

### 오디오 재생

이 API는 오디오를 재생하는 데 사용됩니다.

#### API 프로토타입
``` bash
ITMGPTT PlayRecordedFile(string filePath)
ITMGPTT PlayRecordedFile(string filePath,int voiceType);
```
<table>
<tr>
<td rowspan="1" colSpan="1" >매개변수</td>
<td rowspan="1" colSpan="1" >유형</td>
<td rowspan="1" colSpan="1" >설명</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >filePath</td>
<td rowspan="1" colSpan="1" >String</td>
<td rowspan="1" colSpan="1" >로컬 오디오 파일 경로</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >voicetype</td>
<td rowspan="1" colSpan="1" >int</td>
<td rowspan="1" colSpan="1" >음성 변조 유형. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/607/44995">음성 변조</a>를 참고하십시오.</td>
</tr>
</table>


#### 에러 코드
<table>
<tr>
<td rowspan="1" colSpan="1" >에러 코드 값</td>
<td rowspan="1" colSpan="1" >원인</td>
<td rowspan="1" colSpan="1" >솔루션 제안</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >20485</td>
<td rowspan="1" colSpan="1" >재생이 시작되지 않음</td>
<td rowspan="1" colSpan="1" >파일의 존재와 파일 경로의 유효성을 확인하십시오</td>
</tr>
</table>


#### 예시 코드
``` bash
ITMGContext.GetInstance().GetPttCtrl().PlayRecordedFile(filePath); 
```

### 오디오 재생 콜백

오디오 파일이 재생될 때 메시지를 전달하기 위해 델리게이트 함수를 통해 콜백이 실행됩니다.

#### API 프로토타입
``` bash
public delegate void QAVPlayFileCompleteCallback(int code, string filepath);
public abstract event QAVPlayFileCompleteCallback OnPlayFileComplete;
```
<table>
<tr>
<td rowspan="1" colSpan="1" >매개변수</td>
<td rowspan="1" colSpan="1" >유형</td>
<td rowspan="1" colSpan="1" >설명</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >code</td>
<td rowspan="1" colSpan="1" >int</td>
<td rowspan="1" colSpan="1" >0: 재생 완료</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >filepath</td>
<td rowspan="1" colSpan="1" >String</td>
<td rowspan="1" colSpan="1" >저장된 녹음 파일의 경로</td>
</tr>
</table>


#### 에러 코드
<table>
<tr>
<td rowspan="1" colSpan="1" >에러 코드 값</td>
<td rowspan="1" colSpan="1" >원인</td>
<td rowspan="1" colSpan="1" >솔루션 제안</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >20481</td>
<td rowspan="1" colSpan="1" >초기화 오류</td>
<td rowspan="1" colSpan="1" >디바이스가 사용 중인지, 권한이 정상인지, 초기화가 정상인지 확인하십시오</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >20482</td>
<td rowspan="1" colSpan="1" >재생 중에 클라이언트가 중단하고 다음 재생을 시도했지만 실패함(정상적으로 성공해야 함)</td>
<td rowspan="1" colSpan="1" >코드 로직이 올바른지 확인하십시오</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >20483</td>
<td rowspan="1" colSpan="1" >매개변수가 비어 있음</td>
<td rowspan="1" colSpan="1" >코드의 API 매개변수가 올바른지 확인하십시오</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >20484</td>
<td rowspan="1" colSpan="1" >내부 오류</td>
<td rowspan="1" colSpan="1" >플레이어를 초기화하는 동안 오류가 발생했습니다. 이 오류 코드는 일반적으로 디코딩 실패로 인해 발생하며 오류는 로그를 통해 찾아야 합니다.</td>
</tr>
</table>


#### 예시 코드
``` bash
//이벤트 수신:
ITMGContext.GetInstance().GetPttCtrl().OnPlayFileComplete +=new  QAVPlayFileCompleteCallback(OnPlayFileComplete);
//수신한 이벤트 처리:
void OnPlayFileComplete(int code, string filepath){
    //오디오 재생 콜백
}
```

### 오디오 재생 중지

이 API는 오디오 재생을 중지하는 데 사용됩니다. 재생이 중지되면 재생 완료 콜백이 발생합니다.

#### API 프로토타입
``` bash
ITMGPTT int StopPlayFile()
```

#### 예시 코드
``` bash
ITMGContext.GetInstance().GetPttCtrl().StopPlayFile();
```

### 오디오 파일 사이즈 획득

이 API는 오디오 파일의 크기를 가져오는 데 사용됩니다.

#### API 프로토타입
``` bash
ITMGPTT GetFileSize(string filePath) 
```
<table>
<tr>
<td rowspan="1" colSpan="1" >매개변수</td>
<td rowspan="1" colSpan="1" >유형</td>
<td rowspan="1" colSpan="1" >설명</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >filePath</td>
<td rowspan="1" colSpan="1" >String</td>
<td rowspan="1" colSpan="1" >로컬 경로인 오디오 파일의 경로입니다</td>
</tr>
</table>


#### 예시 코드
``` bash
int fileSize = ITMGContext.GetInstance().GetPttCtrl().GetFileSize(filepath);
```

### 오디오 파일 길이 가져오기

이 API는 오디오 파일의 길이를 밀리초 단위로 가져오는 데 사용됩니다.

#### API 프로토타입
``` bash
ITMGPTT int GetVoiceFileDuration(string filePath)
```
<table>
<tr>
<td rowspan="1" colSpan="1" >매개변수</td>
<td rowspan="1" colSpan="1" >유형</td>
<td rowspan="1" colSpan="1" >설명</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >filePath</td>
<td rowspan="1" colSpan="1" >String</td>
<td rowspan="1" colSpan="1" >로컬 경로인 오디오 파일의 경로입니다</td>
</tr>
</table>


#### 예시 코드
``` bash
int fileDuration = ITMGContext.GetInstance().GetPttCtrl().GetVoiceFileDuration(filepath);
```

## 빠른 녹음-텍스트 변환
<table>
<tr>
<td rowspan="1" colSpan="1" >API</td>
<td rowspan="1" colSpan="1" >설명</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >SpeechToText</td>
<td rowspan="1" colSpan="1" >음성을 텍스트로 변환</td>
</tr>
</table>


### 오디오 파일을 텍스트로 변환

이 API는 지정된 오디오 파일을 텍스트로 변환하는 데 사용됩니다.

#### API 프로토타입
``` bash
ITMGPTT int SpeechToText(String fileID)
```
<table>
<tr>
<td rowspan="1" colSpan="1" >매개변수</td>
<td rowspan="1" colSpan="1" >유형</td>
<td rowspan="1" colSpan="1" >설명</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >fileID</td>
<td rowspan="1" colSpan="1" >String</td>
<td rowspan="1" colSpan="1" >오디오 파일 url</td>
</tr>
</table>


#### 예시 코드
``` bash
ITMGContext.GetInstance().GetPttCtrl().SpeechToText(fileID);
```

### 오디오 파일을 지정된 언어의 텍스트로 번역

이 API는 인식할 언어를 지정하거나 음성으로 인식된 정보를 지정된 언어로 번역하여 반환할 수 있습니다.

>!
> 
> 번역은 추가 요금이 발생합니다. 자세한 내용은 [구매 가이드](https://intl.cloud.tencent.com/document/product/607/50009)를 참고하십시오.
> 


#### API 프로토타입
``` bash
ITMGPTT int SpeechToText(String fileID,String speechLanguage)
ITMGPTT int SpeechToText(String fileID,String speechLanguage,String translatelanguage)
```
<table>
<tr>
<td rowspan="1" colSpan="1" >매개변수</td>
<td rowspan="1" colSpan="1" >유형</td>
<td rowspan="1" colSpan="1" >설명</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >fileID</td>
<td rowspan="1" colSpan="1" >String</td>
<td rowspan="1" colSpan="1" >녹음 파일 url 경로, 녹음 파일은 서버에 90일 동안 보관됨</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >speechLanguage</td>
<td rowspan="1" colSpan="1" >String</td>
<td rowspan="1" colSpan="1" >언어 매개변수를 지정하여 해당 언어로 텍스트 변환을 진행합니다. 매개변수는 <a href="https://intl.cloud.tencent.com/document/product/607/30260">Language Parameter Reference List</a>를 참고하십시오.</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >translatelanguage</td>
<td rowspan="1" colSpan="1" >String</td>
<td rowspan="1" colSpan="1" >언어 매개변수를 지정하여 해당 언어로 번역합니다. 매개변수는 <a href="https://intl.cloud.tencent.com/document/product/607/30260">Language Parameter Reference List</a>를 참고하십시오.</td>
</tr>
</table>


#### 예시 코드
``` bash
ITMGContext.GetInstance().GetPttCtrl().SpeechToText(fileID,"cmn-Hans-CN","cmn-Hans-CN");
```

### 인식 콜백

지정된 오디오 파일이 인식되어 텍스트로 변환되면 메시지를 전달하기 위해 델리게이트 함수를 통해 콜백이 실행됩니다.

#### API 프로토타입
``` bash
public delegate void QAVSpeechToTextCallback(int code, string fileid, string result);
public abstract event QAVSpeechToTextCallback OnSpeechToTextComplete;
```
<table>
<tr>
<td rowspan="1" colSpan="1" >매개변수</td>
<td rowspan="1" colSpan="1" >유형</td>
<td rowspan="1" colSpan="1" >설명</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >code</td>
<td rowspan="1" colSpan="1" >int</td>
<td rowspan="1" colSpan="1" >0: 녹음 완료</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >fileid</td>
<td rowspan="1" colSpan="1" >String</td>
<td rowspan="1" colSpan="1" >파일 url 경로, 녹음 파일은 서버에 90일 동안 보관됨</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >result</td>
<td rowspan="1" colSpan="1" >String</td>
<td rowspan="1" colSpan="1" >변환된 텍스트</td>
</tr>
</table>


#### 에러 코드
<table>
<tr>
<td rowspan="1" colSpan="1" >에러 코드 값</td>
<td rowspan="1" colSpan="1" >원인</td>
<td rowspan="1" colSpan="1" >솔루션 제안</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >32769</td>
<td rowspan="1" colSpan="1" >내부 오류</td>
<td rowspan="1" colSpan="1" >로그를 분석하여 백엔드에서 클라이언트로 반환된 실제 오류 코드를 얻은 후 백엔드 담당자에게 도움을 요청하십시오</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >32770</td>
<td rowspan="1" colSpan="1" >네트워크 실패</td>
<td rowspan="1" colSpan="1" >장치가 인터넷에 액세스할 수 있는지 확인하십시오</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >32772</td>
<td rowspan="1" colSpan="1" >반환된 패킷 디코딩 실패</td>
<td rowspan="1" colSpan="1" >로그를 분석하여 백엔드에서 클라이언트로 반환된 실제 오류 코드를 얻은 후 백엔드 담당자에게 도움을 요청하십시오</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >32774</td>
<td rowspan="1" colSpan="1" >appinfo가 설정되지 않음</td>
<td rowspan="1" colSpan="1" >인증키가 정확한지, 음성 메시지 및 음성 변환 기능이 초기화 되었는지 확인하십시오</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >32776</td>
<td rowspan="1" colSpan="1" >authbuffer 확인 실패</td>
<td rowspan="1" colSpan="1" >authbuffer가 올바른지 확인하십시오</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >32784</td>
<td rowspan="1" colSpan="1" >잘못된 음성-텍스트 변환 매개변수</td>
<td rowspan="1" colSpan="1" >코드의 API 매개변수 fileid가 비어 있는지 확인하십시오</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >32785</td>
<td rowspan="1" colSpan="1" >음성-텍스트 변환에서 오류 반환</td>
<td rowspan="1" colSpan="1" >음성 메시지 및 음성 텍스트 변환 기능의 백엔드에 오류가 있습니다. 로그를 분석하고 백엔드에서 클라이언트로 반환된 실제 오류 코드를 받고 백엔드 담당자에게 도움을 요청하십시오</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >32787</td>
<td rowspan="1" colSpan="1" >음성-텍스트 변환에 성공했지만 텍스트 번역 서비스가 활성화되지 않음</td>
<td rowspan="1" colSpan="1" >콘솔에서 텍스트 번역 서비스를 활성화해야 합니다</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >32788</td>
<td rowspan="1" colSpan="1" >음성-텍스트 변환에 성공했지만 텍스트 번역 서비스의 언어 매개변수가 잘못됨</td>
<td rowspan="1" colSpan="1" >전달된 매개변수를 확인하십시오</td>
</tr>
</table>


#### 예시 코드
``` bash
//이벤트 수신
ITMGContext.GetInstance().GetPttCtrl().OnSpeechToTextComplete += new QAVSpeechToTextCallback(OnSpeechToTextComplete);
//수신한 이벤트 처리
void OnSpeechToTextComplete(int code, string fileid, string result){
    //콜백 인식
}
```

## 음성 메시지 볼륨 레벨 API
<table>
<tr>
<td rowspan="1" colSpan="1" >API</td>
<td rowspan="1" colSpan="1" >설명</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >GetMicLevel</td>
<td rowspan="1" colSpan="1" >실시간 마이크 볼륨 레벨 가져오기</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >SetMicVolume</td>
<td rowspan="1" colSpan="1" >녹음 볼륨 레벨 설정</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >GetMicVolume</td>
<td rowspan="1" colSpan="1" >녹음 볼륨 레벨 가져오기</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >GetSpeakerLevel</td>
<td rowspan="1" colSpan="1" >실시간 스피커 볼륨 가져오기</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >SetSpeakerVolume</td>
<td rowspan="1" colSpan="1" >재생 볼륨 레벨 설정</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >GetSpeakerVolume</td>
<td rowspan="1" colSpan="1" >재생 볼륨 레벨 가져오기</td>
</tr>
</table>


### 음성 메시지의 실시간 마이크 볼륨 가져오기

이 API는 실시간 마이크 볼륨을 가져오는 데 사용됩니다. int 유형 값이 반환됩니다. 값 범위: 0 - 200.

#### API 프로토타입
``` bash
ITMGPTT int GetMicLevel()
```

#### 예시 코드
``` bash
ITMGContext.GetInstance().GetPttCtrl().GetMicLevel();
```

### 음성 메시지의 녹음 볼륨 설정

이 API는 음성 메시지의 녹음 볼륨을 설정하는 데 사용됩니다. 값 범위: 0 - 200.

#### API 프로토타입
``` bash
ITMGPTT int SetMicVolume(int vol)
```

#### 예시 코드
``` bash
ITMGContext.GetInstance().GetPttCtrl().SetMicVolume(100);
```

### 음성 메시지의 녹음 볼륨 가져오기

이 API는 음성 메시지의 녹음 볼륨을 가져오는 데 사용됩니다. int 유형 값이 반환됩니다. 값 범위: 0 - 200.

#### API 프로토타입
``` bash
ITMGPTT int GetMicVolume()
```

#### 예시 코드
``` bash
ITMGContext.GetInstance().GetPttCtrl().GetMicVolume();
```

### 음성 메시지의 실시간 스피커 볼륨 가져오기

이 API는 실시간 스피커 볼륨을 가져오는 데 사용됩니다. int 유형 값이 반환됩니다. 값 범위: 0 - 200.

#### API 프로토타입
``` bash
ITMGPTT int GetSpeakerLevel()
```

#### 예시 코드
``` bash
ITMGContext.GetInstance().GetPttCtrl().GetSpeakerLevel();
```

### 음성 메시지 재생 볼륨 설정

이 API는 음성 메시지의 재생 볼륨을 설정하는 데 사용됩니다. 값 범위: 0 - 200.

#### API 프로토타입
``` bash
ITMGPTT int SetSpeakerVolume(int vol)
```

#### 예시 코드
``` bash
ITMGContext.GetInstance().GetPttCtrl().SetSpeakerVolume(100);
```

### 음성 메시지의 재생 볼륨 가져오기

이 API는 음성 메시지의 재생 볼륨을 가져오는 데 사용됩니다. int 유형 값이 반환됩니다. 값 범위: 0 - 200.

#### API 프로토타입
``` bash
ITMGPTT int GetSpeakerVolume()
```

#### 예시 코드
``` bash
ITMGContext.GetInstance().GetPttCtrl().GetSpeakerVolume();
```

## 고급 API

### 버전 번호 가져오기

이 API는 분석을 위한 SDK 버전 번호를 가져오는 데 사용됩니다.

#### API 프로토타입
``` bash
ITMGContext  abstract string GetSDKVersion()
```

#### 예시 코드
``` bash
ITMGContext.GetInstance().GetSDKVersion();
```

### 로그 출력 레벨 설정

이 API는 출력할 로그의 수준을 설정하는 데 사용되며 초기화 전에 호출해야 합니다. 기본 수준을 유지하는 것이 좋습니다.

#### API 프로토타입
``` bash
ITMGContext  SetLogLevel(ITMG_LOG_LEVEL levelWrite, ITMG_LOG_LEVEL levelPrint)
```

#### 매개변수 설명
<table>
<tr>
<td rowspan="1" colSpan="1" >매개변수</td>
<td rowspan="1" colSpan="1" >유형</td>
<td rowspan="1" colSpan="1" >설명</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >levelWrite</td>
<td rowspan="1" colSpan="1" >ITMG_LOG_LEVEL</td>
<td rowspan="1" colSpan="1" >기록할 로그 수준을 설정합니다. TMG_LOG_LEVEL_NONE은 쓰지 않음을 나타냅니다. 기본값: TMG_LOG_LEVEL_INFO</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >levelPrint</td>
<td rowspan="1" colSpan="1" >ITMG_LOG_LEVEL</td>
<td rowspan="1" colSpan="1" >출력할 로그 수준을 설정합니다. TMG_LOG_LEVEL_NONE은 인쇄하지 않음을 나타냅니다. 기본값: TMG_LOG_LEVEL_ERROR</td>
</tr>
</table>


ITMG_LOG_LEVEL은 아래와 같습니다.
<table>
<tr>
<td rowspan="1" colSpan="1" >ITMG_LOG_LEVEL</td>
<td rowspan="1" colSpan="1" >설명</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >TMG_LOG_LEVEL_NONE</td>
<td rowspan="1" colSpan="1" >로그를 출력하지 않음</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >TMG_LOG_LEVEL_ERROR</td>
<td rowspan="1" colSpan="1" >오류 로그 출력(기본값)</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >TMG_LOG_LEVEL_INFO</td>
<td rowspan="1" colSpan="1" >정보 로그 출력</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >TMG_LOG_LEVEL_DEBUG</td>
<td rowspan="1" colSpan="1" >디버그 로그 출력</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >TMG_LOG_LEVEL_VERBOSE</td>
<td rowspan="1" colSpan="1" >상세 로그 출력</td>
</tr>
</table>


#### 예시 코드
``` bash
ITMGContext.GetInstance().SetLogLevel(TMG_LOG_LEVEL_INFO,TMG_LOG_LEVEL_INFO);
```

### 로그 출력 경로 설정

이 API는 로그 출력 경로를 설정하는 데 사용됩니다. 기본 경로는 다음과 같습니다. Init 전에 호출해야 합니다.
<table>
<tr>
<td rowspan="1" colSpan="1" >운영체제</td>
<td rowspan="1" colSpan="1" >경로</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >Windows</td>
<td rowspan="1" colSpan="1" >%appdata%\Tencent\GME\ProcessName</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >iOS</td>
<td rowspan="1" colSpan="1" >Application/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/Documents</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >Android</td>
<td rowspan="1" colSpan="1" >/sdcard/Android/data/xxx.xxx.xxx/files</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >Mac</td>
<td rowspan="1" colSpan="1" >/Users/username/Library/Containers/xxx.xxx.xxx/Data/Documents</td>
</tr>
</table>


#### API 프로토타입
``` bash
ITMGContext  SetLogPath(string logDir)
```
<table>
<tr>
<td rowspan="1" colSpan="1" >매개변수</td>
<td rowspan="1" colSpan="1" >유형</td>
<td rowspan="1" colSpan="1" >설명</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >logDir</td>
<td rowspan="1" colSpan="1" >String</td>
<td rowspan="1" colSpan="1" >경로</td>
</tr>
</table>


#### 예시 코드
``` bash
ITMGContext.GetInstance().SetLogPath(path);
```

