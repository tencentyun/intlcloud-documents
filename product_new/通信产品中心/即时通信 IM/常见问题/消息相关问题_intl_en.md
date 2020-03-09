### What should I do when I fail to receive the message or the message is discarded?

- For one-to-one chat messages
 - Check whether the message was sent successfully.
 - Check whether the recipient has logged in successfully.
 - Check whether the specified conversation of the sent message is consistent with that of the recipient.
- For group chat messages
 - Check whether the message was sent successfully.
 - Check whether the recipient has logged in successfully.
 - Check whether the recipient is a group member.

For both C2C and group messages, if you cannot determine the cause by completing the preceding procedure, check the following items:
1. Check whether the message listener has been registered.
2. Check whether the sender has added `elem` to the message when sending the message (the return value of `addElement` needs to be checked when the message is sent.)
3. For Android users, check whether multiple message listeners have been registered and whether `true` is returned in the message listeners.



### What should I do if offline push messages fail to be received?

- For APNs
Check the following items by referring to [Offline Push (iOS)](https://intl.cloud.tencent.com/document/product/1047/34347):
 - Check whether the certificate has been uploaded to the Tencent Cloud console correctly.
 - Check whether the token has been successfully uploaded to Tencent Cloud after successful login.
 - Check whether the correct certificate ID has been reported when reporting the token.
 - Check whether foreground-background switch events have been reported correctly.
 - Check whether the message contains only `TIMCustomElem` and the attribute of `desc` in it is null.
 - Check whether `MsgRandom` and other deduplication identifiers are the same, which results in push failure due to deduplication.
 - For a group message, check whether the no message reminder option is enabled.

- For Android
Check the following items by referring to [Offline Push](https://intl.cloud.tencent.com/document/product/1047/34336):
 - Check whether the push certificate has been uploaded correctly.
 - Check whether the token has been reported successfully.
 - If the message is not pushed online by a third party (Huawei, MI, or Meizu), check whether the QALService process is active. If no, no offline push messages can be received. In this case, the auto-start permission of the system is required.
 - In cases where multiple processes exist, check whether only the main process has performed IM SDK initialization. If no, modify the configuration so that only the main process performs initialization.
 - If messages are pushed offline by a third party, such as MI, Huawei, or Meizu, you can directly push the messages through the corresponding third-party console and check whether the receiving mobile phone can receive them. If the mobile phone cannot receive them, two possible reasons apply:
  1) The user’s integration with third-party offline push is abnormal. In this case, handle it according to the relevant document. 
  2) The mobile phone is incompatible with the offline push feature. For example, some Huawei mobile phones cannot receive messages pushed offline by the Huawei push service.
 - For OPPO offline push, check whether MasterSecret, instead of AppSecret, has been entered into the Android push certificate in the IM console.

