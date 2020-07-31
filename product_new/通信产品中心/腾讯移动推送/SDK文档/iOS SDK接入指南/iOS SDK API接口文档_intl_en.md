# SDK API Description

## Launching TPNS Service

**Description**

This API is used to launch the TPNS service by using the information of the application registered at the official website of TPNS. It is applicable to SDK v1.2.7.2. For SDKs of earlier versions, please see XGPush.h.

```objective-c
- (void)startXGWithAppID:(uint32_t)appID appKey:(nonnull NSString *)appKey delegate:(nullable id<XGPushDelegate>)delegate ;
```

**Parameter description**

* appID: application ID applied through the frontend, i.e., the `Access ID`
* appKey: `appKey` applied through the frontend, i.e., the `Access Key`
* delegate: callback object 

_**Note: the parameters required by the API must be entered correctly; otherwise, TPNS will not be able to push messages correctly for the app.**_

**Sample**

```Objective-C
[[XGPush defaultManager] startXGWithAppID: <#your access ID#>appKey:<#your access key#> delegate:<#your delegate#>];
```

## Stopping TPNS Service

**Description**

* After the TPNS service is stopped, the application will not be able to push messages to devices through TPNS. To receive messages pushed by TPNS again, you must call `startXGWithAppID:appKey:delegate:` method again to restart the TPNS service.

**API**

```objective-c
- (void)stopXGNotification;
```

**Sample**

```Objective-C
[[XGPush defaultManager] stopXGNotification];
```

## Customizing Notification Bar Message Action

### Creating message action

**Description**

Create a click event action in the notification

**API**

```objective-c
+ (nullable id)actionWithIdentifier:(nonnull NSString *)identifier title:(nonnull NSString *)title options:(XGNotificationActionOptions)options;
```

**Parameter description**

* identifier: unique action ID 
* title: action name 
* options: options supported by action

**Sample**

```objective-c
XGNotificationAction *action1 = [XGNotificationAction actionWithIdentifier:@"xgaction001" title:@"xgAction1" options:XGNotificationActionOptionNone];
```

_**Note: the notification bar has the click event feature, which is only supported on iOS 8.0+. For iOS 7.x or earlier, this method will return null**_

### Creating category object

**Description**

Create a category object to manage the action object of the notification panel

**API**

```objective-c
+ (nullable id)categoryWithIdentifier:(nonnull NSString *)identifier actions:(nullable NSArray<XGNotificationAction *> *)actions intentIdentifiers:(nullable NSArray<NSString *> *)intentIdentifiers options:(XGNotificationCategoryOptions)options;
```

**Parameter description**

* identifier: category object ID
* actions: action object group owned by the current category
* intentIdentifiers: used to indicate identifiers that can be recognized by Siri
* options: category characteristics

_**Note: the notification bar has the click event feature, which is only supported in iOS 8+. For iOS 8 or earlier, this method will return null**_

**Sample**

```Objective-C
XGNotificationCategory *category = [XGNotificationCategory categoryWithIdentifier:@"xgCategory" actions:@[action1, action2] intentIdentifiers:@[] options:XGNotificatio nCategoryOptionNone];
```

### Creating configuration class

Manage the style and characteristics of the push message notification bar

**API**

```objective-c
+ (nullable instancetype)configureNotificationWithCategories:(nullable NSSet<XGNotificationCategory *> *)categories types:(XGUserNotificationTypes)types;
```

**Parameter description**

* categories: the collection of categories supported by the notification bar 
* types: style of registered notification

**Sample**

```objective-c
XGNotificationConfigure *configure = [XGNotificationConfigure configureNotificationWithCategories:[NSSet setWithObject:category] types:XGUserNotificationTypeAlert|XGUserNotificationTypeBadge|XGUserNotificationTypeSound];
```

## Reporting Location

**Description**

* Report the geographical location, and later use TPNS to send targeted push based on specific locations

**API**

```objective-c
- (void)reportLocationWithLatitude:(double)latitude longitude:(double)longitude;
```

**Parameter description**

* latitude: latitude
* longitude: longitude

**Sample**

```Objective-C
[[XGPush defaultManager] reportLocationWithLatitude:20.0 longitude:19.0];
```

