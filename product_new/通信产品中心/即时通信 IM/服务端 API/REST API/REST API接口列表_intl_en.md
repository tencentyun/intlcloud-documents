## Account Management

| Feature Description  | API |
|---------|---------|
| Import an account. | v4/im_open_login_svc/account_import |
| Batch imports accounts. | v4/im_open_login_svc/multiaccount_import |
| Deletes accounts.  | v4/im_open_login_svc/account_delete |
| Checks accounts.  | v4/im_open_login_svc/account_check  |
| Invalidates the login state of an account.  | v4/im_open_login_svc/kick |



## Online States

| Feature Description         | API                                                       |
| ---------------- | ---------------------------------------------------------- |
| Obtains uers' online states. | v4/openim/querystate |

## Profile Management

| Feature Description | API                                                         |
| -------- | ------------------------------------------------------------ |
| Pulls profiles. | v4/profile/portrait_get |
| Configures profiles. | v4/profile/portrait_set |

## Relationship Chain Management

| Feature Description | API                                                         |
| -------- | ------------------------------------------------------------ |
| Adds friends. | v4/sns/friend_add |
| Imports friends. | v4/sns/friend_import |
| Deletes friends. | v4/sns/friend_delete |
| Deletes all friends. | v4/sns/friend_delete_all |
| Verifies friends. | v4/sns/friend_check |
| Pulls friends. | v4/sns/friend_get |
| Pulls specific friends. | v4/sns/friend_get_list |
| Adds a blacklist. | v4/sns/black_list_add |
| Deletes a blacklist. | v4/sns/black_list_delete |
| Pulls a blacklist. | v4/sns/black_list_get |
| Verifies a blacklist. | v4/sns/black_list_check |
| Adds a list. | v4/sns/group_add |
| Deletes a list. | v4/sns/group_delete |

## One-to-one Message

| Feature Description  | API |
|---------|---------|
| Sends a one-to-one message. | v4/openim/sendmsg |
| Batch sends one-to-one messages. | v4/openim/batchsendmsg |
| Imports one-to-one messages. | v4/openim/importmsg |
| Recalls one-to-one messages. | v4/openim/admin_msgwithdraw |

## Group Management

| Feature Description               | API                                                         |
| ---------------------- | ------------------------------------------------------------ |
| Obtains all groups in an app.    | v4/group_open_http_svc/get_appid_group_list |
| Creates a group.               | v4/group_open_http_svc/create_group |
| Obtains detailed group profiles.       | v4/group_open_http_svc/get_group_info |
| Obtains detailed member profiles of a group.     | v4/group_open_http_svc/get_group_member_info |
| Modifies basic group profiles.       | v4/group_open_http_svc/modify_group_base_info |
| Adds group members.           | v4/group_open_http_svc/add_group_member |
| Deletes group members.           | v4/group_open_http_svc/delete_group_member |
| Modifies the profiles of group members.       | v4/group_open_http_svc/modify_group_member_info |
| Disbands groups.               | v4/group_open_http_svc/destroy_group |
| Obtains the groups a user has joined.   | v4/group_open_http_svc/get_joined_group_list |
| Queries the identity of a user in a group. | v4/group_open_http_svc/get_role_in_group |
| Batch mutes and unmutes group members.     | v4/group_open_http_svc/forbid_send_msg |
| Obtains muted users in a group. | v4/group_open_http_svc/get_group_shutted_uin |
| Sends ordinary messages in a group.   | v4/group_open_http_svc/send_group_msg |
| Sends system messages in a group.   | v4/group_open_http_svc/send_group_system_notification |
| Recalls messages in a group.           | v4/group_open_http_svc/group_msg_recall |
| Transfers the ownership of a group.               | v4/group_open_http_svc/change_group_owner |
| Imports basic group profiles.         | v4/group_open_http_svc/import_group |
| Imports group messages.             | v4/group_open_http_svc/import_group_msg |
| Imports group members.             | v4/group_open_http_svc/import_group_member |
| Configures unread message counts.   | v4/group_open_http_svc/set_unread_msg_num |
| Deletes messages sent by the specified user. | v4/group_open_http_svc/delete_group_msg_by_sender |
| Pulls roaming group messages.         | v4/group_open_http_svc/group_msg_get_simple |


## Global Mute Management
| Feature Description |API |
|---------|---------|
| Configures global mute. |v4/openconfigsvr/setnospeaking |
| Queries global mute. |v4/openconfigsvr/getnospeaking |



## Operations Management

| Feature Description |API |
|---------|---------|
| Downloads message history.  |v4/open_msg_svc/get_history |
| Pulls operations data.  |v4/openconfigsvr/getappinfo |
