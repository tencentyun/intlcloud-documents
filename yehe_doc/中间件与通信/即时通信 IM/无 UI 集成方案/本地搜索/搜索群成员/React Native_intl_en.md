## Feature Description

Only locally stored group members can be searched for, such as the list of group members or group member profiles that have been pulled.
> ?This feature cannot be used for audio-video groups (AVChatRoom) as the group members are not stored locally.
## Searching a Local Group

Call the `searchGroupMembers` API ([Details](https://comm.qq.com/im/doc/RN/en/Api/V2TIMGroupManager/searchGroupMembers.html)) to search for a local group member.
You can set the search keyword `keywordList` and specify the search scope to set whether to search by the `memberUserID`, `memberNickName`, `memberRemark`, and `memberNameCard` fields of a group member.

Depending on whether `groupIDList` of the `V2TIMGroupMemberSearchParam` ([Details](https://comm.qq.com/im/doc/RN/en/Api/V2TIMGroupManager/searchGroupMembers.html)) in `searchGroupMembers` is empty (`null`/`nil`), there are two cases:

- If `groupIDList` is left empty, members in all the groups will be searched for and returned by `groupID`.
- If `groupIDList` is not left empty, members in the specified group will be searched for.

Sample code:

```javascript
// Search for group members by the keyword and group ID
const searchGroupMem = await groupManager.searchGroupMembers({
  groupIDList: ["The group ID can be specified"],
  keywordList: ["Keyword"],
  isSearchMemberNameCard: true,
  isSearchMemberNickName: true,
  isSearchMemberRemark: true,
  isSearchMemberUserID: true,
});
```
