## Environment Requirements
- Xcode 10 or later
- iOS 9.0 or later

## CocoaPods Integration
TUIKit supports modular integration starting from version 5.7.1435. You can choose modules for integration according to your needs.

1. According to your business requirements, add the corresponding TUI components to your Podfile. For example, you can add `pod 'TUIChat'` to implement the chat feature, add `pod 'TUIConversation'` to implement the conversation list feature, and add `pod 'TUICallKit'` to implement the audio/video call feature. TUI components are independent of each other, and adding or removing them does not affect project compilation.
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
# Integrate the search feature (To use this feature, you need to purchase the Ultimate edition)
pod 'TUISearch'
# Integrate the audio/video call feature
pod 'TUICallKit'
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
 <img src="https://qcloudimg.tencent-cloud.cn/raw/6e34bd1058ab0f84109bed307a38e134.png" width = "300"/>


## Quick Build
Instant messaging software usually consists of several basic UIs such as the conversation list, chat window, contacts, and audio/video call UIs. It only takes a few lines of code to build these UIs in your project. The process is as follows:

### Step 1. Log in to TUIKit
```objectivec
#import "TUILogin.h"
// You can click Log in on the user UI to log in to TUIKit
- (void)loginSDK:(NSString *)userID userSig:(NSString *)sig succ:(TSucc)succ fail:(TFail)fail {
    // You can obtain the SDKAppID in the IM console
    // For how to generate a UserSig, see GenerateTestUserSig.h
    [TUILogin login:SDKAppID userID:userID userSig:sig succ:^{
        NSLog(@"-----> login succeeds");
    } fail:^(int code, NSString *msg) {
        NSLog(@"-----> login fails");
    }];
}
```

### Step 2. Build the conversation list UI
To build the conversation list UI, you only need to create a `TUIConversationListController` object. The conversation list reads recent contacts from the database. When a user clicks a contact, `TUIConversationListController` calls back the event to the upper layer.

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
TUI components allow users to start audio/video calls in chat UIs and can be quickly integrated with a few steps:
<table style="text-align:center;vertical-align:middle;width: 800px">
  <tr>
    <th style="text-align:center;" ><b>Video Call<br></b></th>
    <th style="text-align:center;"><b>Audio Call</b><br></th>
  </tr>
  <tr>
    <td><img src="https://qcloudimg.tencent-cloud.cn/raw/b9f362503d25179db6f75fc91cfd000a.jpg"/></td>
    <td><img src="https://qcloudimg.tencent-cloud.cn/raw/2f037d7de8270c0edef68c0b829465ec.png"/></td>
	 </tr>
</table>

1. **Activate the TRTC service**
	1. Log in to the [IM console](https://console.cloud.tencent.com/im) and click the target app card to go to the basic configuration page of the app.
	2. Click **Free trial** under **Activate Tencent Real-Time Communication (TRTC)** to activate the 7-day free trial service of TUICallKit.
	3. Click **Confirm** in the pop-up dialog box. A TRTC app with the same SDKAppID as the IM app will be created in the [TRTC console](https://console.cloud.tencent.com/trtc). You can use the same account and authentication information for IM and TRTC.

2. **Integrate the TUICallKit component**
Add the following content to your Podfile:
```objectivec
// Integrate the TRTCCalling component
pod 'TUICallKit'                  
```

3. **Start and answer a video or audio call**
<table style="text-align:center;vertical-align:middle;width: 800px">
  <tr>
    <th style="text-align:center;" ><b>Starting a Call via a Message Page<br></b></th>
    <th style="text-align:center;" ><b>Starting a Call via a Contact Profile Page<br></b></th>
  </tr>
  <tr>
    <td><img style="width:400px" src="https://qcloudimg.tencent-cloud.cn/raw/b7b6aca5e1f3f3e5d775cfa3316e30f4.png"/></td>
    <td><img style="width:400px" src="https://qcloudimg.tencent-cloud.cn/raw/31fd1d8fb263e953825cf5531a24ffca.png"/></td>
     </tr>
</table>

	- After integrating the TUICallKit component, the chat UI and contact profile UI display the **Video Call** and **Audio Call** buttons by default. When a user clicks either of the buttons, TUIKit automatically displays the call invitation UI and sends the call invitation request to the callee.
	- When an **online** user receives a call invitation, TUIKit automatically displays the call receiving UI, where the user can answer or reject the call.
	- When an **offline** user receives a call invitation, offline push is required to wake up the app call. For more information about offline push, see [Add the offline push feature](#Step5.4).

4. **Add offline push**
Before using offline push, you need to activate the [IM offline push](https://intl.cloud.tencent.com/document/product/1047/39157) service.
For related app configuration, see [Integrating TUIOfflinePush and Running the Offline Push Feature](https://intl.cloud.tencent.com/document/product/1047/47949).

**After the configuration is completed, when you click a received audio/video call notification pushed offline, TUICallKit automatically opens the audio/video call invitation UI.**


## FAQs
1. What should I do when I receive the message "target has transitive dependencies that include statically linked binaries"?
If this error occurs during the `pod` process, this is because TUIKit is using a third-party static library. You need to comment out `use_frameworks!` in your Podfile.
If you need to use `use_frameworks!`, use CocoaPods 1.9.0 or a later version for `pod install` and modify it as follows:
```
use_frameworks! :linkage => :static
```
If you use Swift, change the reference of the header file to the reference format of @import module name.

2. What should I do if TUICallKit conflicts with the integrated audio and video library?
Do not integrate different Tencent Cloud [audio and video libraries](https://intl.cloud.tencent.com/document/product/647/34615) at the same time to avoid symbol conflicts. If you use a library not of the [TRTC](https://intl.cloud.tencent.com/document/product/647/34615#TRTC) version, we recommend that you remove it and integrate the TUICallKit Professional version via `pod`. The audio and video library of the [LiteAV_Professional](https://intl.cloud.tencent.com/document/product/647/34615#.E4.B8.93.E4.B8.9A.E7.89.88.EF.BC.88professional.EF.BC.89) version contains all basic audio and video capabilities. **The audio and video library of the [LiteAV_Enterprise](https://intl.cloud.tencent.com/document/product/647/34615#Enterprise) version cannot coexist with TUICallKit.** For the detailed solution, see [here](https://intl.cloud.tencent.com/document/product/1047/50024#.E5.B8.B8.E8.A7.81.E9.97.AE.E9.A2.98).

3. How long is the default call invitation timeout duration?
The default call invitation timeout duration is 30 seconds.

4. Will an invitee receive a call invitation immediately if the invitee goes offline and then online within the call invitation timeout duration?

   - If the call invitation is started in a one-to-one chat, the invitee can receive the call invitation, and the TUIKit will automatically open the call invitation UI internally.
   - If the call invitation is started in a group chat, the TUIKit will automatically pull the call invitations of the last 30 seconds and open the group call UI.

