IM 오프라인 푸시 기능은 [TPNS(Tencent Push Notification Service)](https://intl.cloud.tencent.com/document/product/1024/32592)에서 제공합니다. 본문은 TPNS에 액세스하고 오프라인 푸시 기능을 실행하는 자세한 단계를 소개합니다.

>!
>
>- TPNS에 액세스하려면 IM SDK를 [6.0.1975 버전 이상](https://intl.cloud.tencent.com/document/product/1047/33996)으로 업그레이드해야 합니다.
## TPNS를 연결하여 오프라인 푸시 기능 실행

[](id:step1)
### 1단계: Apple 푸시 인증서 신청

오프라인 푸시는 Apple의 네이티브 푸시 터널에 종속하므로 TPNS 푸시를 설정하기 전에 [푸시 인증서 획득 가이드](https://intl.cloud.tencent.com/document/product/1024/30728)  를 참고하여 Apple 푸시 인증서를 받아야 합니다.

[](id:step2)
### 2단계: TPNS 콘솔 설정

이전에 IM 콘솔에서 오프라인 푸시 정보를 설정하지 않았다면 [TPNS 콘솔](https://console.cloud.tencent.com/tpns/product)에 직접 로그인한 후 아래 단계에 따라 오프라인 푸시 정보를 설정하십시오.

1. 제품 생성: **TPNS 콘솔** > **제품 관리** > **제품 추가**로 이동하여 이름 및 설명과 같은 정보를 입력합니다.
>! 서비스 액세스 포인트 선택:
>- 중국 본토 외 고객을 지원하려면 싱가포르/중국홍콩 액세스 포인트를 선택하십시오.
>- 중국 내 고객만 지원하려면 광저우/상하이 액세스 포인트를 선택하십시오.
>
![](https://qcloudimg.tencent-cloud.cn/raw/44b868c7e3781ceed24c5e1e925ab2c3.png)
2. 기본 설정 열에서 새로 추가된 제품을 선택하고 설정 애플리케이션의 BundleID를 입력합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/8ab7746b97b0dea6690ec0bdf8cb7c21.png)
3. 제품이 성공적으로 생성되면 TPNS의 AccessID 및 AsscessKey와 같은 매개변수를 얻습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/1f510d09d97d1eb25fd5f4efc51fc7cc.png)
4. 푸시 인증서 업로드: **TPNS 콘솔** > **제품 선택** > **기본 설정** > **푸시 인증서** > **업로드**로 이동하여 1단계에서 신청한 Apple 푸시 인증서를 TPNS로 설정합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/f406d41e17ffa726bedb65e2855767ad.png)
5.  타사 서비스 권한 부여: 타사 서비스 권한로 이동하여 IM 애플리케이션의 오프라인 푸시 기능 권한을 TPNS에 부여합니다.
  1. Cloud IM 애플리케이션 권한 부여를 선택하고 **권한 추가**를 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/5e6aff8a59c09303897fe7fb040f9fd1.png)
  2. 바인딩 권한을 부여할 IM 애플리케이션을 선택하고 새로 생성된 TPNS 제품 애플리케이션을 선택한 후 권한 부여를 제출합니다.
<img src="https://qcloudimg.tencent-cloud.cn/raw/8b50ddd0eb4b1e3a734845ffd3046226.png" width=450>

>? 이전에 IM 콘솔에서 오프라인 푸시 정보를 설정한 경우 이러한 설정 정보는 [TPNS 콘솔](https://console.cloud.tencent.com/tpns/product)로 자동 마이그레이션되며, [TPNS 콘솔](https://console.cloud.tencent.com/tpns/product)에 로그인하여 설정 정보를 수정할 수 있습니다. IM은 오프라인 푸시에 이러한 설정 정보를 계속 사용합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/501fbd5af9d19961827968d608755bf3.png)


[](id:step3)
### 3단계: TPNS-iOS SDK 연결

TPNS의 [SDK 연결 문서](https://intl.cloud.tencent.com/document/product/1024/30726)를 참고하여 TPNS-iOS SDK를 프로젝트에 통합합니다. 'cocoapods' 사용을 추천합니다.

[](id:step4)
### 4단계: IM 관련 연결

TUIKitDemo에서 [AppDelegate+Push](https://github.com/tencentyun/TIMSDK/blob/master/iOS/Demo/TUIKitDemo/AppDelegate+Push.h) 및 [AppDelegate+TPNS](https://github.com/tencentyun/TIMSDK/blob/master/iOS/Demo/TUIKitDemo/AppDelegate+TPNS.m) 파일을 참고하여 IM 및 TPNS를 빠르게 연결할 수 있습니다.

1. **푸시 서비스 초기화**. TPNS 푸시 서비스를 초기화할 때 TPNS의 인터페이스 설정을 호출해야 합니다.
	-  `- configureClusterDomainName:` ​​액세스 포인트를 설정합니다. 여기에서 액세스 포인트는 [2단계](#step2)에서 제품 생성 시 선택한 액세스 포인트와 동일합니다. 제품 생성 시 광저우를 선택한 경우 이 설정은 무시할 수 있습니다.
	-  `- startXGWithAccessID:accessKey:delegate:` TPNS 서비스를 초기화합니다. 여기서 `tpnsAccessID`와 `tpnsAccessKey`는 [2단계](#step2)에서 해당 제품의 콘솔에서 얻을 수 있습니다.
```
- (void)push_init
{
    // debug 활성화
#if DEBUG
    [[XGPush defaultManager] setEnableDebug:YES];
#endif
    // tpns 콘솔이 광저우 액세스 포인트로 설정된 경우 무시
    [[XGPush defaultManager] configureClusterDomainName:@"tpns.hk.tencent.com"];
    [[XGPush defaultManager] startXGWithAccessID:tpnsAccessID accessKey:tpnsAccessKey delegate:self];
    NSLog(@"[PUSH][TPNS] %s", __func__);
}
```
2. **로그인 시 계정 바인딩**. IM SDK에 로그인한 후 다음 두 가지 작업을 수행해야 합니다.
	 1. TPNS-iOS SDK의 '- xgPushDidRegisteredDeviceToken:xgToken:error:' 콜백에서 TPNS 가입 token을 받아 저장합니다.
	 2.  현재 로그인한 IM 계정을 TPNS 푸시에 바인딩합니다.
```
/**
@brief 푸시 서비스 등록 콜백
@param deviceToken APNs에 의해 ​​생성된 Device Token
@param xgToken TPNS에 의해 생성된 Token으로, 메시지를 푸시할 때 이 값을 사용해야 합니다. TPNS는 이 값과 APN의 Device Token 간의 매핑 관계를 점검합니다
@param error 오류 메시지, error가 nil이면 푸시 서비스 등록 성공
@note TPNS SDK1.2.6.0+
*/
- (void)xgPushDidRegisteredDeviceToken:(nullable NSString *)deviceToken xgToken:(nullable NSString *)xgToken error:(nullable NSError *)error
{
    NSLog(@"[PUSH][TPNS] %s, deviceToken:%@, xgToken:%@, error:%@", __func__, deviceToken, xgToken, error);
    if (error == nil) {
        // 1. tpns의 token 저장
        NSData *data = [xgToken dataUsingEncoding:NSUTF8StringEncoding];
        self.deviceToken = data;
        
        // 2. 로그인 시 token 가입 및 계정 바인딩
        [self push_registerIfLogined:_currentAccount];
    }
}

// 이 메소드는 두 곳에서 호출해야 합니다.
// 1. IM SDK 로그인 완료 후 이 메소드를 호출해야 함
// 2. TPNS 콜백 xgPushDidRegisteredDeviceToken:xgToken:error: token를 가져온 후
- (void)push_registerIfLogined:(NSString *)userID
{
    NSLog(@"[PUSH] %s, %@", __func__, userID);
    // 1. token 리포트
    if (self.deviceToken) {
        V2TIMAPNSConfig *confg = [[V2TIMAPNSConfig alloc] init];
        // TPNS인 경우 businessID를 입력할 필요가 없음
        confg.businessID = 0;
        // TPNS인 경우 획득한 TPNS token을 리포트해야 함
        confg.token = self.deviceToken;
        // 현재 token이 TPNS의 token 임을 표시
        confg.isTPNSToken = YES;
        [[V2TIMManager sharedInstance] setAPNS:confg succ:^{
             NSLog(@"%s, succ, %@", __func__, supportTPNS ? @"TPNS": @"APNS");
        } fail:^(int code, NSString *msg) {
             NSLog(@"%s, fail, %d, %@", __func__, code, msg);
        }];
    }
    
    // 2. 로그인 후 계정 바인딩
    [XGPushTokenManager.defaultTokenManager upsertAccountsByDict:@{ @(0): userID?:@"" }];
}
```
3. **로그아웃 시 계정 바인딩 해제**. IM SDK에서 로그아웃한 후 다음 메소드를 호출하여 TPNS 푸시 계정의 바인딩을 해제해야 로그아웃 후에도 푸시 메시지가 수신되는 문제를 방지할 수 있습니다.
```
- (void)push_unregisterIfLogouted
{
    // 계정 바인딩 해제
    [XGPushTokenManager.defaultTokenManager delAccountsByKeys:[NSSet setWithObject:@(0)]];
    NSLog(@"[PUSH][TPNS] %s", __func__);
}
```
4. **메시지 전송 시 오프라인 푸시 매개변수 설정**.
[sendMessage](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a3694cd507a21c7cfdf7dfafdb0959e56)를 호출하여 메시지를 보낼 때 [V2TIMOfflinePushInfo](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMOfflinePushInfo.html)를 통해 오프라인 푸시 매개변수를 설정할 수 있습니다. TUIKitDemo의 [TUIMessageDataProvider](https://github.com/tencentyun/TIMSDK/blob/master/iOS/TUIKit/TUIChat/DataProvider/TUIMessageDataProvider.m)의 `+ sendMessage:toConversation:isSendPushInfo:isOnlineUserOnly:priority:Progress:SuccBlock:FailBlock:` 메소드를 참고하십시오.
```java
    NSString *userID = conversationData.userID;
    NSString *groupID = conversationData.groupID;
    NSAssert(userID || groupID, @"타깃 세션에 최소 1개 필요");
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
        // Android oppo 필드와 호환되며 여기의 설정은 무시할 수 있습니다.
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
5. **오프라인 푸시 메시지 리졸브**.
TPNS에 액세스 후 TPNS의 콜백 `- xgPushDidReceiveNotificationResponse:withCompletionHandler:`  에서 알림 표시줄 클릭을 수신할 수 있습니다. [4단계](#step4)에서  [V2TIMOfflinePushInfo](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMOfflinePushInfo.html)를 통해 설정한 오프라인 푸시 형식에 따라 리졸브 및 리디렉션합니다. TUIKitDemo의 오프라인 푸시 메시지에 대한 리졸브 코드를 참고하십시오.
```
 /// 통합 클릭 콜백
/// @param response 만약 iOS 10+/macOS 10.14+ 이면 UNNotificationResponse, 타깃 버전보다 낮으면 NSDictionary
- (void)xgPushDidReceiveNotificationResponse:(nonnull id)response withCompletionHandler:(nonnull void (^)(void))completionHandler {
    /// code
    NSDictionary *custom = nil;
    if (@available(iOS 10.0, *)) {
        /// iOS10+ 메시지 내용 가져오기
        if ([response isKindOfClass:UNNotificationResponse.class]) {
            NSDictionary *userInfo = ((UNNotificationResponse *)response).notification.request.content.userInfo;
            if ([userInfo.allKeys containsObject:@"custom"]) {
                NSString *customStr = userInfo[@"custom"];
                custom = [TCUtil jsonSring2Dictionary:customStr];
            }
        }
    } else {
        /// <IOS10 메시지 내용 가져오기
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
    
    // 구체적인 메시지 내용 응답
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
    // 업무,   action : 1 일반 텍스트 푸시. 2 음성 및 영상 통화 푸시
    // 채팅 유형, chatType : 1 1:1 채팅. 2 그룹 채팅
    NSString *action = entity[@"action"];
    NSString *chatType = entity[@"chatType"];
    if (action == nil || chatType == nil) {
        return;
    }

    // action : 1 일반 메시지 푸시
    if ([action intValue] == APNs_Business_NormalMsg) {
        if ([chatType intValue] == 1) {   //C2C
            self.userID = entity[@"sender"];
        } else if ([chatType intValue] == 2) { //Group
            self.groupID = entity[@"sender"];
        }
        if ([[V2TIMManager sharedInstance] getLoginStatus] == V2TIM_STATUS_LOGINED) {
            
            // 일반 오프라인 메시지에 대한 응답으로 해당 채팅 페이지로 리디렉션할 수 있습니다.
            ...
        }
    }
    // action : 2 음성 및 영상 통화 푸시
    else if ([action intValue] == APNs_Business_Call) {
        // 1:1 채팅에서 멀티미디어 초대 푸시는 처리할 필요가 없으며 APP 실행 후 TUIkit에서 자동으로 처리합니다.
        if ([chatType intValue] == 1) {   //C2C
            return;
        }
        // 콘텐츠
        NSDictionary *content = [TCUtil jsonSring2Dictionary:entity[@"content"]];
        if (!content) {
            return;
        }
        UInt64 sendTime = [entity[@"sendTime"] integerValue];
        uint32_t timeout = [content[@"timeout"] intValue];
        UInt64 curTime = [[V2TIMManager sharedInstance] getServerTime];
        if (curTime - sendTime > timeout) {
            [TUITool makeToast:@"전화 수신 시간 초과"];
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
            // 그룹 호출의 오프라인 메시지에 대한 응답으로 그룹 호출 인터페이스를 직접 열 수 있습니다.
            ...
        }
    }
}


```



## FAQ

### 일반 메시지 오프라인 푸시를 수신할 수 없는 이유는 무엇입니까?

우선 App 실행 환경과 인증서 환경이 일치하는지 확인합니다. 일치하지 않으면 오프라인 푸시을 받을 수 없습니다.

### 사용자 정의 메시지 오프라인 푸시 알림을 받을 수 없는 이유는 무엇입니까?

사용자 정의 메시지의 오프라인 푸시는 일반 메시지와 다릅니다. 사용자 정의 메시지 내용을 리졸브할 수 없고 푸시 내용을 확인할 수 없으므로 기본적으로 푸시되지 않습니다. 푸시하려면 [sendMessage](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a3694cd507a21c7cfdf7dfafdb0959e56) 시 [offlinePushInfo](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMOfflinePushInfo.html)의 `desc` 필드를 설정해야 하며 푸시 시 기본적으로 `desc` 정보가 표시됩니다.

### 오프라인 푸시 메시지 수신을 비활성화하는 방법은 무엇입니까?

오프라인 푸시 메시지 수신을 비활성화하려면, [setAPNS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07APNS_08.html#a6aecbdc0edaa311c3e4e0ed3e71495b1) 인터페이스의 'config' 매개변수를 'nil'로 설정하면 됩니다. 이 기능은 버전 5.6.1200부터 지원됩니다.

### 푸시된 읽지 않음 표시 Badge가 올바르지 않은 이유는 무엇입니까?
TPNS 푸시를 통합한 후 TPNS 오프라인 푸시 Badge를 설정해야 합니다. [AppDelegate+TPNS](https://github.com/tencentyun/TIMSDK/blob/master/iOS/Demo/TUIKitDemo/AppDelegate+TPNS.m)의 `-onTPNSBadgeChanged:` 메소드를 참고하여 로컬 아이콘을 TPNS에 설정할 수 있습니다.






