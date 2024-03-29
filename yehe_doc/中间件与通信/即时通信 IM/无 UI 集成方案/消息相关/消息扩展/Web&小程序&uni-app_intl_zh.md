## 功能描述
消息扩展可以为消息增加 key/value 状态标识。基于消息扩展，我们可以实现投票、接龙、问卷调查等功能。
- 在投票场景，我们可以先通过 [createCustomMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createCustomMessage) 接口创建一条用于投票的自定义消息，其中 `data` 存储投票的标题和选项，然后用消息扩展 key 存储投票用户 ID，用消息扩展 value 存储投票用户选项，有了每个用户的投票选项，我们就可以动态计算出投票选项的用户占比。
- 在接龙场景，我们可以先通过 [createCustomMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createCustomMessage) 接口创建一条用于接龙的自定义消息，其中 `data` 存储接龙的标题，然后用消息扩展 key 存储接龙用户 ID，用消息扩展 value 存储接龙信息。
- 在问卷调查场景，我们可以先通过 [createCustomMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createCustomMessage) 接口创建一条用于问卷调查的自定义消息，其中 `data` 存储问卷调查的标题和选项，然后用消息扩展 key 存储问卷调查的用户 ID，用消息扩展 value 存储问卷调查信息。

> ?
- 该功能仅对旗舰版客户开放，购买 [旗舰版](https://buy.cloud.tencent.com/avc?from=17220) 后可使用。
- 该功能 v2.25.0 及以上版本支持。
- 该功能需要先在 [即时通信 IM 控制台](https://console.cloud.tencent.com/im) > 功能配置 > 登录与消息 > 消息扩展设置中开启。
- 社群（Community）和直播群（AVChatRoom）消息不支持该功能。

### 设置消息扩展
调用 [setMessageExtensions](https://web.sdk.qcloud.com/im/doc/en/SDK.html#setMessageExtensions) 接口可以设置消息扩展，如果扩展 key 已经存在，则修改扩展的 value 信息，如果扩展 key 不存在，则新增扩展。设置成功后，自己和对端用户（C2C）或群组成员（Group）都会收到 [TIM.EVENT.MESSAGE_EXTENSIONS_UPDATED](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.MESSAGE_EXTENSIONS_UPDATED) 事件。

**接口**

<dx-codeblock>
:::  js

tim.setMessageExtensions(message, extensions);

:::
</dx-codeblock>

**参数**

| Name       | Type    | Description                                                  |
| ---------- | ------- | ------------------------------------------------------------ |
| message    | Message | 消息实例                                                     |
| extensions | Array   | 消息扩展 key-value 列表，如果扩展 key 已经存在，则修改扩展的 value 信息，如果扩展 key 不存在，则新增扩展。 |

> ? 
> 1. 消息需满足三个条件：
 - 消息的 isSupportExtension 属性必须为 true
 - 消息必须是发送成功的状态
 - 消息不能是社群（Community）和直播群（AVChatRoom）消息
2. 扩展 key 最大支持 100 字节，扩展 value 最大支持 1KB，单次最多支持设置 20 个扩展，单条消息最多可设置 300 个扩展。
3. 当多个用户同时设置或删除同一个扩展 key 时，只有第一个用户可以执行成功，其它用户会在设置回包收到 23001 错误码和最新的扩展信息，在收到错误码和扩展信息后，请按需重新发起设置操作。
4. 我们强烈建议不同的用户设置不同的扩展 key，这样大部分场景都不会冲突，例如投票、接龙、问卷调查，都可以把自己的 userID 作为扩展 key。

**返回值**

`Promise` 对象。

**示例** 

<dx-codeblock>
:::  js

let promise = tim.setMessageExtensions(message, [{ key: 'a', value: '1' }, { key: 'b', value: '2' }]);
promise.then(function(imResponse) {
  // 设置消息扩展成功
   const { extensions } = imResponse.data;
   extensions.forEach((item) => {
     const { code, key, value } = item;
     if (code === 23001) {
       // 设置 key 冲突，请根据返回的最新扩展信息，按需进行重试
     }
   });
}).catch(function(imError) {
  // 设置消息扩展失败
  console.warn('setMessageExtensions error:', imError);
});

:::
</dx-codeblock>


### 获取消息扩展

调用 [getMessageExtensions](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getMessageExtensions) 接口获取消息扩展列表。

**接口**

<dx-codeblock>
:::  js

tim.getMessageExtensions(message);

:::
</dx-codeblock>

**参数**

| Name    | Type    | Description |
| ------- | ------- | ----------- |
| message | Message | 消息实例    |

> ? 
> 消息需满足三个条件：
- 消息的 isSupportExtension 属性必须为 true
- 消息必须是发送成功的状态
- 消息不能是社群（Community）和直播群（AVChatRoom）消息

**返回值**

`Promise` 对象。

**示例**

<dx-codeblock>
:::  js

let promise = tim.getMessageExtensions(message);
promise.then(function(imResponse) {
  // 获取消息扩展成功
   const { extensions } = imResponse.data;
   extensions.forEach((item) => {
     const { key, value } = item;
     // key - 消息扩展 key
     // value - 消息扩展 key 对应的 value 值
   });
}).catch(function(imError) {
  // 获取消息扩展失败
  console.warn('getMessageExtensions error:', imError);
});

:::
</dx-codeblock>


### 删除消息扩展

调用 [deleteMessageExtensions](https://web.sdk.qcloud.com/im/doc/en/SDK.html#deleteMessageExtensions) 接口删除指定消息扩展，如果 `keyList` 字段不传，则会清空所有消息扩展。删除成功后，自己和对端用户（C2C）或群组成员（Group）都会收到 [TIM.EVENT.MESSAGE_EXTENSIONS_DELETED](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.MESSAGE_EXTENSIONS_DELETED) 事件。

**接口**

<dx-codeblock>
:::  js

tim.deleteMessageExtensions(message, keyList);

:::
</dx-codeblock>

**参数**

| Name    | Type             | Description         |
| ------- | ---------------- | ------------------- |
| message | Message          | 消息实例            |
| keyList | Array\|undefined | 消息扩展 key 列表。 |

> ? 
> 1. 消息需满足三个条件：
 - 消息的 isSupportExtension 属性必须为 true
 - 消息必须是发送成功的状态
 - 消息不能是社群（Community）和直播群（AVChatRoom）消息
2. 当多个用户同时设置或删除同一个扩展 key 时，只有第一个用户可以执行成功，其它用户会收到 23001 错误码和最新的扩展信息，在收到错误码和扩展信息后，请按需重新发起删除操作。

**返回值**

`Promise` 对象。

**示例**

<dx-codeblock>
:::  js

// 删除消息扩展 key
let promise = tim.deleteMessageExtensions(message, ['a', 'b']);
promise.then(function(imResponse) {
   // 删除消息扩展成功
   const { extensions } = imResponse.data;
   extensions.forEach((item) => {
     const { code, key, value } = item;
     if (code === 23001) {
       // 删除 key 冲突，请根据返回的最新扩展信息，按需进行重试
     }
   });
}).catch(function(imError) {
  // 删除消息扩展失败
  console.warn('deleteMessageExtensions error:', imError);
});

:::
</dx-codeblock>

<dx-codeblock>
:::  js

// 清空所有消息扩展 key
let promise = tim.deleteMessageExtensions(message);
promise.then(function(imResponse) {
   // 清空消息扩展成功
   console.log('deleteMessageExtensions ok:', imResponse)
}).catch(function(imError) {
  // 清空消息扩展失败
  console.warn('deleteMessageExtensions error:', imError);
});

:::
</dx-codeblock>


### 消息扩展更新

如果您提前注册了 [TIM.EVENT.MESSAGE_EXTENSIONS_UPDATED](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.MESSAGE_EXTENSIONS_UPDATED) 事件，当消息扩展发生了新增或者更新时，SDK 会派发 `TIM.EVENT.MESSAGE_EXTENSIONS_UPDATED` 事件，您可以在注册的回调中获取到更新的 key-value 信息。

**示例**

<dx-codeblock>
:::  js

let onMessageExtensionsUpdated = function(event) {
  const { messageID, extensions } = event.data;
  // messageID - 消息 ID
  // extensions - 消息扩展列表
  extensions.forEach((item) => {
   const { key, value } = item;
   // key - 消息扩展 key
   // value - 消息扩展 key 对应的 value 值
  });
};
tim.on(TIM.EVENT.MESSAGE_EXTENSIONS_UPDATED, onMessageExtensionsUpdated);

:::
</dx-codeblock>

### 消息扩展删除

如果您提前注册了 [TIM.EVENT.MESSAGE_EXTENSIONS_DELETED](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.MESSAGE_EXTENSIONS_DELETED) 事件，当消息被删除时，SDK 会派发 `TIM.EVENT.MESSAGE_EXTENSIONS_DELETED` 事件，您可以在注册的回调中获取到被删除的 key。
**示例**

<dx-codeblock>
:::  js

let onMessageExtensionsDeleted = function(event) {
  const { messageID, keyList } = event.data;
  // messageID - 消息 ID
  // keyList - 被删除的消息扩展 key 列表
  keyList.forEach((key) => {
   // console.log(key)
  });
};
tim.on(TIM.EVENT.MESSAGE_EXTENSIONS_DELETED, onMessageExtensionsDeleted);

:::
</dx-codeblock>
