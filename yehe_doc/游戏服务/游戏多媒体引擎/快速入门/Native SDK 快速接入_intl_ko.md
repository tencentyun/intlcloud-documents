본문에서는 Native 프로젝트 개발자가 GME(Game Multimedia Engine)용 API를 쉽게 디버깅하고 통합할 수 있도록 자세한 설명을 제공합니다.

이 문서는 API 디버깅 및 통합을 위해 GME를 시작하는 데 도움이 되는 기본 API만 제공합니다.

## GME 사용 시 주의할 점

GME는 실시간 음성 채팅 서비스와 음성 메시지 및 음성-텍스트 변환 서비스의 두 가지 서비스를 제공하며 둘 다 Init 및 Poll과 같은 주요 API에 의존합니다.

<dx-alert infotype="notice" title="Init API 정보">
실시간 음성 채팅과 음성 메시지 서비스를 동시에 사용해야 하는 경우 **Init API를 한 번만 호출하면 됩니다**.
</dx-alert>

### API 호출 순서도

![image](https://qcloudimg.tencent-cloud.cn/raw/c8758a24fe68fc084b8d12b09de5e27a.jpg)

### 액세스 단계

#### 핵심 API


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

- <dx-tag-link link="#Init" tag="API: UnInit">GME 초기화 해제</dx-tag-link>

## 핵심 API 액세스

### 1. SDK 다운로드 

SDK 다운로드 가이드 페이지에서 적절한 <dx-tag-link link="https://intl.cloud.tencent.com/document/product/607/18521" tag="DownLoad">클라이언트 SDK</dx-tag-link>를 다운로드합니다.


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

음성 기능을 사용하려면 ITMGContext 객체를 먼저 가져와야 합니다.

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

API 클래스는 Delegate 메소드를 사용하여 애플리케이션에 콜백 알림을 보냅니다. 콜백 메시지 수신을 위해 입장 전 SDK에 콜백 함수를 등록합니다.

#### 함수 프로토타입 및 예시 코드

콜백 메시지 수신을 위해 입장 전에 SDK에 콜백 함수를 등록합니다.

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


| 매개변수             | 유형               | 설명                     |
| ---- | :------------------------------: | ------------------------ |
| type | ITMGContext.ITMG_MAIN_EVENT_TYPE | 콜백 이벤트 유형           |
| data |         Intent 메시지 유형          | 콜백 메시지, 즉, 이벤트 데이터 |

### [5. SDK 초기화](id:Init)

실시간 음성, 음성 메시지, 음성 텍스트 변환 서비스를 사용하려면 먼저 **Init API를 통해 SDK를 초기화해야 합니다**. Init API는 다른 API와 동일한 스레드에서 호출해야 합니다. 기본 스레드에서 모든 API를 호출하는 것이 좋습니다.

#### API 프로토타입

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


| 매개변수     |  유형  | 설명                                                         |
| -------- | :----: | ------------------------------------------------------------ |
| sdkAppId | string | [GME 콘솔](https://console.cloud.tencent.com/gamegme)에서 제공되는 AppID는 [서비스 활성화](https://intl.cloud.tencent.com/document/product/607/10782)에서 안내된 대로 얻을 수 있습니다. |
| openID   | string | openID는 Int64 타입만 가능하며 문자열로 변환되어 전달됩니다. 해당 규칙을 사용자 정의할 수 있으며 App에서 고유해야 합니다. Openid를 문자열로 전달하기 위해서는 [Submit Ticket](https://console.cloud.tencent.com/workorder/category?level1_id=438&level2_id=445&source=0&data_title=%E6%B8%B8%E6%88%8F%E5%A4%9A%E5%AA%92%E4%BD%93%E5%BC%95%E6%93%8EGME&step=1)하여 신청하십시오.|

#### 예시 코드 

<dx-codeblock>
::: Java Java
//MainActivity.java
int nRet = tmgContext.Init(appId, openId);
if (nRet == AV_OK )
{
    GMEAuthBufferHelper.getInstance().setGEMParams(appId, key, openId);
    // Step 4/11: Poll to trigger callback
    //https://www.tencentcloud.com/document/product/607/40860
    EnginePollHelper.createEnginePollHelper();
    showToast("Init success");
}else if (nRet == AV_ERR_HAS_IN_THE_STATE) // SDK가 초기화되었습니다. 이 작업은 성공적입니다.
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

이벤트 콜백은 update에서 Poll API를 주기적으로 호출하여 트리거할 수 있습니다. Poll API는 GME의 메시지 펌프이며 GME가 이벤트 콜백을 트리거하도록 주기적으로 호출해야 합니다. 그렇지 않으면 전체 SDK 서비스가 비정상적으로 실행됩니다. 자세한 내용은 [SDK 다운로드 가이드](https://intl.cloud.tencent.com/document/product/607/18521)의 EnginePollHelper 파일을 참고하십시오.

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

### 7. 로컬 인증 키 계산

관련 기능의 암호화 및 인증을 위해 AuthBuffer를 생성합니다. 프로덕션 환경에서 릴리스하려면 [Authentication Key](https://intl.cloud.tencent.com/document/product/607/12218)에 설명된 대로 백엔드 배포 키를 사용하십시오.    

#### API 프로토타입

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

| 매개변수   |  유형  | 설명                                                         |
| ------ | :----: | ------------------------------------------------------------ |
| appId  |  int   | Tencent Cloud 콘솔의 AppId.                              |
| roomId | string | 방 ID, 최대 127자 지원(음성 메시지의 경우 null 입력).   |
| openId | string | 사용자 ID. Init 시 openId와 동일.                       |
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

생성된 인증 정보로 방에 입장하기 위해 사용하는 API입니다. 마이크와 스피커는 방 입장 후 기본적으로 켜지지 않습니다. 반환된 AV_OK 값은 API 호출은 성공했지만 방 입장은 성공하지 못했다는 의미입니다.

#### API 프로토타입

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

| 매개변수     |  유형  | 설명                    |
| ---------- | :----: | ----------------------- |
| roomId     | String | 방 ID, 최대 127자 지원 |
| roomType   |  int   | FLUENCY 음질을 사용하여 방에 입장하십시오 |
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
context->EnterRoom(roomID, ITMG_ROOM_TYPE_FLUENCY, (char*)retAuthBuff,bufferLen);
:::
</dx-codeblock>

#### 방 입장 콜백

사용자가 방에 입장한 후 ITMG_MAIN_EVENT_TYPE_ENTER_ROOM 메시지가 전송되고 콜백 및 처리를 위해 OnEvent 함수에서 식별됩니다. 성공적인 콜백은 방 입장 성공 및 **과금** 시작을 의미합니다.

<dx-fold-block title="과금 참고">
[Purchase Guide](https://intl.cloud.tencent.com/document/product/607/50009)
[Billing](https://intl.cloud.tencent.com/document/product/607/30255)
[음성 채팅 사용 시 클라이언트가 서버와 연결이 끊긴 경우에도 계속 과금됩니까?](https://intl.cloud.tencent.com/document/product/607/30255#.E4.BD.BF.E7.94.A8.E5.AE.9E.E6.97.B6.E8.AF.AD.E9.9F.B3.E5.90.8E.EF.BC.8C.E5.A6.82.E6.9E.9C.E5.AE.A2.E6.88.B7.E7.AB.AF.E6.8E.89.E7.BA.BF.E4.BA.86.EF.BC.8C.E6.98.AF.E5.90.A6.E8.BF.98.E4.BC.9A.E7.BB.A7.E7.BB.AD.E8.AE.A1.E8.B4.B9.EF.BC.9F)
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

이 API는 현재 방을 나가기 위해 호출됩니다. 종료를 위해 콜백을 기다리고 처리해야 합니다.

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
        //프로세스
        break;
        }
    }
}
:::
</dx-codeblock>



## 음성 메시지 액세스


### [1. 인증 초기화](id:ApplyPtt)

SDK 초기화 후 인증 초기화를 호출합니다. authBuffer를 얻는 방법에 대한 자세한 내용은 genAuthBuffer(실시간 음성 채팅 인증 정보 API)를 참고하십시오.

#### API 프로토타입  

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

이 API는 스트리밍 음성 인식을 시작하는 데 사용됩니다. 음성-텍스트 변환에서 얻은 텍스트는 콜백에서 실시간으로 반환됩니다. **녹음을 중지하려면 StopRecording을 호출합니다**. 녹음이 중지된 후 콜백이 반환됩니다.

#### API 프로토타입  

<dx-codeblock>
::: Java Java
public abstract int StartRecordingWithStreamingRecognition (String filePath);

public abstract int StopRecording();
:::
::: Object-C objetctive-c
-(int)StartRecordingWithStreamingRecognition:(NSString *)filePath;

-(QAVResult)StopRecording;
:::
::: C++ C++
ITMGPTT virtual int StartRecordingWithStreamingRecognition(const char* filePath) 

ITMGPTT virtual int StopRecording()
:::
</dx-codeblock>


| 매개변수              |  유형  | 설명                                                         |
| ----------------- | :----: | ------------------------------------------------------------ |
| filePath          | String | 저장된 오디오 파일의 경로                                               |


#### 예시 코드  

<dx-codeblock>
::: Java Java
//VoiceMessageRecognitionActivity.java
ITMGContext.GetInstance(this).GetPTT().StartRecordingWithStreamingRecognition(recordfilePath);
:::
::: Object-C objetctive-c
//TMGPTTViewController.m
QAVResult ret = [[[ITMGContext GetInstance] GetPTT] StartRecordingWithStreamingRecognition:[self pttTestPath]];
if (ret == 0) {
    self.currentStatus = @"스트리밍 녹음 시작";
} else {
    self.currentStatus = @"스트리밍 녹음 시작 실패";
}
:::
::: C++ C++
ITMGContextGetInstance()->GetPTT()->StartRecordingWithStreamingRecognition(filePath);
:::
</dx-codeblock>

#### 스트리밍 음성 인식 콜백

스트리밍 음성 인식이 시작된 후 콜백 함수 OnEvent에서 콜백 메시지를 수신 대기해야 합니다. 이벤트 메시지는 `ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_COMPLETE`입니다. 즉, 녹화가 중지되고 인식이 완료된 후 텍스트를 반환합니다. 이는 한 단락을 말한 이후에 인식된 텍스트를 반환하는 것과 같습니다.

이벤트 메시지는 실제 필요에 따라 OnEvent 함수에서 식별됩니다. 전달된 매개변수에는 다음 네 가지 메시지가 포함됩니다.

| 메시지 이름  |                    설명                     |
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
  // https://www.tencentcloud.com/document/product/607/15221
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

	
