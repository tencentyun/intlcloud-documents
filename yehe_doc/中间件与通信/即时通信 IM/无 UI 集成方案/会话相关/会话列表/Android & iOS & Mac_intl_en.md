## Feature Description
After a user logs in to the application, the list of recent conversations can be displayed to make it easy to locate the target conversation.
The conversation list is as follows:
<img src="https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/res/RPReplay_Final0511.gif" alt="" style="zoom:40%;" />

The conversation list features include getting the conversation list and processing the conversation list update.
This document describes how to implement such features.

## Ordinary API for Getting the Conversation List
You can call `getConversationList` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#a1bb5ba2beecb4f68146e7f664124fd8b) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Conversation_08.html#af94d9d44e90da448a395e6d92b4e512e)) to get the conversation list. This API pulls locally cached conversations. If any server conversation is updated, the SDK will automatically sync the update and notify you in the `V2TIMConversationListener` callback.

User conversations are returned in a list that stores `V2TIMConversation` objects. Currently, the IM SDK sorts conversations according to the following rules:
* Starting from v5.5.892, the obtained conversations are sorted based on the `orderKey` conversation object by default. The greater the `orderKey` value of a conversation, the higher position the conversation is in the list. The `orderKey` field is an integer that increases as the conversation is activated when a message is sent/received, a draft is set, or the conversation is pinned to the top.
* On versions earlier than v5.5.892, the obtained conversations are sorted based on the `lastMessage` > `timestamp` of the conversation by default. The greater the `timestamp` value, the higher position the conversation is in the list.

> ! In certain cases, the `lastMessage` of a conversation may be empty, such as when the messages in the conversation are cleared. If you use the SDK earlier than v5.5.892, you need to handle the exception when sorting the conversations by `lastMessage`. We recommend you upgrade the SDK to v5.5.892 or later and sort the conversations by `orderKey`.

You can use `getConversationList` to implement one-time or paged pull as detailed below.

### One-time pull
One-time pull is suitable for scenarios with a small number of conversations (up to 100). You can set the `count` of the pull to `INT_MAX` (which is generally greater than the number of conversations).

Sample code:
<dx-tabs>
::: Android
```java
V2TIMManager.getConversationManager().getConversationList(0, Integer.MAX_VALUE, new V2TIMValueCallback<V2TIMConversationResult>() {
    @Override
    public void onSuccess(V2TIMConversationResult v2TIMConversationResult) {
        long nextSeq = v2TIMConversationResult.getNextSeq();
        Log.i("imsdk", "success nextSeq:" + nextSeq + ", isFinish:" + v2TIMConversationResult.isFinished());

        List<V2TIMConversation> v2TIMConversationList = v2TIMConversationResult.getConversationList();
        for (V2TIMConversation v2TIMConversation : v2TIMConversationList) {
            Log.i("imsdk", "success showName:" + v2TIMConversation.getShowName());
        }
    }

    @Override
    public void onError(int code, String desc) {
        Log.i("imsdk", "failure, code:" + code + ", desc:" + desc);
    }
});
```
:::
::: iOS and macOS
```objectivec
[[V2TIMManager sharedInstance] getConversationList:0
                                             count:INT_MAX
                                              succ:^(NSArray<V2TIMConversation *> *list, uint64_t lastTS, BOOL isFinished) {
    // Obtained the conversation list successfully. `list` is the conversation list.
} fail:^(int code, NSString *msg) {
    // Failed to obtain the conversation list
}];
```
:::
</dx-tabs>

### Pulling by page
If the number of conversations is high, pulling by page is recommended to enhance the loading efficiency and save network traffic. The recommended number of conversations pulled per page is up to 100.

Directions:
1. When you call `getConversationList` for the first time, set `nextSeq` to `0` (indicating to pull the conversation list from the beginning) and `count` to `50` (indicating to pull 50 conversation objects at a time).
   
2. After the conversation list is pulled successfully for the first time, the `V2TIMConversationResult` callback of `getConversationList` will contain `nextSeq` (field for the next pull) and `isFinish` (indicating whether the conversation pull is completed).
   * If `isFinished` is `true`, all the conversations have been pulled.
   * If `isFinished` is `false`, there are more conversations that can be pulled. This does not mean that the next page of the conversation list will be pulled immediately. In common software, a paged pull is often triggered by a swipe operation.

3. When the user continues to pull up the conversation list, if there are more conversations that can be pulled, you can continue to call the `getConversationList` API and pass in the `nextSeq` (the value is from the `V2TIMConversationResult` object returned by the last pull) and `count` parameters for the next pull.

