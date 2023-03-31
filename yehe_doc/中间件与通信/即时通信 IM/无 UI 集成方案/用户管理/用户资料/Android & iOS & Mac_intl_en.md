## Feature Description
Users can query the information of themselves, friends, and non-friend users. They can also change their nicknames, profile photos, and statuses, as well as friend remarks and list.
The methods are in the `V2TIMManager` and `V2TIMFriendshipManager(Android)` / `V2TIMManager(Friendship)(iOS and macOS)` core classes.


## Relationship Chain Event Listener
Call `addFriendListener` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#af09d0d2297fe73cc81b8e8941bcd35b2) / [iOS and Mac](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#a1de011b63b3c20b1be519dc7ba124704) / [Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMFriendshipManager.html#ac4c542617008471fa1fe7a64ba963fbb)) to add a relationship chain event listener.

To stop receiving relationship chain events, call `removeFriendListener` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a6a823459f109bcd8744806f8f1b8bfea) / [iOS and Mac](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#aed40ccbbc4e15be79154077a6d3ec085) / [Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMFriendshipManager.html#ae21ca2737c35305ecc1f25e054265ed8)) to remove the relationship chain event listener.

> ! You need to set the relationship chain event listener in advance to receive event notifications.

Sample code:
<dx-tabs>
::: Android
```java
// Add a relationship chain listener
V2TIMManager.getFriendshipManager().addFriendListener(listener);
// Remove the relationship chain listener
V2TIMManager.getFriendshipManager().removeFriendListener(listener);
```
:::
::: iOS and macOS
```objectivec
// Add a relationship chain listener
// `self` is id<V2TIMFriendshipListener>.
[[V2TIMManager sharedInstance] addFriendListener:self];

// Remove the relationship chain listener
[[V2TIMManager sharedInstance] removeFriendListener:self];
```
:::
::: Windows
```cpp
class FriendshipListener final : public V2TIMFriendshipListener {
    // Member...
};

// Add a relationship chain event listener. Keep `friendshipListener` valid before the listener is removed to ensure event callbacks are received.
FriendshipListener friendshipListener;
V2TIMManager::GetInstance()->GetFriendshipManager()->AddFriendListener(&friendshipListener);

// Remove the relationship chain listener
V2TIMManager::GetInstance()->GetFriendshipManager()->RemoveFriendListener(&friendshipListener);
```
:::
</dx-tabs>


## User Profile Management
### Querying and modifying your own profile
Call the `getUsersInfo` API ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a7ca8c0f71a9875021fc35dfcaff68d1e) / [iOS and Mac](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#ac638c1dd6ec1e5204637e4b87129cd38) / [Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMManager.html#ac7aa404aec07fc0d9823d9da5fd4e443)) and enter a user's `UserID` for the `userIDList` parameter to query the user's profile.

Sample code:
<dx-tabs>
::: Android
```java
// Obtain a user's personal profile
String loginUser = V2TIMManager.getInstance().getLoginUser();
List<String> userIDList = new ArrayList<>();
userIDList.add(loginUser);
V2TIMManager.getInstance().getUsersInfo(userIDList, new V2TIMValueCallback<List<V2TIMUserFullInfo>>() {
  @Override
  public void onSuccess(List<V2TIMUserFullInfo> profiles) {
  	// User's profile obtained successfully
  }
  @Override
  public void onError(int code, String desc) {
  	// Failed to obtain the user's profile
  }
});
```
:::
::: iOS and macOS
```objectivec
// Obtain a user's personal profile
NSString *loginUser = [[V2TIMManager sharedInstance] getLoginUser];
[[V2TIMManager sharedInstance] getUsersInfo:@[loginUser] succ:^(NSArray<V2TIMUserFullInfo *> *infoList) {
    // User's profile obtained successfully
} fail:^(int code, NSString *desc) {
    // Failed to obtain the user's profile
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

V2TIMString loginUser = V2TIMManager::GetInstance()->GetLoginUser();
V2TIMStringVector userIDList;
userIDList.PushBack(loginUser);

auto callback = new ValueCallback<V2TIMUserFullInfoVector>{};
callback->SetCallback(
    [=](const V2TIMUserFullInfoVector& userFullInfoList) {
        // User's profile obtained successfully
        delete callback;
    },
    [=](int error_code, const V2TIMString& error_message) {
        // Failed to obtain the user's profile
        delete callback;
    });

V2TIMManager::GetInstance()->GetUsersInfo(userIDList, callback);
```
:::
</dx-tabs>

Call the `setSelfInfo` API ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#af004ab2f1d1458de354883f1995b678a) / [iOS and Mac](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a328a0d2d07e8d34e12effb73937c3437) / [Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMManager.html#acb89663576c7f68cc4b9983733835e29)) to modify a user's profile.
A user's profile includes the user's nickname, profile photo, status, gender, birth date, and friend request approval method. For more information, see the definitions of the `V2TIMUserFullInfo` class ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMUserFullInfo.html) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMUserFullInfo.html) / [Windows](https://im.sdk.qcloud.com/doc/en/structV2TIMUserFullInfo.html)).
After the profile is modified successfully, you will receive the `onSelfInfoUpdated` callback ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMSDKListener.html#a94852c92bb087e5aabb6cf6fe9ba77f8) / [iOS and Mac](https://im.sdk.qcloud.com/doc/en/protocolV2TIMSDKListener-p.html#ab3e8543e99934530763daa7eeffbab89) / [Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMSDKListener.html#a0aa71b6e7638fddd65f3e82f7eb264c3)).

Sample code:
<dx-tabs>
::: Android
```java
// Set the user's profile
V2TIMUserFullInfo info = new V2TIMUserFullInfo();
info.setNickname("nickName");
info.setFaceUrl("faceUrl");
V2TIMManager.getInstance().setSelfInfo(info, new V2TIMCallback() {
  @Override
  public void onSuccess() {
		// User's profile set successfully
  }

  @Override
  public void onError(int code, String desc) {
		// Failed to set the user's profile
  }
});

// Listen for the callback for a user's profile change
V2TIMManager.getInstance().addIMSDKListener(new V2TIMSDKListener() {
  @Override
  public void onSelfInfoUpdated(V2TIMUserFullInfo info) {
  	// Received the callback for a user's profile change
  }
});
```
:::
::: iOS and macOS
```objectivec
// Set the user's profile
V2TIMUserFullInfo *info = [[V2TIMUserFullInfo alloc] init];
info.nickName = @"nickName";
info.faceURL = @"faceURL";
[[V2TIMManager sharedInstance] setSelfInfo:info succ:^{
    // User's profile set successfully
} fail:^(int code, NSString *desc) {
    // Failed to set the user's profile
}];

// Listen for the callback for a user's profile change
[[V2TIMManager sharedInstance] addIMSDKListener:self];
- (void)onSelfInfoUpdated:(V2TIMUserFullInfo *)Info {
    // Received the callback for a user's profile change
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

V2TIMUserFullInfo info;
info.nickName = u8"nickName";
info.faceURL = u8"faceUrl";
info.modifyFlag = V2TIMUserInfoModifyFlag::V2TIM_USER_INFO_MODIFY_FLAG_NICK |
                  V2TIMUserInfoModifyFlag::V2TIM_USER_INFO_MODIFY_FLAG_FACE_URL;

auto callback = new Callback{};
callback->SetCallback(
    [=]() {
        // User's profile set successfully
        delete callback;
    },
    [=](int error_code, const V2TIMString& error_message) {
        // Failed to set the user's profile
        delete callback;
    });

V2TIMManager::GetInstance()->SetSelfInfo(info, callback);

// Listen for the callback for a user's profile change
class SDKListener final : public V2TIMSDKListener {
public:
    SDKListener() = default;
    ~SDKListener() override = default;

    void OnSelfInfoUpdated(const V2TIMUserFullInfo& info) override {
        // Received the callback for a user's profile change
    }
    // Other members …
};
// Add an event listener. Keep `sdkListener` valid before the listener is removed to ensure event callbacks are received.
SDKListener sdkListener;
V2TIMManager::GetInstance()->AddSDKListener(&sdkListener);
```
:::
</dx-tabs>

### Querying and modifying a friend's profile
Call the `getFriendsInfo` API ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a8c4e51e508d140e4a7ce5f4caf49c870) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#a39f6752da11b595e4a5b6dcb0eb6a584) / [Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMFriendshipManager.html#a9b263f612a1e7e35ee2c745b5f36a1e3)) to query the profile of the specified friend. For more information, see [Friend Management](https://intl.cloud.tencent.com/document/product/1047/48159).

