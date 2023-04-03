## IM SDK Event Callbacks


### TIMRecvNewMsgCallback

Callback for new messages.

**Prototype**

```c
typedef void (*TIMRecvNewMsgCallback)(const char* json_msg_array, const void* user_data);
```

**Parameters**

| Parameter      | Type         | Description                                                  |
| -------------- | ------------ | ------------------------------------------------------------ |
| json_msg_array | const char\* | New message array.                                           |
| user_data      | const void\* | User-defined data, which is passed through by the IM SDK without being processed. |

>?This callback is used to obtain the newly received message array. Note that the elements in the message are also an array, and each element is defined by the `elem_type` field.


**Example 1: parse the message array**

```c
Json::Value json_value_msgs; // Parse the message
Json::Reader reader;
if (!reader.parse(json_msg_array, json_value_msgs)) {
    printf("reader parse failure!%s", reader.getFormattedErrorMessages().c_str());
    return;
}
for (Json::ArrayIndex i = 0; i < json_value_msgs.size(); i++) {  // Traverse the messages
    Json::Value& json_value_msg = json_value_msgs[i];
    Json::Value& elems = json_value_msg[kTIMMsgElemArray];
    for (Json::ArrayIndex m = 0; m < elems.size(); m++) {   // Traverse the elements
        Json::Value& elem = elems[i];

        uint32_t elem_type = elem[kTIMElemType].asUInt();
        if (elem_type == TIMElemType::kTIMElem_Text) {  // Text
            
        } else if (elem_type == TIMElemType::kTIMElem_Sound) {  // Sound
            
        } else if (elem_type == TIMElemType::kTIMElem_File) {  // File
            
        } else if (elem_type == TIMElemType::kTIMElem_Image) { // Image
            
        } else if (elem_type == TIMElemType::kTIMElem_Custom) { // Custom element
            
        } else if (elem_type == TIMElemType::kTIMElem_GroupTips) { // Group notification
            
        } else if (elem_type == TIMElemType::kTIMElem_Face) { // Emoji
            
        } else if (elem_type == TIMElemType::kTIMElem_Location) { // Location
            
        } else if (elem_type == TIMElemType::kTIMElem_GroupReport) { // Group system message
            
        } else if (elem_type == TIMElemType::kTIMElem_Video) { // Video
            
        }
    }
}
```


