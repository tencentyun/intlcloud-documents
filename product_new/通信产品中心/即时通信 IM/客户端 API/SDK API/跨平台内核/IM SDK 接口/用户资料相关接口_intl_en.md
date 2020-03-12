For information on user profiles, see [Profile System Overview](https://intl.cloud.tencent.com/document/product/1047/33520#.E8.B5.84.E6.96.99.E7.B3.BB.E7.BB.9F.E7.AE.80.E4.BB.8B).

## TIMProfileGetUserProfileList

This API is used to obtain a specified user profile list.

**Prototype**

```c
TIM_DECL int TIMProfileGetUserProfileList(const char* json_get_user_profile_list_param, TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| json_get_user_profile_list_param | const char\* | The JSON parameter string of the API for obtaining the specified user profile list. |
| cb | TIMCommCallback | The callback for notifying whether obtaining the specified user profile list succeeded or failed. For the definition of the callback function, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34551#timcommcallback). |
| user_data | const void\* | User-defined data. The IM SDK is only responsible for returning the user data to the callback function cb without processing the data. |

**Returned values**

| Type | Description |
|-----|-----|
| int | If TIM_SUCC is returned, the API was successfully invoked (the callback will be invoked only when the API returns TIM_SUCC.) If other values are returned, the API failed to be invoked. For the definition of each returned value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551#timresult). |

> You can use this API to obtain the profile of any user, including yourself. If the obtained profile is not of your own, `kTIMProfileAddPermission’ in the obtained profile is `kTIMProfileAddPermission_Unknown`. For users other than yourself, you cannot obtain friend addition permission information, and Unknown is returned by default.


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

This API is used to modify your own user profile.

**Prototype**

```c
TIM_DECL int TIMProfileModifySelfUserProfile(const char* json_modify_self_user_profile_param, TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| json_modify_self_user_profile_param | const char\* | The JSON parameter string of the API for modifying your own user profile. |
| cb | TIMCommCallback | The callback for notifying whether modifying your own user profile succeeded or failed. For the definition of the callback function, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34551#timcommcallback). |
| user_data | const void\* | User-defined data. The IM SDK is only responsible for returning the user data to the callback function cb without processing the data. |

**Returned values**

| Type | Description |
|-----|-----|
| int | If TIM_SUCC is returned, the API was successfully invoked (the callback will be invoked only when the API returns TIM_SUCC.) If other values are returned, the API failed to be invoked. For the definition of each returned value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551#timresult). |

> When using this API to modify your own profile, see [UserProfileItem](https://intl.cloud.tencent.com/document/product/1047/34551#userprofileitem) for currently modifiable fields. You can modify multiple fields at a time. When modifying a custom field, you can add the `Tag_Profile_Custom_` prefix to the entered key value. If you do not add this prefix, the SDK automatically adds it.


**Example**

```c
Json::Value modify_item;
modify_item[kTIMUserProfileItemNickName] = "change my nick name"; // Change the nickname
modify_item[kTIMUserProfileItemGender] = kTIMGenderType_Female;  // Change the gender
modify_item[kTIMUserProfileItemAddPermission] = kTIMProfileAddPermission_NeedConfirm;  // Modify permissions for adding friends

Json::Value json_user_profile_item_custom;
json_user_profile_item_custom[kTIMUserProfileCustemStringInfoKey] = "Str";  // Change the value of "Str", which is a custom field of the user profile
json_user_profile_item_custom[kTIMUserProfileCustemStringInfoValue] = "my define data";
modify_item[kTIMUserProfileItemCustomStringArray].append(json_user_profile_item_custom);
int ret = TIMProfileModifySelfUserProfile(modify_item.toStyledString().c_str(), [](int32_t code, const char* desc, const char* json_params, const void* user_data) {
    if (ERR_SUCC != code) {
        // Failed to modify your own user profile.
        return;
    }
}, nullptr);
```


