- ## 功能描述
  TUIKit 从 v0.1.3 版本开始，支持单聊会话“对方正在输入”功能。

  本功能使用更多腾讯云IM SDK在线消息能力实现，在线消息相关内容详见：[在线消息](https://cloud.tencent.com/document/product/269/75341)。

  | 开启“对方正在输入”                                           | 关闭“对方正在输入”                                           |
  | ------------------------------------------------------------ | ------------------------------------------------------------ |
  | <img style="width:250px" src="https://qcloudimg.tencent-cloud.cn/raw/0280b25ab42e0fff206ecdc19edca344.jpg"  /> | <img style="width:250px" src="https://qcloudimg.tencent-cloud.cn/raw/d51e2f6820c0146e1685ddd4173aefec.jpg" /> |

  ## 控制对方正在输入能力状态

  在 TIMUIKitChat 的配置参数 `config` 中，提供了“对方正在输入”功能开关 **showC2cMessageEditStatus** , 其类型为 boolean，默认为 `true` 。

  ```dart
  TIMUIKitChat(
    config: TIMUIKitChatConfig(
      showC2cMessageEditStatus: true 或 false,
      // ... 其他 config 配置
    ),
    // ... 其他 TIMUIKitChat 参数
  )
  ```


  ## 联系我们[](id:contact)

  如果您在接入使用过程中有任何疑问，请通过如下方式联系我们。

  - [Telegram Group](https://t.me/+1doS9AUBmndhNGNl)
  - [WhatsApp Group](https://chat.whatsapp.com/Gfbxk7rQBqc8Rz4pzzP27A)
