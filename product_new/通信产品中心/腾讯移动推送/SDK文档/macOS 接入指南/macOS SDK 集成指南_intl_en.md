# macOS Integration Guide
## Version Requirements
The SDK used in this guide is v1.0+.



## SDK Composition

#### TPNS-Push-SDK-macOS-IOT1.* .* .*

* ```doc``` folder: TPNS SDK for macOS development guide
* ```demo``` folder: mainly contains sample projects and the TPNS SDK.



## Integration Steps

1. Log in to TPNS Console, and click **Product Management** on the left sidebar.

2. Enter the **Product Management** page, and click **Add a product**.

3. Go to the **Add Product** page and enter the product name and product details. Select the product type and click **OK** to add a new product.

4. After creating a new product, select **Application Management**>**Application List** to go to the application list and get the product `AppID` and `AppKey`. (`AppID` is the `Access ID`, and `AppKey` is the `Access Key`).

5. Import the SDK:
**Method 1. import using Cocoapods**
Download through Cocoapods:

 ``` 
 pod 'TPNS-macOS' 
 ```

**Method 2. manual import**
Enter the console and click **SDK Download** on the left sidebar to go to the download page. Select the macOS platform and click **Download** in the "Operation" column.


Go to the `demo` directory, and open the `XG-Demo-macOS` folder. Add ```XG_SDK_Cloud_macOS.framework``` and ```XGMTACloud_macOS.framework``` to the project.

 Add the following frameworks to ```Build Phases```:

```
 * XG_SDK_Cloud_macOS.framework
 * XGMTACloud_macOS.framework
 * UserNotifications.framework(10.14+)
```

After adding the frameworks, the library references are as follows: 
![](https://main.qcloudimg.com/raw/e79a5a2cf536fadead09187c7f955f94.png)

4. Open the push notification in project configuration and background mode, as shown below: 

![](https://main.qcloudimg.com/raw/633deecbe4a0599a5c59424796cddcfb.png)

5. Add the compilation parameter ```-ObjC```. 

![](https://main.qcloudimg.com/raw/a2b155eb1c1454cd3a05004dd37f595e.png)

	Note: if `checkTargetOtherLinkFlagForObjc` reports an error, it means -ObjC has not been added to Other link flags in build setting.

6. Call the API for launching TPNS and implement the method in the ```XGPushDelegate``` protocol as needed to launch the push service.

   - Launch the TPNS service; the following is a demonstration in ```AppDelegate```:

   ```objective-c
   @interface AppDelegate () <XGPushDelegate>
   @end

   -(BOOL)application:(NSApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions 
       {
           [[XGPush defaultManager] startXGWithAppID:<#your AppID#> appKey:<#your appKey#>  delegate:<#your delegate#>];
   	return YES;
       }
   ```

   - In```AppDelegate```, choose to implement the method in the ```XGPushDelegate ``` protocol.

```objective-c
	/**
	 Callback of received push
	 @param application   `NSApplication` instance
	 @param userInfo: parameters specified during push
	 @param completionHandler: callback completed
	 */
	- (void)xgPushDidReceiveRemoteNotification:(id)notification withCompletionHandler:(void (^)(NSUInteger))completionHandler {
    NSLog(@"notificaion is %@", notification);
}
```




## Debugging
#### Enabling debug mode

After turning on debug mode, you can view the detailed TPNS debug information on the device for troubleshooting.

##### [Sample code]

```
// This is to enable debugging
[[XGPush defaultManager] setEnableDebug:YES];
```



#### Implementing ```XGPushDelegate``` protocol

During debugging, you are recommended to implement the following two methods in the protocol to get detailed debug information.

```objective-c
/**
 @brief This monitors the launch condition of the TPNS service

 @param isSuccess   This checks whether TPNS is successfully launched
 @param error This message indicates an error in TPNS launch
 */
- (void)xgPushDidFinishStart:(BOOL)isSuccess error:(nullable NSError *)error;

/**
 @brief This registers the callback of the device token with the TPNS server
 
 @param deviceToken: token of current device
 @param error: error message
 @note After the current token is registered, this method will no longer be called
 */
- (void)xgPushDidRegisteredDeviceToken:(nullable NSString *)deviceToken error:(nullable NSError *)error;

```

#### Observing log

If Xcode console displays a log similar to the one below, the client has properly integrated the SDK.

```javascript
[xgpush]Current device token is 623e4a477abce566a74c449ae32c1ca6066fbb243e7417b3fe393811b54792eb
The server (193.112.115.248) returns correctly, the device token has been successfully registered.
```





