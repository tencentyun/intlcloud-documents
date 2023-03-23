
## Overview

The Web SDK starts to provide the group counter feature since v2.26.0. You can configure a specific number of counters for each group.

Unlike [custom group attributes](https://intl.cloud.tencent.com/document/product/1047/48174), group counters are used to store data of the integer type. You can use group counters to store additional information related to a group, such as the cumulative number of viewers, the number of views, the number of times the host has been liked, and the number of gifts the audience has given to the host of an audio-video group.

> ? 
>
> - Group counters support all types of groups, excluding topic-enabled community groups.
> - The group counter feature is supported only by the Ultimate edition.

Keep the following in mind for group counters:

1. A single group supports up to 20 group counters, that is, up to 20 keys per group.
2. For a single group counter, the key can contain up to 128 characters, and the value must be of the integer type (signed integer of up to 64 bits).
3. The `setGroupCounters`, `increaseGroupCounter`, and `decreaseGroupCounter` APIs together can be called by a logged-in user up to 20 times every five seconds in the SDK, and the 2996 error code will be returned if the limit is exceeded.
4. The `getGroupCounters` API can be called by a logged-in user up to 20 times every five seconds in the SDK, and the 2996 error code will be returned if the limit is exceeded.

[](id:set)

### Setting Group Counters

You can call the [setGroupCounters](https://web.sdk.qcloud.com/im/doc/en/SDK.html#setGroupCounters) API to set multiple group counters. After group counters are set, the [TIM.EVENT.GROUP_COUNTER_UPDATED](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.GROUP_COUNTER_UPDATED) event will be triggered. For the use directions of `TIM.EVENT.GROUP_COUNTER_UPDATED`, see [Group Counter Change Notifications](#notify).

> ? 
>
> - If `key` of the group counter to be set already exists, the value of `key` is updated directly. Otherwise, a key-value pair will be added.
> - If multiple users set the same counter at the same time, the final value of the counter will be used. It's recommended that the group owner performs counter setting operations.

**API**

<dx-codeblock>
:::  js

tim.setGroupCounters(options);

:::
</dx-codeblock>

**Parameters**

The `options` parameter is of the `Object` type. It contains the following attribute values:

| Name               | Type     | Description                                                  |
| ------------------ | -------- | ------------------------------------------------------------ |
| groupID            | String   | Group ID. |
| counters           | Object   | Group counter key-value pair. |


**Return values**

`Promise` object.

**Sample** 

<dx-codeblock>
:::  js
// Set the values of counters `key1` and `key2` to 0.
let promise = tim.setGroupCounters({
  groupID: 'group1',
  counters: { key1: 0, key2: 0 }
});
promise.then(function(imResponse) { // Set successfully.
  console.log(imResponse.data.counters); // Group attributes set successfully.
}).catch(function(imError) { // Setting failed.
  console.warn('setGroupCounters error:', imError); // Error information.
});

:::
</dx-codeblock>

[](id:increase)

### Increasing the Value of a Group Counter

You can call the [increaseGroupCounter](https://web.sdk.qcloud.com/im/doc/en/SDK.html#increaseGroupCounter) API to increase the value of a group counter. After the value of the group counter is increased, the [TIM.EVENT.GROUP_COUNTER_UPDATED](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.GROUP_COUNTER_UPDATED) event will be triggered. For the use directions of `TIM.EVENT.GROUP_COUNTER_UPDATED`, see [Group Counter Change Notifications](#notify).

> ? 
>
> - The API parameter `value` is the change value. Each time when the API is called, the current value of `value` is increased by the value passed in.
> - If the `key` of the group counter to be set already exists, the current value of `value` is directly increased by the value passed in. Otherwise, a `key` will be added, and the default value (0) of `value` is increased by the value passed in.

**API**

<dx-codeblock>
:::  js

tim.increaseGroupCounter(options);

:::
</dx-codeblock>

**Parameters**

The `options` parameter is of the `Object` type. It contains the following attribute values:

| Name | Type | Description |
| ------------------ | -------- | ------------------------------------------------------------ |
| groupID            | String   | Group ID. |
| key                | String   | Group counter key. |
| value              | Number   | Increment value of the group counter key. |


**Return values**

`Promise` object.

**Sample**

<dx-codeblock>
:::  js
// Assume that the value of counter `key1` is 8. After you call the `increaseGroupCounter` API to pass in an increment value of 2, the value of `key1` becomes 10.
let promise = tim.increaseGroupCounter({
  groupID: 'group1',
  key: 'key1',
  value: 2,
});
promise.then(function(imResponse) { // Group counter increased successfully.
  console.log(imResponse.data);
  const { groupID, key, value } = imResponse.data;
}).catch(function(imError) { // Failed to increase the group counter.
  console.warn('increaseGroupCounter error:', imError);
});

:::
</dx-codeblock>


[](id:decrease)

### Decreasing the Value of a Group Counter

You can call the [decreaseGroupCounter](https://web.sdk.qcloud.com/im/doc/en/SDK.html#decreaseGroupCounter) API to decrease the value of a group counter. After the value of the group counter is decreased, the [TIM.EVENT.GROUP_COUNTER_UPDATED](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.GROUP_COUNTER_UPDATED) event will be triggered. For the use directions of `TIM.EVENT.GROUP_COUNTER_UPDATED`, see [Group Counter Change Notifications](#notify).

> ?
>
> - The API parameter `value` is the change value. Each time when the API is called, the current value of `value` is decreased by the value passed in.
> - If the `key` of the group counter to be set already exists, the current value of `value` is directly decreased by the value passed in. Otherwise, a `key` will be added, and the default value (0) of `value` is decreased by the value passed in.

**API**

<dx-codeblock>
:::  js

tim.decreaseGroupCounter(options);

:::
</dx-codeblock>

**Parameters**

The `options` parameter is of the `Object` type. It contains the following attribute values:

| Name | Type | Description |
| ------------------ | -------- | ------------------------------------------------------------ |
| groupID            | String   | Group ID. |
| key                | String   | Group counter key. |
| value              | Number   | Decrement value of the group counter key. |

**Return values**

`Promise` object.

**Sample**

<dx-codeblock>
:::  js
// Assume that the value of counter `key1` is 8. After you call the `decreaseGroupCounter` API to pass in a decrement value of 2, the value of `key1` becomes 6.
let promise = tim.decreaseGroupCounter({
  groupID: 'group1',
  key: 'key1',
  value: 2
});
promise.then(function(imResponse) { // Group counter decreased successfully.
  console.log(imResponse.data);
  const { groupID, key, value } = imResponse.data;
}).catch(function(imError) { // Setting failed.
  console.warn('decreaseGroupCounter error:', imError);
});

:::
</dx-codeblock>


[](id:get)

### Getting Group Counters
You can call the [getGroupCounters](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getGroupCounters) API to pass in a set of keys to get the information of the corresponding group counters. The API will return all key-value pairs matching the keys that are passed in.

> ? If you do not pass in the key list, all group counters are returned.

**API**

<dx-codeblock>
:::  js

tim.getGroupCounter(options);

:::
</dx-codeblock>

**Parameters**

The `options` parameter is of the `Object` type. It contains the following attribute values:

| Name | Type | Description |
| ------------------ | -------- | ------------------------------------------------------------ |
| groupID            | String   | Group ID. |
| keyList            | Array\|undefined | List of group counter keys. |

**Return values**

`Promise` object.

**Sample**

<dx-codeblock>
:::  js
// Get the values of counters `key1` and `key2`.
let promise = tim.getGroupCounters({
  groupID: 'group1',
  keyList: ['key1', 'key2']
});
promise.then(function(imResponse) { // Got successfully.
  console.log(imResponse.data.counters);
}).catch(function(imError){
  console.warn('getGroupCounters error:', imError); // Error information.
});

:::
</dx-codeblock>

<dx-codeblock>
:::  js
// Get the values of all counters in a group.
let promise = tim.getGroupCounters({
  groupID: 'group1'
});
promise.then(function(imResponse) { // Got successfully.
  console.log(imResponse.data.counters);
}).catch(function(imError){
  console.warn('getGroupCounters error:', imError); // Error information.
});

:::
</dx-codeblock>

[](id:notify)

### Group Counter Change Notifications

When you call the `setGroupCounters`, `increaseGroupCounter`, or `decreaseGroupCounter` API to modify group counters, the `TIM.EVENT.GROUP_COUNTER_UPDATED` event will be triggered and the updated values will be returned.

> ? Before you can use the foregoing event, you need to call the [on](https://web.sdk.qcloud.com/im/doc/en/SDK.html#on) API to register for group counter change events.

**Sample**

<dx-codeblock>
:::  js

let onGroupCounterUpdated = function(event) {
  const { groupID, key, value } = event.data;
  // groupID - Group ID.
  // key - Group counter key.
  // value - Value of the group counter key.
};
tim.on(TIM.EVENT.GROUP_COUNTER_UPDATED, onGroupCounterUpdated);

:::
</dx-codeblock>