For APNs push or offline push on Android systems, if you cannot determine the cause by completing the preceding procedure, check the following items:
1. Check whether the recipient ID is consistent with the ID of the target user.
2. Check whether the offline push listener (Android) is enabled.
3. Check whether the silent mode is enabled. For iOS, see [Setting Custom Push Notification Sounds](https://intl.cloud.tencent.com/document/product/1047/34347#.E8.AE.BE.E7.BD.AE.E8.87.AA.E5.AE.9A.E4.B9.89.E6.8E.A8.E9.80.81.E6.8F.90.E7.A4.BA.E9.9F.B3). For Android, see [Configuring Global Offline Push Settings](https://intl.cloud.tencent.com/document/product/1047/34336#.E8.AE.BE.E7.BD.AE.E5.85.A8.E5.B1.80.E7.A6.BB.E7.BA.BF.E6.8E.A8.E9.80.81.E9.85.8D.E7.BD.AE).
4. Check whether the message is an online message that is sent through the `sendOnlineMessage` API or whether `MsgLifeTime` is set to `0` through a RESTful API during push.
5. Check whether an identifier indicating no offline push has been set for the message. For iOS, see [Customizing Offline Message Attributes](https://intl.cloud.tencent.com/document/product/1047/34347#.E8.87.AA.E5.AE.9A.E4.B9.89.E7.A6.BB.E7.BA.BF.E6.B6.88.E6.81.AF.E5.B1.9E.E6.80.A7). For Android, see [Configuring Offline Push Settings for a Single Message](https://intl.cloud.tencent.com/document/product/1047/34336#.E9.92.88.E5.AF.B9.E5.8D.95.E6.9D.A1.E6.B6.88.E6.81.AF.E8.AE.BE.E7.BD.AE.E7.A6.BB.E7.BA.BF.E6.8E.A8.E9.80.81).
6. If you still cannot identify the cause, you can provide relevant information to technical personnel for troubleshooting.

### How to process group @ messages?

There is basically no difference between an @ group message and a common group message, except that when the user specified by @ receives the message, special processing on the UI is required. For example, the message is highlighted in red in the QQ message list. For the detailed implementation, see the following solutions:
1. During message sending, monitor keyboard events to check whether the @ character is entered. If yes, display the group member list on the UI for the sender to choose the target user for the @ sign. Here, assume that the chosen target user is user1.
2. After the target user for the @ sign is chosen, add the @ sign and the ID of the chosen user to the message input box, for example, "@user1".
3. Add `TIMCustomElem` in the message. In `TIMCustomElem`, design and add a message protocol to mark the message as an @ message.
A simple protocol definition is similar to the following:
```
{
	"type":"REMIND",
	"target":"user1"
}
```
The sample code for constructing an @ message (by using the Android platform as an example) is as follows:

```java
// Send a text message, with the @ sign added before group member user1
TIMMessage msg = new TIMMessage();
// Construct text message elements
TIMTextElem txtElem = new TIMTextElem();
txtElem.setText("@user1 nice to meet u");
if(msg.addElement(txtElem) != 0){
	Log.e(TAG, "add text elem failed");
	return;
}
try {
	// Specify the custom message protocol
	JSONObject remindProto = new JSONObject();
	remindProto.put("type", "REMIND");
	remindProto.put("target", "user1");
	// Construct custom message elements based on the defined protocol
	TIMCustomElem customElem = new TIMCustomElem();
	customElem.setDesc("remind msg");
	customElem.setData(remindProto.toString().getBytes("utf-8"));
	if(msg.addElement(customElem) != 0){
		Log.e(TAG, "add custom elem failed");
		return;
	}
}catch(Exception e){
	Log.e(TAG, "build custom elem failed");
	return;
}
```

> Here, `TIMTextElem` is not required. If dirty word filtering is not required, you can enter the message content of `TIMTextElem` in the `desc` field of `TIMCustomElem`.
>
4. After constructing the message, send it to the group.
5. After group members receive the message, check whether the message protocol in `TIMCustomElem` of the message is the @ message protocol. If yes, proceed to the next step. Otherwise, skip it.
6. Check whether the user specified by the @ sign is consistent with the currently logged-in user. If yes, perform special processing on the UI. Otherwise, no processing is required.

### How should I process red packet messages?

Red packet messages are similar to @ messages and can be implemented through `TIMCustomElem`. Apps need to perform corresponding special processing on the UI. For example, after detecting that the current message is a red packet message, the app needs to display it as a red packet.
In addition, as red packet messages are important messages, we recommend that you set them as high-priority messages when sending them to ensure, as far as possible, that they can reach the recipients successfully even under delivery restrictions (currently, the default maximum frequency of sending group messages is 40 messages per second, and the default maximum frequency of sending one-to-one chat messages is 5 messages per second.)

For details on message priorities, see [Message Priorities](https://intl.cloud.tencent.com/document/product/1047/33526#.E7.BE.A4.E6.B6.88.E6.81.AF.E4.BC.98.E5.85.88.E7.BA.A7).

> The payment feature of red packet messages requires apps to integrate corresponding payment SDKs on their own. Currently, the IM SDK does not provide this feature.

The process of constructing a simple red packet message (Android) is as follows:
```java
// Construct a new message
TIMMessage msg = new TIMMessage();
try {
	// Specify the custom message protocol
    JSONObject redPacket= new JSONObject();
	redPacket.put("type", "RED_PACKET");
    redPacket.put("amount", 2018);
	redPacket.put("msg", "Happy new year!");

    // Construct custom message elements based on the defined protocol
	TIMCustomElem customElem = new TIMCustomElem();
    customElem.setDesc("red packet");
	customElem.setData(redPacket.toString().getBytes("utf-8");
    if(msg.addElement(customElem) != 0){
	    Log.e(TAG, "add custom elem failed");
	    return;
	}
}catch(Exception e){
	Log.e(TAG, "build custom elem failed");
    return;
}

// Set the priority of the message to high
msg.setPriority(TIMMessagePriority.High);
```

### How long are IM messages retained?
By default, one-to-one and group chat messages are retained for 7 days. You can extend the retention period for historical messages in **App Configuration** in the [IM console](https://console.cloud.tencent.com/im). The maximum extended period is 12 months. Extending the retention period of historical messages is an added-value service. For billing details, see [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350#.E5.A2.9E.E5.80.BC.E6.9C.8D.E5.8A.A1.E8.B5.84.E8.B4.B9).

