TUIKit 4.8.50 and later versions provide audio/video call features and support interconnection between iOS, Android, and web platforms.

> ? 
> - **TUIKit 6.5.xxxx and later versions provide upgraded audio/video call features with brand-new TUICallKit. To use these upgraded features, you need to purchase the dedicated IM audio/video call capability package.** The purchase method is described in [**Step 1. Activate the TRTC Service**](#step1). If you have already activated the TRTC service, ignore this step.
> - It should be noted that the integration method varies depending on the TUIKit version, as described in [Version Description](#version). **You are advised to upgrade to 6.5.2816 or later. This document focuses on the integration solutions for 6.5.2816 or later.**

Audio/Video call UIs are shown as follows:

<table style="text-align:center;vertical-align:middle;width:1000px">
  <tr>
    <th style="text-align:center;" width="500px">Video Call<br></th>
    <th style="text-align:center;" width="500px">Voice Call<br></th>
  </tr>
  <tr>
    <td><img style="width:500px" src="https://qcloudimg.tencent-cloud.cn/raw/5ca955c288c0c45b74e4fcfcb0ec6ebb.png"  />    </td>
    <td><img style="width:500px" src="https://qcloudimg.tencent-cloud.cn/raw/068a66d2a99a910d516e645ffb06a23a.png" />     </td>
	 </tr>
</table>
[](id:step1)

## Step 1: Activate the TRTC Service
1. Log in to the [IM console](https://console.cloud.tencent.com/im) and click the target app card to go to the basic configuration page of the app.
2. In the lower-right corner, click **Free trial** under **Activate Tencent Real-Time Communication (TRTC)** to activate the 7-day free trial service of TUICallKit. After the completion of the experience, if you want to purchase the official audio/video call capability package, click **[here](https://buy.cloud.tencent.com/avc)**.

   <img src="https://qcloudimg.tencent-cloud.cn/raw/667633f7addfd0c589bb086b1fc17d30.png" style="zoom:75%;" />

>= **Notes**: If you have used [TRTC](https://intl.cloud.tencent.com/document/product/647/35078) before, after clicking **Free trial**, the following error may occur: `[-100013]:TRTC service is suspended. Please check if the package balance is 0 or the Tencent Cloud account is in arrears`.
>
>This is because the new IM audio/video call capability is based on two basic PaaS services: [TRTC](https://intl.cloud.tencent.com/document/product/647/35078) and [IM](https://intl.cloud.tencent.com/document/product/1047/35448). If you have used up your free monthly minutes (10,000) for TRTC, you will fail to activate the capability. You can log in to the [TRTC console](https://console.cloud.tencent.com/trtc/app), go to the application management page of the corresponding SDKAppID, and activate the pay-as-you-go feature, as shown in the figure below. Then, next time when you **start the application**, you can experience the new audio/video call capability properly.
><img width=800px src="https://qcloudimg.tencent-cloud.cn/raw/a568f2790baf160f4aff4f42f60e8c1c.png" />

[](id:step2)
## Step 2: Configure Project Files
Add `tuicallkit` dependency to the `build.gradle` file in `APP`:
```groovy
api project(':tuicallkit')
```

[](id:step3)
## Step 3: Enable/Disable Audio/Video Call 
**TUICallKit and TUIChat can be freely combined. After TUICallKit is integrated, the audio and video call features are enabled for TUIChat by default and their entries are displayed on the More menu on the chat UI.**

If you want to dynamically enable or disable the audio/video call entry in TUIChat, you can manually change the `addActionsFromListeners` function in the `InputView.java` file. Sample code:
```java
    private void addActionsFromListeners() {
    		...
    	boolean enableAudio = true; // Dynamically enable the audio call entry
        boolean enableVideo = true; // Dynamically enable the video call entry
        Map<String, Object> audioCallExtension = TUICore.getExtensionInfo(TUIConstants.TUIChat.EXTENSION_INPUT_MORE_AUDIO_CALL, param);
        if (audioCallExtension != null && enableAudio) {
            ...
            mInputMoreActionList.add(audioUnit);
        }

        Map<String, Object> videoCallExtension = TUICore.getExtensionInfo(TUIConstants.TUIChat.EXTENSION_INPUT_MORE_VIDEO_CALL, param);
        if (videoCallExtension != null && enableVideo) {
            ...
            mInputMoreActionList.add(videoUnit);
        }
        ...
    }
```

<img src="https://qcloudimg.tencent-cloud.cn/raw/63d6ae09138aa70deff8c388e8fc39c7.png" style="zoom:50%;" />

[](id:step4)

## Step 4: Offline Push
Before using offline push, you need to activate the [IM offline push](https://intl.cloud.tencent.com/document/product/1047/39156) service. For application configuration, you can refer to [OEMPush](https://github.com/TencentCloud/TIMSDK/tree/master/Android/Demo/app/src/main/java/com/tencent/qcloud/tim/demo/thirdpush/OEMPush) in TUIKitDemo to quickly integrate vendor push feature. After that, offline push notifications can be received on the receiver.
<img src="https://qcloudimg.tencent-cloud.cn/raw/4927cbb3d4d430ae0a8d052ffde7f730.png" style="zoom:50%;" />

You can click such a notification to redirect to the call UI.

>? After the configuration is completed, when you click a received audio/video call notification pushed offline, the redirected-to page that you configure for the application is displayed first, and then TUICallKit automatically opens the audio/video call invitation UI.


[](id:version)

## Version Description

| Version                | Library/Component Name | Description                                                         |
| :------------------ | ----------- | ------------------------------------------------------------ |
| 4.8.50 - 5.1.60     | tuikit      | TUIKit is integrated with the TRTC UI components and [TRTC](https://intl.cloud.tencent.com/document/product/647/35078) audio/video library by default. |
| 5.4.666 - 5.6.1200  | tuikitlive  | TUIKit is no longer integrated with the TRTC UI components and TRTC audio/video library by default.  <br/>Related audio/video logic is moved to the TUIKitLive component. |
| 5.7.1435 - 6.0.1992 | tuicalling  | TUICalling includes all audio/video call UI components and [TRTC](https://intl.cloud.tencent.com/document/product/647/35078) audio/video library. <br/>TUICalling can be freely combined with other components of [TUIKit](https://intl.cloud.tencent.com/document/product/1047/34547). |
| 6.1.2155 - 6.5.2803 | tuicalling  | The foreground/background switch experience of TUICalling is optimized.                                |
| 6.5.2816 or above     | tuicallkit  | The audio/video call component is upgraded and provides more powerful features.                           |

[](id:qa)

## FAQs

[](id:question1)

### 1. Will the call UI be displayed if the invitee goes offline and then online within the call invitation timeout duration?

Depending on the startup type of the application, there are different cases:
![](https://im.sdk.cloud.tencent.cn/tools/resource/tuicalling/android/calling_backgroud.png)

### 2. Why can't the call UI be pulled when I click an offline push notification?

Check the configured redirection logic of offline push to ensure that the main UI of the application can be pulled.

>?For example, the intent configured in the application must be consistent with that configured in the Mi push console.
>
<img src="https://qcloudimg.tencent-cloud.cn/raw/36a58d694140e96d550771a4b9fb40b6.png" width="600px"/>

```
<activity
    android:name="Application package name.MainActivity"
    android:launchMode="singleTask"
    android:screenOrientation="portrait">
    <intent-filter>
        <action android:name="android.intent.action.VIEW" />
        <category android:name="android.intent.category.DEFAULT" />
        <data
            android:host="com.tencent.qcloud"
            android:path="/detail"
            android:scheme="pushscheme" />
    </intent-filter>
</activity>
```

### 3. Why can't the call UI be pulled to the foreground when the application is running on the background?

**To automatically pull the application from the background to the foreground, it is necessary to check whether the "background autostart" or "floating window" permission is enabled on the application.**

Note that different vendors or even different Android versions from the same vendor offers different permissions and permission names. For example, you only need to enable the **background pop-up window** permission for Mi 6, while you need to enable both the **background pop-up window** and **floating window display** permissions.

> ? If you manually enable all permissions during the test, the call UI cannot be automatically pulled up to the foreground, and compatibility processing is required. You can join QQ group **592465424** to contact us for assistance.

The following figure shows the path to permission setting on an OPPO phone.

<img src="https://qcloudimg.tencent-cloud.cn/raw/754e8fa031d599f431c68851e49ccdd9.png" width="350px"/>


[](id:feedback)