4. Repeat step 3 until `isFinished` is `true`.

Sample code:
<dx-tabs>
::: Android
```java
V2TIMManager.getConversationManager().getConversationList(0, 20, new V2TIMValueCallback<V2TIMConversationResult>() {
    @Override
    public void onSuccess(V2TIMConversationResult v2TIMConversationResult) {
        long nextSeq = v2TIMConversationResult.getNextSeq();
        Log.i("imsdk", "success nextSeq:" + nextSeq + ", isFinish:" + v2TIMConversationResult.isFinished());

        List<V2TIMConversation> v2TIMConversationList = v2TIMConversationResult.getConversationList();
        for (V2TIMConversation v2TIMConversation : v2TIMConversationList) {
            Log.i("imsdk", "success showName:" + v2TIMConversation.getShowName());
        }

        if (!v2TIMConversationResult.isFinished()) {
            getConversationListInternal(nextSeq, 20);
        }
    }

    @Override
    public void onError(int code, String desc) {
        Log.i("imsdk", "failure, code:" + code + ", desc:" + desc);
    }
});
```
:::
::: iOS and macOS
```objectivec
// It will be triggered when the user pulls up the conversation list to the bottom and no more conversation data is displayed.
- (void)loadConversation {
    if (self.isFinished) {
        return;
    }
    @weakify(self)
    [[V2TIMManager sharedInstance] getConversationList:self.nextSeq 
                                                 count:20 // Pull 20 conversations each time 
                                                  succ:^(NSArray<V2TIMConversation *> *list, uint64_t nextSeq, BOOL isFinished) {
        // Conversations pulled successfully
        @strongify(self)
        // Update the `nextSeq` and `isFinished` for the next pull
        self.nextSeq = nextSeq;
        self.isFinished = isFinished;

        // Update the UI with the `list`
    } fail:^(int code, NSString *msg) {
        // Failed to pull the conversations; in this case, end the pull.
        self.isFinished = YES;
    }];
}
```
:::
</dx-tabs>

## Advanced API for Getting the Conversation List
If the ordinary API mentioned above cannot meet your needs to pull the conversation list, you can use the advanced API `getConversationListByFilter` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#abf71156b8b6423e98943e25a77dc1967) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Conversation_08.html#ac1b77eedff7f2f8742a873cf766daec9)). Here, `V2TIMConversationListFilter` of the conversations is pulled and as detailed below:

| Attribute | Definition | Description |
| --- |  --- | --- |
| type | Conversation type | One-to-one or group conversation |
| nextSeq | Cursor for the paged pull | Pass in `0` for the first pull and the `nextSeq` returned by the previous pull for the subsequent pull. |
| count | Number of conversations to be pulled per page | Up to 100 conversations per page are recommended. |
| markType | Conversation tag type | For more information, see [Conversation Tag](https://intl.cloud.tencent.com/document/product/1047/48853). |
| groupName | Conversation group name | It is not the group name but the conversation group name. For more information, see [Conversation Group](https://intl.cloud.tencent.com/document/product/1047/48854). |

Sample code:
<dx-tabs>
::: Android
```java
V2TIMConversationListFilter filter = new V2TIMConversationListFilter();
filter.setConversationType(V2TIMConversation.V2TIM_C2C);
filter.setMarkType(V2TIMConversation.V2TIM_CONVERSATION_MARK_TYPE_STAR);
filter.setGroupName("conversation_group");
filter.setCount(50);
filter.setNextSeq(0);
V2TIMManager.getConversationManager().getConversationListByFilter(filter, new V2TIMValueCallback<V2TIMConversationResult>() {
    @Override
    public void onSuccess(V2TIMConversationResult v2TIMConversationResult) {
        // Conversation list obtained successfully
    }

    @Override
    public void onError(int code, String desc) {
        // Failed to obtain the conversation list
    }
});
```
:::
::: iOS and macOS
```objectivec
V2TIMConversationListFilter *filter = [[V2TIMConversationListFilter alloc] init];
filter.type = V2TIM_C2C;
filter.markType = V2TIM_CONVERSATION_MARK_TYPE_STAR;
filter.groupName = @"conversation_group";
filter.count = 50;
filter.nextSeq = 0;
[[V2TIMManager sharedInstance] getConversationListByFilter:filter succ:^(NSArray<V2TIMConversation *> *list, uint64_t nextSeq, BOOL isFinished) {
   // Conversation list obtained successfully. `list` is the conversation list.
} fail:^(int code, NSString *desc) {
   // Failed to obtain the conversation list
}];
```
:::
</dx-tabs>

## Updating the Conversation List
After the IM SDK is logged in successfully, the user goes online, or the network is disconnected and reconnected, the IM SDK will automatically update the conversation list.
You can get the updated conversation list in the following steps:
1. Add a conversation listener.
2. Receive and process conversation changes.
3. Remove the conversation listener. This step is optional and can be performed as needed.

### Adding a conversation listener
Call `addConversationListener` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#a806534684e5d4d01b94126cd1397fee4) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Conversation_08.html#a39b4f352f1740171fb56143149201cd9)) to add a conversation listener to receive conversation change events.

Sample code:
<dx-tabs>
::: Android
```java
V2TIMManager.getConversationManager().addConversationListener(conversationListener);
```
:::
::: iOS and macOS
```objectivec
// `self` is of the id<V2TIMConversationListener> type.
[[V2TIMManager sharedInstance] addConversationListener:self];
```
:::
</dx-tabs>

### Getting the notification of a conversation change
You can listen for the event in `V2TIMConversationListener` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationListener.html) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/protocolV2TIMConversationListener-p.html)) to get the notification of a conversation list change.

