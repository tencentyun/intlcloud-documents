TUIKit 4.8.50 and later versions provide video and voice call features for one-to-one and group chats based on [TRTC](https://intl.cloud.tencent.com/document/product/647/35078) and support interconnection between iOS and Android platforms. To quickly integrate TUIKit video and voice call features, follow the steps described in this document.




>!
>- In TUIKit 4.8.50 and later versions, the voice and video call features are integrated in the TUIKit component and designed based on the new signaling solution.
>- In versions earlier than TUIKit 4.8.50, the voice and video call features are integrated in the TUIKitDemo sample on the iOS client. **If you use the voice and video call features of an earlier version, we do not recommend that you upgrade the version to avoid compatibility issues.**

<span id="Step1"></span>

## Step 1: Enable the TRTC Service
1. Log in to the [IM console](https://console.cloud.tencent.com/im) and click the target application card to go to the basic configuration page of the application.
2. Click **Activate** in the **Tencent Real-Time Communication (TRTC)** area.
3. In the dialog box that appears, click **OK**.
 The system will create a TRTC application with the same SDKAppID as the current IM application in the [TRTC console](https://console.cloud.tencent.com/trtc). You can use the same account and authentication information for the two applications.

<span id="Step2"></span>
## Step 2: Configure the Engineering File
We recommend that you use source code to integrate TUIKit so that you can modify the source code to meet your business requirements.

```
implementation project(':tuikit')
```

<span id="Step3"></span>
## Step 3: Initialize TUIKit 
To initialize TUIKit, enter the SDKAppID generated in [Step 1](#Step1).
```
TUIKitConfigs configs = TUIKit.getConfigs();
TUIKit.init(this, SDKAPPID, configs);
```

<span id="Step4"></span>
## Step 4: Log In to TUIKit
Call the `login` API provided by TUIKit to log in to IM. For more information on how to generate UserSig, see [How to Generate Usersig](https://intl.cloud.tencent.com/document/product/647/35166).
```
TUIKit.login(userID, userSig, new IUIKitCallBack() {
	@Override
	public void onSuccess(Object data) {
		//Login successful
	}
	
	@Override
	public void onError(String module, final int code, final String desc) {
		// Login failed
	}
});
```

<span id="Step5"></span>
## Step 5: Initiate a Video or Voice Call 
When you tap **Video** or **Voice** on the chat UI, TUIKit displays the call invitation UI and sends a call request to the peer.

## Step 6: Answer a Video or Voice Call




- When an **online** user receives a call invitation, TUIKit displays the call accept UI. The user can answer or reject the call.

- When an **offline** user receives a call invitation, offline push is required to wake up the app call UI. For more information about offline push, see [Step 7](#Step7).

  <span id="Step7"></span>

## Step 7: Offline Push
To implement offline push for voice and video calls, follow these steps:
1. Configure offline push for the app. For more information, see [Offline Push Configuration](https://intl.cloud.tencent.com/document/product/1047/34336).
2. Upgrade TUIKit to 4.9.1 or later.
3. Use TUIKit to initiate a call invitation. An offline push message will be generated by default. For more information about the message generation logic, see the `sendOnlineMessageWithOfflinePushInfo` method in the [TRTCAVCallImpl.java](https://github.com/tencentyun/TIMSDK/blob/master/Android/tuikit/src/main/java/com/tencent/liteav/model/TRTCAVCallImpl.java) class.
4. After the peer receives the offline push message, refer to the `redirect` method in the [OfflineMessageDispatcher.java](https://github.com/tencentyun/TIMSDK/blob/master/Android/app/src/main/java/com/tencent/qcloud/tim/demo/thirdpush/OfflineMessageDispatcher.java) class to wake up the call UI.

## FAQs
### 1. What should I be aware of if I have created the TRTC and IM SDKAppIDs and want to integrate the IM SDK and TRTC SDK at the same time?
If you have created the TRTC and IM SDKAppIDs, you cannot use the same account or authentication information for these two applications. You need to generate a UserSig corresponding to the TRTC SDKAppID to perform authentication. For more information on how to generate UserSig, see [How to Generate Usersig](https://intl.cloud.tencent.com/document/product/647/35166).
After obtaining the TRTC SDKAppID and UserSig, you need to replace the corresponding values in the `TRTCAVCallImpl` source code.
```
 private void enterTRTCRoom() {
	 ...
	 TRTCCloudDef.TRTCParams TRTCParams = new TRTCCloudDef.TRTCParams(mSdkAppId, mCurUserId, mCurUserSig, mCurRoomID, "", "");
	 ...
 }
```

### 2. How long is the default call invitation timeout time? How can I modify the default timeout time?
The default call invitation timeout time is 30s. You can modify the `TIME_OUT_COUNT` field in `TRTCAVCallImpl` to customize the timeout time.

### 3. Will an invitee receive a call invitation if the invitee goes offline and then online within the call invitation timeout time?
- If the call invitation is initiated in a one-to-one chat, the invitee can receive the call invitation.
- If the call invitation is initiated in a group chat, the invitee cannot receive the call invitation.
