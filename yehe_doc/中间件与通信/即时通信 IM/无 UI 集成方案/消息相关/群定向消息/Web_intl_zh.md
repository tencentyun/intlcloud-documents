## 功能描述
群定向消息是指向群内部分成员发送消息，其他群成员无法收到该消息。

> ?
> 1. 该功能 v2.23.1 及以上版本支持。
> 2. 该功能仅对旗舰版客户开放，详情请参见 [基础服务详情](https://intl.cloud.tencent.com/document/product/1047/34350)。
> 3. 创建群 @ 消息不支持指定消息接收成员列表 `receiverList`。
> 4. 社群（Community）和直播群（AVChatRoom）不支持发送群定向消息。
> 5. 群定向消息默认不计入群会话的未读计数。

## 发送群定向消息
定向消息是指，向群内部分指定的成员发送消息，而未被指定的群成员不会通过 [TIM.EVENT.MESSAGE_RECEIVED](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.MESSAGE_RECEIVED) 事件收到该消息。


如果您希望向群组内特定的群成员发消息，可以按照下面的方式实现：
- 调用 `createXxxMessage` (其中 Xxx 表示具体的消息类型) 接口指定消息接收成员列表 `receiverList` 创建一条消息。
- 调用 `sendMessage` 接口发送消息。

## 示例
<dx-codeblock>
:::  js

// 创建群定向消息
let message = tim.createTextMessage({
  to: 'test',
  conversationType: TIM.TYPES.CONV_GROUP,
  payload: {
    text: 'Hello world!'
  },
  // v2.23.1起支持群定向消息功能，如果您需要发群定向消息，需购买旗舰版套餐，并且创建消息时通过 receiverList 指定消息接收者。
  // 注意：群定向消息不计入会话未读，receiverList 最大支持50个接收者。
  receiverList: ['user0', 'user1']
});

// 发送消息
let promise = tim.sendMessage(message);
promise.then(function(imResponse) {
  // 发送成功
  console.log(imResponse);
}).catch(function(imError) {
  // 发送失败
  console.warn('sendMessage error:', imError);
});

:::
</dx-codeblock>

## 接收群定向消息
群定向消息默认不计入群会话的未读计数。
接收群定向消息跟接收普通消息是一样的操作步骤，参见 [接收消息](https://intl.cloud.tencent.com/document/product/1047/47996)。
