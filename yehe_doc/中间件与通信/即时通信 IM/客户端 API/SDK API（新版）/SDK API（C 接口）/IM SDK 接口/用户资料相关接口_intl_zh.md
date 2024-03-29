用户资料介绍请参考 [资料系统简介](https://intl.cloud.tencent.com/document/product/1047/33520#.E8.B5.84.E6.96.99.E7.B3.BB.E7.BB.9F.E7.AE.80.E4.BB.8B)。

## TIMProfileGetUserProfileList

获取指定用户列表的个人资料。

**原型**

```c
TIM_DECL int TIMProfileGetUserProfileList(const char* json_get_user_profile_list_param, TIMCommCallback cb, const void* user_data);
```

**参数**

| 参数                             | 类型            | 含义                                                         |
| -------------------------------- | --------------- | ------------------------------------------------------------ |
| json_get_user_profile_list_param | const char\*    | 获取指定用户列表的用户资料接口参数的 JSON 字符串             |
| cb                               | TIMCommCallback | 获取指定用户列表的用户资料成功与否的回调。回调函数定义请参考 [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550#timcommcallback) |
| user_data                        | const void\*    | 用户自定义数据，IM SDK 只负责传回给回调函数 cb，不做任何处理 |

**返回值**

| 类型 | 含义                                                         |
| ---- | ------------------------------------------------------------ |
| int  | 返回 TIM_SUCC 表示接口调用成功（接口只有返回 TIM_SUCC，回调 cb 才会被调用），其他值表示接口调用失败。每个返回值的定义请参考 [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551#timresult) |

>?可以通过该接口获取任何人的个人资料，包括自己的个人资料。


**示例**

```c
Json::Value json_get_user_profile_list_param;
json_get_user_profile_list_param[kTIMFriendShipGetProfileListParamForceUpdate] = false;
json_get_user_profile_list_param[kTIMFriendShipGetProfileListParamIdentifierArray].append("user1");
json_get_user_profile_list_param[kTIMFriendShipGetProfileListParamIdentifierArray].append("user2");

int ret = TIMProfileGetUserProfileList(json_get_user_profile_list_param.toStyledString().c_str(), [](int32_t code, const char* desc, const char* json_params, const void* user_data) {
    if (ERR_SUCC != code) {
        // 获取资料列表失败
        return;
    }
}, nullptr);
```


## TIMProfileModifySelfUserProfile

修改自己的个人资料。

**原型**

```c
TIM_DECL int TIMProfileModifySelfUserProfile(const char* json_modify_self_user_profile_param, TIMCommCallback cb, const void* user_data);
```

**参数**

| 参数                                | 类型            | 含义                                                         |
| ----------------------------------- | --------------- | ------------------------------------------------------------ |
| json_modify_self_user_profile_param | const char\*    | 修改自己的资料接口参数的 JSON 字符串                         |
| cb                                  | TIMCommCallback | 修改自己的资料成功与否的回调。回调函数定义请参考 [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550#timcommcallback) |
| user_data                           | const void\*    | 用户自定义数据，IM SDK 只负责传回给回调函数 cb，不做任何处理 |

**返回值**

| 类型 | 含义                                                         |
| ---- | ------------------------------------------------------------ |
| int  | 返回 TIM_SUCC 表示接口调用成功（接口只有返回 TIM_SUCC，回调 cb 才会被调用），其他值表示接口调用失败。每个返回值的定义请参考 [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551#timresult) |

>?修改自己的资料时，目前支持修改的字段请参考 [UserProfileItem](https://intl.cloud.tencent.com/document/product/1047/34551#userprofileitem)，一次可更新多个字段。修改自定义字段时填入的 key 值可以添加`Tag_Profile_Custom_`前缀，也可以不添加`Tag_Profile_Custom_`前缀，当不添加时，SDK 内部会自动添加该前缀。


**示例**

```c
Json::Value modify_item;
modify_item[kTIMUserProfileItemNickName] = "change my nick name"; // 修改昵称
modify_item[kTIMUserProfileItemGender] = kTIMGenderType_Female;  // 修改性别
modify_item[kTIMUserProfileItemAddPermission] = kTIMProfileAddPermission_NeedConfirm;  // 修改添加好友权限

Json::Value json_user_profile_item_custom;
json_user_profile_item_custom[kTIMUserProfileCustemStringInfoKey] = "Str";  // 修改个人资料自定义字段 " Str " 的值
json_user_profile_item_custom[kTIMUserProfileCustemStringInfoValue] = "my define data";
modify_item[kTIMUserProfileItemCustomStringArray].append(json_user_profile_item_custom);
int ret = TIMProfileModifySelfUserProfile(modify_item.toStyledString().c_str(), [](int32_t code, const char* desc, const char* json_params, const void* user_data) {
    if (ERR_SUCC != code) {
        // 修改自己的个人资料失败
        return;
    }
}, nullptr);
```
