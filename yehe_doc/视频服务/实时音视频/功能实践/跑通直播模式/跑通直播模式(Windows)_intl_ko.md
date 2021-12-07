## 문서 가이드
본 문서에서는 TRTC SDK를 기반으로 비디오와 마이크 동시 연결이 지원되면서도 수많은 사용자가 동시 접속해 시청할 수 있는 온라인 라이브 방송 기능을 소개합니다. 본 문서에서는 가장 많이 사용되는 몇 가지 인터페이스만 소개하고 있으며, 더 많은 인터페이스 함수에 대한 자세한 내용은 [API 문서](https://intl.cloud.tencent.com/document/product/647/35119)를 참고하십시오.


## 예시 코드

| 소속 플랫폼 | 예시 코드 |
|---------|---------|
| Windows(MFC) | [TRTCMainViewController.cpp](https://github.com/tencentyun/TRTCSDK/blob/master/Windows/MFCDemo/TRTCMainViewController.cpp) |
| Windows(Duilib) | [TRTCMainViewController.cpp](https://github.com/tencentyun/TRTCSDK/blob/master/Windows/DuilibDemo/TRTCMainViewController.cpp) |
| Windows(C#) | [TRTCMainForm.cs](https://github.com/tencentyun/TRTCSDK/blob/master/Windows/CSharpDemo/TRTCMainForm.cs) |


## 온라인 라이브 방송
### 1. SDK 초기화

TRTC SDK 사용의 첫 단계는 `TRTCCloud`의 단일 항목 객체를 획득하고, 리스너의 SDK 이벤트에 대한 콜백을 등록하는 것입니다.

- `ITRTCCloudCallback` 이벤트의 콜백 인터페이스 유형을 상속하여 로컬 사용자의 입장/퇴장 이벤트, 원격 사용자의 추가/퇴장 이벤트, 오류 이벤트, 경고 이벤트 등 중요한 이벤트의 콜백 인터페이스를 재작성합니다.
- `addCallback` 인터페이스를 호출하여 리스너 SDK 이벤트를 등록합니다.

>!`addCallback`이 N번 등록되면 동일한 이벤트의 SDK는 N번의 콜백을 트리거하므로, `addCallback`은 1회만 호출하기를 권장합니다.

<dx-codeblock>
::: C++ 버전 C++
// TRTCMainViewController.h

// ITRTCCloudCallback 이벤트를 상속하여 인터페이스 유형 콜백
class TRTCMainViewController : public ITRTCCloudCallback
{
public:
	TRTCMainViewController();
	virtual ~TRTCMainViewController();

    virtual void onError(TXLiteAVError errCode, const char* errMsg, void* arg);
    virtual void onWarning(TXLiteAVWarning warningCode, const char* warningMsg, void* arg);
    virtual void onEnterRoom(uint64_t elapsed);
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
::: C# 버전 C#
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
			// 리스너 SDK 이벤트 취소
			mTRTCCloud.removeCallback(this);
			// TRTCCloud 인스턴스 릴리스
			ITRTCCloud.destroyTRTCShareInstance();
			mTRTCCloud = null;
		}
		...
	}
	...
	// 오류 공지는 리스너가 필요하며, SDK가 계속해서 실행될 수 없음을 의미
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

TRTCParams는 SDK의 가장 중요한 매개변수로 sdkAppId, userId, userSig, roomId의 네 가지 필수 입력 필드가 있습니다.

- **SDKAppID**
Tencent Cloud TRTC [콘솔](https://console.cloud.tencent.com/rav)에 들어갑니다. 아직 애플리케이션이 없는 경우, 하나를 생성하면 곧바로 SDKAppID를 확인할 수 있습니다.

- **userId**
  자유롭게 지정할 수 있으며, 문자열 유형이기 때문에 기존의 계정 체계와 동일하게 입력할 수 있습니다. 단, **동일한 멀티미디어 방 안에 2개의 동일한 userId가 존재할 수 없습니다**.

- **userSig**
  SDKAppID와 userId를 기반으로 userSig를 계산할 수 있으며, 계산 방법은 [UserSig 계산 방법](https://intl.cloud.tencent.com/document/product/647/35166)을 참고하십시오.

- **roomId**
  방 번호는 숫자로 구성되어 있으며 자유롭게 지정할 수 있습니다. 단, **동일한 애플리케이션의 멀티미디어 룸 2개에 동일한 roomId를 할당할 수 없습니다**. 문자열 형식의 방 번호를 사용하려면 TRTCParams에서 strRoomId를 사용하십시오.

### 3. 호스트 미리보기 카메라 화면
TRTC SDK는 기본적으로 로컬 카메라 수집 기능이 비활성화되어 있습니다. `startLocalPreview`로 로컬 카메라를 활성화하고 미리보기 화면을 표시하며, `stopLocalPreview`는 비활성화됩니다.

로컬 미리보기를 실행하기 전, `setLocalViewFillMode` 호출을 통해 비디오 표시 모드를 `Fill` 또는 `Fit` 모드로 지정할 수 있습니다. 두 모드에서의 비디오 크기는 모두 동일한 비율로 축소/확대되며, 차이점은 다음과 같습니다.
- `Fill` 모드는 창 전체 화면을 우선으로 합니다. 축소/확대 후의 비디오 크기와 창의 화면 크기가 일치하지 않는 경우, 크기를 초과한 비디오의 나머지 부분을 잘라냅니다.
- `Fit` 모드는 비디오 콘텐츠 전체 표시를 우선으로 합니다. 축소/확대 후의 비디오 크기와 창 화면 크기가 일치하지 않는 경우, 채워지지 않은 비디오의 나머지 부분을 검은색으로 처리합니다.

<dx-codeblock>
::: C++ 버전 C++
void TRTCMainViewController::onEnterRoom(uint64_t elapsed)
{
	// 렌더링 창 핸들 가져오기.
    CWnd *pLocalVideoView = GetDlgItem(IDC_LOCAL_VIDEO_VIEW);
    HWND hwnd = pLocalVideoView->GetSafeHwnd();
    
    if(m_pTRTCSDK)
    {
        // SDK 인터페이스를 호출하여 렌더링 모드 및 렌더링 창 설정.
        m_pTRTCSDK->setLocalViewFillMode(TRTCVideoFillMode_Fit);
        m_pTRTCSDK->startLocalPreview(hwnd);
    }

}
:::
::: C# 버전 C#
// TRTCMainForm.cs
public void onEnterRoom(int result)
{
	...
	// 렌더링 창 핸들 가져오기.
	IntPtr ptr = GetHandle();
    if (mTRTCCloud != null)
    {
        // SDK 인터페이스를 호출하여 렌더링 모드 및 렌더링 창 설정.
        mTRTCCloud.setLocalViewFillMode(TRTCVideoFillMode_Fit);
        mTRTCCloud.startLocalPreview(ptr);
    }
	...
}
:::
</dx-codeblock>

### 4. 호스트의 마이크 음성 수집 기능 활성화

TRTC SDK는 기본적으로 로컬 마이크 음성 수집 기능이 비활성화되어 있습니다. 호스트는 `startLocalAudio`를 호출하여 로컬 음성 수집을 활성화하고 멀티미디어 데이터를 방송할 수 있으며, `stopLocalAudio`는 비활성화됩니다. `startLocalPreview` 이후 계속 `startLocalAudio`를 호출할 수 있습니다.

>?`startLocalAudio`는 마이크 사용 권한을 확인합니다. 마이크 사용 권한이 없는 경우 SDK는 사용자에게 활성화를 신청합니다.

### 5. 호스트의 신규 방 생성 및 방송 시작

호스트는 `enterRoom`을 사용해 멀티미디어 룸을 생성하고, 매개변수 `TRTCParams`의 `roomId`를 방 번호 지정에 사용할 수 있습니다. 또한 `role` 필드를 `TRTCRoleAnchor`로 지정해야 합니다(호스트).

`appScene` 매개변수는 SDK의 응용 시나리오를 지정합니다. 본 문서에서는 `TRTCAppSceneLIVE`(온라인 라이브 방송)을 사용합니다.

- 생성에 성공하면, SDK는 `onEnterRoom` 인터페이스를 콜백합니다. 매개변수: `elapsed`는 입장 소요 시간, 단위: ms.
- 생성에 실패하면, SDK는 `onError` 인터페이스를 콜백합니다. 매개변수: `errCode`(에러 코드 `ERR_ROOM_ENTER_FAIL`, 에러 코드는 `TXLiteAVCode.h` 참고), `errMsg`(오류 원인), `extraInfo`(매개변수 유지).

<dx-codeblock>
::: C++ 버전 C++
// TRTCMainViewController.cpp

void TRTCMainViewController::startBroadCasting()
{
    // TRTCParams 정의는 헤더 파일 TRTCCloudDef.h 참고
    TRTCParams params;
    params.sdkAppId = sdkappid;
    params.userId   = userid;
    params.userSig  = usersig;
    params.roomId   = 908; // 입장하고 싶은 방 입력
    params.role     = TRTCRoleAnchor; //호스트
    if(m_pTRTCSDK)
    {
    	m_pTRTCSDK->enterRoom(params, TRTCAppSceneLIVE);
    }
}

void TRTCMainViewController::onError(TXLiteAVError errCode, const char* errMsg, void* arg)
{
    if(errCode == ERR_ROOM_ENTER_FAIL)
    {
        LOGE(L"onError errorCode[%d], errorInfo[%s]", errCode, UTF82Wide(errMsg).c_str());
        // userSig 적합성 여부 및 네트워크 정상 여부 등 확인
    }
}

...

void TRTCMainViewController::onEnterRoom(uint64_t elapsed)
{
    LOGI(L"onEnterRoom elapsed[%lld]", elapsed);
    
	// 로컬 비디오 미리보기 실행은 아래 비디오 코딩 매개변수 설정과 로컬 카메라 화면 미리보기 콘텐츠를 참고하십시오.
}
:::
::: C# 버전 C#
// TRTCMainForm.cs

public void createRoom()
{
    // TRTCParams 정의는 헤더 파일 TRTCCloudDef.h 참고
    TRTCParams @params = new TRTCParams();
    @params.sdkAppId = sdkappid;
    @params.userId   = userid;
    @params.userSig  = usersig;
    @params.roomId   = 908; // 입장하고 싶은 방 입력
    @params.role     = TRTCRoleAnchor; //호스트
    if(mTRTCCloud != null)
    {
    	mTRTCCloud.enterRoom(@params, TRTCAppSceneLIVE);
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
    // 로컬 비디오 미리보기 실행은 아래 비디오 코딩 매개변수 설정과 로컬 카메라 화면 미리보기 콘텐츠를 참고하십시오.
}
:::
</dx-codeblock>

### 6. 호스트의 프라이버시 보호 모드 사용

라이브 방송 중 호스트가 프라이버시 보호를 목적으로 로컬 멀티미디어 데이터를 차단하고 싶은 경우, `muteLocalVideo`를 호출하여 로컬 비디오 수집을 차단할 수 있고, `muteLocalAudio`를 호출하여 로컬 음성 수집을 차단할 수 있습니다.

### 7. 시청자의 방 입장 후 시청

시청자는 `enterRoom`을 호출하여 멀티미디어 룸에 입장할 수 있습니다. 매개변수 RTCParams의 `roomId`를 방 번호 지정에 사용할 수 있습니다.
`appScene`도 동일하게 `TRTCAppSceneLIVE`(온라인 라이브 방송)를 입력합니다. 단, `role` 필드는 `TRTCRoleAudience`(시청자)로 지정되어야 합니다.

<dx-codeblock>
::: C++ 버전 C++
void TRTCMainViewController::startPlaying()
{
    // TRTCParams 정의는 헤더 파일 TRTCCloudDef.h 참고
    TRTCParams params;
    params.sdkAppId = sdkappid;
    params.userId   = userid;
    params.userSig  = usersig;
    params.roomId   = 908; // 입장하고 싶은 방 입력
    params.role     = TRTCRoleAudience; //시청자
    if(m_pTRTCSDK)
    {
    	m_pTRTCSDK->enterRoom(params, TRTCAppSceneLIVE);
    }
}
:::
::: C# 버전 C#
public void startPlaying()
{
    // TRTCParams 정의는 헤더 파일 TRTCCloudDef.h 참고
    TRTCParams @params = new TRTCParams();
    @params.sdkAppId = sdkappid;
    @params.userId   = userid;
    @params.userSig  = usersig;
    @params.roomId   = 908; // 입장하고 싶은 방 입력
    @params.role     = TRTCRoleAudience; //시청자
    if(mTRTCCloud != null)
    {
    	mTRTCCloud.enterRoom(@params, TRTCAppSceneLIVE);
    }
}
:::
</dx-codeblock>

호스트가 방에 있을 경우, 시청자는 TRTCCloudDelegate의 `onUserVideoAvailable` 콜백을 통해 호스트의 userid를 확인할 수 있습니다. 그 후, 시청자는 `startRemoteView`를 호출해 호스트의 비디오 화면을 볼 수 있습니다.

`setRemoteViewFillMode`를 통해 비디오 표시 모드를 `Fill` 또는 `Fit` 모드로 지정할 수 있습니다. 두 모드에서의 비디오 크기는 모두 동일한 비율로 축소/확대되며, 차이점은 다음과 같습니다.
- `Fill` 모드: 창 전체 화면을 우선으로 합니다. 축소/확대 후의 비디오 크기와 창의 화면 크기가 일치하지 않는 경우, 크기를 초과한 비디오의 나머지 부분을 잘라냅니다.
- `Fit` 모드: 비디오 콘텐츠 전체 표시를 우선으로 합니다. 축소/확대 후의 비디오 크기와 창의 화면 크기가 일치하지 않는 경우, 채워지지 않은 비디오의 나머지 부분을 검은색으로 처리합니다.

<dx-codeblock>
::: C++ 버전 C++
void TRTCMainViewController::onUserVideoAvailable(const char* userId, bool available){
    if (available)  {
        // 렌더링 창 핸들 가져오기
        CWnd *pRemoteVideoView = GetDlgItem(IDC_REMOTE_VIDEO_VIEW);
        HWND hwnd = pRemoteVideoView->GetSafeHwnd();  
        
        // 원격 사용자 비디오 렌더링 모드 설정.
        m_pTRTCSDK->setRemoteViewFillMode(TRTCVideoFillMode_Fill);
        // SDK 인터페이스를 호출하여 원격 사용자 스트림 재생.
        m_pTRTCSDK->startRemoteView(userId, hwnd);
    } else {
        m_pTRTCSDK->stopRemoteView(userId);
    }    
}
:::
::: C# 버전 C#
public void onUserVideoAvailable(string userId, bool available)
{
    if (available)
	{
		// 창 핸들 가져오기
		IntPtr ptr = GetHandleAndSetUserId(pos, userId, false);
		SetVisableInfoView(pos, false);
		// 원격 사용자 비디오 렌더링 모드 설정.
		mTRTCCloud.setRemoteViewFillMode(userId, TRTCVideoFillMode.TRTCVideoFillMode_Fit);
		// SDK 인터페이스를 호출하여 원격 사용자 스트림 재생.
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

>!
>- TRTCAppSceneLIVE 모드에서는 같은 방에 있는 시청자(TRTCRoleAudience) 인원 제한이 없습니다.
>- 각 엔드는 appScene에서 통일되어야 합니다. 그렇지 않으면 예기치 않은 문제가 발생할 수 있습니다.

### 8. 시청자와 호스트의 마이크 연결
호스트와 시청자 모두 TRTCCloud가 제공하는 `switchRole`을 통해 상호 역할 전환이 가능합니다. 가장 일반적인 시나리오는 시청자와 호스트의 마이크 연결입니다. 시청자는 해당 인터페이스를 통해 '보조 호스트'가 되고, 방의 기존 '메인 호스트'와 마이크를 연결해 인터랙션할 수 있습니다.

### 9. 방 퇴장
`exitRoom`을 호출하면 방에서 퇴장할 수 있습니다. 통화 중인 것과 상관 없이, 해당 방법을 호출하면 영상 통화와 관련된 모든 리소스를 릴리스합니다. `exitRoom`을 호출한 후, SDK는 복잡한 퇴장 핸드셰이크 프로세스에 들어가고, SDK가 `onExitRoom`을 콜백해야만 실제 리소스 릴리스가 완료됩니다.

<dx-codeblock>
::: C++ 버전 C++
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
	// 퇴장 성공, reason 매개변수 유지는 현재 미사용.

}
:::
::: C# 버전 C#
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
    // 퇴장 성공
    ...
}
:::
</dx-codeblock>
