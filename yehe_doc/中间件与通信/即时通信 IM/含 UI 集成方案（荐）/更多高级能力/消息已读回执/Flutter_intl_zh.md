- ## 功能描述
  TUIKit 从 v0.0.8 版本开始，支持“单聊消息已读回执”与“群消息已读回执”功能。

  > ! “群消息已读回执”功能仅旗舰版套餐支持，使用前请确认。


  ## 效果展示

  ### 单聊消息已读回执

  通过消息左侧 “已读” / “未读” 展示。

  <img style="width:250px" src="https://qcloudimg.tencent-cloud.cn/raw/29f0379b70276a5c907c7bd276a08c95.jpg"  />

  ### 群聊消息已读回执

  通过消息旁圆圈，体现群成员已读数量。点击后，进入展示详情。

  #### 消息列表

  <img style="width:250px" src="https://qcloudimg.tencent-cloud.cn/raw/3d0a47c4a67e74642f1dea9853dbf81f.jpg"  />


  #### 已读回执详情

  | 已读 群成员                                                  | 未读 群成员                                                  |
  | ------------------------------------------------------------ | ------------------------------------------------------------ |
  | <img style="width:200px" src="https://qcloudimg.tencent-cloud.cn/raw/49ad2e079f0a62bcb5c3628886910e49.jpg"  /> | <img style="width:200px" src="https://qcloudimg.tencent-cloud.cn/raw/170a8e7640a6e561c0af456c641790b0.jpg" /> |


  ## 控制消息已读回执

  在 TIMUIKitChat 的配置参数 `config` 中，提供了一系列“消息已读回执”功能开关，具体如下代码说明。对于 Boolean 类型的配置开关，默认值均为 `true`。

  ```dart
  TIMUIKitChat(
    config: TIMUIKitChatConfig(
      isShowReadingStatus: true 或 false, // 【单聊】是否展示单聊消息已读回执
      isShowGroupReadingStatus: true 或 false, // 【群聊】是否展示群聊消息已读回执
      isReportGroupReadingStatus: true 或 false, // 【群聊】是否上报群聊消息已读回执
      groupReadReceiptPermissionList: [
        GroupReceiptAllowType.work,
        GroupReceiptAllowType.meeting,
        GroupReceiptAllowType.public
      ], // 【群聊】哪些类型的群，需要展示群聊消息已读回执
      // ... 其他 config 配置
    ),
    // ... 其他 TIMUIKitChat 参数
  )
  ```

  ## 联系我们[](id:contact)

  如果您在接入使用过程中有任何疑问，请通过如下方式联系我们。

  - [Telegram Group](https://t.me/+1doS9AUBmndhNGNl)
  - [WhatsApp Group](https://chat.whatsapp.com/Gfbxk7rQBqc8Rz4pzzP27A)
