## Account Management

| Feature Description | API |
|---------|---------|
| Import an account | [v4/im_open_login_svc/account_import](https://intl.cloud.tencent.com/document/product/1047/34953) |
| Import multiple accounts | [v4/im_open_login_svc/multiaccount_import](https://intl.cloud.tencent.com/document/product/1047/34954) |
| Delete accounts | [v4/im_open_login_svc/account_delete](https://intl.cloud.tencent.com/document/product/1047/34955) |
| Query accounts | [v4/im_open_login_svc/account_check](https://intl.cloud.tencent.com/document/product/1047/34956) | 
| Invalidate the login status of an account | [v4/im_open_login_svc/kick](https://intl.cloud.tencent.com/document/product/1047/34957) |
| Query the login status of an account | [ v4/openim/querystate](https://intl.cloud.tencent.com/document/product/1047/35477) |

## One-to-one Chat Messages

| Feature Description | API |
|---------|---------|
| Send a one-to-one chat message | [v4/openim/sendmsg](https://intl.cloud.tencent.com/document/product/1047/34919) |
| Batch send one-to-one chat messages | [v4/openim/batchsendmsg](https://intl.cloud.tencent.com/document/product/1047/34920) |
| Import one-to-one chat messages | [v4/openim/importmsg](https://intl.cloud.tencent.com/document/product/1047/35014) |
| Query one-to-one chat messages | [v4/openim/admin_getroammsg](https://intl.cloud.tencent.com/document/product/1047/35478) |
| Recalls one-to-one chat messages | [v4/openim/admin_msgwithdraw](https://intl.cloud.tencent.com/document/product/1047/35015) |



## Profile Management

| Feature Description | API |
| -------- | ------------------------------------------------------------ |
| Configure profiles | [v4/profile/portrait_set](https://intl.cloud.tencent.com/document/product/1047/34916) |
| Pulls profiles | [v4/profile/portrait_get](https://intl.cloud.tencent.com/document/product/1047/34917) |

## Relationship Chain Management

| Feature Description | API |
| -------- | ------------------------------------------------------------ |
| Add friends | [v4/sns/friend_add](https://intl.cloud.tencent.com/document/product/1047/34902) |
| Import friends | [v4/sns/friend_import](https://intl.cloud.tencent.com/document/product/1047/34903) |
| Update friends | [v4/sns/friend_update](https://intl.cloud.tencent.com/document/product/1047/34904) |
| Delete friends | [v4/sns/friend_delete](https://intl.cloud.tencent.com/document/product/1047/34905) |
| Delete all friends | [v4/sns/friend_delete_all](https://intl.cloud.tencent.com/document/product/1047/34906) |
| Verify friends | [v4/sns/friend_check](https://intl.cloud.tencent.com/document/product/1047/34907) |
| Pull friends | [v4/sns/friend_get](https://intl.cloud.tencent.com/document/product/1047/34908) |
| Pull specific friends | [v4/sns/friend_get_list](https://intl.cloud.tencent.com/document/product/1047/34910) |
| Add a blacklist | [v4/sns/black_list_add](https://intl.cloud.tencent.com/document/product/1047/34911) |
| Delete a blacklist | [v4/sns/black_list_delete](https://intl.cloud.tencent.com/document/product/1047/34912) |
| Pull a blacklist | [v4/sns/black_list_get](https://intl.cloud.tencent.com/document/product/1047/34914) |
| Verify a blacklist | [v4/sns/black_list_check](https://intl.cloud.tencent.com/document/product/1047/34913) |
| Add a list | [v4/sns/group_add](https://intl.cloud.tencent.com/document/product/1047/34950) |
| Delete a list | [v4/sns/group_delete](https://intl.cloud.tencent.com/document/product/1047/34926) |



## Group Management

| Feature Description | API |
| ---------------------- | ------------------------------------------------------------ |
| Create a group | [v4/group_open_http_svc/create_group](https://intl.cloud.tencent.com/document/product/1047/34895) |
| Obtain detailed group profiles | [v4/group_open_http_svc/get_group_info](https://intl.cloud.tencent.com/document/product/1047/34961) |
| Obtain detailed member information of a group | [v4/group_open_http_svc/get_group_member_info](https://intl.cloud.tencent.com/document/product/1047/34948) |
| Modify basic group information | [v4/group_open_http_svc/modify_group_base_info](https://intl.cloud.tencent.com/document/product/1047/34962) |
| Add group members | [v4/group_open_http_svc/add_group_member](https://intl.cloud.tencent.com/document/product/1047/34921) |
| Delete group members | [v4/group_open_http_svc/delete_group_member](https://intl.cloud.tencent.com/document/product/1047/34949) |
| Modify the profiles of group members | [v4/group_open_http_svc/modify_group_member_info](https://intl.cloud.tencent.com/document/product/1047/34900) |
| Disband groups | [v4/group_open_http_svc/destroy_group ](https://intl.cloud.tencent.com/document/product/1047/34896) |
| Obtain the groups a user has joined | [v4/group_open_http_svc/get_joined_group_list](https://intl.cloud.tencent.com/document/product/1047/34925) |
| Query the identity of a user in a group | [v4/group_open_http_svc/get_role_in_group](https://intl.cloud.tencent.com/document/product/1047/34963) |
| Batch mute and unmute group members | [v4/group_open_http_svc/forbid_send_msg](https://intl.cloud.tencent.com/document/product/1047/34951) |
| Obtain muted users in a group | [v4/group_open_http_svc/get_group_shutted_uin](https://intl.cloud.tencent.com/document/product/1047/34964) |
| Send ordinary messages in a group | [v4/group_open_http_svc/send_group_msg](https://intl.cloud.tencent.com/document/product/1047/34959) |
| Send system messages in a group | [v4/group_open_http_svc/send_group_system_notification](https://intl.cloud.tencent.com/document/product/1047/34958) |
| Recall messages in a group | [v4/group_open_http_svc/group_msg_recall](https://intl.cloud.tencent.com/document/product/1047/34965) |
| Transfer the ownership of a group | [v4/group_open_http_svc/change_group_owner](https://intl.cloud.tencent.com/document/product/1047/34966) |
| Import basic group information | [v4/group_open_http_svc/import_group](https://intl.cloud.tencent.com/document/product/1047/34967) |
| Import group messages | [v4/group_open_http_svc/import_group_msg ](https://intl.cloud.tencent.com/document/product/1047/34968) |
| Import group members | [v4/group_open_http_svc/import_group_member](https://intl.cloud.tencent.com/document/product/1047/34969) |
| Configure unread message counts | [v4/group_open_http_svc/set_unread_msg_num](https://intl.cloud.tencent.com/document/product/1047/34909) |
| Delete messages sent by the specified user | [v4/group_open_http_svc/delete_group_msg_by_sender](https://intl.cloud.tencent.com/document/product/1047/34970) |
| Pull roaming group messages | [v4/group_open_http_svc/group_msg_get_simple](https://intl.cloud.tencent.com/document/product/1047/34971) |


## Global Muting Management
| Feature Description | API |
|---------|---------|
| Configure global muting |[ v4/openconfigsvr/setnospeaking](https://intl.cloud.tencent.com/document/product/1047/34923) |
| Query global muting |[ v4/openconfigsvr/getnospeaking](https://intl.cloud.tencent.com/document/product/1047/34924) |



## Operational Management

| Feature Description | API |
|---------|---------|
| Pull operational data | [v4/openconfigsvr/getappinfo](https://intl.cloud.tencent.com/document/product/1047/34886) |
| Download the message history | [v4/open_msg_svc/get_history](https://intl.cloud.tencent.com/document/product/1047/34885) |
