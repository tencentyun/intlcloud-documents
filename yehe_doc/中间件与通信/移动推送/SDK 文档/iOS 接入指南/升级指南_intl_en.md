

## TPNS iOS SDK v1.3.4.0

### 1. Adding support for in-app message display
#### 1.1 setting the polling time of in-app messages

##### API description

This API can be used to set the polling time (minimum: 10s; default: 258s) of in-app messages.

```objective-c
/// Set the message polling time interval (minimum: 10s). This API should be called before the singleton initialization.
(void)setMessageTimerInterval:(NSTimeInterval)interval;
```

#### 1.2. Custom event handling for in-app messages

##### XGInAppMessageActionDelegate proxy description

You can obtain custom event parameters through the proxy method `onClickWithCustomAction` to handle related businesses.

```objective-c
/// Button event response proxy
@property (weak, nonatomic, nullable) id<XGInAppMessageActionDelegate> actionDelegate;
```

## TPNS iOS SDK v1.3.2.1

### 1. The SDK has added the API for binding mobile numbers to send ordinary and intelligent SMS messages.

#### API description

This API is used to add or update a mobile number. It is equivalent to calling `upsertAccountsByDict:@{@(1002):@"specific mobile number"}`.

```objective-c
/// @note TPNS SDK1.3.2.1+
- (void)upsertPhoneNumber:(nonnull NSString *)phoneNumber;
```

#### Parameter description

phoneNumber: mobile number in E.164 format `[+][country code or area code][subscriber number]`, for example, +8613711112222. The SDK will encrypt the mobile number for transmission.

#### Sample code

```Objective-C
[[XGPushTokenManager defaultTokenManager] upsertPhoneNumber:@"+8613712345678"];;
```

>! 
>- This API should be called after `xgPushDidRegisteredDeviceToken:error:` returns a success.
>- You can call `delAccountsByKeys:[[NSSet alloc] initWithObjects:@(1002), nil]` to delete a mobile number.

 

### 2. The demo demonstrates the method of push notification pop-up window after "license agreement".

 Uncomment the 18th line in the `AppDelegate.h` file to demonstrate the feature in the demo, as shown in the figure below:
 ![](https://main.qcloudimg.com/raw/6bcbd5ce23386a28d47aca3565f6dbd1.png)


