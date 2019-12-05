# macOS SDK Integration Guide

- [Version Notes](https://intl.cloud.tencent.com/document/product/1024/32002?!editLang=en&!preview#version-notes)
- [SDK Group](https://intl.cloud.tencent.com/document/product/1024/32002?!editLang=en&!preview#sdk-group)
- [Integration Process](https://intl.cloud.tencent.com/document/product/1024/32002?!editLang=en&!preview#integration-process)
- [Debugging](https://intl.cloud.tencent.com/document/product/1024/32002?!editLang=en&!preview#debugging)

# macOS Integration Guide

## Version Notes

This guide applies to SDK V1.0+

## SDK Group

#### TPNS-Push-SDK-macOS-IOT1.* .* .*

- `doc` folder: TPNS macOS SDK Development Guide
- `demo` folder: mainly includes sample projects. TPNS SDK is also included.

## Integration Process

1. Log in to TPNS Console, and click **Product Management** in the left sidebar.
2. Enter the Product Management page, and click **Add a product**.
3. Enter the **Add a product** page and input the product name and details, select your product category and click **Confirm** to add the product.
4. After you create the product, select **App Management** > **App List** to enter the application list and obtain a product AppID and AppKey. (The AppID is the Access ID and the AppKey is the Access Key)

5.Import the SDK :
**Method 1: Importing using Cocoapods**
Via the Cocoapods:

```
 pod 'TPNS-macOS' 
```

**Method 2: Importing manually**
Enter the Console and click **SDK Download** in the left sidebar to enter the download page. Select the macOS platform and click **Download** in the action bar.

Go to the `demo` directory, and open the `XG-Demo-macOS` folder. Add `XG_SDK_Cloud_macOS.framework` and `XGMTACloud_macOS.framework` to the project.

Go to `Build Phases` and add the following Framework:

```
 * XG_SDK_Cloud_macOS.framework
 * XGMTACloud_macOS.framework
 * UserNotifications.framework(10.14+)
```

The library references are as follows:
![img](https://main.qcloudimg.com/raw/e79a5a2cf536fadead09187c7f955f94.png)

1. Enable the push in project configuration mode and backend mode, as shown below:

![img](https://main.qcloudimg.com/raw/633deecbe4a0599a5c59424796cddcfb.png)

1. Add compilation parameter `-ObjC`

![img](https://main.qcloudimg.com/raw/a2b155eb1c1454cd3a05004dd37f595e.png)

```
Note: `checkTargetOtherLinkFlagForObjc` errors are reported because `ObjC` hasn’t been added to `Other link flags` in `build setting`.
```

1. Call the API to launch TPNS, implement the methods in the `XGPushDelegate` protocol as needed, and enable the push service.

   - Launch the TPNS service. The following is a demonstration in `AppDelegate`:

   ```objective-c
   @interface AppDelegate () <XGPushDelegate>
   @end
   
   -(BOOL)application:(NSApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions 
       {
           [[XGPush defaultManager] startXGWithAppID:<#your AppID#> appKey:<#your appKey#>  delegate:<#your delegate#>];
       return YES;
       }
   ```

   - In `AppDelegate`, select the method in `XGPushDelegate` to implement.

```objective-c
    /**
     Received push callback
     @param application  NSApplication instance
     @param userInfo Parameter specified during push
     @param completionHandler Callback completed
     */
    - (void)xgPushDidReceiveRemoteNotification:(id)notification withCompletionHandler:(void (^)(NSUInteger))completionHandler {
    NSLog(@"notificaion is %@", notification);
}
```

## Debugging

#### Enabling Debug Mode

Enable Debug mode to view detailed TPNS Debug information on the terminal and easily locate issues.

##### [Sample code]

```
//Enabling debug
[[XGPush defaultManager] setEnableDebug:YES];
```

#### Implementing `XGPushDelegate` Protocol

In the debugging phase, we recommend that you implement the following two methods in the protocol to obtain debugging details.

```objective-c
/**
 @brief Monitor TPNS service status

 @param isSuccess Whether TPNS is launched successfully
 @param error Error messages returned from TPNS launch failure
 */
- (void)xgPushDidFinishStart:(BOOL)isSuccess error:(nullable NSError *)error;

/**
 @brief Callback of the device token registered to the TPNS server

 @param deviceToken Current device token
 @param error Error information
 @note After the current token is registered, this method will not be called again
 */
- (void)xgPushDidRegisteredDeviceToken:(nullable NSString *)deviceToken error:(nullable NSError *)error;
```

#### Observation Log

If the Xcode Console displays a log similar to the one below, the client has correctly integrated the SDK.

```javascript
[xgpush]Current device token is 623e4a477abce566a74c449ae32c1ca6066fbb243e7417b3fe393811b54792eb
Server (193.112.115.248) returned correctly. Device token has been registered
```

## Obtaining a token (optional)
It is recommended that after you integrate the SDK, you use gestures or other methods to display the token in the app’s less commonly used UI such as **About** or **Feedback**. Doing so will facilitate subsequent troubleshooting.

#### Sample code
```objective-c
//Obtain the token generated by TPNS
[[XGPushTokenManager defaultTokenManager] xgTokenString];
//Obtain the DeviceToken generated by APN
[[XGPushTokenManager defaultTokenManager] deviceTokenString];
```

```


