## Overview

`TUICalling` is an open-source UI component for audio/video communication. With just a few lines of code changes, you can integrate it into your project to implement one-to-one audio/video calls that support offline push notifications. In addition to the iOS component, we also offer components for Android, web, Flutter, UniApp, and more.

>? All components of TUIKit use two basic PaaS services of Tencent Cloud, namely [TRTC](https://intl.cloud.tencent.com/document/product/647/35078) and [IM](https://intl.cloud.tencent.com/document/product/1047/35448). When you activate TRTC, IM and the trial edition of the IM SDK (which supports only 100 DAUs) will be activated automatically. For the billing details of IM, see [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350).

![](https://qcloudimg.tencent-cloud.cn/raw/af697557d2746585a0d9f4b894dc42d5.png)

## Integration

### Step 1. Import the `TUICalling` component

**To import the component using CocoaPods**, follow the steps below:
1. Create a `TUICalling` folder in the same directory as `Podfile` in your project.
2. Go to the component’s [GitHub page](https://github.com/tencentyun/TUICalling), clone or download the code, and copy the `Source` and `Resources` folders and the `TUICalling.podspec` file in [TUICalling/iOS/](https://github.com/tencentyun/TUICalling/tree/main/iOS) to the `TUICalling` folder in your project.
3. Add the following dependencies to your `Podfile` and run `pod install` to import the component.
```
# :path => "The relative path of `TUICalling.podspec`"
pod 'TUICalling', :path => "TUICalling/TUICalling.podspec", :subspecs => ["TRTC"]
```

>! The `Source` and `Resources` folders and the `TUICalling.podspec` file must be in the same directory.

### Step 2. Configure permissions

Your app needs mic and camera permissions to implement audio/video communication. Add the two items below to `Info.plist` of your app. Their content is what users see in the mic and camera access pop-up windows.

```
<key>NSCameraUsageDescription</key>
<string>CallingApp needs to access your camera to capture video.</string>
<key>NSMicrophoneUsageDescription</key>
<string>CallingApp needs to access your mic to capture audio.</string>
```
![](https://qcloudimg.tencent-cloud.cn/raw/224ae568f11d50124ea663ac0ef1c6e9.png)

### Step 3. Create and initialize an instance of the component

<dx-codeblock>
::: Objective-C
```
// 1. Log in to the component
[TUILogin initWithSdkAppID:@"Your SDKAppID"];
[TUILogin login:@"Your UserID" userSig:@"Your UserSig" succ:^{
    NSLog(@"login success");
} fail:^(int code, NSString *msg) {
    NSLog(@"login failed, code: %d, error: %@", code, msg);
}];

// 2. Initialize the `TUICalling` instance
[TUICalling shareInstance];
```
:::
::: Swift
```
// 1. Log in to the component
TUILogin.initWithSdkAppID("Your SDKAppID")
TUILogin.login("Your UserID", userSig: "Your UserSig") {
    print("login success")
} fail: { code, message in
    print("login failed, code: \(code), error: \(message ?? "nil")")
}

// 2. Initialize the `TUICalling` instance
TUICalling.shareInstance()
```
:::
</dx-codeblock>

**Parameter description:**
- **SDKAppID**: **TRTC application ID**. If you haven't activated TRTC, log in to the [TRTC console](https://console.cloud.tencent.com/trtc/app), create a TRTC application, click **Application Info**, and select the **Quick Start** tab to view its `SDKAppID`.
![](https://qcloudimg.tencent-cloud.cn/raw/435d5615e0c4075640bb05c49884360c.png)
- **SecretKey**: **TRTC application key**. Each secret key corresponds to a `SDKAppID`. You can view your application’s secret key on the [Application Management](https://console.cloud.tencent.com/trtc/app) page of the TRTC console.
- **UserID**: Current user ID, which is a custom string that can contain up to 32 bytes of letters and digits (special characters are not supported).
- **UserSig**: Security signature calculated based on `SDKAppID`, `userID`, and `SecretKey`. You can click [here](https://console.cloud.tencent.com/trtc/usersigtool) to quickly generate a `UserSig` for testing or calculate it on your own by referring to our [TUICalling demo project](https://github.com/tencentyun/TUICalling/blob/main/iOS/Example/Debug/GenerateTestUserSig.swift#L39). For more information, see [UserSig](https://intl.cloud.tencent.com/document/product/647/35166).

### Step 4. Make an audio/video call
Make a one-to-one audio/video call using [TUICalling#call](https://intl.cloud.tencent.com/document/product/647/43139):
<dx-codeblock>
:::  Objective-C Objectivec
// Make a one-to-one video call. Suppose the `userId` is `1111`
[[TUICalling shareInstance] call:@[@"1111"] type:TUICallingTypeVideo];
:::
::: Swift Swift
// Make a one-to-one video call. Suppose the `userId` is `1111`
TUICalling.shareInstance().call(userIDs: ["1111"], type: .video)
:::
</dx-codeblock>


>? After the callee completes step 3, (that is, after successful login), the `TUICalling` component will display the call answering UI when the callee receives a call invitation.

### Step 5. Implement offline push notifications (optional)
You can make audio/video calls after completing the previous four steps. However, if you want your users to be able to receive call invitations even when your app is in the background or after it is closed, then you need to also implement the offline push notification feature. For details, see [Offline Push (iOS)](https://intl.cloud.tencent.com/document/product/1047/39157).

### Step 6. Listen for call status (optional)

If you want to be notified of [call status](https://intl.cloud.tencent.com/document/product/647/43139) (for example, the start and end of a call), register the following listeners:
<dx-codeblock>
:::  Objective-C Objectivec
[[TUICalling shareInstance] setCallingListener:self];

- (BOOL)shouldShowOnCallView {
    return YES;
}

- (void)callStart:(nonnull NSArray<NSString *> *)userIDs type:(TUICallingType)type role:(TUICallingRole)role viewController:(UIViewController * _Nullable)viewController {

}

- (void)callEnd:(nonnull NSArray<NSString *> *)userIDs type:(TUICallingType)type role:(TUICallingRole)role totalTime:(float)totalTime {

}

- (void)onCallEvent:(TUICallingEvent)event type:(TUICallingType)type role:(TUICallingRole)role message:(nonnull NSString *)message {

}
:::
::: Swift Swift
TUICalling.shareInstance().setCallingListener(listener: self)

public func shouldShowOnCallView() -> Bool {
    return true
}
    
public func callStart(userIDs: [String], type: TUICallingType, role: TUICallingRole, viewController: UIViewController?) {

}
    
public func callEnd(userIDs: [String], type: TUICallingType, role: TUICallingRole, totalTime: Float) {

}
    
public func onCallEvent(event: TUICallingEvent, type: TUICallingType, role: TUICallingRole, message: String) {

}
:::
</dx-codeblock>

### Step 7. Add the floating window feature (optional)

To implement the [floating window](https://intl.cloud.tencent.com/document/product/647/43139) feature in your app, call `TUICalling.shareInstance().enableFloatWindow(enable: true)` when initializing the `TUICalling` component.

>? Currently, the iOS component supports only in-app floating windows (after users tap the Back button to return to a previous page).

## FAQs

### Does the `TUICalling` component support customizing ringtones?

Yes. You can implement this by calling [TUICalling#setCallingBell](https://intl.cloud.tencent.com/document/product/647/43139).

### How do I install CocoaPods?

Enter the following command in a terminal window (you need to install Ruby on your Mac first):
```
sudo gem install cocoapods
```

### Can `TUICalling` run in the background?

Yes. If you want the SDK to run in the background, select your project, under the **Capabilities** tab, toggle on **Background Modes**, and select **Audio, AirPlay, and Picture in Picture**.
![](https://main.qcloudimg.com/raw/d960dfec88388936abce2d4cb77ac766.jpg)

>? If you have any requirements or feedback, contact colleenyu@tencent.com.