## Automatically Increasing Badge Number by 1

**Description**

* Call this API to report the current application badge number to the TPNS server. After the client is configured, you can set the badge number “auto increased by 1” feature, which can be found in the console (create push > notification bar message > advanced settings > badge number)

**API**

```objective-c
- (void)setBadge:(NSInteger)badgeNumber;
```

**Parameter description**

* badgeNumber, badge number of application

**Note:  
1. This API must be called locally; otherwise, the badge number by default will not change, even if the "auto increased by 1" feature is enabled.  
**

**Sample**

```Objective-C
[[XGPush defaultManager] setBadge:7];
```

## Managing Application Badge

**Description**

* Manage the badge number displayed by the application

**API**

```objective-c
@property (nonatomic) NSInteger xgApplicationBadgeNumber;
```

**Sample**

```objective-c
// Set the application badge
[[XGPush defaultManager] setXgApplicationBadgeNumber:0];

// Get the application badge
NSInteger number = [[XGPush defaultManager] xgApplicationBadgeNumber];
```

## Push Effect Statistics

**Description**

* In order to better understand the operational effect of each push message, it is necessary to report the user action on the message

The data reporting API needs to be called  
**API**

```Objective-C
- (void)reportXGNotificationInfo:(nonnull NSDictionary *)info;
```

**Sample**

```Objective-C
- (BOOL)application:(UIApplication *)application
  didFinishLaunchingWithOptions:(NSDictionary *)launchOptions 
  {
      [[XGPush defaultManager] reportXGNotificationInfo:launchOptions];
      return YES;
  }
```

* For **iOS 9.x** and earlier, you need to call the data reporting API in the callback method of `UIApplicationDelegate` \(see below\):

```objective-c
- (void)application:(UIApplication *)application 
    didReceiveRemoteNotification:(NSDictionary *)userInfo 
        fetchCompletionHandler:(void (^)(UIBackgroundFetchResult))completionHandler 
{ 
}
```

**Sample**

```objective-c
- (void)application:(UIApplication *)application 
    didReceiveRemoteNotification:(NSDictionary *)userInfo 
        fetchCompletionHandler:(void (^)(UIBackgroundFetchResult))completionHandler 
{
    [[XGPush defaultManager] reportXGNotificationInfo:userInfo];
    completionHandler(UIBackgroundFetchResultNewData);
}
```

* For **iOS 10.0+**, you need to call the data reporting API in the callback method of `XGPushDelegate` \(see below\):

**Sample**

```Objective-C
 - (void)xgPushUserNotificationCenter:(UNUserNotificationCenter *)center
   didReceiveNotificationResponse:(UNNotificationResponse *)response
   withCompletionHandler:(void(^)())completionHandler 
   {
  
    [[XGPush defaultManager] reportXGNotificationResponse:response];
            completionHandler();

   }
```

If you want to enable the application to display the push message in the foreground, you need to implement the following method and call the reporting API

**API**

```Objective-C
- (void)xgPushUserNotificationCenter:(UNUserNotificationCenter *)center willPresentNotification:(UNNotification *)notification withCompletionHandler:(void (^)(UNNotificationPresentationOptions))completionHandler;
```

**Sample**

```Objective-C
- (void)xgPushUserNotificationCenter:(UNUserNotificationCenter *)center willPresentNotification:(UNNotification *)notification withCompletionHandler:(void (^)(UNNotificationPresentationOptions))completionHandler {
    [[XGPush defaultManager] reportXGNotificationInfo:notification.request.content.userInfo];
    completionHandler(UNNotificationPresentationOptionBadge | UNNotificationPresentationOptionSound | UNNotificationPresentationOptionAlert);
}
```

## Managing Device Token

### Querying device token

**Description**

* Query the token string obtained from APNs by the current application

**API**

```objective-c
@property (copy, nonatomic, nullable, readonly) NSString *deviceTokenString;
```

**Sample**

```objective-c
NSString *token = [[XGPushTokenManager defaultTokenManager] deviceTokenString];
```

### Querying APNs registration result

**Description**

* If the registration is successful, the application will call the callback method of the `UIApplicationDelegate` delegate object \(see below\):

**API**

