## Feature Description
Only locally stored groups can be searched for, such as the list of joined groups and group profiles that have been pulled.

> ? The group search feature is supported only by v5.4.666 or later.

## Searching a Local Group
Call the `searchGroups` API ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a94a72082b7e2682942f35196a7e28023) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#ac9a960921e512621340159d82a4b5259)) to search a local group.
You can set the search keyword `keywordList` and specify the search scope to set whether to search by the `groupID` and `groupName` fields of a group.

Sample code:

<dx-tabs>
::: Android

```java
V2TIMGroupSearchParam searchParam = new V2TIMGroupSearchParam();
searchParam.setKeywordList(keywordList);
searchParam.setSearchGroupID(true);
searchParam.setSearchGroupName(true);

V2TIMManager.getGroupManager().searchGroups(searchParam, new V2TIMValueCallback<List<V2TIMGroupInfo>>() {
  @Override
  public void onSuccess(List<V2TIMGroupInfo> v2TIMGroupInfos) {
		// Group found successfully
  }

  @Override
  public void onError(int code, String desc) {
  	// Failed to find the group
  }
});
```
:::
::: iOS and macOS
```objectivec
V2TIMGroupSearchParam *searchParam = [[V2TIMGroupSearchParam alloc] init];
searchParam.keywordList = @[@"keyword1", @"keyword2"];
searchParam.isSearchGroupID = YES;
searchParam.isSearchGroupName = YES;
[[V2TIMManager sharedInstance] searchGroups:searchParam succ:^(NSArray<V2TIMGroupInfo *> *groupList) {
    // Group found successfully
} fail:^(int code, NSString *desc) {
    // Failed to find the group
}];
```
:::
</dx-tabs>


