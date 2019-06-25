## Version Requirements
The SDKs used in this guide are V1.0+.

## SDK Composition

#### TPNS-Push-SDK-iOS-IOT1.*.*.*


* ```doc``` folder: TPNS iOS SDK development guide.
* ```demo``` folder: It mainly contains sample projects and the TPNS SDK.



## Integration Steps

You can follow the steps below to complete integration.




1. Go to the TPNS console to register the iOS app and get ```App ID``` and ```App Key```.

* <font color= red>Note:</font> App ID corresponds to the app's ```Access ID```, while ```App Key``` the app's ```Access Key```.

2. Download the TPNS SDK and unzip it.

Open the sdk folder in the demo directory and add ```XGPush.h``` and ```libXG-SDK-Cloud.a``` to the project.

3. Add the following frameworks to ```Build Phases```:

```
* CoreTelephony.framework
* SystemConfiguration.framework
* UserNotifications.framework
* libXG-SDK-Cloud.a 
* libz.tbd
* CoreData.framework
* CFNetwork.framework
```

After the addition is completed, the library references are as follows: 
![](https://main.qcloudimg.com/raw/b587ab23c09427994214cadb08cca521.png)

4. Open the push in the project configuration and background mode, as shown below: 

![](https://main.qcloudimg.com/raw/83b667d05c224bfdf81bc7a618b55436.png)

5. Add the compilation parameter ```-ObjC```. 

![](https://main.qcloudimg.com/raw/062c66bb679e30be6a640df412f5408e.png)

	Note: If checkTargetOtherLinkFlagForObjc prompts an error, the reason is that -ObjC has not been added to Other link flags in build setting.

6. Call the API for starting TPNS at the right time and implement the method in the ```XGPushDelegate``` protocol as needed to start the push service.

   - Start the TPNS service; the following is a demonstration in  ```AppDelegate```:

   ```objective-c
   @interface AppDelegate () <XGPushDelegate>
   @end

   -(BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions 
       {
           [[XGPush defaultManager] startXGWithAppID:<#your AppID#> appKey:<#your appKey#>  delegate:<#your delegate#>];
   	return YES;
       }
   ```

   - Select to implement the method in the ```XGPushDelegate ``` protocol in ```AppDelegate```

```objective-c
	/**
	 Callback of received push
	 @param application  UIApplication instance
	@param userInfo Parameters specified during push
	 @param completionHandler Completed callback
	 */
	- (void)application:(UIApplication *)application 
        didReceiveRemoteNotification:(NSDictionary *)userInfo 
            fetchCompletionHandler:(void (^)(UIBackgroundFetchResult))completionHandler 
    {
    	[[XGPush defaultManager] reportXGNotificationInfo:userInfo];
    	completionHandler(UIBackgroundFetchResultNewData);
	}
	// iOS 10 new callback API
	// App user taps the notification
	// App user selects a behavior in the notification
	// App user clears the message in the notification center
	// This callback will be used no matter whether it is a local push or a remote push
#if __IPHONE_OS_VERSION_MAX_ALLOWED >= 	__IPHONE_10_0
	- (void)xgPushUserNotificationCenter:(UNUserNotificationCenter *)center 
        didReceiveNotificationResponse:(UNNotificationResponse *)response 
        withCompletionHandler:(void (^)(void))completionHandler 
        {
            [[XGPush defaultManager] reportXGNotificationResponse:response];
            completionHandler();
	}

	// This API needs to be used when the app pops up a notification in the foreground
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

After turning on debugging mode, you can view the detailed TPNS debugging information on the device for troubleshooting.

##### [Sample code]

```
// Toggle the debugging switch
[[XGPush defaultManager] setEnableDebug:YES];
```



#### Implementing the ```XGPushDelegate``` protocol

In the debugging phase, it is recommended to implement the following two methods in the protocol to get more detailed debugging information.

```objective-c
/**
 @brief This monitors the start condition of the TPNS service

 @param isSuccess This checks whether TPNS is successfully started
 @param error Error message for the TPNS start error
 */
- (void)xgPushDidFinishStart:(BOOL)isSuccess error:(nullable NSError *)error;

/**
 @brief This registers the callback of the device token with the TPNS server
 
 @param deviceToken The token of the current device
 @param error Error message
 @note After the current token is registered, this method will not be called again
 */
- (void)xgPushDidRegisteredDeviceToken:(nullable NSString *)deviceToken error:(nullable NSError *)error;

```

#### Observing the Log

If the Xcode console displays a log similar to the one below, the client has properly integrated the SDK.

```javascript
-[AppDelegate xgPushDidFinishStart:error:], result OK, error (null)
[xgpush] clientid is 331F8A86-CDF5-4C6F-BF8C-13EFB8EAD34E
package Size is 359
[xgpush]Current device token is c4294001507045547bfe64581eecb95f6d6a46c9cf9a9a0878233f6c0e8e3b8f
[xgpush info]msgLen's length is 108
[xgpush] Server return code: 0
-[AppDelegate xgPushDidRegisteredDeviceToken:error:], result OK, error (null)
```




## Push Testing Tool  
In order to make it easy for you to test whether the SDK access is successful, this tool can be used to test whether pushes are delivered from the APNs server or TPNS server.

Click [here](http://ixg.qq.com/pigeon_v2/resource/sdk/XGPushTool.zip) to download the TPNS testing tool.

If pushes cannot be received, see the [iOS FAQs](https://intl.cloud.tencent.com/document/product/1024/30732).

