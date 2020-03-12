## Account Management

| Feature Description  | API |
|---------|---------|
| Import an account. | [v4/im_open_login_svc/account_import](https://intl.cloud.tencent.com/document/product/1047/34953) |
| Batch imports accounts. | [v4/im_open_login_svc/multiaccount_import](https://intl.cloud.tencent.com/document/product/1047/34954) |
| Deletes accounts.  | [v4/im_open_login_svc/account_delete](https://intl.cloud.tencent.com/document/product/1047/34955) |
| Checks accounts.  | [v4/im_open_login_svc/account_check](https://intl.cloud.tencent.com/document/product/1047/34956)  | 
| Invalidates the login state of an account.  | [v4/im_open_login_svc/kick](https://intl.cloud.tencent.com/document/product/1047/34957) |



## Online States

| Feature Description         | API                                                       |
| ---------------- | ---------------------------------------------------------- |
| Obtains uers' online states. | [ v4/openim/querystate](https://intl.cloud.tencent.com/document/product/1047/35057) |

## Profile Management

| Feature Description | API                                                         |
| -------- | ------------------------------------------------------------ |
| Pulls profiles. | [v4/profile/portrait_get](https://intl.cloud.tencent.com/document/product/1047/34917) |
| Configures profiles. | [v4/profile/portrait_set](https://intl.cloud.tencent.com/document/product/1047/34916 ) |

## Relationship Chain Management

| Feature Description | API                                                         |
| -------- | ------------------------------------------------------------ |
| Adds friends. | [v4/sns/friend_add](https://intl.cloud.tencent.com/document/product/1047/34902) |
| Imports friends. | [v4/sns/friend_import](https://intl.cloud.tencent.com/document/product/1047/34903) |
| Deletes friends. | [v4/sns/friend_delete](https://intl.cloud.tencent.com/document/product/1047/34905) |
| Deletes all friends. | [v4/sns/friend_delete_all](https://intl.cloud.tencent.com/document/product/1047/34906) |
| Verifies friends. | [v4/sns/friend_check](https://intl.cloud.tencent.com/document/product/1047/34907) |
| Pulls friends. | [v4/sns/friend_get](https://intl.cloud.tencent.com/document/product/1047/34908) |
| Pulls specific friends. | [v4/sns/friend_get_list](https://intl.cloud.tencent.com/document/product/1047/34910) |
| Adds a blacklist. | [v4/sns/black_list_add](https://intl.cloud.tencent.com/document/product/1047/34911) |
| Deletes a blacklist. | [v4/sns/black_list_delete](https://intl.cloud.tencent.com/document/product/1047/34912) |
| Pulls a blacklist. | [v4/sns/black_list_get](https://intl.cloud.tencent.com/document/product/1047/34914) |
| Verifies a blacklist. | [v4/sns/black_list_check](https://intl.cloud.tencent.com/document/product/1047/34913) |
| Adds a list. | [v4/sns/group_add](https://intl.cloud.tencent.com/document/product/1047/34950) |
| Deletes a list. | [v4/sns/group_delete](https://intl.cloud.tencent.com/document/product/1047/34926) |

## One-to-one Message

| Feature Description  | API |
|---------|---------|
| Sends a one-to-one message. | [v4/openim/sendmsg](https://intl.cloud.tencent.com/document/product/1047/34919) |
| Batch sends one-to-one messages. | [v4/openim/batchsendmsg](https://intl.cloud.tencent.com/document/product/1047/34920) |
| Imports one-to-one messages. | [v4/openim/importmsg](https://intl.cloud.tencent.com/document/product/1047/35014) |
| Recalls one-to-one messages. | [v4/openim/admin_msgwithdraw](https://intl.cloud.tencent.com/document/product/1047/35015) |

## Group Management

| Feature Description               | API                                                         |
| ---------------------- | ------------------------------------------------------------ |
| Obtains all groups in an app.    | [v4/group_open_http_svc/get_appid_group_list](https://intl.cloud.tencent.com/document/product/1047/34960) |
| Creates a group.               | [v4/group_open_http_svc/create_group](https://intl.cloud.tencent.com/document/product/1047/34895) |
| Obtains detailed group profiles.       | [v4/group_open_http_svc/get_group_info](https://intl.cloud.tencent.com/document/product/1047/34961) |
| Obtains detailed member profiles of a group.     | [v4/group_open_http_svc/get_group_member_info](https://intl.cloud.tencent.com/document/product/1047/34948) |
| Modifies basic group profiles.       | [v4/group_open_http_svc/modify_group_base_info](https://intl.cloud.tencent.com/document/product/1047/34962) |
| Adds group members.           | [v4/group_open_http_svc/add_group_member](https://intl.cloud.tencent.com/document/product/1047/34921) |
| Deletes group members.           | [v4/group_open_http_svc/delete_group_member](https://intl.cloud.tencent.com/document/product/1047/34949) |
| Modifies the profiles of group members.       | [v4/group_open_http_svc/modify_group_member_info](https://intl.cloud.tencent.com/document/product/1047/34900) |
| Disbands groups.               | [v4/group_open_http_svc/destroy_group ](https://intl.cloud.tencent.com/document/product/1047/34896) |
| Obtains the groups a user has joined.   | [v4/group_open_http_svc/get_joined_group_list](https://intl.cloud.tencent.com/document/product/1047/34925) |
| Queries the identity of a user in a group. | [v4/group_open_http_svc/get_role_in_group](https://intl.cloud.tencent.com/document/product/1047/34963) |
| Batch mutes and unmutes group members.     | [v4/group_open_http_svc/forbid_send_msg](https://intl.cloud.tencent.com/document/product/1047/34951) |
| Obtains muted users in a group. | [v4/group_open_http_svc/get_group_shutted_uin](https://intl.cloud.tencent.com/document/product/1047/34964) |
| Sends ordinary messages in a group.   | [v4/group_open_http_svc/send_group_msg](https://intl.cloud.tencent.com/document/product/1047/34959) |
| Sends system messages in a group.   | [v4/group_open_http_svc/send_group_system_notification](https://intl.cloud.tencent.com/document/product/1047/34958) |
| Recalls messages in a group.           | [v4/group_open_http_svc/group_msg_recall](https://intl.cloud.tencent.com/document/product/1047/34965) |
| Transfers the ownership of a group.               | [v4/group_open_http_svc/change_group_owner](https://intl.cloud.tencent.com/document/product/1047/34966) |
| Imports basic group profiles.         | [v4/group_open_http_svc/import_group](https://intl.cloud.tencent.com/document/product/1047/34967) |
| Imports group messages.             | [v4/group_open_http_svc/import_group_msg ](https://intl.cloud.tencent.com/document/product/1047/34968) |
| Imports group members.             | [v4/group_open_http_svc/import_group_member](https://intl.cloud.tencent.com/document/product/1047/34969) |
| Configures unread message counts.   | [v4/group_open_http_svc/set_unread_msg_num](https://intl.cloud.tencent.com/document/product/1047/34909) |
| Deletes messages sent by the specified user. | [v4/group_open_http_svc/delete_group_msg_by_sender](https://intl.cloud.tencent.com/document/product/1047/34970) |
| Pulls roaming group messages.         | [v4/group_open_http_svc/group_msg_get_simple](https://intl.cloud.tencent.com/document/product/1047/34971) |


## Global Mute Management
| Feature Description |API |
|---------|---------|
| Configures global mute. |[ v4/openconfigsvr/setnospeaking](https://intl.cloud.tencent.com/document/product/1047/34923) |
| Queries global mute. |[ v4/openconfigsvr/getnospeaking](https://intl.cloud.tencent.com/document/product/1047/34924) |



## Operations Management

| Feature Description |API |
|---------|---------|
| Downloads message history.  |[v4/open_msg_svc/get_history](https://intl.cloud.tencent.com/document/product/1047/34885) |
| Pulls operations data.  |[v4/openconfigsvr/getappinfo](https://intl.cloud.tencent.com/document/product/1047/34886) |
