## Feature Description
Local message search is a feature essential for the application's improved user experience. It allows users to quickly and conveniently find the expected information from massive amounts of complex data. It can also be used as an operations tool to easily and efficiently navigate to extensive content.
>?
>- Only local messages can be searched for, for example, received messages or historical messages obtained after the API is called. 
>- This feature is supported only by the SDK for Flutter on v3.8.0 or later.
>- The local message search feature is only available on the IM Ultimate edition. To use it, purchase the [Ultimate edition](https://www.tencentcloud.com/document/product/1047/34577#.E5.8D.87.E7.BA.A7.E5.BA.94.E7.94.A8). For more information, see [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350).
>)。

## Message Search Class
### Message search parameter class
The message search parameter class is `V2TimMessageSearchParam` ([Details](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Message/V2TimMessageSearchParam.html)). When searching for messages, the SDK will execute different search logics based on the object settings.

The `V2TIMMessageSearchParam` parameters are as described below:

| Parameter            | Definition                                                   | Description                                                  |
| -------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| keywordList          | Keyword list                                                 | It can contain up to five keywords. When the message sender and the message type are not specified, the keyword list must be set; in other cases, it can be left empty. |
| keywordListMatchType | Match type of the keyword list                               | It can be set to `OR` or `AND`. Valid values: V2TIM_KEYWORD_LIST_MATCH_TYPE_OR (default), V2TIM_KEYWORD_LIST_MATCH_TYPE_AND. |
| senderUserIDList     | `userID` who sent messages                                   | It can contain up to five user IDs.                          |
| messageTypeList      | Set of the message types to be searched for                  | If it is left empty, messages of all the supported types (excluding `V2TIMFaceElem` and `V2TIMGroupTipsElem`) will be searched for. For more information on the values of other types, see `V2TIMElemType` ([Details](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Message/V2TimMessage.html#elemtype)). |
| conversationID       | Whether to search all the conversations or the specified conversation | If it is left empty, all the conversations will be searched; otherwise, the specified conversation will be searched. |
| searchTimePosition   | Start time for the search                                    | It is `0` by default, indicating to search from the current time point. It is a UTC timestamp in seconds. |
| searchTimePeriod     | A past period of time starting from the start time           | It is `0` by default, indicating not to limit the time range. It is in seconds. `24x60x60` represents a past day. |
| pageIndex            | Page number                                                  | It is used to display the search result by page. `0` indicates the first page. |
| pageSize             | Number of result items per page                              | It is used to display the search result by page. Set it to `0` if you don't want paged display. If too many result items are pulled at a time, a performance problem may occur. |

### Message search result class
The message search result class is `V2TIMMessageSearchResult` ([Details](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Message/V2TimMessageSearchResult.html)). The parameters are as described below:

| Parameter                | Definition                              | Description                                                  |
| ------------------------ | --------------------------------------- | ------------------------------------------------------------ |
| totalCount               | Total number of the search result items | If the specified conversation is searched, the **total number of messages** that meet the search criteria will be returned.<br>If all the conversations are searched, the **total number of the conversations** to which messages that meet the search criteria belong will be returned. |
| messageSearchResultItems | Match type of the keyword list          | If the specified conversation is searched, only the result items in the conversation will be included in the returned result list.<br>If all the conversations are searched, messages that meet the search criteria will be grouped by conversation ID and returned by page. |

Here, `messageSearchResultItems` is a list that contains the `V2TIMMessageSearchResultItem` objects ([Details](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Message/V2TimMessageSearchResultItem.html)). The parameters are as described below:

| Parameter      | Definition                                     | Description                                                  |
| -------------- | ---------------------------------------------- | ------------------------------------------------------------ |
| conversationID | Conversation ID                                | –                                                            |
| messageCount   | Number of messages                             | Number of messages that meet the search criteria and are found in the current conversation. |
| messageList    | List of messages that meet the search criteria | If the specified conversation is searched, `messageList` is the list of messages in the conversation that meet the search criteria.<br>If all the conversations are searched, `messageList` may display either of the following results:<br>* If the number of matched messages in a conversation is greater than 1, `messageList` is empty, and you can display "{messageCount} relevant records" on the UI.<br>* If the number of matched messages in a conversation is equal to 1, `messageList` is the matched message, and you can display it on the UI and highlight the matched keyword. |


## Searching for the Messages in All the Conversations
When a user enters a keyword in the search box to search for messages, you can call `searchLocalMessages` ([Details](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMMessageManager/searchLocalMessages.html)) to search for local messages of the IM SDK.

If you want to search for all the conversations, you only need to leave `conversationID` in `V2TIMMessageSearchParam` empty (`null`/`nil`) or unspecified.

Sample code:


```dart
// Search for local messages by keyword
V2TimValueCallback<V2TimMessageSearchResult> searchMessage = await messageManager.searchLocalMessages(searchParam: V2TimMessageSearchParam(keywordList: ['Keyword 1'],pageIndex: 0,pageSize: 10,type: 1));
```


## Searching for the Messages in the Specified Conversation
When a user enters a keyword in the search box to search for messages, you can call `searchLocalMessages` ([Details](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMMessageManager/searchLocalMessages.html)) to search for local messages of the IM SDK.

Sample code:


```dart
// Search for local messages by conversation ID and keyword
V2TimValueCallback<V2TimMessageSearchResult> searchMessage = await messageManager.searchLocalMessages(searchParam: V2TimMessageSearchParam(keywordList: ['Keyword 1'],pageIndex: 0,pageSize: 10,type: 1,conversationID:'conversationID'));
```



## Typical Use Cases for the Search
In general IM chat software, a search UI is usually displayed as follows:

| Figure 1. Chat history                                       | Figure 2. More chat history                                  | Figure 3. Messages in the specified conversation             |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| <img src="https://qcloudimg.tencent-cloud.cn/raw/51cdbb15e8e730967932e340a4565aae.png" alt="" style="zoom:40%;" /> | <img src="https://qcloudimg.tencent-cloud.cn/raw/1230eb47eb30e49e387178a2ae459361.png" alt="" style="zoom:40%;" /> | <img src="https://qcloudimg.tencent-cloud.cn/raw/56ea202d7de75b40e7fd4bd6e19682f1.png" alt="" style="zoom:50%;" /> |

The following describes how to implement the above scenarios through IM SDK's search APIs.

### Displaying the latest active conversations
As shown in Figure 1, a list of the latest three conversations to which the messages found belong is displayed at the bottom. The implementation method is as follows:
1. Set the search parameter `V2TIMMessageSearchParam`.
   * Set `conversationID` to `null`, which indicates to search all the conversations.
   * Set `pageIndex` to `0`, which indicates the first page of the conversations to which the messages found belong.
   * Set `pageSize` to `3`, which indicates the number of the latest conversations to be returned. Generally, the latest three conversations will be displayed on the UI.

2. Process the search callback result `V2TIMMessageSearchResult`.
   * `totalCount` indicates the number of all the conversations to which the matched messages belong.
   * The `messageSearchResultItems` list contains the information of the latest three conversations (that is, the `pageSize` parameter). Here, `messageCount` of the `V2TIMMessageSearchResultItem` element indicates the total number of messages found in the current conversation.
   * If the number of messages found is greater than 1, `messageList` is empty, and you can display "4 relevant records" on the UI. Here, `4` is `messageCount`.
   * If the number of messages found is equal to 1, `messageList` is the matched message, and you can display it on the UI and highlight the search keyword, for example, "test" in the above figure.


Sample code:



```dart
// Search for messages of a specified type through `messageTypeList`
V2TimValueCallback<V2TimMessageSearchResult> searchMessage = await messageManager.searchLocalMessages(searchParam: V2TimMessageSearchParam(keywordList: ['Keyword 1'],pageIndex: 0,pageSize: 10,type: 1,conversationID: "",messageTypeList: [MessageElemType.V2TIM_ELEM_TYPE_TEXT]));
```


## Searching for a Custom Message
In general, if you call the `createCustomMessage(data)` API ([Details](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMMessageManager/createCustomMessage.html)) to create a custom message, the message cannot be found, as the SDK will save it as a binary data stream.

To enable a user to find a custom message, you need to call the `createCustomMessage(data, description, extension)` API [dart](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMMessageManager/createCustomMessage.html) to create and send the custom message and put the text to be searched for in the `description` parameter.

If you have configured the offline push feature, after the `description` parameter is set, the custom message will be pushed offline, and the parameter content will be displayed on the notification bar.
If you don't need offline push, you can use the `disablePush` in the `V2TIMOfflinePushInfo` parameter of the `sendMessage` API ([Details](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMMessageManager/sendMessage.html)).

If you don't want to display the content pushed on the notification bar as the text to be searched for, you can use `desc` in the `V2TIMOfflinePushInfo` parameter to set the push content.


## Searching for a Rich Media Message
Rich media messages include file, image, audio, and video messages.

For a file message, the filename is usually displayed on the UI. If you pass in the `fileName` parameter when calling `createFileMessage` to create a file message, `fileName` will be used as the content to be searched for and match the search keyword. If `fileName` is not set, the SDK will automatically extract the filename from `filePath` as the content to be searched for.
Both `fileName` and `filePath` will be saved in the local database and on the server, which can be searched for after being pulled on another device.

For image, audio, and video messages, there is no such name as `fileName`, and a thumbnail or duration is usually displayed on the UI; in this case, `keywordList` is invalid.
To enable a user to find such messages, you can specify `messageTypeList` as `V2TIM_ELEM_TYPE_IMAGE`/`V2TIM_ELEM_TYPE_SOUND`/`V2TIM_ELEM_TYPE_VIDEO` for categorized search.
