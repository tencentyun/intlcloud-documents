- ## Description

  Read receipt for both one-to-one and group chat are supported since the version of 0.0.8 of Flutter TUIKit.

  > ! Read receipt for  group chat works with [Premium Edition](https://www.tencentcloud.com/document/product/1047/34349) only.

  ## Demonstrations

  ### One-to-one Chat

  Shows with 'Read' / 'Unread' on the left side of the messages.

  <img style="width:250px" src="https://qcloudimg.tencent-cloud.cn/raw/29f0379b70276a5c907c7bd276a08c95.jpg"  />

  ### Group Chat

  The circle on the left side of the messages indicates the amount of members reading the messages. And the details can be shown after clicking it.

  #### Message list

  <img style="width:250px" src="https://qcloudimg.tencent-cloud.cn/raw/3d0a47c4a67e74642f1dea9853dbf81f.jpg"  />


  #### Read receipt details

  | Read Member                                                  | Unread Member                                                |
  | ------------------------------------------------------------ | ------------------------------------------------------------ |
  | <img style="width:200px" src="https://qcloudimg.tencent-cloud.cn/raw/49ad2e079f0a62bcb5c3628886910e49.jpg"  /> | <img style="width:200px" src="https://qcloudimg.tencent-cloud.cn/raw/170a8e7640a6e561c0af456c641790b0.jpg" /> |


  ## Using this module

  Several fields of the "Read Receipt" function switch have been provided at `config` of `TIMUIKitChat`. For those Boolean field, the default value are `true`.

  ```dart
  TIMUIKitChat(
    config: TIMUIKitChatConfig(
      isShowReadingStatus: true or false, // 【One-to-one Chat】Whether to display the read receipt of One-to-one Chat messages
      isShowGroupReadingStatus: true or false, // 【Group Chat】Whether to display the read receipt of Group Chat messages
      isReportGroupReadingStatus: true or false, // 【Group Chat】Whether to mark and report the messages from Group Chat as read
      groupReadReceiptPermissionList: [
        GroupReceiptAllowType.work,
        GroupReceiptAllowType.meeting,
        GroupReceiptAllowType.public
      ], // 【Group Chat】Control which types of groups can mark messages as read.
      // ... Other configurations
    ),
    // ... Other configurations
  )
  ```

  ## Contact us[](id:contact)

  If there's anything unclear or you have more ideas, feel free to contact us!

  - [Telegram Group](https://t.me/+1doS9AUBmndhNGNl)
  - [WhatsApp Group](https://chat.whatsapp.com/Gfbxk7rQBqc8Rz4pzzP27A)
