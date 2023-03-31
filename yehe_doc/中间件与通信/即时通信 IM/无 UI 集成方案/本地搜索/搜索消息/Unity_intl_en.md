## Feature Description
Only local messages can be searched for, for example, received messages or historical messages obtained after the API is called.

> ? This feature is supported only by the Ultimate edition.
>

## Message Search Class
### Message search parameter class
The message search parameter class is `MessageSearchParam` ([Details](https://comm.qq.com/im/doc/unity/en/types/MessageAttributes/MessageSearchParam.html)). When searching for messages, the SDK will execute different search logics based on the object settings.

The `MessageSearchParam` parameters are as described below:

| Parameter                                | Definition                                                   | Description                                                  |
| ---------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| msg_search_param_keyword_array           | Keyword list                                                 | It can contain up to five keywords. When the message sender and the message type are not specified, the keyword list must be set; in other cases, it can be left empty. |
| msg_search_param_keyword_list_match_type | Match type of the keyword list                               | It can be set to `OR` or `AND`. Valid values: TIMKeywordListMatchType_Or (default), TIMKeywordListMatchType_And. |
| msg_search_param_send_indentifier_array  | `userID` who sent messages                                   | It can contain up to five user IDs.                          |
| msg_search_param_message_type_array      | Set of the message types to be searched for                  | If it is left empty, messages of all the supported types (excluding `FaceElem` and `GroupTipsElem`) will be searched for. For more information on the values of other types, see `TIMElemType` ([Details](https://comm.qq.com/im/doc/unity/en/enums/TIMElemType.html)). |
| msg_search_param_conv_id                 | Whether to search all the conversations or the specified conversation | If it is not left empty, the specified conversation will be searched. |
| msg_search_param_search_time_position    | Start time for the search                                    | It is `0` by default, indicating to search from the current time point. It is a UTC timestamp in seconds. |
| msg_search_param_search_time_period      | A past period of time starting from the start time           | It is `0` by default, indicating not to limit the time range. It is in seconds. `24x60x60` represents a past day. |
| msg_search_param_page_index              | Page number                                                  | It is used to display the search result by page. `0` indicates the first page. |
| msg_search_param_page_size               | Number of result items per page                              | It is used to display the search result by page. Set it to `0` if you don't want paged display. If too many result items are pulled at a time, a performance problem may occur. |

### Message search result class
The message search result class is `MessageSearchResult` ([Details](https://comm.qq.com/im/doc/unity/en/types/MessageAttributes/MessageSearchResult.html)). The parameters are as described below:

| Parameter                     | Definition                              | Description                                                  |
| ----------------------------- | --------------------------------------- | ------------------------------------------------------------ |
| msg_search_result_total_count | Total number of the search result items | If the specified conversation is searched, the **total number of messages** that meet the search criteria will be returned.<br>If all the conversations are searched, the **total number of the conversations** to which messages that meet the search criteria belong will be returned. |
| msg_search_result_item_array  | Match type of the keyword list          | If the specified conversation is searched, only the result items in the conversation will be included in the returned result list.<br>If all the conversations are searched, messages that meet the search criteria will be grouped by conversation ID and returned by page. |

Here, `msg_search_result_item_array` is a list that contains the `MessageSearchResultItem` objects ([Details](https://comm.qq.com/im/doc/unity/en/types/MessageAttributes/MessageSearchResultItem.html)). The parameters are as described below:

| Parameter                                  | Definition                                     | Description                                                  |
| ------------------------------------------ | ---------------------------------------------- | ------------------------------------------------------------ |
| msg_search_result_item_conv_id             | Conversation ID                                | –                                                            |
| msg_search_result_item_total_message_count | Number of messages                             | Number of messages that meet the search criteria and are found in the current conversation. |
| messageList                                | List of messages that meet the search criteria | If the specified conversation is searched, `messageList` is the list of messages in the conversation that meet the search criteria.<br>If all the conversations are searched, `messageList` may display either of the following results:<br>* If the number of matched messages in a conversation is greater than 1, `messageList` is empty, and you can display "{messageCount} relevant records" on the UI.<br>* If the number of matched messages in a conversation is equal to 1, `messageList` is the matched message, and you can display it on the UI and highlight the matched keyword. |
| msg_search_result_item_conv_type           | Conversation type                              | `TIMConvType` ([Details](https://comm.qq.com/im/doc/unity/en/enums/TIMConvType.html)) |


## Searching for the Messages in All the Conversations
When a user enters a keyword in the search box to search for messages, you can call `MsgSearchLocalMessages` ([Details](https://comm.qq.com/im/doc/unity/en/api/MessageApi/MsgSearchLocalMessages.html)) to search for local messages of the IM SDK.

If you want to search all the conversations, you only need to leave `msg_search_param_conv_id` in `MessageSearchParam` empty (`null`) or unspecified.

Sample code:


```c#
// Search for local messages by keyword
MessageSearchParam param = new MessageSearchParam
{
  msg_search_param_keyword_array = new List<string>
  {
    "Keyword 1"
  },
  msg_search_param_page_index = 0,
  msg_search_param_page_size = 10,
  msg_search_param_conv_type = TIMConvType.kTIMConv_C2C
};
TIMResult res = TencentIMSDK.MsgSearchLocalMessages(param, (int code, string desc, MessageSearchResult result, string user_data)=>{
 // Process the async logic
});
```


## Searching for the Messages in the Specified Conversation
When a user enters a keyword in the search box to search for messages, you can call `MsgSearchLocalMessages` ([Details](https://comm.qq.com/im/doc/unity/en/api/MessageApi/MsgSearchLocalMessages.html)) to search for local messages of the IM SDK.

Sample code:


```c#
// Search for local messages by conversation ID and keyword
MessageSearchParam param = new MessageSearchParam
{
  msg_search_param_keyword_array = new List<string>
  {
    "Keyword 1"
  },
  msg_search_param_page_index = 0,
  msg_search_param_page_size = 10,
  msg_search_param_conv_id = "group_id"
};
TIMResult res = TencentIMSDK.MsgSearchLocalMessages(param, (int code, string desc, MessageSearchResult result, string user_data)=>{
 // Process the async logic
});
```
