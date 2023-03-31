## Overview
The group profile refers to the information about the group, such as group ID, group type, custom group field, and the number of joined members. It is saved in the `V2TIMGroupInfo` object, which is created and returned by the IM SDK and cannot be customized.
The methods to get the group profile are in the `V2TIMGroupManager(Android)` / `V2TIMManager(Group)(iOS and macOS)` core class.

[](id:getGroupInfo)
## Getting the Group Profile
Call `getGroupsInfo` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#ada614335043d548c11f121500e279154) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a9bca7e5318cfed44335566a783a6b568) / [Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMGroupManager.html#a8c98b92b45c3a2c4e57901e6c4cd3435)) to get the group profile. This API supports passing in multiple `groupID` values at a time to batch get group profiles.

Sample code:

<dx-tabs>
::: Android
```java
V2TIMManager.getGroupManager().getGroupsInfo(groupIDList, new V2TIMValueCallback<List<V2TIMGroupInfoResult>>() {
  @Override
  public void onSuccess(List<V2TIMGroupInfoResult> v2TIMGroupInfoResults) {
  	// Obtained the group profile successfully
  }

  @Override
  public void onError(int code, String desc) {
  	// Failed to obtain the group profile
  }
});
```
:::
::: iOS and macOS
```objectivec
[[V2TIMManager sharedInstance] getGroupsInfo:@[@"groupA"] succ:^(NSArray<V2TIMGroupInfoResult *> *groupResultList) {
    // Obtained the group profile successfully
} fail:^(int code, NSString *desc) {
    // Failed to obtain the group profile
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
groupIDList.PushBack("group1");

auto callback = new ValueCallback<V2TIMGroupInfoResultVector>{};
callback->SetCallback(
    [=](const V2TIMGroupInfoResultVector& groupInfoResultList) {
        // Obtained the group profile successfully
        delete callback;
    },
    [=](int error_code, const V2TIMString& error_message) {
        // Failed to obtain the group profile
        delete callback;
    });
V2TIMManager::GetInstance()->GetGroupManager()->GetGroupsInfo(groupIDList, callback);
```
:::
</dx-tabs>

[](id:setGroupInfo)
## Modifying Group Profiles
Call `setGroupInfo` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#ad4ceef92975fa00c4a5dddc8f7e1edcf) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#aa9519a479493e56d7920e40aba796144) / [Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMGroupManager.html#a10785c46e166879250c2c2ba2001b354)) to modify the group profile.

If you have called `addGroupListener` to add a group event listener, after the group profile is modified, all the group members will receive the `onGroupInfoChanged` callback ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupListener.html#ac3a88ea430c6dc35845472ed98ad049b) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/protocolV2TIMGroupListener-p.html#abbe2208a234d77364bff697eea503d27) / [Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMGroupListener.html#a37aa57b23295e6b295413fafba2eda07)).

Member roles that can modify the group profile vary by group type as follows:

| Group Type                     | Member Roles Allowed to Modify the Group Profile |
| ------------------------------ | ------------------------------------------------ |
| Work group (Work)              | All group members                                |
| Public group (Public)          | Group owner and admin                            |
| Meeting group (Meeting)        | Group owner and admin                            |
| Community (Community)          | Group owner and admin                            |
| Audio-video group (AVChatRoom) | Group owner                                      |

> ! Not all the fields of the group profile `V2TIMGroupInfo` can be modified, but only those writable.

Sample code:
<dx-tabs>
::: Android
```java
// Sample code: Modify group profile
V2TIMGroupInfo v2TIMGroupInfo = new V2TIMGroupInfo();
v2TIMGroupInfo.setGroupID("Group ID of the group to be modified");
v2TIMGroupInfo.setFaceUrl("http://xxxx");
V2TIMManager.getGroupManager().setGroupInfo(v2TIMGroupInfo, new V2TIMCallback() {
  @Override
  public void onSuccess() {
  	// Modified the group profile successfully
  }
  
  @Override
  public void onError(int code, String desc) {
  	// Failed to modify the group profile
  }
});
```
:::
::: iOS and macOS
```objectivec
V2TIMGroupInfo *info = [[V2TIMGroupInfo alloc] init];
info.groupID = @"Group ID of the group to be modified";
info.faceURL = @"http://xxxx";
[[V2TIMManager sharedInstance] setGroupInfo:info succ:^{
    // Modified the group profile successfully
} fail:^(int code, NSString *desc) {
    // Failed to modify the group profile
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

V2TIMGroupInfo info;
info.groupID = "Group ID to be modified";
info.faceURL = "http://xxxx";
info.modifyFlag |= V2TIM_GROUP_INFO_MODIFY_FLAG_FACE_URL;

auto callback = new Callback;
callback->SetCallback(
    [=]() {
        // Modified the group profile successfully
        delete callback;
    },
    [=](int error_code, const V2TIMString& error_message) {
        // Failed to modify the group profile
        delete callback;
    });

V2TIMManager::GetInstance()->GetGroupManager()->SetGroupInfo(info, callback);
```
:::
</dx-tabs>


[](id:setGroupInfoCustomInfo)
## Setting a Custom Group Field
The `customInfo` attribute in the `V2TIMGroupInfo` group profile is the custom group field, which can be modified by calling the `setGroupInfo` API mentioned in the previous section.

