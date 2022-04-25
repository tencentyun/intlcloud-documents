## Component Overview

`TUICalling` is an open-source audio/video UI component. After integrating it into your project, you can make your application support scenarios such as one-to-one and group audio/video calls and offline call simply by writing a few lines of code. It also supports Android, web, mini program, Flutter, and UniApp platforms. Its basic features are as shown below:

<table class="tablestyle">
<tbody><tr>
<td><img src="https://qcloudimg.tencent-cloud.cn/raw/94bbec9961b0d569cc7068389dc41412.jpg" width="400"></td>
<td><img src="https://qcloudimg.tencent-cloud.cn/raw/534089ed0be5c78fb63c65cde79ad866.jpg" width="400"></td>
</tr>
</tbody></table>


## Component Integration

### Step 1. Import the `TUICalling` component

**To import the component through CocoaPods**, follow the steps below:
1. Create the `TUICalling` folder at the same level as the `Podfile` of your project.
2. Go to [**GitHub/TUICalling**](https://github.com/tencentyun/TUICalling), clone or download the code, and copy the `Source` and `Resources` folders and the `TUICalling.podspec` file in the [**TUICalling/iOS/**](https://github.com/tencentyun/TUICalling/tree/main/iOS) directory to the `TUICalling` folder created in step 1.
3. Add the following dependencies to your `Podfile` and run `pod install` to complete the import.
```
# :path => "Points to the relative path of `TUICalling.podspec`"
pod 'TUICalling', :path => "TUICalling/TUICalling.podspec", :subspecs => ["TRTC"]
```

>! The `Source` and `Resources` folders and the `TUICalling.podspec` file must be in the same directory.

### Step 2. Configure permissions

To use the audio/video features, you need to grant mic and camera permissions. Add the two items below to `Info.plist` of your application. Their content is what users see in the mic and camera access pop-up windows.

```
<key>NSCameraUsageDescription</key>
<string>`TUICalling` needs to access your camera to be able to shoot videos with images.</string>
<key>NSMicrophoneUsageDescription</key>
<string>`TUICalling` needs to access your mic to be able to shoot videos with audio.</string>
```
![](https://qcloudimg.tencent-cloud.cn/raw/224ae568f11d50124ea663ac0ef1c6e9.png)

### Step 3. Create and initialize the component

<dx-tabs>
:::  Objective-C
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
</dx-tabs>

**Parameter description:**
- **SDKAppID**: **TRTC application ID**. If you haven't activated the TRTC service, log in to the [TRTC console](https://console.cloud.tencent.com/trtc/app), create a TRTC application, and click **Application Info**. The `SDKAppID` is as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/435d5615e0c4075640bb05c49884360c.png)
- **SecretKey**: **TRTC application key**, which corresponds to `SDKAppID`. On the [Application Management](https://console.cloud.tencent.com/trtc/app) page in the TRTC console, the `SecretKey` is as shown below:
- **UserID**: Current user ID, which is a string and can contain up to 32 bytes of letters and digits (special symbols are not supported). You can customize it based on your actual account system.
- **UserSig**: Security protection signature calculated based on `SDKAppID`, `UserID`, and `SecretKey`. You can click [here](https://console.cloud.tencent.com/trtc/usersigtool) to directly generate a debugging `userSig` online or calculate it on your own by referring to the [TUICalling demo project](https://github.com/tencentyun/TUICalling/blob/main/iOS/Example/Debug/GenerateTestUserSig.swift#L39). For more information, see [UserSig](https://intl.cloud.tencent.com/document/product/647/35166).

### Step 4. Make an audio/video call

- Make a one-to-one audio/video call through [TUICalling#call](https://intl.cloud.tencent.com/document/product/647/43139)
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
- Make a group video call through [TUICalling#call](https://intl.cloud.tencent.com/document/product/647/43139)
<dx-codeblock>
:::  Objective-C Objectivec
// Make a group video call. Suppose the `userId` values are `1111`, `2222`, and `3333`
[[TUICalling shareInstance] call:@[@"1111", @"2222", @"3333"] type:TUICallingTypeVideo];
:::
::: Swift Swift
// Make a group video call. Suppose the `userId` values are `1111`, `2222`, and `3333`
TUICalling.shareInstance().call(userIDs: ["1111", "2222", "3333"], type: .video)
:::
</dx-codeblock>

>? After the callee completes step 3, (i.e., after successful login) when receiving a call request again, the `TUICalling` component will automatically display the corresponding call answering UI.

### Step 5. Add the offline push feature (optional)
After the above four steps are completed, video calls can be made and answered. However, if your business scenarios require that audio/video call requests can be normally received even **after the application process is killed** or **runs in the background**, you need to add the offline push feature to the `TUICalling` component. For more information, see [**Offline Push (iOS)**](https://intl.cloud.tencent.com/document/product/1047/39157).

### Step 6. Add the status listening feature (optional)

If your business needs to [listen on the call status](https://intl.cloud.tencent.com/document/product/647/43139) such as call start and end, listen on the following events:
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

If your business needs to enable the [floating window feature](https://intl.cloud.tencent.com/document/product/647/43139), you can call `TUICalling.shareInstance().enableFloatWindow(enable: true)` during `TUICalling` component initialization.

>? Currently, the component supports only the in-app floating window (minimize and return to the previous page).

## FAQs

### Does the `TUICalling` component support customizing ringtones?

Yes. You can implement this simply by calling [TUICalling#setCallingBell](https://intl.cloud.tencent.com/document/product/647/43139).

### How do I install CocoaPods?

Enter the following command in a terminal window (you need to install Ruby on your Mac first):
```
sudo gem install cocoapods
```

### Can `TUICalling` run in the background?

Yes. If you want the SDK to run in the background, select your project, under the **Capabilities** tab, toggle on **Background Modes**, and select **Audio, AirPlay, and Picture in Picture**, as shown below:
![](https://main.qcloudimg.com/raw/d960dfec88388936abce2d4cb77ac766.jpg)

>? If you have any requirements or feedback, contact colleenyu@tencent.com.
