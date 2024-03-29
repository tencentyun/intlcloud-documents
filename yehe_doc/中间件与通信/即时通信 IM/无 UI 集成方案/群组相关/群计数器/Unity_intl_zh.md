## 功能描述

从 Native SDK 7.0 版本开始，IMSDK 提供了群计数器的功能，每个群都可以设置一定数量的计数器。

与 [群自定义属性不同](https://intl.cloud.tencent.com/document/product/1047/48175) ，群计数器主要用来存储整数类型的数据，您可以使用群计数器来存储一些群相关的附加信息，例如直播群的累计观看人数、观看人次、主播被点赞的次数、观众累计送给主播的礼物数等。

> ?
>
> - 除了话题外，群计数器支持所有的群类型。
> - 群计数器功能仅旗舰版本支持。

关于群计数器，需要注意的是：

1. 单个群内最大支持 20 组群计数器，也即单个群内 key 的个数不超过 20 个；
2. 单个群计数器的 key 不超过 128 个字符，value 必须为整数类型（最大支持 64  位有符号整型）；
3. `GroupSetGroupCounters`、`GroupIncreaseGroupCounter`、`GroupDecreaseGroupCounter` 接口合并计算，SDK 限制为单个登录用户最多 5 秒调用 20 次，超过限制后接口回调 8516 错误码；
4. `GroupGetGroupCounters` 接口单独计算，SDK 限制为单个登录用户最多 5 秒 20 次调用，超过限制后接口回调 8516 错误码。



[](id:set)

## 设置群计数器

您可以调用接口 `GroupSetGroupCounters`（[点击查看详情](https://comm.qq.com/im/doc/unity/zh/api/GroupApi/GroupSetGroupCounters.html)）设置多组群计数器。计数器设置成功后会触发 `GroupCounterChangedCallback` （[点击查看详情](https://comm.qq.com/im/doc/unity/zh/callback/GroupCounterChangedCallback.html)）回调， GroupCounterChangedCallback 的使用参见下文的 [群计数器变更通知](#notify)。

> ?
>
> - 如果您即将设置的计数器的 key 存在，则直接更新计数器的 value 值；如果不存在，则直接添加 key-value。
> - 如果多个用户同时设置同一个计数器时，计数器最终的值会相互覆盖，推荐由群主发起设置操作。



示例：调用 `GroupSetGroupCounters` 接口分别设置计数器 key1 和 key2 的值为 0。

```c#
    //设置群计数器
    List<GroupCounter> list = new List<GroupCounter>
    {
      new GroupCounter
      {
        group_counter_key = "key",
        group_counter_value = 1
      }
    };
    TIMResult res = TencentIMSDK.GroupSetGroupCounters("groupID", list, (int code, string desc, List<GroupCounter> results, string user_data)=>{
      // 设置群计数器异步结果
    });
```

[](id:increase)

## 递增群计数器

您可以调用递增接口 `GroupIncreaseGroupCounter` ([点击查看详情](https://comm.qq.com/im/doc/unity/zh/api/GroupApi/GroupIncreaseGroupCounter.html)) 对群计数器作累加操作，操作成功后会触发 `GroupCounterChangedCallback` （[点击查看详情](https://comm.qq.com/im/doc/unity/zh/callback/GroupCounterChangedCallback.html)）回调。 GroupCounterChangedCallback 的使用参见下文的 [群计数器变更通知](#notify)。

> ?
>
> - 接口参数中的 value 为变化量，调用接口后会在当前值的基础上累加传入的变化量；
> - 如果您即将设置的计数器的 key 存在，则直接在当前值的基础上根据传入的 value 作递增操作；反之，添加 key，并在默认值为 0 的基础上根据传入的 value 作递增操作。



示例：假设当前的计数器 key1 的值是 8，调用 `GroupIncreaseGroupCounter` 接口传入的递增变化量 value 为 2 后，最终 key1 的值变为 10。

```c#
    //递增群计数器
    TIMResult res = TencentIMSDK.GroupIncreaseGroupCounter("groupID", "key1", 2, (int code, string desc, List<GroupCounter> results, string user_data)=>{
      // 递增群计数器异步结果
    });
```

[](id:decrease)

## 递减群计数器

您可以调用递减接口 `GroupDecreaseGroupCounter` ([点击查看详情](https://comm.qq.com/im/doc/unity/zh/api/GroupApi/GroupDecreaseGroupCounter.html)) 对群计数器作累减操作，操作成功后会触发 `GroupCounterChangedCallback` （[点击查看详情](https://comm.qq.com/im/doc/unity/zh/callback/GroupCounterChangedCallback.html)）回调， GroupCounterChangedCallback 的使用参见下文的 [群计数器变更通知](#notify)。

> ?
>
> - 接口参数中的  value 为递减的变化量，调用接口后会在当前值的基础上减去传入的变化量；
> - 如果您即将设置的计数器的 key 存在，则直接在当前值的基础上根据传入的 value 作递减操作；反之，添加 key，并在默认值为 0 的基础上根据传入的 value 作递减操作。



示例：假设当前的计数器 key1 的值是 8，调用 `GroupDecreaseGroupCounter` 接口传入的递减变化量 value 为 2 后，最终 key1 的值变为 6。

```c#
    //递减群计数器
    TIMResult res = TencentIMSDK.GroupDecreaseGroupCounter("groupID", "key1", 2, (int code, string desc, List<GroupCounter> results, string user_data)=>{
      // 递减群计数器异步结果
    });
```

[](id:get)

## 获取群计数器

您可以调用接口 `GroupGetGroupCounters` ([点击查看详情](https://comm.qq.com/im/doc/unity/zh/api/GroupApi/GroupGetGroupCounters.html)) ，并通过传入一组指定的 key 来获取对应的群计数器信息。接口会返回所有的与 key 相匹配的 key-value 键值对。

> ? 如果传入的 key 列表为空，则返回所有的群计数器。

示例：调用接口 `GroupGetGroupCounters` 分别获取计数器 key1 和 key2 的值。

```c#
    //获取群计数器
    TIMResult res = TencentIMSDK.GroupGetGroupCounters("groupID", new List<string> {"key1", "key2"}, (int code, string desc, List<GroupCounter> results, string user_data)=>{
      // 获取群计数器异步结果
    });
```

[](id:notify)

## 群计数器变更通知

当您调用 `GroupSetGroupCounters`、`GroupIncreaseGroupCounter`、`GroupDecreaseGroupCounter` 接口修改群计数器时，会触发 `GroupCounterChangedCallback` 回调，并返回变化后的 value 值。

> ? 在使用上述回调之前，您需要调用接口 `SetGroupCounterChangedCallback` （[点击查看详情](https://comm.qq.com/im/doc/unity/zh/api/SDKRegisteringCallback/SetGroupCounterChangedCallback.html)）添加群监听器。

示例代码如下：

```c#
    // 设置群计数器变更回调
    TencentIMSDK.SetGroupCounterChangedCallback((string group_id, string group_counter_key, ulong group_counter_new_value, string user_data) => {
    });
```

[](id:feedback)
