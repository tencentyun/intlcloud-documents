
## Overview
This document provides sample code for integrating with the SDK and launching TPNS. (SDK version: v1.0+)
>If you are migrating from the XG Platform (https://xg.qq.com) to TPNS, please be sure to:
1. [Unregister XG platform service API](#zhuxiao).
2. Implement corresponding changes based on the application integration conditions as instructed in the iOS migration guide and then return to this document.
3. Complete the integration as described below.

## SDK Composition
- doc folder: TPNS SDK for iOS development guide.
- demo folder: it mainly contains demo projects and TPNS SDK (only the OC demo is included. For the Swift demo, please go to [TGit](https://git.code.tencent.com/tpns/XG-Demo-Swift)). 



## SDK Integration
### Preparations for integration
1. Before integrating the SDK, you need to log in to the [TPNS Console](https://console.cloud.tencent.com/tpns) and create the product and iOS application. For detailed directions, please see [Creating Products and Applications](https://intl.cloud.tencent.com/document/product/1024/32603).
![](https://main.qcloudimg.com/raw/e77221c1f77b71e6087860a9cf6b60af.png)
2. Once the application is created, you can apply for trial for it as instructed in [Applying for Trial](https://intl.cloud.tencent.com/document/product/1024/32603#.E7.94.B3.E8.AF.B7.E8.AF.95.E7.94.A8) or purchase the TPNS service as instructed in [Purchasing Push Service](https://intl.cloud.tencent.com/document/product/1024/32604).
![](https://main.qcloudimg.com/raw/f051b5d7fa3a7a3e8c4c9498ff39007b.png)
3. Upload the push certificate on the **Configuration Management** page. You can get the push certificate as instructed in [Getting Certificate](https://intl.cloud.tencent.com/document/product/1024/30728).
 ![](https://main.qcloudimg.com/raw/320272c9e0afb1ece871d6562600d606.png)

4. After the certificate is uploaded, get `Access ID` and `Access KEY` from the Application Information column.

### SDK import
 - **Method 1. Import through Cocoapods**
Download through Cocoapods:
``` 
 pod 'TPNS-iOS' 
```
 >
  - For the first download, you need to log in to the [git address](https://git.code.tencent.com/users/sign_in) to [set the username and password](https://code.tencent.com/help/productionDoc/profile#password) in **Account** and then enter the corresponding username and password in Terminal. Subsequently, no login is required on the current PC.
  - Due to the change of the git address, if the pod prompts `Unable to find a specification for 'TPNS-iOS'`, you need to run the following command to update the git and confirm the version:
``` 
pod repo update
pod search TPNS-iOS
pod install // Install the SDK 
```

 - **Method 2. Import through carthage**
 Specify the dependent third-party libraries in the Cartfile file:
```
 github "xingePush/carthage-TPNS-iOS"
```
 - **Method 3. Import manually**
Enter the TPNS Console and click **[SDK Download](https://console.cloud.tencent.com/tpns/sdkdownload)** on the left sidebar to go to the download page. Select the SDK version to download, and click **Download** in the **Operations** column.
  - Open the SDK folder under the `demo` directory. Add `XGPush.h` and `libXG-SDK-Cloud.a` to the project. Open the `---XGPushStatistics` folder and get `XGMTACloud.framework`.
  - Add the following frameworks to `Build Phases`:

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
  - After the frameworks are added, the library references are as follows:
![](https://main.qcloudimg.com/raw/92f32ba9287713e009988ba8ee962ec8.png)

### Project configuration
1. Enabled Push Notifications in Project Configuration and Background Modes as shown below:
![](https://main.qcloudimg.com/raw/549acb8c1cf61c1d2f41de4762baf47b.png)
2. Add the compilation parameter `-ObjC` .
![](https://main.qcloudimg.com/raw/b0b74cec883f69fb0287fedc7bad4140.png)
> If `checkTargetOtherLinkFlagForObjc` reports an error, it means that `-ObjC` has not been added to `Other link flags` in `build setting`.

### Connection sample
Call the API for launching TPNS and implement the method in the `XGPushDelegate` protocol as needed to launch the push service.
1. Launch TPNS. The `AppDelegate` sample is as follows:
   ```Objective-C
@interface AppDelegate () <XGPushDelegate>
@end 
/**
@param appID   `AccessID` applied for in the TPNS Console
@param appKey   `AccessKey` applied for in the TPNS Console
@param delegate   Callback object
**/
-(BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions 
{
[[XGPush defaultManager] startXGWithAppID:<#your appID#> appKey:<#your appKey#>  delegate:<#your delegate#>];
return YES;
}
   ```
 ```
2. In `AppDelegate`, choose to implement the method in the `XGPushDelegate` protocol:
 ```objective-c
		/// Unified callback for message receipt
		/// @param notification   Message object
		/// @param completionHandler   Completion callback
		/// Message type description: if `msgtype` in the `xg` field is 1, it means notification message; if `msgtype` is 2, it means silent message
		/// notification message object description: there are two types: `NSDictionary` and `UNNotification`. For detailed interpretations, please see the sample code
		- (void)xgPushDidReceiveRemoteNotification:(nonnull id)notification withCompletionHandler:(nullable void (^)(NSUInteger))completionHandler{
		/// code
		} 
		#if __IPHONE_OS_VERSION_MAX_ALLOWED >= __IPHONE_10_0
		/// New API in iOS 10
		/// iOS 10 will use the new API, while iOS 10 or below will use the legacy API
		/// Application user clicks a notification and selects a behavior in the notification
		/// This callback will be used in both local push and remote push
		- (void)xgPushUserNotificationCenter:(UNUserNotificationCenter *)center
      didReceiveNotificationResponse:(UNNotificationResponse *)response
               withCompletionHandler:(void (^)(void))completionHandler {
                                                         /// code
	}
	#endif
 ```


## Notification Service Extension Plugin Integration
To implement the features of arrived data reporting and rich media messaging, the SDK provides a Service Extension API, which can be called by the client to listen on the arrivals of messages and send rich media messages.
### Connection method
#### Method 1. Import through Cocoapods
Download through Cocoapods:

``` 
pod 'TPNS-iOS-Extension' 
```
**Use instructions:**
1. Create a `Notification Service Extension` target in `Application Extension` type, such as `XXServiceExtension`.
2. Add the configuration item of `XXServiceExtension` in Podfile.

**Sample**
Display effect after the configuration item is added in Podfile:
```
target ‘XXServiceExtension'do
     pod 'TPNS-iOS-Extension' , '~>1.2.6.1' 
end
```
> You are recommended to use it together with pod 'TPNS-iOS' version 1.2.6.1 or above.


#### Method 2. Import manually
For the integration guide, please see [Notification Service Extension Use Instructions](https://intl.cloud.tencent.com/document/product/1024/30730).

>If this API is not integrated, the `number of arriving messages` and `number of clicks` in the statistics will be the same.

#### Integration guide for service outside Mainland China
1. Decompress the SDK file package and add the `XGPushPrivate.h` file in the SDK directory to the project.
2. Call the configuration `HOST` API in the header file:
 - To integrate with a cluster in Singapore, set `HOST` to `https://api.tpns.sgp.tencent.com` and `PORT` to 0.
 - To integrate with a cluster in Hong Kong (China), set `HOST` to `https://api.tpns.hk.tencent.com` and `PORT` to 0.

**Sample**
``` object-c
[[XGPush defaultManager] configureHost:@"https://api.tpns.hk.tencent.com" port:0]
```
>The `HOST` configuring API should be called before the `startXGWithAppID` method.


## Debugging Method
#### Enabling debug mode
Enable debug mode to view detailed TPNS debug information in the end terminal, facilitating fault location.

#### Sample code
```
// This is to enable debugging
[[XGPush defaultManager] setEnableDebug:YES];
```

#### Implementing `XGPushDelegate` protocol

During debugging, you are recommended to implement this method in the protocol to get detailed debugging information.

```objective-c
/**
 @brief   This registers the callback of the push service
 @param deviceToken   `Device Token` generated by APNs
 @param xgToken   `Token` generated by TPNS, which needs to be used during message push. TPNS maintains the mapping relationship between this value and the `Device Token` of APNs
 @param error   Error message. If `error` is `nil`, the push service has been successfully registered
 */
- (void)xgPushDidRegisteredDeviceToken:(nullable NSString *)deviceToken xgToken:(nullable NSString *)xgToken error:(nullable NSError *)error;
```

#### Observing logs
If Xcode console displays a log similar to the one below, the client has properly integrated the SDK.

```javascript
[TPNS] Current device token is 9298da5605c3b242261b57****376e409f826c2caf87aa0e6112f944
[TPNS] Current TPNS token is 00c30e0aeddff1270d8****dc594606dc184  
```
>Use a XG 36-bit token for pushing to a single target device.

## Unified Message Receipt and Message Click Callback Description

- If the message is clicked on devices above iOS 10.0, this function will be called:
```objective-c
	- (void)xgPushUserNotificationCenter:(UNUserNotificationCenter *)center didReceiveNotificationResponse:(UNNotificationResponse *)response withCompletionHandler:(void (^)(void))completionHandler;
```
- If the message is clicked on devices below iOS 10.0, this function will be called:
```objective-c
	- (void)xgPushDidReceiveRemoteNotification:(nonnull id)notification withCompletionHandler:(nullable void (^)(NSUInteger))completionHandler;
```

- If a silent message is received, this function will be called:
```objective-c
	- (void)xgPushDidReceiveRemoteNotification:(nonnull id)notification withCompletionHandler:(nullable void (^)(NSUInteger))completionHandler;
```

>
>- `xgPushDidReceiveRemoteNotification` will be used to receive message callback regardless of whether the message is clicked or not in the application in the foreground 
>- You are not recommended to implement the `application:didReceiveRemoteNotification:fetchCompletionHandler` API as it is processed inside the SDK

<span id="zhuxiao"></span>
## Unregistering XG Platform Service

If the application push service is migrated from the XG platform (https://xg.qq.com) to the TPNS platform, you need to call the API of `TPNS SDK(1.2.5.3+)` to unregister the device information on the XG platform.

#### API

```objective-c
// TPNS `accessId` (TPNS SDK v2 and v3 supported)
@property uint32_t freeAccessId;
```

#### Usage

- Import the header file `XGForFreeVersion.h` 
- Call this API before `startXGWithAppID:appKey:delegate:`. Please see the sample below:

```objective-c
[XGForFreeVersion defaultForFreeVersion].freeAccessId = 2200262432;
[[XGPush defaultManager] startXGWithAppID: <#your tpns access ID#>appKey:<#your tpns access key#> delegate:<#your delegate#>];
```
>If the above configuration is not completed, duplicate messages may appear when pushing on both the XG and TPNS platforms at the same time.



## Suggestions on Integration
<span id="QHToken"></span>
### Getting token
After you integrate the SDK, you are recommended to use gestures or other methods to display the token in the application's less commonly used UIs such as **About** or **Feedback**. Doing so will facilitate subsequent troubleshooting.

#### Sample code
```objective-c
// Get the token generated by TPNS
[[XGPushTokenManager defaultTokenManager] xgTokenString];
// Get the `DeviceToken` generated by APNs
[[XGPushTokenManager defaultTokenManager] deviceTokenString];
```




