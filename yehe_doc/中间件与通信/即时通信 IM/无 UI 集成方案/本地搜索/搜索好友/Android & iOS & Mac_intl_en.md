## Feature Description
Only locally stored users can be searched for, such as contacts or user profiles that have been pulled.

> ? The user search feature is supported only by v5.4.666 or later.

## Searching for the Local User Profile
Call the `searchFriends` API ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a3e657c9ec5d68a4c423a64d71f5f9c6e) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#a9a036dcc1bd65474a3d2e90f2bb6b9c6)) to search for the local user profile.
You can set the search keyword `keywordList` and specify the search scope to set whether to search by the `userID`, `nickName`, and `remark` fields of a user.

Sample code:

<dx-tabs>
::: Android
```java
V2TIMFriendSearchParam searchParam = new V2TIMFriendSearchParam();
searchParam.setKeywordList(keywordList);
searchParam.setSearchUserID(true);
searchParam.setSearchNickName(true);
searchParam.setSearchRemark(true);

V2TIMManager.getFriendshipManager().searchFriends(searchParam, new V2TIMValueCallback<List<V2TIMFriendInfoResult>>() {
  @Override
  public void onSuccess(List<V2TIMFriendInfoResult> v2TIMFriendInfos) {
  	// User profile found successfully
  }

  @Override
  public void onError(int code, String desc) {
  	// Failed to find the user profile
  }
});
```
:::
::: iOS and macOS
```objectivec
V2TIMFriendSearchParam *searchParam = [[V2TIMFriendSearchParam alloc] init];
searchParam.keywordList = @[@"keyword1", @"keyword2"];
searchParam.isSearchUserID = YES;
searchParam.isSearchNickName = YES;
searchParam.isSearchRemark = YES;
[[V2TIMManager sharedInstance] searchFriends:searchParam succ:^(NSArray<V2TIMFriendInfoResult *> *resultList) {
    // User profile found successfully
} fail:^(int code, NSString *desc) {
    // Failed to find the user profile
}];
```
:::
</dx-tabs>


