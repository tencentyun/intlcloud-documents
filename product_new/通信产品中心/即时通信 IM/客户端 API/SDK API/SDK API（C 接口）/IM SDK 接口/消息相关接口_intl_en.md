For more information about messages, see [One-to-One Chat Messages](https://intl.cloud.tencent.com/document/product/1047/33523), [Group Chat Messages](https://intl.cloud.tencent.com/document/product/1047/33526), and [Message Format Description](https://intl.cloud.tencent.com/document/product/1047/33527).

## TIMMsgSendNewMsg

This API is used to send a new message.

**Prototype**

```c
TIM_DECL int TIMMsgSendNewMsg(const char* conv_id, enum TIMConvType conv_type, const char* json_msg_param, TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| conv_id | const char\* | Conversation ID. |
| conv_type | enum TIMConvType | Conversation type. For more information, see [TIMConvType](https://intl.cloud.tencent.com/document/product/1047/34551). |
| json_msg_param | const char\* | JSON string of a message. |
| cb | TIMCommCallback | Callback function for notifying whether the new message is sent. For more information about the callback function definition, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data | const void\* | User-defined data. The IM SDK only transfers the user data to the callback function cb without processing the data. |

**Return values**

| Type | Description |
|-----|-----|
| int | If TIM_SUCC is returned, the API was successfully called. (The callback cb is called only when the API returns TIM_SUCC.) If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

>?
>- This API is used to send a new one-to-one or group chat message.
 >    - When this API is used to send a one-to-one chat message, `conv_id` is set to UserID of the peer party and `conv_type` is set to `kTIMConv_C2C`.
 >    - When this API is used to send a group chat message, `conv_id` is set to the group ID and `conv_type` is set to `kTIMConv_Group`.
>- When a message is sent, `kTIMElem_GroupTips` and `kTIMElem_GroupReport` cannot be sent. They are delivered by the backend to update or notify the group information. The following elements in the message can be sent:
 >     - Text message element. For more information, see [TextElem](https://intl.cloud.tencent.com/document/product/1047/34551).
 >     -  Emoji message element. For more information, see [FaceElem](https://intl.cloud.tencent.com/document/product/1047/34551).
 >     - Location message element. For more information, see [LocationElem](https://intl.cloud.tencent.com/document/product/1047/34551).
 >     -  Image message element. For more information, see [ImageElem](https://intl.cloud.tencent.com/document/product/1047/34551).
 >     -  Sound message element. For more information, see [SoundElem](https://intl.cloud.tencent.com/document/product/1047/34551).
 >     -  Custom message element. For more information, see [CustomElem](https://intl.cloud.tencent.com/document/product/1047/34551).
 >     - File message element. For more information, see [FileElem](https://intl.cloud.tencent.com/document/product/1047/34551).
 >     - Video message element. For more information, see [VideoElem](https://intl.cloud.tencent.com/document/product/1047/34551).



**Example**

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
        // Failed to send a message.
        return;
    }
    // The message was sent successfully.
}, this);

// The json_msg_param JSON string obtained by json_value_msg.toStyledString().c_str() is as follows:
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


## TIMMsgReportReaded

This API is used to report that a message has been read.

**Prototype**

```c
TIM_DECL int TIMMsgReportReaded(const char* conv_id, enum TIMConvType conv_type, const char* json_msg_param, TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| conv_id | const char\* | Conversation ID. |
| conv_type | enum TIMConvType | Conversation type. For more information, see [TIMConvType](https://intl.cloud.tencent.com/document/product/1047/34551). |
| json_msg_param | const char\* | JSON string of a message. |
| cb | TIMCommCallback | Callback function for notifying whether the message read state is reported. For more information about the callback function definition, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data | const void\* | User-defined data. The IM SDK only transfers the user data to the callback function cb without processing the data. |

**Return values**

| Type | Description |
|-----|-----|
| int | If TIM_SUCC is returned, the API was successfully called. (The callback cb is called only when the API returns TIM_SUCC.) If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

>? `json_msg_param` can be set to the `NULL` string pointer or the null string "". At this time, the timestamp of the latest message (if any) in the conversation or the current time is used as the read timestamp for reporting. If a message needs to be specified, the timestamp of this specified message is used as the read timestamp for reporting. We recommend that the message JSON content in the message array obtained from the received new message or the message JSON content located by the message locator be used to avoid repeated construction of the message JSON content.


## TIMMsgRevoke

This API is used to revoke a message.

**Prototype**

```c
TIM_DECL int TIMMsgRevoke(const char* conv_id, enum TIMConvType conv_type, const char* json_msg_param, TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| conv_id | const char\* | Conversation ID. |
| conv_type | enum TIMConvType | Conversation type. For more information, see [TIMConvType](https://intl.cloud.tencent.com/document/product/1047/34551). |
| json_msg_param | const char\* | JSON string of a message. |
| cb | TIMCommCallback | Callback function for notifying whether a message was revoked. For more information about the callback function definition, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data | const void\* | User-defined data. The IM SDK only transfers the user data to the callback function cb without processing the data. |

**Return values**

| Type | Description |
|-----|-----|
| int | If TIM_SUCC is returned, the API was successfully called. (The callback cb is called only when the API returns TIM_SUCC.) If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

>?This API is used to revoke a message. The stored message JSON content or the message JSON content located by the message locator is used to avoid repeated construction of the message JSON content.


**Example**

```c
Json::Value json_value_text;
json_value_text[kTIMElemType] = kTIMElem_Text;
json_value_text[kTIMTextElemContent] = "send text";
Json::Value json_value_msg;
json_value_msg[kTIMMsgElemArray].append(json_value_text);

int ret = TIMMsgSendNewMsg("test_win_03", kTIMConv_C2C, json_value_msg.toStyledString().c_str(), [](int32_t code, const char* desc, const char* json_param, const void* user_data) {
    if (ERR_SUCC != code) {
        // Failed to send a message.
        return;
    }
    // The message was successfully sent. json_param returns the message JSON string after the message is sent.
    TIMMsgRevoke("test_win_03", kTIMConv_C2C, json_param, [](int32_t code, const char* desc, const char* json_param, const void* user_data) {
        if (ERR_SUCC != code) {
            // The message failed to be revoked.
            return;
        }
        // The message was successfully revoked.

    }, user_data);
}, this);
```


## TIMMsgFindByMsgLocatorList

This API is used to accurately locate a message of the specified conversation by using the message locator.

**Prototype**

```c
TIM_DECL int TIMMsgFindByMsgLocatorList(const char* conv_id, enum TIMConvType conv_type, const char* json_msg_Locator_array, TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| conv_id | const char\* | Conversation ID. |
| conv_type | enum TIMConvType | Conversation type. For more information, see [TIMConvType](https://intl.cloud.tencent.com/document/product/1047/34551). |
| json_msg_Locator_array | const char\* | Message locator array. |
| cb | TIMCommCallback | Callback function for notifying whether a message of the specified conversation was successfully and accurately located by the message locator. For more information about the callback definition and parameter parsing, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data | const void\* | User-defined data. The IM SDK only transfers the user data to the callback function cb without processing the data. |

**Return values**

| Type | Description |
|-----|-----|
| int | If TIM_SUCC is returned, the API was successfully called. (The callback cb is called only when the API returns TIM_SUCC.) If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

>?
>- This API is used to accurately locate a message of the specified conversation by using the message locator. It is often used to search for a specified message upon message revocation.
>- One message locator corresponds to one message.


**Example**

```c
Json::Value json_msg_locator;                      // One message locator corresponds to one message (accurate location).
json_msg_locator[kTIMMsgLocatorIsRevoked] = false; // Whether the message is revoked.
json_msg_locator[kTIMMsgLocatorTime] = 123;        // Specifies the message time.
json_msg_locator[kTIMMsgLocatorSeq] = 1;           
json_msg_locator[kTIMMsgLocatorIsSelf] = false;    
json_msg_locator[kTIMMsgLocatorRand] = 12345678;   

Json::Value json_msg_locators;
json_msg_locators.append(json_msg_locator);
TIMMsgFindByMsgLocatorList("user2", kTIMConv_C2C, json_msg_locators.toStyledString().c_str(), [](int32_t code, const char* desc, const char* json_param, const void* user_data) {
    
}, nullptr);

// The json_msg_Locator_array JSON string obtained by json_msg_locators.toStyledString().c_str() is as follows:
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

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| conv_id | const char\* | Conversation ID. |
| conv_type | enum TIMConvType | Conversation type. For more information, see [TIMConvType](https://intl.cloud.tencent.com/document/product/1047/34551). |
| json_msg_array | const char\* | Message array. |
| cb | TIMCommCallback | Callback indicating whether the message list was imported to the specified conversation. For more information about the callback function definition, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data | const void\* | User-defined data. The IM SDK only transfers the user data to the callback function cb without processing the data. |

**Return values**

| Type | Description |
|-----|-----|
| int | If TIM_SUCC is returned, the API was successfully called. (The callback cb is called only when the API returns TIM_SUCC.) If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

>?This API is used to import messages in batches. You can construct messages for importing. Alternatively, you can store the JSON string of the message array to be imported and call this API to import the JSON string, avoiding repeated construction of the message array.


**Example**

```c
Json::Value json_value_elem; // Constructs the message text element.
json_value_elem[kTIMElemType] = TIMElemType::kTIMElem_Text;
json_value_elem[kTIMTextElemContent] = "this is import msg";

Json::Value json_value_msg; // Constructs a message.
json_value_msg[kTIMMsgSender] = login_id;
json_value_msg[kTIMMsgClientTime] = time(NULL);
json_value_msg[kTIMMsgServerTime] = time(NULL);
json_value_msg[kTIMMsgElemArray].append(json_value_elem);

Json::Value json_value_msgs;  // Message array
json_value_msgs.append(json_value_msg);

TIMMsgImportMsgList("user2", kTIMConv_C2C, json_value_msgs.toStyledString().c_str(), [](int32_t code, const char* desc, const char* json_param, const void* user_data) {
    
}, nullptr);

// The json_msg_array JSON string obtained by json_value_msgs.toStyledString().c_str() is as follows:
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

This API is used to store a custom message.

**Prototype**

```c
TIM_DECL int TIMMsgSaveMsg(const char* conv_id, enum TIMConvType conv_type, const char* json_msg_param, TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| conv_id | const char\* | Conversation ID. |
| conv_type | enum TIMConvType | Conversation type. For more information, see [TIMConvType](https://intl.cloud.tencent.com/document/product/1047/34551). |
| json_msg_param | const char\* | JSON string of a message. |
| cb | TIMCommCallback | Callback function for notifying whether the custom message was stored. For more information about the callback function definition, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data | const void\* | User-defined data. The IM SDK only transfers the user data to the callback function cb without processing the data. |

**Return values**

| Type | Description |
|-----|-----|
| int | If TIM_SUCC is returned, the API was successfully called. (The callback cb is called only when the API returns TIM_SUCC.) If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

>?This API is used to store a message. Generally, you can construct a message JSON string and save it to a specified conversation.


## TIMMsgGetMsgList

This API is used to obtain the message list of a specified conversation.

**Prototype**

```c
TIM_DECL int TIMMsgGetMsgList(const char* conv_id, enum TIMConvType conv_type, const char* json_get_msg_param, TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| conv_id | const char\* | Conversation ID. |
| conv_type | enum TIMConvType | Conversation type. For more information, see [TIMConvType](https://intl.cloud.tencent.com/document/product/1047/34551). |
| json_get_msg_param | const char\* | Parameter for obtaining messages. |
| cb | TIMCommCallback | Callback function for notifying whether the message list of the specified conversation was obtained. For more information about the callback function definition and parameter parsing, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data | const void\* | User-defined data. The IM SDK only transfers the user data to the callback function cb without processing the data. |

**Return values**

| Type | Description |
|-----|-----|
| int | If TIM_SUCC is returned, the API was successfully called. (The callback cb is called only when the API returns TIM_SUCC.) If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

>? The `kTIMMsgGetMsgListParamLastMsg` parameter specifies a session from which the local message list is obtained. The `kTIMMsgGetMsgListParamCount` parameter specifies the number of messages to be obtained. If you do not specify `kTIMMsgGetMsgListParamLastMsg`, the latest message `LastMsg` of the session will be used.  If you set `kTIMMsgGetMsgListParamIsRamble` to `true`, the roaming message in the cloud will be obtained when the local messages are not enough. If you set `kTIMMsgGetMsgListParamIsForward` to `true`, messages latter than the value of `kTIMMsgGetMsgListParamLastMsg` will be obtained.  If you set it to ` false`, messages earlier than the value of `kTIMMsgGetMsgListParamLastMsg` will be obtained.


**Example: obtaining `Windows-02` message list** of the C2C session

```c
Json::Value json_msg(Json::objectValue); // Constructs a message.
Json::Value json_get_msg_param;
json_get_msg_param[kTIMMsgGetMsgListParamLastMsg] = json_msg;
json_get_msg_param[kTIMMsgGetMsgListParamIsRamble] = false;
json_get_msg_param[kTIMMsgGetMsgListParamIsForward] = true;
json_get_msg_param[kTIMMsgGetMsgListParamCount] = 100;

int ret = TIMMsgGetMsgList("Windows-02", kTIMConv_C2C, json_get_msg_param.toStyledString().c_str(), [](int32_t code, const char* desc, const char* json_params, const void* user_data) {
}, this);

// The json_get_msg_param JSON string obtained by json_get_msg_param.toStyledString().c_str() is as follows:
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

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| conv_id | const char\* | Conversation ID. |
| conv_type | enum TIMConvType | Conversation type. For more information, see [TIMConvType](https://intl.cloud.tencent.com/document/product/1047/34551). |
| json_msgdel_param | const char\* | Parameter for obtaining messages. |
| cb | TIMCommCallback | Callback function for notifying whether messages of the specified conversation were deleted. For more information about the callback function definition, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data | const void\* | User-defined data. The IM SDK only transfers the user data to the callback function cb without processing the data. |

**Return values**

| Type | Description |
|-----|-----|
| int | If TIM_SUCC is returned, the API was successfully called. (The callback cb is called only when the API returns TIM_SUCC.) If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

>?
>- If `kTIMMsgDeleteParamMsg` is specified, the specified local message is deleted from the conversation.
>- If `kTIMMsgDeleteParamMsg` is not specified and `kTIMMsgDeleteParamIsRamble` is set to false, all local messages of the conversation are deleted. If `kTIMMsgDeleteParamIsRamble` is set to true, all roaming messages of the conversation are deleted. Currently, 5.5.904 and later versions are supported.
>- Generally, the stored message JSON string or the JSON string located by the message locator is used. You do not need to construct the message JSON string when deleting messages.


**Example**

```c
Json::Value json_value_msg(Json::objectValue);
Json::Value json_value_msgdelete;
json_value_msgdelete[kTIMMsgDeleteParamIsRamble] = false;
json_value_msgdelete[kTIMMsgDeleteParamMsg] = json_value_msg;
TIMMsgDelete("user2", kTIMConv_C2C, json_value_msgdelete.toStyledString().c_str(), [](int32_t code, const char* desc, const char* json_param, const void* user_data) {

}, nullptr);

// The json_msgdel_param JSON string obtained by json_value_msgdelete.toStyledString().c_str() is as follows:
{
  "msg_delete_param_is_remble" : false,
  "msg_delete_param_msg" : {}
}
```


## TIMMsgDownloadElemToPath

This API is used to download message elements (including image, video, audio, and file) to a specified path.

**Prototype**

```c
TIM_DECL int TIMMsgDownloadElemToPath(const char* json_download_elem_param, const char* path, TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| json_download_elem_param | const char\* | JSON string of the download parameter. |
| path | const char\* | Storage path of the downloaded file. |
| cb | TIMCommCallback | Callback function for notifying whether the download was successful and the callback for indicating the download process. For more information about the callback function definition and parameter parsing, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data | const void\* | User-defined data. The IM SDK only transfers the user data to the callback function cb without processing the data. |

**Return values**

| Type | Description |
|-----|-----|
| int | If TIM_SUCC is returned, the API was successfully called. (The callback cb is called only when the API returns TIM_SUCC.) If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

>? This API is used to download the image, file, audio, and video elements in messages. The download parameters, including kTIMMsgDownloadElemParamFlag, kTIMMsgDownloadElemParamId, kTIMMsgDownloadElemParamBusinessId, and kTIMMsgDownloadElemParamUrl, can be found in the corresponding elements. `kTIMMsgDownloadElemParamType` indicates the download file type. For more information, see [TIMDownloadType](https://intl.cloud.tencent.com/document/product/1047/34551).


**Example**

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


## TIMMsgBatchSend

This API is used to send messages in batches, but not to groups.

**Prototype**

```c
TIM_DECL int TIMMsgBatchSend(const char* json_batch_send_param, TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| json_batch_send_param | const char\* | JSON string of batch sent messages. |
| cb | TIMCommCallback | Callback function for notifying whether the messages were batch sent successfully. For more information about the callback function definition and parameter parsing, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data | const void\* | User-defined data. The IM SDK only transfers the user data to the callback function cb without processing the data. |

**Return values**

| Type | Description |
|-----|-----|
| int | If TIM_SUCC is returned, the API was successfully called. (The callback cb is called only when the API returns TIM_SUCC.) If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

>? This API is used to send messages in batch. The callback cb returns whether each UserID is sent successfully.


**Example**

```c
// Constructs a text message element.
Json::Value json_value_elem;
json_value_elem[kTIMElemType] = TIMElemType::kTIMElem_Text;
json_value_elem[kTIMTextElemContent] = "this is batch send msg";
// Constructs a message.
Json::Value json_value_msg;
json_value_msg[kTIMMsgSender] = login_id;
json_value_msg[kTIMMsgClientTime] = time(NULL);
json_value_msg[kTIMMsgServerTime] = time(NULL);
json_value_msg[kTIMMsgElemArray].append(json_value_elem);

// Constructs an ID array list for batch sending.
Json::Value json_value_ids(Json::arrayValue);
json_value_ids.append("user2");
json_value_ids.append("user3");
// Constructs API parameters for batch sending.
Json::Value json_value_batchsend;
json_value_batchsend[kTIMMsgBatchSendParamIdentifierArray] = json_value_ids;
json_value_batchsend[kTIMMsgBatchSendParamMsg] = json_value_msg;
int ret = TIMMsgBatchSend(json_value_batchsend.toStyledString().c_str(), [](int32_t code, const char* desc, const char* json_param, const void* user_data) {
}, nullptr);

// The json_batch_send_param JSON string obtained by json_value_batchsend.toStyledString().c_str() is as follows:
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


