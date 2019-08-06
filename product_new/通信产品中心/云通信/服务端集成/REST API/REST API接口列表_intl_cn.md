## 帐号管理

| 功能说明  | 接口 |
|---------|---------|
| 导入单个帐号 | [v4/im_open_login_svc/account_import](https://intl.cloud.tencent.com/document/product/1027/31313) |
| 导入批量帐号 | [v4/im_open_login_svc/multiaccount_import](https://intl.cloud.tencent.com/document/product/1027/31314) |
| 失效帐号登录态  | [v4/im_open_login_svc/kick](https://intl.cloud.tencent.com/document/product/1027/31316) |

## 在线状态

| 功能说明         | 接口                                                       |
| ---------------- | ---------------------------------------------------------- |
| 获取用户在线状态 | [ v4/openim/querystate](https://intl.cloud.tencent.com/document/product/1027/31322) |

## 资料管理

| 功能说明 | 接口                                                         |
| -------- | ------------------------------------------------------------ |
| 拉取资料 | [v4/profile/portrait_get](https://intl.cloud.tencent.com/document/product/1027/31324) |
| 设置资料 | [v4/profile/portrait_set](https://intl.cloud.tencent.com/document/product/1027/31325 ) |

## 关系链管理

| 功能说明 | 接口                                                         |
| -------- | ------------------------------------------------------------ |
| 添加好友 | [v4/sns/friend_add](https://intl.cloud.tencent.com/document/product/1027/31327) |
| 导入好友 | [v4/sns/friend_import](https://intl.cloud.tencent.com/document/product/1027/31328) |
| 删除好友 | [v4/sns/friend_delete](https://intl.cloud.tencent.com/document/product/1027/31330) |
| 删除所有好友 | [v4/sns/friend_delete_all](https://intl.cloud.tencent.com/document/product/1027/31331) |
| 校验好友 | [v4/sns/friend_check](https://intl.cloud.tencent.com/document/product/1027/31332) |
| 拉取好友 | [v4/sns/friend_get_all](https://intl.cloud.tencent.com/document/product/1027/31333) |
| 拉取指定好友 | [v4/sns/friend_get_list](https://intl.cloud.tencent.com/document/product/1027/31333) |
| 添加黑名单 | [v4/sns/black_list_add](https://intl.cloud.tencent.com/document/product/1027/31335) |
| 删除黑名单 | [v4/sns/black_list_delete](https://intl.cloud.tencent.com/document/product/1027/31336) |
| 拉取黑名单 | [v4/sns/black_list_get](https://intl.cloud.tencent.com/document/product/1027/31337) |
| 校验黑名单 | [v4/sns/black_list_check](https://intl.cloud.tencent.com/document/product/1027/31338) |
| 添加分组 | [v4/sns/group_add](https://intl.cloud.tencent.com/document/product/1027/31339) |
| 删除分组 | [v4/sns/group_delete](https://intl.cloud.tencent.com/document/product/1027/31340) |

## 单聊消息

| 功能说明  | 接口 |
|---------|---------|
| 单发单聊消息 | [v4/openim/sendmsg](https://intl.cloud.tencent.com/document/product/1027/31318) |
| 批量发单聊消息 | [v4/openim/batchsendmsg](https://intl.cloud.tencent.com/document/product/1027/31319) |
| 导入单聊消息 | [v4/openim/importmsg](https://intl.cloud.tencent.com/document/product/1027/31320) |

## 群组管理

| 功能说明               | 接口                                                         |
| ---------------------- | ------------------------------------------------------------ |
| 获取APP中的所有群组    | [v4/group_open_http_svc/get_appid_group_list](https://intl.cloud.tencent.com/document/product/1027/31342) |
| 创建群组               | [v4/group_open_http_svc/create_group](https://intl.cloud.tencent.com/document/product/1027/31343) |
| 获取群组详细资料       | [v4/group_open_http_svc/get_group_info](https://intl.cloud.tencent.com/document/product/1027/31344) |
| 获取群成员详细资料     | [v4/group_open_http_svc/get_group_member_info](https://intl.cloud.tencent.com/document/product/1027/31345) |
| 修改群组基础资料       | [v4/group_open_http_svc/modify_group_base_info](https://intl.cloud.tencent.com/document/product/1027/31346) |
| 增加群组成员           | [v4/group_open_http_svc/add_group_member](https://intl.cloud.tencent.com/document/product/1027/31347) |
| 删除群组成员           | [v4/group_open_http_svc/delete_group_member](https://intl.cloud.tencent.com/document/product/1027/31348) |
| 修改群组成员资料       | [v4/group_open_http_svc/modify_group_member_info](https://intl.cloud.tencent.com/document/product/1027/31349) |
| 解散群组               | [v4/group_open_http_svc/destroy_group ](https://intl.cloud.tencent.com/document/product/1027/31350) |
| 获取用户所加入的群组   | [v4/group_open_http_svc/get_joined_group_list](https://intl.cloud.tencent.com/document/product/1027/31351) |
| 查询用户在群组中的身份 | [v4/group_open_http_svc/get_role_in_group](https://intl.cloud.tencent.com/document/product/1027/31352) |
| 批量禁言和取消禁言     | [v4/group_open_http_svc/forbid_send_msg](https://intl.cloud.tencent.com/document/product/1027/31353) |
| 获取群组被禁言用户列表 | [v4/group_open_http_svc/get_group_shutted_uin](https://intl.cloud.tencent.com/document/product/1027/31354) |
| 在群组中发送普通消息   | [v4/group_open_http_svc/send_group_msg](https://intl.cloud.tencent.com/document/product/1027/31355) |
| 在群组中发送系统通知   | [v4/group_open_http_svc/send_group_system_notification](https://intl.cloud.tencent.com/document/product/1027/31356) |
| 群组消息撤回           | [v4/group_open_http_svc/group_msg_recall](https://intl.cloud.tencent.com/document/product/1027/31357) |
| 转让群组               | [v4/group_open_http_svc/change_group_owner](https://intl.cloud.tencent.com/document/product/1027/31358) |
| 导入群基础资料         | [v4/group_open_http_svc/import_group](https://intl.cloud.tencent.com/document/product/1027/31359) |
| 导入群消息             | [v4/group_open_http_svc/import_group_msg ](https://intl.cloud.tencent.com/document/product/1027/31360) |
| 导入群成员             | [v4/group_open_http_svc/import_group_member](https://intl.cloud.tencent.com/document/product/1027/31361) |
| 设置成员未读消息计数   | [v4/group_open_http_svc/set_unread_msg_num](https://intl.cloud.tencent.com/document/product/1027/31362) |
| 删除指定用户发送的消息 | [v4/group_open_http_svc/delete_group_msg_by_sender](https://intl.cloud.tencent.com/document/product/1027/31363) |
| 拉取群漫游消息         | [v4/group_open_http_svc/group_msg_get_simple](https://intl.cloud.tencent.com/document/product/1027/31364) |


## 全局禁言管理
| 功能说明 |接口 |
|---------|---------|
| 设置全局禁言 |[ v4/openconfigsvr/setnospeaking](https://intl.cloud.tencent.com/document/product/1027/31370) |
| 查询全局禁言 |[ v4/openconfigsvr/getnospeaking](https://intl.cloud.tencent.com/document/product/1027/31371) |

## 脏字管理

| 功能说明 | 接口 |
|---------|---------|
| 查询 App 自定义脏字  | [v4/openim_dirty_words/get](https://intl.cloud.tencent.com/document/product/1027/31366)|
| 添加 App 自定义脏字   | [v4/openim_dirty_words/add](https://intl.cloud.tencent.com/document/product/1027/31367) |
| 删除 App 自定义脏字  | [v4/openim_dirty_words/delete](https://intl.cloud.tencent.com/document/product/1027/31368) |

## 运营管理

| 功能说明 |接口 |
|---------|---------|
| 下载消息记录  |[v4/open_msg_svc/get_history](https://intl.cloud.tencent.com/document/product/1027/31374) |
| 拉取运营数据  |[v4/openconfigsvr/getappinfo](https://intl.cloud.tencent.com/document/product/1027/31373) |
