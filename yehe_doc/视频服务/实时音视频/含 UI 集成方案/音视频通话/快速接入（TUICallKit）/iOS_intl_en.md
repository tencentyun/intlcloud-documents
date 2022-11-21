This document describes how to quickly integrate the `TUICallKit` component. Performing the following key steps generally takes about an hour, after which you can implement the video call feature with complete UIs.

## Environment Preparations

iOS 9.0 (API level 16) or later.

[](id:step1)
## Step 1. Activate the service

`TUICallKit` is an audio/video call component developed based on two paid PaaS services: [IM](https://www.tencentcloud.com/document/product/1047) and [TRTC](https://www.tencentcloud.com/document/product/647). You can activate the services and enjoy a 7-day free trial as follows:

1. Log in to the [IM console](https://console.tencentcloud.com/im) and click **Create Application**. In the pop-up window, enter your application name and click **OK**.
![img](https://qcloudimg.tencent-cloud.cn/raw/c9a076ece348019d689c6c562b6a3c78.png)

2. Click the application just created to enter the **Basic Configuration** page. Click **Free trial** under **Activate Tencent Real-Time Communication (TRTC)** in the bottom-right corner of the page for a 7-day free trial of `TUICallKit`. To officially release the application, [contact us](https://intl.cloud.tencent.com/contact-us).
![img](https://qcloudimg.tencent-cloud.cn/raw/4ee28e98dd28c9ae91078832f0105092.png)

>! Different paid editions of the IM audio/video call capability are available for different business needs. To learn more about the available features and purchase the edition that’s right for you, please [contact us](https://intl.cloud.tencent.com/contact-us).

3. On the same page, find and record the **SDKAppID** and **Key**, which will be used in [step 4](#step4).
![img](https://qcloudimg.tencent-cloud.cn/raw/c3158845c9c0227a2da9eea8c0a975bb.png)


>? **Note:** After you click **Free trial**, the following message will be displayed for some users who have used [TRTC](https://www.tencentcloud.com/document/product/647/35078) before:
```java
[-100013]:TRTC service is suspended. Please check if the package balance is 0 or the Tencent Cloud account is in arrears
```
This is because the new IM audio/video call capability is based on two basic PaaS services: [TRTC](https://www.tencentcloud.com/document/product/647/35078) and [IM](https://www.tencentcloud.com/document/product/1047). If you have used up your free monthly quota (10,000 minutes) for TRTC, you will fail to activate the capability. You can log in to the [TRTC console](https://console.tencentcloud.com/trtc/app), go to the **Application Management** page of the corresponding `SDKAppID`, and activate the pay-as-you-go feature. Then, next time you **start the application**, you can experience the new audio/video call capability properly.


[](id:step2)
## Step 2. Import the component

Use CocoaPods to import the component as follows:
1. Add the following dependency to your `Podfile`.

```shell
pod 'TUICallKit'
```

2. Run the following command to install the component:
```shell
pod install
```
If the latest version of `TUICallKit` cannot be installed, run the following command to update the local CocoaPods repository list:
```shell
pod repo update
```

[](id:step3)
## Step 3. Configure the project
Your app needs mic and camera permissions to implement audio/video communication. Add the two items below to `Info.plist` of your app. Their content is what users see in the mic and camera access pop-up windows.

```objectivec
<key>NSCameraUsageDescription</key>
<string>CallingApp needs to access your camera to capture video.</string>
<key>NSMicrophoneUsageDescription</key>
<string>CallingApp needs to access your mic to capture audio.</string>
```
![img](https://qcloudimg.tencent-cloud.cn/raw/5579558165eae672db5259a8989fe5d4.png)

[](id:step4)
## Step 4. Log in to the `TUICallKit` component
Add the following code to your project to call the relevant APIs in `TUICore` to log in to the `TUICallKit` component. This step is very important, as the user can use the component features properly only after a successful login. Carefully check whether the relevant parameters are correctly configured:

<dx-codeblock>
:::  Objective-C Objectivec
// Log in to the component
[TUILogin login:1400000001           // Replace it with the `SDKAppID` obtained in step 1.
         userID:@"denny"             // Replace it with your `UserID`.
         userSig:@"xxxxxxxxxxx"      // You can calculate a `UserSig` in the console and enter it here.
            succ:^{
    NSLog(@"login success");
} fail:^(int code, NSString *msg) {
    NSLog(@"login failed, code: %d, error: %@", code, msg);
}
:::
::: Swift
// Log in to the component
TUILogin.login(1400000001,                   // Replace it with the `SDKAppID` obtained in step 1.
            userID: "denny",                 // Replace it with your `UserID`.
            userSig: "xxxxxxxxxxx") {        // You can calculate a `UserSig` in the console and enter it here.
    print("login success")
} fail: { (code, message) in
    print("login failed, code: \(code), error: \(message ?? "nil")")
}
:::
</dx-codeblock>

**Parameter description:**
The key parameters used by the `login` function are as detailed below:
- `sdkAppId`: Obtained in the last step in step 1 and not detailed here.
- `userId`: The ID of the current user, which is a string that can contain only letters (a–z and A–Z), digits (0–9), hyphens (-), or underscores (_).
- `userSig`: The authentication credential used by Tencent Cloud to verify whether the current user is allowed to use the TRTC service. You can get it by using the `SecretKey` obtained in step 3 to encrypt the information such as `SDKAppID` and `UserID`. You can generate a temporary `UserSig` by clicking the [`UserSig` generation](https://console.tencentcloud.com/trtc/app) button in the console.
For more information, see [UserSig](https://www.tencentcloud.com/document/product/647/35166).

> ! 
>- **Many developers have contacted us with many questions regarding this step. Below are some of the frequently encountered problems:** 
    - `sdkAppId` is invalid. It is generally a 10-digit integer starting with `140`.
    - `userSig` is set to the value of `Secretkey` mistakenly. The `userSig` is generated by using the `SecretKey` for the purpose of encrypting information such as `sdkAppId`, `userId`, and the expiration time. But the value of the `userSig` that is required cannot be directly substituted with the value of the `SecretKey`.
    - `userId` is set to a simple string such as `1`, `123`, or `111`, and your colleague may be using the same `userId` while working on a project simultaneously. In this case, login will fail as **TRTC doesn't support login on multiple terminals with the same `UserID`**. Therefore, we recommend you use some distinguishable `userId` values during debugging.
>- The sample code on GitHub uses the `genTestUserSig` function to calculate `userSig` locally, so as to help you complete the current integration process more quickly. However, this scheme exposes your `SecretKey` in the application code, which makes it difficult for you to upgrade and protect your `SecretKey` subsequently. Therefore, we strongly recommend you run the `userSig` calculation logic on the server and make the application request the `userSig` calculated in real time every time the application uses the `TUICallKit` component from the server.

[](id:step5)
## Step 5. Make a call
### One-to-one video call
You can call the `call` function of `TUICallKit` and specify the call type and the callee's `userId` to make an audio/video call.
<dx-codeblock>
:::  Objective-C Objectivec
// Make a one-to-one video call. Suppose the `userId` is `mike`.
[[TUICallKit createInstance] call:@"mike" callMediaType:TUICallMediaTypeVideo];
:::
::: Swift
// Make a one-to-one video call. Suppose the `userId` is `mike`.
TUICallKit.createInstance().call(userId: "mike", callMediaType: .video)
:::
</dx-codeblock>

| Parameter | Type | Description |
|-----|-----|-----|
| userId | String | The ID of the target user, such as `"mike"`. |
| callMediaType | TUICallMediaType | The call media type, such as `TUICallMediaTypeVideo`. |

### Group video call
You can call the `groupCall` function of `TUICallKit` and specify the call type and the list of callees' `UserID` values to make a group audio/video call.
<dx-codeblock>
:::  Objective-C Objectivec
[[TUICallKit createInstance] groupCall:@"12345678" userIdList:@[@"denny", @"mike", @"tommy"] callMediaType:TUICallMediaTypeVideo];
:::
::: Swift
TUICallKit.createInstance().groupCall(groupId: "12345678", userIdList: ["denny", "mike", "tommy"], callMediaType: .video)
:::
</dx-codeblock>

| Parameter | Type | Description |
|-----|-----|-----|
| groupId | String | The group ID, such as `@"12345678"`. |
| userIdList | Array | The list of `userId` values of the target users, such as `@[@"denny", @"mike", @"tommy"]`. |
| callMediaType | TUICallMediaType | The call media type, such as `TUICallMediaTypeVideo`. |

>? 
>- You can create a group as instructed in [Android, iOS, and macOS](https://www.tencentcloud.com/document/product/1047/48466). You can also use [IM TUIKit](https://intl.cloud.tencent.com/document/product/1047/34286) to integrate chat and call scenarios at one stop.
>- `TUICallKit` currently doesn't support making a multi-person video call among users not in a group. If you have such a need, contact colleenyu@tencent.com.

[](id:step6)
## Step 6. Answer a call
After **step 4**, when receiving an incoming call, the `TUICallKit` component will automatically display the call answering UI.

[](id:step7)
## Step 7. Implement more features
### 1. Nickname and profile photo settings
To customize the nickname or profile photo, use the following API for update:
<dx-codeblock>
:::  Objective-C Objectivec
[[TUICallKit createInstance] setSelfInfo:@"nickname" avatar:@"profile photo URL" succ:^{

} fail:^(int code, NSString *errMsg) {

}];
:::
::: Swift
TUICallKit.createInstance().setSelfInfo(nickname: "nickname", avatar: "profile photo URL", succ: {

}) { code, desc in

}
:::
</dx-codeblock>

> ! The update of the callee's nickname and profile photo may be delayed during a call between non-friend users due to the user privacy settings. After a call is made successfully, the information will also be updated properly in subsequent calls.

### 2. Offline call push
You can make/answer audio or video calls after completing the above steps. However, if you want your users to be able to receive call invitations even when your application is in the background or after it is closed, then you need to also implement the offline call push feature. For more information, see [**Offline Call Push (iOS)**](https://www.tencentcloud.com/document/product/647/51000).

### 3. Floating window
To implement the floating window feature in your application, call the following API when initializing the `TUICallKit` component:
 <dx-codeblock>
:::  Objective-C Objectivec
[[TUICallKit createInstance] enableFloatWindow:YES];
:::
::: Swift
TUICallKit.createInstance().enableFloatWindow(true)
:::
</dx-codeblock>

### 4. Listening on the call status
To **listen on the call status** (for example, the start or end of a call or the call quality during a call), listen on the following events:
<dx-codeblock>
:::  Objective-C Objectivec
[[TUICallEngine createInstance] addObserver:self];

- (void)onCallBegin:(TUIRoomId *)roomId callMediaType:(TUICallMediaType)callMediaType callRole:(TUICallRole)callRole {
  

}
- (void)onCallEnd:(TUIRoomId *)roomId callMediaType:(TUICallMediaType)callMediaType callRole:(TUICallRole)callRole totalTime:(float)totalTime {
  

}
- (void)onUserNetworkQualityChanged:(NSArray<TUINetworkQualityInfo *> *)networkQualityList {
  

}
:::
::: Swift
TUICallEngine.createInstance().add(self)

public func onCallBegin(roomId: TUIRoomId, callMediaType: TUICallMediaType, callRole: TUICallRole) {
        
}
public func onCallEnd(roomId: TUIRoomId, callMediaType: TUICallMediaType, callRole: TUICallRole, totalTime: Float) {
        
}
public func onUserNetworkQualityChanged(networkQualityList: [TUINetworkQualityInfo]) {
        
}
:::
</dx-codeblock>

### 5. Custom ringtone
You can use the following API to customize the ringtone:
<dx-codeblock>
:::  Objective-C Objectivec
[[TUICallKit createInstance] setCallingBell:filePath];
:::
::: Swift
TUICallKit.createInstance().setCallingBell(filePath: filePath)
:::
</dx-codeblock>


## FAQs
### 1. What should I do if I receive the error message "The package you purchased does not support this ability"?

The error message indicates that your application's audio/video call capability package has expired or is not activated. You can claim or activate the audio/video call capability as instructed in [step 1](#step1) to continue using `TUICallKit`.

### 2. How do I purchase a plan?

For more information, see [Billing Overview](https://www.tencentcloud.com/document/product/647/50553). If you have any questions, please contact us.

>? For more information, see [FAQs (iOS)](https://www.tencentcloud.com/document/product/647/51023).

## Exchange and Feedback

If you have any suggestions or comments, contact colleenyu@tencent.com.
