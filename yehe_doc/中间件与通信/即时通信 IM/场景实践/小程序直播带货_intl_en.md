
Traditional sales methods are costly and the results are difficult to assess. Livestream marketing, however, can integrate search channels, delivery channels, order channels, assessment channels, and operation channels to prevent customer loss due to channel redirection. Therefore, livestream marketing is an integral part of your integrated marketing blueprint in the Internet era.
Data shows that the number of online livestream service users in China reached 504 million in 2019 and is expected to reach 526 million in 2020. Retail sales via livestream platforms will hit RMB 916 billion, accounting for 8.7% of online retail sales in China. With the current boom in livestream e-commerce, it might be a good idea to build your own livestream marketing platform instead of merely selling through mainstream platforms.
## Background

The following features must be implemented for interactive scenarios:
- Chat room
- Announcement
- Notifications on user joining and exit of the group
- Notification on new products on the backend
- Notification on gift giving
- Notification on new gifts on the backend
- Like and like notifications
- Livstreaming
- Live room status control

As you can see, the core functionality of livestream marketing consists of Instant Messaging (IM) and livestreaming. Therefore, you can use [Instant Messaging (IM)](https://intl.cloud.tencent.com/document/product/1047) and [Live Video Broadcasting (LVB)](https://intl.cloud.tencent.com/document/product/267) as the underlying services to meet your needs.

## Demo
![](https://main.qcloudimg.com/raw/3158cc06a9e6fafa48554bbe1918fa8e.jpg)

## Scenario-based SDK

In livestreaming scenarios, you can enable like, gift, and follow notifications through custom messages, and enable notifications on new products and group status changes through group custom fields. For this purpose, we encapsulate a [scenario-based SDK](https://www.npmjs.com/package/im-live-sells) for easy implementation of the related features.

You can also build your own livestream marketing platform by completing these steps:

## Directions
### Step 1: Create a live chat room by using AVChatroom in IM

Chat rooms are a crucial component of livestreaming. They allow users to send messages and receive messages from other users in the same room.

1. Log in to the [IM console](https://console.cloud.tencent.com/im) and click **Add Application**.
2. In the **Create Application** dialog box, enter your app name and click **OK**.
    After the app is created, you can view the status, version, SDKAppID, creation time, and expiry time of the new app on the overview page in the console.
  >New apps are created as Trial Edition apps by default and can be upgraded to Pro Edition or Flagship Edition when needed.
  >A Tencent Cloud account supports a maximum of 300 IM apps. If you have reached that limit, [disable and delete](https://intl.cloud.tencent.com/document/product/1047/34540) unwanted apps before creating a new one. **Once an app is deleted, all the data and services associated with the SDKAppID are removed and cannot be restored, so please proceed with caution.**
3. Click the target app card and select **Group Management** in the left sidebar.
4. On the **Group Management** page, click **Add Group**.
5. Configure the following parameters in the "Add Group" dialog box that appears.
 - Group Name: enter the name of the group. This parameter is required, and its maximum length is 30 bytes.
 - Group Owner ID: enter the group owner ID. This parameter is optional, and you must enter a registered user name.
 - Group Type: set the group type. **Audio-video chat room is recommended** according to [Group Types](https://intl.cloud.tencent.com/document/product/1047/33529).
3. Click **OK** to save the configuration.
 After the group is created, you can see the group ID, group name, group owner, type, and creation time in the group list.


### Step 2: Enable like, gift, and purchase notifications through custom messages

In a livestream marketing scenario, you want to send lots of messages in real time to engage group members. For example, when a group member sends a gift to the host, and you want all group members to be notified of this with a special effect. This can be achieved by using custom messages in IM. Custom messages can carry additional information. For example, a gift message can have gift information and user information attached to it. Other user behaviors such as giving likes, purchasing products, and following the host can trigger notifications in the same way. Unlike text messages and rich-text messages, custom messages are a special kind of message that carry special signals.

The following shows the sample code for sending custom messages in the SDK:

```
public async sendCustomMsgAndEmitEvent(type: string, extension?: string) {
        const message = this.tim.createCustomMessage({
            to: this.roomID,
            conversationType: this.TIM.TYPES.CONV_GROUP,
            priority: this.TIM.TYPES.MSG_PRIORITY_HIGH,
            payload: {
                data: type,
                description: '',
                extension: extension
            }
        })
        await this.tim.sendMessage(message)
        const res = {
            nick: this.userInfo.nick,
            avatar: this.userInfo.avatar,
            value: extension,
            userID:this.userInfo.userID
        }
        this.eventBus.emit(type, res)
        return res
}
```

### Step 3: Enable notifications on new products and lives room status changes through group custom fields

In a livestream marketing scenario, when the host is introducing a product, the product area at the bottom of the screen should be updated with the current product, and all users in the chat room should be notified of the launch of the new product. Generally, new product messages are triggered by the assistant.
Technically, the assistant can trigger new product messages in two ways:
- The assistant sends custom messages:
 - This method requires that the assistant has already joined the current livestreaming group.
 - When there are too many group messages, the IM backend returns messages based on message priority. As custom messages have lower priority, the product displayed in the client app might not be promptly updated.
- The assistant modifies the group profile:
 - In this case, the assistant may or may not be a member of the current livestreaming group. For example, the assistant can be the group admin.
 - While there are defined default group profile fields, IM provides group-level custom fields for which you can specify definitions and read-write permissions.

We recommend that you enable notifications on new products by having the admin modify group custom fields. The steps are as follows:

#### Adding group custom fields

1. Log in to the [IM console](https://console.cloud.tencent.com/im) and click the target app card. In the left sidebar, choose **Feature Configuration** > **Group Custom Field**.
2. On the **Group Custom Field** page, click **Add Group-level Custom Field**.
3. In the "Group Custom Field" dialog that appears, enter a name for the custom field and set the group type and access permissions.
  >
  >- The field name can only contain letters, numbers, and underscores (\_), but cannot begin with a number. The maximum length of the name is 16 characters.
  >- A group custom field and a group member custom field cannot have the same name.
  >
3. Select **I understand that after adding a group custom field and group type, the read-write permissions of the group type can be modified, but the custom field cannot be deleted.** and click **Confirm** to save the configuration.
 The group-level custom field configuration takes effect in about 10 minutes.

#### Using group custom fields

The assistant calls the [RESTful API for modifying basic group profiles](https://intl.cloud.tencent.com/document/product/1047/34962) as the group admin to update the corresponding group custom field and send notification messages for new products or LVB status changes.


### Step 4: Calculate user levels by using the callback triggered by group message sending

In addition to a profile photo and nickname, every livestreaming audience member has a level, which increases after sending messages or gifts. This feature can be enabled with callbacks. You can use callbacks to be notified of user changes related to groups, relationship chains, one-to-one chat messages, and online statuses and then change a user’s level depending on whether the user sends text messages or gift messages.
For callback-related operations, see [Callback Configuration](https://intl.cloud.tencent.com/document/product/1047/34520) and [Third-Party Callback Overview](https://intl.cloud.tencent.com/document/product/1047/34354).

### Step 5: Block sensitive words with content filtering

Content filtering capabilities are essential in fields like livestreaming, social networking, and consultation. In the live streaming scenario, sending sensitive content could have serious consequences. IM provides a feature to filter out sensitive words and supports filtering some national leader names by default. You can also purchase the value-added [content filtering service](https://intl.cloud.tencent.com/document/product/1047/34350) for this purpose.


### Step 6: Generate a push address and start streaming with LVB
Tencent Cloud Live Video Broadcasting (LVB) helps with the growth of e-commerce platforms by enabling merchants to display items in greater detail and assisting consumers in making informed decisions, ultimately reducing marketing costs and boosting sales.
Before starting a live stream, you need to generate a push address through the [address generator](https://intl.cloud.tencent.com/document/product/267/31084) and then begin [LVB push](https://intl.cloud.tencent.com/document/product/267/31558).

