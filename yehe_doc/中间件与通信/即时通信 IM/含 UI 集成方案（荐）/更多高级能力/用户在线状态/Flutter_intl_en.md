- ## Description

  Showing the online status of the other users, on both conversation list and contacts list, are supported since the version of 0.1.3 of Flutter TUIKit.

  > ! This module works with [Premium Edition](https://www.tencentcloud.com/document/product/1047/34349) only.

  ## Demonstrations

  ### Conversation list

  | Turn on "Online Status"                                      | Turn off "Online Status"                                     |
  | ------------------------------------------------------------ | ------------------------------------------------------------ |
  | <img style="width:250px" src="https://qcloudimg.tencent-cloud.cn/raw/6d12b2a180272dc9852e81065436702d.jpg"  /> | <img style="width:250px" src="https://qcloudimg.tencent-cloud.cn/raw/065fef5624ab9ec622a7bc110c6a084c.jpg" /> |

  ### Contacts list

  | Turn on "Online Status"                                      | Turn off "Online Status"                                     |
  | ------------------------------------------------------------ | ------------------------------------------------------------ |
  | <img style="width:250px" src="https://qcloudimg.tencent-cloud.cn/raw/1359d29d2a7b550e9b300ca4096935f1.jpg"  /> | <img style="width:250px" src="https://qcloudimg.tencent-cloud.cn/raw/48552d7fad6bf2d69b2e4c6e884788d0.jpg" /> |

  ## Using this module

  Config the online status configuration field `isShowOnlineStatus` in TUIKit global `TIMUIKitConfig` when initializing TUIKit to control whether this function is enabled or disabled.

  ```dart
  final CoreServicesImpl _coreInstance = TIMUIKitCore.getInstance();
  
  _coreInstance.init(
    config: const TIMUIKitConfig(
      isShowOnlineStatus: true or false,  // Add this line
      // ... Other configurations
    ),
    // ... Other configurations
  );
  ```

  This field is the main switch of the following fields, while all the online status will be turned off if this field is `false` and the following field can be specified separately if this field is `true`.

  ### Conversation list

  TIMUIKitConversation is the widget of conversation list.

  A field of the "user online status" function switch **isShowOnlineStatus** been provided at `TIMUIKitConversation`, its type is boolean, and the default is `true`.


  ```dart
  TIMUIKitConversation(
    isShowOnlineStatus: true or false,
    // ... Other configurations
  )
  ```


  ### Contacts list

  TIMUIKitContact is the widget of contacts list.

  A field of the "user online status" function switch **isShowOnlineStatus** been provided at `TIMUIKitContact`, its type is boolean, and the default is `true`.
  ```dart
  TIMUIKitContact(
    isShowOnlineStatus: true or false,
    // ... Other configurations
  ）
  ```

  ## Contact us[](id:contact)

  If there's anything unclear or you have more ideas, feel free to contact us!

  - [Telegram Group](https://t.me/+1doS9AUBmndhNGNl)
  - [WhatsApp Group](https://chat.whatsapp.com/Gfbxk7rQBqc8Rz4pzzP27A)
