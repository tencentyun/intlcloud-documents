


## Launching TPNS Service

#### API description
Launch the TPNS service by using the information of the application registered at the official website of TPNS.

```objective-c
- (void)startXGWithAppID:(uint32_t)appID appKey:(nonnull NSString *)appKey delegate:(nullable id<XGPushDelegate>)delegate ;
```

#### Parameter description
- AppID: application ID applied on the console, i.e., the `Access ID`.
- AppKey: `appKey` applied on the console, i.e., the `Access Key`.
- Delegate: callback object. 

>The parameters required by the API must be entered correctly; otherwise, TPNS will not be able to push messages correctly for the application.

#### Sample code
```Objective-C
[[XGPush defaultManager] startXGWithAppID: <#your access ID#>appKey:<#your access key#> delegate:<#your delegate#>];
```

## Ending TPNS Service

#### API description
After the TPNS service is stopped, the application will not be able to push messages to devices through TPNS. To receive messages pushed by TPNS again, you must call `startXGWithAppID:appKey:delegate:` method again to restart the TPNS service.
```objective-c
- (void)stopXGNotification;
```

#### Sample code
```Objective-C
[[XGPush defaultManager] stopXGNotification];
```

## Customizing Notification Bar Message Action

### Creating message action

#### API description
Create a click event action in the notification

```objective-c
+ (nullable id)actionWithIdentifier:(nonnull NSString *)identifier title:(nonnull NSString *)title options:(XGNotificationActionOptions)options;
```

#### Parameter description
- identifier: unique action ID. 
- title: action name. 
- options: options supported by action.


#### Sample code
```objective-c
XGNotificationAction *action1 = [XGNotificationAction actionWithIdentifier:@"xgaction001" title:@"xgAction1" options:XGNotificationActionOptionNone];
```

>The notification bar has the event click feature, which is only supported in iOS 8.0+. For iOS 7.x or earlier, this method will return null.

### Creating category object

#### API description
Create a category object to manage the action object of the notification bar.
```objective-c
+ (nullable id)categoryWithIdentifier:(nonnull NSString *)identifier actions:(nullable NSArray<XGNotificationAction *> *)actions intentIdentifiers:(nullable NSArray<NSString *> *)intentIdentifiers options:(XGNotificationCategoryOptions)options;
```

#### Parameter description
- identifier: category object ID.
- actions: action object group owned by the current category.
- intentIdentifiers: used to indicate identifiers that can be recognized by Siri.
- options: category characteristics.

>The notification bar has the event clicking feature, which is only supported in iOS 8+. For iOS 8 or earlier, this method will return null.


#### Sample code
```Objective-C
XGNotificationCategory *category = [XGNotificationCategory categoryWithIdentifier:@"xgCategory" actions:@[action1, action2] intentIdentifiers:@[] options:XGNotificatio nCategoryOptionNone];
```

### Creating configuration class
#### API description
Manage the style and characteristics of the push message notification bar.
```objective-c
+ (nullable instancetype)configureNotificationWithCategories:(nullable NSSet<XGNotificationCategory *> *)categories types:(XGUserNotificationTypes)types;
```

#### Parameter description
- categories: collection of categories supported by the notification bar. 
- types: style of registered notification.

#### Sample code
```objective-c
XGNotificationConfigure *configure = [XGNotificationConfigure configureNotificationWithCategories:[NSSet setWithObject:category] types:XGUserNotificationTypeAlert|XGUserNotificationTypeBadge|XGUserNotificationTypeSound];
```


## Automatically Increasing Badge Number by 1

#### API description
Call this API to report the current application badge number to the TPNS server. After the client is configured, you can use the badge number "auto increased by 1" feature, which can be found in the console (create push > notification bar message > advanced settings > badge number).

```objective-c
- (void)setBadge:(NSInteger)badgeNumber;
```

#### Parameter description
badgeNumber: badge number of application.

 
>This API must be called locally; otherwise, the badge number by default will not change, even if the "auto increased by 1" feature is enabled.  


#### Sample code
```Objective-C
[[XGPush defaultManager] setBadge:7];
```

## Managing application badge

#### API description
This API is used to manage the badge number displayed by the application and needs to be called in the main thread.
```objective-c
@property (nonatomic) NSInteger xgApplicationBadgeNumber;
```

#### Sample code
```objective-c
// Set the application badge
[[XGPush defaultManager] setXgApplicationBadgeNumber:0];

// Get the application badge
NSInteger number = [[XGPush defaultManager] xgApplicationBadgeNumber];
```



## Managing Device Token

### Querying device token

#### API description
This API is used to query the token string obtained from APNs by the current application.
```objective-c
@property (copy, nonatomic, nullable, readonly) NSString *deviceTokenString;
```

#### Sample code
```objective-c
NSString *token = [[XGPushTokenManager defaultTokenManager] deviceTokenString];
```


### Querying XGToken
#### API description
This API is used to query the token string generated by the current application on the TPNS server.
```objective-c
@property (copy, nonatomic, nullable, readonly) NSString *xgTokenString;
```

#### Sample code
```objective-c
NSString *token = [[XGPushTokenManager defaultTokenManager] xgTokenString];
```




