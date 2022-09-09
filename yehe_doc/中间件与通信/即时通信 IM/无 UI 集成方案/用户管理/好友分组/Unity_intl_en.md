## Feature Description
To group friends into categories such as "Classmates at university" and "Coworkers", call the following APIs.

## Friend List

### Creating a friend list
Call the `FriendshipCreateFriendGroup` API ([c#](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html#com_tencent_imsdk_unity_TencentIMSDK_FriendshipCreateFriendGroup_com_tencent_imsdk_unity_types_FriendGroupInfo_com_tencent_imsdk_unity_callback_ValueCallback_System_Collections_Generic_List_com_tencent_imsdk_unity_types_FriendResult___)) to create a friend list.

Sample code:


```c#
// Create a friend list and add a friend to the list
FriendGroupInfo param = new FriendGroupInfo
{
  friendship_create_friend_group_param_name_array = new List<string>
  {
    "group_name"
  },
  friendship_create_friend_group_param_identifier_array = new List<string>
  {
    "user_id"
  }
};
TIMResult res = TencentIMSDK.FriendshipCreateFriendGroup(param, (int code, string desc, List<FriendResult> result, string user_data)=>{
 // Process the async logic
});
```


### Deleting a friend list
Call the `FriendshipDeleteFriendGroup` API ([c#](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html#com_tencent_imsdk_unity_TencentIMSDK_FriendshipDeleteFriendGroup_System_Collections_Generic_List_System_String__com_tencent_imsdk_unity_callback_NullValueCallback_)) to delete a friend list.

Sample code:


```c#
// Delete a friend list
List<string> param = new List<string>
{
  "user_id"
};
TIMResult res = TencentIMSDK.FriendshipDeleteFriendGroup(param, (int code, string desc, string user_data)=>{
 // Process the async logic
});
```


### Renaming a friend list
Call the `FriendshipModifyFriendGroup` API ([c#](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html#com_tencent_imsdk_unity_TencentIMSDK_FriendshipModifyFriendGroup_com_tencent_imsdk_unity_types_FriendshipModifyFriendGroupParam_com_tencent_imsdk_unity_callback_ValueCallback_System_Collections_Generic_List_com_tencent_imsdk_unity_types_FriendResult___)) to rename a friend list.

Sample code:


```c#
// Rename a friend list
FriendshipModifyFriendGroupParam param = new FriendshipModifyFriendGroupParam
{
  friendship_modify_friend_group_param_name = "old_group_name",
  friendship_modify_friend_group_param_new_name = "new_group_name"
};
TIMResult res = TencentIMSDK.FriendshipModifyFriendGroup(param, (int code, string desc, List<FriendResult> result, string user_data)=>{
 // Process the async logic
});
```


### Getting a friend list
Call the `FriendshipGetFriendGroupList` API ([c#](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html#com_tencent_imsdk_unity_TencentIMSDK_FriendshipGetFriendGroupList_System_Collections_Generic_List_System_String__com_tencent_imsdk_unity_callback_ValueCallback_System_Collections_Generic_List_com_tencent_imsdk_unity_types_FriendGroupInfo___)) to get a friend list.

Sample code:


```c#
// Get the information of a friend list by list name
List<string> param = new List<string>
  {
    "user_id"
  };
TIMResult res = TencentIMSDK.FriendshipGetFriendGroupList(param, (int code, string desc, List<FriendGroupInfo> info_list, string user_data)=>{
 // Process the async logic
});
```


### Adding a friend to a list
Call the `FriendshipModifyFriendGroup` API ([c#](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html#com_tencent_imsdk_unity_TencentIMSDK_FriendshipModifyFriendGroup_com_tencent_imsdk_unity_types_FriendshipModifyFriendGroupParam_com_tencent_imsdk_unity_callback_ValueCallback_System_Collections_Generic_List_com_tencent_imsdk_unity_types_FriendResult___)) to add a friend to a list.

Sample code:


```c#
// Add a friend to a friend list
FriendshipModifyFriendGroupParam param = new FriendshipModifyFriendGroupParam
{
  friendship_modify_friend_group_param_name = "group_name",
  friendship_modify_friend_group_param_add_identifier_array = new List<string>
  {
    "user_id"
  }
};
TIMResult res = TencentIMSDK.FriendshipModifyFriendGroup(param, (int code, string desc, List<FriendResult> result, string user_data)=>{
 // Process the async logic
});
```


### Removing a friend from a list
Call `FriendshipModifyFriendGroup` ([c#](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html#com_tencent_imsdk_unity_TencentIMSDK_FriendshipModifyFriendGroup_com_tencent_imsdk_unity_types_FriendshipModifyFriendGroupParam_com_tencent_imsdk_unity_callback_ValueCallback_System_Collections_Generic_List_com_tencent_imsdk_unity_types_FriendResult___)) to remove a friend from a list.

Sample code:


```c#
// Remove a friend from a list
FriendshipModifyFriendGroupParam param = new FriendshipModifyFriendGroupParam
{
  friendship_modify_friend_group_param_name = "group_name",
  friendship_modify_friend_group_param_delete_identifier_array = new List<string>
  {
    "user_id"
  }
};
TIMResult res = TencentIMSDK.FriendshipModifyFriendGroup(param, (int code, string desc, List<FriendResult> result, string user_data)=>{
 // Process the async logic
});
```




