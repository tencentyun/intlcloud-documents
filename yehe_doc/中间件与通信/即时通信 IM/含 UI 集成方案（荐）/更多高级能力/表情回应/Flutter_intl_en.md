- ## Description

  **Message Reactions** Emoji have been added since the version of 0.1.3 of Flutter TUIKit.

  This module is developed with message modification.

  ## Demonstrations

  ### Send Emoji reactions

  Press and hold the message you want to reply to, and the Message Action Menu will appear.

  After enabling this module, on this menu, near the direction of the message itself, there will be an additional emoticon selection area. This area supports clicking the "+" to expand and display more stickers.


  | Message Action Menu                                          | More Emoji                                                   |
  | ------------------------------------------------------------ | ------------------------------------------------------------ |
  | <img style="width:250px" src="https://qcloudimg.tencent-cloud.cn/raw/b33931c12c614b68ef719f3d47e570e3.jpg"  /> | <img style="width:250px" src="https://qcloudimg.tencent-cloud.cn/raw/65d2c3e75d13ca7157cd9222f322d4aa.jpg" /> |

  ### View Emoji reactions

  All message reactions are displayed below the message and all users in the chat can see them.

  Below the message, the sender names are displayed after the emoji. Click on the name to trigger the `onTapAvatar` callback, to view the sender's profile.

  Click on each reaction being sent, can easily quickly send the same Emoji or remove this reaction. After removal, the reaction disappears with no trace and no one will be notified.

  Click on "...total xx" to view the complete list of senders.

  | Message Reactions                                            | Complete list of senders                                     |
  | ------------------------------------------------------------ | ------------------------------------------------------------ |
  | <img style="width:250px" src="https://qcloudimg.tencent-cloud.cn/raw/0601fcf0383b35a94600bda9ad1495fc.jpg"  /> | <img style="width:250px" src="https://qcloudimg.tencent-cloud.cn/raw/2ed71f237a64a8f47cf565f75902d370.jpg" /> |


  ## Using this module

  A field of the "Message Reaction" function switch **isUseMessageReaction** been provided at `config` of `TIMUIKitChat`, its type is boolean, and the default is `true`.

  ```dart
  TIMUIKitChat(
    config: TIMUIKitChatConfig(
      isUseMessageReaction: true  false, // Add this line
      // ... Other configurations
    ),
    // ... Other configurations
  )
  ```

  ## Contact us[](id:contact)

  If there's anything unclear or you have more ideas, feel free to contact us!

  - [Telegram Group](https://t.me/+1doS9AUBmndhNGNl)
  - [WhatsApp Group](https://chat.whatsapp.com/Gfbxk7rQBqc8Rz4pzzP27A)