Currently, the IM SDK supports the following conversation change events:

| Event                             | Description                 | Suggestion                                                                                                                         |
| --- | --- | --- |
|onSyncServerStart | Server conversation sync started.  | Listen for such an event when the user logged in successfully or went online or the network was disconnected and reconnected and display the progress on the UI.                                 |
| onSyncServerFinish               | Server conversation sync was completed.   | Notify a conversation change through the `onNewConversation`/`onConversationChanged` callback.                                                |
|onSyncServerFailed | Server conversation sync failed.   | Listen for such an event and display the exception on the UI.                                                                                   |
|onNewConversation | There is a new conversation.           | Re-sort the conversations when the user receives a one-to-one message from a new colleague or is invited to a new group.                                     |
|onConversationChanged | A conversation was updated.           | Re-sort the conversations when the unread count changes or the last message is updated. |
|onTotalUnreadMessageCountChanged | The total unread count of the conversation changed.  | For more information, see [Conversation Unread Count](https://intl.cloud.tencent.com/document/product/1047/48320). This event is supported by v5.3.425 or later. |

> !
> 1. To ensure that the conversations are sorted by the last message, you need to re-sort the data sources each time a conversation is changed/added.
> * If you use the version earlier than v5.5.892, you can sort the conversations by `lastMessage`, but note that sometimes `lastMessage` may be empty (such as when messages in a conversation are cleared).
> * If you use the SDK on v5.5.892 or later, you can sort the conversations by `orderKey`. Therefore, we recommend you upgrade the SDK to v5.5.892 or later.
> 2. Conversations pulled by calling the `getConversationList` API may have been added to the data source of the conversation list on the UI through the `onNewConversation` callback API. To avoid adding the same conversation repeatedly, you need to find and replace the same conversation based on `getConversationID` in the data source of the conversation list on the UI.

Sample code:
<dx-tabs>
::: Android
```java
// Listen for the conversation callback

V2TIMConversationListener conversationListener = new V2TIMConversationListener() {
    @Override
    public void onSyncServerStart() {
        Log.i("imsdk", "onSyncServerStart");
    }

    @Override
    public void onSyncServerFinish() {
        Log.i("imsdk", "onSyncServerFinish");
    }

    @Override
    public void onSyncServerFailed() {
        Log.i("imsdk", "onSyncServerFailed");
    }

    @Override
    public void onNewConversation(List<V2TIMConversation> conversationList) {
        Log.i("imsdk", "onNewConversation");
    }

    @Override
    public void onConversationChanged(List<V2TIMConversation> conversationList) {
        Log.i("imsdk", "onConversationChanged");
    }

    @Override
    public void onTotalUnreadMessageCountChanged(long totalUnreadCount) {
        Log.i("imsdk", "onTotalUnreadMessageCountChanged");
    }
};
```
:::
::: iOS and macOS
```objectivec
- (void)onSyncServerStart {
    // Server conversation sync started.
}

- (void)onSyncServerFinish {
    // Server conversation sync was completed.
}

- (void)onSyncServerFailed {
    // Server conversation sync failed.
}

- (void)onNewConversation:(NSArray<V2TIMConversation*> *)conversationList {
    // Received the notification of a new conversation. `conversationList` is the new conversation.
    [self updateConversation:conversationList];
}

- (void)onConversationChanged:(NSArray<V2TIMConversation*> *)conversationList {
    // Received the notification of a conversation change. `conversationList` is the changed conversation object.
    [self updateConversation:conversationList];
}

- (void)updateConversation:(NSArray *)convList {
    // Update the conversation list on the UI. If the new/changed conversation already exists in the conversation list on the UI, replace the existing conversation with that new/changed conversation; otherwise, add a conversation object.
    for (int i = 0 ; i < convList.count ; ++ i) {
        V2TIMConversation *conv = convList[i];
        BOOL isExit = NO;
        for (int j = 0; j < self.localConvList.count; ++ j) {
            V2TIMConversation *localConv = self.localConvList[j];
            if ([localConv.conversationID isEqualToString:conv.conversationID]) {
                // If the updated conversation already exists in the conversation list on the UI, replace the conversation.
                [self.localConvList replaceObjectAtIndex:j withObject:conv];
                isExit = YES;
                break;
            }
        }
        // If the updated conversation does not exist in the conversation list on the UI, add the conversation.
        if (!isExit) {
            [self.localConvList addObject:conv];
        }
    }
    // Re-sort the conversations on the UI
    [self sortDataList:dataList];
    self.dataList = dataList;
}

```
:::
</dx-tabs>

### Removing a conversation listener
Call `removeConversationListener` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#a661d479b6f704a2e319d0c744b8ad2bc) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Conversation_08.html#ab9e1627559fb4259228b4e547b192c83)) to remove a conversation listener to stop receiving conversation change events.
This step is optional and can be performed as needed.

Sample code:
<dx-tabs>
::: Android
```java
V2TIMManager.getConversationManager().removeConversationListener(conversationListener);
```
:::
::: iOS and macOS
```objectivec
// `self` is of the id<V2TIMConversationListener> type.
[[V2TIMManager sharedInstance] removeConversationListener:self];
```
:::
</dx-tabs>

[](id:isExcludedFromLastMessage)
### Sending a message without updating the lastMessage
On UI of the conversation list, it is usually necessary to display the preview and send time of the latest message in each conversation. In this case, you can use `lastMessage` of `V2TIMConversation` as the data source for implementation.
However, in some cases, if you don't want some messages (such as system tips) to be displayed as the latest message in a conversation, you can set `isExcludedFromLastMessage` to `false`/`NO` when calling `sendMessage`.

For directions on how to send a message by calling `sendMessage`, see [Sending Message](https://intl.cloud.tencent.com/document/product/1047/47994).

>? The `isExcludedFromLastMessage` parameter is supported only by the SDK of the Enhanced edition on v5.4.666 or later.

Sample code:
<dx-tabs>
::: Android
```java
// Create a message object
V2TIMMessage v2TIMMessage = V2TIMManager.getMessageManager().createTextMessage(content);
// Set not to update the `lastMessage` of the conversation
v2TIMMessage.setExcludedFromLastMessage(true);

// Send the message
V2TIMManager.getMessageManager().sendMessage(v2TIMMessage, "userID", null, V2TIMMessage.V2TIM_PRIORITY_DEFAULT, false, null, new V2TIMSendCallback<V2TIMMessage>() {
    @Override
    public void onSuccess(V2TIMMessage v2TIMMessage) {
        Log.i("imsdk", "success");
    }

    @Override
    public void onProgress(int progress) {
        Log.i("imsdk", "progress:" + progress);
    }

    @Override
    public void onError(int code, String desc) {
        Log.i("imsdk", "failure, code:" + code + ", desc:" + desc);
    }
});
```
:::
::: iOS and macOS
```objectivec
// Create a message object
V2TIMMessage *message = [V2TIMManager.sharedInstance createTextMessage:content];
// Set not to update the `lastMessage` of the conversation
message.isExcludedFromLastMessage = YES;
// Send the message
[V2TIMManager.sharedInstance sendMessage:message 
                                receiver:@"userA" 
                                 groupID:nil 
                                priority:V2TIM_PRIORITY_NORMAL 
                          onlineUserOnly:NO 
                         offlinePushInfo:nil 
                                progress:^(uint32_t progress) {
    // Sending progress
} succ:^{
    // Message sent successfully
} fail:^(int code, NSString *desc) {
    // Failed to send the message
}];
```
:::
</dx-tabs>