### Querying APNs registration result

#### API description
If the registration is successful, the application will call the callback method of the `UIApplicationDelegate` delegate object \(see below\).

```Objective-C
- (void)application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken;
```

### Querying TPNS registration result

#### API description
The SDK launch method automatically registers the token obtained by the device from APNs to the TPNS server, and the registration result will be returned in the callback method of `XGPushDelegate` \(see below\).


```objective-c
- (void)xgPushDidRegisteredDeviceToken:(NSString *)deviceToken error:(NSError *)error;
```


### Binding/Unbinding tag and account

#### API description
You can bind tags to different users and then push based on a specific tag.

>This API should be called after `xgPushDidRegisteredDeviceToken:error:` returns a success.

#### Single-operation API 
```Objective-C
- (void)bindWithIdentifier:(nullable NSString *)identifier type:(XGPushTokenBindType)type;
- (void)unbindWithIdentifer:(nullable NSString *)identifier type:(XGPushTokenBindType)type;
```

#### Parameter description
- identifier: tag or account.
- type: binding type.

#### Sample code
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

#### Batch operation APIs

```Objective-C
- (void)bindWithIdentifiers:(nonnull NSArray <NSString *> *)identifiers type:(XGPushTokenBindType)type
- (void)unbindWithIdentifers:(nonnull NSArray <NSString *> *)identifiers type:(XGPushTokenBindType)type;
```

#### Parameter description
- identifiers: tag or account list.
- type: binding type.


>The tag or account string cannot contain spaces or tabs.

### Batch updating tags/accounts

#### API description
This API is used to overwrite the original ID (tag/account). If no ID was previously bound, this API will add an ID.

>This API should be called after `xgPushDidRegisteredDeviceToken:error:` returns a success.

```Objective-C
- (void)updateBindedIdentifiers:(nonnull NSArray <NSString *> *)identifiers bindType:(XGPushTokenBindType)type;
```
#### Parameter description 
- identifiers: tag ID string array. The tag string cannot contain spaces or tabs.
- type: ID type.


>If the tag type is specified, this API will replace all the old tags corresponding to the current token with the current tag; if the account type is specified, this API will only take the first one in the `identifiers` list

### Clearing all tags/accounts

#### API description
This API is used to clear all IDs by ID type.

>This API should be called after `xgPushDidRegisteredDeviceToken:error:` returns a success.

```Objective-C
- (void)clearAllIdentifiers:(XGPushTokenBindType)type;
```
**Parameter description**
type: ID type.


### Querying tags and accounts bound to token
#### API description
This API is used to query the ID bound to the current token object by the specified type.

>This API should be called after `xgPushDidRegisteredDeviceToken:error:` returns a success.

```objective-c
- (nullable NSArray<NSString *> *)identifiersWithType:(XGPushTokenBindType)type;
```

#### Sample code
```objective-c
// Query the tag
[[XGPushTokenManager defaultTokenManager] identifiersWithType:XGPushTokenBindTypeTag];
// Query the account
[[XGPushTokenManager defaultTokenManager] identifiersWithType:XGPushTokenBindTypeAccount];
```

## Querying Device Notification Permission

#### API description
This API is used to query whether the user allows device notification. 


```objective-c
- (void)deviceNotificationIsAllowed:(nonnull void (^)(BOOL isAllowed))handler;
```

#### Parameter description
handler: return method of query result.


#### Sample code
```objective-c
[[XGPush defaultManager] deviceNotificationIsAllowed:^(BOOL isAllowed) {
        <#code#>
    }];
```

## Querying SDK Version
#### API description
This API is used to query the current SDK version.

```objective-c
- (nonnull NSString *)sdkVersion;
```

#### Sample code
```objective-c
[[XGPush defaultManager] sdkVersion];
```


## Log Reporting APIs

#### API description
If you find exceptions with push, you can call this API to trigger reporting of local push logs. When feeding back the problem, please provide the file address for us to troubleshoot.
```
- (void)uploadLogCompletionHandler:(nullable void(^)(BOOL result,  NSString * _Nullable errorMessage))handler;
```
#### Parameter description
-  @brief: report log information (SDK 1.2.4.1+).
-  @param handler: report callback.

#### Sample code
```
[[XGPush defaultManager] uploadLogCompletionHandler:nil];
```

## Unregistering XG Platform Service

#### API description
Background: if the application push service is migrated from the XG platform (https://xg.qq.com) to the TPNS platform, duplicate messages may appear when pushing on both platform at the same time. Therefore, you need to call the API of `TPNS SDK(1.2.5.3+)` to unregister the device information on the XG platform.
Import the header file `XGForFreeVersion.h` and call before `startXGWithAppID`:
```
@property uint32_t freeAccessId;
```
#### Parameter description
-  @freeAccessId    `accessId` of the TPNS platform (SDK 1.2.5.3+).

#### Sample code
```
[XGForFreeVersion defaultForFreeVersion].freeAccessId = 2200262432;
```



## Local Push
For local push features, please see [Apple developer documentation](https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/SchedulingandHandlingLocalNotifications.html#//apple_ref/doc/uid/TP40008194-CH5-SW1).






