# SDK API Description

## Launching TPNS

**Note**

* Launch TPNS by using the information of the app registered at the official TPNS website

**API**

```objective-c
- (void)startXGWithAppID:(uint32_t)appID appKey:(nonnull NSString *)appKey delegate:(nullable id<XGPushDelegate>)delegate ;
```

**Parameter description**

* appID: App ID applied through the frontend, i.e., the Access ID
* appKey: appKey applied through the frontend, i.e., the Access Key
* delegate: Callback object 

_**Note: The parameters required by the API must be entered correctly. Otherwise, TPNS will not be able to push messages correctly for the app.**_

**Example**

```Objective-C
[[XGPush defaultManager] startXGWithAppID: <#your access ID#>appKey:<#your access key#> delegate:<#your delegate#>];
```

## Stopping the TPNS Service

**Note**

* After the TPNS service is stopped, the app will not be able to push messages to devices through TPNS. If you need to make devices able to receive the message pushed by TPNS, you must call the `startXGWithAppID:appKey:delegate:` method again to restart the TPNS service.

**API**

```objective-c
- (void)stopXGNotification;
```

**Example**

```Objective-C
[[XGPush defaultManager] stopXGNotification];
```

## Customizing Notification Bar Message Actions

### Creating an Action Supported by Messages

**Note**

Create a tappable event action in the notification message

**API**

```objective-c
+ (nullable id)actionWithIdentifier:(nonnull NSString *)identifier title:(nonnull NSString *)title options:(XGNotificationActionOptions)options;
```

**Parameter description**

* identifier: Unique action identifier 
* title: Action name 
* options: Options supported by the action

**Example**

```objective-c
XGNotificationAction *action1 = [XGNotificationAction actionWithIdentifier:@"xgaction001" title:@"xgAction1" options:XGNotificationActionOptionNone];
```

_**Note: The notification bar has the tappable event feature, which is only supported on iOS 8.0+. For iOS 7.x or earlier, this method will return null**_

### Creating a Category Object

**Note**

Create a category object to manage the action object of the notification bar

**API**

```objective-c
+ (nullable id)categoryWithIdentifier:(nonnull NSString *)identifier actions:(nullable NSArray<XGNotificationAction *> *)actions intentIdentifiers:(nullable NSArray<NSString *> *)intentIdentifiers options:(XGNotificationCategoryOptions)options;
```

**Parameter description**

* identifier: The identifier of the category object
* actions: The action object group owned by the current category
* intentIdentifiers: Used to indicate the identifier that can be recognized by Siri
* options: The characteristics of the category

_**Note: The notification bar has the tappable event feature, which is only supported on iOS 8+. For iOS 8 or earlier, this method will return null**_

**Example**

```Objective-C
XGNotificationCategory *category = [XGNotificationCategory categoryWithIdentifier:@"xgCategory" actions:@[action1, action2] intentIdentifiers:@[] options:XGNotificationCategoryOptionNone];
```

### Creating a Configuration Class

Manage the style and characteristics of the push message notification bar

**API**

```objective-c
+ (nullable instancetype)configureNotificationWithCategories:(nullable NSSet<XGNotificationCategory *> *)categories types:(XGUserNotificationTypes)types;
```

**Parameter description**

* categories: The collection of categories supported in the notification bar 
* types: The style of the registered notification

**Example**

```objective-c
XGNotificationConfigure *configure = [XGNotificationConfigure configureNotificationWithCategories:[NSSet setWithObject:category] types:XGUserNotificationTypeAlert|XGUserNotificationTypeBadge|XGUserNotificationTypeSound];
```

## Reporting Location

**Note**

* Report the geographical location information, which can be used for location-based targeted pushes by TPNS

**API**

```objective-c
- (void)reportLocationWithLatitude:(double)latitude longitude:(double)longitude;
```

**Parameter description**

* latitude: Latitude
* longitude: Longitude

