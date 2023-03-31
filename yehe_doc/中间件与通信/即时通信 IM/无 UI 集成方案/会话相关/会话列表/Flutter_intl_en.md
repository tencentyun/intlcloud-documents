## Overview
After a user logs in to the application, the list of recent conversations can be displayed to make it easy to locate the target conversation.
The conversation list features include getting the conversation list and processing the conversation list update.
This document describes how to implement such features.

### Obtaining the Conversation List
You can call the `getConversationList` API ([details](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMConversationManager/getConversationList.html)) to get the conversation list. This API pulls locally cached conversations. If any server conversation is updated, the SDK will automatically sync the update and notify you in the `V2TIMConversationListener` callback.

User conversations are returned in a list that stores `V2TIMConversation` objects. Currently, the Chat SDK sorts conversations according to the following rules:
* Starting from the SDK for Flutter 3.8.0, the conversations obtained through this API are sorted based on the `orderKey` conversation object by default. The greater the `orderKey` value of a conversation, the higher position the conversation is in the list. The `orderKey` field is an integer that increases as the conversation is activated when a message is sent/received, a draft is set, or the conversation is pinned to the top.
* For Flutter SDK versions earlier than 3.8.0, conversations on the conversion list obtained by this API are sorted by `lastMessage` -> `timestamp` by default. The later the timestamp, the higher the order of the conversation.

> ! In certain cases, the `lastMessage` of a conversation might be empty, such as when the messages in the conversation are cleared. If you use the SDK earlier than v3.8.0, you need to handle the exception when sorting the conversations by `lastMessage`. We recommend you upgrade the SDK to v3.8.0 or later and sort the conversations by `orderKey`.

You can use `getConversationList` to implement one-time or paged pull as detailed below.

### One-time pull
One-time pull is suitable for scenarios with a small number of conversations (up to 100). You can set the `count` of the pull to `INT_MAX` (which is generally greater than the number of conversations).

Sample code:


```dart
V2TimValueCallback<V2TimConversationResult> convList = await TencentImSDKPlugin.v2TIMManager.getConversationManager().getConversationList(nextSeq: '0',count: 100);
```
### Pulling by page
If the number of conversations is great, pulling by page is recommended to enhance the loading efficiency and save network traffic. The recommended number of conversations pulled per page is up to 100.

Directions:
1. When the `getConversationList` API is called for the first time, you can set the `nextSeq` parameter to `0` (pulling the conversation list from the beginning) and set `count` to `50` (pulling 50 conversation objects at a time).
2. After the conversation list is pulled successfully for the first time, the `V2TIMConversationResult` callback of `getConversationList` will contain `nextSeq` (field for the next pull) and `isFinished` (indicating whether the conversation pull is completed).
   * If `isFinished` is `true`, all conversations have been pulled.
   * If `isFinished` is `false`, more conversations can be pulled. This does not mean that the next page of the conversation list will be pulled immediately. In common communications software, pulling by page is often triggered by your swipe operations. Your each swipe on the conversation list triggers the pulling by page once.
3. When the user continues to pull up the conversation list, if there are more conversations that can be pulled, you can continue to call the `getConversationList` API and pass in the `nextSeq` and `count` parameters (the values are from the `V2TIMConversationResult` object returned by the last pull) for the next pull.
4. Repeat **step 3** until `isFinished` is `true`.

Sample code:


```dart
    // Get the conversation list
    V2TimValueCallback<V2TimConversationResult> getConversationListRes =
        await TencentImSDKPlugin.v2TIMManager
            .getConversationManager()
            .getConversationList(
            count: 100, // Number of conversations pulled per page. The value of this field cannot be too large; otherwise, the pulling speed is affected. We recommend that you pull 100 conversations per page.
            nextSeq: "0" // Pulling-by-page cursor. It is set to 0 when the conversation is pulled for the first time. The value of this field in the callback for the current paginated pulling is passed in for the next pull.
            );
    if (getConversationListRes.code == 0) {
      // Pulled successfully
      bool? isFinished = getConversationListRes.data?.isFinished; // Whether the list is fully pulled
      String? nextSeq = getConversationListRes.data?.nextSeq; // Cursor for the subsequent paged pull
      List<V2TimConversation?>? conversationList =
          getConversationListRes.data?.conversationList; // List of conversations pulled this time
      // If more conversations need to be pulled, use the returned `nextSeq` to continue pulling until `isFinished` is `true`.
      if (!isFinished!) {
        V2TimValueCallback<V2TimConversationResult> nextConversationListRes =
            await TencentImSDKPlugin.v2TIMManager
                .getConversationManager()
                .getConversationList(count: 100, nextSeq: nextSeq = "0"); // Use the returned `nextSeq` to continue pulling until `isFinished` is `true`.
      }

      getConversationListRes.data?.conversationList?.forEach((element) {
        element?.conversationID; // Unique conversation ID. It is in the format of `c2c_userID` for a one-to-one chat or `group_groupID` for a group chat.
        element?.draftText; // Draft message
        element?.draftTimestamp; // Draft editing time. It is automatically generated when a draft is set.
        element?.faceUrl; // Displayed conversation profile photo. It is the group profile photo for a group chat or the profile photo of the message receiver for a one-to-one chat.
        element?.groupAtInfoList; // List of @ information in the group conversation. Generally, it is used to display the notifications of "someone@me" and "@all".
        element?.groupID; // ID of the current group. If the conversation type is group chat, `groupID` is the ID of the current group. Otherwise, it is `null`.
        element?.groupType; // Type of the current group. If the conversation type is group chat, `groupType` is the type of the current group. Otherwise, it is `null`.
        element?.isPinned; // Whether the conversation is pinned to the top
        element?.lastMessage; // Last message in the conversation
        element?.orderkey; // Field for sorting conversations
        element?.recvOpt; // Message receiving option
        element?.showName; // Displayed conversation name. The name of a group chat is displayed in the following order of priority: group name > group ID. The name of a one-to-one chat is displayed in the following order of priority: friend remarks of the message receiver > nickname of the message receiver > `userID` of the message receiver.
        element?.type; // Conversation type, which can be `C2C` (one-to-one chat) or `Group` (group chat).
        element?.unreadCount; // Unread message count of the conversation. It is invalid and defaults to `0` for an audio-video group (AVChatRoom).
        element?.userID; // User ID of the message receiver. If the conversation type is one-to-one chat, `userID` is the user ID of the message receiver. Otherwise, it is `null`.
      });
    }
```



## Updating the Conversation List
After the Chat SDK is successfully logged in, or the user goes online, or the connection is re-established after being interrupted, the Chat SDK will automatically update the conversation list.
You can get the updated conversation list in the following steps:
1. Add a conversation listener.
2. Receive and process conversation changes.
3. Remove the conversation listener. This step is optional and can be performed as needed.

### Adding a conversation listener
Call the `addConversationListener` API ([details](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMConversationManager/addConversationListener.html)) to add a conversation listener to receive conversation change events.

Sample code:

```dart
TencentImSDKPlugin.v2TIMManager.getConversationManager().addConversationListener(listener: V2TimConversationListener(onConversationChanged: (conversationList) {
    
  },
	// Others                                                                                                                ));
```


### Getting the notification of a conversation change
You can listen for the event in `V2TIMConversationListener` ([details](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Class/Listener/V2TimConversationListener.html)) to get the notification of a conversation list change.

Currently, the Chat SDK supports the following conversation change events:

