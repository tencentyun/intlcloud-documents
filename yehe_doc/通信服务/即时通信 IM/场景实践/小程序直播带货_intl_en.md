
The cost of traditional marketing methods is high, and their effect is hard to assess. Live marketing is a new marketing method that enables merchants to overcome obstacles in traditional marketing. It combines search channels, outreach channels, order channels, assessment channels, and operation channels to effectively prevent consumer loss caused by channel redirection. Therefore, live marketing has become a necessary choice for integrated marketing in the Internet era.
According to statistics, in 2019, there were 504 million live-streaming users in China, and that figure is expected to reach 526 million in 2020. Live-streaming sales volume is projected to reach RMB 916 billion, accounting for 8.7% of China’s online retail sales. Given the huge size of the market and the great effectiveness of live marketing, merchants must establish their own live marketing platforms in addition to joining various live-streaming platforms.
## Background
According to scenario analysis, the interaction effect can be designed as follows:
<img src="https://main.qcloudimg.com/raw/5f9c19773bcfc22334f3d6cbf4f9e13f.png" width="450px"></img>
The following capabilities need to be implemented in interaction scenarios:
- Chat room features
- Announcement features
- Notifications of users joining or quitting a group
- Notifications of new commodities launched on the backend
- Gift notifications
- Notifications of new gifts launched on the backend
- Likes & like notifications
- Live-streaming features
- Live room status control features

