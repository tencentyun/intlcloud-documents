## Demo UI
You can [download](https://intl.cloud.tencent.com/document/product/647/35076) and install the app we provide to try out the real-time audio/video call feature.
<table>
<tr>
   <th>Call</th>
   <th>Answer</th>
 </tr>
<tr>
<td><img src="https://main.qcloudimg.com/raw/ef83db73d0a8c487e72986dd1f92e361.jpeg"/></td>
<td><img src="https://main.qcloudimg.com/raw/f57ed3a55112233b05260f5dc37342ca.jpeg"/></td>
</tr>
</table>



>! To make it easier for you to implement the real-time audio/video call feature, we have refactored the `TUICalling` component. You no longer need to pay attention to UI as it is now implemented within the `TUICalling` component.

[](id:ui)

## Running the Demo

[](id:ui.step1)

### Step 1. Create an application
1. Log in to the TRTC console and select **Development Assistance** > **[Demo Quick Run](https://console.cloud.tencent.com/trtc/quickstart)**.
2. Enter an application name such as `TestVideoCall` and click **Create**.
3. Click **Next**.

![](https://main.qcloudimg.com/raw/9f4c878c0a150d496786574cae2e89f9.png)
>!This feature uses two basic PaaS services of Tencent Cloud, namely [TRTC](https://intl.cloud.tencent.com/document/product/647/35078) and [IM](https://intl.cloud.tencent.com/document/product/1047). When you activate TRTC, IM will be activated automatically. IM is a value-added service. See [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350) for its billing details.


[](id:ui.step2)
### Step 2. Download the application source code
Clone or download the [TUICalling](https://github.com/tencentyun/TUICalling) source code.

[](id:ui.step3)
### Step 3. Configure application project files
1. In the **Modify Configuration** step, select your platform.
2. Find and open `iOS/Example/Debug/GenerateTestUserSig.swift`.
3. Set the following parameters in `GenerateTestUserSig.swift`:
<ul style="margin:0"><li/>SDKAPPID: `0` by default. Set it to the actual `SDKAppID`.
<li/>SECRETKEY: left empty by default. Set it to the actual key.</ul>
<img src="https://main.qcloudimg.com/raw/87dc814a675692e76145d76aab91b414.png">

4. Click **Next** to complete the creation.
5. After compilation, click **Return to Overview Page**.

>!
>- The method for generating `UserSig` described in this document involves configuring `SECRETKEY` in client code. In this method, `SECRETKEY` may be easily decompiled and reversed, and if your key is disclosed, attackers can steal your Tencent Cloud traffic. Therefore, **this method is suitable only for the local execution and debugging of the app**.
>- The correct `UserSig` distribution method is to integrate the calculation code of `UserSig` into your server and provide an application-oriented API. When `UserSig` is needed, your application can send a request to the business server for a dynamic `UserSig`. For more information, see [How do I calculate UserSig on the server?](https://intl.cloud.tencent.com/document/product/647/35166).

[](id:ui.step4)
### Step 4. Run the application

Open the source code project `TUICalling/Example/TUICallingApp.xcworkspace` with Xcode (version 11.0 or above) and click **Run**.



## Tryout
>! You need at least two devices to try out the application.

### User A
1. Enter a username (**which must be unique**) and log in.
2. Enter the `userId` of the person you want to call and tap **Search**.
3. Tap **Call** and select **Video Call** (**Make sure that the callee is active in the application, or the call may fail**).<br>


### User B
1. Enter a username (**which must be unique**) and log in.
2. Go to the homepage and wait for the incoming call.



[](id:model)
## Integration Directions

In the [source code](https://github.com/tencentyun/TUICalling/tree/master/Android/Source/src/main/java/com/tencent/liteav/trtccalling), the `Source` folder contains three subfolders: `ui`, `model`, and `Service`. The `Service` subfolder includes the open-source `TUICallingManager` component, which we share with the public. You can find the component’s APIs in the `TUICallingManager.h` file.
![](https://qcloudimg.tencent-cloud.cn/raw/0de26d679e6e0dc1d9aeadb6dbf6f8aa.png)


You can enable the real-time audio/video call feature for your project with ease using the open-source `TUICalling` and `TUICallingManager` components, with no need to implement complicated call UI or logic by yourself.

[](id:model.step1)
### Step 1. Integrate the SDKs

The call component `TRTCCalling` depends on the TRTC SDK and IM SDK. You can integrate the two SDKs into your project by following the steps below:

- **Method 1: adding dependencies via CocoaPods**
<dx-codeblock>
::: swift
 pod 'TXIMSDK_iOS'
 pod 'TXLiteAVSDK_TRTC' 
:::
</dx-codeblock>
>?You can view the latest version numbers of the two SDKs by visiting their GitHub pages at [TRTC](https://github.com/tencentyun/TRTCSDK) and [IM](https://github.com/tencentyun/TIMSDK).
- **Method 2: adding dependencies through local files**
If your access to the CocoaPods repository is slow, you can download the ZIP files of the SDKs and manually integrate them into your project as instructed in the documents below.
<table>
<tr>
<th>SDK</th>
<th>Download Page</th>
<th>Integration Guide</th>
</tr>
<tr>
<td>TRTC SDK</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34615">Download</a></td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/35092">Integration Documentation</a></td>
</tr>
<tr>
<td>IM SDK</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">Download</a></td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/34306">Integration document</a></td>
</tr>
</table>

[](id:model.step2)
### Step 2. Configure permission requests

Configure camera and mic permission requests by adding `Privacy - Camera Usage Description` and `Privacy - Microphone Usage Description` in `info.plist`.

[](id:model.step3)
### Step 3. Import the `TUICalling` component
**To import the component through CocoaPods**, follow the steps below:
1. Copy the `Source`, `Resources`, and `TXAppBasic` folders and the `TUICalling.podspec` file under the demo project directory to your project directory.
2. Add the following dependencies to your `Podfile` and run `pod install` to complete the import.
<dx-codeblock>
::: swift
 pod 'TXAppBasic', :path => "../TXAppBasic/"
 pod 'TXLiteAVSDK_TRTC'
 pod 'TUICalling', :path => "../", :subspecs => ["TRTC"] 
:::
</dx-codeblock>

[](id:model.step4)

### Step 4. Initialize the component and log in

1. Call `TUICallingManager.sharedInstance()` to initialize the component.
2. Call `TUILogin.initWithSdkAppID(SDKAPPID)` to initialize login.
3. Call `TUILogin.login(userId, userSig)` to log in to the component. Specify the key parameters as described below:
<table>
<tr><th>Parameter</th><th>Description</th></tr><tr>
<tr>
<td>sdkAppID</td>
<td>You can view `SDKAppID` in the <a href="https://console.cloud.tencent.com/trtc/app">TRTC console</a>.</td>
</tr><tr>
<td>userId</td>
<td>ID of the current user, which is a string that can contain letters (a-z and A-Z), digits (0-9), hyphens (-), and underscores (_). We recommend you set it based on your business account system.</td>
</tr><tr>
<td>userSig</td>
<td>Tencent Cloud's proprietary security signature. For the calculation method, please see <a href="https://intl.cloud.tencent.com/document/product/647/35166">UserSig</a>.</td>
</tr></table>

<dx-codeblock>
::: swift
// Initialize the component
TUICallingManager.sharedInstance();
// Log in to the component
TUILogin.initWithSdkAppID(SDKAPPID)
TUILogin.login(userId, userSig) {
   print("login success")
} fail: { code, errorDes in
   print("login failed, code:\(code), error: \(errorDes ?? "nil")")
}
:::
</dx-codeblock>

[](id:model.step5)

### Step 5. Make an audio/video call

1. Caller: call `call();` of `TUICallingManager` to initiate a call, passing in the user IDs (`userIDs`) and call type (`type`). For the call type, you can pass in `.audio` (audio call) or `.video` (video call). If only one user ID is passed in for `userIDs`, the call is a one-to-one call; if two or more user IDs are passed in, the call is a group call.
2. Callee: If a callee is logged in, the answering view will be displayed. If you want offline users to receive call invitations, please see [Enable offline call answering](#model.offline).

<dx-codeblock>
::: swift
// 2. Register the listener
TUICallingManager.shareInstance().setCallingListener(listener: TUICallingListerner())

// 2. Set whether to enable custom views (disabled by default)
TUICallingManager.shareInstance().enableCustomViewRoute(enable: true)

// 3. Set callbacks
public func shouldShowOnCallView() -> Bool {
    return true;
}

public func callStart(userIDs: [String], type: TUICallingType, role: TUICallingRole, viewController: UIViewController?) {         if let vc = viewController {
        callingVC = vc;
        vc.modalPresentationStyle = .fullScreen
            
        if var topController = UIApplication.shared.keyWindow?.rootViewController {
            while let presentedViewController = topController.presentedViewController {
                topController = presentedViewController
            }
                
            if let navigationVC = topController as? UINavigationController {
                if navigationVC.viewControllers.contains(self) {
                    present(vc, animated: false, completion: nil)
                } else {
                    navigationVC.popToRootViewController(animated: false)
                    navigationVC.pushViewController(self, animated: false)
                    navigationVC.present(vc, animated: false, completion: nil)
                }
            } else {
                topController.present(vc, animated: false, completion: nil)
            }
        }
    }
}

public func callEnd(userIDs: [String], type: TUICallingType, role: TUICallingRole, totalTime: Float) {
    callingVC.dismiss(animated: true, completion: nil)
}
    
public func onCallEvent(event: TUICallingEvent, type: TUICallingType, role: TUICallingRole, message: String) {
       	
}
// 4. Make a call
TUICallingManager.shareInstance().call(userIDs, .video)
:::
</dx-codeblock>

[](id:model.offline)


### Step 6. Enable offline call answering

>?If your project does not require the offline answering feature, for example, if it offers online customer service, your integration can end at [step 5](#model.step5). If your project is a social networking service, we recommend you enable offline answering.

The IM SDK supports offline push, but additional configuration is required to enable the feature.

1. Apply for an Apple push certificate. For detailed directions, please see [Obtaining Apple Push Notification Service Certificates](https://intl.cloud.tencent.com/document/product/1047/34346).
2. Configure offline push on the backend and client. For detailed directions, please see [Offline Push (iOS)](https://intl.cloud.tencent.com/document/product/1047/39157).
3. The offline push API has been integrated into the signaling API (`sendModel`) of `TRTCCallingImpl`. After completing the offline push configuration for your application, you will be able to send notifications to offline users.

[](id:api)

## Component APIs

The table below lists the APIs of the `TUICalling` component.

| API        | Description                                                  |
| --------------- | --------------------------------------------------------- |
| call            | Sends call invitations by user ID.         |
| receiveAPNSCalled          | Answers a call.                                      |
| setCallingListener          | Sets the listener.                                     |
| setCallingBell          | Sets the ringtone (preferably shorter than 30s).                                                 |
| enableMuteMode | Enables/Disables the mute mode.    |
| enableCustomViewRoute      | Enables/Disables custom views. After enabling custom views, you will receive a `CallingView` instance in the callback for calling/being called, and can decide how to display the view by yourself. The view must be displayed full screen or in proportion to the screen size; otherwise, an error may occur.           |

