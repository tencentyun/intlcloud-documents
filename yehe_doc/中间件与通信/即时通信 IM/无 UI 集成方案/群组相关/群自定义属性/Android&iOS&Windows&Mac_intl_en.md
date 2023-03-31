## Overview
New custom group fields, also called group attributes, are designed based on API 2.0.
With group attributes, you can manage the seats of audio chat rooms. When a user mics on, you can set a group attribute to manage the information of the user. When the user mics off, you can delete the group attribute. Other members can get the list of group attributes to display the seat list.
Group attributes are represented by key-value pairs, and the methods are in the `V2TIMGroupManager(Android)` / `V2TIMManager(Group)(iOS and macOS)` core class.

> ?  
>
> - On versions 6.7 and earlier, only the audio-video group (AVChatRoom) is supported.
> - Starting from version 6.8, the audio-video group (AVChatRoom), public group (Public), meeting group (Meeting), and work group (Work) are supported.
> - Currently, the community and topic are not supported.



The group attribute has the following features:
1. You can configure up to 16 group attributes. The size of each group attribute can be up to 4 KB, and the total size of all group attributes can be up to 16 KB.
2. The `initGroupAttributes`, `setGroupAttributes`, and `deleteGroupAttributes` APIs each can be called by a logged-in user up to ten times every five seconds in the SDK, and the 8511 error code will be called back if the limit is exceeded. The APIs each can be called by a logged-in user up to five times every second in the backend, and the 10049 error code will be called back if the limit is exceeded.
3. The `getGroupAttributes` API can be called by a logged-in user 20 times every five seconds in the SDK.
4. Starting from version 5.6, when you modify group attributes for the first time after the app is started, call `getGroupAttributes` to pull the latest group attributes before you initiate the modification operation.
5. Starting from version 5.6, when multiple users modify the same group attributes at the same time, only the first user can execute successfully, and other users will receive the 10056 error code. After receiving this error code, call `getGroupAttributes` to update the locally stored group attributes to the latest before you initiate the modification operation.

### Initializing group attributes
Call the `initGroupAttributes` API ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a17569b57abc77adb6be9356b9eb70182) / [iOS and Mac](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a1b3a56dfc345f1ef2a575cb36156e745) / [Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMGroupManager.html#a049a490d04dde4cf925491809a6df6e2)) to initialize the group attributes, and the original group attributes, if any, will be cleared first.

Sample code:

<dx-tabs>
::: Android
```java
V2TIMManager.getGroupManager().initGroupAttributes("groupA", attributeMap, new V2TIMCallback() {
  @Override
  public void onSuccess() {
		// Initialized the group attributes successfully
  }

  @Override
  public void onError(int code, String desc) {
		// Failed to initialized the group attributes
  }
});
```
:::
::: iOS and macOS
```objectivec
[[V2TIMManager sharedInstance] initGroupAttributes:@"groupA" attributes:@{@"key1" : @"value1"} succ:^{
    // Initialized the group attributes successfully
} fail:^(int code, NSString *desc) {
    // Failed to initialized the group attributes
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

V2TIMString groupID = "groupA";
V2TIMGroupAttributeMap attributes;
attributes.Insert("key1", "value1");
attributes.Insert("key2'", "value2");

auto callback = new Callback;
callback->SetCallback(
    [=]() {
        // Initialized the group attributes successfully
        delete callback;
    },
    [=](int error_code, const V2TIMString& error_message) {
        // Failed to initialized the group attributes
        delete callback;
    });

V2TIMManager::GetInstance()->GetGroupManager()->InitGroupAttributes(groupID, attributes, callback);
```
:::
</dx-tabs>

### Setting group attributes

Call the `setGroupAttributes` API ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a3ec31101e4763dab7a1c99a71bc3da08) / [iOS and Mac](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a134342ddb51d1ee83f3981ed91d26885) / [Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMGroupManager.html#a35accef15afd5def586332c7397cee7b)) to set the group attributes. If a group attribute doesn't exist, it will be automatically added.

Sample code:

<dx-tabs>
::: Android

```java
HashMap<String, String> attributeMap = new HashMap<>();
attributeMap.put("key1", "value1");
attributeMap.put("key2", "value2");
V2TIMManager.getGroupManager().setGroupAttributes("groupA", attributeMap, new V2TIMCallback() {
  @Override
  public void onSuccess() {
		// Set the group attributes successfully
  }

  @Override
  public void onError(int code, String desc) {
		// Failed to set the group attributes
  }
});
```
:::
::: iOS and macOS

```objectivec
[[V2TIMManager sharedInstance] setGroupAttributes:@"groupA" attributes:@{@"key1" : @"value1"} succ:^{
    // Set the group attributes successfully
} fail:^(int code, NSString *desc) {
    // Failed to set the group attributes
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

V2TIMString groupID = "groupA";
V2TIMGroupAttributeMap attributes;
attributes.Insert("key1", "value1");
attributes.Insert("key2'", "value2");

auto callback = new Callback;
callback->SetCallback(
    [=]() {
        // Set the group attributes successfully
        delete callback;
    },
    [=](int error_code, const V2TIMString& error_message) {
        // Failed to set the group attributes
        delete callback;
    });

V2TIMManager::GetInstance()->GetGroupManager()->SetGroupAttributes(groupID, attributes, callback);
```
:::
</dx-tabs>

### Deleting group attributes

Call the `deleteGroupAttributes` API ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a45f211bafddc58bf5e199e18a6814578) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#aa504ffca9492580ca27a45f78a87e2cb) / [Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMGroupManager.html#acdbc438459cfd970bd557a3b252db768)) to delete a specified group attribute. If `keys` is set to `null`/`nil`, all the group attributes will be cleared.

