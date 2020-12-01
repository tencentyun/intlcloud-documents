## Displaying the Conversation List
After the user logs in to the app, the app can display a list of recent conversions like WeChat. The overall display process includes the following steps: **pulling the conversation list**, **processing the change notifications**, and **updating the UI content (including the unread count)**. This document describes these steps in detail.


### Pulling the conversation list
After logging in to the app, you can call [getConversationList()](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Conversation_08.html#af94d9d44e90da448a395e6d92b4e512e) to pull the local conversation list and display the list on the UI. The conversation list is a list of [V2TIMConversation][V2TIMConversation](http://doc.qcloudtrtc.com/im/interfaceV2TIMConversation.html) objects, and every object represents a conversation.

The number of local conversations may be large, even more than 500. Therefore, it may take a long time to load all conversations at once, which results in the slow display of the list on the UI. To improve the user experience, we provide the `getConversationList()` API to support pulling by page.
1. When the `getConversationList()` API is called for the first time, you can set the `nextSeq` parameter to 0, indicating that the conversation list is pulled from the beginning, and set `count` to 50, indicating that 50 conversation objects are pulled at a time.
2. The IM SDK pulls the conversation list in reverse chronological order. After the conversation list is pulled successfully for the first time, [V2TIMConversationResult](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Conversation_08.html#a7ff14d2973291fdac42592bfc57369f5), which is the callback result of `getConversationList()`, will contain the `nextSeq` field for the next pulling by page operation and the `isFinish` field that indicates whether all conversation objects have been pulled.
 - If the returned value of `isFinished` is `true`, all conversations have been pulled.
 - If the returned value of `isFinished` is `false`, more conversations can be pulled. This does not mean that the next page of the conversation list will be pulled immediately. In common communications software, pulling by page is often triggered when the user swipes. Each time the user swipes on the conversation list, pulling by page is triggered once.
<span id="get_step3"></span>
3. If the user continues to pull down the conversation list and the conversation list has content yet to be pulled, the SDK continues to call the [getConversationList()](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Conversation_08.html#af94d9d44e90da448a395e6d92b4e512e) API and passes in the `nextSeq` and `count` parameters again. The values of the two parameters come from the [V2TIMConversationResult](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Conversation_08.html#a7ff14d2973291fdac42592bfc57369f5) object returned in the previous pull.
4. The IM SDK repeats [step 3](#get_step3) until the returned value of `isFinished` is `true`.

### Displaying the conversation information
After obtaining the [V2TIMConversation](http://doc.qcloudtrtc.com/im/interfaceV2TIMConversation.html) object, the IM SDK displays the conversation information on the UI. `V2TIMConversation` contains the following key fields, which are often used to construct the conversation list.

| Field | Description |
|---------|---------|
| [showName](http://doc.qcloudtrtc.com/im/interfaceV2TIMConversation.html#a2b76165dc084dda2e7779c1e2cf4be1b) | The conversion name:<ul><li>For a one-to-one chat, the API preferentially returns the friend’s remark. If the remark is unavailable or if the other party is not a friend, the API returns the nickname of the other party. If the nickname is also unavailable, the API returns the UserID of the other party.</li><li>For a group chat, the group name is displayed.</li></ul> |
| [faceUrl](http://doc.qcloudtrtc.com/im/interfaceV2TIMConversation.html#aae280a300859e7d01cb7f94bb5d40fbd) | The profile photo for the conversation: <ul><li>For a one-to-one chat, the other party’s profile photo is displayed.</li><li>For a group chat, the group's profile photo is displayed.</li></ul> |
| [recvOpt](http://doc.qcloudtrtc.com/im/interfaceV2TIMConversation.html#ae40fd527e110178e73b34fe72fcfd778) | The message receiving option, which is generally used for a group conversation. It indicates whether the **Do Not Disturb** mode is enabled for the group. |
| [unreadCount](http://doc.qcloudtrtc.com/im/interfaceV2TIMConversation.html#a816b83eb32d84ea5345f14ced92bb7f6) | The unread count, which indicates the number of unread messages. |
| [lastMessage](http://doc.qcloudtrtc.com/im/interfaceV2TIMConversation.html#a63f0969319d4f1638e395bb2a781587b) | The last message, which displays the message digest of the conversation. |

### Updating the conversation list

After login is successful, the user goes online, or the connection is re-established after being interrupted, the IM SDK will automatically update the conversation list. The update process is as follows:
- When any conversation is updated, such as when a new message is received, the SDK will notify you by using the [onConversationChanged](http://doc.qcloudtrtc.com/im/protocolV2TIMConversationListener-p.html#a371039feea8aa04047bd3ebcf8d12931) event in `V2TIMConversationListener`.
- When any conversation is added, the SDK will notify you by using the [onNewConversation](http://doc.qcloudtrtc.com/im/protocolV2TIMConversationListener-p.html#a33ddb9c261e10426b0e257be93e5fc19) event in `V2TIMConversationListener`.

>! To ensure that the order of the conversation list complies with the sequencing principle specified in the last message, the data source must be re-sequenced based on [timestamp](http://doc.qcloudtrtc.com/im/interfaceV2TIMMessage.html#ae250d327c18ffaff77fa22fec3119e0f) in [lastMessage](http://doc.qcloudtrtc.com/im/interfaceV2TIMConversation.html#a63f0969319d4f1638e395bb2a781587b).

### Sample code
The sample code shows how to pull, display, and update the conversation list.

```
// 1. Set the conversation listener.
[[V2TIMManager sharedInstance] setConversationListener:self];
// 2. Log in to the IM SDK.
[[V2TIMManager sharedInstance] login:@"yahaha" userSig:@"Pass in the actual UserSig" succ:^{
    // 3. Pull 50 local conversations to display them on the UI. Set the value of `nextSeq` that is passed in for the first pull to 0.
    __weak __typeof(self) weakSelf = self;
    [[V2TIMManager sharedInstance] getConversationList:0 count:50
        succ:^(NSArray<V2TIMConversation *> *list, uint64_t nextSeq, BOOL isFinished) {
        __strong __typeof(weakSelf) strongSelf = weakSelf;
        // Pulling is successful, and the UI conversation list is updated.
        [strongSelf updateConversation:list];
        // 4. If more conversations need to be pulled, the value of `nextSeq` returned in the previous pull will be passed in.
        if(!isFinished) {
            [[V2TIMManager sharedInstance] getConversationList:nextSeq count:50
                        succ:^(NSArray<V2TIMConversation *> *list, uint64_t nextSeq, BOOL isFinished) {
                // Pulling is successful, and the UI conversation list is updated.
                [strongSelf updateConversation:list];
            } fail:^(int code, NSString *msg) {
                // The conversation list failed to be pulled.
            }];
        }
    } fail:^(int code, NSString *msg) {
        // The conversation list failed to be pulled.
    }];
} fail:^(int code, NSString *msg) {
    // Login fails.
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

## Deleting a Conversation
You can call the [deleteConversation](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Conversation_08.html#a142f5289632f29a603937f1d770748c6) API to delete a conversation. This operation cannot be synchronized across multiple devices. When a conversation is deleted, its local history and messages on the server will also be deleted by default, which are unrecoverable.


## Drafts
When sending a message, the user may need to switch to another chat window before message editing is completed. In this case, call the [setConversationDraft](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Conversation_08.html#a462cd163c03cdce230ed3647b414382b) API to save the unfinished message. Later, the user can return to the original chat window and call [draftText](http://doc.qcloudtrtc.com/im/interfaceV2TIMConversation.html#a6b2c25f269b30a487761b305f069952f) to continue editing the message.

>!
>- Only text content can be stored in drafts.
>- Drafts are stored only locally, instead of on the server. Therefore, drafts cannot be synchronized across multiple devices. If the program is reinstalled, drafts cannot be reloaded.

## FAQs
### 1. What is the maximum number of conversations that can be stored in a conversation list?
A locally stored conversation list can have an unlimited number of conversations. A conversation list stored in the cloud can have up to 100 conversations.
If the information of a conversation has not been updated for a long time, this conversation will be stored in the cloud for up to 7 days. To adjust the period for storing the conversation, [contact us](https://console.cloud.tencent.com/workorder/category).

### 2. Why are the conversation lists pulled on different mobile phones in the same account inconsistent?
Locally stored conversations may not always be consistent with those stored in the cloud. If the user does not call the [deleteConversation](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Conversation_08.html#a142f5289632f29a603937f1d770748c6) API to delete the local conversations, these conversations will always exist. However, only up to 100 conversations can be stored in the cloud. In addition, if the information of a conversation has not been updated for a long time, this conversation can be stored in the cloud for up to 7 days. Therefore, local conversations displayed on different mobile phones may be inconsistent with each other.


### 3. Why is the same conversation pulled multiple times?
Conversations that are pulled by the `getConversationList` API may already have been added to the data source of the UI conversation list through the `onNewConversation` callback API. Therefore, to avoid adding the same conversation repeatedly, you need to find and replace duplicate conversations based on [getConversationID](http://doc.qcloudtrtc.com/im/interfaceV2TIMConversation.html#a89d34fa0d0d62e831c27ae2a75a37fac).

### 4. Does the IM SDK support pinning a conversation to the top of the list?
The IM SDK does not provide the feature of pinning a conversation to the top of the list, but supports re-sequencing of conversations by means of encapsulation. For more information, see the implementation of TUIKit. Such pinning settings take effect only on the local device, and will not be stored on the IM server.

