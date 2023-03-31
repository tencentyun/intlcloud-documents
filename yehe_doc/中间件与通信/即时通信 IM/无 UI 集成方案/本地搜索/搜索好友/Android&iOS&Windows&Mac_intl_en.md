## Overview
Only locally stored users can be searched for, such as contacts or user profiles that have been pulled.

>?
>- The local user search feature is supported only by v5.4.666 or later.
>- The local user profile search feature is only available on the IM Ultimate edition. To use it, purchase the Ultimate edition. For more information, see [Billing Overview](https://www.tencentcloud.com/document/product/1047/34349#.E5.9F.BA.E7.A1.80.E6.9C.8D.E5.8A.A1.E8.AF.A6.E6.83.85).
>)。

## Searching for the Local User Profile
Call the `searchFriends` API ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a3e657c9ec5d68a4c423a64d71f5f9c6e) / [iOS and Mac](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#a9a036dcc1bd65474a3d2e90f2bb6b9c6) / [Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMFriendshipManager.html#aea84cd163665db3b0f2338d787446f53)) to search for the local user profile.
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

V2TIMFriendSearchParam searchParam;
searchParam.keywordList = keywordList;
searchParam.isSearchUserID = true;
searchParam.isSearchNickName = true;
searchParam.isSearchRemark = true;

auto callback = new ValueCallback<V2TIMFriendInfoResultVector>{};
callback->SetCallback(
    [=](const V2TIMFriendInfoResultVector& friendInfoResultList) {
        // User profile found successfully
        delete callback;
    },
    [=](int error_code, const V2TIMString& error_message) {
        // Failed to find the user profile
        delete callback;
    });

V2TIMManager::GetInstance()->GetFriendshipManager()->SearchFriends(searchParam, callback);
```
:::
</dx-tabs>