Unlike setting other fields in `V2TIMGroupInfo`, setting the custom group field involves two steps:
1. In the [IM console](https://console.cloud.tencent.com/im), configure the `key` of the custom group field. The `key` is a string of up to 16 bytes. If the `key` is not preconfigured, setting the `key-value` will fail. The configuration page is as shown below:
    <img src="https://qcloudimg.tencent-cloud.cn/raw/446a7e97dce929f68de190567a807449.png" style="zoom:30%;" />

2. Call the `setGroupInfo` API to set the field with up to 512 bytes.

>!
>1. You can set up to ten custom fields, which cannot be deleted and whose name and type cannot be changed.
>2. The custom field is mainly used to ensure compatibility with v1 and v2. If you use the API on v2, we recommend you use the `initGroupAttributes` API to set the group attribute. This allows for greater flexibility (requiring no configuration in the console) and storage (up to 16 KB). For more information, see [Custom Group Attribute](https://intl.cloud.tencent.com/document/product/1047/48175).


[](id:setGroupReceiveMessageOpt)
## Setting the Group Message Receiving Option
Any group member can call the `setGroupReceiveMessageOpt` API ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a2735427ac22485626aea278a9d465b3e) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a379eeef926e41ec5d48287e7fb55b80a) / [Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMMessageManager.html#a866d06c28faf058f253f29be6f5b3fe2)) to change the group message receiving option. This setting will take effect only for the group member and will not affect the setting of other group members.

`V2TIMReceiveMessageOpt` has the following options:

| Message Receiving Option         | Description                                                  |
| -------------------------------- | ------------------------------------------------------------ |
| V2TIM_RECEIVE_MESSAGE            | Messages will be received when the user is online, and push notifications will be received when the user is offline. |
| V2TIM_NOT_RECEIVE_MESSAGE        | No group messages will be received.                          |
| V2TIM_RECEIVE_NOT_NOTIFY_MESSAGE | Messages will be received when the user is online, and no push notifications will be received when the user is offline. |

Different `V2TIMReceiveMessageOpt` options can be used to implement group message notification muting:

**No group messages will be received.**
With the group message receiving option set to `V2TIM_NOT_RECEIVE_MESSAGE`, no group message will be received, and the conversation list will not be updated.

**Group messages will be received but will not be notified to the user, and a badge without the unread count will be displayed on the conversation list UI.**
1. The group message receiving option is set to `V2TIM_RECEIVE_NOT_NOTIFY_MESSAGE`.
2. When the receiver receives a new group message and needs to update the conversation list, it can get the unread count through `unreadCount` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversation.html#ab6a7667ac8a9f7a17a38ee8e7caec98e) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMConversation.html#a816b83eb32d84ea5345f14ced92bb7f6) / [Windows](https://im.sdk.qcloud.com/doc/en/structV2TIMTopicInfo.html#a15eb6e4566938daff8b8e82e45549a78)) of `V2TIMConversation`.
3. The receiver displays a badge rather than the unread count when identifying the group message receiving option as `V2TIM_RECEIVE_NOT_NOTIFY_MESSAGE` based on the `recvOpt` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversation.html#a82f673186669d31f7acd38c52d412ba2) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMConversation.html#a851651878491c64d73aa83131134e6cc) / [Windows](https://im.sdk.qcloud.com/doc/en/structV2TIMTopicInfo.html#a851651878491c64d73aa83131134e6cc)) of `V2TIMConversation`.

> ? As this method requires the `unreadCount` feature, it applies only to work groups (Work), public groups (Public), and communities (Community), but not to audio-video groups (AVChatRoom) or meeting groups (Meeting). For more information on group types, see [Group System](https://intl.cloud.tencent.com/document/product/1047/33529).

Sample code:

<dx-tabs>
::: Android
```java
V2TIMManager.getMessageManager().setGroupReceiveMessageOpt("groupA", V2TIMMessage.V2TIM_RECEIVE_NOT_NOTIFY_MESSAGE, new V2TIMCallback() {
  @Override
  public void onSuccess() {
  	// Changed the group message receiving option successfully
  }

  @Override
  public void onError(int code, String desc) {
  	// Failed to change the group message receiving option
  }
});
```
:::
::: iOS and macOS
```objectivec
[[V2TIMManager sharedInstance] setGroupReceiveMessageOpt:@"groupA" opt:V2TIM_RECEIVE_NOT_NOTIFY_MESSAGE succ:^{
    // Changed the group message receiving option successfully
} fail:^(int code, NSString *desc) {
    // Failed to change the group message receiving option
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
V2TIMReceiveMessageOpt opt = V2TIMReceiveMessageOpt::V2TIM_RECEIVE_NOT_NOTIFY_MESSAGE;

auto callback = new Callback;
callback->SetCallback(
    [=]() {
        // Changed the group message receiving option successfully
        delete callback;
    },
    [=](int error_code, const V2TIMString& error_message) {
        // Failed to change the group message receiving option
        delete callback;
    });

V2TIMManager::GetInstance()->GetMessageManager()->SetGroupReceiveMessageOpt(groupID, opt, callback);
```
:::
</dx-tabs>
