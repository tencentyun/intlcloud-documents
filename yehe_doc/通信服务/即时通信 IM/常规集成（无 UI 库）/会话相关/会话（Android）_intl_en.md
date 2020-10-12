
## Displaying the Conversation List
After the user logs in to the app, the app can display a list of recent conversions like WeChat. The overall display process includes the following steps: **pulling the conversation list**, **processing the change notifications**, and **updating the UI content (including the unread count)**. This document describes these steps in detail.


### Pulling the conversation list
After logging in to the app, you can call [getConversationList()](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#a1bb5ba2beecb4f68146e7f664124fd8b) to pull the local conversation list and display the list on the UI. The conversation list is a list of [V2TIMConversation](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversation.html) objects, and every object represents a conversation.

The number of local conversations may be large, even more than 500. Therefore, it may take a long time to load all conversations at once, which results in the slow display of the list on the UI. To improve the user experience, we provide the `getConversationList()` API to support pulling by page.
1. When the `getConversationList()` API is called for the first time, you can set the `nextSeq` parameter to 0, indicating that the conversation list is pulled from the beginning, and set `count` to 50, indicating that 50 conversation objects are pulled at a time.
2. The IM SDK pulls the conversation list in reverse chronological order. After the conversation list is pulled successfully for the first time, [V2TIMConversationResult](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationResult.html), which is the callback result of `getConversationList()`, will contain the `nextSeq` field for the next pulling by page operation and the `isFinish` field that indicates whether all conversation objects have been pulled.
 - If the returned value of `isFinished` is `true`, all conversations have been pulled.
 - If the returned value of `isFinished` is `false`, more conversations can be pulled. This does not mean that the next page of the conversation list will be pulled immediately. In common communications software, pulling by page is often triggered when the user swipes. Each time the user swipes on the conversation list, pulling by page is triggered once.
<span id="get_step3"></span>
3. When the user continues to pull down the conversation list, and the conversation list has content yet to be pulled, the user can continue to call the [getConversationList](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#a1bb5ba2beecb4f68146e7f664124fd8b) API and passes in the `nextSeq` and `count` parameters again. The values of the two parameters come from the [V2TIMConversationResult](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationResult.html) object returned in the previous pull operation.
4. The IM SDK repeats [step 3](#get_step3) until the returned value of [isFinished](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationResult.html#a3e7d1138f146a8f19c15d0f5d81f6448) is `true`.

### Displaying the conversation information
After obtaining the [V2TIMConversation](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversation.html) object, the IM SDK displays the conversation information on the UI. `V2TIMConversation` contains the following key fields, which are often used to construct the conversation list.

| Field | Description |
|---------|---------|
| [getShowName ()](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversation.html#af52fcfb1e5f622051f6cccb21e03c140) | The conversion name:<ul><li>For a one-to-one chat, the API preferentially returns the friend’s remark. If the remark is unavailable or if the other party is not a friend, the API returns the nickname of the other party. If the nickname is also unavailable, the API returns the UserID of the other party.</li><li>For a group chat, the group name is displayed.</li></ul> |
| [getFaceUrl ()](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversation.html#a5325fc744fb7284babef0eaa56884182) | The profile photo for the conversation: <ul><li>For a one-to-one chat, the other party’s profile photo is displayed.</li><li>For a group chat, the group's profile photo is displayed.</li></ul> |
| [getRecvOpt ()](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversation.html#a82f673186669d31f7acd38c52d412ba2) | The message receiving option, which is generally used for a group conversation. It indicates whether the **Do Not Disturb** mode is enabled for the group. |
| [getUnreadCount ()](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversation.html#ab6a7667ac8a9f7a17a38ee8e7caec98e) | The unread count, which indicates the number of unread messages. |
| [getLastMessage ()](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversation.html#ad3a7004f1c2bd06831720a38d4209520) | The last message, which displays the message digest of the conversation. |

### Updating the conversation list

After login is successful, the user goes online, or the connection is re-established after being interrupted, the IM SDK will automatically update the conversation list. The update process is as follows:
- When any conversation is updated, such as when a new message is received, the SDK will notify you by using the [onConversationChanged](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationListener.html#a4ca1b0c3ec948d9cb76acd6022a1ebf9) event in `V2TIMConversationListener`.
- When any conversation is added, the SDK will notify you by using the [onNewConversation](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationListener.html#ab213c51c45045665dde1542c276e2530) event in `V2TIMConversationListener`.

>!To ensure that the order of the conversation list complies with the sequencing principle specified in the last message, the data source must be re-sequenced based on [getTimestamp](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessage.html#aa5fc8709c93d77e6978075466a4e819a) in [getLastMessage](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversation.html#ad3a7004f1c2bd06831720a38d4209520).

### Sample code
The sample code shows how to pull, display, and update the conversation list.

```
// 1. Set the conversation listener.
V2TIMManager.getConversationManager().setConversationListener(this);
// 2. Pull 50 local conversations to display them on the UI. Set the value of `nextSeq` that is passed in for the first pull to 0.
V2TIMManager.getConversationManager().getConversationList(0, 50, 
    new V2TIMValueCallback<V2TIMConversationResult>() {
	@Override
	public void onError(int code, String desc) {
		// The conversation list failed to be pulled.
	}
	@Override
	public void onSuccess(V2TIMConversationResult v2TIMConversationResult) {
		// Pulling is successful, and the UI conversation list is updated.
		updateConversation(v2TIMConversationResult.getConversationList(), false);
		if (!v2TIMConversationResult.isFinished()) {
			V2TIMManager.getConversationManager().getConversationList(
			    v2TIMConversationResult.getNextSeq(), 50, 
					new V2TIMValueCallback<V2TIMConversationResult>() {
			@Override
			public void onError(int code, String desc) {}
			@Override
			public void onSuccess(V2TIMConversationResult v2TIMConversationResult) {
				// Pulling is successful, and the UI conversation list is updated.
				updateConversation(v2TIMConversationResult.getConversationList(), false);
			}
		});
	}
}
// 3.1 Receive the callback for adding a conversation.
@Override
public void onNewConversation(List<V2TIMConversation> conversationList) {
	updateConversation(conversationList, true);
}
// 3.2 Receive the callback for updating the conversation.
@Override
public void onConversationChanged(List<V2TIMConversation> conversationList) {
	updateConversation(conversationList, true);
}

private void updateConversation(List<V2TIMConversation> convList, boolean needSort) {
	for (int i = 0; i < convList.size(); i++) {
		V2TIMConversation conv = convList.get(i);
		boolean isExit = false;
		for (int j = 0; j < uiConvList.size(); j++) {
			V2TIMConversation uiConv = uiConvList.get(j);
			// If the conversation exists in the UI conversation list, replace this conversation.
			if (uiConv.getConversationID().equals(conv.getConversationID())) {
				uiConvList.set(j, conv);
				isExit = true;
				break;
			}
		}
		// If the conversation does not exist in the UI conversation list, add this conversation.
		if (!isExit) {
			uiConvList.add(conv);
		}
	}
	// 4. Based on the timestamp in the lastMessage of the conversation, sort the UI conversation list, and refresh the UI.
	if (needSort) {
		Collections.sort(uiConvList, new Comparator<V2TIMConversation>() {
			@Override
			public int compare(V2TIMConversation o1, V2TIMConversation o2) {
				if (o1.getLastMessage().getTimestamp() -> o2.getLastMessage().getTimestamp()) {
						return -1;
				} else {
						return 1;
				}
			}
		});
	}
	...
	mAdapter.setDataResource(uiConvList);
	mAdapter.notifyDataSetChanged();
}

```

## Deleting a Conversation
You can call the [deleteConversation](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#a7a6e38c5a7431646bd4c0c4c66279077) API to delete a conversation. This operation cannot be synchronized across multiple devices. When a conversation is deleted, its local history and messages on the server will also be deleted by default, which are unrecoverable.



## Drafts
When sending a message, the user may need to switch to another chat window before message editing is completed. In this case, call the [setConversationDraft](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#ae7f2f52bf375dae69368eae42edb28ab) API to save the unfinished message. Later, the user can return to the original chat window and call [getDraftText](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversation.html#a56ac45415e28fe634dfdb1e0aaeea805) to continue editing the message.

>!
>- Only text content can be stored in drafts.
>- Drafts are stored only locally, instead of on the server. Therefore, drafts cannot be synchronized across multiple devices. If the program is reinstalled, drafts cannot be reloaded.

## FAQs
### 1. What is the maximum number of conversations that can be stored in a conversation list?
A locally stored conversation list can have an unlimited number of conversations. A conversation list stored in the cloud can have up to 100 conversations.
If the information of a conversation has not been updated for a long time, this conversation will be stored in the cloud for up to 7 days. To adjust the period for storing the conversation, [contact us](https://console.cloud.tencent.com/workorder/category).

### 2. Why are the conversation lists pulled on different mobile phones in the same account inconsistent?
Locally stored conversations may not always be consistent with those stored in the cloud. If the user does not call the [deleteConversation](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#a7a6e38c5a7431646bd4c0c4c66279077) API to delete the local conversations, these conversations will always exist. However, only up to 100 conversations can be stored in the cloud. In addition, if the information of a conversation has not been updated for a long time, this conversation can be stored in the cloud for up to 7 days. Therefore, local conversations displayed on different mobile phones may be inconsistent with each other.

### 3. Why is the same conversation pulled multiple times?
Conversations that are pulled by the `getConversationList` API may have been already added to the data source of the UI conversation list through the `onNewConversation` callback API. Therefore, to avoid adding the same conversation repeatedly, you need to find and replace duplicate conversations based on [getConversationID](http://doc.qcloudtrtc.com/im/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversation.html#ae599509f3d5e39bbcfb176b8976ff620).

### 4. Does the IM SDK support pinning a conversation to the top of the list?
The IM SDK does not provide the feature of pinning a conversation to the top of the list, but supports re-sequencing conversations by means of encapsulation. For more information, see the implementation of TUIKit. Such pinning settings take effect only on the local device, and will not be stored in the cloud.

