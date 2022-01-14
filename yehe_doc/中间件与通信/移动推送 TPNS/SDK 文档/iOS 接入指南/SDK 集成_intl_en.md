## Overview
This document provides sample code for integrating with the TPNS SDK and launching the TPNS service (SDK version: v1.0+).


## SDK Composition
- `doc` folder: contains the development guide of the TPNS SDK for iOS.
- `demo` folder: contains demo projects and the TPNS SDK (only the OC demo is included. For the Swift demo, please go to [TGit](https://git.code.tencent.com/tpns/XG-Demo-Swift)). 

## SDK Integration
### Preparing for integration
1. Before integrating the SDK, you need to log in to the [TPNS console](https://console.cloud.tencent.com/tpns) and create the product and iOS application. For detailed directions, please see [Creating Products and Applications](https://intl.cloud.tencent.com/document/product/1024/32603).
   ![](https://main.qcloudimg.com/raw/e77221c1f77b71e6087860a9cf6b60af.png)
2. Click **Configuration Management** to go to the management page.
   ![](https://main.qcloudimg.com/raw/f051b5d7fa3a7a3e8c4c9498ff39007b.png)
3. Click **Upload Certificate** to complete the upload. For more information on how to get a push certificate, please see [Acquisition of Push Certificate](https://intl.cloud.tencent.com/document/product/1024/30728).
   ![](https://main.qcloudimg.com/raw/5ea7fd7ec5ae1e7e4a31622a5c41ab00.png)
4. After the certificate is uploaded, get `AccessID` and `AccessKey` from the application information column.

### Importing the SDK (two methods)
#### Method 1. Import through CocoaPods
Download through CocoaPods:
``` 
pod 'TPNS-iOS', '~> version'  // If the version is not specified, the latest version of the local pod `TPNS-iOS` will be downloaded
```
>?
> - For a first download, you need to log in to [TGit](https://git.code.tencent.com/users/sign_in) to [set the username and password](https://code.tencent.com/help/productionDoc/profile#password) on the **Account** page. After successful setting, you only need to enter the corresponding username and password in the terminal, and you do not need to log in again on the current PC.
> - Due to the change of the repository address, if the pod prompts `Unable to find a specification for 'TPNS-iOS'`, you need to run the following command to update the repository and confirm the version:
>	``` 
	pod repo update
	pod search TPNS-iOS
	pod install // Install the SDK 
		```
``` 

#### Method 2. Import manually
1. Log in to the [TPNS console](https://console.cloud.tencent.com/tpns) and click **[SDK Download](https://console.cloud.tencent.com/tpns/sdkdownload)** in the left sidebar to go to the download page. Select the SDK version to download, and click **Download** in the **Operations** column.
2. Open the SDK folder under the `demo` directory. Add `XGPush.h` and `libXG-SDK-Cloud.a` to the project. Open the `XGPushStatistics` folder and obtain `XGMTACloud.framework`.
3. Import the `InAppMessage` folder into the project and add the search path in **Build Setting > **Framework Search Paths** (if your SDK version is below 1.2.8.0, you can skip this step).
4. Add the following frameworks to `Build Phases`:
```
 * XGInAppMessage.framework
 * XGMTACloud.framework
 * CoreTelephony.framework
 * SystemConfiguration.framework
 * UserNotifications.framework
 * libXG-SDK-Cloud.a 
 * libz.tbd
 * CoreData.framework
 * CFNetwork.framework
 * libc++.tbd
```
5. After the frameworks are added, the library references are as follows:
![](https://main.qcloudimg.com/raw/79976648574060954cebfb894cc5cdd4.png)


### Project configuration
1. Open the push notification in the project configuration and backend modes, as shown in the following figure:
![](https://main.qcloudimg.com/raw/549acb8c1cf61c1d2f41de4762baf47b.png)
1.1 To use the "Time Sensitive Notifications" feature introduced in iOS 15, please enable `Time Sensitive Notifications` in `Capabilities`.
![](https://qcloudimg.tencent-cloud.cn/raw/f07a8d6912cc85830a99358dcf66d28a.png)
2. Add the compilation parameter `-ObjC`.
![](https://main.qcloudimg.com/raw/b0b74cec883f69fb0287fedc7bad4140.png)
If `checkTargetOtherLinkFlagForObjc` reports an error, it means that `-ObjC` has not been added to `Other link flags` in `build setting`.
>! If the service access point of your application is Guangzhou, the SDK implements this configuration by default. The domain name for Guangzhou is `tpns.tencent.com`.
>

If the service access point of your application is Shanghai, Singapore, or Hong Kong (China), please follow the step below to complete the configuration:
1. Decompress the SDK file package and add the `XGPushPrivate.h` file in the SDK directory to the project.
2. Call the domain name configuration API in the header file before calling the `startXGWithAccessID:accessKey:delegate:` method.

To integrate with the Shanghai service access point, set the domain name to `tpns.sh.tencent.com`.
**Example**
​``` object-c
/// @note TPNS SDK1.2.7.1+
[[XGPush defaultManager] configureClusterDomainName:@"tpns.sh.tencent.com"];
```
To integrate with the Singapore service access point, set the domain name to `tpns.sgp.tencent.com`.
**Example**
``` object-c
/// @note TPNS SDK1.2.7.1+
[[XGPush defaultManager] configureClusterDomainName:@"tpns.sgp.tencent.com"];
```
To integrate with the Hong Kong (China) service access point, set the domain name to `tpns.hk.tencent.com`.
**Example**
``` object-c
/// @note TPNS SDK1.2.7.1+
[[XGPush defaultManager] configureClusterDomainName:@"tpns.hk.tencent.com"];
```
To integrate with the Guangzhou service access point, set the domain name to `tpns.tencent.com`.
**Example**
```
/// @note TPNS SDK1.2.7.1+
[[XGPush defaultManager] configureClusterDomainName:@"tpns.tencent.com"];
```



### Integration sample
Call the API for launching TPNS and implement the method in the `XGPushDelegate` protocol as needed to launch the push service.
1. Launch TPNS. The `AppDelegate` sample is as follows:

```Objective-C
@interface AppDelegate () <XGPushDelegate>
@end 
/**
@param AccessID  //`AccessID` applied for in the TPNS console
@param AccessKey  //`AccessKey` applied for in the TPNS console
@param delegate  //Callback object
**/
-(BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions 
{
  [[XGPush defaultManager] startXGWithAccessID:<your AccessID> accessKey:<your AccessKey> delegate:self];
return YES;
}
```

2. In `AppDelegate`, choose to implement the method in the `XGPushDelegate` protocol:

```objective-c
/// Unified callback for message receipt
/// @param notification   //Message object (there are two types: `NSDictionary` and `UNNotification`. For detailed interpretations, please see the sample code)
/// @note   //This callback is the callback for receipt of notification messages in the foreground and silent messages in all states (unified message click callback should be used for message clicks)
/// Message type description: if `msgtype` in the `xg` field is `1`, it means notification message; if `msgtype` is `2`, it means silent message.
- (void)xgPushDidReceiveRemoteNotification:(nonnull id)notification withCompletionHandler:(nullable void (^)(NSUInteger))completionHandler{
 /// code
} 
 /// Unified message click callback
/// @param response   //`UNNotificationResponse` for iOS 10+ and macOS 10.14+, or `NSDictionary` for earlier versions
- (void)xgPushDidReceiveNotificationResponse:(nonnull id)response withCompletionHandler:(nonnull void (^)(void))completionHandler {
  /// code
}
```

## Notification Service Extension Plugin Integration
The SDK provides the Service Extension API, which can be called by the client to use the following extended features:
- Collect precise statistics of message arrivals through the APNs channel.
- Receive images and audiovisual rich media messages through the APNs channel.

For the integration steps, please see [Notification Service Extension](https://intl.cloud.tencent.com/document/product/1024/30730).
>!If the Service Extension API is not integrated, arrival statistics cannot be collected for the APNs channel.


## Debugging Method
#### Enable debug mode
After enabling debug mode, you can view the detailed TPNS debug information on the device for troubleshooting.

#### Sample code
```
// Enable debugging
[[XGPush defaultManager] setEnableDebug:YES];
```

#### Implementing the `XGPushDelegate` protocol
During debugging, it is recommended that you implement the following method in the protocol to obtain detailed debugging information.
```objective-c
/**
@brief   //Callback for TPNS registration
@param deviceToken   //`Device Token` generated by APNs
@param xgToken   // token generated by TPNS, which needs to be used during message push. TPNS maintains the mapping relationship between this value and the device token generated by APNs
@param error   //Error message. If `error` is `nil`, the push service has been successfully registered
@note TPNS SDK1.2.6.0+
*/
- (void)xgPushDidRegisteredDeviceToken:(nullable NSString *)deviceToken xgToken:(nullable NSString *)xgToken error:(nullable NSError *)error;

/// Callback for TPNS registration failure
/// @param error   //Error message for registration failure
/// @note TPNS SDK1.2.7.1+
- (void)xgPushDidFailToRegisterDeviceTokenWithError:(nullable NSError *)error {
}
```

#### Observing logs
If the Xcode console displays a log similar to the one below, the client has properly integrated the SDK.

```javascript
[TPNS] Current device token is 9298da5605c3b242261b57****376e409f826c2caf87aa0e6112f944
[TPNS] Current TPNS token is 00c30e0aeddff1270d8****dc594606dc184  
```
>!Use a TPNS 36-bit token for pushing to a single target device.

## Unified Message Receipt Callback and Unified Message Click Callback
**Unified message receipt callback for the TPNS and APNs channels:** this callback will be triggered when the application receives a notification message in the foreground and receives a silent message in all states (foreground, background, and shutdown).
```objective-c
- (void)xgPushDidReceiveRemoteNotification:(nonnull id)notification withCompletionHandler:(nullable void (^)(NSUInteger))completionHandler;
```
>?
- When the application receives a notification message in the foreground or a silent message in all states, the unified message receipt callback `xgPushDidReceiveRemoteNotification` will be triggered.
The following is the sample code for differentiating the receipt of a notification message in the foreground or a silent message in all states.
```
NSDictionary *tpnsInfo = notificationDic[@"xg"];
NSNumber *msgType = tpnsInfo[@"msgtype"];
if (msgType.integerValue == 1) {
        /// Receipt of a notification message in the foreground
    } else if (msgType.integerValue == 2) {
        /// Receipt of a silent message
    } else if (msgType.integerValue == 9) {
        /// Receipt of a local notification (TPNS local notification)
    }
```

**Unified message click callback:** this callback applies to the notification messages of the application in states (foreground, background and shutdown).
```objective-c
/// Unified message click callback
/// @param response will be `UNNotificationResponse` for iOS 10+/macOS 10.14+, or `NSDictionary` for earlier versions.
/// @note TPNS SDK1.2.7.1+
- (void)xgPushDidReceiveNotificationResponse:(nonnull id)response withCompletionHandler:(nonnull void (^)(void))completionHandler;
```

>!
>
>- The unified message receipt callback `xgPushDidReceiveRemoteNotification` of the TPNS will process message receipt and then automatically call the `application:didReceiveRemoteNotification:fetchCompletionHandler` method, which, however, may also be hooked by other SDKs.
- If you have integrated only the TPNS platform, you are advised not to implement the system notification callback method; use only the TPNS notification callback method instead.
- If you have integrated multiple push platforms and need to process the services of other platforms using the `application:didReceiveRemoteNotification:fetchCompletionHandler` method, please see the following guidelines to avoid repeated service processing:
 - You need to distinguish between message platforms. After getting the message dictionary in the two message callback methods, use the `xg` field to tell whether it is a TPNS message. If it is a TPNS message, process it using the `xgPushDidReceiveRemoteNotification` method; otherwise, process it using the `application:didReceiveRemoteNotification:fetchCompletionHandler` method.
 - If both `xgPushDidReceiveRemoteNotification` and `application:didReceiveRemoteNotification:fetchCompletionHandler` are executed, then `completionHandler` needs to be called only once in total. If it is also called by other SDKs, make sure that it is called only once overall; otherwise, crashes may occur.




## Advanced Configuration (Optional)

<span id="QHToken"></span>
### Suggestions on getting the TPNS token
After you integrate the SDK, we recommend you use gestures or other methods to display the TPNS token in the application's less commonly used UIs such as **About** or **Feedback**. The console and RESTful API requires the TPNS token to push messages. Subsequent troubleshooting will also require the TPNS token for problem locating.

#### Sample code
```objective-c
// Get the token generated by TPNS.
[[XGPushTokenManager defaultTokenManager] xgTokenString];
```
![]()

### Suggestions on getting TPNS running logs
After integrating the SDK, you are advised to use gestures or other methods to display TPNS running logs in the app’s less commonly used UI such as **About** or **Feedback**. Doing so will facilitate subsequent troubleshooting.

![]()
#### Sample code
```objective-c
[[XGPush defaultManager] uploadLogCompletionHandler:^(BOOL result, NSString * _Nullable errorMessage) {
NSString *title = result ? NSLocalizedString(@"report_log_info", nil) : NSLocalizedString(@"failed", nil);
if (result && errorMessage.length>0) {
UIPasteboard *pasteboard = [UIPasteboardgeneralPasteboard];
pasteboard.string = errorMessage;
}
[TPNSCommonMethodshowAlert:title message:errorMessage viewController:selfcompletion:nil];
}];

```




