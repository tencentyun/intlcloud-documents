## 帐号管理

| 功能说明  | 接口 |
|---------|---------|
| 导入单个帐号 | [v4/im_open_login_svc/account_import](https://intl.cloud.tencent.com/document/product/1047/34953) |
| 导入多个帐号 | [v4/im_open_login_svc/multiaccount_import](https://intl.cloud.tencent.com/document/product/1047/34954) |
| 删除帐号  | [v4/im_open_login_svc/account_delete](https://intl.cloud.tencent.com/document/product/1047/34955) |
| 查询帐号  | [v4/im_open_login_svc/account_check](https://intl.cloud.tencent.com/document/product/1047/34956)  | 
| 失效帐号登录态  | [v4/im_open_login_svc/kick](https://intl.cloud.tencent.com/document/product/1047/34957) |
| 查询帐号在线状态 | [ v4/openim/querystate](https://intl.cloud.tencent.com/document/product/1047/35477) |

## 单聊消息

| 功能说明  | 接口 |
|---------|---------|
| 单发单聊消息 | [v4/openim/sendmsg](https://intl.cloud.tencent.com/document/product/1047/34919) |
| 批量发单聊消息 | [v4/openim/batchsendmsg](https://intl.cloud.tencent.com/document/product/1047/34920) |
| 导入单聊消息 | [v4/openim/importmsg](https://intl.cloud.tencent.com/document/product/1047/35014) |
| 查询单聊消息 | [v4/openim/admin_getroammsg](https://intl.cloud.tencent.com/document/product/1047/35478) |
| 撤回单聊消息 | [v4/openim/admin_msgwithdraw](https://intl.cloud.tencent.com/document/product/1047/35015) |




## 资料管理

| 功能说明 | 接口                                                         |
| -------- | ------------------------------------------------------------ |
| 拉取资料 | [v4/profile/portrait_get](https://intl.cloud.tencent.com/document/product/1047/34917) |
| 设置资料 | [v4/profile/portrait_set](https://intl.cloud.tencent.com/document/product/1047/34916 ) |

## 关系链管理

| 功能说明 | 接口                                                         |
| -------- | ------------------------------------------------------------ |
| 添加好友 | [v4/sns/friend_add](https://intl.cloud.tencent.com/document/product/1047/34902) |
| 导入好友 | [v4/sns/friend_import](https://intl.cloud.tencent.com/document/product/1047/34903) |
| 删除好友 | [v4/sns/friend_delete](https://intl.cloud.tencent.com/document/product/1047/34905) |
| 删除所有好友 | [v4/sns/friend_delete_all](https://intl.cloud.tencent.com/document/product/1047/34906) |
| 校验好友 | [v4/sns/friend_check](https://intl.cloud.tencent.com/document/product/1047/34907) |
| 拉取好友 | [v4/sns/friend_get](https://intl.cloud.tencent.com/document/product/1047/34908) |
| 拉取指定好友 | [v4/sns/friend_get_list](https://intl.cloud.tencent.com/document/product/1047/34910) |
| 添加黑名单 | [v4/sns/black_list_add](https://intl.cloud.tencent.com/document/product/1047/34911) |
| 删除黑名单 | [v4/sns/black_list_delete](https://intl.cloud.tencent.com/document/product/1047/34912) |
| 拉取黑名单 | [v4/sns/black_list_get](https://intl.cloud.tencent.com/document/product/1047/34914) |
| 校验黑名单 | [v4/sns/black_list_check](https://intl.cloud.tencent.com/document/product/1047/34913) |
| 添加分组 | [v4/sns/group_add](https://intl.cloud.tencent.com/document/product/1047/34950) |
| 删除分组 | [v4/sns/group_delete](https://intl.cloud.tencent.com/document/product/1047/34926) |



## 群组管理

| 功能说明               | 接口                                                         |
| ---------------------- | ------------------------------------------------------------ |
| 获取 App 中的所有群组    | [v4/group_open_http_svc/get_appid_group_list](https://intl.cloud.tencent.com/document/product/1047/34960) |
| 创建群组               | [v4/group_open_http_svc/create_group](https://intl.cloud.tencent.com/document/product/1047/34895) |
| 获取群组详细资料       | [v4/group_open_http_svc/get_group_info](https://intl.cloud.tencent.com/document/product/1047/34961) |
| 获取群成员详细资料     | [v4/group_open_http_svc/get_group_member_info](https://intl.cloud.tencent.com/document/product/1047/34948) |
| 修改群组基础资料       | [v4/group_open_http_svc/modify_group_base_info](https://intl.cloud.tencent.com/document/product/1047/34962) |
| 增加群组成员           | [v4/group_open_http_svc/add_group_member](https://intl.cloud.tencent.com/document/product/1047/34921) |
| 删除群组成员           | [v4/group_open_http_svc/delete_group_member](https://intl.cloud.tencent.com/document/product/1047/34949) |
| 修改群组成员资料       | [v4/group_open_http_svc/modify_group_member_info](https://intl.cloud.tencent.com/document/product/1047/34900) |
| 解散群组               | [v4/group_open_http_svc/destroy_group ](https://intl.cloud.tencent.com/document/product/1047/34896) |
| 获取用户所加入的群组   | [v4/group_open_http_svc/get_joined_group_list](https://intl.cloud.tencent.com/document/product/1047/34925) |
| 查询用户在群组中的身份 | [v4/group_open_http_svc/get_role_in_group](https://intl.cloud.tencent.com/document/product/1047/34963) |
| 批量禁言和取消禁言     | [v4/group_open_http_svc/forbid_send_msg](https://intl.cloud.tencent.com/document/product/1047/34951) |
| 获取群组被禁言用户列表 | [v4/group_open_http_svc/get_group_shutted_uin](https://intl.cloud.tencent.com/document/product/1047/34964) |
| 在群组中发送普通消息   | [v4/group_open_http_svc/send_group_msg](https://intl.cloud.tencent.com/document/product/1047/34959) |
| 在群组中发送系统通知   | [v4/group_open_http_svc/send_group_system_notification](https://intl.cloud.tencent.com/document/product/1047/34958) |
| 群组消息撤回           | [v4/group_open_http_svc/group_msg_recall](https://intl.cloud.tencent.com/document/product/1047/34965) |
| 转让群组               | [v4/group_open_http_svc/change_group_owner](https://intl.cloud.tencent.com/document/product/1047/34966) |
| 导入群基础资料         | [v4/group_open_http_svc/import_group](https://intl.cloud.tencent.com/document/product/1047/34967) |
| 导入群消息             | [v4/group_open_http_svc/import_group_msg ](https://intl.cloud.tencent.com/document/product/1047/34968) |
| 导入群成员             | [v4/group_open_http_svc/import_group_member](https://intl.cloud.tencent.com/document/product/1047/34969) |
| 设置成员未读消息计数   | [v4/group_open_http_svc/set_unread_msg_num](https://intl.cloud.tencent.com/document/product/1047/34909) |
| 删除指定用户发送的消息 | [v4/group_open_http_svc/delete_group_msg_by_sender](https://intl.cloud.tencent.com/document/product/1047/34970) |
| 拉取群漫游消息         | [v4/group_open_http_svc/group_msg_get_simple](https://intl.cloud.tencent.com/document/product/1047/34971) |


## 全局禁言管理
| 功能说明 |接口 |
|---------|---------|
| 设置全局禁言 |[ v4/openconfigsvr/setnospeaking](https://intl.cloud.tencent.com/document/product/1047/34923) |
| 查询全局禁言 |[ v4/openconfigsvr/getnospeaking](https://intl.cloud.tencent.com/document/product/1047/34924) |



## 运营管理

| 功能说明 |接口 |
|---------|---------|
| 下载消息记录  |[v4/open_msg_svc/get_history](https://intl.cloud.tencent.com/document/product/1047/34885) |
| 拉取运营数据  |[v4/openconfigsvr/getappinfo](https://intl.cloud.tencent.com/document/product/1047/34886) |
