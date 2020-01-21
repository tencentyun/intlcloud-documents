## TIM

TIM 是 IM Web SDK 的命名空间，提供了创建 SDK 实例的静态方法**create()**，以及事件常量**EVENT**，类型常量**TYPES**。

**初始化**

| API | 描述 |
| --- | --- |
| **create** | 创建 SDK 实例。 |

## SDK 实例

| 基本概念 | 说明 |
| :--- | :---- |
| Message（消息） | IM SDK 中**Message** 表示要发送给对方的内容，消息包括若干属性，例如自己是否为发送者，发送人帐号以及消息产生时间等。 |
| Conversation（会话） | IM SDK 中 **Conversation**分为两种：<li> C2C（Client to Client）会话，表示单聊情况，自己与对方建立的对话。</li><li> GROUP（群）会话，表示群聊情况下群内成员组成的会话。 |
| Profile（资料） | IM SDK 中 **Profile**描述个人的常用基本信息，例如昵称、性别、个性签名以及头像地址等。 |
| Group（群组） | IM SDK 中 **Group**表示一个支持多人聊天的通信系统，支持私有群、公开群、聊天室以及音视频聊天室。 |
| GroupMember（群成员） | IM SDK 中**GroupMember**描述群内成员的常用基本信息，例如 ID、昵称、群内身份以及入群时间等。 |
| 群提示消息 | 当有用户被邀请加入群组或被移出群组等事件发生时，群内会产生提示消息，接入侧可以根据实际需求展示给群组用户或忽略。|
| 群系统通知消息 | 当有用户申请加群等事件发生时，管理员会收到申请加群等系统消息。管理员同意或拒绝加群申请，IM SDK 会通过群系统通知消息将申请加群等相应消息发送给接入侧，由接入侧展示给用户。  |
| 消息上屏 | 用户单击发送后，事先输入的文字或选择的图片等信息显示在用户电脑屏幕或手机屏幕上的过程。 |

### 登录相关
| API | 描述 |
| --- | --- |
| **login** | 登录。 |
| **logout** | 登出。 |


### 消息
| API | 描述 |
| --- | --- |
| **createTextMessage** | 创建文本消息。 |
| **createImageMessage** | 创建图片消息。 |
| **createAudioMessage** | 创建音频消息。 |
| **createVideoMessage** | 创建视频消息。 |
| **createCustomMessage** | 创建自定义消息。 |
| **createFaceMessage** | 创建表情消息。 |
| **createFileMessage** | 创建文件消息。 |
| **sendMessage** | 发送消息。 |
| **resendMessage** | 重发消息。 |
| **getMessageList** | 获取消息列表。  |
| **setMessageRead** | 设置消息已读。  |

### 会话
| API | 描述 |
| --- | --- |
| **getConversationList** | 获取会话列表。 |
| **getConversationProfile** | 获取会话资料。 |
| **deleteConversation** | 删除会话。 |

### 资料
| API | 描述 |
| --- | --- |
| **getMyProfile** | 获取个人资料。 |
| **getUserProfile**| 获取其他用户资料。 |
| **updateMyProfile** | 更新个人资料。 |
| **getBlacklist** | 获取我的黑名单列表。 |
| **addToBlacklist** | 添加用户到黑名单列表。 |
| **removeFromBlacklist** | 将用户从黑名单中移除。 |

### 群组
| API | 描述 |
| --- | --- |
| **getGroupList** | 获取群组列表。 |
| **getGroupProfile** | 获取群详细资料。 |
| **createGroup** | 创建群组。 |
| **dismissGroup** | 解散群组。 |
| **updateGroupProfile** | 修改群组资料。 |
| **joinGroup** | 申请加群。 |
| **quitGroup** | 退出群组。 |
| **searchGroupByID** | 搜索群组。 |
| **changeGroupOwner** | 转让群组。 |
| **handleGroupApplication** | 处理申请加群。 |
| **setMessageRemindType** | 设置群消息提示类型。 |

### 群成员
| API | 描述 |
| --- | --- |
| **getGroupMemberList** | 获取群成员列表。 |
| **getGroupMemberProfile** | 获取群成员资料。 |
| **addGroupMember** | 添加群成员。 |
| **deleteGroupMember** | 删除群成员。 |
| **setGroupMemberMuteTime** |设置群成员的禁言时间。|
| **setGroupMemberRole** | 修改群成员角色。 |
| **setGroupMemberNameCard** | 设置群成员名片。 |
| **setGroupMemberCustomField** | 设置群成员自定义字段。 |

### 其他
| API | 描述 |
| --- | --- |
| **on** | 监听事件。 |
| **off** | 取消监听事件。 |
| **registerPlugin** | 注册插件。 |
| **setLogLevel** | 设置日志级别。 |

