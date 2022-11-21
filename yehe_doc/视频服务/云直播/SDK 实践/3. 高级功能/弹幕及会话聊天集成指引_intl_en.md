## Overview
In the live streaming business, hosts and viewers usually need to interact in real time through various means such as on-screen comments and chat. However, integration of such features is complex. This document uses IM as an example to describe how to implement requirements such as on-screen comments, chat, and item recommendations during live streaming as well as possible problems and considerations, giving a glimpse of the live streaming business and requirements.
![](https://qcloudimg.tencent-cloud.cn/raw/f4f23f4f722c178b85488aeefd760c1b.jpg)

## Key Feature Description
| Feature | Description |
|---------|---------|
| Live on-screen comments, gifts, and likes | Hundreds of millions of concurrent messages can be sustained to build a friendly interaction experience. |
| Various chat modes such as one-to-one and group live chat | Users can send messages and receive messages from other members in the same chat room. Diverse message types such as text, images, audio, and short videos can be pushed in real time, which encourages more user activity. |
| Item push in live shopping | In live shopping scenarios, when the host recommends an item, it needs to be immediately displayed in the item slot at the bottom of the screen and notified to all viewers. Notifications of new items are generally triggered by the virtual assistant. |
| Broadcast in a live room | The broadcast feature is similar to a system notice sent to live rooms. When the system admin delivers a broadcast message, all the live rooms under the `SDKAppID` will receive it. |


## Integration Method

### Step 1. Create an application
To set up a live room in Tencent Cloud, you need to create an IM application in the [console](https://console.tencentcloud.com/im) as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/63a4addb1394488d16f4873765066f6d.png)


### Step 2. Complete the relevant configuration
The application created in step 1 is the Free edition, which applies only to development. In the production environment, you need to activate the Pro or Ultimate edition as needed. For more information on differences between different editions, see [Pricing](https://www.tencentcloud.com/document/product/1047/34350).
In live streaming scenarios, you need some extra configurations after creating the application.
- **Calculating the `UserSig` with a key**
In the IM account system, the password required by a user login is calculated by the server with a key provided by IM. For more information, see [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385). In the development phase, to avoid holding back development on the client, you can also calculate the `UserSig` in the [console](https://console.cloud.tencent.com/im/tool-usersig) as shown below:
<img src="https://qcloudimg.tencent-cloud.cn/raw/12e52c2d8bde72fa76c750657ead2a10.png" width=850>
- **Configuring an admin account**
During live streaming, an admin may need to send messages to a live room and mute (remove) non-compliant users, which can be done through APIs on the IM server as described in [RESTful API List](https://www.tencentcloud.com/document/product/1047/34621). To call these APIs, you need to [create an IM admin account](https://console.cloud.tencent.com/im/account-management). By default, IM provides an account with the `UserID` of `administrator`. You can also create multiple admin accounts as needed. Note that you can create up to five admin accounts.
- **Configuring the callback address and enabling the callback**
To implement lucky draws based on on-screen comments, message statistics collection, sensitive content detection, and other requirements, you need to use the IM callback module, where the IM backend calls back the business backend in certain scenarios. You only need to provide an HTTP API and configure it in the [**Callback configuration**](https://console.tencentcloud.com/im/callback-setting) module in the console as shown below:<br>
<img src="https://qcloudimg.tencent-cloud.cn/raw/5f6d94568152fc508fcd9b119a9f01cd.png" width=850>

### Step 3. Integrate the client SDK
After completing the preparations, you need to integrate the IM and TRTC client SDKs into your project. You can select different integration options as needed. For detailed directions, see [Get Started](https://www.tencentcloud.com/document/product/1047/34552).
The following describes common features in a live room and provides best practices with implementation code.

### Step 4. Develop key live room features
1. **Group type selection**
	The user chat section in live streaming scenarios has the following characteristics:
<ul>
<li>Users join and leave a group frequently, and group conversation information (unread count and `lastMessage`) doesn't need to be managed.</li>
<li>Users can join a group without approval.</li>
<li>Users send messages without caring about the chat history.</li>
<li>There are usually a large number of group members.</li>
<li>Group member information doesn't need to be stored.
</ul>

Therefore, you can select **AVChatRoom** as the **Group type** for the live room based on the group characteristics of IM as described in [Group System](https://intl.cloud.tencent.com/document/product/1047/33529). IM audio-video groups (`AVChatRoom`) have the following characteristics:
 - **Support interactive live streaming scenarios with unlimited group members.**
 - Messages (group system notifications) can be pushed to all online members.
 - Users can enter the group directly with no admin approval required.
>? The IM SDK for web allows users to join only one audio-video group (`AVChatRoom`) at a time. If a user logs in to an client and enters live room A, multi-client login is enabled in the [console](https://console.cloud.tencent.com/im/login-message), and the user logs in to another client and enters live room B, the user will be removed from live room A.

2. **Configuration of on-screen comments, gifting, and likes for the live room**
	
- **On-screen comments**
	Audio-video groups (`AVChatRoom`) support on-screen comments, gifts, and like messages to build a friendly interaction experience.
	To create an on-screen comment, you can use the IM API to create a text or custom message. After the message is sent successfully, you need to get its text or custom attributes in the live room by receiving the [OnRecvNewMessage()](https://im.sdk.qcloud.com/doc/zh-cn/classV2TIMAdvancedMsgListener.html#acbd1dba3526377d88f14c2183901511c) callback and then display it on the desired UI.
- **Gift**
	- Non-persistent connection requests from the client are sent to the business server, which involves the billing logic.
	- After fees are incurred, the sender can see that XXX sent the XXX gift (so that the sender can see the gift sent by himself/herself; when there are a large number of messages, the policy for discarding messages may be triggered).
	- After the fees are settled, you can call the server API to send the custom message (gift).
	- If multiple gifts are sent in a row, you need to merge the messages.
		- If the number of gifts is selected in advance, for example 99 gifts, you can send a message with `99` included in the parameter.
		     - If gifts are sent multiple times and the total number is uncertain, you can send a message for every 20 gifts (the value can be adjusted) or clicks within a second. For example, if 99 gifts are clicked in a row, only five messages need to be sent after the optimization.
- **Like**
	- Unlike a gift message, a like message is not billed and directly sent on the client.
	- For like messages that need to be counted on the server, after traffic throttling is performed on the client, likes on the client are counted, and like messages within a short period of time are merged into one. The business server gets the like count in the callback before sending a message.
	- For like messages that don't need to be counted, the logic in step 2 is used, where the business server sends a message after traffic throttling is performed on the client and doesn't need to get the count in the callback before sending a message.
	
3. **Item push in live shopping**
	When the host recommends an item, it needs to be immediately displayed in the item slot at the bottom of the screen and notified to all viewers. Notifications of new items are generally triggered by the virtual assistant. We recommend you implement notifications of new items by enabling the admin to modify a custom group field as follows:
	1. **Add a custom group field**
		
		1. Log in to the [IM console](https://console.cloud.tencent.com/im), click the target IM application card, and select **Feature Configuration** > **Group configuration** on the left sidebar.
		2. On the **Custom Group Field** page, click **Add** in the top-right corner.
		3. In the pop-up dialog box, enter a field name and set the group types and read/write permissions.
		>?
		>- The field name can contain up to 16 characters, supporting letters, digits, and underscores (_). It cannot begin with a digit.
		>- A custom group field and a custom group member field cannot have the same name.
		 ![](https://qcloudimg.tencent-cloud.cn/raw/5766f42c8c06e0979d0c1f2e2898f97a.png)
		
		4. Select **I understand that after a custom group field is added, only the read-write permissions of the added group type can be modified; the group type cannot be reselected or deleted; the field cannot be deleted.** and click **Confirm**.
        >? The custom group field will take effect in about ten minutes after configuration.

	2. **Use the custom group field**
	The virtual assistant calls the [RESTful API for modifying the profile of a group](https://www.tencentcloud.com/document/product/1047/34962) as the group admin at an appropriate time to update the custom group field, so as to send notifications of new items and notifications of live streaming status change in the live room.

4. **Broadcast in a live room**
The broadcast feature is similar to a system notice feature in the live room, but it differs from the latter in that it belongs to messaging. When the system admin delivers a broadcast message, all the live rooms under the `SDKAppID` will receive it.
The broadcast feature is currently available only for the Ultimate edition and needs to be enabled in the console. For more information on how to send a broadcast message on the business backend, see [Broadcast Message of Audio-Video Group](https://www.tencentcloud.com/document/product/1047/49440).
>? If you are not an Ultimate edition user, you can implement the feature by sending a custom group message on the server.

## References
To implement more live room features such as user identity, user level, historical messages, and displaying the number of online users, see [Live Room Setup Guide](https://www.tencentcloud.com/document/product/1047/49589#.E4.BA.8C.E3.80.81.E7.9B.B4.E6.92.AD.E9.97.B4.E5.90.84.E5.8A.9F.E8.83.BD.E5.BC.80.E5.8F.91.E6.8C.87.E5.BC.95).