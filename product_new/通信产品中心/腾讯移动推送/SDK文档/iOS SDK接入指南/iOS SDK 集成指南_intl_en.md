# iOS Integration Guide
## Overview

This document provides sample codes for integrating SDK and launching push service. (SDK version: V1.0+ version）



## SDK Composition

#### TPNS-Push-SDK-iOS-IOT1.* .* .*

* ```doc``` folder: TPNS iOS SDK development guide
* ```demo``` folder: Mainly contains sample projects and the TPNS SDK.



## Integration Steps

1. Log in to TPNS Console, and click **Product Management** in the left sidebar.

2. Enter the product management page, and click **Add a product**.

3. Go to the **Add a product** page, and enter the product name and product details. Select the product type, and click **Confirm** to add a new product.

4. After creating a new product, select **Application Management**>**Application List** to go to the application list and obtain the product AppID and AppKey. (AppID is the Access ID, and AppKey is the Access Key).

5. Import SDK
**Method One: Cocoapods Import**
Use the Cocoapods download address:

 ``` 
 pod 'TPNS-iOS' 
 ```
 
** Method Two: Manual Import**
Go to the console, and then click **SDK Download** in the left sidebar to go to the download page. Select iOS platform, and click **Download** in the operations column.

Open the SDK folder under the demo directory. Add XGPush.h and libXG-SDK-Cloud.a to the project. Open the XGPushStatistics folder, and obtain XGMTACloud.framework.

Add the following frameworks to Build Phases:
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
 
After adding the frameworks, the library references are as follows: 
![](https://main.qcloudimg.com/raw/6b85c14fa5e43431c9392f56bab4969e.png)

4. Open the push notification in project configuration and background mode, as shown below: 

![](https://main.qcloudimg.com/raw/0a893471a34042d4b436a1522da5b02a.png)

5. Add the compilation parameter ```-ObjC```. 

![](https://main.qcloudimg.com/raw/97c4d1627d2ebe124fde4c90af8a19ad.png)

	Note: If checkTargetOtherLinkFlagForObjc reports an error, it means -ObjC has not been added to Other link flags in build setting.

6. Call the API for launching TPNS and implement the method in the ```XGPushDelegate``` protocol as needed to launch the push service.

   - Launch the TPNS service; the following is a demonstration in ```AppDelegate```:

   ```objective-c
   @interface AppDelegate () <XGPushDelegate>
   @end

   -(BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions 
       {
           [[XGPush defaultManager] startXGWithAppID:<#your AppID#> appKey:<#your appKey#>  delegate:<#your delegate#>];
   	return YES;
       }
   ```

   - In```AppDelegate```, choose to implement the method in the ```XGPushDelegate ``` protocol.

```objective-c
	/**
	 Callback of received push
	 @param application UIApplication instance
	 @param userInfo Parameters specified during push
	 @param completionHandler Callback completed
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




## Debugging
#### Turning on debugging mode

After turning on debugging mode, you can view the detailed TPNS debug information on the device for troubleshooting.

##### [Sample code]

```
// This is to enable debugging
[[XGPush defaultManager] setEnableDebug:YES];
```



#### Implementing the ```XGPushDelegate``` protocol

During debugging, we recommend that you implement the following two methods in the protocol to get detailed debug information.

```objective-c
/**
 @brief This monitors the launch condition of the TPNS service

 @param isSuccess This checks whether TPNS is successfully launched
 @param error This message indicates an error in TPNS launch
 */
- (void)xgPushDidFinishStart:(BOOL)isSuccess error:(nullable NSError *)error;

/**
 @brief This registers the callback of the device token with the TPNS server
 
 @param deviceToken The token of the current device
 @param error Error message
 @note After the current token is registered, this method will no longer be called
 */
- (void)xgPushDidRegisteredDeviceToken:(nullable NSString *)deviceToken error:(nullable NSError *)error;

```

#### Observing the log

If Xcode console displays a log similar to the one below, the client has properly integrated the SDK.

```javascript
[xgpush]Current device token is 623e4a477abce566a74c449ae32c1ca6066fbb243e7417b3fe393811b54792eb
The server (193.168.115.248) returns correctly, the device token has been successfully registered.
```