### Querying the user profile of a non-friend user
Call the `getUsersInfo` API ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a7ca8c0f71a9875021fc35dfcaff68d1e) / [iOS and Mac](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#ac638c1dd6ec1e5204637e4b87129cd38) / [Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMManager.html#ac7aa404aec07fc0d9823d9da5fd4e443)) and enter the `UserID` of a non-friend user for the `userIDList` parameter to query the profile of the non-friend user.

> ? 
> 1. The profile of a non-friend user cannot be modified.
> 2. When the profile of a non-friend user is updated, the backend cannot send any system notification to the SDK because there is no friend relationship, so the non-friend user's profile **will not be updated in real time**. To avoid sending a network request to the backend every time the user profile is obtained and save network resources, the SDK adds a caching logic, setting a 10-minute interval between proactive pulls of the same user's profile from the backend.

Sample code:

<dx-tabs>
::: Android
```java
List<String> userIDList = new ArrayList<>();
userIDList.add("userA");
V2TIMManager.getInstance().getUsersInfo(userIDList, new V2TIMValueCallback<List<V2TIMUserFullInfo>>() {
  @Override
  public void onSuccess(List<V2TIMUserFullInfo> profiles) {
  	// Obtained the profile of the non-friend user successfully
  }

  @Override
  public void onError(int code, String desc) {
  	// Failed to obtain the profile of the non-friend user
  }
});
```
:::
::: iOS and macOS
```objectivec
// Get the profile of a non-friend user
[[V2TIMManager sharedInstance] getUsersInfo:@[@"userA"] succ:^(NSArray<V2TIMUserFullInfo *> *infoList) {
    // Obtained the profile of the non-friend user successfully
} fail:^(int code, NSString *desc) {
    // Failed to obtain the profile of the non-friend user
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
userIDList.PushBack(u8"userA");

auto callback = new ValueCallback<V2TIMUserFullInfoVector>{};
callback->SetCallback(
    [=](const V2TIMUserFullInfoVector& userFullInfoList) {
        // Obtained the profile of the non-friend user successfully
        delete callback;
    },
    [=](int error_code, const V2TIMString& error_message) {
        // Failed to obtain the profile of the non-friend user
        delete callback;
    });

V2TIMManager::GetInstance()->GetUsersInfo(userIDList, callback);
```
:::
</dx-tabs>
