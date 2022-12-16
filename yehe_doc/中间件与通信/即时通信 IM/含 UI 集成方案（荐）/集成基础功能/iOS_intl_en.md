TUIKit supports modular integration starting from version 5.7.1435. You can integrate modules for integration according to your needs.
Starting from version 6.9.3557, TUIKit provides a new set of minimalist version UI components. The previous version UI components are still retained, which are called the classic version UI components. You can choose either the classic or minimalist version as needed.

For more information about TUIKit components, see [here](https://www.tencentcloud.com/document/product/1047/50062).

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
  After all TUIKit components are integrated, the project structure is as follows:
  <img src="https://staticintl.cloudcachetci.com/yehe/backend-news/CZff221_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_1671075129288.png" style="zoom:50%;"/> 

## Quick Build
Instant messaging software usually consists of several basic UIs such as the conversation list, chat window, contacts, and audio/video call UIs. It only takes a few lines of code to build these UIs in your project. The process is as follows:

> ? About TUIKit component features:
>
> If you want to learn more, you can [download and run TUIKitDemo source code](https://www.tencentcloud.com/document/product/1047/45913), where you can find samples of frequently used features.


### Step 1. Log in to TUIKit
You need to log in to TUIKit before you can use the component features properly. To log in to TUIKit, click `Login` on your app.
You need to create an app and obtain the SDKAppID in the [IM console](https://console.cloud.tencent.com/im). `userSig` needs to be calculated according to rules. For operation details, see [Get Started](https://www.tencentcloud.com/document/product/1047/45913).

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

>? You can [download TUIKitDemo source code](https://www.tencentcloud.com/document/product/1047/45913) and view the implementation of more contacts events.

### Step 5. Build the audio/video call feature
TUI components allow users to start audio/video calls in chat UIs and can be quickly integrated with a few steps:
<table style="text-align:center;vertical-align:middle;width: 700px">
  <tr>
    <th style="text-align:center;" ><b>Video Call<br></b></th>
    <th style="text-align:center;"><b>Audio Call</b><br></th>
  </tr>
  <tr>
    <td><img src="https://qcloudimg.tencent-cloud.cn/raw/44d4c8a412752abda898341665a90016.png"/></td>
    <td><img src="https://qcloudimg.tencent-cloud.cn/raw/5eb84936666da81b0331a28c3c779b77.png"/></td>
  </tr>
</table>


1. Activate the TRTC service
  1. Log in to the [IM console](https://console.cloud.tencent.com/im) and click the target app card to go to the basic configuration page of the app.
  2. Click **Free trial** under **Activate Tencent Real-Time Communication (TRTC)** to activate the 7-day free trial service of TUICallKit.
  3. Click **Confirm** in the pop-up dialog box. A TRTC app with the same SDKAppID as the IM app will be created in the [TRTC console](https://console.cloud.tencent.com/trtc). You can use the same account and authentication information for IM and TRTC.
2. Integrate the TUICallKit component.
Add the following content to your Podfile:
```objectivec
// Integrate the TUICallKit component
pod 'TUICallKit'                  
```
3. Start and answer a video or audio call
<table style="text-align:center;vertical-align:middle;width: 600px">
  <tr>
    <th style="text-align:center;" ><b>Starting a Call via a Message Page/Starting a Call via a Contact Profile Page<br></b></th>
  </tr>
  <tr>
    <td><img style="width:600px" src="https://staticintl.cloudcachetci.com/yehe/backend-news/EseX367_%E9%9B%86%E5%90%88%281%29.png"/></td>
    </tr>
</table>
<ul>
<li>After integrating the TUICallKit component, the chat UI and contact profile UI display the <b>Video Call</b> and <b>Audio Call</b> buttons by default. When a user clicks either of the buttons, TUIKit automatically displays the call invitation UI and sends the call invitation request to the callee.</li>
<li>When an <strong>online</strong> user receives a call invitation, TUIKit automatically displays the call receiving UI, where the user can answer or reject the call.</li>
<li>When an <strong>offline</strong> user receives a call invitation and wants to start the app to accept the call, the offline push capability is required. For how to implement offline push, see <a href="#Step5.4">Add offline push</a>.</li>
</ul>

4. Add offline push
Before using offline push, you need to activate the [IM offline push](https://intl.cloud.tencent.com/document/product/1047/39157) service.
For related app configuration, see [Integrating TUIOfflinePush and Running the Offline Push Feature](https://www.tencentcloud.com/document/product/1047/39157).

After the configuration is completed, when you click a **received audio/video call notification pushed offline**, TUICallKit automatically opens the **audio/video call invitation UI**.

## FAQs
#### What should I do when I receive the message "target has transitive dependencies that include statically linked binaries"?
If this error occurs during the `pod` process, this is because TUIKit is using a third-party static library. You need to comment out `use_frameworks!` in your Podfile.
If you need to use `use_frameworks!`, use CocoaPods 1.9.0 or a later version for `pod install` and modify it as follows:
```
use_frameworks! :linkage => :static
```
If you use Swift, change the reference of the header file to the reference format of @import module name.

#### What should I do if TUICallKit conflicts with an audio/video library that I have integrated?
Do not integrate different Tencent Cloud [audio and video libraries](https://intl.cloud.tencent.com/document/product/647/34615) at the same time to avoid symbol conflicts. If you use a library not of the [TRTC](https://intl.cloud.tencent.com/document/product/647/34615#TRTC) version, we recommend that you remove it and integrate the TUICallKit Professional version via `pod`. The audio and video library of the [LiteAV_Professional](https://intl.cloud.tencent.com/document/product/647/34615#.E4.B8.93.E4.B8.9A.E7.89.88.EF.BC.88professional.EF.BC.89) version contains all basic audio and video capabilities. **The audio and video library of the [LiteAV_Enterprise](https://intl.cloud.tencent.com/document/product/647/34615#Enterprise) version cannot coexist with TUICallKit.** For the detailed solution, see [here](https://www.tencentcloud.com/document/product/1047/50024).

#### How long is the default call invitation timeout duration?
The default call invitation timeout duration is 30 seconds.

#### Will an invitee receive a call invitation immediately if the invitee goes offline and then online within the call invitation timeout duration?

- If the call invitation is started in a one-to-one chat, the invitee can receive the call invitation, and the TUIKit will automatically open the call invitation UI internally.
- If the call invitation is started in a group chat, the TUIKit will automatically pull the call invitations of the last 30 seconds and open the group call UI.
