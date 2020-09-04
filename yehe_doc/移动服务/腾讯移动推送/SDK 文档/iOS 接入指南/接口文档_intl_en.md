## Launching TPNS Service

#### API description
Launch the TPNS service by using the information of the application registered at the official website of TPNS. This is new in SDK v1.2.7.2 or above. For legacy versions, please see `XGPush.h`.

```objective-c
/// @note TPNS SDK1.2.7.2+
- (void)startXGWithAccessID:(uint32_t)accessID accessKey:(nonnull NSString *)accessKey delegate:(nullable id<XGPushDelegate>)delegate;
```

#### Parameter description
- accessID: `AccessID` applied through the frontend.
- accessKey: `AccessKey` applied through the frontend.
- Delegate: callback object. 

>!The parameters required by the API must be entered correctly; otherwise, TPNS will not be able to push messages correctly for the application.

#### Sample code
```Objective-C
 [[XGPush defaultManager] startXGWithAccessID:<your AccessID> accessKey:<your AccessKey> delegate:self];
```

## Ending TPNS Service

#### API description
After the TPNS service is stopped, the application will not be able to push messages to devices through TPNS. To receive messages pushed by TPNS again, you must call the `startXGWithAccessID:accessKey:delegate:` method again to restart the TPNS service.
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
Create a clickable event action in the notification message.

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

>!The notification bar has the click event feature, which is only supported in iOS 8.0+. For iOS 7.x or earlier, this method will return null.

### Creating category object

#### API description
Create a category object to manage the action object of the notification bar.
```objective-c
+ (nullable id)categoryWithIdentifier:(nonnull NSString *)identifier actions:(nullable NSArray<id> *)actions intentIdentifiers:(nullable NSArray<NSString *> *)intentIdentifiers options:(XGNotificationCategoryOptions)options
```

#### Parameter description
- identifier: category object ID.
- actions: action object group owned by the current category.
- intentIdentifiers: used to indicate identifiers that can be recognized by Siri.
- options: category characteristics.

>!The notification bar has the click event feature, which is only supported in iOS 8+. For iOS 8 or earlier, this method will return null.


#### Sample code
```Objective-C
XGNotificationCategory *category = [XGNotificationCategory categoryWithIdentifier:@"xgCategory" actions:@[action1, action2] intentIdentifiers:@[] options:XGNotificationCategoryOptionNone];
```

### Creating configuration class
#### API description
Manage the style and characteristics of the push message notification bar.
```objective-c
+ (nullable instancetype)configureNotificationWithCategories:(nullable NSSet<id> *)categories types:(XGUserNotificationTypes)types;
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
Call this API to report the current application badge number to the TPNS server. After the client is configured, you can use the "auto increased by 1" feature for iOS, which can be found in the console (create push > notification bar message > general settings > badge number).

```objective-c
- (void)setBadge:(NSInteger)badgeNumber;
```

#### Parameter description
badgeNumber: badge number of application.


>!This API must be called locally; otherwise, the badge number by default will not change, even if the "auto increased by 1" feature for iOS is enabled.  


#### Sample code
```Objective-C
[[XGPush defaultManager] setBadge:7];
```

## Managing Application Badge

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



## TPNS Token and Registration Result


### Querying TPNS token
#### API description
This API is used to query the token string generated by the current application on the TPNS server.
```objective-c
@property (copy, nonatomic, nullable, readonly) NSString *xgTokenString;
```

#### Sample code
```objective-c
NSString *token = [[XGPushTokenManager defaultTokenManager] xgTokenString];
```

### Registration result callback
#### API description

After the SDK is started, use this method callback to return the registration result and token.

```objective-c
- (void)xgPushDidRegisteredDeviceToken:(nullable NSString *)deviceToken xgToken:(nullable NSString *)xgToken error:(nullable NSError *)error
```


#### Response parameter description

- deviceToken: `Device Token` generated by APNs.
- xgToken: `Token` generated by TPNS, which needs to be used during message push. TPNS maintains the mapping relationship between this value and the `Device Token` of APNs.
- error: error message. If `error` is `nil`, the push service has been successfully registered.

### Registering failure callback
#### API description
This callback is new in SDK 1.2.7.2 and used for TPNS registration failures.

```objective-c
/// @note TPNS SDK1.2.7.2+
- (void)xgPushDidFailToRegisterDeviceTokenWithError:(nullable NSError *)error
```

## Account/Tag Feature
### Binding/Unbinding tag and account
#### API description
You can bind tags/accounts to different users and then push based on a specific tag/account.

>?
>- This API should be called after `xgPushDidRegisteredDeviceToken:error:` returns a success.
>- One application can have up to 10,000 custom tags. One device token can be bound to up to 100 custom tags (if you want to increase this limit, please submit a ticket). One custom tag can be bound to an unlimited number of device tokens.

#### Operation APIs 
```Objective-C
- (void)bindWithIdentifiers:(nonnull NSArray *)identifiers type:(XGPushTokenBindType)type;
- (void)unbindWithIdentifers:(nonnull NSArray *)identifiers type:(XGPushTokenBindType)type;
```

#### Parameter description
- identifiers: specifies the ID to be bound. The tag string cannot contain spaces or tabs.
- type: binding type.

>?
>- For tag operations, `identifiers` is a tag string array (the tag string cannot contain spaces or tabs).
>- For account operations, a dictionary array is required, and the key is fixed.
>- Syntax for Objective-C: @[@{@"account":identifier, @"accountType":@(0)}].
>- Syntax for Swift: [["account":identifier, "accountType":NSNumber(0)]].
>- For more `accountType` values, please see the enumerated values of `XGPushTokenAccountType`.


#### Sample code
```Objective-C
// Bind the tag:
[[XGPushTokenManager defaultTokenManager] bindWithIdentifiers:@[identifier] type:XGPushTokenBindTypeTag];

