## Overview
To group friends into categories such as "classmates" and "coworkers", call the following APIs.

## Friend Lists

### Creating a friend list
Call the `createFriendGroup` API ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#afe729e7a74d1e7fd06a5f23c155a08ae) / [iOS and Mac](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#a8b33edab15ae7d179e4e2d885e7d2b7d) / [Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMFriendshipManager.html#a8f4192055ef6b4d85e01983a6369f0d4)) to create a friend list.

Sample code:
<dx-tabs>
::: Android
```java
List<String> userIDList = new ArrayList<>();
userIDList.add("user1");
userIDList.add("user2");
V2TIMManager.getFriendshipManager().createFriendGroup("Friends at university", userIDList, new V2TIMValueCallback<List<V2TIMFriendOperationResult>>() {
  @Override
  public void onSuccess(List<V2TIMFriendOperationResult> v2TIMFriendOperationResults) {
    // Friend list created successfully
  }

  @Override
  public void onError(int code, String desc) {
    // Failed to create the friend list
  }
});
```
:::
::: iOS and macOS
```objectivec
// Create a friend list
[[V2TIMManager sharedInstance] createFriendGroup:@"Friends at university" userIDList:@[@"user1", @"user2"] succ:^(NSArray<V2TIMFriendOperationResult *> *resultList) {
    // Friend list created successfully
} fail:^(int code, NSString *desc) {
    // Failed to create the friend list
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

V2TIMString groupName = u8"Friends at university";
V2TIMStringVector userIDList;
userIDList.PushBack(u8"user1");
userIDList.PushBack(u8"user2");

auto callback = new ValueCallback<V2TIMFriendOperationResultVector>{};
callback->SetCallback(
    [=](const V2TIMFriendOperationResultVector& friendOperationResultList) {
        // Friend list created successfully
        delete callback;
    },
    [=](int error_code, const V2TIMString& error_message) {
        // Failed to create the friend list
        delete callback;
    });

V2TIMManager::GetInstance()->GetFriendshipManager()->CreateFriendGroup(groupName, userIDList, callback);
```
:::
</dx-tabs>

### Deleting a friend list
Call the `deleteFriendGroup` API ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#ac9f06f447ee4452aa12e078b48023cee) / [iOS and Mac](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#a2dc49f2abb1238fc2d47ce6d4f14c1e7) / [Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMFriendshipManager.html#aef0784eca4e5c17d5ef12da5788338b6)) to delete a friend list. This will not delete the friends.

Sample code:
<dx-tabs>
::: Android

```java
List<String> friendGroupList = new ArrayList<>();
friendGroupList.add("Friends at university");
V2TIMManager.getFriendshipManager().deleteFriendGroup(friendGroupList, new V2TIMCallback() {
  @Override
  public void onSuccess() {
    // Friend list deleted successfully
  }

  @Override
  public void onError(int code, String desc) {
    // Failed to delete the friend list
  }
});
```
:::
::: iOS and macOS
```objectivec
// Delete a friend list
[[V2TIMManager sharedInstance] deleteFriendGroup:@[@"Friends at university"] succ:^{
    // Friend list deleted successfully
} fail:^(int code, NSString *desc) {
    // Failed to delete the friend list
}];
```
:::
::: Windows
```cpp
class Callback final : public V2TIMCallback {
public:
    using SuccessCallback = std::function<void()>;
    using ErrorCallback = std::function<void(int, const V2TIMString&)>;

    Callback() = default;
    ~Callback() override = default;

    void SetCallback(SuccessCallback success_callback, ErrorCallback error_callback) {
        success_callback_ = std::move(success_callback);
        error_callback_ = std::move(error_callback);
    }

    void OnSuccess() override {
        if (success_callback_) {
            success_callback_();
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

V2TIMStringVector groupNameList;
groupNameList.PushBack(u8"Friends at university");

auto callback = new Callback{};
callback->SetCallback(
    [=]() {
        // Friend list deleted successfully
        delete callback;
    },
    [=](int error_code, const V2TIMString& error_message) {
        // Failed to delete the friend list
        delete callback;
    });

V2TIMManager::GetInstance()->GetFriendshipManager()->DeleteFriendGroup(groupNameList, callback);
```
:::
</dx-tabs>

