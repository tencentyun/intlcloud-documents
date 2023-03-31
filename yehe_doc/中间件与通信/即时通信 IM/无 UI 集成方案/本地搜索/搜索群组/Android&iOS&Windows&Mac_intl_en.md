## Overview
Only locally stored groups can be searched for, such as the list of joined groups and group profiles that have been pulled.

> ?
> - The local group search feature is supported only by v5.4.666 or later. 
> - The local group search feature is only available on the IM Ultimate edition. To use it, purchase the Ultimate edition. For more information, see [Billing Overview](https://www.tencentcloud.com/document/product/1047/34349#.E5.9F.BA.E7.A1.80.E6.9C.8D.E5.8A.A1.E8.AF.A6.E6.83.85).
> )。

## Searching a Local Group
Call the `searchGroups` API ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a94a72082b7e2682942f35196a7e28023) / [iOS and Mac](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#ac9a960921e512621340159d82a4b5259) / [Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMGroupManager.html#a63b463ce1a5952adf8d88bc794b32f22)) to search a local group.
You can set the search keyword `keywordList` and specify the search scope to set whether to search by the `userID` and `groupName` fields of a group.

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

V2TIMGroupSearchParam searchParam;
searchParam.keywordList = keywordList;
searchParam.isSearchGroupID = true;
searchParam.isSearchGroupName = true;

auto callback = new ValueCallback<V2TIMGroupInfoVector>{};
callback->SetCallback(
    [=](const V2TIMGroupInfoVector& groupInfoList) {
        // Group found successfully
        delete callback;
    },
    [=](int error_code, const V2TIMString& error_message) {
        // Failed to find the group
        delete callback;
    });

V2TIMManager::GetInstance()->GetGroupManager()->SearchGroups(searchParam, callback);
```
:::
</dx-tabs>
