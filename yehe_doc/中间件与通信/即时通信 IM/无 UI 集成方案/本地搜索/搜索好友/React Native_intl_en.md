## Feature Description

Only locally stored users can be searched for, such as contacts or user profiles that have been pulled.

## Searching for the Local User Profile

Call the `searchFriends` API ([Details](https://comm.qq.com/im/doc/RN/en/Api/V2TIMFriendshipManager/searchFriends.html)) to search for the local user profile.
You can set the search keyword `keywordList` and specify the search scope to set whether to search by the `userID`, `nickName`, and `remark` fields of a user.

Sample code:

```javascript
// Search for a friend by keyword
const serchFriend = await friendshipManager.searchFriends({
  isSearchNickName: true,
  isSearchRemark: true,
  isSearchUserID: true,
  keywordList: ["Keyword"],
});
```