### Renaming a friend list
Call the `renameFriendGroup` API ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a5345957f4d75d8e57ea3b4cff9adee13) / [iOS and Mac](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#a93f6ba132d9706db7c74daff97a2abd0) / [Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMFriendshipManager.html#a74ada64658763bc5eb7f918993e15649)) to rename a friend list.

Sample code:
<dx-tabs>
::: Android
```java
V2TIMManager.getFriendshipManager().renameFriendGroup("Friends at university", "Friends in high school", new V2TIMCallback() {
  @Override
  public void onSuccess() {
    // Friend list name changed successfully
  }

  @Override
  public void onError(int code, String desc) {
    // Failed to rename the friend list
  }
});
```
:::
::: iOS and macOS
```objectivec
// Rename a friend list
[[V2TIMManager sharedInstance] renameFriendGroup:@"Friends at university" newName:@"Friends in high school" succ:^{
    // Friend list name changed successfully
} fail:^(int code, NSString *desc) {
    // Failed to rename the friend list
}];
```
:::
::: Windows
```cpp
class Callback final : public V2TIMCallback {
public:
    using SuccessCallback = std::function<void()>;
    using ErrorCallback = std::function<void(int, const V2TIMString&)>;

    Callback() = default;
    ~Callback() override = default;

    void SetCallback(SuccessCallback success_callback, ErrorCallback error_callback) {
        success_callback_ = std::move(success_callback);
        error_callback_ = std::move(error_callback);
    }

    void OnSuccess() override {
        if (success_callback_) {
            success_callback_();
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

V2TIMString oldName = u8"Friends at university";
V2TIMString newName = u8"Friends in high school";

auto callback = new Callback{};
callback->SetCallback(
    [=]() {
        // Friend list name changed successfully
        delete callback;
    },
    [=](int error_code, const V2TIMString& error_message) {
        // Failed to rename the friend list
        delete callback;
    });

V2TIMManager::GetInstance()->GetFriendshipManager()->RenameFriendGroup(oldName, newName, callback);
```
:::
</dx-tabs>

### Getting a friend list
Call the `getFriendGroupList` API ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a0043ca81fdeec5d3e842e85278003d1e) / [iOS and Mac](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#a63f3eaae567586077d5a8d27c31e2229) / [Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMFriendshipManager.html#a3190b203cda3e1cabb947aded25c6354)) to get a friend list.

Sample code:
<dx-tabs>
::: Android
```java
List<String> friendGroups = new ArrayList<>();
friendGroups.add("Friends at university");
V2TIMManager.getFriendshipManager().getFriendGroups(friendGroups, new V2TIMValueCallback<List<V2TIMFriendGroup>>() {
  @Override
  public void onSuccess(List<V2TIMFriendGroup> v2TIMFriendGroups) {
    // Friend list obtained successfully
  }

  @Override
  public void onError(int code, String desc) {
    // Failed to obtain the friend list
  }
});
```
:::
::: iOS and macOS
```objectivec
// Get a friend list
[[V2TIMManager sharedInstance] getFriendGroupList:@[@"Friends at university"] succ:^(NSArray<V2TIMFriendGroup *> *groups) {
    // Friend list obtained successfully
} fail:^(int code, NSString *desc) {
    // Failed to obtain the friend list
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

V2TIMStringVector groupNameList;
groupNameList.PushBack(u8"Friends at university");

auto callback = new ValueCallback<V2TIMFriendGroupVector>{};
callback->SetCallback(
    [=](const V2TIMFriendGroupVector& friendGroupList) {
        // Friend list obtained successfully
        delete callback;
    },
    [=](int error_code, const V2TIMString& error_message) {
        // Failed to obtain the friend list
        delete callback;
    });

V2TIMManager::GetInstance()->GetFriendshipManager()->GetFriendGroups(groupNameList, callback);
```
:::
</dx-tabs>

### Adding a friend to a list
Call the `addFriendsToFriendGroup` API ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a6de9168d476ac14e21025ec5c26251df) / [iOS and Mac](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#a0265241c39600c390406ca1f8f6ff75d) / [Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMFriendshipManager.html#a6bb688a4a82c1bc158a7873eda738c2f)) to add a friend to a list.

Sample code:
<dx-tabs>
::: Android
```java
List<String> userIDList = new ArrayList<>();
userIDList.add("user1");
userIDList.add("user2");
V2TIMManager.getFriendshipManager().addFriendsToFriendGroup("Friends at university", userIDList, new V2TIMValueCallback<List<V2TIMFriendOperationResult>>() {
  @Override
  public void onSuccess(List<V2TIMFriendOperationResult> v2TIMFriendOperationResults) {
    // Added successfully
  }

  @Override
  public void onError(int code, String desc) {
    // Failed to add
  }
});
```
:::
::: iOS and macOS
```objectivec
// Add a friend to a list
[[V2TIMManager sharedInstance] addFriendsToFriendGroup:@"Friends at university" userIDList:@[@"user1", @"user2"] succ:^(NSArray<V2TIMFriendOperationResult *> *resultList) {
    // Added successfully
} fail:^(int code, NSString *desc) {
    // Failed to add
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

V2TIMString groupName = u8"Friends at university";
V2TIMStringVector userIDList;
userIDList.PushBack(u8"user1");
userIDList.PushBack(u8"user2");

auto callback = new ValueCallback<V2TIMFriendOperationResultVector>{};
callback->SetCallback(
    [=](const V2TIMFriendOperationResultVector& friendOperationResultList) {
        // Added successfully
        delete callback;
    },
    [=](int error_code, const V2TIMString& error_message) {
        // Failed to add
        delete callback;
    });

V2TIMManager::GetInstance()->GetFriendshipManager()->AddFriendsToFriendGroup(groupName, userIDList, callback);
```
:::
</dx-tabs>

### Removing a friend from a friend list
Call `deleteFriendsFromFriendGroup` API ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#ae367dfec88522e96d96c5ab942e50653) / [iOS and Mac](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#a4a14a878816c8d6a20981d1903fcf359) / [Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMFriendshipManager.html#a0d9d90dc372d82b07a79fe5e843f3ab6)) to remove a friend from a list. This will only remove the friend from the list and will not delete the friend.

Sample code:
<dx-tabs>
::: Android
```java
List<String> userIDList = new ArrayList<>();
userIDList.add("user1");
userIDList.add("user2");
V2TIMManager.getFriendshipManager().deleteFriendsFromFriendGroup("Friends at university", userIDList, new V2TIMValueCallback<List<V2TIMFriendOperationResult>>() {
  @Override
  public void onSuccess(List<V2TIMFriendOperationResult> v2TIMFriendOperationResults) {
    // Deleted successfully
  }

  @Override
  public void onError(int code, String desc) {
    // Failed to delete
  }
});
```
:::
::: iOS and macOS
```objectivec
// Remove a friend from a list
[[V2TIMManager sharedInstance] deleteFriendsFromFriendGroup:@"Friends at university" userIDList:@[@"user1", @"user2"] succ:^(NSArray<V2TIMFriendOperationResult *> *resultList) {
    // Deleted successfully
} fail:^(int code, NSString *desc) {
    // Failed to delete
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

V2TIMString groupName = u8"Friends at university";
V2TIMStringVector userIDList;
userIDList.PushBack(u8"user1");
userIDList.PushBack(u8"user2");

auto callback = new ValueCallback<V2TIMFriendOperationResultVector>{};
callback->SetCallback(
    [=](const V2TIMFriendOperationResultVector& friendOperationResultList) {
        // Deleted successfully
        delete callback;
    },
    [=](int error_code, const V2TIMString& error_message) {
        // Failed to delete
        delete callback;
    });

V2TIMManager::GetInstance()->GetFriendshipManager()->DeleteFriendsFromFriendGroup(groupName, userIDList,
                                                                                  callback);
```
:::
</dx-tabs>
