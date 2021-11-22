## Overview
This document describes how to use the TRTC SDK to implement the simple video call feature. It covers only the most used APIs. To learn about other APIs, please see the [API documentation](https://intl.cloud.tencent.com/document/product/647/35119).


## Sample Code

| Platform | Sample Code |
|---------|---------|
| Windows (MFC) | [TRTCMainViewController.cpp](https://github.com/tencentyun/TRTCSDK/blob/master/Windows/MFCDemo/TRTCMainViewController.cpp) |
| Windows (Duilib) | [TRTCMainViewController.cpp](https://github.com/tencentyun/TRTCSDK/blob/master/Windows/DuilibDemo/TRTCMainViewController.cpp) |
| Windows (C#) | [TRTCMainForm.cs](https://github.com/tencentyun/TRTCSDK/blob/master/Windows/CSharpDemo/TRTCMainForm.cs) |

## Video Call
### 1. Initialize the SDK
To use the TRTC SDK, the first step is obtaining the `ITRTCCloud*` pointer to a singleton object of `TRTCCloud` through the export API `getTRTCShareInstance`, and subscribing to the SDK’s events.

- Inherit the `ITRTCCloudCallback` callback API class and rewrite the callback APIs for key events including room entry/exit by local user, room entry/exit by remote user, error event, and warning event.
- Call the `addCallback` API to subscribe to the SDK’s events.

>!If `addCallback` is called N times, the SDK will trigger N callbacks for the same event. Therefore, you are advised to call `addCallback` only once.

<dx-codeblock>
::: C++ C++
// TRTCMainViewController.h

// Inherit the `ITRTCCloudCallback` callback API class
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
::: C# C#
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

`TRTCParams` is the most critical parameter in the SDK. It contains four required fields: `SDKAppID`, `userId`, `userSig`, and `roomId`.

- **SDKAppID**
  Log in to the [TRTC console](https://console.cloud.tencent.com/rav). If you don't have an application yet, create one, and you will see its `SDKAppID`.
  
- **userId**
  A custom string, which you can keep in line with the naming of your account. Please note that **there cannot be users with identical `userId` in a room**.

- **userSig**
  Calculated based on `SDKAppID` and `userID`. For details, see [UserSig](https://intl.cloud.tencent.com/document/product/647/35166).

- **roomId**
  A custom number. Please note that **rooms under the same application cannot have identical `roomId`**. For string-type room ID, use `strRoomId` in `TRTCParams`.

### 3. Enter (or create) a room
Call `enterRoom` to enter the room specified by the `roomId` field in `TRTCParams`. If the room does not exist, the SDK will create one whose room number is the value of `roomId`.

The **appScene** parameter specifies the application scenario of the SDK. In this document, it is set to `TRTCAppSceneVideoCall` (video call). In this scenario, the codec and network components give a higher priority to ensuring video smoothness and reducing call latency and stutter.
				
- After calling the room entry API, you will receive the `onEnterRoom` callback. If `result` is greater than 0, room entry succeeds, and the value represents the time (ms) room entry takes; if `result` is less than 0, room entry fails, and the value is the error code for the failure.
- If room entry fails, you will also receive the `onError` callback, which contains `errCode` (error code, whose value is `ERR_ROOM_ENTER_FAIL`; for other error code values, please see `TXLiteAVCode.h`), `errMsg` (error message), and `extraInfo` (reserved parameter).
- If you are already in a room, you must call `exitRoom` to exit the room before entering another room. 

<dx-codeblock>
::: C++ C++
// TRTCMainViewController.cpp

void TRTCMainViewController::enterRoom()
{
    // For the definition of `TRTCParams`, please see the header file `TRTCCloudDef.h`.
    TRTCParams params;
    params.sdkAppId = sdkappid;
    params.userId   = userid;
    params.userSig  = usersig;
    params.roomId   = 908; // Set it to the ID of the room you want to enter
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
        // Check whether `userSig` is valid, network is normal, etc.
    }
}

...

void TRTCMainViewController::onEnterRoom(int result)
{
    LOGI(L"onEnterRoom result[%d]", result);
    if(result >= 0)
	{
		// Entered room successfully
	}
	else
	{
		// Failed to enter room. Error code = result;
	}
}
:::
::: C# C#
// TRTCMainForm.cs

public void EnterRoom()
{
    // For the definition of `TRTCParams`, please see the header file `TRTCCloudDef.h`.
    TRTCParams @params = new TRTCParams();
    @params.sdkAppId = sdkappid;
    @params.userId   = userid;
    @params.userSig  = usersig;
    @params.roomId   = 908; // Set it to the ID of the room you want to enter
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
        // Check whether `userSig` is valid, network is normal, etc.
    }
}

...

public void onEnterRoom(int result)
{
    if(result >= 0)
	{
		// Entered room successfully
	}
	else
	{
		// Failed to enter room. Error code = result;
	}
}
:::
</dx-codeblock>


>!
>- Set the `appScene` parameter according to your actual application scenario. Inappropriate `appScene` values may lead to increased stutter or decreased clarity.
>- The value of `appScene` must be the same on each client. Inconsistent `appScene` may cause unexpected problems.

### 4. Play remote audio streams
The TRTC SDK pulls remote audio streams by default, so there is no need for extra code. If you do not want to play the audio stream of a specified user (`userid`), you can mute it by calling `muteRemoteAudio`.

### 5. Play remote video streams

The TRTC SDK does not pull remote video streams by default. If a user is sending video data, other users in the room can get his or her `userid` through the `onUserVideoAvailable` callback in `ITRTCCloudCallback` and call `startRemoteView` to display the user’s video image.

Call `setRemoteViewFillMode` to set the video display mode to `Fill` or `Fit`. Video may be resized proportionally in both modes, but they differ in that:
- In the `Fill` mode, the image fills the entire screen. If the dimensions of the image do not match those of the screen after scaling, the excess parts are cropped.
- In the `Fit` mode, the image is displayed in whole. If the dimensions of the image do not match those of the screen after scaling, the blank area is filled with black bars.

<dx-codeblock>
::: C++ C++
// TRTCMainViewController.cpp
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
::: C# C#
// TRTCMainForm.cs
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


### 6. Enable/Disable local audio capturing

Mic capturing is disabled by default. Call `startLocalAudio` to enable local audio capturing and send the data captured, and `stopLocalAudio` to disable audio capturing.
>? You can call `startLocalAudio` after `startLocalPreview`.

### 7. Enable/Disable local video capturing

Camera capturing is disabled by default. You can call `startLocalPreview` to turn the local camera on and enable preview, and `stopLocalPreview` to disable camera capturing and preview.

- Call `startLocalPreview`, specifying the window for local video rendering. **The SDK dynamically detects window size and renders the video in the window represented by `rendHwnd`.**
- Call the `setLocalViewFillMode` API to set the local video rendering mode to `Fill` or `Fit`. In both modes, video may be resized proportionally, but they differ in that:
  - In the `Fill` mode, the image fills the entire screen. If the dimensions of the image do not match those of the screen after scaling, the parts that do not fit are cropped.
  - In the `Fit` mode, the image is displayed in whole. If the dimensions of the image do not match those of the screen after scaling, the unoccupied space is painted black.

<dx-codeblock>
::: C++ C++
// TRTCMainViewController.cpp

void TRTCMainViewController::onEnterRoom(uint64_t elapsed)
{
    ...
    
	// Get the handle of the rendering window
	CWnd *pLocalVideoView = GetDlgItem(IDC_LOCAL_VIDEO_VIEW);
	HWND hwnd = pLocalVideoView->GetSafeHwnd();
	
	if(m_pTRTCSDK)
	{
	    // Call the APIs below to set the rendering mode and rendering window
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


### 8. Block audio/video

- **Block local video data**
  Call `muteLocalVideo` to block local video data to other users in the room if you do not want them to see your video for privacy reasons.
  
- **Block local audio data**
  Call `muteLocalAudio` to block local audio data to other users in the room if you do not want them to hear your audio for privacy reasons.
  
- **Block remote video data**
  Call `stopRemoteView` to block the video data of a specified user (`userid`).
  Call `stopAllRemoteView` to block the video data of all remote users.
  
- **Block remote audio data**
  Call `muteRemoteAudio` to block the audio data of a specified user (`userid`).
  Call `muteAllRemoteAudio` to block the audio data of all remote users.

### 9. Exit the room

Call `exitRoom` to exit the room. Regardless of whether the call has ended, the SDK will release all resources used by the call.
>?After `exitRoom` is called, the SDK will start a complex handshake process, which finishes only after the `onExitRoom` callback is received.
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
	// Exited room successfully. `reason` is a reserved parameter and is not used for the time being.

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
    // Exited room successfully
    ...
}
:::
</dx-codeblock>

