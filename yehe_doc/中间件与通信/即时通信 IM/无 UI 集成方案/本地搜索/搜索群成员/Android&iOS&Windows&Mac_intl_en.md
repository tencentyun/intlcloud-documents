## Overview
Only locally stored group members can be searched for, such as the list of group members or group member profiles that have been pulled.

> ? 
> - The local group member search feature is supported only by the SDK on v5.4.666 or later. It cannot be used for audio-video groups (AVChatRoom) as the group members are not stored locally.
> - The local group member search feature is only available on the IM Ultimate edition. To use it, purchase the [Ultimate edition](https://www.tencentcloud.com/document/product/1047/34577). For more information, see [Billing Overview](https://www.tencentcloud.com/document/product/1047/34349#.E5.9F.BA.E7.A1.80.E6.9C.8D.E5.8A.A1.E8.AF.A6.E6.83.85).
> )。

## Searching for Local Group Members
Call the `searchGroupMembers` API ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a493fb73258019961f3ca8934ff625b0a) / [iOS and Mac](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a35ceb734976c833047cceb8b31055b18) / [Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMGroupManager.html#a705a17828623117e51da885da02d8b12)) to search for local group members.
You can set the search keyword `keywordList` and specify the search scope to set whether to search by the `memberUserID`, `memberNickName`, `memberRemark`, and `memberNameCard` fields of group members.

Depending on whether `groupIDList` of `V2TIMGroupMemberSearchParam` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupMemberSearchParam.html) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMGroupMemberSearchParam.html) / [Windows](https://im.sdk.qcloud.com/doc/en/structV2TIMGroupMemberSearchParam.html)) in `searchGroupMembers` is empty (`null`/`nil`), there are two cases:
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
::: Windows
```cpp
template <class T>
class ValueCallback final : public V2TIMValueCallback<T> {
public:
    using SuccessCallback = std::function<void(const T&)>;
    using ErrorCallback = std::function<void(int, const V2TIMString&)>;

    ValueCallback() = default;
    ~ValueCallback() override = default;

    void SetCallback(SuccessCallback success_callback, ErrorCallback error_callback) {
        success_callback_ = std::move(success_callback);
        error_callback_ = std::move(error_callback);
    }

    void OnSuccess(const T& value) override {
        if (success_callback_) {
            success_callback_(value);
        }
    }
    void OnError(int error_code, const V2TIMString& error_message) override {
        if (error_callback_) {
            error_callback_(error_code, error_message);
        }
    }

private:
    SuccessCallback success_callback_;
    ErrorCallback error_callback_;
};

V2TIMGroupMemberSearchParam param;
param.groupIDList = groupIDList;
param.keywordList = keywordList;
param.isSearchMemberUserID = true;
param.isSearchMemberNickName = true;
param.isSearchMemberRemark = true;
param.isSearchMemberNameCard = true;

auto callback = new ValueCallback<V2TIMGroupSearchGroupMembersMap>{};
callback->SetCallback(
    [=](const V2TIMGroupSearchGroupMembersMap& groupSearchGroupMembersMap) {
        V2TIMStringVector allKeys = groupSearchGroupMembersMap.AllKeys();
        for (size_t i = 0; i < allKeys.Size(); i++) {
            // Group ID
            const V2TIMString& groupID = allKeys[i];
            // Group member list
            V2TIMGroupMemberFullInfoVector groupMemberFullInfoList = groupSearchGroupMembersMap.Get(groupID);
        }
        delete callback;
    },
    [=](int error_code, const V2TIMString& error_message) {
        // Failed to find the group members
        delete callback;
    });

V2TIMManager::GetInstance()->GetGroupManager()->SearchGroupMembers(param, callback);
```
:::
</dx-tabs>
