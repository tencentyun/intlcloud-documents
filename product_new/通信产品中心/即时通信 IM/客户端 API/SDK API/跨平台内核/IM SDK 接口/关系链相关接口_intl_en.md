For the information on relationship chains, see [Introduction to the Relationship Chain System](https://intl.cloud.tencent.com/document/product/1047/33521#.E5.85.B3.E7.B3.BB.E9.93.BE.E7.B3.BB.E7.BB.9F.E7.AE.80.E4.BB.8B).

## TIMFriendshipGetFriendProfileList

Obtains the friend list.

**Prototype**

```c
TIM_DECL int TIMFriendshipGetFriendProfileList(TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| cb | TIMCommCallback | The callback for checking whether obtaining the friend list succeeded or failed. For the definition of the callback function, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550#timcommcallback).  |
| user_data | const void\* | User-defined data. The IM SDK is only responsible for returning the user data to the callback function cb without any processing. |

**Returned value**

| Type | Description |
|-----|-----|
| int | If TIM_SUCC is returned, the API is invoked successfully (the callback cb will be invoked only when the API returns TIM_SUCC.) If other values than this are returned, the API failed to be invoked. For the definition of each returned value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551#timresult). |

> Through the callback, this API returns all [FriendProfile](https://intl.cloud.tencent.com/document/product/1047/34551#friendprofile) friend profiles.


## TIMFriendshipAddFriend

Adds a friend.

**Prototype**

```c
TIM_DECL int TIMFriendshipAddFriend(const char* json_add_friend_param, TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| json_add_friend_param | const char\* | The JSON parameter string of the API for adding a friend. |
| cb | TIMCommCallback | The callback for checking whether adding the friend succeeded or failed. For the definition of the callback function, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550#timcommcallback). |
| user_data | const void\* | User-defined data. The IM SDK is only responsible for returning the user data to the callback function cb without any processing. |

**Returned value**

| Type | Description |
|-----|-----|
| int | If TIM_SUCC is returned, the API is invoked successfully (the callback cb will be invoked only when the API returns TIM_SUCC). If other values than this are returned, the API failed to be invoked. For the definition of each returned value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551#timresult). |

> Friendships are divided into one-way and two-way friendships. For details, see [Adding a Friend](https://intl.cloud.tencent.com/document/product/1047/33521#.E6.B7.BB.E5.8A.A0.E5.A5.BD.E5.8F.8B).


**Example**

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

Processes a friend request.

**Prototype**

```c
TIM_DECL int TIMFriendshipHandleFriendAddRequest(const char* json_handle_friend_add_param, TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| json_handle_friend_add_param | const char\* | The JSON parameter string of the API for processing friend requests. |
| cb | TIMCommCallback | The callback for checking whether processing the friend request succeeded or failed. For the definition of the callback function, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550#timcommcallback). |
| user_data | const void\* | User-defined data. The IM SDK is only responsible for returning the user data to the callback function cb without any processing. |

**Returned value**

| Type | Description |
|-----|-----|
| int | If TIM_SUCC is returned, the API is invoked successfully (the callback cb will be invoked only when the API returns TIM_SUCC). If other values than this are returned, the API failed to be invoked. For the definition of each returned value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551#timresult). |

> If `kTIMUserProfileAddPermission` is set to `kTIMProfileAddPermission_NeedConfirm` in your profile, you will receive a friend request when someone requests to friend you. In this case, you can process the request through this API.


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

Updates a friend’s profile (such as remarks).

**Prototype**

```c
TIM_DECL int TIMFriendshipModifyFriendProfile(const char* json_modify_friend_info_param, TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| json_modify_friend_info_param | const char\* | The JSON parameter string of the API for updating a friend’s profile. |
| cb | TIMCommCallback | The callback for checking whether updating the friend’s profile succeeded or failed. For the definition of the callback function, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550#timcommcallback). |
| user_data | const void\* | User-defined data. The IM SDK is only responsible for returning the user data to the callback function cb without any processing. |

**Returned value**

| Type | Description |
|-----|-----|
| int | If TIM_SUCC is returned, the API is invoked successfully (the callback cb will be invoked only when the API returns TIM_SUCC). If other values than this are returned, the API failed to be invoked. For the definition of each returned value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551#timresult). |

**Example**

```c
Json::Value json_modify_friend_profile_item;
json_modify_friend_profile_item[kTIMFriendProfileItemRemark] = "xxxx yyyy";  // Modify the remarks
json_modify_friend_profile_item[kTIMFriendProfileItemGroupNameArray].append("group1"); // Change the friend’s belonging group
json_modify_friend_profile_item[kTIMFriendProfileItemGroupNameArray].append("group2");

Json::Value json_modify_friend_profilie_custom;
json_modify_friend_profilie_custom[kTIMFriendProfileCustemStringInfoKey] = "Str";
json_modify_friend_profilie_custom[kTIMFriendProfileCustemStringInfoValue] = "this is changed value";
json_modify_friend_profile_item[kTIMFriendProfileItemCustomStringArray].append(json_modify_friend_profilie_custom); // Change the value of the "St" custom field in the friend’s profile.
```


## TIMFriendshipDeleteFriend

Deletes a friend.

**Prototype**

```c
TIM_DECL int TIMFriendshipDeleteFriend(const char* json_delete_friend_param, TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| json_delete_friend_param | const char\* | The JSON parameter string of the API for deleting a friend. |
| cb | TIMCommCallback | The callback for checking  whether deleting the friend succeeded or failed. For the definition of the callback function, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550#timcommcallback). |
| user_data | const void\* | User-defined data. The IM SDK is only responsible for returning the user data to the callback function cb without any processing. |

**Returned value**

| Type | Description |
|-----|-----|
| int | If TIM_SUCC is returned, the API is invoked successfully (the callback cb will be invoked only when the API returns TIM_SUCC). If other values than this are returned, the API failed to be invoked. For the definition of each returned value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551#timresult). |

> Friend deletion is divided into one-way deletion and two-way deletion. For details, see [Deleting a Friend](https://intl.cloud.tencent.com/document/product/1047/33521#.E5.88.A0.E9.99.A4.E5.A5.BD.E5.8F.8B).


**Example**

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

Detects the friend type (one-way or two-way).

**Prototype**

```c
TIM_DECL int TIMFriendshipCheckFriendType(const char* json_check_friend_list_param, TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| json_check_friend_list_param | const char\* | The JSON parameter string of the API for detecting the friend type. |
| cb | TIMCommCallback | The callback for checking whether detecting the friend type succeeded or failed. For the definition of the callback function, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550#timcommcallback). |
| user_data | const void\* | User-defined data. The IM SDK is only responsible for returning the user data to the callback function cb without any processing. |

**Returned value**

| Type | Description |
|-----|-----|
| int | If TIM_SUCC is returned, the API is invoked successfully (the callback cb will be invoked only when the API returns TIM_SUCC). If other values than this are returned, the API failed to be invoked. For the definition of each returned value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551#timresult). |

> The developer can use this API to check the friendship between a specified `UserID` list and the current account. For information on detecting friends, see [Detecting Friends](https://intl.cloud.tencent.com/document/product/1047/33521#.E6.A0.A1.E9.AA.8C.E5.A5.BD.E5.8F.8B).


**Example**

```c
Json::Value json_check_friend_list_param;
json_check_friend_list_param[kTIMFriendshipCheckFriendTypeParamCheckType] = FriendTypeBoth;
json_check_friend_list_param[kTIMFriendshipCheckFriendTypeParamIdentifierArray].append("user4");
int ret = TIMFriendshipCheckFriendType(json_check_friend_list_param.toStyledString().c_str(), [](int32_t code, const char* desc, const char* json_params, const void* user_data) {

}, nullptr);
```


## TIMFriendshipCreateFriendGroup

Creates a friend group.

**Prototype**

```c
TIM_DECL int TIMFriendshipCreateFriendGroup(const char* json_create_friend_group_param, TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| json_create_friend_group_param | const char\* | The JSON parameter string of the API for creating a friend group. |
| cb | TIMCommCallback | The callback for checking whether creating the friend group succeeded or failed. For the definition of the callback function, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550#timcommcallback). |
| user_data | const void\* | User-defined data. The IM SDK is only responsible for returning the user data to the callback function cb without any processing. |

**Returned value**

| Type | Description |
|-----|-----|
| int | If TIM_SUCC is returned, the API is invoked successfully (the callback cb will be invoked only when the API returns TIM_SUCC). If other values than this are returned, the API failed to be invoked. For the definition of each returned value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551#timresult). |

> You cannot create a group that already exists.


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

Obtains the group information of a specified friend group.

**Prototype**

```c
TIM_DECL int TIMFriendshipGetFriendGroupList(const char* json_get_friend_group_list_param, TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| json_get_friend_group_list_param | const char\* | The JSON parameter string of the API for obtaining the group information of a specified friend group. |
| cb | TIMCommCallback | The callback for checking whether obtaining friend group information succeeded or failed. For the definition of the callback function, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550#timcommcallback). |
| user_data | const void\* | User-defined data. The IM SDK is only responsible for returning the user data to the callback function cb without any processing. |

**Returned value**

| Type | Description |
|-----|-----|
| int | If TIM_SUCC is returned, the API is invoked successfully (the callback cb will be invoked only when the API returns TIM_SUCC). If other values than this are returned, the API failed to be invoked. For the definition of each returned value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551#timresult). |

**Example**

```c
Json::Value json_get_friend_group_list_param;
json_get_friend_group_list_param.append("Group123");
int ret = TIMFriendshipGetFriendGroupList(json_get_friend_group_list_param.toStyledString().c_str(), [](int32_t code, const char* desc, const char* json_params, const void* user_data) {
    
}, nullptr);
```


## TIMFriendshipModifyFriendGroup

Modifies a friend group.

**Prototype**

```c
TIM_DECL int TIMFriendshipModifyFriendGroup(const char* json_modify_friend_group_param, TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| json_modify_friend_group_param | const char\* | The JSON parameter string of the API for modifying a friend group. |
| cb | TIMCommCallback | The callback for checking whether modifying the friend group succeeded or failed. For the definition of the callback function, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550#timcommcallback). |
| user_data | const void\* | User-defined data. The IM SDK is only responsible for returning the user data to the callback function cb without any processing. |

**Returned value**

| Type | Description |
|-----|-----|
| int | If TIM_SUCC is returned, the API is invoked successfully (the callback cb will be invoked only when the API returns TIM_SUCC). If other values than this are returned, the API failed to be invoked. For the definition of each returned value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551#timresult). |

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

Deletes a friend group.

**Prototype**

```c
TIM_DECL int TIMFriendshipDeleteFriendGroup(const char* json_delete_friend_group_param, TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| json_delete_friend_group_param | const char\* | The JSON parameter string of the API for deleting a friend group. |
| cb | TIMCommCallback | The callback for checking whether deleting the friend group succeeded or failed. For the definition of the callback function, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550#timcommcallback). |
| user_data | const void\* | User-defined data. The IM SDK is only responsible for returning the user data to the callback function cb without any processing. |

**Returned value**

| Type | Description |
|-----|-----|
| int | If TIM_SUCC is returned, the API is invoked successfully (the callback cb will be invoked only when the API returns TIM_SUCC). If other values than this are returned, the API failed to be invoked. For the definition of each returned value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551#timresult). |

**Example**

```c
Json::Value json_delete_friend_group_param;
json_delete_friend_group_param.append("GroupNewName");
int ret = TIMFriendshipDeleteFriendGroup(json_delete_friend_group_param.toStyledString().c_str(), [](int32_t code, const char* desc, const char* json_params, const void* user_data) {
    
}, nullptr);
```


## TIMFriendshipAddToBlackList

Adds a specified user to the blacklist.

**Prototype**

```c
TIM_DECL int TIMFriendshipAddToBlackList(const char* json_add_to_blacklist_param, TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| json_add_to_blacklist_param | const char\* | The JSON parameter string of the API for adding a specified user to the blacklist. |
| cb | TIMCommCallback | The callback for checking whether adding a specified user to the blacklist succeeded or failed. For the definition of the callback function, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550#timcommcallback). |
| user_data | const void\* | User-defined data. The IM SDK is only responsible for returning the user data to the callback function cb without any processing. |

**Returned value**

| Type | Description |
|-----|-----|
| int | If TIM_SUCC is returned, the API is invoked successfully (the callback cb will be invoked only when the API returns TIM_SUCC). If other values than this are returned, the API failed to be invoked. For the definition of each returned value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551#timresult). |

**Example**

```c
Json::Value json_add_to_blacklist_param;
json_add_to_blacklist_param.append("user5");
json_add_to_blacklist_param.append("user10");
int ret = TIMFriendshipAddToBlackList(json_add_to_blacklist_param.toStyledString().c_str(), [](int32_t code, const char* desc, const char* json_params, const void* user_data) {
    
}, nullptr);
```


## TIMFriendshipGetBlackList

Obtains the blacklist.

**Prototype**

```c
TIM_DECL int TIMFriendshipGetBlackList(TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| cb | TIMCommCallback | The callback for checking whether obtaining the blacklist succeeded or failed. For the definition of the callback function, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550#timcommcallback). |
| user_data | const void\* | User-defined data. The IM SDK is only responsible for returning the user data to the callback function cb without any processing. |

**Returned value**

| Type | Description |
|-----|-----|
| int | If TIM_SUCC is returned, the API is invoked successfully (the callback cb will be invoked only when the API returns TIM_SUCC). If other values than this are returned, the API failed to be invoked. For the definition of each returned value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551#timresult). |

## TIMFriendshipDeleteFromBlackList

Deletes a specified user from the blacklist.

**Prototype**

```c
TIM_DECL int TIMFriendshipDeleteFromBlackList(const char* json_delete_from_blacklist_param, TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| json_delete_from_blacklist_param | const char\* | The JSON parameter string of the API for deleting a specified user from the blacklist. |
| cb | TIMCommCallback | The callback for checking whether deleting a specified user from the blacklist succeeded or failed. For the definition of the callback function, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550#timcommcallback). |
| user_data | const void\* | User-defined data. The IM SDK is only responsible for returning the user data to the callback function cb without any processing. |

**Returned value**

| Type | Description |
|-----|-----|
| int | If TIM_SUCC is returned, the API is invoked successfully (the callback cb will be invoked only when the API returns TIM_SUCC). If other values than this are returned, the API failed to be invoked. For the definition of each returned value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551#timresult). |

**Example**

```c
Json::Value json_delete_from_blacklist_param;
json_delete_from_blacklist_param.append("user5");
json_delete_from_blacklist_param.append("user10");
int ret = TIMFriendshipDeleteFromBlackList(json_delete_from_blacklist_param.toStyledString().c_str(), [](int32_t code, const char* desc, const char* json_params, const void* user_data) {
    
}, nullptr);
```


## TIMFriendshipGetPendencyList

Obtains the list of pending friend request information.

**Prototype**

```c
TIM_DECL int TIMFriendshipGetPendencyList(const char* json_get_pendency_list_param, TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| json_get_pendency_list_param | const char\* | The JSON parameter string of the API for obtaining the list of pending friend request information. |
| cb | TIMCommCallback | The callback for checking whether obtaining the pending request information list succeeded or failed. For the definition of the callback function, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550#timcommcallback). |
| user_data | const void\* | User-defined data. The IM SDK is only responsible for returning the user data to the callback function cb without any processing. |

**Returned value**

| Type | Description |
|-----|-----|
| int | If TIM_SUCC is returned, the API is invoked successfully (the callback cb will be invoked only when the API returns TIM_SUCC). If other values than this are returned, the API failed to be invoked. For the definition of each returned value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551#timresult). |

> The list of pending friend request information refers to friend requests that have not yet been handled. For example, the developer sends a friend request to a user, but the user does not handle the request; or a user sends a friend request to the developer, but the developer does not handle the request. This is referred to as pending friend request information.


**Example**

```c
Json::Value json_get_pendency_list_param;
json_get_pendency_list_param[kTIMFriendshipGetPendencyListParamType] = FriendPendencyTypeBoth;
json_get_pendency_list_param[kTIMFriendshipGetPendencyListParamStartSeq] = 0;
int ret = TIMFriendshipGetPendencyList(json_get_pendency_list_param.toStyledString().c_str(), [](int32_t code, const char* desc, const char* json_params, const void* user_data) {
    
}, nullptr);
```


## TIMFriendshipDeletePendency

Deletes the specified pending friend request information.

**Prototype**

```c
TIM_DECL int TIMFriendshipDeletePendency(const char* json_delete_pendency_param, TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| json_delete_pendency_param | const char\* | The JSON parameter string of the API for deleting the specified pending friend request information. |
| cb | TIMCommCallback | The callback for checking whether deleting the specified pending request information succeeded or failed. For the definition of the callback function, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550#timcommcallback). |
| user_data | const void\* | User-defined data. The IM SDK is only responsible for returning the user data to the callback function cb without any processing. |

**Returned value**

| Type | Description |
|-----|-----|
| int | If TIM_SUCC is returned, the API is invoked successfully (the callback cb will be invoked only when the API returns TIM_SUCC). If other values than this are returned, the API failed to be invoked. For the definition of each returned value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551#timresult). |

**Example**

```c
Json::Value json_delete_pendency_param;
json_delete_pendency_param[kTIMFriendshipDeletePendencyParamType] = FriendPendencyTypeComeIn;
json_delete_pendency_param[kTIMFriendshipDeletePendencyParamIdentifierArray].append("user1");
int ret = TIMFriendshipDeletePendency(json_delete_pendency_param.toStyledString().c_str(), [](int32_t code, const char* desc, const char* json_params, const void* user_data) {
    
}, nullptr);
```


## TIMFriendshipReportPendencyReaded

Reports that pending friend request information has been read.

**Prototype**

```c
TIM_DECL int TIMFriendshipReportPendencyReaded(uint64_t time_stamp, TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| time_stamp | uint64_t | The timestamp for reporting that the pending information has been read. |
| cb | TIMCommCallback | The callback for checking whether reporting that the pending information has been read succeeded or failed. For the definition of the callback function, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550#timcommcallback). |
| user_data | const void\* | User-defined data. The IM SDK is only responsible for returning the user data to the callback function cb without any processing. |

**Returned value**

| Type | Description |
|-----|-----|
| int | If TIM_SUCC is returned, the API is invoked successfully (the callback cb will be invoked only when the API returns TIM_SUCC). If other values than this are returned, the API failed to be invoked. For the definition of each returned value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551#timresult). |

