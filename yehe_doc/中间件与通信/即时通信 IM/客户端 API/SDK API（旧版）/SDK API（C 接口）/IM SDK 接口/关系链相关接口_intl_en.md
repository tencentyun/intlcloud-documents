For more information about relationship chains, see [Relationship Chain System Overview](https://intl.cloud.tencent.com/document/product/1047/33521).

## TIMFriendshipGetFriendProfileList

This API is used to obtain the contacts.

**Prototype**

```c
TIM_DECL int TIMFriendshipGetFriendProfileList(TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type            | Description                                                  |
| --------- | --------------- | ------------------------------------------------------------ |
| cb        | TIMCommCallback | Callback function for indicating whether the contacts are obtained. For more information about the callback function definition, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data | const void\*    | User-defined data. The Chat SDK only transfers the user data to the callback function `cb` without processing the data. |

**Return values**

| Type | Description                                                  |
| ---- | ------------------------------------------------------------ |
| int  | If `TIM_SUCC` is returned, the API was successfully called. (The callback `cb` is called only when the API returns `TIM_SUCC`.) If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

>?The callback set by this API returns all friend profiles. For more information, see [FriendProfile](https://intl.cloud.tencent.com/document/product/1047/34551)


## TIMFriendshipAddFriend

Adding friends

**Prototype**

```c
TIM_DECL int TIMFriendshipAddFriend(const char* json_add_friend_param, TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter             | Type            | Description                                                  |
| --------------------- | --------------- | ------------------------------------------------------------ |
| json_add_friend_param | const char\*    | JSON string of the API parameter for adding a friend.        |
| cb                    | TIMCommCallback | Callback function for indicating whether a friend is added. For more information about the callback function definition, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data             | const void\*    | User-defined data. The Chat SDK only transfers the user data to the callback function `cb` without processing the data. |

**Return values**

| Type | Description                                                  |
| ---- | ------------------------------------------------------------ |
| int  | If `TIM_SUCC` is returned, the API was successfully called. (The callback `cb` is called only when the API returns `TIM_SUCC`.) If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

>? Friend relationships are classified as two-way friends and one-way friends. For more information, see [Adding friends](https://intl.cloud.tencent.com/document/product/1047/33521).


**Sample**

```c
Json::Value json_add_friend_param;
json_add_friend_param[kTIMFriendshipAddFriendParamIdentifier] = "user4";
json_add_friend_param[kTIMFriendshipAddFriendParamFriendType] = FriendTypeBoth;
json_add_friend_param[kTIMFriendshipAddFriendParamAddSource] = "Windows";
json_add_friend_param[kTIMFriendshipAddFriendParamAddWording] = "I am Iron Man";
int ret = TIMFriendshipAddFriend(json_add_friend_param.toStyledString().c_str(), [](int32_t code, const char* desc, const char* json_params, const void* user_data) {
    if (ERR_SUCC != code) {
        // Failed to add the friend
        return;
    }
}, nullptr);
```


## TIMFriendshipHandleFriendAddRequest

This API is used to process friend requests.

**Prototype**

```c
TIM_DECL int TIMFriendshipHandleFriendAddRequest(const char* json_handle_friend_add_param, TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter                    | Type            | Description                                                  |
| ---------------------------- | --------------- | ------------------------------------------------------------ |
| json_handle_friend_add_param | const char\*    | JSON string of the API parameter for processing friend requests. |
| cb                           | TIMCommCallback | Callback function for indicating whether a friend request is processed. For more information about the callback function definition, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data                    | const void\*    | User-defined data. The Chat SDK only transfers the user data to the callback function `cb` without processing the data. |

**Return values**

| Type | Description                                                  |
| ---- | ------------------------------------------------------------ |
| int  | If `TIM_SUCC` is returned, the API was successfully called. (The callback `cb` is called only when the API returns `TIM_SUCC`.) If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

>?If `kTIMUserProfileAddPermission` is set to `kTIMProfileAddPermission_NeedConfirm` in your profile, you will receive a friend request when someone adds you as a friend, and you can process the request through this API.


**Sample**

```c
Json::Value json_handle_friend_add_param;
json_handle_friend_add_param[kTIMFriendResponeIdentifier] = "user1";
json_handle_friend_add_param[kTIMFriendResponeAction] = ResponseActionAgreeAndAdd;
json_handle_friend_add_param[kTIMFriendResponeRemark] = "I am Captain China";
json_handle_friend_add_param[kTIMFriendResponeGroupName] = "schoolmate";
int ret = TIMFriendshipHandleFriendAddRequest(json_handle_friend_add_param.toStyledString().c_str(), [](int32_t code, const char* desc, const char* json_params, const void* user_data) {

}, nullptr);
```


## TIMFriendshipModifyFriendProfile

This API is used to update a friend's profile (such as remarks).

**Prototype**

```c
TIM_DECL int TIMFriendshipModifyFriendProfile(const char* json_modify_friend_info_param, TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter                     | Type            | Description                                                  |
| ----------------------------- | --------------- | ------------------------------------------------------------ |
| json_modify_friend_info_param | const char\*    | JSON string of the API parameter for updating a friend's profile. |
| cb                            | TIMCommCallback | Callback function for indicating whether a friend's profile is updated. For more information about the callback function definition, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data                     | const void\*    | User-defined data. The Chat SDK only transfers the user data to the callback function `cb` without processing the data. |

**Return values**

| Type | Description                                                  |
| ---- | ------------------------------------------------------------ |
| int  | If `TIM_SUCC` is returned, the API was successfully called. (The callback `cb` is called only when the API returns `TIM_SUCC`.) If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

**Sample**

```c
Json::Value json_modify_friend_profile_item;
json_modify_friend_profile_item[kTIMFriendProfileItemRemark] = "xxxx yyyy";  // Modify the remarks
json_modify_friend_profile_item[kTIMFriendProfileItemGroupNameArray].append("group1"); // Modify the group to which the friend belongs
json_modify_friend_profile_item[kTIMFriendProfileItemGroupNameArray].append("group2");

Json::Value json_modify_friend_profilie_custom;
json_modify_friend_profilie_custom[kTIMFriendProfileCustemStringInfoKey] = "Str";
json_modify_friend_profilie_custom[kTIMFriendProfileCustemStringInfoValue] = "this is changed value";
json_modify_friend_profile_item[kTIMFriendProfileItemCustomStringArray].append(json_modify_friend_profilie_custom); // Modify the value of the custom field `Str` in the friend's profile
```


## TIMFriendshipDeleteFriend

This API is used to delete friends.

**Prototype**

```c
TIM_DECL int TIMFriendshipDeleteFriend(const char* json_delete_friend_param, TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter                | Type            | Description                                                  |
| ------------------------ | --------------- | ------------------------------------------------------------ |
| json_delete_friend_param | const char\*    | JSON string of the API parameter for deleting friends.       |
| cb                       | TIMCommCallback | Callback function for indicating whether a friend is deleted. For more information about the callback function definition, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data                | const void\*    | User-defined data. The Chat SDK only transfers the user data to the callback function `cb` without processing the data. |

**Return values**

| Type | Description                                                  |
| ---- | ------------------------------------------------------------ |
| int  | If `TIM_SUCC` is returned, the API was successfully called. (The callback `cb` is called only when the API returns `TIM_SUCC`.) If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

>?Friend deletion is classified as one-way deletion and two-way deletion. For more information, see [Deleting friends](https://intl.cloud.tencent.com/document/product/1047/33521).


**Sample**

```c
Json::Value json_delete_friend_param;
json_delete_friend_param[kTIMFriendshipDeleteFriendParamIdentifierArray].append("user4");
json_delete_friend_param[kTIMFriendshipDeleteFriendParamFriendType] = FriendTypeSignle;
int ret = TIMFriendshipDeleteFriend(json_delete_friend_param.toStyledString().c_str(), [](int32_t code, const char* desc, const char* json_params, const void* user_data) {
    if (ERR_SUCC != code) {
        // Failed to delete the friend
        return;
    }
}, nullptr);
```


## TIMFriendshipCheckFriendType

This API is used to check the friend type (one-way or two-way).

**Prototype**

```c
TIM_DECL int TIMFriendshipCheckFriendType(const char* json_check_friend_list_param, TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter                    | Type            | Description                                                  |
| ---------------------------- | --------------- | ------------------------------------------------------------ |
| json_check_friend_list_param | const char\*    | JSON string of the API parameter for checking the friend type. |
| cb                           | TIMCommCallback | Callback function for indicating whether the friend type is checked. For more information about the callback function definition, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data                    | const void\*    | User-defined data. The Chat SDK only transfers the user data to the callback function `cb` without processing the data. |

**Return values**

| Type | Description                                                  |
| ---- | ------------------------------------------------------------ |
| int  | If `TIM_SUCC` is returned, the API was successfully called. (The callback `cb` is called only when the API returns `TIM_SUCC`.) If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

>?Developers can use this API to check the friend relationship between the provided `UserID` list and the current account. For more information, see [Verifying friends](https://intl.cloud.tencent.com/document/product/1047/33521).


**Sample**

```c
Json::Value json_check_friend_list_param;
json_check_friend_list_param[kTIMFriendshipCheckFriendTypeParamCheckType] = FriendTypeBoth;
json_check_friend_list_param[kTIMFriendshipCheckFriendTypeParamIdentifierArray].append("user4");
int ret = TIMFriendshipCheckFriendType(json_check_friend_list_param.toStyledString().c_str(), [](int32_t code, const char* desc, const char* json_params, const void* user_data) {

}, nullptr);
```


## TIMFriendshipCreateFriendGroup

This API is used to create a friend list.

**Prototype**

```c
TIM_DECL int TIMFriendshipCreateFriendGroup(const char* json_create_friend_group_param, TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter                      | Type            | Description                                                  |
| ------------------------------ | --------------- | ------------------------------------------------------------ |
| json_create_friend_group_param | const char\*    | JSON string of the API parameter for creating a friend list. |
| cb                             | TIMCommCallback | Callback function for indicating whether a friend list is created. For more information about the callback function definition, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data                      | const void\*    | User-defined data. The Chat SDK only transfers the user data to the callback function `cb` without processing the data. |

**Return values**

| Type | Description                                                  |
| ---- | ------------------------------------------------------------ |
| int  | If `TIM_SUCC` is returned, the API was successfully called. (The callback `cb` is called only when the API returns `TIM_SUCC`.) If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

>?An existing friend list cannot be created.


**Sample**

```c
Json::Value json_create_friend_group_param;
json_create_friend_group_param[kTIMFriendshipCreateFriendGroupParamNameArray].append("Group123");
json_create_friend_group_param[kTIMFriendshipCreateFriendGroupParamIdentifierArray].append("user4");
json_create_friend_group_param[kTIMFriendshipCreateFriendGroupParamIdentifierArray].append("user10");
int ret = TIMFriendshipCreateFriendGroup(json_create_friend_group_param.toStyledString().c_str(), [](int32_t code, const char* desc, const char* json_params, const void* user_data) {
    
}, nullptr);
```


## TIMFriendshipGetFriendGroupList

This API is used to obtain the information about a specified friend list.

**Prototype**

```c
TIM_DECL int TIMFriendshipGetFriendGroupList(const char* json_get_friend_group_list_param, TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter                        | Type            | Description                                                  |
| -------------------------------- | --------------- | ------------------------------------------------------------ |
| json_get_friend_group_list_param | const char\*    | JSON string of the API parameter for obtaining the information about a specified friend list. |
| cb                               | TIMCommCallback | Callback function for indicating whether the friend list information is obtained. For more information about the callback function definition, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data                        | const void\*    | User-defined data. The Chat SDK only transfers the user data to the callback function `cb` without processing the data. |

**Return values**

| Type | Description                                                  |
| ---- | ------------------------------------------------------------ |
| int  | If `TIM_SUCC` is returned, the API was successfully called. (The callback `cb` is called only when the API returns `TIM_SUCC`.) If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

**Sample**

```c
Json::Value json_get_friend_group_list_param;
json_get_friend_group_list_param.append("Group123");
int ret = TIMFriendshipGetFriendGroupList(json_get_friend_group_list_param.toStyledString().c_str(), [](int32_t code, const char* desc, const char* json_params, const void* user_data) {
    
}, nullptr);
```


## TIMFriendshipModifyFriendGroup

This API is used to modify a friend list.

**Prototype**

```c
TIM_DECL int TIMFriendshipModifyFriendGroup(const char* json_modify_friend_group_param, TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter                      | Type            | Description                                                  |
| ------------------------------ | --------------- | ------------------------------------------------------------ |
| json_modify_friend_group_param | const char\*    | JSON string of the API parameter for modifying a friend list. |
| cb                             | TIMCommCallback | Callback function for indicating whether a friend list is modified. For more information about the callback function definition, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data                      | const void\*    | User-defined data. The Chat SDK only transfers the user data to the callback function `cb` without processing the data. |

**Return values**

| Type | Description                                                  |
| ---- | ------------------------------------------------------------ |
| int  | If `TIM_SUCC` is returned, the API was successfully called. (The callback `cb` is called only when the API returns `TIM_SUCC`.) If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

**Sample**

```c
Json::Value json_modify_friend_group_param;
json_modify_friend_group_param[kTIMFriendshipModifyFriendGroupParamName] = "Group123";
json_modify_friend_group_param[kTIMFriendshipModifyFriendGroupParamNewName] = "GroupNewName";
json_modify_friend_group_param[kTIMFriendshipModifyFriendGroupParamDeleteIdentifierArray].append("user4");
json_modify_friend_group_param[kTIMFriendshipModifyFriendGroupParamAddIdentifierArray].append("user9");
json_modify_friend_group_param[kTIMFriendshipModifyFriendGroupParamAddIdentifierArray].append("user5");
int ret = TIMFriendshipModifyFriendGroup(json_modify_friend_group_param.toStyledString().c_str(), [](int32_t code, const char* desc, const char* json_params, const void* user_data) {
    
}, nullptr);
```


## TIMFriendshipDeleteFriendGroup

This API is used to delete a friend list.

**Prototype**

```c
TIM_DECL int TIMFriendshipDeleteFriendGroup(const char* json_delete_friend_group_param, TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter                      | Type            | Description                                                  |
| ------------------------------ | --------------- | ------------------------------------------------------------ |
| json_delete_friend_group_param | const char\*    | JSON string of the API parameter for deleting a friend list. |
| cb                             | TIMCommCallback | Callback function for indicating whether a friend list is deleted. For more information about the callback function definition, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data                      | const void\*    | User-defined data. The Chat SDK only transfers the user data to the callback function `cb` without processing the data. |

**Return values**

| Type | Description                                                  |
| ---- | ------------------------------------------------------------ |
| int  | If `TIM_SUCC` is returned, the API was successfully called. (The callback `cb` is called only when the API returns `TIM_SUCC`.) If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

**Sample**

```c
Json::Value json_delete_friend_group_param;
json_delete_friend_group_param.append("GroupNewName");
int ret = TIMFriendshipDeleteFriendGroup(json_delete_friend_group_param.toStyledString().c_str(), [](int32_t code, const char* desc, const char* json_params, const void* user_data) {
    
}, nullptr);
```


## TIMFriendshipAddToBlackList

This API is used to add a specified user to the blocklist.

**Prototype**

```c
TIM_DECL int TIMFriendshipAddToBlackList(const char* json_add_to_blacklist_param, TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter                   | Type            | Description                                                  |
| --------------------------- | --------------- | ------------------------------------------------------------ |
| json_add_to_blacklist_param | const char\*    | JSON string of the API parameter for adding a specified user to the blocklist. |
| cb                          | TIMCommCallback | Callback function for indicating whether a specified user is added to the blocklist. For more information about the callback function definition, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data                   | const void\*    | User-defined data. The Chat SDK only transfers the user data to the callback function `cb` without processing the data. |

**Return values**

| Type | Description                                                  |
| ---- | ------------------------------------------------------------ |
| int  | If `TIM_SUCC` is returned, the API was successfully called. (The callback `cb` is called only when the API returns `TIM_SUCC`.) If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

**Sample**

```c
Json::Value json_add_to_blacklist_param;
json_add_to_blacklist_param.append("user5");
json_add_to_blacklist_param.append("user10");
int ret = TIMFriendshipAddToBlackList(json_add_to_blacklist_param.toStyledString().c_str(), [](int32_t code, const char* desc, const char* json_params, const void* user_data) {
    
}, nullptr);
```


## TIMFriendshipGetBlackList

This API is used to obtain the blocklist.

**Prototype**

```c
TIM_DECL int TIMFriendshipGetBlackList(TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type            | Description                                                  |
| --------- | --------------- | ------------------------------------------------------------ |
| cb        | TIMCommCallback | Callback function for indicating whether the blocklist is obtained. For more information about the callback function definition, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data | const void\*    | User-defined data. The Chat SDK only transfers the user data to the callback function `cb` without processing the data. |

**Return values**

| Type | Description                                                  |
| ---- | ------------------------------------------------------------ |
| int  | If `TIM_SUCC` is returned, the API was successfully called. (The callback `cb` is called only when the API returns `TIM_SUCC`.) If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

## TIMFriendshipDeleteFromBlackList

This API is used to delete a specified user from the blocklist.

**Prototype**

```c
TIM_DECL int TIMFriendshipDeleteFromBlackList(const char* json_delete_from_blacklist_param, TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter                        | Type            | Description                                                  |
| -------------------------------- | --------------- | ------------------------------------------------------------ |
| json_delete_from_blacklist_param | const char\*    | JSON string of the API parameter for deleting a specified user from the blocklist. |
| cb                               | TIMCommCallback | Callback function for indicating whether a specified user is deleted from the blocklist. For more information about the callback function definition, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data                        | const void\*    | User-defined data. The Chat SDK only transfers the user data to the callback function `cb` without processing the data. |

**Return values**

| Type | Description                                                  |
| ---- | ------------------------------------------------------------ |
| int  | If `TIM_SUCC` is returned, the API was successfully called. (The callback `cb` is called only when the API returns `TIM_SUCC`.) If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

**Sample**

```c
Json::Value json_delete_from_blacklist_param;
json_delete_from_blacklist_param.append("user5");
json_delete_from_blacklist_param.append("user10");
int ret = TIMFriendshipDeleteFromBlackList(json_delete_from_blacklist_param.toStyledString().c_str(), [](int32_t code, const char* desc, const char* json_params, const void* user_data) {
    
}, nullptr);
```


## TIMFriendshipGetPendencyList

This API is used to obtain the pending friend request information list.

**Prototype**

```c
TIM_DECL int TIMFriendshipGetPendencyList(const char* json_get_pendency_list_param, TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter                    | Type            | Description                                                  |
| ---------------------------- | --------------- | ------------------------------------------------------------ |
| json_get_pendency_list_param | const char\*    | JSON string of the API parameter for obtaining the pending friend request information list. |
| cb                           | TIMCommCallback | Callback function for indicating whether the pending information list is obtained. For more information about the callback function definition, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data                    | const void\*    | User-defined data. The Chat SDK only transfers the user data to the callback function `cb` without processing the data. |

**Return values**

| Type | Description                                                  |
| ---- | ------------------------------------------------------------ |
| int  | If `TIM_SUCC` is returned, the API was successfully called. (The callback `cb` is called only when the API returns `TIM_SUCC`.) If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

>?Pending friend request information refers to friend requests that are not handled. For example, a developer sends a friend request to a user, but the user does not handle the request. Alternatively, a user sends a friend request to the developer, but the developer does not handle the request.


**Sample**

```c
Json::Value json_get_pendency_list_param;
json_get_pendency_list_param[kTIMFriendshipGetPendencyListParamType] = FriendPendencyTypeBoth;
json_get_pendency_list_param[kTIMFriendshipGetPendencyListParamStartSeq] = 0;
int ret = TIMFriendshipGetPendencyList(json_get_pendency_list_param.toStyledString().c_str(), [](int32_t code, const char* desc, const char* json_params, const void* user_data) {
    
}, nullptr);
```


## TIMFriendshipDeletePendency

This API is used to delete the specified pending friend request information.

**Prototype**

```c
TIM_DECL int TIMFriendshipDeletePendency(const char* json_delete_pendency_param, TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter                  | Type            | Description                                                  |
| -------------------------- | --------------- | ------------------------------------------------------------ |
| json_delete_pendency_param | const char\*    | JSON string of the API parameter for deleting the specified pending friend request information. |
| cb                         | TIMCommCallback | Callback function for indicating whether the specified pending information is deleted. For more information about the callback function definition, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data                  | const void\*    | User-defined data. The Chat SDK only transfers the user data to the callback function `cb` without processing the data. |

**Return values**

| Type | Description                                                  |
| ---- | ------------------------------------------------------------ |
| int  | If `TIM_SUCC` is returned, the API was successfully called. (The callback `cb` is called only when the API returns `TIM_SUCC`.) If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

**Sample**

```c
Json::Value json_delete_pendency_param;
json_delete_pendency_param[kTIMFriendshipDeletePendencyParamType] = FriendPendencyTypeComeIn;
json_delete_pendency_param[kTIMFriendshipDeletePendencyParamIdentifierArray].append("user1");
int ret = TIMFriendshipDeletePendency(json_delete_pendency_param.toStyledString().c_str(), [](int32_t code, const char* desc, const char* json_params, const void* user_data) {
    
}, nullptr);
```


## TIMFriendshipReportPendencyReaded

This API is used to report that pending friend request information has been read.

**Prototype**

```c
TIM_DECL int TIMFriendshipReportPendencyReaded(uint64_t time_stamp, TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter  | Type            | Description                                                  |
| ---------- | --------------- | ------------------------------------------------------------ |
| time_stamp | uint64_t        | Timestamp for reporting that the pending information has been read. |
| cb         | TIMCommCallback | Callback function for indicating whether the pending information read state is reported. For more information about the callback function definition, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data  | const void\*    | User-defined data. The Chat SDK only transfers the user data to the callback function `cb` without processing the data. |

**Return values**

| Type | Description                                                  |
| ---- | ------------------------------------------------------------ |
| int  | If `TIM_SUCC` is returned, the API was successfully called. (The callback `cb` is called only when the API returns `TIM_SUCC`.) If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

**Sample**

```c
TIMFriendshipReportPendencyReaded(0, [](int32_t code, const char* desc, const char* json_param, const void* user_data) {

}, nullptr);

// `json_param` is an empty string. Check `code` to determine the result.
```


## TIMFriendshipSearchFriends

This API is used to search for friends. (This API is supported only in SDK 5.4.666 or later, and you need to purchase the Ultimate edition to use this API.)

**Prototype**

```c
TIM_DECL int TIMFriendshipSearchFriends(const char *json_search_friends_param, TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter                 | Type            | Description                                                  |
| ------------------------- | --------------- | ------------------------------------------------------------ |
| json_search_friends_param | const char\*    | Keywords and domains for friend searching. For more information, see [FriendSearchParam](https://intl.cloud.tencent.com/document/product/1047/34551). |
| cb                        | TIMCommCallback | Callback function for searching for friends. For more information about the callback function definition, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data                 | const void\*    | User-defined data. The Chat SDK only transfers the user data to the callback function `cb` without processing the data. |

**Return values**

| Type | Description                                                  |
| ---- | ------------------------------------------------------------ |
| int  | If `TIM_SUCC` is returned, the API was successfully called. (The callback `cb` is called only when the API returns `TIM_SUCC`.) If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

**Sample**

```c
Json::Object json_obj;

Json::Array json_keyword_list;
json_keyword_list.push_back("98826");
json_obj[kTIMFriendshipSearchParamKeywordList] = json_keyword_list;

Json::Array json_search_field_list;
json_search_field_list.push_back(kTIMFriendshipSearchFieldKey_Identifier);
json_obj[kTIMFriendshipSearchParamSearchFieldList] = json_search_field_list;
TIMFriendshipSearchFriends(json_obj.toStyledString().c_str(), [](int32_t code, const char* desc, const char* json_param, const void* user_data) {

}, nullptr);

The JSON string obtained by `json_obj.toStyledString().c_str()` is as follows:
{
    "friendship_search_param_keyword_list": ["98826"],
    "friendship_search_param_search_field_list": [1]
}

// Example of the callback `json_param`. For details on JSON keys, see [FriendProfile](TIMCloudDef.h).
[{
"friend_profile_add_source": "AddSource_Type_contact",
"friend_profile_add_time": 1620786162,
"friend_profile_add_wording": "work together",
"friend_profile_custom_string_array": [{
    "friend_profile_custom_string_info_key": "Tag_Profile_Custom_Str",
    "friend_profile_custom_string_info_value": "test3-lamar-value"
}],
"friend_profile_group_name_array": ["friend1"],
"friend_profile_identifier": "98826",
"friend_profile_remark": "shoujihao",
"friend_profile_user_profile": {
    "user_profile_add_permission": 1,
    "user_profile_birthday": 2000,
    "user_profile_custom_string_array": [{
        "user_profile_custom_string_info_key": "Tag_Profile_Custom_Str",
        "user_profile_custom_string_info_value": "test3-lamar-value"
    }],
    "user_profile_face_url": "test1-www.google.com",
    "user_profile_gender": 2,
    "user_profile_identifier": "98826",
    "user_profile_language": 1000,
    "user_profile_level": 3000,
    "user_profile_location": "Shenzhen",
    "user_profile_nick_name": "test change8888",
    "user_profile_role": 4000,
    "user_profile_self_signature": "1111111"
}
}]
```


## TIMFriendshipGetFriendsInfo

This API is used to get friend information.

**Prototype**

```c
TIM_DECL int TIMFriendshipGetFriendsInfo(const char *json_get_friends_info_param,  TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter                   | Type            | Description                                                  |
| --------------------------- | --------------- | ------------------------------------------------------------ |
| json_get_friends_info_param | const char\*    | List of user IDs whose data is to be obtained.               |
| cb                          | TIMCommCallback | Callback function for obtaining friend information. For more information about the callback function definition, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data                   | const void\*    | User-defined data. The Chat SDK only transfers the user data to the callback function `cb` without processing the data. |

**Return values**

| Type | Description                                                  |
| ---- | ------------------------------------------------------------ |
| int  | If `TIM_SUCC` is returned, the API was successfully called. (The callback `cb` is called only when the API returns `TIM_SUCC`.) If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

**Sample**

```c
Json::Array json_array;
json_array.append("98826");
TIMFriendshipGetFriendsInfo(json_array.toStyledString().c_str(), [](int32_t code, const char* desc, const char* json_param, const void* user_data) {
    printf("GetFriendsInfo code:%d|desc:%s|json_param %s\r\n", code, desc, json_param);
}, nullptr);

The JSON string obtained by json_array.toStyledString().c_str()` is as follows:
["98826"]

// Example of the callback `json_param`. For details on JSON keys, see [FriendInfoGetResult](TIMCloudDef.h).

[{
"friendship_friend_info_get_result_error_code": 0,
"friendship_friend_info_get_result_error_message": "OK",
"friendship_friend_info_get_result_field_info": {
    "friend_profile_add_source": "AddSource_Type_contact",
    "friend_profile_add_time": 1620786162,
    "friend_profile_add_wording": "work together",
    "friend_profile_custom_string_array": [{
        "friend_profile_custom_string_info_key": "Tag_Profile_Custom_Str",
        "friend_profile_custom_string_info_value": "test3-lamar-value"
    }],
    "friend_profile_group_name_array": ["friend1"],
    "friend_profile_identifier": "98826",
    "friend_profile_remark": "shoujihao",
    "friend_profile_user_profile": {
        "user_profile_add_permission": 1,
        "user_profile_birthday": 2000,
        "user_profile_custom_string_array": [{
            "user_profile_custom_string_info_key": "Tag_Profile_Custom_Str",
            "user_profile_custom_string_info_value": "test3-lamar-value"
        }],
        "user_profile_face_url": "test1-www.google.com",
        "user_profile_gender": 2,
        "user_profile_identifier": "98826",
        "user_profile_language": 1000,
        "user_profile_level": 3000,
        "user_profile_location": "shenzhen",
        "user_profile_nick_name": "test change8888",
        "user_profile_role": 4000,
        "user_profile_self_signature": "1111111"
    }
},
"friendship_friend_info_get_result_relation_type": 3,
"friendship_friend_info_get_result_userid": "98826"
]
```
