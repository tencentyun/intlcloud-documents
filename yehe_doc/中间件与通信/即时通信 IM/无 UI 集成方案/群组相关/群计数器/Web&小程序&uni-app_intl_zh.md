
## 功能描述

从 v2.26.0 起，Web IMSDK 提供了群计数器的功能，每个群都可以设置一定数量的计数器。

与 [群自定义属性](https://intl.cloud.tencent.com/document/product/1047/48174) 不同，群计数器主要用来存储整数类型的数据，您可以使用群计数器来存储一些群相关的附加信息，例如直播群的累计观看人数、观看人次、主播被点赞的次数、观众累计送给主播的礼物数等。

> ? 
>
> - 除了话题外，群计数器支持所有的群类型。
> - 群计数器功能仅旗舰版本支持。

关于群计数器，需要注意的是：

1. 单个群内最大支持 20 组群计数器，也即单个群内 key 的个数不超过 20 个。
2. 单个群计数器的 key 不超过 128 个字符，value 必须为整数类型（最大支持 64  位有符号整型）。
3. `setGroupCounters`、`increaseGroupCounter`、`decreaseGroupCounter` 接口合并计算，SDK 限制为单个登录用户最多 5 秒调用 20 次，超过限制后接口返回 2996 错误码。
4. `getGroupCounters` 接口单独计算，SDK 限制为单个登录用户最多 5 秒 20 次调用，超过限制后接口返回 2996 错误码。

[](id:set)

### 设置群计数器

您可以调用接口 [setGroupCounters](https://web.sdk.qcloud.com/im/doc/en/SDK.html#setGroupCounters) 设置多组群计数器。计数器设置成功后会触发 [TIM.EVENT.GROUP_COUNTER_UPDATED](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.GROUP_COUNTER_UPDATED) 事件，`TIM.EVENT.GROUP_COUNTER_UPDATED` 的使用参见下文的 [群计数器变更通知](#notify)。

> ? 
>
> - 如果您即将设置的计数器的 key 存在，则直接更新计数器的 value 值；如果不存在，则直接添加 key-value。
> - 如果多个用户同时设置同一个计数器时，计数器最终的值会相互覆盖，推荐由群主发起设置操作。

**接口**

<dx-codeblock>
:::  js

tim.setGroupCounters(options);

:::
</dx-codeblock>

**参数**

参数 options 为 Object 类型，包含的属性值如下：

| Name               | Type     | Description                                                  |
| ------------------ | -------- | ------------------------------------------------------------ |
| groupID            | String   | 群组ID |
| counters           | Object   | 群计数器 key-value |


**返回值**

`Promise` 对象。

**示例** 

<dx-codeblock>
:::  js
// 设置计数器 key1 和 key2 的值为 0
let promise = tim.setGroupCounters({
  groupID: 'group1',
  counters: { key1: 0, key2: 0 }
});
promise.then(function(imResponse) { // 设置成功
  console.log(imResponse.data.counters); // 设置成功的群计数器
}).catch(function(imError) { // 设置失败
  console.warn('setGroupCounters error:', imError); // 设置群计数器失败的相关信息
});

:::
</dx-codeblock>

[](id:increase)

### 递增群计数器

您可以调用递增接口 [increaseGroupCounter](https://web.sdk.qcloud.com/im/doc/en/SDK.html#increaseGroupCounter) 对群计数器作累加操作，操作成功后会触发 [TIM.EVENT.GROUP_COUNTER_UPDATED](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.GROUP_COUNTER_UPDATED) 事件，`TIM.EVENT.GROUP_COUNTER_UPDATED` 的使用参见下文的 [群计数器变更通知](#notify)。

> ? 
>
> - 接口参数中的 value 为变化量，调用接口后会在当前值的基础上累加传入的变化量；
> - 如果您即将设置的计数器的 key 存在，则直接在当前值的基础上根据传入的 value 作递增操作；反之，添加 key，并在默认值为 0 的基础上根据传入的 value 作递增操作。

**接口**

<dx-codeblock>
:::  js

tim.increaseGroupCounter(options);

:::
</dx-codeblock>

**参数**

参数 options 为 Object 类型，包含的属性值如下：

| Name               | Type     | Description                                                  |
| ------------------ | -------- | ------------------------------------------------------------ |
| groupID            | String   | 群组ID |
| key                | String   | 群计数器 key |
| value              | Number   | 群计数器 key 的变化量 |


**返回值**

`Promise` 对象。

**示例**

<dx-codeblock>
:::  js
// 假设当前的计数器 key1 的值是 8，调用 increaseGroupCounter 接口传入的递增变化量 value 为 2 后，最终 key1 的值变为 10。
let promise = tim.increaseGroupCounter({
  groupID: 'group1',
  key: 'key1',
  value: 2,
});
promise.then(function(imResponse) { // 递增成功
  console.log(imResponse.data);
  const { groupID, key, value } = imResponse.data;
}).catch(function(imError) { // 递增失败
  console.warn('increaseGroupCounter error:', imError);
});

:::
</dx-codeblock>


[](id:decrease)

### 递减群计数器

您可以调用递减接口 [decreaseGroupCounter](https://web.sdk.qcloud.com/im/doc/en/SDK.html#decreaseGroupCounter) 对群计数器作累减操作，操作成功后会触发 [TIM.EVENT.GROUP_COUNTER_UPDATED](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.GROUP_COUNTER_UPDATED) 事件，`TIM.EVENT.GROUP_COUNTER_UPDATED` 的使用参见下文的 [群计数器变更通知](#notify)。

> ?
>
> - 接口参数中的  value 为递减的变化量，调用接口后会在当前值的基础上减去传入的变化量；
> - 如果您即将设置的计数器的 key 存在，则直接在当前值的基础上根据传入的 value 作递减操作；反之，添加 key，并在默认值为 0 的基础上根据传入的 value 作递减操作。

**接口**

<dx-codeblock>
:::  js

tim.decreaseGroupCounter(options);

:::
</dx-codeblock>

**参数**

参数 options 为 Object 类型，包含的属性值如下：

| Name               | Type     | Description                                                  |
| ------------------ | -------- | ------------------------------------------------------------ |
| groupID            | String   | 群组ID |
| key                | String   | 群计数器 key |
| value              | Number   | 群计数器 key 的变化量 |

**返回值**

`Promise` 对象。

**示例**

<dx-codeblock>
:::  js
// 假设当前的计数器 key1 的值是 8，调用 decreaseGroupCounter 接口传入的递减变化量 value 为 2 后，最终 key1 的值变为 6。
let promise = tim.decreaseGroupCounter({
  groupID: 'group1',
  key: 'key1',
  value: 2
});
promise.then(function(imResponse) { // 递减成功
  console.log(imResponse.data);
  const { groupID, key, value } = imResponse.data;
}).catch(function(imError) { // 设置失败
  console.warn('decreaseGroupCounter error:', imError);
});

:::
</dx-codeblock>


[](id:get)

### 获取群计数器
您可以调用接口 [getGroupCounters](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getGroupCounters) ，并通过传入一组指定的 key 来获取对应的群计数器信息。接口会返回所有的与 key 相匹配的 key-value 键值对。

> ? 如果不传 keyList，则返回所有的群计数器。

**接口**

<dx-codeblock>
:::  js

tim.getGroupCounter(options);

:::
</dx-codeblock>

**参数**

参数 options 为 Object 类型，包含的属性值如下：

| Name               | Type     | Description                                                  |
| ------------------ | -------- | ------------------------------------------------------------ |
| groupID            | String   | 群组ID |
| keyList            | Array\|undefined | 群计数器 key 列表 |

**返回值**

`Promise` 对象。

**示例**

<dx-codeblock>
:::  js
// 获取群计数器 key1 和 key2 的值
let promise = tim.getGroupCounters({
  groupID: 'group1',
  keyList: ['key1', 'key2']
});
promise.then(function(imResponse) { // 获取成功
  console.log(imResponse.data.counters);
}).catch(function(imError) {
  console.warn('getGroupCounters error:', imError); // 获取群计数器失败的相关信息
});

:::
</dx-codeblock>

<dx-codeblock>
:::  js
// 获取某一个群组全部的计数器
let promise = tim.getGroupCounters({
  groupID: 'group1'
});
promise.then(function(imResponse) { // 获取成功
  console.log(imResponse.data.counters);
}).catch(function(imError) {
  console.warn('getGroupCounters error:', imError); // 获取群计数器失败的相关信息
});

:::
</dx-codeblock>

[](id:notify)

### 群计数器变更通知

当您调用 `setGroupCounters`、`increaseGroupCounter`、`decreaseGroupCounter` 接口修改群计数器时，会触发 `TIM.EVENT.GROUP_COUNTER_UPDATED` 事件，并返回变化后的 value 值。

> ? 在使用上述事件之前，您需要调用接口 [on](https://web.sdk.qcloud.com/im/doc/en/SDK.html#on) 注册群计时器变更事件。

**示例**

<dx-codeblock>
:::  js

let onGroupCounterUpdated = function(event) {
  const { groupID, key, value } = event.data;
  // groupID - 群组 ID
  // key - 群计数器 key
  // value - 群计数器 key 对应的 value
};
tim.on(TIM.EVENT.GROUP_COUNTER_UPDATED, onGroupCounterUpdated);

:::
</dx-codeblock>

