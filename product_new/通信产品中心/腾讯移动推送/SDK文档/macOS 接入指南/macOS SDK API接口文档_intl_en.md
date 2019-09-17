# SDK API Description

## Launching TPNS

**Description**

* Launch the TPNS service with information of the application registered on the official TPNS website.

**API**

```objective-c
- (void)startXGWithAppID:(uint32_t)appID appKey:(nonnull NSString *)appKey delegate:(nullable id<XGPushDelegate>)delegate ;
```

**Parameter description**

* appID: The application ID you requested through the console, i.e., Access ID
* appKey: The appKey you requested through the console, i.e., Access Key
* delegate: Callback object 

_**Note: the parameters required by the API must be entered correctly, otherwise the TPNS service will not push the message to the application correctly.**_

**Sample**

```Objective-C
[[XGPush defaultManager] startXGWithAppID: <#your access ID#>appKey:<#your access key#> delegate:<#your delegate#>];
```

## Terminating TPNS

**Description**

* After you terminate the TPNS service, you will not be able to use TPNS to push messages to devices. If you to need to use the service again, you must call `startXGWithAppID:appKey:delegate:` to restart the service.

**API**

```objective-c
- (void)stopXGNotification;
```

**Sample**

```Objective-C
[[XGPush defaultManager] stopXGNotification];
```

## Customizing Notification Bar Message Actions

### Creating Actions Supported by Messages

**Description**

Create a clickable event action in the notification message.

**API**

```objective-c
+ (nullable id)actionWithIdentifier:(nonnull NSString *)identifier title:(nonnull NSString *)title options:(XGNotificationActionOptions)options;
```

**Parameter description**

* identifier: Unique identifier of an action 
* title: Action name 
* options: Options supported by the action

**Sample**

```objective-c
XGNotificationAction *action1 = [XGNotificationAction actionWithIdentifier:@"xgaction001" title:@"xgAction1" options:XGNotificationActionOptionNone];
```

_**Note: Only macOS10.14 and higher versions support clickable events in the notification bar. For earlier versions, this method returns null**_

### Creating a Category Object

**Description**

Create a category object in order to manage the Action object of the notification bar.

**API**

```objective-c
+ (nullable id)categoryWithIdentifier:(nonnull NSString *)identifier actions:(nullable NSArray<XGNotificationAction *> *)actions intentIdentifiers:(nullable NSArray<NSString *> *)intentIdentifiers options:(XGNotificationCategoryOptions)options;
```

**Parameter description**

* identifier: Identifier of a category object
* actions: The action object groups of the current category
* intentIdentifiers: Used to indicate the identifiers that can be recognized by Siri
* options: Characteristics of the category

_**Note: Only macOS10.14 and higher versions support clickable events in the notification bar. For earlier versions, this method returns null**_

**Sample**

```Objective-C
XGNotificationCategory *category = [XGNotificationCategory categoryWithIdentifier:@"xgCategory" actions:@[action1, action2] intentIdentifiers:@[] options:XGNotificationCategoryOptionNone];
```

### Creating Configuration Categories

Manage the types and characteristics of the push notification bar

**API**

```objective-c
+ (nullable instancetype)configureNotificationWithCategories:(nullable NSSet<XGNotificationCategory *> *)categories types:(XGUserNotificationTypes)types;
```

**Parameter description**

* categories: The category collection supported in the notification bar 
* types: The registered notification type

**Sample**

```objective-c
XGNotificationConfigure *configure = [XGNotificationConfigure configureNotificationWithCategories:[NSSet setWithObject:category] types:XGUserNotificationTypeAlert|XGUserNotificationTypeBadge|XGUserNotificationTypeSound];
```


## Badge Auto-add 1

**Description**

* Call this API to report the current App badge number to the TPNS server. After client configuration is complete, you can use the **macOS badge auto-add 1** function. This feature is can be configured on console (Create a push notification→Notification bar messages→Common settings→Badge number)

**API**

```objective-c
- (void)setBadge:(NSInteger)badgeNumber;
```

**Parameter description**

* `badgeNumber` is the badge number of the application

**Note:  
1. This API must be called locally, otherwise when the console uses the **macOS badge auto-add 1** feature, the badge will not change by default.  
**

**Sample**

```Objective-C
[[XGPush defaultManager] setBadge:7];
```

## Managing Application Badges

**Description**

* Manage the badge number displayed by Apps

**API**

```objective-c
@property (nonatomic) NSInteger xgApplicationBadgeNumber;
```

**Sample**

```objective-c
// Set the application badge
[[XGPush defaultManager] setXgApplicationBadgeNumber:0];

// Get application badge
NSInteger number = [[XGPush defaultManager] xgApplicationBadgeNumber];
```

## Push Results Statistics

**Description**

* The action the user takes for each message must be reported to help you better understand the operational results of each push message.

The data reporting API needs to be called  
**API**

```Objective-C
- (void)reportXGNotificationInfo:(nonnull NSDictionary *)info;
```

**Sample 1**

```Objective-C
- (BOOL)application:(NSApplication *)application
  didFinishLaunchingWithOptions:(NSDictionary *)launchOptions 
  {
      [[XGPush defaultManager] reportXGNotificationInfo:launchOptions];
      return YES;
  }
```

**Callback API**

