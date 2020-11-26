### If Flutter is integrated, how can I obtain custom parameters at the cold start of an iOS device?

To obtain custom parameters, use the `runner->AppDelegate->didFinishLaunchingWithOptions` method of the following APIs:
```objective-c
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions 
{
		// Getting the message content
		NSDictionary *remoteNotification = [launchOptions objectForKey:UIApplicationLaunchOptionsRemoteNotificationKey];
		// Processing logically based on the message content
}
```
