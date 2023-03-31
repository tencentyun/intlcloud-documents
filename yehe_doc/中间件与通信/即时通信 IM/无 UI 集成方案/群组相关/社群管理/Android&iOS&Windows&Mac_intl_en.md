## Feature Description
A community group is a large group of people brought together by common topics, and multiple topics can be created under the same community group based on different interests.
Communities are used to manage group members. All topics under the same community are shared among members, who can send and receive messages within each topic independently.

- Community and topic management APIs are in the `V2TIMGroupManager(Android)` / `V2TIMManager(Group)(iOS and macOS)` core class.
- APIs related to messages in topics are in the `V2TIMMessageManager(Android)` / `V2TIMManager(Message)(iOS and Mac)` core class.

> ? This feature is supported by v6.2.2363 or later. To use it, you need to [purchase the Ultimate edition](https://www.tencentcloud.com/document/product/1047/34577), go to the [**console**](https://console.cloud.tencent.com/im/qun-setting), choose **Feature Configuration** > **Group configuration** > **Group feature configuration** > **Community**, and enable the community feature.

## Community Group Management
### Creating a community group

You need to perform two steps to create a community group that supports topics:

1. Create the `V2TIMGroupInfo` object ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupInfo.html) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMGroupInfo.html) / [Windows](https://im.sdk.qcloud.com/doc/en/structV2TIMGroupInfo.html)) and set `groupType` to `Community` and `isSupportTopic` to `true`/`YES`.
2. Call the `createGroup` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a121d53137a38d0fc0bc8a8e0a9c55647) / [iOS & Mac](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a59824434b6096180b94d8152183dcd2c) / [Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMManager.html#a0325514b94a734186be684eb9bb5cc80)) API to create a group.

Sample code:
<dx-tabs>
::: Android
```java
V2TIMGroupInfo v2TIMGroupInfo = new V2TIMGroupInfo();
v2TIMGroupInfo.setGroupName("This is a Community");
v2TIMGroupInfo.setGroupType(V2TIMManager.GROUP_TYPE_COMMUNITY);
v2TIMGroupInfo.setSupportTopic(true);
V2TIMManager.getGroupManager().createGroup(v2TIMGroupInfo, null, new V2TIMValueCallback<String>() {
  @Override
  public void onSuccess(String groupID) {
    // Community group created successfully
  }

  @Override
  public void onError(int code, String desc) {
  	// Creation failed
  }
});
```
:::
::: iOS and macOS
```objectivec
V2TIMGroupInfo *groupInfo = [[V2TIMGroupInfo alloc] init];;
groupInfo.groupName = @"This is a Community";
groupInfo.groupType = GroupType_Community;
groupInfo.isSupportTopic = YES;
[[V2TIMManager sharedInstance] createGroup:groupInfo memberList:nil succ:^(NSString *groupID) {
    // Community group created successfully
} fail:^(int code, NSString *desc) {
    // Creation failed
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
    void OnError(int error_code, const V2TIMString &error_message) override {
        if (error_callback_) {
            error_callback_(error_code, error_message);
        }
    }

private:
    SuccessCallback success_callback_;
    ErrorCallback error_callback_;
};

V2TIMGroupInfo info;
info.groupType = "Community";
info.groupName = "This is a Community";
info.isSupportTopic = true;

auto callback = new ValueCallback<V2TIMString>{};
callback->SetCallback(
    [=](const V2TIMString& groupID) {
        // Community group created successfully
        delete callback;
    },
    [=](int error_code, const V2TIMString& error_message) {
        // Creation failed
        delete callback;
    });

V2TIMManager::GetInstance()->GetGroupManager()->CreateGroup(info, {}, callback);
```
:::
</dx-tabs>

### Getting the list of community groups joined
You can call the `getJoinedCommunityList`([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#acb37b83f357fc7ee04905f8bcd5a5c67) / [iOS & Mac](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a17350dec83b7cd32d308a1f2b2827fdd) / [Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMGroupManager.html#af131f5f9aa08f7ba81fd9b5632e60e0d)) API to get the list of topic supporting communities that you have joined.

Sample code:
<dx-tabs>
::: Android
```java
V2TIMManager.getGroupManager().getJoinedCommunityList(new V2TIMValueCallback<List<V2TIMGroupInfo>>() {
  @Override
  public void onSuccess(List<V2TIMGroupInfo> v2TIMGroupInfos) {
  	// Community group list got successfully
  }
  @Override
  public void onError(int code, String desc) {
  	// Failed to get the community group list
  }
});

```
:::
::: iOS and macOS
```objectivec
[[V2TIMManager sharedInstance] getJoinedCommunityList:^(NSArray<V2TIMGroupInfo *> *groupList) {
    // Community group list got successfully
} fail:^(int code, NSString *desc) {
    // Failed to get the community group list
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
    void OnError(int error_code, const V2TIMString &error_message) override {
        if (error_callback_) {
            error_callback_(error_code, error_message);
        }
    }

private:
    SuccessCallback success_callback_;
    ErrorCallback error_callback_;
};

auto callback = new ValueCallback<V2TIMGroupInfoVector>{};
callback->SetCallback(
    [=](const V2TIMGroupInfoVector& groupInfoList) {
        // Community group list obtained successfully
        delete callback;
    },
    [=](int error_code, const V2TIMString& error_message) {
        // Failed to get the community group list
        delete callback;
    });

V2TIMManager::GetInstance()->GetGroupManager()->GetJoinedCommunityList(callback);
```
:::
</dx-tabs>

### Other management APIs
Other features can be used in the same way as an ordinary group feature and involve the following APIs:

<table>
<tr>
<th width="15%">Category</th>
<th width="25%">Feature</th>
<th width="60%">API</th>
</tr>
<tr>
<td rowspan="5">Community group management</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/48466">Joining a Group</a></td>
<td>joinGroup (<a href="https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#ad64a09bea508672d6d5a402b3455b564">Android</a> / <a href="https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a4762156b7a98489eb4715de53028e12a">iOS and macOS)</a></td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/48466">Leaving a Group</a></td>
<td>quitGroup (<a href="https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a6d140dbeb44906de9cb69f69c2ce5919">Android</a> / <a href="https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#ac2a43b3ada447131df0c5f19e8079be5">iOS and macOS)</a></td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/48466">Disbanding a Group</a></td>
<td>dismissGroup (<a href="https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#afd0221c0c842a6dcfa0acc657e50caeb">Android</a> / <a href="https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a5bd55cb04867985253949d8cc78f860e">iOS and macOS)</a></td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/48185">Getting the Group Profile</a></td>
<td>getGroupsInfo (<a href="https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#ada614335043d548c11f121500e279154">Android</a> / <a href="https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a9bca7e5318cfed44335566a783a6b568">iOS and macOS)</a></td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/48185">Modifying the Group Profile</a></td>
<td>setGroupInfo (<a href="https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#ad4ceef92975fa00c4a5dddc8f7e1edcf">Android</a> / <a href="https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#aa9519a479493e56d7920e40aba796144">iOS and macOS)</a></td>
</tr>
<tr>
<td rowspan="4">Community group member management</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/48181">Getting the Group Member List</a></td>
<td>getGroupMemberList (<a href="https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a69fc0831aacaa0585c1855f4c91320be">Android</a> / <a href="https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a98681b9036e73acbe8f84737b5291326">iOS and macOS)</a></td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/48178">Getting the Profile of a Group Member</a></td>
<td>getGroupMembersInfo (<a href="https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#adb08e1c4fa9aff407c7b2678757f66d5">Android</a> / <a href="https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a1ab284b80811bcc697d689d7b97edf04">iOS and macOS)</a></td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/48178">Modifying the Profile of a Group Member</a></td>
<td>setGroupMemberInfo (<a href="https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a6f1cf8ede41348b4cd7b63b8e4caa77b">Android</a> / <a href="https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a40b97ee4b138f93e1b2073d1bdff3756">iOS and macOS)</a></td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/48181">Removing a Group Member</a></td>
<td>kickGroupMember (<a href="https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a6da6755c6e0c46e96cb02575074a5333">Android</a> / <a href="https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a0581f28fddf2ade890aa62e4318d7a97">iOS and macOS)</a></td>
</tr>
</table>

## Topic Management
Multiple topics can be created under the same community group. All the topics are shared among group members, who can send and receive messages within each topic independently.
>?To use the feature, you need to go to the [**console**](https://console.cloud.tencent.com/im/qun-setting), choose **Feature Configuration** > **Group configuration** > **Group feature configuration** > **Community**, enable the community feature and then enable the topic feature.

### Creating a topic

You need to perform two steps to create a topic:
1. Create the `V2TIMTopicInfo` object ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMTopicInfo.html) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMTopicInfo.html) / [Windows](https://im.sdk.qcloud.com/doc/en/structV2TIMTopicInfo.html)).
2. Call the `createTopicInCommunity` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a52eed1b07ad64a3aa3d3561d8cd147f0) / [iOS and Mac](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a8cc04d04254867787060cf1cae0fc5b8) / [Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMGroupManager.html#a4461759ad1c51eae318dfe5d478575c9)) API to create a topic.

Sample code:
<dx-tabs>
::: Android
```java
V2TIMTopicInfo topicInfo = new V2TIMTopicInfo();
topicInfo.setTopicName(topicName);
topicInfo.setTopicFaceUrl(topicFaceUrl);
topicInfo.setIntroduction(topicIntroduction);
topicInfo.setNotification(topicNotification);
topicInfo.setCustomString(topicCustomString);

// Set `groupID` to the ID of a community group that supports topics
V2TIMManager.getGroupManager().createTopicInCommunity(groupID, topicInfo, new V2TIMValueCallback<String>() {
  @Override
  public void onSuccess(String topicID) {
  	// Topic created successfully
  }

  @Override
  public void onError(int code, String desc) {
  	// Failed to create the topic
  }
});

```
:::
::: iOS and macOS
```objectivec
V2TIMTopicInfo *topicInfo = [[V2TIMTopicInfo alloc] init];
topicInfo.topicName = @"topicName";
topicInfo.topicFaceURL = @"topicFaceUrl";
topicInfo.introduction = @"topicIntroduction";
topicInfo.notification = @"topicNotification";
topicInfo.customString = @"topicCustomString";

// Set `groupID` to the ID of a community group that supports topics
[[V2TIMManager sharedInstance] createTopicInCommunity:@"groupID" topicInfo:topicInfo succ:^(NSString *topicID) {
    // Topic created successfully
} fail:^(int code, NSString *desc) {
    // Failed to create the topic
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
    void OnError(int error_code, const V2TIMString &error_message) override {
        if (error_callback_) {
            error_callback_(error_code, error_message);
        }
    }

private:
    SuccessCallback success_callback_;
    ErrorCallback error_callback_;
};

V2TIMTopicInfo topicInfo;
topicInfo.topicID = "topicID";
topicInfo.topicName = "topicName";
topicInfo.topicFaceURL = "topicFaceURL";
topicInfo.introduction = "introduction";
topicInfo.notification = "notification";

auto callback = new ValueCallback<V2TIMString>{};
callback->SetCallback(
    [=](const V2TIMString& string) {
        // Topic created successfully
        delete callback;
    },
    [=](int error_code, const V2TIMString& error_message) {
        // Failed to create the topic
        delete callback;
    });

// Set `groupID` to the ID of a community group that supports topics
V2TIMManager::GetInstance()->GetGroupManager()->CreateTopicInCommunity("groupID", topicInfo, callback);
```
:::
</dx-tabs>

### Deleting a topic
You can call the `deleteTopicFromCommunity`([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a77c4502346e800e43c22a0f15138d699) / [iOS & Mac](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a31b726136637a58b5bb246eaac41187c) / [Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMGroupManager.html#aadbe5002f65d5202da3b1b4e6180264d)) API to delete a topic.

Sample code:
<dx-tabs>
::: Android
```java
V2TIMManager.getGroupManager().deleteTopicFromCommunity(groupID, topicIDList, new V2TIMValueCallback<List<V2TIMTopicOperationResult>>() {
  @Override
  public void onSuccess(List<V2TIMTopicOperationResult> v2TIMTopicOperationResults) {
  	// Topic deleted successfully
  }

  @Override
  public void onError(int code, String desc) {
  	// Failed to delete the topic
  }
});

```
:::
::: iOS and macOS
```objectivec
[[V2TIMManager sharedInstance] deleteTopicFromCommunity:@"groupID" topicIDList:@[@"topic1", @"topic2"] succ:^(NSMutableArray<V2TIMTopicOperationResult *> *resultList) {
    // Topic deleted successfully
} fail:^(int code, NSString *desc) {
    // Failed to delete the topic
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
    void OnError(int error_code, const V2TIMString &error_message) override {
        if (error_callback_) {
            error_callback_(error_code, error_message);
        }
    }

private:
    SuccessCallback success_callback_;
    ErrorCallback error_callback_;
};

V2TIMStringVector topicIDList;
topicIDList.PushBack("topic1");
topicIDList.PushBack("topic2");

auto callback = new ValueCallback<V2TIMTopicOperationResultVector>{};
callback->SetCallback(
    [=](const V2TIMTopicOperationResultVector& topicOperationResultList) {
        // Topic deleted successfully
        delete callback;
    },
    [=](int error_code, const V2TIMString& error_message) {
        // Failed to delete the topic
        delete callback;
    });

V2TIMManager::GetInstance()->GetGroupManager()->DeleteTopicFromCommunity("groupID", topicIDList, callback);
```
:::
</dx-tabs>

### Modifying topic information
You need to perform two steps to modify the information of a topic:

1. Create the `V2TIMTopicInfo` object ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMTopicInfo.html) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMTopicInfo.html) / [Windows](https://im.sdk.qcloud.com/doc/en/structV2TIMTopicInfo.html)) and set the fields to be modified.
2. Call the `setTopicInfo` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#acaff2edad6eb208478be9ab06d30035d) / [iOS and Mac](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a237e2fa6e16e55143c516c5428a23936) / [Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMGroupManager.html#a128f08ef6e675d7c8fc96a5d124e59af)) API to modify topic information.

Sample code:
<dx-tabs>
::: Android
```java
V2TIMTopicInfo topicInfo = new V2TIMTopicInfo();
topicInfo.setTopicID(topicID);
topicInfo.setTopicName(topicName);
topicInfo.setTopicFaceUrl(topicFaceUrl);
topicInfo.setIntroduction(topicIntroduction);
topicInfo.setNotification(topicNotification);
topicInfo.setCustomString(topicCustomString);
topicInfo.setDraft(topicDraft);
topicInfo.setAllMute(false);
V2TIMManager.getGroupManager().setTopicInfo(topicInfo, new V2TIMCallback() {
  @Override
  public void onSuccess() {
  	// Topic information modified successfully
  }

  @Override
  public void onError(int code, String desc) {
  	// Failed to modify the topic information
  }
});

```
:::
::: iOS and macOS
```objectivec
V2TIMTopicInfo *topicInfo = [[V2TIMTopicInfo alloc] init];
topicInfo.topicID = @"topicID";
topicInfo.topicName = @"topicName";
topicInfo.topicFaceURL = @"topicFaceUrl";
topicInfo.introduction = @"topicIntroduction";
topicInfo.notification = @"topicNotification";
topicInfo.customString = @"topicCustomString";
topicInfo.draftText =  @"topicDraft";
topicInfo.isAllMuted = NO;
[[V2TIMManager sharedInstance] setTopicInfo:topicInfo succ:^{
    // Topic information modified successfully
} fail:^(int code, NSString *desc) {
    // Failed to modify the topic information
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
    void OnError(int error_code, const V2TIMString &error_message) override {
        if (error_callback_) {
            error_callback_(error_code, error_message);
        }
    }

private:
    SuccessCallback success_callback_;
    ErrorCallback error_callback_;
};

V2TIMTopicInfo topicInfo;
topicInfo.topicID = "topicID";
topicInfo.topicName = "topicName";
topicInfo.notification = "topicFaceURL";
topicInfo.introduction = "introduction";
topicInfo.topicFaceURL = "notification";
topicInfo.customString = "customString";
topicInfo.modifyFlag = V2TIMGroupInfoModifyFlag::V2TIM_GROUP_INFO_MODIFY_FLAG_GROUP_NAME |
                       V2TIMGroupInfoModifyFlag::V2TIM_GROUP_INFO_MODIFY_FLAG_NOTIFICATION |
                       V2TIMGroupInfoModifyFlag::V2TIM_GROUP_INFO_MODIFY_FLAG_INTRODUCTION |
                       V2TIMGroupInfoModifyFlag::V2TIM_GROUP_INFO_MODIFY_FLAG_FACE_URL |
                       V2TIMGroupInfoModifyFlag::V2TIM_TOPIC_INFO_MODIFY_FLAG_CUSTOM_STRING;

auto callback = new Callback;
callback->SetCallback(
    [=]() {
        // Topic information modified successfully
        delete callback;
    },
    [=](int error_code, const V2TIMString& error_message) {
        // Failed to modify the topic information
        delete callback;
    });

V2TIMManager::GetInstance()->GetGroupManager()->SetTopicInfo(topicInfo, callback);
```
:::
</dx-tabs>

For how to modify other information of a topic, see [Muting Member](https://intl.cloud.tencent.com/document/product/1047/48181) and [Changing Topic Message Receiving Option](https://intl.cloud.tencent.com/document/product/1047/48185).
	
### Getting the topic list[](id:getTopicList)
You can call the `getTopicInfoList` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a5d2b18a76cff650cb9bb2abf2ef07306) / [iOS and Mac](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#af93ad10e0e2b21d6ae3c8ec45021b159) / [Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMGroupManager.html#a7b2ffb5e2e526b7d30b2c8741380d0ac)) API to get the topic list.
- If `topicIDList` is empty, the list of all topics of the community group will be got.
- If `topicIDList` is the ID of specified topics, the list of the specified topics will be got.

Sample code:
<dx-tabs>
::: Android
```java
V2TIMManager.getGroupManager().getTopicInfoList(groupID, topicIDList, new V2TIMValueCallback<List<V2TIMTopicInfoResult>>() {
  @Override
  public void onSuccess(List<V2TIMTopicInfoResult> v2TIMTopicInfoResults) {
		// Topic list obtained successfully
  }

  @Override
  public void onError(int code, String desc) {
		// Failed to obtain the topic list
  }
});
```
:::
::: iOS and macOS
```objectivec
[[V2TIMManager sharedInstance] getTopicInfoList:@"groupID" topicIDList:@[@"topic1", @"topic2"] succ:^(NSMutableArray<V2TIMTopicInfoResult *> *resultList) {
    // Topic list obtained successfully
} fail:^(int code, NSString *desc) {
    // Failed to obtain the topic list
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
    void OnError(int error_code, const V2TIMString &error_message) override {
        if (error_callback_) {
            error_callback_(error_code, error_message);
        }
    }

private:
    SuccessCallback success_callback_;
    ErrorCallback error_callback_;
};

V2TIMStringVector topicIDList;
topicIDList.PushBack("topic1");
topicIDList.PushBack("topic2");

auto callback = new ValueCallback<V2TIMTopicInfoResultVector>{};
callback->SetCallback(
    [=](const V2TIMTopicInfoResultVector& topicInfoResultList) {
        // Topic list obtained successfully
        delete callback;
    },
    [=](int error_code, const V2TIMString& error_message) {
        // Failed to obtain the topic list
        delete callback;
    });

V2TIMManager::GetInstance()->GetGroupManager()->GetTopicInfoList("groupID", topicIDList, callback);
```
:::
</dx-tabs>

### Topic group
The community-**group**-topic hierarchy is implemented as follows:
The `customInfo` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupInfo.html#a56511a5bcd9efbf2853ee71c47eac2f4) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMGroupInfo.html#a47c0485212c1952ab2bafaa5421e3529) / [Windows](https://im.sdk.qcloud.com/doc/en/structV2TIMUserFullInfo.html#a9c8d19de15a107b7a6d18f63b28f9609)) in the community profile defines a field to store the topic group list of the community. The `customString` field ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMTopicInfo.html#aad0cc8249c21c5ccae385fdfb8ba32ea) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMTopicInfo.html#a28b1153ccc4a0bd7b3123ea05d0e1c3e) / [Windows](https://im.sdk.qcloud.com/doc/en/structV2TIMTopicInfo.html#a969217a3f928638622a2cb829e8c6b79)) in the topic profile stores the topic group.

- When a community is loaded, the `customInfo` field for the topic group list in the community (group) profile is used to display the group list.
- When the topic list of a community is loaded, the `customString` in the topic profile is used to get the group name for assignment.

>? 
>
>You can customize the `key` value of the `customInfo` field for the topic group list of the community (group).
>The following sample code names it `topic_category`.

#### Configuring the group list for the community
You just need to modify the `customInfo` in `groupInfo`. Here is a `Map`, and the `key` value is the name of the field for the topic group list you defined.
Sample code:

<dx-tabs>
::: Android
```java
List<String> categoryList = new ArrayList<>();
categoryList.add("Group 1");
categoryList.add("Group 2");
byte[] categoriesByteArray = gson.toJson(categoryList).getBytes();

Map<String, byte[]> customMap = new HashMap<>();
// You need to configure the custom group field `topic_category` in the console first.
customMap.put("topic_category", categoriesByteArray);

V2TIMGroupInfo modifyInfo = new V2TIMGroupInfo();
modifyInfo.setGroupID(groupID);
modifyInfo.setCustomInfo(customMap);
V2TIMManager.getGroupManager().setGroupInfo(modifyInfo, new V2TIMCallback() {
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
NSArray *categoryList = @[@"Group 1", @"Group 2"];
NSError *error = nil;
NSData *data = [NSJSONSerialization dataWithJSONObject:categoryList
                                                options:NSJSONWritingPrettyPrinted
                                                  error:&error];
if ([data length] > 0 && error == nil) {
    // You need to configure the custom group field `topic_category` in the console first.
    NSDictionary *customInfo = @{@"topic_category": data};
    
    V2TIMGroupInfo *info = [[V2TIMGroupInfo alloc] init];
    info.groupID = @"Group ID of the group to be modified";
    info.customInfo = customInfo;
    [[V2TIMManager sharedInstance] setGroupInfo:info
                                            succ:^{
        // Modified the group profile successfully
    } fail:^(int code, NSString *desc) {
        // Failed to modify the group profile
    }];
}
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
    void OnError(int error_code, const V2TIMString &error_message) override {
        if (error_callback_) {
            error_callback_(error_code, error_message);
        }
    }

private:
    SuccessCallback success_callback_;
    ErrorCallback error_callback_;
};

V2TIMGroupInfo info;
info.groupID = "groupA";

V2TIMCustomInfo customInfo;
std::string str{u8"[\"Group 1\", \"Group 2\"]"};
// You need to configure the custom group field `topic_category` in the console first.
customInfo.Insert("topic_category", {reinterpret_cast<const uint8_t*>(str.data()), str.size()});
info.modifyFlag = V2TIMGroupInfoModifyFlag::V2TIM_GROUP_INFO_MODIFY_FLAG_CUSTOM_INFO;

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

#### Getting the list of groups in the community
Sample code:

<dx-tabs>
::: Android
```java
String groupID = "group1";
List<String> groupIDList = new ArrayList<>();
groupIDList.add(groupID);
V2TIMManager.getGroupManager().getGroupsInfo(groupIDList, new V2TIMValueCallback<List<V2TIMGroupInfoResult>>() {
	@Override
	public void onSuccess(List<V2TIMGroupInfoResult> v2TIMGroupInfos) {
		if (v2TIMGroupInfos.size() == 0) {
			return;
		}
		V2TIMGroupInfoResult v2TIMGroupInfoResult = v2TIMGroupInfos.get(0);
		if (v2TIMGroupInfoResult.getResultCode() == BaseConstants.ERR_SUCC) {
			byte[] topicCategoryBytes = v2TIMGroupInfoResult.getGroupInfo().getCustomInfo().get("topic_category");
			List<String> topicCategories = null;
			if (topicCategoryBytes != null) {
				Gson gson = new Gson();
				try {
					// Parse the group list
					topicCategories = gson.fromJson(new String(topicCategoryBytes), List.class);
				} catch (JsonParseException e) {
				}
			}
		}
	}

	@Override
	public void onError(int code, String desc) {

	}
});
```
:::
::: iOS and macOS
```objectivec
NSArray *groupIDList = @[@"group1"];
[[V2TIMManager sharedInstance] getGroupsInfo:groupIDList
                                        succ:^(NSArray<V2TIMGroupInfoResult *> *groupResultList) {
    // Conversation profile obtained successfully
    if (groupResultList.count == 0) {
        return;
    }
    V2TIMGroupInfoResult *result = groupResultList.firstObject;
    if (result.resultCode != 0) {
        return;
    }
    NSData *categoryData = result.info.customInfo[@"topic_category"];
    if (categoryData == nil) {
        return;
    }
    NSArray *categoryList;
    NSError *error = nil;
    id jsonObject = [NSJSONSerialization JSONObjectWithData:categoryData
                                                    options:NSJSONReadingAllowFragments
                                                      error:nil];
    if (jsonObject != nil && error == nil) {
        // Parse the group list
        categoryList = (NSArray *)jsonObject;
    }
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
    void OnError(int error_code, const V2TIMString &error_message) override {
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
        if (groupInfoResultList.Size() == 1) {
            const V2TIMGroupInfoResult& groupInfoResult = groupInfoResultList[0];
            if (groupInfoResult.resultCode == 0) {
                V2TIMGroupInfo info = groupInfoResult.info;
                V2TIMCustomInfo customInfo = info.customInfo;
                if (customInfo.Count("topic_category")) {
                    const V2TIMBuffer& topicCategory = customInfo.Get("topic_category");
                    // Parse the group list
                }
            }
        }

        delete callback;
    },
    [=](int error_code, const V2TIMString& error_message) {
        // Failed to get the community group list
        delete callback;
    });
V2TIMManager::GetInstance()->GetGroupManager()->GetGroupsInfo(groupIDList, callback);
```
:::
</dx-tabs>

#### Adding a topic to a group
You can save the topic group with the `customString` field of the topic.

Sample code:
<dx-tabs>
::: Android
```java
Map<String, Object> map = new HashMap<>();
map.put("category", "Group 1");
Gson gson = new Gson();
V2TIMTopicInfo topicInfo = new V2TIMTopicInfo();
topicInfo.setTopicID(topicID);
topicInfo.setCustomString(gson.toJson(map));
V2TIMManager.getGroupManager().setTopicInfo(topicInfo, new V2TIMCallback() {
  @Override
  public void onSuccess() {
  	// Topic information modified successfully
  }

  @Override
  public void onError(int code, String desc) {
  	// Failed to modify the topic information
  }
});

```
:::
::: iOS and macOS
```objectivec
NSDictionary *dict = @{@"category": @"Group 1"};
NSError *error = nil;
NSData *data = [NSJSONSerialization dataWithJSONObject:dict
                                               options:0
                                                 error:&error];
if ([data length] > 0 && error == nil) {
    NSString *dataStr = [[NSString alloc] initWithData:data encoding:NSUTF8StringEncoding];
    V2TIMTopicInfo *info = [[V2TIMTopicInfo alloc] init];
    info.topicID = @"ID of the topic to be set";
    info.customString = dataStr;
    [[V2TIMManager sharedInstance] setTopicInfo:info succ:^{
      // Set the topic profile successfully
    } fail:^(int code, NSString *desc) {
      // Failed to set the topic profile
    }];
}
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
    void OnError(int error_code, const V2TIMString &error_message) override {
        if (error_callback_) {
            error_callback_(error_code, error_message);
        }
    }

private:
    SuccessCallback success_callback_;
    ErrorCallback error_callback_;
};

V2TIMTopicInfo topicInfo;
topicInfo.topicID = "topicID";
topicInfo.customString = u8"{\"category\": \"Group 1\"}}";
topicInfo.modifyFlag = V2TIMGroupInfoModifyFlag::V2TIM_TOPIC_INFO_MODIFY_FLAG_CUSTOM_STRING;

auto callback = new Callback;
callback->SetCallback(
    [=]() {
        // Topic information modified successfully
        delete callback;
    },
    [=](int error_code, const V2TIMString& error_message) {
        // Failed to modify the topic information
        delete callback;
    });

V2TIMManager::GetInstance()->GetGroupManager()->SetTopicInfo(topicInfo, callback);
```
:::
</dx-tabs>

#### Getting the topic group

Use the `customString` to parse the JSON content after [getting the topic list](#getTopicList).	
	
### Listening for topic callbacks
In `V2TIMGroupListener` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupListener.html) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/protocolV2TIMGroupListener-p.html) / [Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMGroupListener.html)), topic callback methods such as `onTopicCreated`, `onTopicDeleted`, and `onTopicInfoChanged` are added to listen for topic events. 

Sample code:
<dx-tabs>
::: Android
```java
V2TIMGroupListener v2TIMGroupListener = new V2TIMGroupListener() {
  @Override
  public void onTopicCreated(String groupID, String topicID) {
  	// Listen for topic creation notifications
  }

  @Override
  public void onTopicDeleted(String groupID, List<String> topicIDList) {
  	// Listen for topic deletion notifications
  }

  @Override
  public void onTopicInfoChanged(String groupID, V2TIMTopicInfo topicInfo) {
  	// Listen for topic information update notifications
  }
};
V2TIMManager.getInstance().addGroupListener(v2TIMGroupListener);
```
:::
::: iOS and macOS
```objectivec
[[V2TIMManager sharedInstance] addGroupListener:self];
- (void)onTopicCreated:(NSString *)groupID topicID:(NSString *)topicID {
    // Listen for topic creation notifications
}
- (void)onTopicDeleted:(NSString *)groupID topicIDList:(NSArray<NSString *> *)topicIDList {
    // Listen for topic deletion notifications
}
- (void)onTopicChanged:(NSString *)groupID topicInfo:(V2TIMTopicInfo *)topicInfo {
    // Listen for topic information update notifications
}
```
:::
::: Windows
```cpp
class GroupListener final : public V2TIMGroupListener {
public:
    GroupListener() = default;
    ~GroupListener() override = default;

    void OnTopicCreated(const V2TIMString& groupID, const V2TIMString& topicID) override {
        // Listen for topic creation notifications
    }
    void OnTopicDeleted(const V2TIMString& groupID, const V2TIMStringVector& topicIDList) override {
        // Listen for topic deletion notifications
    }
    void OnTopicChanged(const V2TIMString& groupID, const V2TIMTopicInfo& topicInfo) override {
        // Listen for topic information update notifications
    }
};

// Add a group event listener. Keep `groupListener` valid before the listener is removed to ensure event callbacks are received.
GroupListener groupListener;
V2TIMManager::GetInstance()->AddGroupListener(&groupListener);
```
:::
</dx-tabs>


## Topic Messages
Topic messages can be used in the same way as ordinary messages and involve the following APIs:

<table>
<tr>
<th width="15%">Feature</th>
<th width="40%">API</th>
<th width="30%">Description</th>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/47994">Sending messages</a></td>
<td>sendMessage (<a href="https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a28e01403acd422e53e999f21ec064795">Android</a> / <a href="https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a681947465d6ab718da40f7f983740a21">iOS & Mac)</a> </td>
<td>Set `groupID` to the topic ID.</td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/47995">Receiving messages</a></td>
<td>`onRecvNewMessage` method in V2TIMAdvancedMsgListener (<a href="https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMAdvancedMsgListener.html">Android</a> / <a href="https://im.sdk.qcloud.com/doc/en/protocolV2TIMAdvancedMsgListener-p.html">iOS and macOS)</a></td>
<td>Set `groupID` in the message to the topic ID.</td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/48320">Marking a conversation as read</a></td>
<td>markGroupMessageAsRead (<a href="https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#ac0a65f18d361abde8a0ac16132027e69">Android</a> / <a href="https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a7fc79e30877b8d77fbdfa24e057376dc">iOS and macOS)</a></td>
<td>Set `groupID` to the topic ID.</td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/47998">Getting the message history</a></td>
<td>getGroupHistoryMessageList (<a href="https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a671e8737fcea0c05dc661c753e5b3597">Android</a> / <a href="https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a9e242ba327377fe74b83e8d5572d39a0">iOS & Mac)</a></td>
<td>Set `groupID` to the topic ID.</td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/48016">Recalling messages</a></td>
<td>revokeMessage (<a href="https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#ad0dfce6be749165cd90a9ff67a1308b1">Android</a> / <a href="https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a2ef856a792923811e9d16ed7a101336a">iOS & Mac)</a></td>
<td>Set `groupID` to the topic ID.</td>
</tr>
</table>
