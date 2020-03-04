## TIMManager

IM SDK 主核心模块，负责 IM SDK 的初始化、登录、创建会话以及管理推送等功能。
- 初始化：初始化是使用 IM SDK 的前提，调用 init 接口后，才能调用其它 API。
- 登录：需要设置 SDKAppID，UserID 和 UserSig 才能使用即时通信 IM 服务。
- 会话：一个会话对应一个聊天窗口，例如，与单个好友的 C2C 聊天或者一个聊天群都是一个会话。
- 推送：管理和设置离线推送的相关功能，包括 token 和开关等。

### 初始化相关接口
| API | 描述 |
| --- | --- |
| **getInstance** | 获取管理器实例 **TIMManager**。 |
| **init** | 初始化 SDK，设置全局配置信息。 |
| **unInit** | 反初始化。 |
| **getSdkConfig** | 获取全局配置信息。 |
| **setUserConfig** | 设置用户配置信息。 |
| **getUserConfig** | 获取用户配置信息。 |
| **addMessageListener** | 新增新消息接收监听。 |
| **removeMessageListener** | 移除消息监听。 |
| **isInited**| 确认是否已经初始化。 |


### 登录相关接口
| API | 描述 |
| --- | --- |
| **login** | 登录。 |
| **autoLogin** | 自动登录。 |
| **logout** | 登出。 |
| **getLoginUser** | 获取当前登录的用户。 |


### 会话管理器
| API | 描述 |
| --- | --- |
| **getConversationList** | 获取会话列表。 |
| **getConversation** | 获取单个会话。 |
| **deleteConversation** | 删除单个会话。 |
| **deleteConversationAndLocalMsgs** | 删除单个会话和对应的会话消息。 |


### 设置离线推送
| API | 描述 |
| --- | --- |
| **setOfflinePushToken** | 设置客户端 token 和证书 busiID。 |
| **setOfflinePushSettings** | 初始化离线推送配置，需登录后设置才生效。 |
| **getOfflinePushSettings** | 获取离线推送配置，需登录后才能获取。 |
| **setOfflinePushListener** | 设置 App 在后台时的消息通知监听器（已废弃）。 |
| **doBackground** | 上报 App 应用退至后台。 |
| **doForeground** | 上报 App 应用切换回前台。 |


### 未登录查看本地会话和消息
| API | 描述 |
| --- | --- |
| **initStorage** | 在未登录的情况下加载本地存储。 |


### 调试相关接口
| API | 描述 |
| --- | --- |
| **getVersion** | 获取版本号。 |
| **addMessageUpdateListener** | 添加一个消息更新监听器，以便监听消息变更。 |
| **removeMessageUpdateListener** | 删除一个消息更新监听器。 |
| **getNetworkStatus** | 获取网络连接状态。 |
| **getServerTimeDiff** | 获取服务器与本地的时间差，单位为秒，`时间差值 = svrTime - localTime`。 |


## TIMConversation

一个会话对应一个聊天窗口，例如，与单个好友的 C2C 聊天或者一个聊天群都是一个会话。
**TIMConversation** 提供的接口函数都是围绕消息的相关操作，包括发送消息、获取历史消息、设置消息已读、撤回消息和删除消息等。

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
| **getUnreadMessageNum** | 获取会话的未读消息计数。 |


### 撤回/删除消息相关接口
| API | 描述 |
| --- | --- |
| **revokeMessage** | 撤回一条已发送的消息（消息发送成功后）。 |
| **deleteLocalMessage** | 删除当前会话的本地历史消息。 |


### 获取会话信息相关接口
| API | 描述 |
| --- | --- |
| **getType** | 获取会话类型。 |
| **getPeer** | 获取会话 ID。 |
| **getGroupName** | 获取群名称。 |


### 草稿箱
| API | 描述 |
| --- | --- |
| **setDraft** | 添加未编辑完的草稿消息。 |
| **getDraft** | 获取未编辑完的草稿消息。 |
| **hasDraft** | 确认当前会话是否存在草稿。 |


### 导入消息到会话相关接口
| API | 描述 |
| --- | --- |
| **saveMessage** | 向本地消息列表中添加一条消息，但并不将其发送出去。 |
| **importMsg** | 将消息导入本地数据库。 |
| **findMessages** | 根据提供的消息定位符查找相应消息。 |


## TIMGroupManager

群组管理模块负责群组的创建群组、删除群组、邀请群成员、删除群成员、修改群信息和修改群成员信息等功能。

### 获取群组实例
| API | 描述 |
| --- | --- |
| **getInstance** | 获取群管理器实例。 |


### 创建/删除/加入/退出群组
| API | 描述 |
| --- | --- |
| **createGroup** | 创建群组。 |
| **deleteGroup** | 解散群组。 |
| **applyJoinGroup** | 申请加群。 |
| **quitGroup** | 主动退出群组。 |


### 邀请/删除群成员
| API | 描述 |
| --- | --- |
| **inviteGroupMember** | 邀请好友入群。 |
| **deleteGroupMember** | 删除群成员。 |


