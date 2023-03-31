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
## Step 2: Integrate the TUICallKit Component

1. Add the following content to the Podfile.
```objectivec
// Integrate the TUICallKit component
pod 'TUICallKit'                  
```
2. Run the following command to download the third-party library to the current project:
```sh
pod install
```
 If you cannot install the latest TUIKit version, run the following command to update the local CocoaPods repository list:
```sh
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

<img src="https://qcloudimg.tencent-cloud.cn/raw/e7c9702e70914acd930d91d1dfb4548b.png" style="zoom:40%;" />

[](id:step4)

## Step 4: Offline Push

Before using offline push, you need to activate the [IM offline push](https://intl.cloud.tencent.com/document/product/1047/39157) service. For application configuration, you can refer to [Integrating TUIOfflinePush and Running the Offline Push Feature](https://intl.cloud.tencent.com/document/product/1047/47949).

**After the configuration is completed, when you click a received audio/video call notification pushed offline, TUICallKit automatically opens the audio/video call invitation UI.**



[](id:version)
## Version Description

| Version             | Library/Component Name  | Description                                                  |
| ------------------- | ----------------------- | ------------------------------------------------------------ |
| 4.8.50 - 5.1.60     | TXIMSDK_TUIKit_iOS      | TUIKit is integrated with the TRTC UI components and [TRTC](https://intl.cloud.tencent.com/document/product/647/35078) audio/video library by default. |
| 5.4.666 - 5.6.1200  | TXIMSDK_TUIKit_live_iOS | - TUIKit is no longer integrated with the TRTC UI components and TRTC audio/video library by default.  <br/>- Related audio/video logic is moved to the TXIMSDK_TUIKit_live_iOS component. |
| 5.7.1435 - 6.0.1992 | TUICalling              | TUICalling includes all audio/video call UI components and [TRTC](https://intl.cloud.tencent.com/document/product/647/35078) audio/video library. <br/>TUICalling can be freely combined with other components of [TUIKit](https://intl.cloud.tencent.com/document/product/1047/34547). |
| 6.1.2155 or above   | TUICalling              | The foreground/background switch experience of TUICalling is optimized. |
| 6.5 or above        | TUICallKit              | The audio/video call component is upgraded and provides more powerful features. |

[](id:qa)

## FAQs

[](id:question1)

#### What should I do if I receive the error message "The package you purchased does not support this ability"?
The error message indicates that your app's **audio/video call capability package has expired or is not activated**. You can refer to [step 1](#step1) to claim or activate the audio/video call capability to continue using TUICallKit.

#### How do I purchase a package?
The audio/video call SDK **is currently in beta, with a 60-day free edition provided**. 

#### Will an invitee receive a call invitation immediately if the invitee goes offline and then online within the call invitation timeout duration?

- If the call invitation is started in a one-to-one chat, the invitee can receive the call invitation, and the TUIKit will automatically open the call invitation UI internally.
- If the call invitation is started in a group chat, the invitee will see the last 20 call invitations, and the TUICallKit will automatically open the group call UI.

#### What should I do if TUICallKit conflicts with an audio/video library that I have integrated?

TUICallKit and Tencent Cloud [audio/video libraries](https://intl.cloud.tencent.com/document/product/647/34615) cannot be integrated at the same time. Otherwise, symbol conflicts may occur. Do as follows:

- If you have integrated the `TXLiteAVSDK_TRTC` library, no symbol conflict will occur, and you can directly add dependency in the Podfile as follows:
```sh
pod 'TUICallKit'
```
- If you have integrated the `TXLiteAVSDK_Professional` library, symbol conflicts will occur, and you can add dependency in the Podfile as follows:
```sh
pod 'TUICallKit/Professional'
```
- If you have integrated the `TXLiteAVSDK_Enterprise` library, symbol conflicts will occur, and you are advised to upgrade it to `TXLiteAVSDK_Professional` before using `TUICallKit/Professional`.

#### What should I do if "ld: framework not found BoringSSL clang: error: linker command failed with exit code 1  sdk" is reported after TUICallKit is integrated?

The audio/video library on which TUICallKit relies currently does not support simulators. Please use real devices for demo running or debugging.

#### What should I do if I am using TUICalling of an earlier version and want to upgrade the IM-related components (TUIChat/TUIConversation/TUIGroup/TUIContact/TUISearch/TUIOfflinePush) separately?

The last stable CocoaPods version for TUICalling is v9.6.4. If you use CocoaPods for integration, you only need to upgrade the version numbers of the IM-related components. If you use manual integration, you only need to replace the source code of the IM-related components.

TUICalling and TUICallKit can interconnect with each other, and you are advised to upgrade to the latest TUICallKit.

[](id:feedback)


## Open Source Construction

You can find the TUICalling open source project before the upgrade [**here**](https://github.com/tencentyun/TUICalling/tree/open).
