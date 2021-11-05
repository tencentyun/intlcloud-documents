[](id:Q1)
### Large numbers of vendor conflicts occur after the simultaneous integration of IM and TPNS. What should I do?
Currently, IM uses the vendor JAR package provided by [TPNS](https://intl.cloud.tencent.com/product/tpns). You can solve this problem by referring to the [IM Offline Push (Android)](https://intl.cloud.tencent.com/document/product/1047/39156) documentation and replacing relevant dependency packages.

[](id:Q2)
### What if a message fails to be received or is lost?

- One-to-one chat message
 - Confirm that the message was sent successfully.
 - Confirm that the recipient has logged in successfully.
 - Confirm that the specified conversation that sent the message is consistent with the recipient’s conversation.
- Group message
 - Confirm that the message was sent successfully.
 - Confirm that the recipient has logged in successfully.
 - Confirm that the recipient is a group member.

Whether it’s a C2C message or a group message, if the problem cannot be confirmed through the above steps, you need to continue to confirm the following issues:
1. Confirm that a message listener has been registered.
2. Confirm that the sender added `elem` to the message when sending the message (check the return value of `addElement` when sending a message).
3. For Android users, confirm that multiple message listeners have been registered and that `true` was returned in the message listeners.


[](id:Q3)
### What should I do if offline push messages fail to be received?

- APNs
Refer to [Offline Push (iOS)](https://intl.cloud.tencent.com/zh/document/product/1047/34347) to confirm the following:
 - Confirm that the correct certificate has been uploaded to the Tencent Cloud console.
 - Confirm that the token was successfully uploaded to Tencent Cloud after successful login.
 - Confirm that the correct certificate ID was reported when you reported the token.
 - Confirm that foreground/background switch events have been reported correctly.
 - Check if the message contains only `TIMCustomElem`, with the `desc` attribute being left empty.
 - Check if the deduplication identifiers such as `MsgRandom` were set to the same value, resulting in push failures due to deduplication.
 - For a group message, confirm that no alert has been enabled.

- Android
Refer to [Offline Push Configuration](https://intl.cloud.tencent.com/document/product/1047/34336) to confirm the following:
 - Confirm that the correct push certificate has been uploaded.
 - Confirm that the token has been reported successfully.
 - When not using third-party offline push (Huawei, Xiaomi, or Meizu), confirm that the QALService process is active. If the process is not active, offline push messages will fail to be received. In that case, the auto-start permissions of the system need to be relied on.
 - In the case of multiple processes, confirm that IM SDK initialization was performed only in the main process. If not, you need to modify the configuration to ensure that IM SDK initialization is performed only in the main process.
 - When using third-party offline push (such as Xiaomi, Huawei, and Meizu), you can first use the corresponding third-party console to directly push a message and confirm whether the mobile phone can receive the message. If the mobile phone fails to receive the message, there are two possible reasons:
    1) The user failed to correctly integrate third-party offline push. Please refer to the relevant documentation.
    2) The mobile phone is not compatible with the offline push. For example, some Huawei mobile phones cannot receive Huawei offline push.
 - When using OPPO offline push, confirm that MasterSecret, instead of AppSecret, was entered in the Android push certificate on the IM console.

When using either APNs push or Android offline push, if the problem cannot be located through the above steps, you need to continue on to confirm the following issues:
1. Confirm that the recipient ID is consistent with the target user ID of the push message.
2. Confirm that you have enabled the offline push listener (Android).
3. Confirm that notifications are enabled. For iOS, see [Offline Push (iOS)](https://intl.cloud.tencent.com/zh/document/product/1047/34347); for Android, see [Offline Push Configuration](https://intl.cloud.tencent.com/document/product/1047/34336#.E8.AE.BE.E7.BD.AE.E5.85.A8.E5.B1.80.E7.A6.BB.E7.BA.BF.E6.8E.A8.E9.80.81.E9.85.8D.E7.BD.AE).
4. Confirm that the message is an online message sent through the `sendOnlineMessage` API or that `MsgLifeTime` was set to `0` during push through a RESTful API.
5. Confirm that the offline notification is enabled for the message. For iOS, see (https://intl.cloud.tencent.com/zh/document/product/1047/34347); for Android, see [Offline Push Configuration](https://intl.cloud.tencent.com/document/product/1047/34336#.E9.92.88.E5.AF.B9.E5.8D.95.E6.9D.A1.E6.B6.88.E6.81.AF.E8.AE.BE.E7.BD.AE.E7.A6.BB.E7.BA.BF.E6.8E.A8.E9.80.81).
6. If you still cannot identify the problem, you can provide the relevant information to tech support personnel for troubleshooting.

[](id:Q4)
### How is a group @ message processed?
There is no essential difference between an in-group @ message and an ordinary message, although the user specified by @ will see a special UI effect. For example, the message will be highlighted in red on the QQ message list. For the specific implementation, you can refer to the following scheme:
1. When sending a message, listen for keyboard events to detect whether the @ character is input. If it is input, display the group member list on the UI of the sender, allowing the sender to select the @ target user. Here, it is assumed that the selected user is user1.
2. After the @ target user is selected, add @ and the ID of the selected user, for example "@user1", to the message input box.
3. Add a `TIMCustomElem` in the message, and in the `TIMCustomElem`, add a custom message protocol to mark the message as an @ message.
A simple protocol definition can be as follows:
```
{
	"type":"REMIND",
	"target":"user1"
}
```
The sample code for constructing an @ message is as follows (here, the Android platform is used as an example):

```java
// Send a text message and specify user1 as the @ target
TIMMessage msg = new TIMMessage();
// Construct the text message elements
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
	// Construct custom message elements based on the custom protocol
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

>! In the configuration, `TIMTextElem` is not required. If you are sure that foul language filtering is not needed, you can fill the message content of `TIMTextElem` to the `desc` attribute in `TIMCustomElem`.
>
4. After constructing the message, send the message to the group.
5. After group members receive the message, check whether the message protocol in `TIMCustomElem` is the @ message protocol. If yes, go to the next step. Otherwise, skip it.
6. Check whether the @ target user is consistent with the currently logged-in user. If yes, perform special processing on the UI. Otherwise, no processing is needed.

[](id:Q5)
### How is a red packet message processed?

Red packet messages are similar to @ messages and can be implemented via `TIMCustomElem`. Red packet messages require apps to perform special processing on the UI. For example, if the system detects that the current message is a red packet message, the message should be displayed in the form of a red packet.
In addition, as red packet messages are important messages, we recommend that you set the message priority to high when sending a red packet message. As far as possible, this ensures that the red packet message will reach the target user even if the message frequency limit is reached (currently, the default frequency limit for in-group messages is 40 messages per second, and that for one-to-one chat messages is 5 messages per second).

For more information about message priority, see [Message Priority](https://intl.cloud.tencent.com/document/product/1047/33526).

>! The payment feature of red packet messages requires manual integration of the corresponding payment SDK. At present, the IM SDK does not provide this payment feature.

The process for constructing a simple red packet message is as follows (Android):
```java
// Construct a new message
TIMMessage msg = new TIMMessage();
try{
	// Specify the custom message protocol
    JSONObject redPacket= new JSONObject();
	redPacket.put("type", "RED_PACKET");
    redPacket.put("amount", 2018);
	redPacket.put("msg", "Happy new year!");

    // Construct custom message elements based on the custom protocol
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

// Set the message priority to high
msg.setPriority(TIMMessagePriority.High);
```

[](id:Q6)
### What’s the storage period of an IM message?
Historical message storage is available for one-to-one chat messages and non–audio-video group messages. You can log in to the <a href="https://console.cloud.tencent.com/im">IM console</a> to modify the relevant configuration. The default configuration for different packages is as follows: <ul style="margin:0;"><li>Trial edition: 7 days, with no extension supported</li><li>Pro edition: 7 days, with extension supported</li><li>Flagship edition: 30 days, with extension supported</li></ul>The extension of the historical message storage period is a value-added service. For more information, see <a href="https://intl.cloud.tencent.com/document/product/1047/34350">Value-added Service Pricing</a>.

[](id:Q7)

### Why does it show that messages are sent successfully even though the senders are blocklisted?
When you enable **Show "Sent successfully" After Sending Messages** in the [Blocklist Check](https://intl.cloud.tencent.com/document/product/1047/34419) section in the IM console, blocklisted users will be prompted that the messages are sent successfully when they send messages, but the recipients will not receive the messages. When you disable this feature, blocklisted users will be prompted that message sending fails when they send messages and the SDK will receive [error code 20007](https://intl.cloud.tencent.com/document/product/1047/34348). For more information, see the **Blocklist check** section in [Feature Configuration](https://intl.cloud.tencent.com/document/product/1047/34419).

