- ## 功能描述

  TUIKit 从 v0.1.3 版本开始，支持在会话列表及联系人列表，展示用户在线状态。

  > ! “用户在线状态”功能仅旗舰版套餐支持，使用前请确认。

  ## 效果展示

  ### 会话列表

  | 开启“显示用户在线状态”                                       | 关闭“显示用户在线状态”                                       |
  | ------------------------------------------------------------ | ------------------------------------------------------------ |
  | <img style="width:250px" src="https://qcloudimg.tencent-cloud.cn/raw/6d12b2a180272dc9852e81065436702d.jpg"  /> | <img style="width:250px" src="https://qcloudimg.tencent-cloud.cn/raw/065fef5624ab9ec622a7bc110c6a084c.jpg" /> |

  ### 联系人列表


  | 开启“显示用户在线状态”                                       | 关闭“显示用户在线状态”                                       |
  | ------------------------------------------------------------ | ------------------------------------------------------------ |
  | <img style="width:250px" src="https://qcloudimg.tencent-cloud.cn/raw/1359d29d2a7b550e9b300ca4096935f1.jpg"  /> | <img style="width:250px" src="https://qcloudimg.tencent-cloud.cn/raw/48552d7fad6bf2d69b2e4c6e884788d0.jpg" /> |

  ## 使用此功能

  请在初始化TUIKit时，通过配置TUIKit全局 `TIMUIKitConfig` 中在线状态功能字段 `isShowOnlineStatus`，来控制此功能开启或关闭。

  ```dart
  final CoreServicesImpl _coreInstance = TIMUIKitCore.getInstance();
  
  _coreInstance.init(
    config: const TIMUIKitConfig(
      isShowOnlineStatus: true 或 false,  // 添加此行
      // ... 其他TUIKit全局配置
    ),
    // ... 其他启动配置
  );
  ```

  此配置是后续配置的总开关，请在此状态打开后，再继续开启后续页面在线状态。

  ### 会话列表用户在线状态

  TIMUIKitConversation 提供会话列表功能。

  在 TIMUIKitConversation 顶层提供了“用户在线状态”功能开关 **isShowOnlineStatus**， 其类型为 boolean，默认为 `true` 。


  ```dart
  TIMUIKitConversation(
    isShowOnlineStatus: true 或 false,
    // ... 其他 TIMUIKitConversation 配置
  )
  ```


  ### 联系人列表用户在线状态

  TIMUIKitContact 提供联系人列表功能。
  在 TIMUIKitContact 顶层提供了“用户在线状态”功能开关 **isShowOnlineStatus**， 其类型为 boolean，默认为 `true` 。

  ```dart
  TIMUIKitContact(
    isShowOnlineStatus: true 或 false,
    // ... 其他 TIMUIKitContact 配置
  ）
  ```

  ## 联系我们[](id:contact)

  如果您在接入使用过程中有任何疑问，请通过如下方式联系我们。

  - [Telegram Group](https://t.me/+1doS9AUBmndhNGNl)
  - [WhatsApp Group](https://chat.whatsapp.com/Gfbxk7rQBqc8Rz4pzzP27A)
