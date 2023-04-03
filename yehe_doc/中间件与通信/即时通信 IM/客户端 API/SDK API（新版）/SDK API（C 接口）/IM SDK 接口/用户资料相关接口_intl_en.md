For more information about user profile introduction, see [Profile System Overview](https://intl.cloud.tencent.com/document/product/1047/33520).

## TIMProfileGetUserProfileList

This API is used to obtain the profiles of a specified user list.

**Prototype**

```c
TIM_DECL int TIMProfileGetUserProfileList(const char* json_get_user_profile_list_param, TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter                        | Type            | Description                                                  |
| -------------------------------- | --------------- | ------------------------------------------------------------ |
| json_get_user_profile_list_param | const char\*    | JSON string of the API parameter for obtaining the profile of a specified user list. |
| cb                               | TIMCommCallback | Callback function for notifying whether the profile of the specified user list was obtained. For more information about the callback function definition, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data                        | const void\*    | User-defined data. The IM SDK only transfers the user data to the callback function cb without processing the data. |

**Return values**

| Type | Description                                                  |
| ---- | ------------------------------------------------------------ |
| int  | If TIM_SUCC is returned, the API was successfully called. (The callback cb is called only when the API returns TIM_SUCC.) If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

>?You can use this API to obtain the profile of any person, including yourself.


**Example**

```c
Json::Value json_get_user_profile_list_param;
json_get_user_profile_list_param[kTIMFriendShipGetProfileListParamForceUpdate] = false;
json_get_user_profile_list_param[kTIMFriendShipGetProfileListParamIdentifierArray].append("user1");
json_get_user_profile_list_param[kTIMFriendShipGetProfileListParamIdentifierArray].append("user2");

int ret = TIMProfileGetUserProfileList(json_get_user_profile_list_param.toStyledString().c_str(), [](int32_t code, const char* desc, const char* json_params, const void* user_data) {
    if (ERR_SUCC != code) {
        // Failed to obtain the profile list.
        return;
    }
}, nullptr);
```


## TIMProfileModifySelfUserProfile

This API is used to modify your own profile.

**Prototype**

```c
TIM_DECL int TIMProfileModifySelfUserProfile(const char* json_modify_self_user_profile_param, TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter                           | Type            | Description                                                  |
| ----------------------------------- | --------------- | ------------------------------------------------------------ |
| json_modify_self_user_profile_param | const char\*    | JSON string of the API parameter for modifying your own profile. |
| cb                                  | TIMCommCallback | Callback function for notifying whether your own profile was modified. For more information about the callback function definition, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data                           | const void\*    | User-defined data. The IM SDK only transfers the user data to the callback function cb without processing the data. |

**Return values**

| Type | Description                                                  |
| ---- | ------------------------------------------------------------ |
| int  | If TIM_SUCC is returned, the API was successfully called. (The callback cb is called only when the API returns TIM_SUCC.) If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

>?When using this API to modify your own profile, see [UserProfileItem](https://intl.cloud.tencent.com/document/product/1047/34551) for information about the fields that can be modified. You can modify multiple fields at a time. When modifying a custom field, you can add the prefix `Tag_Profile_Custom_` to the entered key value. If you do not add this prefix, the SDK will automatically add this prefix.


**Example**

```c
Json::Value modify_item;
modify_item[kTIMUserProfileItemNickName] = "change my nick name"; // Modify the nickname.
modify_item[kTIMUserProfileItemGender] = kTIMGenderType_Female;  // Modify the gender.
modify_item[kTIMUserProfileItemAddPermission] = kTIMProfileAddPermission_NeedConfirm;  // Modify the permissions for adding friends.

Json::Value json_user_profile_item_custom;
json_user_profile_item_custom[kTIMUserProfileCustemStringInfoKey] = "Str";  // Modify the value of "Str", which is a custom field of the user profile.
json_user_profile_item_custom[kTIMUserProfileCustemStringInfoValue] = "my define data";
modify_item[kTIMUserProfileItemCustomStringArray].append(json_user_profile_item_custom);
int ret = TIMProfileModifySelfUserProfile(modify_item.toStyledString().c_str(), [](int32_t code, const char* desc, const char* json_params, const void* user_data) {
    if (ERR_SUCC != code) {
        // Failed to modify your own profile.
        return;
    }
}, nullptr);
```
