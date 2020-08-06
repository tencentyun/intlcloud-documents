## Effect Demo



To quickly implement the audio call feature, you can directly modify the demo provided by TRTC for adaptation or use the provided `TRTCAudioCall` component and implement custom UI.

<span id="ui"> </span>
## Reusing Demo UI
<span id="ui.step1"></span>
### Step 1. Create an application
1. Log in to the TRTC Console and select **Development Assistance** > **[Demo Quick Run](https://console.cloud.tencent.com/trtc/quickstart)**.
2. Click **Start Now**, enter the application name such as `TestAudioCall`, and click **Create Application**.

>! This feature uses two basic PaaS services of Tencent Cloud, namely, [TRTC](https://intl.cloud.tencent.com/document/product/647/35078) and [IM](https://intl.cloud.tencent.com/document/product/1047). When TRTC is activated, IM will be activated automatically.

<span id="ui.step2"></span>
### Step 2. Download the SDK and demo source code
1. Mouse over the corresponding block, click **[GitHub](https://github.com/tencentyun/TRTCSDK/tree/master/Android)** to enter GitHub (or click **[ZIP](http://liteavsdk-1252463788.cosgz.myqcloud.com/TXLiteAVSDK_TRTC_Android_latest.zip)**), and download the relevant SDK and supporting demo source code.
 ![](https://main.qcloudimg.com/raw/b0f6f1bd5e0bc083bafddcc7c04a1593.png)
2. After the download is completed, return to the TRTC Console and click **Downloaded and Next**. Then, you can see the `SDKAppID` and key information.

<span id="ui.step3"></span>
### Step 3. Configure demo project files
1. Decompress the source package downloaded in [step 2](#ui.step2).
2. Find and open the `Android/TRTCScenesDemo/debug/src/main/java/com/tencent/liteav/debug/GenerateTestUserSig.java` file.
3. Set the relevant parameters in the `GenerateTestUserSig.java` file:
  <ul><li>SDKAPPID: it is 0 by default. Please replace it with your real `SDKAppID`.</li>
  <li>SECRETKEY: it is an empty string by default. Please replace it with your real key information.</li></ul> 
	<img src="https://main.qcloudimg.com/raw/87dc814a675692e76145d76aab91b414.png">
4. Return to the TRTC Console and click **Pasted and Next**.
5. Click **Close Guide and Enter Console** to manage the application.

>!The scheme for generating `UserSig` mentioned in this document is to configure `SECRETKEY` in the client code. In this method, `SECRETKEY` may be easily decompiled and reversed, and if your key is leaked, attackers can steal your Tencent Cloud traffic; therefore, **this method is only suitable for local execution and debugging of the demo**.
>The correct `UserSig` distribution method is to integrate the calculation code of `UserSig` into your server and provide an application-oriented API. When `UserSig` is needed, your application can make a request to the business server for dynamic `UserSig`. For more information, please see [How to Calculate UserSig](https://intl.cloud.tencent.com/document/product/647/35166).

<span id="ui.step4"></span>
### Step 4. Run the demo
Use Android Studio (v3.5 or above) to open the `TRTCDemo` project and click **Run** to start debugging the demo.

<span id="ui.step5"></span>
### Step 5. Modify the demo source code
The source code folder `trtcaudiocalldemo` contains two subfolders: `ui` and `model`. The `ui` folder contains the UI code:

| File or Folder | Feature Description |
|:-------:|:--------|
| TRTCAudioCallActivity.java | Audio call homepage where calls can be answered or rejected. | 
| SelectContactActivity.java| UI for selecting contacts. |
| TRTCAudioCallHistoryActivity.java| UI for displaying historical contacts, where you can only initiate calls currently. |
| audiolayout | User image rendering and layout logic during call. | 

<span id="model"> </span>
## Implementing Custom UI

The [source code](https://github.com/tencentyun/TRTCSDK/tree/master/Android/TRTCScenesDemo/trtcaudiocalldemo/src/main/java/com/tencent/liteav/trtcaudiocalldemo) folder `trtcaudiocalldemo` contains two subfolders: `ui` and `model`. The `model` folder contains the implemented reusable open-source component `TRTCAudioCall`. You can find the API functions provided by this component in the `ITRTCAudioCall.java` file.
![](https://main.qcloudimg.com/raw/c9e700bcca0adb259529e66fe7400d91.png)

You can use the open-source component `TRTCAudioCall` to implement your own UI, i.e., only reusing the `model` to implement your custom UI.

<span id="model.step1"> </span>
### Step 1. Integrate SDKs
The audio call component `TRTCAudioCall` depends on the TRTC SDK and IM SDK. You can integrate the two SDKs into your project in the following steps:

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
>
2. In `defaultConfig`, specify the CPU architecture to be used by the application.
```
defaultConfig {
    ndk {
        abiFilters "armeabi-v7a"
    }
}
```
3. Click **Sync Now** to sync the SDK.
 >? If JCenter can be connected to, the SDK will be automatically downloaded and integrated into the project.

**Method 2. Implement dependency through local AAR files**
If the access to the Maven repository is slow in your development environment, you can download the ZIP packages and manually integrate the SDKs into your project as instructed in the integration document.

| SDK | Download Page | Integration Guide |
|---------|---------|---------|
| TRTC SDK | [Download](https://intl.cloud.tencent.com/document/product/647/34615) | [Integration document](https://intl.cloud.tencent.com/document/product/647/35093) |
| IM SDK | [Download](https://intl.cloud.tencent.com/document/product/1047/33996) | [Integration document](https://intl.cloud.tencent.com/document/product/1047/34306) |

<span id="model.step2"> </span>
### Step 2. Configure permissions and obfuscation rules
Configure application permissions in `AndroidManifest.xml`. The SDK requires the following permissions (on Android 6.0 and above, the camera and storage read permissions need to be requested dynamically):
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
```java
-keep class com.tencent.** { *; }
```

<span id="model.step3"> </span>
### Step 3. Import the TRTCAudioCall component

Copy all files in the following directory to your project:
```
trtcaudiocalldemo/src/main/java/com/tencent/liteav/trtcaudiocalldemo/model 
```


<span id="model.step4"> </span>
### Step 4. Initialize and log in to the component
1. Call `TRTCAudioCallImpl.sharedInstance(context)` to get the component instance.
2. Call `init()` to initialize the component.
3. Call `login(SDKAppID, userId, userSig, callback)` to log in to the component. Enter key parameters as shown below:
 <table>
<tr>
<th>Parameter Name</th>
<th>Description</th>
</tr>
<tr>
<td>SDKAppID</td>
<td>You can view the `SDKAppID` in the <a href="https://console.cloud.tencent.com/trtc/app">TRTC Console</a>.</td>
</tr>
<tr>
<td>userId</td>
<td>ID of current user, which is a string that can contain only letters (a–z and A–Z), digits (0–9), hyphens (-), and underscores (_).</td>
</tr>
<tr>
<td>userSig</td>
<td>Tencent Cloud's proprietary security protection signature. For the calculation method, please see <a href="https://intl.cloud.tencent.com/document/product/647/35166">How to Calculate UserSig</a>.</td>
</tr>
</table>
<pre>
// Initialize
sCall = TRTCAudioCallImpl.sharedInstance(context);
sCall.init();
sCall.login(1400000123, "userA", "xxxx", new ActionCallback());
</pre>

<span id="model.step5"> </span>
### Step 5. Make a one-to-one audio call
1. Caller: the caller can call the `call()` method in `ITRTCAudioCall` and specify the receiver's `userid` to initiate an audio call request.
2. Receiver: if already logged in, the receiver will receive the `onInvited()` event notification. If you want the receiver to receive call requests even when logged out, please see [Offline Answering](#model.offline).
3. Receiver: to answer the call, the receiver can call the `accept()` function. The receiver can also call `reject()` to reject the call.
3. After the audio/video channel between the caller and receiver is established, they will both receive the `onUserEnter()` event notification, which indicates that they have joined the call.

```
// 1. Initialize the component
ITRTCAudioCall sCall =  TRTCAudioCallImpl.sharedInstance(context);
sCall.init();
// 2. Register the listener
sCall.addListener(new TRTCAudioCallListener() {
	// ... Some listening code snippets are omitted
	public void onInvited(String sponsor, final List<String> userIdList, boolean isFromGroup, int callType) {
		// The sample code here is to answer the call after receiving the call request from `sponsor`. `reject()` can also be called to reject the call
		sCall.accept();
	} 
});
// 3. Log in to the component. Only after successful login can functions of other features of the component be called
sCall.login(sdkappid, "aaa", usersig, new ActionCallback() {
    public void onSuccess() {
        // 4. The sample code here is for reference only, which calls the user "aaa" after successful login.
        sCall.call("aaa");
    }
});
```

<span id="model.step6"> </span>
### Step 6. Make a group audio call
1. Caller: to initiate a group audio call, the caller needs to call the `groupCall()` function in `ITRTCAudioCall` and pass in the required user list (`userIdList`) and optional group ID (`groupId`).
2. Receiver: a receiver can receive the request through the `onInvited()` event notification.
3. Receiver: a receiver can call the `accept()` method to answer the call or call the `reject()` method to reject the call after receiving the event notification.
4. If a receiver does not respond to the call for a certain period of time (30 seconds by default), this receiver will receive the `onCallingTimeOut()` event notification, and the caller will receive the `onNoResp(String userId)` event notification. If multiple receivers do not answer the call, the caller can call `hangup()`, and each receiver will receive the `onCallingCancel()` event notification.
5. A user can call the`hangup()` method to leave the current group call.
6. If there is a user joining or leaving the call, other users will receive the `onUserEnter()` or `onUserLeave()` event notification.

>?The `groupID` parameter in the `groupCall()` API is the group ID in the IM SDK. If this parameter is set, the call request will be broadcast through the group message system, which is simple and reliable. If this parameter is left empty, the `TRTCAudioCall` component will send the message to users one by one.

```
// Omitted content...
// Splice the list of users to be called
List<String> callList = new ArrayList();
callList.add("bbb");
callList.add("ccc");
callList.add("ddd");
// If the call is not initiated in an IM group, an empty string can be passed in for `groupId`
sCall.groupCall(callList, "");
```

<span id="model.offline"> </span>
### Step 7. Answer a call offline
>?If your business is online customer service or any other service that does not require the offline answering feature, you only need to complete [step 1](#model.step1) to [step 6](#model.step6) for integration. If your business is used for social networking, you are recommended to implement offline answering.

The IM SDK supports offline push; however, different Android phone vendors have different offline push services, so the access complexity is higher than that on iOS. You need to complete the corresponding settings to meet its availability standard.

1. Apply for the certificate required by the corresponding vendor's push channel, configure it in the IM Console, and add the certificate and ID according to the push requirements.
2. Modify the commented part of the `sendModel` function in the `TRTCAudioCallImpl` configuration.

<span id="api"> </span>
## Component API List
Below is the list of `TRTCAudioCall` component APIs:

| API Function | Feature |
|---------|---------|
| init | Performs the required initialization before all other features can be used | 
| destroy | Terminates instance |
| addListener | Adds `TRTCAudioCallListener` listener, through which users can get status notifications |
| removeListener | Removes listener |
| login | Logs in to IM. All other features can be used only after login |
| logout | Logs out of IM. Calls cannot be made after logout |
| call | Invites user to C2C call. The invited user will receive the `onInvited` event notification |
| groupCall | Invites users to IM group call. The invited users will receive the `onInvited` event notification |
| accept | Answers call as receiver |
| reject | Rejects call as receiver |
| hangup | Ends call |
| setMicMute | Specifies whether to mute the mic |
| setHandsFree | Specifies whether to enable the hands-free mode |