Sample code:

<dx-tabs>
::: Android
```java
List<String> keyList = new ArrayList<>();
keyList.add("key1");
V2TIMManager.getGroupManager().deleteGroupAttributes("groupA", keyList, new V2TIMCallback() {
  @Override
  public void onSuccess() {
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
[[V2TIMManager sharedInstance] deleteGroupAttributes:@"groupA" keys:@[@"key1"] succ:^{
    // Deleted successfully
} fail:^(int code, NSString *desc) {
    // Failed to delete
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

V2TIMString groupID = "groupA";
V2TIMStringVector keys;
keys.PushBack("key1");
keys.PushBack("key2");

auto callback = new Callback;
callback->SetCallback(
    [=]() {
        // The group attributes deleted successfully
        delete callback;
    },
    [=](int error_code, const V2TIMString& error_message) {
        // Failed to delete the group attributes
        delete callback;
    });

V2TIMManager::GetInstance()->GetGroupManager()->DeleteGroupAttributes(groupID, keys, callback);
```
:::
</dx-tabs>

### Getting group attributes

Call the `getGroupAttributes` API ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#ade2155fb24ed1c0b8eb976e146c14e3d) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#ac8a74db230669d1b49da47bb0895cbf9) / [Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMGroupManager.html#a7e719bb36c782f56849a6b46bf2afab4)) to get a specified group attribute. If `keys` is set to `null`/`nil`, all the group attributes will be obtained.

> ? The `getGroupAttributes` API can be called by a logged-in user 20 times every five seconds in the SDK.

Sample code:

<dx-tabs>
::: Android
```java
V2TIMManager.getGroupManager().getGroupAttributes("groupA", null, new V2TIMValueCallback<Map<String, String>>() {
  @Override
  public void onSuccess(Map<String, String> stringStringMap) {
  	// Obtained successfully
  }

  @Override
  public void onError(int code, String desc) {
  	// Failed to obtain
  }
});
```
:::
::: iOS and macOS
```objectivec
[[V2TIMManager sharedInstance] getGroupAttributes:@"groupA" keys:nil succ:^(NSMutableDictionary<NSString *,NSString *> *groupAttributeList) {
    // Obtained successfully
} fail:^(int code, NSString *desc) {
    // Failed to obtain
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

auto callback = new ValueCallback<V2TIMGroupAttributeMap>{};
callback->SetCallback(
    [=](const V2TIMGroupAttributeMap& groupAttributeMap) {
        // The group attributes obtained successfully
        delete callback;
    },
    [=](int error_code, const V2TIMString& error_message) {
        // Failed to obtain the group attributes
        delete callback;
    });

V2TIMManager::GetInstance()->GetGroupManager()->GetGroupAttributes("groupID", {}, callback);
```
:::
</dx-tabs>

### Updating group attributes

If you have called `addGroupListener` to add a group event listener, all the group attributes will be called back through `onGroupAttributeChanged` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupListener.html#aa390fa93bc73a0262bdddb540227dc45) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/protocolV2TIMGroupListener-p.html#a7b76343c7ef46af4a2cd09db6d51db13) / [Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMGroupListener.html#a08aae62ce4f50a3787689404c2e4899a)) when a group attribute is changed.

Sample code:

<dx-tabs>
::: Android
```java
V2TIMManager.getInstance().addGroupListener(new V2TIMGroupListener() {
  @Override
  public void onGroupAttributeChanged(String groupID, Map<String, String> groupAttributeMap) {
  	// A group attribute was changed.
  }
});
```
:::
::: iOS and macOS
```objectivec
[[V2TIMManager sharedInstance] addGroupListener:self];
- (void)onGroupAttributeChanged:(NSString *)groupID attributes:(NSMutableDictionary<NSString *,NSString *> *)attributes {
    // A group attribute was changed.
}
```
:::
::: Windows
```cpp
class GroupListener final : public V2TIMGroupListener {
public:
    GroupListener() = default;
    ~GroupListener() override = default;

    void OnGroupAttributeChanged(const V2TIMString& groupID,
                                 const V2TIMGroupAttributeMap& groupAttributeMap) override {
        // A group attribute was changed.
    }
    // Other members …
};
// Add a group event listener. Keep `groupListener` valid before the listener is removed to ensure event callbacks are received.
GroupListener groupListener;
V2TIMManager::GetInstance()->AddGroupListener(&groupListener);
```
:::
</dx-tabs>
