## Feature Description
The sender listens for the characters in the input box. When the user enters @, the group member selection UI will pop up. After the target group members are selected, the message will be displayed in the input box in the format of `"@A @B @C......"`, which can be further edited before sent.
In the group chat list of the receiver's conversation UI, the identifier `"someone@me"` or `"@ all"` will be displayed to remind the user that the user was mentioned by someone in the group chat.

> ? Currently, only text @ messages are supported.

## Demo

| Listening for the @ character for group member selection | Editing and sending the group @ message | Receiving the group @ message |
|---------|---------|---------|
| ![](https://main.qcloudimg.com/raw/870063a7d732d5df29971609b39d4796.png) | ![](https://main.qcloudimg.com/raw/f4ace5e8b7d697be14c18c8b08de0b36.png) | ![](https://main.qcloudimg.com/raw/0291a12d3ce8edfb880dab2e4b9541c8.png) |

Figure 1: When the @ character is detected in the input box on the chat UI, the user is redirected to the group member selection UI to select the target group members.
Figure 2: After selecting the target group members, the user goes back to the chat UI to edit and send the group @ message.
Figure 3: If a user is mentioned, the user receives the conversation update, and the "someone@me" information is displayed in the conversation `Cell`.

## Sending a Group @ Message

1. The sender listens for the text input box on the chat UI and launches the group member selection UI. After group members are selected, the ID and nickname information of the members is called back. The ID is used to create the `V2TIMMessage` object, while the nickname is to be displayed in the text box.
2. The sender calls the `createTextAtMessage` API ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a09a259ceb314754dd267533597138391) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#aaebbd8ed9b9766d01f996ec722744346)) to create a text @ message, get the `V2TIMMessage` object, and specify the target group members.
3. The sender calls the `sendMessage` API ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a28e01403acd422e53e999f21ec064795) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a681947465d6ab718da40f7f983740a21)) to send the created @ message.

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
      // Failed to send the group @ message
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
</dx-tabs>


## Receiving a Group @ Message

1. When the conversation is loaded and updated, call the `groupAtInfolist` API ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversation.html#a54790b0fd99c2504a73b42b884fba8a9) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMConversation.html#a5659c29a54304e89e61c25c2b073f8da)) of `V2TIMConversation` to get the @ data list of the conversation.
2. Call the `atType` API ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupAtInfo.html#aebb86a00883eb70fdab2c5f4728aae5d) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMGroupAtInfo.html#a1486d853fd6f8ae074714ec8059f7621)) of the `V2TIMGroupAtInfo` object in the list to get the @ data type and update it to the @ information of the conversation.

Sample code:
<dx-tabs>
::: Android
```java
// Get the list of group @ data
List<V2TIMGroupAtInfo> atInfoList = conversation.getGroupAtInfoList();
// Parse the @ type (@me, @all, @me and @all)
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
    atTips = "[Someone@me][@all]";
}
```
:::
::: iOS and macOS
```objectivec
// Get the list of group @ data
NSArray<V2TIMGroupAtInfo *> *atInfoList = conversation.groupAtInfolist;

// Parse the @ type (@me, @all, @me and @all)
BOOL atMe = NO;         // Whether it's @me
BOOL atAll = NO;        // Whether it's @all
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
</dx-tabs>


