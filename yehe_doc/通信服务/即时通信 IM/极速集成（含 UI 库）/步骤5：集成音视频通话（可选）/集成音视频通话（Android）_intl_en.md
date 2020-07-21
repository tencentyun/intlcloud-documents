In version 4.8.50 and later versions, the TUIKit component provides a voice and video call feature for one-to-one chats and group chats based on [TRTC](https://intl.cloud.tencent.com/document/product/647/35078) and implements intercommunication between iOS and Android. This document shows you how to achieve quick integration in a few simple steps.
<table style="text-align:center;vertical-align:middle;width: 400px">
  <tr>
    <th style="text-align:center;" width="180px"><b>Video Call<br></b></th>
    <th style="text-align:center;" width="180px"><b>Voice Call</b><br></th>
  </tr>
  <tr>
    <td><img style="width:180px" src="https://main.qcloudimg.com/raw/59713f77fc8e0dbe4787288aba0898f7.jpeg"  />    </td>
    <td><img style="width:180px" src="https://main.qcloudimg.com/raw/9c20238b4af83283fb677059b8693380.jpeg" />     </td>
	 </tr>
</table>

>!
>- In TUIKit 4.8.50 and later versions, the voice and video call feature is directly integrated into the TUIKit component and designed based on a new signaling scheme.
>- In versions earlier than TUIKit 4.8.50, the voice and video call feature is integrated in the iOS TUIKitDemo. **This feature is not compatible with later and earlier versions. If you have already used the voice and video call feature of earlier versions, we do not recommend upgrading to a later version. Otherwise, compatibility issues may arise**.

<span id="Step1"></span>
## Step 1: Activate the TRTC Service
1. Log in to the [IM console](https://console.cloud.tencent.com/im) and click the target app card to go to the basic configuration page of the app.
2. Click **Activate Now** in the **Activate Tencent TRTC Service** area.
3. In the displayed dialog box for activating the TRTC service, click **OK**.
 In the [TRTC console](https://console.cloud.tencent.com/trtc), the system will create a TRTC app with the same SDKAppID as the current IM app. The two apps can share account and authentication data.

<span id="Step2"></span>
## Step 2: Configure the Project File
We recommend that you use the source-code integrated TUIKit so that you can modify the source code to meet your own business needs.

```
implementation project(':tuikit')
```

<span id="Step3"></span>
## Step 3: Initialize the TUIKit 
To initialize the TUIKit, you need to pass in the SDKAppID generated in [Step 1](#Step1).
```
TUIKitConfigs configs = TUIKit.getConfigs();
TUIKit.init(this, SDKAPPID, configs);
```

<span id="Step4"></span>
## Step 4: Log in to the TUIKit
To log in to IM, you need to call the `login` API provided by the TUIKit. For more information on how to generate the UserSig, see [How to Calculate UserSig](https://intl.cloud.tencent.com/document/product/647/35166).
```
TUIKit.login(userID, userSig, new IUIKitCallBack() {
	@Override
	public void onSuccess(Object data) {
		// Login successful
	}
	
	@Override
	public void onError(String module, final int code, final String desc) {
		// Login failed
	}
});
```

<span id="Step5"></span>
## Step 5: Initiate a Video or Voice Call
<img style="width:180px" src="https://main.qcloudimg.com/raw/17698afaedf9ba86045c03ef85159bec.png"  /> 

When a user clicks the video call or voice call feature on the chat interface, the TUIKit will automatically display the call invitation UI to initiate a call invitation request to the other party in the chat.

## Step 6: Accept the Video or Voice Call

<table style="text-align:center;vertical-align:middle;width: 400px">
  <tr>
    <th style="text-align:center;" width="180px"><b>Accept a Video Call<br></b></th>
    <th style="text-align:center;" width="180px"><b>Accept a Voice Call</b><br></th>
  </tr>
  <tr>
    <td><img style="width:180px" src="https://main.qcloudimg.com/raw/d4f0d5c7f208932055588c1ac59b9a91.jpg"  />    </td>
    <td><img style="width:180px" src="https://main.qcloudimg.com/raw/a621580a0553271c70a9fec0738400c5.jpg" />     </td>
	 </tr>
</table>

- When an **online** user receives a call invitation, the TUIKit will automatically display the incoming call UI, and the user can choose to accept or reject the call.
- When an **offline** user receives a call invitation, the user will not be notified of it. Call invitations currently do not support offline push capabilities.

## FAQs
### 1. Assuming that the TRTC SDKAppID and IM SDKAppID have already been created separately, are there any special instructions for integrating the IM SDK and TRTC SDK?
If the TRTC SDKAppID and IM SDKAppID have been created separately, their SDKAppIDs are inconsistent, and the apps cannot share account and authentication data. You need to generate the corresponding UserSig for authentication of the TRTC SDKAppID. For more information on how to generate the UserSig, see [How to Calculate UserSig](https://intl.cloud.tencent.com/document/product/647/35166).
After obtaining the TRTC SDKAppID and UserSig, you need to replace the value in the `TRTCAVCallImpl` source code:
```
 private void enterTRTCRoom() {
	 ...
	 TRTCCloudDef.TRTCParams TRTCParams = new TRTCCloudDef.TRTCParams(mSdkAppId, mCurUserId, mCurUserSig, mCurRoomID, "", "");
	 ...
 }
```
 
### 2. What is the default timeout threshold for a call invitation? How can I modify the default timeout threshold?
The default timeout threshold for a call invitation is 30s. You can set the timeout threshold by modifying the `TIME_OUT_COUNT` field in `TRTCAVCallImpl`.
 
### 3. Before the invitation times out, if the invitee goes offline and then comes online again, will the invitee receive the invitation?
- If it is a one-to-one call invitation, the invitee can still receive the call invitation after going offline and then online again.
- If it is a group call invitation, the invitee cannot receive the call invitation after going offline and then online again.
