## Demo UI
You can [download](https://intl.cloud.tencent.com/document/product/647/35076) and install the app we provide to try out the real-time audio/video call feature.
<table>
<tr>
   <th>Call</th>
   <th>Answer</th>
 </tr>
<tr>
<td><img src="https://main.qcloudimg.com/raw/ef83db73d0a8c487e72986dd1f92e361.jpeg"/></td>
<td><img src="https://main.qcloudimg.com/raw/f57ed3a55112233b05260f5dc37342ca.jpeg"/></td>
</tr>
</table>


>! To make it easier for you to implement the real-time audio/video call feature, we have refactored the `TUICalling` component. You no longer need to pay attention to UI as it is now implemented within the `TUICalling` component.

[](id:ui)

## Running the Demo

[](id:ui.step1)

### Step 1. Create an application
1. Log in to the TRTC console and select **Development Assistance** > **[Demo Quick Run](https://console.cloud.tencent.com/trtc/quickstart)**.
2. Enter an application name such as `TestVideoCall` and click **Create**.
3. Click **Next**.

![](https://main.qcloudimg.com/raw/9f4c878c0a150d496786574cae2e89f9.png)
>!This feature uses two basic PaaS services of Tencent Cloud, namely [TRTC](https://intl.cloud.tencent.com/document/product/647/35078) and [IM](https://intl.cloud.tencent.com/document/product/1047). When you activate TRTC, IM will be activated automatically. IM is a value-added service. See [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350) for its billing details.


[](id:ui.step2)
### Step 2. Download the application source code
Clone or download the [TUICalling](https://github.com/tencentyun/TUICalling) source code.

[](id:ui.step3)
### Step 3. Configure application project files
1. In the **Modify Configuration** step, select your platform.
2. Find and open `Android/Debug/src/main/java/com/tencent/liteav/debug/GenerateTestUserSig.java`.
3. Set parameters in `GenerateTestUserSig.java`:
<ul style="margin:0"><li/>SDKAPPID: a placeholder by default. Set it to the actual `SDKAppID`.
<li>SECRETKEY: a placeholder by default. Set it to the actual key.</ul>
<img src="https://main.qcloudimg.com/raw/87dc814a675692e76145d76aab91b414.png">

4. Click **Next** to complete the creation.
5. After compilation, click **Return to Overview Page**.

>!
>- The method for generating `UserSig` described in this document involves configuring `SECRETKEY` in client code. In this method, `SECRETKEY` may be easily decompiled and reversed, and if your key is disclosed, attackers can steal your Tencent Cloud traffic. Therefore, **this method is suitable only for the local execution and debugging of the app**.
>- The correct `UserSig` distribution method is to integrate the calculation code of `UserSig` into your server and provide an application-oriented API. When `UserSig` is needed, your application can send a request to the business server for a dynamic `UserSig`. For more information, see [How do I calculate UserSig on the server?](https://intl.cloud.tencent.com/document/product/647/35166).

[](id:ui.step4)
### Step 4. Run the application

Open the source code project `TUICalling` with Android Studio (version 3.5 or above) and click **Run**.



## Tryout
>! You need at least two devices to try out the application.

### User A
1. Enter a username (**which must be unique**) and log in.
2. Enter the `userId` of the person you want to call and tap **Search**.
3. Tap **Call** and select **Video Call** (**Make sure that the callee is active in the application, or the call may fail**).<br>

### User B
1. Enter a username (**which must be unique**) and log in.
2. Go to the homepage and wait for the incoming call.



[](id:model)
## Integration Directions

In the [source code](https://github.com/tencentyun/TUICalling/tree/master/Android/Source/src/main/java/com/tencent/liteav/trtccalling), the `Source` folder contains two subfolders: `ui` and `model`. The `model` subfolder includes the open-source `TUICallingManager` component, which we share with the public. You can find the component’s APIs in the `TUICalling.java` file.
![](https://qcloudimg.tencent-cloud.cn/raw/0de26d679e6e0dc1d9aeadb6dbf6f8aa.png)


You can enable the real-time audio/video call feature for your project with ease using the open-source `TUICalling` and `TUICallingManager` components, with no need to implement complicated call UI or logic by yourself.

[](id:model.step1)
### Step 1. Integrate the SDKs

The audio/video call component `TUICalling` depends on the TRTC SDK and IM SDK. Follow the steps below to integrate the two SDKs into your project:

#### Method 1: adding dependencies via Maven

1. Add the TRTC SDK and IM SDK dependencies to `dependencies`.
<dx-codeblock>
::: java java
dependencies {
    compile "com.tencent.liteav:LiteAVSDK_TRTC:latest.release"
    compile 'com.tencent.imsdk:imsdk:latest.release'

    // As we use Gson for parsing, you also need to add the Google Gson dependency.
    compile 'com.google.code.gson:gson:latest.release'
}
:::
</dx-codeblock>
>?You can view the latest version numbers of the two SDKs by visiting their GitHub pages at [TRTC](https://github.com/tencentyun/TRTCSDK) and [IM](https://github.com/tencentyun/TIMSDK).
2. In `defaultConfig`, specify the CPU architecture to be used by your application.
<dx-codeblock>
::: java java
defaultConfig {
      ndk {
            abiFilters "armeabi-v7a"
      }
}
:::
</dx-codeblock>
3. Click **Sync Now** to sync the SDKs.
>?If you have no problem connecting to JCenter, the SDKs will be downloaded and integrated into your project automatically.


#### Method 2: adding dependencies through local AAR files
If your access to the Maven repository is slow, you can download the ZIP files of the SDKs and manually integrate them into your project as instructed in the documents below.

| SDK | Download Page | Integration Guide |
| -------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| TRTC SDK | [Download](https://intl.cloud.tencent.com/document/product/647/34615) | [Integration document](https://intl.cloud.tencent.com/document/product/647/35093) |
| IM SDK | [Download](https://intl.cloud.tencent.com/document/product/1047/33996) | [Integration documentation](https://intl.cloud.tencent.com/document/product/1047/34306) |

[](id:model.step2)

### Step 2. Configure permission requests and obfuscation rules

Configure permission requests for your application in `AndroidManifest.xml`. The SDKs need the following permissions (on Android 6.0 and above, the camera and read storage permissions must be requested at runtime.)

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
-keep class com.tencent.** { *;}
```

[](id:model.step3)

### Step 3. Import the `TUICalling` component

Copy the `Source` directory to your project and import it in `setting.gradle` as shown below:

```
include ':Source'
```

[](id:model.step4)

### Step 4. Initialize the component and log in

1. Call `TUICallingManager.sharedInstance()` to initialize the component.
2. Call `TUILogin.init(context, SDKAppID, config, listener)` to initialize login.
3. Call `TUILogin.login(userId, userSig, callback)` to log in to the component. Specify the key parameters as described below:
 <table>
<tr><th>Parameter</th><th>Description</th></tr><tr>
<tr>
<td>SDKAppID</td>
<td>You can view `SDKAppID` in the <a href="https://console.cloud.tencent.com/trtc/app">TRTC console</a>.</td>
</tr><tr>
<td>userId</td>
<td>ID of the current user, which is a string that can contain letters (a-z and A-Z), digits (0-9), hyphens (-), and underscores (_). We recommend you set it based on your business account system.</td>
</tr><tr>
<td>userSig</td>
<td>Tencent Cloud's proprietary security signature. For the calculation method, please see <a href="https://intl.cloud.tencent.com/document/product/647/35166">UserSig</a>.</td>
</tr>
</tr><tr>
<td>config</td>
<td>SDK configuration, which is used to set the log output level and log callback. You can pass `null` for this parameter. For details, see the sample code below.</td>
</tr><tr>
</tr><tr>
<td>listener</td>
<td>IM listener, which is used to listen for some crucial callbacks, such as forced logout and `userSig` expiration. For details, see the sample code below.</td>
</tr><tr>
</tr><tr>
<td>callback</td>
<td>Callback for login, which indicates whether login is successful. For details, see the sample code below.</td>
</tr><tr>
</table>
<dx-codeblock>
::: java java
     // Initialize the component
     TUICallingManager manager = TUICallingManager.sharedInstance();
  // Log in to the component
  V2TIMSDKConfig config = new V2TIMSDKConfig();
  config.setLogLevel(V2TIMSDKConfig.V2TIM_LOG_DEBUG);
  config.setLogListener(new V2TIMLogListener() {
        @Override
        public void onLog(int logLevel, String logContent) {
                
        }
  });
  TUILogin.init(this, ${Your `SDKAPPID`}, config, new V2TIMSDKListener() {

            @Override
            public void onKickedOffline() {  // Callback for forced logout
                mIsKickedOffline = true;
                checkUserStatus();
            }
    
            @Override
            public void onUserSigExpired() { // Callback for `userSig` expiration
                mIsUserSigExpired = true;
                checkUserStatus();
            }
  });
  TUILogin.login("${Your `userId`}", "${Your `userSig`}", new V2TIMCallback() {
            @Override
            public void onError(int code, String msg) {
                Log.d(TAG, "code: " + code + " msg:" + msg);
            }

            @Override
            public void onSuccess() {
                Log.d(TAG, "onSuccess");
            }
  });

:::
</dx-codeblock>

[](id:model.step5)

### Step 5. Make an audio/video call

1. Caller: Call `call();` of `TUICallingManager` to initiate a call, passing in the user IDs (`userids`) and call type (`type`). For the call type, you can pass in `TUICalling.Type.AUDIO` (audio call) or `TUICalling.Type.VIDEO` (video call). If only one user ID is passed in for `userids`, the call is a one-to-one call; if two or more user IDs are passed in, the call is a group call.
2. Callee: If a callee is logged in, the answering view will be displayed. If you want offline users to receive call invitations, please see [Enable offline call answering](#model.offline).


<dx-codeblock>
::: java java
// 1. Initialize the component
TUICallingManager manager = TUICallingManager.sharedInstance();
// 2. Register the listener
manager.setCallingListener(new TUICalling.TUICallingListener() {
            @Override
            public boolean shouldShowOnCallView() {
                return true;
            }

            @Override
            public void onCallStart(String[] userIDs, TUICalling.Type type, TUICalling.Role role, final View tuiCallingView) {
                if (!shouldShowOnCallView() || null == tuiCallingView) {
                    return;
                }
                runOnUiThread(new Runnable() {
                    @Override
                    public void run() {
                        FrameLayout.LayoutParams params = new FrameLayout.LayoutParams(FrameLayout.LayoutParams.MATCH_PARENT, FrameLayout.LayoutParams.MATCH_PARENT);
                        mCallingView = tuiCallingView;
                        addContentView(tuiCallingView, params);
                    }
                });
            }
    
            @Override
            public void onCallEnd(String[] userIDs, TUICalling.Type type, TUICalling.Role role, long totalTime) {
                removeView();
            }
    
            @Override
            public void onCallEvent(TUICalling.Event event, TUICalling.Type type, TUICalling.Role role, String message) {
                if (TUICalling.Event.CALL_FAILED == event) {
                    removeView();
                }
            }
});
// 3. Make a call
manager.call(userIDs, TUICalling.Type.VIDEO);
:::
</dx-codeblock>

[](id:model.offline)

### Step 6. Enable offline call answering

>?If your project does not require the offline answering feature, for example, if it offers online customer service, your integration can end at [step 5](#model.step5). If your project is a social networking service, we recommend you enable offline answering.

The IM SDK supports offline push. However, since the offline push service of Android phones varies from vendor to vendor, the configuration required to enable offline push for Android is more complicated than that for iOS.

1. Apply for a certificate required by the vendor's push channel, configure it in the IM console, and add the certificate and ID as required. For detailed directions, please see [IM > Offline Push (Android)](https://intl.cloud.tencent.com/document/product/1047/39156).
2. The offline push API has been integrated into the signaling API (`sendModel`) of `TRTCCallingImpl`. After completing the offline push configuration for your application, you will be able to send notifications to offline users.

[](id:api)

## Component APIs

The table below lists the APIs of the `TUICalling` component.

| API        | Description                                                  |
| --------------- | --------------------------------------------------------- |
| call            | Sends call invitations by user ID.         |
| receiveAPNSCalled          | Answers a call.                                      |
| setCallingListener          | Sets the listener.                                     |
| setCallingBell          | Sets the ringtone (preferably shorter than 30s).                                                 |
| enableMuteMode | Enables/Disables the mute mode.    |
| enableCustomViewRoute      | Enables/Disables custom views. After enabling custom views, you will receive a `CallingView` instance in the callback for calling/being called, and can decide how to display the view by yourself. The view must be displayed full screen or in proportion to the screen size; otherwise, an error may occur.           |