```Objective-C
- (void)xgPushUserNotificationCenter:(UNUserNotificationCenter *)center willPresentNotification:(UNNotification *)notification withCompletionHandler:(void (^)(UNNotificationPresentationOptions))completionHandler;
```

**Sample 2**

```Objective-C
- (void)xgPushUserNotificationCenter:(UNUserNotificationCenter *)center willPresentNotification:(UNNotification *)notification withCompletionHandler:(void (^)(UNNotificationPresentationOptions))completionHandler {
    [[XGPush defaultManager] reportXGNotificationInfo:notification.request.content.userInfo];
    completionHandler(UNNotificationPresentationOptionBadge | UNNotificationPresentationOptionSound | UNNotificationPresentationOptionAlert);
}
```

## Managing a Device Token

### Querying a Device Token

**Description**

* Query the Token string obtained from APNs by the current application

**API**

```objective-c
@property (copy, nonatomic, nullable, readonly) NSString *deviceTokenString;
```

**Sample**

```objective-c
NSString *token = [[XGPushTokenManager defaultTokenManager] deviceTokenString];
```

### Querying APN Registration Results

**Description**

* If registration is successful, the application will call the callback method of the `NSApplicationDelegate` proxy object \(as shown below\).

**API**

```Objective-C
- (void)application:(NSApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken;
```

### Querying the Registration Results of TPNS

**Description**

* SDK’s launch method automatically registers the Token obtained by the device from APNs to the TPNS server. The registration result can be returned by using the `XGPushDelegate` \(below\) callback method.

**API**

```objective-c
- (void)xgPushDidRegisteredDeviceToken:(NSString *)deviceToken error:(NSError *)error;
```

_**Note: This callback method is called after successful registration. After the current Token is registered, the SDK caches the registration info, and the method will not be called again.**_

### Binding and Unbinding Tags/Accounts

**Description**

* Developers can bind tags to different users and then push messages to the tag. Pushing messages to tags allows all devices under the tag to receive the push messages. Multiple tags can be bound to a single device.

** Single operation API **
```Objective-C
- (void)bindWithIdentifier:(nullable NSString *)identifier type:(XGPushTokenBindType)type;
- (void)unbindWithIdentifer:(nullable NSString *)identifier type:(XGPushTokenBindType)type;
```

**Parameter description**

* identifier: Tags or accounts
* type: Binding type

**Sample**

```Objective-C
//Bind a tag:
[[XGPushTokenManager defaultTokenManager] bindWithIdentifier:@"your tag" type:XGPushTokenBindTypeTag];

//Unbind a tag:
[[XGPushTokenManager defaultTokenManager] unbindWithIdentifer:@"your tag" type:XGPushTokenBindTypeTag];

//Bind an account:
[[XGPushTokenManager defaultTokenManager] bindWithIdentifier:@"your account" type:XGPushTokenBindTypeAccount];

//Unbind an account:
[[XGPushTokenManager defaultTokenManager] unbindWithIdentifer:@"your account" type:XGPushTokenBindTypeAccount];
```

** Batch operation API **

```Objective-C
- (void)bindWithIdentifiers:(nonnull NSArray <NSString *> *)identifiers type:(XGPushTokenBindType)type
- (void)unbindWithIdentifers:(nonnull NSArray <NSString *> *)identifiers type:(XGPushTokenBindType)type;
```
**Parameter description**

* identifiers: Tags or accounts
* type: Binding type

** Note **
* At present, account type is not supported. Tag strings cannot contain spaces or tab characters.

### Batch Updating Tags/Accounts

** API **
```Objective-C
- (void)updateBindedIdentifiers:(nonnull NSArray <NSString *> *)identifiers bindType:(XGPushTokenBindType)type;
```
**Parameter description**

* identifiers: A string array of tag identifiers. Tag strings cannot contain spaces or tab characters.
* type: Identifier type

** Note **
* If specified as a tag type, the API will replace the old tags corresponding to the Token with the current tags. If specified as an account type, the API takes the first one from the identifiers list.

### Clearing All Tags/Accounts

** API **
```Objective-C
- (void)clearAllIdentifiers:(XGPushTokenBindType)type;
```
**Parameter description**
* type: Identifier type


### Querying Bound Tags and Accounts

**Description**

* Query identifiers bound to current Token objects based on the specified type 

**API**

```objective-c
- (nullable NSArray<NSString *> *)identifiersWithType:(XGPushTokenBindType)type;
```

**Sample**

```objective-c
// Query tags
[[XGPushTokenManager defaultTokenManager] identifiersWithType:XGPushTokenBindTypeTag];
// Query accounts
[[XGPushTokenManager defaultTokenManager] identifiersWithType:XGPushTokenBindTypeAccount];
```

## Querying Device Notification Permissions

**Description**

* Query whether device notification permissions have been allowed by the user 

**API**

```objective-c
- (void)deviceNotificationIsAllowed:(nonnull void (^)(BOOL isAllowed))handler;
```

**Parameter description**

* handler: The return method for the query result

**Sample**

```objective-c
[[XGPush defaultManager] deviceNotificationIsAllowed:^(BOOL isAllowed) {
        <#code#>
    }];
```

## Querying the SDK Version

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

For information about local push-related functions, see [Apple Developer Documentation](https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/SchedulingandHandlingLocalNotifications.html#//apple_ref/doc/uid/TP40008194-CH5-SW1).