// Unbind the tag
[[XGPushTokenManager defaultTokenManager] unbindWithIdentifers:@[identifier] type:XGPushTokenBindTypeTag];

// Bind an account:
[[XGPushTokenManager defaultTokenManager] bindWithIdentifiers:@[@{@"account":identifier, @"accountType":@(0)}] type:XGPushTokenBindTypeAccount];

// Unbind an account:
[[XGPushTokenManager defaultTokenManager] unbindWithIdentifers:@[@{@"account":identifier, @"accountType":@(0)}]type:XGPushTokenBindTypeAccount];
```

### Batch updating tags/accounts
#### API description
This API is used to overwrite the original ID (tag/account). If no ID was previously bound, this API will add an ID.

>?This API should be called after `xgPushDidRegisteredDeviceToken:error:` returns a success.


```Objective-C
- (void)updateBindedIdentifiers:(nonnull NSArray *)identifiers bindType:(XGPushTokenBindType)type;
```

#### Parameter description 
- identifiers: tag ID string array. The tag string cannot contain spaces or tabs.
- type: ID type.

>?
>- For tag operations, `identifiers` is a tag string array (the tag string cannot contain spaces or tabs).
>- For account operations, a dictionary array is required, and the key is fixed.
>- Syntax for Objective-C: @[@{@"account":identifier, @"accountType":@(0)}].
>- Syntax for Swift: [["account":identifier, "accountType":NSNumber(0)]].
>- For more `accountType` values, please see the enumerated values of `XGPushTokenAccountType`.

>!If the tag type is specified, this API will replace all the old tags corresponding to the current token with the current tag; if the account type is specified, this API will only take the first one in the `identifiers` list

### Clearing all tags/accounts

#### API description
This API is used to clear all IDs by ID type.

>?This API should be called after `xgPushDidRegisteredDeviceToken:error:` returns a success.

```Objective-C
- (void)clearAllIdentifiers:(XGPushTokenBindType)type;
```
**Parameter description**
type: ID type.


### Querying tags and accounts bound to token
#### API description
This API is used to query the ID bound to the current token object by the specified type.

>?This API should be called after `xgPushDidRegisteredDeviceToken:error:` returns a success.

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
/// @note TPNS SDK1.2.4.1+
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
Import the header file `XGForFreeVersion.h` and call before `startXGWithAccessID`:
```
@property uint32_t freeAccessId;
```
#### Parameter description
-  @freeAccessId    `accessId` of the TPNS platform (SDK 1.2.5.3+).

#### Sample code
```
[XGForFreeVersion defaultForFreeVersion].freeAccessId = 2200262432;
```
## TPNS Log Hosting

#### API description
You can get TPNS logs by using this method, which has nothing to do with `XGPush->enableDebug`.
#### Parameter description
-  logInfo   Log information

#### Sample code

```
- (void)xgPushLog:(nullable NSString *)logInfo;
```


## Local Push
For local push features, please see [Apple developer documentation](https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/SchedulingandHandlingLocalNotifications.html#//apple_ref/doc/uid/TP40008194-CH5-SW1).





