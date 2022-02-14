## Introduction to TUIKit
TUIKit is a set of TUI components based on IM SDKs. It provides features such as the conversation, chat, search, relationship chain, group, and audio/video call features. You can use these TUI components to quickly build your own business logic.
![](https://qcloudimg.tencent-cloud.cn/raw/b250365ff88461f38c9f57afb3b2eadc.png)

## Importing TUIKit

### Environment requirements

- Xcode 10 or above
- iOS 9.0 or above


### CocoaPods integration

TUIKit supports modular integration starting from version 5.7.1435. You can choose modules for integration according to your needs.

1. According to your business requirements, add the corresponding TUI components to your Podfile. For example, you can add `pod 'TUIChat'` to include the chat feature, add `pod 'TUIConversation'` to include the conversation list feature, and add `pod 'TUICalling'` to include the audio/video call feature. TUI components are independent of each other, and adding or removing them does not affect project compilation.
```
# Prevent `*.xcassets` in TUI components from conflicting with your project.
install! 'cocoapods', :disable_input_output_paths => true  

# TUI components are dependent on static libraries. Therefore, you need to mask the following configuration. If an error is reported, see the explanation in the FAQs part.
# use_frameworks!

# Integrate the chat feature
pod 'TUIChat'
# Integrate the conversation list feature
pod 'TUIConversation'
# Integrate the relationship chain feature
pod 'TUIContact'
# Integrate the group feature
pod 'TUIGroup'
# Integrate the search feature (To use this feature, you need to purchase the Flagship Edition package.)
pod 'TUISearch'
# Integrate the audio/video call feature
pod 'TUICalling'
```
2. Run the following command to install TUI components.
```bash
pod install
```
 If you cannot install the latest TUIKit version, run the following command to update the local CocoaPods repository list:
```bash
 pod repo update
```
**Expected TUI component integration result**:<br>
 <img src="https://qcloudimg.tencent-cloud.cn/raw/083905832dcc7f8cc1d14ddaf15232e9.jpg" width = "400"/>
>? After TUI component integration, folders are displayed in hierarchical mode, making it easy for you to read and modify source code.
</ol></li>

## Quick Build

Instant messaging software usually consists of several basic UIs such as the conversation list, chat window, friend list, and audio/video call UIs. It only takes a few lines of code to build these UIs in your project. The process is as follows:

### Step 1. Log in to TUIKit
```objectivec
#import "TUILogin.h"
// You can initialize TUIKit during program startup
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    [TUILogin initWithSdkAppID:SDKAppID]; // You can obtain the SDKAppID in the IM console
}

// You can click Login on the user UI to log in to TUIKit
- (void)login:(NSString *)identifier userSig:(NSString *)sig succ:(TSucc)succ fail:(TFail)fail
{
    [TUILogin login:identifier userSig:sig succ:^{
        NSLog(@"-----> login succeeds");
    } fail:^(int code, NSString *msg) {
        NSLog(@"-----> login fails");
    }];
}
```

### Step 2. Build a conversation list

To create a conversation list, you only need to create a `TUIConversationListController` object. The conversation list reads recent contacts from the database. When a user clicks a contact, `TUIConversationListController` calls back the event to the upper layer.

```java
@implementation ConversationController // Your own ViewController
- (void)viewDidLoad {
    [super viewDidLoad];
    // Create TUIConversationListController
    TUIConversationListController *conv = [[TUIConversationListController alloc] init];
    conv.delegate = self;
    // Add TUIConversationListController to your own ViewController
    [self addChildViewController:conv];
    [self.view addSubview:conv.view];
}

- (void)conversationListController:(TUIConversationListController *)conversationController didSelectConversation:(TUIConversationCell *)conversation
{
    // Conversation list click event, typically, opening the chat UI
}
@end
```

### Step 3. Build the chat UI

During chat UI initialization, the upper layer needs to pass in the conversation information of the current chat UI. The sample code is as follows:

```java
@implementation ChatViewController // Your own ViewController
- (void)viewDidLoad {
   // Create conversation information
   TUIChatConversationModel *data = [[TUIChatConversationModel alloc] init];
   data.userID = @"userID";    
   // Create TUIC2CChatViewController
   TUIC2CChatViewController *vc = [[TUIC2CChatViewController alloc] init];  
   [vc setConversationData:data];
   // Add TUIC2CChatViewController to your own ViewController
   [self addChildViewController:conv];
   [self.view addSubview:conv.view];
}
@end
```
`TUIC2CChatViewController` will automatically pull and display the historical messages of the user.

### Step 4. Build the contacts UI

The contacts UI does not require other dependencies. You only need to create the object and display it.

```java
@implementation ContactController // Your own ViewController
- (void)viewDidLoad {    
   // Create TUIContactController
   TUIContactController *vc = [[TUIContactController alloc] init];
   // Add TUIContactController to your own ViewController
   [self addChildViewController:conv];
   [self.view addSubview:conv.view];
}
@end
```

### Step 5. Build the audio/video call feature

TUI components allow users to initiate audio/video calls in chat UIs and can be quickly integrated with a few steps:
<table style="text-align:center;vertical-align:middle;width: 600px">
  <tr>
    <th style="text-align:center;" ><b>Video Call<br></b></th>
    <th style="text-align:center;"><b>Audio Call</b><br></th>
  </tr>
  <tr>
    <td><img  src="https://qcloudimg.tencent-cloud.cn/raw/f7c246e9f646e199af88c64308c326c7.png"  />    </td>
    <td><img  src="https://qcloudimg.tencent-cloud.cn/raw/6e3369c96b316f5a65d4f6760412427f.png" />     </td>
     </tr>
</table>


1. **Activate the TRTC service:**
	1. Log in to the [IM console](https://console.cloud.tencent.com/im) and click the target app card to go to the basic configuration page of the app.
	2. Click **Activate** under **Activate Tencent Real-Time Communication (TRTC)**.
	3. Click **Confirm** in the pop-up dialog box.
	 A TRTC app with the same SDKAppID as the IM app will be created in the [TRTC console](https://console.cloud.tencent.com/trtc). You can use the same account and authentication information for IM and TRTC.
2. **Integrate the TUICalling component:**
Add the following content to your Podfile:
```objectivec
// Integrate the TRTCCalling component
pod 'TUICalling'                  
```
3. **Initiate and answer a video or audio call:**
<table style="text-align:center;vertical-align:middle;width: 600px">
  <tr>
        <th style="text-align:center;"><b>Initiate an Audio/Video Call<br></b></th>
    <th style="text-align:center;"><b>Answer a Video Call<br></b></th>
    <th style="text-align:center;"><b>Answer an Audio Call</b><br></th>
  </tr>
  <tr>
        <td><img style="width:210px" src="https://qcloudimg.tencent-cloud.cn/raw/f7d4b75ff1f299e655805518984a6e58.png"  />    </td>
    <td><img style="width:200px" src="https://qcloudimg.tencent-cloud.cn/raw/e201ea282ef9e757df2ade9bd8c71955.png"  />    </td>
    <td><img style="width:200px" src="https://qcloudimg.tencent-cloud.cn/raw/314875a92058f1e46296f458767cb0ba.png" />     </td>
     </tr>
</table>


	- After integrating the TUICalling component, the chat UI displays the **Video Call** and **Audio Call** buttons by default. When a user clicks either of the buttons, TUIKit automatically displays the call invitation UI and sends the call invitation request to the callee.
	- When an **online** user receives a call invitation, TUIKit automatically displays the call receiving UI, where the user can answer or reject the call.
	- When an **offline** user receives a call invitation, offline push is required to wake up the App call. For more information about offline push, see [Add the offline push feature](#Step5.4).
4. **Add the offline push feature:**[](id:Step5.4)
To implement offline push for audio/video calls, follow these steps:
	1. Configure offline push for App.
	2. Integrate the TUICalling component via `pod`.
	3. When a user initiates a call, `TUICalling` sets offline push with the push title "You are invited to a call" for audio/video calls by default. If you want to modify the push title, modify the source code of the `getOfflinePushInfoWithInviteeList` function in [TRTCCalling+Signal.m](https://github.com/tencentyun/TIMSDK/blob/master/iOS/TUIKit/TUICalling/iOS/Source/model/Impl/TRTCCalling%2BSignal.m).
```objectivec
- (V2TIMOfflinePushInfo *)getOfflinePushInfoWithInviteeList:(NSArray *)inviteeList callID:(NSString *)callID groupid:(NSString *)groupid roomid:(UInt32)roomid{
		....
		V2TIMOfflinePushInfo *info = [[V2TIMOfflinePushInfo alloc] init];
		info.desc = "Custom push title";
		....
		return info;
}
```
	4. After the peer receives the offline push message, the peer can initiate the call UI by calling the `onReceiveOfflinePushEntity` function in [AppDelegate+Push.m](https://github.com/tencentyun/TIMSDK/blob/master/iOS/Demo/TUIKitDemo/AppDelegate%2BPush.m).


## FAQs

### 1. Why do I receive the message "target has transitive dependencies that include statically linked binaries"?

- If this error occurs during the `pod` process, this is because TUIKit is using a third-party static library. You need to comment out `use_frameworks!` in your Podfile.
- If you need to use `use_frameworks!`, use CocoaPods 1.9.0 or a later version for `pod install` and modify it as follows:
```
use_frameworks! :linkage => :static
```
- If you use Swift, change the reference of the header file to the reference format of @import module name.

### 2. What can I do if TUICalling conflicts with the integrated audio and video library?
Do not integrate different Tencent Cloud [audio and video libraries](https://intl.cloud.tencent.com/document/product/647/34615) at the same time to avoid symbol conflicts. If you use a library not of the [TRTC](https://intl.cloud.tencent.com/document/product/647/34615#TRTC) version, we recommend that you remove it and integrate the TUICalling Professional version via `pod`. The audio and video library of the [LiteAV_Professional](https://intl.cloud.tencent.com/document/product/647/34615#.E4.B8.93.E4.B8.9A.E7.89.88.EF.BC.88professional.EF.BC.89) version contains all basic audio and video capabilities.
**The audio and video library of the [LiteAV_Enterprise](https://intl.cloud.tencent.com/document/product/647/34615#Enterprise) version cannot coexist with TUICalling.**

### 3. What should I be aware of if I have created the TRTC and IM SDKAppIDs and want to integrate the IM SDK and TRTC SDK at the same time?

If you have created the TRTC and IM SDKAppIDs, you cannot use the same account or authentication information for these two apps. You need to generate a UserSig corresponding to the TRTC SDKAppID to perform authentication. For more information on how to generate UserSig, see [How to Generate Usersig](https://intl.cloud.tencent.com/document/product/647/35166).

After obtaining the TRTC SDKAppID and UserSig, you need to modify the following code in the [TRTCCalling.m](https://github.com/tencentyun/TIMSDK/blob/master/iOS/TUIKit/TUICalling/iOS/Source/model/Impl/TRTCCalling.m) source code:
```
 - (void)enterRoom {
     TRTCParams *param = [[TRTCParams alloc] init];
     // TRTC SDKAppID
     param.sdkAppId = 1000000000 
     // UserSig generated based on the TRTC SDKAppID
     param.userSig = "userSig"
}
```

### 4. How long is the default call invitation timeout duration? How can I modify the default timeout duration?
The default call invitation timeout duration is 30s. You can modify the `SIGNALING_EXTRA_KEY_TIME_OUT` field in [TRTCCallingModel.m](https://github.com/tencentyun/TIMSDK/blob/master/iOS/TUIKit/TUICalling/iOS/Source/model/Impl/TRTCCallingModel.m) to customize the timeout duration.

### 5. Will an invitee receive a call invitation if the invitee goes offline and then online within the call invitation timeout duration?
- If the call invitation is initiated in a one-to-one chat, the invitee can receive the call invitation.
- If the call invitation is initiated in a group chat, the invitee cannot receive the call invitation.

