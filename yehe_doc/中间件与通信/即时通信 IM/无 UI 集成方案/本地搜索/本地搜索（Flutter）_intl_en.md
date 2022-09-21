## Feature Demonstration
For the feature effect, see [Android SDK Tuikit](https://intl.cloud.tencent.com/document/product/1047/41795).

## Integration Guide
### Step 1. Purchase the package
Upgrade to the Flagship Edition package by referring to [Purchase Guide](https://intl.cloud.tencent.com/document/product/1047/36021).

### Step 2. Call the local user profile search API
You can call the [searchFriends](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/searchFriends.html) API to search for local user profiles. The API parameter [searchParams](https://pub.dev/documentation/tencent_im_sdk_plugin_platform_interface/latest/models_v2_tim_friend_search_param/V2TimFriendSearchParam-class.html) supports the search fields `nickName`, `userID`, and `remark`. You can use this API to implement the friend search feature, such as searching for friends' nicknames.

```dart
 V2TimFriendSearchParam searchParam = new V2TimFriendSearchParam(
        keywordList: ["Your keyword"],
        isSearchUserID: true,  // Whether to include `userId` in the search
        isSearchNickName: true, // Whether to include `nickName` in the search
        isSearchRemark: true); // Whether to include `remark` in the search
    var res = await TencentImSDKPlugin.v2TIMManager
        .getFriendshipManager()
        .searchFriends(searchParam: searchParam);
```

### Step 3. Call the local group and group member search APIs

You can call the [searchGroups](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_group_manager/V2TIMGroupManager/searchGroups.html) API to search for the profiles of local groups.
You can call the [searchGroupMembers](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_group_manager/V2TIMGroupManager/searchGroupMembers.html) API to search for the profiles of local group members. There are two cases, depending on whether the value of `groupIDList` in [V2TimGroupMemberSearchParam](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Group/V2TimGroupMemberSearchParam.html) is `null`:
- groupIDList == null: search the members in all groups, and the returned results will be classified by group ID.
- groupIDList != null: search the members in a specified group.


### Step 4. Call the local message search API
You can enter keywords in the search box to call [searchLocalMessages](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_message_manager/V2TIMMessageManager/searchLocalMessages.html) to search for local messages. There are two cases, depending on whether the value of [conversationID](https://pub.dev/documentation/tencent_im_sdk_plugin_platform_interface/latest/models_v2_tim_message_search_param/V2TimMessageSearchParam/conversationID.html) in [V2TIMMessageSearchParam](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Message/V2TimMessageSearchParam.html) is `null`:
- conversationID == null: search all conversations, and the returned results will be classified by conversation.
- conversationID != null: search a specified conversation.   

**Displaying recent active conversations**
The list of the recent conversations to which the messages found belong is implemented as follows:
- In the [V2TimMessageSearchParam](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Message/V2TimMessageSearchParam.html) API, [conversationID](https://pub.dev/documentation/tencent_im_sdk_plugin_platform_interface/latest/models_v2_tim_message_search_param/V2TimMessageSearchParam/conversationID.html) is set to `null`, indicating the messages of all conversations are searched;[pageIndex](https://pub.dev/documentation/tencent_im_sdk_plugin_platform_interface/latest/models_v2_tim_message_search_param/V2TimMessageSearchParam/pageIndex.html) is set to `0`, indicating data on page 0 of the conversations to which the messages found belong; [pageSize](https://pub.dev/documentation/tencent_im_sdk_plugin_platform_interface/latest/models_v2_tim_message_search_param/V2TimMessageSearchParam/pageSize.html) indicates the number of recent conversations to be returned.
- In the search callback result API [V2TimMessageSearchResult](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Message/V2TimMessageSearchResult.html), `totalCount` indicates the total number of conversations to which the matched messages belong; [messageSearchResultItems](https://pub.dev/documentation/tencent_im_sdk_plugin_platform_interface/latest/models_v2_tim_message_search_result/V2TimMessageSearchResult/messageSearchResultItems.html) indicates the information of the recent conversations (conversation quantity specified by [pageSize](https://pub.dev/documentation/tencent_im_sdk_plugin_platform_interface/latest/models_v2_tim_message_search_param/V2TimMessageSearchParam/pageSize.html)). In [V2TimMessageSearchResultItem](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Message/V2TimMessageSearchResultItem.html), `conversationID` indicates the conversation ID, `messageCount` indicates the total number of messages found in the current conversation, and `messageList` indicates the list of messages found. When searching for messages in `all conversations`, `messageList` has two cases:
	- If the number of messages found is greater than 1, `messageList` is empty. You can display related chat records (quantity specified by `messageCount`) on the UI.
	- If the number of messages found is equal to 1, `messageList` is the matched message. You can display the message content on the UI and highlight the search keyword, such as **test** in the above figures.
When searching for messages in `a specified conversation`, `messageList` lists all eligible messages in the specified conversation.

**Sample**

```dart
    V2TimMessageSearchParam searchParam = V2TimMessageSearchParam(
      keywordList: [keyword],
      type:1, // Corresponds to the V2TIMKeywordListMatchType.KEYWORD_LIST_MATCH_TYPE_AND SDK-layer processing. Indicates the OR or AND relationship.
      pageSize: 50, 
      pageIndex: 0, 
      conversationID: null, // Setting `conversationID` to `null` is to search for messages in all conversations.
    );
    V2TimValueCallback<V2TimMessageSearchResult> res = await TencentImSDKPlugin.v2TIMManager
        .getMessageManager()
        .searchLocalMessages(searchParam: searchParam);
```

**Displaying the list of conversations to which the messages found belong**
![](https://qcloudimg.tencent-cloud.cn/raw/2577ec15dbdae9d8978ea82c4c120cfe.png)
For example, you can click **More Chat History** in Figure 1 to redirect to the list of conversations to which the messages found belong, as shown in Figure 2. The search parameters and results are similar to those in the preceding scenario. To avoid memory ballooning, it is strongly recommended that you load the conversation list with pagination. For example, to display the search results by 10 conversations per page you can set the search parameter API [V2TIMMessageSearchParam](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Message/V2TimMessageSearchParam.html) as follows:

- First call: Set `pageSize` to `10` and `pageIndex` to `0`, and call [searchLocalMessages](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_message_manager/V2TIMMessageManager/searchLocalMessages.html). Then you can get the total number of conversations from `totalCount` in the callback.
- Page quantity calculation: totalPage = (totalCount % pageSize == 0) ? (totalCount / pageSize) : (totalCount / pageSize + 1)
- Second call: You can specify `pageIndex` (`pageIndex` < `totalPage`) to return the subsequent page number.

  

**Sample**

```dart
......
static int totalCount = 0;
int index = 0;
// Calculate the total number of pages, given that 10 messages are displayed per page
 double totalPage = (totalCount % 10 == 0) ? (totalCount / 10) : (totalCount / 10 + 1);
......
    searchLocaltMessage(int index) async {
    if (index >= totalPage) {
      return;
    }

    V2TimMessageSearchParam searchParam = V2TimMessageSearchParam(
      keywordList: ["Your keyword"],
      type:
          1, // Corresponds to the V2TIMKeywordListMatchType.KEYWORD_LIST_MATCH_TYPE_AND SDK-layer processing. Indicates the OR or AND relationship.
      pageSize: 10,
      pageIndex: index,
      conversationID: null, // Setting `conversationID` to `null` is to search for messages in all conversations.
    );
    V2TimValueCallback<V2TimMessageSearchResult> res = await TencentImSDKPlugin
        .v2TIMManager
        .getMessageManager()
        .searchLocalMessages(searchParam: searchParam);
    // Total number of messages matching the conversation
    totalCount = res.data?.totalCount ?? 0;
    List<V2TimMessageSearchResultItem> list =
        res.data!.messageSearchResultItems!;
    totalPage =
        (totalCount % 10 == 0) ? (totalCount / 10) : (totalCount / 10 + 1);
    for (V2TimMessageSearchResultItem resultItem in list) {
      // Conversation ID
      String conversationID = resultItem.conversationID!;
      // Total number of messages matching the conversation
      int totalMessageCount = resultItem.messageCount!;
      // List of messages. If `totalMessageCount` is greater than 1, the list is empty. If `totalMessageCount` is equal to 1, the list contains the current message.
      List<V2TimMessage> v2TIMMessageList = resultItem.messageList!;
      // ...
    }
  }

  void loadMore() {
    index = index++;
    searchLocaltMessage(index);
  }

```

**Searching for messages in a specified conversation**
The following introduces how to search for messages in a specified conversation. To avoid memory ballooning, it is strongly recommended that you load the message list with pagination. The implementation method is as follows:
- In the [V2TimMessageSearchParam](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Message/V2TimMessageSearchParam.html) API, set `conversationID` to the ID of the conversation to search, and set `pageIndex` and `pageSize` by referring to the settings in the preceding calculation mode.
- In the [V2TimMessageSearchResult](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Message/V2TimMessageSearchResult.html) API, `totalCount` indicates the total number of messages matched in the conversation, and [messageSearchResultItems](https://pub.dev/documentation/tencent_im_sdk_plugin_platform_interface/latest/models_v2_tim_message_search_result/V2TimMessageSearchResult/messageSearchResultItems.html) lists only the results in the conversation. In [V2TIMMessageSearchResultItem](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Message/V2TimMessageSearchResultItem.html), `messageCount` is the number of messages on the current page, and `messageList` is the list of messages on the current page.

**Sample**

```dart
......
static int totalCount = 0;
int index = 0;
// Calculate the total number of pages, given that 10 messages are displayed per page
 double totalPage = (totalCount % 10 == 0) ? (totalCount / 10) : (totalCount / 10 + 1);
......
    searchLocaltMessage(int index) async {
    if (index >= totalPage) {
      return;
    }

    V2TimMessageSearchParam searchParam = V2TimMessageSearchParam(
      keywordList: ["Your keyword"],
      type:
          1, // Corresponds to the V2TIMKeywordListMatchType.KEYWORD_LIST_MATCH_TYPE_AND SDK-layer processing. Indicates the OR or AND relationship.
      pageSize: 10,
      pageIndex: index,
      conversationID: "ID of the conversation for message searching", // Specify the conversation ID
    );
    V2TimValueCallback<V2TimMessageSearchResult> res = await TencentImSDKPlugin
        .v2TIMManager
        .getMessageManager()
        .searchLocalMessages(searchParam: searchParam);
    // Total number of messages matching the conversation
    totalCount = res.data?.totalCount ?? 0;
    List<V2TimMessageSearchResultItem> list =
        res.data!.messageSearchResultItems!;
    totalPage =
        (totalCount % 10 == 0) ? (totalCount / 10) : (totalCount / 10 + 1);
    for (V2TimMessageSearchResultItem resultItem in list) {
      // Conversation ID
      String conversationID = resultItem.conversationID!;
      // Total number of messages matching the conversation
      int totalMessageCount = resultItem.messageCount!;
      // List of messages. If `totalMessageCount` is greater than 1, the list is empty. If `totalMessageCount` is equal to 1, the list contains the current message.
      List<V2TimMessage> v2TIMMessageList = resultItem.messageList!;
      // ...
    }
  }

  void loadMore() {
    index = index++;
    searchLocaltMessage(index);
  }

```

## FAQs
### 1. How do I search for custom messages?
Use the [createCustomMessage({required String data,String desc,String extension})](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMMessageManager/createCustomMessage.html) API to create and send a search request. In the request, you need to specify the text to search in the `desc` parameter. Custom messages created via the [createCustomMessage (required String data)](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMMessageManager/createCustomMessage.html) API cannot be searched because the binary data stream passed in by parameters is saved locally.
If you configure the offline push feature and the `description` parameter, custom messages will also be pushed offline, and the content specified in the `description` parameter will be displayed in the notification bar. If offline push is not needed, disable it using [disablePush](https://pub.dev/documentation/tencent_im_sdk_plugin_platform_interface/latest/models_v2_tim_offline_push_info/V2TimOfflinePushInfo/disablePush.html) in [V2TIMOfflinePushInfo](https://pub.dev/documentation/tencent_im_sdk_plugin_platform_interface/latest/models_v2_tim_offline_push_info/V2TimOfflinePushInfo-class.html) of the [sendMessage](https://pub.dev/documentation/tencent_im_sdk_plugin/latest/manager_v2_tim_message_manager/V2TIMMessageManager/sendMessage.html) API. If you do not want to display the searched text in the push notification bar, set other push content using [desc](https://pub.dev/documentation/tencent_im_sdk_plugin_platform_interface/latest/models_v2_tim_offline_push_info/V2TimOfflinePushInfo/desc.html) in [V2TIMOfflinePushInfo](https://pub.dev/documentation/tencent_im_sdk_plugin_platform_interface/latest/models_v2_tim_offline_push_info/V2TimOfflinePushInfo-class.html).

### 2. How do I search for rich media messages?
Rich media messages include file, image, voice, and video messages.
For file messages, the screen usually displays the filename. Therefore, you can set the `fileName` parameter as the searched content when creating messages. If `fileName` is not set, the system gets the filename from `filePath` and saves it to the local storage and the server. Note that file messages cannot be searched in the web SDK. For image, voice, and video messages, the screen usually displays the thumbnail or duration. In this case, you can specify the message type to search by type, but cannot search by keywords.