**Example**

```Objective-C
[[XGPush defaultManager] reportLocationWithLatitude:20.0 longitude:19.0];
```

## Automatically Increasing Badge Number by 1

**Note**

* Call this API to report the current app badge number to the TPNS server. After the client is configured, you can use the "automatically increasing badge number by 1" feature, which is at Console > Create a push > Notification bar message > General settings > Badge number.

**API**

```objective-c
- (void)setBadge:(NSInteger)badgeNumber;
```

**Parameter description**

* badgeNumber The badge number of the app

**Note:  
1. This API must be called locally; otherwise, the badge number will not change even if the "automatically increasing badge number by 1" feature is enabled.  
2. This API is only available for SDK v3.1.0 and higher. In older versions, the badge count will not change even if the "automatically increasing badge number by 1" feature is enabled in the console.
**

**Example**

```Objective-C
[[XGPush defaultManager] setBadge:7];
```

## Managing App Badge

**Note**

* Manage the badge number displayed by the app

**API**

```objective-c
@property (nonatomic) NSInteger xgApplicationBadgeNumber;
```

**Example**

```objective-c
// Set the app badge
[[XGPush defaultManager] setXgApplicationBadgeNumber:0];

// Get the app badge
NSInteger number = [[XGPush defaultManager] xgApplicationBadgeNumber];
```

## Push Effect Statistics

**Note**

* In order to better understand the operational effect of each push message, it is necessary to report the action of the user on the message.

The data reporting API needs to be called.  
**API**

```Objective-C
- (void)reportXGNotificationInfo:(nonnull NSDictionary *)info;
```

**Example**

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

**Example**

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

**Example**

```Objective-C
 - (void)xgPushUserNotificationCenter:(UNUserNotificationCenter *)center
   didReceiveNotificationResponse:(UNNotificationResponse *)response
   withCompletionHandler:(void(^)())completionHandler 
   {
  
    [[XGPush defaultManager] reportXGNotificationResponse:response];
            completionHandler();

   }
```

If you want to enable the app to display the push message in the foreground, you need to implement the following method and call the reporting API.

**API**

```Objective-C
- (void)xgPushUserNotificationCenter:(UNUserNotificationCenter *)center willPresentNotification:(UNNotification *)notification withCompletionHandler:(void (^)(UNNotificationPresentationOptions))completionHandler;
```

**Example**

```Objective-C
- (void)xgPushUserNotificationCenter:(UNUserNotificationCenter *)center willPresentNotification:(UNNotification *)notification withCompletionHandler:(void (^)(UNNotificationPresentationOptions))completionHandler {
    [[XGPush defaultManager] reportXGNotificationInfo:notification.request.content.userInfo];
    completionHandler(UNNotificationPresentationOptionBadge | UNNotificationPresentationOptionSound | UNNotificationPresentationOptionAlert);
}
```

## Managing Device Token

### Querying Device Token

**Note**

* Query the Token string obtained by the current app from APNs

**API**

```objective-c
@property (copy, nonatomic, nullable, readonly) NSString *deviceTokenString;
```

**Example**

```objective-c
NSString *token = [[XGPushTokenManager defaultTokenManager] deviceTokenString];
```

### Querying APNs Registration Result

**Note**

* If the registration is successful, the app will call the callback method of the `UIApplicationDelegate` delegate object \(see below\):

**API**

```Objective-C
- (void)application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken;
```

### Querying TPNS Registration Result

**Note**

* The SDK startup method automatically registers the Token obtained by the device from APNs to the TPNS server, and the registration result will be returned in the callback method of `XGPushDelegate` \(see below\):

**API**

```objective-c
- (void)xgPushDidRegisteredDeviceToken:(NSString *)deviceToken error:(NSError *)error;
```

_**Note: This callback method is called after the registration is successful. After the current Token is registered, the SDK will cache the registration information, and this method will not be called again.**_

