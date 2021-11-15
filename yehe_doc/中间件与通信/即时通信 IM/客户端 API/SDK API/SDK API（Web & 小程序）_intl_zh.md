
## TIM

TIM 是 IM Web SDK 的命名空间，提供了创建 SDK 实例的静态方法 [create()](https://web.sdk.qcloud.com/im/doc/en/TIM.html#.create) ，以及事件常量 [EVENT](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html)，类型常量 [TYPES](https://web.sdk.qcloud.com/im/doc/en/module-TYPES.html)。

**初始化**

| API | 描述 |
| --- | --- |
| [create](https://web.sdk.qcloud.com/im/doc/en/TIM.html#.create) | 创建 SDK 实例。 |

## SDK 实例

| 基本概念 | 说明 |
| :--- | :---- |
| Message（消息） | IM SDK 中 [Message](https://web.sdk.qcloud.com/im/doc/en/Message.html) 表示要发送给对方的内容，消息包括若干属性，例如自己是否为发送者，发送人帐号以及消息产生时间等。 |
| Conversation（会话） | IM SDK 中 [Conversation](https://web.sdk.qcloud.com/im/doc/en/Conversation.html) 分为两种：<li> C2C（Client to Client）会话，表示单聊情况，自己与对方建立的对话。</li><li> GROUP（群）会话，表示群聊情况下群内成员组成的会话。 |
| Profile（资料） | IM SDK 中 [Profile](https://web.sdk.qcloud.com/im/doc/en/Profile.html) 描述个人的常用基本信息，例如昵称、性别、个性签名以及头像地址等。 |
| Friend（好友） | IM SDK 中 [Friend](https://web.sdk.qcloud.com/im/doc/en/Friend.html) 描述好友的常用基本信息，例如备注、分组等。 |
| FriendApplication（好友申请）	| IM SDK 中 [FriendApplication](https://web.sdk.qcloud.com/im/doc/en/FriendApplication.html) 描述好友申请的常用基本信息，例如加好友来源、备注等。 |
| FriendGroup（好友分组）| IM SDK 中 [FriendGroup](https://web.sdk.qcloud.com/im/doc/en/FriendGroup.html) 描述好友分组的常用基本信息，例如分组名、分组成员等。
| Group（群组） | IM SDK 中 [Group](https://web.sdk.qcloud.com/im/doc/en/Group.html) 表示一个支持多人聊天的通信系统，支持好友工作群、陌生人社交群、临时会议群以及直播群。 |
| GroupMember（群成员） | IM SDK 中 [GroupMember](https://web.sdk.qcloud.com/im/doc/en/GroupMember.html) 描述群内成员的常用基本信息，例如 ID、昵称、群内身份以及入群时间等。 |
| 群提示消息 | 当有用户被邀请加入群组或被移出群组等事件发生时，群内会产生提示消息，接入侧可以根据实际需求展示给群组用户或忽略。<br/>群提示消息有多种类型，详细描述请参见  [Message.GroupTipPayload](https://web.sdk.qcloud.com/im/doc/en/Message.html#.GroupTipPayload)。|
| 群系统通知消息 | 当有用户申请加群等事件发生时，管理员会收到申请加群等系统消息。管理员同意或拒绝加群申请，IM SDK 会通过群系统通知消息将申请加群等相应消息发送给接入侧，由接入侧展示给用户。<br/>群系统通知消息有多种类型，详细描述请参见 [Message.GroupSystemNoticePayload](https://web.sdk.qcloud.com/im/doc/en/Message.html#.GroupSystemNoticePayload)。  |
| 消息上屏 | 用户单击发送后，事先输入的文字或选择的图片等信息显示在用户电脑屏幕或手机屏幕上的过程。 |

### 登录相关
| API | 描述 |
| --- | --- |
| [login](https://web.sdk.qcloud.com/im/doc/en/SDK.html#login) | 登录。 |
| [logout](https://web.sdk.qcloud.com/im/doc/en/SDK.html#logout) | 登出。 |


### 消息
| API | 描述 |
| --- | --- |
| [createTextMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createTextMessage) | 创建文本消息。 |
| [createTextAtMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createTextAtMessage) |创建可以附带 @ 提醒功能的文本消息。 |
| [createImageMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createImageMessage) | 创建图片消息。 |
| [createAudioMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createAudioMessage) | 创建音频消息。 |
| [createVideoMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createVideoMessage) | 创建视频消息。 |
| [createCustomMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createCustomMessage) | 创建自定义消息。 |
| [createFaceMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createFaceMessage) | 创建表情消息。 |
| [createFileMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createFileMessage) | 创建文件消息。 |
| [createMergerMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createMergerMessage) | 创建合并消息。 |
| [downloadMergerMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#downloadMergerMessage) | 下载合并消息。 |
| [createForwardMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createForwardMessage) | 创建转发消息。 |
| [sendMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#sendMessage) | 发送消息。 |
| [revokeMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#revokeMessage) | 撤回消息。 |
| [resendMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#resendMessage) | 重发消息。 |
| [deleteMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#deleteMessage) | 删除消息。 |

### 会话
| API | 描述 |
| --- | --- |
| [getMessageList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getMessageList) | 获取消息列表。  |
| [setMessageRead](https://web.sdk.qcloud.com/im/doc/en/SDK.html#setMessageRead) | 设置消息已读。  |
| [getConversationList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getConversationList) | 获取会话列表。 |
| [getConversationProfile](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getConversationProfile) | 获取会话资料。 |
| [deleteConversation](https://web.sdk.qcloud.com/im/doc/en/SDK.html#deleteConversation) | 删除会话。 |
| [pinConversation](https://web.sdk.qcloud.com/im/doc/en/SDK.html#pinConversation) | 置顶或取消置顶会话。 |

### 资料
| API | 描述 |
| --- | --- |
| [getMyProfile](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getMyProfile) | 获取个人资料。 |
| [getUserProfile](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getUserProfile) | 获取其他用户资料。 |
| [updateMyProfile](https://web.sdk.qcloud.com/im/doc/en/SDK.html#updateMyProfile) | 更新个人资料。 |
| [getBlacklist](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getBlacklist) | 获取我的黑名单列表。 |
| [addToBlacklist](https://web.sdk.qcloud.com/im/doc/en/SDK.html#addToBlacklist) | 添加用户到黑名单列表。 |
| [removeFromBlacklist](https://web.sdk.qcloud.com/im/doc/en/SDK.html#removeFromBlacklist) | 将用户从黑名单中移除。 |

### 关系链
| API | 描述 |
| --- | --- |
| [getFriendList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getFriendList) | 获取 SDK 缓存的好友列表。 |
| [addFriend](https://web.sdk.qcloud.com/im/doc/en/SDK.html#addFriend) | 添加好友。 |
| [deleteFriend](https://web.sdk.qcloud.com/im/doc/en/SDK.html#deleteFriend) | 删除好友。 |
| [checkFriend](https://web.sdk.qcloud.com/im/doc/en/SDK.html#checkFriend) | 校验好友关系。 |
| [getFriendProfile](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getFriendProfile) | 获取指定好友的好友数据和资料数据。 |
| [updateFriend](https://web.sdk.qcloud.com/im/doc/en/SDK.html#updateFriend) | 更新好友的关系链数据。 |
| [getFriendApplicationList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getFriendApplicationList) | 获取 SDK 缓存的好友申请列表。 |
| [acceptFriendApplication](https://web.sdk.qcloud.com/im/doc/en/SDK.html#acceptFriendApplication) | 同意好友申请。 |
| [refuseFriendApplication](https://web.sdk.qcloud.com/im/doc/en/SDK.html#refuseFriendApplication) | 拒绝好友申请。 |
| [deleteFriendApplication](https://web.sdk.qcloud.com/im/doc/en/SDK.html#deleteFriendApplication) | 删除好友申请。 |
| [setFriendApplicationRead](https://web.sdk.qcloud.com/im/doc/en/SDK.html#setFriendApplicationRead) | 上报好友申请已读。 |
| [getFriendGroupList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getFriendGroupList) | 获取 SDK 缓存的好友分组列表。 |
| [createFriendGroup](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createFriendGroup) | 创建好友分组。 |
| [deleteFriendGroup](https://web.sdk.qcloud.com/im/doc/en/SDK.html#deleteFriendGroup) | 删除好友分组。 |
| [addToFriendGroup](https://web.sdk.qcloud.com/im/doc/en/SDK.html#addToFriendGroup) | 添加好友到分组列表。 |
| [removeFromFriendGroup](https://web.sdk.qcloud.com/im/doc/en/SDK.html#removeFromFriendGroup) | 从好友分组移除好友。 |
| [renameFriendGroup](https://web.sdk.qcloud.com/im/doc/en/SDK.html#renameFriendGroup) | 修改好友分组的名称。 |

### 群组
| API | 描述 |
| --- | --- |
| [getGroupList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getGroupList) | 获取群组列表。 |
| [getGroupProfile](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getGroupProfile) | 获取群详细资料。 |
| [createGroup](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createGroup) | 创建群组。 |
| [dismissGroup](https://web.sdk.qcloud.com/im/doc/en/SDK.html#dismissGroup) | 解散群组。 |
| [updateGroupProfile](https://web.sdk.qcloud.com/im/doc/en/SDK.html#updateGroupProfile) | 修改群组资料。 |
| [joinGroup](https://web.sdk.qcloud.com/im/doc/en/SDK.html#joinGroup) | 申请加群。 |
| [quitGroup](https://web.sdk.qcloud.com/im/doc/en/SDK.html#quitGroup) | 退出群组。 |
| [searchGroupByID](https://web.sdk.qcloud.com/im/doc/en/SDK.html#searchGroupByID) | 搜索群组。 |
| [getGroupOnlineMemberCount](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getGroupOnlineMemberCount) | 获取直播群在线人数。 |
| [changeGroupOwner](https://web.sdk.qcloud.com/im/doc/en/SDK.html#changeGroupOwner) | 转让群组。 |
| [handleGroupApplication](https://web.sdk.qcloud.com/im/doc/en/SDK.html#handleGroupApplication) | 处理申请加群。 |
| [initGroupAttributes](https://web.sdk.qcloud.com/im/doc/en/SDK.html#initGroupAttributes) | 初始化群属性。 |
| [setGroupAttributes](https://web.sdk.qcloud.com/im/doc/en/SDK.html#setGroupAttributes) | 设置群属性。 |
| [deleteGroupAttributes](https://web.sdk.qcloud.com/im/doc/en/SDK.html#deleteGroupAttributes) | 删除群属性。 |
| [getGroupAttributes](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getGroupAttributes) | 获取群属性。 |

### 群成员
| API | 描述 |
| --- | --- |
| [getGroupMemberList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getGroupMemberList) | 获取群成员列表。 |
| [getGroupMemberProfile](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getGroupMemberProfile) | 获取群成员资料。 |
| [addGroupMember](https://web.sdk.qcloud.com/im/doc/en/SDK.html#addGroupMember) | 添加群成员。 |
| [deleteGroupMember](https://web.sdk.qcloud.com/im/doc/en/SDK.html#deleteGroupMember) | 删除群成员。 |
| [setGroupMemberMuteTime](https://web.sdk.qcloud.com/im/doc/en/SDK.html#setGroupMemberMuteTime) |设置群成员的禁言时间。|
| [setGroupMemberRole](https://web.sdk.qcloud.com/im/doc/en/SDK.html#setGroupMemberRole) | 修改群成员角色。 |
| [setGroupMemberNameCard](https://web.sdk.qcloud.com/im/doc/en/SDK.html#setGroupMemberNameCard) | 设置群成员名片。 |
| [setGroupMemberCustomField](https://web.sdk.qcloud.com/im/doc/en/SDK.html#setGroupMemberCustomField) | 设置群成员自定义字段。 |
| [setMessageRemindType](https://web.sdk.qcloud.com/im/doc/en/SDK.html#setMessageRemindType) | 设置群消息提示类型。 |

### 其他
| API | 描述 |
| --- | --- |
| [on](https://web.sdk.qcloud.com/im/doc/en/SDK.html#on) | 监听事件。 |
| [off](https://web.sdk.qcloud.com/im/doc/en/SDK.html#off) | 取消监听事件。 |
| [registerPlugin](https://web.sdk.qcloud.com/im/doc/en/SDK.html#registerPlugin) | 注册插件。 |
| [setLogLevel](https://web.sdk.qcloud.com/im/doc/en/SDK.html#setLogLevel) | 设置日志级别。 |
| [destroy](https://web.sdk.qcloud.com/im/doc/en/SDK.html#destroy)  | 销毁 SDK 实例。 |


