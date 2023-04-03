For more information about messages, see [One-to-One Message](https://intl.cloud.tencent.com/document/product/1047/33523), [Group Message](https://intl.cloud.tencent.com/document/product/1047/33526), and [Message Formats](https://intl.cloud.tencent.com/document/product/1047/33527).

## TIMMsgSendMessage

This API is used to send a new message.

**Prototype**

```c
TIM_DECL int TIMMsgSendMessage(const char* conv_id, enum TIMConvType conv_type, const char* json_msg_param, char* message_id_buffer, TIMCommCallback cb, const void* user_data);
```

**Parameter**

| Parameter      | Type             | Description                                                  |
| -------------- | ---------------- | ------------------------------------------------------------ |
| conv_id        | const char\*     | Conversation ID                                              |
| conv_type      | enum TIMConvType | Conversation type. For more information, see [TIMConvType](https://intl.cloud.tencent.com/document/product/1047/34551). |
| json_msg_param | const char\*     | JSON string of the message.                                  |
| cb             | TIMCommCallback  | Callback function for indicating whether the new message is sent. For more information about the callback function definition, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data      | const void\*     | User-defined data. The IM SDK only transfers the user data to the callback function `cb` without processing the data. |

**Returned value**

| Type | Description                                                  |
| ---- | ------------------------------------------------------------ |
| int  | If `TIM_SUCC` is returned, the API was called successfully. If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

>?
 - This API is used to send a new one-to-one or group chat message.
 - When this API is used to send a one-to-one message, `conv_id` is set to UserID of the receiver, and `conv_type` is set to `kTIMConv_C2C`.
 - When this API is used to send a group message, `conv_id` is set to the group ID, and `conv_type` is set to `kTIMConv_Group`.
 - When a message is sent, `kTIMElem_GroupTips` and `kTIMElem_GroupReport` cannot be sent. They are delivered by the backend to update or notify the group information. The following elements in the message can be sent:
 - Text message element ([TextElem](https://intl.cloud.tencent.com/document/product/1047/34551))
 - Emoji message element ([FaceElem](https://intl.cloud.tencent.com/document/product/1047/34551))
 - Location message element ([LocationElem](https://intl.cloud.tencent.com/document/product/1047/34551))
 - Image message element ([ImageElem](https://intl.cloud.tencent.com/document/product/1047/34551))
 - Audio message element ([SoundElem](https://intl.cloud.tencent.com/document/product/1047/34551))
 - Custom message element ([CustomElem](https://intl.cloud.tencent.com/document/product/1047/34551))
 - File message element ([FileElem](https://intl.cloud.tencent.com/document/product/1047/34551))
 - Video message element ([VideoElem](https://intl.cloud.tencent.com/document/product/1047/34551))

**Sample**

```c
Json::Value json_value_text;
json_value_text[kTIMElemType] = kTIMElem_Text;
json_value_text[kTIMTextElemContent] = "send text";
Json::Value json_value_msg;
json_value_msg[kTIMMsgElemArray].append(json_value_text);
json_value_msg[kTIMMsgSender] = login_id;
json_value_msg[kTIMMsgClientTime] = time(NULL);
json_value_msg[kTIMMsgServerTime] = time(NULL);

const size_t kMessageIDLength = 128;
char message_id_buffer[kMessageIDLength] = {0};
int ret = TIMMsgSendMessage(conv_id.c_str(), kTIMConv_C2C, json_value_msg.toStyledString().c_str(), message_id_buffer, 
    [](int32_t code, const char* desc, const char* json_param, const void* user_data) {
    if (ERR_SUCC != code) {
        // Failed to send the message
        return;
    }
    // Message sent successfully
}, nullptr);

// The `json_msg_param` JSON string obtained by `json_value_msg.toStyledString().c_str()` is as follows:
{
   "message_id" : "14400111550110000_1551446728_45598731"
   "message_client_time" : 1551446728,
   "message_elem_array" : [
      {
         "elem_type" : 0,
         "text_elem_content" : "send text"
      }
   ],
   "message_sender" : "user1",
   "message_server_time" : 1551446728
}
```


## TIMMsgSendNewMsg

This API is used to send a new message. (This API is to be disused. Use the `TIMMsgSendMessage` API instead.)

**Prototype**

```c
TIM_DECL int TIMMsgSendNewMsg(const char* conv_id, enum TIMConvType conv_type, const char* json_msg_param, TIMCommCallback cb, const void* user_data);
```

**Parameter**

| Parameter      | Type             | Description                                                  |
| -------------- | ---------------- | ------------------------------------------------------------ |
| conv_id        | const char\*     | Conversation ID                                              |
| conv_type      | enum TIMConvType | Conversation type. For more information, see [TIMConvType](https://intl.cloud.tencent.com/document/product/1047/34551). |
| json_msg_param | const char\*     | JSON string of the message.                                  |
| cb             | TIMCommCallback  | Callback function for indicating whether the new message is sent. For more information about the callback function definition, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data      | const void\*     | User-defined data. The IM SDK only transfers the user data to the callback function `cb` without processing the data. |

**Returned value**

| Type | Description                                                  |
| ---- | ------------------------------------------------------------ |
| int  | If `TIM_SUCC` is returned, the API was successfully called. (The callback `cb` is called only when the API returns `TIM_SUCC`.) If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

>?
- This API is used to send a new one-to-one or group chat message.
 - When this API is used to send a one-to-one message, `conv_id` is set to UserID of the receiver, and `conv_type` is set to `kTIMConv_C2C`.
 - When this API is used to send a group message, `conv_id` is set to the group ID, and `conv_type` is set to `kTIMConv_Group`.
- When a message is sent, `kTIMElem_GroupTips` and `kTIMElem_GroupReport` cannot be sent. They are delivered by the backend to update or notify the group information. The following elements in the message can be sent:
 - Text message element ([TextElem](https://intl.cloud.tencent.com/document/product/1047/34551))
 - Emoji message element ([FaceElem](https://intl.cloud.tencent.com/document/product/1047/34551))
 - Location message element ([LocationElem](https://intl.cloud.tencent.com/document/product/1047/34551))
 - Image message element ([ImageElem](https://intl.cloud.tencent.com/document/product/1047/34551))
 - Audio message element ([SoundElem](https://intl.cloud.tencent.com/document/product/1047/34551))
 - Custom message element ([CustomElem](https://intl.cloud.tencent.com/document/product/1047/34551))
 - File message element ([FileElem](https://intl.cloud.tencent.com/document/product/1047/34551))
 - Video message element ([VideoElem](https://intl.cloud.tencent.com/document/product/1047/34551))


**Sample**

```c
Json::Value json_value_text;
json_value_text[kTIMElemType] = kTIMElem_Text;
json_value_text[kTIMTextElemContent] = "send text";
Json::Value json_value_msg;
json_value_msg[kTIMMsgElemArray].append(json_value_text);
json_value_msg[kTIMMsgSender] = login_id;
json_value_msg[kTIMMsgClientTime] = time(NULL);
json_value_msg[kTIMMsgServerTime] = time(NULL);

int ret = TIMMsgSendNewMsg(conv_id.c_str(), kTIMConv_C2C, json_value_msg.toStyledString().c_str(), [](int32_t code, const char* desc, const char* json_param, const void* user_data) {
    if (ERR_SUCC != code) {
        // Failed to send the message
        return;
    }
    // Message sent successfully
}, this);

// The `json_msg_param` JSON string obtained by `json_value_msg.toStyledString().c_str()` is as follows:
{
   "message_client_time" : 1551446728,
   "message_elem_array" : [
      {
         "elem_type" : 0,
         "text_elem_content" : "send text"
      }
   ],
   "message_sender" : "user1",
   "message_server_time" : 1551446728
}
```


## TIMMsgCancelSend

This API is used to cancel a message being sent based on `messageID`.

**Prototype**

```c
TIM_DECL int TIMMsgCancelSend(const char* conv_id, enum TIMConvType conv_type, const char* message_id, TIMCommCallback cb, const void* user_data);
```

**Parameter**

| Parameter  | Type             | Description                                                  |
| ---------- | ---------------- | ------------------------------------------------------------ |
| conv_id    | const char\*     | Conversation ID                                              |
| conv_type  | enum TIMConvType | Conversation type. For more information, see [TIMConvType](https://intl.cloud.tencent.com/document/product/1047/34551). |
| message_id | const char\*     | Message ID.                                                  |
| cb         | TIMCommCallback  | Callback function for cancelling a message being sent. For more information about the callback function definition, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data  | const void\*     | User-defined data. The IM SDK only transfers the user data to the callback function `cb` without processing the data. |

**Returned value**

| Type | Description                                                  |
| ---- | ------------------------------------------------------------ |
| int  | If `TIM_SUCC` is returned, the API was called successfully. If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

**Sample**

```c
TIMMsgCancelSend("test_win_03", kTIMConv_C2C, "message_id_1", [](int32_t code, const char* desc, const char* json_param, const void* user_data) {

}, nullptr);
```


## TIMMsgFindMessages

This API is used to query local messages by `messageID`.

**Prototype**

```c
TIM_DECL int TIMMsgFindMessages(const char* json_message_id_array, TIMCommCallback cb, const void* user_data);
```

**Parameter**

| Parameter             | Type            | Description                                                  |
| --------------------- | --------------- | ------------------------------------------------------------ |
| json_message_id_array | const char\*    | List of message IDs.                                         |
| cb                    | TIMCommCallback | Callback function for indicating whether the exact search of messages cached locally is successful. For more information about the callback function definition, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data             | const void\*    | User-defined data. The IM SDK only transfers the user data to the callback function `cb` without processing the data. |

**Returned value**

| Type | Description                                                  |
| ---- | ------------------------------------------------------------ |
| int  | If `TIM_SUCC` is returned, the API was called successfully. If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

**Sample**

```c
Json::Value json_message_id_1("id_clienttime_rand_1");
Json::Value json_message_id_2("id_clienttime_rand_2");

Json::Value json_message_id_array;
json_message_id_array.append(json_message_id_1);
json_message_id_array.append(json_message_id_2);
TIMMsgFindMessages(json_message_id_array.toStyledString().c_str(), [](int32_t code, const char* desc, const char* json_param, const void* user_data) {

}, nullptr);

// The `json_message_id_array` JSON string obtained by `json_message_id_array.toStyledString().c_str()` is as follows:
[
   "id_clienttime_rand_1",
   "id_clienttime_rand_2",
]
```


## TIMMsgReportReaded

This API is used to report that a message has been read.

**Prototype**

```c
TIM_DECL int TIMMsgReportReaded(const char* conv_id, enum TIMConvType conv_type, const char* json_msg_param, TIMCommCallback cb, const void* user_data);
```

**Parameter**

| Parameter      | Type             | Description                                                  |
| -------------- | ---------------- | ------------------------------------------------------------ |
| conv_id        | const char\*     | Conversation ID. Starting from v5.8, if `conv_id` is set to the `NULL` string pointer or the null string "", `conv_type` indicates that all one-to-one or group messages are read. |
| conv_type      | enum TIMConvType | Conversation type. For more information, see [TIMConvType](https://intl.cloud.tencent.com/document/product/1047/34551). |
| json_msg_param | const char\*     | JSON string of the message.                                  |
| cb             | TIMCommCallback  | Callback function for notifying whether the message read state is reported. For more information about the callback function definition, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data      | const void\*     | User-defined data. The IM SDK only transfers the user data to the callback function `cb` without processing the data. |

**Returned value**

| Type | Description                                                  |
| ---- | ------------------------------------------------------------ |
| int  | If `TIM_SUCC` is returned, the API was successfully called. (The callback `cb` is called only when the API returns `TIM_SUCC`.) If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

>?`json_msg_param` can be set to the `NULL` string pointer or the null string "". In that case, the timestamp of the latest message (if any) in the conversation or the current time is used as the read timestamp for reporting. If a message needs to be specified, the timestamp of this specified message is used as the read timestamp for reporting. We recommend that the message JSON content in the message array obtained from the received new message or the message JSON content located by the message locator be used to avoid repeated construction of the message JSON content.


## TIMMsgMarkAllMessageAsRead

This API is used to mark all messages as read. (This API is supported from v5.8.)

**Prototype**

```c
TIM_DECL int TIMMsgMarkAllMessageAsRead(TIMCommCallback cb, const void* user_data);
```

**Parameter**

| Parameter | Type            | Description                                                  |
| --------- | --------------- | ------------------------------------------------------------ |
| cb        | TIMCommCallback | Callback function for indicating whether all messages are marked as read. For more information about the callback function definition, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data | const void\*    | User-defined data. The IM SDK only transfers the user data to the callback function `cb` without processing the data. |

**Returned value**

| Type | Description                                                  |
| ---- | ------------------------------------------------------------ |
| int  | If `TIM_SUCC` is returned, the API was called successfully. If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |


## TIMMsgRevoke

This API is used to recall a message.

**Prototype**

```c
TIM_DECL int TIMMsgRevoke(const char* conv_id, enum TIMConvType conv_type, const char* json_msg_param, TIMCommCallback cb, const void* user_data);
```

**Parameter**

| Parameter      | Type             | Description                                                  |
| -------------- | ---------------- | ------------------------------------------------------------ |
| conv_id        | const char\*     | Conversation ID                                              |
| conv_type      | enum TIMConvType | Conversation type. For more information, see [TIMConvType](https://intl.cloud.tencent.com/document/product/1047/34551). |
| json_msg_param | const char\*     | JSON string of the message                                   |
| cb             | TIMCommCallback  | Callback function for indicating whether the message is recalled. For more information about the callback function definition, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data      | const void\*     | User-defined data. The IM SDK only transfers the user data to the callback function `cb` without processing the data. |

**Returned value**

| Type | Description                                                  |
| ---- | ------------------------------------------------------------ |
| int  | If `TIM_SUCC` is returned, the API was successfully called. (The callback `cb` is called only when the API returns `TIM_SUCC`.) If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

>?This API is used to recall a message. The stored message JSON content or the message JSON content located by the message locator is used to avoid repeated construction of the message JSON content.


**Sample**

```c
Json::Value json_value_text;
json_value_text[kTIMElemType] = kTIMElem_Text;
json_value_text[kTIMTextElemContent] = "send text";
Json::Value json_value_msg;
json_value_msg[kTIMMsgElemArray].append(json_value_text);

int ret = TIMMsgSendNewMsg("test_win_03", kTIMConv_C2C, json_value_msg.toStyledString().c_str(), [](int32_t code, const char* desc, const char* json_param, const void* user_data) {
    if (ERR_SUCC != code) {
        // Failed to send the message
        return;
    }
    // Message sent successfully. `json_param` returns the message JSON string after the message is sent.
    TIMMsgRevoke("test_win_03", kTIMConv_C2C, json_param, [](int32_t code, const char* desc, const char* json_param, const void* user_data) {
        if (ERR_SUCC != code) {
            // Failed to recall the message
            return;
        }
        // Message recalled successfully

    }, user_data);
}, this);
```


## TIMMsgFindByMsgLocatorList

This API is used to accurately locate a message of the specified conversation by using the message locator.

**Prototype**

```c
TIM_DECL int TIMMsgFindByMsgLocatorList(const char* conv_id, enum TIMConvType conv_type, const char* json_msg_Locator_array, TIMCommCallback cb, const void* user_data);
```

**Parameter**

| Parameter              | Type             | Description                                                  |
| ---------------------- | ---------------- | ------------------------------------------------------------ |
| conv_id                | const char\*     | Conversation ID                                              |
| conv_type              | enum TIMConvType | Conversation type. For more information, see [TIMConvType](https://intl.cloud.tencent.com/document/product/1047/34551). |
| json_msg_Locator_array | const char\*     | Message locator array                                        |
| cb                     | TIMCommCallback  | Callback function for indicating whether a message of the specified conversation is successfully and accurately located by the message locator. For more information about the callback definition and parameter parsing, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data              | const void\*     | User-defined data. The IM SDK only transfers the user data to the callback function `cb` without processing the data. |

**Returned value**

| Type | Description                                                  |
| ---- | ------------------------------------------------------------ |
| int  | If `TIM_SUCC` is returned, the API was successfully called. (The callback `cb` is called only when the API returns `TIM_SUCC`.) If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

>?
- This API is used to accurately locate a message of the specified conversation by using the message locator. It is often used to search for a specified message upon message recall.
- One message locator corresponds to one message.


**Sample**

```c
Json::Value json_msg_locator;                      // One message locator corresponds to one message (accurate location)
json_msg_locator[kTIMMsgLocatorIsRevoked] = false; // Whether the message is recalled
json_msg_locator[kTIMMsgLocatorTime] = 123;        // Specifies the message time
json_msg_locator[kTIMMsgLocatorSeq] = 1;           
json_msg_locator[kTIMMsgLocatorIsSelf] = false;    
json_msg_locator[kTIMMsgLocatorRand] = 12345678;   

Json::Value json_msg_locators;
json_msg_locators.append(json_msg_locator);
TIMMsgFindByMsgLocatorList("user2", kTIMConv_C2C, json_msg_locators.toStyledString().c_str(), [](int32_t code, const char* desc, const char* json_param, const void* user_data) {
    
}, nullptr);

// The `json_msg_Locator_array` JSON string obtained by `json_msg_locators.toStyledString().c_str()` is as follows:
[
   {
      "message_locator_is_revoked" : false,
      "message_locator_is_self" : false,
      "message_locator_rand" : 12345678,
      "message_locator_seq" : 1,
      "message_locator_time" : 123
   }
]
```


## TIMMsgImportMsgList

This API is used to import a message list to a specified conversation.

**Prototype**

```c
TIM_DECL int TIMMsgImportMsgList(const char* conv_id, enum TIMConvType conv_type, const char* json_msg_array, TIMCommCallback cb, const void* user_data);
```

**Parameter**

| Parameter      | Type             | Description                                                  |
| -------------- | ---------------- | ------------------------------------------------------------ |
| conv_id        | const char\*     | Conversation ID                                              |
| conv_type      | enum TIMConvType | Conversation type. For more information, see [TIMConvType](https://intl.cloud.tencent.com/document/product/1047/34551). |
| json_msg_array | const char\*     | Message array.                                               |
| cb             | TIMCommCallback  | Callback function for indicating whether the message list is imported to the specified conversation. For more information about the callback function definition, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data      | const void\*     | User-defined data. The IM SDK only transfers the user data to the callback function `cb` without processing the data. |

**Returned value**

| Type | Description                                                  |
| ---- | ------------------------------------------------------------ |
| int  | If `TIM_SUCC` is returned, the API was successfully called. (The callback `cb` is called only when the API returns `TIM_SUCC`.) If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

>?This API is used to import messages in batches. You can construct messages for importing. Alternatively, you can store the JSON string of the message array to be imported and call this API to import the JSON string, avoiding repeated construction of the message array.


**Sample**

```c
Json::Value json_value_elem; // Construct the message text element
json_value_elem[kTIMElemType] = TIMElemType::kTIMElem_Text;
json_value_elem[kTIMTextElemContent] = "this is import msg";

Json::Value json_value_msg; // Construct a message
json_value_msg[kTIMMsgSender] = login_id;
json_value_msg[kTIMMsgClientTime] = time(NULL);
json_value_msg[kTIMMsgServerTime] = time(NULL);
json_value_msg[kTIMMsgElemArray].append(json_value_elem);

Json::Value json_value_msgs;  // Message array
json_value_msgs.append(json_value_msg);

TIMMsgImportMsgList("user2", kTIMConv_C2C, json_value_msgs.toStyledString().c_str(), [](int32_t code, const char* desc, const char* json_param, const void* user_data) {
    
}, nullptr);

// The `json_msg_array` JSON string obtained by `json_value_msgs.toStyledString().c_str()` is as follows:
[
   {
      "message_client_time" : 1551446728,
      "message_elem_array" : [
         {
            "elem_type" : 0,
            "text_elem_content" : "this is import msg"
         }
      ],
      "message_sender" : "user1",
      "message_server_time" : 1551446728
   }
]
```


## TIMMsgSaveMsg

This API is used to save a custom message.

**Prototype**

```c
TIM_DECL int TIMMsgSaveMsg(const char* conv_id, enum TIMConvType conv_type, const char* json_msg_param, TIMCommCallback cb, const void* user_data);
```

**Parameter**

| Parameter      | Type             | Description                                                  |
| -------------- | ---------------- | ------------------------------------------------------------ |
| conv_id        | const char\*     | Conversation ID                                              |
| conv_type      | enum TIMConvType | Conversation type. For more information, see [TIMConvType](https://intl.cloud.tencent.com/document/product/1047/34551). |
| json_msg_param | const char\*     | JSON string of the message                                   |
| cb             | TIMCommCallback  | Callback function for indicating whether the custom message is stored. For more information about the callback function definition, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data      | const void\*     | User-defined data. The IM SDK only transfers the user data to the callback function `cb` without processing the data. |

**Returned value**

| Type | Description                                                  |
| ---- | ------------------------------------------------------------ |
| int  | If `TIM_SUCC` is returned, the API was successfully called. (The callback `cb` is called only when the API returns `TIM_SUCC`.) If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

>?This API is used to save a message. Generally, you can construct a message JSON string and save it to a specified conversation.


## TIMMsgGetMsgList

This API is used to obtain the message list of a specified conversation.

**Prototype**

```c
TIM_DECL int TIMMsgGetMsgList(const char* conv_id, enum TIMConvType conv_type, const char* json_get_msg_param, TIMCommCallback cb, const void* user_data);
```

**Parameter**

| Parameter          | Type             | Description                                                  |
| ------------------ | ---------------- | ------------------------------------------------------------ |
| conv_id            | const char\*     | Conversation ID                                              |
| conv_type          | enum TIMConvType | Conversation type. For more information, see [TIMConvType](https://intl.cloud.tencent.com/document/product/1047/34551). |
| json_get_msg_param | const char\*     | Parameter for obtaining messages.                            |
| cb                 | TIMCommCallback  | Callback function for indicating whether the message list of the specified conversation is obtained. For more information about the callback function definition and parameter parsing, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data          | const void\*     | User-defined data. The IM SDK only transfers the user data to the callback function `cb` without processing the data. |

**Returned value**

| Type | Description                                                  |
| ---- | ------------------------------------------------------------ |
| int  | If `TIM_SUCC` is returned, the API was successfully called. (The callback `cb` is called only when the API returns `TIM_SUCC`.) If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

>?
- The `kTIMMsgGetMsgListParamLastMsg` parameter specifies the message as the start point for local message pulling. The `kTIMMsgGetMsgListParamCount` parameter specifies the number of messages to be pulled. `kTIMMsgGetMsgListParamLastMsg` is optional. If you do not specify `kTIMMsgGetMsgListParamLastMsg`, the newest message of the conversation will be used as the start point for local message pulling.
- If you set `kTIMMsgGetMsgListParamIsRamble` to `true`, the roaming messages in the cloud will be pulled if the local messages are not enough.
- If you set `kTIMMsgGetMsgListParamIsForward` to `true`, messages later than the message specified by `kTIMMsgGetMsgListParamLastMsg` will be pulled. If you set it to `false`, messages earlier than the message specified by `kTIMMsgGetMsgListParamLastMsg` will be pulled.

- When kTIMConv_C2C messages are pulled, only `kTIMMsgGetMsgListParamLastMsg` can be used to specify the start point for message pulling. If `kTIMMsgGetMsgListParamLastMsg` is not specified, the IM SDK uses the newest message of the conversation as the start point for message pulling.
- When kTIMConv_Group messages are pulled, `kTIMMsgGetMsgListParamLastMsg` or `kTIMMsgGetMsgListParamLastMsgSeq` can be used to specify the start point for message pulling:
- If `kTIMMsgGetMsgListParamLastMsg` is used to specify the start point for message pulling, the returned message list does not include the message specified by `kTIMMsgGetMsgListParamLastMsg`.
- If `kTIMMsgGetMsgListParamLastMsgSeq` is used to specify the start point for message pulling, the returned message list includes the message specified by `kTIMMsgGetMsgListParamLastMsgSeq`.

- When kTIMConv_Group messages are pulled:
- If both `kTIMMsgGetMsgListParamLastMsg` and `kTIMMsgGetMsgListParamLastMsgSeq` are specified, the IM SDK uses `kTIMMsgGetMsgListParamLastMsg` to determine the start point for message pulling.
- If both `kTIMMsgGetMsgListParamLastMsg` and `kTIMMsgGetMsgListParamLastMsgSeq` are not specified, there are two cases for the start point for message pulling:
- If the time range for message pulling is specified, the IM SDK uses the point in time specified by `kTIMMsgGetMsgListParamTimeBegin` as the start point for message pulling.
- If the time range for message pulling is not specified, the IM SDK uses the newest message of the conversation as the start point for message pulling.

**Example: obtaining the `Windows-02` message list of the C2C conversation**

```c
Json::Value json_msg(Json::objectValue); // Construct a message
Json::Value json_get_msg_param;
json_get_msg_param[kTIMMsgGetMsgListParamLastMsg] = json_msg;
json_get_msg_param[kTIMMsgGetMsgListParamIsRamble] = false;
json_get_msg_param[kTIMMsgGetMsgListParamIsForward] = true;
json_get_msg_param[kTIMMsgGetMsgListParamCount] = 100;

int ret = TIMMsgGetMsgList("Windows-02", kTIMConv_C2C, json_get_msg_param.toStyledString().c_str(), [](int32_t code, const char* desc, const char* json_params, const void* user_data) {
}, this);

// The `json_get_msg_param` JSON string obtained by `json_get_msg_param.toStyledString().c_str()` is as follows:
{
   "msg_getmsglist_param_count" : 100,
   "msg_getmsglist_param_is_forward" : true,
   "msg_getmsglist_param_is_remble" : false,
   "msg_getmsglist_param_last_msg" : {}
}
```


## TIMMsgDelete

This API is used to delete messages of a specified conversation.

**Prototype**

```c
TIM_DECL int TIMMsgDelete(const char* conv_id, enum TIMConvType conv_type, const char* json_msgdel_param, TIMCommCallback cb, const void* user_data);
```

**Parameter**

| Parameter         | Type             | Description                                                  |
| ----------------- | ---------------- | ------------------------------------------------------------ |
| conv_id           | const char\*     | Conversation ID.                                             |
| conv_type         | enum TIMConvType | Conversation type. For more information, see [TIMConvType](https://intl.cloud.tencent.com/document/product/1047/34551). |
| json_msgdel_param | const char\*     | Parameter for obtaining messages.                            |
| cb                | TIMCommCallback  | Callback function for indicating whether messages of the specified conversation are deleted. For more information about the callback function definition, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data         | const void\*     | User-defined data. The IM SDK only transfers the user data to the callback function `cb` without processing the data. |

**Returned value**

| Type | Description                                                  |
| ---- | ------------------------------------------------------------ |
| int  | If `TIM_SUCC` is returned, the API was successfully called. (The callback `cb` is called only when the API returns `TIM_SUCC`.) If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

**Sample**

```c
Json::Value json_value_msg(Json::objectValue);
Json::Value json_value_msgdelete;
json_value_msgdelete[kTIMMsgDeleteParamIsRamble] = false;
json_value_msgdelete[kTIMMsgDeleteParamMsg] = json_value_msg;
TIMMsgDelete("user2", kTIMConv_C2C, json_value_msgdelete.toStyledString().c_str(), [](int32_t code, const char* desc, const char* json_param, const void* user_data) {

}, nullptr);

// The `json_msgdel_param` JSON string obtained by `json_value_msgdelete.toStyledString().c_str()` is as follows:
{
  "msg_delete_param_is_remble" : false,
  "msg_delete_param_msg" : {}
}
```


## TIMMsgListDelete

This API is used to delete the local and roaming messages of a specified conversation.

**Prototype**

```c
TIM_DECL int TIMMsgListDelete(const char* conv_id, enum TIMConvType conv_type, const char* json_msg_array, TIMCommCallback cb, const void* user_data);
```

**Parameter**

| Parameter      | Type             | Description                                                  |
| -------------- | ---------------- | ------------------------------------------------------------ |
| conv_id        | const char\*     | Conversation ID.                                             |
| conv_type      | enum TIMConvType | Conversation type. For more information, see [TIMConvType](https://intl.cloud.tencent.com/document/product/1047/34551). |
| json_msg_array | const char\*     | Message array.                                               |
| cb             | TIMCommCallback  | Callback function for indicating whether messages of the specified conversation are deleted. For more information about the callback function definition, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data      | const void\*     | User-defined data. The IM SDK only transfers the user data to the callback function `cb` without processing the data. |

**Returned value**

| Type | Description                                                  |
| ---- | ------------------------------------------------------------ |
| int  | If `TIM_SUCC` is returned, the API was successfully called. (The callback `cb` is called only when the API returns `TIM_SUCC`.) If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

>?
- This API deletes both local and roaming messages. Keep the following in mind:
- > We recommend that you store the JSON string of the message array and then call this API to delete the messages, avoiding repeated construction of the message array.
- > Up to 30 messages can be deleted at a time.
- > This API can be called only once per second.
- > If messages have been pulled on other devices by the account, they will remain on those devices after the API is called to delete them; in other words, the operation of message deletion is not synced across multiple devices.

**Sample**

```c
Json::Value json_value_elem; // Construct the message text element
json_value_elem[kTIMElemType] = TIMElemType::kTIMElem_Text;
json_value_elem[kTIMTextElemContent] = "this is import msg";

Json::Value json_value_msg; // Construct a message
json_value_msg[kTIMMsgSender] = login_id;
json_value_msg[kTIMMsgClientTime] = time(NULL);
json_value_msg[kTIMMsgServerTime] = time(NULL);
json_value_msg[kTIMMsgElemArray].append(json_value_elem);

Json::Value json_value_msgs;  // Message array
json_value_msgs.append(json_value_msg);

TIMMsgListDelete("user2", kTIMConv_C2C, json_value_msgs.toStyledString().c_str(), [](int32_t code, const chardesc, const charjson_param, const voiduser_data) {

}, nullptr);

// The `json_msg_array` JSON string obtained by `json_value_msgs.toStyledString().c_str()` is as follows:
[
   {
      "message_client_time" : 1551446728,
      "message_elem_array" : [
         {
            "elem_type" : 0,
            "text_elem_content" : "I will be deleted"
         }
      ],
      "message_sender" : "user1",
      "message_server_time" : 1551446728
   }
]
```


## TIMMsgClearHistoryMessage

This API is used to clear messages of a specified conversation.

**Prototype**

```c
TIM_DECL int TIMMsgClearHistoryMessage(const char* conv_id, enum TIMConvType conv_type, TIMCommCallback cb, const void* user_data);
```

**Parameter**

| Parameter | Type             | Description                                                  |
| --------- | ---------------- | ------------------------------------------------------------ |
| conv_id   | const char\*     | Conversation ID.                                             |
| conv_type | enum TIMConvType | Conversation type. For more information, see [TIMConvType](https://intl.cloud.tencent.com/document/product/1047/34551). |
| cb        | TIMCommCallback  | Callback function for indicating whether messages are cleared. For more information about the callback function definition, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data | const void\*     | User-defined data. The IM SDK only transfers the user data to the callback function `cb` without processing the data. |

**Returned value**

| Type | Description                                                  |
| ---- | ------------------------------------------------------------ |
| int  | If `TIM_SUCC` is returned, the API was successfully called. (The callback `cb` is called only when the API returns `TIM_SUCC`.) If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

**Sample**

```c
TIMMsgClearHistoryMessage("user2", kTIMConv_C2C, [](int32_t code, const char* desc, const char* json_param, const void* user_data) {

}, nullptr);
```


## TIMMsgSetC2CReceiveMessageOpt

This API is used to set the one-to-one message receiving option for specified users (batch setting supported).

**Prototype**

```c
TIM_DECL int TIMMsgSetC2CReceiveMessageOpt(const char* json_identifier_array, TIMReceiveMessageOpt opt, TIMCommCallback cb, const void* user_data);
```

**Parameter**

| Parameter             | Type                 | Description                                                  |
| --------------------- | -------------------- | ------------------------------------------------------------ |
| json_identifier_array | const char\*         | List of user IDs                                             |
| opt                   | TIMReceiveMessageOpt | Message receiving option. For more information, see [TIMReceiveMessageOpt](https://intl.cloud.tencent.com/document/product/1047/34551). |
| conv_type             | enum TIMConvType     | Conversation type. For more information, see [TIMConvType](https://intl.cloud.tencent.com/document/product/1047/34551). |
| cb                    | TIMCommCallback      | Callback function for indicating whether the one-to-one message receiving option is set. For more information about the callback function definition, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data             | const void\*         | User-defined data. The IM SDK only transfers the user data to the callback function `cb` without processing the data. |

**Returned value**

| Type | Description                                                  |
| ---- | ------------------------------------------------------------ |
| int  | If `TIM_SUCC` is returned, the API was successfully called. (The callback `cb` is called only when the API returns `TIM_SUCC`.) If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

>?
- This API supports batch setting. You can use the `userIDList` field to specify up to 30 users for batch setting.
- This API can be called five times every second.

**Sample**

```c
Json::Value json_identifier_array(Json::arrayValue);
json_identifier_array.append("user1");
json_identifier_array.append("user2");

TIMMsgSetC2CReceiveMessageOpt(json_identifier_array.toStyledString().c_str(), kTIMRecvMsgOpt_Receive, [](int32_t code, const char* desc, const char* json_param, const void* user_data) {

}, this);
```


## TIMMsgGetC2CReceiveMessageOpt

This API is used to query the one-to-one message receiving option for specified users.

**Prototype**

```c
TIM_DECL int TIMMsgGetC2CReceiveMessageOpt(const char* json_identifier_array, TIMCommCallback cb, const void* user_data);
```

**Parameter**

| Parameter             | Type             | Description                                                  |
| --------------------- | ---------------- | ------------------------------------------------------------ |
| json_identifier_array | const char\*     | List of user IDs                                             |
| conv_type             | enum TIMConvType | Conversation type. For more information, see [TIMConvType](https://intl.cloud.tencent.com/document/product/1047/34551). |
| cb                    | TIMCommCallback  | Query result callback function. For more information about the callback function definition, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data             | const void\*     | User-defined data. The IM SDK only transfers the user data to the callback function `cb` without processing the data. |

**Returned value**

| Type | Description                                                  |
| ---- | ------------------------------------------------------------ |
| int  | If `TIM_SUCC` is returned, the API was successfully called. (The callback `cb` is called only when the API returns `TIM_SUCC`.) If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

**Sample**

```c
Json::Value json_identifier_array(Json::arrayValue);
json_identifier_array.append("user1");
json_identifier_array.append("user2");

TIMMsgGetC2CReceiveMessageOpt(json_identifier_array.toStyledString().c_str(), [](int32_t code, const char* desc, const char* json_param, const void* user_data) {

}, this);

// Example of the callback `json_param`. For details on JSON keys, see [GetC2CRecvMsgOptResult](TIMCloudDef.h).
[
   {
      "msg_recv_msg_opt_result_identifier" : "user1",
      "msg_recv_msg_opt_result_opt" : 0,
   },
   {
      "msg_recv_msg_opt_result_identifier" : "user2",
      "msg_recv_msg_opt_result_opt" : 1,
   }
]
```


## TIMMsgSetGroupReceiveMessageOpt

This API is used to set the group message receiving option.

**Prototype**

```c
TIM_DECL int TIMMsgSetGroupReceiveMessageOpt(const char* group_id, TIMReceiveMessageOpt opt, TIMCommCallback cb, const void* user_data);
```

**Parameter**

| Parameter | Type                      | Description                                                  |
| --------- | ------------------------- | ------------------------------------------------------------ |
| group_id  | const char\*              | Group ID.                                                    |
| opt       | enum TIMReceiveMessageOpt | Message receiving option. For more information, see [TIMReceiveMessageOpt](https://intl.cloud.tencent.com/document/product/1047/34551). |
| conv_type | enum TIMConvType          | Conversation type. For more information, see [TIMConvType](https://intl.cloud.tencent.com/document/product/1047/34551). |
| cb        | TIMCommCallback           | Callback function for indicating whether the one-to-one message receiving option is set. For more information about the callback function definition, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data | const void\*              | User-defined data. The IM SDK only transfers the user data to the callback function `cb` without processing the data. |

**Returned value**

| Type | Description                                                  |
| ---- | ------------------------------------------------------------ |
| int  | If `TIM_SUCC` is returned, the API was successfully called. (The callback `cb` is called only when the API returns `TIM_SUCC`.) If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

>?
- You can obtain the group message receiving option from the group profile `GroupBaseInfo`.

**Sample**

```c
TIMMsgSetGroupReceiveMessageOpt("group_id", kTIMRecvMsgOpt_Receive, [](int32_t code, const char* desc, const char* json_param, const void* user_data) {

}, this);
```


## TIMMsgDownloadElemToPath

This API is used to download message elements (including image, video, audio, and file) to a specified path.

**Prototype**

```c
TIM_DECL int TIMMsgDownloadElemToPath(const char* json_download_elem_param, const char* path, TIMCommCallback cb, const void* user_data);
```

**Parameter**

| Parameter                | Type            | Description                                                  |
| ------------------------ | --------------- | ------------------------------------------------------------ |
| json_download_elem_param | const char\*    | JSON string of the download parameters.                      |
| path                     | const char\*    | Storage path of the downloaded file.                         |
| cb                       | TIMCommCallback | Callback function for indicating whether the download is successful and the download process. For more information about the callback function definition and parameter parsing, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data                | const void\*    | User-defined data. The IM SDK only transfers the user data to the callback function `cb` without processing the data. |

**Returned value**

| Type | Description                                                  |
| ---- | ------------------------------------------------------------ |
| int  | If `TIM_SUCC` is returned, the API was successfully called. (The callback `cb` is called only when the API returns `TIM_SUCC`.) If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

>?This API is used to download the image, file, audio, and video elements in messages. The download parameters, including `kTIMMsgDownloadElemParamFlag`, `kTIMMsgDownloadElemParamId`, `kTIMMsgDownloadElemParamBusinessId, and `kTIMMsgDownloadElemParamUrl` can be found in the corresponding elements. `kTIMMsgDownloadElemParamType` indicates the download file type. For more information, see [TIMDownloadType](https://intl.cloud.tencent.com/document/product/1047/34551).


**Sample**

```c
Json::Value download_param;
download_param[kTIMMsgDownloadElemParamFlag] = flag;
download_param[kTIMMsgDownloadElemParamType] = type;
download_param[kTIMMsgDownloadElemParamId] = id;
download_param[kTIMMsgDownloadElemParamBusinessId] = business_id;
download_param[kTIMMsgDownloadElemParamUrl] = url;

TIMMsgDownloadElemToPath(download_param.toStyledString().c_str(), (path_ + "\\" + name).c_str(), [](int32_t code, const char* desc, const char* json_param, const void* user_data) {

}, this);
```


## TIMMsgDownloadMergerMessage

This API is used to download a combined message.

**Prototype**

```c
TIM_DECL int TIMMsgDownloadMergerMessage(const char* json_single_msg, TIMCommCallback cb, const void* user_data);
```

**Parameter**

| Parameter       | Type            | Description                                                  |
| --------------- | --------------- | ------------------------------------------------------------ |
| json_single_msg | const char\*    | JSON string of a combined message.                           |
| cb              | TIMCommCallback | Callback function for indicating whether the download is successful and the download process. For more information about the callback function definition , see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data       | const void\*    | User-defined data. The IM SDK only transfers the user data to the callback function `cb` without processing the data. |

**Returned value**

| Type | Description                                                  |
| ---- | ------------------------------------------------------------ |
| int  | If `TIM_SUCC` is returned, the API was successfully called. (The callback `cb` is called only when the API returns `TIM_SUCC`.) If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

**Sample**

```c
// Received a message (`json_single_msg`) 
TIMMsgDownloadMergerMessage(json_single_msg, [](int32_t code, const char* desc, const char* json_param, const void* user_data) {

}, this);
```


## TIMMsgSearchLocalMessages

Local message search is a feature essential to improve user experience of the application. It allows users to quickly and conveniently find the expected information from massive amounts of complex data. It can also be used as an operations tool to easily and efficiently navigate to extensive content.
>!This feature is supported only by v5.4.666 or later. To use it, purchase the [Ultimate edition](https://www.tencentcloud.com/document/product/1047/34577#.E5.8D.87.E7.BA.A7.E5.BA.94.E7.94.A8). For more information, see [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350).

**Prototype**

```c
TIM_DECL int TIMMsgSearchLocalMessages(const char* json_search_message_param, TIMCommCallback cb, const void* user_data);
```

**Parameter**

| Parameter                 | Type            | Description                                                  |
| ------------------------- | --------------- | ------------------------------------------------------------ |
| json_search_message_param | const char\*    | Message search parameter.                                    |
| cb                        | TIMCommCallback | Callback function for indicating whether the search is successful. For more information about the callback function definition, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data                 | const void\*    | User-defined data. The IM SDK only transfers the user data to the callback function `cb` without processing the data. |

**Returned value**

| Type | Description                                                  |
| ---- | ------------------------------------------------------------ |
| int  | If `TIM_SUCC` is returned, the API was successfully called. (The callback `cb` is called only when the API returns `TIM_SUCC`.) If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

**Sample**

```c
// Received a message (`json_single_msg`) 
Json::Value json_search_message_param;
json_search_message_param[kTIMMsgSearchParamKeywordArray].append("keyword1");
json_search_message_param[kTIMMsgSearchParamKeywordArray].append("keyword2");
json_search_message_param[kTIMMsgSearchParamMessageTypeArray].append(kTIMElem_Text);
json_search_message_param[kTIMMsgSearchParamMessageTypeArray].append(kTIMElem_Image);
json_search_message_param[kTIMMsgSearchParamConvId] = "xxxxx";
json_search_message_param[kTIMMsgSearchParamConvType] = kTIMConv_Group;
json_search_message_param[kTIMMsgSearchParamPageIndex] = 0;
json_search_message_param[kTIMMsgSearchParamPageSize] = 10;

int ret = TIMMsgSearchLocalMessages(json_search_message_param.toStyledString().c_str(), [](int32_t code, const char* desc, const char* json_params, const void* user_data) {

}, this);

// The `json_search_message_param` JSON string obtained by `json_search_message_param.toStyledString().c_str()` is as follows:
{
   "msg_search_param_keyword_array" : ["keyword1", "keyword2"],
   "msg_search_param_message_type_array" : [0, 1],
   "msg_search_param_page_index" : 0,
   "msg_search_param_page_size" : 10
}
```


## TIMMsgSetLocalCustomData

This API is used to set custom message data (saved locally, will not be sent to the peer end, and will become invalid after the app is uninstalled and reinstalled).

**Prototype**

```c
TIM_DECL int TIMMsgSetLocalCustomData(const char* json_msg_param, TIMCommCallback cb, const void* user_data);
```

**Parameter**

| Parameter      | Type            | Description                                                  |
| -------------- | --------------- | ------------------------------------------------------------ |
| json_msg_param | const char\*    | JSON string of the message.                                  |
| cb             | TIMCommCallback | Callback function for indicating whether the custom message is stored. For more information about the callback function definition, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data      | const void\*    | User-defined data. The IM SDK only transfers the user data to the callback function `cb` without processing the data. |

**Returned value**

| Type | Description                                                  |
| ---- | ------------------------------------------------------------ |
| int  | If `TIM_SUCC` is returned, the API was successfully called. (The callback `cb` is called only when the API returns `TIM_SUCC`.) If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

**Sample**

```c
// Received a message (`json_single_msg`) 
Json::Value json_parameters;
json_parameters[kTIMMsgGetMsgListParamIsRamble] = true;
json_parameters[kTIMMsgGetMsgListParamIsForward] = false;
json_parameters[kTIMMsgGetMsgListParamCount] = 1;
 TIMMsgGetMsgList("98826", kTIMConv_C2C, json_parameters.toStyledString().c_str(),
    [](int32_t code, const char* desc, const char* json_params, const void* user_data) {
        Json::Reader json_reader;
        json::Array json_message_array;
        json_reader.parse(json_params, json_message_array);
        if (json_message_array.size() > 0) {
            Json::Value json_obj_msg = json_message_array[0];
            json_obj_msg[kTIMMsgCustomStr] = "custom Str";
            json_obj_msg[kTIMMsgCustomInt] = "custom int";
            TIMMsgSetLocalCustomData(json_obj_msg.toStyledString().c_str(),
                [](int32_t code, const char* desc, const char* json_param, const void* user_data) {
                    printf("TIMMsgSetLocalCustomData complete|code:%d|desc:%s\n", code, desc);
                }, nullptr);
        }
}, nullptr);
```


## TIMMsgBatchSend

This API is used to send messages in batches, but not to groups.

**Prototype**

```c
TIM_DECL int TIMMsgBatchSend(const char* json_batch_send_param, TIMCommCallback cb, const void* user_data);
```

**Parameter**

| Parameter             | Type            | Description                                                  |
| --------------------- | --------------- | ------------------------------------------------------------ |
| json_batch_send_param | const char\*    | JSON string of batch sent messages.                          |
| cb                    | TIMCommCallback | Callback function for indicating whether the messages are batch sent successfully. For more information about the callback function definition and parameter parsing, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data             | const void\*    | User-defined data. The IM SDK only transfers the user data to the callback function `cb` without processing the data. |

**Returned value**

| Type | Description                                                  |
| ---- | ------------------------------------------------------------ |
| int  | If `TIM_SUCC` is returned, the API was successfully called. (The callback `cb` is called only when the API returns `TIM_SUCC`.) If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

>?This API is used to send messages in batches. The callback function `cb` returns whether the messages are sent to each UserID successfully.


**Sample**

```c
// Construct a text message element
Json::Value json_value_elem;
json_value_elem[kTIMElemType] = TIMElemType::kTIMElem_Text;
json_value_elem[kTIMTextElemContent] = "this is batch send msg";
// Construct a message
Json::Value json_value_msg;
json_value_msg[kTIMMsgSender] = login_id;
json_value_msg[kTIMMsgClientTime] = time(NULL);
json_value_msg[kTIMMsgServerTime] = time(NULL);
json_value_msg[kTIMMsgElemArray].append(json_value_elem);

// Construct an ID array list for batch sending
Json::Value json_value_ids(Json::arrayValue);
json_value_ids.append("user2");
json_value_ids.append("user3");
// Construct API parameters for batch sending
Json::Value json_value_batchsend;
json_value_batchsend[kTIMMsgBatchSendParamIdentifierArray] = json_value_ids;
json_value_batchsend[kTIMMsgBatchSendParamMsg] = json_value_msg;
int ret = TIMMsgBatchSend(json_value_batchsend.toStyledString().c_str(), [](int32_t code, const char* desc, const char* json_param, const void* user_data) {
}, nullptr);

// The `json_batch_send_param` JSON string obtained by `json_value_batchsend.toStyledString().c_str()` is as follows:
{
   "msg_batch_send_param_identifier_array" : [ "user2", "user3" ],
   "msg_batch_send_param_msg" : {
      "message_client_time" : 1551340614,
      "message_elem_array" : [
         {
            "elem_type" : 0,
            "text_elem_content" : "this is batch send msg"
         }
      ],
      "message_sender" : "user1",
      "message_server_time" : 1551340614
   }
}
```
