## Overview
This document describes how to implement a simple video call feature based on the TRTC SDK:

- This document only mentions the most basic features. If you want to learn more about advanced features, please see [Advanced Features](https://intl.cloud.tencent.com/document/product/647/35242).
- This document only lists the most commonly used APIs. If you want to learn more about API functions, please see the [API documentation](https://intl.cloud.tencent.com/document/product/647/35123/32258).

## Sample Code

| Platform | Sample Code |
|---------|---------|
| Windows (MFC) | [TRTCMainViewController.cpp](https://github.com/tencentyun/TRTCSDK/blob/master/Windows/MFCDemo/TRTCMainViewController.cpp) |
| Windows (Duilib) | [TRTCMainViewController.cpp](https://github.com/tencentyun/TRTCSDK/blob/master/Windows/DuilibDemo/TRTCMainViewController.cpp) |
| Windows (C#) | [TRTCMainForm.cpp](https://github.com/tencentyun/TRTCSDK/blob/master/Windows/CSharpDemo/TRTCMainForm.cs) |

## Video Call
### 1. Initialize the SDK
The first step in using the TRTC SDK is to get the `ITRTCCloud*` pointer to the singleton object of TRTCCloud through the `getTRTCShareInstance` export API and register a callback that listens on SDK events.

- Inherit the `ITRTCCloudCallback` event callback API class and override the callback APIs for key events such as room entry/exit by local user, room entry/exit by remote user, error event, and warning event.
- Call the `addCallback` API to register and listen on SDK events.

>If `addCallback` is registered N times, the SDK will trigger N callbacks for the same event. It is recommended to call `addCallback` only once.

C++ edition:

```c++
// TRTCMainViewController.h

// Inherit the `ITRTCCloudCallback` event callback API class
class TRTCMainViewController : public ITRTCCloudCallback
{
public:
	TRTCMainViewController();
	virtual ~TRTCMainViewController();

    virtual void onError(TXLiteAVError errCode, const char* errMsg, void* arg);
    virtual void onWarning(TXLiteAVWarning warningCode, const char* warningMsg, void* arg);
    virtual void onEnterRoom(int result);
    virtual void onExitRoom(int reason);
    virtual void onUserEnter(const char* userId);
    virtual void onUserExit(const char* userId, int reason);
...
private:
	ITRTCCloud * m_pTRTCSDK = NULL；
...
}

// TRTCMainViewController.cpp

TRTCMainViewController::TRTCMainViewController()
{
    // Create a TRTCCloud instance
    m_pTRTCSDK = getTRTCShareInstance();
    
    // Register an SDK callback event
    m_pTRTCSDK->addCallback(this);
}

TRTCMainViewController::~TRTCMainViewController()
{
    // Cancel listening on the SDK event
    if(m_pTRTCSDK) {
        m_pTRTCSDK->removeCallback(this);
    }
    
    // Release the TRTCCloud instance
	  if(m_pTRTCSDK != NULL) {
       destroyTRTCShareInstance();
        m_pTRTCSDK = null;
    }
}

// Error notifications should be listened on, as they indicate that the SDK cannot continue to run
virtual void TRTCMainViewController::onError(TXLiteAVError errCode, const char* errMsg, void* arg)
{
    if (errCode == ERR_ROOM_ENTER_FAIL) {
        LOGE(L"onError errorCode[%d], errorInfo[%s]", errCode, UTF82Wide(errMsg).c_str());
		    exitRoom();
	 }
}
```

C# edition:

```c#
// TRTCMainForm.cs

// Inherit the `ITRTCCloudCallback` event callback API class
public partial class TRTCMainForm : Form, ITRTCCloudCallback, ITRTCLogCallback
{
	...
	private ITRTCCloud mTRTCCloud; 
	...
	
	public TRTCMainForm(TRTCLoginForm loginForm)
    {
    	InitializeComponent();
    	this.Disposed += new EventHandler(OnDisposed);
    	// Create a TRTCCloud instance
    	mTRTCCloud = ITRTCCloud.getTRTCShareInstance();
    	// Register an SDK callback event
    	mTRTCCloud.addCallback(this);
    	...
    }
    
    private void OnDisposed(object sender, EventArgs e)
    {
    	if (mTRTCCloud != null)
    	{
    		// Cancel listening on the SDK event
    		mTRTCCloud.removeCallback(this);
    		// Release the TRTCCloud instance
    		ITRTCCloud.destroyTRTCShareInstance();
    		mTRTCCloud = null;
    	}
    	...
    }
    ...
    // Error notifications should be listened on, as they indicate that the SDK cannot continue to run
    public void onError(TXLiteAVError errCode, string errMsg, IntPtr arg)
    {
         if (errCode == TXLiteAVError.ERR_ROOM_ENTER_FAIL) {
		    exitRoom();
		}
         ...
    }
    ...
}
```

### 2. Assemble `TRTCParams`

`TRTCParams` is the most critical parameter in the SDK. It contains the following four required fields: `sdkAppId`, `userId`, `userSig`, and `roomId`.

- **sdkAppId**
  Log in to the [TRTC Console](https://console.cloud.tencent.com/rav). If you don't have an application yet, please create one and you will see the `sdkAppId`.

- **userId**
  It can be specified arbitrarily. As it is of string type, it can be directly in line with your existing account system; however, please note that **there should not be identical `userIds` in the same audio/video room**.

- **userSig**
  `userSig` can be calculated based on `sdkAppId` and `userId`. For the calculation method, please see [How to Generate UserSig](https://intl.cloud.tencent.com/document/product/647/35166).

- **roomId**
  The room number is of numeric type and can be specified arbitrarily; however, please note that **different audio/video rooms in the same application cannot have the same `roomId`**.

### 3. Enter (or create) a room
Call `enterRoom` to enter the audio/video room specified by `roomId` in the `TRTCParams` parameter. If the room does not exist, the SDK will automatically create it with the `roomId` as the room number.

The **appScene** parameter specifies the application scenario of the SDK, which is `TRTCAppSceneVideoCall` (video call) in this document. In this scenario, the SDK's internal codec and network component focus more on video smoothness to reduce call latency and lagging.
				
- If the room entry succeeds, the SDK will call back the `onEnterRoom` API. Parameters: when `result` is greater than 0, the room entry succeeds, and the value indicates the time in milliseconds (ms) used for entering the room; when `result` is less than 0, the room entry fails, and the value indicates the error code of the failure.
- If the room entry fails, the SDK will also call back the `onError` API, which contains the following parameters: `errCode` (error code `ERR_ROOM_ENTER_FAIL`; for more information, please see `TXLiteAVCode.h`), `errMsg` (cause of error), and `extraInfo` (reserved parameter).
- If you are already in the room, you must call the `exitRoom` method to exit the current room before entering the next room. 

C++ edition:

```c++
// TRTCMainViewController.cpp

void TRTCMainViewController::enterRoom()
{
    // For the definition of `TRTCParams`, please see the `TRTCCloudDef.h` header file
    TRTCParams params;
    params.sdkAppId = sdkappid;
    params.userId   = userid;
    params.userSig  = usersig;
    params.roomId   = 908; // Enter the ID of the room you want to enter
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
		//The user successfully enters the room
	}
	else
	{
		// Failed to enter the room. Error code = result;
	}
}
```

C# edition:

```c#
// TRTCMainForm.cs

public void EnterRoom()
{
    // For the definition of `TRTCParams`, please see the `TRTCCloudDef.h` header file
    TRTCParams @params = new TRTCParams();
    @params.sdkAppId = sdkappid;
    @params.userId   = userid;
    @params.userSig  = usersig;
    @params.roomId   = 908; // Enter the ID of the room you want to enter
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
		//The user successfully enters the room
	}
	else
	{
		// Failed to enter the room. Error code = result;
	}
}
```

>Please select the appropriate `scene` parameter according to the actual application scenario. An incorrect selection may lead to higher lagging rate or lower video definition than expected.

### 4. Listen to remote audio stream
The TRTC SDK receives remote audio streams by default, so you don't need to write extra code for this. If you don't want to listen to the audio stream of a certain `userid`, you can mute it by calling `muteRemoteAudio`.

### 5. Watch remote video stream

The TRTC SDK does not pull remote video streams by default. When there is a user upstreaming video data in the room, other users in the room can get the `userid` of the user through the `onUserVideoAvailable` callback in `ITRTCCloudCallback`. After that, they can call the `startRemoteView` method to display the video image of the user.

`setRemoteViewFillMode` can be used to specify the video display mode as `Fill` or `Fit`. In both modes, the video size will be proportionally scaled. The difference lies in that:
- The `Fill` mode gives priority to ensuring that the window is filled (i.e., if the size of the scaled video does not match the display window size, the excessive video part will be truncated).
- The `Fit` mode gives priority to ensuring that all video content is displayed (i.e., if the size of the scaled video does not match the display window size, the excessive window part will be filled with black color blocks).

C++ edition:

```c++
// TRTCMainViewController.cpp
void TRTCMainViewController::onUserVideoAvailable(const char* userId, bool available){
    if (available) {
        // Get the handle of the rendering window.
        CWnd *pRemoteVideoView = GetDlgItem(IDC_REMOTE_VIDEO_VIEW);
        HWND hwnd = pRemoteVideoView->GetSafeHwnd();  
        
        // Set rendering mode of the remote user's video.
        m_pTRTCSDK->setRemoteViewFillMode(TRTCVideoFillMode_Fill);
        // Call the SDK API to play back the remote user's stream.
        m_pTRTCSDK->startRemoteView(userId， hwnd);
    } else {
        m_pTRTCSDK->stopRemoteView(userId);
    }    
}
```

C# edition:

```c#
// TRTCMainForm.cs
public void onUserVideoAvailable(string userId, bool available)
{
    if (available)
	{
		// Get the window handle.
		IntPtr ptr = GetHandleAndSetUserId(pos, userId, false);
		SetVisableInfoView(pos, false);
		// Set rendering mode of the remote user's video.
		mTRTCCloud.setRemoteViewFillMode(userId, TRTCVideoFillMode.TRTCVideoFillMode_Fit);
		// Call the SDK API to play back the remote user's stream.
		mTRTCCloud.startRemoteView(userId, ptr);
	}
	else
	{
		mTRTCCloud.stopRemoteView(userId);
		...
	}
}
```

### 6. Enable/disable local sound capture

The TRTC SDK does not enable local mic capture by default. `startLocalAudio` can be called to enable local sound capture and broadcast audio/video data, while `stopLocalAudio` can disable sound capture.
>`startLocalAudio` can be called after `startLocalPreview`.

### 7. Enable/disable local video capture

The TRTC SDK does not enable local camera capture by default. `startLocalPreview` can enable the local camera and display the preview image, while `stopLocalPreview` will disable the camera.

- Call the `startLocalPreview` API to specify the window for local video rendering. **Note: the SDK dynamically detects the window size and renders the video in the entire window represented by `rendHwnd`.**
- Call the `setLocalViewFillMode` API to set the local video rendering mode to `Fill` or `Fit`. In both modes, the video size will be proportionally scaled. The difference lies in that:
  - The `Fill` mode gives priority to ensuring that the window is filled (i.e., if the size of the scaled video does not match the window size, the excessive video part will be truncated).
  - The `Fit` mode gives priority to ensuring that all video content is displayed (i.e., if the size of the scaled video does not match the window size, the excessive window part will be filled with black color blocks).

C++ edition:

```c++
// TRTCMainViewController.cpp

void TRTCMainViewController::onEnterRoom(uint64_t elapsed)
{
    ...
    
	// Get the handle of the rendering window.
    CWnd *pLocalVideoView = GetDlgItem(IDC_LOCAL_VIDEO_VIEW);
    HWND hwnd = pLocalVideoView->GetSafeHwnd();
    
    if(m_pTRTCSDK)
    {
        // Call the SDK API to set the rendering mode and rendering window.
        m_pTRTCSDK->setLocalViewFillMode(TRTCVideoFillMode_Fit);
        m_pTRTCSDK->startLocalPreview(hwnd);
    }
    
	...
}
```

C# edition:

``` c#
// TRTCMainForm.cs

public void onEnterRoom(int result)
{
	...
	// Get the handle of the rendering window.
	IntPtr ptr = GetHandle();
    if (mTRTCCloud != null)
    {
        // Call the SDK API to set the rendering mode and rendering window.
        mTRTCCloud.setLocalViewFillMode(TRTCVideoFillMode_Fit);
        mTRTCCloud.startLocalPreview(ptr);
    }
	...
}
```

### 8. Block audio/video data stream

- **Block local video data**
  If the user wants to block local video data for privacy reason during the call, so that other users in the room cannot temporarily view their video image, `muteLocalVideo` can be called to this end.
  
- **Block local audio data**
  If the user wants to block local audio data for privacy reason during the call, so that other users in the room cannot temporarily hear their sound, `muteLocalAudio` can be called to this end.
  
- **Block remote video data**
  `stopRemoteView` can be called to block the video data of a certain `userid`.
  `stopAllRemoteView` can be called to block the video data of all remote users.
  
- **Block remote audio data**
  `muteRemoteAudio` can be called to block the audio data of a certain `userid`.
  `muteAllRemoteAudio` can be called to block the audio data of all remote users.

### 9. Exit the room

Call the `exitRoom` method to exit the room. No matter whether or not a video call is currently in progress, calling this method will release all resources related to the video call.
>After `exitRoom` is called, the SDK will enter a complex exit handshake process, and the resources will be actually released only after the SDK calls back the `onExitRoom` method.

C++ edition:

```c++
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
	// Exited room successfully. The `reason` parameter is reserved and not used for now.

    ...
}
```

C# edition:

```c#
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
```