| Event                            | Description                                                  | Suggestion                                                   |
| -------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| onSyncServerStart                | Server conversation sync started.                            | The SDK will automatically sync server conversations after a successful login or network reconnection. You can listen for such an event and display the event progress on the UI. |
| onSyncServerFinish               | Server conversation sync was completed.                      | If there is a conversation change, the change will be notified through the `onNewConversation`/`onConversationChanged` callback. |
| onSyncServerFailed               | Server conversation sync failed.                             | You can listen for such an event and display the event exception on the UI. |
| onNewConversation                | A new conversation was added.                                | When the user receives a one-to-one message from a new colleague or is invited to a new group, you can re-sort the conversations. |
| onConversationChanged            | There is a conversation update.                              | When the unread count changes or the last message is updated, you can re-sort the conversations. |
| onTotalUnreadMessageCountChanged | The total unread message count of all conversations has changed. | For details, see [unreadCount](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Class/Message/V2TimConversation.html#unreadcount). |

> ? To ensure that the conversations are sorted by the last message, you need to re-sort the data sources each time a conversation is changed/added.
> * If you use the SDK for Flutter earlier than v3.8.0, you can sort the conversations by `lastMessage`, but note that sometimes `lastMessage` may be empty (such as when messages in a conversation are cleared).
> * If you use the SDK for Flutter on v3.8.0 or later, you can sort the conversations by `orderKey`.
> * We recommend you upgrade the SDK for Flutter to v3.8.0 or later.

Sample code:


```dart
    // Set a group event listener
    V2TimGroupListener listener = V2TimGroupListener(onApplicationProcessed:
        (String groupID, V2TimGroupMemberInfo opUser, bool isAgreeJoin,
            String opReason) async {
      // Group joining request handled by group owner or admin (received only by the applicant)
      // groupID: Group ID
      // opUser: Handler
      // isAgreeJoin: Whether to agree to join the group
      // opReason: Handling reason
    }, onGrantAdministrator: (String groupID, V2TimGroupMemberInfo opUser,
        List<V2TimGroupMemberInfo> memberList) async {
      // Specify the admin identity
      // groupID: Group ID
      // opUser: Handler
      // memberList: Group members handled
    }, onGroupAttributeChanged:
        (String groupID, Map<String, String> groupAttributeMap) async {
      // Received group attribute update callback
      // groupID: Group ID
      // groupAttributeMap: All attributes of the group
    }, onGroupCreated: (String groupID) async {
      // Group created (used for multi-device synchronization)
      // groupID: Group ID
    }, onGroupDismissed: (String groupID, V2TimGroupMemberInfo opUser) async {
      // The group is deleted (received by all users)
      // groupID: Group ID
      // opUser: Handler
    }, onGroupInfoChanged:
        (String groupID, List<V2TimGroupChangeInfo> changeInfos) async {
      // Group information modified (received by all members)
      // groupID: Group ID
      // changeInfos: Group information modified
    }, onGroupRecycled: (String groupID, V2TimGroupMemberInfo opUser) async {
      // Group repossessed (received by all members)
      // groupID: Group ID
      // opUser: Handler
    }, onMemberEnter:
        (String groupID, List<V2TimGroupMemberInfo> memberList) async {
      // Users join the group (received by all members)
      // groupID: Group ID
      // memberList: Members who join the group
    }, onMemberInfoChanged: (String groupID,
        List<V2TimGroupMemberChangeInfo> v2TIMGroupMemberChangeInfoList) async {
      // Group member information modified, supporting notifications for muting only (received by all members)
      // groupID: Group ID
      // v2TIMGroupMemberChangeInfoList: Group member information modified
    }, onMemberInvited: (String groupID, V2TimGroupMemberInfo opUser,
        List<V2TimGroupMemberInfo> memberList) async {
      // Users are added to a group by others (received by all members)
      // groupID: Group ID
      // opUser: Handler
      // memberList: Members who are added to the group
    }, onMemberKicked: (String groupID, V2TimGroupMemberInfo opUser,
        List<V2TimGroupMemberInfo> memberList) async {
      // Users are removed from a group by others (received by all members)
      // groupID: Group ID
      // opUser: Handler
      // memberList: Members who are removed from the group
    }, onMemberLeave: (String groupID, V2TimGroupMemberInfo member) async {
      // Users leave the group (received by all members)
      // groupID: Group ID
      // member: Members who leave the group
    }, onQuitFromGroup: (String groupID) async {
      // Leave a group (mainly used for multi-device synchronization, not supported by audio-video groups)
      // groupID: Group ID
    }, onReceiveJoinApplication:
        (String groupID, V2TimGroupMemberInfo member, String opReason) async {
      // New group joining request (received only by the group owner and admin)
      // groupID: Group ID
      // member: Applicant
      // opReason: Request reason
    }, onReceiveRESTCustomData: (String groupID, String customData) async {
      // Received a custom system message delivered via the RESTful API
      // groupID: Group ID
      // customData: Custom data
    }, onRevokeAdministrator: (String groupID, V2TimGroupMemberInfo opUser,
        List<V2TimGroupMemberInfo> memberList) async {
      // Cancel the admin identity
      // groupID: Group ID
      // opUser: Handler
      // memberList: Group members handled
    }, onTopicCreated: (String groupID, String topicID) async {
      // Topic creation notification
      // groupID: ID of the group for which the topic is created
      // topicID: ID of the topic created
    }, onTopicDeleted: (String groupID, List<String> topicIDList) async {
      // Topic deletion notification
      // groupID: ID of the group for which the topic is deleted
      // topicIDList: List of IDs of the topics deleted
    }, onTopicInfoChanged: (String groupID, V2TimTopicInfo topicInfo) async {
      // Topic information update notification
      // groupID: ID of the group for which the topic information is updated
      // topicInfo: Attributes updated in the topic information
    });
    // Add a group event listener
    TencentImSDKPlugin.v2TIMManager.addGroupListener(listener: listener);
```


### Removing a conversation listener
Call the `removeConversationListener` API ([details](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMConversationManager/removeConversationListener.html)) to remove a conversation listener to stop receiving conversation change events.
This step is optional and can be performed as needed.

Sample code:


```dart
conversationManager.removeConversationListener(conversationListener);
```



### Sending a message without updating the lastMessage
On the UI of conversation list, it is usually necessary to display the preview and send time of the latest message in each conversation. In this case, you can use `lastMessage` of `V2TIMConversation` as the data source for implementation. However, in some cases, if you don't want some messages (such as system tips) to be displayed as the latest message in a conversation, you can set `isExcludedFromLastMessage` to `false`/`no` when calling `sendMessage`.

For how to send a message, see [sendMessage](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMMessageManager/sendMessage.html).


>? `isExcludedFromLastMessage` is supported only by the SDK for Flutter on v4.0.0 or later.
