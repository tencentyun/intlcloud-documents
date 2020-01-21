
## TIMManager

IM SDK 主核心模块，负责 IM SDK 的初始化、登录、创建会话以及管理推送等功能。
- 初始化：初始化是使用 IM SDK 的前提，调用 init 接口后，才能调用其它 API。
- 登录：需要设置 SDKAppID，UserID 和 UserSig 才能使用即时通信 IM 服务。
- 会话：一个会话对应一个聊天窗口，例如，与单个好友的 C2C 聊天或者一个聊天群都是一个会话。
- 推送：管理和设置离线推送的相关功能，包括 token 和开关等。

### 初始化相关接口
| API | 描述 |
| --- | --- |
| **sharedInstance** | 获取管理器实例 **TIMManager**。 |
| **initSdk** | 初始化 SDK，设置全局配置信息。 |
| **unInit** | 反初始化。 |
| **getGlobalConfig** | 获取全局配置信息。 |
| **setUserConfig** | 设置用户配置信息。 |
| **getUserConfig** | 获取用户配置信息。 |
| **addMessageListener** | 新增新消息接收监听。 |
| **removeMessageListener** | 移除消息监听。 |


### 登录相关接口
| API | 描述 |
| --- | --- |
| **login** | 登录。 |
| **autoLogin** | 自动登录。 |
| **logout** | 登出。 |
| **getLoginUser** | 获取当前登录的用户。 |
| **getLoginStatus** | 获取当前登录状态。 |


### 会话管理器
| API | 描述 |
| --- | --- |
| **getConversationList** | 获取会话列表。 |
| **getConversation** | 获取单个会话。 |
| **deleteConversation** | 删除单个会话。 |
| **deleteConversationAndMessages** | 删除单个会话和对应的会话消息。 |


### 设置 APNs 推送
| API | 描述 |
| --- | --- |
| **setToken** | 设置客户端 Token 和证书 busiId。 |
| **setAPNS** | 配置 APNS。 |
| **getAPNSConfig** | 获取 APNS 配置。 |
| **doBackground** | 上报 App 应用退至后台。 |
| **doForeground** | 上报 App 应用切换回前台。 |


### 未登录查看本地会话和消息
| API | 描述 |
| --- | --- |
| **initStorage** | 在未登录的情况下加载本地存储。 |


### 调试相关接口
| API | 描述 |
| --- | --- |
| **GetVersion** | 获取版本号。 |
| **log** | 打印日志。 |
| **getLogPath** | 获取日志文件路径。 |
| **getIsLogPrintEnabled** | 获取日志打印开启状态。 |
| **getLogLevel** | 获取日志级别。 |


## TIMConversation

一个会话对应一个聊天窗口，例如，与单个好友的 C2C 聊天或者一个聊天群都是一个会话。
TIMConversation 提供的接口函数都是围绕消息的相关操作，包括发送消息、获取历史消息、设置消息已读设置、撤回和删除等。

### 发消息相关接口
| API | 描述 |
| --- | --- |
| **sendMessage** | 发送消息。 |
| **sendOnlineMessage** | 发送在线消息（无痕消息）。 |


### 获取消息相关接口
| API | 描述 |
| --- | --- |
| **getMessage** | 从云端拉取历史消息。 |
| **getLocalMessage** | 从本地数据库中获取历史消息。 |
| **getLastMsg** | 获取当前会话的最后一条消息。 |


### 设置消息已读
| API | 描述 |
| --- | --- |
| **setReadMessage** | 标记消息为已读状态。 |
| **getUnReadMessageNum** | 获取会话的未读消息计数。 |


### 撤回/删除消息相关接口
| API | 描述 |
| --- | --- |
| **revokeMessage** | 撤回一条已发送的消息（消息发送成功后 ）。 |
| **deleteLocalMessage** | 删除当前会话的本地历史消息。 |


### 获取会话信息相关接口
| API | 描述 |
| --- | --- |
| **getType** | 获取会话类型。 |
| **getReceiver** | 获取会话 ID。 |
| **getGroupName** | 获取群名称。 |


### 草稿箱
| API | 描述 |
| --- | --- |
| **setDraft** | 添加未编辑完的草稿消息。 |
| **getDraft** | 获取未编辑完的草稿消息。 |


### 导入消息到会话相关接口
| API | 描述 |
| --- | --- |
| **saveMessage** | 向本地消息列表中添加一条消息，但并不将其发送出去。 |
| **importMessages** | 将消息导入本地数据库。 |


## TIMGroupManager

群组管理模块负责群组的创建群组、删除群组、邀请群成员、删除群成员、修改群信息和修改群成员信息等功能。

### 获取群组实例
| API | 描述 |
| --- | --- |
| **sharedInstance** | 获取群管理器实例。 |


### 创建/删除/加入/退出群组
| API | 描述 |
| --- | --- |
| **createPrivateGroup** | 创建私有群。 |
| **createPublicGroup** | 创建公开群。 |
| **createChatRoomGroup** | 创建聊天室。 |
| **createAVChatRoomGroup** | 创建音视频聊天室。 |
| **createGroup** | 创建指定类型和 ID 的群组。 |
| **createGroup** | 创建自定义群组。 |
| **deleteGroup** | 解散群组。 |
| **joinGroup** | 申请加群。 |
| **quitGroup** | 主动退出群组。 |


### 邀请/删除群成员
| API | 描述 |
| --- | --- |
| **inviteGroupMember** | 邀请好友入群。 |
| **deleteGroupMemberWithReason** | 删除群成员。 |


