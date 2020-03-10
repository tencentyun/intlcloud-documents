The IM SDK supports two types of conversations.
- C2C conversation: is a one-to-one chat established between you and another user. Messages are read and sent through the conversation.
- Group conversation: is a conversation among group members in a group chat. Messages sent in the group conversation can be received by all group members.


## TIMConvCreate

Creates a conversation.

**Prototype**

```c
TIM_DECL int TIMConvCreate(const char* conv_id, enum TIMConvType conv_type, TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| conv_id | const char\* | The conversation ID. |
| conv_type | enum TIMConvType | The conversation type. For more information, see [TIMConvType](https://cloud.tencent.com/document/product/269/33553#timconvtype). |
| cb | TIMCommCallback | The callback for conversation creation. For the definition and parameter explanation of the callback function, see [TIMCommCallback](https://cloud.tencent.com/document/product/269/33552#timcommcallback). |
| user_data | const void\* | User-defined data. The IM SDK is only responsible for returning the user data to the callback function cb without any processing. |

**Returned value**

| Type | Description |
|-----|-----|
| int | If TIM_SUCC is returned, the API is invoked successfully (the callback cb will be invoked only when the API returns TIM_SUCC). If other values than this are returned, the API failed to be invoked. For the definition of each returned value, see [TIMResult](https://cloud.tencent.com/document/product/269/33553#timresult). |

>
- A conversation is a one-to-one chat or a group chat, through which messages are sent and received between you and another user or in a group.
- This API creates or obtains conversation information. The conversation type (group chat or one-to-one chat) and the conversation party identifier (the conversation party’s account or group ID) need to be specified. Conversation information is returned through the callback cb.


**Example 1: retrieving a one-to-one conversation with a party whose UserID is Windows-02**

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
    // Failed to invoke the TIMConvCreate API.
}
```


**Example 2: retrieving a conversation whose group ID is Windows-Group-01**

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
    // Failed to invoke the TIMConvCreate API.
}
```


## TIMConvDelete

Deletes a conversation.

**Prototype**

```c
TIM_DECL int TIMConvDelete(const char* conv_id, enum TIMConvType conv_type, TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| conv_id | const char\* | The conversation ID. |
| conv_type | enum TIMConvType | The conversation type. For more information, see [TIMConvType](https://cloud.tencent.com/document/product/269/33553#timconvtype). |
| cb | TIMCommCallback | The callback for checking whether deleting the conversation succeeded or failed. For the definition of the callback function, see [TIMCommCallback](https://cloud.tencent.com/document/product/269/33552#timcommcallback). |
| user_data | const void\* | User-defined data. The IM SDK is only responsible for returning the user data to the callback function cb without any processing. |

**Returned value**

| Type | Description |
|-----|-----|
| int | If TIM_SUCC is returned, the API is invoked successfully (the callback cb will be invoked only when the API returns TIM_SUCC). If other values than this are returned, the API failed to be invoked. For the definition of each returned value, see [TIMResult](https://cloud.tencent.com/document/product/269/33553#timresult). |

> This API is used to delete a conversation. The conversation deletion result is returned through the callback.


## TIMConvGetConvList

Obtains the list of recent contact conversations.

**Prototype**

```c
TIM_DECL int TIMConvGetConvList(TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| cb | TIMCommCallback | The callback for obtaining the list of recent contact conversations. For the definition and parameter explanation of the callback function, see [TIMCommCallback](https://cloud.tencent.com/document/product/269/33552#timcommcallback). |
| user_data | const void\* | User-defined data. The IM SDK is only responsible for returning the user data to the callback function cb without any processing. |

**Returned value**

| Type | Description |
|-----|-----|
| int | If TIM_SUCC is returned, the API is invoked successfully (the callback cb will be invoked only when the API returns TIM_SUCC). If other values than this are returned, the API failed to be invoked. For the definition of each returned value, see [TIMResult](https://cloud.tencent.com/document/product/269/33553#timresult). |

## TIMConvSetDraft

Sets the draft of a specified conversation.

**Prototype**

```c
TIM_DECL int TIMConvSetDraft(const char* conv_id, enum TIMConvType conv_type, const char* json_draft_param);
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| conv_id | const char\* | The conversation ID. |
| conv_type | enum TIMConvType | The conversation type. For more information, see [TIMConvType](https://cloud.tencent.com/document/product/269/33553#timconvtype). |
| json_draft_param | const char\* | The JSON string of the set draft. |

**Returned value**

| Type | Description |
|-----|-----|
| int | If TIM_SUCC is returned, it indicates that the API is invoked successfully. If other values than this are returned, it indicates that the API failed to be invoked. For the definition of each returned value, see [TIMResult](https://cloud.tencent.com/document/product/269/33553#timresult). |

> Conversation drafts are often used to store pending messages that are currently input by the user.


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
    // Failed to invoke the TIMConvSetDraft API.
} 

// json_value_draft.toStyledString().c_str() obtains the following json_draft_param JSON string:
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

Deletes the draft of a specified conversation.

**Prototype**

```c
TIM_DECL int TIMConvCancelDraft(const char* conv_id, enum TIMConvType conv_type);
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| conv_id | const char\* | The conversation ID. |
| conv_type | enum TIMConvType | The conversation type. For more information, see [TIMConvType](https://cloud.tencent.com/document/product/269/33553#timconvtype). |

**Returned value**

| Type | Description |
|-----|-----|
| int | If TIM_SUCC is returned, it indicates that the API is invoked successfully. If other values than this are returned, it indicates that the API failed to be invoked. For the definition of each returned value, see [TIMResult](https://cloud.tencent.com/document/product/269/33553#timresult). |

