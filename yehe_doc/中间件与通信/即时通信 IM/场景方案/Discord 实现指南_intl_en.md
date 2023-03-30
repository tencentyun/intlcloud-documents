## Discord Overview

Discord is a free online real-time messaging app and digital distribution platform designed for the communities. It allows users in the gaming, education, and business fields to communicate with each other through messages, pictures, videos, and audio in the software's chat channel.

## Discord Concepts

### Server

In Discord, there is a kind of group chat, which is different from the normal communication software groups, called servers (similar to communities), and server owners can create their own communities in the servers.

### Channel

In servers, you can create chat channels, including the voice and text channels. The voice channel can be used for game broadcasting, chatting, etc. Channels can be set to integrate various permissions with identity groups, making the Discord community system more diverse.

### Threads

Users can discuss specific topics in threads.

## Preparations

### Creating Tencent Cloud Chat apps

This tutorial is based on Tencent Cloud Chat. Therefore, you need to create an app in the [Tencent Cloud Chat console](https://console.cloud.tencent.com/im). See the figure below. 

After the app is created successfully, you can view the basic information of the app on the [basic information page](https://console.cloud.tencent.com/im/detail) of the app in the Chat console.

### Understanding related configuration and capabilities

To use Tencent Cloud Chat to implement Discord features, you need to understand the basic concepts related to Tencent Cloud Chat in advance and some proper terms that will be mentioned later in this tutorial, including but not limited to the following:

- SDKAppID: Tencent Cloud Chat assigns an SDKAppID for each app. The SDKAppID of an app can be viewed on the app details page after the app is created in the console and used when initializing the Chat SDK and calculating user login tickets. For more information, see UI SDK [Initialization](https://intl.cloud.tencent.com/document/product/1047/47968) and [Login](https://intl.cloud.tencent.com/document/product/1047/47971).
- Key: The key of an app can be viewed on the Tencent Cloud Chat console app details page and used to calculate SDK login tickets for users.
- User account: Only users with Tencent Cloud Chat accounts can log in to Tencent Cloud Chat. When a user successfully [logs in](https://intl.cloud.tencent.com/document/product/1047/47971) via a client SDK, the Chat backend automatically creates a Chat account for the user. In addition, you can use the server API that Chat provides to [import the user to the user system of Chat](https://intl.cloud.tencent.com/document/product/1047/34953).
- Group: So far, Chat offers [five types of groups](https://intl.cloud.tencent.com/document/product/1047/33529) for different scenarios, where users can send and receive messages.
- Webhook configuration: You can proactively integrate the client and server APIs provided by Chat, and Chat will automatically return necessary information to your server when specific business logic is triggered. What you need to do is to simply complete related configuration in the [Webhook Configuration](https://console.cloud.tencent.com/im/callback-setting) module of the Chat console. Chat provides various webhook configuration and ensures high reliability for webhook events. You can use webhooks to implement various custom requirements.
- Custom field: By default, Tencent Cloud Chat provides developers with fields that meet most of their needs. It also provides the following custom fields for each module to meet users' needs for extended fields:
    - [Custom user fields](https://console.cloud.tencent.com/im/user-data)
    - [Custom friend fields](https://console.cloud.tencent.com/im/friends-diy-vars)
    - [Custom group fields](https://console.cloud.tencent.com/im/qun-setting)
    - [Custom group member fields](https://console.cloud.tencent.com/im/qun-setting)
  
  >?To use custom fields, you can configure them in the console and then read/write them via SDK/API.

### Integrating client and server SDKs

To implement Discord related features, you need to integrate Tencent Cloud Chat SDK. Chat provides diverse and easy-to-use SDKs and server APIs. Messages are synced across clients if you log in to the app with the same SDKAppID. Select an appropriate SDK according to your business requirement scenario and technology stack.

## Discord Features 

As the figure above shows, Discord features include servers, channels, and threads. Different servers are used for different content. For example, we have the Honor of Kings server and Game for Peace server. You can create different types of channel in a server, such as the text channel, voice channel, and notice channel. Users communicate with each other in channels. If they have more ideas on a certain topic, they can create a thread for further discussion. The following will introduce how to implement these key Discord features through Tencent Cloud Chat one by one.

>?**For code demos, we use the Android client (Java SDK) as an example. For the calling of APIs of other SDK editions, see [Integration Solution (No UI)](https://intl.cloud.tencent.com/document/product/1047/34306).**

### Server

#### Creating a server 

Analysis found the following characteristics with the Discord server list:

1. Servers can have a huge number of users.
2. Users don't actually communicate with each other in servers. Instead, they chat only in channels or threads in a server.
3. Historical chat messages in servers need to be stored on roaming servers.
4. Users have free access to servers.
5. Channels can be created in servers.

Though Chat provides five types of groups, only [community groups](https://intl.cloud.tencent.com/document/product/1047/33529) meet the characteristics of Discord servers. A Chat community group allows users to join and leave freely, supports up to 100,000 members, and stores the message history. To join the group, a user needs to search for the group ID and send an application, and the application does not need to be approved by an admin before the user can join the group.

You can use the `createGroup` API to create a server (group). Note that the group type should be Community and [setSupportTopic](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupInfo.html#af97a85fc91302dbbdf0f6c0a0a022ccd) be `true` so that channels can be created in the server. The following is sample code:

```java
V2TIMGroupInfo  groupinfo = new V2TIMGroupInfo();
groupinfo.setGroupName("Test server");
groupinfo.setSupportTopic(true);
// Initial group members
List<V2TIMCreateGroupMemberInfo> memberList = new LinkedList<V2TIMCreateGroupMemberInfo>();
// Other settings, such as the server profile photo
V2TIMManager.getGroupManager().createGroup(groupinfo, memberList, new V2TIMValueCallback<String>() {
            @Override
            public void onError(int i, String s) {
                // Creation failed
            }

            @Override
            public void onSuccess(String s) {
            	// The server is created successfully, and the server ID is returned.
            }
});
```

After the API is called successfully, the server ID will be returned in the `onSuccess` callback, which will be used later when you create a channel in the server.

>!You can also use the [server creation API](https://intl.cloud.tencent.com/document/product/1047/34895) provided by Chat. Key parameters are as follows:
>
>```json
>{
>"Type": "Community", // Group type (required)
>"Name": "TestCommunityGroup", // Group name (required)
>"SupportTopic": 1// Whether the topic option is supported. Valid values: `1`: yes; `0`: no.
>}
```

###### Server list

There is a list of servers that the current user has joined on the far left of Discord. For the community scenario, Tencent Cloud Chat provides a dedicated API for querying the server list.

```java
V2TIMManager.getGroupManager().getJoinedCommunityList(new V2TIMValueCallback<List<V2TIMGroupInfo>>() {
            @Override
            public void onSuccess(List<V2TIMGroupInfo> v2TIMGroupInfos) {
                // The server list is got successfully, and the basic information of the server list is provided in the returned `List<V2TIMGroupInfo>`.
            }

            @Override
            public void onError(int i, String s) {
              // Failed to get the service list.
            }
});
```

The returned [V2TIMGroupInfo](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupInfo.html) provides the basic server information. However, the returned server information does not include information such as the unread message count and custom status. To achieve the same effect as that on Discord, we need to use other APIs provided by Chat to implement the unread message count for the server list, which will be discussed later in the document.

#### Server categories

When a server is created, a default category will be created for it. After the server is created, you can create a new category. In Tencent Cloud Chat, a server is essentially a community. Therefore, we can set a custom field for a community group to implement the server type feature. To use a custom group field, perform the steps below:

1. Enable the custom field `key` in the console.
2. User the client SDK or server API to read/write the custom field. 

Set the custom group field by using the [server API](https://intl.cloud.tencent.com/document/product/1047/34962) and [client SDK](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#ad4ceef92975fa00c4a5dddc8f7e1edcf).

>!The community group feature is only available in the Ultimate edition. Before setting a custom field for the community group, you need to purchase the Ultimate edition.

#### Display of the unread message count and custom status for the server

![image-20221205031412051](https://markdown-1252238885.cos.ap-guangzhou.myqcloud.com/2022-12-04-191412.png)

![image-20221205031429070](https://markdown-1252238885.cos.ap-guangzhou.myqcloud.com/2022-12-04-191429.png)

As mentioned previously, the API for getting the list of joined servers does not return information such as the unread message count and server status. It should be noted that we not only need to obtain this data, but also need to listen to the change of this data to update the client UI in time. Since the server is implemented by a Chat community group, and a community group does not generate conversations in Chat, we need to count the sum of unread messages in all public and private channel conversations. We can use the [getUnreadCount](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMTopicInfo.html#ac2e3266d20b348145d75079020ac50c7) API of [V2TIMTopicInfo](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMTopicInfo.html) to get the unread message count of public channels and use the [getConversation](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#a619aaff2bb5664e094d2341819b95096) API to get the unread message count of private channels (because private channels are implemented by work groups).

```java
// Public channels
List<String> conversationIDList = new LinkedList();
conversationIDList.add("GROUP_$GROUPID");
V2TIMManager.getConversationManager().getConversationList(conversationIDList, new V2TIMValueCallback<List<V2TIMConversation>>() {
            @Override
            public void onError(int i, String s) {
                // Failed to get the conversation information of the server
            }

            @Override
            public void onSuccess(V2TIMConversationList List<V2TIMConversation>) {
               // Got the conversation information of the server successfully
            }
});
// Private channels
V2TIMManager.getGroupManager().getTopicInfoList(groupID, topicIDList, new V2TIMValueCallback<List<V2TIMTopicInfoResult>>() {
                @Override
                public void onSuccess(List<V2TIMTopicInfoResult> v2TIMTopicInfoResults) {
                    
                }

                @Override
                public void onError(int i, String s) {
                }
});
```

To implement the custom status feature for servers, we can use the [setConversationCustomData](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#ac11ca7227145e3f359f6a3473ed600a5) API to set custom server conversation data.

```java
List<String> conversationIDList = new LinkedList();
String customData = "Busy"
V2TIMManager.getConversationManager().setConversationCustomData(conversationIDList, customData, new V2TIMValueCallback<List<V2TIMConversationOperationResult>>() {
            @Override
            public void onSuccess(List<V2TIMConversationOperationResult> v2TIMConversationOperationResults) {
                // The custom group conversation data is set successfully
            }

            @Override
            public void onError(int i, String s) {
                // Failed to set the custom group conversation data
            }
});
```

When data related to the server conversation changes, the client needs to try to update the UI display. For listening for server conversation changes, Chat provides a corresponding event listener function [addConversationListener](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#a806534684e5d4d01b94126cd1397fee4). This callback function will be triggered in the following cases:

1. Server messages are added, deleted, or modified.
2. The unread count of server messages changes.
3. The custom server information is modified.
4. The server is pinned to the top.
5. The message receiving configuration of the server is modified.
6. The server mark is modified.
7. The server group is modified.
8. ...

```java
V2TIMConversationListener conversationLister = new V2TIMConversationListener() {
            @Override
            public void onSyncServerStart() {
            }

            @Override
            public void onSyncServerFinish() {
            }

            @Override
            public void onSyncServerFailed() {
            }

            @Override
            public void onNewConversation(List<V2TIMConversation> conversationList) {
            }

            @Override
            public void onConversationChanged(List<V2TIMConversation> conversationList) {
            }
            @Override
            public void onTotalUnreadMessageCountChanged(long totalUnreadCount) {
            }

            @Override
            public void onConversationGroupCreated(String groupName, List<V2TIMConversation> conversationList) {
            }

            @Override
            public void onConversationGroupDeleted(String groupName) {
            }

            @Override
            public void onConversationGroupNameChanged(String oldName, String newName) {
            }

            @Override
            public void onConversationsAddedToGroup(String groupName, List<V2TIMConversation> conversationList) {、
            }

            @Override
            public void onConversationsDeletedFromGroup(String groupName, List<V2TIMConversation> conversationList) {
            }
}
V2TIMManager.getConversationManager().addConversationListener(conversationLister);
```

To sum up, we can use the `getJoinedCommunityList` and `getConversationList` APIs and the `addConversationListener` callback to implement the Discord feature of displaying the server list.

### Channel

Multiple channels can be created in a server. As the figure below shows, four channels are created under the server, and the four channels are placed in two categories. 

Users can invite others to join a channel and modify the basic settings of the channel. Users do most of their chatting within channels, so channel capabilities are of paramount importance in Discord. Channel capabilities in Discord correspond to topic capabilities in Tencent Cloud Chat. Chat's community groups provide the capability to create topics in groups.

#### Default channels

When a server is created, Discord will create four default channels for the server. Tencent Cloud Chat can also implement such a feature. The process is as follows:

1. Notify the business server that the server is created successfully via the [After a group is created](https://console.cloud.tencent.com/im/callback-setting) webhook.
2. The business side determines whether the created group is a community group, so as not to affect the business related to other groups.
3. [Create a topic on the server](https://intl.cloud.tencent.com/document/product/1047/49471) based on the server attributes.

Parameters for creating a topic on the server are as follows:

```json
{
    "GroupId": "@TGS#_@TGS#cQVLVHIM62CJ", // Group ID of the topic, which is required
    "TopicId": "@TGS#_@TGS#cQVLVHIM62CJ@TOPIC#_TestTopic", // Custom topic ID, which is optional
    "TopicName": "TestTopic", // Topic name, which is required
    "From_Account": "1400187352", // Member creating the topic
    "CustomString": "This is a custom string",// Custom string
    "FaceUrl": "http://this.is.face.url", // (Optional) Topic profile photo URL
    "Notification": "This is topic Notification", // (Optional) Topic notice
    "Introduction": "This is topic Introduction" // (Optional) Topic introduction
}
```

#### Creating a channel

On a Discord client, users can create channels under different channel categories, as shown in the figure below: 

Creating a channel in Discord is equivalent to creating a topic in a community group in Chat. When creating a topic in Chat, you can set the category and basic information of the topic. 

You can use the [createTopicInCommunity](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a52eed1b07ad64a3aa3d3561d8cd147f0) API to implement related features.

```java
String groupID = "Server ID"
V2TIMTopicInfo info = new V2TIMTopicInfo();
info.setCustomString("{'categray':'Game','type':'text'}") // Set the channel category and type
// Set the basic information for `V2TIMTopicInfo`
V2TIMManager.getGroupManager().createTopicInCommunity(groupID, info, new V2TIMValueCallback<String>() {
            @Override
            public void onSuccess(String s) {
                // Channel created successfully
            }

            @Override
            public void onError(int i, String s) {
                // Failed to create the channel
            }
});
```

When creating a channel, you can call the [V2TIMTopicInfo](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMTopicInfo.html) method to set the channel information and call the [setCustomString](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMTopicInfo.html#aad0cc8249c21c5ccae385fdfb8ba32ea) API to set the channel category and type. 

When creating a channel, you can specify whether it is a private channel. A private channel is different from a general channel:

1. Users do not join a private channel after they join the server.
2. Users can join a private channel only when they are invited by the server admin.

Therefore, we can use a work group to implement the private channel feature. However, the information about the private channels bound with a server needs to be stored on the business side.

#### Channel types

When creating a channel in Discord, you can set the channel type to voice or text. A text channel allows chatting based on text, emojis, and images, while a voice channel allows audio/video chatting. Note that a user can be in only one voice channel at a time. To join a new voice channel, the user needs to leave the currently joined voice channel. 

Pay attention to the following:

1. When creating a channel, you need to set the channel type. Find the setting method in the channel creation section.
2. When a user joins a voice channel, the system needs to determine whether the user is already in another voice channel.
3. A user can join only one voice channel within an application.
4. Tencent Cloud Chat currently does not provide an API to query whether a user is in a voice channel and in which voice channel. This part of data needs to be maintained on the business side.

Regarding the last point above, developers can use the group joining and leaving callbacks provided by Tencent Cloud Chat to maintain the voice channel statuses of users and store the statuses on the business side. Note that the callbacks provided by Tencent Cloud Chat may have delays, which means that after a user leaves one voice channel, the user may not be able to join another voice channel for a short period of time. Therefore, to address this issue, we can also use the client to report the user's voice channel joining or leaving status to the business server in real time.

#### Inviting a user to a channel

There are three ways a user can join a channel:

1. Be invited to join a server by another user. When a user joins a server, the user joins all the server's public channels.
2. Search for a server and then join the server.
3. Be invited by the server admin to join a private channel.

According to the characteristics of the community, users only need to join a server to join public channels.

1. Supports joining a server by accurate group ID search.
2. Supports joining a server via an invitation.
3. Supports proactively applying for joining a server, and approval is not required.



#### Setting a channel

You can mute or unmute a channel and configure notifications for a channel. The corresponding APIs are [setAllMute](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMTopicInfo.html#a13fbe06ce357215cfd7053954552030b) and [setGroupReceiveMessageOpt](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a2735427ac22485626aea278a9d465b3e) respectively.

```java
// Set the basic channel information
V2TIMManager.getGroupManager().setTopicInfo(topicInfo, new V2TIMCallback() {
    @Override
    public void onSuccess() {
        // Configured successfully
    }

    @Override
    public void onError(int i, String s) {
        // Failed to configure
    }
});
```

```java
// Set the message receiving option for the channel
String groupID = "topicid"
int opt = 0; 
V2TIMManager.getMessageManager().setGroupReceiveMessageOpt(groupID, opt, new V2TIMCallback() {
    @Override
    public void onSuccess() {
        
    }

    @Override
    public void onError(int i, String s) {
        
    }
});
```

#### Channel message list

You can use the [getHistoryMessageList](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a97fe2d6a7bab8f45b758f84df48c0b12) API to get the historical messages of a channel.

```java
final V2TIMMessageListGetOption option = new V2TIMMessageListGetOption();
option.setGroupID("Channel ID");
option.setCount(20);
// Other settings
V2TIMManager.getMessageManager().getHistoryMessageList(option, new V2TIMValueCallback<List<V2TIMMessage>>() {
    @Override
    public void onSuccess(List<V2TIMMessage> v2TIMMessages) {
        // The historical messages of the channel are got successfully
    }

    @Override
    public void onError(int code, String desc) {
        // Failed to get the historical messages of the channel
    }
});
```

#### Unread message count of a channel

The unread message count of a channel is different from that of a server. The unread message count of a server is in the conversation information, while the unread message count of a channel is in the channel basic information. We can use the group callback [onTopicInfoChanged](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupListener.html#a29285e4e127337e299bd2b695a1afdeb) provided by Tencent Cloud Chat to get the unread message count in real time.

```java
String groupID = "Server ID";
List< String > topicIDList= new LinkedList(); // List of channel messages
V2TIMManager.getGroupManager().getTopicInfoList(groupID, topicIDList, new V2TIMValueCallback<List<V2TIMTopicInfoResult>>() {
    @Override
    public void onSuccess(List<V2TIMTopicInfoResult> v2TIMTopicInfoResults) {
        // Get the channel information, such as the channel ID, name, and unread message count
    }

    @Override
    public void onError(int i, String s) {
        
    }
});
```

#### Channel member list

A user that joins a server will join all public channels under the server by default. Therefore, to get the public channel member list, you only need to get the group member list of a server. The following shows how to get the public channel member list:

```java
String groupID = "Server ID";
int filter = 0; // Group member role: admin, ordinary members...
long nextSeq = 0;// Pagination parameter
V2TIMManager.getGroupManager().getGroupMemberList(groupID, filter, nextSeq , new V2TIMValueCallback<V2TIMGroupMemberInfoResult>() {
    @Override
    public void onError(int i, String s) {
        CommonUtil.returnError(result,i,s);
    }

    @Override
    public void onSuccess(V2TIMGroupMemberInfoResult v2TIMGroupMemberInfoResult) {
        
    }
});
```

To get the member list of a private channel, you can also call the [getGroupMemberList](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a69fc0831aacaa0585c1855f4c91320be) API but pass in the group ID of the private channel.

### Threads

A thread is a discussion group for a specific topic in a channel. Users can browse messages on a specific topic within a thread, and the digest of the thread can also be viewed in the message list of the channel. A thread is also considered a group in Tencent Cloud Chat.

#### Creating a thread

A thread can be created separately or by binding with a message in a channel. You can use the `createGroup` API provided by Tencent Cloud Chat to create a thread. Pay attention to the following:

1. When a thread is created, all members of the current server are in the thread by default.
2. Members who join the server after the thread is created will also be added to the thread.
3. Users who later join the thread can view the thread's chat history since its creation.

To sum up, when a thread/group is created, the server's group members are added to the thread, and when a user joins the server, we need to add the user to all the threads of the server in the user's group joining callback. It's best to implement these two steps on the business server side, using the following APIs:

1. [Querying members in a group](https://intl.cloud.tencent.com/document/product/1047/34948)
2. [Creating a group and setting group members](https://intl.cloud.tencent.com/document/product/1047/34895)
3. [Inviting users to join a group](https://intl.cloud.tencent.com/document/product/1047/34921)

The server-side webhook is the webhook [After a User Joins a Group](https://intl.cloud.tencent.com/document/product/1047/34372).

#### Number of threads

In the channel list, you can get the list of threads in the channel. Therefore, we need to set up the many-to-one relationships between threads and the server. If threads have historical messages, we also need to set up the one-to-one relationships between the threads and messages. Tencent Cloud Chat currently does not provide capabilities to set up these relationships, so these relationships need to be maintained on the business side. We can use the HTTP API provided by the business side to get the number of threads and the thread list and send online messages to update the thread list in real time.

#### Thread digests

When a user creates a thread for a message, the user can view the following message digest information in the message list:

1. Number of messages in the thread
2. `lastMessage` related information in the thread
3. Other information that needs to be displayed in the message list in real time

To implement the message digest capability of threads, we need to use the group message sending callback and message editing capabilities. After a user sends a message in a thread, the Chat service triggers the message sending callback and synchronizes related information to the business side. Then the business counts the number of messages of the thread, maintains the `lastMessage` information, and stores the information to the message via the message editing API.

### Messages

#### Message feedback

Message feedback is the extension of a message for users, as shown in the figure below: 

Because all types of messages support editing and feedback and require community group support, we recommend that the data be stored in the `cloudCustomData` field. The following is the detailed data storage format for your reference:

```json
{
  "reaction": {
    "simle":["user1","user2"]
  }
}
```

```java
V2TIMManager.getMessageManager().modifyMessage(modifiedMessage, new V2TIMCompleteCallback<V2TIMMessage>() {
    @Override
    public void onComplete(int i, String s, V2TIMMessage v2TIMMessage) {
        // Message modification completed
    }
});
```

#### Message editing

Message editing works the same as message feedback, with only a few differences in the custom data configured. To enable all messages to support editing, we recommend that the data be edited in the `cloudCustomData` field. The data format is as follows:

```json
{
  "isEdited": true
}
```

```java
V2TIMManager.getMessageManager().modifyMessage(modifiedMessage, new V2TIMCompleteCallback<V2TIMMessage>() {
    @Override
    public void onComplete(int i, String s, V2TIMMessage v2TIMMessage) {
        // Message editing completed
    }
});
```

#### Message starring  

Message starring is to star a message in a group chat so that other users can see the starred message. Since community groups do not support group attributes, we use custom messages to implement the message starring capability.

To use custom group messages, we need to make configuration as shown in the figure below in the [Tencent Cloud Chat console](https://console.cloud.tencent.com/im/qun-setting) first:

Then make the following configuration:

```java
V2TIMGroupInfo info =  new V2TIMGroupInfo();
info.setCustomInfo("pin data");
V2TIMManager.getGroupManager().setGroupInfo(info, new V2TIMCallback() {
    @Override
    public void onError(int i, String s) {
        // Failed to configure
    }

    @Override
    public void onSuccess() {
        // Configured successfully
    }
});
```

Then, group members can receive the [onMemberInfoChanged](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupListener.html#a4ac777faad07e32408ae7ef5e2e3fc86) event, and offline users can also get the starred message content via the group profile:

```java
List< String > groupIDList = new LinkedList();
V2TIMManager.getGroupManager().getGroupsInfo(groupIDList, new V2TIMValueCallback<List<V2TIMGroupInfoResult>>() {
    @Override
    public void onError(int i, String s) {
        
    }

    @Override
    public void onSuccess(List<V2TIMGroupInfoResult> v2TIMGroupInfoResults) {
        
    }
});
```

Note that custom fields currently can be configured only on the server, not on channels.

#### "Typing..." status

When a friend is typing, users on other clients can see the user's "typing..." status, as shown in the figure above. We can use the online message feature of Tencent Cloud Chat to implement this capability. The "typing..." status message:

1. Can be received only by online users.
2. Will not be stored on a roaming server.

In addition, we've made the following optimizations for better performance:

- The sending of the "typing..." status message will only be triggered if two users send messages to each other within 20s.
- The same text message does not trigger online message sending multiple times.

### Private messages

Private messages are messages that Discord users send to each other, regardless of whether they are friends or not.

- To send a private message to another user that is not your friend, you need to know the user's userID and disable the [relationship chain check for message sending option](https://console.cloud.tencent.com/im/login-message) in the Tencent Cloud Chat console. Otherwise, message sending will fail.
- Alternatively, you can call the [addFriend](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a19d0f22aaea285e8cee85a5dd6ed9208) API to add that user as your friend and use the [getFriendList](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#ae478de55db21d42b72a6c5a6a5d16624) API to get your contacts.

The relevant code is as follows:

```java
// Add a friend
V2TIMManager.getFriendshipManager().addFriend(info, new V2TIMValueCallback<V2TIMFriendOperationResult>() {
            @Override
            public void onError(int i, String s) {
                // Failed to add the friend
            }

            @Override
            public void onSuccess(V2TIMFriendOperationResult v2TIMFriendOperationResult) {
               // Friend added successfully
            }
});
```

```java
// Obtain the contacts
V2TIMManager.getFriendshipManager().getFriendList(new V2TIMValueCallback<List<V2TIMFriendInfo>>() {
            @Override
            public void onError(int i, String s) {
               // Failed to obtain the contacts
            }

            @Override
            public void onSuccess(List<V2TIMFriendInfo> v2TIMFriendInfos) {
               // The contacts obtained successfully
            }
});
```

### Personal center

#### Online status 
The online status capabilities of Discord's user panel can be implemented by the following online status APIs provided by Tencent Cloud Chat:

- [setSelfStatus](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a7520045679f1493c890f2b3b5eee7b84): API for setting one's own custom online status. Users' online/offline statuses are set by Tencent Cloud Chat and cannot be modified by developers.
- [getUserStatus](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a2428c7f87859dd85bed1730ad8d3b92a): API for getting the online statuses of friends.
- [onUserStatusChanged](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMSDKListener.html#a94251d1971d7b6692b3278ed0d42b73e): API for listening for the online status changes of friends.

The relevant code is as follows:

```java
// Set your own online status
V2TIMUserStatus customStatus = new V2TIMUserStatus();
V2TIMManager.getInstance().setSelfStatus(customStatus, new V2TIMCallback() {
    @Override
    public void onSuccess() {
        
    }

    @Override
    public void onError(int i, String s) {
        
    }
});
```

```java
// Get the online statuses of friends
List<String> userIDList = new LinkerList();
V2TIMManager.getInstance().getUserStatus(userIDList, new V2TIMValueCallback<List<V2TIMUserStatus>>() {
    @Override
    public void onSuccess(List<V2TIMUserStatus> v2TIMUserStatuses) {
       
    }

    @Override
    public void onError(int i, String s) {
        
    }
});
```

#### Personal information

Personal information related features can be implemented by the following relationship chain related APIs provided by Tencent Cloud Chat:

- [getUsersInfo](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a7ca8c0f71a9875021fc35dfcaff68d1e): API for getting user profiles
- [setSelfInfo](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#af004ab2f1d1458de354883f1995b678a): API for setting the user's profile

```java
// Set the user's profile
final V2TIMUserFullInfo userFullInfo = new V2TIMUserFullInfo();
V2TIMManager.getInstance().setSelfInfo(userFullInfo, new V2TIMCallback() {
    @Override
    public void onError(int i, String s) {
        
    }

    @Override
    public void onSuccess() {
        
    }
});
```

```java
// Get user profiles
List<String> userIDList = new LinkedList();
V2TIMManager.getInstance().getUsersInfo(userIDList, new V2TIMValueCallback<List<V2TIMUserFullInfo>>() {
    @Override
    public void onError(int i, String s) {
        
    }

    @Override
    public void onSuccess(List<V2TIMUserFullInfo> v2TIMUserFullInfos) {
        
    }
});
```

### Others

#### Search

Discord provides the following search capabilities: 

Tencent Cloud Chat provides rich search capabilities, including:

- [searchLocalMessages](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a9364c8a0c6a0899b17c0a479b8ca848a): API for searching for messages
- [searchGroups](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a94a72082b7e2682942f35196a7e28023): API for searching for groups
- [searchGroupMembers](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a493fb73258019961f3ca8934ff625b0a): API for searching for group members
- [searchFriends](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a3e657c9ec5d68a4c423a64d71f5f9c6e): API for searching for friends

For how to use the APIs, see the [official documentation](https://intl.cloud.tencent.com/document/product/1047/48134).

#### Offline push

Tencent Cloud Chat's online messages cannot reach offline users. To address this issue, we need to integrate the offline push capabilities provided by device vendors to Tencent Cloud Chat. For more information, see [Offline Push](https://intl.cloud.tencent.com/document/product/1047/39156).

#### Sensitive word verification

When you send information and configuration in Discord, the content needs to be filtered. Tencent Cloud Chat also provides a similar scheme to help users use Chat with compliance.
