### If I integrate TPNS via Flutter/React Native, how do I get the custom parameters when I cold start my iOS app?

1. We recommend that you update your tpns_flutter_plugin to version 1.0.7 or above, and tpns_rn_plugin to version 1.1.3 or above.
2. If your tpns_flutter_plugin version is below 1.0.7 and tpns_rn_plugin below 1.1.3, you need to get the parameters by calling the following APIs in the `runner->AppDelegate->didFinishLaunchingWithOptions` method.
```objective-c
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions 
{
// Get the message content.
NSDictionary *remoteNotification = [launchOptions objectForKey:UIApplicationLaunchOptionsRemoteNotificationKey];
// Perform logical processing according to the message content.
}
```

### I integrated TPNS into my Android app via Flutter, why are callbacks not triggered sometimes?
We recommend that you call `XgFlutterPlugin().addEventHandler()` to set callbacks right after you initialize your app in Flutter. This helps ensure that the callback API remains valid when you cold start your app. Also, make sure that you configure all the callbacks you need in one `XgFlutterPlugin().addEventHandler()` call. Repeated calls will overwrite the callbacks set in previous calls. For details, see the calling methods in `example/lib/main.dart` of the project directory.
