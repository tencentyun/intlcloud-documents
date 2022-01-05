## Overview
This document describes how to use the TRTC SDK to build a live streaming service that supports both co-anchoring and high-concurrency streaming to over 10,000 users. Only the most commonly used APIs are covered in this document. To learn about other APIs, please see the [API documentation](https://intl.cloud.tencent.com/document/product/647/35119).


## Sample Code

| Platform | Sample Code |
|---------|---------|
| Windows (MFC) | [TRTCMainViewController.cpp](https://github.com/tencentyun/TRTCSDK/blob/master/Windows/MFCDemo/TRTCMainViewController.cpp) |
| Windows (Duilib) | [TRTCMainViewController.cpp](https://github.com/tencentyun/TRTCSDK/blob/master/Windows/DuilibDemo/TRTCMainViewController.cpp) |
| Windows (C#) | [TRTCMainForm.cs](https://github.com/tencentyun/TRTCSDK/blob/master/Windows/CSharpDemo/TRTCMainForm.cs) |


## Online Live Streaming
### 1. Initialize the SDK

The first step is to get a singleton object of `TRTCCloud` and subscribe to the SDK’s event callbacks.

- Inherit the `ITRTCCloudCallback` callback API class and rewrite the callback APIs for key events including room entry/exit by local user, room entry/exit by remote user, error event, and warning event.
- Call the `addCallback` API to subscribe to the SDK’s events.

>!If `addCallback` is called N times, the SDK will trigger N callbacks for the same event. Therefore, you are advised to call `addCallback` only once.

<dx-codeblock>
::: C++
// TRTCMainViewController.h

// Inherit the `ITRTCCloudCallback` callback API class
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
    // Create a `TRTCCloud` instance
    m_pTRTCSDK = getTRTCShareInstance();
    
    // Subscribe to the SDK’s events
    m_pTRTCSDK->addCallback(this);
}

TRTCMainViewController::~TRTCMainViewController()
{
    // Unsubscribe from the SDK’s events
    if(m_pTRTCSDK) {
        m_pTRTCSDK->removeCallback(this);
    }
    
    // Release the `TRTCCloud` instance
      if(m_pTRTCSDK != NULL) {
       destroyTRTCShareInstance();
        m_pTRTCSDK = null;
    }
}

// Error notifications indicate that the SDK has stopped working and therefore must be listened for.
virtual void TRTCMainViewController::onError(TXLiteAVError errCode, const char* errMsg, void* arg)
{
    if (errCode == ERR_ROOM_ENTER_FAIL) {
        LOGE(L"onError errorCode[%d], errorInfo[%s]", errCode, UTF82Wide(errMsg).c_str());
		    exitRoom();
	 }
}
:::
::: C#
// TRTCMainForm.cs

// Inherit the `ITRTCCloudCallback` callback API class
public partial class TRTCMainForm : Form, ITRTCCloudCallback, ITRTCLogCallback
{
	...
	private ITRTCCloud mTRTCCloud; 
	...
	
	public TRTCMainForm(TRTCLoginForm loginForm)
	{
		InitializeComponent();
		this.Disposed += new EventHandler(OnDisposed);
		// Create a `TRTCCloud` instance
		mTRTCCloud = ITRTCCloud.getTRTCShareInstance();
		// Subscribe to the SDK’s events
		mTRTCCloud.addCallback(this);
		...
	}
	
	private void OnDisposed(object sender, EventArgs e)
	{
		if (mTRTCCloud != null)
		{
			// Unsubscribe from the SDK’s events
			mTRTCCloud.removeCallback(this);
			// Release the `TRTCCloud` instance
			ITRTCCloud.destroyTRTCShareInstance();
			mTRTCCloud = null;
		}
		...
	}
	...
	// Error notifications indicate that the SDK has stopped working and therefore must be listened for.
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

### 2. Assemble `TRTCParams`

`TRTCParams` is the most critical parameter in the SDK. It contains four required fields: `sdkAppId`, `userId`, `userSig`, and `roomId`.

- **SDKAppID**
Log in to the [TRTC console](https://console.cloud.tencent.com/rav). If you don't have an application yet, create one, and you will see its `SDKAppID`.

- **userId**
  A custom string, which you can keep in line with the naming of your account. Please note that **there cannot be users with identical `userId` in a room**.

- **userSig**
  Calculated based on `SDKAppID` and `userID`. For details, see [UserSig](https://intl.cloud.tencent.com/document/product/647/35166).

- **roomId**
  A custom number. Note that **you cannot assign the same `roomId` to two rooms under the same application**. For string-type room ID, use `strRoomId` in `TRTCParams`.

### 3. Enable preview of the local camera
Camera capturing is disabled by default. You can call `startLocalPreview` to turn the local camera on and enable preview, and `stopLocalPreview` to disable camera capturing and preview.

Before enabling preview of the local camera, you can call `setLocalViewFillMode` to set the video display mode to `Fill` or `Fit`. Video may be resized proportionally in both modes, but they differ in that:
- In the `Fill` mode, the image fills the entire screen. If the dimensions of the image do not match those of the screen after scaling, the parts that do not fit are cropped.
- In the `Fit` mode, the image is displayed in whole. If the dimensions of the image do not match those of the screen after scaling, the unoccupied space is painted black.

<dx-codeblock>
::: C++
void TRTCMainViewController::onEnterRoom(uint64_t elapsed)
{
	// Get the handle of the rendering window
    CWnd *pLocalVideoView = GetDlgItem(IDC_LOCAL_VIDEO_VIEW);
    HWND hwnd = pLocalVideoView->GetSafeHwnd();
    
    if(m_pTRTCSDK)
    {
        // Call the APIs below to set the rendering mode and rendering window
        m_pTRTCSDK->setLocalViewFillMode(TRTCVideoFillMode_Fit);
        m_pTRTCSDK->startLocalPreview(hwnd);
    }

}
:::
::: C#
// TRTCMainForm.cs
public void onEnterRoom(int result)
{
	...
	// Get the handle of the rendering window
	IntPtr ptr = GetHandle();
    if (mTRTCCloud != null)
    {
        // Call the APIs below to set the rendering mode and rendering window
        mTRTCCloud.setLocalViewFillMode(TRTCVideoFillMode_Fit);
        mTRTCCloud.startLocalPreview(ptr);
    }
	...
}
:::
</dx-codeblock>

### 4. Enable mic capturing

Mic capturing is disabled by default. Call `startLocalAudio` to enable local audio capturing and send the data captured, and `stopLocalAudio` to disable audio capturing. You can call `startLocalAudio` after `startLocalPreview`.

>? After you call `startLocalAudio`, the SDK will check mic access and will ask for mic permission from the user if it does not have access.

### 5. Create a room and push streams

Call `enterRoom` to create a room, setting `role` to `TRTCRoleAnchor` (anchor) and specifying `roomId` in the `TRTCParams` parameter.

Specify `appScene`, which indicates the application scenario. `TRTCAppSceneLIVE` (online live streaming) is used in the example of this document.

- If the room is created successfully, you will receive the `onEnterRoom` callback, in which the `elapsed` field represents the time (ms) room entry takes.
- If room creation fails, you will receive the `onError` callback, which contains `errCode` (error code, whose value is `ERR_ROOM_ENTER_FAIL`; for other error code values, please see `TXLiteAVCode.h`), `errMsg` (error message), and `extraInfo` (reserved parameter).

<dx-codeblock>
::: C++
// TRTCMainViewController.cpp

void TRTCMainViewController::startBroadCasting()
{
    // For the definition of `TRTCParams`, please see the header file `TRTCCloudDef.h`.
    TRTCParams params;
    params.sdkAppId = sdkappid;
    params.userId   = userid;
    params.userSig  = usersig;
    params.roomId   = 908; // Set it to the ID of the room you want to enter
    params.role     = TRTCRoleAnchor; //Anchor
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
        // Check whether `userSig` is valid, network is normal, etc.
    }
}

...

void TRTCMainViewController::onEnterRoom(uint64_t elapsed)
{
    LOGI(L"onEnterRoom elapsed[%lld]", elapsed);
    
	// Enable local video preview. For details, please see the sections below about encoding settings and local video preview
}
:::
::: C#
// TRTCMainForm.cs

public void createRoom()
{
    // For the definition of `TRTCParams`, please see the `TRTCCloudDef.h` header file
    TRTCParams @params = new TRTCParams();
    @params.sdkAppId = sdkappid;
    @params.userId   = userid;
    @params.userSig  = usersig;
    @params.roomId   = 908; // Set it to the ID of the room you want to enter
    @params.role     = TRTCRoleAnchor; // Anchor
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
        // Check whether `userSig` is valid, network is normal, etc.
    }
}

...

public void onEnterRoom(int result)
{
    // Enable local video preview. For details, please see the sections below about encoding settings and local video preview
}
:::
</dx-codeblock>

### 6. Enable/Disable the privacy mode

At some points during a live stream, you may not want to publish your video or audio for privacy concerns. You can call `muteLocalVideo` to stop publishing local video and `muteLocalAudio` to stop publishing local audio.

### 7. Enter the room as audience

Call `enterRoom` to enter the room, specifying the room number via the `roomId` field in `TRTCParams`.
Set `appScene` to `TRTCAppSceneLIVE` (online live streaming), and `role` to `TRTCRoleAudience` (audience).

<dx-codeblock>
::: C++
void TRTCMainViewController::startPlaying()
{
    // For the definition of `TRTCParams`, please see the header file `TRTCCloudDef.h`.
    TRTCParams params;
    params.sdkAppId = sdkappid;
    params.userId   = userid;
    params.userSig  = usersig;
    params.roomId   = 908; // Set it to the ID of the room you want to enter
    params.role     = TRTCRoleAudience; // Viewer
    if(m_pTRTCSDK)
    {
    	m_pTRTCSDK->enterRoom(params, TRTCAppSceneLIVE);
    }
}
:::
::: C#
public void startPlaying()
{
    // For the definition of `TRTCParams`, please see the `TRTCCloudDef.h` header file
    TRTCParams @params = new TRTCParams();
    @params.sdkAppId = sdkappid;
    @params.userId   = userid;
    @params.userSig  = usersig;
    @params.roomId   = 908; // Set it to the ID of the room you want to enter
    @params.role     = TRTCRoleAudience; // Viewer
    if(mTRTCCloud != null)
    {
    	mTRTCCloud.enterRoom(@params, TRTCAppSceneLIVE);
    }
}
:::
</dx-codeblock>

If the anchor is in the room, you can find the anchor’s `userid` in the `onUserVideoAvailable` callback in `TRTCCloudDelegate`, and then call `startRemoteView` to display the anchor’s video.

Call `setRemoteViewFillMode` to set the video display mode to `Fill` or `Fit`. Video may be resized proportionally in both modes, but they differ in that:
- In the `Fill` mode, the image fills the entire screen. If the dimensions of the image do not match those of the screen after scaling, the excess parts are cropped.
- In the `Fit` mode, the image is displayed in whole. If the dimensions of the image do not match those of the screen after scaling, the blank area is filled with black bars.

<dx-codeblock>
::: C++
void TRTCMainViewController::onUserVideoAvailable(const char* userId, bool available){
    if (available) {
        // Get the handle of the rendering window
        CWnd *pRemoteVideoView = GetDlgItem(IDC_REMOTE_VIDEO_VIEW);
        HWND hwnd = pRemoteVideoView->GetSafeHwnd();  
        
        // Set the rendering mode of the remote video
        m_pTRTCSDK->setRemoteViewFillMode(TRTCVideoFillMode_Fill);
        // Call the API below to play the remote video
        m_pTRTCSDK->startRemoteView(userId, hwnd);
    } else {
        m_pTRTCSDK->stopRemoteView(userId);
    }    
}
:::
::: C#
public void onUserVideoAvailable(string userId, bool available)
{
    if (available)
	{
		// Get the window handle
		IntPtr ptr = GetHandleAndSetUserId(pos, userId, false);
		SetVisableInfoView(pos, false);
		// Set the rendering mode of the remote video
		mTRTCCloud.setRemoteViewFillMode(userId, TRTCVideoFillMode.TRTCVideoFillMode_Fit);
		// Call the API below to play the remote video
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
>- In the `TRTCAppSceneLIVE` mode, there is no limit on the number of users in the role of “audience” (`TRTCRoleAudience`) in a room.
>- The value of `appScene` must be the same on each client. Inconsistent `appScene` may cause unexpected problems.

### 8. Co-anchor
Both audience and anchors can call the `switchRole` API of `TRTCCloud` to switch their roles. The most common application for the API is co-anchoring: audience call this API to switch their role to “anchor” so as to interact with the room owner.

### 9. Exit the room
Call `exitRoom` to exit the room. Whether the live streaming has ended or not, the SDK will start a complex handshake process where it releases all resources used by the live streaming. The process finishes only after you receive the `onExitRoom` callback.

<dx-codeblock>
::: C++
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
	// Exited room successfully. `reason` is a reserved parameter and is not used for the time being.

}
:::
::: C#
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
    // Exited room successfully
    ...
}
:::
</dx-codeblock>
