## Feature Description
The class for the group member profile is `V2TIMGroupMemberFullInfo`, which contains the `userID`, custom information, role, and muting information of the group member.
The methods are in the `V2TIMGroupManager(Android)` / `V2TIMManager(Group)(iOS and macOS)` core class.

[](id:getGroupMembersInfo)
## Getting the Profile of Group Members
You can call `getGroupMembersInfo` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#adb08e1c4fa9aff407c7b2678757f66d5) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a1ab284b80811bcc697d689d7b97edf04) / [Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMGroupManager.html#a6db2fcfd78bbd71003ae31584c88c672)) to get the group member profile. This API supports passing in multiple `userID` values at a time to get group member profiles in batch and therefore improve the network transfer efficiency.

Sample code:

<dx-tabs>
::: Android
```java
List<String> userIDList = new ArrayList<>();
userIDList.add("userA");
userIDList.add("userB");
V2TIMManager.getGroupManager().getGroupMembersInfo("groupA", userIDList, new V2TIMValueCallback<List<V2TIMGroupMemberFullInfo>>() {
  @Override
  public void onSuccess(List<V2TIMGroupMemberFullInfo> v2TIMGroupMemberFullInfos) {
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
[[V2TIMManager sharedInstance] getGroupMembersInfo:@"groupA" memberList:@[@"user1"] succ:^(NSArray<V2TIMGroupMemberFullInfo *> *memberList) {
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

V2TIMString groupID = "groupA";
V2TIMStringVector memberList;
memberList.PushBack("userA");
memberList.PushBack("userB");

auto callback = new ValueCallback<V2TIMGroupInfoVector>{};
callback->SetCallback(
    [=](const V2TIMGroupMemberFullInfoVector& groupMemberFullInfoList) {
        // Obtained successfully
        delete callback;
    },
    [=](int error_code, const V2TIMString& error_message) {
        // Failed to obtain
        delete callback;
    });

V2TIMManager::GetInstance()->GetGroupManager()->GetGroupMembersInfo(groupID, memberList, callback);
```
:::
</dx-tabs>

[](id:setGroupMemberInfo)
## Modifying Group Member Profiles
The group owner or admin can call the `setGroupMemberInfo` API ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a6f1cf8ede41348b4cd7b63b8e4caa77b) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a40b97ee4b138f93e1b2073d1bdff3756) / [Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMGroupManager.html#acd0e222e4c3d5997666aaf4126bd974e)) to modify the group name card (`nameCard`), custom field (`customInfo`), and other information of a group member.

Ordinary group members can call `setGroupMemberInfo` to set their group name card (`nameCard`) and custom field (`customInfo`).

> ? As an audio-video group (AVChatRoom) doesn't store group member information, the name card of a group member cannot be set.

To modify a custom group member field, you must configure it in the [IM console](https://console.cloud.tencent.com/im) in advance as follows:
<img src="https://qcloudimg.tencent-cloud.cn/raw/9cd876542e8082db92d05810fd883b8d.png" alt="" style="zoom:90%;" />

> ! You can set up to five custom group member fields, which cannot be deleted and whose name and type cannot be changed.

Sample code:

<dx-tabs>
::: Android

```java
V2TIMGroupMemberFullInfo memberFullInfo = new V2TIMGroupMemberFullInfo();
// Specify a group member
memberFullInfo.setUserID("userA");
// Set the `nameCard` value to be modified
memberFullInfo.setNameCard("userA_namecard");
// Set a group member custom field
Map<String, byte[]> customMap = new HashMap<>();
customMap.put("member_key1", "value1".getBytes());
memberFullInfo.setCustomInfo(customMap);
V2TIMManager.getGroupManager().setGroupMemberInfo("groupA", memberFullInfo, new V2TIMCallback() {
  @Override
  public void onSuccess() {
		// Modified successfully
  }

  @Override
  public void onError(int code, String desc) {
		// Failed to modify
  }
});
```
:::
::: iOS and macOS
```objectivec
V2TIMGroupMemberFullInfo *memberFullInfo = [[V2TIMGroupMemberFullInfo alloc] init];
// Specify a group member
memberFullInfo.userID = @"user1";
// Set the `nameCard` value to be modified
memberFullInfo.nameCard = @"user1_namecard";
// Set a group member custom field
memberFullInfo.customInfo = @{@"member_key1" : [@"value1" dataUsingEncoding:NSUTF8StringEncoding]};
[[V2TIMManager sharedInstance] setGroupMemberInfo:@"groupA" info:memberFullInfo succ:^{
    // Modified successfully
} fail:^(int code, NSString *desc) {
    // Failed to modify
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

// Specify a group member
V2TIMGroupMemberFullInfo info;
info.userID = "userA";
// Set the `nameCard` value to be modified
info.nameCard = "userA_namecard";
info.modifyFlag = V2TIMGroupMemberInfoModifyFlag::V2TIM_GROUP_MEMBER_INFO_MODIFY_FLAG_NAME_CARD;
// Set a group member custom field
V2TIMCustomInfo customInfo;
std::string str{u8"value1"};
customInfo.Insert("member_key1", {reinterpret_cast<const uint8_t*>(str.data()), str.size()});
info.customInfo = customInfo;
info.modifyFlag |= V2TIMGroupMemberInfoModifyFlag::V2TIM_GROUP_MEMBER_INFO_MODIFY_FLAG_CUSTOM_INFO;

auto callback = new Callback;
callback->SetCallback(
    [=]() {
        // Modified successfully
        delete callback;
    },
    [=](int error_code, const V2TIMString& error_message) {
        // Failed to modify
        delete callback;
    });

V2TIMManager::GetInstance()->GetGroupManager()->SetGroupMemberInfo("userA", info, callback);
```
:::
</dx-tabs>
