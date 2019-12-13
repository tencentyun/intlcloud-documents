
## Overview
This document provides sample codes for integrating the SDK and launching TPNS. (SDK version: V1.0+ version）



## SDK composition
- doc folder: TPNS iOS SDK development guide.
- demo folder: mainly contains sample projects, the TPNS SDK. 



## Integration steps
1. Log in to the [TPNS Console](https://console.cloud.tencent.com/tpns), and click **Product Management** in the left sidebar.
2. Enter the **Product Management** page, and click **Add a Product**.
3. Go to the **Add a Product** page, and enter the product name and product details. Select the product type, and click **OK** to add a new product.
4. After the product is created, select **Application Management** > **Application List** to go to the application list and obtain the product AppID and AppKey. (AppID is Access ID, AppKey is Access Key.)
5. Import SDK:
 - **Method one: import using Cocoapods**
Use the Cocoapods download address:
 ``` 
 pod 'TPNS-iOS' 
 ```
 - **Method two: import using carthage**
 Specify the dependent third-party libraries in the Cartfile file:
 ```
 github "xingePush/carthage-TPNS-iOS"
 ```
 - **Method three: manual import**
Enter the TPNS Console and click **[SDK Download](https://console.cloud.tencent.com/tpns/sdkdownload)** in the left sidebar to go to the download page. Select the SDK version to download, and click **Download** in the **Operations** column.
6. Open the SDK folder under the demo directory. Add XGPush.h and libXG-SDK-Cloud.a to the project. Open the XGPushStatistics folder, and obtain XGMTACloud.framework.
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
```
8. After adding the frameworks, the library references are as follows:
![](https://main.qcloudimg.com/raw/e61961cd6db798d0f02d4b4c1a996fa0.png)
9. Open the push notification in the project configuration and backend modes, as shown in the following figure:
![](https://main.qcloudimg.com/raw/549acb8c1cf61c1d2f41de4762baf47b.png)
10. Add the compilation parameter ```-ObjC```.
![](https://main.qcloudimg.com/raw/b0b74cec883f69fb0287fedc7bad4140.png)

>If checkTargetOtherLinkFlagForObjc reports an error, it means -ObjC has not been added to Other link flags in build setting.

11. Call the API for launching TPNS and implement the method in the ```XGPushDelegate``` protocol as needed to launch the push service.
	1. Launch TPNS,  the ```AppDelegate``` sample is as follows:
	```objective-c
		 @interface AppDelegate () <XGPushDelegate>
		 @end

		 -(BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions 
				 {
						 [[XGPush defaultManager] startXGWithAppID:<#your AppID#> appKey:<#your appKey#>  delegate:<#your delegate#>];
			return YES;
				 }
	 ```
	2. In ```AppDelegate```, choose to implement the method in the ```XGPushDelegate ``` protocol:
	```objective-c
		/**
		 Callback of received push
		 @param application: UIApplication instance
		 @param userInfo: parameters specified during push
		 @param completionHandler: callback completed
		 */
		- (void)application:(UIApplication *)application 
					didReceiveRemoteNotification:(NSDictionary *)userInfo 
							fetchCompletionHandler:(void (^)(UIBackgroundFetchResult))completionHandler 
			{
				[[XGPush defaultManager] reportXGNotificationInfo:userInfo];
				completionHandler(UIBackgroundFetchResultNewData);
		}
		// iOS 10 new callback API
		// App user clicks the notification
		// App user selects a behavior in the notification
		// App user clears the message in the notification center
		// This callback will be used in both local push and remote push
	#if __IPHONE_OS_VERSION_MAX_ALLOWED >= __IPHONE_10_0
		- (void)xgPushUserNotificationCenter:(UNUserNotificationCenter *)center 
					didReceiveNotificationResponse:(UNNotificationResponse *)response 
					withCompletionHandler:(void (^)(void))completionHandler 
					{
							[[XGPush defaultManager] reportXGNotificationResponse:response];
							completionHandler();
		}

		// This API will be used when the app pushes a notification in the notification panel
		- (void)xgPushUserNotificationCenter:(UNUserNotificationCenter *)center
					 willPresentNotification:(UNNotification *)notification 
							 withCompletionHandler:(void (^)(UNNotificationPresentationOptions))completionHandler
							 {
									 [[XGPush defaultManager] reportXGNotificationInfo:notification.request.content.userInfo];
									 completionHandler(UNNotificationPresentationOptionBadge | UNNotificationPresentationOptionSound | UNNotificationPresentationOptionAlert);
		}
		#endif
	```




## Debugging method
#### Enable debug mode
Enable debug mode to view detailed TPNS debug information in the end terminal, facilitating fault location.

#### Sample code
```
// This is to enable debugging
[[XGPush defaultManager] setEnableDebug:YES];
```



#### Implementing the ```XGPushDelegate``` protocol

During debugging, it is recommended that you implement the following two methods in the protocol to obtain detailed debugging information.

```objective-c
/**
 @brief: this monitors the launch condition of TPNS

 @param isSuccess: this checks whether TPNS is successfully launched
 @param error: this message indicates an error in TPNS launch
 */
- (void)xgPushDidFinishStart:(BOOL)isSuccess error:(nullable NSError *)error;

/**
 @brief: this is the callback to register the device token with the TPNS server
 
 @param deviceToken: the token of the current device
 @param error: error message
- (void)xgPushDidRegisteredDeviceToken:(nullable NSString *)deviceToken error:(nullable NSError *)error;

```

#### Observing the log
If Xcode console displays a log similar to the one below, the client has properly integrated the SDK.

```javascript
[xgpush]Current device token is 80ba1c251161a397692a107f0433d7fd9eb59991583a925030f1b913625a9dab
[xgpush]Current XG token is 05da87c0ae5973bd2dfa9e08d884aada5bb2
```
>Use a XG 36-bit token for pushing to a single target device.

## Obtaining a token (optional)
It is recommended that after you integrate the SDK, you use gestures or other methods to display the token in the app’s less commonly used UI such as **About** or **Feedback**. Doing so will facilitate subsequent troubleshooting.

#### Sample code
```objective-c
//Obtain the token generated by TPNS
[[XGPushTokenManager defaultTokenManager] xgTokenString];
//Obtain the DeviceToken generated by APN
[[XGPushTokenManager defaultTokenManager] deviceTokenString];
```

