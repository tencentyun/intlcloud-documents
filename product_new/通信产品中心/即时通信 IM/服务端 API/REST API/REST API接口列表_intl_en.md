## Account Management

| Feature Description  | API |
|---------|---------|
| Import an account. | [v4/im_open_login_svc/account_import](https://cloud.tencent.com/document/product/269/1608) |
| Batch imports accounts. | [v4/im_open_login_svc/multiaccount_import](https://cloud.tencent.com/document/product/269/4919) |
| Deletes accounts.  | [v4/im_open_login_svc/account_delete](https://cloud.tencent.com/document/product/269/36443) |
| Checks accounts.  | [v4/im_open_login_svc/account_check](https://cloud.tencent.com/document/product/269/38417)  | 
| Invalidates the login state of an account.  | [v4/im_open_login_svc/kick](https://cloud.tencent.com/document/product/269/3853) |



## Online States

| Feature Description         | API                                                       |
| ---------------- | ---------------------------------------------------------- |
| Obtains uers' online states. | [ v4/openim/querystate](https://cloud.tencent.com/document/product/269/2566) |

## Profile Management

| Feature Description | API                                                         |
| -------- | ------------------------------------------------------------ |
| Pulls profiles. | [v4/profile/portrait_get](https://cloud.tencent.com/document/product/269/1639) |
| Configures profiles. | [v4/profile/portrait_set](https://cloud.tencent.com/document/product/269/1640 ) |

## Relationship Chain Management

| Feature Description | API                                                         |
| -------- | ------------------------------------------------------------ |
| Adds friends. | [v4/sns/friend_add](https://cloud.tencent.com/document/product/269/1643) |
| Imports friends. | [v4/sns/friend_import](https://cloud.tencent.com/document/product/269/8301) |
| Deletes friends. | [v4/sns/friend_delete](https://cloud.tencent.com/document/product/269/1644) |
| Deletes all friends. | [v4/sns/friend_delete_all](https://cloud.tencent.com/document/product/269/1645) |
| Verifies friends. | [v4/sns/friend_check](https://cloud.tencent.com/document/product/269/1646) |
| Pulls friends. | [v4/sns/friend_get](https://cloud.tencent.com/document/product/269/1647) |
| Pulls specific friends. | [v4/sns/friend_get_list](https://cloud.tencent.com/document/product/269/8609) |
| Adds a blacklist. | [v4/sns/black_list_add](https://cloud.tencent.com/document/product/269/3718) |
| Deletes a blacklist. | [v4/sns/black_list_delete](https://cloud.tencent.com/document/product/269/3719) |
| Pulls a blacklist. | [v4/sns/black_list_get](https://cloud.tencent.com/document/product/269/3722) |
| Verifies a blacklist. | [v4/sns/black_list_check](https://cloud.tencent.com/document/product/269/3725) |
| Adds a list. | [v4/sns/group_add](https://cloud.tencent.com/document/product/269/10107) |
| Deletes a list. | [v4/sns/group_delete](https://cloud.tencent.com/document/product/269/10108) |

## One-to-one Message

| Feature Description  | API |
|---------|---------|
| Sends a one-to-one message. | [v4/openim/sendmsg](https://cloud.tencent.com/document/product/269/2282) |
| Batch sends one-to-one messages. | [v4/openim/batchsendmsg](https://cloud.tencent.com/document/product/269/1612) |
| Imports one-to-one messages. | [v4/openim/importmsg](https://cloud.tencent.com/document/product/269/2568) |
| Recalls one-to-one messages. | [v4/openim/admin_msgwithdraw](https://cloud.tencent.com/document/product/269/38980) |

## Group Management

| Feature Description               | API                                                         |
| ---------------------- | ------------------------------------------------------------ |
| Obtains all groups in an app.    | [v4/group_open_http_svc/get_appid_group_list](https://cloud.tencent.com/document/product/269/1614) |
| Creates a group.               | [v4/group_open_http_svc/create_group](https://cloud.tencent.com/document/product/269/1615) |
| Obtains detailed group profiles.       | [v4/group_open_http_svc/get_group_info](https://cloud.tencent.com/document/product/269/1616) |
| Obtains detailed member profiles of a group.     | [v4/group_open_http_svc/get_group_member_info](https://cloud.tencent.com/document/product/269/1617) |
| Modifies basic group profiles.       | [v4/group_open_http_svc/modify_group_base_info](https://cloud.tencent.com/document/product/269/1620) |
| Adds group members.           | [v4/group_open_http_svc/add_group_member](https://cloud.tencent.com/document/product/269/1621) |
| Deletes group members.           | [v4/group_open_http_svc/delete_group_member](https://cloud.tencent.com/document/product/269/1622) |
| Modifies the profiles of group members.       | [v4/group_open_http_svc/modify_group_member_info](https://cloud.tencent.com/document/product/269/1623) |
| Disbands groups.               | [v4/group_open_http_svc/destroy_group ](https://cloud.tencent.com/document/product/269/1624) |
| Obtains the groups a user has joined.   | [v4/group_open_http_svc/get_joined_group_list](https://cloud.tencent.com/document/product/269/1625) |
| Queries the identity of a user in a group. | [v4/group_open_http_svc/get_role_in_group](https://cloud.tencent.com/document/product/269/1626) |
| Batch mutes and unmutes group members.     | [v4/group_open_http_svc/forbid_send_msg](https://cloud.tencent.com/document/product/269/1627) |
| Obtains muted users in a group. | [v4/group_open_http_svc/get_group_shutted_uin](https://cloud.tencent.com/document/product/269/2925) |
| Sends ordinary messages in a group.   | [v4/group_open_http_svc/send_group_msg](https://cloud.tencent.com/document/product/269/1629) |
| Sends system messages in a group.   | [v4/group_open_http_svc/send_group_system_notification](https://cloud.tencent.com/document/product/269/1630) |
| Recalls messages in a group.           | [v4/group_open_http_svc/group_msg_recall](https://cloud.tencent.com/document/product/269/12341) |
| Transfers the ownership of a group.               | [v4/group_open_http_svc/change_group_owner](https://cloud.tencent.com/document/product/269/1633) |
| Imports basic group profiles.         | [v4/group_open_http_svc/import_group](https://cloud.tencent.com/document/product/269/1634) |
| Imports group messages.             | [v4/group_open_http_svc/import_group_msg ](https://cloud.tencent.com/document/product/269/1635) |
| Imports group members.             | [v4/group_open_http_svc/import_group_member](https://cloud.tencent.com/document/product/269/1636) |
| Configures unread message counts.   | [v4/group_open_http_svc/set_unread_msg_num](https://cloud.tencent.com/document/product/269/1637) |
| Deletes messages sent by the specified user. | [v4/group_open_http_svc/delete_group_msg_by_sender](https://cloud.tencent.com/document/product/269/2359) |
| Pulls roaming group messages.         | [v4/group_open_http_svc/group_msg_get_simple](https://cloud.tencent.com/document/product/269/2738) |


## Global Mute Management
| Feature Description |API |
|---------|---------|
| Configures global mute. |[ v4/openconfigsvr/setnospeaking](https://cloud.tencent.com/document/product/269/4230) |
| Queries global mute. |[ v4/openconfigsvr/getnospeaking](https://cloud.tencent.com/document/product/269/4229) |



## Operations Management

| Feature Description |API |
|---------|---------|
| Downloads message history.  |[v4/open_msg_svc/get_history](https://cloud.tencent.com/document/product/269/1650) |
| Pulls operations data.  |[v4/openconfigsvr/getappinfo](https://cloud.tencent.com/document/product/269/4193) |
