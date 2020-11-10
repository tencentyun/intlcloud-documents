### What should I do if an expected message is not received or lost?

- One-to-one chat message
 - Check whether the message was sent successfully.
 - Check whether the recipient has logged in successfully.
 - Check whether the specified conversation of the sent message is consistent with that of the recipient.
- Group chat message
 - Check whether the message was sent successfully.
 - Check whether the recipient has logged in successfully.
 - Check whether the recipient is a group member.

For both one-to-one and group chat messages, if you cannot confirm the cause through the preceding steps, proceed as follows:
1. Check whether a message listener is registered.
2. Check whether `elem` is added to the message when the sender sends the message (the return value of `addElement` needs to be checked when the message is sent).
3. For Android users, check whether multiple message listeners are registered and whether `true` is returned in the message listeners.



### What should I do if offline push notifications cannot be received?

- APNs
Check the following items by referring to "Offline Push (iOS)":
 - Check whether the certificate is correctly uploaded to the Tencent Cloud console.
 - Check whether the token is successfully uploaded to Tencent Cloud after successful login.
 - Check whether the correct certificate ID is reported when the token is reported.
 - Check whether a foreground-background switching event is reported correctly.
 - Check whether the message contains only `TIMCustomElem` and the `desc` attribute in it is null.
 - Check whether `MsgRandom` and other deduplication identifiers are the same, which results in push failure due to deduplication.
 - For a group message, check whether the system is configured to provide no reminder for messages.

- Android
Check the following items by referring to "Offline Push Configuration":
 - Check whether the push certificate is uploaded correctly.
 - Check whether the token is reported successfully.
 - If the message is not pushed offline by a third party (for example, Huawei, Xiaomi, or Meizu), check whether the QALService process is alive. If not, no messages pushed offline will be received. In this case, the auto-start permission of the system is required.
 - In cases where multiple processes exist, check whether IM SDK initialization is only performed on the main process. If no, modify the configuration to ensure the initialization is only performed on the main process.
 - If the message is pushed offline by a third party (for example, Huawei, Xiaomi, or Meizu), you can directly push the message through the corresponding third-party console and check whether the receiving mobile phone can receive the message. If the mobile phone cannot receive the message, there are two possible reasons:
    1) A problem exists when integrating the third-party offline push feature. Please handle according to the documentation.
    2) The mobile phone is incompatible with the offline push feature. For example, certain Huawei phones cannot receive messages pushed offline by the Huawei push service.
 - For OPPO offline push, check whether MasterSecret, instead of AppSecret, is entered in the Android push certificate on the IM Console.

For APNs push or offline push on Android systems, if you cannot find the cause by completing the preceding steps, proceed as follows:
1. Check whether the recipient ID is consistent with the ID of the user to which the message is to be pushed.
2. Check whether the offline push listener (for Android) is enabled.
3. Check whether the silent mode is enabled. For iOS, see "Setting Custom Push Notification Sounds". For Android, see "Configuring Global Offline Push Settings".
4. Check whether the message is an online message sent through the `sendOnlineMessage` API or whether `MsgLifeTime` is set to `0` during push through a RESTful API.
5. Check whether an identifier indicating no offline push is set for the message. For iOS, see "Customizing Offline Message Attributes". For Android, see "Configuring Offline Push Settings for a Single Message".
6. If you still cannot locate the cause, provide relevant information to technical personnel for troubleshooting.

### How do I process @ group messages?

There is basically no difference between an @ group message and a common group message, except that when the user targeted by @ receives the message, special processing on the UI is required. For example, the message is highlighted in red in the QQ message list. For detailed implementation, see the following sample solution:
1. During message sending, monitor keyboard events to check whether the @ sign is entered. If yes, display the group member list on the UI for the sender to choose the target user for the @ sign. Here, assume that the chosen target user is `user1`.
2. After the target user for the @ sign is chosen, add the @ sign and the ID of the chosen user to the message input box, for example, `@user1`.
3. Add `TIMCustomElem` to the message. In `TIMCustomElem`, add the message protocol that you design to mark the message as an @ message.
A simple protocol definition can be as follows:
```
{
	"type":"REMIND",
	"target":"user1"
}
```
The sample code for constructing an @ message (using the Android platform as an example) is as follows:

```java
// Send a text message, with the @ sign added before group member user1.
TIMMessage msg = new TIMMessage();
// Construct text message elements
TIMTextElem txtElem = new TIMTextElem();
txtElem.setText("@user1 nice to meet u");
if(msg.addElement(txtElem) != 0){
	Log.e(TAG, "add text elem failed");
	return;
}
try{
	// Specify the custom message protocol
	JSONObject remindProto = new JSONObject();
	remindProto.put("type", "REMIND");
	remindProto.put("target", "user1");
	// Construct custom message elements based on the protocol you have defined
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

>! Here, `TIMTextElem` is not required. If vulgar language filtering is not required, you can enter the message content of `TIMTextElem` in the `desc` attribute of `TIMCustomElem`.
>
4. After constructing the message, send it to the group.
5. After group members receive the message, check whether the message protocol in `TIMCustomElem` of the message is the @ message protocol. If yes, proceed to the next step. Otherwise, skip the next step.
6. Check whether the user specified by the @ sign is consistent with the currently logged-in user. If yes, perform special processing on the UI. Otherwise, no processing is needed.

### How should I process red packet messages?

Red packet messages are similar to @ messages and can be implemented through `TIMCustomElem`. Apps need to perform corresponding special processing on the UI. For example, after detecting that the current message is a red packet message, the app needs to display it as a red packet.
In addition, as red packet messages are important messages, we recommend that you set them as high-priority messages when sending them to ensure, as far as possible, that they can reach the recipients successfully even under delivery restrictions (currently, the default maximum frequency of sending group messages is 40 messages per second, and the default maximum frequency of sending one-to-one chat messages is 5 messages per second).

For more information about message priorities, see [Message Priorities](https://intl.cloud.tencent.com/document/product/1047/33526).

>! The payment feature of red packet messages requires apps to integrate corresponding payment SDKs on their own. The IM SDK currently does not provide this feature.

The process of constructing a simple red packet message (Android) is as follows:
```java
// Construct a new message
TIMMessage msg = new TIMMessage();
try{
	// Specify the custom message protocol
    JSONObject redPacket= new JSONObject();
	redPacket.put("type", "RED_PACKET");
    redPacket.put("amount", 2018);
	redPacket.put("msg", "Happy new year!");

    // Construct custom message elements based on the protocol you have defined
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

// Set the priority of the message to high priority
msg.setPriority(TIMMessagePriority.High);
```

### How long are IM messages retained?
Historical message retention is available for one-to-one chat messages and non-AVChatRoom group messages. You can log in to the <a href="https://console.cloud.tencent.com/im">IM Console</a> to modify the relevant configuration. The default retention periods for different billing plans are as follows:<ul style="margin:0;"><li>Trial edition: free retention for 7 days, no extension supported. </li><li>Pro edition: free retention for 7 days, extension supported. </li><li>Flagship edition: free retention for 30 days, extension supported.</li></ul>Extending the retention period of historical messages is a paid value-added service. For specific billing information, see <a href="https://intl.cloud.tencent.com/document/product/1047/34350">Value-added Service Pricing</a>.

