## Feature Description
You can merge and forward messages in the following steps:
1. Create a merged message based on the list of original messages.
2. Send the merged message to the receiver.
3. The receiver receives the merged message and parses the list of original messages.

The title and digest are needed to display the merged message, as shown below:

| Merge and Forward                                            | Display of Merged Message                                    | Click Merged Message to Download Message List for Display    |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| <img src="https://qcloudimg.tencent-cloud.cn/raw/cb970fdd471cdd668b5ce31d188970fd.png" width = "300" /> | <img src="https://qcloudimg.tencent-cloud.cn/raw/2304c7ea1e29de702f99d96e52a9739c.png" width = "300" /> | <img src="https://qcloudimg.tencent-cloud.cn/raw/f2c81dc8df0064cf8202d06a79f7af16.png" width = "219"/> |


## Merging and Forwarding Messages
### Creating and sending a merged message

A merged message can be created by setting the message list along with the merged message title and digest. The process is as follows:
1. Call the `createMergerMessage` API ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#acebe275789ab49cc8abe6af5e07aa3b0) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a2943bb31403aeb22f8582cd9966cf13e) to create a merged message. The list of original messages as well as the merged message title and digest also need to be set.

<img src="https://qcloudimg.tencent-cloud.cn/raw/dbc9a0f199effcf6d865b6497ec185f3.png" width = "450" />


| Attribute      | Description                | Remarks                                                      |
| -------------- | -------------------------- | ------------------------------------------------------------ |
| messageList    | List of original messages  | List of original messages to be merged and forwarded         |
| title          | Title                      | Title of the merged message, such as "Chat History of xixiyah and Hello" as shown above |
| abstractList   | Digest list                | Digest list of the merged message as shown above. The original message digests need to be displayed for the merged message, which will be unfolded after the user clicks the cell. |
| compatibleText | Compatibility text message | If the early SDK version does not support the merged message, the user will receive a text message with the content `compatibleText` by default. |

Sample code:
<dx-tabs>
::: Android
```java
// List of messages to be forwarded, which can contain merged messages but not group tips
List<V2TIMMessage> msgs = new ArrayList<>();
msgs.add(message1);
msgs.add(message2);
// Title of the merged message
String title = "Chat History of vinson and lynx"; 
// Digest list of the merged message
List<String> abstactList = new ArrayList<>();
msgs.add("abstract1");
msgs.add("abstract2");
msgs.add("abstract3");
// Compatibility text of the merged message. If the early SDK version does not support the merged message, the user will receive a text message with the content `compatibleText` by default.
String compatibleText = "Upgrade to the latest version to check the merged message"; 
// Create a merged message
V2TIMMessage mergeMessage = V2TIMManager.getMessageManager().createMergerMessage(msgs, title, abstractList, compatibleText);
```
:::
::: iOS and macOS
```objectivec
// List of messages to be forwarded, which can contain merged messages but not group tips
NSArray *msgs = @[message1,message2...];  
// Title of the merged message
NSString *title = @"Chat History of vinson and lynx";  
// Digest list of the merged message
NSArray *abstactList = @[@"abstract1",@"abstract2",@"abstract3"]; 
// Compatibility text of the merged message. If the SDK on an early version does not support the merged message, the user will receive a text message with the content `compatibleText` by default.
NSString *compatibleText = @"Upgrade to the latest version to check the merged message"; 
// Create a merged message
V2TIMMessage *mergeMessage = [[V2TIMManager sharedInstance] createMergerMessage:msgs title:title 
abstractList:abstactList compatibleText:compatibleText];
```
:::
</dx-tabs>

2. Call the `sendMessage` API ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a28e01403acd422e53e999f21ec064795) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a681947465d6ab718da40f7f983740a21)) to send the merged message.

Sample code:
<dx-tabs>
::: Android
```java
// Send the merged message to the user `denny`
V2TIMManager.getMessageManager().sendMessage(mergeMessage, "denny", null, V2TIMMessage.V2TIM_PRIORITY_NORMAL, false, null, new V2TIMSendCallback<V2TIMMessage>() {
  @Override
  public void onProgress(int progress) {}

  @Override
  public void onSuccess(V2TIMMessage v2TIMMessage) {}

  @Override
  public void onError(int code, String desc) {}
  })
```
:::
::: iOS and macOS
```objectivec
// Send the merged message to the user `denny`
[[V2TIMManager sharedInstance] sendMessage:mergeMessage receiver:@"denny"  groupID:nil
 priority:V2TIM_PRIORITY_NORMAL  onlineUserOnly:NO  offlinePushInfo:nil progress:nil succ:nil fail:nil];
```
:::
</dx-tabs>


### Receiving a merged message

#### Adding a listener
The receiver can call `addAdvancedMsgListener` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#aaccdec10b9fbee5e43eaf908e359c823) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#acf794752cc6bfa786aea5cd7fabadfab)) to add the advanced message listener.
We recommend it be called early, such as after the chat page is initialized, to ensure timely message receiving in the application.

Sample code:
<dx-tabs>
::: Android
```java
V2TIMManager.getMessageManager().addAdvancedMsgListener(advancedMsgListener);
```
:::
::: iOS and macOS
```objectivec
// `self` is id<V2TIMAdvancedMsgListener>
[[V2TIMManager sharedInstance] addAdvancedMsgListener:self];
```
:::
</dx-tabs>

