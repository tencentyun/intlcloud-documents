## Feature Description
Only locally stored users can be searched for, such as contacts or user profiles that have been pulled.


## Searching for the Local User Profile
Call the `FriendshipSearchFriends` API ([c#](https://comm.qq.com/im/sdk/unity_plus/_site_en/api/com.tencent.imsdk.unity.TencentIMSDK.html#com_tencent_imsdk_unity_TencentIMSDK_FriendshipSearchFriends_com_tencent_imsdk_unity_types_FriendSearchParam_com_tencent_imsdk_unity_callback_ValueCallback_System_Collections_Generic_List_com_tencent_imsdk_unity_types_FriendInfoGetResult___)) to search for the local user profile.
You can set the search keyword `friendship_search_param_keyword_list` and specify the search scope to set whether to search by the `userID`, `nickName`, and `remark` fields of a user.

Sample code:



```c#
// Search for a friend by keyword
FriendSearchParam param = new FriendSearchParam
{
  friendship_search_param_keyword_list = new List<string>
  {
    "Keyword 1"
  },
  friendship_search_param_search_field_list = new List<TIMFriendshipSearchFieldKey>
  {
    TIMFriendshipSearchFieldKey.kTIMFriendshipSearchFieldKey_Identifier,
    TIMFriendshipSearchFieldKey.kTIMFriendshipSearchFieldKey_NikeName,
    TIMFriendshipSearchFieldKey.kTIMFriendshipSearchFieldKey_Remark
  }
};
TIMResult res = TencentIMSDK.MsgSearchLocalMessages(param, (int code, string desc, List<FriendInfoGetResult> result, string user_data)=>{
 // Process the async logic
});
```




