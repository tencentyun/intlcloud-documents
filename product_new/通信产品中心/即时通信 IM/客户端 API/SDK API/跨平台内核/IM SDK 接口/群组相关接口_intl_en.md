For information on groups, see [Group Systems](https://intl.cloud.tencent.com/document/product/1047/33529), [Group Management](https://intl.cloud.tencent.com/document/product/1047/33530), and [Group Custom Fields](https://intl.cloud.tencent.com/document/product/1047/33529#.E8.87.AA.E5.AE.9A.E4.B9.89.E5.AD.97.E6.AE.B5).

## TIMGroupCreate

This API is used to create a group.

**Prototype**

```c
TIM_DECL int TIMGroupCreate(const char* json_group_create_param, TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| json_group_create_param | const char\* | The JSON parameter string of the API for creating a group. |
| cb | TIMCommCallback | The callback for notifying whether creating the group succeeded or failed. For the definition of the callback function and the description of parameter parsing, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550#timcommcallback). |
| user_data | const void\* | User-defined data. The IM SDK is only responsible for returning the user data to the callback function cb without processing the data. |

**Returned values**

| Type | Description |
|-----|-----|
| int | If TIM_SUCC is returned, the API was called successfully (the callback will be called only when the API returns TIM_SUCC.) If other values are returned, the API failed to be called. For the definition of each returned value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551#timresult). |

>
- You can specify a group ID when creating a group. If no group ID is specified, the IM CVM generates a unique ID to facilitate subsequent operations. The group ID is returned by the callback that is passed in during the group creation.
- For details on JSON Keys for group creation parameters, see [CreateGroupParam](https://intl.cloud.tencent.com/document/product/1047/34551#creategroupparam).


**Example**

```c
Json::Value json_group_member_array(Json::arrayValue);

Json::Value json_value_param;
json_value_param[kTIMCreateGroupParamGroupId] = "first group id";
json_value_param[kTIMCreateGroupParamGroupType] = kTIMGroup_Public;
json_value_param[kTIMCreateGroupParamGroupName] = "first group name";
json_value_param[kTIMCreateGroupParamGroupMemberArray] = json_group_member_array;

json_value_param[kTIMCreateGroupParamNotification] = "group notification";
json_value_param[kTIMCreateGroupParamIntroduction] = "group introduction";
json_value_param[kTIMCreateGroupParamFaceUrl] = "group face url";
json_value_param[kTIMCreateGroupParamMaxMemberCount] = 2000;
json_value_param[kTIMCreateGroupParamAddOption] = kTIMGroupAddOpt_Any;

const void* user_data = nullptr; // Returns by the callback function.
int ret = TIMGroupCreate(json_value_param.toStyledString().c_str(), [](int32_t code, const char* desc, const char* json_params, const void* user_data) {
   if (ERR_SUCC != code) { 
        // Failed to create the group.
        return;
    }
    
    // The group has been created successfully. Meanwhile, the returned JSON result is parsed to extract the resulting GroupID.
}, user_data);
if (TIM_SUCC != ret) {
    // Failed to call the TIMGroupCreate API.
}

// The json_group_create_param JSON string obtained by json_value_param.toStyledString().c_str() is as follows:
{
   "create_group_param_add_option" : 2,
   "create_group_param_face_url" : "group face url",
   "create_group_param_group_id" : "first group id",
   "create_group_param_group_member_array" : [],
   "create_group_param_group_name" : "first group name",
   "create_group_param_group_type" : 0,
   "create_group_param_introduction" : "group introduction",
   "create_group_param_max_member_num" : 2000,
   "create_group_param_notification" : "group notification"
}
```


## TIMGroupDelete

This API is used to delete (or dismiss) a group.

**Prototype**

```c
TIM_DECL int TIMGroupDelete(const char* group_id, TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| group_id | const char\* | The ID of the group to be deleted. |
| cb | TIMCommCallback | The callback for notifying whether deleting the group succeeded or failed. For the definition of the callback function, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550#timcommcallback). |
| user_data | const void\* | User-defined data. The IM SDK is only responsible for returning the user data to the callback function cb without processing the data. |

**Returned values**

| Type | Description |
|-----|-----|
| int | If TIM_SUCC is returned, the API was called successfully (the callback will be called only when the API returns TIM_SUCC.) If other values are returned, the API failed to be called. For the definition of each returned value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551#timresult). |

>
- Description of permissions:
 - For a Private group, nobody has the permission to dismiss the group.
 - For a Public, ChatRoom, or BChatRoom group, the group owner can dismiss the group.
- When the API is called to delete a group with the specified group_id, whether the group was deleted successfully can be determined based on the parameters of the cb callback function.


## TIMGroupJoin

This API is used to submit an application for joining a group.

**Prototype**

```c
TIM_DECL int TIMGroupJoin(const char* group_id, const char* hello_msg, TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| group_id | const char\* | The ID of the group to be joined. |
| hello_msg | const char\* | (Optional) The application reason. |
| cb | TIMCommCallback | The callback for notifying whether applying to join the group succeeded or failed. For the definition of the callback function, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550#timcommcallback). |
| user_data | const void\* | User-defined data. The IM SDK is only responsible for returning the user data to the callback function cb without processing the data. |

**Returned values**

| Type | Description |
|-----|-----|
| int | If TIM_SUCC is returned, the API was called successfully (the callback will be called only when the API returns TIM_SUCC.) If other values are returned, the API failed to be called. For the definition of each returned value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551#timresult). |

>
- Description of permissions:
 - For a Private group, a user cannot actively apply to join the group.
 - For a Public or ChatRoom group, a user can actively apply to join the group.
 If approval is required according to the group configuration, after the application is submitted, the admin and group owner will receive a system message concerning the application. Then, the admin or group owner needs to approve the application. If all users are allowed to join the group according to the group configuration, the applicant can directly join the group. For a BChatRoom group, anyone can join the group freely.
- When the API is called to submit an application to join a group with the specified group_id, whether the application was submitted successfully can be determined based on the parameters of the cb callback function.


## TIMGroupQuit

This API is used to quit a group.

**Prototype**

```c
TIM_DECL int TIMGroupQuit(const char* group_id, TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| group_id | const char\* | The ID of the group to be quit. |
| cb | TIMCommCallback | The callback for notifying whether quitting the group succeeded or failed. For the definition of the callback function, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550#timcommcallback). |
| user_data | const void\* | User-defined data. The IM SDK is only responsible for returning the user data to the callback function cb without processing the data. |

**Returned values**

| Type | Description |
|-----|-----|
| int | If TIM_SUCC is returned, the API was called successfully (the callback will be called only when the API returns TIM_SUCC.) If other values are returned, the API failed to be called. For the definition of each returned value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551#timresult). |

>
- Description of permissions:
 - For a Private group, all members can quit the group.
 - For a Public, ChatRoom, or BChatRoom group, the group owner cannot quit the group.
- When the API is called to quit a group with the specified group_id, whether the user successfully quit the group can be determined based on the parameters of the cb callback function.


## TIMGroupInviteMember

This API is used to invite a user to a group.

**Prototype**

```c
TIM_DECL int TIMGroupInviteMember(const char* json_group_invite_param, TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| json_group_invite_param | const char\* | The JSON parameter string of the API for inviting a user to a group. |
| cb | TIMCommCallback | The callback for notifying whether inviting the user to the group succeeded or failed. For the definition of the callback function and the description of parameter parsing, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550#timcommcallback). |
| user_data | const void\* | User-defined data. The IM SDK is only responsible for returning the user data to the callback function cb without processing the data. |

**Returned values**

| Type | Description |
|-----|-----|
| int | If TIM_SUCC is returned, the API was called successfully (the callback will be called only when the API returns TIM_SUCC.) If other values are returned, the API failed to be called. For the definition of each returned value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551#timresult). |

>
- Description of permissions:
 - Users can be added only to a Private group.
 - Users can be invited to a Public or ChatRoom group.
 - Users cannot be invited to a BChatRoom group without their agreement.
- You can use this API to invite multiple users to a group. For details on JSON Keys for invitation parameters, see [GroupInviteMemberParam](https://intl.cloud.tencent.com/document/product/1047/34551#groupinvitememberparam).


**Example**

```c
Json::Value json_value_invite;
json_value_invite[kTIMGroupInviteMemberParamGroupId] = groupid;
json_value_invite[kTIMGroupInviteMemberParamUserData] = "userdata";
json_value_invite[kTIMGroupInviteMemberParamIdentifierArray].append("user1");
json_value_invite[kTIMGroupInviteMemberParamIdentifierArray].append("user2");

const void* user_data = nullptr; // Returns by the callback function.
int ret = TIMGroupInviteMember(json_value_invite.toStyledString().c_str(), [](int32_t code, const char* desc, const char* json_params, const void* user_data) {
    if (ERR_SUCC != code) { 
        // Failed to invite the users to the group.
        return;
    }
    // Successfully invited the users to the group. Meanwhile, the returned JSON result is parsed to extract the invitation result for each user.
}, user_data);
if (TIM_SUCC != ret) {
    // Failed to call the TIMGroupInviteMember API.
}

// The json_group_invite_param JSON string obtained by json_value_invite.toStyledString().c_str() is as follows:
{
   "group_invite_member_param_group_id" : "first group id",
   "group_invite_member_param_identifier_array" : [ "user1", "user2" ],
   "group_invite_member_param_user_data" : "userdata"
}
```


## TIMGroupDeleteMember

This API is used to delete a member from a group.

**Prototype**

```c
TIM_DECL int TIMGroupDeleteMember(const char* json_group_delete_param, TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| json_group_delete_param | const char\* | The JSON parameter string of the API for deleting a group member. |
| cb | TIMCommCallback | The callback for notifying whether deleting the group member succeeded or failed. For the definition of the callback function and the description of parameter parsing, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550#timcommcallback). |
| user_data | const void\* | User-defined data. The IM SDK is only responsible for returning the user data to the callback function cb without processing the data. |

**Returned values**

| Type | Description |
|-----|-----|
| int | If TIM_SUCC is returned, the API was called successfully (the callback will be called only when the API returns TIM_SUCC.) If other values are returned, the API failed to be called. For the definition of each returned value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551#timresult). |

>
- Description of permissions:
 - For a Private group, only the group creator can delete group members.
 - For a Public or ChatRoom group, only the admin and group owner can delete group members.
 - For a BChatRoom group, no group members can be deleted.
- You can use this API to delete multiple group members. For details on JSON Keys for member deletion parameters, see [GroupDeleteMemberParam](https://intl.cloud.tencent.com/document/product/1047/34551#groupdeletememberparam).


**Example**

```c
Json::Value json_value_delete;
json_value_delete[kTIMGroupDeleteMemberParamGroupId] = groupid;
json_value_delete[kTIMGroupDeleteMemberParamUserData] = "reason";
json_value_delete[kTIMGroupDeleteMemberParamIdentifierArray].append("user1");
json_value_delete[kTIMGroupDeleteMemberParamIdentifierArray].append("user2");

int ret = TIMGroupDeleteMember(json_value_delete.toStyledString().c_str(), [](int32_t code, const char* desc, const char* json_params, const void* user_data) {
      
}, this));

// The json_group_delete_param JSON string obtained by json_value_delete.toStyledString().c_str() is as follows:
{
  "group_delete_member_param_group_id" : "third group id",
  "group_delete_member_param_identifier_array" : [ "user2", "user3" ],
  "group_delete_member_param_user_data" : "reason"
}
```


## TIMGroupGetJoinedGroupList

This API is used to obtain the list of groups a user has joined.

**Prototype**

```c
TIM_DECL int TIMGroupGetJoinedGroupList(TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| cb | TIMCommCallback | The callback for notifying whether obtaining the list of groups the user has joined succeeded or failed. For the definition of the callback function and the description of parameter parsing, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550#timcommcallback). |
| user_data | const void\* | User-defined data. The IM SDK is only responsible for returning the user data to the callback function cb without processing the data. |

**Returned values**

| Type | Description |
|-----|-----|
| int | If TIM_SUCC is returned, the API was called successfully (the callback will be called only when the API returns TIM_SUCC.) If other values are returned, the API failed to be called. For the definition of each returned value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551#timresult). |

>
- Description of permissions:
 - You can use this API to obtain the list of groups you have joined.
 - This API can only obtain the list of BChatRoom groups that a user has joined.
- This API is used to obtain the list of groups that the current user has joined, and returns the basic information of the groups. For details on the returned basic group information fields, see [GroupBaseInfo](https://intl.cloud.tencent.com/document/product/1047/34551#groupbaseinfo).


## TIMGroupGetGroupInfoList

This API is used to obtain the list of group information.

**Prototype**

```c
TIM_DECL int TIMGroupGetGroupInfoList(const char* json_group_getinfo_param, TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| json_group_getinfo_param | const char\* | The JSON parameter string of the API for obtaining the group information list. |
| cb | TIMCommCallback | The callback for notifying whether obtaining the group information list succeeded or failed. For the definition of the callback function and the description of parameter parsing, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550#timcommcallback). |
| user_data | const void\* | User-defined data. The IM SDK is only responsible for returning the user data to the callback function cb without processing the data. |

**Returned values**

| Type | Description |
|-----|-----|
| int | If TIM_SUCC is returned, the API was called successfully (the callback will be called only when the API returns TIM_SUCC.) If other values are returned, the API failed to be called. For the definition of each returned value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551#timresult). |

> This API is used to obtain the details of the groups in the specified group ID list. For details on the returned detailed group information fields, see [GroupDetailInfo](https://intl.cloud.tencent.com/document/product/1047/34551#groupdetailinfo).


**Example**

```c
Json::Value groupids;
groupids.append("third group id");
groupids.append("second group id");
groupids.append("first group id");
int ret = TIMGroupGetGroupInfoList(groupids.toStyledString().c_str(), [](int32_t code, const char* desc, const char* json_param, const void* user_data) {

}, this);

// The json_group_getinfo_param string obtained by groupids.toStyledString().c_str() is as follows:
[ "third group id", "second group id", "first group id" ]
```


## TIMGroupModifyGroupInfo

This API is used to modify the information of a group.

**Prototype**

```c
TIM_DECL int TIMGroupModifyGroupInfo(const char* json_group_modifyinfo_param, TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| json_group_modifyinfo_param | const char\* | The JSON parameter string of the API for modifying group information. |
| cb | TIMCommCallback | The callback for notifying whether modifying the group information succeeded or failed. For the definition of the callback function, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550#timcommcallback). |
| user_data | const void\* | User-defined data. The IM SDK is only responsible for returning the user data to the callback function cb without processing the data. |

**Returned values**

| Type | Description |
|-----|-----|
| int | If TIM_SUCC is returned, the API was called successfully (the callback will be called only when the API returns TIM_SUCC.) If other values are returned, the API failed to be called. For the definition of each returned value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551#timresult). |

>
- Description of permissions for modifying the group owner (group ownership transfer):
 - Only the group owner has the permission to transfer the group ownership.
 - The ownership of a BChatRoom group cannot be transferred.
- Description of permissions for modifying other group information:
 - For a Public, ChatRoom, or BChatRoom group, only the group owner or admin can modify the group introduction.
 - For a Private group, anyone can modify the group introduction.
- `kTIMGroupModifyInfoParamModifyFlag` can be set by bit or set to multiple values. Different flags are used to set different keys. For details, see [GroupModifyInfoParam](https://intl.cloud.tencent.com/document/product/1047/34551#groupmodifyinfoparam).


**Example 1: setting the group owner**

```c
Json::Value json_value_modifygroupinfo;
json_value_modifygroupinfo[kTIMGroupModifyInfoParamGroupId] = "first group id";
json_value_modifygroupinfo[kTIMGroupModifyInfoParamModifyFlag] = kTIMGroupModifyInfoFlag_Owner;
json_value_modifygroupinfo[kTIMGroupModifyInfoParamOwner] = "user2";

int ret = TIMGroupModifyGroupInfo(json_value_modifygroupinfo.toStyledString().c_str(), [](int32_t code, const char* desc, const char* json_param, const void* user_data) {

}, nullptr);

// The json_group_modifyinfo_param JSON string obtained by json_value_modifygroupinfo.toStyledString().c_str() is as follows:
{
  "group_modify_info_param_group_id" : "first group id",
  "group_modify_info_param_modify_flag" : -2147483648,
  "group_modify_info_param_owner" : "user2"
}
```


**Example 2: setting the group name and group notification**

```c
Json::Value json_value_modifygroupinfo;
json_value_modifygroupinfo[kTIMGroupModifyInfoParamGroupId] = "first group id";
json_value_modifygroupinfo[kTIMGroupModifyInfoParamModifyFlag] = kTIMGroupModifyInfoFlag_Name | kTIMGroupModifyInfoFlag_Notification;
json_value_modifygroupinfo[kTIMGroupModifyInfoParamGroupName] = "first group name to other name";
json_value_modifygroupinfo[kTIMGroupModifyInfoParamNotification] = "first group notification";

int ret = TIMGroupModifyGroupInfo(json_value_modifygroupinfo.toStyledString().c_str(), [](int32_t code, const char* desc, const char* json_param, const void* user_data) {

}, nullptr);

// The json_group_modifyinfo_param JSON string obtained by json_value_modifygroupinfo.toStyledString().c_str() is as follows:
{
   "group_modify_info_param_group_id" : "first group id",
   "group_modify_info_param_group_name" : "first group name to other name",
   "group_modify_info_param_modify_flag" : 3,
   "group_modify_info_param_notification" : "first group notification"
}
```


## TIMGroupGetMemberInfoList

This API is used to obtain the group member information list.

**Prototype**

```c
TIM_DECL int TIMGroupGetMemberInfoList(const char* json_group_getmeminfos_param, TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| json_group_getinfo_param | const char\* | The JSON parameter string of the API for obtaining the group member information list. |
| cb | TIMCommCallback | The callback for notifying whether obtaining the group member information list succeeded or failed. For the definition of the callback function and the description of parameter parsing, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550#timcommcallback). |
| user_data | const void\* | User-defined data. The IM SDK is only responsible for returning the user data to the callback function cb without processing the data. |

**Returned values**

| Type | Description |
|-----|-----|
| int | If TIM_SUCC is returned, the API was called successfully (the callback will be called only when the API returns TIM_SUCC.) If other values are returned, the API failed to be called. For the definition of each returned value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551#timresult). |

>
- Description of permissions:
 - The member information list can be obtained for any type of groups. 
 - For a BChatRoom group, the group member information list only contains the information of the group owner, admins, and some members.
- This API is used to obtain the group member information list based on specified options. For details on each field in the information list, see [GroupMemberInfo](https://intl.cloud.tencent.com/document/product/1047/34551#groupmemberinfo).


**Example**

```c
Json::Value identifiers(Json::arrayValue); 
...
Json::Value customs(Json::arrayValue);
...
Json::Value option;
option[kTIMGroupMemberGetInfoOptionInfoFlag] = kTIMGroupMemberInfoFlag_None;
option[kTIMGroupMemberGetInfoOptionRoleFlag] = kTIMGroupMemberRoleFlag_All;
option[kTIMGroupMemberGetInfoOptionCustomArray] = customs;
Json::Value getmeminfo_opt;
getmeminfo_opt[kTIMGroupGetMemberInfoListParamGroupId] = groupid;
getmeminfo_opt[kTIMGroupGetMemberInfoListParamIdentifierArray] = identifiers;
getmeminfo_opt[kTIMGroupGetMemberInfoListParamOption] = option;
getmeminfo_opt[kTIMGroupGetMemberInfoListParamNextSeq] = 0;

int ret = TIMGroupGetMemberInfoList(getmeminfo_opt.toStyledString().c_str(), [](int32_t code, const char* desc, const char* json_param, const void* user_data) {

}, this);

// The json_group_getmeminfos_param JSON string obtained by getmeminfo_opt.toStyledString().c_str() is as follows:
{
   "group_get_members_info_list_param_group_id" : "first group id",
   "group_get_members_info_list_param_identifier_array" : [],
   "group_get_members_info_list_param_next_seq" : 0,
   "group_get_members_info_list_param_option" : {
      "group_member_get_info_option_custom_array" : [],
      "group_member_get_info_option_info_flag" : 0,
      "group_member_get_info_option_role_flag" : 0
   }
}
```


## TIMGroupModifyMemberInfo

This API is used to modify the information of a group member.

**Prototype**

```c
TIM_DECL int TIMGroupModifyMemberInfo(const char* json_group_modifymeminfo_param, TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| json_group_modifymeminfo_param | const char\* | The JSON parameter string of the API for modifying group member information. |
| cb | TIMCommCallback | The callback for notifying whether modifying the group member information succeeded or failed. For the definition of the callback function, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550#timcommcallback). |
| user_data | const void\* | User-defined data. The IM SDK is only responsible for returning the user data to the callback function cb without processing the data. |

**Returned values**

| Type | Description |
|-----|-----|
| int | If TIM_SUCC is returned, the API was called successfully (the callback will be called only when the API returns TIM_SUCC.) If other values are returned, the API failed to be called. For the definition of each returned value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551#timresult). |

>
- Description of permissions:
 - Only the group owner or admin can modify the identities of group members.
 - A BChatRoom group does not support the modification of users’ identities within the group.
 - Only the group owner or admin can mute group members.
- `kTIMGroupModifyMemberInfoParamModifyFlag` can be set by bit or set to multiple values. Different flags are used to set different keys. For details, see [GroupModifyMemberInfoParam](https://intl.cloud.tencent.com/document/product/1047/34551#groupmodifymemberinfoparam).


**Example**

```c
Json::Value json_value_setgroupmeminfo;
json_value_setgroupmeminfo[kTIMGroupModifyMemberInfoParamGroupId] = "third group id";
json_value_setgroupmeminfo[kTIMGroupModifyMemberInfoParamIdentifier] = "user2";
json_value_setgroupmeminfo[kTIMGroupModifyMemberInfoParamModifyFlag] = kTIMGroupMemberModifyFlag_MemberRole | kTIMGroupMemberModifyFlag_NameCard;
json_value_setgroupmeminfo[kTIMGroupModifyMemberInfoParamMemberRole] = kTIMMemberRole_Admin;
json_value_setgroupmeminfo[kTIMGroupModifyMemberInfoParamNameCard] = "change name card";

int ret = TIMGroupModifyMemberInfo(json_value_setgroupmeminfo.toStyledString().c_str(), [](int32_t code, const char* desc, const char* json_param, const void* user_data) {
  
}, nullptr);

// The json_group_modifymeminfo_param JSON string obtained by json_value_modifygroupmeminfo.toStyledString().c_str() is as follows:
{
   "group_modify_member_info_group_id" : "third group id",
   "group_modify_member_info_identifier" : "user2",
   "group_modify_member_info_member_role" : 1,
   "group_modify_member_info_modify_flag" : 10,
   "group_modify_member_info_name_card" : "change name card"
}
```


## TIMGroupGetPendencyList

This API is used to obtain the pending request list of a group. A pending request refers to a request that has not yet been processed. For example, if an invitation to a user to join a group or a request from a user to join a group has not been processed, they are referred to as pending requests for the group.

**Prototype**

```c
TIM_DECL int TIMGroupGetPendencyList(const char* json_group_getpendence_list_param, TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| json_group_getpendence_list_param | const char\* | The JSON parameter string of the API for obtaining the pending request list of a group. |
| cb | TIMCommCallback | The callback for notifying whether obtaining the pending request list of the group succeeded or failed. For the definition of the callback function and the description of parameter parsing, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550#timcommcallback). |
| user_data | const void\* | User-defined data. The IM SDK is only responsible for returning the user data to the callback function cb without processing the data. |

**Returned values**

| Type | Description |
|-----|-----|
| int | If TIM_SUCC is returned, the API was called successfully (the callback will be called only when the API returns TIM_SUCC.) If other values are returned, the API failed to be called. For the definition of each returned value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551#timresult). |

>
- Here, group pending requests refer to all group-related operations that need to be approved, for example, a request for joining a group or for adding a user to a group that needs to be approved. No matter whether this request will be approved or rejected, the request can still be obtained through this API, and the obtained request contains the settlement flag.
- If user A requests to join group A, the group admin can obtain information related to this pending request. Since user A does not have the approval permission, this user does not need to obtain the pending request.
- If admin A adds user A to group A, user A can obtain information related to this pending request because this pending request needs to be approved by user A.
- Description of permissions:
 - Only the approver has the permission to pull related pending requests.
- `kTIMGroupPendencyOptionStartTime` specifies the timestamp for obtaining pending requests and is set to 0 for the first request. For subsequent requests, it is set based on the timestamp specified by `kTIMGroupPendencyResultNextStartTime` in the [GroupPendencyResult](https://intl.cloud.tencent.com/document/product/1047/34551#grouppendencyresult) returned by the server.
- `kTIMGroupPendencyOptionMaxLimited` specifies the recommended number of pending requests to be obtained. The server can return pending requests as required, but this key cannot be used as a flag that indicates whether a pending request is completed or not.


**Example**

```c
Json::Value get_pendency_option;
get_pendency_option[kTIMGroupPendencyOptionStartTime] = 0;
get_pendency_option[kTIMGroupPendencyOptionMaxLimited] = 0;
int ret = TIMGroupGetPendencyList(get_pendency_option.toStyledString().c_str(), [](int32_t code, const char* desc, const char* json_param, const void* user_data) {
    if (ERR_SUCC != code) { 
        // Failed to obtain the group’s pending requests.
        return;
    }
}, nullptr);

// The json_group_getpendence_list_param JSON string obtained by get_pendency_option.toStyledString().c_str() is as follows:
{
   "group_pendency_option_max_limited" : 0,
   "group_pendency_option_start_time" : 0
}
```


## TIMGroupReportPendencyReaded

This API is used to report the read state of pending requests.

**Prototype**

```c
TIM_DECL int TIMGroupReportPendencyReaded(uint64_t time_stamp, TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| time_stamp | uint64_t | The read timestamp (in seconds), which is relative to the time specified by `kTIMGroupPendencyAddTime` of [GroupPendency](https://intl.cloud.tencent.com/document/product/1047/34551#grouppendency). |
| cb | TIMCommCallback | The callback for notifying whether reporting the read state of pending requests succeeded or failed. For the definition of the callback function, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550#timcommcallback). |
| user_data | const void\* | User-defined data. The IM SDK is only responsible for returning the user data to the callback function cb without processing the data. |

**Returned values**

| Type | Description |
|-----|-----|
| int | If TIM_SUCC is returned, the API was called successfully (the callback will be called only when the API returns TIM_SUCC.) If other values are returned, the API failed to be called. For the definition of each returned value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551#timresult). |

> All group pending requests generated earlier than time_stamp are set as read. After the read state is reported, these pending requests can still be obtained, and you can determine whether these pending requests have been read based on the read timestamp.


## TIMGroupHandlePendency

This API is used to process the pending requests of a group.

**Prototype**

```c
TIM_DECL int TIMGroupHandlePendency(const char* json_group_handle_pendency_param, TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| json_group_getpendence_list_param | const char\* | The JSON parameter string of the API for processing the pending requests of a group. |
| cb | TIMCommCallback | The callback for notifying whether processing pending requests of the group succeeded or failed. For the definition of the callback function, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550#timcommcallback). |
| user_data | const void\* | User-defined data. The IM SDK is only responsible for returning the user data to the callback function cb without processing the data. |

**Returned values**

| Type | Description |
|-----|-----|
| int | If TIM_SUCC is returned, the API was called successfully (the callback will be called only when the API returns TIM_SUCC.) If other values are returned, the API failed to be called. For the definition of each returned value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551#timresult). |

>
- The IM SDK provides an API for processing the pending requests of a group. An approver can choose to approve or reject a single pending request. Pending requests that have been successfully processed cannot be processed again.
- To process a pending request, the request must carry the pending request [GroupPendency](https://intl.cloud.tencent.com/document/product/1047/34551#grouppendency). The pending request will be stored in the pending request list returned by the [TIMGroupGetPendencyList](#timgroupgetpendencylist) API. When a pending request is processed, the [GroupPendency](https://intl.cloud.tencent.com/document/product/1047/34551#grouppendency) is passed in to the key `kTIMGroupHandlePendencyParamPendency`.


**Example**

```c
Json::Value pendency; // Constructs GroupPendency.
...
Json::Value handle_pendency;
handle_pendency[kTIMGroupHandlePendencyParamIsAccept] = true;
handle_pendency[kTIMGroupHandlePendencyParamHandleMsg] = "I accept this pendency";
handle_pendency[kTIMGroupHandlePendencyParamPendency] = pendency;
int ret = TIMGroupHandlePendency(handle_pendency.toStyledString().c_str(), [](int32_t code, const char* desc, const char* json_param, const void* user_data) {
    if (ERR_SUCC != code) {
        // Failed to report that the group pending request is read.
        return;
    }
}, nullptr);

// The json_group_handle_pendency_param JSON string obtained by handle_pendency.toStyledString().c_str() is as follows:
{
   "group_handle_pendency_param_handle_msg" : "I accept this pendency",
   "group_handle_pendency_param_is_accept" : true,
   "group_handle_pendency_param_pendency" : {
      "group_pendency_add_time" : 1551414487947,
      "group_pendency_apply_invite_msg" : "Want Join Group, Thank you",
      "group_pendency_approval_msg" : "",
      "group_pendency_form_identifier" : "user2",
      "group_pendency_form_user_defined_data" : "",
      "group_pendency_group_id" : "four group id",
      "group_pendency_handle_result" : 0,
      "group_pendency_handled" : 0,
      "group_pendency_pendency_type" : 0,
      "group_pendency_to_identifier" : "user1",
      "group_pendency_to_user_defined_data" : ""
   }
}
```


