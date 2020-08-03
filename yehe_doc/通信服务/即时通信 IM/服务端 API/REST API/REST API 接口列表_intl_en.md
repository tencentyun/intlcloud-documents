## Account Management

| Feature Description | API |
|---------|---------|
| Import an account. | [v4/im_open_login_svc/account_import](https://intl.cloud.tencent.com/document/product/1047/34953) |
| Batch import accounts. | [v4/im_open_login_svc/multiaccount_import](https://intl.cloud.tencent.com/document/product/1047/34954) |
| Delete accounts. | [v4/im_open_login_svc/account_delete](https://intl.cloud.tencent.com/document/product/1047/34955) |
| Check accounts. | [v4/im_open_login_svc/account_check](https://intl.cloud.tencent.com/document/product/1047/34956) |
| Invalidate the login status of an account. | [v4/im_open_login_svc/kick](https://intl.cloud.tencent.com/document/product/1047/34957) |
| Query the login status of an account. | [v4/openim/querystate](https://intl.cloud.tencent.com/document/product/1047/35477) |

## One-to-one Message

| Feature Description | API |
|---------|---------|
| Send a one-to-one message. | [v4/openim/sendmsg](https://intl.cloud.tencent.com/document/product/1047/34919) |
| Batch send one-to-one messages. | [v4/openim/batchsendmsg](https://intl.cloud.tencent.com/document/product/1047/34920) |
| Import one-to-one messages. | [v4/openim/importmsg](https://intl.cloud.tencent.com/document/product/1047/35014) |
| Query one-to-one messages. | [v4/openim/admin_getroammsg](https://intl.cloud.tencent.com/document/product/1047/35478) |
| Recall one-to-one messages. | [v4/openim/admin_msgwithdraw](https://intl.cloud.tencent.com/document/product/1047/35015) |


## Push Notifications

| Feature Description | API |
|---------|---------|
| Push to All Users        | [v4/all_member_push/im_push](https://intl.cloud.tencent.com/document/product/1047/37166) |
| Set App Attribute Names | [v4/all_member_push/im_set_attr_name](https://intl.cloud.tencent.com/document/product/1047/37167) |
| Obtain App Attribute Names | [v4/all_member_push/im_get_attr_name](https://intl.cloud.tencent.com/document/product/1047/37168) |
| Obtain User Attributes     | [v4/all_member_push/im_get_attr](https://intl.cloud.tencent.com/document/product/1047/37169) |
| Set User Attributes     | [v4/all_member_push/im_set_attr](https://intl.cloud.tencent.com/document/product/1047/37170) |
| Delete User Attributes     | [v4/all_member_push/im_remove_attr](https://intl.cloud.tencent.com/document/product/1047/37171) |
| Obtain User Tags     | [v4/all_member_push/im_get_tag](https://intl.cloud.tencent.com/document/product/1047/37172) |
| Add User Tags     | [v4/all_member_push/im_add_tag](https://intl.cloud.tencent.com/document/product/1047/37173) |
| Delete User Tags     | [v4/all_member_push/im_remove_tag](https://intl.cloud.tencent.com/document/product/1047/37174) |
| Delete All Tags of a User | [v4/all_member_push/im_remove_all_tags](https://intl.cloud.tencent.com/document/product/1047/37175) |

## Profile Management

| Feature Description | API |
| -------- | ------------------------------------------------------------ |
| Configure profiles. | [v4/profile/portrait_set](https://intl.cloud.tencent.com/document/product/1047/34916) |
| Pull profiles. | [v4/profile/portrait_get](https://intl.cloud.tencent.com/document/product/1047/34917) |

## Relationship Chain Management

| Feature Description | API |
| -------- | ------------------------------------------------------------ |
| Add friends. | [v4/sns/friend_add](https://intl.cloud.tencent.com/document/product/1047/34902) |
| Import friends. | [v4/sns/friend_import](https://intl.cloud.tencent.com/document/product/1047/34903) |
| Delete friends. | [v4/sns/friend_delete](https://intl.cloud.tencent.com/document/product/1047/34905) |
| Delete all friends. | [v4/sns/friend_delete_all](https://intl.cloud.tencent.com/document/product/1047/34906) |
| Verify friends. | [v4/sns/friend_check](https://intl.cloud.tencent.com/document/product/1047/34907) |
| Pull friends. | [v4/sns/friend_get](https://intl.cloud.tencent.com/document/product/1047/34908) |
| Pull specific friends. | [v4/sns/friend_get_list](https://intl.cloud.tencent.com/document/product/1047/34910) |
| Add users to blocklist. | [v4/sns/black_list_add](https://intl.cloud.tencent.com/document/product/1047/34911) |
| Remove users from blocklist. | [v4/sns/black_list_delete](https://intl.cloud.tencent.com/document/product/1047/34912) |
| Pull a blocklist. | [v4/sns/black_list_get](https://intl.cloud.tencent.com/document/product/1047/34914) |
| Verify a blocklist. | [v4/sns/black_list_check](https://intl.cloud.tencent.com/document/product/1047/34913) |
| Add a list. | [v4/sns/group_add](https://intl.cloud.tencent.com/document/product/1047/34950) |
| Delete a list. | [v4/sns/group_delete](https://intl.cloud.tencent.com/document/product/1047/34926) |



## Group Management

| Feature Description | API |
| ---------------------- | ------------------------------------------------------------ |
| Create a group. | [v4/group_open_http_svc/create_group](https://intl.cloud.tencent.com/document/product/1047/34895) |
| Obtain detailed group profiles. | [v4/group_open_http_svc/get_group_info](https://intl.cloud.tencent.com/document/product/1047/34961) |
| Obtain detailed group member profiles. | [v4/group_open_http_svc/get_group_member_info](https://intl.cloud.tencent.com/document/product/1047/34948) |
| Modify basic group profiles. | [v4/group_open_http_svc/modify_group_base_info](https://intl.cloud.tencent.com/document/product/1047/34962) |
| Add group members. | [v4/group_open_http_svc/add_group_member](https://intl.cloud.tencent.com/document/product/1047/34921) |
| Delete group members. | [v4/group_open_http_svc/delete_group_member](https://intl.cloud.tencent.com/document/product/1047/34949) |
| Modify group member profiles. | [v4/group_open_http_svc/modify_group_member_info](https://intl.cloud.tencent.com/document/product/1047/34900) |
| Disband groups. | [v4/group_open_http_svc/destroy_group ](https://intl.cloud.tencent.com/document/product/1047/34896) |
| Obtain the groups a user has joined. | [v4/group_open_http_svc/get_joined_group_list](https://intl.cloud.tencent.com/document/product/1047/34925) |
| Query the identity of a user in a group. | [v4/group_open_http_svc/get_role_in_group](https://intl.cloud.tencent.com/document/product/1047/34963) |
| Mute and unmute group members. | [v4/group_open_http_svc/forbid_send_msg](https://intl.cloud.tencent.com/document/product/1047/34951) |
| Obtain muted users in a group. | [v4/group_open_http_svc/get_group_shutted_uin](https://intl.cloud.tencent.com/document/product/1047/34964) |
| Send ordinary messages in a group. | [v4/group_open_http_svc/send_group_msg](https://intl.cloud.tencent.com/document/product/1047/34959) |
| Send system messages in a group. | [v4/group_open_http_svc/send_group_system_notification](https://intl.cloud.tencent.com/document/product/1047/34958) |
| Recall group messages. | [v4/group_open_http_svc/group_msg_recall](https://intl.cloud.tencent.com/document/product/1047/34965) |
| Transfer a group. | [v4/group_open_http_svc/change_group_owner](https://intl.cloud.tencent.com/document/product/1047/34966) |
| Import basic group profiles. | [v4/group_open_http_svc/import_group](https://intl.cloud.tencent.com/document/product/1047/34967) |
| Import group messages. | [v4/group_open_http_svc/import_group_msg ](https://intl.cloud.tencent.com/document/product/1047/34968) |
| Import group members. | [v4/group_open_http_svc/import_group_member](https://intl.cloud.tencent.com/document/product/1047/34969) |
| Configure unread message counts. | [v4/group_open_http_svc/set_unread_msg_num](https://intl.cloud.tencent.com/document/product/1047/34909) |
| Delete messages sent by the specified user. | [v4/group_open_http_svc/delete_group_msg_by_sender](https://intl.cloud.tencent.com/document/product/1047/34970) |
| Pull roaming group messages. | [v4/group_open_http_svc/group_msg_get_simple](https://intl.cloud.tencent.com/document/product/1047/34971) |


## Global Mute Management
| Feature Description | API |
|---------|---------|
| Configure global mute. | [v4/openconfigsvr/setnospeaking](https://intl.cloud.tencent.com/document/product/1047/34923) |
| Query global mute. | [v4/openconfigsvr/getnospeaking](https://intl.cloud.tencent.com/document/product/1047/34924) |



## Operations Management

| Feature Description | API |
|---------|---------|
| Download message history. | [v4/open_msg_svc/get_history](https://intl.cloud.tencent.com/document/product/1047/34885) |
| Pull operations data. | [v4/openconfigsvr/getappinfo](https://intl.cloud.tencent.com/document/product/1047/34886) |
| Obtain Server IP Addresses  |[v4/ConfigSvc/GetIPList](https://intl.cloud.tencent.com/document/product/1047/36742) |
