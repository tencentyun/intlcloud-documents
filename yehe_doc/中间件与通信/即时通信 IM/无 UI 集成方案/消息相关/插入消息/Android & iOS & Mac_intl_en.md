## Feature Description
When a message is inserted, the message will only be inserted into the local database but not be sent to the server.
This API is used to insert tips into a conversation, such as "You have left the group" and "Keep your information secure. Do not send private information such as account, password, and verification code to the group chat". Such messages need to be displayed in the chat area, but do not need to be sent to others.

> ! Inserted messages will be lost if the account is logged in on another mobile device or the application is uninstalled and reinstalled.


### Inserting a local message between one-to-one messages

Call `insertC2CMessageToLocalStorage` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a5afe4461b4a47205d2865ea94317d4aa) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#acc1dccd310d1965248cff0d4fd5ca45f)) to insert a local message between one-to-one messages.

Sample code:

<dx-tabs>
::: Android
```java
// Create a message
V2TIMMessage msg = V2TIMManager.getMessageManager().createTextMessage("Insert a local message between one-to-one messages");
// Insert the message into the local database
V2TIMManager.getMessageManager().insertC2CMessageToLocalStorage(msg, "receiver_userID", "sender_userID", new V2TIMValueCallback<V2TIMMessage>() {
  @Override
  public void onSuccess(V2TIMMessage message) {
  	// Inserted the message between one-to-one messages successfully
  }

  @Override
  public void onError(int code, String desc) {
  	// Failed to insert the message between one-to-one messages
  }
});
```
:::
::: iOS and macOS
```objectivec
// Create a message
V2TIMMessage *msg = [[V2TIMManager sharedInstance] createTextMessage:@"Insert a local message between C2C messages"];
// Insert the message into the local database
[[V2TIMManager sharedInstance] insertC2CMessageToLocalStorage:msg
                                                           to:@"receiver_userID"  // `userID` of the receiver
                                                       sender:@"sender_userID"  // `userID` of the sender
                                                         succ:^{
    NSLog(@"Message inserted between one-to-one messages successfully");
} fail:^(int code, NSString *msg) {
    NSLog(@"Failed to insert the message between one-to-one messages, code: %d, msg: %@", code, msg);
}];
```
:::
</dx-tabs>


### Inserting a local message between group messages

Call `insertGroupMessageToLocalStorage` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a04a3f6c250f9d6c0053fd71be74f047f) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a9b312b67e4da19978b55a7b915815dfe)) to insert a local message between group messages.

Sample code:
<dx-tabs>
::: Android
```java
// Create a message
V2TIMMessage msg = V2TIMManager.getMessageManager().createTextMessage("Insert a local message between group messages");
// Insert the message into the local database
V2TIMManager.getMessageManager().insertGroupMessageToLocalStorage(msg, "groupID", "sender_userID", new V2TIMValueCallback<V2TIMMessage>() {
  @Override
  public void onSuccess(V2TIMMessage message) {
  	// Message inserted between group messages successfully
  }

  @Override
  public void onError(int code, String desc) {
  	// Failed to insert the message between group messages
  }
});
```
:::
::: iOS and macOS
```objectivec
// Create a message 
V2TIMMessage *msg = [[V2TIMManager sharedInstance] createTextMessage:@"Insert a local message between group messages"];
// Insert the message into the local database
[[V2TIMManager sharedInstance] insertGroupMessageToLocalStorage:msg 
                                                             to:@"groupID"  // `groupID` of the group chat
                                                         sender:@"sender_userID"  // `userID` of the sender
                                                           succ:^{
    NSLog(@"Message inserted between group messages successfully");
} fail:^(int code, NSString *msg) {
    NSLog(@"Failed to insert the message between group messages, code: %d, msg: %@", code, msg);
}];
```
:::
</dx-tabs>
