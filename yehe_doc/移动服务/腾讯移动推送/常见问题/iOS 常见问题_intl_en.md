### Why XGForFreeVersion symbol not found in simulator for TPNS SDK 1.2.5.4 or earlier versions?
The version 1.2.5.4 or earlier do not support simulator. You need to use real machine for debugging. To use a simulator, upgrade TPNS SDK to the latest version.

### Why can't push messages be received?
Message push is a task involving the collaboration of many associated modules. An exception in any step may result in failure in message delivery. Below lists the most common problems:

**Client troubleshooting**
- Check notification settings on the device
Please select **Notifications** > **application name** and check whether your application has the permission to push messages.
- Check network settings on the device
A device network problem may cause the client to fail to get the token used to receive messages when signing up with APNs, which results in the inability to use the TPNS service to push message to the specified device.

Even if the client has correctly gotten the token and registered it with the TPNS backend, after a message is successfully delivered by the TPNS server, the client will not receive the message if the device is not connected to the internet. If the device goes online later, it may receive the message (APNs will retain the message for a while and then deliver it again).

Check the SDK integration. After the SDK is integrated, please make sure that it can get the device token used to receive messages. For more information, please see [iOS SDK Integration Guide](https://intl.cloud.tencent.com/document/product/1024/30726).


**Server troubleshooting**
- APNs server problem
As a message sent to an iOS device by the TPNS service is delivered through APNs, if APNs fails, the request to APNs by the TPNS server to deliver the message to the device will fail.
- TPNS push server problem
The TPNS server implements message delivery through the collaboration of multiple feature modules. If any of the modules has a problem, message push will fail.


**Push certificate troubleshooting**
When the TPNS server requests APNs to deliver the message, it needs to use two required parameters: the message push certificate and the device token. When pushing the message, please make sure that the message push certificate is valid. For more information on how to configure the message push certificate, please see [Guide for Getting Push Certificates on iOS](https://intl.cloud.tencent.com/document/product/1024/30728).





### Why account/tag binding or unbinding does not work?
When the SDK APIs are used to bind or unbind an account or tag, the TPNS server needs about 10 seconds for data sync.



### The device prompts an error "No valid "aps-environment" entitlement string found for application". What should I do?
Check whether the `bundle id` configured in the Xcode project matches the configured `Provision Profile` file and whether the `Provision Profile` file corresponding to the application has been configured with the message push capability.



### How does the client redirect or respond based on the message content?

When an iOS device receives a push message and the user taps the message to open the app, the application will respond differently according to the status:

- This function will be invoked if the application status is "not running".
 - If `launchOptions` contains `UIApplicationLaunchOptionsRemoteNotificationKey`, it means that the user's tap on the push message will cause the application to launch.
 - If the corresponding key value is not included, it means that the application launch is not caused by the tap on the message but probably by the tap on the icon or other actions.
	```objective-c
	- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions 
	{
			// Get the message content
			NSDictionary *remoteNotification = [launchOptions objectForKey:UIApplicationLaunchOptionsRemoteNotificationKey];
			// Then process logically based on the message content
	}
	```
- If the application status is "in the foreground" or "in the background but still active":
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

	// This API needs to be called when the application pops up the push message in the foreground
	- (void)xgPushUserNotificationCenter:(UNUserNotificationCenter *)center willPresentNotification:(UNNotification *)notification withCompletionHandler:(void (^)(UNNotificationPresentationOptions))completionHandler {
		completionHandler(UNNotificationPresentationOptionBadge | UNNotificationPresentationOptionSound | UNNotificationPresentationOptionAlert);
	}
	```



### How does the client play back custom push message audio?

First, on the device development side, place the audio file in the `bundle` directory:
- If you use the TPNS console to create a push, enter the audio file name in **Advanced Settings** (the full path of the audio file is not required).
- If you use RESTful API calls, set the `sound` parameter to the audio file name (the full path of the audio file is not required).


### Does iOS support offline retention of push messages? 
No. After the TPNS sever delivers a message to APNs, if APNs finds that the device is not online, it will retain the message for a while; however, details of the specific duration of retention by APNs are not provided by Apple.



### Why is arrival data unavailable for iOS?
- On versions below iOS 9.x, the operating system does not provide an API to listen on message arrivals at the devices, so the arrival data cannot be collected.  
- On versions above iOS 10.0, the operating system provides a `Service Extension` API, which can be called by the client to listen on message arrivals.


### How do I create silent push with the TPNS server SDK?
Assign the value `1` to `content-available` and do not use `alert`, `badge`, or `sound`.




### What should I do if `DeviceToken` is not returned occasionally for registration in the development environment of iOS 13?
This problem is caused by instability of APNs. You can fix it in the following ways:
1. Insert a SIM card into the phone and use the 4G network.
2. Uninstall and reinstall the application, restart the application, or shut down and restart the phone.
3. Use a package for the production environment.
4. Use another iPhone on iOS 13.


### How do I expand the testing scope on iOS if the number of testing devices is limited?
1. Enterprise signature certificate
Apply for enterprise signature and push certificates and release your application as follows:
Use the enterprise signature certificate to build and release your app. Testers can download and install the application through the dedicated enterprise channel.
2. App Store signature certificate
Use the current push certificate released on App Store as follows:
Release the preview version in TestFlight: upload the IPA package to [App Store Connect](https://appstoreconnect.apple.com), use TestFlight to create a beta version, and set the list of testers (Apple IDs) for the specified version in TestFlight. Testers can download and install your application through the official TestFlight application on App Store.


### For iOS, how do I configure to change the badge number only without displaying the message?
When creating a push, you can use the API to specify the notification panel message type, leave the title empty, and only set `badge_type`. For more information, please see the [API documentation](https://intl.cloud.tencent.com/document/product/1024/33764).
Below is a sample:
```
{
    "platform": "ios",
    "audience_type": "token",
    "environment":"dev",
        "token_list": [
    "05a8ea6924590dd3a94480fa1c9fc8448b4e"],
    "message_type":"notify",
    "message":{
    "ios":{
        "aps": {
            "badge_type":-2
        }
    }
 }
}
```


### What should I do when the App prompts an error "Crash: you can't call -sendResponse: twice nor after encoding it"?
This error occurs if your APP integrates TPNS iOS SDK (1.2.7.2 - 1.2.5.4), uses the **Recall** feature of TPNS, and implements the following system callback:
```
- (void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo  fetchCompletionHandler:(void (^)(UIBackgroundFetchResult))completionHandler
```
In this case, **override** the sent messages to process them.
