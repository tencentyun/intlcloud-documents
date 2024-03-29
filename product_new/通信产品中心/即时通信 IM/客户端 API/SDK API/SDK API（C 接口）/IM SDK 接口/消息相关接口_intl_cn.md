消息介绍请参考 [单聊消息](https://intl.cloud.tencent.com/document/product/1047/33523)、[群组消息](https://intl.cloud.tencent.com/document/product/1047/33526) 和 [消息格式描述](https://intl.cloud.tencent.com/document/product/1047/33527)。

## TIMMsgSendNewMsg

发送新消息。

**原型**

```c
TIM_DECL int TIMMsgSendNewMsg(const char* conv_id, enum TIMConvType conv_type, const char* json_msg_param, TIMCommCallback cb, const void* user_data);
```

**参数**

| 参数 | 类型 | 含义 |
|-----|-----|-----|
| conv_id | const char\* | 会话的 ID  |
| conv_type | enum TIMConvType | 会话类型，请参考 [TIMConvType](https://intl.cloud.tencent.com/document/product/1047/34551#timconvtype)  |
| json_msg_param | const char\* | 消息 JSON 字符串 |
| cb | TIMCommCallback | 发送新消息成功与否的回调。回调函数定义请参考 [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550#timcommcallback)  |
| user_data | const void\* | 用户自定义数据，IM SDK 只负责传回给回调函数 cb，不做任何处理 |

**返回值**

| 类型 | 含义 |
|-----|-----|
| int | 返回 TIM_SUCC 表示接口调用成功（接口只有返回 TIM_SUCC，回调 cb 才会被调用），其他值表示接口调用失败。每个返回值的定义请参考 [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551#timresult)  |

>?
>- 发送新消息，单聊消息和群消息的发送均采用此接口。
  >    - 发送单聊消息时`conv_id`为对方的 UserID，`conv_type`为`kTIMConv_C2C`。
  >    - 发送群聊消息时`conv_id`为群 ID，`conv_type`为`kTIMConv_Group`。
>- 发送消息时不能发送`kTIMElem_GroupTips`、`kTIMElem_GroupReport`，他们由为后台下发，用于更新（通知）群的信息。可以的发送消息内元素。
  >    - 文本消息元素，请参考 [TextElem](https://intl.cloud.tencent.com/document/product/1047/34551#textelem)。
  >    - 表情消息元素，请参考 [FaceElem](https://intl.cloud.tencent.com/document/product/1047/34551#faceelem)。
  >    - 位置消息元素，请参考 [LocationElem](https://intl.cloud.tencent.com/document/product/1047/34551#locationelem)。
  >    - 图片消息元素，请参考 [ImageElem](https://intl.cloud.tencent.com/document/product/1047/34551#imageelem)。
  >    - 声音消息元素，请参考 [SoundElem](https://intl.cloud.tencent.com/document/product/1047/34551#soundelem)。
  >    -  自定义消息元素，请参考 [CustomElem](https://intl.cloud.tencent.com/document/product/1047/34551#customelem)。
  >    -  文件消息元素，请参考 [FileElem](https://intl.cloud.tencent.com/document/product/1047/34551#fileelem)。
  >    - 视频消息元素，请参考 [VideoElem](https://intl.cloud.tencent.com/document/product/1047/34551#videoelem)。


**示例**

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
        // 消息发送失败
        return;
    }
    // 消息发送成功
}, this);

// json_value_msg.toStyledString().c_str() 得到 json_msg_param JSON 字符串如下
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

消息上报已读。

**原型**

```c
TIM_DECL int TIMMsgReportReaded(const char* conv_id, enum TIMConvType conv_type, const char* json_msg_param, TIMCommCallback cb, const void* user_data);
```

**参数**

| 参数 | 类型 | 含义 |
|-----|-----|-----|
| conv_id | const char\* | 会话的 ID  |
| conv_type | enum TIMConvType | 会话类型，请参考 [TIMConvType](https://intl.cloud.tencent.com/document/product/1047/34551#timconvtype)  |
| json_msg_param | const char\* | 消息 JSON 字符串 |
| cb | TIMCommCallback | 消息上报已读成功与否的回调。回调函数定义请参考 [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550#timcommcallback)  |
| user_data | const void\* | 用户自定义数据，IM SDK 只负责传回给回调函数 cb，不做任何处理 |

**返回值**

| 类型 | 含义 |
|-----|-----|
| int | 返回 TIM_SUCC 表示接口调用成功（接口只有返回 TIM_SUCC，回调 cb 才会被调用），其他值表示接口调用失败。每个返回值的定义请参考 [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551#timresult)  |

>?`json_msg_param`可以填`NULL`空字符串指针或者""空字符串，此时以会话当前最新消息的时间戳（如果会话存在最新消息）或当前时间为已读时间戳上报。当要指定消息时，则以该指定消息的时间戳为已读时间戳上报，最好用接收新消息获取的消息数组里面的消息 JSON 或者用消息定位符查找到的消息 JSON，避免重复构造消息 JSON。


## TIMMsgRevoke

消息撤回。

**原型**

```c
TIM_DECL int TIMMsgRevoke(const char* conv_id, enum TIMConvType conv_type, const char* json_msg_param, TIMCommCallback cb, const void* user_data);
```

**参数**

| 参数 | 类型 | 含义 |
|-----|-----|-----|
| conv_id | const char\* | 会话的 ID  |
| conv_type | enum TIMConvType | 会话类型，请参考 [TIMConvType](https://intl.cloud.tencent.com/document/product/1047/34551#timconvtype)  |
| json_msg_param | const char\* | 消息 JSON 字符串 |
| cb | TIMCommCallback | 消息撤回成功与否的回调。回调函数定义请参考 [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550#timcommcallback)  |
| user_data | const void\* | 用户自定义数据，IM SDK 只负责传回给回调函数 cb，不做任何处理 |

**返回值**

| 类型 | 含义 |
|-----|-----|
| int | 返回 TIM_SUCC 表示接口调用成功（接口只有返回 TIM_SUCC，回调 cb 才会被调用），其他值表示接口调用失败。每个返回值的定义请参考 [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551#timresult)  |

>?消息撤回。使用保存的消息 JSON 或者用消息定位符查找到的消息 JSON，避免重复构造消息 JSON。


**示例**

```c
Json::Value json_value_text;
json_value_text[kTIMElemType] = kTIMElem_Text;
json_value_text[kTIMTextElemContent] = "send text";
Json::Value json_value_msg;
json_value_msg[kTIMMsgElemArray].append(json_value_text);

int ret = TIMMsgSendNewMsg("test_win_03", kTIMConv_C2C, json_value_msg.toStyledString().c_str(), [](int32_t code, const char* desc, const char* json_param, const void* user_data) {
    if (ERR_SUCC != code) {
        // 消息发送失败
        return;
    }
    // 消息发送成功 json_param 返回发送后的消息 JSON 字符串
    TIMMsgRevoke("test_win_03", kTIMConv_C2C, json_param, [](int32_t code, const char* desc, const char* json_param, const void* user_data) {
        if (ERR_SUCC != code) {
            // 消息撤回失败
            return;
        }
        // 消息撤回成功

    }, user_data);
}, this);
```


## TIMMsgFindByMsgLocatorList

根据消息定位精准查找指定会话的消息。

**原型**

```c
TIM_DECL int TIMMsgFindByMsgLocatorList(const char* conv_id, enum TIMConvType conv_type, const char* json_msg_Locator_array, TIMCommCallback cb, const void* user_data);
```

**参数**

| 参数 | 类型 | 含义 |
|-----|-----|-----|
| conv_id | const char\* | 会话的 ID  |
| conv_type | enum TIMConvType | 会话类型，请参考 [TIMConvType](https://intl.cloud.tencent.com/document/product/1047/34551#timconvtype)  |
| json_msg_Locator_array | const char\* | 消息定位符数组 |
| cb | TIMCommCallback | 根据消息定位精准查找指定会话的消息成功与否的回调。回调函数定义和参数解析请参考 [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550#timcommcallback)  |
| user_data | const void\* | 用户自定义数据，IM SDK 只负责传回给回调函数 cb，不做任何处理 |

**返回值**

| 类型 | 含义 |
|-----|-----|
| int | 返回 TIM_SUCC 表示接口调用成功（接口只有返回 TIM_SUCC，回调 cb 才会被调用），其他值表示接口调用失败。每个返回值的定义请参考 [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551#timresult)  |

>?
>- 此接口根据消息定位符精准查找指定会话的消息，该功能一般用于消息撤回时查找指定消息等。
>- 一个消息定位符对应一条消息。


**示例**

```c
Json::Value json_msg_locator;                      //一条消息对应一个消息定位符(精准定位)
json_msg_locator[kTIMMsgLocatorIsRevoked] = false; //消息是否被撤回
json_msg_locator[kTIMMsgLocatorTime] = 123;        //填入消息的时间
json_msg_locator[kTIMMsgLocatorSeq] = 1;           
json_msg_locator[kTIMMsgLocatorIsSelf] = false;    
json_msg_locator[kTIMMsgLocatorRand] = 12345678;   

Json::Value json_msg_locators;
json_msg_locators.append(json_msg_locator);
TIMMsgFindByMsgLocatorList("user2", kTIMConv_C2C, json_msg_locators.toStyledString().c_str(), [](int32_t code, const char* desc, const char* json_param, const void* user_data) {
    
}, nullptr);

// json_msg_locators.toStyledString().c_str() 的到 json_msg_Locator_array JSON 字符串如下
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

导入消息列表到指定会话。

**原型**

```c
TIM_DECL int TIMMsgImportMsgList(const char* conv_id, enum TIMConvType conv_type, const char* json_msg_array, TIMCommCallback cb, const void* user_data);
```

**参数**

| 参数 | 类型 | 含义 |
|-----|-----|-----|
| conv_id | const char\* | 会话的 ID  |
| conv_type | enum TIMConvType | 会话类型，请参考 [TIMConvType](https://intl.cloud.tencent.com/document/product/1047/34551#timconvtype)  |
| json_msg_array | const char\* | 消息数组 |
| cb | TIMCommCallback | 导入消息列表到指定会话成功与否的回调。回调函数定义请参考 [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550#timcommcallback)  |
| user_data | const void\* | 用户自定义数据，IM SDK 只负责传回给回调函数 cb，不做任何处理 |

**返回值**

| 类型 | 含义 |
|-----|-----|
| int | 返回 TIM_SUCC 表示接口调用成功（接口只有返回 TIM_SUCC，回调 cb 才会被调用），其他值表示接口调用失败。每个返回值的定义请参考 [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551#timresult)  |

>?批量导入消息，可以自己构造消息去导入。也可以将之前要导入的消息数组 JSON 保存，然后导入的时候直接调用接口，避免构造消息数组。


**示例**

```c
Json::Value json_value_elem; //构造消息文本元素
json_value_elem[kTIMElemType] = TIMElemType::kTIMElem_Text;
json_value_elem[kTIMTextElemContent] = "this is import msg";

Json::Value json_value_msg; //构造消息
json_value_msg[kTIMMsgSender] = login_id;
json_value_msg[kTIMMsgClientTime] = time(NULL);
json_value_msg[kTIMMsgServerTime] = time(NULL);
json_value_msg[kTIMMsgElemArray].append(json_value_elem);

Json::Value json_value_msgs;  //消息数组
json_value_msgs.append(json_value_msg);

TIMMsgImportMsgList("user2", kTIMConv_C2C, json_value_msgs.toStyledString().c_str(), [](int32_t code, const char* desc, const char* json_param, const void* user_data) {
    
}, nullptr);

// json_value_msgs.toStyledString().c_str() 得到 json_msg_array JSON 字符串如下
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

保存自定义消息。

**原型**

```c
TIM_DECL int TIMMsgSaveMsg(const char* conv_id, enum TIMConvType conv_type, const char* json_msg_param, TIMCommCallback cb, const void* user_data);
```

**参数**

| 参数 | 类型 | 含义 |
|-----|-----|-----|
| conv_id | const char\* | 会话的 ID  |
| conv_type | enum TIMConvType | 会话类型，请参考 [TIMConvType](https://intl.cloud.tencent.com/document/product/1047/34551#timconvtype)  |
| json_msg_param | const char\* | 消息 JSON 字符串 |
| cb | TIMCommCallback | 保存自定义消息成功与否的回调。回调函数定义请参考 [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550#timcommcallback)  |
| user_data | const void\* | 用户自定义数据，IM SDK 只负责传回给回调函数 cb，不做任何处理 |

**返回值**

| 类型 | 含义 |
|-----|-----|
| int | 返回 TIM_SUCC 表示接口调用成功（接口只有返回 TIM_SUCC，回调 cb 才会被调用），其他值表示接口调用失败。每个返回值的定义请参考 [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551#timresult)  |

>?消息保存接口，一般是自己构造一个消息 JSON 字符串，然后保存到指定会话。


## TIMMsgGetMsgList

获取指定会话的消息列表。

**原型**

```c
TIM_DECL int TIMMsgGetMsgList(const char* conv_id, enum TIMConvType conv_type, const char* json_get_msg_param, TIMCommCallback cb, const void* user_data);
```

**参数**

| 参数 | 类型 | 含义 |
|-----|-----|-----|
| conv_id | const char\* | 会话的 ID  |
| conv_type | enum TIMConvType | 会话类型，请参考 [TIMConvType](https://intl.cloud.tencent.com/document/product/1047/34551#timconvtype)  |
| json_get_msg_param | const char\* | 消息获取参数 |
| cb | TIMCommCallback | 获取指定会话的消息列表成功与否的回调。回调函数定义和参数解析请参考 [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550#timcommcallback)  |
| user_data | const void\* | 用户自定义数据，IM SDK 只负责传回给回调函数 cb，不做任何处理 |

**返回值**

| 类型 | 含义 |
|-----|-----|
| int | 返回 TIM_SUCC 表示接口调用成功（接口只有返回 TIM_SUCC，回调 cb 才会被调用），其他值表示接口调用失败。每个返回值的定义请参考 [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551#timresult)  |

>?从`kTIMMsgGetMsgListParamLastMsg`指定的消息开始获取本地消息列表，kTIMMsgGetMsgListParamCount  为要获取的消息数目。kTIMMsgGetMsgListParamLastMsg 可以不指定，不指定时表示以会话最新的消息为`LastMsg`。若指定`kTIMMsgGetMsgListParamIsRamble`为 true 则本地消息获取不够指定数目时，会去获取云端漫游消息。`kTIMMsgGetMsgListParamIsForward`为 true 时表示获取比`kTIMMsgGetMsgListParamLastMsg`新的消息，为 false 时表示获取比`kTIMMsgGetMsgListParamLastMsg`旧的消息。


**示例：获取 C2C 会话`Windows-02`消息列表**

```c
Json::Value json_msg(Json::objectValue); // 构造 Message
Json::Value json_get_msg_param;
json_get_msg_param[kTIMMsgGetMsgListParamLastMsg] = json_msg;
json_get_msg_param[kTIMMsgGetMsgListParamIsRamble] = false;
json_get_msg_param[kTIMMsgGetMsgListParamIsForward] = true;
json_get_msg_param[kTIMMsgGetMsgListParamCount] = 100;

int ret = TIMMsgGetMsgList("Windows-02", kTIMConv_C2C, json_get_msg_param.toStyledString().c_str(), [](int32_t code, const char* desc, const char* json_params, const void* user_data) {
}, this);

// json_get_msg_param.toStyledString().c_str() 得到 json_get_msg_param JSON 字符串如下
{
   "msg_getmsglist_param_count" : 100,
   "msg_getmsglist_param_is_forward" : true,
   "msg_getmsglist_param_is_remble" : false,
   "msg_getmsglist_param_last_msg" : {}
}
```


## TIMMsgDelete

删除指定会话的消息。

**原型**

```c
TIM_DECL int TIMMsgDelete(const char* conv_id, enum TIMConvType conv_type, const char* json_msgdel_param, TIMCommCallback cb, const void* user_data);
```

**参数**

| 参数 | 类型 | 含义 |
|-----|-----|-----|
| conv_id | const char\* | 会话的 ID  |
| conv_type | enum TIMConvType | 会话类型，请参考 [TIMConvType](https://intl.cloud.tencent.com/document/product/1047/34551#timconvtype)  |
| json_msgdel_param | const char\* | 消息获取参数 |
| cb | TIMCommCallback | 删除指定会话的消息成功与否的回调。回调函数定义请参考 [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550#timcommcallback)  |
| user_data | const void\* | 用户自定义数据，IM SDK 只负责传回给回调函数 cb，不做任何处理 |

**返回值**

| 类型 | 含义 |
|-----|-----|
| int | 返回 TIM_SUCC 表示接口调用成功（接口只有返回 TIM_SUCC，回调 cb 才会被调用），其他值表示接口调用失败。每个返回值的定义请参考 [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551#timresult)  |

>?
>- 当设置`kTIMMsgDeleteParamMsg`时，在会话中删除指定本地消息。
>- 当未设置`kTIMMsgDeleteParamMsg`时，`kTIMMsgDeleteParamIsRamble`为 false 表示删除会话所有本地消息，true  表示删除会话所有漫游消息（5.5.904 及以后的版本支持）。
>- 一般直接使用保存的消息 JSON，或者通过消息定位符查找得到的 JSON。不用删除的时候构造消息 JSON。


**示例**

```c
Json::Value json_value_msg(Json::objectValue);
Json::Value json_value_msgdelete;
json_value_msgdelete[kTIMMsgDeleteParamIsRamble] = false;
json_value_msgdelete[kTIMMsgDeleteParamMsg] = json_value_msg;
TIMMsgDelete("user2", kTIMConv_C2C, json_value_msgdelete.toStyledString().c_str(), [](int32_t code, const char* desc, const char* json_param, const void* user_data) {

}, nullptr);

// json_value_msgdelete.toStyledString().c_str() 得到 json_msgdel_param JSON 字符串如下
{
  "msg_delete_param_is_remble" : false,
  "msg_delete_param_msg" : {}
}
```


## TIMMsgDownloadElemToPath

下载消息内元素到指定文件路径（图片、视频、音频、文件）。

**原型**

```c
TIM_DECL int TIMMsgDownloadElemToPath(const char* json_download_elem_param, const char* path, TIMCommCallback cb, const void* user_data);
```

**参数**

| 参数 | 类型 | 含义 |
|-----|-----|-----|
| json_download_elem_param | const char\* | 下载的参数 JSON 字符串 |
| path | const char\* | 下载文件保存路径 |
| cb | TIMCommCallback | 下载成功与否的回调以及下载进度回调。回调函数定义和参数解析请参考 [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550#timcommcallback)  |
| user_data | const void\* | 用户自定义数据，IM SDK 只负责传回给回调函数 cb，不做任何处理 |

**返回值**

| 类型 | 含义 |
|-----|-----|
| int | 返回 TIM_SUCC 表示接口调用成功（接口只有返回 TIM_SUCC，回调 cb 才会被调用），其他值表示接口调用失败。每个返回值的定义请参考 [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551#timresult)  |

>?此接口用于下载消息内图片、文件、声音、视频等元素。下载的参数kTIMMsgDownloadElemParamFlag、kTIMMsgDownloadElemParamId、kTIMMsgDownloadElemParamBusinessId、kTIMMsgDownloadElemParamUrl  均可以在相应元素内找到。其中`kTIMMsgDownloadElemParamType`为下载文件类型 [TIMDownloadType](https://intl.cloud.tencent.com/document/product/1047/34551#timdownloadtype)。


**示例**

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

群发消息，该接口不支持向群组发送消息。

**原型**

```c
TIM_DECL int TIMMsgBatchSend(const char* json_batch_send_param, TIMCommCallback cb, const void* user_data);
```

**参数**

| 参数 | 类型 | 含义 |
|-----|-----|-----|
| json_batch_send_param | const char\* | 群发消息 JSON 字符串 |
| cb | TIMCommCallback | 群发消息成功与否的回调。回调函数定义和参数解析请参考 [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550#timcommcallback)  |
| user_data | const void\* | 用户自定义数据，IM SDK 只负责传回给回调函数 cb，不做任何处理 |

**返回值**

| 类型 | 含义 |
|-----|-----|
| int | 返回 TIM_SUCC 表示接口调用成功（接口只有返回 TIM_SUCC，回调 cb 才会被调用），其他值表示接口调用失败。每个返回值的定义请参考 [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551#timresult)  |

>?批量发送消息的接口，每个 UserID 发送成功与否，通过回调 cb 返回。


**示例**

```c
//构造消息文本元素
Json::Value json_value_elem;
json_value_elem[kTIMElemType] = TIMElemType::kTIMElem_Text;
json_value_elem[kTIMTextElemContent] = "this is batch send msg";
//构造消息
Json::Value json_value_msg;
json_value_msg[kTIMMsgSender] = login_id;
json_value_msg[kTIMMsgClientTime] = time(NULL);
json_value_msg[kTIMMsgServerTime] = time(NULL);
json_value_msg[kTIMMsgElemArray].append(json_value_elem);

// 构造批量发送 ID 数组列表
Json::Value json_value_ids(Json::arrayValue);
json_value_ids.append("user2");
json_value_ids.append("user3");
// 构造批量发送接口参数
Json::Value json_value_batchsend;
json_value_batchsend[kTIMMsgBatchSendParamIdentifierArray] = json_value_ids;
json_value_batchsend[kTIMMsgBatchSendParamMsg] = json_value_msg;
int ret = TIMMsgBatchSend(json_value_batchsend.toStyledString().c_str(), [](int32_t code, const char* desc, const char* json_param, const void* user_data) {
}, nullptr);

// json_value_batchsend.toStyledString().c_str() 得到 json_batch_send_param JSON 字符串如下
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


