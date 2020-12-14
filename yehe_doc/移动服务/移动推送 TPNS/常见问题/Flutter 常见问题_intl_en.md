### If Flutter is integrated, how can I get custom parameters upon the cold start of an iOS device?

To get custom parameters, use the `runner->AppDelegate->didFinishLaunchingWithOptions` method of the following APIs:
```objective-c
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions 
{
		// Get the message content
		NSDictionary *remoteNotification = [launchOptions objectForKey:UIApplicationLaunchOptionsRemoteNotificationKey];
		// Then process logically based on the message content
}
```
### Why can't the notification click callback be triggered on Android sometimes after Flutter is integrated?
We recommend you call the `XgFlutterPlugin().addEventHandler()` API to set notification callback events as soon as Flutter is initialized in order to ensure the timeliness of callback API settings upon cold start of the application. In addition, please add all the required callbacks in one call of the `XgFlutterPlugin().addEventHandler()` API, as multiple calls will overwrite them in turn and invalidate callbacks added previously. For more information, please refer to the API call method in the `example/lib/main.dart` file in the project directory.
