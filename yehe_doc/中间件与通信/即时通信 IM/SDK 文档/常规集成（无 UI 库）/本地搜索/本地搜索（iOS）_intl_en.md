Local search is supported starting from Enhanced Edition v5.4.666. To use local search, you need to purchase the Flagship Edition package. For operation details, please see [Purchase Guide](https://intl.cloud.tencent.com/document/product/1047/36021).

## Feature Demonstration
The search API interface consists of three parts: the upper part is for friend search, the middle part is for group and group member search, and the lower part is for message search, where messages are classified by conversation.
[Download and install the app](https://intl.cloud.tencent.com/document/product/1047/34279) to experience it now.

## Integration Guide
### Scheme 1: Integrating TUIKit search source code
#### Step 1. Purchase the package
Purchase the Flagship Edition package by referring to [Purchase Guide](https://intl.cloud.tencent.com/document/product/1047/36021).
#### Step 2. Download source code
[Download source code](https://github.com/tencentyun/TIMSDK) to integrate the TUIKit module. TUIKit supports local search starting from v5.4.666.
```
pod 'TXIMSDK_TUIKit_iOS', ~>'5.4.666'
```
#### Step 3. Initialize TUIKit and log in

```
// Initialize TUIKit
[[TUIKit sharedInstance] setupWithAppId:SDKAPPID];
// Log in to TUIKit
[[TUIKit sharedInstance] login:identifier userSig:sig succ:^{
	// Login succeeded 
} fail:^(int code, NSString *msg) {
   // Login failed
}];
```

#### Step 4. Start the search interface
Enable `TUISearchViewController`.


### Scheme 2: Integrate the IM SDK search API
#### Step 1. Purchase the package
Purchase the Flagship Edition package by referring to [Purchase Guide](https://intl.cloud.tencent.com/document/product/1047/36021).
#### Step 2. Integrate IM SDK Enhance Edition
The IM SDK supports local search starting from v5.4.666.

```
pod 'TXIMSDK_Plus_iOS', ~>'5.4.666'
```

#### Step 3. Call the local user profile search API
You can call the [searchFriends](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#aee1472e90ebbf114878ac98d84fcb85e) API to search for local user profiles. The API supports the following search fields: [userID](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMFriendSearchParam.html#a7cdac10e1b445a630859473344b4ed54), [nickName](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMFriendSearchParam.html#a6b5cf6d9a1e8bb080965b43a6a9dc096), and [remark](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMFriendSearchParam.html#a4d7d3fa58f199f65733f299360305728).

#### Step 4. Call the local group and group member search APIs

You can call the [searchGroups](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#aa29694be71b0ff8ca31f04b557f35431) API to search for the profiles of local groups.
You can call the [searchGroupMembers](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#ab76a8f27aa8e8bd26447da50d58d0bac) API to search for the profiles of local group members. There are two cases, depending on whether the value of `groupIDList` in [V2TIMGroupMemberSearchParam](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMGroupMemberSearchParam.html) is `nil`:

- groupIDList == nil: search the members in all groups, and the returned results will be classified by group ID.
- groupIDList != nil: search the members in a specified group.

#### Step 5. Call the local message search API
You can enter keywords in the search box to call [searchLocalMessages](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a749eade1ce83d6ee1d3f971257141e6c) to search for local messages. There are two cases, depending on whether the value of [conversationID](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMMessageSearchParam.html#a89d34fa0d0d62e831c27ae2a75a37fac) in the [V2TIMMessageSearchParam](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMMessageSearchParam.html) API is `nil`:
- conversationID == nil: search all conversations, and the returned results will be classified by conversation.
- conversationID != nil: search a specified conversation.

**Displaying recent active conversations**
As shown in Figure 1, the bottom part of the search interface is the list of the last 3 conversations to which the messages found belong. The implementation method is as follows:

- In the [V2TIMMessageSearchParam](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMMessageSearchParam.html) API, [conversationID](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMMessageSearchParam.html#a89d34fa0d0d62e831c27ae2a75a37fac) is set to `nil`, indicating that the messages of all conversations are searched; [pageIndex](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMMessageSearchParam.html#a98b1615f1cd990166445b0e876640df8) is set to `0`, indicating data on page 0 of the conversations to which the messages found belong; [pageSize](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMMessageSearchParam.html#a6f9bca9cda8f858a7a3ec3dccccc882c) indicates the number of recent conversations to be returned. Usually, 3 recent conversations are displayed on the UI.
- In the search callback result API [V2TIMMessageSearchResult](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMMessageSearchResult.html), [totalCount](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMMessageSearchResult.html#a2756e7c8275dbe1292df0fbaf470877b) indicates the total number of conversations to which the matched messages belong; [messageSearchResultItems](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMMessageSearchResult.html#a56378d51655fa42d11f93f7bc3d38083) indicates the information of the recent conversations (conversation quantity specified by [pageSize](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMMessageSearchParam.html#a6f9bca9cda8f858a7a3ec3dccccc882c)). In [V2TIMMessageSearchResultItem](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMMessageSearchResultItem.html), [conversationID](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMMessageSearchResultItem.html#a89d34fa0d0d62e831c27ae2a75a37fac) indicates the conversation ID, [messageCount](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMMessageSearchResultItem.html#a3f155494f52d0132a282e73768328042) indicates the total number of messages found in the current conversation, and [messageList](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMMessageSearchResultItem.html#ad966d1fa8e8541c888e4a9b7b493133f) indicates the list of messages found. `messageList` has two cases:
	- If the number of messages found is greater than 1, `messageList` is empty. You can display related chat records (quantity specified by `messageCount`) on the UI.
	- If the number of messages found is equal to 1, `messageList` is the matched message. You can display the message content on the UI and highlight the search keyword, such as **test** in the above figures.

**Sample**

```
  V2TIMMessageSearchParam *param = [[V2TIMMessageSearchParam alloc] init];
  param.keywordList = @[@"test"];
  // Setting `conversationID` to `nil` is to search for messages in all conversations and the results will be classified by conversation
  param.conversationID = nil;
  param.pageIndex = 0;
  param.pageSize = 3;
  [V2TIMManager.sharedInstance searchLocalMessages:param succ:^(V2TIMMessageSearchResult *searchResult) {
      // Total number of matched conversations to which messages belong
      NSInteger totalCount = searchResult.totalCount;
      // Last 3 messages classified by conversation
      NSArray<V2TIMMessageSearchResultItem *> *messageSearchResultItems = searchResult.messageSearchResultItems;
      for (V2TIMMessageSearchResultItem *searchItem in messageSearchResultItems) {
          // Conversation ID
          NSString *conversationID = searchItem.conversationID;
          // Total number of messages matching the conversation
          NSUInteger messageCount = searchItem.messageCount;
          // Message list
          NSArray<V2TIMMessage *> *messageList = searchItem.messageList ?: @[];
      }
  } fail:^(int code, NSString *desc) {
      // fail
  }];
```

**Displaying the list of conversations to which the messages found belong**
For example, you can click **More Chat History** in Figure 1 to redirect to the list of conversations to which the messages found belong, as shown in Figure 2. The search parameters and results are similar to those in the preceding scenario. To avoid memory ballooning, it is strongly recommended that you load the conversation list with pagination. For example, to display 10 conversations as the result, you can set the search parameter API [V2TIMMessageSearchParam](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMMessageSearchParam.html) as follows:

- First call: Set `pageSize` to `10` and `pageIndex` to `0`, and call [searchLocalMessages](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a749eade1ce83d6ee1d3f971257141e6c). Then you can get the total number of conversations from `totalCount` in the callback.
- Page quantity calculation: totalPage = (totalCount % pageSize == 0) ? (totalCount / pageSize) : (totalCount / pageSize + 1)
- Second call: You can specify `pageIndex` (`pageIndex` < `totalPage`) to return the subsequent page number.

**Sample**

```
......
// Calculate the total number of pages, given that 10 messages are displayed per page
NSInteger totalPage = (totalCount % 10 == 0) ? (totalCount / 10) : (totalCount / 10 + 1);
......

- (void)searchConversation:(NSUInteger)index {
    if (index >= totalPage) {
        return;
    }
    V2TIMMessageSearchParam *param = [[V2TIMMessageSearchParam alloc] init];
    param.keywordList = @[@"test"];
    param.conversationID = nil;
    param.pageIndex = index;
    param.pageSize = 10;
    [V2TIMManager.sharedInstance searchLocalMessages:param succ:^(V2TIMMessageSearchResult *searchResult) {
        // Total number of matched conversations to which messages belong
        NSUInteger totalCount = searchResult.totalCount;
        // Calculate the total number of pages, given that 10 messages are displayed per page
        NSUInteger totalPage = (totalCount % 10 == 0) ? (totalCount / 10) : (totalCount / 10 + 1);
        // Information of messages classified by conversation
        NSArray<V2TIMMessageSearchResultItem *> *messageSearchResultItems = searchResult.messageSearchResultItems;
        for (V2TIMMessageSearchResultItem *searchItem in messageSearchResultItems) {
            // Conversation ID
            NSString *conversationID = searchItem.conversationID;
            // Total number of messages matching the conversation
            NSUInteger totalMessageCount = searchItem.messageCount;
            // List of messages. If `totalMessageCount` is greater than 1, the list is empty. If `totalMessageCount` is equal to 1, the list contains the current message.
            NSArray<V2TIMMessage *> *messageList = searchItem.messageList ?: @[];
        }
    } fail:^(int code, NSString *desc) {
        // fail
    }];
}

// Load the next page
- (void)loadMore {
    [self searchConversation:++pageIndex];
}
```

**Searching for messages in a specified conversation**
Figure 2 shows the effect of displaying the conversation list, while Figure 3 shows the effect of displaying the list of the messages found in a specified conversation. To avoid memory ballooning, it is strongly recommended that you load the message list with pagination. The implementation method is as follows:

- In the [V2TIMMessageSearchParam](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMMessageSearchParam.html) API, set [conversationID](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMMessageSearchParam.html#a89d34fa0d0d62e831c27ae2a75a37fac) to the conversation ID, and set [pageIndex](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMMessageSearchParam.html#a98b1615f1cd990166445b0e876640df8) and [pageSize](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMMessageSearchParam.html#a6f9bca9cda8f858a7a3ec3dccccc882c) by referring to the settings in the preceding calculation mode.
- In the [V2TIMMessageSearchResult](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMMessageSearchResult.html) API, [totalCount](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMMessageSearchResult.html#a2756e7c8275dbe1292df0fbaf470877b) indicates the total number of messages matched in the conversation, and [messageSearchResultItems](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMMessageSearchResult.html#a56378d51655fa42d11f93f7bc3d38083) lists only the results in the conversation. In the [V2TIMMessageSearchResultItem](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMMessageSearchResultItem.html) API, [messageCount](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMMessageSearchResultItem.html#a3f155494f52d0132a282e73768328042) is the number of messages on the current page, and [messageList](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMMessageSearchResultItem.html#ad966d1fa8e8541c888e4a9b7b493133f) is the list of messages on the current page.

**Sample**

```
......
// Calculate the total number of pages, given that 10 messages are displayed per page
NSInteger totalMessagePage = (totalMessageCount % 10 == 0) ? (totalMessageCount / 10) : (totalMessageCount / 10 + 1);
......

- (void)searchMessage:(NSUInteger)index {
    if (index >= totalMessagePage) {
            return;
    }
    V2TIMMessageSearchParam *param = [[V2TIMMessageSearchParam alloc] init];
    param.keywordList = @[@"test"];
    param.conversationID = conversationID;
    param.pageIndex = index;
    param.pageSize = 10;
    [V2TIMManager.sharedInstance searchLocalMessages:param succ:^(V2TIMMessageSearchResult *searchResult) {
        // Total number of messages matching the conversation
        NSUInteger totalMessageCount = searchResult.totalCount;
        // Calculate the total number of pages, given that 10 messages are displayed per page
        NSUInteger totalMessagePage = (totalMessageCount % 10 == 0) ? (totalMessageCount / 10) : (totalMessageCount / 10 + 1);
        // Information of the messages on the conversation page
        NSArray<V2TIMMessageSearchResultItem *> *messageSearchResultItems = searchResult.messageSearchResultItems;
        for (V2TIMMessageSearchResultItem *searchItem in messageSearchResultItems) {
            // Conversation ID
            NSString *conversationID = searchItem.conversationID;
            // Number of messages on the current page
            NSUInteger totalMessageCount = searchItem.messageCount;
            // List of messages on the current page
            NSArray<V2TIMMessage *> *messageList = searchItem.messageList ?: @[];
        }
    } fail:^(int code, NSString *desc) {
        // fail
    }];
}

// Load the next page
- (void)loadMore {
    [self searchMessage:++pageIndex];
}
```

## FAQs
### 1. How do I search for custom messages?
Use the [createCustomMessage:desc:extension](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a4395ae33520dcf53da3190d56931852d) API to create and send a search request. In the request, you need to specify the text to search in the `desc` parameter. Custom messages created via the [createCustomMessage](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a7a38c42f63a4e0c9e89f6c56dd0da316) API cannot be searched because the binary data stream passed in by parameters is saved locally.
If you configure the offline push feature and the `desc` parameter, custom messages will also be pushed offline, and the content specified in the `desc` parameter will be displayed in the notification bar. If offline push is not needed, disable it using [disablePush](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMOfflinePushInfo.html#a7df0e95cb5cd8567cf04c287649157b9) in [V2TIMOfflinePushInfo](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMOfflinePushInfo.html) in the [sendMessage](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a681947465d6ab718da40f7f983740a21) API. If you do not want to display the searched text in the push notification bar, set other push content using [desc](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMOfflinePushInfo.html#aca3d09a4807ffc6486d556c055605c41) in [V2TIMOfflinePushInfo](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMOfflinePushInfo.html).

### 2. How do I search for rich media messages?
Rich media messages include file, image, voice, and video messages.
For file messages, the screen usually displays the filename. Therefore, you can set the `fileName` parameter as the searched content when creating messages. If `fileName` is not set, the system gets the filename from `filePath` and saves it to the local storage and the server.
For image, voice, and video messages, the screen usually displays the thumbnail or duration. In this case, you can specify the message type to search by type, but cannot search by keywords.


