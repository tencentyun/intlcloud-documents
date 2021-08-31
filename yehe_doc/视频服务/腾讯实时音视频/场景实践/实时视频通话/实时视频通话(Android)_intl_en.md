## Effect Demo

To quickly implement the video call feature, you can directly modify the demo provided by TRTC for adaptation or use the provided `TRTCCalling` component and implement custom UI.

>! Previously we offered `TRTCVideoCall` component, which was moved to the [Component Repository](https://github.com/tencentyun/LiteAVClassic). We now provide `TRTCCalling` component which uses IM signaling API and is not compatible with the previous version.

<span id="ui"> </span>

## Reusing Demo UI

<span id="ui.step1"></span>

### Step 1. Create an application

1. Log in to the TRTC Console and select **Development Assistance** > **[Demo Quick Run](https://console.cloud.tencent.com/trtc/quickstart)**.
2. Click **Start Now**, enter the application name such as `TestVideoCall`, and click **Create Application**.

>! This feature uses two basic PaaS services of Tencent Cloud, namely, [TRTC](https://intl.cloud.tencent.com/document/product/647/35078) and [IM](https://intl.cloud.tencent.com/document/product/1047). When TRTC is activated, IM will be activated automatically.IM is a value-added service at the prices as detailed in [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350).

<span id="ui.step2"></span>

### Step 2. Download the SDK and demo source code

1. Mouse over the corresponding block, click **[GitHub](https://github.com/tencentyun/TRTCSDK/tree/master/Android)** to enter GitHub (or click **[ZIP](https://liteavsdk-1252463788.cosgz.myqcloud.com/TXLiteAVSDK_TRTC_Android_latest.zip)**), and download the relevant SDK and supporting demo source code.
   ![](https://main.qcloudimg.com/raw/b0f6f1bd5e0bc083bafddcc7c04a1593.png)
2. After the download is completed, return to the TRTC Console and click **Downloaded and Next**. Then, you can see the `SDKAppID` and key information.

<span id="ui.step3"></span>

### Step 3. Configure demo project files

1. Decompress the source package downloaded in [step 2](#ui.step2).
2. Find and open the `Android/TRTCScenesDemo/debug/src/main/java/com/tencent/liteav/debug/GenerateTestUserSig.java` file.
3. Set the relevant parameters in the `GenerateTestUserSig.java` file:
	- SDKAPPID: it is 0 by default. Please replace it with the real `SDKAppID`.
	- SECRETKEY: it is an empty string by default. Please replace it with the real key information.
![](https://main.qcloudimg.com/raw/87dc814a675692e76145d76aab91b414.png)
4. Return to the TRTC Console and click **Pasted and Next**.
5. Click **Close Guide and Log in to the Console to Manage the Application**.

>!
>- In this document, the `SECRETKEY` is configured in the client code to obtain `UserSig`. The `SECRETKEY` is easily decompiled and reverse cracked. If the `SECRETKEY` is leaked, hackers can steal your Tencent Cloud traffic. Therefore, **this method only applies to locally running a demo project and commissioning features**.
>- The correct `UserSig` distribution method is to integrate the calculation code of `UserSig` into your server and provide an application-oriented API. When `UserSig` is needed, your application can make a request to the business server for dynamic `UserSig`. For more information, please see [How to Calculate UserSig](https://intl.cloud.tencent.com/document/product/647/35166#Server).

<span id="ui.step4"></span>

### Step 4. Run the demo

Use Android Studio (v3.5 or above) to open the `TRTCDemo` project and click **Run** to debug the demo.

<span id="ui.step5"></span>

### Step 5. Modify the demo source code

The source code folder `trtccallingdemo` contains two subfolders: `ui` and `model`. The `ui` folder contains the UI code:

| File or Folder                     | Description                                                     |
| -------------------------------- | ------------------------------------------------------------ |
| TRTCVideoCallActivity.java | Video call homepage where calls can be answered or rejected. |
| TRTCCallingEntranceActivity.java | It is used to show the interface for selecting contacts. You can search for registered users to initiate calls on this UI. |
| videolayout                      | Video image rendering and layout logic                       |

<span id="model"> </span>

## Implementing Custom UI

The [source code] folder `trtccallingdemo` contains two subfolders: `ui` and `model`. The `model` folder contains the implemented reusable open-source component `TRTCCalling`. You can find the API functions provided by this component in the `TRTCCalling.java` file.
![](https://main.qcloudimg.com/raw/9b4087b68541912ce9e7a48955cd48e8.png)

You can use the open-source component `TRTCCalling` to implement your own UI, i.e., only reusing the `model` to implement your custom UI.

<span id="model.step1"> </span>

### Step 1. Integrate the SDK

The audio/video call component `TRTCCalling` depends on the TRTC SDK and IM SDK. You can integrate the two SDKs into your project in the following steps:

**Method 1. Implement dependency through Maven repository**

1. Add the TRTC SDK and IM SDK dependencies to `dependencies`.
```
dependencies {
  complie "com.tencent.liteav:LiteAVSDK_TRTC:latest.release"
    complie 'com.tencent.imsdk:imsdk:latest.release'

  // As Gson parsing is used, Google's Gson needs to be depended on
    complie 'com.google.code.gson:gson:latest.release'
}
```
>?You can get the latest version numbers of the two SDKs on the [TRTC](https://github.com/tencentyun/TRTCSDK) and [IM](https://github.com/tencentyun/TIMSDK) homepages on GitHub.

2. In `defaultConfig`, specify the CPU architecture to be used by the application.
```
defaultConfig {
    ndk {
        abiFilters "armeabi-v7a"
    }
}
```
3. Click **Sync Now** to sync the SDK.
>?If JCenter can be connected to, the SDK will be automatically downloaded and integrated into the project.


**Method 2. Implement dependency through local AAR files**
If the access to the Maven repository is slow in your development environment, you can download the ZIP packages and manually integrate the SDKs into your project as instructed in the integration document.

| SDK      | Download Page                                                     | Integration Guide                                                     |
| -------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| TRTC SDK | [Download](https://intl.cloud.tencent.com/document/product/647/34615) | [Integration Documentation](https://intl.cloud.tencent.com/document/product/647/35093) |
| IM SDK | [Download](https://intl.cloud.tencent.com/document/product/1047/33996) | [Integration Documentation](https://intl.cloud.tencent.com/document/product/1047/34306) |

<span id="model.step2"> </span>

### Step 2. Configure permissions and obfuscation rules

Configure application permissions in `AndroidManifest.xml`. The SDK requires the following permissions (on Android 6.0 and above, the camera and storage read permissions need to be requested at runtime):

```
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.RECORD_AUDIO" />
<uses-permission android:name="android.permission.MODIFY_AUDIO_SETTINGS" />
<uses-permission android:name="android.permission.BLUETOOTH" />
<uses-permission android:name="android.permission.CAMERA" />
<uses-permission android:name="android.permission.READ_PHONE_STATE" />
<uses-feature android:name="android.hardware.camera"/>
<uses-feature android:name="android.hardware.camera.autofocus" />
```

In the `proguard-rules.pro` file, add the classes related to the SDK to the "do not obfuscate" list:

```
-keep class com.tencent.** { *; }
```

<span id="model.step3"> </span>

### Step 3. Import the TRTCCalling component

Copy all files in the following directory to your project:

```
trtccallingdemo/src/main/java/com/tencent/liteav/trtccalling/model 
```

<span id="model.step4"> </span>

### Step 4. Initialize and log in to the component

1. Call `TRTCCallingImpl.sharedInstance(context)` to get the component instance.
2. Call `login(SDKAppID, userId, userSig, callback)` to log in to the component. Enter key parameters as shown below:
 <table>
<tr><th>Parameter Name</th><th>Content</th></tr>
<tr>
<td>SDKAppID</td>
<td>You can view the `SDKAPPID` in the <a href="https://console.cloud.tencent.com/trtc/app">TRTC Console</a>.</td>
</tr><tr>
<td>userId</td>
<td>ID of current user, which is a string that can contain only letters (a–z and A–Z), digits (0–9), hyphens (-), and underscores (_).</td>
</tr><tr>
<td>userSig</td>
<td>Tencent Cloud's proprietary security protection signature. For the calculation method, please see <a href="https://intl.cloud.tencent.com/document/product/647/35166">How to Calculate UserSig</a>.</td>
</tr></table>
<pre>
// Initialize
sCall = TRTCCallingImpl.sharedInstance(context);
sCall.login(1400000123, "userA", "xxxx", new ActionCallback());
</pre>

<span id="model.step5"> </span>

### Step 5. Make an one-to-one video call

1. Caller: Call `call()` method of `TRTCCalling` to initiate a call, and then pass in the `userId` (user ID) and call type parameter `TYPE_VIDEO_CALL` to initiate a video call request.
2. Callee: if already logged in, the callee will receive the `onInvited()` callback. The the caller can use the parameter `callType` to set the call type and and the callee can use this parameter to initiate the call interface. If you want the callee to receive call requests even when logged out, please see [Offline Answering](#model.offline).
3. Callee: to answer the call, the callee can call the `accept()` function and the `openCamera()` function to enable the local camera. The callee can also call `reject()` to reject the call.
4. After the audio/video channel between the caller and callee is established, they will both receive the `onUserVideoAvailable()` event notification, which indicates that they have received each other's image. At this point, they can call `startRemoteView()` to display the remote video image, and the remote audio will be played back by default.

```
// 1. Initialize the component
TRTCCalling sCall = TRTCCallingImpl.sharedInstance(context);
// 2. Register the listener
sCall.addDelegate(new TRTCCallingDelegate() {
    // ... Some listening code snippets are omitted
    public void onInvited(String sponsor, final List<String> userIdList, boolean isFromGroup, int callType) {
        // The sample code here is to answer the call after receiving the call request from `sponsor`. `reject()` can also be called to reject the call
        sCall.accept();
        // Enable local camera after accepting the call request
        TXCloudVideoView localView = new TXCloudVideoView(mContext);
        mParentView.add(remoteView);
        sCall.openCamera(true, localView);
    }
		
    public void onUserVideoAvailable(final String userId, boolean available){
        if (isVideoAvailable) {
            // This indicates that the other party's video image has been obtained, which can be viewed at this point
            TXCloudVideoView remoteView = new TXCloudVideoView(mContext);
            mParentView.add(remoteView);
            trtcCloud.startRemoteView(userId, remoteView);
        } else {
            sCall.stopRemoteView(userId);
        }
    }
});

// 3. Log in to the component. Only after successful login can functions of other features of the component be called
sCall.login(sdkappid, "aaa", usersig, new ActionCallback() {
    public void onSuccess() {
        // 4. The sample code here is for reference only, which enables the camera and calls the user "aaa" after successful login.
        TXCloudVideoView localView = new TXCloudVideoView(mContext);
        mParentView.add(remoteView);
        sCall.openCamera(true, localView);
        sCall.call("aaa", TRTCCalling.TYPE_VIDEO_CALL);
    }
});
```

<span id="model.step6"> </span>

### Step 6. Make a group video call

1. Caller: to initiate a group video call, the caller needs to call the `groupCall()` function in `TRTCCalling` and pass in the required user list (`userIdList`) and optional IM group ID (`groupId`).
2. Callee: a callee can receive the call request through the `onInvited()` event notification.
3. Callee: a callee can call the `accept()` method to answer the call or call the `reject()` method to reject the call after receiving the event notification.
4. If a callee does not respond to the call for a certain period of time (30 seconds by default), this callee will receive the `onCallingTimeOut()` event notification, and the caller will receive the `onNoResp(String userId)` event notification. If multiple callees do not answer the call, the caller can call `hangup()`, and each callee will receive the `onCallingCancel()` event notification.
5. A user can call the `hangup()` method to leave the current group call.
6. If there is a user joining or leaving the call, other users will receive the `onUserEnter()` or `onUserLeave()` event notification.

>?The `groupID` parameter in the `groupCall()` API is the group ID in the IM SDK. If this parameter is set, the call request will be broadcast through the group message system, which is simple and reliable. If this parameter is left empty, the `TRTCCalling` component will send the message to users one by one.

```
// Omitted content...
// Splice the list of users to be called
List<String> callList = new ArrayList();
callList.add("bbb");
callList.add("ccc");
callList.add("ddd");
// If the call is not initiated in an IM group, an empty string can be passed in for `groupId`
sCall.groupCall(callList, TRTCCalling.TYPE_VIDEO_CALL, "");
// Enable local camera
TXCloudVideoView localView = new TXCloudVideoView(mContext);
mParentView.add(remoteView);
sCall.openCamera(true, txCloudVideoView);
```

<span id="model.offline"> </span>

### Step 7. Answer a call offline

>?If your business is online customer service or any other service that does not require the offline answering feature, you only need to complete [step 1](#model.step1) to [step 6](#model.step6) for integration. If your business is used for social networking, you are recommended to implement offline answering.

The IM SDK supports offline push; however, different Android phone vendors have different offline push services, so the access complexity is higher than that on iOS. You need to complete the corresponding settings to meet its availability standard.

1. Apply for the certificate required by the corresponding vendor's push channel, configure it in the IM Console, and add the certificate and ID according to the push requirements. For detailed directions, please see [IM > Offline Push (Android)](https://intl.cloud.tencent.com/document/product/1047/34336).
2. Offline sending function is integrated in `sendModel` IM signaling function of `TRTCCallingImpl`. After the offline push feature is configured, messages can be pushed offline.

<span id="api"> </span>

## Component APIs

Below is the list of `TRTCCalling` component APIs:

| API Fuction        | Description                                                  |
| --------------- | --------------------------------------------------------- |
| addDelegate     | Adds TRTCCalling listener for users to obtain status notifications |
| removeDelegate  | Removes the listener                                                |
| destroy         | Terminates the instance                                                  |
| login           | Logs in to IM. All other features can be used only after login                 |
| logout          | Logs out of IM. Calls cannot be made after logout                         |
| call            | Invites users to C2C call. The invited users will receive the `onInvited` callback         |
| groupCall       | Invites users to IM group call. The invited users will receive the `onInvited` event notification |
| accept          | Answers the call as a callee                                      |
| reject          | Rejects the call as a callee                                      |
| hangup          | Hangs up the call                                                  |
| startRemoteView | Renders the camera data of remote user in the specified `TXCloudVideoView`    |
| stopRemoteView  | Stops rendering the camera data for a remote user                          |
| openCamera      | Enables camera and renders data in the specified `TXCloudVideoView`            |
| closeCamera     | Disables the camera                                                |
| switchCamera    | Switches between front and rear cameras                                            |
| setMicMute      | Specifies whether to mute the mic                                              |
| setHandsFree    | Specifies whether to enable the hands-free mode                                              |

