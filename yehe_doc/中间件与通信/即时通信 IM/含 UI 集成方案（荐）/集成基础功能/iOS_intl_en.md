TUIKit supports modular integration starting from version 5.7.1435. You can integrate modules for integration according to your needs.
Starting from version 6.9.3557, TUIKit provides a new set of minimalist version UI components. The previous version UI components are still retained, which are called the classic version UI components. You can choose either the classic or minimalist version as needed.

For more information about TUIKit components, see [here](https://intl.cloud.tencent.com/document/product/1047/50062).

The following describes how to integrate TUIKit components. 

## Environment Requirements
- Xcode 10 or later
- iOS 9.0 or later

## CocoaPods Integration
1. Install CocoaPods
Enter the following command in a terminal (you need to install Ruby on your Mac first):
```
sudo gem install cocoapods
```
2. Create a Podfile
Go to the path where the project is located and run the following command. Then, a Podfile will appear under the project path.
```
pod init
```
3. Add the corresponding TUIKit components to your Podfile according to your business requirements. TUIKit components are independent of each other, and adding or removing them does not affect project compilation. The following is a Podfile configuration example:
<dx-tabs>

::: Classic version
  ```
  # Uncomment the next line to define a global platform for your project
  # ...
  
  # Prevent `*.xcassets` in TUIKit from conflicting with your project
  install! 'cocoapods', :disable_input_output_paths => true
  
  # Replace `your_project_name` with your actual project name
  target 'your_project_name' do
    # Comment the next line if you don't want to use dynamic frameworks
    # TUIKit components are dependent on static libraries. Therefore, you need to mask the configuration.
    # use_frameworks!
  
    # Enable modular headers as needed. Only after you enable modular headers, the Pod module can be imported using @import.
    # use_modular_headers!
    
    # Integrate the chat feature
    pod 'TUIChat/UI_Classic' 
    # Integrate the conversation list feature
    pod 'TUIConversation/UI_Classic'
    # Integrate the relationship chain feature
    pod 'TUIContact/UI_Classic'
    # Integrate the group feature
    pod 'TUIGroup/UI_Classic' 
    # Integrate the search feature (To use this feature, you need to purchase the Ultimate edition)
    pod 'TUISearch/UI_Classic' 
    # Integrate the offline push feature
    pod 'TUIOfflinePush'
    # Integrate the audio/video call feature
    pod 'TUICallKit'
		
  end
  ```
:::

::: Minimalist version
  ```
  # Uncomment the next line to define a global platform for your project
  # ...
  
  # Prevent `*.xcassets` in TUIKit from conflicting with your project
  install! 'cocoapods', :disable_input_output_paths => true
  
  # Replace `your_project_name` with your actual project name
  target 'your_project_name' do
    # Comment the next line if you don't want to use dynamic frameworks
    # TUIKit components are dependent on static libraries. Therefore, you need to mask the configuration.
    # use_frameworks!
  
    # Enable modular headers as needed. Only after you enable modular headers, the Pod module can be imported using @import.
    # use_modular_headers!
    
    # Integrate the chat feature
    pod 'TUIChat/UI_Minimalist' 
    # Integrate the conversation list feature
    pod 'TUIConversation/UI_Minimalist'
    # Integrate the relationship chain feature
    pod 'TUIContact/UI_Minimalist'
    # Integrate the group feature
    pod 'TUIGroup/UI_Minimalist' 
    # Integrate the search feature (To use this feature, you need to purchase the Ultimate edition)
    pod 'TUISearch/UI_Minimalist' 
    # Integrate the offline push feature
    pod 'TUIOfflinePush'
    # Integrate the audio/video call feature
    pod 'TUICallKit'
		
  end
  ```
:::
</dx-tabs>
> ?1. If you run `pod 'TUIChat'` without specifying the classic or minimalist version, the two versions of UI components will be integrated by default. 
> 2. The classic and minimalist versions of UI components cannot be used together. If you integrate multiple components, all the integrated components must be of the same version: classic or minimalist.
> For example, the classic version TUIChat must be used together with the classic version TUIConversation, TUIContact, and TUIGroup, and the minimalist version TUIChat must be used together with the minimalist version TUIConversation, TUIContact, and TUIGroup.
> 3. If you use Swift, enable `use_modular_headers!` and change the reference of the header file to the reference format of @import module name.
> 
4. Run the following command to install TUIKit.
```bash
pod install
```
If you cannot install the latest TUIKit version, run the following command to update the local CocoaPods repository list:
```bash
pod repo update
```
Then run the following command to update the Pod version of the component library:
```bash
pod update
```
  After all TUIKit components are integrated, the project structure is as follows:
  <img src="https://qcloudimg.tencent-cloud.cn/raw/42a839342ac69e1d87952a05458df0e4.png" style="zoom:50%;"/> 

## Quick Build
Instant messaging software usually consists of several basic UIs such as the conversation list, chat window, contacts, and audio/video call UIs. It only takes a few lines of code to build these UIs in your project. The process is as follows:

> ? About TUIKit component features:
> 1. For the Hands-on tutorial video, see [TUIKit Quick Integration (iOS)](https://cloud.tencent.com/edu/learning/course-3130-56699).
> 2. If you want to learn more, you can [download and run TUIKitDemo source code](https://github.com/TencentCloud/TIMSDK/tree/master/iOS), where you can find samples of frequently used features.


### Step 1. Log in to TUIKit
You need to log in to TUIKit before you can use the component features properly. To log in to TUIKit, click `Login` on your app.
You need to create an app and obtain the SDKAppID in the [Chat console](https://console.cloud.tencent.com/im). `userSig` needs to be calculated according to rules. For operation details, see [Get Started](https://intl.cloud.tencent.com/document/product/1047/45913).

Sample code:
```objectivec
#import "TUILogin.h"
 
- (void)loginSDK:(NSString *)userID userSig:(NSString *)sig succ:(TSucc)succ fail:(TFail)fail {
    [TUILogin login:SDKAppID userID:userID userSig:sig succ:^{
        NSLog(@"Login successful");
    } fail:^(int code, NSString *msg) {
        NSLog(@"Login failed");
    }];
}
```

### Step 2. Build the conversation list UI
To build the conversation list UI, you only need to create a `TUIConversationListController` object. The conversation list reads recent contacts from the database. When a user clicks a contact, `TUIConversationListController` calls back the `didSelectConversation` event to the upper layer.

Sample code:

<dx-tabs>
::: Classic version
```java
#import "TUIConversationListController.h"

// ConversationController is your own ViewController
@implementation ConversationController 
- (void)viewDidLoad {
    [super viewDidLoad];
    // TUIConversationListController
    TUIConversationListController *vc = [[TUIConversationListController alloc] init];
    vc.delegate = self;
    // Add TUIConversationListController to your own ViewController
    [self addChildViewController:vc];
    [self.view addSubview:vc.view];
}

- (void)conversationListController:(TUIConversationListController *)conversationController 
            didSelectConversation:(TUIConversationCell *)conversation
{
    // Conversation list click event, typically, opening the chat UI
}
@end
```
:::

::: Minimalist version
```java
#import "TUIConversationListController_Minimalist.h"

// ConversationController is your own ViewController
@implementation ConversationController
- (void)viewDidLoad {
    [super viewDidLoad];
    // TUIConversationListController_Minimalist
    TUIConversationListController_Minimalist *vc = [[TUIConversationListController_Minimalist alloc] init];
    vc.delegate = self;
    // Add TUIConversationListController_Minimalist to your own ViewController
    [self addChildViewController:vc];
    [self.view addSubview:vc.view];
}

- (void)conversationListController:(TUIConversationListController_Minimalist *)conversationController 
            didSelectConversation:(TUIConversationCell *)conversation
{
    // Conversation list click event, typically, opening the chat UI
}
@end
```
:::
</dx-tabs>

### Step 3. Build the chat panel
During chat panel initialization, the upper layer needs to pass in the conversation information of the current chat panel.

Sample code:
<dx-tabs>
::: Classic version
```java
#import "TUIC2CChatViewController.h"

// ChatViewController is your own ViewController
@implementation ChatViewController
- (void)viewDidLoad {
  // Create conversation information
  TUIChatConversationModel *data = [[TUIChatConversationModel alloc] init];
  data.userID = @"userID";    
  // TUIC2CChatViewController
  TUIC2CChatViewController *vc = [[TUIC2CChatViewController alloc] init];  
  [vc setConversationData:data];
  // Add TUIC2CChatViewController to your own ViewController
  [self addChildViewController:vc];
  [self.view addSubview:vc.view];
}
@end
```
>? `TUIC2CChatViewController` will automatically pull and display the historical messages of the user.
:::

::: Minimalist version
```java
# Import "TUIC2CChatViewController_Minimalist.h"

// ChatViewController is your own ViewController
@implementation ChatViewController
- (void)viewDidLoad {
  // Create conversation information
  TUIChatConversationModel *data = [[TUIChatConversationModel alloc] init];
  data.userID = @"userID";    
  // Create TUIC2CChatViewController_Minimalist
  TUIC2CChatViewController_Minimalist *vc = [[TUIC2CChatViewController_Minimalist alloc] init];  
  [vc setConversationData:data];
  // Add TUIC2CChatViewController to your own ViewController
  [self addChildViewController:vc];
  [self.view addSubview:vc.view];
}
@end
```
>?`TUIC2CChatViewController_Minimalist` will automatically pull and display the historical messages of the user.
:::
</dx-tabs>

[](id:textTranslation)
#### Enabling text message translation
When you are on the chat UI, you can tap and hold a text message in the message list, and tap the **Translate** button on the pop-up menu to translate the text message.
The translation feature is disabled by default, and the **Translate** button is not displayed on the menu that pops up when you tap and hold a text message.

To enable the translation feature, perform the following steps:
1. Text translation is a **value-added paid service**, and is billed based on the number of characters translated. The feature is currently in beta test. To try it out, contact your Tencent Cloud rep. **If the translation service is not activated, even if the Translate button is displayed on the UI, the translation service cannot work properly.**
2. After the translation service is activated and before the chat UI is initialized, you can configure the system to display the **Translate** button. Sample code:
```objectivec
// Display the Translate button
TUIChatConfig.defaultConfig.enableTextTranslation = YES;
```

> ! 
> 1. The text message translation feature is supported from TUIChat 7.0.
> 2. Only text messages, and quote and reply text messages support translation. Image, audio, video, file, and emoji messages do not support translation.
> 3. When you click **Translate**, the text will be translated into the language that is currently used by TUIChat. For example, if the current TUIChat language is English, the text will be translated into English regardless of which language it is in.

The following figure shows the effect after the translation service is activated and the **Translate** button display is enabled.
<dx-tabs>
::: Classic version
<table style="text-align:center;vertical-align:middle;width: 900px">
  <tr>
    <th style="text-align:center;" width="300px">Not Displaying the Translate Button</th>
    <th style="text-align:center;" width="300px">Displaying the Translate Button</th>
    <th style="text-align:center;" width="300px">Text Message Translation Effect</th>
  </tr>
  <tr>
    <td><img style="width:300px" src="https://qcloudimg.tencent-cloud.cn/raw/773e84c24e7841e4869c02928fc9cb38.jpg"/></td>
    <td><img style="width:300px" src="https://qcloudimg.tencent-cloud.cn/raw/120664399ca36b38d6c262f2672cc0db.jpg"/></td>
    <td><img style="width:300px" src="https://qcloudimg.tencent-cloud.cn/raw/9a6bdc1138ad9956257d1f7305f00eef.jpg"/></td>
	 </tr>
</table>
:::
::: Minimalist version
<table style="text-align:center;vertical-align:middle;width: 900px">
  <tr>
    <th style="text-align:center;" width="300px">Not Displaying the Translate Button</th>
    <th style="text-align:center;" width="300px">Displaying the Translate Button</th>
    <th style="text-align:center;" width="300px">Text Message Translation Effect</th>
  </tr>
  <tr>
    <td><img style="width:300px" src="https://qcloudimg.tencent-cloud.cn/raw/1b440a16a852d0cc2a9878d49da96d5f.jpg"/></td>
    <td><img style="width:300px" src="https://qcloudimg.tencent-cloud.cn/raw/e80da5a3e10967329c6334bf798053f9.jpg"/></td>
    <td><img style="width:300px" src="https://qcloudimg.tencent-cloud.cn/raw/4387ad821803260c15ad65de770560ed.jpg"/></td>
	 </tr>
</table>
:::
</dx-tabs>


### Step 4. Build the contacts panel
The contacts panel does not require other dependencies. You only need to create the object and display it.
<dx-tabs>
::: Classic version
```java
#import "TUIContactController.h"

// ContactController is your own ViewController
@implementation ContactController
- (void)viewDidLoad {    
  // Create TUIContactController
  TUIContactController *vc = [[TUIContactController alloc] init];
  // Add TUIContactController to your own ViewController
  [self addChildViewController:vc];
  [self.view addSubview:vc.view];
}
@end
```

Note: The preceding code only initializes `TUIContactController` and displays it. For the click actions (such as clicking a friend and adding a friend) on the contacts UI, TUIKit will deliver them to the upper layer for processing through `TUIContactControllerListener`.
```java
@protocol TUIContactControllerListener <NSObject>
@optional
- (void)onSelectFriend:(TUICommonContactCell *)cell;
- (void)onAddNewFriend:(TUICommonTableViewCell *)cell;
- (void)onGroupConversation:(TUICommonTableViewCell *)cell;
@end
```
:::

::: Minimalist version
```java
#import "TUIContactController_Minimalist.h"

// ContactController is your own ViewController
@implementation ContactController
- (void)viewDidLoad {    
  // Create TUIContactController_Minimalist
  TUIContactController_Minimalist *vc = [[TUIContactController_Minimalist alloc] init];
  // Add TUIContactController_Minimalist to your own ViewController
  [self addChildViewController:vc];
  [self.view addSubview:vc.view];
}
@end
```
Note: The preceding code only initializes `TUIContactController_Minimalist` and displays it. For the click actions (such as clicking a friend and adding a friend) on the contacts UI, TUIKit will deliver them to the upper layer for processing through ``TUIContactControllerListener_Minimalist`.
```java
@protocol TUIContactControllerListener_Minimalist <NSObject>
@optional
- (void)onSelectFriend:(TUICommonContactCell *)cell;
- (void)onAddNewFriend:(TUICommonTableViewCell *)cell;
- (void)onGroupConversation:(TUICommonTableViewCell *)cell;
@end
```
:::
</dx-tabs>

For example, when a user clicks a friend, the friend's profile page will be displayed:
<dx-tabs>
::: Classic version
```objectivec
#import "TUIFriendProfileController.h"

- (void)onSelectFriend:(TUICommonContactCell *)cell
{
    TUICommonContactCellData *data = cell.contactData;
    // Create the friend's profile
    TUIFriendProfileController *vc = [[TUIFriendProfileController alloc] init];
    vc.friendProfile = data.friendProfile;
    // Display the friend's profile
    [self.navigationController pushViewController:(UIViewController *)vc animated:YES];
}
```
:::

::: Minimalist version
```objectivec
#import "TUIFriendProfileController_Minimalist.h"

- (void)onSelectFriend:(TUICommonContactCell *)cell
{
    TUICommonContactCellData *data = cell.contactData;
    // Create the friend's profile
    TUIFriendProfileController_Minimalist *vc = [[TUIFriendProfileController_Minimalist alloc] init];
    vc.friendProfile = data.friendProfile;
    // Display the friend's profile
    [self.navigationController pushViewController:(UIViewController *)vc animated:YES];
}
```
:::

</dx-tabs>

>? You can download [TUIKitDemo source code](https://github.com/TencentCloud/TIMSDK/tree/master/iOS) and view the implementation of more contacts events.

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

1. Activate the TRTC service
  1. Log in to the [Chat console](https://console.cloud.tencent.com/im) and click the target app card to go to the basic configuration page of the app.
  2. Click **Free trial** under **Activate Tencent Real-Time Communication (TRTC)** to activate the 7-day free trial service of TUICallKit.
  3. Click **Confirm** in the pop-up dialog box. A TRTC app with the same SDKAppID as the Chat app will be created in the [TRTC console](https://console.cloud.tencent.com/trtc). You can use the same account and authentication information for Chat and TRTC.
2. Integrate the TUICallKit component.
Add the following content to your Podfile:
```objectivec
// Integrate the TUICallKit component
pod 'TUICallKit'                  
```
3. Start and answer a video or audio call
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
<ul>
<li>After integrating the TUICallKit component, the chat UI and contact profile UI display the **Video Call** and **Audio Call** buttons by default. When a user clicks either of the buttons, TUIKit automatically displays the call invitation UI and sends the call invitation request to the callee.</li>
<li>When an <strong>online</strong> user receives a call invitation, TUIKit automatically displays the call receiving UI, where the user can answer or reject the call.</li>
<li>When an <strong>offline</strong> user receives a call invitation and wants to start the app to accept the call, the offline push capability is required. For how to implement offline push, see <a href = "https://intl.cloud.tencent.com/document/product/1047/50033">here</a>.</li>
</ul>
4. Add offline push
Before using offline push, you need to activate the [Chat offline push](https://www.tencentcloud.com/document/product/1047/39157) service.
For related app configuration, see [Integrating TUIOfflinePush and Running the Offline Push Feature](https://intl.cloud.tencent.com/document/product/1047/50033).

After the configuration is completed, when you click a **received audio/video call notification pushed offline**, TUICallKit automatically opens the **audio/video call invitation UI**.
	
5. Add value-added capabilities.
After TUIChat and TUICallKit are integrated, when you send a voice message on the chat UI, **the voice message can be recorded with AI-based noise reduction and automatic gain control**. This feature relies on the audio/video call capability of higher-level plans, which is supported in Chat SDK 7.0 and later versions. If the dependent plan expires, voice message recording is switched to the system API.
The following compares the voice messages recorded simultaneously using two Huawei P10 phones:
<table style="text-align:center;vertical-align:middle;width: 800px">
  <tr>
    <th style="text-align:center;" ><b>Voice Message Recorded by the System<br></b></th>
    <th style="text-align:center;" ><b>Voice Message with AI-based Noise Reduction and Automatic Gain Control Recorded by TUICallkit<br></b></th>
  </tr>
  <tr>
    <td>
      <audio id="audio" controls="" preload="none" >
	<source id="m4a" src="https://im.sdk.cloudcachetci.com/tools/resource/rain_system_record.m4a">
      </audio>
    </td>

    <td>
      <audio id="audio" controls="" preload="none">
    <source id="m4a" src="https://im.sdk.cloudcachetci.com/tools/resource/rain_tuicallkit_record_with_agc_aidenoise.m4a">
      </audio>
    </td>
  </tr>
</table>

## FAQs
#### What should I do when I receive the message "target has transitive dependencies that include statically linked binaries"?
If this error occurs during the `pod` process, this is because TUIKit is using a third-party static library. You need to comment out `use_frameworks!` in your Podfile.
If you need to use `use_frameworks!`, use CocoaPods 1.9.0 or a later version for `pod install` and modify it as follows:
```
use_frameworks! :linkage => :static
```
If you use Swift, change the reference of the header file to the reference format of @import module name.

#### What should I do if TUICallKit conflicts with an audio/video library that I have integrated?
Do not integrate different Tencent Cloud [audio and video libraries](https://www.tencentcloud.com/document/product/647/34615) at the same time to avoid symbol conflicts. If you use a library not of the [TRTC](https://www.tencentcloud.com/document/product/647/34615#TRTC) version, we recommend that you remove it and integrate the TUICallKit Professional version via `pod`. The audio and video library of the [LiteAV_Professional](https://www.tencentcloud.com/document/product/647/34615#.E4.B8.93.E4.B8.9A.E7.89.88.EF.BC.88professional.EF.BC.89) version contains all basic audio and video capabilities. **The audio and video library of the [LiteAV_Enterprise](https://www.tencentcloud.com/document/product/647/34615#Enterprise) version cannot coexist with TUICallKit.** For the detailed solution, see [here](https://www.tencentcloud.com/document/product/1047/50024#.E5.B8.B8.E8.A7.81.E9.97.AE.E9.A2.98).

#### How long is the default call invitation timeout duration?
The default call invitation timeout duration is 30 seconds.

#### Will an invitee receive a call invitation immediately if the invitee goes offline and then online within the call invitation timeout duration?

- If the call invitation is started in a one-to-one chat, the invitee can receive the call invitation, and the TUIKit will automatically open the call invitation UI internally.
- If the call invitation is started in a group chat, the TUIKit will automatically pull the call invitations of the last 30 seconds and open the group call UI.
