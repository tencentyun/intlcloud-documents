## Demonstration

To quickly implement the video call feature, you can directly modify the demo provided by TRTC for adaptation or use the provided `TRTCCalling` component and implement your custom UI.

>! We previously provided the `TRTCVideoCall` component, which has been moved to the [component repository](https://github.com/tencentyun/LiteAVClassic). The `TRTCCalling` component uses IM signaling APIs and is not compatible with the old component.

[](id:ui)

## Using Demo UI

[](id:ui.step1)

### Step 1. Create an application
1. Log in to the TRTC console and select **Development Assistance** > **[Demo Quick Run](https://console.cloud.tencent.com/trtc/quickstart)**.
2. Enter an application name, e.g., `TestVideoCall`, and click **Create**.

>!This feature uses two basic PaaS services of Tencent Cloud, namely [TRTC](https://intl.cloud.tencent.com/document/product/647/35078) and [IM](https://intl.cloud.tencent.com/document/product/1047). When you activate TRTC, IM will be activated automatically. IM is a value-added service. See [Value-added Service Pricing](https://intl.cloud.tencent.com/document/product/1047/34350) for its billing details.


[](id:ui.step2)
### Step 2. Download the SDK and demo source code
1. Download the SDK and demo source code for your platform.
2. Click **Next**.

[](id:ui.step3)
### Step 3. Configure demo project files
1. In the **Modify Configuration** step, select the platform in line with the source package downloaded.
2. Find and open the `Android/TRTCScenesDemo/debug/src/main/java/com/tencent/liteav/debug/GenerateTestUserSig.java` file.
3. Set parameters in `GenerateTestUserSig.java` as follows.
<ul style="margin:0"><li/>SDKAPPID: 0 by default. Set it to the actual `SDKAppID`.
<li/>SECRETKEY: left empty by default. Set it to the actual key.</ul>
<img src="https://main.qcloudimg.com/raw/87dc814a675692e76145d76aab91b414.png">

4. Click **Next** to complete the creation.
5. After compilation, click **Return to Overview Page**.

>!
>- The method for generating `UserSig` described in this document involves configuring `SECRETKEY` in client code. In this method, `SECRETKEY` may be easily decompiled and reversed, and if your key is leaked, attackers can steal your Tencent Cloud traffic. Therefore, **this method is only suitable for the local execution and debugging of the demo**.
>- The correct `UserSig` distribution method is to integrate the calculation code of `UserSig` into your server and provide an application-oriented API. When `UserSig` is needed, your application can send a request to the business server for a dynamic `UserSig`. For more information, please see [How do I calculate UserSig on the server?](https://intl.cloud.tencent.com/document/product/647/35166).

[](id:ui.step4)

### Step 4. Run the demo

Open the `TRTCDemo` project with Android Studio (version 3.5 or above) and click **Run**.

[](id:ui.step5)

### Step 5. Modify the demo source code

The source code folder `trtccallingdemo` contains two subfolders: `ui` and `model`. The `ui` folder contains the UI code:

| File or Folder | Feature Description |
| -------------------------------- | ------------------------------------------------------------ |
| TRTCVideoCallActivity.java | Video call UI where calls can be answered or rejected. |
| TRTCCallingEntranceActivity.java | UI for selecting contacts, where registered users can be searched for and called. |
| videolayout | Video image rendering and layout logic. |

[](id:model)

## Implementing Your Custom UI

The [source code](https://github.com/tencentyun/TRTCSDK/tree/master/Android/TRTCScenesDemo/trtccallingdemo/src/main/java/com/tencent/liteav/trtccalling) folder `trtccallingdemo` contains two subfolders: `ui` and `model`. The `model` folder contains the implemented reusable open-source component `TRTCCalling`. You can find the API functions provided by this component in the `TRTCCalling.java` file.
![](https://main.qcloudimg.com/raw/9b4087b68541912ce9e7a48955cd48e8.png)

You can use the open-source component `TRTCCalling` to implement your own UI, i.e., only reusing the `model` to implement your custom UI.

<span id="model.step1"></span>

### Step 1. Integrate SDKs

The audio/video call component `TRTCCalling` depends on the TRTC SDK and IM SDK. You can integrate the two SDKs into your project by following the steps below:

**Method 1: implement dependency through the Maven repository**

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

2. In `defaultConfig`, specify the CPU architecture to be used by the app.
```
defaultConfig {
    ndk {
        abiFilters "armeabi-v7a"
    }
}
```
3. Click **Sync Now** to sync the SDK.
>?If JCenter can be connected to, the SDK will be automatically downloaded and integrated into the project.


**Method 2: implement dependency through the local AAR files**
If the access to the Maven repository is slow in your development environment, you can download the ZIP packages and manually integrate the SDKs into your project as instructed in the integration document.

| SDK | Download Page | Integration Guide |
| -------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| TRTC SDK | [Download](https://intl.cloud.tencent.com/document/product/647/34615) | [Integration documentation](https://intl.cloud.tencent.com/document/product/647/35093) |
| IM SDK | [Download](https://intl.cloud.tencent.com/document/product/1047/33996) | [Integration documentation](https://intl.cloud.tencent.com/document/product/1047/34306) |

[](id:model.step2)

### Step 2. Configure permission requests and obfuscation rules

Configure permissions for your app in `AndroidManifest.xml`. The SDKs need the following permissions (on Android 6.0 and above, the camera and read storage permissions must be requested at runtime.)

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

In the `proguard-rules.pro` file, add the SDK classes to the "do not obfuscate" list.

```
-keep class com.tencent.** { *; }
```

[](id:model.step3)

### Step 3. Import the TRTCCalling component

Copy all the files in the following directory to your project:

```
trtccallingdemo/src/main/java/com/tencent/liteav/trtccalling/model 
```

[](id:model.step4)

### Step 4. Initialize and log in to the component

1. Call `TRTCCallingImpl.sharedInstance(context)` to get the component instance.
2. Call `login(SDKAppID, userId, userSig, callback)` to log in to the component. Enter the key parameters as shown below:
 <table>
<tr><th>Parameter</th><th>Description</th></tr>
<tr>
<td>SDKAppID</td>
<td>You can view the `SDKAppID` of your application in the <a href="https://console.cloud.tencent.com/trtc/app">TRTC console</a>.</td>
</tr><tr>
<td>userId</td>
<td>ID of the current user, which is a string that can contain only letters (a–z and A–Z), digits (0–9), hyphens (-), and underscores (_).</td>
</tr><tr>
<td>userSig</td>
<td>Tencent Cloud's proprietary security protection signature. For the calculation method, please see <a href="https://intl.cloud.tencent.com/document/product/647/35166">UserSig</a>.</td>
</tr></table>
<dx-codeblock>

```
sCall = TRTCCallingImpl.sharedInstance(context);
sCall.login(1400000123, "userA", "xxxx", new ActionCallback());
```

[](id:model.step5)

### Step 5. Make a one-to-one call

1. Caller: the caller can call the `call()` method in `TRTCCalling` and pass in the user ID as `userid` and `TYPE_VIDEO_CALL` as `type` to initiate a call request.
2. Receiver: if already logged in, the receiver will receive the `onInvited()` event notification, where `callType` is the call type entered by the caller. You can start the corresponding UI according to this parameter. If you want the receiver to receive call requests even when logged out, please see [Offline Answering](#model.offline).
3. Receiver: to answer the call, the receiver can call the `accept()` function and the `openCamera()` function to enable the local camera. The receiver can also call `reject()` to reject the call.
4. After the audio/video channel between the caller and receiver is established, they will both receive the `onUserVideoAvailable()` event notification, which indicates that they have received each other's image. At this point, they can call `startRemoteView()` to display the remote video image, and the remote audio will be played back by default.


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
        mParentView.add(localView);
        sCall.openCamera(true, localView);
    }
    
    public void onUserVideoAvailable(final String userId, boolean isVideoAvailable) {
        if (isVideoAvailable) {
            // This indicates that the other party's video image has been obtained, which can be viewed at this point
            TXCloudVideoView remoteView = new TXCloudVideoView(mContext);
            mParentView.add(remoteView);
            sCall.startRemoteView(userId, remoteView);
        } else {
            sCall.stopRemoteView(userId);
        }
    }
});

// 3. Log in to the component. Only after successful login can functions of the other features of the component be called
sCall.login(sdkappid, "aaa", usersig, new ActionCallback() {
    public void onSuccess() {
        // 4. The sample code here is for reference only, which enables the camera and calls the user "aaa" after successful login.
        TXCloudVideoView localView = new TXCloudVideoView(mContext);
        mParentView.add(localView);
        sCall.openCamera(true, localView);
        sCall.call("aaa", TRTCCalling.TYPE_VIDEO_CALL);
    }
});
```

<span id="model.step6"></span>

### Step 6. Make a group video call

1. Caller: to initiate a group video call, the caller needs to call the `groupCall()` function in `TRTCCalling` and pass in the required user list (`userIdList`), `TYPE_VIDEO_CALL` as the required call type (`type`), and the optional IM group ID (`groupId`).
2. Receiver: a receiver can receive the call request through the `onInvited()` event notification.
3. Receiver: a receiver can call the `accept()` method to answer the call or call the `reject()` method to reject the call after receiving the event notification.
4. If a receiver does not respond to the call for a certain period of time (30 seconds by default), this receiver will receive the `onCallingTimeOut()` event notification, and the caller will receive the `onNoResp(String userId)` event notification. If multiple receivers do not answer the call, the caller can call `hangup()`, and each receiver will receive the `onCallingCancel()` event notification.
5. A user can call the`hangup()` method to leave the current group call.
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
mParentView.add(localView);
sCall.openCamera(true, txCloudVideoView);
```

<span id="model.offline"></span>

### Step 7. Answer a call offline

>?If your business is an online customer service or any other service that does not require the offline answering feature, you only need to complete [step 1](#model.step1) to [step 6](#model.step6) for integration. If your business is used for social networking, we recommend that you implement offline answering.

The IM SDK supports offline push. However, different Android phone vendors have different offline push services, so the access complexity is higher than that on iOS. You need to complete the corresponding settings to meet its availability standard.

1. Apply for the certificate required by the corresponding vendor's push channel, configure it in the IM console, and add the certificate and ID according to the push requirements. For detailed directions, please see [IM > Offline Push (Android)](https://intl.cloud.tencent.com/document/product/1047/39156).
2. Currently, the offline sending function has already been integrated in the `sendModel` signaling function of `TRTCCallingImpl`. After offline push is configured for the application, messages can be pushed offline.

[](id:api)

## Component API List

Below is the list of `TRTCCalling` component APIs:

| API Function | Feature |
| --------------- | --------------------------------------------------------- |
| addDelegate | Adds the `TRTCCalling` listener, through which users can get status notifications |
| removeDelegate | Removes the listener |
| destroy | Terminates the instance |
| login | Logs in to IM. All other features can be used only after login |
| logout | Logs out of IM. Calls cannot be made after logout |
| call | Invites the user to the C2C call. The invited user will receive the `onInvited` event notification |
| groupCall | Invites users to an IM group call. The invited users will receive the `onInvited` event notification |
| accept | Answers the call as a receiver |
| reject | Rejects the call as a receiver |
| hangup | Ends the call |
| startRemoteView | Renders the camera data of the remote user in the specified `TXCloudVideoView` |
| stopRemoteView | Stops rendering the camera data of the remote user |
| openCamera | Enables the camera and renders the camera data into the specified `TXCloudVideoView` |
| closeCamera | Disables the camera |
| switchCamera | Switches between the front and rear cameras |
| setMicMute | Specifies whether to mute the mic |
| setHandsFree | Specifies whether to enable the hands-free mode |

