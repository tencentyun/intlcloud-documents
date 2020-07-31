In version 4.8.50 and later versions, the TUIKit component implements the voice call and video call features for one-to-one chats and group chats based on [TRTC](https://intl.cloud.tencent.com/document/product/647/35078) and implements intercommunication between iOS and Android. This document will show you how to complete integration in a few easy steps.
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
>- In TUIKit 4.8.50 and later versions, the voice call and video call features are directly integrated into the TUIKit component and designed based on a new signaling scheme.
>- In versions earlier than TUIKit 4.8.50, the voice call and video call features are integrated in the iOS TUIKitDemo. **The features in the new and old versions are not compatible. If you have already used the voice and video call features of previous versions, we do not recommend that you upgrade. Otherwise, compatibility issues may arise**.

<span id="Step1"></span>
## Step 1: Activate the TRTC Service
1. Log in to the [IM Console](https://console.cloud.tencent.com/im) and click the target app card to go to the basic configuration page of the app.
2. Click **Activate Now** in the **Activate Tencent TRTC Service** area.
3. In the displayed dialog box for activating the TRTC service, click **OK**.
 On the [TRTC console](https://console.cloud.tencent.com/trtc), the system will create a TRTC app with the same SDKAppID as the current IM app for you. The two apps can share account and authentication data with each other.
 
<span id="Step2"></span>
## Step 2: Configure the Project File

1. Add the following content in the podfile file:
 ```
use_modular_headers!
// The earliest TUIKit version that supports TRTC is 4.8.50.
pod 'TXIMSDK_TUIKit_iOS'
```
2. Run the following command to download the third-party database to the current project.
```
pod install
```


<span id="Step3"></span>
## Step 3: Initialize the TUIKit 
To initialize the TUIKit, you need to pass in the SDKAppID generated in [Step 1](#Step1).
```
[[TUIKit sharedInstance] setupWithAppId:SDKAppID];
```

<span id="Step4"></span>
## Step 4: Log In to the TUIKit
To log in to IM, you need to use the `login` API provided by the TUIKit. For more information on how to generate the UserSig, see [How to Calculate UserSig](https://intl.cloud.tencent.com/document/product/647/35166).
```
[[TUIKit sharedInstance] login:@"userID" userSig:@"userSig" succ:^{
     NSLog(@"-----> login succeeded");
} fail:^(int code, NSString *msg) {
     NSLog(@"-----> login failed");
}];
```

<span id="Step5"></span>
## Step 5: Initiate a Video or Voice Call

<img style="width:180px" src="https://main.qcloudimg.com/raw/17698afaedf9ba86045c03ef85159bec.png"  /> 

When a user clicks the video call or voice call feature on the chat interface, the TUIKit will automatically display the call invitation UI to initiate a call invitation request to the other party of the chat.

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
- When an **offline** user receives a call invitation, the user will not be aware of it, because call invitations currently cannot be pushed offline.

## FAQs
### 1. Assume that the TRTC SDKAppID and IM SDKAppID have both already been created. Are there any special instructions for integrating the IM SDK and TRTC SDK simultaneously?

If the TRTC SDKAppID and IM SDKAppID have both already been created, meaning that the SDKAppIDs are inconsistent, then the account and authentication data of the two apps cannot be shared. You need to generate the corresponding UserSig for authentication of the TRTC SDKAppID. For more information on how to generate the UserSig, see [How to Calculate UserSig](https://intl.cloud.tencent.com/document/product/647/35166).
 
After obtaining the TRTC SDKAppID and UserSig, you need to modify the following code in the source code of `TRTCCall+Room.swift`:
```
 func enterRoom() {
	 let param = TRTCParams()
	 // TRTC SDKAppID
	 param.sdkAppId = 1000000000 
	 // UserSig generated by TRTC SDKAppID
	 param.userSig = "userSig"
  }
```

 
### 2. What is the default timeout threshold for a call invitation? How can I modify the default timeout threshold?
The default timeout threshold for a call invitation is 30s. You can set the timeout threshold by modifying the `timeOut` field in `TRTCCall.swift`.
 
### 3. Before the invitation times out, if the invitee goes offline and then comes online again, can the invitee still receive the invitation?
- If it is a one-to-one call invitation, the invitee can still receive the call invitation after going offline and then coming back online.
- If it is a group call invitation, the invitee cannot receive the call invitation after going offline and then coming back online.
