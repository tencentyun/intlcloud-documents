## Overview

Starting from native SDK v7.0, Tencent Cloud Chat SDK provides the group counter feature. You can configure a certain number of counters for each group.

Unlike [custom group attributes](https://intl.cloud.tencent.com/document/product/1047/48175), group counters are used to store data of integer type. Group counters can be used to store additional information related to a group, such as the cumulative number of viewers, the number of views, the number of likes, and the number of gifts the audience has given to the host of an audio-video group.

> ?
>
> - Group counters support all types of groups, excluding topic-enabled community groups.
> - The group counter feature is supported only by the Ultimate edition.

Keep the following in mind for group counters:

1. A single group supports up to 20 group counters, that is, up to 20 keys per group.
2. For a single group counter, the key can contain up to 128 bytes, and the value must be of integer type (signed integer of up to 64 bits).
3. The `GroupSetGroupCounters`, `GroupIncreaseGroupCounter`, and `GroupDecreaseGroupCounter` APIs together can be called by a logged-in user up to 20 times every five seconds in the SDK, and the 8516 error code will be called back if the limit is exceeded.
4. The `GroupGetGroupCounters` API can be called by a logged-in user up to 20 times every five seconds in the SDK, and the 8516 error code will be called back if the limit is exceeded.



[](id:set)

## Setting Group Counters

Call the `GroupSetGroupCounters` ([details](https://comm.qq.com/im/doc/unity/zh/api/GroupApi/GroupSetGroupCounters.html)) API to set group counters. After group counters are set, the `GroupCounterChangedCallback` ([details](https://comm.qq.com/im/doc/unity/zh/callback/GroupCounterChangedCallback.html)) callback will be triggered. For the usage of the `GroupCounterChangedCallback` callback, see [Group Counter Change Notification](#notify).

> ?
>
> - If the `key` of the group counter to be set already exists, the value of `key` is updated directly. Otherwise, a key-value pair will be added.
> - If multiple users set the same counter at the same time, the final value of the counter will be used. It's recommended that the group owner performs counter setting operations.



Sample: Call the `GroupSetGroupCounters` API to set the values of counters `key1` and `key2` to 0

```c#
    // Set a group counter
    List<GroupCounter> list = new List<GroupCounter>
    {
      new GroupCounter
      {
        group_counter_key = "key",
        group_counter_value = 1
      }
    };
    TIMResult res = TencentIMSDK.GroupSetGroupCounters("groupID", list, (int code, string desc, List<GroupCounter> results, string user_data)=>{
      // Async result of the group counter setting
    });
```

[](id:increase)

## Incrementing the Value of a Group Counter

Call the `GroupIncreaseGroupCounter` ([details](https://comm.qq.com/im/doc/unity/zh/api/GroupApi/GroupIncreaseGroupCounter.html)) API to increment the value of a group counter. After the value of the group counter is incremented, the `GroupCounterChangedCallback` ([details](https://comm.qq.com/im/doc/unity/zh/callback/GroupCounterChangedCallback.html)) callback will be triggered. For the usage of the `GroupCounterChangedCallback` callback, see [Group Counter Change Notification](#notify).

> ?
>
> - The API parameter `value` is the change value. Each time when the API is called, the current value is incremented by the value passed in.
> - If the `key` of the group counter to be set already exists, the current value is directly incremented by the value passed in. Otherwise, a `key` will be added, and the default value (0) is incremented by the value passed in.



Sample: Assume that the current value of counter `key1` is 8. After you call the `GroupIncreaseGroupCounter` API to pass in an increment value 2, the final value of `key1` becomes 10.

```c#
    // Increment the value of a group counter
    TIMResult res = TencentIMSDK.GroupIncreaseGroupCounter("groupID", "key1", 2, (int code, string desc, List<GroupCounter> results, string user_data)=>{
      // Async result of the group counter increment
    });
```

[](id:decrease)

## Decrementing the Value of a Group Counter

Call the `GroupDecreaseGroupCounter` ([details](https://comm.qq.com/im/doc/unity/zh/api/GroupApi/GroupDecreaseGroupCounter.html)) API to decrement the value of a group counter. After the value of the group counter is decremented, the `GroupCounterChangedCallback` ([details](https://comm.qq.com/im/doc/unity/zh/callback/GroupCounterChangedCallback.html)) callback will be triggered. For the usage of the `GroupCounterChangedCallback` callback, see [Group Counter Change Notification](#notify).

> ?
>
> - The API parameter `value` is the change value. Each time when the API is called, the current value is decreased by the value passed in.
> - If the `key` of the group counter to be set already exists, the current value is directly decremented by the value passed in. Otherwise, a `key` will be added, and the default value (0) is decreased by the value passed in.



Sample: Assume that the current value of counter `key1` is 8. After you call the `GroupDecreaseGroupCounter` API to pass in a decrement value 2, the final value of `key1` becomes 6.

```c#
    // Decrement the value of a group counter
    TIMResult res = TencentIMSDK.GroupDecreaseGroupCounter("groupID", "key1", 2, (int code, string desc, List<GroupCounter> results, string user_data)=>{
      // Async result of the group counter decrement
    });
```

[](id:get)

## Getting Group Counters

Call the `GroupGetGroupCounters` ([details](https://comm.qq.com/im/doc/unity/zh/api/GroupApi/GroupGetGroupCounters.html)) API to pass in a set of keys to get the information of the corresponding group counters. The API will return all key-value pairs matching the keys passed in.

> ? If the key list passed in is empty, all group counters are returned.

Sample: Call the `GroupGetGroupCounters`` API to get the values of counters `key1` and `key2`

```c#
    // Get group counters
    TIMResult res = TencentIMSDK.GroupGetGroupCounters("groupID", new List<string> {"key1", "key2"}, (int code, string desc, List<GroupCounter> results, string user_data)=>{
      // Async result of the group counter getting
    });
```

[](id:notify)

## Group Counter Change Notification

When you call the `GroupSetGroupCounters`, `GroupIncreaseGroupCounter`, or `GroupDecreaseGroupCounter` API to modify group counters, the SDK will trigger the `GroupCounterChangedCallback` callback and return the updated values of `value`.

> ? Before you can invoke the above-mentioned callback, you need to call the `SetGroupCounterChangedCallback` ([details](https://comm.qq.com/im/doc/unity/zh/api/SDKRegisteringCallback/SetGroupCounterChangedCallback.html)) API to add a group listener.

Sample code:

```c#
    // Set the group counter change callback
    TencentIMSDK.SetGroupCounterChangedCallback((string group_id, string group_counter_key, ulong group_counter_new_value, string user_data) => {
    });
```

[](id:feedback)
