````
## Overview
IM terminal users need to obtain the latest messages at any time. However, considering the limited performance and battery SoC of mobile devices, IM recommends you use the system-grade push channels (APNs) provided by Apple for message notifications when the app is running in the background to avoid excessive resource consumption caused by maintaining a persistent connection. Compared with third-party push channels, APNs provides more stable system-grade persistent connections, enabling users to receive push messages at any time and greatly reducing resource consumption.

> !
>- If you want users to receive IM message notifications when, without proactive logout, the app is switched to the background, the mobile phone screen is locked, or the app process is killed by a user, you can enable the IM offline push.
>- If the `logout` API is called to log out proactively or users are forced to log out due to multi-device login, users cannot receive offline push messages even though IM offline push is enabled.

## Integrating TUIOfflinePush and Running the Offline Push Feature
Before integrating the TUIOfflinePush component, you need to [apply for APNs certificates](https://intl.cloud.tencent.com/document/product/1047/39157#step-1.3A-apply-for-apns-certificates) from Apple and [upload them to the IM console](https://intl.cloud.tencent.com/document/product/1047/39157#step-2.3A-upload-the-certificates-to-the-console). Then you can perform the following steps to quickly integrate IM offline push:

1. [Integrate the TUIOfflinePush component](#pod_tuiofflinepush).
2. [Set push parameters](#push_para).
3. [Customize the tap-to-redirect logic for offline push](#jump).

> ? If you want to integrate the TUIOfflinePush component as easily as possible, you need to log in and log out using the login and logout APIs provided by TUILogin of the TUICore component, and the TUIOfflinePush component automatically senses the login and logout events. If you don't want to use the APIs provided by TUILogin, see [Advanced Usage - Customize login/logout](#advance_login_logout) of TUIOfflinePush.

[](id:pod_tuiofflinepush)
### Step 1. Integrate the TUIOfflinePush component
1. The TUIOfflinePush component supports CocoaPods integration. You need to add the component dependencies in the Podfile.
```
# Prevent `*.xcassets` in TUI components from conflicting with your project.
install! 'cocoapods', :disable_input_output_paths => true  

# TUI components are dependent on static libraries. Therefore, you need to mask the following configuration. If an error is reported, see the explanation in the FAQs part.
# use_frameworks!

# Integrate the TUIOfflinePush component.
pod 'TUIOfflinePush'
```

2. Run the following command to install the TUIOfflinePush component.
```
pod install
```
If you cannot install the latest TUIKit version, run the following command to update the local CocoaPods repository list:
```
 pod repo update
```

[](id:push_para)
### Step 2. Set push parameters
1. After you [upload the certificates to the IM console](https://intl.cloud.tencent.com/document/product/1047/39157), the IM console allocates certificate IDs for you. 



2. In `AppDelegate`, call the `TUIOfflinePushCertificateIDForAPNS` macro to set certificate IDs.
```
@implementation AppDelegate

#ifdef DEBUG
// Configure the development environment certificate
TUIOfflinePushCertificateIDForAPNS(31287)
#else
// Configure the production environment certificate
TUIOfflinePushCertificateIDForAPNS(31288)
#endif

@end
```

> ? `TUIOfflinePushCertificateIDForAPNS` is a built-in macro definition of the component. You can call it from any position in `@implementation` of `AppDelegate`.


[](id:jump)
### Step 3. Customize the tap-to-redirect logic for offline push
1. Upon a tap on a message pushed offline on the notification bar, the TUIOfflinePush component parses the pushed content.
2. If you want to redirect to the chat list, you only need to implement the `-navigateToTUIChatViewController:groupID:` redirection method in AppDelegate.

> ? 
> - TUIOfflinePush parses the message pushed offline and obtains the `userID` and `groupID` of the message by default.
> - If `groupID` is not empty, the message tapped is a group chat message pushed offline.
> - If `groupID` is empty but `userID` is not empty, the message tapped is a one-to-one message pushed offline.
> - You need to implement the `- navigateToTUIChatViewController:groupID:` method in `@implementation` of AppDelegate.

The following sample code demonstrates the redirection logic where, upon a tap on a message pushed offline, the SDK first obtains the current conversation page and then pushes the message to the chat page through the conversation page. You can implement your own redirection logic as needed.

```
// Unified tap-to-redirect
// You can directly copy the current method name to your AppDelegate
- (void)navigateToTUIChatViewController:(NSString *)userID groupID:(NSString *)groupID
{
  // Example: Upon a tap on a push notification, the SDK first redirects to the conversation list page and then redirects to the chat page from the conversation list page
  // 1. Obtain the tabBarController of the current app.
  // 2. Obtain `firstObject` (ConversationController) of the tabBarController.
  // 3. Run `pushToViewController` to redirect to the ChatViewController.
  // After redirecting to the chat page, the SDK allows users to tap the Back button on the upper-left corner to go back to the home page.
  
    UITabBarController *tab = [self getMainController];
    if (![tab isKindOfClass: UITabBarController.class]) {
        // Logging in…
        return;
    }
    if (tab.selectedIndex != 0) {
        [tab setSelectedIndex:0];
    }
    self.window.rootViewController = tab;
    UINavigationController *nav = (UINavigationController *)tab.selectedViewController;
    if (![nav isKindOfClass:UINavigationController.class]) {
        return;
    }

    UIViewController *vc = nav.viewControllers.firstObject;
    if (![vc isKindOfClass:NSClassFromString(@"ConversationController")]) {
        return;
    }
    if ([vc respondsToSelector:NSSelectorFromString(@"pushToChatViewController:userID:")]) {
        [vc performSelector:NSSelectorFromString(@"pushToChatViewController:userID:") withObject:groupID withObject:userID];
    }
}
```

[](id:advance)
## Advanced Usage

[](id:advance_login_logout)
### 1. Customize login/logout

TUIOfflinePush uses the login/logout API provided by TUILogin of the TUICore component by default. If you want to implement your own app/IM login/logout instead of depending on TUILogin, you need to manually call the `registerService` and `unregisterService` APIs after the login and logout operations are completed. 

> ? If you use the login/logout API provided by TUILogin, you do not need to call the `registerService` and `unregisterService` APIs.

[]()

```
// Call after successful login
- (void)onLoginSuccess
{
	// Call the login API of TUIOfflinePush
	[TUIOfflinePushManager.shareManager registerService];
}

// Call after successful logout
- (void)onLogoutSuccess
{
	// Call the logout API of TUIOfflinePush
	[TUIOfflinePushManager.shareManager unregisterService];
}
```
[](id:advance_parse)
### 2. Customize the parsing of content pushed offline

TUIOfflinePush participates in parsing content pushed offline by default and uses the `- navigateToTUIChatViewController:groupID:` API to call back the parsing result to the business layer for custom redirection.

If you want to customize the parsing of the content pushed offline or view the received content pushed offline, you can implement the `- processTUIOfflinePushNotification:` method in AppDelegate.

> ? The returned values of the `- processTUIOfflinePushNotification:` method are described as follows:
>
> * `YES`: the component does not execute the default parsing logic any more, and the processing is taken over by the business layer instead.
> * `NO`: the component continues to execute the default parsing logic and proceeds to call the `- navigateToTUIChatViewController:groupID:` method.

[]()

```
// Receive a message pushed offline
- (BOOL)processTUIOfflinePushNotification:(NSDictionary *)userInfo
{
    // Customize the parsing of the received `userInfo`
    NSLog(@">>> Customize parsing here, %@", userInfo);
    
    // If you do not want the SDK to execute the default parsing logic of TUIOfflinePush, enter `YES`.
    // If you only want to view the pushed content and still use the default parsing and unified tap-to-redirect logic of TUIOfflinePush, enter `NO`.
    return NO;
}
```

[](id:qa)

## FAQs
### Why doesn't offline push work for common messages?
- First, check that the app runtime environment is the same as the certificate environment. Otherwise, offline push messages will not be received.
- Then, check that the app and the certificate run in the production environment. If they run in the development environment, requesting `deviceToken` from Apple might fail. In that case, switch to the production environment to solve the problem.

### Why doesn't offline push work for custom messages?

The offline push for custom messages is different from that for ordinary messages. As we cannot parse the content of custom messages, the push content cannot be determined. Therefore, by default, custom messages are not pushed offline. If you need offline push for custom messages, you need to set the `desc` field in [offlinePushInfo](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMOfflinePushInfo.html) during [sendMessage](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a3694cd507a21c7cfdf7dfafdb0959e56), and the `desc` information will be displayed by default during push.

### How do I disable the receiving of offline push messages?

To disable the receiving of offline push messages, set the `config` parameter of the [setAPNS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07APNS_08.html#a6aecbdc0edaa311c3e4e0ed3e71495b1) API to `nil`. This feature is supported from v5.6.1200.

### What should I do if push messages cannot be received and the backend reports the "bad devicetoken" error?

For Apple devices, `deviceToken` is related to the current compilation environment. If the certificate ID used to [upload deviceToken to Tencent Cloud after logging in to IM SDK](#uploadDeviceToken) is inconsistent with the environment token, the error will be reported.

- If the compilation environment is `Release`, `- application:didRegisterForRemoteNotificationsWithDeviceToken:` calls back the release environment token, `businessID` must be set to the [certificate ID](#businessid) of the production environment.
- If the compilation environment is `Debug`, `- application:didRegisterForRemoteNotificationsWithDeviceToken:` calls back the development environment token, `businessID` must be set to the [certificate ID](#businessid) of the development environment.
```
V2TIMAPNSConfig *confg = [[V2TIMAPNSConfig alloc] init];
/* You need to register a developer certificate with Apple, download and generate the certificate (P12 file) in their developer accounts, and upload the generated P12 file to the Tencent certificate console. The console will automatically generate a certificate ID and pass it to the `businessID` parameter.*/
// Push certificate ID
confg.businessID = sdkBusiId;
confg.token = self.deviceToken;
[[V2TIMManager sharedInstance] setAPNS:confg succ:^{
     NSLog(@"%s, succ, %@", __func__, supportTPNS ? @"TPNS": @"APNS");
} fail:^(int code, NSString *msg) {
     NSLog(@"%s, fail, %d, %@", __func__, code, msg);
}];
```

### What should I do if `deviceToken` is not returned for registration occasionally or APNs' request for token fails in the iOS development environment?
This problem is caused by instability of APNs. You can fix it in the following ways:

1. Insert a SIM card into the phone and use the 4G network.
2. Uninstall and reinstall the application, restart the application, or shut down and restart the phone.
3. Use a package for the production environment.
4. Use another iPhone.xxxxxxxxxx // Call after successful login- (void)onLoginSuccess{    // Call the login API of TUIOfflinePush    [TUIOfflinePushManager.shareManager registerService];}// Call after successful logout- (void)onLogoutSuccess{    // Call the logout API of TUIOfflinePush    [TUIOfflinePushManager.shareManager unregisterService];}```[](id:advance_parse)### 2. Customize the parsing of content pushed offlineTUIOfflinePush participates in parsing content pushed offline by default and uses the `- navigateToTUIChatViewController:groupID:` API to call back the parsing result to the business layer for custom redirection.If you want to customize the parsing of the content pushed offline or view the received content pushed offline, you can implement the `- processTUIOfflinePushNotification:` method in AppDelegate.> ? The returned values of the `- processTUIOfflinePushNotification:` method are described as follows:>> * `YES`: the component does not execute the default parsing logic any more, and the processing is taken over by the business layer instead.> * `NO`: the component continues to execute the default parsing logic and proceeds to call the `- navigateToTUIChatViewController:groupID:` method.[]()```// Receive a message pushed offline- (BOOL)processTUIOfflinePushNotification:(NSDictionary *)userInfo{    // Customize the parsing of the received `userInfo`    NSLog(@">>> Customize parsing here, %@", userInfo);        // If you do not want the SDK to execute the default parsing logic of TUIOfflinePush, enter `YES`.    // If you only want to view the pushed content and still use the default parsing and unified tap-to-redirect logic of TUIOfflinePush, enter `NO`.    return NO;}```[](id:qa)## FAQs### Why doesn't offline push work for common messages?- First, check that the app runtime environment is the same as the certificate environment. Otherwise, offline push messages will not be received.- Then, check that the app and the certificate run in the production environment. If they run in the development environment, requesting `deviceToken` from Apple might fail. In that case, switch to the production environment to solve the problem.### Why doesn't offline push work for custom messages?The offline push for custom messages is different from that for ordinary messages. As we cannot parse the content of custom messages, the push content cannot be determined. Therefore, by default, custom messages are not pushed offline. If you need offline push for custom messages, you need to set the `desc` field in [offlinePushInfo](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMOfflinePushInfo.html) during [sendMessage](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a3694cd507a21c7cfdf7dfafdb0959e56), and the `desc` information will be displayed by default during push.### How do I disable the receiving of offline push messages?To disable the receiving of offline push messages, set the `config` parameter of the [setAPNS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07APNS_08.html#a6aecbdc0edaa311c3e4e0ed3e71495b1) API to `nil`. This feature is supported from v5.6.1200.### What should I do if push messages cannot be received and the backend reports the "bad devicetoken" error?For Apple devices, `deviceToken` is related to the current compilation environment. If the certificate ID used to [upload deviceToken to Tencent Cloud after logging in to IM SDK](#uploadDeviceToken) is inconsistent with the environment token, the error will be reported.- If the compilation environment is `Release`, `- application:didRegisterForRemoteNotificationsWithDeviceToken:` calls back the release environment token, `businessID` must be set to the [certificate ID](#businessid) of the production environment.- If the compilation environment is `Debug`, `- application:didRegisterForRemoteNotificationsWithDeviceToken:` calls back the development environment token, `businessID` must be set to the [certificate ID](#businessid) of the development environment.```V2TIMAPNSConfig *confg = [[V2TIMAPNSConfig alloc] init];/* You need to register a developer certificate with Apple, download and generate the certificate (P12 file) in their developer accounts, and upload the generated P12 file to the Tencent certificate console. The console will automatically generate a certificate ID and pass it to the `businessID` parameter.*/// Push certificate IDconfg.businessID = sdkBusiId;confg.token = self.deviceToken;[[V2TIMManager sharedInstance] setAPNS:confg succ:^{     NSLog(@"%s, succ, %@", __func__, supportTPNS ? @"TPNS": @"APNS");} fail:^(int code, NSString *msg) {     NSLog(@"%s, fail, %d, %@", __func__, code, msg);}];```### What should I do if `deviceToken` is not returned for registration occasionally or APNs' request for token fails in the iOS development environment?This problem is caused by instability of APNs. You can fix it in the following ways:1. Insert a SIM card into the phone and use the 4G network.2. Uninstall and reinstall the application, restart the application, or shut down and restart the phone.3. Use a package for the production environment.4. Use another iPhone.
````
