본문에서는 Native 프로젝트 개발자가 GME(Game Multimedia Engine)용 API를 쉽게 디버깅하고 통합할 수 있도록 자세한 설명을 제공합니다.

이 문서는 GME를 시작하는 데 도움이 되는 주요 API만 제공합니다. Demo를 참고하여 API를 디버깅하고 통합할 수 있습니다.


## GME 사용 시 주의할 점

GME는 실시간 음성 채팅 서비스와 음성 메시지 및 음성-텍스트 변환 서비스의 두 가지 서비스를 제공하며 둘 다 Init 및 Poll과 같은 주요 API에 의존합니다.

<dx-alert infotype="notice" title="Init API 정보">
실시간 음성 채팅과 음성 메시지 서비스를 동시에 사용해야 하는 경우 **Init API를 한 번만 호출하면 됩니다**.
</dx-alert>

### API 호출 순서도

![image](https://qcloudimg.tencent-cloud.cn/raw/20564e5a251c6a53a06fa2b660a93061.png)

### 액세스 단계

#### 주요 API


<dx-tag-link link="#Init" tag="API: Init">GME 초기화</dx-tag-link>
<dx-tag-link link="#Poll" tag="API: Poll">이벤트 콜백을 트리거하기 위해 주기적으로 Poll 호출</dx-tag-link>

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

<dx-tag-link link="#Init" tag="API: UnInit">GME 초기화 해제</dx-tag-link>

## 주요 API 액세스

### 1. Demo 다운로드 

SDK 다운로드 가이드 페이지에서 클라이언트의 <dx-tag-link link="https://cloud.tencent.com/document/product/607/18521" tag="DownLoad"> Demo 프로젝트 코드</dx-tag-link>를 다운로드합니다.


### 2. 헤더 파일 가져오기

<dx-codeblock>
::: Java Java
import com.tencent.TMG.ITMGContext;
import com.tencent.av.sig.AuthBuffer;
import com.tencent.bugly.crashreport.CrashReport;
:::
::: Object-C objetctive-c
#import "GMESDK/TMGEngine.h"
#import "GMESDK/QAVAuthBuffer.h"
:::
::: C++ C++
#include "auth_buffer.h"
#include "tmg_sdk.h"
#include "AdvanceHeaders/tmg_sdk_adv.h"
#include <vector>
:::
</dx-codeblock>


### 3. 싱글톤 가져오기

음성 기능 사용 시, ITMGContext 오브젝트를 먼저 획득해야 합니다.

####  함수 프로토타입 

<dx-codeblock>
::: Java Java
public static ITMGContext GetInstance(Context context)
:::
::: Object-C objetctive-c

+ (ITMGContext*) GetInstance;
  :::
  ::: C++ C++
  __UNUSED static ITMGContext* ITMGContextGetInstance(){
  return ITMGContextGetInstanceInner(TMG_SDK_VERSION);
  }
  :::
  </dx-codeblock>

####  예시 코드  


<dx-codeblock>
::: Java Java
//MainActivity.java
import com.tencent.TMG.ITMGContext; 
ITMGContext tmgContext = ITMGContext.GetInstance(this);
:::
::: Object-C objetctive-c
//TMGSampleViewController.m
ITMGContext* _context = [ITMGContext GetInstance];
:::
::: C++ C++
ITMGContext* context = ITMGContextGetInstance();
:::
</dx-codeblock>

### 4. 콜백 설정

API 클래스는 Delegate 메서드를 사용하여 애플리케이션에 콜백 알림을 보냅니다. 콜백 메시지 수신을 위해 입장 전 SDK에 콜백 함수를 등록합니다.

#### 함수 프로토타입 및 예시 코드

콜백 메시지 수신을 위해 입장 전에 SDK에 콜백 함수를 설정합니다.

<dx-codeblock>
::: Java Java
//ITMGContext
public abstract int SetTMGDelegate(ITMGDelegate delegate);

//MainActivity.java
tmgContext.SetTMGDelegate(TMGCallbackDispatcher.getInstance());
:::
::: Object-C objetctive-c
ITMGDelegate < NSObject >

//TMGSampleViewController.m
ITMGContext* _context = [ITMGContext GetInstance];
_context.TMGDelegate = [DispatchCenter getInstance];
:::
::: C++ C++
//SDK 초기화 시
m_pTmgContext = ITMGContextGetInstance();
m_pTmgContext->SetTMGDelegate(this);
//소멸자 중
CTMGSDK_For_AudioDlg::~CTMGSDK_For_AudioDlg()
{
    ITMGContextGetInstance()->SetTMGDelegate(NULL);
}
:::
</dx-codeblock>

#### 콜백 예시  

콜백의 매개변수를 처리하려면 생성자에서 이 콜백 함수를 재정의하십시오.


<dx-codeblock>
::: Java Java
//MainActivity.java
tmgContext.SetTMGDelegate(TMGCallbackDispatcher.getInstance());

//RealTimeVoiceActivity.java
public void OnEvent(ITMGContext.ITMG_MAIN_EVENT_TYPE type, Intent data) {
        if (type == ITMG_MAIN_EVENT_TYPE_ENTER_ROOM)
		{
			//콜백 프로세스
		}
}

//TMGCallbackDispatcher.java, TMGCallbackHelper.java 및 TMGDispatcherBase.java 참고
:::
::: Object-C Object-C
//TMGRealTimeViewController.m
TMGRealTimeViewController ()< ITMGDelegate >


- (void)OnEvent:(ITMG_MAIN_EVENT_TYPE)eventType data:(NSDictionary *)data {
  NSString *log = [NSString stringWithFormat:@"OnEvent:%d,data:%@", (int)eventType, data];
  [self showLog:log];
  NSLog(@"====%@====", log);
  switch (eventType) {
      // Step 6/11 : Perform the enter room event
      case ITMG_MAIN_EVENT_TYPE_ENTER_ROOM: {
          int result = ((NSNumber *)[data objectForKey:@"result"]).intValue;
          NSString *error_info = [data objectForKey:@"error_info"];

          [self showLog:[NSString stringWithFormat:@"OnEnterRoomComplete:%d msg:(%@)", result, error_info]];
      
          if (result == 0) {
              [self updateStatusEnterRoom:YES];
          }
      }
      break;

  }
  }

//DispatchCenter.h 및 DispatchCenter.m 참고
:::
::: C++ C++
//헤더 파일 중 선언
virtual void OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data);
//예시 코드
void CTMGSDK_For_AudioDlg::OnEvent(ITMG_MAIN_EVENT_TYPE eventType, const char* data)
{
    switch(eventType)
    {
    case ITMG_MAIN_EVENT_TYPE_XXXX_XXXX:
        {
            //콜백 처리 진행
        }
        break;
    }
}
:::
</dx-codeblock>