As we can see, the core features of live marketing consist of IM capabilities and live-streaming capabilities. You can use [IM](https://intl.cloud.tencent.com/zh/document/product/1047) and [LVB](https://intl.cloud.tencent.com/zh/document/product/1047) to realize these capabilities.

## Demo Experience
![](https://main.qcloudimg.com/raw/3158cc06a9e6fafa48554bbe1918fa8e.jpg)

## Scenario-based SDK

In live marketing scenarios, you can use custom messages to implement the like, gift, and follower notification features and use custom fields to implement commodity launch notifications and group status change notifications. On that basis, we have encapsulated a [scenario-based SDK](https://www.npmjs.com/package/im-live-sells) to implement the features of live marketing. For more information on its usage, see [Mini Program live-streaming SDK API](https://intl.cloud.tencent.com/document/product/1047/36211).

You can follow the directions below to establish your own live marketing platform:

## Directions
### Step 1: use the IM AVChatRoom feature to create live chat rooms

Chat rooms are an important part of live-streaming. In a chat room, users can send messages to and receive messages from other members in the chat room.

1. Log in to the [IM console](https://console.cloud.tencent.com/im) and then click **+Add App**
2. In the **Create App** dialog box, enter an app name and click **OK**.
    After the app is created, you can view the status, service version, SDKAppID, creation time, and expiration time of the new app on the overview page of the console.
  >? The default service version of a new app is Trial Edition. You can [upgrade](https://intl.cloud.tencent.com/document/product/1047/34577) it to Pro Edition or Ultimate Edition as needed.
  > A Tencent Cloud account can be used to create a maximum of 100 IM apps. If you have already created 100 IM apps, you can create a new app after [disabling and deleting](https://intl.cloud.tencent.com/document/product/1047/34540) an unwanted app. **After an app is deleted, all the data and services associated with the SDKAppID are irrecoverable, so proceed with caution.**
  >
  ![](https://main.qcloudimg.com/raw/2753962b67754a9ebb2a2a5b8042f2ef.png)
3. Click the target app card and select **Group Management** in the left sidebar.
4. On the **Group Management** page, click **Add Group**.
5. Configure the following parameters in the pop-up dialog box:
 - Group name: enter the name of the new group. This is a required parameter, and its length cannot exceed 30 bytes.
 - Group owner ID: enter the group owner ID. This parameter is optional. The value must be the name of a registered user.
 - Group type: set the group type. Based on [Group Types](https://intl.cloud.tencent.com/document/product/1047/33529), **we recommend that you set the group type to	
AVChatRoom**.
3. Click **OK** to save the configuration.
 After the group is created, you can view the group ID, group name, group owner, type, and creation time of the new group in the group list.


### Step 2: use custom messages to implement notifications of likes, gifts, purchases, and other behavior

In live-streaming scenarios, to make a group lively, it is necessary to send large numbers of real-time feedback messages to group members. For example, when someone gives a gift to the host, all group members need to be notified, and the gift needs to be displayed with a flashy special effect. Gift notification messages for all members can be implemented by IM custom messages, and custom messages can carry extra information. When a gift is sent, the gift information and user information can be carried in the message. Likewise, custom messages can be used to implement notifications of user likes, commodity purchases, following the host, and other behavior. Custom messages differ from text messages and rich text messages. Custom messages can be viewed as a special type of message used to transmit special signals.

The following is sample code for custom messages sent in the SDK:

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

### Step 3: use custom group fields to implement notifications for new commodity launches in the live room and live-streaming status changes

In live marketing scenarios, when the host recommends a product, the relevant product must be immediately displayed in the commodity spot in the lower section of the screen, and all users in the live room need to be notified of the new commodity launch. Commodity launch messages are usually triggered by the Assistant.
From a technical perspective, two solutions are available to allow the Assistant to trigger commodity launch messages:
- The Assistant sends custom messages.
 - This solution requires the Assistant to be in the live-streaming group.
 - When there are too many group messages, the IM backend returns messages based on message priority. The priority of custom messages is low, so users may not receive commodity updates promptly.
- The Assistant modifies the group profile.
 - In this solution, the Assistant can be a member (for example, an admin) of the current live-streaming group or a non-member user.
 - Besides the default group profile fields for which there are already existing definitions, IM also provides custom group fields. You can specify the meanings of custom fields and the corresponding read-write permissions.

Therefore, we recommend that you adopt the **admin modifying custom group fields** solution to implement commodity launch notifications. The specific directions are as follows:

#### Adding custom group fields

1. Log in to the [Instant Messaging console](https://console.cloud.tencent.com/im), click the target IM app card, and select **Feature Configuration** -> **Custom Group Fields** in the left sidebar.
2. On the **Custom Group Fields** page, click **Add Custom Group Fields**.
3. In the pop-up dialog box, enter the field name and set the group type and corresponding read-write permissions.
  >?
  >- The field name can only consist of letters, digits, and underscores (\_) and cannot start with a digit. The length cannot exceed 16 characters.
  >- Custom group field names cannot be the same as custom group member field names.
  >
 ![](https://main.qcloudimg.com/raw/8fe4aa2bb4efdce9027affa2a0a4831f.png)
4. Check **I know that custom fields and group types cannot be deleted after being added, and that only the read-write permissions of the group type can be modified** and click **OK** to save the configuration.
 Custom group fields take effect about 10 minutes after configuration.

#### Using custom group fields

The Assistant, in the role of group admin, calls the [RESTful API for modifying basic group profiles](https://intl.cloud.tencent.com/zh/document/product/1047/1620) to update the corresponding custom group fields. This allows it to implement notifications for new commodity launches in the live room and live-streaming status changes.


### Step 4: use the callback after group messages to implement user level changes

In live-streaming scenarios, in addition to profile photos and nicknames, users often have level information. For example, after a user sends messages or gifts in a live room, the user’s level should increase. You can implement the relevant features via callbacks. Service providers can use callbacks to obtain messages related to users’ groups, relationship chains, one-to-one chat messages, online status changes, and other status changes and then change their levels based on their sending of ordinary text messages and gift messages in the group chat.
For relevant the callback operations, see [Callback Configuration](https://intl.cloud.tencent.com/document/product/1047/34520) and [Third-Party Callback Overview](https://intl.cloud.tencent.com/document/product/1047/34354).

### Step 5: use content filtering to block sensitive words

Content filtering is always a necessary capability in fields such as live-streaming, social media, and consultation. In live-streaming scenarios, serious consequences can result from content that contains sensitive information. IM provides a sensitive word filtering feature that, by default, supports the filtering of sensitive words such as the names of certain national leaders. You can also purchase the value-added [content filtering service](https://intl.cloud.tencent.com/document/product/1047/34350).


### Step 6: use LVB to generate a push address and start live-streaming
LVB facilitates the growth of e-commerce platforms by enabling merchants to display items in greater detail and assisting consumers in making informed decisions, ultimately reducing marketing costs and boosting sales.
Before you start live-streaming, you need to generate a push address via the [address generator](https://intl.cloud.tencent.com/document/product/267/31084) and then perform [live-streaming push](https://intl.cloud.tencent.com/document/product/267/31558).

