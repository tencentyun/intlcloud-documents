For more information about relationship chains, see [Introduction to the Relationship Chain System](https://intl.cloud.tencent.com/document/product/1047/33521).

## TIMFriendshipGetFriendProfileList

This API is used to obtain the friend list.

**Prototype**

```c
TIM_DECL int TIMFriendshipGetFriendProfileList(TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| cb | TIMCommCallback | Callback for notifying whether the friend list is obtained. For more information about the callback function definition, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data | const void\* | User-defined data. The IM SDK only transfers the user data to the callback function cb without processing the data. |

**Return values**

| Type | Description |
|-----|-----|
| int | If TIM_SUCC is returned, the API was successfully called. (The callback cb is called only when the API returns TIM_SUCC.) If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

>?The callback set by this API returns all friend profiles. For more information, see [FriendProfile](https://intl.cloud.tencent.com/document/product/1047/34551).


## TIMFriendshipAddFriend

This API is used to add friends.

**Prototype**

```c
TIM_DECL int TIMFriendshipAddFriend(const char* json_add_friend_param, TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| json_add_friend_param | const char\* | JSON string of the API parameter for adding a friend. |
| cb | TIMCommCallback | Callback for notifying whether a friend is added. For more information about the callback function definition, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data | const void\* | User-defined data. The IM SDK only transfers the user data to the callback function cb without processing the data. |

**Return values**

| Type | Description |
|-----|-----|
| int | If TIM_SUCC is returned, the API was successfully called. (The callback cb is called only when the API returns TIM_SUCC.) If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

>?Friend relationships are classified as two-way friends and one-way friends. For more information, see [Adding friends](https://intl.cloud.tencent.com/document/product/1047/33521).


**Example**

```c
Json::Value json_add_friend_param;
json_add_friend_param[kTIMFriendshipAddFriendParamIdentifier] = "user4";
json_add_friend_param[kTIMFriendshipAddFriendParamFriendType] = FriendTypeBoth;
json_add_friend_param[kTIMFriendshipAddFriendParamAddSource] = "Windows";
json_add_friend_param[kTIMFriendshipAddFriendParamAddWording] = "I am Iron Man";
int ret = TIMFriendshipAddFriend(json_add_friend_param.toStyledString().c_str(), [](int32_t code, const char* desc, const char* json_params, const void* user_data) {
    if (ERR_SUCC != code) {
        // Failed to add a friend.
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

| Parameter | Type | Description |
|-----|-----|-----|
| json_handle_friend_add_param | const char\* | JSON string of the API parameter for processing friend requests. |
| cb | TIMCommCallback | Callback for notifying whether a friend request is processed. For more information about the callback function definition, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data | const void\* | User-defined data. The IM SDK only transfers the user data to the callback function cb without processing the data. |

**Return values**

| Type | Description |
|-----|-----|
| int | If TIM_SUCC is returned, the API was successfully called. (The callback cb is called only when the API returns TIM_SUCC.) If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

>?If `kTIMUserProfileAddPermission` is set to `kTIMProfileAddPermission_NeedConfirm` in your profile, you will receive a friend request when someone adds you as a friend. You can process the request through this API.


**Example**

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

| Parameter | Type | Description |
|-----|-----|-----|
| json_modify_friend_info_param | const char\* | JSON string of the API parameter for updating a friend's profile. |
| cb | TIMCommCallback | Callback for notifying whether a friend's profile is updated. For more information about the callback function definition, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data | const void\* | User-defined data. The IM SDK only transfers the user data to the callback function cb without processing the data. |

**Return values**

| Type | Description |
|-----|-----|
| int | If TIM_SUCC is returned, the API was successfully called. (The callback cb is called only when the API returns TIM_SUCC.) If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

**Example**

```c
Json::Value json_modify_friend_profile_item;
json_modify_friend_profile_item[kTIMFriendProfileItemRemark] = "xxxx yyyy";  // Modify the remarks.
json_modify_friend_profile_item[kTIMFriendProfileItemGroupNameArray].append("group1"); // Modify the group to which the friend belongs.
json_modify_friend_profile_item[kTIMFriendProfileItemGroupNameArray].append("group2");

Json::Value json_modify_friend_profilie_custom;
json_modify_friend_profilie_custom[kTIMFriendProfileCustemStringInfoKey] = "Str";
json_modify_friend_profilie_custom[kTIMFriendProfileCustemStringInfoValue] = "this is changed value";
json_modify_friend_profile_item[kTIMFriendProfileItemCustomStringArray].append(json_modify_friend_profilie_custom); // Modify the value of the custom field "Str" in the friend's profile.
```


## TIMFriendshipDeleteFriend

This API is used to delete friends.

**Prototype**

```c
TIM_DECL int TIMFriendshipDeleteFriend(const char* json_delete_friend_param, TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| json_delete_friend_param | const char\* | JSON string of the API parameter for deleting friends. |
| cb | TIMCommCallback | Callback for notifying whether a friend is deleted. For more information about the callback function definition, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data | const void\* | User-defined data. The IM SDK only transfers the user data to the callback function cb without processing the data. |

**Return values**

| Type | Description |
|-----|-----|
| int | If TIM_SUCC is returned, the API was successfully called. (The callback cb is called only when the API returns TIM_SUCC.) If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

>?Friend deletion is classified as one-way deletion and two-way deletion. For more information, see [Deleting friends](https://intl.cloud.tencent.com/document/product/1047/33521).


**Example**

```c
Json::Value json_delete_friend_param;
json_delete_friend_param[kTIMFriendshipDeleteFriendParamIdentifierArray].append("user4");
json_delete_friend_param[kTIMFriendshipDeleteFriendParamFriendType] = FriendTypeSignle;
int ret = TIMFriendshipDeleteFriend(json_delete_friend_param.toStyledString().c_str(), [](int32_t code, const char* desc, const char* json_params, const void* user_data) {
    if (ERR_SUCC != code) {
        // Failed to delete a friend.
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

| Parameter | Type | Description |
|-----|-----|-----|
| json_check_friend_list_param | const char\* | JSON string of the API parameter for checking the friend type. |
| cb | TIMCommCallback | Callback for notifying whether the friend type is checked. For more information about the callback function definition, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data | const void\* | User-defined data. The IM SDK only transfers the user data to the callback function cb without processing the data. |

**Return values**

| Type | Description |
|-----|-----|
| int | If TIM_SUCC is returned, the API was successfully called. (The callback cb is called only when the API returns TIM_SUCC.) If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

>?Developers can use this API to check the friend relationship between the provided `UserID` list and the current account. For more information, see [Verifying friends](https://intl.cloud.tencent.com/document/product/1047/33521).


**Example**

```c
Json::Value json_check_friend_list_param;
json_check_friend_list_param[kTIMFriendshipCheckFriendTypeParamCheckType] = FriendTypeBoth;
json_check_friend_list_param[kTIMFriendshipCheckFriendTypeParamIdentifierArray].append("user4");
int ret = TIMFriendshipCheckFriendType(json_check_friend_list_param.toStyledString().c_str(), [](int32_t code, const char* desc, const char* json_params, const void* user_data) {

}, nullptr);
```


## TIMFriendshipCreateFriendGroup

This API is used to create a friend group.

**Prototype**

```c
TIM_DECL int TIMFriendshipCreateFriendGroup(const char* json_create_friend_group_param, TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| json_create_friend_group_param | const char\* | JSON string of the API parameter for creating a friend group. |
| cb | TIMCommCallback | Callback for notifying whether a friend group is created. For more information about the callback function definition, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data | const void\* | User-defined data. The IM SDK only transfers the user data to the callback function cb without processing the data. |

**Return values**

| Type | Description |
|-----|-----|
| int | If TIM_SUCC is returned, the API was successfully called. (The callback cb is called only when the API returns TIM_SUCC.) If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

>?You cannot create a group that already exists.


**Example**

```c
Json::Value json_create_friend_group_param;
json_create_friend_group_param[kTIMFriendshipCreateFriendGroupParamNameArray].append("Group123");
json_create_friend_group_param[kTIMFriendshipCreateFriendGroupParamIdentifierArray].append("user4");
json_create_friend_group_param[kTIMFriendshipCreateFriendGroupParamIdentifierArray].append("user10");
int ret = TIMFriendshipCreateFriendGroup(json_create_friend_group_param.toStyledString().c_str(), [](int32_t code, const char* desc, const char* json_params, const void* user_data) {
    
}, nullptr);
```


## TIMFriendshipGetFriendGroupList

This API is used to obtain the information about a specified friend group.

**Prototype**

```c
TIM_DECL int TIMFriendshipGetFriendGroupList(const char* json_get_friend_group_list_param, TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| json_get_friend_group_list_param | const char\* | JSON string of the API parameter for obtaining the information about a specified friend group. |
| cb | TIMCommCallback | Callback for notifying whether friend group information is obtained. For more information about the callback function definition, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550).|
| user_data | const void\* | User-defined data. The IM SDK only transfers the user data to the callback function cb without processing the data. |

**Return values**

| Type | Description |
|-----|-----|
| int | If TIM_SUCC is returned, the API was successfully called. (The callback cb is called only when the API returns TIM_SUCC.) If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

**Example**

```c
Json::Value json_get_friend_group_list_param;
json_get_friend_group_list_param.append("Group123");
int ret = TIMFriendshipGetFriendGroupList(json_get_friend_group_list_param.toStyledString().c_str(), [](int32_t code, const char* desc, const char* json_params, const void* user_data) {
    
}, nullptr);
```


## TIMFriendshipModifyFriendGroup

This API is used to modify a friend group.

**Prototype**

```c
TIM_DECL int TIMFriendshipModifyFriendGroup(const char* json_modify_friend_group_param, TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| json_modify_friend_group_param | const char\* | JSON string of the API parameter for modifying a friend group. |
| cb | TIMCommCallback | Callback for notifying whether a friend group is modified. For more information about the callback function definition, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data | const void\* | User-defined data. The IM SDK only transfers the user data to the callback function cb without processing the data. |

**Return values**

| Type | Description |
|-----|-----|
| int | If TIM_SUCC is returned, the API was successfully called. (The callback cb is called only when the API returns TIM_SUCC.) If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

**Example**

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

This API is used to delete a friend group.

**Prototype**

```c
TIM_DECL int TIMFriendshipDeleteFriendGroup(const char* json_delete_friend_group_param, TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| json_delete_friend_group_param | const char\* | JSON string of the API parameter for deleting a friend group. |
| cb | TIMCommCallback | Callback for notifying whether a friend group is deleted. For more information about the callback function definition, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data | const void\* | User-defined data. The IM SDK only transfers the user data to the callback function cb without processing the data. |

**Return values**

| Type | Description |
|-----|-----|
| int | If TIM_SUCC is returned, the API was successfully called. (The callback cb is called only when the API returns TIM_SUCC.) If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

**Example**

```c
Json::Value json_delete_friend_group_param;
json_delete_friend_group_param.append("GroupNewName");
int ret = TIMFriendshipDeleteFriendGroup(json_delete_friend_group_param.toStyledString().c_str(), [](int32_t code, const char* desc, const char* json_params, const void* user_data) {
    
}, nullptr);
```


## TIMFriendshipAddToBlackList

This API is used to add a specified user to the blacklist.

**Prototype**

```c
TIM_DECL int TIMFriendshipAddToBlackList(const char* json_add_to_blacklist_param, TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| json_add_to_blacklist_param | const char\* | JSON string of the API parameter for adding a specified user to the blacklist. |
| cb | TIMCommCallback | Callback for notifying whether a specified user is added to the blacklist. For more information about the callback function definition, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data | const void\* | User-defined data. The IM SDK only transfers the user data to the callback function cb without processing the data. |

**Return values**

| Type | Description |
|-----|-----|
| int | If TIM_SUCC is returned, the API was successfully called. (The callback cb is called only when the API returns TIM_SUCC.) If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

**Example**

```c
Json::Value json_add_to_blacklist_param;
json_add_to_blacklist_param.append("user5");
json_add_to_blacklist_param.append("user10");
int ret = TIMFriendshipAddToBlackList(json_add_to_blacklist_param.toStyledString().c_str(), [](int32_t code, const char* desc, const char* json_params, const void* user_data) {
    
}, nullptr);
```


## TIMFriendshipGetBlackList

This API is used to obtain the blacklist.

**Prototype**

```c
TIM_DECL int TIMFriendshipGetBlackList(TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| cb | TIMCommCallback | Callback for notifying whether the blacklist is obtained. For more information about the callback function definition, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data | const void\* | User-defined data. The IM SDK only transfers the user data to the callback function cb without processing the data. |

**Return values**

| Type | Description |
|-----|-----|
| int | If TIM_SUCC is returned, the API was successfully called. (The callback cb is called only when the API returns TIM_SUCC.) If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

## TIMFriendshipDeleteFromBlackList

This API is used to delete a specified user from the blacklist.

**Prototype**

```c
TIM_DECL int TIMFriendshipDeleteFromBlackList(const char* json_delete_from_blacklist_param, TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| json_delete_from_blacklist_param | const char\* | JSON string of the API parameter for deleting a specified user from the blacklist. |
| cb | TIMCommCallback | Callback for notifying whether a specified user is deleted from the blacklist. For more information about the callback function definition, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data | const void\* | User-defined data. The IM SDK only transfers the user data to the callback function cb without processing the data. |

**Return values**

| Type | Description |
|-----|-----|
| int | If TIM_SUCC is returned, the API was successfully called. (The callback cb is called only when the API returns TIM_SUCC.) If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

**Example**

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

| Parameter | Type | Description |
|-----|-----|-----|
| json_get_pendency_list_param | const char\* | JSON string of the API parameter for obtaining the pending friend request information list. |
| cb | TIMCommCallback | Callback for notifying whether the pending information list is obtained. For more information about the callback function definition, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data | const void\* | User-defined data. The IM SDK only transfers the user data to the callback function cb without processing the data. |

**Return values**

| Type | Description |
|-----|-----|
| int | If TIM_SUCC is returned, the API was successfully called. (The callback cb is called only when the API returns TIM_SUCC.) If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

>?Pending friend request information refers to friend requests that are not handled. For example, a developer sends a friend request to a user, but the user does not handle the request. Alternatively, a user sends a friend request to the developer, but the developer does not handle the request.


**Example**

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

| Parameter | Type | Description |
|-----|-----|-----|
| json_delete_pendency_param | const char\* | JSON string of the API parameter for deleting the specified pending friend request information. |
| cb | TIMCommCallback | Callback for notifying whether the specified pending information is deleted. For more information about the callback function definition, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data | const void\* | User-defined data. The IM SDK only transfers the user data to the callback function cb without processing the data. |

**Return values**

| Type | Description |
|-----|-----|
| int | If TIM_SUCC is returned, the API was successfully called. (The callback cb is called only when the API returns TIM_SUCC.) If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

**Example**

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

| Parameter | Type | Description |
|-----|-----|-----|
| time_stamp | uint64_t | Timestamp for reporting that the pending information has been read. |
| cb | TIMCommCallback | Callback for notifying whether the pending information read state is reported. For more information about the callback function definition, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data | const void\* | User-defined data. The IM SDK only transfers the user data to the callback function cb without processing the data. |

**Return values**

| Type | Description |
|-----|-----|
| int | If TIM_SUCC is returned, the API was successfully called. (The callback cb is called only when the API returns TIM_SUCC.) If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |


