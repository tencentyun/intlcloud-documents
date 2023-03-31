- ## 功能描述

  TUIKit 从 v0.1.3 版本开始 ，支持表情回应功能。

  “表情回应”功能采用消息编辑能力实现。

  ## 效果展示

  ### 发送表情回应

  开启表情回应能力后，长按消息菜单中，靠近消息本身的方向，会多一条表情选择区。该区域支持点击“加号”扩大，展示更多表情。

  | 长按消息菜单                                                 | 更多表情                                                     |
  | ------------------------------------------------------------ | ------------------------------------------------------------ |
  | <img style="width:250px" src="https://qcloudimg.tencent-cloud.cn/raw/b33931c12c614b68ef719f3d47e570e3.jpg"  /> | <img style="width:250px" src="https://qcloudimg.tencent-cloud.cn/raw/65d2c3e75d13ca7157cd9222f322d4aa.jpg" /> |

  ### 展示表情回应

  一条消息收到的所有回应表情，都会展示在这条消息的下方，会话中所有成员均可看到。

  在消息下方，回应表情后面会显示该表情的发送人姓名，点击姓名可以触发 `onTapAvatar` 回调，以查看其Profile。

  点击展示中表情，可以方便快捷回应同样的表情，或取消该表情。

  当发送同一个回应表情人数过多被省略时，点击最后的“...共xx人”，可查看完整的回应成员名单。

  | 表情回应消息展示                                             | 完整回应成员名单                                             |
  | ------------------------------------------------------------ | ------------------------------------------------------------ |
  | <img style="width:250px" src="https://qcloudimg.tencent-cloud.cn/raw/0601fcf0383b35a94600bda9ad1495fc.jpg"  /> | <img style="width:250px" src="https://qcloudimg.tencent-cloud.cn/raw/2ed71f237a64a8f47cf565f75902d370.jpg" /> |


  ## 控制表情回应

  在 TIMUIKitChat 的配置参数 `config` 中，提供了“表情回应”功能开关 **isUseMessageReaction** , 其类型为 boolean，默认为 `true` 。

  ```dart
  TIMUIKitChat(
    config: TIMUIKitChatConfig(
      isUseMessageReaction: true 或 false,
      // ... 其他 config 配置
    ),
    // ... 其他 TIMUIKitChat 参数
  )
  ```

  ## 联系我们[](id:contact)

  如果您在接入使用过程中有任何疑问，请通过如下方式联系我们。

  - [Telegram Group](https://t.me/+1doS9AUBmndhNGNl)
  - [WhatsApp Group](https://chat.whatsapp.com/Gfbxk7rQBqc8Rz4pzzP27A)