| 매개변수 |               유형               | 의미                     |
| ---- | :------------------------------: | ------------------------ |
| type    |ITMGContext.ITMG_MAIN_EVENT_TYPE |콜백 이벤트 유형|
| data |         Intent 메시지 유형          | 콜백 메시지, 즉, 이벤트 데이터 |

### [5. SDK 초기화](id:Init)

- 이 API는 GME 서비스를 초기화하는 데 사용됩니다. 애플리케이션을 초기화할 때 호출하는 것이 좋습니다.
- **sdkAppId 매개변수를 가져오는 방법에 대한 자세한 내용은 [Voice Service Activation Guide](https://intl.cloud.tencent.com/document/product/607/39698)를 참고하십시오**.
- **OpenId는 App 개발자가 규정한 규칙으로 사용자를 고유하게 식별하며, App 내에서 중복될 수 없습니다(현재 INT64만 지원됨)**.

#### 함수 프로토타입

<dx-codeblock>
::: Java Java
public abstract int Init(String sdkAppId, String openId);
:::
::: Object-C objetctive-c
-(int)InitEngine:(NSString*)sdkAppID openID:(NSString*)openID;
:::
::: C++ C++
ITMGContext virtual int Init(const char* sdkAppId, const char* openId)
:::
</dx-codeblock>


| 매개변수     |  유형  | 의미                                                         |
| -------- | :----: | ------------------------------------------------------------ |
| sdkAppId | String | [Tencent Cloud 콘솔](https://console.cloud.tencent.com/gamegme)에서 GME 서비스가 제공하는 AppId. |
| OpenId   | String | OpenId는 Int64 유형만 가능(string으로 변환되어 전달됩니다).               |

#### 예시 코드 

<dx-codeblock>
::: Java Java
//MainActivity.java
int nRet = tmgContext.Init(appId, openId);
if (nRet == AV_OK )
{
    GMEAuthBufferHelper.getInstance().setGEMParams(appId, key, openId);
    // Step 4/11: Poll to trigger callback
    //https://cloud.tencent.com/document/product/607/15210#.E8.A7.A6.E5.8F.91.E4.BA.8B.E4.BB.B6.E5.9B.9E.E8.B0.83
    EnginePollHelper.createEnginePollHelper();
    showToast("Init success");
}else if (nRet == AV_ERR_HAS_IN_THE_STATE) // 이미 초기화되었으므로 작업 성공으로 간주함
{
    showToast("Init success");
}else
{
    showToast("Init error errorCode:" + nRet);
}
:::
::: Object-C objetctive-c
//TMGSampleViewController.m
QAVResult result = [_context InitEngine:self.appIDTF.text openID:self.openIDTF.text];
if (result == QAV_OK) {
    self.isSDKInit = YES;
}
:::
::: C++ C++
#define SDKAPPID3RD "14000xxxxx"
cosnt char* openId="10001";
ITMGContext* context = ITMGContextGetInstance();
context->Init(SDKAPPID3RD, openId);
:::
</dx-codeblock>


### [6. 이벤트 콜백 트리거](id:Poll)

update에서 Poll API를 주기적으로 호출하여 이벤트 콜백을 트리거할 수 있습니다. GME가 이벤트 콜백을 트리거하려면 Poll API를 주기적으로 호출해야 합니다. 그렇지 않으면 전체 SDK 서비스가 예외적으로 실행됩니다.

Demo의 EnginePollHelper.java 파일을 참고할 수 있습니다.

#### 예시 코드

<dx-codeblock>
::: Java Java
//MainActivity.java
[EnginePollHelper createEnginePollHelper];

//EnginePollHelper.java
private Handler mhandler = new Handler();
    private Runnable mRunnable = new Runnable() {
        @Override
        public void run() {
            if (s_pollEnabled) {
                if (ITMGContext.GetInstance(null) != null)
                    ITMGContext.GetInstance(null).Poll();
            }
            mhandler.postDelayed(mRunnable, 33);
        }
    };
//Poll을 주기적으로 호출하는 코드는 EnginePollHelper.java를 참고하십시오.
:::
::: Object-C objetctive-c
//TMGSampleViewController.m
[EnginePollHelper createEnginePollHelper];
//EnginePollHelper.m 및 EnginePollHelper.h 참고
:::
::: C++ C++
void TMGTestScene::update(float delta)
{
  ITMGContextGetInstance()->Poll();
}
:::
</dx-codeblock>

### 7. 인증 정보

관련 기능의 암호화 및 인증을 위해 AuthBuffer를 생성합니다.    
음성 메시지 및 음성 텍스트 변환에 대한 인증을 얻으려면 방 ID 매개변수를 null로 설정해야 합니다.

#### 함수 프로토타입

<dx-codeblock>
::: Java Java
AuthBuffer public native byte[] genAuthBuffer(int sdkAppId, String roomId, String openId, String key)
:::
::: Object-C objetctive-c
//TMGSampleViewController.m
[EnginePollHelper createEnginePollHelper];
//EnginePollHelper.m 및 EnginePollHelper.h 참고
:::
::: C++ C++
void TMGTestScene::update(float delta)
{
  ITMGContextGetInstance()->Poll();
}
:::
</dx-codeblock>

| 매개변수   |  유형  | 의미                                                         |
| ------ | :----: | ------------------------------------------------------------ |
| appId  |  int   | Tencent Cloud 콘솔의 AppId.                              |
| roomId | string | 방 ID, 최대 127자 지원(음성 메시지의 경우 null 입력).   |
| openId | string | Init 시 openId와 동일한 사용자 ID.                        |
| key    | string | Tencent Cloud [콘솔](https://console.cloud.tencent.com/gamegme)의 권한 키. |


####  예시 코드  

<dx-codeblock>
::: Java Java
//GMEAuthBufferHelper.java
import com.tencent.av.sig.AuthBuffer;//헤더파일
public byte[] createAuthBuffer(String roomId)
    {
        byte[] authBuffer;
        // Generate AuthBuffer for encryption and authentication of relevant features. For release in the production environment,
        // please use the backend deployment key as detailed in https://intl.cloud.tencent.com/document/product/607/12218
        if (TextUtils.isEmpty(roomId))
        {
            authBuffer =  AuthBuffer.getInstance().genAuthBuffer(Integer.parseInt(mAppId), "0", mOpenId, mKey);
        }else
        {
            authBuffer =  AuthBuffer.getInstance().genAuthBuffer(Integer.parseInt(mAppId), roomId, mOpenId, mKey);
        }
        return authBuffer;
    }
:::
::: Object-C objetctive-c
//실시간 음성 채팅 인증 
NSData* authBuffer = [QAVAuthBuffer GenAuthBuffer:SDKAPPID3RD.intValue roomID:self.roomIdTF.text openID:_openId key:_key];
//음성 메시지 인증
NSData* authBuffer =  [QAVAuthBuffer GenAuthBuffer:(unsigned int)SDKAPPID3RD.integerValue roomID:nil openID:self.openId key:AUTHKEY];
:::
::: C++ C++
unsigned int bufferLen = 512;
unsigned char retAuthBuff[512] = {0};
QAVSDK_AuthBuffer_GenAuthBuffer(atoi(SDKAPPID3RD), roomId, "10001", AUTHKEY,retAuthBuff,bufferLen);
:::
</dx-codeblock>


## 실시간 음성 채팅 액세스

###  [1. 방 입장](id:EnterRoom)

생성된 인증 정보로 방에 진입하며, 수신 정보는 ITMG_MAIN_EVENT_TYPE_ENTER_ROOM의 콜백입니다. 진입한 방은 마이크와 스피커 끔 상태가 디폴트이며, 리턴값이 AV_OK 일 경우 성공입니다.

방 오디오 유형은 [Sound Quality](https://intl.cloud.tencent.com/document/product/607/18522)을 참고하십시오.

#### 함수 프로토타입

<dx-codeblock>
::: Java Java
public abstract int EnterRoom(String roomID, int roomType, byte[] authBuffer);
:::
::: Object-C objetctive-c
-(int)EnterRoom:(NSString*) roomId roomType:(int)roomType authBuffer:(NSData*)authBuffer;
:::
::: C++ C++
ITMGContext virtual int EnterRoom(const char*  roomID, ITMG_ROOM_TYPE roomType, const char* authBuff, int buffLen);
:::
</dx-codeblock>

| 매개변수       |  유형  | 의미                    |
| ---------- | :----: | ----------------------- |
| roomId     | String | 방 ID, 최대 127자 지원 |
| roomType   |  int   | 방 오디오 유형            |
| authBuffer | byte[] | 인증 코드                  |

#### 예시 코드  

<dx-codeblock>
::: Java Java
//RealTimeVoiceActivity.java
byte[] authBuffer =  GMEAuthBufferHelper.getInstance().createAuthBuffer(roomId);
ITMGContext.GetInstance(this).EnterRoom(roomId, roomType, authBuffer);
:::
::: Object-C objetctive-c
//TMGRealTimeViewController.m
[[ITMGContext GetInstance] EnterRoom:self.roomIdTF.text roomType:(int)self.roomTypeControl.selectedSegmentIndex + 1 authBuffer:authBuffer];
:::
::: C++ C++
ITMGContext* context = ITMGContextGetInstance();
context->EnterRoom(roomID, ITMG_ROOM_TYPE_STANDARD, (char*)retAuthBuff,bufferLen);
:::
</dx-codeblock>

#### 방 입장 이벤트 콜백

사용자가 방에 입장한 후 ITMG_MAIN_EVENT_TYPE_ENTER_ROOM 메시지가 전송되고 콜백 및 처리를 위해 OnEvent 함수에서 식별됩니다. 성공적인 콜백은 방 입장 성공 및 **과금** 시작을 의미합니다.

<dx-fold-block title="과금 참고">
[Purchase Guide](https://intl.cloud.tencent.com/document/product/607/36276)
[Billing](https://intl.cloud.tencent.com/document/product/607/30255)
[Will the billing continue if the client is disconnected from the server when using the voice chat?](https://intl.cloud.tencent.com/document/product/607/30255)
</dx-fold-block>

- **예시 코드**  
방 입장 및 네트워크 연결 해제 이벤트를 포함한 콜백 처리 예시 코드입니다.
<dx-codeblock>
::: Java Java
//RealTimeVoiceActivity.java
public void OnEvent(ITMGContext.ITMG_MAIN_EVENT_TYPE type, Intent data) {
    if (type == ITMG_MAIN_EVENT_TYPE_ENTER_ROOM)
    {
        // Step 6/11 : Perform the enter room event
        int nErrCode = TMGCallbackHelper.ParseIntentParams2(data).nErrCode;
        String strMsg = TMGCallbackHelper.ParseIntentParams2(data).strErrMsg;
        if (nErrCode == AV_OK)
        {
            appendLog2MonitorView("EnterRomm success");
        }else
        {
            appendLog2MonitorView(String.format(Locale.getDefault(), "EnterRomm errCode:%d errMsg:%s", nErrCode, strMsg));
        }
    }
}		
:::
::: Object-C objetctive-c
//TMGRealTimeViewController.m

- (void)OnEvent:(ITMG_MAIN_EVENT_TYPE)eventType data:(NSDictionary *)data {
  NSString *log = [NSString stringWithFormat:@"OnEvent:%d,data:%@", (int)eventType, data];
  [self showLog:log];
  NSLog(@"====%@====", log);
  switch (eventType) {
      // Step 6/11 : Perform the enter room event
      case ITMG_MAIN_EVENT_TYPE_ENTER_ROOM: {
          int result = ((NSNumber *)[data objectForKey:@"result"]).intValue;
          NSString *error_info = [data objectForKey:@"error_info"];

          [self showLog:[NSString stringWithFormat:@"OnEnterRoomComplete:%d msg:(%@)", result, error_info]];
      
          if (result == 0) {
              [self updateStatusEnterRoom:YES];
          }
      }
      break;

  }
  :::
  ::: C++ C++
  void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data){
  switch (eventType) {
      case ITMG_MAIN_EVENT_TYPE_ENTER_ROOM:
      {
          ListMicDevices();
          ListSpeakerDevices();
              std::string strText = "EnterRoom complete: ret=";
          strText += data;
          m_EditMonitor.SetWindowText(MByteToWChar(strText).c_str());
          }
  }
  }
  :::
  </dx-codeblock>
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

<dx-codeblock>
::: Java Java
//RealTimeVoiceActivity.java
ITMGContext.GetInstance(this).GetAudioCtrl().EnableMic(true);
:::
::: Object-C objetctive-c
//TMGRealTimeViewController.m
[[[ITMGContext GetInstance] GetAudioCtrl] EnableMic:YES];
:::
::: C++ C++
ITMGContextGetInstance()->GetAudioCtrl()->EnableMic(true);
:::
</dx-codeblock>

### [3. 스피커 활성화 또는 비활성화](id:EnableSpeaker)

이 API는 스피커를 활성화/비활성화하는 데 사용됩니다.

#### 예시 코드  

<dx-codeblock>
::: Java Java
//RealTimeVoiceActivity.java
ITMGContext.GetInstance(this).GetAudioCtrl().EnableSpeaker(true);
:::
::: Object-C objetctive-c
//TMGRealTimeViewController.m
[[[ITMGContext GetInstance] GetAudioCtrl] EnableSpeaker:YES];
:::
::: C++ C++
ITMGContextGetInstance()->GetAudioCtrl()->EnableSpeaker(true);
:::
</dx-codeblock>


### [4. 방 퇴장](id:ExitRoom)

이 API는 현재 방을 나가기 위해 호출됩니다. 비동기 API입니다. 반환된 AV_OK 값은 성공적인 비동기 전달을 나타냅니다.

#### 예시 코드  

<dx-codeblock>
::: Java Java
//RealTimeVoiceActivity.java
ITMGContext.GetInstance(this).ExitRoom();
:::
::: Object-C objetctive-c
//TMGRealTimeViewController.m
[[ITMGContext GetInstance] ExitRoom];
:::
::: C++ C++
ITMGContext* context = ITMGContextGetInstance();
context->ExitRoom();
:::
</dx-codeblock>


#### 방 퇴장 콜백

사용자가 방을 나가면 ITMG_MAIN_EVENT_TYPE_EXIT_ROOM이라는 메시지와 함께 콜백이 반환됩니다. 예시 코드는 아래와 같습니다.
<dx-codeblock>
::: Java Java
//RealTimeVoiceActivity.java
public void OnEvent(ITMGContext.ITMG_MAIN_EVENT_TYPE type, Intent data) {
	if (ITMGContext.ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVENT_TYPE_EXIT_ROOM == type)
        {
            //방 퇴장 성공 이벤트 수신
        }
}
:::
::: Object-C objetctive-c
//TMGRealTimeViewController.m
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
:::
::: C++ C++
void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data){
switch (eventType) {
    case ITMG_MAIN_EVENT_TYPE_EXIT_ROOM:
    {
        //처리 진행
        break;
        }
    }
}
:::
</dx-codeblock>



## 음성 메시지 액세스


### [1. 인증 초기화](id:ApplyPtt)

SDK 초기화 후 인증 초기화를 호출합니다. authBuffer를 얻는 방법에 대한 자세한 내용은 genAuthBuffer(실시간 음성 채팅 인증 정보 API)를 참고하십시오.

#### 함수 프로토타입  

<dx-codeblock>
::: Java Java
public abstract int ApplyPTTAuthbuffer(byte[] authBuffer);
:::
::: Object-C objetctive-c
-(QAVResult)ApplyPTTAuthbuffer:(NSData *)authBuffer;
:::
::: C++ C++
ITMGPTT virtual int ApplyPTTAuthbuffer(const char* authBuffer, int authBufferLen)
:::
</dx-codeblock>

| 매개변수       |  유형  | 의미                    |
| ---------- | :----: | ---- |
| authBuffer | String | 인증 |

#### 예시 코드  

<dx-codeblock>
::: Java Java
//VoiceMessageRecognitionActivity.java
byte[] authBuffer = GMEAuthBufferHelper.getInstance().createAuthBuffer("");
ITMGContext.GetInstance(this).GetPTT().ApplyPTTAuthbuffer(authBuffer);
:::
::: Object-C objetctive-c
//TMGPTTViewController.m
NSData* authBuffer =  [QAVAuthBuffer GenAuthBuffer:(unsigned int)SDKAPPID3RD.integerValue roomID:nil openID:self.openId key:AUTHKEY];
[[[ITMGContext GetInstance] GetPTT] ApplyPTTAuthbuffer:authBuffer];
:::
::: C++ C++
ITMGContextGetInstance()->GetPTT()->ApplyPTTAuthbuffer(authBuffer,authBufferLen);
:::
</dx-codeblock>

### [2. 스트리밍 음성 인식 시작](id:StartRWSR)

이 API는 스트리밍 음성 인식을 시작하는 데 사용됩니다. 음성을 텍스트로 변환하여 얻은 텍스트는 콜백에서 실시간으로 반환됩니다. 인식할 언어를 지정하거나 음성으로 인식된 정보를 지정된 언어로 번역하고 번역을 반환할 수 있습니다. **녹음을 중지하려면 StopRecording을 호출합니다**. 녹음이 중지된 후 콜백이 반환됩니다.

#### API 프로토타입  

<dx-codeblock>
::: Java Java
public abstract int StartRecordingWithStreamingRecognition (String filePath);
public abstract int StartRecordingWithStreamingRecognition (String filePath,String language,String translatelanguage);
public abstract int StopRecording();
:::
::: Object-C objetctive-c
-(int)StartRecordingWithStreamingRecognition:(NSString *)filePath;
-(int)StartRecordingWithStreamingRecognition:(NSString *)filePath language:(NSString*)speechLanguage translatelanguage:(NSString*)translatelanguage;
-(QAVResult)StopRecording;
:::
::: C++ C++
ITMGPTT virtual int StartRecordingWithStreamingRecognition(const char* filePath) 
ITMGPTT virtual int StartRecordingWithStreamingRecognition(const char* filePath,const char* translateLanguage,const char* translateLanguage)
ITMGPTT virtual int StopRecording()
:::
</dx-codeblock>


| 매개변수              |  유형  | 의미                                                         |
| ----------------- | :----: | ------------------------------------------------------------ |
| filePath          | String | 저장된 오디오 파일의 경로                                               |
| speechLanguage    | String | 오디오 파일이 텍스트로 변환될 언어이며, 매개변수는 [Language Parameter Reference List](https://intl.cloud.tencent.com/document/product/607/30260) 참고 |
| translateLanguage | String | 오디오 파일이 번역될 언어 매개변수. [Language Parameter Reference List](https://intl.cloud.tencent.com/document/product/607/30260) 참고(현재 이 매개변수는 사용할 수 없으며, speechLanguage와 동일한 값을 입력하십시오) |

#### 예시 코드  

<dx-codeblock>
::: Java Java
//VoiceMessageRecognitionActivity.java
ITMGContext.GetInstance(this).GetPTT().StartRecordingWithStreamingRecognition(recordfilePath,"cmn-Hans-CN");
:::
::: Object-C objetctive-c
//TMGPTTViewController.m
QAVResult ret = [[[ITMGContext GetInstance] GetPTT] StartRecordingWithStreamingRecognition:[self pttTestPath] language:@"cmn-Hans-CN"];
if (ret == 0) {
    self.currentStatus = @"스트리밍 녹화 시작";
} else {
    self.currentStatus = @"스트리밍 녹화 시작 실패";
}
:::
::: C++ C++
ITMGContextGetInstance()->GetPTT()->StartRecordingWithStreamingRecognition(filePath,"cmn-Hans-CN","cmn-Hans-CN");
:::
</dx-codeblock>

#### 스트리밍 음성 인식 콜백

스트리밍 음성 인식이 시작된 후 콜백 함수 OnEvent에서 콜백 메시지를 수신해야 합니다. 이벤트 메시지는 `ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_COMPLETE`입니다. 즉, 녹음이 중지되고 인식이 완료된 후 텍스트를 반환하는데, 이는 한 단락을 말한 후에 인식된 텍스트를 반환하는 것과 같습니다.

이벤트 메시지는 실제 필요에 따라 OnEvent 함수에서 식별됩니다. 전달된 매개변수에는 다음 네 가지 메시지가 포함됩니다.

| 메시지 이름  |                    의미                     |
| --------- | :-----------------------------------------: |
| result    |    스트리밍 음성 인식 성공 여부를 판단하기 위한 반환 코드     |
| text      |            음성에서 변환된 텍스트             |
| file_path |             저장된 녹음 파일의 로컬 경로              |
| file_id   | 90일 동안 보관되는 녹음 파일의 백엔드 url 주소 |

- **예시 코드**  
<dx-codeblock>
::: Java Java
//VoiceMessageRecognitionActivity.java
import static com.tencent.TMG.ITMGContext.ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_COMPLETE;
public void OnEvent(ITMGContext.ITMG_MAIN_EVENT_TYPE type, Intent data) {
	if (type == ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_COMPLETE)
        {
            // Step 1.3/3 handle ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_COMPLETE event
            mIsRecording = false;
            if (nErrCode ==0)
            {
                String recordfilePath = data.getStringExtra("file_path");
                mRecFilePathView.setText(recordfilePath);

                String recordFileUrl = data.getStringExtra("file_id");
                mRecFileUrlView.setText(recordFileUrl);
            }
            else
            {
                appendLog2MonitorView("Record and recognition fail errCode:" + nErrCode);
            }
        }

}
:::
::: Object-C objetctive-c
//TMGPTTViewController.m

- (void)OnEvent:(ITMG_MAIN_EVENT_TYPE)eventType data:(NSDictionary*)data
  {
  NSNumber *number = [data objectForKey:@"result"];
  switch (eventType)
  {
  	case ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_COMPLETE:
  	{
            if (data != NULL &&[[data objectForKey:@"result"] intValue]== 0)
            {
                self.translateTF.text = [data objectForKey:@"text"] ;
                 self.currentStatus = @"스트리밍 변환 완료";
            }
        }
  	break;
  }
  :::
  ::: C++ C++
  void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data){
    switch (eventType) {
        case ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_COMPLETE:
        {
            HandleSTREAM2TEXTComplete(data,true);
            break;
        }
        ...
        case ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_IS_RUNNING:
        {
            HandleSTREAM2TEXTComplete(data, false);
            break;
        }
    }
  }
  void CTMGSDK_For_AudioDlg::HandleSTREAM2TEXTComplete(const char* data, bool isComplete)
  {
    std::string strText = "STREAM2TEXT: ret=";
    strText += data;
    m_EditMonitor.SetWindowText(MByteToWChar(strText).c_str());
    Json::Reader reader;
    Json::Value root;
    bool parseRet = reader.parse(data, root);
    if (!parseRet) {
        ::SetWindowText(m_EditInfo.GetSafeHwnd(),MByteToWChar(std::string("parse result Json error")).c_str());
    }
        else
        {
            if (isComplete) {
                                ::SetWindowText(m_EditUpload.GetSafeHwnd(), MByteToWChar(root["file_id"].asString()).c_str());
                            }
                            else{
                                    std::string isruning = "STREAMINGRECOGNITION_IS_RUNNING";
                                    ::SetWindowText(m_EditUpload.GetSafeHwnd(), MByteToWChar(isruning).c_str());
                                 }
    }
  }
  :::
  </dx-codeblock>
- **에러 코드**
<table>
<thead>
<tr>
<th>에러 코드</th>
<th align="center">의미</th>
<th align="center">처리 방식</th>
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
<td align="center">스트리밍 녹화 중 상태에서 스트리밍 녹화 API의 실행 결과가 반환될 때까지 기다리십시오</td>
</tr>
</tbody></table>



### [3. 녹음 중지](id:Stop)

이 API는 녹음을 중지하는 데 사용됩니다. 비동기식이며 녹음이 중지된 후 녹음 완료를 위한 콜백이 반환됩니다. 녹음 파일은 녹음이 성공한 후에만 사용할 수 있습니다.

#### API 프로토타입  

<dx-codeblock>
::: Java Java
public abstract int StopRecording();
:::
::: Object-C objetctive-c
-(QAVResult)StopRecording;
:::
::: C++ C++
ITMGPTT virtual int StopRecording();
:::
</dx-codeblock>


#### 예시 코드  

<dx-codeblock>
::: Java Java
//VoiceMessageRecognitionActivity.java
ITMGContext.GetInstance(this).GetPTT().StopRecording();
:::
::: Object-C objetctive-c
//TMGPTTViewController.m

- (void)stopRecClick {
  // Step 3/12 stop recording,  need handle ITMG_MAIN_EVNET_TYPE_PTT_RECORD_COMPLETE event
  // https://cloud.tencent.com/document/product/607/15221#.E5.81.9C.E6.AD.A2.E5.BD.95.E9.9F.B3
  QAVResult ret =  [[[ITMGContext GetInstance] GetPTT] StopRecording];
   if (ret == 0) {
       self.currentStatus = @"녹음 중지";
   } else {
        self.currentStatus = @"녹음 중지 실패";
   }
  }
  :::
  ::: C++ C++
  ITMGContextGetInstance()->GetPTT()->StopRecording();
  :::
  </dx-codeblock>
