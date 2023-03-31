## Overview
You can set the message receiving option for a one-to-one or group chat to implement the notification muting feature.
The IM SDK supports the following three message receiving options as defined in `V2TIMReceiveMessageOpt`:

| Message Receiving Option         | Feature Description                                          |
| -------------------------------- | ------------------------------------------------------------ |
| V2TIM_RECEIVE_MESSAGE            | Messages will be received when the user is online, and offline push notifications will be received when the user is offline. |
| V2TIM_NOT_RECEIVE_MESSAGE        | Messages will not be received no matter whether the user is online or offline. |
| V2TIM_RECEIVE_NOT_NOTIFY_MESSAGE | Messages will be received when the user is online, and offline push notifications will not be received when the user is offline. |

> ? The message receiving options are supported only by the SDK of the Enhanced edition on v5.3.425 or later.

Different `V2TIMReceiveMessageOpt` options can be set to implement group message notification muting:

**No messages will be received.**
After the message receiving option is set to `V2TIM_NOT_RECEIVE_MESSAGE`, no one-to-one or group messages will be received, and the conversation list will not be updated.

**Messages will be received but will not be notified to the user, and a badge without the unread count will be displayed on the conversation list UI.**
1. The message receiving option is set to `V2TIM_RECEIVE_NOT_NOTIFY_MESSAGE`.
2. When the receiver receives a one-to-one or group message and needs to update the conversation list, it can get the unread count through the `unreadCount` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversation.html#ab6a7667ac8a9f7a17a38ee8e7caec98e) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMConversation.html#a816b83eb32d84ea5345f14ced92bb7f6) / [Windows](https://im.sdk.qcloud.com/doc/en/structV2TIMTopicInfo.html#a15eb6e4566938daff8b8e82e45549a78)) in the `V2TIMConversation` of the conversation.
3. The receiver displays a badge rather than the unread count when identifying the message receiving option as `V2TIM_RECEIVE_NOT_NOTIFY_MESSAGE` based on the `recvOpt` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversation.html#a82f673186669d31f7acd38c52d412ba2) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMConversation.html#a851651878491c64d73aa83131134e6cc) / [Windows](https://im.sdk.qcloud.com/doc/en/structV2TIMTopicInfo.html#a851651878491c64d73aa83131134e6cc)) of `V2TIMConversation`.

> ? As this method requires the `unreadCount` feature, it applies only to work groups (Work), public groups (Public), and communities (Community), but not to audio-video groups (AVChatRoom) or meeting groups (Meeting). For more information on group types, see [Group System](https://intl.cloud.tencent.com/document/product/1047/33529).


## Setting the Message Receiving Option for a One-to-One Chat
Call `setC2CReceiveMessageOpt` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a6524143895cdee25fabd9aeeae73a3c5) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#ae628f19d856921d27081c3f40005e9d9) / [Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMMessageManager.html#adf166f08b68a5df8de19d152bcf868b3)) to set the message receiving option for a one-to-one chat.
You can use the `userIDList` parameter to specify up to 30 users at a time.

> ! This API can be called by a user up to 5 times every second.

Sample code:
<dx-tabs>
::: Android
```java
// Set not to receive messages no matter whether the user is online or offline

List<String> userList = new ArrayList<>();
userList.add("user1");
userList.add("user2");

V2TIMManager.getMessageManager().setC2CReceiveMessageOpt(userList, V2TIMMessage.V2TIM_NOT_RECEIVE_MESSAGE, new V2TIMCallback() {
    @Override
    public void onSuccess() {
        Log.i("imsdk", "success");
    }

    @Override
    public void onError(int code, String desc) {
        Log.i("imsdk", "failure, code:" + code + ", desc:" + desc);
    }
});
```
:::
::: iOS and macOS
```objectivec
// Set not to receive messages no matter whether the user is online or offline

NSArray* array = [NSArray arrayWithObjects:@"user1", @"user2", nil]];
[[V2TIMManager sharedInstance] setC2CReceiveMessageOpt:array opt:V2TIM_NOT_RECEIVE_MESSAGE succ:^{
    NSLog(@"success");
} fail:^(int code, NSString *desc) {
    NSLog(@"failure, code:%d, desc:%@", code, desc);
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

V2TIMStringVector userIDList;
userIDList.PushBack("user1");
userIDList.PushBack("user2");
V2TIMReceiveMessageOpt opt = V2TIMReceiveMessageOpt::V2TIM_NOT_RECEIVE_MESSAGE;

auto callback = new Callback;
callback->SetCallback(
    [=]() {
        // Configured successfully
        delete callback;
    },
    [=](int error_code, const V2TIMString& error_message) {
        // Failed to configure
        delete callback;
    });

V2TIMManager::GetInstance()->GetMessageManager()->SetC2CReceiveMessageOpt(userIDList, opt, callback);
```
:::
</dx-tabs>

