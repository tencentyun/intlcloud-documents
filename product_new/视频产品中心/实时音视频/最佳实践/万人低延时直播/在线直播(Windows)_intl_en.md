## Overview
This document describes how to implement an online live broadcasting service that supports video co-anchoring and viewing by tens of thousands of concurrent viewers based on the TRTC SDK:
- This document only mentions the most basic features. If you want to learn more about advanced features, please see [Advanced Features](https://intl.cloud.tencent.com/document/product/647/35242).
- This document only lists the most commonly used APIs. If you want to learn more about API functions, please see the [API documentation](https://intl.cloud.tencent.com/zh/document/product/647/35119).

## Sample Code

| Platform | Sample Code | 
|---------|---------|
| Windows (MFC) | [TRTCMainViewController.cpp](https://github.com/tencentyun/TRTCSDK/blob/master/Windows/MFCDemo/TRTCMainViewController.cpp) |
| Windows (Duilib) | [TRTCMainViewController.cpp](https://github.com/tencentyun/TRTCSDK/blob/master/Windows/DuilibDemo/TRTCMainViewController.cpp) |
| Windows (C#) | [TRTCMainForm.cs](https://github.com/tencentyun/TRTCSDK/blob/master/Windows/CSharpDemo/TRTCMainForm.cs) |


## Live Broadcasting
### 1. Initialize the SDK

The first step in using the TRTC SDK is to get the singleton object of TRTCCloud and register a callback that listens on SDK events.

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
    virtual void onEnterRoom(uint64_t elapsed);
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
  `userSig` can be calculated based on `sdkAppId` and `userId`. For the calculation method, please see [How to Calculate UserSig](https://intl.cloud.tencent.com/document/product/647/35166).

- **roomId**
  The room number is of numeric type and can be specified arbitrarily; however, please note that **different audio/video rooms in the same application cannot have the same `roomId`**.

### 3. Anchor previews camera image
The TRTC SDK does not enable local camera capture by default. `startLocalPreview` can enable the local camera and display the preview image, while `stopLocalPreview` will disable the camera.

Before local preview is started, `setLocalViewFillMode` can be called to specify the video display mode as `Fill` or `Fit`. In both modes, the video size will be proportionally scaled. The difference is that the `Fill` mode gives priority to ensuring that the window is filled (i.e., if the size of the scaled video does not match the display window size, the excessive video part will be truncated), while the `Fit` mode gives priority to ensuring that all video content is displayed (i.e., if the size of the scaled video does not match the display window size, the excessive window part will be filled with black color blocks).

C++ edition:

```c++
void TRTCMainViewController::onEnterRoom(uint64_t elapsed)
{
	// Get the handle of the rendering window.
    CWnd *pLocalVideoView = GetDlgItem(IDC_LOCAL_VIDEO_VIEW);
    HWND hwnd = pLocalVideoView->GetSafeHwnd();
    
    if(m_pTRTCSDK)
    {
        // Call the SDK API to set the rendering mode and rendering window.
        m_pTRTCSDK->setLocalViewFillMode(TRTCVideoFillMode_Fit);
        m_pTRTCSDK->startLocalPreview(hwnd);
    }
    
}
```

C# edition:

```c#
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

### 4. Anchor enables mic capture

The TRTC SDK does not enable local mic capture by default. The anchor can call `startLocalAudio` to enable local sound capture and broadcast audio/video data, or call `stopLocalAudio` to disable sound capture. `startLocalAudio` can be called after `startLocalPreview`.

>`startLocalAudio` will check the mic permission. If there is no permission to use the mic, the SDK will ask the user to grant the permission.

### 5. Anchor creates a room and starts broadcasting

The anchor can use `enterRoom` to create an audio/video room. The `roomId` in the `TRTCParams` parameter is used to specify the room number. At the same time, the `role` field should be specified as `TRTCRoleAnchor` (anchor).

The `appScene` parameter specifies the application scenario of the SDK. In this document, `TRTCAppSceneLIVE` (online live broadcasting) is used as an example.

- If the creation is successful, the SDK will call back the `onEnterRoom` API. The `elapsed` parameter represents the time in ms it takes to enter the room.
- If the creation fails, the SDK will call back the `onError` API, which contains the following parameters: `errCode` (error code `ERR_ROOM_ENTER_FAIL`; for more information, please see `TXLiteAVCode.h`), `errMsg` (cause of error), and `extraInfo` (reserved parameter).

C++ edition:

```c++
// TRTCMainViewController.cpp

void TRTCMainViewController::startBroadCasting()
{
    // For the definition of `TRTCParams`, please see the `TRTCCloudDef.h` header file
    TRTCParams params;
    params.sdkAppId = sdkappid;
    params.userId   = userid;
    params.userSig  = usersig;
    params.roomId   = 908; // Enter the ID of the room you want to enter
    params.role     = TRTCRoleAnchor; // Anchor
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
    
	// Enable local video preview. For more information, please see the "video encoding parameter settings" and "local camera image preview" sections below
}
```

C# edition:

```c#
// TRTCMainForm.cs

public void createRoom()
{
    // For the definition of `TRTCParams`, please see the `TRTCCloudDef.h` header file
    TRTCParams @params = new TRTCParams();
    @params.sdkAppId = sdkappid;
    @params.userId   = userid;
    @params.userSig  = usersig;
    @params.roomId   = 908; // Enter the ID of the room you want to enter
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
    // Enable local video preview. For more information, please see the "video encoding parameter settings" and "local camera image preview" sections below
}
```

### 6. Anchor enables/disables privacy mode

During the live broadcasting, the anchor may want to block local audio/video data for privacy reason. To this end, `muteLocalVideo` and `muteLocalAudio` can be called to block local video and audio capture, respectively.

### 7. Viewer enters the room to view

The viewer can call `enterRoom` to enter the audio/video room. `roomId` in the `TRTCParams` parameter is used to specify the room number.
`appScene` also needs to be specified as `TRTCAppSceneLIVE` (online live broadcasting), but the `role` field needs to be specified as `TRTCRoleAudience` (viewer).

C++ edition:

```c++

void TRTCMainViewController::startPlaying()
{
    // For the definition of `TRTCParams`, please see the `TRTCCloudDef.h` header file
    TRTCParams params;
    params.sdkAppId = sdkappid;
    params.userId   = userid;
    params.userSig  = usersig;
    params.roomId   = 908; // Enter the ID of the room you want to enter
    params.role     = TRTCRoleAudience; // Viewer
    if(m_pTRTCSDK)
    {
    	m_pTRTCSDK->enterRoom(params, TRTCAppSceneLIVE);
    }
}
```

C# edition:

```c#
public void startPlaying()
{
    // For the definition of `TRTCParams`, please see the `TRTCCloudDef.h` header file
    TRTCParams @params = new TRTCParams();
    @params.sdkAppId = sdkappid;
    @params.userId   = userid;
    @params.userSig  = usersig;
    @params.roomId   = 908; // Enter the ID of the room you want to enter
    @params.role     = TRTCRoleAudience; // Viewer
    if(mTRTCCloud != null)
    {
    	mTRTCCloud.enterRoom(@params, TRTCAppSceneLIVE);
    }
}
```

If the anchor is in the room, the viewer will get the `userid` of the anchor through the `onUserVideoAvailable` callback in `TRTCCloudDelegate`. After that, the viewer can call the `startRemoteView` method to display the video image of the anchor.

`setRemoteViewFillMode` can be used to specify the video display mode as `Fill` or `Fit`. In both modes, the video size will be proportionally scaled. The difference lies in that:
- The `Fill` mode gives priority to ensuring that the window is filled (i.e., if the size of the scaled video does not match the display window size, the excessive video part will be truncated).
- The `Fit` mode gives priority to ensuring that all video content is displayed (i.e., if the size of the scaled video does not match the display window size, the excessive window part will be filled with black color blocks).

C++ edition:

```c++
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

> In `TRTCAppSceneLIVE` mode, there is no limit on the number of viewers (TRTCRoleAudience) in one single room.

### 8. Viewer co-anchors with anchor
Both the viewer and anchor can switch their roles through the `switchRole` API provided by TRTCCloud. The most common scenario is that the viewer co-anchors with the anchor: the viewer can call this API to turn themselves into an "assistant anchor" and co-anchor with the original "primary anchor" in the room.

### 9. Exit the room
Call the `exitRoom` method to exit the room. No matter whether or not a video call is currently in progress, calling this method will release all resources related to the video call. After `exitRoom` is called, the SDK will enter a complex exit handshake process, and the resources will be actually released only after the SDK calls back the `onExitRoom` method.

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
