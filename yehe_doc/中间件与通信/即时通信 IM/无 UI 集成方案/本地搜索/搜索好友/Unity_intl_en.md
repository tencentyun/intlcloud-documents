## Feature Description
Only locally stored users can be searched for, such as contacts or user profiles that have been pulled.


## Searching for the Local User Profile
Call the `FriendshipSearchFriends` API ([Details](https://comm.qq.com/im/doc/unity/en/api/FriendshipApi/FriendshipSearchFriends.html)) to search for the local user profile.
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