### Binding/Unbinding Tag and Account

**Note**

* You can bind tags to different users and then push based on a specific tag, i.e., enabling all devices with the tag to receive the push. One device can bind multiple tags.

**Single-operation API**
```Objective-C
- (void)bindWithIdentifier:(nullable NSString *)identifier type:(XGPushTokenBindType)type;
- (void)unbindWithIdentifer:(nullable NSString *)identifier type:(XGPushTokenBindType)type;
```

**Parameter description**

* identifier: Tag or account
* type: Binding type

**Example**

```Objective-C
// Bind the tag:
[[XGPushTokenManager defaultTokenManager] bindWithIdentifier:@"your tag" type:XGPushTokenBindTypeTag];

// Unbind the tag
[[XGPushTokenManager defaultTokenManager] unbindWithIdentifer:@"your tag" type:XGPushTokenBindTypeTag];

// Bind the account:
[[XGPushTokenManager defaultTokenManager] bindWithIdentifier:@"your account" type:XGPushTokenBindTypeAccount];

// Unbind the account:
[[XGPushTokenManager defaultTokenManager] unbindWithIdentifer:@"your account" type:XGPushTokenBindTypeAccount];
```

**Batch operation API**

```Objective-C
- (void)bindWithIdentifiers:(nonnull NSArray <NSString *> *)identifiers type:(XGPushTokenBindType)type
- (void)unbindWithIdentifers:(nonnull NSArray <NSString *> *)identifiers type:(XGPushTokenBindType)type;
```
**Parameter description**

* identifiers: List of tags or accounts
* type: Binding type

**Note**
* XG SDK 3.2.0+
* Account type is not supported for the time being. The tag string cannot contain spaces or tabs.

### Batch Updating Tags/accounts

**API**
```Objective-C
- (void)updateBindedIdentifiers:(nonnull NSArray <NSString *> *)identifiers bindType:(XGPushTokenBindType)type;
```
**Parameter description**

* identifiers: Tag identifier string array. The tag string cannot contain spaces or tabs
* type: Identifier type

**Note**
* XG SDK 3.2.0+
* If the tag type is specified, this API will replace all the old tags corresponding to the current Token with the current tag; if the account type is specified, this API will only take the first one in the identifiers list.

### Clearing All Tags/accounts

**API**
```Objective-C
- (void)clearAllIdentifiers:(XGPushTokenBindType)type;
```
**Parameter description**
* type: Identifier type

**Note**
* XG SDK 3.2.0+

### Querying Bound Tags and Accounts

**Note**

* Query the identifier bound to the current Token object according to the specified type 

**API**

```objective-c
- (nullable NSArray<NSString *> *)identifiersWithType:(XGPushTokenBindType)type;
```

**Example**

```objective-c
// Query the tag
[[XGPushTokenManager defaultTokenManager] identifiersWithType:XGPushTokenBindTypeTag];
// Query the account
[[XGPushTokenManager defaultTokenManager] identifiersWithType:XGPushTokenBindTypeAccount];
```

## Querying Device Notification Permission

**Note**

* Query whether the device notification permission is granted by the user 

**API**

```objective-c
- (void)deviceNotificationIsAllowed:(nonnull void (^)(BOOL isAllowed))handler;
```

**Parameter description**

* handler: The return method of the query result

**Example**

```objective-c
[[XGPush defaultManager] deviceNotificationIsAllowed:^(BOOL isAllowed) {
        <#code#>
    }];
```

## Querying SDK Version

**Note**

* Query the current SDK version

**API**

```objective-c
- (nonnull NSString *)sdkVersion;
```

**Example**

```objective-c
[[XGPush defaultManager] sdkVersion];
```

## Local Push

For local push-related features, see the [Apple developer documentation](https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/SchedulingandHandlingLocalNotifications.html#//apple_ref/doc/uid/TP40008194-CH5-SW1).

