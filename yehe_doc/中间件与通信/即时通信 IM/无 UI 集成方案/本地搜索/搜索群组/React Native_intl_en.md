## Feature Description

Only locally stored groups can be searched for, such as the list of joined groups and group profiles that have been pulled.

## Searching a Local Group

Call the `searchGroups` API ([Details](https://comm.qq.com/im/doc/RN/en/Api/V2TIMGroupManager/searchGroups.html)) to search a local group.
You can set the search keyword `keywordList` and specify the search scope to set whether to search by the `userID` and `groupName` fields of a group.

Sample code:

```javascript
// Search for a group by the keyword
const searchGroup = await groupManager.searchGroups({
  keywordList: ["Keyword"],
  isSearchGroupID: true,
  isSearchGroupName: true,
});
```