**Example 2: return the JSON string of a text message. For details on the JSON keys, see [Message](https://intl.cloud.tencent.com/document/product/1047/34551) and [TextElem](https://intl.cloud.tencent.com/document/product/1047/34551)**

```c
[
   {
      "message_client_time" : 1551080111,
      "message_conv_id" : "user2",
      "message_conv_type" : 1,
      "message_elem_array" : [
         {
            "elem_type" : 0,
            "text_elem_content" : "123213213"
         }
      ],
      "message_is_from_self" : true,
      "message_is_read" : true,
      "message_rand" : 2130485001,
      "message_sender" : "user1",
      "message_seq" : 1,
      "message_server_time" : 1551080111,
      "message_status" : 2
   }
]
```


**Example 3: return the JSON string of a group system message. For details on the JSON keys, see [Message](https://intl.cloud.tencent.com/document/product/1047/34551) and [GroupReportElem](https://intl.cloud.tencent.com/document/product/1047/34551)**

```c
[
   {
      "message_client_time" : 1551344977,
      "message_conv_id" : "",
      "message_conv_type" : 3,
      "message_elem_array" : [
         {
            "elem_type" : 9,
            "group_report_elem_group_id" : "first group id",
            "group_report_elem_group_name" : "first group name",
            "group_report_elem_msg" : "",
            "group_report_elem_op_group_memberinfo" : {
               "group_member_info_custom_info" : {},
               "group_member_info_identifier" : "user1",
               "group_member_info_join_time" : 0,
               "group_member_info_member_role" : 0,
               "group_member_info_msg_flag" : 0,
               "group_member_info_msg_seq" : 0,
               "group_member_info_name_card" : "",
               "group_member_info_shutup_time" : 0
            },
            "group_report_elem_op_user" : "",
            "group_report_elem_platform" : "Windows",
            "group_report_elem_report_type" : 6,
            "group_report_elem_user_data" : ""
         }
      ],
      "message_is_from_self" : false,
      "message_is_read" : true,
      "message_rand" : 2207687390,
      "message_sender" : "@TIM#SYSTEM",
      "message_seq" : 1,
      "message_server_time" : 1551344977,
      "message_status" : 2
   }
]
```


**Example 4: return the JSON string of a group notification. For details on the JSON keys, see [Message](https://intl.cloud.tencent.com/document/product/1047/34551) and [GroupTipsElem](https://intl.cloud.tencent.com/document/product/1047/34551)**

```c
[
   {
      "message_client_time" : 1551412814,
      "message_conv_id" : "first group id",
      "message_conv_type" : 2,
      "message_elem_array" : [
         {
            "elem_type" : 6,
            "group_tips_elem_changed_group_memberinfo_array" : [],
            "group_tips_elem_group_change_info_array" : [
               {
                  "group_tips_group_change_info_flag" : 10,
                  "group_tips_group_change_info_value" : "first group name to other name"
               }
            ],
            "group_tips_elem_group_id" : "first group id",
            "group_tips_elem_group_name" : "first group name to other name",
            "group_tips_elem_member_change_info_array" : [],
            "group_tips_elem_member_num" : 0,
            "group_tips_elem_op_group_memberinfo" : {
               "group_member_info_custom_info" : {},
               "group_member_info_identifier" : "user1",
               "group_member_info_join_time" : 0,
               "group_member_info_member_role" : 0,
               "group_member_info_msg_flag" : 0,
               "group_member_info_msg_seq" : 0,
               "group_member_info_name_card" : "",
               "group_member_info_shutup_time" : 0
            },
            "group_tips_elem_op_user" : "user1",
            "group_tips_elem_platform" : "Windows",
            "group_tips_elem_time" : 0,
            "group_tips_elem_tip_type" : 6,
            "group_tips_elem_user_array" : []
         }
      ],
      "message_is_from_self" : false,
      "message_is_read" : true,
      "message_rand" : 1,
      "message_sender" : "@TIM#SYSTEM",
      "message_seq" : 1,
      "message_server_time" : 1551412814,
      "message_status" : 2
   },
]
```


### TIMMsgReadedReceiptCallback

Callback for message read receipts.

**Prototype**

```c
typedef void (*TIMMsgReadedReceiptCallback)(const char* json_msg_readed_receipt_array, const void* user_data);
```

**Parameters**

| Parameter                     | Type         | Description                                                  |
| ----------------------------- | ------------ | ------------------------------------------------------------ |
| json_msg_readed_receipt_array | const char\* | Message read receipt array                                   |
| user_data                     | const void\* | User-defined data, which is passed through by the IM SDK without being processed. |

**Example**

```c
void MsgReadedReceiptCallback(const char* json_msg_readed_receipt_array, const void* user_data) {
    Json::Value json_value_receipts;
    Json::Reader reader;
    if (!reader.parse(json_msg_readed_receipt_array, json_value_receipts)) {
        // Failed to parse the JSON string
        return;
    }
    
    for (Json::ArrayIndex i = 0; i < json_value_receipts.size(); i++) {
        Json::Value& json_value_receipt = json_value_receipts[i];
    
        std::string convid = json_value_receipt[kTIMMsgReceiptConvId].asString();
        uint32_t conv_type = json_value_receipt[kTIMMsgReceiptConvType].asUInt();
        uint64_t timestamp = json_value_receipt[kTIMMsgReceiptTimeStamp].asUInt64();
    
        // Message read logic
    }
}
```


### TIMMsgRevokeCallback

Callback for notifying received message revocation.

**Prototype**

```c
typedef void (*TIMMsgRevokeCallback)(const char* json_msg_locator_array, const void* user_data);
```

**Parameters**

| Parameter              | Type         | Description                                                  |
| ---------------------- | ------------ | ------------------------------------------------------------ |
| json_msg_locator_array | const char\* | Message locator array.                                       |
| user_data              | const void\* | User-defined data, which is passed through by the IM SDK without being processed. |

**Example**

```c
void MsgRevokeCallback(const char* json_msg_locator_array, const void* user_data) {
    Json::Value json_value_locators;
    Json::Reader reader;
    if (!reader.parse(json_msg_locator_array, json_value_locators)) {
        // Failed to parse the JSON string
        return;
    }
    for (Json::ArrayIndex i = 0; i < json_value_locators.size(); i++) {
        Json::Value& json_value_locator = json_value_locators[i];
    
        std::string convid = json_value_locator[kTIMMsgLocatorConvId].asString();
        uint32_t conv_type = json_value_locator[kTIMMsgLocatorConvType].asUInt();
        bool isrevoke      = json_value_locator[kTIMMsgLocatorIsRevoked].asBool();
        uint64_t time      = json_value_locator[kTIMMsgLocatorTime].asUInt64();
        uint64_t seq       = json_value_locator[kTIMMsgLocatorSeq].asUInt64();
        uint64_t rand      = json_value_locator[kTIMMsgLocatorRand].asUInt64();
        bool isself        = json_value_locator[kTIMMsgLocatorIsSelf].asBool();
    
        // Message revocation logic
    }
}
```


### TIMMsgElemUploadProgressCallback

Callback for checking the progress of uploading files pertaining to message elements.

**Prototype**

```c
typedef void (*TIMMsgElemUploadProgressCallback)(const char* json_msg, uint32_t index, uint32_t cur_size, uint32_t total_size, const void* user_data);
```

**Parameters**

| Parameter  | Type         | Description                                                  |
| ---------- | ------------ | ------------------------------------------------------------ |
| json_msg   | const char\* | New message                                                  |
| index      | uint32_t     | Subscript of the uploaded element `Elem` in the `json_msg` message |
| cur_size   | uint32_t     | Current size uploaded                                        |
| total_size | uint32_t     | Total size uploaded                                          |
| user_data  | const void\* | User-defined data, which is passed through by the IM SDK without being processed. |

**Example**

```c
void MsgElemUploadProgressCallback(const char* json_msg, uint32_t index, uint32_t cur_size, uint32_t total_size, const void* user_data) {
    Json::Value json_value_msg;
    Json::Reader reader;
    if (!reader.parse(json_msg, json_value_msg)) {
        // Failed to parse the JSON string
        return;
    }
    Json::Value& elems = json_value_msg[kTIMMsgElemArray];
    if (index >= elems.size()) {
        // The value of `index` exceeds the number of message elements
        return;
    }
    uint32_t elem_type = elems[index][kTIMElemType].asUInt();
    if (kTIMElem_File ==  elem_type) {

    }
    else if (kTIMElem_Sound == elem_type) {

    }
    else if (kTIMElem_Video == elem_type) {

    }
    else if (kTIMElem_Image == elem_type) {

    }
    else {
        // Other types of elements do not meet the upload requirements
    }
}
```


### TIMGroupTipsEventCallback

Callback for group events.

**Prototype**

```c
typedef void (*TIMGroupTipsEventCallback)(const char* json_group_tip_array, const void* user_data);
```

**Parameters**

| Parameter            | Type         | Description                                                  |
| -------------------- | ------------ | ------------------------------------------------------------ |
| json_group_tip_array | const char\* | Group notification list                                      |
| user_data            | const void\* | User-defined data, which is passed through by the IM SDK without being processed. |

### TIMConvEventCallback

Callback for conversation events.

**Prototype**

```c
typedef void (*TIMConvEventCallback)(enum TIMConvEvent conv_event, const char* json_conv_array, const void* user_data);
```

**Parameters**

| Parameter       | Type              | Description                                                  |
| --------------- | ----------------- | ------------------------------------------------------------ |
| conv_event      | enum TIMConvEvent | Conversation event type. For details, see [TIMConvEvent](https://intl.cloud.tencent.com/document/product/1047/34551). |
| json_conv_array | const char\*      | Conversation information list                                |
| user_data       | const void\*      | User-defined data, which is passed through by the IM SDK without being processed. |

**Example: parse the conversation event callback data**

```c
void ConvEventCallback(TIMConvEvent conv_event, const char* json_conv_array, const void* user_data) {
    Json::Reader reader;
    Json::Value json_value;
    if (!reader.parse(json_conv_array, json_value)) {
        // Failed to parse the JSON string
        return;
    }
    for (Json::ArrayIndex i = 0; i < json_value.size(); i++) { // Traverse the conversation types
        Json::Value& convinfo = json_value[i];
        // Identifies the conversation event type
        if (conv_event == kTIMConvEvent_Add) {

        }
        else if (conv_event == kTIMConvEvent_Del) {

        }
        else if (conv_event == kTIMConvEvent_Update) {

        }
    }
}
```


### TIMNetworkStatusListenerCallback

Callback for network status.

**Prototype**

```c
typedef void (*TIMNetworkStatusListenerCallback)(enum TIMNetworkStatus status, int32_t code, const char* desc, const void* user_data);
```

**Parameters**

| Parameter | Type                  | Description                                                  |
| --------- | --------------------- | ------------------------------------------------------------ |
| status    | enum TIMNetworkStatus | Network status. For details, see [TIMNetworkStatus](https://intl.cloud.tencent.com/document/product/1047/34551). |
| code      | int32_t               | `ERR_SUCC`: succeeded. Others: failed. For details, see [Error Codes](https://intl.cloud.tencent.com/document/product/1047/34348). |
| desc      | const char\*          | String of the error description                              |
| user_data | const void\*          | User-defined data, which is passed through by the IM SDK without being processed. |

**Example: process the callback for monitoring the network status**

```c
void NetworkStatusListenerCallback(TIMNetworkStatus status, int32_t code, const char* desc, const void* user_data) {
    switch(status) {
    case kTIMConnected: {
        printf("OnConnected ! user_data:0x%08x", user_data);
        break;
    }
    case kTIMDisconnected:{
        printf("OnDisconnected ! user_data:0x%08x", user_data);
        break;
    }
    case kTIMConnecting:{
        printf("OnConnecting ! user_data:0x%08x", user_data);
        break;
    }
    case kTIMConnectFailed:{
        printf("ConnectFailed code:%u desc:%s ! user_data:0x%08x", code, desc, user_data);
        break;
    }
    }
}
```


### TIMKickedOfflineCallback

Callback for forced logout.

**Prototype**

```c
typedef void (*TIMKickedOfflineCallback)(const void* user_data);
```

**Parameters**

| Parameter | Type         | Description                                                  |
| --------- | ------------ | ------------------------------------------------------------ |
| user_data | const void\* | User-defined data, which is passed through by the IM SDK without being processed. |

### TIMUserSigExpiredCallback

Callback for user ticket expiration.

**Prototype**

```c
typedef void (*TIMUserSigExpiredCallback)(const void* user_data);
```

**Parameters**

| Parameter | Type         | Description                                                  |
| --------- | ------------ | ------------------------------------------------------------ |
| user_data | const void\* | User-defined data, which is passed through by the IM SDK without being processed. |

### TIMOnAddFriendCallback

Callback for adding friends.

**Prototype**

```c
typedef void(*TIMOnAddFriendCallback)(const char* json_identifier_array, const void* user_data);
```

**Parameters**

| Parameter             | Type         | Description                                                  |
| --------------------- | ------------ | ------------------------------------------------------------ |
| json_identifier_array | const char\* | List of added friends                                        |
| user_data             | const void\* | User-defined data, which is passed through by the IM SDK without being processed. |

**Example: json_identifier_array**

```c
[ "user15" ]
```


### TIMOnDeleteFriendCallback

Callback for deleting friends.

**Prototype**

```c
typedef void(*TIMOnDeleteFriendCallback)(const char* json_identifier_array, const void* user_data);
```

**Parameters**

| Parameter             | Type         | Description                                                  |
| --------------------- | ------------ | ------------------------------------------------------------ |
| json_identifier_array | const char\* | List of deleted friends                                      |
| user_data             | const void\* | User-defined data, which is passed through by the IM SDK without being processed. |

**Example: json_identifier_array**

```c
[ "user15" ]
```


### TIMUpdateFriendProfileCallback

Callback for updating friend profiles.

**Prototype**

```c
typedef void(*TIMUpdateFriendProfileCallback)(const char* json_friend_profile_update_array, const void* user_data);
```

**Parameters**

| Parameter                        | Type         | Description                                                  |
| -------------------------------- | ------------ | ------------------------------------------------------------ |
| json_friend_profile_update_array | const char\* | Friend profile update list                                   |
| user_data                        | const void\* | User-defined data, which is passed through by the IM SDK without being processed. |

**Example: json_friend_profile_update_array**

```c
[
   {
      "friend_profile_update_identifier" : "user4",
      "friend_profile_update_item" : {
         "friend_profile_item_group_name_array" : [ "group1", "group2" ],
         "friend_profile_item_remark" : "New Remark"
      }
   }
]
```


### TIMFriendAddRequestCallback

Callback for friend requests.

**Prototype**

```c
typedef void(*TIMFriendAddRequestCallback)(const char* json_friend_add_request_pendency_array, const void* user_data);
```

**Parameters**

| Parameter                              | Type         | Description                                                  |
| -------------------------------------- | ------------ | ------------------------------------------------------------ |
| json_friend_add_request_pendency_array | const char\* | List of pending friend requests                              |
| user_data                              | const void\* | User-defined data, which is passed through by the IM SDK without being processed. |

**Example: json_friend_add_request_pendency_array**

```c
[
   {
      "friend_add_pendency_add_source" : "AddSource_Type_android",
      "friend_add_pendency_add_wording" : "aaaa",
      "friend_add_pendency_identifier" : "v222",
      "friend_add_pendency_nick_name" : ""
   }
]
```


### TIMLogCallback

Callback for logs.

**Prototype**

```c
typedef void (*TIMLogCallback)(enum TIMLogLevel level, const char* log, const void* user_data);
```

**Parameters**

| Parameter | Type             | Description                                                  |
| --------- | ---------------- | ------------------------------------------------------------ |
| level     | Enum TIMLogLevel | Log level. For details, see [TIMLogLevel](https://intl.cloud.tencent.com/document/product/1047/34551). |
| log       | const char\*     | Log string                                                   |
| user_data | const void\*     | User-defined data, which is passed through by the IM SDK without being processed. |

### TIMMsgUpdateCallback

Callback for message updating.

**Prototype**

```c
typedef void (*TIMMsgUpdateCallback)(const char* json_msg_array, const void* user_data);
```

**Parameters**

| Parameter      | Type         | Description                                                  |
| -------------- | ------------ | ------------------------------------------------------------ |
| json_msg_array | const char\* | Updated message array                                        |
| user_data      | const void\* | User-defined data, which is passed through by the IM SDK without being processed. |

>?For details, see [TIMRecvNewMsgCallback](#timrecvnewmsgcallback).


## IM SDK API Callbacks


### TIMCommCallback

Definition of common API callbacks.

**Prototype**

```c
typedef void (*TIMCommCallback)(int32_t code, const char* desc, const char* json_params, const void* user_data);
```

**Parameters**

| Parameter   | Type         | Description                                                  |
| ----------- | ------------ | ------------------------------------------------------------ |
| code        | int32_t      | `ERR_SUCC`: succeeded. Others: failed. For details, see [Error Codes](https://intl.cloud.tencent.com/document/product/1047/34348). |
| desc        | const char\* | String of the error description                              |
| json_params | const char\* | JSON string, which varies with APIs.                         |
| user_data   | const void\* | User-defined data, which is passed through by the IM SDK without being processed. |

>? All the callbacks need to check whether the value of code is `ERR_SUC`. If not, the API failed to be called, and the specific cause of the failure is revealed by the parameters `code` and `desc`. For details, see [Error Codes](https://intl.cloud.tencent.com/document/product/1047/34348).


>?
>For the following APIs, the `TIMCommCallback` parameter `json_params` is a "" null string:
- [TIMLogin](https://intl.cloud.tencent.com/document/product/1047/34390)
- [TIMLogout](https://intl.cloud.tencent.com/document/product/1047/34390)
- [TIMMsgSaveMsg](https://intl.cloud.tencent.com/document/product/1047/34391)
- [TIMMsgReportReaded](https://intl.cloud.tencent.com/document/product/1047/34391)
- [TIMMsgRevoke](https://intl.cloud.tencent.com/document/product/1047/34391)
- [TIMMsgImportMsgList](https://intl.cloud.tencent.com/document/product/1047/34391)
- [TIMMsgDelete](https://intl.cloud.tencent.com/document/product/1047/34391)
- [TIMConvDelete](https://intl.cloud.tencent.com/document/product/1047/34557)
- [TIMGroupDelete](https://intl.cloud.tencent.com/document/product/1047/34393)
- [TIMGroupJoin](https://intl.cloud.tencent.com/document/product/1047/34393)
- [TIMGroupQuit](https://intl.cloud.tencent.com/document/product/1047/34393)
- [TIMGroupModifyGroupInfo](https://intl.cloud.tencent.com/document/product/1047/34393)
- [TIMGroupModifyMemberInfo](https://intl.cloud.tencent.com/document/product/1047/34393)
- [TIMGroupReportPendencyReaded](https://intl.cloud.tencent.com/document/product/1047/34393)
- [TIMGroupHandlePendency](https://intl.cloud.tencent.com/document/product/1047/34393)
- [TIMProfileModifySelfUserProfile](https://intl.cloud.tencent.com/document/product/1047/34558)
- [TIMFriendshipModifyFriendProfile](https://intl.cloud.tencent.com/document/product/1047/34559)
- [TIMFriendshipDeleteFriendGroup](https://intl.cloud.tencent.com/document/product/1047/34559)
- [TIMFriendshipReportPendencyReaded](https://intl.cloud.tencent.com/document/product/1047/34559)


**Example 1: JSON string of the TIMCommCallback parameter json_params for the API [TIMSetConfig](https://intl.cloud.tencent.com/document/product/1047/34388). For details on JSON keys, see [SetConfig](https://intl.cloud.tencent.com/document/product/1047/34551).**

```c
{
   "set_config_callback_log_level" : 2,
   "set_config_is_log_output_console" : true,
   "set_config_log_level" : 2,
   "set_config_proxy_info" : {
      "proxy_info_ip" : "",
      "proxy_info_port" : 0
   },
   "set_config_user_config" : {
      "user_config_group_getinfo_option" : {
         "get_info_option_custom_array" : [],
         "get_info_option_info_flag" : 0xffffffff,
         "get_info_option_role_flag" : 0
      },
      "user_config_group_member_getinfo_option" : {
         "get_info_option_custom_array" : [],
         "get_info_option_info_flag" : 0xffffffff,
         "get_info_option_role_flag" : 0
      },
      "user_config_is_ingore_grouptips_unread" : false,
      "user_config_is_read_receipt" : false,
      "user_config_is_sync_report" : false
   }
}
```


**Example 2: JSON string of the TIMCommCallback parameter json_params for the API [TIMConvCreate](https://intl.cloud.tencent.com/document/product/1047/34557). For details on JSON keys, see [ConvInfo](https://intl.cloud.tencent.com/document/product/1047/34551).**

```c
{
   "conv_active_time" : 1551269275,
   "conv_id" : "user2",
   "conv_is_has_draft" : false,
   "conv_is_has_lastmsg" : true,
   "conv_last_msg" : {
      "message_client_time" : 1551101578,
      "message_conv_id" : "user2",
      "message_conv_type" : 1,
      "message_elem_array" : [
         {
            "elem_type" : 0,
            "text_elem_content" : "12"
         }
      ],
      "message_is_from_self" : false,
      "message_is_read" : true,
      "message_rand" : 3726251374,
      "message_sender" : "user2",
      "message_seq" : 56858,
      "message_server_time" : 1551101578,
      "message_status" : 2
   },
   "conv_owner" : "",
   "conv_type" : 1,
   "conv_unread_num" : 1
}
```


**Example 3: JSON string of the TIMCommCallback parameter json_params for the API [TIMConvGetConvList](https://intl.cloud.tencent.com/document/product/1047/34557). For details on JSON keys, see [ConvInfo](https://intl.cloud.tencent.com/document/product/1047/34551).**

```c
[
   {
      "conv_active_time" : 1551269275,
      "conv_id" : "user2",
      "conv_is_has_draft" : false,
      "conv_is_has_lastmsg" : true,
      "conv_last_msg" : {
         "message_client_time" : 1551235066,
         "message_conv_id" : "user2",
         "message_conv_type" : 1,
         "message_elem_array" : [
            {
               "elem_type" : 0,
               "text_elem_content" : "ccccccccccccccccc"
            }
         ],
         "message_is_from_self" : true,
         "message_is_read" : true,
         "message_rand" : 1073033786,
         "message_sender" : "user1",
         "message_seq" : 16373,
         "message_server_time" : 1551235067,
         "message_status" : 2
      },
      "conv_owner" : "",
      "conv_type" : 1,
      "conv_unread_num" : 0
   }
]
```


**Example 4: JSON string of the TIMCommCallback parameter json_params for the API [TIMMsgSendNewMsg](https://intl.cloud.tencent.com/document/product/1047/34391). For details on JSON keys, see [Message](https://intl.cloud.tencent.com/document/product/1047/34551).**

```c
{
   "message_client_time" : 1558598732,
   "message_conv_id" : "asd12341",
   "message_conv_type" : 1,
   "message_custom_int" : 0,
   "message_custom_str" : "",
   "message_elem_array" : [
      {
         "elem_type" : 0,
         "text_elem_content" : "test"
      }
   ],
   "message_is_from_self" : true,
   "message_is_online_msg" : false,
   "message_is_peer_read" : false,
   "message_is_read" : true,
   "message_priority" : 1,
   "message_rand" : 1340036983,
   "message_sender" : "test_win_01",
   "message_seq" : 20447,
   "message_server_time" : 1558598733,
   "message_status" : 2
}
```


**Example 5: JSON string of the TIMCommCallback parameter json_params for the API [TIMMsgFindByMsgLocatorList](https://intl.cloud.tencent.com/document/product/1047/34391). For details on JSON keys, see [Message](https://intl.cloud.tencent.com/document/product/1047/34551).**

```c
[
   {
      "message_client_time" : 1551080111,
      "message_conv_id" : "user2",
      "message_conv_type" : 1,
      "message_elem_array" : [
         {
            "elem_type" : 0,
            "text_elem_content" : "123213213"
         }
      ],
      "message_is_from_self" : true,
      "message_is_read" : true,
      "message_rand" : 2130485001,
      "message_sender" : "user1",
      "message_seq" : 1,
      "message_server_time" : 1551080111,
      "message_status" : 2
   },
   ...
]
```


**Example 6: JSON string of the TIMCommCallback parameter json_params for the API [TIMMsgGetMsgList](https://intl.cloud.tencent.com/document/product/1047/34391). For details on JSON keys, see [Message](https://intl.cloud.tencent.com/document/product/1047/34551).**

```c
[
   {
      "message_client_time" : 1551080111,
      "message_conv_id" : "user2",
      "message_conv_type" : 1,
      "message_elem_array" : [
         {
            "elem_type" : 0,
            "text_elem_content" : "123213213"
         }
      ],
      "message_is_from_self" : true,
      "message_is_read" : true,
      "message_rand" : 2130485001,
      "message_sender" : "user1",
      "message_seq" : 1,
      "message_server_time" : 1551080111,
      "message_status" : 2
   },
   ...
]
```


**Example 7: JSON string of the TIMCommCallback parameter json_params for the API [TIMMsgDownloadElemToPath](https://intl.cloud.tencent.com/document/product/1047/34391). For details on JSON keys, see [MsgDownloadElemResult](https://intl.cloud.tencent.com/document/product/1047/34551).**

```c
{
  "msg_download_elem_result_current_size" : 10,
  "msg_download_elem_result_total_size" : 100
}
```


**Example 8: JSON string of the TIMCommCallback parameter json_params for the API [TIMMsgBatchSend](https://intl.cloud.tencent.com/document/product/1047/34391). For details on JSON keys, see [MsgBatchSendResult](https://intl.cloud.tencent.com/document/product/1047/34551).**

```c
[
   {
      "msg_batch_send_result_code" : 0,
      "msg_batch_send_result_desc" : "",
      "msg_batch_send_result_identifier" : "test_win_05",
      "msg_batch_send_result_msg" : {
         "message_client_time" : 1558598923,
         "message_conv_id" : "test_win_05",
         "message_conv_type" : 1,
         "message_custom_int" : 0,
         "message_custom_str" : "",
         "message_elem_array" : [
            {
               "elem_type" : 0,
               "text_elem_content" : "this is batch send msgs"
            }
         ],
         "message_is_from_self" : true,
         "message_is_online_msg" : false,
         "message_is_peer_read" : false,
         "message_is_read" : true,
         "message_priority" : 1,
         "message_rand" : 673379256,
         "message_sender" : "test_win_01",
         "message_seq" : 10274,
         "message_server_time" : 1558598924,
         "message_status" : 2
      }
   },
   {
      "msg_batch_send_result_code" : 0,
      "msg_batch_send_result_desc" : "",
      "msg_batch_send_result_identifier" : "test_win_02",
      "msg_batch_send_result_msg" : {
         "message_client_time" : 1558598923,
         "message_conv_id" : "test_win_02",
         "message_conv_type" : 1,
         "message_custom_int" : 0,
         "message_custom_str" : "",
         "message_elem_array" : [
            {
               "elem_type" : 0,
               "text_elem_content" : "this is batch send msgs"
            }
         ],
         "message_is_from_self" : true,
         "message_is_online_msg" : false,
         "message_is_peer_read" : false,
         "message_is_read" : true,
         "message_priority" : 1,
         "message_rand" : 673460408,
         "message_sender" : "test_win_01",
         "message_seq" : 10276,
         "message_server_time" : 1558598924,
         "message_status" : 2
      }
   }
]
```


**Example 9: JSON string of the TIMCommCallback parameter json_params for the API [TIMGroupCreate](https://intl.cloud.tencent.com/document/product/1047/34393). For details on JSON keys, see [CreateGroupResult](https://intl.cloud.tencent.com/document/product/1047/34551).**

```c
{
   "create_group_result_groupid" : "first group id"
}
```


**Example 10: JSON string of the TIMCommCallback parameter json_params for the API [TIMGroupInviteMember](https://intl.cloud.tencent.com/document/product/1047/34393). For details on JSON keys, see [GroupInviteMemberResult](https://intl.cloud.tencent.com/document/product/1047/34551).**

```c
[
   {
      "group_invite_member_result_identifier" : "user2",
      "group_invite_member_result_result" : 1
   },
   {
      "group_invite_member_result_identifier" : "user3",
      "group_invite_member_result_result" : 1
   }
]
```


**Example 11: JSON string of the TIMCommCallback parameter json_params for the API [TIMGroupDeleteMember](https://intl.cloud.tencent.com/document/product/1047/34393). For details on JSON keys, see [GroupDeleteMemberResult](https://intl.cloud.tencent.com/document/product/1047/34551).**

```c
[
   {
      "group_delete_member_result_identifier" : "user2",
      "group_delete_member_result_result" : 1
   },
   {
      "group_delete_member_result_identifier" : "user3",
      "group_delete_member_result_result" : 1
   }
]
```


**Example 12: JSON string of the TIMCommCallback parameter json_params for the API [TIMGroupGetJoinedGroupList](https://intl.cloud.tencent.com/document/product/1047/34393). For details on JSON keys, see [GroupBaseInfo](https://intl.cloud.tencent.com/document/product/1047/34551).**

```c
[
   {
      "group_base_info_face_url" : "group face url",
      "group_base_info_group_id" : "first group id",
      "group_base_info_group_name" : "first group name",
      "group_base_info_group_type" : "Public",
      "group_base_info_info_seq" : 7,
      "group_base_info_is_shutup_all" : false,
      "group_base_info_lastest_seq" : 0,
      "group_base_info_msg_flag" : 0,
      "group_base_info_readed_seq" : 0,
      "group_base_info_self_info" : {
         "group_self_info_join_time" : 1551344977,
         "group_self_info_msg_flag" : 0,
         "group_self_info_role" : 400,
         "group_self_info_unread_num" : 0
      }
   }
]
```


**Example 13: JSON string of the TIMCommCallback parameter json_params for the API [TIMGroupGetGroupInfoList](https://intl.cloud.tencent.com/document/product/1047/34393). For details on JSON keys, see [GetGroupInfoResult](https://intl.cloud.tencent.com/document/product/1047/34551).**

```c
[
   {
      "get_groups_info_result_code" : 0,
      "get_groups_info_result_desc" : "",
      "get_groups_info_result_info" : {
         "group_detial_info_add_option" : 2,
         "group_detial_info_create_time" : 1551344977,
         "group_detial_info_custom_info" : {},
         "group_detial_info_face_url" : "group face url",
         "group_detial_info_group_id" : "first group id",
         "group_detial_info_group_name" : "first group name",
         "group_detial_info_group_type" : "Public",
         "group_detial_info_info_seq" : 7,
         "group_detial_info_introduction" : "group introduction",
         "group_detial_info_is_shutup_all" : false,
         "group_detial_info_last_info_time" : 1551344977,
         "group_detial_info_last_msg_time" : 0,
         "group_detial_info_max_member_num" : 2000,
         "group_detial_info_member_num" : 1,
         "group_detial_info_next_msg_seq" : 0,
         "group_detial_info_notification" : "group notification",
         "group_detial_info_online_member_num" : 0,
         "group_detial_info_owener_identifier" : "user1",
         "group_detial_info_searchable" : 2,
         "group_detial_info_visible" : 2
      }
   }
]
```


**Example 14: JSON string of the TIMCommCallback parameter json_params for the API [TIMGroupGetMemberInfoList](https://intl.cloud.tencent.com/document/product/1047/34393). For details on JSON keys, see [GroupGetMemberInfoListResult](https://intl.cloud.tencent.com/document/product/1047/34551).**

```c
{
   "group_get_memeber_info_list_result_info_array" : [
      {
         "group_member_info_custom_info" : {},
         "group_member_info_identifier" : "user1",
         "group_member_info_join_time" : 1551344977,
         "group_member_info_member_role" : 400,
         "group_member_info_msg_flag" : 0,
         "group_member_info_msg_seq" : 0,
         "group_member_info_name_card" : "",
         "group_member_info_shutup_time" : 0
      }
   ],
   "group_get_memeber_info_list_result_next_seq" : 0
}
```


**Example 15: JSON string of the TIMCommCallback parameter json_params for the API [TIMGroupGetPendencyList](https://intl.cloud.tencent.com/document/product/1047/34393). For details on JSON keys, see [GroupPendencyResult](https://intl.cloud.tencent.com/document/product/1047/34551).**

```c
{
   "group_pendency_result_next_start_time" : 0,
   "group_pendency_result_pendency_array" : [
      {
         "group_pendency_add_time" : 1551414487947,
         "group_pendency_apply_invite_msg" : "Want Join Group, Thank you",
         "group_pendency_approval_msg" : "",
         "group_pendency_form_identifier" : "user2",
         "group_pendency_form_user_defined_data" : "",
         "group_pendency_group_id" : "four group id",
         "group_pendency_handle_result" : 0,
         "group_pendency_handled" : 0,
         "group_pendency_pendency_type" : 0,
         "group_pendency_to_identifier" : "user1",
         "group_pendency_to_user_defined_data" : ""
      }
   ],
   "group_pendency_result_read_time_seq" : 0,
   "group_pendency_result_unread_num" : 1
}
```


**Example 16: JSON string of the TIMCommCallback parameter json_params for the API [TIMProfileGetUserProfileList](https://intl.cloud.tencent.com/document/product/1047/34558). For details on JSON keys, see [UserProfile](https://intl.cloud.tencent.com/document/product/1047/34551).**

```c
[
   {
      "user_profile_add_permission" : 1,
      "user_profile_birthday" : 0,
      "user_profile_face_url" : "",
      "user_profile_gender" : 0,
      "user_profile_identifier" : "user1",
      "user_profile_language" : 0,
      "user_profile_level" : 0,
      "user_profile_location" : "",
      "user_profile_nick_name" : "User1NickName",
      "user_profile_role" : 0,
      "user_profile_self_signature" : ""
   },
   {
      "user_profile_add_permission" : 0,
      "user_profile_birthday" : 0,
      "user_profile_face_url" : "",
      "user_profile_gender" : 0,
      "user_profile_identifier" : "user2",
      "user_profile_language" : 0,
      "user_profile_level" : 0,
      "user_profile_location" : "",
      "user_profile_nick_name" : "",
      "user_profile_role" : 0,
      "user_profile_self_signature" : ""
   }
]
```


**Example 17: JSON string of the TIMCommCallback parameter json_params for the API [TIMFriendshipGetFriendProfileList](https://intl.cloud.tencent.com/document/product/1047/34559). For details on JSON keys, see [FriendProfile](https://intl.cloud.tencent.com/document/product/1047/34551).**

```c
[
   {
      "friend_profile_add_source" : "AddSource_Type_android",
      "friend_profile_add_time" : 1562229520,
      "friend_profile_add_wording" : "",
      "friend_profile_group_name_array" : [],
      "friend_profile_identifier" : "asd12341",
      "friend_profile_item_custom_string_array" : [
         {
            "friend_profile_custom_string_info_key" : "Tag_Profile_Custom_Str",
            "friend_profile_custom_string_info_value" : "qcloud"
         }
      ],
      "friend_profile_remark" : "",
      "friend_profile_user_profile" : {
         "user_profile_add_permission" : 0,
         "user_profile_birthday" : 20190419,
         "user_profile_face_url" : "faceUrl",
         "user_profile_gender" : 0,
         "user_profile_identifier" : "asd12341",
         "user_profile_item_custom_string_array" : [
            {
               "user_profile_custom_string_info_key" : "Tag_Profile_Custom_Str",
               "user_profile_custom_string_info_value" : "qcloud"
            }
         ],
         "user_profile_language" : 1,
         "user_profile_level" : 3,
         "user_profile_location" : "sz\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000\u0000",
         "user_profile_nick_name" : "nick_test23",
         "user_profile_role" : 4,
         "user_profile_self_signature" : "sig_test"
      }
   },
   {
      "friend_profile_add_source" : "AddSource_Type_Android",
      "friend_profile_add_time" : 1555659941,
      "friend_profile_add_wording" : "",
      "friend_profile_group_name_array" : [],
      "friend_profile_identifier" : "lttest1",
      "friend_profile_remark" : "",
      "friend_profile_user_profile" : {
         "user_profile_add_permission" : 0,
         "user_profile_birthday" : 0,
         "user_profile_face_url" : "",
         "user_profile_gender" : 0,
         "user_profile_identifier" : "lttest1",
         "user_profile_language" : 0,
         "user_profile_level" : 0,
         "user_profile_location" : "",
         "user_profile_nick_name" : "",
         "user_profile_role" : 0,
         "user_profile_self_signature" : ""
      }
   }
]
```


**Example 18: JSON string of the TIMCommCallback parameter json_params for the API [TIMFriendshipAddFriend](https://intl.cloud.tencent.com/document/product/1047/34559). For details on JSON keys, see [FriendResult](https://intl.cloud.tencent.com/document/product/1047/34551).**

```c
{
   "friend_result_code" : 0,
   "friend_result_desc" : "",
   "friend_result_identifier" : "user4"
}
```


**Example 19: JSON string of the TIMCommCallback parameter json_params for the API [TIMFriendshipDeleteFriend](https://intl.cloud.tencent.com/document/product/1047/34559). For details on JSON keys, see [FriendResult](https://intl.cloud.tencent.com/document/product/1047/34551).**

```c
[
   {
      "friend_result_code" : 0,
      "friend_result_desc" : "OK",
      "friend_result_identifier" : "user4"
   }
]
```


**Example 20: JSON string of the TIMCommCallback parameter json_params for the API [TIMFriendshipHandleFriendAddRequest](https://intl.cloud.tencent.com/document/product/1047/34559). For details on JSON keys, see [FriendResult](https://intl.cloud.tencent.com/document/product/1047/34551).**

```c
{
   "friend_result_code" : 0,
   "friend_result_desc" : "",
   "friend_result_identifier" : "user1"
}
```


**Example 21: JSON string of the TIMCommCallback parameter json_params for the API [TIMFriendshipGetPendencyList](https://intl.cloud.tencent.com/document/product/1047/34559). For details on JSON keys, see [PendencyPage](https://intl.cloud.tencent.com/document/product/1047/34551).**

```c
{
   "pendency_page_current_seq" : 2,
   "pendency_page_pendency_info_array" : [
      {
         "friend_add_pendency_info_add_source" : "AddSource_Type_Windows",
         "friend_add_pendency_info_add_time" : 1563026447,
         "friend_add_pendency_info_add_wording" : "I am Iron Man",
         "friend_add_pendency_info_idenitifer" : "user4",
         "friend_add_pendency_info_nick_name" : "change my nick name",
         "friend_add_pendency_info_type" : 1
      }
   ],
   "pendency_page_start_time" : 0,
   "pendency_page_unread_num" : 0
}
```


**Example 22: JSON string of the TIMCommCallback parameter json_params for the API [TIMFriendshipDeletePendency](https://intl.cloud.tencent.com/document/product/1047/34559). For details on JSON keys, see [FriendResult](https://intl.cloud.tencent.com/document/product/1047/34551).**

```c
[
   {
      "friend_result_code" : 0,
      "friend_result_desc" : "OK",
      "friend_result_identifier" : "user4"
   }
]
```


**Example 23: JSON string of the TIMCommCallback parameter json_params for the API [TIMFriendshipCheckFriendType](https://intl.cloud.tencent.com/document/product/1047/34559). For details on JSON keys, see [FriendshipCheckFriendTypeResult](https://intl.cloud.tencent.com/document/product/1047/34551).**

```c
[
   {
      "friendship_check_friendtype_result_code" : 0,
      "friendship_check_friendtype_result_desc" : "",
      "friendship_check_friendtype_result_identifier" : "user4",
      "friendship_check_friendtype_result_relation" : 3
   }
]
```


**Example 24: JSON string of the TIMCommCallback parameter json_params for the API [TIMFriendshipCreateFriendGroup](https://intl.cloud.tencent.com/document/product/1047/34559). For details on JSON keys, see [FriendResult](https://intl.cloud.tencent.com/document/product/1047/34551).**

```c
[
   {
      "friend_result_code" : 0,
      "friend_result_desc" : "",
      "friend_result_identifier" : "user4"
   },
   {
      "friend_result_code" : 0,
      "friend_result_desc" : "",
      "friend_result_identifier" : "user10"
   }
]
```


**Example 25: JSON string of the TIMCommCallback parameter json_params for the API [TIMFriendshipGetFriendGroupList](https://intl.cloud.tencent.com/document/product/1047/34559). For details on JSON keys, see [FriendGroupInfo](https://intl.cloud.tencent.com/document/product/1047/34551).**

```c
[
   {
      "friend_group_info_count" : 2,
      "friend_group_info_identifier_array" : [ "user4", "user10" ],
      "friend_group_info_name" : "Group123"
   }
]
```


**Example 26: JSON string of the TIMCommCallback parameter json_params for the API [TIMFriendshipModifyFriendGroup](https://intl.cloud.tencent.com/document/product/1047/34559). For details on JSON keys, see [FriendResult](https://intl.cloud.tencent.com/document/product/1047/34551).**

```c
[
   {
      "friend_result_code" : 30001,
      "friend_result_desc" : "Err_SNS_GroupUpdate_Friend_Not_Exist",
      "friend_result_identifier" : "user5"
   },
   {
      "friend_result_code" : 0,
      "friend_result_desc" : "",
      "friend_result_identifier" : "user4"
   },
   {
      "friend_result_code" : 0,
      "friend_result_desc" : "",
      "friend_result_identifier" : "user9"
   }
]
```


**Example 27: JSON string of the TIMCommCallback parameter json_params for the API [TIMFriendshipAddToBlackList](https://intl.cloud.tencent.com/document/product/1047/34559). For details on JSON keys, see [FriendResult](https://intl.cloud.tencent.com/document/product/1047/34551).**

```c
[
   {
      "friend_result_code" : 0,
      "friend_result_desc" : "OK",
      "friend_result_identifier" : "user5"
   },
   {
      "friend_result_code" : 0,
      "friend_result_desc" : "OK",
      "friend_result_identifier" : "user10"
   }
]
```


**Example 28: JSON string of the TIMCommCallback parameter json_params for the API [TIMFriendshipGetBlackList](https://intl.cloud.tencent.com/document/product/1047/34559). For details on JSON keys, see [FriendProfile](https://intl.cloud.tencent.com/document/product/1047/34551).**

```c
[
   {
      "friend_profile_add_source" : "AddSource_Type_Android",
      "friend_profile_add_time" : 1555656865,
      "friend_profile_add_wording" : "",
      "friend_profile_group_name_array" : [ "Group123" ],
      "friend_profile_identifier" : "user10",
      "friend_profile_remark" : "",
      "friend_profile_user_profile" : {
         "user_profile_add_permission" : 0,
         "user_profile_birthday" : 0,
         "user_profile_face_url" : "",
         "user_profile_gender" : 0,
         "user_profile_identifier" : "user10",
         "user_profile_language" : 0,
         "user_profile_level" : 0,
         "user_profile_location" : "",
         "user_profile_nick_name" : "",
         "user_profile_role" : 0,
         "user_profile_self_signature" : ""
      }
   },
   {
      "friend_profile_add_source" : "",
      "friend_profile_add_time" : 0,
      "friend_profile_add_wording" : "",
      "friend_profile_group_name_array" : [],
      "friend_profile_identifier" : "user5",
      "friend_profile_remark" : "",
      "friend_profile_user_profile" : {
         "user_profile_add_permission" : 0,
         "user_profile_birthday" : 0,
         "user_profile_face_url" : "",
         "user_profile_gender" : 0,
         "user_profile_identifier" : "user5",
         "user_profile_language" : 0,
         "user_profile_level" : 0,
         "user_profile_location" : "",
         "user_profile_nick_name" : "",
         "user_profile_role" : 0,
         "user_profile_self_signature" : ""
      }
   }
]
```


**Example 29: JSON string of the TIMCommCallback parameter json_params for the API [TIMFriendshipDeleteFromBlackList](https://intl.cloud.tencent.com/document/product/1047/34559). For details on JSON keys, see [FriendResult](https://intl.cloud.tencent.com/document/product/1047/34551).**

```c
[
   {
      "friend_result_code" : 0,
      "friend_result_desc" : "OK",
      "friend_result_identifier" : "user5"
   },
   {
      "friend_result_code" : 0,
      "friend_result_desc" : "OK",
      "friend_result_identifier" : "user10"
   }
]
```
