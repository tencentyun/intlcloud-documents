## 문서 가이드
본 문서에서는 TRTC SDK를 기반으로 간단한 영상 통화 기능 구현을 소개합니다. 가장 많이 사용되는 몇 가지 인터페이스만 소개하고 있으며, 더 많은 인터페이스 함수에 대한 자세한 내용은 [API 문서](https://intl.cloud.tencent.com/document/product/647/35119)를 참고하십시오.


## 예시 코드

| 소속 플랫폼 | 예시 코드 |
|---------|---------|
| Windows(MFC) | [TRTCMainViewController.cpp](https://github.com/tencentyun/TRTCSDK/blob/master/Windows/MFCDemo/TRTCMainViewController.cpp) |
| Windows(Duilib) | [TRTCMainViewController.cpp](https://github.com/tencentyun/TRTCSDK/blob/master/Windows/DuilibDemo/TRTCMainViewController.cpp) |
| Windows(C#) | [TRTCMainForm.cs](https://github.com/tencentyun/TRTCSDK/blob/master/Windows/CSharpDemo/TRTCMainForm.cs) |

## 비디오 통화
### 1. SDK 초기화
TRTC SDK 사용의 첫 번째 단계는 먼저 `getTRTCShareInstance` 내보내기 인터페이스를 통해 `TRTCCloud` 단일 인스턴스 객체의 포인터 `ITRTCCloud*`를 획득하고 SDK 이벤트 리슨 콜백을 등록하는 것입니다.

- `ITRTCCloudCallback` 이벤트 콜백 인터페이스 유형을 상속하여 로컬 사용자의 방 입장/퇴장 이벤트, 원격 사용자의 방 추가/퇴장 이벤트, 오류 이벤트, 알람 이벤트 등 관련 이벤트 콜백 인터페이스를 재작성합니다.
- `addCallback` 인터페이스를 호출하여 SDK 이벤트 리슨을 등록합니다.

>!동일한 이벤트의 `addCallback`이 N번 등록되면 SDK는 N번의 콜백을 트리거하므로 `addCallback`은 1회만 호출하기를 권장합니다.

<dx-codeblock>
::: C++ C++
// TRTCMainViewController.h

// ITRTCCloudCallback 이벤트를 상속하여 인터페이스 유형 콜백
class TRTCMainViewController : public ITRTCCloudCallback
{
public:
	TRTCMainViewController();
	virtual ~TRTCMainViewController();

    virtual void onError(TXLiteAVError errCode, const char* errMsg, void* arg);
    virtual void onWarning(TXLiteAVWarning warningCode, const char* warningMsg, void* arg);
    virtual void onEnterRoom(int result);
    virtual void onExitRoom(int reason);
    virtual void onRemoteUserEnterRoom(const char* userId);
    virtual void onRemoteUserLeaveRoom(const char* userId, int reason);
    virtual void onUserVideoAvailable(const char* userId, bool available);
    virtual void onUserAudioAvailable(const char* userId, bool available);
...
private:
	ITRTCCloud * m_pTRTCSDK = NULL；
...
}

// TRTCMainViewController.cpp

TRTCMainViewController::TRTCMainViewController()
{
    // TRTCCloud 인스턴스 생성
    m_pTRTCSDK = getTRTCShareInstance();
    
    // SDK 콜백 이벤트 등록
    m_pTRTCSDK->addCallback(this);
}

TRTCMainViewController::~TRTCMainViewController()
{
    // 리스너 SDK 이벤트 취소
    if(m_pTRTCSDK) {
        m_pTRTCSDK->removeCallback(this);
    }
    
    // TRTCCloud 인스턴스 릴리스
      if(m_pTRTCSDK != NULL) {
       destroyTRTCShareInstance();
        m_pTRTCSDK = null;
    }
}

// 오류 공지는 리스너가 필요하며, SDK가 계속해서 실행될 수 없음을 의미
virtual void TRTCMainViewController::onError(TXLiteAVError errCode, const char* errMsg, void* arg)
{
    if (errCode == ERR_ROOM_ENTER_FAIL) {
        LOGE(L"onError errorCode[%d], errorInfo[%s]", errCode, UTF82Wide(errMsg).c_str());
		    exitRoom();
	 }
}
:::
::: C# C#
// TRTCMainForm.cs

// ITRTCCloudCallback 이벤트를 상속하여 인터페이스 유형 콜백
public partial class TRTCMainForm : Form, ITRTCCloudCallback, ITRTCLogCallback
{
	...
	private ITRTCCloud mTRTCCloud; 
	...
	
	public TRTCMainForm(TRTCLoginForm loginForm)
	{
		InitializeComponent();
		this.Disposed += new EventHandler(OnDisposed);
		// TRTCCloud 인스턴스 생성
		mTRTCCloud = ITRTCCloud.getTRTCShareInstance();
		// SDK 콜백 이벤트 등록
		mTRTCCloud.addCallback(this);
		...
	}
	
	private void OnDisposed(object sender, EventArgs e)
	{
		if (mTRTCCloud != null)
		{
			// SDK 이벤트 리슨 취소
			mTRTCCloud.removeCallback(this);
			// TRTCCloud 인스턴스 릴리스
			ITRTCCloud.destroyTRTCShareInstance();
			mTRTCCloud = null;
		}
		...
	}
	...
	// 오류 통지는 리스너가 존재해야 하며, SDK가 계속해서 실행될 수 없음을 의미
	public void onError(TXLiteAVError errCode, string errMsg, IntPtr arg)
	{
	     if (errCode == TXLiteAVError.ERR_ROOM_ENTER_FAIL) {
		    exitRoom();
		}
	     ...
	}
	...
}
:::
</dx-codeblock>

### 2. TRTCParams 어셈블리

TRTCParams는 SDK의 가장 주요한 매개변수로 SDKAppID, userId, userSig, roomId의 네 가지 필수 작성 입력 필드가 있습니다.

- **SDKAppID**
  Tencent Cloud TRTC [콘솔](https://console.cloud.tencent.com/rav)에 들어갑니다. 아직 애플리케이션이 없는 경우, 하나를 생성하면 곧바로 SDKAppID를 확인할 수 있습니다.
  
- **userId**
  자유롭게 지정할 수 있으며, 문자열 유형이기 때문에 기존의 계정 체계와 동일하게 입력할 수 있습니다. 단, **동일한 멀티미디어 방 안에 2개의 동일한 userId가 존재할 수 없습니다**.

- **userSig**
  SDKAppID와 userId를 기반으로 userSig를 계산할 수 있으며, 계산 방법은 [UserSig 계산 방법](https://intl.cloud.tencent.com/document/product/647/35166)을 참고하십시오.

- **roomId**
  방 번호는 숫자로 구성되어 있으며 자유롭게 지정할 수 있습니다. 단, **동일한 애플리케이션의 멀티미디어 방 2개에 동일한 roomId를 할당할 수 없습니다.** 문자열 형식의 방 번호를 사용하려면 TRTCParams의 strRoomId를 사용하십시오.

### 3. 방 입장(또는 생성)
`enterRoom`을 호출하여 TRTCParams 매개변수 roomId가 지정한 멀티미디어 방에 입장할 수 있으며, 해당 방이 존재하지 않는 경우 SDK는 자동으로 roomId를 방 번호로 하는 새로운 방을 생성합니다.

**appScene** 매개변수가 SDK를 지정하는 응용 시나리오의 경우 본 문서에서는 `TRTCAppSceneVideoCall`(영상 통화)을 이용합니다. 해당 시나리오에서의 SDK 내부 코덱과 네트워크 모듈은 영상의 원활성에 더 초점을 맞춰 통화 딜레이 및 랙 발생률이 감소됩니다.
				
- 방에 입장하면 SDK는 `onEnterRoom` 인터페이스를 콜백합니다. 매개변수 `result`가 0보다 큰 경우 방 입장에 성공하며, 해당 값은 방 입장에 소요된 시간을 나타내고 단위는 밀리초(ms)입니다. `result`가 0보다 작은 경우 방 입장에 실패하며, 값은 방 입장 실패 에러 코드입니다.
- 방 입장에 실패하면 SDK는 동시에 `onError` 인터페이스를 콜백합니다. 매개변수: `errCode`(에러 코드 `ERR_ROOM_ENTER_FAIL`, 에러 코드는 `TXLiteAVCode.h` 참고), `errMsg`(오류 원인), `extraInfo`(매개변수 보관)
- 이미 방에 입장한 경우 `exitRoom`을 호출하여 해당 방에서 퇴장해야만 다른 방에 들어갈 수 있습니다. 

<dx-codeblock>
::: C++ C++
// TRTCMainViewController.cpp

void TRTCMainViewController::enterRoom()
{
    // 헤더 파일 TRTCCloudDef.h 참고하여 TRTCParams 정의
    TRTCParams params;
    params.sdkAppId = sdkappid;
    params.userId   = userid;
    params.userSig  = usersig;
    params.roomId   = 908; // 입장하려는 방 입력
    if(m_pTRTCSDK)
    {
    	m_pTRTCSDK->enterRoom(params, TRTCAppSceneVideoCall);
    }
}

...
    
void TRTCMainViewController::onError(TXLiteAVError errCode, const char* errMsg, void* arg)
{
    if(errCode == ERR_ROOM_ENTER_FAIL)
    {
        LOGE(L"onError errorCode[%d], errorInfo[%s]", errCode, UTF82Wide(errMsg).c_str());
        // userSig 적합성 여부 및 네트워크 정상 여부 등 확인
    }
}

...

void TRTCMainViewController::onEnterRoom(int result)
{
    LOGI(L"onEnterRoom result[%d]", result);
    if(result >= 0)
	{
		//방 들어가기
	}
	else
	{
		//방 입장 실패, 에러 코드 = result；
	}
}
:::
::: C# C#
// TRTCMainForm.cs

public void EnterRoom()
{
    // 헤더 파일 TRTCCloudDef.h 참고하여 TRTCParams 정의
    TRTCParams @params = new TRTCParams();
    @params.sdkAppId = sdkappid;
    @params.userId   = userid;
    @params.userSig  = usersig;
    @params.roomId   = 908; // 입장하려는 방 입력
    if(mTRTCCloud != null)
    {
    	mTRTCCloud.enterRoom(@params, TRTCAppSceneVideoCall);
    }
}

...
    
public void onError(TXLiteAVError errCode, string errMsg, IntPtr arg)
{
    if(errCode == TXLiteAVError.ERR_ROOM_ENTER_FAIL)
    {
        Log.E(String.Format("errCode : {0}, errMsg : {1}, arg = {2}", errCode, errMsg, arg));
        // userSig 적합성 여부 및 네트워크 정상 여부 등 확인
    }
}

...

public void onEnterRoom(int result)
{
    if(result >= 0)
	{
		//방 들어가기
	}
	else
	{
		//방 입장 실패, 에러 코드 = result；
	}
}
:::
</dx-codeblock>


>!
>- 응용 시나리오에 따라 적합한 scene 매개변수를 선택하십시오. 잘못된 매개변수를 사용하는 경우 랙이 발생하거나 화면 해상도가 떨어질 수 있습니다.
>- 각 엔드는 appScene에서 통일되어야 합니다. 그렇지 않으면 예기치 않은 문제가 발생할 수 있습니다.

### 4. 원격 오디오 스트림 듣기
TRTC SDK는 기본적으로 원격 오디오 스트림을 수신하므로 이를 위해 별도의 코드를 작성할 필요가 없습니다. 특정 userid의 오디오 스트림을 수신하고 싶지 않은 경우 `muteRemoteAudio`를 사용해 음소거할 수 있습니다.

### 5. 원격 비디오 스트림 보기

TRTC SDK는 기본적으로 원격 비디오 스트림을 가져오지 않으며, 방 안의 사용자가 미디오 데이터를 업스트림하는 경우 방 안의 다른 사용자는 ITRTCCloudCallback의 `onUserVideoAvailable` 콜백을 통해 해당 사용자의 userid를 획득하고 `startRemoteView`를 호출하여 해당 사용자의 비디오 화면을 볼 수 있습니다.

`setRemoteViewFillMode`를 통해 비디오 표시 모드를 `Fill` 또는 `Fit` 모드로 지정할 수 있습니다. 두 모드에서의 비디오 사이즈는 모두 동일한 비율로 축소/확대되며, 차이점은 다음과 같습니다.
- `Fill` 모드: 창 전체 화면을 우선으로 합니다. 축소/확대 후의 비디오 크기와 창의 화면 크기가 일치하지 않는 경우, 크기를 초과한 비디오의 나머지 부분을 잘라냅니다.
- `Fit` 모드: 비디오 콘텐츠 전체 표시를 우선으로 하며, 축소/확대 후의 비디오 사이즈와 비디오 창 사이즈가 일치하지 않는 경우 비디오 창의 나머지 부분을 검은색으로 처리합니다.

<dx-codeblock>
::: C++ C++
// TRTCMainViewController.cpp
void TRTCMainViewController::onUserVideoAvailable(const char* userId, bool available){
    if (available) {
        // 렌더링 창 핸들 가져오기
        CWnd *pRemoteVideoView = GetDlgItem(IDC_REMOTE_VIDEO_VIEW);
        HWND hwnd = pRemoteVideoView->GetSafeHwnd();  
        
        // 원격 사용자 비디오 렌더링 모드 설정
        m_pTRTCSDK->setRemoteViewFillMode(TRTCVideoFillMode_Fill);
        // SDK 인터페이스를 호출하여 원격 사용자 스트림 재생
        m_pTRTCSDK->startRemoteView(userId, hwnd);
    } else {
        m_pTRTCSDK->stopRemoteView(userId);
    }    
}
:::
::: C# C#
// TRTCMainForm.cs
public void onUserVideoAvailable(string userId, bool available)
{
    if (available)
	{
		// 창 핸들 가져오기
		IntPtr ptr = GetHandleAndSetUserId(pos, userId, false);
		SetVisableInfoView(pos, false);
		// 원격 사용자 비디오 렌더링 모드 설정
		mTRTCCloud.setRemoteViewFillMode(userId, TRTCVideoFillMode.TRTCVideoFillMode_Fit);
		// SDK 인터페이스를 호출하여 원격 사용자 스트림 재생
		mTRTCCloud.startRemoteView(userId, ptr);
	}
	else
	{
		mTRTCCloud.stopRemoteView(userId);
		...
	}
}
:::
</dx-codeblock>


### 6. 로컬 음성 수집 활성화/비활성화

TRTC SDK는 기본적으로 로컬 마이크 음성 수집 기능이 비활성화되어 있으며, `startLocalAudio`로 로컬 음성 수집을 활성화하여 멀티미디어 데이터를 방송할 수 있고 `stopLocalAudio`은 비활성화됩니다.
>?'startLocalPreview'에서 이후 계속해서 `startLocalAudio`를 호출할 수 있습니다.

### 7. 로컬 비디오 수집 활성화/비활성화

TRTC SDK는 기본적으로 로컬 카메라 수집 기능이 비활성화되어 있으며, `startLocalPreview`에서 로컬 카메라를 활성화하고 미리보기 화면을 표시할 수 있고 `stopLocalPreview`는 비활성화됩니다.

- `startLocalPreview`를 호출하여 로컬 비디오 렌더링 창을 지정하면 **SDK가 동적으로 창 사이즈를 점검하고 `rendHwnd`에서 전체 창에 렌더링합니다**.
- `setLocalViewFillMode` 인터페이스를 호출하여 로컬 비디오 렌더링 모드를 `Fill` 또는 `Fit` 모드로 지정할 수 있습니다. 두 모드에서의 비디오 사이즈는 모두 동일한 비율로 축소/확대되며, 차이점은 다음과 같습니다.
  - `Fill` 모드: 창 전체 표시를 우선으로 하며, 축소/확대 후의 비디오 사이즈와 창 사이즈가 일치하지 않는 경우 창을 초과한 나머지 부분을 잘라냅니다.
  - `Fit` 모드: 비디오 콘텐츠 전체 표시를 우선으로 하며, 축소/확대 후의 비디오 사이즈와 창 사이즈가 일치하지 않는 경우 창의 나머지 부분을 검은색으로 처리합니다.

<dx-codeblock>
::: C++ C++
// TRTCMainViewController.cpp

void TRTCMainViewController::onEnterRoom(uint64_t elapsed)
{
    ...
    
	// 렌더링 창 핸들 가져오기
	CWnd *pLocalVideoView = GetDlgItem(IDC_LOCAL_VIDEO_VIEW);
	HWND hwnd = pLocalVideoView->GetSafeHwnd();
	
	if(m_pTRTCSDK)
	{
	    // SDK 인터페이스를 호출하여 렌더링 모드 및 렌더링 창 설정
	    m_pTRTCSDK->setLocalViewFillMode(TRTCVideoFillMode_Fit);
	    m_pTRTCSDK->startLocalPreview(hwnd);
	}
	
	...
}
:::
::: C# C#
// TRTCMainForm.cs

public void onEnterRoom(int result)
{
	...
	// 렌더링 창 핸들 가져오기
	IntPtr ptr = GetHandle();
    if (mTRTCCloud != null)
    {
        //SDK 인터페이스를 호출하여 렌더링 모드 및 렌더링 창 설정
        mTRTCCloud.setLocalViewFillMode(TRTCVideoFillMode_Fit);
        mTRTCCloud.startLocalPreview(ptr);
    }
	...
}
:::
</dx-codeblock>


### 8. 멀티미디어 데이터 플로 차단

- **로컬 비디오 데이터 차단**
  통화 중 프라이버시 보호를 목적으로 방 안의 다른 사용자가 일시적으로 귀하의 화면을 보지 못하게 로컬 비디오 데이터를 차단하고 싶은 경우 `muteLocalVideo`를 호출할 수 있습니다.
  
- **로컬 오디오 데이터 차단**
  통화 중 프라이버시 보호를 목적으로 방 안의 다른 사용자가 일시적으로 귀하의 음성을 듣지 못하게 로컬 오디오 데이터를 차단하고 싶은 경우 `muteLocalAudio`를 호출할 수 있습니다.
  
- **원격 비디오 데이터 차단**
  `stopRemoteView`를 통해 특정 userid의 비디오 데이터를 차단할 수 있습니다.
  `stopAllRemoteView`를 통해 모든 원격 사용자의 비디오 데이터를 차단할 수 있습니다.
  
- **원격 오디오 데이터 차단**
  `muteRemoteAudio`를 통해 특정 userid의 오디오 데이터를 차단할 수 있습니다.
  `muteAllRemoteAudio`를 통해 모든 원격 사용자의 오디오 데이터를 차단할 수 있습니다.

### 9. 방 퇴장

`exitRoom`을 호출하여 방에서 나갈 수 있습니다. 현재 통화 중인 상태에서도 해당 방법을 호출하여 영상 통화 관련 모든 리소스를 릴리스할 수 있습니다.
>?`exitRoom`을 호출하면 SDK는 복잡한 퇴장 핸드셰이크 프로세스에 들어가게 되며, SDK가 `onExitRoom`을 콜백해야만 실제로 리소스 릴리스가 완료됩니다.
<dx-codeblock>
::: C++ C++
// TRTCMainViewController.cpp

void TRTCMainViewController::exitRoom()
{
    if(m_pTRTCSDK)
    {
    	m_pTRTCSDK->exitRoom();
    }
}
....
void TRTCMainViewController::onExitRoom(int reason)
{
	// 방 퇴장 성공, 현재는 reason 매개변수 보관은 사용하지 않음.

    ...
}
:::
::: C# C#
// TRTCMainForm.cs

public void OnExit()
{
    if(mTRTCCloud != null)
    {
    	mTRTCCloud.exitRoom();
    }
}
...
public void onExitRoom(int reason)
{
    //방 퇴장 성공
    ...
}
:::
</dx-codeblock>

