## Overview
This document provides sample code for integrating with the SDK and launching TPNS. (SDK version: v1.0+)
>!If you are migrating from the [XG Platform](https://xg.qq.com) to TPNS, please be sure to:
>1. [Unregister XG platform service API](#zhuxiao).
>2. Implement corresponding changes based on the application integration conditions and then return to this document.
>3. Complete the integration as described below.

## SDK Composition
- doc folder: TPNS SDK for iOS development guide.
- demo folder: it contains demo projects and TPNS SDK (only the OC demo is included. For the Swift demo, please go to [TGit](https://git.code.tencent.com/tpns/XG-Demo-Swift)). 

## SDK Integration
### Preparations for integration
1. Before integrating the SDK, please log in to the [TPNS Console](https://console.cloud.tencent.com/tpns) and create the product and iOS application. For detailed directions, please see [Creating Products and Applications](https://intl.cloud.tencent.com/document/product/1024/32603).
   ![](https://main.qcloudimg.com/raw/e77221c1f77b71e6087860a9cf6b60af.png)
2. Click **Configuration Management** to enter the management page.
   ![](https://main.qcloudimg.com/raw/f051b5d7fa3a7a3e8c4c9498ff39007b.png)
3. Click **Upload Certificate** to complete the upload. For more information on how to get a push certificate, please see [Acquisition of Push Certificate](https://main.qcloudimg.com/raw/320272c9e0afb1ece871d6562600d606.png).
   ![](https://main.qcloudimg.com/raw/5ea7fd7ec5ae1e7e4a31622a5c41ab00.png)
4. After the certificate is uploaded, get `Access ID` and `Access KEY` from the application information column.

### SDK import (two methods)
#### Method 1. Import through Cocoapods
Download through Cocoapods:
``` 
pod 'TPNS-iOS' 
```
>?
> - For the first download, you need to log in to the [git address](https://git.code.tencent.com/users/sign_in) to [set the username and password](https://code.tencent.com/help/productionDoc/profile#password) in **Account**. After successful configuration, enter the corresponding username and password in Terminal. Subsequently, no login is required on the current PC.
> - Due to the change of the git address, if the pod prompts `Unable to find a specification for 'TPNS-iOS'`, you need to run the following command to update the git and confirm the version:
>``` 
pod repo update
pod search TPNS-iOS
pod install // Install the SDK 
>```

#### Method 2. Import manually
1. Enter the [TPNS Console](https://console.cloud.tencent.com/tpns) and click **[SDK Download](https://console.cloud.tencent.com/tpns/sdkdownload)** on the left sidebar to go to the download page. Select the SDK version to download and click **Download** in the "Operation" column.
2. Open the SDK folder under the `demo` directory. Add `XGPush.h` and `libXG-SDK-Cloud.a` to the project. Open the `---XGPushStatistics` folder and get `XGMTACloud.framework`.
3. Add the following frameworks to Build Phases:
 ```
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
4. After the frameworks are added, the library references are as follows:
![](https://main.qcloudimg.com/raw/92f32ba9287713e009988ba8ee962ec8.png)

### Project configuration
1. Enabled Push Notifications in Project Configuration and Background Modes as shown below:
![](https://main.qcloudimg.com/raw/549acb8c1cf61c1d2f41de4762baf47b.png)
2. Add the compilation parameter `-ObjC` .
![](https://main.qcloudimg.com/raw/b0b74cec883f69fb0287fedc7bad4140.png)
If `checkTargetOtherLinkFlagForObjc` reports an error, it means that `-ObjC` has not been added to `Other link flags` in `build setting`.

>! If your application service access point is Guangzhou, the SDK implements this configuration by default.
If your application service access point is Singapore or Hong Kong (China), please follow the steps below to complete the configuration.
>1. Decompress the SDK file package and add the `XGPushPrivate.h` file in the SDK directory to the project.
>2. Call the configuration `domain name` API in the header file before calling the `startXGWithAccessID:accessKey:delegate:` method (SDK v1.2.7.2+):

To integrate with the Singapore service access point, set the domain name to ```tpns.sgp.tencent.com```.
**Sample**
``` object-c
 [[XGPush defaultManager] configureClusterDomainName:@"tpns.sgp.tencent.com"];
```
To integrate with the Hong Kong (China) service access point, set the domain name to ```tpns.hk.tencent.com```.
**Sample**
``` object-c
 [[XGPush defaultManager] configureClusterDomainName:@"tpns.hk.tencent.com"];
```

### Connection sample
Call the API for launching TPNS and implement the method in the `XGPushDelegate` protocol as needed to launch the push service.
1. Launch TPNS. The `AppDelegate` sample is as follows:

```Objective-C
@interface AppDelegate () <XGPushDelegate>
@end 
/**
@param AccessID   `AccessID` applied for in the TPNS Console
@param AccessKey    `AccessKey` applied for in the TPNS Console
@param delegate   Callback object
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
/// @param notification   Message object (there are two types: `NSDictionary` and `UNNotification`. For detailed interpretations, please see the sample code)
/// @note   This callback is the callback for receipt of notification messages in the foreground and of silent messages in all states (the unified click callback should be used for message clicks)
/// Message type description: if `msgtype` in the `xg` field is 1, it means notification message; if `msgtype` is 2, it means silent message
- (void)xgPushDidReceiveRemoteNotification:(nonnull id)notification withCompletionHandler:(nullable void (^)(NSUInteger))completionHandler{
 /// code
} 
 /// Unified click callback
/// @param response   It is `UNNotificationResponse` on iOS 10+/macOS 10.14+ or `NSDictionary` on an older version
- (void)xgPushDidReceiveNotificationResponse:(nonnull id)response withCompletionHandler:(nonnull void (^)(void))completionHandler {
  /// code
}
```

## Notification Service Extension Plugin Integration
The SDK provides the Service Extension API, which can be called by the client to use the following extensions:
- Collect precise statistics of message arrivals.
- Receive images and audiovisual rich media messages.

For the integration steps, please see [Notification Service Extension Use Instructions](https://intl.cloud.tencent.com/document/product/1024/30730).
>! If this API is not integrated, the **Reached** number cannot be counted.

## Debugging Method
#### Enabling debug mode
Enable debug mode to view detailed TPNS debug information in the end terminal, facilitating fault location.

#### Sample code
```
// This is to enable debugging
[[XGPush defaultManager] setEnableDebug:YES];
```

#### Implementing `XGPushDelegate` protocol
During debugging, we recommend you implement this method in the protocol to get detailed debugging information.
```objective-c
/**
@brief   Callback for TPNS registration
@param deviceToken   `Device Token` generated by APNs
@param xgToken   `Token` generated by TPNS, which needs to be used during message push. TPNS maintains the mapping relationship between this value and the `Device Token` of APNs
@param error   Error message. If `error` is `nil`, the push service has been successfully registered
@note TPNS SDK1.2.6.0+
*/
- (void)xgPushDidRegisteredDeviceToken:(nullable NSString *)deviceToken xgToken:(nullable NSString *)xgToken error:(nullable NSError *)error;

/// Callback for TPNS registration failure
/// @param error   Error message for registration failure
/// @note   TPNS SDK1.2.7.1+
- (void)xgPushDidFailToRegisterDeviceTokenWithError:(nullable NSError *)error {
}
```

#### Observing logs
If Xcode console displays a log similar to the one below, the client has properly integrated the SDK.

```javascript
[TPNS] Current device token is 9298da5605c3b242261b57****376e409f826c2caf87aa0e6112f944
[TPNS] Current TPNS token is 00c30e0aeddff1270d8****dc594606dc184  
```
>!Use an XG 36-bit token for pushing to a single target device.

## Unified Message Receipt and Message Click Callback Description
Unified message receipt callback. This callback will be used when the application receives a notification message in the foreground and receives a silent message in all states (foreground, background, closed).
```objective-c
- (void)xgPushDidReceiveRemoteNotification:(nonnull id)notification withCompletionHandler:(nullable void (^)(NSUInteger))completionHandler;
```
>!
>- When the application receives a notification message in the foreground or a silent message in all states, the unified message receipt callback `xgPushDidReceiveRemoteNotification` will be triggered.
The following is the sample code for differentiating notification message and silent message received in the foreground:
>```
NSDictionary *tpnsInfo = notificationDic[@"xg"];
NSNumber *msgType = tpnsInfo[@"msgtype"];
 if ([UIApplication sharedApplication].applicationState == UIApplicationStateActive && msgType.integerValue == 1) {
        /// Receipt of notification message in the foreground
    } else {
        /// Silent message
    }
>```
>- If the unified message receipt callback `xgPushDidReceiveRemoteNotification` is implemented, then there is no need to implement `application:didReceiveRemoteNotification:fetchCompletionHandler` again.


Unified message click callback. This callback method is the notification message click callback in all states of the application (foreground, background, and closed).
```objective-c
/// Unified click callback
/// @param response   It is `UNNotificationResponse` on iOS 10+/macOS 10.14+ or `NSDictionary` on an older version
/// @note   TPNS SDK1.2.7.1+
- (void)xgPushDidReceiveNotificationResponse:(nonnull id)response withCompletionHandler:(nonnull void (^)(void))completionHandler;
```



## Advanced Configuration (Optional)
<span id="zhuxiao"></span>
### Unregistering XG platform service
If the application push service is migrated from the [XG platform](https://xg.qq.com) to the TPNS platform, you need to call the API of `TPNS SDK(1.2.5.3+)` to unregister the device information on the XG platform.

#### API

```objective-c
// TPNS `accessId` (TPNS SDK v2 and v3 supported)
@property uint32_t freeAccessId;
```

#### Usage

- Import the header file `XGForFreeVersion.h`
- Call this API before `startXGWithAccessID:accessKey:delegate:`. Please see the sample below:

```objective-c
[XGForFreeVersion defaultForFreeVersion].freeAccessId = 2200262432;
[[XGPush defaultManager] startXGWithAccessID: <#your tpns access ID#>appKey:<#your tpns access key#> delegate:<#your delegate#>];
```
>!If the above configuration is not completed, duplicate messages may appear when pushing on both the XG and TPNS platforms at the same time.


<span id="QHToken"></span>
### Suggestions on getting TPNS token
After you integrate the SDK, you are recommended to use gestures or other methods to display the TPNS token in the application's less commonly used UIs such as **About** or **Feedback**. Push through the console and RESTful API requires the TPNS token for token push. Subsequent troubleshooting will also require the TPNS token for problem locating.

#### Sample code
```objective-c
// Get the token generated by TPNS
[[XGPushTokenManager defaultTokenManager] xgTokenString];
```

