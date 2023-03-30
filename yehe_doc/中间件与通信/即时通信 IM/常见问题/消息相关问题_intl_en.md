[](id:Q1)

### Large numbers of vendor conflicts occur after the integration with both IM and TPNS. What should I do?
Currently, IM uses the vendor JAR package provided by [TPNS](https://intl.cloud.tencent.com/product/tpns). You can solve this problem by referring to the [IM Offline Push (Android)](https://intl.cloud.tencent.com/document/product/1047/39156) documentation and replacing relevant dependency packages.

[](id:Q2)
### What if a message fails to be received or is lost?

- One-to-one chat message
  - Check that the message was sent successfully.
  - Check that the recipient has logged in successfully.
  - Check that the specified conversation that sent the message is consistent with the recipient’s conversation.
- Group message
  - Check that the message was sent successfully.
  - Check that the recipient has logged in successfully.
  - Check that the recipient is a group member.

Whether it’s a C2C message or a group message, if the problem cannot be resolved through the above steps, you need to continue to check the following:
1. Check that a message listener has been registered.
2. Check that the sender added `elem` to the message when sending the message (check the return value of `addElement` when sending a message).
3. For Android users, check that multiple message listeners have been registered and that `true` was returned in the message listeners.


[](id:Q3)
### What should I do if offline push messages fail to be received?

- APNs
Refer to [Offline Push (iOS)](https://intl.cloud.tencent.com/document/product/1047/39157) to check the following:
  - Check that the correct certificate has been uploaded to the Tencent Cloud console.
  - Check that the token was successfully uploaded to Tencent Cloud after successful login.
  - Check that the correct certificate ID was reported when you reported the token.
  - Check that foreground/background switch events have been reported correctly.
  - Check if the message contains only `TIMCustomElem`, with the `desc` attribute being left empty.
  - Check if the deduplication identifiers such as `MsgRandom` were set to the same value, resulting in push failures due to deduplication.
  - For a group message, check that no alert has been enabled.

- Android
  Refer to [Offline Push Configuration](https://intl.cloud.tencent.com/document/product/1047/34336) to check the following:
  - Check that the correct push certificate has been uploaded.
  - Check that the token has been reported successfully.
  - When not using third-party offline push (Huawei, Xiaomi, or Meizu), check that the QALService process is active. If the process is not active, offline push messages will fail to be received. In that case, the auto-start permissions of the system need to be relied on.
  - In the case of multiple processes, check that IM SDK initialization was performed only in the main process. If not, you need to modify the configuration to ensure that IM SDK initialization is performed only in the main process.
  - When using third-party offline push (such as Xiaomi, Huawei, and Meizu), you can first use the corresponding third-party console to directly push a message and check whether the mobile phone can receive the message. If the mobile phone fails to receive the message, there are two possible reasons:
    1) The user failed to correctly integrate third-party offline push. Please refer to the relevant documentation.
    2) The mobile phone is not compatible with the offline push. For example, some Huawei mobile phones cannot receive Huawei offline push.
  - When using OPPO offline push, check the MasterSecret, instead of AppSecret, was entered in the Android push certificate on the IM console.

When using either APNs push or Android offline push, if the problem cannot be located through the above steps, you need to continue to check the following issues:
1. Check that the recipient ID is consistent with the target user ID of the push message.
2. Check that you have enabled the offline push listener (Android).
3. Check that notifications are enabled. For iOS, see [Offline Push (iOS)](https://intl.cloud.tencent.com/document/product/1047/39157#.E8.AE.BE.E7.BD.AE.E8.87.AA.E5.AE.9A.E4.B9.89.E6.8E.A8.E9.80.81.E6.8F.90.E7.A4.BA.E9.9F.B3); for Android, see [Offline Push Configuration](https://intl.cloud.tencent.com/document/product/1047/34336#.E8.AE.BE.E7.BD.AE.E5.85.A8.E5.B1.80.E7.A6.BB.E7.BA.BF.E6.8E.A8.E9.80.81.E9.85.8D.E7.BD.AE).
4. Check that the message is an online message sent through the `sendOnlineMessage` API or that `MsgLifeTime` was set to `0` during push through a RESTful API.
5. Check that the offline notification is enabled for the message. For iOS, see (https://intl.cloud.tencent.com/document/product/1047/39157#.E8.87.AA.E5.AE.9A.E4.B9.89.E7.A6.BB.E7.BA.BF.E6.B6.88.E6.81.AF.E5.B1.9E.E6.80.A7); for Android, see [Offline Push Configuration](https://intl.cloud.tencent.com/document/product/1047/34336#.E9.92.88.E5.AF.B9.E5.8D.95.E6.9D.A1.E6.B6.88.E6.81.AF.E8.AE.BE.E7.BD.AE.E7.A6.BB.E7.BA.BF.E6.8E.A8.E9.80.81).
6. If you still cannot identify the problem, you can provide the relevant information to tech support personnel for troubleshooting.


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
Historical message storage is available for one-to-one chat messages and non-audio-video group messages. You can log in to the <a href="https://console.cloud.tencent.com/im">IM console</a> to modify the relevant configuration. The default configuration for different packages is as follows: <ul style="margin:0;"><li>Free edition: 7 days, with no extension supported</li><li>Pro edition: 7 days, with extension supported</li><li>Ultimate edition: 30 days, with extension supported</li></ul>The extension of the historical message storage period is a value added service. For more information, see <a href="https://intl.cloud.tencent.com/document/product/1047/34350">Value-added Service Pricing</a>.

[](id:Q7)
### Why does it show that messages are sent successfully even though the senders are blocklisted?
When you enable **Show "Sent successfully" After Sending Messages** in the [Blocklist Check](https://intl.cloud.tencent.com/document/product/1047/34419) section in the IM console, blocklisted users will be prompted that the messages are sent successfully when they send messages, but the recipients will not receive the messages. When you disable this feature, blocklisted users will be prompted that message sending fails when they send messages and the SDK will receive [error code 20007](https://intl.cloud.tencent.com/document/product/1047/34348). For more information, see the **Blocklist check** section in [Feature Configuration](https://intl.cloud.tencent.com/document/product/1047/34419).

[](id:Q8)
### How to convert an image address into the downloadable domain name format by using COS?
You need to upload the image yourself. If the image uses COS private read, you need to get a signed URL to obtain the download permission ([Download via Pre-Signed URL](https://intl.cloud.tencent.com/document/product/436/14116)).

[](id:Q9)
### What are the rules for unique identification of IM messages?
IM uses `sg_id`, `msgID`, and `msgKey` as the unique identifiers of one-to-one and group chat messages.

Different types of IM messages and SDKs use different unique identifiers:
- For client SDKs, one-to-one and group chat messages are identified by `msg_id` in the following format: tinyid-clientTime-random.
- For web SDKs of v2.17.0 or earlier, one-to-one and group chat messages are identified by `msgID` in the following format: Conversation ID-msgSeq-random-1 (messages sent by me) / 0 (messages sent by others).
- For web SDKs of v2.18.0 or later, one-to-one and group chat messages are identified by `msgID` in the following format: tinyid-clientTime-random.
- For server SDKs, one-to-one messages are identified by `msgKey` in the following format: clientSeq_random_serverTime.
- For server SDKs, group chat messages are identified by "Group ID + msgSeq".

[](id:Q10)
### Do audio-video groups and community groups support @ messages?
Audio-video groups do not support sending @ messages. Community groups support @ a single user but do not support @ all users.
