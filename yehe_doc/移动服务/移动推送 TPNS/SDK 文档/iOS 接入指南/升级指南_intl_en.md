
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
[[XGPushTokenManager defaultTokenManager] upsertPhoneNumber:@"13712345678"];;
```

>! 
>- This API should be called after `xgPushDidRegisteredDeviceToken:error:` returns a success.
>- You can call `delAccountsByKeys:[[NSSet alloc] initWithObjects:@(1002), nil]` to delete a mobile number.

 

### 2. The demo demonstrates the method of push notification pop-up window after "license agreement".

 Uncomment the 18th line in the `AppDelegate.h` file to demonstrate the feature in the demo, as shown in the figure below:
 ![](https://main.qcloudimg.com/raw/5799568949d6174519a0ed21b8a6ad1d.png)

