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
## Step 2: Integrate the TUICallKit Component

1. Add the following content to the Podfile.
```objectivec
// Integrate the TRTCCalling component
pod 'TUICallKit'                  
```

2. Run the following command to download the third-party library to the current project:
```
pod install
```

 If you cannot install the latest TUIKit version, run the following command to update the local CocoaPods repository list:
```
 pod repo update
```

[](id:step3)

## Step 3: Enable/Disable Audio/Video Call

TUICallKit and TUIChat can be freely combined. After TUICallKit is integrated, the audio and video call features are enabled for TUIChat by default and their entries are displayed on the More menu on the chat UI.

If you want to dynamically enable or disable the audio/video call entry in TUIChat, configure `enableVideoCall` and `enableAudioCall` in `TUIChatConfig` before entering the chat UI.
Sample code:
```
[TUIChatConfig defaultConfig].enableVideoCall = NO; // `YES`: Enable. `NO`: Disable
[TUIChatConfig defaultConfig].enableAudioCall = NO; // `YES`: Enable. `NO`: Disable
```

<img src="https://main.qcloudimg.com/raw/17698afaedf9ba86045c03ef85159bec.png" style="zoom:40%;" />

[](id:step4)

## Step 4: Offline Push

Before using offline push, you need to activate the [IM offline push](https://intl.cloud.tencent.com/document/product/1047/39157) service. For application configuration, you can refer to [Integrating TUIOfflinePush and Running the Offline Push Feature](https://intl.cloud.tencent.com/document/product/1047/47949).

**After the configuration is completed, when you click a received audio/video call notification pushed offline, TUICallKit automatically opens the audio/video call invitation UI.**



[](id:version)
## Version Description

| Version | Library/Component Name | Description |
| --- | --- | --- |
| 4.8.50 - 5.1.60 | TXIMSDK_TUIKit_iOS   | TUIKit is integrated with the TRTC UI components and [TRTC](https://intl.cloud.tencent.com/document/product/647/35078) audio/video library by default. |
| 5.4.666 - 5.6.1200  | TXIMSDK_TUIKit_live_iOS  | - TUIKit is no longer integrated with the TRTC UI components and TRTC audio/video library by default.  <br/>- Related audio/video logic is moved to the TXIMSDK_TUIKit_live_iOS component. |
| 5.7.1435 - 6.0.1992 | TUICalling | TUICalling includes all audio/video call UI components and [TRTC](https://intl.cloud.tencent.com/document/product/647/35078) audio/video library. <br/>TUICalling can be freely combined with other components of [TUIKit](https://intl.cloud.tencent.com/document/product/1047/34547). |
| 6.1.2155 or above | TUICalling | he foreground/background switch experience of TUICalling is optimized. |
| 6.5 or above | TUICallKit | The audio/video call component is upgraded and provides more powerful features. |

[](id:qa)

## FAQs

[](id:question1)

1. Will an invitee receive a call invitation immediately if the invitee goes offline and then online within the call invitation timeout duration?

   If the call invitation is initiated in a one-to-one chat, the invitee can receive the call invitation, and the TUIKit will automatically open the call invitation UI internally.

   If the call invitation is initiated in a group chat, the TUIKit will automatically pull the call invitations of the last 30 seconds and open the group call UI.

2. What should I do if TUICallKit conflicts with an audio/video library that I have integrated?

   TUICallKit and Tencent Cloud [audio/video libraries](https://intl.cloud.tencent.com/document/product/647/34615) cannot be integrated at the same time. Otherwise, symbol conflicts may occur. Do as follows:

   If you have integrated the `TXLiteAVSDK_TRTC` library, no symbol conflict will occur, and you can directly add dependency in the Podfile as follows:

   ```
   pod 'TUICallKit'
   ```

   If you have integrated the `TXLiteAVSDK_Professional` library, symbol conflicts will occur, and you can add dependency in the Podfile as follows:

   ```
   pod 'TUICallKit/Professional'
   ```

   If you have integrated the `TXLiteAVSDK_Enterprise` library, symbol conflicts will occur, and you are advised to upgrade it to `TXLiteAVSDK_Professional` before using `TUICallKit/Professional`.

   

3. What should I do if "ld: framework not found BoringSSL clang: error: linker command failed with exit code 1  sdk" is reported after TUICallKit is integrated?

   The audio/video library on which TUICallKit relies currently does not support simulators. Please use real devices for demo running or debugging.

[](id:feedback)



## Open Source Construction

You can find the TUICalling open source project before the upgrade [**here**](https://github.com/tencentyun/TUICalling/tree/open).
