- ## Description

  Showing the message typing status, used to indicate the other user is typing a new message on a one-to-one chat, are supported since the version of 0.1.3 of Flutter TUIKit.

  This module is developed with online message capability.

  | Turn on "Typing Status"                                      | Turn off "Typing Status"                                     |
  | ------------------------------------------------------------ | ------------------------------------------------------------ |
  | <img style="width:250px" src="https://qcloudimg.tencent-cloud.cn/raw/0280b25ab42e0fff206ecdc19edca344.jpg"  /> | <img style="width:250px" src="https://qcloudimg.tencent-cloud.cn/raw/d51e2f6820c0146e1685ddd4173aefec.jpg" /> |

  ## Using this module

  A field of the "typing status" function switch **showC2cMessageEditStatus** been provided at `config` of `TIMUIKitChat`, its type is boolean, and the default is `true`.

  ```dart
  TIMUIKitChat(
    config: TIMUIKitChatConfig(
      showC2cMessageEditStatus: true or false, // Add this line
      // ... Other configurations
    ),
    // ... Other configurations
  )
  ```

  ## Contact us[](id:contact)

  If there's anything unclear or you have more ideas, feel free to contact us!

  - [Telegram Group](https://t.me/+1doS9AUBmndhNGNl)
  - [WhatsApp Group](https://chat.whatsapp.com/Gfbxk7rQBqc8Rz4pzzP27A)
