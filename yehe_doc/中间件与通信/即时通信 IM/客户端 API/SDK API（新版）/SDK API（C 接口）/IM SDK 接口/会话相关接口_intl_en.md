Two types of Conversation are available:
- C2C conversation: a one-to-one chat between you and another user. Messages are read and sent through the conversation.
- Group conversation: a group chat among group members. All group members can receive messages sent in the group conversation.


## TIMConvCreate

This API is used to create a conversation. (This API is to be disused. The IM SDK will automatically create conversations for message sending and receiving. No manual creation is required.)

**Prototype**

```c
TIM_DECL int TIMConvCreate(const char* conv_id, enum TIMConvType conv_type, TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type             | Description                                                  |
| --------- | ---------------- | ------------------------------------------------------------ |
| conv_id   | const char\*     | Conversation ID.                                             |
| conv_type | enum TIMConvType | Conversation type. For more information, see [TIMConvType](https://intl.cloud.tencent.com/document/product/1047/34551). |
| cb        | TIMCommCallback  | Callback function for conversation creation. For more information about the callback function definition, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data | const void\*     | User-defined data. The IM SDK only transfers the user data to the callback function `cb` without processing the data. |

**Return values**

| Type | Description                                                  |
| ---- | ------------------------------------------------------------ |
| int  | If `TIM_SUCC` is returned, the API was successfully called. (The callback `cb` is called only when the API returns `TIM_SUCC`.) If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

>?
>- A conversation is a one-to-one or group chat, through which messages are sent and received between you and another user or in a group.
>- This API creates a conversation or obtains conversation information. The conversation type (group or one-to-one chat) and the conversation party identifier (the conversation party's account or group ID) need to be specified. Conversation information is returned through the callback function `cb`.


**Example 1: obtaining a one-to-one chat with a party whose UserID is Windows-02**

```c
const void* user_data = nullptr; // Returned by the callback function
const char* userid = "Windows-02";
int ret = TIMConvCreate(userid, kTIMConv_C2C, [](int32_t code, const char* desc, const char* json_param, const void* user_data) {
    if (ERR_SUCC != code) {
        return;
    }
    // The callback returns detailed information about the conversation
}, user_data);
if (ret != TIM_SUCC) {
    // Failed to call the `TIMConvCreate` API
}
```


**Example 2: obtaining a group chat with the group ID set to Windows-Group-01**

```c
const void* user_data = nullptr; // Returned by the callback function
const char* userid = "Windows-Group-01";
int ret = TIMConvCreate(userid, kTIMConv_Group, [](int32_t code, const char* desc, const char* json_param, const void* user_data) {
    if (ERR_SUCC != code) {
        return;
    }
    // The callback returns detailed information about the conversation
}, user_data);
if (ret != TIM_SUCC) {
    // Failed to call the `TIMConvCreate` API
}
```


## TIMConvDelete

This API is used to delete a conversation.

**Prototype**

```c
TIM_DECL int TIMConvDelete(const char* conv_id, enum TIMConvType conv_type, TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type             | Description                                                  |
| --------- | ---------------- | ------------------------------------------------------------ |
| conv_id   | const char\*     | Conversation ID.                                             |
| conv_type | enum TIMConvType | Conversation type. For more information, see [TIMConvType](https://intl.cloud.tencent.com/document/product/1047/34551). |
| cb        | TIMCommCallback  | Callback function for indicating whether a conversation is deleted. For more information about the callback function definition, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data | const void\*     | User-defined data. The IM SDK only transfers the user data to the callback function `cb` without processing the data. |

**Return values**

| Type | Description                                                  |
| ---- | ------------------------------------------------------------ |
| int  | If `TIM_SUCC` is returned, the API was successfully called. (The callback `cb` is called only when the API returns `TIM_SUCC`.) If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

>?This API is used to delete a conversation. Whether a conversation is successfully deleted is returned through the callback.


## TIMConvGetConvList

This API is used to obtain the conversation list of recent contacts.

**Prototype**

```c
TIM_DECL int TIMConvGetConvList(TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type            | Description                                                  |
| --------- | --------------- | ------------------------------------------------------------ |
| cb        | TIMCommCallback | Callback function for obtaining the conversation list of recent contacts. For more information about the callback function definition, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data | const void\*    | User-defined data. The IM SDK only transfers the user data to the callback function `cb` without processing the data. |

**Return values**

| Type | Description                                                  |
| ---- | ------------------------------------------------------------ |
| int  | If `TIM_SUCC` is returned, the API was successfully called. (The callback `cb` is called only when the API returns `TIM_SUCC`.) If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

## TIMConvGetConvInfo

This API is used to query the list of conversations.

**Prototype**

```c
TIM_DECL int TIMConvGetConvInfo(const char* json_get_conv_list_param, TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter                | Type            | Description                                                  |
| ------------------------ | --------------- | ------------------------------------------------------------ |
| json_get_conv_list_param | const char\*    | List of conversation IDs and types.                          |
| cb                       | TIMCommCallback | Callback function for obtaining the conversation list. For more information about the callback function definition, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data                | const void\*    | User-defined data. The IM SDK only transfers the user data to the callback function `cb` without processing the data. |

**Return values**

| Type | Description                                                  |
| ---- | ------------------------------------------------------------ |
| int  | If `TIM_SUCC` is returned, the API was successfully called. (The callback `cb` is called only when the API returns `TIM_SUCC`.) If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

**Example**

```c
Json::Object json_obj;
json_obj[kTIMGetConversationListParamConvId] = "98826";
json_obj[kTIMGetConversationListParamConvType] = kTIMConv_C2C;

Json::Array json_arry;
json_arry.append(json_obj);

TIMConvGetConvInfo(json_arry.toStyledString().c_str(),
   [](int32_t code, const char* desc, const char* json_param, const void* user_data) {
   printf("TIMConvGetConvInfo|code:%d|desc:%s\n", code, desc);
}, nullptr);

// Example of `json_params`. For details, see [ConvInfo](TIMCloudDef.h).
[{
  "conv_active_time": 5,
  "conv_id": "98826",
  "conv_is_has_draft": false,
  "conv_is_has_lastmsg": true,
  "conv_is_pinned": false,
  "conv_last_msg": {
      "message_client_time": 1620877708,
      "message_conv_id": "98826",
      "message_conv_type": 1,
      "message_custom_int": 0,
      "message_custom_str": "",
      "message_elem_array": [{
          "elem_type": 0,
          "text_elem_content": "11111"
  }],
      "message_is_from_self": false,
      "message_is_online_msg": false,
      "message_is_peer_read": false,
      "message_is_read": false,
      "message_msg_id": "144115233874815003-1620877708-1038050731",
      "message_platform": 0,
      "message_priority": 1,
      "message_rand": 1038050731,
      "message_sender": "98826",
      "message_sender_profile": {
          "user_profile_add_permission": 1,
          "user_profile_birthday": 0,
          "user_profile_custom_string_array": [],
          "user_profile_face_url": "test1-www.google.com",
          "user_profile_gender": 0,
          "user_profile_identifier": "98826",
          "user_profile_language": 0,
          "user_profile_level": 0,
          "user_profile_location": "",
          "user_profile_nick_name": "test change8888",
          "user_profile_role": 0,
          "user_profile_self_signature": ""
      },
      "message_seq": 15840,
      "message_server_time": 1620877708,
      "message_status": 2,
      "message_unique_id": 6961616747713488299
   },
   "conv_type": 1,
   "conv_unread_num": 1
}]
```

## TIMConvSetDraft

This API is used to set the draft of a specified conversation.

**Prototype**

```c
TIM_DECL int TIMConvSetDraft(const char* conv_id, enum TIMConvType conv_type, const char* json_draft_param);
```

**Parameters**

| Parameter        | Type             | Description                                                  |
| ---------------- | ---------------- | ------------------------------------------------------------ |
| conv_id          | const char\*     | Conversation ID.                                             |
| conv_type        | enum TIMConvType | Conversation type. For more information, see [TIMConvType](https://intl.cloud.tencent.com/document/product/1047/34551). |
| json_draft_param | const char\*     | JSON string of the set draft.                                |

**Return values**

| Type | Description                                                  |
| ---- | ------------------------------------------------------------ |
| int  | If `TIM_SUCC` is returned, the API was called successfully. If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

>?Conversation drafts are usually used to save entered messages that have not been sent.


**Example**

```c
Json::Value json_value_text;  // Construct a message
json_value_text[kTIMElemType] = kTIMElem_Text;
json_value_text[kTIMTextElemContent] = "this draft";
Json::Value json_value_msg;
json_value_msg[kTIMMsgElemArray].append(json_value_text);

Json::Value json_value_draft; // Construct a draft
json_value_draft[kTIMDraftEditTime] = time(NULL);
json_value_draft[kTIMDraftUserDefine] = "this is userdefine";
json_value_draft[kTIMDraftMsg] = json_value_msg;

if (TIM_SUCC != TIMConvSetDraft(userid.c_str(), TIMConvType::kTIMConv_C2C, json_value_draft.toStyledString().c_str())) {
    // Failed to call the `TIMConvSetDraft` API
} 

// The `json_draft_param` JSON string obtained by `json_value_draft.toStyledString().c_str()` is as follows:
{
   "draft_edit_time" : 1551271429,
   "draft_msg" : {
      "message_elem_array" : [
         {
            "elem_type" : 0,
            "text_elem_content" : "this draft"
         }
      ]
   },
   "draft_user_define" : "this is userdefine"
}
```


## TIMConvCancelDraft

This API is used to delete the draft of a specified conversation.

**Prototype**

```c
TIM_DECL int TIMConvCancelDraft(const char* conv_id, enum TIMConvType conv_type);
```

**Parameters**

| Parameter | Type             | Description                                                  |
| --------- | ---------------- | ------------------------------------------------------------ |
| conv_id   | const char\*     | Conversation ID.                                             |
| conv_type | enum TIMConvType | Conversation type. For more information, see [TIMConvType](https://intl.cloud.tencent.com/document/product/1047/34551). |

**Return values**

| Type | Description                                                  |
| ---- | ------------------------------------------------------------ |
| int  | If `TIM_SUCC` is returned, the API was called successfully. If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |


## TIMConvPinConversation

This API is used to pin a conversation to the top.

**Prototype**

```c
TIM_DECL int TIMConvPinConversation(const char* conv_id, TIMConvType conv_type, bool is_pinned, TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type             | Description                                                  |
| --------- | ---------------- | ------------------------------------------------------------ |
| conv_id   | const char\*     | Conversation ID.                                             |
| conv_type | enum TIMConvType | Conversation type. For more information, see [TIMConvType](https://intl.cloud.tencent.com/document/product/1047/34551). |
| is_pinned | bool             | Whether to pin the conversation to the top.                  |
| cb        | TIMCommCallback  | Callback function for pinning the conversation to the top. For more information about the callback function definition, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data | const void\*     | User-defined data. The IM SDK only transfers the user data to the callback function `cb` without processing the data. |

**Return values**

| Type | Description                                                  |
| ---- | ------------------------------------------------------------ |
| int  | If `TIM_SUCC` is returned, the API was successfully called. (The callback `cb` is called only when the API returns `TIM_SUCC`.) If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

**Example**

```c
// The return value of `json_param` is an empty string, and you only need to check `code` to determine the result.
TIMConvPinConversation(
     [](int32_t code, const char* desc, const char* json_param, const void* user_data) {
     printf("TIMConvPinConversation|code:%d|desc:%s\n", code, desc);
}, nullptr);
```


## TIMConvGetTotalUnreadMessageCount

This API is used to obtain the total unread message count of all conversations.

**Prototype**

```c
TIM_DECL int TIMConvGetTotalUnreadMessageCount(TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type            | Description                                                  |
| --------- | --------------- | ------------------------------------------------------------ |
| cb        | TIMCommCallback | Callback function for obtaining the total unread message count of all conversations. For more information about the callback function definition, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data | const void\*    | User-defined data. The IM SDK only transfers the user data to the callback function `cb` without processing the data. |

**Return values**

| Type | Description                                                  |
| ---- | ------------------------------------------------------------ |
| int  | If `TIM_SUCC` is returned, the API was successfully called. (The callback `cb` is called only when the API returns `TIM_SUCC`.) If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

**Example**

```c
TIMConvGetTotalUnreadMessageCount(
    [](int32_t code, const char* desc, const char* json_param, const void* user_data) {
    printf("TIMConvGetTotalUnreadMessageCount|code:%d|desc:%s\n", code, desc);
}, nullptr);

// Example of `json_param`. For details on JSON keys, see [GetTotalUnreadNumberResult](TIMCloudDef.h).
// {"conv_get_total_unread_message_count_result_unread_count":4}
```
