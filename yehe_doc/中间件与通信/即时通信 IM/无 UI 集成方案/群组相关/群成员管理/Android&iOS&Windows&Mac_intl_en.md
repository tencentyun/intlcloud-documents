## Overview
Group member management includes pulling the member list, muting group members, removing group members, granting permissions, and transferring the group ownership, which can be implemented through the methods in the `V2TIMGroupManager(Android)` / `V2TIMManager(Group)(iOS and macOS)` core class.

[](id:getGroupMemberList)
## Getting the Group Member List
Call the `getGroupMemberList` API ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a69fc0831aacaa0585c1855f4c91320be) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a98681b9036e73acbe8f84737b5291326) / [Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMGroupManager.html#ade696bf03f06de9cdfb534570de35254)) to get the list of members in a specified group.
The list contains profile information about individual group members, such as user ID (`userID`), group name card (`nameCard`), profile photo (`faceUrl`), nickname (`nickName`), and time of joining group (`joinTime`).

As an audio-video group (AVChatRoom) has a large number of members, the feature of pulling the list of all the members is unavailable. The Ultimate edition and non-Ultimate edition differ as follows:
1. A non-Ultimate edition user can call `getGroupMemberList` to pull the latest 30 group members.
2. An Ultimate edition user can call `getGroupMemberList` to pull the latest 1,000 group members. This feature needs to be enabled in the Chat console. If it is not enabled, only the latest 30 group members will be pulled, just as in the non-Ultimate edition.
   To enable this feature for the Ultimate edition, log in to the [Chat console](https://console.cloud.tencent.com/im) and modify related configuration.


As a group might have a large number of members (for example, over 5,000), this API supports two advanced features: pulling by filter (`filter`) and pulling by page (`nextSeq`).

### Pulling by filter (`filter`)
When calling the `getGroupMemberList` API ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a69fc0831aacaa0585c1855f4c91320be) / [iOS and Mac](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a98681b9036e73acbe8f84737b5291326) / [Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMGroupManager.html#ade696bf03f06de9cdfb534570de35254)), you can set `filter` to `V2TIMGroupMemberFilter` to pull the information of certain roles.

| Filter                           | Type                                                |
| -------------------------------- | --------------------------------------------------- |
| V2TIM_GROUP_MEMBER_FILTER_ALL    | Pull the information list of all group members      |
| V2TIM_GROUP_MEMBER_FILTER_OWNER  | Pull the information list of the group owner        |
| V2TIM_GROUP_MEMBER_FILTER_ADMIN  | Pull the information list of the group admin        |
| V2TIM_GROUP_MEMBER_FILTER_COMMON | Pull the information list of ordinary group members |

For audio-video groups, you can set `filter` to a custom group member mark other than `V2TIMGroupMemberFilter` to filter group members as needed. For more information, see [Marking Group Members](#markGroupMemberList).

Sample code:

<dx-tabs>
::: Android
```java
// Use the `filter` parameter to specify only the profile of the group owner is to be pulled
int role = V2TIMGroupMemberFullInfo.V2TIM_GROUP_MEMBER_FILTER_OWNER;
V2TIMManager.getGroupManager().getGroupMemberList("testGroup", role, 0, 
    new V2TIMValueCallback<V2TIMGroupMemberInfoResult>() {
	@Override
	public void onError(int code, String desc) {
		// Messages failed to be pulled
	}

	@Override
	public void onSuccess(V2TIMGroupMemberInfoResult v2TIMGroupMemberInfoResult) {
		// Conversations pulled successfully
	}
});
```
:::
::: iOS and macOS
```objectivec
[[V2TIMManager sharedInstance] getGroupMemberList:@"groupA" filter:V2TIM_GROUP_MEMBER_FILTER_OWNER nextSeq:0 succ:^(uint64_t nextSeq, NSArray<V2TIMGroupMemberFullInfo *> *memberList) {
    // Conversations pulled successfully
} fail:^(int code, NSString *desc) {
    // Messages failed to be pulled
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

V2TIMString groupID = "testGroup";
// Use the `filter` parameter to specify only the profile of the group owner is to be pulled
uint32_t filter = V2TIMGroupMemberFilter::V2TIM_GROUP_MEMBER_FILTER_OWNER;
uint64_t nextSeq = 0;

auto callback = new ValueCallback<V2TIMGroupMemberInfoResult>{};
callback->SetCallback(
    [=](const V2TIMGroupMemberInfoResult& groupMemberInfoResult) {
        // Conversations pulled successfully
        delete callback;
    },
    [=](int error_code, const V2TIMString& error_message) {
        // Messages failed to be pulled
        delete callback;
    });

V2TIMManager::GetInstance()->GetGroupManager()->GetGroupMemberList(groupID, filter, nextSeq, callback);
```
:::
</dx-tabs>

### Pulling by page (`nextSeq`)
In many cases, only the first page of the group member list, not the information of all the group members, needs to be displayed on the user UI. More group members need to be pulled only when the user clicks **Next Page** or pulls up the list page. In this case, you can use pulling by page.

Directions for pulling by page:
1. When you call `getGroupMemberList` for the first time, set `nextSeq` to `0` (indicating to pull the group member list from the beginning). Up to 50 group member objects can be pulled at a time.
   
2. After the group member list is pulled successfully for the first time, the `V2TIMGroupMemberInfoResult` callback of `getGroupMemberList` will contain `nextSeq` (field for the next pull):
   * If `nextSeq` is `0`, all the group members have been pulled.
   * If `nextSeq` is greater than `0`, there are more group members that can be pulled. This doesn't mean that the next page of the member list will be pulled immediately. In common software, a paged pull is often triggered by a swipe operation.

3. When the user continues to pull up the group member list, if there are more members that can be pulled, you can continue to call the `getGroupMemberList` API and pass in the `nextSeq` parameter (the value is from the `V2TIMGroupMemberInfoResult` object returned by the last pull) for the next pull.

4. Repeat [step 3] until `nextSeq` is `0`.

Sample code:

<dx-tabs>
::: Android
```java
{
	...
	long nextSeq = 0;
	getGroupMemberList(nextSeq);
	...
}

public void getGroupMemberList(long nextSeq) {
	int filterRole = V2TIMGroupMemberFullInfo.V2TIM_GROUP_MEMBER_FILTER_ALL;
	V2TIMManager.getGroupManager().getGroupMemberList("testGroup", filterRole, nextSeq, 
	    new V2TIMValueCallback<V2TIMGroupMemberInfoResult>() {
		@Override
		public void onError(int code, String desc) {
			// Messages failed to be pulled
		}

		@Override
		public void onSuccess(V2TIMGroupMemberInfoResult groupMemberInfoResult) {
			if (groupMemberInfoResult.getNextSeq() != 0) {
				// Make another pull
				getGroupMemberList(groupMemberInfoResult.getNextSeq());
				...
			} else {
				// Pull ends
			}
		}
	});
}
```
:::
::: iOS and macOS
```objectivec
- (void)getGroupMemberList:(uint32_t)seq {
    [[V2TIMManager sharedInstance] getGroupMemberList:@"groupA" filter:V2TIM_GROUP_MEMBER_FILTER_OWNER nextSeq:seq succ:^(uint64_t nextSeq, NSArray<V2TIMGroupMemberFullInfo *> *memberList) {
        if (nextSeq != 0) {
            // Make another pull
            [self getGroupMemberList:nextSeq];
            //...
        } else {
            // Pull ends
        }
    } fail:^(int code, NSString *desc) {
        // Messages failed to be pulled
    }];
}
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

V2TIMString groupID = "testGroup";
uint32_t filter = V2TIMGroupMemberFilter::V2TIM_GROUP_MEMBER_FILTER_ALL;
uint64_t nextSeq = 0;

auto callback = new ValueCallback<V2TIMGroupMemberInfoResult>{};
callback->SetCallback(
    [=](const V2TIMGroupMemberInfoResult& groupMemberInfoResult) {
        if (groupMemberInfoResult.nextSequence != 0) {
            // Make another pull
        }

        delete callback;
    },
    [=](int error_code, const V2TIMString& error_message) {
        // Messages failed to be pulled
        delete callback;
    });

V2TIMManager::GetInstance()->GetGroupManager()->GetGroupMemberList(groupID, filter, nextSeq, callback);
```
:::
</dx-tabs>

[](id:markGroupMemberList)
## Marking Group Members
The group owner can call the `markGroupMemberList` API ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#abdd5f157904dd50012c7a93f66f85dba) / [iOS and Mac](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a21238536e7cb2c3fd086797e7dc1b970)) to mark or unmark members of an audio-video group. Rules are as follows:
1. This feature is supported only on audio-video groups, and only group owners have the permission to mark or unmark group members.
2. Up to ten custom marks can be added per audio-video group.
3. Custom marks configured through Chat SDK must be of uint32_t type and greater than or equal to 1,000.
4. Up to 100 group members can be marked at a time.
5. Only online members can be marked. When a member leaves a group or goes offline, its mark information will be cleared. When the member joins the group or goes online again, you can reset a mark for the member through a third-party callback.

After marking group members, the group owner can call [`getGroupMemberList`](#getGroupMemberList) to set `filter` to a configured custom group member mark to filter group members as needed. 

> ?
> 1. This feature is available only in Enhanced edition v6.6 or later.
> 2. To use this feature, you need to purchase the Ultimate edition as instructed in [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350).
> 3. Before using this feature, you need to log in to the [Chat console](https://console.cloud.tencent.com/im) and modify related configuration.



[](id:mute)
## Muting group members

### Muting a specified group member
The group owner or admin can call `muteGroupMember` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a450230c4d129611e1b0519827ec0f8b5) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#aa8a0206f75d75400b517f7e0d80fe9ee) / [Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMGroupManager.html#ab19d433e5552205fcba61627e54f7569)) and set `muteTime` (in seconds) to mute a group member. If `muteTime` is set to `120`, the member is muted for 120 seconds.
If a group member is muted, message sending will fail, and an error code will be reported. To unmute the member, set `muteTime` to `0`.

The muting timestamp is stored in the `muteUntil` field ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupMemberFullInfo.html#a2caecbec07bdd4fa8e6b8072bc39be58) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMGroupMemberFullInfo.html#a953345fe02297a7192b727abe4b772c6) / [Windows](https://im.sdk.qcloud.com/doc/en/structV2TIMGroupMemberFullInfo.html#a953345fe02297a7192b727abe4b772c6)) of the group member information. Note that `muteUntil` indicates the end time for muting a group member.

After a group member is muted, all the group members (including the muted member) will receive the `onMemberInfoChanged` callback ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupListener.html#a4ac777faad07e32408ae7ef5e2e3fc86) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/protocolV2TIMGroupListener-p.html#a18b147301296642e7193e4321e33fd24) / [Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMGroupListener.html#af87ae2fa909e0e10a521074371359125)).

> ? The group owner can mute/unmute the admin and ordinary group members. The admin can mute/unmute ordinary group members.

### Muting the entire group
The group owner or admin can also call the `setGroupInfo` API ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#ad4ceef92975fa00c4a5dddc8f7e1edcf) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#aa9519a479493e56d7920e40aba796144) / [Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMGroupManager.html#a10785c46e166879250c2c2ba2001b354)) to mute the entire group by setting the `allMuted` field ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupInfo.html#a6faf73364372206bfee9c2b99ed5807e) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMGroupInfo.html#aff22b39b539249ee6d84aa136ca36573) / [Windows](https://im.sdk.qcloud.com/doc/en/structV2TIMGroupInfo.html#a56a7991eaae72bd28c0345889f77c71b)) to `true`/`YES`. The entire group can be muted for an unlimited period of time and needs to be unmuted through `setAllMuted(false/NO)` of the group profile.

Muting all the group members will trigger the `onGroupInfoChanged` callback ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupListener.html#ac3a88ea430c6dc35845472ed98ad049b) / [iOS and Mac](https://im.sdk.qcloud.com/doc/en/protocolV2TIMGroupListener-p.html#abbe2208a234d77364bff697eea503d27) / [Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMGroupListener.html#a37aa57b23295e6b295413fafba2eda07)).

This notification is disabled by default. To enable it, log in to the [Chat console](https://console.cloud.tencent.com/im) and modify related configuration.

> ? Only the group owner can mute the admin.

Sample code:

<dx-tabs>
::: Android

```java
// Mute the `userB` group member for one minute
V2TIMManager.getGroupManager().muteGroupMember("groupA", "userB", 60, new V2TIMCallback() {
  @Override
  public void onSuccess() {
  	// Muted the group member successfully
  }

  @Override
  public void onError(int code, String desc) {
  	// Failed to mute the group member
  }
});

// Mute all members
V2TIMGroupInfo info = new V2TIMGroupInfo();
info.setGroupID("groupA");
info.setAllMuted(true);
V2TIMManager.getGroupManager().setGroupInfo(info, new V2TIMCallback() {
  @Override
  public void onSuccess() {
  	// Muted all successfully
  }

  @Override
  public void onError(int code, String desc) {
  	// Failed to mute all
  }
});

V2TIMManager.getInstance().addGroupListener(new V2TIMGroupListener() {
  @Override
  public void onMemberInfoChanged(String groupID, List<V2TIMGroupMemberChangeInfo> v2TIMGroupMemberChangeInfoList) {
    // Listen for the muting of a group member
    for (V2TIMGroupMemberChangeInfo memberChangeInfo : v2TIMGroupMemberChangeInfoList) {
      // ID of the muted user
      String userID = memberChangeInfo.getUserID();
      // Muting duration
      long muteTime = memberChangeInfo.getMuteTime();
    }
  }

  @Override
  public void onGroupInfoChanged(String groupID, List<V2TIMGroupChangeInfo> changeInfos) {
    // Listen for the muting of all
    for (V2TIMGroupChangeInfo groupChangeInfo : changeInfos) {
      if (groupChangeInfo.getType() == V2TIMGroupChangeInfo.V2TIM_GROUP_INFO_CHANGE_TYPE_SHUT_UP_ALL) {
        // Whether all members are muted
        boolean isMuteAll = groupChangeInfo.getBoolValue();
      }
    }
  }
});
```
:::
::: iOS and macOS
```objectivec
// Mute the group member `user1` for one minute
[[V2TIMManager sharedInstance] muteGroupMember:@"groupA" member:@"user1" muteTime:60 succ:^{
    // Muted the group member successfully
} fail:^(int code, NSString *desc) {
    // Failed to mute the group member
}];

// Mute all members
V2TIMGroupInfo *info = [[V2TIMGroupInfo alloc] init];
info.groupID = @"groupA";
info.allMuted = YES;
[[V2TIMManager sharedInstance] muteGroupMember:@"groupA" member:@"user1" muteTime:60 succ:^{
    // Muted all successfully
} fail:^(int code, NSString *desc) {
    // Failed to mute all
}];

[[V2TIMManager sharedInstance] addGroupListener:self];
- (void)onMemberInfoChanged:(NSString *)groupID changeInfoList:(NSArray <V2TIMGroupMemberChangeInfo *> *)changeInfoList {
    // Listen for the muting of a group member
    for (V2TIMGroupMemberChangeInfo *memberChangeInfo in changeInfoList) {
      // ID of the muted user
      NSString *userID = memberChangeInfo.userID;
      // Muting duration
        uint32_t muteTime = memberChangeInfo.muteTime;
    }
}

- (void)onGroupInfoChanged:(NSString *)groupID changeInfoList:(NSArray <V2TIMGroupChangeInfo *> *)changeInfoList {
    // Listen for the muting of all
    for (V2TIMGroupChangeInfo groupChangeInfo in changeInfoList) {
      if (groupChangeInfo.type == V2TIM_GROUP_INFO_CHANGE_TYPE_SHUT_UP_ALL) {
        // Whether all members are muted
        BOOL isMuteAll = groupChangeInfo.boolValue;
      }
    }
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
    void OnError(int error_code, const V2TIMString& error_message) override {
        if (error_callback_) {
            error_callback_(error_code, error_message);
        }
    }

private:
    SuccessCallback success_callback_;
    ErrorCallback error_callback_;
};

// Mute the `userB` group member for one minute
auto callback = new Callback;
callback->SetCallback(
    [=]() {
        // Muted the group member successfully
        delete callback;
    },
    [=](int error_code, const V2TIMString& error_message) {
        // Failed to mute the group member
        delete callback;
    });
V2TIMManager::GetInstance()->GetGroupManager()->MuteGroupMember("groupA", "userB", 60, callback);

// Mute all members
V2TIMGroupInfo info;
info.groupID = "groupA";
info.allMuted = true;
info.modifyFlag = V2TIMGroupInfoModifyFlag::V2TIM_GROUP_INFO_MODIFY_FLAG_SHUTUP_ALL;
auto callback = new Callback;
callback->SetCallback(
    [=]() {
        // Muted all successfully
        delete callback;
    },
    [=](int error_code, const V2TIMString& error_message) {
        // Failed to mute all
        delete callback;
    });
V2TIMManager::GetInstance()->GetGroupManager()->SetGroupInfo(info, callback);

// Listen for the muting of a group member or all
class GroupListener final : public V2TIMGroupListener {
public:
    GroupListener() = default;
    ~GroupListener() override = default;

    void OnMemberInfoChanged(const V2TIMString& groupID,
                             const V2TIMGroupMemberChangeInfoVector& groupMemberChangeInfoList) override {
        // Listen for the muting of a group member
        for (size_t i = 0; i < groupMemberChangeInfoList.Size(); ++i) {
            const V2TIMGroupMemberChangeInfo& groupMemberChangeInfo = groupMemberChangeInfoList[i];
            // ID of the muted user
            V2TIMString userID = groupMemberChangeInfo.userID;
            // Muting duration
            uint32_t muteTime = groupMemberChangeInfo.muteTime;
        }
    }
    void OnGroupInfoChanged(const V2TIMString& groupID,
                            const V2TIMGroupChangeInfoVector& groupChangeInfoList) override {
        // Listen for the muting of all
        for (size_t i = 0; i < groupChangeInfoList.Size(); ++i) {
            const V2TIMGroupChangeInfo& groupChangeInfo = groupChangeInfoList[i];
            if (groupChangeInfo.type == V2TIMGroupInfoChangeType::V2TIM_GROUP_INFO_CHANGE_TYPE_SHUT_UP_ALL) {
                // Whether all members are muted
                bool boolValue = groupChangeInfo.boolValue;
            }
        }
    }
    // Other members …
};
// Add a group event listener. Keep `groupListener` valid before the listener is removed to ensure event callbacks are received.
GroupListener groupListener;
V2TIMManager::GetInstance()->AddGroupListener(&groupListener);
```
:::
</dx-tabs>

[](id:kick)
## Removing Group Members
The group owner or admin can call the `kickGroupMember` API ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a6da6755c6e0c46e96cb02575074a5333) / [iOS and Mac](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a0581f28fddf2ade890aa62e4318d7a97) / [Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMGroupManager.html#ad2e4f74f4e26fb0db455d8e92f774032)) to remove a specified group member from a group.

After the group member is removed, all the members (including the removed member) will receive the `onMemberKicked` callback ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupListener.html#a2874b768866c2d255144c128a766c7fe) / [iOS and Mac](https://im.sdk.qcloud.com/doc/en/protocolV2TIMGroupListener-p.html#a85e7f32f403d876018a26a1b37607edc) / [Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMGroupListener.html#a08eea992617b046a983ca8757414d8d5)).

> ? For a non-audio-video group, only the group owner can remove the admin from the group.

For an audio-video group (AVChatRoom):
1. **For Enhanced edition earlier than v6.6, audio-video groups do not support member removal,** and you can use `muteGroupMember` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a450230c4d129611e1b0519827ec0f8b5) / [iOS and Mac](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#aa8a0206f75d75400b517f7e0d80fe9ee) / [Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMGroupManager.html#ab19d433e5552205fcba61627e54f7569)) to mute a specified member to implement similar controls. For detailed directions, see [Muting](#mute).
2. **For Enhanced edition v6.6 or later, audio-video groups support member removal,** and the corresponding member removal API is the same as that of non-audio-video groups. After a member is removed from an audio-video group, it cannot join the group again nor sending messages to the group. For an audio-video group, only the group owner, not the admin or ordinary members, has the permission to remove members.
> !
> 1. To use this feature, you need to purchase the Ultimate edition as instructed in [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350).
> 2. Before using this feature, you need to log in to the [Chat console](https://console.cloud.tencent.com/im) and modify related configuration.


Sample code:

<dx-tabs>
::: Android
```java
List<String> userIDList = new ArrayList<>();
userIDList.add("userB");
V2TIMManager.getGroupManager().kickGroupMember("groupA", userIDList, "", new V2TIMValueCallback<List<V2TIMGroupMemberOperationResult>>() {
  @Override
  public void onSuccess(List<V2TIMGroupMemberOperationResult> v2TIMGroupMemberOperationResults) {
  	// Removed the member successfully
  }

  @Override
  public void onError(int code, String desc) {
  	// Failed to remove the member
  }
});

V2TIMManager.getInstance().addGroupListener(new V2TIMGroupListener() {
  @Override
  public void onMemberKicked(String groupID, V2TIMGroupMemberInfo opUser,
  List<V2TIMGroupMemberInfo> memberList) {
  	// A group member was removed.
  }
});
```
:::
::: iOS and macOS
```objectivec
[[V2TIMManager sharedInstance] kickGroupMember:@"groupA" memberList:@[@"user1"] reason:@"" succ:^(NSArray<V2TIMGroupMemberOperationResult *> *resultList) {
    // Removed the member successfully
} fail:^(int code, NSString *desc) {
    // Failed to remove the member
}];

[[V2TIMManager sharedInstance] addGroupListener:self];
- (void)onMemberKicked:(NSString *)groupID opUser:(V2TIMGroupMemberInfo *)opUser memberList:(NSArray<V2TIMGroupMemberInfo *>*)memberList {
    // A group member was removed.
}
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
memberList.PushBack("userB");

auto callback = new ValueCallback<V2TIMGroupMemberOperationResultVector>{};
callback->SetCallback(
    [=](const V2TIMGroupMemberOperationResultVector& groupMemberOperationResultList) {
        // Removed the member successfully
        delete callback;
    },
    [=](int error_code, const V2TIMString& error_message) {
        // Failed to remove the member
        delete callback;
    });

V2TIMManager::GetInstance()->GetGroupManager()->KickGroupMember(groupID, memberList, {}, callback);

// Listen for group member removal
class GroupListener final : public V2TIMGroupListener {
public:
    GroupListener() = default;
    ~GroupListener() override = default;

    void OnMemberKicked(const V2TIMString& groupID, const V2TIMGroupMemberInfo& opUser,
                        const V2TIMGroupMemberInfoVector& memberList) override {
        // A group member was removed.
    }
    // Other members …
};
// Add a group event listener. Keep `groupListener` valid before the listener is removed to ensure event callbacks are received.
GroupListener groupListener;
V2TIMManager::GetInstance()->AddGroupListener(&groupListener);
```
:::
</dx-tabs>

[](id:setGroupMemberRole)
## Setting an Admin
The group owner can call `setGroupMemberRole` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a34ebf60528d02626834f022b4ebabfa8) / [iOS and Mac](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a0f1c341a3dc53d6a6557a438b0c64b65) / [Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMGroupManager.html#ab429c1ded6aa3ae27bb0917be6f71dd3)) to set a group member in a public group (Public) or meeting group (Meeting) as the admin.

An ordinary member set as the admin has the admin permission to perform the following operations:
* Modify the basic group profile.
* Remove an ordinary member from the group
* Mute an ordinary member (prevent the member from speaking during a specified period of time)
* Approve a request to join the group
For more information, see [Group Member Roles](https://intl.cloud.tencent.com/document/product/1047/33529).

After an ordinary member is set as the admin, all the members (including the ordinary member) will receive the `onGrantAdministrator` callback ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupListener.html#ae4e23c72489eafc882a40a24f36f1ae9)  / [iOS and Mac](https://im.sdk.qcloud.com/doc/en/protocolV2TIMGroupListener-p.html#af9148b7c76b1ecc89f52be0ffc8316d2) / [Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMGroupListener.html#a97e81d2409ca8fe6d657762a314c4363)).

After the ordinary member is unset as the admin, all the members (including the ordinary member) will receive the `onRevokeAdministrator` callback ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupListener.html#a089480ee71485b5842c75b8c1985f72f) / [iOS and Mac](https://im.sdk.qcloud.com/doc/en/protocolV2TIMGroupListener-p.html#ad82c255d1cbff590fa580f4b746e0f3e) / [Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMGroupListener.html#aea80df2e365ad58339e1e5095c4154cf)).


Sample code:
<dx-tabs>
::: Android
```java
V2TIMManager.getGroupManager().setGroupMemberRole("groupA", "userB", V2TIMGroupMemberFullInfo.V2TIM_GROUP_MEMBER_ROLE_ADMIN, new V2TIMCallback() {
  @Override
  public void onSuccess() {
  	// Changed the group member role successfully
  }

  @Override
  public void onError(int code, String desc) {
  	// Failed to change the group member role
  }
});

V2TIMManager.getInstance().addGroupListener(new V2TIMGroupListener() {
  @Override
  public void onGrantAdministrator(String groupID, V2TIMGroupMemberInfo opUser,
  List<V2TIMGroupMemberInfo> memberList) {
  	// A group member was set as the admin.
  }

  @Override
  public void onRevokeAdministrator(String groupID, V2TIMGroupMemberInfo opUser,
  List<V2TIMGroupMemberInfo> memberList) {
  	// A group member was unset as the admin.
  }
});
```
:::
::: iOS and macOS
```objectivec
[[V2TIMManager sharedInstance] setGroupMemberRole:@"groupA" member:@"user1" newRole:V2TIM_GROUP_MEMBER_ROLE_ADMIN succ:^{
    // Changed the group member role successfully
} fail:^(int code, NSString *desc) {
    // Failed to change the group member role
}];

[[V2TIMManager sharedInstance] addGroupListener:self];
- (void)onGrantAdministrator:(NSString *)groupID opUser:(V2TIMGroupMemberInfo *)opUser memberList:(NSArray <V2TIMGroupMemberInfo *> *)memberList {
    // A group member was set as the admin.
}

- (void)onRevokeAdministrator:(NSString *)groupID opUser:(V2TIMGroupMemberInfo *)opUser memberList:(NSArray <V2TIMGroupMemberInfo *> *)memberList {
    // A group member was unset as the admin.
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
V2TIMString userID = "userB";
uint32_t role = V2TIMGroupMemberRole::V2TIM_GROUP_MEMBER_ROLE_ADMIN;

auto callback = new Callback;
callback->SetCallback(
    [=]() {
        // Changed the group member role successfully
        delete callback;
    },
    [=](int error_code, const V2TIMString& error_message) {
        // Failed to change the group member role
        delete callback;
    });

V2TIMManager::GetInstance()->GetGroupManager()->SetGroupMemberRole(groupID, userID, role, callback);

// Listen for setting a user as the admin
class GroupListener final : public V2TIMGroupListener {
public:
    GroupListener() = default;
    ~GroupListener() override = default;

    void OnGrantAdministrator(const V2TIMString& groupID, const V2TIMGroupMemberInfo& opUser,
                              const V2TIMGroupMemberInfoVector& memberList) override {
        // A group member was set as the admin.
    }
    void OnRevokeAdministrator(const V2TIMString& groupID, const V2TIMGroupMemberInfo& opUser,
                               const V2TIMGroupMemberInfoVector& memberList) override {
        // A group member was unset as the admin.
    }
    // Other members …
};
// Add a group event listener. Keep `groupListener` valid before the listener is removed to ensure event callbacks are received.
GroupListener groupListener;
V2TIMManager::GetInstance()->AddGroupListener(&groupListener);
```
:::
</dx-tabs>

[](id:transfer)
## Transferring Group Ownership
The group owner can call `transferGroupOwner` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#ac16d66c8e293c2ee95c7b673e5ad80c4) / [iOS and Mac](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a58a2ffae60505a43984fe21bf0bc1101) / [Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMGroupManager.html#a2fedff98e2e41e9d30f7a49f5c7adc8f)) to transfer the ownership of a group to another group member.

After the group ownership is transferred, all the group members will receive the `onGroupInfoChanged` callback ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupListener.html#ac3a88ea430c6dc35845472ed98ad049b) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/protocolV2TIMGroupListener-p.html#abbe2208a234d77364bff697eea503d27) / [Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMGroupListener.html#a37aa57b23295e6b295413fafba2eda07)). Here, the `type` of `V2TIMGroupChangeInfo` is `V2TIMGroupChangeInfo.V2TIM_GROUP_INFO_CHANGE_TYPE_OWNER`, and the value is the `UserID` of the new group owner.

Sample code:

<dx-tabs>
::: Android
```java
V2TIMManager.getGroupManager().transferGroupOwner("groupA", "userB", new V2TIMCallback() {
  @Override
  public void onSuccess() {
  	// Transferred the group ownership successfully
  }

  @Override
  public void onError(int code, String desc) {
  	// Failed to transfer the group ownership
  }
});
```
:::
::: iOS and macOS
```objectivec
[[V2TIMManager sharedInstance] transferGroupOwner:@"groupA" member:@"user1" succ:^{
    // Transferred the group ownership successfully
} fail:^(int code, NSString *desc) {
    // Failed to transfer the group ownership
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
V2TIMString userID = "userB";

auto callback = new Callback;
callback->SetCallback(
    [=]() {
        // Transferred the group ownership successfully
        delete callback;
    },
    [=](int error_code, const V2TIMString& error_message) {
        // Failed to transfer the group ownership
        delete callback;
    });

V2TIMManager::GetInstance()->GetGroupManager()->TransferGroupOwner(groupID, userID, callback);
```
:::
</dx-tabs>

[](id:getGroupOnlineMemberCount)
## Getting the Number of Online Group Members
Call `getGroupOnlineMemberCount` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a56840105a4b3371eeab2046d8c300bce) / [iOS and Mac](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#ada2eadb44f6865e9848df94fb5bae4ae) / [Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMGroupManager.html#a7633181ee22e54741600908ed45b3138)) to get the number of online group members.

> ? 
> 1. Currently, only the number of online members in an audio-video group (AVChatRoom) can be obtained.
> 2. This API can be called by a logged-in user once every 60 seconds in the SDK.

Sample code:

<dx-tabs>
::: Android
```java
V2TIMManager.getGroupManager().getGroupOnlineMemberCount("group_avchatroom", new V2TIMValueCallback<Integer>() {
  @Override
  public void onSuccess(Integer integer) {
  	// Obtained the number of online members in the audio-video group (AVChatRoom) successfully
  }

  @Override
  public void onError(int code, String desc) {
  	// Failed to obtain the number of online members in the audio-video group (AVChatRoom)
  }
});
```
:::
::: iOS and macOS
```objectivec
[[V2TIMManager sharedInstance] getGroupOnlineMemberCount:@"group_avchatroom" succ:^(NSInteger count) {
    // Obtained the number of online members in the audio-video group (AVChatRoom) successfully
} fail:^(int code, NSString *desc) {
    // Failed to obtain the number of online members in the audio-video group (AVChatRoom)
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

V2TIMString groupID = "group_avchatroom";

auto callback = new ValueCallback<uint32_t>{};
callback->SetCallback(
    [=](const uint32_t& count) {
        // Obtained the number of online members in the audio-video group (AVChatRoom) successfully
        delete callback;
    },
    [=](int error_code, const V2TIMString& error_message) {
        // Failed to obtain the number of online members in the audio-video group (AVChatRoom)
        delete callback;
    });

V2TIMManager::GetInstance()->GetGroupManager()->GetGroupOnlineMemberCount(groupID, callback);
```
:::
</dx-tabs>
