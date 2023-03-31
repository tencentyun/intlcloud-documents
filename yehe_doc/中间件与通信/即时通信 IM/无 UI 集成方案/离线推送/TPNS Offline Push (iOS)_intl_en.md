The offline push feature of IM is provided by [Tencent Push Notification Service (TPNS)](https://intl.cloud.tencent.com/document/product/1024/32592). This document introduces how to integrate TPNS and run through the offline push feature.

>!
>
>- Before integrating TPNS, you need to upgrade your IM SDK to [v6.0.1975 or later](https://intl.cloud.tencent.com/document/product/1047/33996).
## Integrating TPNS and Run Through the Offline Push Feature

[](id:step1)
### Step 1. Apply for an Apple push certificate

Offline push depends on Apple's native push channel. Before configuring TPNS push, you need to acquire an Apple push certificate by referring to [Acquisition of Push Certificate](https://intl.cloud.tencent.com/document/product/1024/30728).

[](id:step2)
### Step 2. TPNS console configuration

If you haven't configured offline push information in the IM console, log in to the [TPNS console](https://console.cloud.tencent.com/tpns/product) and configure offline push information as follows:

1. Create a product: go to the TPNS console, choose **Product Management**, click **Create Product**, and enter product information such as the product name and description.
![](https://sdk-im-1252463788.cos.ap-hongkong.myqcloud.com/tools/resource/offlinepush/ios/en/1.png)
2. In the **Basic Configuration** area, select the added product and enter the bundle ID of the app configured.
![](https://sdk-im-1252463788.cos.ap-hongkong.myqcloud.com/tools/resource/offlinepush/ios/en/2.png)
3. After the product is successfully created, you can obtain the product's TPNS parameters such as AccessID and AccessKey.
![](https://sdk-im-1252463788.cos.ap-hongkong.myqcloud.com/tools/resource/offlinepush/ios/en/3.png)
4. Upload the push certificate: go to the TPNS console, select a product, choose **Basic Config** > **Push Certificate** > **Upload**, and configure the Apple push certificate obtained in step 1 to TPNS.
![](https://sdk-im-1252463788.cos.ap-hongkong.myqcloud.com/tools/resource/offlinepush/ios/en/4.png)
5. Third-party service authorization: go to the **Third-Party Service Authorization** page to authorize the offline push feature of the IM app to TPNS.
  1. Select **Cloud IM App Authorization** and click **Add Authorization**.
![](https://sdk-im-1252463788.cos.ap-hongkong.myqcloud.com/tools/resource/offlinepush/ios/en/5.png)
  2. Select the IM app for authorization, select the newly created TPNS product app, and submit the authorization.
<img src="https://qcloudimg.tencent-cloud.cn/raw/dbd9bea878d12e4fc1db8d4909e1dc5b.png" width=450>

>? If you have already configured offline push information in the IM console, the system will automatically migrate the information to the [TPNS console](https://console.cloud.tencent.com/tpns/product), and you can log in to the [TPNS console](https://console.cloud.tencent.com/tpns/product) to modify the information. IM will continue to use the configured information to perform offline push.
>![](https://sdk-im-1252463788.cos.ap-hongkong.myqcloud.com/tools/resource/offlinepush/ios/en/6.png)


[](id:step3)
### Step 3. TPNS-iOS SDK integration

See the TPNS [SDK integration document](https://intl.cloud.tencent.com/document/product/1024/30726) to integrate the TPNS-iOS SDK in the project. You are advised to use CocoaPods to perform the integration.

[](id:step4)
### Step 4. IM integration

See the [AppDelegate+Push](https://github.com/tencentyun/TIMSDK/blob/master/iOS/Demo/TUIKitDemo/AppDelegate+Push.h) and [AppDelegate+TPNS](https://github.com/tencentyun/TIMSDK/blob/master/iOS/Demo/TUIKitDemo/AppDelegate+TPNS.m) files in the TUIKit demo to quickly interconnect IM and TPNS.

1. **Initialize the push service**: when initializing the TPNS push service, you need to call the TPNS API to configure the following:
	-  `- configureClusterDomainName`: configure the access point, which should be consistent with the access point selected during product creation in [step 2](#step2). If Guangzhou is selected during product creation, you can ignore this configuration.
	-  `- startXGWithAccessID:accessKey:delegate`: initialize the TPNS service. The `tpnsAccessID` and `tpnsAccessKey` can be obtained from the product created in [step 2](#step2) in the console.
```
- (void)push_init
{
    // Enable debugging
#if DEBUG
    [[XGPush defaultManager] setEnableDebug:YES];
#endif
    // If Guangzhou is selected as the access point, you can ignore this configuration.
    [[XGPush defaultManager] configureClusterDomainName:@"tpns.hk.tencent.com"];
    [[XGPush defaultManager] startXGWithAccessID:tpnsAccessID accessKey:tpnsAccessKey delegate:self];
    NSLog(@"[PUSH][TPNS] %s", __func__);
}
```

2. **Perform account binding during login**: after logging in to the IM SDK, you need to perform the following operations:
	 1. Get and save the token obtained after TPNS registration from the TPNS-iOS SDK callback `- xgPushDidRegisteredDeviceToken:xgToken:error:`.
	 2. Bind the current login IM account with the TPNS push service.

```
/**
@brief   // Callback for TPNS registration
@param deviceToken   // `Device Token` generated by APNs
@param xgToken   // Token generated by TPNS, which needs to be used during message push. TPNS maintains the mapping relationship between this value and the device token generated by APNs.
@param error   // Error message. If `error` is `nil`, the push service has been successfully registered.
@note TPNS SDK1.2.6.0+
*/

- (void)xgPushDidRegisteredDeviceToken:(nullable NSString *)deviceToken xgToken:(nullable NSString *)xgToken error:(nullable NSError *)error
{
    NSLog(@"[PUSH][TPNS] %s, deviceToken:%@, xgToken:%@, error:%@", __func__, deviceToken, xgToken, error);
    if (error == nil) {
        // 1. Save the TPNS token.
        NSData *data = [xgToken dataUsingEncoding:NSUTF8StringEncoding];
        self.deviceToken = data;
        
        // 2. Register the token and bind the account during login.
        [self push_registerIfLogined:_currentAccount];
    }
}

// This method needs to be called twice:
// 1. Call this method after logging in to the IM SDK.
// 2. Call this method after getting the token from the TPNS callback `xgPushDidRegisteredDeviceToken:xgToken:error`.
- (void)push_registerIfLogined:(NSString *)userID
{
    NSLog(@"[PUSH] %s, %@", __func__, userID);
    // 1. Report the token.
    if (self.deviceToken) {
        V2TIMAPNSConfig *confg = [[V2TIMAPNSConfig alloc] init];
        // For TPNS, you do not need to set `businessID`.
        confg.businessID = 0;
        // For TPNS, you need to report the obtained TPNS token here.
        confg.token = self.deviceToken;
        // Specify that the current token is a TPNS token.
        confg.isTPNSToken = YES;
        [[V2TIMManager sharedInstance] setAPNS:confg succ:^{
             NSLog(@"%s, succ, %@", __func__, supportTPNS ? @"TPNS": @"APNS");
        } fail:^(int code, NSString *msg) {
             NSLog(@"%s, fail, %d, %@", __func__, code, msg);
        }];
    }
    
    // 2. Bind the account after login.
    [XGPushTokenManager.defaultTokenManager upsertAccountsByDict:@{ @(0): userID?:@"" }];
}
```

3. **Unbind the account upon logout**: after logging out of the IM SDK, you need to call the following method to unbind the TPNS push account to avoid receiving pushed messages after logout.

```
- (void)push_unregisterIfLogouted
{
    // Unbind the account.
    [XGPushTokenManager.defaultTokenManager delAccountsByKeys:[NSSet setWithObject:@(0)]];
    NSLog(@"[PUSH][TPNS] %s", __func__);
}
```

4. **Set offline push messages when sending messages.**
When calling [sendMessage](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a3694cd507a21c7cfdf7dfafdb0959e56) to send messages, you can use [V2TIMOfflinePushInfo](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMOfflinePushInfo.html) to set offline push parameters. For more information, see the `+ sendMessage:toConversation:isSendPushInfo:isOnlineUserOnly:priority:Progress:SuccBlock:FailBlock:` method of [TUIMessageDataProvider](https://github.com/tencentyun/TIMSDK/blob/master/iOS/TUIKit/TUIChat/DataProvider/TUIMessageDataProvider.m) in the TUIKit demo.

```java
    NSString *userID = conversationData.userID;
    NSString *groupID = conversationData.groupID;
    NSAssert(userID || groupID, @"At least one target conversation is required");
    NSParameterAssert(message);
    
    V2TIMOfflinePushInfo *pushInfo = nil;
    if (isSendPushInfo) {
        pushInfo = [[V2TIMOfflinePushInfo alloc] init];
        BOOL isGroup = groupID.length > 0;
        NSString *senderId = isGroup ? (groupID) : ([TUILogin getUserID]);
        senderId = senderId?:@"";
        NSString *nickName = isGroup ? (conversationData.title) : ([TUILogin getNickName]?:[TUILogin getUserID]);
        nickName = nickName ?: @"";
        NSDictionary *ext = @{
            @"entity": @{
                    @"action": @1,
                    @"content": [self getDisplayString:message],
                    @"sender": senderId,
                    @"nickname": nickName,
                    @"faceUrl": [TUILogin getFaceUrl]?:@"",
                    @"chatType": isGroup?@(V2TIM_GROUP):@(V2TIM_C2C)
            }
        };
        NSData *data = [NSJSONSerialization dataWithJSONObject:ext options:NSJSONWritingPrettyPrinted error:nil];
        pushInfo.ext = [[NSString alloc] initWithData:data encoding:NSUTF8StringEncoding];
        // Android OPPO model compatibility field. You can ignore this setting.
        pushInfo.AndroidOPPOChannelID = @"tuikit";
    }
    
    return [V2TIMManager.sharedInstance sendMessage:message
                                           receiver:userID
                                            groupID:groupID
                                           priority:priority
                                     onlineUserOnly:isOnlineUserOnly
                                    offlinePushInfo:pushInfo
                                           progress:progress
                                               succ:succ
                                               fail:fail];
```

5. **Parse offline push messages.**
After TPNS is integrated, your app can listen for notification bar push clicks via the TPNS callback `- xgPushDidReceiveNotificationResponse:withCompletionHandler:`, parse offline push messages based on the offline push format configured via [V2TIMOfflinePushInfo](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMOfflinePushInfo.html) in [step 4](#step4), and implement redirection. For more information, see the code for parsing offline push messages in the TUIKit demo.

```
 /// Unified click callback
/// @param response   //`UNNotificationResponse` for iOS 10+ and macOS 10.14+, or `NSDictionary` for earlier versions
- (void)xgPushDidReceiveNotificationResponse:(nonnull id)response withCompletionHandler:(nonnull void (^)(void))completionHandler {
    /// code
    NSDictionary *custom = nil;
    if (@available(iOS 10.0, *)) {
        /// Getting messages on iOS 10 or later versions
        if ([response isKindOfClass:UNNotificationResponse.class]) {
            NSDictionary *userInfo = ((UNNotificationResponse *)response).notification.request.content.userInfo;
            if ([userInfo.allKeys containsObject:@"custom"]) {
                NSString *customStr = userInfo[@"custom"];
                custom = [TCUtil jsonSring2Dictionary:customStr];
            }
        }
    } else {
        /// Getting messages on iOS versions earlier than 10
        NSLog(@"notification dic: %@", response);
        custom = response;
    }
    
    if (custom == nil || ![custom isKindOfClass:NSDictionary.class]) {
        completionHandler();
        return;
    }
    
    if (![custom.allKeys containsObject:@"entity"]) {
        completionHandler();
        return;
    }
    
    // Response message content
    [self onReceiveOfflinePushEntity:custom[@"entity"]];
    
    completionHandler();
}

- (void)onReceiveOfflinePushEntity:(NSDictionary *)entity
{
    NSLog(@"[PUSH] %s, %@", __func__, entity);
    if (entity == nil ||
        ![entity.allKeys containsObject:@"action"] ||
        ![entity.allKeys containsObject:@"chatType"]) {
        return;
    }
    // Business (`action`): 1 - plain text push; 2 - audio/video call push
    // Chat type (`chatType`): 1 - one-to-one chat; 2 - group chat
    NSString *action = entity[@"action"];
    NSString *chatType = entity[@"chatType"];
    if (action == nil || chatType == nil) {
        return;
    }

    // `action`: 1 - plain text push
    if ([action intValue] == APNs_Business_NormalMsg) {
        if ([chatType intValue] == 1) {   //C2C
            self.userID = entity[@"sender"];
        } else if ([chatType intValue] == 2) { //Group
            self.groupID = entity[@"sender"];
        }
        if ([[V2TIMManager sharedInstance] getLoginStatus] == V2TIM_STATUS_LOGINED) {
            
            // Respond with a common offline message, which can be redirected to the corresponding chat page.
            ...
        }
    }
    // `action`: 2 - audio/video call push
    else if ([action intValue] == APNs_Business_Call) {
        // Audio/Video call invitation push in a one-to-one chat does not require processing. It will be automatically processed by TUIKit after your app is started.
        if ([chatType intValue] == 1) {   //C2C
            return;
        }
        // Content
        NSDictionary *content = [TCUtil jsonSring2Dictionary:entity[@"content"]];
        if (!content) {
            return;
        }
        UInt64 sendTime = [entity[@"sendTime"] integerValue];
        uint32_t timeout = [content[@"timeout"] intValue];
        UInt64 curTime = [[V2TIMManager sharedInstance] getServerTime];
        if (curTime - sendTime > timeout) {
            [TUITool makeToast:@"Call receiving timeout"];
            return;
        }
        self.signalingInfo = [[V2TIMSignalingInfo alloc] init];
        self.signalingInfo.actionType = (SignalingActionType)[content[@"action"] intValue];
        self.signalingInfo.inviteID = content[@"call_id"];
        self.signalingInfo.inviter = entity[@"sender"];
        self.signalingInfo.inviteeList = content[@"invited_list"];
        self.signalingInfo.groupID = content[@"group_id"];
        self.signalingInfo.timeout = timeout;
        self.signalingInfo.data = [TCUtil dictionary2JsonStr:@{@"room_id" : content[@"room_id"],
                                                               @"version" : content[@"version"],
                                                               @"call_type" : content[@"call_type"]}];
        if ([[V2TIMManager sharedInstance] getLoginStatus] == V2TIM_STATUS_LOGINED) {
            // Respond with the offline message of the group chat, through which you can directly open the group chat page.
            ...
        }
    }
}


```



## FAQs

### Why doesn't offline push work for common messages?

First, verify that the app and the certificate have the same runtime environment. Otherwise, offline pushes will not be received.

### Why doesn't offline push work for custom messages?

The offline push for custom messages is different from that for ordinary messages. As we cannot parse the content of custom messages, the push content cannot be determined. Therefore, by default, custom messages are not pushed offline. If you need offline push for custom messages, you need to set the `desc` field in [offlinePushInfo](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMOfflinePushInfo.html) during [sendMessage](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a3694cd507a21c7cfdf7dfafdb0959e56), and the `desc` information will be displayed by default during push.

### How do I disable the receiving of offline push messages?

To disable the receiving of offline push messages, set the `config` parameter of the [setAPNS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07APNS_08.html#a6aecbdc0edaa311c3e4e0ed3e71495b1) API to `nil`. This feature is supported from v5.6.1200.

### Why is the badge of unread pushed messages incorrect?
After integrating TPNS, you need to set the TPNS offline push badge. See the `-onTPNSBadgeChanged:` method in [AppDelegate+TPNS](https://github.com/tencentyun/TIMSDK/blob/master/iOS/Demo/TUIKitDemo/AppDelegate+TPNS.m) to set the local badge for TPNS.
