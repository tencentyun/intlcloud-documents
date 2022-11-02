### If I send a message in which `Message.nick` and `Message.avatar` are both empty, how can the message be processed to normally display the nickname and profile photo on the screen?

You can call [getMyProfile](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getMyProfile) to obtain your nickname and profile photo.

### How can I mute a group member in a livestreaming group?

You can use a custom message to mute a specific group member. The custom message must contain the Members_Account of the group member to be muted and the muting time. Send the custom message to the business backend by calling the [Callback Before Delivering Group Messages](https://intl.cloud.tencent.com/document/product/1047/34374). The business backend will call [Muting and Unmuting Group Members](https://intl.cloud.tencent.com/document/product/1047/34951) to mute the group member.

### How can I remove a group member from a livestreaming group?

You can use a custom message to remove a specific group member. The custom message must contain the Members_Account of the group member to be removed. Set the priority of the custom message to High to prevent the message from being discarded by the backend due to the message sending frequency limit of 40 messages per second. After the SDK receives the message, it calls the [kickGroupMember API](https://intl.cloud.tencent.com/document/product/1047/36169) to remove the group member from the group.

### Why are messages lost?

Messages can be lost due to the following conditions:

- Livestreaming groups have a message sending frequency limit of 40 messages per second. You can determine whether a message is discarded due to the frequency limit based on the callbacks before and after delivering group messages. If a message receives the callback before delivering group messages but does not receive the callback after delivering group messages, the message is discarded due to the frequency limit.
- When a group member leaves a livestreaming group from the WeChat Mini Program or web client, the member may also leave on the Android, iOS, or PC client. For more information, see [FAQ 4](#p4).
- If the WeChat Mini Program or web client encounters an exception, check whether your SDK version is earlier than v2.7.6. If yes, upgrade your SDK to the latest version.

If the problem persists, submit a ticket to contact us.

### How can I compile statistics on likes and follows?

Customize the like or follow message type. When a user clicks the like or follow icon on the frontend to deliver a custom message, send the like or follow message to the business side by calling the [Callback Before Delivering Group Messages](https://intl.cloud.tencent.com/document/product/1047/34374). The business side counts the number of received like and follow messages and updates the data to the group profile field every 3 to 5 seconds by calling [Modify Basic Group Profiles](https://intl.cloud.tencent.com/document/product/1047/34962). The SDK calls the [getGroupsInfo API](https://intl.cloud.tencent.com/document/product/1047/36169) to count the number of like or follow messages.

### How can I properly set message priorities?

To prevent important messages from being discarded, a livestreaming group provides three message priorities for all messages. The SDK preferentially obtains high priority messages. We recommend that you set the priorities of custom messages as follows:

- High: red packets, gifts, and messages for removing group members
- Normal: common text messages
- Low: likes and follows

### Are there any open-source livestreaming components that can be directly used to watch videos and chat?

Yes. The code is also open-source. For more information, see [Tencent Cloud TWebLive](https://github.com/tencentyun/TWebLive).
