
## Overview
This document provides sample code for integrating with the SDK and launching TPNS. (SDK version: v1.0+)

## SDK Composition
- doc folder: TPNS SDK for iOS development guide.
- demo folder: it mainly contains demo projects and TPNS SDK (only the OC demo is included. For the Swift demo, please go to [TGit](https://git.code.tencent.com/tpns/XG-Demo-Swift)). 



## Integration Steps
1. Log in to the [TPNS Console](https://console.cloud.tencent.com/tpns) and click **Product Management** on the left sidebar.
2. Go to the **Product Management** page and click **Add a Product**.
3. Go to the **Add a Product** page, and enter the product name and product details. Select the product type, and click **OK** to add a new product.
4. After the product is created, select **Configuration Management** on the left sidebar. Get `Access ID` and `SECRET KEY` from the "Application Info" column.
5. Import SDK:
 - **Method one: import using Cocoapods**
Download through Cocoapods:
``` 
 pod 'TPNS-iOS' 
```
 >
    - For the first download, you need to log in to the [git address](https://git.code.tencent.com/users/sign_in) to set the account and password in **Account** and then enter the corresponding account and password in Terminal. Subsequently, no login is required on the current PC.
    - Due to the change of the git address, if the pod prompts `Unable to find a specification for 'TPNS-iOS'`, you need to run the following command to update the git and confirm the version:
``` 
pod repo update
pod search TPNS-iOS
pod install // Install the SDK 
```  

 - **Method two: import using carthage**
 Specify the dependent third-party libraries in the Cartfile file:
```
 github "xingePush/carthage-TPNS-iOS"
```
 
 - **Method three: manual import**
Enter the TPNS Console and click **[SDK Download](https://console.cloud.tencent.com/tpns/sdkdownload)** on the left sidebar to go to the download page. Select the SDK version to download, and click **Download** in the **Operations** column.

6. Open the SDK folder under the demo directory. Add `XGPush.h` and `libXG-SDK-Cloud.a` to the project. Open the `XGPushStatistics` folder, and get `XGMTACloud.framework`.
7. Add the following frameworks to Build Phases:
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
8. After adding the frameworks, the library references are as follows:
![](https://main.qcloudimg.com/raw/92f32ba9287713e009988ba8ee962ec8.png)
9. Open the push notification in the project configuration and backend modes, as shown in the following figure:
![](https://main.qcloudimg.com/raw/549acb8c1cf61c1d2f41de4762baf47b.png)
10. Add the compilation parameter `-ObjC` .
![](https://main.qcloudimg.com/raw/b0b74cec883f69fb0287fedc7bad4140.png)

>If checkTargetOtherLinkFlagForObjc reports an error, it means -ObjC has not been added to Other link flags in build setting.

11. Call the API for launching TPNS and implement the method in the `XGPushDelegate` protocol as needed to launch the push service.
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
	2. In `AppDelegate`, choose to implement the method in the `XGPushDelegate` protocol:
	```objective-c
		/**
		 Callback of received push
		 @param application   UIApplication instance
		 @param userInfo: parameters specified during push
		 @param completionHandler: callback completed
		 */
		- (void)application:(UIApplication *)application 
					didReceiveRemoteNotification:(NSDictionary *)userInfo 
							fetchCompletionHandler:(void (^)(UIBackgroundFetchResult))completionHandler 
			{
				completionHandler(UIBackgroundFetchResultNewData);
		}
		// iOS 10 new callback API
		// Application user clicks the notification
		// Application user selects a behavior in the notification
		// This callback will be used in both local push and remote push
	#if __IPHONE_OS_VERSION_MAX_ALLOWED >= 	__IPHONE_10_0
		- (void)xgPushUserNotificationCenter:(UNUserNotificationCenter *)center 
					didReceiveNotificationResponse:(UNNotificationResponse *)response 
					withCompletionHandler:(void (^)(void))completionHandler 
					{
							completionHandler();
		}

		// This API will be used when the application pushes a notification in the notification panel
		- (void)xgPushUserNotificationCenter:(UNUserNotificationCenter *)center
					 willPresentNotification:(UNNotification *)notification 
							 withCompletionHandler:(void (^)(UNNotificationPresentationOptions))completionHandler
							 {
									 completionHandler(UNNotificationPresentationOptionBadge | UNNotificationPresentationOptionSound | UNNotificationPresentationOptionAlert);
		}
		#endif
	```


#### Integration method for cluster outside Mainland China
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



#### Implementing ```XGPushDelegate``` protocol

During debugging, it is recommended that you implement the second method in the protocol to get detailed debugging information.

```objective-c
/**
 @brief This monitors the start condition of the TPNS service (disused)

 @param isSuccess   This checks whether TPNS is successfully launched
 @param error: this message indicates an error in TPNS launch
 */
- (void)xgPushDidFinishStart:(BOOL)isSuccess error:(nullable NSError *)error;

/**
 @brief This registers the callback of the push service
 
 @param deviceToken   `Device Token` generated by APNs
 @param xgToken   `Token` generated by TPNS, which needs to be used when pushing messages. TPNS maintains the mapping relationship between this value and the `Device Token` of APNs
 @param error   Error message. If `error` is `nil`, the push service has been successfully registered
 */
- (void)xgPushDidRegisteredDeviceToken:(nullable NSString *)deviceToken xgToken:(nullable NSString *)xgToken error:(nullable NSError *)error;
```

#### Observing log
If Xcode console displays a log similar to the one below, the client has properly integrated the SDK.

```javascript
[xgpush]Current device token is 80ba1c251161a397692a107f0433d7fd9eb59991583a925030f1b913625a9dab
[xgpush]Current XG token is 05da87c0ae5973bd2dfa9e08d884aada5bb2
```
>Use a XG 36-bit token for pushing to a single target device.

## Custom Response Message Content

When an iOS device receives a push message and the user taps the message to open the application, the application will respond differently according to the status:

- This function will be invoked if the application status is "not running".
 - If `launchOptions` contains `UIApplicationLaunchOptionsRemoteNotificationKey`, it means that the user's tap on the push message will cause the application to launch.
 - If the corresponding key value is not included, it means that the application launch is not caused by the tap on the message but probably by the tap on the icon or other actions.
 ```objective-c
	- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions 
	{
			// Getting message content
			NSDictionary *remoteNotification = [launchOptions objectForKey:UIApplicationLaunchOptionsRemoteNotificationKey];
			// Processing logically based on the message content
	}
 ```
- If the application status is "in the foreground" or "in the background but still active".
 - On iOS 7.0+, if the Remote Notification feature is used, the following code needs to be used as the handler:
	```objective-c
	- (void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult))completionHandler;
	```
 - On versions above iOS 10.0, if the Remote Notification feature is used, you are recommended to add a `UserNotifications Framework` handler. Please use the following two methods in the `XGPushDelegate` protocol. The sample code is as follows:
	```objective-c
	- (void)xgPushUserNotificationCenter:(UNUserNotificationCenter *)center didReceiveNotificationResponse:(UNNotificationResponse *)response withCompletionHandler:(void (^)(void))completionHandler {
		NSLog(@"[XGDemo] click notification");
		completionHandler();
	}

	// This API needs to be called when the application pushes messages in the notification panel
	- (void)xgPushUserNotificationCenter:(UNUserNotificationCenter *)center willPresentNotification:(UNNotification *)notification withCompletionHandler:(void (^)(UNNotificationPresentationOptions))completionHandler {
		completionHandler(UNNotificationPresentationOptionBadge | UNNotificationPresentationOptionSound | UNNotificationPresentationOptionAlert);
	}
	```

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
- Call this API before `startXGWithAppID:appKey:delegate:`. See the sample below:

```objective-c
[XGForFreeVersion defaultForFreeVersion].freeAccessId = 2200262432;
[[XGPush defaultManager] startXGWithAppID: <#your tpns access ID#>appKey:<#your tpns access key#> delegate:<#your delegate#>];
```
>If the above configuration is not completed, duplicate messages may appear when pushing on both the XG and TPNS platforms at the same time.

## Suggestions on Integration
#### Notification service extension feature (required)
To implement the features of arriving data reporting and rich media messaging, the SDK provides the Service Extension API, which can be called by the client to listen to the arrival of messages and send rich media messages. You are strongly recommended to implement this API. For API integration guide, please see [Notification Service Extension Usage Instructions](https://intl.cloud.tencent.com/document/product/1024/30730).
>If this API is not integrated, the `number of arriving messages` and `number of clicks` in the statistics will be the same.

<span id="QHToken"></span>
#### Getting token (optional)
It is recommended that after you integrate the SDK, you use gestures or other methods to display the token in the application's less commonly used UI such as **About** or **Feedback**. Doing so will facilitate subsequent troubleshooting.

#### Sample code
```objective-c
// Get the token generated by TPNS
[[XGPushTokenManager defaultTokenManager] xgTokenString];
// Get the `DeviceToken` generated by APNs
[[XGPushTokenManager defaultTokenManager] deviceTokenString];
```



