TUIKit 4.8.50 and later versions provide audio/video call features and support interconnection between iOS, Android, and web platforms.

> ? 
> - **TUIKit 6.5.xxxx and later versions provide upgraded audio/video call features with brand-new TUICallKit. To use these upgraded features, you need to purchase the dedicated IM audio/video call capability package.** The purchase method is described in [**Step 1. Activate the TRTC Service**](#step1). If you have already activated the TRTC service, ignore this step.
> - It should be noted that the integration method varies depending on the TUIKit version, as described in [Version Description](#version). **You are advised to upgrade to 6.5.2816 or later. This document focuses on the integration solutions for 6.5.2816 or later.**

Audio/Video call UIs are shown as follows:

<table style="text-align:center;vertical-align:middle;width:1000px">
  <tr>
    <th style="text-align:center;" width="500px">Video Call<br></th>
    <th style="text-align:center;" width="500px">Audio Call<br></th>
  </tr>
  <tr>
    <td><img style="width:500px" src="https://qcloudimg.tencent-cloud.cn/raw/83d6cd991cd0e9251caafebe75e46f12.png"  />    </td>
    <td><img style="width:500px" src="https://qcloudimg.tencent-cloud.cn/raw/842c563a9dd99da4950402e7a61836dd.png" />     </td>
	 </tr>
</table>

[](id:step1)

## Step 1: Activate the Video Calls Service
1. Log in to the [IM console](https://console.cloud.tencent.com/im) and click the target application card to go to the basic configuration page.

2. In the bottom-right corner of the page, click **Audio/Video call capability - free trial** in the **TRTC** section. In the **Activate free trial of audio/video call feature** pop-up window, click **Activate Now** to activate the **60-day free trial** of TUICallKit.

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

<img src="https://qcloudimg.tencent-cloud.cn/raw/e7c9702e70914acd930d91d1dfb4548b.png" style="zoom:50%;" />

[](id:step4)

## Step 4: Offline Push
Before using offline push, you need to activate the [IM offline push](https://www.tencentcloud.com/document/product/1047/39156) service. For application configuration, you can refer to [OEMPush](https://github.com/TencentCloud/TIMSDK/tree/master/Android/TUIKit/TUIOfflinePush/tuiofflinepush/src/main/java/com/tencent/qcloud/tim/tuiofflinepush/OEMPush) in TUIKitDemo to quickly integrate vendor push feature. After that, offline push notifications can be received on the receiver.
<img src="https://qcloudimg.tencent-cloud.cn/raw/4927cbb3d4d430ae0a8d052ffde7f730.png" style="zoom:50%;" />

You can click such a notification to redirect to the call UI.

>? After the configuration is completed, when you click a received audio/video call notification pushed offline, the redirected-to page that you configure for the application is displayed first, and then TUICallKit automatically opens the audio/video call invitation UI.

[](id:version)

## Version Description

| Version             | Library/Component Name | Description                                                  |
| :------------------ | ---------------------- | ------------------------------------------------------------ |
| 4.8.50 - 5.1.60     | TUIKit                 | TUIKit is integrated with the TRTC UI components and [TRTC](https://intl.cloud.tencent.com/document/product/647/35078) audio/video library by default. |
| 5.4.666 - 5.6.1200  | TUIKitLive             | TUIKit is no longer integrated with the TRTC UI components and TRTC audio/video library by default.  <br/>Related audio/video logic is moved to the TUIKitLive component. |
| 5.7.1435 - 6.0.1992 | TUICalling             | TUICalling includes all audio/video call UI components and [TRTC](https://intl.cloud.tencent.com/document/product/647/35078) audio/video library. <br/>TUICalling can be freely combined with other components of [TUIKit](https://intl.cloud.tencent.com/document/product/1047/34547). |
| 6.1.2155 - 6.5.2803 | TUICalling             | The foreground/background switch experience of TUICalling is optimized. |
| 6.5.2816 or above   | TUICallKit             | The audio/video call component is upgraded and provides more powerful features. |

[](id:qa)

## FAQs

[](id:question1)

#### What should I do if I receive the error message "The package you purchased does not support this ability"?

The error message indicates that your app's **audio/video call capability package has expired or is not activated**. You can refer to [step 1](#step1) to claim or activate the audio/video call capability to continue using TUICallKit.

#### How do I purchase a package?

The audio/video call SDK **is currently in beta, with a 60-day free edition provided**. 

#### Will the call UI be displayed if the invitee goes offline and then online within the call invitation timeout duration?

Depending on the startup type of the application, there are different cases:
![](https://qcloudimg.tencent-cloud.cn/raw/3923f257f13a8b5451b36b8b43f05031.jpeg)

>?If the call UI is not displayed when you go offline and then go online again, filter **"onReceiveNewInvitation"** logs and check whether historical messages are pulled successfully.

#### Why can't the call UI be pulled when I click an offline push notification?

Check the configured redirection logic of offline push to ensure that the main UI of the application can be pulled.

>?For example, the intent configured in the application must be consistent with that configured in the Mi push console.
>

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

#### Why can't the call UI be pulled to the foreground when the application is running on the background?

**To automatically pull the application from the background to the foreground, it is necessary to check whether the "background autostart" or "floating window" permission is enabled on the application.**

Note that different vendors or even different Android versions from the same vendor offers different permissions and permission names. For example, you only need to enable the **background pop-up window** permission for Mi 6, while you need to enable both the **background pop-up window** and **floating window display** permissions.

> ? If you manually enable all permissions during the test, the call UI cannot be automatically pulled up to the foreground, and compatibility processing is required.




#### What should I do if I am using TUICalling of an earlier version and want to upgrade the IM-related components (TUIChat/TUIConversation/TUIGroup/TUIContact/TUISearch/TUIOfflinePush) separately?

You only need to replace the source code of the IM-related components. TUICalling and TUICallKit can interconnect with each other, and you are advised to upgrade to the latest TUICallKit.

[](id:feedback)
