## Overview

Starting from v7.0, Tencent Cloud Chat SDK provides the group counter feature. You can configure a certain number of counters for each group.

Unlike [custom group attributes](https://intl.cloud.tencent.com/document/product/1047/48175), group counters are used to store data of integer type. Group counters can be used to store additional information related to a group, such as the cumulative number of viewers, the number of views, the number of likes, and the number of gifts the audience has given to the host of an audio-video group.

Group counter related methods are all in the core classes `V2TIMGroupManager(Android)` / `V2TIMManager(Group)(iOS & Mac)` / `V2TIMGroupManager(Windows)`.

> ? 
>
> - Group counters support all types of groups, excluding topic-enabled community groups.
> - The group counter feature is supported only by the Ultimate edition.

Keep the following in mind for group counters:

1. A single group supports up to 20 group counters, that is, up to 20 keys per group.
2. For a single group counter, the key can contain up to 128 bytes, and the value must be of integer type (signed integer of up to 64 bits).
3. The `setGroupCounters`, `increaseGroupCounter`, and `decreaseGroupCounter` APIs together can be called by a logged-in user up to 20 times every five seconds in the SDK, and the 8516 error code will be called back if the limit is exceeded.
4. The `getGroupCounters` API can be called by a logged-in user up to 20 times every five seconds in the SDK, and the 8516 error code will be called back if the limit is exceeded.



[](id:set)

## Setting Group Counters

Call the `setGroupCounters` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#ab2359bff0ebe5a07a87242023206989f) / [iOS & macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a712b2338d3ea7b8e810111db12709c35) / [Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMGroupManager.html#a7d1499e0f99112bacbb8b5e23b25285a)) API to set group counters. After group counters are set, the `onGroupCounterChanged` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupListener.html#ad3fc730f8c2464af81a6f713cad22899) / [iOS & Mac](https://im.sdk.qcloud.com/doc/en/protocolV2TIMGroupListener-p.html#acca36db98ccd17f98f2693e9ddb077e7) / [Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMGroupListener.html#a0e7c34f9dc2368e275d44ebfdaf605f6)) callback will be triggered. For usage of the `onGroupCounterChanged` callback, see [Group Counter Change Notification](#notify).

> ? 
>
> - If the `key` of the group counter to be set already exists, the value of `key` is updated directly. Otherwise, a key-value pair will be added.
> - If multiple users set the same counter at the same time, the final value of the counter will be used. It's recommended that the group owner performs counter setting operations.



Sample: Call the `setGroupCounters` API to set the values of counters `key1` and `key2` to 0

<dx-tabs>

::: Android

```java
HashMap<String, Long> counters = new HashMap<>();
counters.put("key1", 0);
counters.put("key2", 0);
V2TIMManager.getGroupManager().setGroupCounters("your group id", counters, new V2TIMValueCallback<Map<String, Long>>(){
    @Override
    public void onError(int code, String desc) {
        Log.d(TAG, "set group counters fail");
    }

    @Override
    public void onSuccess(Map<String, Long> stringLongMap) {
        Log.d(TAG, "set group counters succ");
    }
});
```

:::

::: iOS and macOS

```objectivec
NSDictionary *counters = @{
    @"key1": @(0),
    @"key2": @(0)
};
[V2TIMManager.sharedInstance setGroupCounters:@"your group id" counters:counters succ:^(NSDictionary<NSString *,NSNumber *> *groupCounters) {
    NSLog(@"set group counters succ");
} fail:^(int code, NSString *desc) {
    NSLog(@"set group counters fail");
}];
```

:::

::: Windows

```c++
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

void setGroupCounters() {
    V2TIMString groupID = "your group id";
    V2TIMStringToInt64Map counters;
    counters.Insert("key1", 0);
    counters.Insert("key2", 0);

    auto callback = new ValueCallback<V2TIMStringToInt64Map>{};
    callback->SetCallback(
        [=](const V2TIMStringToInt64Map &counters){
            // succ
        },
        [=](int error_code, const V2TIMString& error_message){
            // fail
        });
    V2TIMManager::GetInstance()->GetGroupManager()->SetGroupCounters(groupID, counters, callback);
}
```

:::

</dx-tabs>



[](id:increase)

## Incrementing the Value of a Group Counter

Call the `increaseGroupCounter` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#ad770cab3620a21671d7f83776d56814e) / [iOS & macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a58647ae926410735a0e9b83c3ae05406) / [Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMGroupManager.html#aad7d2b26a8948368d49405313b07aef9)) API to increment the value of a group counter. After the value of the group counter is incremented, the `onGroupCounterChanged` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupListener.html#ad3fc730f8c2464af81a6f713cad22899) / [iOS & Mac](https://im.sdk.qcloud.com/doc/en/protocolV2TIMGroupListener-p.html#acca36db98ccd17f98f2693e9ddb077e7) / [Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMGroupListener.html#a0e7c34f9dc2368e275d44ebfdaf605f6)) callback will be triggered. For the usage of the `onGroupCounterChanged` callback, see [Group Counter Change Notification](#notify).

> ? 
>
> - The API parameter `value` is the change value. Each time when the API is called, the current value is incremented by the value passed in.
> - If the `key` of the group counter to be set already exists, the current value is directly incremented by the value passed in. Otherwise, a `key` will be added, and the default value (0) is incremented by the value passed in.



Sample: Assume that the current value of counter `key1` is 8. After you call the `increaseGroupCounter` API to pass in an increment value 2, the final value of `key1` becomes 10.

<dx-tabs>

::: Android

```java
V2TIMManager.getGroupManager().increaseGroupCounter("your group id", "key1", 2, new V2TIMValueCallback<Map<String, Long>>(){
    @Override
    public void onError(int code, String desc) {
        Log.d(TAG, "increase group counters fail");
    }

    @Override
    public void onSuccess(Map<String, Long> stringLongMap) {
        Log.d(TAG, "increase group counters succ");
    }
});
```

:::

::: iOS and macOS

```objectivec
[V2TIMManager.sharedInstance increaseGroupCounter:@"your group id" key:@"key1" value:2 succ:^(NSDictionary<NSString *,NSNumber *> *groupCounters) {
    NSLog(@"increase group counters succ");
} fail:^(int code, NSString *desc) {
    NSLog(@"increase group counters fail");
}];
```

:::

::: Windows

```c++
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

void increaseGroupCounters() {
    V2TIMString groupID = "your group id";
	  V2TIMString key = "key1";
  	int64_t value = 2;

    auto callback = new ValueCallback<V2TIMStringToInt64Map>{};
    callback->SetCallback(
        [=](const V2TIMStringToInt64Map &counters){
            // succ
        },
        [=](int error_code, const V2TIMString& error_message){
            // fail
        });
    V2TIMManager::GetInstance()->GetGroupManager()->IncreaseGroupCounter(groupID, key, value, callback);
}
```

:::

</dx-tabs>



[](id:decrease)

## Decrementing the Value of a Group Counter

Call the `decreaseGroupCounter` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#ad5841f8f77442c8d0cf1a209a55db6c2) / [iOS & macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a9fb85e6cf4ad0e538de955c46833bafb) / [Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMGroupManager.html#acb406ccc5755b5e6fbb687dfc153201f)) API to decrement the value of a group counter. After the value of the group counter is decremented, the `onGroupCounterChanged` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupListener.html#ad3fc730f8c2464af81a6f713cad22899) / [iOS & macOS](https://im.sdk.qcloud.com/doc/en/protocolV2TIMGroupListener-p.html#acca36db98ccd17f98f2693e9ddb077e7) / [Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMGroupListener.html#a0e7c34f9dc2368e275d44ebfdaf605f6)) callback will be triggered. For the usage of the `onGroupCounterChanged` callback, see [Group Counter Change Notification](#notify).

> ?
>
> - The API parameter `value` is the change value. Each time when the API is called, the current value is decremented by the value passed in.
> - If the `key` of the group counter to be set already exists, the current value is directly decremented by the value passed in. Otherwise, a `key` will be added, and the default value (0) is decremented by the value passed in.



Sample: Assume that the current value of counter `key1` is 8. After you call the `decreaseGroupCounter` API to pass in a decrement value 2, the final value of `key1` becomes 6.

<dx-tabs>

::: Android

```java
V2TIMManager.getGroupManager().decreaseGroupCounter("your group id", "key1", 2, new V2TIMValueCallback<Map<String, Long>>(){
    @Override
    public void onError(int code, String desc) {
        Log.d(TAG, "decrease group counters fail");
    }

    @Override
    public void onSuccess(Map<String, Long> stringLongMap) {
        Log.d(TAG, "decrease group counters succ");
    }
});
```

:::

::: iOS and macOS

```objectivec
[V2TIMManager.sharedInstance decreaseGroupCounter:@"your group id" key:@"key1" value:2 succ:^(NSDictionary<NSString *,NSNumber *> *groupCounters) {
    NSLog(@"decrease group counters succ");
} fail:^(int code, NSString *desc) {
    NSLog(@"decrease group counters fail");
}];
```

:::

::: Windows

```c++
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

void decreaseGroupCounters() {
    V2TIMString groupID = "your group id";
	  V2TIMString key = "key1";
  	int64_t value = 2;

    auto callback = new ValueCallback<V2TIMStringToInt64Map>{};
    callback->SetCallback(
        [=](const V2TIMStringToInt64Map &counters){
            // succ
        },
        [=](int error_code, const V2TIMString& error_message){
            // fail
        });
    V2TIMManager::GetInstance()->GetGroupManager()->decreaseGroupCounter(groupID, key, value, callback);
}
```

:::

</dx-tabs>



[](id:get)

## Getting Group Counters

Call the `getGroupCounters` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a3f70b0f1054a7bf78a9069a01b842cad) / [iOS & macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#ab4e9e7fd4c6db5f979faf7f103dc5bd6) / [Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMGroupManager.html#a4d627b72fef42e640ece749ea8fa8ccd)) API to pass in a set of keys to get the information of the corresponding group counters. The API will return all key-value pairs matching the keys passed in.

> ? If the key list passed in is empty, all group counters are returned.

Sample: Call the `getGroupCounters` API to get the values of group counters `key1` and `key2`

<dx-tabs>

::: Android

```java
List<String> keyList = Arrays.asList("key1", "key2");
V2TIMManager.getGroupManager().getGroupCounters("your group id", keyList, new V2TIMValueCallback<Map<String, Long>>() {
    @Override
    public void onError(int code, String desc) {
        Log.d(TAG, "get group counters fail");
    }

    @Override
    public void onSuccess(Map<String, Long> stringLongMap) {
        Log.d(TAG, "get group counters succ");
    }
});
```

:::

::: iOS and macOS

```objectivec
[V2TIMManager.sharedInstance getGroupCounters:@"your group id" keys:@[@"key1", @"key2"] succ:^(NSDictionary<NSString *,NSNumber *> *groupCounters) {
    NSLog(@"get group counters succ");
} fail:^(int code, NSString *desc) {
    NSLog(@"get group counters fail");
}];
```

:::

::: Windows

```c++
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

void getGroupCounters() {
    V2TIMString groupID = "your group id";
    V2TIMStringVector keys;
    keys.PushBack("key1");
    keys.PushBack("key2");

    auto callback = new ValueCallback<V2TIMStringToInt64Map>{};
    callback->SetCallback(
        [=](const V2TIMStringToInt64Map &counters){
            // succ
        },
        [=](int error_code, const V2TIMString& error_message){
            // fail
        });
    V2TIMManager::GetInstance()->GetGroupManager()->GetGroupCounters(groupID, keys, callback);
}
```

:::

</dx-tabs>



[](id:notify)

## Group Counter Change Notification

When you call the `setGroupCounters`, `increaseGroupCounter`, or `decreaseGroupCounter` API to modify group counters, the SDK will trigger the `onGroupCounterChanged` callback and return the updated values.

> ? Before you can use the above-mentioned callback, you need to call the `addGroupListener` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupListener.html#ad3fc730f8c2464af81a6f713cad22899) / [iOS & macOS](https://im.sdk.qcloud.com/doc/en/protocolV2TIMGroupListener-p.html#acca36db98ccd17f98f2693e9ddb077e7) / [Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMGroupListener.html#a0e7c34f9dc2368e275d44ebfdaf605f6)) API to add a group listener.

Sample code:

<dx-tabs>

::: Android

```java
private void initListener() {
    if (groupListener == null) {
        groupListener = new V2TIMGroupListener() {
            @Override
            public void onGroupCounterChanged(String groupID, String key, long newValue) {
                StringBuilder stringBuilder = new StringBuilder();
                stringBuilder.append("onGroupCounterChanged groupID:").append(groupID).append("\n");
                stringBuilder.append("key:").append(key).append(", newValue:").append(String.valueOf(newValue)).append("\n");
                String result = "onGroupCounterChanged :" + stringBuilder.toString();
                Log.d(TAG, result);
            }
        };
        V2TIMManager.getInstance().addGroupListener(groupListener);
    }
}
```

:::

::: iOS and macOS

```objectivec
[V2TIMManager.sharedInstance addGroupListener:self];

#pragma mark - V2TIMGroupListener
- (void)onGroupCounterChanged:(NSString *)groupID key:(NSString *)key newValue:(NSInteger)newValue {
    NSLog(@"groupID:%@, changed:\n%@:%zd\n", groupID, key, newValue);
}
```

:::

::: Windows

```c++
class GroupListener final : public V2TIMGroupListener {
public:
    GroupListener() = default;
    ~GroupListener() override = default;
    
    void OnGroupCounterChanged(const V2TIMString &groupID, const V2TIMString &key, int64_t newValue) override {
        // changed
    }
};

GroupListener listener;
V2TIMManager::GetInstance()->AddGroupListener(&listener);
```

:::

</dx-tabs>



[](id:feedback)
