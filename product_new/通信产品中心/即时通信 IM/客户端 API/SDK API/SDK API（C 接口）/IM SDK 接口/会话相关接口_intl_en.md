The IM SDK supports the following two types of conversations:
- C2C conversation: a one-to-one chat between you and another user. Messages are read and sent through the conversation.
- Group conversation: a group chat among group members. All group members can receive messages sent in the group conversation.


## TIMConvCreate

This API is used to create a conversation.

**Prototype**

```c
TIM_DECL int TIMConvCreate(const char* conv_id, enum TIMConvType conv_type, TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| conv_id | const char\* | Conversation ID. |
| conv_type | enum TIMConvType | Conversation type. For more information, see [TIMConvType](https://intl.cloud.tencent.com/document/product/1047/34551). |
| cb | TIMCommCallback | Callback for creating a conversation. For more information about the callback function definitions and parameter parsing, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data | const void\* | User-defined data. The IM SDK only transfers the user data to the callback function cb without processing the data. |

**Return values**

| Type | Description |
|-----|-----|
| int | If TIM_SUCC is returned, the API was successfully called. (The callback cb is called only when the API returns TIM_SUCC.) If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

>?
- A conversation is a one-to-one or group chat, through which messages are sent and received between you and another user or in a group.
- This API creates a conversation or obtains conversation information. The conversation type (group or one-to-one chat) and the conversation party identifier (the conversation party's account or group ID) need to be specified. Conversation information is returned through the callback cb.


**Example 1: obtaining a one-to-one chat with a party whose UserID is Windows-02**

```c
const void* user_data = nullptr; // Returned by the callback function
const char* userid = "Windows-02";
int ret = TIMConvCreate(userid, kTIMConv_C2C, [](int32_t code, const char* desc, const char* json_param, const void* user_data) {
    if (ERR_SUCC != code) {
        return;
    }
    // The callback returns detailed information about the conversation.
}, user_data);
if (ret != TIM_SUCC) {
    // Failed to call the TIMConvCreate API.
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
    // The callback returns detailed information about the conversation.
}, user_data);
if (ret != TIM_SUCC) {
    // Failed to call the TIMConvCreate API.
}
```


## TIMConvDelete

This API is used to delete a conversation.

**Prototype**

```c
TIM_DECL int TIMConvDelete(const char* conv_id, enum TIMConvType conv_type, TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| conv_id | const char\* | Conversation ID. |
| conv_type | enum TIMConvType | Conversation type. For more information, see [TIMConvType](https://intl.cloud.tencent.com/document/product/1047/34551). |
| cb | TIMCommCallback | Callback for whether a conversation is successfully deleted. For more information about the callback function definitions, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data | const void\* | User-defined data. The IM SDK only transfers the user data to the callback function cb without processing the data. |

**Return values**

| Type | Description |
|-----|-----|
| int | If TIM_SUCC is returned, the API was successfully called. (The callback cb is called only when the API returns TIM_SUCC.) If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

> This API is used to delete a conversation. Whether a conversion is successfully deleted is returned through the callback.


## TIMConvGetConvList

This API is used to obtain the conversation list of recent contacts.

**Prototype**

```c
TIM_DECL int TIMConvGetConvList(TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| cb | TIMCommCallback | Callback for obtaining the conversation list of recent contacts. For more information about the callback function definitions and parameter parsing, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data | const void\* | User-defined data. The IM SDK only transfers the user data to the callback function cb without processing the data. |

**Return values**

| Type | Description |
|-----|-----|
| int | If TIM_SUCC is returned, the API was successfully called. (The callback cb is called only when the API returns TIM_SUCC.) If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

## TIMConvSetDraft

This API is used to set the draft of a specified conversation.

**Prototype**

```c
TIM_DECL int TIMConvSetDraft(const char* conv_id, enum TIMConvType conv_type, const char* json_draft_param);
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| conv_id | const char\* | Conversation ID. |
| conv_type | enum TIMConvType | Conversation type. For more information, see [TIMConvType](https://intl.cloud.tencent.com/document/product/1047/34551). |
| json_draft_param | const char\* | JSON string of the set draft. |

**Return values**

| Type | Description |
|-----|-----|
| int | If TIM_SUCC is returned, the API was called successfully. If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

>?Conversation drafts are usually used to save entered but not sent messages.


**Example**

```c
Json::Value json_value_text;  // Constructs a message.
json_value_text[kTIMElemType] = kTIMElem_Text;
json_value_text[kTIMTextElemContent] = "this draft";
Json::Value json_value_msg;
json_value_msg[kTIMMsgElemArray].append(json_value_text);

Json::Value json_value_draft; // Constructs a draft.
json_value_draft[kTIMDraftEditTime] = time(NULL);
json_value_draft[kTIMDraftUserDefine] = "this is userdefine";
json_value_draft[kTIMDraftMsg] = json_value_msg;

if (TIM_SUCC != TIMConvSetDraft(userid.c_str(), TIMConvType::kTIMConv_C2C, json_value_draft.toStyledString().c_str())) {
    // Failed to call the TIMConvSetDraft API.
} 

// The json_draft_param JSON string obtained by json_value_draft.toStyledString().c_str() is as follows:
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

| Parameter | Type | Description |
|-----|-----|-----|
| conv_id | const char\* | Conversation ID. |
| conv_type | enum TIMConvType | Conversation type. For more information, see [TIMConvType](https://intl.cloud.tencent.com/document/product/1047/34551). |

**Return values**

| Type | Description |
|-----|-----|
| int | If TIM_SUCC is returned, the API was called successfully. If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

