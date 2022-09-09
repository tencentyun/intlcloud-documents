## Feature Description
Only locally stored group members can be searched for, such as the list of group members or group member profiles that have been pulled.

> ? This feature is supported only by the SDK on v5.4.666 or later. It cannot be used for audio-video groups (AVChatRoom) as the group members are not stored locally.

## Searching for a Local Group Member
Call the `searchGroupMembers` API ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a493fb73258019961f3ca8934ff625b0a) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a35ceb734976c833047cceb8b31055b18)) to search for a local group member.
You can set the search keyword `keywordList` and specify the search scope to set whether to search by the `memberUserID`, `memberNickName`, `memberRemark`, and `memberNameCard` fields of a group member.

Depending on whether `groupIDList` of the `V2TIMGroupMemberSearchParam` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupMemberSearchParam.html) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMGroupMemberSearchParam.html)) in `searchGroupMembers` is empty (`null`/`nil`), there are two cases:
- If `groupIDList` is left empty, members in all the groups will be searched for and returned by `groupID`.
- If `groupIDList` is not left empty, members in the specified group will be searched for.

Sample code:

<dx-tabs>
::: Android
```java
V2TIMGroupMemberSearchParam searchParam = new V2TIMGroupMemberSearchParam();
searchParam.setGroupIDList(groupIDList);
searchParam.setKeywordList(keywordList);
searchParam.setSearchMemberUserID(true);
searchParam.setSearchMemberNickName(true);
searchParam.setSearchMemberRemark(true);
searchParam.setSearchMemberNameCard(true);

V2TIMManager.getGroupManager().searchGroupMembers(searchParam, new V2TIMValueCallback<HashMap<String, List<V2TIMGroupMemberFullInfo>>>() {
  @Override
  public void onSuccess(HashMap<String, List<V2TIMGroupMemberFullInfo>> stringListHashMap) {
    StringBuilder stringBuilder = new StringBuilder();
    for (Map.Entry<String, List<V2TIMGroupMemberFullInfo>> entry : stringListHashMap.entrySet()) {
    	// Group ID
      String groupID = entry.getKey();
			// Group member list
      List<V2TIMGroupMemberFullInfo> memberFullInfoList = entry.getValue();
      }
    }
  }

  @Override
  public void onError(int code, String desc) {
  	// Failed to find the group members
  }
});
```
:::
::: iOS and macOS
```objectivec
V2TIMGroupMemberSearchParam *searchParam = [[V2TIMGroupMemberSearchParam alloc] init];
searchParam.groupIDList = @[@"group1", @"group2"];
searchParam.keywordList = @[@"keyword1", @"keyword2"];
searchParam.isSearchMemberUserID = YES;
searchParam.isSearchMemberNickName = YES;
searchParam.isSearchMemberRemark = YES;
searchParam.isSearchMemberNameCard = YES;
[[V2TIMManager sharedInstance] searchGroupMembers:searchParam succ:^(NSDictionary<NSString *,NSArray<V2TIMGroupMemberFullInfo *> *> *memberList) {
    for (NSString *key in memberList.allKeys) {
        // Group ID
        NSString *groupID = key;
        // Group member list
        NSArray *memberFullInfoList = memberList[key];
    }
} fail:^(int code, NSString *desc) {
    // Failed to find the group members
}];
```
:::
</dx-tabs>