```Objective-C
- (void)application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken;
```

### Querying TPNS registration result

**Description**

* The SDK launch method automatically registers the token obtained by the device from APNs to the TPNS server, and the registration result will be returned in the callback method of `XGPushDelegate` \(see below\):

**API**

```objective-c
- (void)xgPushDidRegisteredDeviceToken:(NSString *)deviceToken error:(NSError *)error;
```

_**Note: this callback method is called after the registration is successful. After the current token is registered, the SDK will cache the registration information, and this method will not be called again**_

### Binding/unbinding tag and account

**Description**

* You can bind tags to different users and then push based on a specific tag, i.e., if you push to a tag, all devices under the tag will receive the push notification. One device can bind multiple tags.

**Single-operation API**
```Objective-C
- (void)bindWithIdentifier:(nullable NSString *)identifier type:(XGPushTokenBindType)type;
- (void)unbindWithIdentifer:(nullable NSString *)identifier type:(XGPushTokenBindType)type;
```

**Parameter description**

* identifier: tag or account
* type: binding type

**Sample**

```Objective-C
// Bind a tag:
[[XGPushTokenManager defaultTokenManager] bindWithIdentifier:@"your tag" type:XGPushTokenBindTypeTag];

// Unbind a tag
[[XGPushTokenManager defaultTokenManager] unbindWithIdentifer:@"your tag" type:XGPushTokenBindTypeTag];

// Bind an account:
[[XGPushTokenManager defaultTokenManager] bindWithIdentifier:@"your account" type:XGPushTokenBindTypeAccount];

// Unbind an account:
[[XGPushTokenManager defaultTokenManager] unbindWithIdentifer:@"your account" type:XGPushTokenBindTypeAccount];
```

**Batch operation API**

```Objective-C
- (void)bindWithIdentifiers:(nonnull NSArray <NSString *> *)identifiers type:(XGPushTokenBindType)type
- (void)unbindWithIdentifers:(nonnull NSArray <NSString *> *)identifiers type:(XGPushTokenBindType)type;
```
**Parameter description**

* identifiers: tag or account list
* type: binding type

**Note**
* Account type is currently not supported. The tag string cannot contain spaces or tabs

### Batch updating tags/accounts

**API**
```Objective-C
- (void)updateBindedIdentifiers:(nonnull NSArray <NSString *> *)identifiers bindType:(XGPushTokenBindType)type;
```
**Parameter description**

* identifiers: tag ID string array. The tag string cannot contain spaces or tabs
* type: ID type

**Note**
* If the tag type is specified, this API will replace all the old tag corresponding to the current token with the current tag; if the account type is specified, this API will only take the first one in the `identifiers` list

### Clearing all tags/accounts

**API**
```Objective-C
- (void)clearAllIdentifiers:(XGPushTokenBindType)type;
```
**Parameter description**
* type: ID type


### Querying tags and accounts bound to token

**Description**

* Query the ID bound to the current token object by the specified type 

**API**

```objective-c
- (nullable NSArray<NSString *> *)identifiersWithType:(XGPushTokenBindType)type;
```

**Sample**

```objective-c
// Query the tag
[[XGPushTokenManager defaultTokenManager] identifiersWithType:XGPushTokenBindTypeTag];
// Query the account
[[XGPushTokenManager defaultTokenManager] identifiersWithType:XGPushTokenBindTypeAccount];
```

## Querying Device Notification Permission

**Description**

* Query whether the user allows device notification 

**API**

```objective-c
- (void)deviceNotificationIsAllowed:(nonnull void (^)(BOOL isAllowed))handler;
```

**Parameter description**

* handler: return method of query result

**Sample**

```objective-c
[[XGPush defaultManager] deviceNotificationIsAllowed:^(BOOL isAllowed) {
        <#code#>
    }];
```

## Querying SDK Version

**Description**

* Query the current SDK version

**API**

```objective-c
- (nonnull NSString *)sdkVersion;
```

**Sample**

```objective-c
[[XGPush defaultManager] sdkVersion];
```

## Local Push

For local push features, please see [Apple developer documentation](https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/SchedulingandHandlingLocalNotifications.html#//apple_ref/doc/uid/TP40008194-CH5-SW1).

