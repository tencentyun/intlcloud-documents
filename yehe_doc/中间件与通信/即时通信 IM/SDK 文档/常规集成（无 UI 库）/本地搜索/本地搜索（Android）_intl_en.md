Local search is supported starting from Enhanced Edition v5.4.666. To use local search, you need to purchase the Flagship Edition package. For operation details, please see [Purchase Guide](https://intl.cloud.tencent.com/document/product/1047/36021).

## Feature Demonstration
The search API interface consists of three parts: the upper part is for friend search, the middle part is for group and group member search, and the lower part is for message search, where messages are classified by conversation.

## Integration Guide
### Scheme 1: Integrating TUIKit search source code
#### Step 1. Purchase the package
Purchase the Flagship Edition package by referring to [Purchase Guide](https://intl.cloud.tencent.com/document/product/1047/36021).
#### Step 2. Download source code
[Download source code](https://github.com/tencentyun/TIMSDK) to integrate the TUIKit module. TUIKit supports local search starting from v5.4.666.

```
implementation project(':tuikit')
```
#### Step 3. Initialize TUIKit and log in

```
// Initialize TUIKit
TUIKitConfigs configs = TUIKit.getConfigs();
TUIKit.init(this, SDKAPPID, configs);
// Log in to TUIKit
TUIKit.login(userID, userSig, new IUIKitCallBack() {
@Override
public void onSuccess(Object data) {
    // Login succeeded
}

@Override
public void onError(String module, final int code, final String desc) {
    // Login failed
}
});
```

#### Step 4. Start the search interface
You only need to start `SearchMainActivity`.

### Scheme 2: Integrate the IM SDK search API
#### Step 1. Purchase the package
Purchase the Flagship Edition package by referring to [Purchase Guide](https://intl.cloud.tencent.com/document/product/1047/36021).
#### Step 2. Integrate IM SDK Enhance Edition
The IM SDK supports local search starting from v5.4.666.

```
dependencies {
  api 'com.tencent.imsdk:imsdk-plus:Version number`
}
```

#### Step 3. Call the local user profile search API
You can call the [searchFriends](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a815b7c4ff79f1441ee1416ff679eda6a) API to search for local user profiles. The API supports the following search fields: [userID](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendSearchParam.html#ae2ee7265c0c966aa5a4e5200bf40b7d2), [nickName](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendSearchParam.html#a1463093770c45df5fca39bdca9103980), and [remark](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendSearchParam.html#a09a945c5cb71a13de5e32c80491363fd).

#### Step 4. Call the local group and group member search APIs

You can call the [searchGroups](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a94a72082b7e2682942f35196a7e28023) API to search for the profiles of local groups.
You can call the [searchGroupMembers](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a493fb73258019961f3ca8934ff625b0a) API to search for the profiles of local group members. There are two cases, depending on whether the value of `groupIDList` in [V2TIMGroupMemberSearchParam](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupMemberSearchParam.html) is `null`:
- groupIDList == null: search the members in all groups, and the returned results will be classified by group ID.
- groupIDList != null: search the members in a specified group.

#### Step 5. Call the local message search API
You can enter keywords in the search box to call [searchLocalMessages](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a9364c8a0c6a0899b17c0a479b8ca848a) to search for local messages. There are two cases, depending on whether the value of [conversationID](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageSearchParam.html#ad0beca2cedf96a08d1e44709c16105d7) in the [V2TIMMessageSearchParam](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageSearchParam.html) API is `null`:
- conversationID == null: search all conversations, and the returned results will be classified by conversation.
- conversationID != null: search a specified conversation.

**Displaying recent active conversations**
As shown in Figure 1, the bottom part of the search interface is the list of the last 3 conversations to which the messages found belong. The implementation method is as follows:
- In the [V2TIMMessageSearchParam](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageSearchParam.html) API, [conversationID](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageSearchParam.html#ad0beca2cedf96a08d1e44709c16105d7) is set to `null`, indicating the messages of all conversations are searched; [pageIndex](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageSearchParam.html#ad5e6b317d430d9e0cda8221a5fff6b19) is set to `0`, indicating data on page 0 of the conversations to which the messages found belong; [pageSize](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageSearchParam.html#a3aca5a82692437f0fb8501533b9f0063) indicates the number of recent conversations to be returned. Usually, 3 recent conversations are displayed on the UI.
- In the search callback result API [V2TIMMessageSearchResult](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageSearchResult.html), [totalCount](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageSearchResult.html#a97f66183ea41a7c123bab9dd5313a74a) indicates the total number of conversations to which the matched messages belong; [messageSearchResultItems](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageSearchResult.html#a6cc0e2f70f0695a74a18a219c31b3ae3) indicates the information of the recent conversations (conversation quantity specified by [pageSize](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageSearchParam.html#a3aca5a82692437f0fb8501533b9f0063)). In [V2TIMMessageSearchResultItem](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageSearchResultItem.html), [conversationID](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageSearchResultItem.html#ae599509f3d5e39bbcfb176b8976ff620) indicates the conversation ID, [messageCount](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageSearchResultItem.html#a41300a43e3530ab3ba00b61f4337a083) indicates the total number of messages found in the current conversation, and [messageList](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageSearchResultItem.html#aceeced8f371a986511be5c63de354587) indicates the list of messages found. `messageList` has two cases:
	- If the number of messages found is greater than 1, `messageList` is empty. You can display related chat records (quantity specified by `messageCount`) on the UI.
	- If the number of messages found is equal to 1, `messageList` is the matched message. You can display the message content on the UI and highlight the search keyword, such as **test** in the above figures.

**Sample**

```
List<String> keywordList = new ArrayList<>();
keywordList.add("test");
V2TIMMessageSearchParam v2TIMMessageSearchParam = new V2TIMMessageSearchParam();
// Setting `conversationID` to `null` is to search for messages in all conversations and the results will be classified by conversation
v2TIMMessageSearchParam.setConversationID(null);
v2TIMMessageSearchParam.setKeywordList(keywordList);
v2TIMMessageSearchParam.setPageSize(3);
v2TIMMessageSearchParam.setPageIndex(0);
V2TIMManager.getMessageManager().searchLocalMessages(v2TIMMessageSearchParam, new V2TIMValueCallback<V2TIMMessageSearchResult>() {
    @Override
    public void onSuccess(V2TIMMessageSearchResult v2TIMMessageSearchResult) {
        // Total number of matched conversations to which messages belong
        int totalCount = v2TIMMessageSearchResult.getTotalCount();
        // Last 3 messages classified by conversation
        List<V2TIMMessageSearchResultItem> resultItemList = v2TIMMessageSearchResult.getMessageSearchResultItems();
        for (V2TIMMessageSearchResultItem resultItem : resultItemList) {
            // Conversation ID
            String conversationID = resultItem.getConversationID();
            // Total number of messages matching the conversation
            int totalMessageCount = resultItem.getMessageCount();
            // List of messages. If `totalMessageCount` is greater than 1, the list is empty. If `totalMessageCount` is equal to 1, the list contains the current message.
            List<V2TIMMessage> v2TIMMessageList = resultItem.getMessageList();
        }
    }

    @Override
    public void onError(int code, String desc) {}
```

**Displaying the list of conversations to which the messages found belong**
For example, you can click **More Chat History** in Figure 1 to redirect to the list of conversations to which the messages found belong, as shown in Figure 2. The search parameters and results are similar to those in the preceding scenario. To avoid memory ballooning, it is strongly recommended that you load the conversation list with pagination. For example, to display 10 conversations as the result, you can set the search parameter API [V2TIMMessageSearchParam](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageSearchParam.html) as follows:
- First call: Set `pageSize` to `10` and `pageIndex` to `0`, and call [searchLocalMessages](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a9364c8a0c6a0899b17c0a479b8ca848a). Then you can get the total number of conversations from `totalCount` in the callback.
- Page quantity calculation: totalPage = (totalCount % pageSize == 0) ? (totalCount / pageSize) : (totalCount / pageSize + 1)
- Second call: You can specify `pageIndex` (`pageIndex` < `totalPage`) to return the subsequent page number.

**Sample**

```
......
// Calculate the total number of pages, given that 10 messages are displayed per page
int totalPage = (totalCount % 10 == 0) ? (totalCount / 10) : (totalCount / 10 + 1);
......

private void searchConversation(int index) {
    if (index >= totalPage) {
        return;
    }
    List<String> keywordList = new ArrayList<>();
    keywordList.add("test");
    V2TIMMessageSearchParam v2TIMMessageSearchParam = new V2TIMMessageSearchParam();
    v2TIMMessageSearchParam.setConversationID(null);
    v2TIMMessageSearchParam.setKeywordList(keywordList);
    v2TIMMessageSearchParam.setPageSize(10);
    v2TIMMessageSearchParam.setPageIndex(index);
    V2TIMManager.getMessageManager().searchLocalMessages(v2TIMMessageSearchParam, new V2TIMValueCallback<V2TIMMessageSearchResult>() {
        @Override
        public void onSuccess(V2TIMMessageSearchResult v2TIMMessageSearchResult) {
					// Total number of matched conversations to which messages belong
					int totalCount = v2TIMMessageSearchResult.getTotalCount();
					// Calculate the total number of pages, given that 10 messages are displayed per page
					int totalPage = (totalCount % 10 == 0) ? (totalCount / 10) : (totalCount / 10 + 1);
					// Information of messages classified by conversation
					List<V2TIMMessageSearchResultItem> resultItemList = v2TIMMessageSearchResult.getMessageSearchResultItems();
					for (V2TIMMessageSearchResultItem resultItem : resultItemList) {
						// Conversation ID
						String conversationID = resultItem.getConversationID();
						// Total number of messages matching the conversation
						int totalMessageCount = resultItem.getMessageCount();
						// List of messages. If `totalMessageCount` is greater than 1, the list is empty. If `totalMessageCount` is equal to 1, the list contains the current message.
						List<V2TIMMessage> v2TIMMessageList = resultItem.getMessageList();
					}

				@Override
				public void onError(int code, String desc) {}
    });
}

// Load the next page
public void loadMore() {
    searchConversation(++pageIndex);
}
```

**Searching for messages in a specified conversation**
Figure 2 shows the effect of displaying the conversation list, while Figure 3 shows the effect of displaying the list of the messages found in a specified conversation. To avoid memory ballooning, it is strongly recommended that you load the message list with pagination. The implementation method is as follows:
- In the [V2TIMMessageSearchParam](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageSearchParam.html) API, set [conversationID](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageSearchParam.html#ad0beca2cedf96a08d1e44709c16105d7) to the ID of the conversation to search, and set [pageIndex](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageSearchParam.html#ad5e6b317d430d9e0cda8221a5fff6b19) and [pageSize](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageSearchParam.html#a3aca5a82692437f0fb8501533b9f0063) by referring to the settings in the preceding calculation mode.
- In the [V2TIMMessageSearchResult](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageSearchResult.html) API, [totalCount](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageSearchResult.html#a97f66183ea41a7c123bab9dd5313a74a) indicates the total number of messages matched in the conversation, and [messageSearchResultItems](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageSearchResult.html#a6cc0e2f70f0695a74a18a219c31b3ae3) lists only the results in the conversation. In [V2TIMMessageSearchResultItem](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageSearchResultItem.html), [messageCount](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageSearchResultItem.html#a41300a43e3530ab3ba00b61f4337a083) is the number of messages on the current page, and [messageList](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageSearchResultItem.html#aceeced8f371a986511be5c63de354587) is the list of messages on the current page.

**Sample**

```
......
// Calculate the total number of pages, given that 10 messages are displayed per page
int totalMessagePage = (totalMessageCount % 10 == 0) ? (totalMessageCount / 10) : (totalMessageCount / 10 + 1);
......

private void searchMessage(int index) {
	if (index >= totalMessagePage) {
			return;
	}
	List<String> keywordList = new ArrayList<>();
	keywordList.add("test");
	V2TIMMessageSearchParam v2TIMMessageSearchParam = new V2TIMMessageSearchParam();
	v2TIMMessageSearchParam.setConversationID(conversationID);
	v2TIMMessageSearchParam.setKeywordList(keywordList);
	v2TIMMessageSearchParam.setPageSize(10);
	v2TIMMessageSearchParam.setPageIndex(index);
	V2TIMManager.getMessageManager().searchLocalMessages(v2TIMMessageSearchParam, new V2TIMValueCallback<V2TIMMessageSearchResult>() {
			@Override
			public void onSuccess(V2TIMMessageSearchResult v2TIMMessageSearchResult) {
				// Total number of messages matching the conversation
				int totalMessageCount = v2TIMMessageSearchResult.getTotalCount();
				// Calculate the total number of pages, given that 10 messages are displayed per page
				int totalMessagePage = (totalMessageCount % 10 == 0) ? (totalMessageCount / 10) : (totalMessageCount / 10 + 1);
				// Information of the messages on the conversation page
				List<V2TIMMessageSearchResultItem> resultItemList = v2TIMMessageSearchResult.getMessageSearchResultItems();
				for (V2TIMMessageSearchResultItem resultItem : resultItemList) {
					// Conversation ID
					String conversationID = resultItem.getConversationID();
					// Number of messages on the current page
					int totalMessageCount = resultItem.getMessageCount();
					// List of messages on the current page
					List<V2TIMMessage> v2TIMMessageList = resultItem.getMessageList();
			}

			@Override
			public void onError(int code, String desc) {
			}
	});
}

// Load the next page
public void loadMore() {
    searchMessage(++pageIndex);
}
```

## FAQs
### 1. How do I search for custom messages?
Use the [createCustomMessage (byte[] data, String description, byte[] extension)](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a313b1ea616f082f535946c83edd2cc7f) API to create and send a search request. In the request, you need to specify the text to search in the `description` parameter. Custom messages created via the [createCustomMessage (byte[] data)](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a5c2495d4b7ecd66e5636aeb865c17efd) API cannot be searched because the binary data stream passed in by parameters is saved locally.
If you configure the offline push feature and the `description` parameter, custom messages will also be pushed offline, and the content specified in the `description` parameter will be displayed in the notification bar. If offline push is not needed, disable it using [disablePush](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMOfflinePushInfo.html#a5d0ea30668513f45eda447875528b9c7) in [V2TIMOfflinePushInfo](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMOfflinePushInfo.html) in the [sendMessage](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a28e01403acd422e53e999f21ec064795) API. If you do not want to display the searched text in the push notification bar, set other push content using [setDesc](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMOfflinePushInfo.html#a78c8e202aa4e0859468ce40bde6fd602) in [V2TIMOfflinePushInfo](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMOfflinePushInfo.html).

### 2. How do I search for rich media messages?
Rich media messages include file, image, voice, and video messages.
For file messages, the screen usually displays the filename. Therefore, you can set the `fileName` parameter as the searched content when creating messages. If `fileName` is not set, the system gets the filename from `filePath` and saves it to the local storage and the server.
For image, voice, and video messages, the screen usually displays the thumbnail or duration. In this case, you can specify the message type to search by type, but cannot search by keywords.