### 获取群信息
| API | 描述 |
| --- | --- |
| **getGroupList** | 获取群列表。 |
| **getGroupInfo** | 获取服务器存储的群组信息。 |
| **queryGroupInfo** | 获取本地存储的群组信息。 |
| **getGroupMembers** | 获取群成员列表。 |
| **getSelfInfo** | 获取本人在群组内的成员信息。 |
| **getGroupMembersInfo** | 获取群组指定成员的信息。 |
| **getGroupMembersByFilter** | 获取指定类型的成员列表（支持按字段拉取，分页）。 |


### 修改群信息
| API | 描述 |
| --- | --- |
| **modifyGroupInfo** | 修改群组基本信息。 |
| **modifyGroupOwner** | 转让群给新群主。 |


### 修改群成员信息
| API | 描述 |
| --- | --- |
| **modifyMemberInfo** | 修改群成员资料。 |


### 群未处理请求逻辑
| API | 描述 |
| --- | --- |
| **getGroupPendencyList** | 获取群组未处理请求列表。 |
| **reportGroupPendency** | 上报群未处理列表已读。 |


## TIMFriendshipManager

资料关系链管理模块负责添加好友、删除好友、获取好友相关信息以及修改资料等功能。

| API | 描述 |
| --- | --- |
| **getInstance** | 获取好友管理器实例。 |
| **init** | 初始化 TIMFriendshipManager。 |
| **getUsersProfile** | 获取指定用户资料。 |
| **getSelfProfile** | 获取自己资料。 |
| **querySelfProfile** | 获取本地自己的资料，没有则返回 null。 |
| **queryUserProfile** | 获取本地用户资料，没有则返回 null。 |
| **modifySelfProfile** | 修改自己的资料。 |
| **getFriendList** | 获取好友列表。 |
| **queryFriendList** | 获取缓存中的关系链列表，缓存数据来自前一次调用 **getFriendList** 的返回结果，请确保已调用过 getFriendList。 |
| **queryFriend** | 在缓存中查询用户的关系链数据，缓存数据来自前一次调用**getFriendList** 的返回结果，请确保已调用过 getFriendList。 |
| **addFriend** | 添加好友。 |
| **deleteFriends** | 删除好友。 |
| **modifyFriend** | 修改好友资料。 |
| **doResponse** | 处理好友请求。 |
| **createFriendGroup** | 新建好友分组。 |
| **getFriendGroups** | 获取指定的好友分组，传入 null 时表示获得所有分组信息。 |
| **deleteFriendGroup** | 删除好友分组。 |
| **renameFriendGroup** | 重命名好友分组。 |
| **addFriendsToFriendGroup** | 添加好友至指定分组。 |
| **deleteFriendsFromFriendGroup** | 从指定分组中删除指定好友。 |
| **getPendencyList** | 获取未决列表。 |
| **deletePendency** | 删除未决消息。 |
| **pendencyReport** | 上报未决消息已读。 |
| **getBlackList** | 获取黑名单列表。 |
| **addBlackList** | 添加用户到黑名单。 |
| **deleteBlackList** |从黑名单中删除指定用户。 |
| **checkFriends** | 检查指定用户的好友关系。 |


## TIMMessage

**TIMMessage** 由多个消息元素（TIMElem）组成，每个 TIMElem 都可以是文本或图片，即每条消息可包含多个文本或图片。<!--详情请参见 [消息收发]()。-->

| API | 描述 |
| --- | --- |
| **addElement** | 增加消息元素。 |
| **getElement** | 获取对应索引的 Elem。 |
| **getElementCount** | 获取 Elem 数量。 |
| **status** | 查询消息状态。 |
| **isSelf** | 确认自己是否为发送方。 |
| **getSender** | 获取消息的发送方。 |
| **getMsgId** | 获取消息 ID。 |
| **getMsgUniqueId** | 获取消息 uniqueId。 |
| **timestamp** | 获取当前消息的时间戳。 |
| **isRead** | 确认自己是否已读。 |
| **isPeerReaded** | 确认对方是否已读（仅 C2C 消息有效）。 |
| **getMessageLocator** | 获取消息定位符。 |
| **checkEquals** | 确认是否为 locator 对应的消息。 |
| **remove** | 删除消息。 |
| **getConversation** | 获取会话。 |
| **getSenderProfile** | 获取发送者资料。 |
| **getSenderGroupMemberProfile** | 获取发送者群内资料。 |
| **setPriority** | 设置消息的优先级（仅对群组消息有效）。 |
| **getPriority** | 获取消息的优先级（仅对群组消息有效）。 |
| **setOfflinePushSettings** | 配置消息离线推送相关参数。 |
| **getOfflinePushSettings** | 获取消息离线推送配置。 |
| **setCustomInt** | 设置自定义整数， 默认为0（此属性仅本地使用）。 |
| **getCustomInt** | 获取自定义整数。 |
| **setCustomStr** | 设置自定义数据内容，默认为空串`""`（此属性仅本地使用）。 |
| **getCustomStr** | 获取自定义数据内容的值。 |
| **copyFrom** | 复制消息内容到当前消息（复制对象包括 Elem、priority、online 以及 offlinePushInfo 等）。 |
| **convertToImportedMsg** | 将消息导入到本地。 |
| **setTimestamp** | 设置消息时间。 |
| **setSender** | 设置消息发送方 ID。 |
| **getRecvFlag** | 获取消息通知类型。 |
| **getRand** | 获取当前消息的随机码。 |
| **getSeq** | 获取当前消息的序列号。 |


