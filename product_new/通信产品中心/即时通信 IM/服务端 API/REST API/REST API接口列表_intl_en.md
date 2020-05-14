## Account Management

| Feature Description | API |
|---------|---------|
| Importing an account | [v4/im_open_login_svc/account_import](https://intl.cloud.tencent.com/document/product/1047/34953) |
| Importing multiple accounts | [v4/im_open_login_svc/multiaccount_import](https://intl.cloud.tencent.com/document/product/1047/34954) |
| Deleting accounts | [v4/im_open_login_svc/account_delete](https://intl.cloud.tencent.com/document/product/1047/34955) |
| Querying accounts | [v4/im_open_login_svc/account_check](https://intl.cloud.tencent.com/document/product/1047/34956) | 
| Invalidating the login state of an account | [v4/im_open_login_svc/kick](https://intl.cloud.tencent.com/document/product/1047/34957) |
| Querying the online status of an account | [ v4/openim/querystate](https://intl.cloud.tencent.com/document/product/1047/35477) |

## One-to-one Message

| Feature Description | API |
|---------|---------|
| Sending a one-to-one message | [v4/openim/sendmsg](https://intl.cloud.tencent.com/document/product/1047/34919) |
| Batch sending one-to-one messages | [v4/openim/batchsendmsg](https://intl.cloud.tencent.com/document/product/1047/34920) |
| Importing one-to-one messages | [v4/openim/importmsg](https://intl.cloud.tencent.com/document/product/1047/35014) |
| Querying one-to-one messages | [v4/openim/admin_getroammsg](https://intl.cloud.tencent.com/document/product/1047/35478) |
| Recalling one-to-one messages | [v4/openim/admin_msgwithdraw](https://intl.cloud.tencent.com/document/product/1047/35015) |




## Profile Management

| Feature Description | API |
| -------- | ------------------------------------------------------------ |
| Pulling profiles | [v4/profile/portrait_get](https://intl.cloud.tencent.com/document/product/1047/34917) |
| Configuring profiles | [v4/profile/portrait_set](https://intl.cloud.tencent.com/document/product/1047/34916) |

## Relationship Chain Management

| Feature Description | API |
| -------- | ------------------------------------------------------------ |
| Adding friends | [v4/sns/friend_add](https://intl.cloud.tencent.com/document/product/1047/34902) |
| Importing friends | [v4/sns/friend_import](https://intl.cloud.tencent.com/document/product/1047/34903) |
| Deleting friends | [v4/sns/friend_delete](https://intl.cloud.tencent.com/document/product/1047/34905) |
| Deleting all friends | [v4/sns/friend_delete_all](https://intl.cloud.tencent.com/document/product/1047/34906) |
| Verifying friends | [v4/sns/friend_check](https://intl.cloud.tencent.com/document/product/1047/34907) |
| Pulling friends | [v4/sns/friend_get](https://intl.cloud.tencent.com/document/product/1047/34908) |
| Pulling specific friends | [v4/sns/friend_get_list](https://intl.cloud.tencent.com/document/product/1047/34910) |
| Adding a blacklist | [v4/sns/black_list_add](https://intl.cloud.tencent.com/document/product/1047/34911) |
| Deleting a blacklist | [v4/sns/black_list_delete](https://intl.cloud.tencent.com/document/product/1047/34912) |
| Pulling a blacklist | [v4/sns/black_list_get](https://intl.cloud.tencent.com/document/product/1047/34914) |
| Verifying a blacklist | [v4/sns/black_list_check](https://intl.cloud.tencent.com/document/product/1047/34913) |
| Adding a list | [v4/sns/group_add](https://intl.cloud.tencent.com/document/product/1047/34950) |
| Deleting a list | [v4/sns/group_delete](https://intl.cloud.tencent.com/document/product/1047/34926) |



## Group Management

| Feature Description | API |
| ---------------------- | ------------------------------------------------------------ |
| Obtaining all groups in an app | [v4/group_open_http_svc/get_appid_group_list](https://intl.cloud.tencent.com/document/product/1047/34960) |
| Creating a group | [v4/group_open_http_svc/create_group](https://intl.cloud.tencent.com/document/product/1047/34895) |
| Obtaining detailed group profiles | [v4/group_open_http_svc/get_group_info](https://intl.cloud.tencent.com/document/product/1047/34961) |
| Obtaining detailed member profiles of a group | [v4/group_open_http_svc/get_group_member_info](https://intl.cloud.tencent.com/document/product/1047/34948) |
| Modifying basic group profiles | [v4/group_open_http_svc/modify_group_base_info](https://intl.cloud.tencent.com/document/product/1047/34962) |
| Adding group members | [v4/group_open_http_svc/add_group_member](https://intl.cloud.tencent.com/document/product/1047/34921) |
| Deleting group members | [v4/group_open_http_svc/delete_group_member](https://intl.cloud.tencent.com/document/product/1047/34949) |
| Modifying the profiles of group members | [v4/group_open_http_svc/modify_group_member_info](https://intl.cloud.tencent.com/document/product/1047/34900) |
| Disbanding groups | [v4/group_open_http_svc/destroy_group ](https://intl.cloud.tencent.com/document/product/1047/34896) |
| Obtaining the groups that a user has joined | [v4/group_open_http_svc/get_joined_group_list](https://intl.cloud.tencent.com/document/product/1047/34925) |
| Querying the identity of a user in a group | [v4/group_open_http_svc/get_role_in_group](https://intl.cloud.tencent.com/document/product/1047/34963) |
| Batch muting and unmuting | [v4/group_open_http_svc/forbid_send_msg](https://intl.cloud.tencent.com/document/product/1047/34951) |
| Obtaining muted users in a group | [v4/group_open_http_svc/get_group_shutted_uin](https://intl.cloud.tencent.com/document/product/1047/34964) |
| Sending common messages in a group | [v4/group_open_http_svc/send_group_msg](https://intl.cloud.tencent.com/document/product/1047/34959) |
| Sending system notifications in a group | [v4/group_open_http_svc/send_group_system_notification](https://intl.cloud.tencent.com/document/product/1047/34958) |
| Recalling messages in a group | [v4/group_open_http_svc/group_msg_recall](https://intl.cloud.tencent.com/document/product/1047/34965) |
| Transferring the ownership of a group | [v4/group_open_http_svc/change_group_owner](https://intl.cloud.tencent.com/document/product/1047/34966) |
| Importing basic group profiles | [v4/group_open_http_svc/import_group](https://intl.cloud.tencent.com/document/product/1047/34967) |
| Importing group messages | [v4/group_open_http_svc/import_group_msg ](https://intl.cloud.tencent.com/document/product/1047/34968) |
| Importing group members | [v4/group_open_http_svc/import_group_member](https://intl.cloud.tencent.com/document/product/1047/34969) |
| Configuring unread message counts | [v4/group_open_http_svc/set_unread_msg_num](https://intl.cloud.tencent.com/document/product/1047/34909) |
| Deleting messages sent by the specified user | [v4/group_open_http_svc/delete_group_msg_by_sender](https://intl.cloud.tencent.com/document/product/1047/34970) |
| Pulling roaming group messages | [v4/group_open_http_svc/group_msg_get_simple](https://intl.cloud.tencent.com/document/product/1047/34971) |


## Global Mute Management
| Feature Description | API |
|---------|---------|
| Configuring global mute |[ v4/openconfigsvr/setnospeaking](https://intl.cloud.tencent.com/document/product/1047/34923) |
| Querying global mute |[ v4/openconfigsvr/getnospeaking](https://intl.cloud.tencent.com/document/product/1047/34924) |



## Operation Management

| Feature Description | API |
|---------|---------|
| Downloading message history |[v4/open_msg_svc/get_history](https://intl.cloud.tencent.com/document/product/1047/34885) |
| Pulling operation data |[v4/openconfigsvr/getappinfo](https://intl.cloud.tencent.com/document/product/1047/34886) |
