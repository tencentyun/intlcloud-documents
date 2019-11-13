# iOS FAQs

## Push messages cannot be received

Message push involves various associated modules, and exception in any steps can lead to message delivery failure. Below are the most common issues:

### Client troubleshooting

- Check the notification setting of the device


Please go to **Notifications**>**App name** and check whether your app has enabled message push.

- Check the network setting of the device


Network issues may cause the client to fail to obtain the device token when registering for APNs, which prevents TPNS from pushing messages to specified devices.

Even when the client has correctly obtained the token, registered it with backend TPNS, and TPNS server has successfully delivered a message, the client still cannot receive the message if the device is not connected to the internet. The client can still receive the message if the device reconnects to the internet within a short time. APNs will retain the message for a while before delivering another message.

SDK integration problem. After integrating the SDK, make sure you get the identifier (Device Token) for receiving messages. For more information, see [iOS SDK integration guide].



### Server troubleshooting

- APNs server problem

As a message sent to an iOS device by the TPNS server is delivered via the APNs service, if APNs fails, the request sent by the TPNS server to APNs to deliver a message to the device will fail.

- TPNS server problem

TPNS server achieves message delivery through the collaboration of multiple feature modules. If any of these modules have an exception, message push will fail.



### Push certificate troubleshooting

When the TPNS server requests the APNs to deliver a message, it must use two parameters: the message push certificate and the device token. When pushing messages, please make sure that the message push certificate is valid. For more information on the message push certificate settings, see [iOS push certificate description](https://intl.cloud.tencent.com/document/product/1024/30728).

In order to troubleshoot server problems, you can use the [TPNS testing tool](http://xg.qq.com/pigeon_v2/resource/sdk/XGPushTool.zip), which helps verify TPNS and APNs servers as well as the validity of the message push certificate, and automatically generates a certificate format that is TPNS-specific.

***After the certificate is uploaded via the TPNS console, it usually takes about 5 minutes for it to take effect.***



### Why account/tag binding and unbinding do not work?

When SDK APIs are used to bind or unbind account/tag, the TPNS server needs about 10 seconds to synchronize data.



### The device prompts an error that no valid 'aps-environment' entitlement string found for application

Please check if the ```bundle id``` configured in the Xcode project matches the configured Provision Profile file, and whether the Provision Profile file corresponding to the app has message push capability.



### How does the client redirect or respond based on the message content?

When iOS device receives a push message and the user clicks on the message to open the app, the app will respond differently according to the status:

- This function will be called if the app status is "not running".


If ```launchOptions``` contains ```UIApplicationLaunchOptionsRemoteNotificationKey```, it means the user clicks on the push message and causes the app to launch.

If there is no corresponding key value, it means the app launch is not caused by the user’s clicks on the push message, but rather clicks on the icon or other actions.

**Sample code**

```objective-c
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions 
{
    // Getting message content
    NSDictionary *remoteNotification = [launchOptions objectForKey:UIApplicationLaunchOptionsRemoteNotificationKey];
    // Processing logically based on the message content
}

```

- If the app status is "in the foreground" or "in the background but still active":


In iOS 7.0+, if the Remote Notification feature is used, the following handler needs to be used:

```objective-c
- (void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult))completionHandler;
```



In iOS 10.0+, if the Remote Notification feature is used, we recommend that you add and use the ```UserNotifications Framework```. In iOS TPNS SDK 3.1.0+, TPNS SDK has encapsulated the new framework. Please use the following two methods in the ```XGPushDelegate``` protocol:

**Sample code**

```objective-c
- (void)xgPushUserNotificationCenter:(UNUserNotificationCenter *)center didReceiveNotificationResponse:(UNNotificationResponse *)response withCompletionHandler:(void (^)(void))completionHandler {
	NSLog(@"[XGDemo] click notification");
	completionHandler();
}

// This API needs to be called when the app pushes messages in the notification panel
- (void)xgPushUserNotificationCenter:(UNUserNotificationCenter *)center willPresentNotification:(UNNotification *)notification withCompletionHandler:(void (^)(UNNotificationPresentationOptions))completionHandler {
	completionHandler(UNNotificationPresentationOptionBadge | UNNotificationPresentationOptionSound | UNNotificationPresentationOptionAlert);
}
```



### How does the client play the custom push message audio?

First, on the device development side, place the audio file under the bundle directory;
If you use the TPNS console to create a push, enter the audio file name in **Advanced settings** (the full path of the audio file is not required).
If you use REST API call, set the ```sound``` parameter to the audio file name (the full path of the audio file is not required).



### Does iOS support offline retention of push messages? 

No. When TPSN server sends a message to APNs, if APNs finds that the device is not online, it will retain the message for a while but the retention duration is not specified.



### Why is delivery data unavailable for iOS?

In versions below iOS 9.x, the operating system does not provide an API to listen to the delivery of messages at the device, so the delivery data cannot be recorded.  
In iOS 10.0+, the operating system provides a ```Service Extension``` API, which can be called by the client to listen to the delivery of messages. But the current iOS message statistics in TPNS do not include this data.



### How do I create silent push notifications using the TPNS server SDK?

Assign a value of 1 to ```content-available ``` and do not use alert, badge, or sound.

