
## Displaying the Conversation List
After logging in to the app, you can display a list of recent conversions like WeChat. The entire display process includes the following steps: **pulling the conversation list**, **processing the change notifications**, and **updating the UI content (including the unread count)**. This document describes these steps in detail.

### Pulling the conversation list
After logging in to the app, you can call [getConversationList()](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#a1bb5ba2beecb4f68146e7f664124fd8b) to pull the local conversation list and display the list on the UI. The conversation list is a list of [V2TIMConversation](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversation.html) objects, and every object represents a conversation.

The number of local conversations may be large, for example, more than 500. It may take a long time to load all conversations at a time, which results in slow display of the list on the UI. To improve user experience, the `getConversationList()` API is provided to support the feature of pulling by page.
1. When the `getConversationList()` API is called for the first time, you can set the `nextSeq` parameter to 0, indicating that the conversation list is pulled from the beginning, and set `count` to 50, indicating that 50 conversation objects are pulled at a time.
2. The IM SDK pulls the conversation list in the new-to-old order. After the conversation list is pulled successfully for the first time, [V2TIMConversationResult](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationResult.html), which is the callback result of `getConversationList()`, will contain the `nextSeq` field for the next pulling by page, and the `isFinish` field that indicates whether the conversation pulling is completed.
 - If the returned value of `isFinished` is `true`, all conversations have been pulled.
 - If the returned value of `isFinished` is `false`, more conversations can be pulled. This does not mean that the next page of the conversation list will be pulled immediately. In common communications software, pulling by page is often triggered by the swipe operation of the user. Each time when you swipe on the conversation list, pulling by page is triggered once.
[](id:get_step3)
3. When you continue to swipe on the conversation list, if more content of the conversation list is yet to be pulled, the IM SDK can continue to call the [getConversationList](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#a1bb5ba2beecb4f68146e7f664124fd8b) API and pass in the `nextSeq` and `count` parameters again. The values of the two parameters come from the [V2TIMConversationResult](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationResult.html) object returned in the previous pulling.
5. The IM SDK repeats [step 3](#get_step3) until the returned value of [isFinished](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationResult.html#a3e7d1138f146a8f19c15d0f5d81f6448) is `true`.

### Displaying the conversation information
After obtaining the [V2TIMConversation](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversation.html) object, the IM SDK can display the conversation information on the UI. `V2TIMConversation` contains the following key fields, which are often used to construct the conversation list.

| Field | Description |
|---------|---------|
| [getShowName ()](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversation.html#af52fcfb1e5f622051f6cccb21e03c140) | The conversion name:<ul><li>For the one-to-one chat, the API preferentially returns the friend’s remark. If the remark is unavailable or if the peer is not a friend, the API returns the nickname of the peer. If the nickname is also unavailable, the API returns the UserID of the peer.</li><li>For a group chat, the group name is displayed.</li></ul> |
| [getFaceUrl ()](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversation.html#a5325fc744fb7284babef0eaa56884182) | The profile photo for the conversation: <ul><li>For a one-to-one chat, the other party’s profile photo is displayed. </li><li>For a group chat, the group's profile photo is displayed.</li></ul> |
| [getRecvOpt ()](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversation.html#a82f673186669d31f7acd38c52d412ba2) | The message receiving option, which is generally used for a group conversation. It indicates whether the **Mute notifications** mode is enabled for the group. |
| [getUnreadCount ()](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversation.html#ab6a7667ac8a9f7a17a38ee8e7caec98e) | The unread count, which indicates the number of unread messages |
| [getLastMessage ()](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversation.html#ad3a7004f1c2bd06831720a38d4209520) | The last message, which displays the message digest of the conversation |

### Updating the conversation list

After the IM SDK is successfully logged in, or the user goes online, or the connection is re-established after being interrupted, the IM SDK will automatically update the conversation list. The update process is as follows:
- When any conversation is updated, for example, when a new message is received, the SDK will notify you by using the [onConversationChanged](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationListener.html#a4ca1b0c3ec948d9cb76acd6022a1ebf9) event in `V2TIMConversationListener`.
- When any conversation is added, the SDK will notify you by using the [onNewConversation](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationListener.html#ab213c51c45045665dde1542c276e2530) event in `V2TIMConversationListener`.

>!To ensure that the order of the conversation list complies with the sequencing principle specified in the last message, the data source must be re-sequenced based on [getTimestamp](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessage.html#aa5fc8709c93d77e6978075466a4e819a) in [getLastMessage](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversation.html#ad3a7004f1c2bd06831720a38d4209520).

### Sample code
The sample code shows how to pull, display, and update the conversation list.

```
// 1. Set the conversation listener.
V2TIMManager.getConversationManager().setConversationListener(this);
// 2. Pull 50 local conversation to display them on the UI. Set the value of `nextSeq` that is passed in for the first pulling to 0.
V2TIMManager.getConversationManager().getConversationList(0, 50, 
    new V2TIMValueCallback<V2TIMConversationResult>() {
	@Override
	public void onError(int code, String desc) {
		// The attempt to pull the conversation list fails.
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
				if (o1.getLastMessage().getTimestamp() > o2.getLastMessage().getTimestamp()) {
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
## Obtaining the Total Unread Message Count of All Conversations (Only Available in Lite Edition v5.3.425 and Above)
You can call the [getTotalUnreadMessageCount](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#a08bdd15d7ee2737335a01285d7f9c44a) API to get the total unread count of all conversations. You don't need to go through the conversation list and add up the unread count of each conversation to get the total unread count. When the total unread count changes, the SDK will proactively call back [onTotalUnreadMessageCountChanged](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationListener.html#a292e893a04cb092fe49c06873c1ea4b3) to your app to notify you of the latest unread count.

## Pinning a Conversation on Top (Only Available in Lite Edition v5.3.425 and Above)
You can pin a one-to-one or group conversation on the top of the conversation list so you can quickly find it. The new SDK version has added the [pinConversation](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#a4da7467f54c891c4929152260e42f4b6) API to pin/unpin conversations to/from top. It also supports roaming and multi-client synchronization.
The [V2TIMConversation](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversation.html) conversation object has added the [isPinned](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversation.html#aff4bf9967af813b87bc1fbf52180319f) API, which is used to determine whether a conversion is pinned on top. When the pinned-on-top status of a conversation changes, the SDK will call back [onConversationChanged](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationListener.html#a4ca1b0c3ec948d9cb76acd6022a1ebf9) to your app.

## Deleting a Conversation
You can call the [deleteConversation](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#a7a6e38c5a7431646bd4c0c4c66279077) API to delete a conversation. Conversation deletion cannot be synchronized across multiple clients. When a conversation is deleted, the message history of this conversation will be deleted from the local storage and the server by default, and cannot be recovered.


## Drafts
When sending a message, you may need to switch to another chat window before message editing is completed. In this case, you can call the [setConversationDraft](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#ae7f2f52bf375dae69368eae42edb28ab) API to save the unfinished message. Later, you can return to the original chat window and call [getDraftText](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversation.html#a56ac45415e28fe634dfdb1e0aaeea805) to continue editing the message.

>!
>- Only text content can be stored in Drafts.
>- Drafts are stored only locally, instead of on the server. Therefore, drafts cannot be synchronized across multiple devices. If the program is uninstalled, drafts cannot be reloaded.

## FAQs
### 1. What is the upper limit for the number of conversations that can be stored in a conversation list?
A locally stored conversation list can have unlimited number of conversations. A conversation list stored in the cloud can have up to 100 conversations.
If the information of a conversation has not been updated for a long time, this conversation can be stored in the cloud for at most 7 days. To adjust the period for storing the conversation, [contact us](https://console.cloud.tencent.com/workorder/category).

### 2. Why are the conversation lists pulled on different mobile phones by using the same account inconsistent?
Locally stored conversations may not always be consistent with those stored in the cloud. If you do not call the [deleteConversation](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#a7a6e38c5a7431646bd4c0c4c66279077) API to delete the local conversations, these conversations will always exist. However, at most 100 conversations can be stored in the cloud. In addition, if the information of a conversation has not been updated for a long time, this conversation can be stored in the cloud for at most 7 days. Therefore, local conversations displayed on different mobile phones may be inconsistent with each other.

### 3. Why are repeated conversations pulled?
Conversations that are pulled by the `getConversationList` API may have already been added to the data source of the UI conversation list through the `onNewConversation` callback API. Therefore, to avoid adding the same conversation repeatedly, you need to find and replace the same conversations based on [getConversationID](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversation.html#ae599509f3d5e39bbcfb176b8976ff620).

### 4. Does the IM SDK support the feature of pinning a conversation to the top?
IM SDK supports pinning a conversation to the top and sync to the cloud starting from v5.3.425.