## Getting the Message Receiving Option for a One-to-One Chat
Call `getC2CReceiveMessageOpt` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a9693dd66432f931ac0a1f2168d899501) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a1c743a6fe1d17a21dc80e584fd1de2d1) / [Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMMessageManager.html#a30a4979460e73c897b6130ba40356afa)) to get the message receiving option for a one-to-one chat.

Sample code:
<dx-tabs>
::: Android
```java
List<String> userList = new ArrayList<>();
userList.add("user1");
userList.add("user2");

V2TIMManager.getMessageManager().getC2CReceiveMessageOpt(userList, new V2TIMValueCallback<List<V2TIMReceiveMessageOptInfo>>() {
    @Override
    public void onSuccess(List<V2TIMReceiveMessageOptInfo> v2TIMReceiveMessageOptInfos) {
        for (int i = 0; i < v2TIMReceiveMessageOptInfos.size(); i++){
            V2TIMReceiveMessageOptInfo info = v2TIMReceiveMessageOptInfos.get(i);
            Log.i("imsdk", "userId: " + info.getUserID() ", receiveOpt: " + info.getC2CReceiveMessageOpt());
        }
    }

    @Override
    public void onError(int code, String desc) {
        Log.i("imsdk", "failure, code:" + code + ", desc:" + desc);
    }
});
```
:::
::: iOS and macOS
```objectivec
NSArray* array = [NSArray arrayWithObjects:@"user1", @"user2", nil]];
[[V2TIMManager sharedInstance] getC2CReceiveMessageOpt:array succ:^(NSArray<V2TIMReceiveMessageOptInfo *> *optList) {
    for (int i = 0; i < optList.count; i++) {
        V2TIMReceiveMessageOptInfo* info = optList[i];
        NSLog(@"userId: %@, receiveOpt: %@", info.userID, info.receiveOpt);
    }
} fail:^(int code, NSString *desc) {
    NSLog(@"failure, code:%d, desc:%@", code, desc);
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

V2TIMStringVector userIDList;
userIDList.PushBack("user1");
userIDList.PushBack("user2");

auto callback = new ValueCallback<V2TIMReceiveMessageOptInfoVector>{};
callback->SetCallback(
    [=](const V2TIMReceiveMessageOptInfoVector& receiveMessageOptInfoList) {
        for (size_t i = 0; i < receiveMessageOptInfoList.Size(); ++i) {
            const V2TIMReceiveMessageOptInfo& opt = receiveMessageOptInfoList[i];
            V2TIMString userID = opt.userID;
            V2TIMReceiveMessageOpt receiveOpt = opt.receiveOpt;
        }

        delete callback;
    },
    [=](int error_code, const V2TIMString& error_message) {
        // Failed to obtain
        delete callback;
    });

V2TIMManager::GetInstance()->GetMessageManager()->GetC2CReceiveMessageOpt(userIDList, callback);
```
:::
</dx-tabs>


## Setting the Message Receiving Option for a Group Chat
Call `setGroupReceiveMessageOpt` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a2735427ac22485626aea278a9d465b3e) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a379eeef926e41ec5d48287e7fb55b80a) / [Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMMessageManager.html#a866d06c28faf058f253f29be6f5b3fe2)) to set the message receiving option for a group chat.

Sample code:
<dx-tabs>
::: Android
```java
// Set not to receive messages no matter whether the user is online or offline

String groupID = "groupID";
V2TIMManager.getMessageManager().setGroupReceiveMessageOpt(groupID, V2TIMMessage.V2TIM_NOT_RECEIVE_MESSAGE, new V2TIMCallback() {
    @Override
    public void onSuccess() {
        Log.i("imsdk", "success");
    }

    @Override
    public void onError(int code, String desc) {
        Log.i("imsdk", "failure, code:" + code + ", desc:" + desc);
    }
});
```
:::
::: iOS and macOS
```objectivec
// Set not to receive messages no matter whether the user is online or offline

NSString *groupID = @"groupID";
[[V2TIMManager sharedInstance] setGroupReceiveMessageOpt:groupID opt:V2TIM_NOT_RECEIVE_MESSAGE succ:^{
    NSLog(@"success");
} fail:^(int code, NSString *desc) {
    NSLog(@"failure, code:%d, desc:%@", code, desc);
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

V2TIMString groupID = "groupID";
V2TIMReceiveMessageOpt opt = V2TIMReceiveMessageOpt::V2TIM_NOT_RECEIVE_MESSAGE;

auto callback = new Callback;
callback->SetCallback(
    [=]() {
        // Configured successfully
        delete callback;
    },
    [=](int error_code, const V2TIMString& error_message) {
        // Failed to configure
        delete callback;
    });

V2TIMManager::GetInstance()->GetMessageManager()->SetGroupReceiveMessageOpt(groupID, opt, callback);
```
:::
</dx-tabs>

## Getting the Message Receiving Option for a Group Chat
Call the `getGroupsInfo` API ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#ada614335043d548c11f121500e279154) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a9bca7e5318cfed44335566a783a6b568) / [Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMGroupManager.html#a8c98b92b45c3a2c4e57901e6c4cd3435)) to get the list of `V2TIMGroupInfo` objects in the group profile. Here, the `recvOpt` field of the object indicates the message receiving option for the group chat.

Sample code:
<dx-tabs>
::: Android
```java
List<String> groupIDList = new ArrayList<>();
groupIDList.add("groupID1");
groupIDList.add("groupID2");
V2TIMManager.getGroupManager().getGroupsInfo(groupIDList, new V2TIMValueCallback<List<V2TIMGroupInfoResult>>() {
    @Override
    public void onSuccess(List<V2TIMGroupInfoResult> v2TIMGroupProfileResults) {
        for (V2TIMGroupInfoResult result : v2TIMGroupProfileResults) {
            V2TIMGroupInfo info = result.getGroupInfo();
            Log.i("imsdk", "recvOpt: " + info.getRecvOpt());
        }
    }

    @Override
    public void onError(int code, String desc) {
        Log.i("imsdk", "failure, code:" + code + ", desc:" + desc);
    }
});
```
:::
::: iOS and macOS
```objectivec
NSArray* array = [NSArray arrayWithObjects:@"groupID1", @"groupID2", nil]];
[[V2TIMManager sharedInstance] getGroupsInfo:array succ:^(NSArray<V2TIMGroupInfoResult *> * groupResultList) {
    for (V2TIMGroupInfoResult *result in groupResultList){
        V2TIMGroupInfo *info = result.info;
        NSLog(@"recvOpt, %d", (int)info.recvOpt);
    }
} fail:^(int code, NSString *desc) {
    NSLog(@"failure, code:%d, desc:%@", code, desc);
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

V2TIMStringVector groupIDList;
groupIDList.PushBack("groupID1");
groupIDList.PushBack("groupID2");

auto callback = new ValueCallback<V2TIMGroupInfoResultVector>{};
callback->SetCallback(
    [=](const V2TIMGroupInfoResultVector& groupInfoResultList) {
        for (size_t i = 0; i < groupInfoResultList.Size(); ++i) {
            const V2TIMGroupInfo& info = groupInfoResultList[i].info;
            V2TIMReceiveMessageOpt recvOpt = info.recvOpt;
        }

        delete callback;
    },
    [=](int error_code, const V2TIMString& error_message) {
        // Failed to obtain
        delete callback;
    });

V2TIMManager::GetInstance()->GetGroupManager()->GetGroupsInfo(groupIDList, callback);
```
:::
</dx-tabs>