#### Parsing a message
After the listener is added, the receiver will receive the merged message `V2TIMMessage` in `onRecvNewMessage`.
You can use the merged message element `V2TIMMergerElem` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMergerElem.html) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMMergerElem.html)) to get the `title` and `abstractList` for UI display.
Then, when the user clicks the merged message, you can call the `downloadMergerMessage` API ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMergerElem.html#af34d8228a9842875652a726f24ac3d30) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMMergerElem.html#ad77abfe27eabf237aee7c951100e6755)) to download the merged message list for UI display.

Sample code:
<dx-tabs>
::: Android
```java
@Override
public void onRecvNewMessage(V2TIMMessage msg) {
  if (msg.getElemType() == V2TIMMessage.V2TIM_ELEM_TYPE_MERGER) {
    // Get the elements of the merged message
    V2TIMMergerElem mergerElem = msg.getMergerElem();
    // Get the `title`
    String title = mergerElem.getTitle();
    // Get the digest list
    List<String> abstractList = mergerElem.getAbstractList();
    // Download the merged message list when the user clicks the merged message
    mergerElem.downloadMergerMessage(new V2TIMValueCallback<List<V2TIMMessage>>() {
      @Override
      public void onSuccess(List<V2TIMMessage> v2TIMMessages) {
        // Downloaded successfully. `v2TIMMessages` is the merged message list.
        for (V2TIMMessage subMsg : v2TIMMessages) {
        // If the merged message list still contains a merged message, continue to parse the message.
        if (subMsg.getElemType() == V2TIMMessage.V2TIM_ELEM_TYPE_MERGER) {
          V2TIMMergerElem mergerElem = subMsg.getMergerElem();
          // Get the `title`
          String title = mergerElem.getTitle();
          // Get the digest list
          List<String> abstractList = mergerElem.getAbstractList();
          // Download the merged message list when the user clicks the merged message
          ......
        }
      }
    }

    @Override
    public void onError(int code, String desc) {
    // Download failed
    }
  });
}
```
:::
::: iOS and macOS
```objectivec
- (void)onRecvNewMessage:(V2TIMMessage *)msg {
    if (msg.elemType == V2TIM_ELEM_TYPE_MERGER) {
        // Get the elements of the merged message
        V2TIMMergerElem *mergerElem = msg.mergerElem;
        // Get the `title`
        NSString *title = mergerElem.title;
        // Get the digest list
        NSArray *abstractList = mergerElem.abstractList;
        // Download the merged message list when the user clicks the merged message
        [msg.mergerElem downloadMergerMessage:^(NSArray<V2TIMMessage *> *msgs) {
            // Downloaded successfully. `msgs` is the merged message list.
            for (V2TIMMessage *subMsg in msgs) {
                // If the merged message list still contains a merged message, continue to parse the message.
                if (subMsg.elemType == V2TIM_ELEM_TYPE_MERGER) {
                    V2TIMMergerElem *mergerElem = subMsg.mergerElem;
                    // Get the `title`
                    NSString *title = mergerElem.title;
                    // Get the digest list
                    NSArray *abstractList = mergerElem.abstractList;
                    // Download the merged message list when the user clicks the merged message
                    [msg.mergerElem downloadMergerMessage:nil fail:nil];
                }
            }
        } fail:^(int code, NSString *desc) {
            // Download failed
        }];
    }
}
```
:::
</dx-tabs>

#### Removing a listener
To stop receiving messages, the receiver can call `removeAdvancedMsgListener` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a44e1e9126bf5b30234330fe19259cd93) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a28aeebff4a791c9bb8f91a4f61e020e6)) to remove the advanced message listener.

Sample code:
<dx-tabs>
::: Android
```java
V2TIMManager.getMessageManager().removeAdvancedMsgListener(advancedMsgListener);
```
:::
::: iOS and macOS
```objectivec
// `self` is id<V2TIMAdvancedMsgListener>
[[V2TIMManager sharedInstance] removeAdvancedMsgListener:self];
```
:::
</dx-tabs>


## Forwarding Messages One by One
To forward a single message, create a message identical to the original message through the `createForwardMessage` API ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#af8f609bfbfe99a0c65611b14159b6b4d) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a05d088b7d9883e18af41355cdd3f4562)) first, and then call the `sendMessage` API ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a28e01403acd422e53e999f21ec064795) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a681947465d6ab718da40f7f983740a21)) to send the message.

Sample code:
<dx-tabs>
::: Android
```java
// Create a message with the same elements as the original message
V2TIMMessage forwardMessage = V2TIMManager.getMessageManager().createForwardMessage(originMsg);
// Send the message to the user `denny`
V2TIMManager.getMessageManager().sendMessage(forwardMessage, "denny", null, V2TIMMessage.V2TIM_PRIORITY_NORMAL, false, null, new V2TIMSendCallback<V2TIMMessage>() {
  @Override
  public void onProgress(int progress) {
  }

  @Override
  public void onSuccess(V2TIMMessage message) {
  }

  @Override
  public void onError(int code, String desc) {
  }
});
```
:::
::: iOS and macOS
```objectivec
// Create a message with the same elements as the original message
V2TIMMessage *forwardMessage = [[V2TIMManager sharedInstance] createForwardMessage:originMsg];
// Send the message to the user `denny`
[[V2TIMManager sharedInstance] sendMessage:forwardMessage receiver:@"denny"  groupID:nil
 priority:V2TIM_PRIORITY_NORMAL  onlineUserOnly:NO  offlinePushInfo:nil progress:nil succ:nil fail:nil];
```
:::
</dx-tabs>
