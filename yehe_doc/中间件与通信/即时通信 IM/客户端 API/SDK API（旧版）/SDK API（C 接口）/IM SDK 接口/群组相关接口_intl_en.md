For more information about groups, see [Group System](https://intl.cloud.tencent.com/document/product/1047/33529), [Group Management](https://intl.cloud.tencent.com/document/product/1047/33530), and [Custom Fields](https://intl.cloud.tencent.com/document/product/1047/33529#.E8.87.AA.E5.AE.9A.E4.B9.89.E5.AD.97.E6.AE.B5).

## TIMGroupCreate

Creating a Group

**Prototype**

```c
TIM_DECL int TIMGroupCreate(const char* json_group_create_param, TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter               | Type            | Description                                                  |
| ----------------------- | --------------- | ------------------------------------------------------------ |
| json_group_create_param | const char\*    | JSON string of the API parameter for creating a group.       |
| cb                      | TIMCommCallback | Callback function for indicating whether a group is created. For more information about the callback function definition and parameter parsing, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data               | const void\*    | User-defined data. The IM SDK only transfers the user data to the callback function `cb` without processing the data. |

**Return values**

| Type | Description                                                  |
| ---- | ------------------------------------------------------------ |
| int  | If `TIM_SUCC` is returned, the API was successfully called. (The callback `cb` is called only when the API returns `TIM_SUCC`.) If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

>?
>- You can specify a group ID when creating a group. If no group ID is specified, the IM server will generate a unique ID to facilitate subsequent operations. The callback set by this API returns the group ID.
>- For more information about JSON keys for creating group parameters, see [CreateGroupParam](https://intl.cloud.tencent.com/document/product/1047/34551).


**Sample**

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

const void* user_data = nullptr; // Returned by the callback function
int ret = TIMGroupCreate(json_value_param.toStyledString().c_str(), [](int32_t code, const char* desc, const char* json_params, const void* user_data) {
   if (ERR_SUCC != code) { 
        // Failed to create the group
        return;
    }
    
    // The group was created. Parse the JSON content to obtain `GroupID` of the created group.
}, user_data);
if (TIM_SUCC != ret) {
    // Failed to call the `TIMGroupCreate` API
}

// The `json_group_create_param` JSON string obtained by `json_value_param.toStyledString().c_str()` is as follows:
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

This API is used to delete a group.

**Prototype**

```c
TIM_DECL int TIMGroupDelete(const char* group_id, TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type            | Description                                                  |
| --------- | --------------- | ------------------------------------------------------------ |
| group_id  | const char\*    | ID of the group to be deleted.                               |
| cb        | TIMCommCallback | Callback function for indicating whether a group is deleted. For more information about the callback function definition, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data | const void\*    | User-defined data. The IM SDK only transfers the user data to the callback function `cb` without processing the data. |

**Return values**

| Type | Description                                                  |
| ---- | ------------------------------------------------------------ |
| int  | If `TIM_SUCC` is returned, the API was successfully called. (The callback `cb` is called only when the API returns `TIM_SUCC`.) If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

>?
>- Permission description:
>  - No one has the permission to delete a private group.
>  - The group owner can delete a public group, chat room, or audio-video group.
>- When this API is called to delete a group with the specified `group_id`, parameters of the callback function `cb` can be used to determine whether the group was deleted.


## TIMGroupJoin

This API is used to request to join a group.

**Prototype**

```c
TIM_DECL int TIMGroupJoin(const char* group_id, const char* hello_msg, TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type            | Description                                                  |
| --------- | --------------- | ------------------------------------------------------------ |
| group_id  | const char\*    | ID of the group to be joined.                                |
| hello_msg | const char\*    | (Optional) Application reason.                               |
| cb        | TIMCommCallback | Callback function for indicating whether group joining is successful. For more information about the callback function definition, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data | const void\*    | User-defined data. The IM SDK only transfers the user data to the callback function `cb` without processing the data. |

**Return values**

| Type | Description                                                  |
| ---- | ------------------------------------------------------------ |
| int  | If `TIM_SUCC` is returned, the API was successfully called. (The callback `cb` is called only when the API returns `TIM_SUCC`.) If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

>?
>- Permission description:
>  - Users cannot request to join a private group.
>  - Users can request to join a public group or chat room.
>   If approval is needed for a group, the group admin and owner will receive a system message for requesting to join the group. A user can join the group only after the group admin or owner approves the request. If any user is allowed to join the group according to the group configuration, the user can join the group directly. Any user can join an audio-video group.
>- When this API is called to request to join a group with the specified `group_id`, parameters of the callback function `cb` can be used to determine whether the join was successful.


## TIMGroupQuit

This API is used to leave a group.

**Prototype**

```c
TIM_DECL int TIMGroupQuit(const char* group_id, TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type            | Description                                                  |
| --------- | --------------- | ------------------------------------------------------------ |
| group_id  | const char\*    | ID of the group to be left.                                  |
| cb        | TIMCommCallback | Callback function for indicating whether a user leaves the group. For more information about the callback function definition, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data | const void\*    | User-defined data. The IM SDK only transfers the user data to the callback function `cb` without processing the data. |

**Return values**

| Type | Description                                                  |
| ---- | ------------------------------------------------------------ |
| int  | If `TIM_SUCC` is returned, the API was successfully called. (The callback `cb` is called only when the API returns `TIM_SUCC`.) If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

>?
>- Permission description:
>  - All members in a private group can leave the group.
>  - The group owner cannot leave a public group, chat room, or audio-video group.
>- When this API is called to leave a group with the specified `group_id`, parameters of the callback function `cb` can be used to determine whether the group leaving was successful.


## TIMGroupInviteMember

This API is used to invite a user to join a group.

**Prototype**

```c
TIM_DECL int TIMGroupInviteMember(const char* json_group_invite_param, TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter               | Type            | Description                                                  |
| ----------------------- | --------------- | ------------------------------------------------------------ |
| json_group_invite_param | const char\*    | JSON string of the API parameter for inviting a user to join a group. |
| cb                      | TIMCommCallback | Callback function for indicating whether a user is invited to join a group. For more information about the callback function definition and parameter parsing, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data               | const void\*    | User-defined data. The IM SDK only transfers the user data to the callback function `cb` without processing the data. |

**Return values**

| Type | Description                                                  |
| ---- | ------------------------------------------------------------ |
| int  | If `TIM_SUCC` is returned, the API was successfully called. (The callback `cb` is called only when the API returns `TIM_SUCC`.) If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

>?
>- Permission description:
>  - Users can be added only to a private group.
>  - Users can be invited to join a public group or chat room.
>  - A user cannot be invited to join an audio-video group unless the user agrees.
>- You can call this API to invite multiple users to join a group. For more information about JSON keys, see [GroupInviteMemberParam](https://intl.cloud.tencent.com/document/product/1047/34551).


**Sample**

```c
Json::Value json_value_invite;
json_value_invite[kTIMGroupInviteMemberParamGroupId] = groupid;
json_value_invite[kTIMGroupInviteMemberParamUserData] = "userdata";
json_value_invite[kTIMGroupInviteMemberParamIdentifierArray].append("user1");
json_value_invite[kTIMGroupInviteMemberParamIdentifierArray].append("user2");

const void* user_data = nullptr; // Returned by the callback function
int ret = TIMGroupInviteMember(json_value_invite.toStyledString().c_str(), [](int32_t code, const char* desc, const char* json_params, const void* user_data) {
    if (ERR_SUCC != code) { 
        // Failed to invite users to join a group
        return;
    }
    // Users are invited to join the group. Parse the JSON content to obtain the invitation result of each user.
}, user_data);
if (TIM_SUCC != ret) {
    // Failed to call the `TIMGroupInviteMember` API
}

// The `json_group_invite_param` JSON string obtained by `json_value_invite.toStyledString().c_str()` is as follows:
{
   "group_invite_member_param_group_id" : "first group id",
   "group_invite_member_param_identifier_array" : [ "user1", "user2" ],
   "group_invite_member_param_user_data" : "userdata"
}
```


## TIMGroupDeleteMember

This API is used to delete group members.

**Prototype**

```c
TIM_DECL int TIMGroupDeleteMember(const char* json_group_delete_param, TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter               | Type            | Description                                                  |
| ----------------------- | --------------- | ------------------------------------------------------------ |
| json_group_delete_param | const char\*    | JSON string of the API parameter for deleting group members. |
| cb                      | TIMCommCallback | Callback function for indicating whether group members are deleted. For more information about the callback function definition and parameter parsing, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data               | const void\*    | User-defined data. The IM SDK only transfers the user data to the callback function `cb` without processing the data. |

**Return values**

| Type | Description                                                  |
| ---- | ------------------------------------------------------------ |
| int  | If `TIM_SUCC` is returned, the API was successfully called. (The callback `cb` is called only when the API returns `TIM_SUCC`.) If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

>?
>- Permission description:
>  - Only the creator of a private group can delete group members.
>  - Only the admins and owner of a public group or chat room can delete group members.
>  - No group members can be deleted from an audio-video group.
>- You can call this API to delete multiple group members. For more information about JSON keys, see [GroupDeleteMemberParam](https://intl.cloud.tencent.com/document/product/1047/34551).


**Sample**

```c
Json::Value json_value_delete;
json_value_delete[kTIMGroupDeleteMemberParamGroupId] = groupid;
json_value_delete[kTIMGroupDeleteMemberParamUserData] = "reason";
json_value_delete[kTIMGroupDeleteMemberParamIdentifierArray].append("user1");
json_value_delete[kTIMGroupDeleteMemberParamIdentifierArray].append("user2");

int ret = TIMGroupDeleteMember(json_value_delete.toStyledString().c_str(), [](int32_t code, const char* desc, const char* json_params, const void* user_data) {
      
}, this));

// The `json_group_delete_param` JSON string obtained by `json_value_delete.toStyledString().c_str()` is as follows:
{
  "group_delete_member_param_group_id" : "third group id",
  "group_delete_member_param_identifier_array" : [ "user2", "user3" ],
  "group_delete_member_param_user_data" : "reason"
}
```


## TIMGroupGetJoinedGroupList

This API is used to obtain the list of groups that a user has joined.

**Prototype**

```c
TIM_DECL int TIMGroupGetJoinedGroupList(TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type            | Description                                                  |
| --------- | --------------- | ------------------------------------------------------------ |
| cb        | TIMCommCallback | Callback function for indicating whether the list of groups that a user has joined is obtained. For more information about the callback function definition and parameter parsing, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data | const void\*    | User-defined data. The IM SDK only transfers the user data to the callback function `cb` without processing the data. |

**Return values**

| Type | Description                                                  |
| ---- | ------------------------------------------------------------ |
| int  | If `TIM_SUCC` is returned, the API was successfully called. (The callback `cb` is called only when the API returns `TIM_SUCC`.) If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

>?
>- Permission description:
>  - You can call this API to obtain the list of groups that you have joined.
>  - This API can only obtain the list of some audio-video groups that a user has joined.
>- This API is used to obtain the list of groups that the current user has joined. The basic group information will be returned. For more information about fields in the returned basic group information, see [GroupBaseInfo](https://intl.cloud.tencent.com/document/product/1047/34551).


## TIMGroupGetGroupInfoList

This API is used to obtain information about groups on a list.

**Prototype**

```c
TIM_DECL int TIMGroupGetGroupInfoList(const char* json_group_getinfo_param, TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter                | Type            | Description                                                  |
| ------------------------ | --------------- | ------------------------------------------------------------ |
| json_group_getinfo_param | const char\*    | JSON string of the API parameter for obtaining information about groups on a list. |
| cb                       | TIMCommCallback | Callback function for indicating whether information about groups on a list is obtained. For more information about the callback function definition and parameter parsing, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data                | const void\*    | User-defined data. The IM SDK only transfers the user data to the callback function `cb` without processing the data. |

**Return values**

| Type | Description                                                  |
| ---- | ------------------------------------------------------------ |
| int  | If `TIM_SUCC` is returned, the API was successfully called. (The callback `cb` is called only when the API returns `TIM_SUCC`.) If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

>?This API is used to obtain detailed information about groups in the specified group ID list. For more information about fields in the returned detailed group information, see [GroupDetailInfo](https://intl.cloud.tencent.com/document/product/1047/34551).


**Sample**

```c
Json::Value groupids;
groupids.append("third group id");
groupids.append("second group id");
groupids.append("first group id");
int ret = TIMGroupGetGroupInfoList(groupids.toStyledString().c_str(), [](int32_t code, const char* desc, const char* json_param, const void* user_data) {

}, this);

// The `json_group_getinfo_param` JSON string obtained by `groupids.toStyledString().c_str()` is as follows:
[ "third group id", "second group id", "first group id" ]
```


## TIMGroupModifyGroupInfo

This API is used to modify group information.

**Prototype**

```c
TIM_DECL int TIMGroupModifyGroupInfo(const char* json_group_modifyinfo_param, TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter                   | Type            | Description                                                  |
| --------------------------- | --------------- | ------------------------------------------------------------ |
| json_group_modifyinfo_param | const char\*    | JSON string of the API parameter for modifying group information. |
| cb                          | TIMCommCallback | Callback function for indicating whether the group information is modified. For more information about the callback function definition, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data                   | const void\*    | User-defined data. The IM SDK only transfers the user data to the callback function `cb` without processing the data. |

**Return values**

| Type | Description                                                  |
| ---- | ------------------------------------------------------------ |
| int  | If `TIM_SUCC` is returned, the API was successfully called. (The callback `cb` is called only when the API returns `TIM_SUCC`.) If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

>?
>- Description of the permissions for modifying the group owner (group ownership transfer):
>  - Only the group owner has the permission to transfer the group ownership.
>  - The ownership of an audio-video group cannot be transferred.
>- Description of the permissions for modifying other group information:
>  - Only the group owner or admin of a public group, chat room, or audio-video group can modify the group introduction.
>  - Any members in a private group can modify the group introduction.
>- `kTIMGroupModifyInfoParamModifyFlag` can be set by bit or set to multiple values. Different flags are used to set different keys. For more information, see [GroupModifyInfoParam](https://intl.cloud.tencent.com/document/product/1047/34551).


**Example 1: Setting the group owner**

```c
Json::Value json_value_modifygroupinfo;
json_value_modifygroupinfo[kTIMGroupModifyInfoParamGroupId] = "first group id";
json_value_modifygroupinfo[kTIMGroupModifyInfoParamModifyFlag] = kTIMGroupModifyInfoFlag_Owner;
json_value_modifygroupinfo[kTIMGroupModifyInfoParamOwner] = "user2";

int ret = TIMGroupModifyGroupInfo(json_value_modifygroupinfo.toStyledString().c_str(), [](int32_t code, const char* desc, const char* json_param, const void* user_data) {

}, nullptr);

// The `json_group_modifyinfo_param` JSON string obtained by `json_value_modifygroupinfo.toStyledString().c_str()` is as follows:
{
  "group_modify_info_param_group_id" : "first group id",
  "group_modify_info_param_modify_flag" : -2147483648,
  "group_modify_info_param_owner" : "user2"
}
```


**Example 2: Setting the group name and group notification**

```c
Json::Value json_value_modifygroupinfo;
json_value_modifygroupinfo[kTIMGroupModifyInfoParamGroupId] = "first group id";
json_value_modifygroupinfo[kTIMGroupModifyInfoParamModifyFlag] = kTIMGroupModifyInfoFlag_Name | kTIMGroupModifyInfoFlag_Notification;
json_value_modifygroupinfo[kTIMGroupModifyInfoParamGroupName] = "first group name to other name";
json_value_modifygroupinfo[kTIMGroupModifyInfoParamNotification] = "first group notification";

int ret = TIMGroupModifyGroupInfo(json_value_modifygroupinfo.toStyledString().c_str(), [](int32_t code, const char* desc, const char* json_param, const void* user_data) {

}, nullptr);

// The `json_group_modifyinfo_param` JSON string obtained by `json_value_modifygroupinfo.toStyledString().c_str()` is as follows:
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

| Parameter                    | Type            | Description                                                  |
| ---------------------------- | --------------- | ------------------------------------------------------------ |
| json_group_getmeminfos_param | const char\*    | JSON string of the API parameter for obtaining the group member information list. |
| cb                           | TIMCommCallback | Callback function for indicating whether the group member information list is obtained. For more information about the callback function definition and parameter parsing, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data                    | const void\*    | User-defined data. The IM SDK only transfers the user data to the callback function `cb` without processing the data. |

**Return values**

| Type | Description                                                  |
| ---- | ------------------------------------------------------------ |
| int  | If `TIM_SUCC` is returned, the API was successfully called. (The callback `cb` is called only when the API returns `TIM_SUCC`.) If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

>?
>- Permission description:
>  - The member list of a group of any type can be obtained.
>  - The member list of an audio-video group contains only the group owner, admins, and some members.
>- This API is used to obtain the group member information list based on different options specified. For more information about each field in the information list, see [GroupMemberInfo](https://intl.cloud.tencent.com/document/product/1047/34551).


**Sample**

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

// The `json_group_getmeminfos_param` JSON string obtained by `getmeminfo_opt.toStyledString().c_str()` is as follows:
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

This API is used to modify group member information.

**Prototype**

```c
TIM_DECL int TIMGroupModifyMemberInfo(const char* json_group_modifymeminfo_param, TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter                      | Type            | Description                                                  |
| ------------------------------ | --------------- | ------------------------------------------------------------ |
| json_group_modifymeminfo_param | const char\*    | JSON string of the API parameter for modifying group member information. |
| cb                             | TIMCommCallback | Callback function for indicating whether the group member information is modified. For more information about the callback function definition, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data                      | const void\*    | User-defined data. The IM SDK only transfers the user data to the callback function `cb` without processing the data. |

**Return values**

| Type | Description                                                  |
| ---- | ------------------------------------------------------------ |
| int  | If `TIM_SUCC` is returned, the API was successfully called. (The callback `cb` is called only when the API returns `TIM_SUCC`.) If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

>?
>- Permission description:
>  - Only the group owner or admin can modify group member roles.
>  - The roles of members in an audio-video group cannot be modified.
>  - Only the group owner or admin can mute group members.
>- `kTIMGroupModifyMemberInfoParamModifyFlag` can be set by bit or set to multiple values. Different flags are used to set different keys. For more information, see [GroupModifyMemberInfoParam](https://intl.cloud.tencent.com/document/product/1047/34551).


**Sample**

```c
Json::Value json_value_setgroupmeminfo;
json_value_setgroupmeminfo[kTIMGroupModifyMemberInfoParamGroupId] = "third group id";
json_value_setgroupmeminfo[kTIMGroupModifyMemberInfoParamIdentifier] = "user2";
json_value_setgroupmeminfo[kTIMGroupModifyMemberInfoParamModifyFlag] = kTIMGroupMemberModifyFlag_MemberRole | kTIMGroupMemberModifyFlag_NameCard;
json_value_setgroupmeminfo[kTIMGroupModifyMemberInfoParamMemberRole] = kTIMMemberRole_Admin;
json_value_setgroupmeminfo[kTIMGroupModifyMemberInfoParamNameCard] = "change name card";

int ret = TIMGroupModifyMemberInfo(json_value_setgroupmeminfo.toStyledString().c_str(), [](int32_t code, const char* desc, const char* json_param, const void* user_data) {
  
}, nullptr);

// The `json_group_modifymeminfo_param` JSON string obtained by `json_value_modifygroupmeminfo.toStyledString().c_str()` is as follows:
{
   "group_modify_member_info_group_id" : "third group id",
   "group_modify_member_info_identifier" : "user2",
   "group_modify_member_info_member_role" : 1,
   "group_modify_member_info_modify_flag" : 10,
   "group_modify_member_info_name_card" : "change name card"
}
```

## TIMGroupMarkGroupMemberList

This API is used to mark group members.

**Prototype**

```c
TIM_DECL int TIMGroupMarkGroupMemberList(const char* group_id, const char* member_array, uint32_t mark_type, bool enable_mark, TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter    | Type         | Description                                                  |
| ------------ | ------------ | ------------------------------------------------------------ |
| group_id     | const char\* | Group ID.                                                    |
| member_array | const char\* | List of group member IDs.                                    |
| mark_type    | uint32_t     | Mark type. Numeric, which is greater than or equal to 1,000. Customizable. You can define up to 10 marks per audio-video group. |
| enable_mark  | bool         | `true`: Adds a mark. `false`: Removes a mark.                |
| cb           | const void\* | Callback function for indicating whether setting or removing group members' custom roles is successful. For the definition of the callback function, see [TIMCommCallback](TIMCloudCallback.h). |
| user_data    | const void\* | User-defined data. The IM SDK only transfers the user data to the callback function `cb` without processing the data. |

**Return values**

| Type | Description                                                  |
| ---- | ------------------------------------------------------------ |
| int  | If `TIM_SUCC` is returned, the API was successfully called. (The callback `cb` is called only when the API returns `TIM_SUCC`.) If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

>?
>- This API is supported only by audio-video groups.
>- Only the owner of a group has the permission to mark others in the group.

**Sample**

```c
std::string group_id = "avchatroom_group_id";
uint32_t mark_type = 30005;
bool enable_mark = true;

json::Array member_array;
member_array.push_back("user1");
member_array.push_back("user2");

TIMGroupMarkGroupMemberList(group_id.c_str(), json::Serialize(member_array).c_str(), mark_type, enable_mark, [](int32_t code, const char* desc, const char* json_param, const void* user_data) {
    Printf("MarkGroupMemberList code:%d|desc:%s|json_param %s\r\n", code, desc, json_param);
}, nullptr);
```

## TIMGroupGetPendencyList

This API is used to obtain the pending request list of a group. Pending requests indicate requests that are not handled, for example, requests for inviting a user to join a group or requesting to join a group.

**Prototype**

```c
TIM_DECL int TIMGroupGetPendencyList(const char* json_group_getpendence_list_param, TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter                         | Type            | Description                                                  |
| --------------------------------- | --------------- | ------------------------------------------------------------ |
| json_group_getpendence_list_param | const char\*    | JSON string of the API parameter for obtaining the pending request list of a group. |
| cb                                | TIMCommCallback | Callback function for indicating whether the pending request list of a group is obtained. For more information about the callback function definition and parameter parsing, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data                         | const void\*    | User-defined data. The IM SDK only transfers the user data to the callback function `cb` without processing the data. |

**Return values**

| Type | Description                                                  |
| ---- | ------------------------------------------------------------ |
| int  | If `TIM_SUCC` is returned, the API was successfully called. (The callback `cb` is called only when the API returns `TIM_SUCC`.) If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

>?
>- Here, group pending requests refer to all group-related operations that need to be approved, for example, a request for joining a group or adding users to a group. You can call this API to obtain a pending request regardless of whether it is approved or rejected, and the returned pending request is marked handled.
>- If user A applies to join group A, the group admin can obtain information related to this pending request. As user A does not have the approval permission, user A does not need to obtain this pending request.
>- If admin A adds user A to group A, user A can obtain information related to this pending request because user A needs to approve this pending request.
>- Permission description:
>  - Only the approver has the permission to obtain related pending requests.
>- `kTIMGroupPendencyOptionStartTime` specifies the timestamp for obtaining pending requests. It is set to `0` for the first request and later set based on the timestamp specified by `kTIMGroupPendencyResultNextStartTime` contained in [GroupPendencyResult](https://intl.cloud.tencent.com/document/product/1047/34551).
>- `kTIMGroupPendencyOptionMaxLimited` specifies the recommended number of pending requests to be obtained. The server can return pending requests as required. However, this key does not indicate whether a pending request is handled.


**Sample**

```c
Json::Value get_pendency_option;
get_pendency_option[kTIMGroupPendencyOptionStartTime] = 0;
get_pendency_option[kTIMGroupPendencyOptionMaxLimited] = 0;
int ret = TIMGroupGetPendencyList(get_pendency_option.toStyledString().c_str(), [](int32_t code, const char* desc, const char* json_param, const void* user_data) {
    if (ERR_SUCC != code) { 
        // Failed to obtain pending requests of a group
        return;
    }
}, nullptr);

// The `json_group_getpendence_list_param` JSON string obtained by `get_pendency_option.toStyledString().c_str()` is as follows:
{
   "group_pendency_option_max_limited" : 0,
   "group_pendency_option_start_time" : 0
}
```


## TIMGroupReportPendencyReaded

This API is used to report that pending requests are read.

**Prototype**

```c
TIM_DECL int TIMGroupReportPendencyReaded(uint64_t time_stamp, TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter  | Type            | Description                                                  |
| ---------- | --------------- | ------------------------------------------------------------ |
| time_stamp | uint64_t        | Read timestamp (in seconds), which is compared with the time specified by `kTIMGroupPendencyAddTime` in [GroupPendency](https://intl.cloud.tencent.com/document/product/1047/34551). |
| cb         | TIMCommCallback | Callback function for indicating whether the read state of pending requests is reported. For more information about the callback function definition, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data  | const void\*    | User-defined data. The IM SDK only transfers the user data to the callback function `cb` without processing the data. |

**Return values**

| Type | Description                                                  |
| ---- | ------------------------------------------------------------ |
| int  | If `TIM_SUCC` is returned, the API was successfully called. (The callback `cb` is called only when the API returns `TIM_SUCC`.) If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

>?Group pending requests generated earlier than `time_stamp` are set to the read state. After the read state is reported, these pending requests can still be obtained. However, you can determine whether these pending requests have been read based on the read timestamp.


## TIMGroupHandlePendency

This API is used to handle pending requests of a group.

**Prototype**

```c
TIM_DECL int TIMGroupHandlePendency(const char* json_group_handle_pendency_param, TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter                        | Type            | Description                                                  |
| -------------------------------- | --------------- | ------------------------------------------------------------ |
| json_group_handle_pendency_param | const char\*    | JSON string of the API parameter for handling pending requests of a group. |
| cb                               | TIMCommCallback | Callback function for indicating whether group pending requests are handled. For more information about the callback function definition, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data                        | const void\*    | User-defined data. The IM SDK only transfers the user data to the callback function `cb` without processing the data. |

**Return values**

| Type | Description                                                  |
| ---- | ------------------------------------------------------------ |
| int  | If `TIM_SUCC` is returned, the API was successfully called. (The callback `cb` is called only when the API returns `TIM_SUCC`.) If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

>?
>- The IM SDK provides this API for handling pending requests of a group. An approver can select a single pending request to accept or reject. Pending requests that have been handled cannot be handled again.
>- To handle a pending request, [GroupPendency](https://intl.cloud.tencent.com/document/product/1047/34551) must be carried. The pending request can be saved in the pending request list returned by the [TIMGroupGetPendencyList](#timgroupgetpendencylist) API. When a pending request is handled, [GroupPendency](https://intl.cloud.tencent.com/document/product/1047/34551) is passed into the `kTIMGroupHandlePendencyParamPendency` key.


**Sample**

```c
Json::Value pendency; // Construct GroupPendency
...
Json::Value handle_pendency;
handle_pendency[kTIMGroupHandlePendencyParamIsAccept] = true;
handle_pendency[kTIMGroupHandlePendencyParamHandleMsg] = "I accept this pendency";
handle_pendency[kTIMGroupHandlePendencyParamPendency] = pendency;
int ret = TIMGroupHandlePendency(handle_pendency.toStyledString().c_str(), [](int32_t code, const char* desc, const char* json_param, const void* user_data) {
    if (ERR_SUCC != code) {
        // Failed to handle a group pending request
        return;
    }
}, nullptr);

// The `json_group_handle_pendency_param` JSON string obtained by `handle_pendency.toStyledString().c_str()` is as follows:
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


## TIMGroupGetOnlineMemberCount

This API is used to obtain the number of online members of a group.

**Prototype**

```c
TIM_DECL int TIMGroupGetOnlineMemberCount(const char* groupid, TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type            | Description                                                  |
| --------- | --------------- | ------------------------------------------------------------ |
| group_id  | const char\*    | Group ID.                                                    |
| cb        | TIMCommCallback | Callback function for obtaining the number of online members of a group. For more information about the callback function definition, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data | const void\*    | User-defined data. The IM SDK only transfers the user data to the callback function `cb` without processing the data. |

**Return values**

| Type | Description                                                  |
| ---- | ------------------------------------------------------------ |
| int  | If `TIM_SUCC` is returned, the API was successfully called. (The callback `cb` is called only when the API returns `TIM_SUCC`.) If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

>? Notes:
>- Currently, this API is supported only by audio-video groups (AVChatRoom).
>- This API implements frequency limit checks. It can be called by the SDK for up to once per 60 seconds.

**Sample**

```c
TIMGroupGetOnlineMemberCount("lamarzhang_group_public", [](int32_t code, const char* desc, const char* json_param, const void* user_data) {

}, nullptr);

Example of `json_param`. For details on JSON keys, see [GroupGetOnlineMemberCountResult](TIMCloudCallback.h).
{"group_get_online_member_count_result":0}
```


## TIMGroupSearchGroups

This API is used to search for group profiles. (This API is supported only in SDK 5.4.666 or later, and you need to purchase the Ultimate edition to use this API.)

**Prototype**

```c
TIM_DECL int TIMGroupSearchGroups(const char *json_group_search_groups_param, TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter                      | Type            | Description                                                  |
| ------------------------------ | --------------- | ------------------------------------------------------------ |
| json_group_search_groups_param | const char\*    | Array of the parameters for searching for a group list. For more information, see [GroupSearchParam](https://intl.cloud.tencent.com/document/product/1047/34551). |
| cb                             | TIMCommCallback | Callback function for searching for a group list. For more information about the callback function definition, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data                      | const void\*    | User-defined data. The IM SDK only transfers the user data to the callback function `cb` without processing the data. |

**Return values**

| Type | Description                                                  |
| ---- | ------------------------------------------------------------ |
| int  | If `TIM_SUCC` is returned, the API was successfully called. (The callback `cb` is called only when the API returns `TIM_SUCC`.) If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

>? The IM SDK will search for all groups whose names are contained in the search keyword list `keywordList` and return the group information list. The keyword list can contain up to 5 keywords.

**Sample**

```c
Json::Array json_keyword_list;
json_keyword_list.append("lamarzhang_group_public");

Json::Array json_field_list;
json_field_list.appned(kTIMGroupSearchFieldKey_GroupId);

Json::Object json_obj;
json_obj[TIMGroupSearchParamKeywordList] = json_keyword_list;
json_obj[TIMGroupSearchParamFieldList] = json_field_list;
TIMGroupSearchGroups(json_array.toStyledString().c_str(), [](int32_t code, const char* desc, const char* json_param, const void* user_data) {

}, nullptr);
// Example of the callback `json_param`. For details on JSON keys, see [GroupDetailInfo](TIMCloudDef.h).
[{
    "group_detial_info_add_option": 1,
    "group_detial_info_create_time": 0,
    "group_detial_info_custom_info": [{
        "group_info_custom_string_info_key": "custom_public",
        "group_info_custom_string_info_value": ""
    }, {
        "group_info_custom_string_info_key": "custom_public2",
        "group_info_custom_string_info_value": ""
    }, {
        "group_info_custom_string_info_key": "group_info",
        "group_info_custom_string_info_value": ""
    }, {
        "group_info_custom_string_info_key": "group_test",
        "group_info_custom_string_info_value": ""
    }],
    "group_detial_info_face_url": "",
    "group_detial_info_group_id": "lamarzhang_group_public",
    "group_detial_info_group_name": "lamarzhang_group_public",
    "group_detial_info_group_type": 0,
    "group_detial_info_info_seq": 9,
    "group_detial_info_introduction": "Instroduction",
    "group_detial_info_is_shutup_all": false,
    "group_detial_info_last_info_time": 1620810613,
    "group_detial_info_last_msg_time": 1620810613,
    "group_detial_info_max_member_num": 1000,
    "group_detial_info_member_num": 2,
    "group_detial_info_next_msg_seq": 2,
    "group_detial_info_notification": "Notification",
    "group_detial_info_online_member_num": 0,
    "group_detial_info_owener_identifier": "lamarzhang",
    "group_detial_info_searchable": true,
    "group_detial_info_visible": true
}]
```


## TIMGroupSearchGroupMembers

This API is used to search for group members. (This API is supported only in SDK 5.4.666 or later, and you need to purchase the Ultimate edition to use this API.)

**Prototype**

```c
TIM_DECL int TIMGroupSearchGroupMembers(const char *json_group_search_group_members_param, TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter                             | Type            | Description                                                  |
| ------------------------------------- | --------------- | ------------------------------------------------------------ |
| json_group_search_group_members_param | const char\*    | Array of the parameters for searching for a group member list. For more information, see [GroupMemberSearchParam](https://intl.cloud.tencent.com/document/product/1047/34551). |
| cb                                    | TIMCommCallback | Callback function for searching for a group member list. For more information about the callback function definition, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data                             | const void\*    | User-defined data. The IM SDK only transfers the user data to the callback function `cb` without processing the data. |

**Return values**

| Type | Description                                                  |
| ---- | ------------------------------------------------------------ |
| int  | If `TIM_SUCC` is returned, the API was successfully called. (The callback `cb` is called only when the API returns `TIM_SUCC`.) If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

>? The IM SDK will search for all group members in the specified group ID list whose group member information (name card, friend remarks, nickname, or userID) is contained in the search keyword list `keywordList` and return the group ID and group member list map. The keyword list can contain up to 5 keywords.

**Sample**

```c
Json::Array json_groupid_list;
json_groupid_list.append("lamarzhang_group_public");

Json::Array json_keyword_list;
json_keyword_list.append("98826");

Json::Array json_field_list;
json_field_list.appned(kTIMGroupMemberSearchFieldKey_Identifier);

Json::Object json_obj;
json_obj[TIMGroupMemberSearchParamGroupidList ] = json_groupid_list;
json_obj[TIMGroupMemberSearchParamKeywordList ] = json_keyword_list;
json_obj[TIMGroupMemberSearchParamFieldList ] = json_field_list;
TIMGroupSearchGroupMembers(json_obj.toStyledString().c_str(), [](int32_t code, const char* desc, const char* json_param, const void* user_data) {

}, nullptr);

// Example of the callback `json_param`. For details on JSON keys, see [GroupGetOnlineMemberCountResult](TIMCloudDef.h).
[{
  "group_search_member_result_groupid": "lamarzhang_group_public",
  "group_search_member_result_menber_info_list": [{
      "group_member_info_custom_info": [{
          "group_info_custom_string_info_key": "group_member_p",
          "group_info_custom_string_info_value": ""
      }, {
          "group_info_custom_string_info_key": "group_member_p2",
          "group_info_custom_string_info_value": ""
      }],
      "group_member_info_identifier": "98826",
      "group_member_info_join_time": 1620810613,
      "group_member_info_member_role": 4,
      "group_member_info_msg_flag": 0,
      "group_member_info_msg_seq": 0,
      "group_member_info_name_card": "",
      "group_member_info_shutup_time": 0
  }]
}]
```


## TIMGroupInitGroupAttributes

This API is used to initialize group attributes. This will clear the existing group attribute list.

**Prototype**

```c
TIM_DECL int TIMGroupInitGroupAttributes(const char *group_id, const char *json_group_atrributes, TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter             | Type            | Description                                                  |
| --------------------- | --------------- | ------------------------------------------------------------ |
| group_id              | const char\*    | Group ID.                                                    |
| json_group_atrributes | const char\*    | Parameters of the group attribute list. For more information, see [GroupAttributes](https://intl.cloud.tencent.com/document/product/1047/34551). |
| cb                    | TIMCommCallback | Callback function for initializing group attributes. For more information about the callback function definition, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data             | const void\*    | User-defined data. The IM SDK only transfers the user data to the callback function `cb` without processing the data. |

**Return values**

| Type | Description                                                  |
| ---- | ------------------------------------------------------------ |
| int  | If `TIM_SUCC` is returned, the API was successfully called. (The callback `cb` is called only when the API returns `TIM_SUCC`.) If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

**Sample**

```c
Json::Object json_obj;
json_obj[TIMGroupAttributeKey] = "atrribute_key1";
json_obj[TIMGroupAttributeValue] = "atrribute_value1";

Json::Array json_array;
json_array.append(json_obj);
TIMGroupInitGroupAttributes("lamarzhang_group_public", json_array.toStyledString().c_str(), [](int32_t code, const char* desc, const char* json_param, const void* user_data) {

}, nullptr);

// `json_param` is an empty string. Check `code` to determine the result.
```


## TIMGroupSetGroupAttributes

This API is used to set group attributes. If the group attributes already exist, their values are updated. Otherwise, the group attributes are added.

**Prototype**

```c
TIM_DECL int TIMGroupSetGroupAttributes(const char *group_id, const char *json_group_atrributes, TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter             | Type            | Description                                                  |
| --------------------- | --------------- | ------------------------------------------------------------ |
| group_id              | const char\*    | Group ID.                                                    |
| json_group_atrributes | const char\*    | Parameters of the group attribute list. For more information, see [GroupAttributes](https://intl.cloud.tencent.com/document/product/1047/34551). |
| cb                    | TIMCommCallback | Callback function for setting group attributes. For more information about the callback function definition, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data             | const void\*    | User-defined data. The IM SDK only transfers the user data to the callback function `cb` without processing the data. |

**Return values**

| Type | Description                                                  |
| ---- | ------------------------------------------------------------ |
| int  | If `TIM_SUCC` is returned, the API was successfully called. (The callback `cb` is called only when the API returns `TIM_SUCC`.) If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

**Sample**

```c
Json::Object json_obj;
json_obj[TIMGroupAttributeKey] = "atrribute_key1";
json_obj[TIMGroupAttributeValue] = "atrribute_value2";

Json::Array json_array;
json_array.append(json_obj);
TIMGroupSetGroupAttributes("lamarzhang_group_public", json_array.toStyledString().c_str(), [](int32_t code, const char* desc, const char* json_param, const void* user_data) {

}, nullptr);

`json_param` is an empty string. Check `code` to determine the result.
```


## TIMGroupDeleteGroupAttributes

This API is used to delete group attributes.

**Prototype**

```c
TIM_DECL int TIMGroupDeleteGroupAttributes(const char *group_id, const char *json_keys, TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type            | Description                                                  |
| --------- | --------------- | ------------------------------------------------------------ |
| group_id  | const char\*    | Group ID.                                                    |
| json_keys | const char\*    | Key of a group attribute.                                    |
| cb        | TIMCommCallback | Callback function for deleting group attributes. For more information about the callback function definition, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data | const void\*    | User-defined data. The IM SDK only transfers the user data to the callback function `cb` without processing the data. |

**Return values**

| Type | Description                                                  |
| ---- | ------------------------------------------------------------ |
| int  | If `TIM_SUCC` is returned, the API was successfully called. (The callback `cb` is called only when the API returns `TIM_SUCC`.) If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

**Sample**

```c
Json::Array json_array;
json_array.append("atrribute_key1");

TIMGroupDeleteGroupAttributes("lamarzhang_group_public", json_array.toStyledString().c_str() ,[](int32_t code, const char* desc, const char* json_param, const void* user_data) {
    printf("InitGroupAttributes code:%d|desc:%s|json_param %s\r\n", code, desc, json_param);
}, nullptr);
// `json_param` is an empty string. Check `code` to determine the result.
```


## TIMGroupGetGroupAttributes

This API is used to get specified group attributes. Passing in `nil` for `keys` means getting all attributes.

**Prototype**

```c
TIM_DECL int TIMGroupGetGroupAttributes(const char *group_id, const char *json_keys, TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type            | Description                                                  |
| --------- | --------------- | ------------------------------------------------------------ |
| group_id  | const char\*    | Group ID.                                                    |
| json_keys | const char\*    | If an empty string is passed in, the SDK obtains the list of all attributes. |
| cb        | TIMCommCallback | Callback function for getting group attributes. For more information about the callback function definition, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data | const void\*    | User-defined data. The IM SDK only transfers the user data to the callback function `cb` without processing the data. |

**Return values**

| Type | Description                                                  |
| ---- | ------------------------------------------------------------ |
| int  | If `TIM_SUCC` is returned, the API was successfully called. (The callback `cb` is called only when the API returns `TIM_SUCC`.) If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

**Sample**

```c
Json::Array json_array;
json_array.append("atrribute_key1");

TIMGroupGetGroupAttributes("lamarzhang_group_public", json_array.toStyledString().c_str(), [](int32_t code, const char* desc, const char* json_param, const void* user_data) {
    printf("InitGroupAttributes code:%d|desc:%s|json_param %s\r\n", code, desc, json_param);
}, nullptr);

// Example of the callback `json_param`. For details on JSON keys, see [GroupAttributes](TIMCloudDef.h).
[{
    "group_atrribute_key": "atrribute_key1",
    "group_atrribute_value": "atrribute_value1"
}]
```