### 获取群信息
| API | 描述 |
| --- | --- |
| **getGroupList** | 获取群列表。 |
| **getGroupInfo** | 获取服务器存储的群组信息。 |
| **queryGroupInfo** | 获取本地存储的群组信息。 |
| **getGroupMembers** | 获取群成员列表。 |
| **getGroupSelfInfo** | 获取本人在群组内的成员信息。 |
| **getGroupMembersInfo** | 获取群组指定成员的信息。 |
| **getGroupMembers** | 获取指定类型的成员列表（支持按字段拉取，分页）。 |
| **getReciveMessageOpt** | 获取接受消息选项。 |


### 修改群信息
| API | 描述 |
| --- | --- |
| **modifyGroupName** | 修改群名。 |
| **modifyGroupIntroduction** | 修改群简介。 |
| **modifyGroupNotification** | 修改群公告。 |
| **modifyGroupFaceUrl** | 修改群头像。 |
| **modifyGroupAddOpt** | 修改加群选项。 |
| **modifyGroupSearchable** | 修改群组是否可被搜索属性。 |
| **modifyReceiveMessageOpt** | 修改接受消息选项。 |
| **modifyGroupAllShutup** | 修改群组全员禁言属性。 |
| **modifyGroupCustomInfo** | 修改群自定义字段集合。 |
| **modifyGroupOwner** | 转让群给新群主。 |


### 修改群成员信息
| API | 描述 |
| --- | --- |
| **modifyGroupMemberInfoSetNameCard** | 修改群成员名片。 |
| **modifyGroupMemberInfoSetRole** | 修改群成员角色。 |
| **modifyGroupMemberVisible** | 修改群组成员是否可见属性。 |
| **modifyGroupMemberInfoSetSilence** | 禁言用户。 |
| **modifyGroupMemberInfoSetCustomInfo** | 修改群成员自定义字段集合。 |


### 群未处理请求逻辑
| API | 描述 |
| --- | --- |
| **getPendencyFromServer** | 获取群组未处理请求列表。 |
| **pendencyReport** | 上报群未处理列表已读。 |


## TIMFriendshipManager

资料关系链管理模块负责添加好友、删除好友、获取好友相关信息以及修改资料等功能。

| API | 描述 |
| --- | --- |
| **sharedInstance** | 获取好友管理器实例。 |
| **modifySelfProfile** | 设置自己的资料。 |
| **getSelfProfile** | 获取自己的资料。 |
| **querySelfProfile** | 在缓存中查询自己的资料。 |
| **getUsersProfile** | 获取指定用户资料。 |
| **queryUserProfile** | 在缓存中查询用户的资料。 |
| **getFriendList** | 获取好友列表。 |
| **queryFriend** | 在缓存中查询用户的关系链数据。 |
| **queryFriendList** | 获取缓存中的关系链列表。 |
| **checkFriends** | 检查指定用户的好友关系。 |
| **addFriend** | 添加好友。 |
| **doResponse** | 响应对方好友邀请。 |
| **deleteFriends** | 删除好友。 |
| **modifyFriend** | 修改好友。 |
| **getPendencyList** | 获取未决列表。 |
| **deletePendency** | 删除未决消息。 |
| **pendencyReport** | 上报未决消息已读。 |
| **getBlackList** | 获取黑名单列表。 |
| **addBlackList** | 添加用户到黑名单。 |
| **deleteBlackList** | 从黑名单中删除指定用户。 |
| **createFriendGroup** | 新建好友分组。 |
| **getFriendGroups** | 获取指定的好友分组信息。 |
| **deleteFriendGroup** | 删除好友分组。 |
| **renameFriendGroup** | 修改好友分组的名称。 |
| **addFriendsToFriendGroup** | 添加好友至指定好友分组。 |
| **deleteFriendsFromFriendGroup** | 从指定分组中删除指定好友。 |


## TIMMessage

**TIMMessage** 由多个 **TIMElem** 组成，每个 TIMElem 可以是文本或图片，即每条消息可包含多个文本或图片。

| API | 描述 |
| --- | --- |
| **addElem** | 增加 Elem。 |
| **getElem** | 获取对应索引的 Elem。 |
| **elemCount** | 获取 Elem 数量。 |
| **setBusinessCmd** | 设置业务命令字。 |
| **status** | 查询消息状态。 |
| **isSelf** | 确认自己是为否发送方。 |
| **sender** | 获取消息的发送方。 |
| **msgId** | 获取消息 ID。 |
| **uniqueId** | 获取消息 uniqueId。 |
| **timestamp** | 获取当前消息的时间戳。 |
| **isReaded** | 确认自己是否已读。 |
| **isPeerReaded** | 确认对方是否已读（仅 C2C 消息有效）。 |
| **locator** | 获取消息定位符。 |
| **respondsToLocator** | 确认是否为 locator 对应的消息。 |
| **remove** | 删除消息。 |
| **getConversation** | 获取会话。 |
| **getSenderProfile** | 获取发送者资料。 |
| **getSenderGroupMemberProfile** | 获取发送者群内资料。 |
| **setPriority** | 设置消息的优先级（仅对群组消息有效）。 |
| **getPriority** | 获取消息的优先级（仅对群组消息有效）。 |
| **setOfflinePushInfo** | 配置消息离线推送相关参数。 |
| **getOfflinePushInfo** | 获取消息离线推送配置。 |
| **setCustomInt** | 设置自定义整数，默认为0。 |
| **customInt** | 获取 CustomInt。 |
| **setCustomData** | 设置自定义数据，默认为空串`""`。 |
| **customData** | 获取 CustomData。 |
| **copyFrom** | 复制消息中的属性（复制对象包括 ELem、priority、online 以及 offlinePushInfo）。 |
| **convertToImportedMsg** | 将消息导入到本地。 |
| **setTime** | 设置消息时间戳。 |
| **setSender** | 设置消息发送方。 |


