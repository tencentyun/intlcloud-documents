# iOS FAQs

## Push messages cannot be received

Message push involves various associated modules, and exception in any steps can leads to message delivery failure. Below are the most common issues.

### Client troubleshooting

- Check device notification settings


Please go to **Notifications** > **App name** and check whether your app has the permission to push messages.

- Check device network settings


Device network problems may lead to client's failure to  obtain message-receiving token when registering APNs, which can prevent TPNS from pushing message to specified devices.

Even if a client correctly obtained token and registered it with TPNS backend, the client will not receive the message after a message is successfully delivered by the TPNS server if the device is not connected to the internet. Device may receive a message if the device connects to the Internet in a short time. APNs will retain the message for a while and deliver it again.

SDK access problem. After the SDK is accessed, please make sure that it can get the device token used to receive messages. For more information, see [iOS SDK Integration Guide](/ios_access/ios-sdk-ji-cheng-zhi-nan.md ).



### Server troubleshooting

- APNs server problem

As a message sent to an iOS device by the TPNS service is delivered via the APNs service, if APNs fails, the request to APNs by the TPNS server to deliver the message to the device will fail.

- TPNS server problem

The TPNS server achieves message delivery through the collaboration of multiple feature modules. If any of the modules has a problem, message push will fail.



### Push certificate troubleshooting

When the TPNS server requests the APNs to deliver the message, it needs to use two required parameters: the message push certificate and the device token. When pushing the message, please make sure that the message push certificate is valid. For more information about the message push certificate settings, see [Notes on iOS Push Certificate](/ios_access/ios-tui-song-zheng-shu-shuo-ming.md).

In order to troubleshoot server problems, you can use the [TPNS testing tool](http://xg.qq.com/pigeon_v2/resource/sdk/XGPushTool.zip), which not only helps verify the conditions of TPNS and APNs servers, but also verifies the validity of the message push certificate and automatically generates the format of the TPNS-specific certificate.

***After the certificate is uploaded to the TPNS console, it usually takes about 5 minutes for it to take effect.***



## Why account/tag binding or unbinding do not work?

When the SDK APIs are used to bind or unbind account or tag, the TPNS server needs about 10 seconds for data synchronization.



## Why is the API for registering token missing in the new version?

In iOS SDK v3.1.0+, the registration of the device token is automated and handled internally by the SDK, eliminating the need for you to manually call the API.







## The device prompts for error "Error Domain=NSCocoaErrorDomain Code=3000" "No valid 'aps-environment' entitlement string found" or "UserInfo=0x16545fc0 {NSLocalizedDescription= No valid 'aps-environment' entitlement string found}".

Please check whether the ```bundle id``` configured in the Xcode project matches the configured Provision Profile file, and whether the Provision Profile file corresponding to the app has been configured with the message push capability.



## How does the client redirect or respond based on the message content?

When the iOS device receives a push message and the user taps the message to open the app, the app will respond differently according to the status:

- This function will be called if the app status is "not running".


If  ```launchOptions``` contains ```UIApplicationLaunchOptionsRemoteNotificationKey``` , it means that the user's tap on the push message causes the app to launch.

If the corresponding key value is not included, it means that the app launch is not because of the tap on the message but probably because of the tap on the icon or other actions.

**Sample code**

```objective-c
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions 
{
    // Get the message content
    NSDictionary *remoteNotification = [launchOptions objectForKey:UIApplicationLaunchOptionsRemoteNotificationKey];
    // Then logically handle based on the message content
}

```

- If the app status is "in the foreground" or "in the background but still active":


In iOS 7.0+, if the Remote Notification feature is used, the following handler needs to be used:

```objective-c
- (void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult))completionHandler;
```



In iOS 10.0+, if the Remote Notification feature is used, it is recommended to add a ```UserNotifications Framework``` handler and use it. In iOS TPNS SDK 3.1.0+, the TPNS SDK has encapsulated the new framework. Please use the following two methods in the ```XGPushDelegate``` protocol:

**Sample code**

```objective-c
- (void)xgPushUserNotificationCenter:(UNUserNotificationCenter *)center didReceiveNotificationResponse:(UNNotificationResponse *)response withCompletionHandler:(void (^)(void))completionHandler {
	NSLog(@"[XGDemo] click notification");
	completionHandler();
}

// This API needs to be called when the app pops up the push message in the foreground
- (void)xgPushUserNotificationCenter:(UNUserNotificationCenter *)center willPresentNotification:(UNNotification *)notification withCompletionHandler:(void (^)(UNNotificationPresentationOptions))completionHandler {
	completionHandler(UNNotificationPresentationOptionBadge | UNNotificationPresentationOptionSound | UNNotificationPresentationOptionAlert);
}
```



## How does the client play custom push message audio?

First, on the device development side, place the audio file in the bundle directory;
If you use the TPNS console to create a push, enter the audio file name in **Advanced settings** (the full path of the audio file is not required).
If you use REST API call, set the ```sound``` parameter to the audio file name (the full path of the audio file is not required).



## Does iOS support offline retention of push message? 

No. After the TPNS sever send the message to APNs, if APNs finds that the device is not online, it will retain the message for a while; however, details of the specific duration of retention by APNs are not provided by Apple.



## Why is arrival data unavailable for iOS?

In versions below iOS 9.x, the operating system does not provide an API to listen to message arrivals at the devices, so the arrival data cannot be collected.  
In iOS 10.0+, the operating system provides a ```Service Extension``` API, which can be called by the client to listen to message arrivals; however, the current iOS message statistics in TPNS does not include this part of data. Please stay tuned.



## How to create silent push using the TPNS server SDK?

Assign a value of 1 to ```content-available ``` and do not use alert, badge, or sound.
