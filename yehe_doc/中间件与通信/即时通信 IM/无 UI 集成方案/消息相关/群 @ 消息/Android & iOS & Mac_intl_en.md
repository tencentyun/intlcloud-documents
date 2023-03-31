## Overview
The sender listens for the characters in the input box. When the user enters @, the group member selection UI will pop up. After the target group members are selected, the message will be displayed in the input box in the format of `"@A @B @C......"`, which can be further edited before sent.
In the group chat list of the receiver's conversation UI, the identifier `"someone@me"` or `"@ all"` will be displayed to remind the user that the user was mentioned by someone in the group chat.

> ? Currently, only text @ messages are supported.

## Feature Demonstration

| Listening for the @ character for group member selection     | Editing and sending the group @ message                      | Receiving the group @ message                                |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| ![](https://qcloudimg.tencent-cloud.cn/raw/ed60cac72b215f6e7128cf2533bab2f7.jpg) | ![](https://qcloudimg.tencent-cloud.cn/raw/fbabe9cac382a7944676565242b29b59.jpg) | ![](https://qcloudimg.tencent-cloud.cn/raw/b20c30564c78b9fec9ab25260110641f.jpg) |

Figure 1: When the @ character is detected in the input box on the chat UI, the user is redirected to the group member selection UI to select the target group members.
Figure 2: After selecting the target group members, the user goes back to the chat UI to edit and send the group @ message.
Figure 3: If a user is mentioned, the user receives the conversation update, and the "someone@me" information is displayed in the conversation `Cell`.

## Sending a Group @ Message

1. The sender listens for the text input box on the chat UI and launches the group member selection UI. After group members are selected, the ID and nickname information of the members is called back. The ID is used to create the `V2TIMMessage` object, while the nickname is to be displayed in the text box.
2. The sender calls the `createTextAtMessage` API ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a09a259ceb314754dd267533597138391) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#aaebbd8ed9b9766d01f996ec722744346) / [Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMMessageManager.html#afa39182f419c621fc929eb3929206107)) to create a text @ message, get the `V2TIMMessage` object, and specify the target group members.
3. The sender calls `sendMessage` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a28e01403acd422e53e999f21ec064795) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a681947465d6ab718da40f7f983740a21) / [Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMMessageManager.html#a42db237e7ae52cd2aa7edebf4f435c61)) to send the created @ message object.

Sample code:
<dx-tabs>
::: Android
```java
// Group members `user1` and `user2`
List<String> atUserList = new ArrayList<>();
atUserList.add("user1");
atUserList.add("user2");
// Create a group @ message
V2TIMMessage v2TIMMessage = V2TIMManager.getMessageManager().createTextAtMessage(message, atUserList);
// Send the group @ message
V2TIMManager.getMessageManager().sendMessage(v2TIMMessage, null, "toGroupID",  V2TIMMessage.V2TIM_PRIORITY_DEFAULT, false, null,  new V2TIMSendCallback<V2TIMMessage>() {
  @Override
  public void onError(int code, String desc) {
      // The group @ message failed to be sent
  }
  @Override
  public void onSuccess(V2TIMMessage v2TIMMessage) {
      // Group @ message sent successfully
  }
  @Override
  public void onProgress(int progress) {
  }
});
```
:::
::: iOS and macOS
```objective-c
// Create a group @ message to @ group members "xixi" and "yahaha"
V2TIMMessage *atMsg = [[V2TIMManager sharedInstance] createTextAtMessage:@"This is a group text @ message." atUserList:@[@"xixi", @"yahaha"]];
// Send the group @ message
[[V2TIMManager sharedInstance] sendMessage:atMsg receiver:nil groupID:@"groupA" priority:V2TIM_PRIORITY_NORMAL onlineUserOnly:NO offlinePushInfo:nil progress:nil succ:nil fail:nil];
```
:::
::: Windows
```cpp
class SendCallback final : public V2TIMSendCallback {
public:
    using SuccessCallback = std::function<void(const V2TIMMessage&)>;
    using ErrorCallback = std::function<void(int, const V2TIMString&)>;
    using ProgressCallback = std::function<void(uint32_t)>;

    SendCallback() = default;
    ~SendCallback() override = default;

    void SetCallback(SuccessCallback success_callback, ErrorCallback error_callback,
                     ProgressCallback progress_callback) {
        success_callback_ = std::move(success_callback);
        error_callback_ = std::move(error_callback);
        progress_callback_ = std::move(progress_callback);
    }

    void OnSuccess(const V2TIMMessage& message) override {
        if (success_callback_) {
            success_callback_(message);
        }
    }
    void OnError(int error_code, const V2TIMString& error_message) override {
        if (error_callback_) {
            error_callback_(error_code, error_message);
        }
    }
    void OnProgress(uint32_t progress) override {
        if (progress_callback_) {
            progress_callback_(progress);
        }
    }

private:
    SuccessCallback success_callback_;
    ErrorCallback error_callback_;
    ProgressCallback progress_callback_;
};

V2TIMStringVector atUserList;
atUserList.PushBack("user1");
atUserList.PushBack("user2");
V2TIMMessage message = V2TIMManager::GetInstance()->GetMessageManager()->CreateTextAtMessage(
    u8"This is a group text @ message.", atUserList);

auto callback = new SendCallback{};
callback->SetCallback(
    [=](const V2TIMMessage& message) {
        // Group @ message sent successfully
        delete callback;
    },
    [=](int error_code, const V2TIMString& error_message) {
        // The group @ message failed to be sent
        delete callback;
    },
    [=](uint32_t progress) {});

V2TIMManager::GetInstance()->GetMessageManager()->SendMessage(
    message, "denny", {}, V2TIMMessagePriority::V2TIM_PRIORITY_NORMAL, false, {}, callback);
```
:::
</dx-tabs>


## Receiving a Group @ Message

1. When the conversation is loaded and updated, call the `groupAtInfolist` API ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversation.html#a54790b0fd99c2504a73b42b884fba8a9) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMConversation.html#a5659c29a54304e89e61c25c2b073f8da) / [Windows](https://im.sdk.qcloud.com/doc/en/structV2TIMConversation.html#a297aabc46d5b475e8e5fbd2054e0a330)) of `V2TIMConversation` to get the @ data list of the conversation.
2. Call the `atType` API ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupAtInfo.html#aebb86a00883eb70fdab2c5f4728aae5d) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMGroupAtInfo.html#a1486d853fd6f8ae074714ec8059f7621) / [Windows](https://im.sdk.qcloud.com/doc/en/structV2TIMGroupAtInfo.html#a1486d853fd6f8ae074714ec8059f7621)) of the `V2TIMGroupAtInfo` object in the list to get the @ data type and update it to the @ information of the conversation.

Sample code:
<dx-tabs>
::: Android
```java
// Obtain the group @ data list
List<V2TIMGroupAtInfo> atInfoList = conversation.getGroupAtInfoList();
// Parse the @ type (@me, @all members, @me and @all members)
boolean atMe = false;
boolean atAll = false;
String atTips = "";
for(V2TIMGroupAtInfo atInfo : atInfoList){
  if (atInfo.getAtType() == V2TIMGroupAtInfo.TIM_AT_ME){
    atMe = true;
    continue;
  }
  if (atInfo.getAtType() == V2TIMGroupAtInfo.TIM_AT_ALL){
    atAll = true;
    continue;
  }
}

// Based on the @ type, prompt:
if (atMe && !atAll) {
    atTips = "[Someone@me]";
} else if (!atMe && atAll) {
    atTips = "[@all]";
} else if (atMe && atAll) {
    atTips = "[someone@me][@all members]";
}
```
:::
::: iOS and macOS
```objectivec
// Obtain the group @ data list
NSArray<V2TIMGroupAtInfo *> *atInfoList = conversation.groupAtInfolist;

// Parse the @ type (@me, @all members, @me and @all members)
BOOL atMe = NO;         // Whether it's @me
BOOL atAll = NO;        // Whether it's @all members
NSString *atTipsStr = @"";
for (V2TIMGroupAtInfo *atInfo in atInfoList) {
    switch (atInfo.atType) {
        case V2TIM_AT_ME:
            atMe = YES;
            break;
        case V2TIM_AT_ALL:
            atAll = YES;
            break;
        case V2TIM_AT_ALL_AT_ME:
            atMe = YES;
            atAll = YES;
            break;
        default:
            break;
    }
}

// Based on the @ type, prompt:
if (atMe && !atAll) {
    atTipsStr = @"[someone@me]";
}
if (!atMe && atAll) {
    atTipsStr = @"[@all members]";
}
if (atMe && atAll) {
    atTipsStr = @"[someone@me][@all members]";
}
```
:::
::: Windows
```cpp
// Obtain the group @ data list
V2TIMGroupAtInfoVector groupAtInfolist = conversation.groupAtInfolist;
// Parse the @ type (@me, @all members, @me and @all members)
bool atMe = false;
bool atAll = false;
std::string atTips = "";

for (size_t i = 0; i < groupAtInfolist.Size(); ++i) {
    const V2TIMGroupAtInfo& atInfo = groupAtInfolist[i];
    switch (atInfo.atType) {
        case V2TIM_AT_ME:
            atMe = true;
            break;
        case V2TIM_AT_ALL:
            atAll = true;
            break;
        case V2TIM_AT_ALL_AT_ME:
            atMe = true;
            atAll = true;
            break;
        default:
            break;
    }
}

// Based on the @ type, prompt:
if (atMe && !atAll) {
    atTips = u8"[someone@me]";
} else if (!atMe && atAll) {
    atTips = u8"[@all members]";
} else if (atMe && atAll) {
    atTips = u8"[someone@me][@all members]";
}
```
:::
</dx-tabs>
