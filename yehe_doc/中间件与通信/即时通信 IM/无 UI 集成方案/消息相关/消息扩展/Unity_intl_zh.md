## 功能描述
消息扩展可以为消息增加 key/value 状态标识。基于消息扩展，我们可以实现投票、接龙、问卷调查等功能。
- 在投票场景，我们可以先创建一条用于投票的自定义消息，其中 `custom_elem_data` 存储投票的标题和选项，然后用消息扩展 key 存储投票用户 ID，用消息扩展 value 存储投票用户选项，有了每个用户的投票选项，我们就可以动态计算出投票选项的用户占比。
- 在接龙场景，我们可以先创建一条用于接龙的自定义消息，其中 `custom_elem_data` 存储接龙的标题，然后用消息扩展 key 存储接龙用户 ID，用消息扩展 value 存储接龙信息。
- 在问卷调查场景，我们可以先创建一条用于问卷调查的自定义消息，其中 `custom_elem_data` 存储问卷调查的标题和选项，然后用消息扩展 key 存储问卷调查的用户 ID，用消息扩展 value 存储问卷调查信息。

> ?
- 该功能仅对旗舰版客户开放，购买 [旗舰版](https://www.tencentcloud.com/document/product/1047/34577) 后可使用。
- 该功能仅Native SDK 6.7 及以上版本支持。
- 该功能需要先在 [即时通信 IM 控制台](https://console.cloud.tencent.com/im) > 功能配置 > 登录与消息 > 消息扩展设置中开启。
- 社群（Community）和直播群（AVChatRoom）消息不支持该功能。

### 设置消息扩展
调用 `MsgSetMessageExtensions` ([点击查看详情](https://comm.qq.com/im/doc/unity/zh/api/MessageApi/MsgSetMessageExtensions.html)) 接口可以设置消息扩展，如果扩展 key 已经存在，则修改扩展的 value 信息，如果扩展 key 不存在，则新增扩展。

设置消息扩展接口入参详解如下：
<table>
<thead>
<tr>
<th>属性</th>
<th>含义</th>
<th>说明</th>
</tr>
</thead>
<tbody><tr>
<td>message</td>
<td>消息对象</td>
<td>消息需满足三个条件：<ul style="margin-bottom: 0px;"><li>消息发送前需设置 <code>message_support_message_extension</code> (<a href="https://comm.qq.com/im/doc/unity/zh/types/MessageAttributes/Message.html">点击查看详情</a>) 为 true。</li><li>消息必须是发送成功的状态。</li><li>消息不能是社群（Community）和直播群（AVChatRoom）消息。 </li></ul></td>
</tr>
<tr>
<td>extensions</td>
<td>扩展列表</td>
<td>如果扩展 key 已经存在，则修改扩展的 value 信息，如果扩展 key 不存在，则新增扩展。</td>
</tr>
</tbody></table>

> ?
> 1. 扩展 key 最大支持 100 字节，扩展 value 最大支持 1KB，单次最多支持设置 20 个扩展，单条消息最多可设置 300 个扩展。
1. 当多个用户同时设置或删除同一个扩展 key 时，只有第一个用户可以执行成功，其它用户会在设置回包收到 23001 错误码和最新的扩展信息，在收到错误码和扩展信息后，请按需重新发起设置操作。
2. 我们强烈建议不同的用户设置不同的扩展 key，这样大部分场景都不会冲突，例如投票、接龙、问卷调查，都可以把自己的 userID 作为扩展 key。

示例代码如下：

```c#
    // 设置消息扩展
    var list = new List<MessageExtension>
    {
      new MessageExtension
      {
        message_extension_key = "key",
        message_extension_value = "value"
      }
    };
    TIMResult res = TencentIMSDK.MsgSetMessageExtensions(message, list, (int code, string desc, List<MessageExtensionResult> results, string user_data)=>{
      // 设置消息扩展异步结果
    });
```

### 获取消息扩展

调用 `MsgGetMessageExtensions` ([点击查看详情](https://comm.qq.com/im/doc/unity/zh/api/MessageApi/MsgGetMessageExtensions.html)) 接口获取消息扩展列表。

> ? 如果没有网络，SDK 会直接返回本地缓存的消息扩展列表。

示例代码如下：

```c#
    // 获取消息扩展
    TIMResult res = TencentIMSDK.MsgGetMessageExtensions(message, (int code, string desc, List<MessageExtension> list, string user_data)=>{
      // 获取消息扩展异步结果
    });
```

### 删除消息扩展

调用 `MsgDeleteMessageExtensions` ([点击查看详情](https://comm.qq.com/im/doc/unity/zh/api/MessageApi/MsgDeleteMessageExtensions.html)) 接口删除指定消息扩展，如果 `keys` 字段填 `null` ，则会清空所有消息扩展。

示例代码如下：

```c#
    // 删除消息扩展
    var list = new List<MessageExtension>
    {
      new MessageExtension
      {
        message_extension_key = "key",
        message_extension_value = "value"
      }
    };
    TIMResult res = TencentIMSDK.MsgDeleteMessageExtensions(message, list, (int code, string desc, List<MessageExtensionResult> results, string user_data)=>{
      // 删除消息扩展异步结果
    });
```

### 消息扩展更新

如果您事先调用 `SetMsgExtensionsChangedCallback` 添加了高级消息事件监听器，当消息扩展发生了新增或者更新，您会收到 `MsgExtensionsChangedCallback` ([点击查看详情](https://comm.qq.com/im/doc/unity/zh/callback/MsgExtensionsChangedCallback.html)) 回调。
如果您事先调用 `SetMsgExtensionsDeletedCallback` 添加了高级消息事件监听器，当消息扩展发生了删除，您会收到 `MsgExtensionsDeletedCallback` ([点击查看详情](https://comm.qq.com/im/doc/unity/zh/callback/MsgExtensionsDeletedCallback.html)) 回调。

示例代码如下：

```c#
    // 添加高级消息的事件监听器
    TencentIMSDK.SetMsgExtensionsChangedCallback((string message_id, List<MessageExtension> message_extension_array, string user_data) => {
      // message_extension_array 为被修改之后的消息扩展对象列表
    });
    TencentIMSDK.SetMsgExtensionsDeletedCallback((string message_id, List<MessageExtension> message_extension_array, string user_data) => {
      // message_extension_array 为被删除之后的消息扩展对象列表
    });
```
