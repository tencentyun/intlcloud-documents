## Displaying the Conversation List
After logging in to the app, you can display a list of recent conversions like WeChat. The entire display process includes the following steps: **pulling the conversation list**, **processing the change notifications**, and **updating the UI content (including the unread count)**. This document describes these steps in detail.


### Pulling the conversation list
After logging in to the app, you can call [getConversationList()](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Conversation_08.html#af94d9d44e90da448a395e6d92b4e512e) to pull the local conversation list and display the list on the UI. The conversation list is a list of [V2TIMConversation](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMConversation.html) objects, and every object represents a conversation.

The number of local conversations may be large, for example, more than 500. It may take a long time to load all conversations at a time, which results in slow display of the list on the UI. To improve user experience, the `getConversationList()` API is provided to support the feature of pulling by page.
1. When the `getConversationList()` API is called for the first time, you can set the `nextSeq` parameter to 0, indicating that the conversation list is pulled from the beginning, and set `count` to 50, indicating that 50 conversation objects are pulled at a time.
2. The IM SDK pulls the conversation list in the new-to-old order. After the conversation list is pulled successfully for the first time, [V2TIMConversationResult](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Conversation_08.html#a7ff14d2973291fdac42592bfc57369f5), which is the callback result of `getConversationList()`, will contain the `nextSeq` field for the next pulling by page and the `isFinish` field that indicates whether the conversation pulling is completed.
 - If the returned value of `isFinished` is `true`, all conversations have been pulled.
 - If the returned value of `isFinished` is `false`, more conversations can be pulled. This does not mean that the next page of the conversation list will be pulled immediately. In common communications software, pulling by page is often triggered by the swipe operation of the user. Each time when you swipe on the conversation list, pulling by page is triggered once.
[](id:get_step3)
3. When you continue to swipe on the conversation list, if more content of the conversation list is yet to be pulled, the IM SDK can continue to call the [getConversationList()](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Conversation_08.html#afbf2764146025df3c2202058026fda77) API and pass in the `nextSeq` and `count` parameters again. The values of the two parameters come from the [V2TIMConversationResult](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Conversation_08.html#a7ff14d2973291fdac42592bfc57369f5) object returned in the previous pulling.
5. The IM SDK repeats [step 3](#get_step3) until the returned value of `isFinished` is `true`.

### Displaying the conversation information
After obtaining the [V2TIMConversation](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMConversation.html) object, the IM SDK can display the conversation information on the UI. `V2TIMConversation` contains the following key fields, which are often used to construct the conversation list.

| Field | Description |
|---------|---------|
| [showName](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMConversation.html#a2b76165dc084dda2e7779c1e2cf4be1b) | The conversion name:<ul><li>For the one-to-one chat, the API preferentially returns the friend’s remark. If the remark is unavailable or if the peer is not a friend, the API returns the nickname of the peer. If the nickname is also unavailable, the API returns the UserID of the peer.</li><li>For a group chat, the group name is displayed.</li></ul> |
| [faceUrl](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMConversation.html#aae280a300859e7d01cb7f94bb5d40fbd) | The profile photo for the conversation: <ul><li>For a one-to-one chat, the other party's profile photo is displayed. </li><li>For a group chat, the group's profile photo is displayed.</li></ul> |
| [unreadCount](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMConversation.html#a816b83eb32d84ea5345f14ced92bb7f6) | The unread count, which indicates the number of unread messages. |
| [recvOpt](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMConversation.html#a851651878491c64d73aa83131134e6cc) | The message receiving option, which is generally used for a group conversation. It indicates whether the **Mute Notifications** mode is enabled for the group. |
| [lastMessage](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMConversation.html#a63f0969319d4f1638e395bb2a781587b) | The last message, which displays the message digest of the conversation. |
|[groupAtInfolist](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMConversation.html#a5659c29a54304e89e61c25c2b073f8da)| The @ information of the conversation, which shows "someone @ me", "@ all members", etc. |
|[isPinned](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMConversation.html#a5659c29a54304e89e61c25c2b073f8da)| Whether the conversation is pinned on top. This is only available in the lite edition. |

### Updating the conversation list

After the IM SDK is successfully logged in, or the user goes online, or the connection is re-established after being interrupted, the IM SDK will automatically update the conversation list. The update process is as follows:
- When any conversation is updated, for example, when a new message is received, the SDK will notify you by using the [onConversationChanged](https://im.sdk.qcloud.com/doc/en/protocolV2TIMConversationListener-p.html#a371039feea8aa04047bd3ebcf8d12931) event in `V2TIMConversationListener`.
- When any conversation is added, the SDK will notify you by using the [onNewConversation](https://im.sdk.qcloud.com/doc/en/protocolV2TIMConversationListener-p.html#a33ddb9c261e10426b0e257be93e5fc19) event in `V2TIMConversationListener`.

>!To ensure that the order of the conversation list complies with the sequencing principle specified in the last message, the data source must be re-sequenced based on [timestamp](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMMessage.html#ae250d327c18ffaff77fa22fec3119e0f) in [lastMessage](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMConversation.html#a63f0969319d4f1638e395bb2a781587b).

### Sample code
The sample code shows how to pull, display, and update the conversation list.

```
// 1. Set the conversation listener.
[[V2TIMManager sharedInstance] setConversationListener:self];
// 2. Log in to the IM SDK.
[[V2TIMManager sharedInstance] login:@"yahaha" userSig:@"Pass in the actual UserSig" succ:^{
    // 3. Pull 50 local conversation to display them on the UI. Set the value of `nextSeq` that is passed in for the first pulling to 0.
    __weak __typeof(self) weakSelf = self;
    [[V2TIMManager sharedInstance] getConversationList:0 count:50
        succ:^(NSArray<V2TIMConversation *> *list, uint64_t nextSeq, BOOL isFinished) {
        __strong __typeof(weakSelf) strongSelf = weakSelf;
        // Pulling is successful, and the UI conversation list is updated.
        [strongSelf updateConversation:list];
        // 4. If more conversations need to be pulled, the value of `nextSeq` returned in the previous pulling will be passed in.
        if(!isFinished) {
            [[V2TIMManager sharedInstance] getConversationList:nextSeq count:50
                        succ:^(NSArray<V2TIMConversation *> *list, uint64_t nextSeq, BOOL isFinished) {
                // Pulling is successful, and the UI conversation list is updated.
                [strongSelf updateConversation:list];
            } fail:^(int code, NSString *msg) {
                // The attempt to pull the conversation list fails.
            }];
        }
    } fail:^(int code, NSString *msg) {
        // The attempt to pull the conversation list fails.
    }];
} fail:^(int code, NSString *msg) {
    // Logn fails.
}];

// Receive the callback for adding a conversation.
- (void)onNewConversation:(NSArray<V2TIMConversation*> *) conversationList {
    [self updateConversation:conversationList];
}

// Receive the callback for updating the conversation.
- (void)onConversationChanged:(NSArray<V2TIMConversation*> *) conversationList {
    [self updateConversation:conversationList];
}

// Update the UI conversation list.
- (void)updateConversation:(NSArray *)convList
{
    // If the updated conversation exists in the UI conversation list, replace this conversation. Otherwise, add this conversation.
    for (int i = 0 ; i < convList.count ; ++ i) {
        V2TIMConversation *conv = convList[i];
        BOOL isExit = NO;
        for (int j = 0; j < self.uiConvList.count; ++ j) {
            V2TIMConversation *uiConv = self.localConvList[j];
            // If the updated conversation exists in the UI conversation list, replace this conversation.
            if ([uiConv.conversationID isEqualToString:conv.conversationID]) {
                [self.uiConvList replaceObjectAtIndex:j withObject:conv];
                isExit = YES;
                break;
            }
        }
        // If the updated conversation does not exist in the UI conversation list, add this conversation.
        if (!isExit) {
            [self.uiConvList addObject:conv];
        }
    }
    // Sort the UI conversation list based on the timestamp in the lastMessage of the conversation.
    [self.uiConvList sortUsingComparator:^NSComparisonResult(V2TIMConversation *obj1, V2TIMConversation *obj2) {
        return [obj2.lastMessage.timestamp compare:obj1.lastMessage.timestamp];
    }];
}

```

## Obtaining the Total Unread Message Count of All Conversations (Only Available in Lite Edition v5.3.425 and Above)
You can call the [getTotalUnreadMessageCount](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Conversation_08.html#a8459f8be316e10808fd3aa39a1ebc3f5) API to get the total unread count of all conversations. You don't need to go through the conversation list and add up the unread count of each conversation to get the total unread count. When the total unread count changes, the SDK will proactively call back [onTotalUnreadMessageCountChanged](https://im.sdk.qcloud.com/doc/en/protocolV2TIMConversationListener-p.html#ab254716e0edb04a0192fb56d27b611e4) to your app to notify you of the latest unread count.

## Pinning a Conversation on Top (Only Available in Lite Edition v5.3.425 and Above)
You can pin a one-to-one or group conversation on the top of the conversation list so you can quickly find it. The new SDK version has added the [pinConversation](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Conversation_08.html#adc50026943585a0aa37ac8856b6b43bb) API to pin/unpin conversations to/from top. It also supports roaming and multi-client synchronization.
The [V2TIMConversation](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMConversation.html) conversation object has added the [isPinned](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMConversation.html#aa3c3bc1113ce3052493288abecc45222) API, which is used to determine whether a conversation is pinned on top. When the pinned-on-top status of a conversation changes, the SDK will call back [onConversationChanged](https://im.sdk.qcloud.com/doc/en/protocolV2TIMConversationListener-p.html#a371039feea8aa04047bd3ebcf8d12931) to your app.

## Deleting a Conversation
You can call the [deleteConversation](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Conversation_08.html#a42238db95428faae2da25a093569fda0) API to delete a conversation. Conversation deletion cannot be synchronized across multiple clients. When a conversation is deleted, the message history of this conversation will be deleted from the local storage and the server by default, and cannot be recovered.

## Drafts
When sending a message, you may need to switch to another chat window before message editing is completed. In this case, you can call the [setConversationDraft](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Conversation_08.html#ade2830b5c35df27a4b8fea44408a07a0) API to save the unfinished message. Later, you can return to the original chat window and call [draftText](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMConversation.html#a6b2c25f269b30a487761b305f069952f) to continue editing the message.

>!
>- Only text content can be stored in Drafts.
>- Drafts are stored only locally, instead of on the server. Therefore, drafts cannot be synchronized across multiple devices. If the program is uninstalled, drafts cannot be reloaded.

## FAQs
### 1. What is the upper limit for the number of conversations that can be stored in a conversation list?
A locally stored conversation list can have unlimited number of conversations. A conversation list stored in the cloud can have up to 100 conversations.
If the information of a conversation has not been updated for a long time, this conversation can be stored in the cloud for at most 7 days. To adjust the period for storing the conversation, [contact us](https://console.cloud.tencent.com/workorder/category).

### 2. Why are the conversation lists pulled on different mobile phones by using the same account inconsistent?
Locally stored conversations may not always be consistent with those stored in the cloud. If you do not call the [deleteConversation](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Conversation_08.html#a42238db95428faae2da25a093569fda0) API to delete the local conversations, these conversations will always exist. However, at most 100 conversations can be stored in the cloud. In addition, if the information of a conversation has not been updated for a long time, this conversation can be stored in the cloud for at most 7 days. Therefore, local conversations displayed on different mobile phones may be inconsistent with each other.


### 3. Why are repeated conversations pulled?
Conversations that are pulled by the `getConversationList` API may have already been added to the data source of the UI conversation list through the `onNewConversation` callback API. Therefore, to avoid adding the same conversation repeatedly, you need to find and replace the same conversations based on [getConversationID](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMConversation.html#a89d34fa0d0d62e831c27ae2a75a37fac).

### 4. Does the IM SDK support the feature of pinning a conversation to the top?
IM SDK supports pinning a conversation to the top and sync to the cloud starting from v5.3.425.

