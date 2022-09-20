## Displaying the Conversation List
After logging in to the app, you can display a list of recent conversations. The entire display process includes the following steps: **pulling the conversation list**, **processing the change notifications**, and **updating the UI content (including the unread count)**. This document describes these steps in detail.

![](https://qcloudimg.tencent-cloud.cn/raw/9645e51a0a98b5aa7725ff742920cfa3.png)

### Pulling the conversation list
After logging in to the app, you can call [getConversationList()](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMConversationManager/getConversationList.html) to pull the local conversation list and display the list on the UI. The conversation list is a list of [V2TIMConversation](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Message/V2TimConversation.html) objects, and every object represents a conversation.

The number of local conversations may be large, for example, more than 500. It may take a long time to load all conversations at a time, which results in slow display of the list on the UI. To improve user experience, the `getConversationList()` API is provided to support the feature of pulling by page.
1. When the `getConversationList()` API is called for the first time, you can set the `nextSeq` parameter to 0, indicating that the conversation list is pulled from the beginning, and set `count` to 50, indicating that 50 conversation objects are pulled at a time.
2. The IM SDK pulls the conversation list in reverse chronological order. After the conversation list is pulled successfully for the first time, [V2TIMConversationResult](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Message/V2TimConversationResult.html), which is the callback result of `getConversationList()`, will contain the `nextSeq` field for the next pulling by page, and the `isFinish` field that indicates whether the conversation pulling is completed.
 - If the returned value of `isFinished` is `true`, all conversations have been pulled.
 - If the returned value of `isFinished` is `false`, more conversations can be pulled. This does not mean that the next page of the conversation list will be pulled immediately. In common communications software, pulling by page is often triggered by the swipe operation of the user. Each time when you swipe on the conversation list, pulling by page is triggered once.
[](id:get_step3)
3. When you continue to swipe on the conversation list, if more content of the conversation list is yet to be pulled, the IM SDK can continue to call the [getConversationList](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMConversationManager/getConversationList.html) API and pass in the `nextSeq` and `count` parameters again. The values of the two parameters come from the [V2TimConversationResult](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Message/V2TimConversationResult.html) object returned in the previous pulling.
4. The IM SDK repeats [step 3](#get_step3) until the returned value of [isFinished](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Message/V2TimConversationResult.html) is `true`.

### Displaying the conversation information
After obtaining the [V2TimConversation](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Message/V2TimConversation.html) object, the IM SDK can display the conversation information on the UI. `V2TIMConversation` contains the following key fields, which are often used to construct the conversation list.

| Field                                                                                                           | Description                                                                                                                                                                                                                                                                                                                                            |
| --------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| [showName](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Message/V2TimConversation.html#showname)          | The conversation name:<li>For the one-to-one chat, the API preferentially returns the friend’s remark. If the remark is unavailable or if the peer is not a friend, the API returns the nickname of the peer. If the nickname is also unavailable, the API returns the UserID of the peer.</li><li>For a group chat, the group name is displayed.</li> |
| [faceUrl](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Message/V2TimConversation.html#faceurl)            | The profile photo for the conversation:<li>For a one-to-one chat, the other party's profile photo is displayed.</li><li>For a group chat, the group's profile photo is displayed.</li>                                                                                                                                                                 |
| [recvOpt](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Message/V2TimConversation.html?q=#recvopt)         | The message receiving option, which is generally used for a group conversation. It indicates whether the **Mute Notifications** mode is enabled for the group.                                                                                                                                                                                         |
| [readCount](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Message/V2TimConversation.html#unreadcount)      | The unread count, which indicates the number of unread messages.                                                                                                                                                                                                                                                                                       |
| [lastMessage](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Message/V2TimConversation.html?q=#lastmessage) | The last message, which displays the message digest of the conversation.                                                                                                                                                                                                                                                                               |

### Updating the conversation list

After the IM SDK is successfully logged in, or the user goes online, or the connection is re-established after being interrupted, the IM SDK will automatically update the conversation list. The update process is as follows:
- When any conversation is updated, for example, when a new message is received, the SDK will notify you by using the [onConversationChanged](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Callback/OnConversationChangedCallback.html) event in `V2TIMConversationListener`.
- When any conversation is added, the SDK will notify you by using the [onNewConversation](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Callback/OnNewConversation.html) event in `V2TIMConversationListener`.

>!To ensure that the order of the conversation list complies with the sequencing principle specified in the last message, the data source must be re-sequenced based on [timestamp](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Message/V2TimMessage.html#timestamp) in [lastMessage](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Message/V2TimConversation.html#lastmessage).

### Sample code
The sample code shows how to pull, display, and update the conversation list.

```dart
// 1. Register the conversation listener.
    await TencentImSDKPlugin.v2TIMManager
        .getConversationManager()
        .setConversationListener(
          listener: new V2TimConversationListener(
            onConversationChanged: (List<V2TimConversation> list){
				// ...
			},
            onNewConversation:(List<V2TimConversation> list){
				// ...
			},
			// Other listening...
          ),
        );
// 2. Pull 50 local conversation to display them on the UI. Set the value of `nextSeq` that is passed in for the first pulling to 0.
  getConversationList() async {
    V2TimValueCallback<V2TimConversationResult> res = await TencentImSDKPlugin
        .v2TIMManager
        .getConversationManager()
        .getConversationList(nextSeq: nextSeq, count: 10);
    V2TimValueCallback<V2TimConversationResult> nextRes =
        await TencentImSDKPlugin.v2TIMManager
            .getConversationManager()
            .getConversationList(nextSeq: res.data?.nextSeq ?? "0", count: 20);
// 3.1 Receive the callback for adding a conversation.
    await TencentImSDKPlugin.v2TIMManager
        .getConversationManager()
        .setConversationListener(
          listener: new V2TimConversationListener(
            onNewConversation:(List<V2TimConversation> conversationList){
				// .......
			},
          ),
        );
// 3.2 Receive the callback for updating the conversation.
     TencentImSDKPlugin.v2TIMManager
        .getConversationManager()
        .setConversationListener(
          listener: new V2TimConversationListener(
            onConversationChanged: (List<V2TimConversation> list){
				// Call the update method
				_onConversationListChanged(list);
				// ...
			},
          ),
        );
	
	final List<V2TimConversation> _conversationList = [];
  // Sorting method
  sort() {
    _conversationList.sort((a, b) => b!.orderkey!.compareTo(a!.orderkey!));
  }

  _onConversationListChanged(List<V2TimConversation> list) {
    for (int element = 0; element < list.length; element++) {
      int index = _conversationList.indexWhere(
          (item) => item!.conversationID == list[element].conversationID);
      if (index > -1) {
        _conversationList.setAll(index, [list[element]]);
      } else {
        _conversationList.add(list[element]);
      }
    }

    
  }

  // Sorting
  sort();
	//...
	
	
}

```
## Obtaining Total Unread Message Count of All Conversations
You can call the [getTotalUnreadMessageCount](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMConversationManager/getTotalUnreadMessageCount.html) API to get the total unread count of all conversations. You don't need to go through the conversation list and add up the unread count of each conversation to get the total unread count. When the total unread count changes, the SDK will proactively call back [onTotalUnreadMessageCountChanged](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Callback/OnTotalUnreadMessageCountChanged.html) to your app to notify you of the latest unread count.


## Pinning a Conversation to the Top
You can pin a one-to-one or group conversation on the top of the conversation list. The new SDK version has added the [pinConversation](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMConversationManager/pinConversation.html) API to pin/unpin conversations to/from the top. It also supports roaming and multi-client synchronization.
The [V2TIMConversation](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Message/V2TimConversation.html) conversation object has added the [isPinned](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Message/V2TimConversation.html#ispinned) field, which is used to determine whether a conversation is pinned on top. When the pinned-on-top status of a conversation changes, the SDK will call back [onConversationChanged](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Callback/OnConversationChangedCallback.html) to your app.

## Deleting a Conversation
You can call the [deleteConversation](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMConversationManager/deleteConversation.html) API to delete a conversation. Conversation deletion cannot be synchronized across multiple clients by default. You can enable the multi-client synchronization feature in the console. When a conversation is deleted, the message history of this conversation will be deleted from the local storage and the server by default, and cannot be recovered.


## Drafts
When sending a message, you may need to switch to another chat window before message editing is completed. In this case, you can call the [setConversationDraft](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMConversationManager/setConversationDraft.html) API to save the unfinished message. Later, you can return to the original chat window and call [draftText in V2TimConversation](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Message/V2TimConversation.html) to continue editing the message.

>?
>- Only text content can be stored in Drafts.
>- Drafts are stored only locally, instead of on the server. Therefore, drafts cannot be synchronized across multiple devices. If the program is uninstalled, drafts cannot be reloaded.

## FAQs
### 1. What is the upper limit for the number of conversations that can be stored in a conversation list?
A locally stored conversation list can have unlimited number of conversations. A conversation list stored in the cloud can have up to 100 conversations.
If the information of a conversation has not been updated for a long time, this conversation can be stored in the cloud for at most 7 days. To adjust the period for storing the conversation, [contact us](https://console.cloud.tencent.com/workorder/category).

### 2. Why are the conversation lists pulled on different mobile phones by using the same account inconsistent?
Locally stored conversations may not always be consistent with those stored in the cloud. If you do not call the [deleteConversation](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMConversationManager/deleteConversation.html) API to delete the local conversations, these conversations will always exist. However, at most 100 conversations can be stored in the cloud. In addition, if the information of a conversation has not been updated for a long time, this conversation can be stored in the cloud for at most 7 days. Therefore, local conversations displayed on different mobile phones may be inconsistent with each other.

### 3. Why are repeated conversations pulled?
Conversations that are pulled by the `getConversationList` API may have already been added to the data source of the UI conversation list through the `onNewConversation` callback API. Therefore, to avoid adding the same conversation repeatedly, you need to find and replace the same conversations based on [ConversationID](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Message/V2TimConversation.html#conversationid).

### 4. Does the IM SDK support the feature of pinning a conversation to the top?
Yes. The `isPinned` field will be obtained for the conversation list and conversation information.
