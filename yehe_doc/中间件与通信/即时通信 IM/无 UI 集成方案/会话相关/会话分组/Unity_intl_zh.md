## 功能描述
在某些场景下，您可能需要对会话进行分组，例如分为 "产品体验"、"需求研发" 等，您可以调用以下接口实现。
> ?
- 该功能仅对旗舰版客户开放，购买 [旗舰版](https://buy.cloud.tencent.com/avc?from=17220) 后可使用。
- 该功能仅增强版 Native SDK 6.5 及以上版本支持。

## 会话分组

### 新建会话分组
您可以调用 `ConvCreateConversationGroup` ([点击查看详情](https://comm.qq.com/im/doc/unity/zh/api/ConvApi/ConvCreateConversationGroup.html)) 接口新建会话分组。
>? 会话分组最大支持 20 个，超过后创建新的分组会报 `51010` 错误，不再使用的分组请及时删除。

| 属性               | 含义         | 说明                                                     |
| ------------------ | ------------ | -------------------------------------------------------- |
| groupName          | 会话分组名   | 长度要大于 0，最大支持 32 bytes，超过后会报 `51011` 错误 |
| conversationIDList | 会话 ID 列表 | 不能为空                                                 |

示例代码如下：

```c#
    //创建会话分组
    TIMResult res = TencentIMSDK.ConvCreateConversationGroup("groupName", new List<string> {
      conv_id
    }, (int code, string desc, List<ConversationOperationResult> results, string user_data)=>{
      // 创建会话分组异步结果
    });
```


### 删除会话分组
您可以调用 `ConvDeleteConversationGroup` ([点击查看详情](https://comm.qq.com/im/doc/unity/zh/api/ConvApi/ConvDeleteConversationGroup.html)) 接口删除会话分组。
>? 如果会话分组不存在，删除对应分组会报 `51009` 错误。

示例代码如下：

```c#
    //删除会话分组
    TIMResult res = TencentIMSDK.ConvDeleteConversationGroup("groupName", (int code, string desc, string result, string user_data)=>{
      // 删除会话分组异步结果
    });
```

### 重命名会话分组
您可以调用 `ConvRenameConversationGroup` ([点击查看详情](https://comm.qq.com/im/doc/unity/zh/api/ConvApi/ConvRenameConversationGroup.html)) 接口重命名会话分组。

示例代码如下：

```c#
    //重命名会话分组
    TIMResult res = TencentIMSDK.ConvRenameConversationGroup("oldGroupName", "newGroupName", (int code, string desc, string result, string user_data)=>{
      // 重命名会话分组异步结果
    });
```

### 获取会话分组列表
您可以调用 `ConvGetConversationGroupList` ([点击查看详情](https://comm.qq.com/im/doc/unity/zh/api/ConvApi/ConvGetConversationGroupList.html)) 接口获取会话分组列表。

示例代码如下：

```c#
    //获取会话分组列表
    TIMResult res = TencentIMSDK.ConvGetConversationGroupList((int code, string desc, List<string> results, string user_data)=>{
      // 获取会话分组列表异步结果
    });
```


如果需要获取分组下面的会话列表，可以调用 `ConvGetConversationListByFilter`  ([点击查看详情](https://comm.qq.com/im/doc/unity/zh/api/ConvApi/ConvGetConversationListByFilter.html)) 接口获取。

示例代码如下：

```c#
    //获取会话列表
    ConversationListFilter filter = new ConversationListFilter
    {
        conversation_list_filter_conv_type: TIMConvType.kTIMConv_C2C,//会话类型
        conversation_list_filter_mark_type: TIMConversationMarkType.kTIMConversationMarkTypeStar,//会话标记类型
        conversation_list_filter_conversation_group: "groupName"//拉取的群组名
    };
    ulong next_seq = 0; // 拉取游标
    uint count = 10; // 拉取数量
    //获取会话列表的高级接口
    TIMResult res = TencentIMSDK.ConvGetConversationListByFilter(filter, next_seq, count, (int code, string desc, ConversationListResult result, string user_data)=>{
      // 获取会话列表异步结果
      if (code == 0) {
        //拉取成功
        bool isFinished = result.conversation_list_result_is_finished; //是否拉取完
        next_seq = result.conversation_list_result_next_seq; //后续分页拉取的游标
        var conversationList = result.conversation_list_result_conv_list; //此次拉取到的消息列表
        //如果没有拉取完，使用返回的nextSeq继续拉取直到isFinished为true
      }
    });
```

### 添加会话到一个分组
当分组创建成功后，您可以调用 `ConvAddConversationsToGroup` ([点击查看详情](https://comm.qq.com/im/doc/unity/zh/api/ConvApi/ConvAddConversationsToGroup.html)) 接口添加一个新会话到分组。

示例代码如下：

```c#
    //添加会话到一个会话分组
    TIMResult res = TencentIMSDK.ConvAddConversationsToGroup("groupName", new List<string> {
      conv_id
    }, (int code, string desc, List<ConversationOperationResult> results, string user_data)=>{
      // 添加会话到一个会话分组异步结果
    });
```


### 从分组中删除某会话
您可以调用 `ConvDeleteConversationsFromGroup` ([点击查看详情](https://comm.qq.com/im/doc/unity/zh/api/ConvApi/ConvDeleteConversationsFromGroup.html)) 从分组中删除某会话。

示例代码如下：

```c#
    //从一个会话分组中删除会话
    TIMResult res = TencentIMSDK.ConvDeleteConversationsFromGroup("groupName", new List<string> {
      conv_id
    }, (int code, string desc, List<ConversationOperationResult> results, string user_data)=>{
      // 从一个会话分组中删除会话异步结果
    });
```


### 监听会话分组变更通知
您可以调用 `SetConvEventCallback` ([点击查看详情](https://comm.qq.com/im/doc/unity/zh/api/SDKRegisteringCallback/SetConvEventCallback.html)) 接口监听会话分组变更通知。

示例代码如下：

```c#
    //设置会话监听器
    TencentIMSDK.SetConvEventCallback((TIMConvEvent conv_event, List<ConvInfo> conv_list, string user_data)=>{
      // 处理回调逻辑
    });
```
