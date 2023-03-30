>- Instant messaging is a common requirement of games, and instant chat has become an essential feature in multiplayer games. The game platform itself involves a variety of group types, custom message types (such as in-game props gifting and trading), global access, and other complex requirements. This document sorts out the implementation methods of common requirements in the process of building in-game chat, along with possible problems and considerations, helping developers quickly understand the business and implement their requirements.
>  ![](https://qcloudimg.tencent-cloud.cn/raw/41bda125b2276c6d70bfa8de480e8748.jfif)
>
>  ## Preparations
>
>  ### Calculating the UserSig with a key
>
>  In the Chat account system, the password required by a user login is calculated by the server with a key provided by Chat. For more information, see [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385). In the development phase, to avoid holding back development on the client, you can also calculate the `UserSig` in the [console](https://console.cloud.tencent.com/im/tool-usersig) as shown below:
>
>  ![](https://qcloudimg.tencent-cloud.cn/raw/3ebfcc9b831fac31ad9b8b722bb7dc50.png)
>
>  ### Configuring an admin account
>
>  Managing in-game instant messaging may require admins to send email announcements to games, manage temporary team-up messages, and so on, which can be done through [Chat server APIs](https://intl.cloud.tencent.com/document/product/1047/34621). To call these APIs, you need to [create a Chat admin account](https://console.cloud.tencent.com/im/account-management). By default, Chat provides an account with the `UserID` of `administrator`. You can also create multiple admin accounts as needed. Note that you can create up to five admin accounts.
>
>  ### Configuring the callback address and enabling the callback
>
>  To implement in-game team-up and other requirements, you use the Webhook event, where the Chat backend calls the business backend in certain scenarios. You only need to provide an HTTP API and configure it in the [**Webhook Configuration**](https://console.cloud.tencent.com/im/callback-setting) module in the console as shown below:
>
>  ![](https://staticintl.cloudcachetci.com/yehe/backend-news/NDSF820_1.png)
>
>  ### Integrating the client SDK
>
>  After completing the preparations, you need to integrate the Chat client SDK into your project. You can select different integration options as needed. For detailed directions, see [TUIKit Introduction](https://intl.cloud.tencent.com/document/product/1047/34547).
>
>  The following describes common Chat features to be integrated into games and provides best practices with implementation code.
>
>  ## Game Chat Room Feature Development Guide
>
>  ### User profile
>
>  #### Common user profile
>  Common user profiles stored in gaming business can be divided into basic information profiles and other information profiles.
>
>  | Basic Information                                            | Other Information                   |
>  | ------------------------------------------------------------ | ----------------------------------- |
>  | Username, gender, date of birth, level, role, mobile number, etc. | Other information required by games |
>
>  #### Profile storage
>  The gaming business has a large number of users and it is difficult to store huge amounts of user data. Tencent Cloud Chat offers a complete set of profile solutions through its user profile hosting capabilities. The following compares storing user profiles to Tencent Cloud Chat and to the business background.
>
>  | Item               | Chat                                                         | Business Background                                          |
>  | ------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
>  | Storage capacity   | Supports automatic scaling                                   | Supports limited capacity and difficult to scale             |
>  | User profiles      | Supports standard and custom fields, with restrictions on the lengths and names of the fields | Customizable, more flexible                                  |
>  | Profile read/write | Supports easy-to-use service APIs and guidelines             | Requires development on your own                             |
>  | APIs               | Requires the API call frequency to be 200 times/second or less | Allows you to develop API call and other capabilities as needed |
>  | Security           | Supports remote disaster recovery and cross-region deployment | Requires maintenance on your own                             |
>
>  In addition to profile storage and read/write capabilities, Chat has the following advantages thanks to its user profile hosting service:
>  1. Chat provides remote disaster recovery, cross-region deployment, and auto scaling capabilities. In this way, you are completely free from complex processing flows, such as server downtime, multi-copy primary-secondary replication, and capacity scaling.
>  2. Chat provides the business processing flows commonly used in the industry, with which you do not have to worry about user profile business logic.
>  3. Chat provides professional operation processes and teams, ensuring 99.99% service quality annually and helping you offer services known for their stability.
>  4. Chat provides easy-to-use service APIs and easy-to-access guidelines, with premium services throughout the whole process.
>
>  #### Chat user profile storage methods
>  The Chat storage scheme includes user profile storage and read/write capabilities. The following describes how Chat stores user profile, friend profile, and extension data. All data is stored in `Key-Value` format. `Key` is of the `String` type and supports only uppercase and lowercase letters, digits, and underscores. `Value` supports the following types:
>
>  | Type         | Description                                                  |
>  | ------------ | ------------------------------------------------------------ |
>  | uint64_t     | Integer (Not supported by custom fields.)                    |
>  | string       | String. The string length cannot exceed 500 bytes.           |
>  | bytes        | Buffer. The buffer length cannot exceed 500 bytes.           |
>  | string array | String array. Each string cannot exceed 500 bytes. Available only to the `Tag_SNS_IM_Group` field of the friend list. |
>
>  - **User profile**: A user profile includes standard and custom fields. For the custom fields, see the extension data part below. For the standard fields currently supported by Chat, see [Standard Profile Fields](https://intl.cloud.tencent.com/document/product/1047/33520).
>  - **Friend profile**: A friend profile includes standard and custom friend fields. Chat's contact list supports up to 3,000 friends. The standard friend fields are described as follows:
>  <table>
>  <thead>
>  <tr>
>  <th>Field Name</th>
>  <th>Type</th>
>  <th>Description</th>
>  </tr>
>  </thead>
>  <tbody><tr>
>  <td>Tag_SNS_IM_Group</td>
>  <td>Array</td>
>  <td>Friend list</td>
>  </tr>
>  <tr>
>  <td>Tag_SNS_IM_Remark</td>
>  <td>String</td>
>  <td>Friend remarks</td>
>  </tr>
>  <tr>
>  <td>Tag_SNS_IM_AddSource</td>
>  <td>String</td>
>  <td>Source of the friend request</td>
>  </tr>
>  <tr>
>  <td>Tag_SNS_IM_AddWording</td>
>  <td>String</td>
>  <td>Content of the friend request</td>
>  </tr>
>  <tr>
>  <td>Tag_SNS_IM_AddTime</td>
>  <td>Integer</td>
>  <td>Timestamp of the friend request</td>
>  </tr>
>  </tbody></table>
>  For more information, see <a href="https://intl.cloud.tencent.com/document/product/1047/33521">Standard friend fields</a>.
>  - **Custom profile**: To apply for custom profile fields, the app admin can log in to the [Chat console](https://console.cloud.tencent.com/im) and find your app and go to **Feature Configuration**. After the application is submitted, custom profile fields will take effect in five minutes.
>   - For more information on user profile management, see [Profile Management](https://intl.cloud.tencent.com/document/product/1047/33520).
>   - For more information on relationship chain custom profile management, see [Custom friend fields](https://intl.cloud.tencent.com/document/product/1047/33521).
>
>  #### Chat user profile storage limits
>  - **Service feature limits**
>   - Data storage: Each string or buffer cannot exceed 500 bytes.
>   - Custom fields: The keywords of custom fields must consist of English letters with a length no longer than 8 bytes. The values of custom fields cannot exceed 500 bytes.
>   - Friend relationship chain: Each user can have up to 3,000 friends.
>  - **API-related limits**
>   - Account management: Up to 100 usernames can be imported at a time, and the status of up to 500 users can be queried per request.
>   - Other call frequency: Up to 200 times per second.
>
>  For more information on the use limits, see [Use Limits](https://intl.cloud.tencent.com/document/product/1047/34381).
>
>  ### Email systems
>
>  Email systems are almost mandatory in games these days. Emails can contain text messages, as well as email attachments such as game props and rewards. An email can be sent to a single user, or it can be sent as a group email to give out event rewards. The following describes how the features of an email system are implemented from diverse aspects such as players receiving emails, email list, email unread count, sending emails to all members, and email validity period.
>
>  #### Email receiving and sending
>
>  - **Players receiving emails**: When system emails are sent successfully and players are online, the players can receive the system emails properly. The players can obtain the historical or latest emails by getting the message list of email conversations. They can also add or delete the listener for the receiving of new messages of all types (including text, custom, and rich media messages). The sample code for Unity is as follows:
>  ```javascript
>  // Configure the message receiving event listener
>  TencentIMSDK.AddRecvNewMsgCallback((List<Message> messages, string user_data)=>{
>    foreach(Message message in messages)
>    {
>      foreach (Elem elem in message.message_elem_array)
>      {
>        // There is a next element
>        if (elem.elem_type == TIMElemType.kTIMElem_Text)
>        {
>           string text = elem.text_elem_content;
>        }
>      }
>    }
>  })
>  // Listen for the `RecvNewMsgCallback` callback to receive messages
>  // To stop receiving messages, call `RemoveRecvNewMsgCallback` to remove the listener. This step is optional and can be performed as needed.
>  ```
>  For more information, see [Unity - Receiving Message](https://intl.cloud.tencent.com/document/product/1047/48573).
>  - **System sending emails**: The system can send system emails to users via different server APIs, which are described as follows:
>  <table>
>  <thead>
>  <tr>
>  <th>API</th>
>  <th>Characteristics</th>
>  <th>Application Scenarios</th>
>  </tr>
>  </thead>
>  <tbody><tr>
>  <td><a href="https://intl.cloud.tencent.com/document/product/1047/34919">Sending one-to-one messages to one user</a></td>
>  <td>Sends a message to a specified account. The sender displayed to the recipient is not the admin, but the account specified by the admin.</td>
>  <td>Sending messages to a specific user, for example, sending a game rewarding message to a user</td>
>  </tr>
>  <tr>
>  <td><a href="https://intl.cloud.tencent.com/document/product/1047/34920">Sending one-to-one messages to multiple users</a></td>
>  <td>A one-to-one message can be sent to up to 500 users at a time, and the highest call frequency is 200 times per second.</td>
>  <td>Sending messages to specific users, without the need to create a recipient group. If the number of recipients is large, you need to send the messages in batches.</td>
>  </tr>
>  <tr>
>  <td><a href="https://intl.cloud.tencent.com/document/product/1047/34959">Sending ordinary messages in a group</a></td>
>  <td>When sending ordinary messages to a group, you need to add all recipients to the same group.</td>
>  <td>Sending ordinary messages to a large number of users (up to 100,000 users per community group)</td>
>  </tr>
>  <tr>
>  <td><a href="https://intl.cloud.tencent.com/document/product/1047/37165">Pushing to all users</a></td>
>  <td>Pushes messages to all users in an app. You can specify user tags and attributes for message sending.</td>
>  <td>Pushing messages to all users in an app or to a large number of users with specific characteristic attributes, such as campaign emails</td>
>  </tr>
>  </tbody></table>
>  <dx-alert infotype="explain" title="">
>  Pushing to all users is available only to the Ultimate edition. To use it, you need to [purchase the Ultimate edition](https://www.tencentcloud.com/document/product/1047/34577), go to the [console](https://console.cloud.tencent.com/im/login-message), choose **Feature Configuration** > **Login and Message** > **Push to all users**, and enable the feature.
>  </dx-alert>
>  The following is a sample of a basic request for sending an ordinary message in a group:
>
>  ```json
>  {
>      "GroupId": "@TGS#2C5SZEAEF",
>      "Random": 8912345, // A random number. If the random numbers of two messages are the same within five minutes, they are considered to be the same message.
>      "MsgBody": [ // Message body, which consists of an element array. For details, see the field description.
>          {
>              "MsgType": "TIMTextElem", // Text
>              "MsgContent":{
>              "Text": "red packet"
>              }
>          },
>          {
>              "MsgType": "TIMCustomElem", // Custom
>              "MsgContent":{
>              "Data": "message",
>              "Desc": "notification",
>              "Ext": "url",
>              "Sound":"dingdong.aiff"
>              }
>          }
>      ],
>  }
>  ```
>  `MsgBody` (message body) is a message array. You can add text and custom messages to be sent to it.
>
>  #### Email list
>
>  The storage of the historical email list is equivalent to the storage of messages. It consists of the storage of historical one-to-one messages and the storage of historical group messages. Because a group chat requires at least two users, you can create a group containing the account specified by the admin and the user receiving the email for storage.
>
>  >? For the Free edition and Pro edition, the storage period is seven days. For the Ultimate edition, the storage period is 30 days. The Pro edition and Ultimate edition allow you to extend the storage period. You can log in to the [console](https://console.cloud.tencent.com/im) to modify related configuration.
>  >Extending the storage period of historical messages is a paid value-added service. For more information on billing, see [Value-added Service Pricing](https://www.tencentcloud.com/zh/document/product/1047/34350).
>
>
>  When the network is normal, the latest cloud data will be pulled; when it is abnormal, the SDK will return the locally stored historical messages. Paged pulling is supported. The following is Unity sample code for pulling the historical email list:
>  ```javascript
>  // Pull historical one-to-one messages
>  // Set `msg_getmsglist_param_last_msg` to `null` for the first pull
>  // `msg_getmsglist_param_last_msg` can be the last message in the returned message list for the second pull.
>  var get_message_list_param = new MsgGetMsgListParam
>  {
>      msg_getmsglist_param_last_msg = LastMessage
>  };
>  TIMResult res = TencentIMSDK.MsgGetMsgList(conv_id, TIMConvType.kTIMConv_C2C, get_message_list_param, (int code, string desc, string user_data) => {
>  // Process the callback logic
>  });
>  ```
>  For more information on how to pull historical messages, see [Historical Message - Unity](https://intl.cloud.tencent.com/document/product/1047/48871).
>
>  #### Unread email count
>
>  A record of a user-system email is equivalent to a conversation in a chat. Tencent Cloud Chat provides a conversation unread count feature to remind users that they have not yet read messages. When a user clicks into the conversation and returns to the conversation list, the unread message count is cleared. The following is Unity sample code:
>  ```javascript
>  // Get the total unread count
>  TIMResult res = TencentIMSDK.ConvGetTotalUnreadMessageCount((int code, string desc, GetTotalUnreadNumberResult unread, string user_data)=>{
>   // Process the async logic
>  });
>  
>  // Unread count change notification
>  TencentIMSDK.SetConvTotalUnreadMessageCountChangedCallback((int total_unread_count, string user_data)=>{
>   // Process the callback logic
>  });
>  
>  // Clear the unread count of all conversations
>  TIMResult res = TencentIMSDK.MsgMarkAllMessageAsRead((int code, string desc, string user_data)=>{
>   // Process the async logic
>  });
>  ```
>  For more information, see [Unity - Conversation Unread Count](https://intl.cloud.tencent.com/document/product/1047/48846).
>
>  #### Sending emails to all members
>  Sending emails to all members is to send email messages to all players in a game. Tencent Cloud Chat provides the pushing to all members feature at the server side. The following is sample code:
>  ```
>  https://console.tim.qq.com/v4/all_member_push/im_push?usersig=xxx&identifier=admin&sdkappid=88888888&random=99999999&contenttype=json
>  ```
>  The following is a sample request:
>  ```json
>  {
>      "From_Account": "admin",
>      "MsgRandom": 56512,
>      "MsgLifeTime": 120, // Offline storage for 120s (two minutes)
>      "MsgBody":[
>          {
>          "MsgType": "TIMTextElem",
>          "MsgContent":{
>              "Text": "hi, beauty"
>              }
>          }
>      ]
>  }
>  ```
>
>  The feature of sending messages to all members allows you to set the offline storage period, so that even if some users are not online, they can still receive the messages within the specified offline storage period. Configure `MsgLifeTime` (unit: second) to specify the offline storage period: The maximum period is 604,800 seconds (seven days). The default value is `0`, which indicates that messages are not stored offline.
>
>  For more information on pushing to all users, see [Pushing to All Users](https://intl.cloud.tencent.com/document/product/1047/37166).
>
>  #### Email validity period
>  The storage period of historical emails is as follows: For the Free edition and Pro edition, the storage period is seven days. For the Ultimate edition, the storage period is 30 days. The Pro edition and Ultimate edition allow you to extend the storage period. For more information on the storage of historical emails, see [Historical message storage period settings](https://intl.cloud.tencent.com/document/product/1047/34419).
>  In addition, when sending a message on the server side, you can set `MsgLifeTime` to specify the offline storage period (up to seven days) of the message. If `MsgLifeTime` is `0`, it indicates that the message is sent to online users only and is not stored offline. For more information, see [here](https://intl.cloud.tencent.com/document/product/1047/34919).
>
>  ### Temporary team-up
>
>  Temporary team-up is essential in online multiplayer games. The following describes temporary team-up scenarios and how the background and team members obtain team information.
>
>  [](id:Team_scene)
>  #### Team-based scenarios
>
>  Team-based scenarios include creating a team, leaving a temporary team, becoming the team leader, inviting others to join a team, and disbanding a team. The following are some code examples to explain the implementation of different scenarios.
>
>  - **Creating a team before the game begins**: When the first player enters the game, the server automatically creates a group and the maximum number of group members can be specified. If the request specifies the group owner or group members, the specified group owner or group members will be automatically added to the group when the group is created. The following is a sample request URL:
>  ```
>  https://console.tim.qq.com/v4/group_open_http_svc/create_group?sdkappid=88888888&identifier=admin&usersig=xxx&random=99999999&contenttype=json
>  ```
>  The following is a basic request sample:
>  ```json
>  {
>      "Owner_Account": "leckie", // UserId of the group owner (optional)
>      "Type": "Public", // Group type: Private, Public, ChatRoom, AVChatRoom, or Community
>      "Name": "TestGroup", // Group name (required)
>      "MaxMemberCount":5 // Maximum number of group members (optional)
>  }
>  ```
>  >? An app supports up to 100,000 groups. For extra groups, you need to pay certain fees, as described in [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350). For more information on group creation on the server side, see [Creating a Group](https://intl.cloud.tencent.com/document/product/1047/34895).
>  - **Adding group members**: If new players enter the game after the group chat is created, you need to add the new players to the existing group. The following is a sample request URL:
>  ```
>  https://console.tim.qq.com/v4/group_open_http_svc/add_group_member?sdkappid=88888888&identifier=admin&usersig=xxx&random=99999999&contenttype=json
>  ```
>  The following is a request sample:
>  ```json
>  {
>      "GroupId": "@TGS#2J4SZEAEL", // The group to which to add members (required)
>      "MemberList": [ // Up to 300 members can be added at a time.
>          {
>              "Member_Account": "tommy" // The ID of the member to be added (required)
>          },
>          {
>              "Member_Account": "jared"
>      }]
>  }
>  ```
>  For more information, see [Adding Group Members](https://intl.cloud.tencent.com/document/product/1047/34921).
>  - **Webhook for successful team-up**: If the maximum number of group members is set when creating a group, the game can start only when all the required number of members are in the group. When the `webhook after a group is full` is received, the game can be started. The following is a sample request URL:
>  ```
>  https://www.example.com?SdkAppid=$SDKAppID&CallbackCommand=$CallbackCommand&contenttype=json&ClientIP=$ClientIP&OptPlatform=$OptPlatform
>  ```
>  The following is a sample request:
>  ```json
>  {
>      "CallbackCommand": "Group.CallbackAfterGroupFull", // Webhook command
>      "GroupId": "@TGS#2J4SZEAEL" // Group ID
>  }
>  ```
>  For more information, see [After a Group Is Full](https://intl.cloud.tencent.com/document/product/1047/34376).
>  - **Notification on a new member joining the group**: When a new player enters the game (group chat), the system sends the `webhook after a user joins a group` to notify other group members. The following is a sample request URL:
>  ```
>  https://www.example.com?SdkAppid=$SDKAppID&CallbackCommand=$CallbackCommand&contenttype=json&ClientIP=$ClientIP&OptPlatform=$OptPlatform
>  ```
>  The following is a sample request:
>  ```json
>  {
>      "CallbackCommand": "Group.CallbackAfterNewMemberJoin", // Webhook command
>      "GroupId" : "@TGS#2J4SZEAEL",
>      "Type": "Public", // Group type
>      "JoinType": "Apply", // Group joining method: `Apply` (application); `Invited` (invitation)
>      "Operator_Account": "leckie", // Operator
>      "NewMemberList": [ // List of new members
>          {
>              "Member_Account": "jared"
>          },
>          {
>              "Member_Account": "tommy
>          }
>      ]
>  }
>  ```
>  >? To enable this webhook, you must configure the webhook URL and toggle on the corresponding protocol. For details on the configuration method, see [Webhook Configuration](https://intl.cloud.tencent.com/document/product/1047/34520). For more information, see [After a User Joins a Group](https://intl.cloud.tencent.com/document/product/1047/34372).
>  >
>  - **Leaving a team during a game**: When a player leaves the game voluntarily or due to network problems, the server can notify other players in the group that someone leaves the group chat through the `webhook after a user leaves a group` and can also send a message to the player who leaves the game due to network problems. The following is a request URL example for [After a User Leaves a Group](https://intl.cloud.tencent.com/document/product/1047/34373):
>  ```
>  https://www.example.com?SdkAppid=$SDKAppID&CallbackCommand=$CallbackCommand&contenttype=json&ClientIP=$ClientIP&OptPlatform=$OptPlatform
>  ```
>  The following is a sample request:
>  ```json
>  {
>      "CallbackCommand": "Group.CallbackAfterMemberExit", // Webhook command
>      "GroupId": "@TGS#2J4SZEAEL", // Group ID
>      "Type": "Public", // Group type
>      "ExitType": "Kicked", // Member leaving type: `Kicked` - being kicked out; `Quit` - voluntarily leaving
>      "Operator_Account": "leckie", // Operator
>      "ExitMemberList": [ // List of members who left the group
>          {
>              "Member_Account": "jared"
>          },
>          {
>              "Member_Account": "tommy"
>          }
>      ]
>  }
>  ```
>  - **Disbanding a group chat after a game ends**: After a game ends, the server side can disband the group chat directly. The following is a request URL example for [Disbanding a Group](https://intl.cloud.tencent.com/document/product/1047/34896):
>  ```
>  https://console.tim.qq.com/v4/group_open_http_svc/destroy_group?sdkappid=88888888&identifier=admin&usersig=xxx&random=99999999&contenttype=json
>  ```
>  The following is a sample request:
>  ```json
>  {
>      "GroupId": "@TGS#2J4SZEAEL"
>  }
>  ```
>  Audio/Video chat in temporary teams is complex and will be elaborated below.
>
>  #### Getting team information in the background
>
>  - **Getting group details**: You can call the server API `Getting Group Profiles` to get group details such as the number of members in the group and the basic information of the group members. You can use the `Filter` field in the request to filter the information to pull. The following is a sample request URL:
>  ```
>  https://console.tim.qq.com/v4/group_open_http_svc/get_group_info?sdkappid=88888888&identifier=admin&usersig=xxx&random=99999999&contenttype=json
>  ```
>  The following is a sample request:
>  ```json
>  {
>      "GroupIdList": [ // The list of group IDs specified for the query. This parameter is required.
>          "@TGS#1NVTZEAE4",
>          "@TGS#1CXTZEAET"
>      ]
>  }
>  ```
>  For more information, see [Getting Group Profiles](https://intl.cloud.tencent.com/document/product/1047/34961).
>  - **Getting group member details**: You can call the API `Getting Group Member Profiles` to get the detailed information of group members (including custom fields). The following is a sample request URL:
>  ```
>  https://console.tim.qq.com/v4/group_open_http_svc/get_group_member_info?sdkappid=88888888&identifier=admin&usersig=xxx&random=99999999&contenttype=json
>  ```
>  The following is a sample request:
>  ```json
>  {
>      "GroupId":"@TGS#1NVTZEAE4"  // Group ID (required)
>  }
>  ```
>  In the response, the `MemberNum` field indicates the total number of members in the group, and `AppMemberDefinedData` indicates the custom field information of group members.
>  >? This API does not support audio-video groups (AVChatRoom). For more information, see [Getting Group Member Profiles](https://intl.cloud.tencent.com/document/product/1047/34948).
>
>
>  #### Team members getting team information
>
>  Members of a team can call the API `Getting Group Member Profiles` to get the detailed information, such as role and status, of other members in the team.
>  ```java
>  GroupGetMemberInfoListParam param = new GroupGetMemberInfoListParam
>  {
>    group_get_members_info_list_param_group_id = "group_id",
>    group_get_members_info_list_param_identifier_array = new List<string>
>    {
>      "user_id"
>    }
>  };
>  TIMResult res = TencentIMSDK.GroupGetMemberInfoList(param, (int code, string desc, GroupGetMemberInfoListResult result, string user_data)=>{
>   // Process the async logic
>  });
>  ```
>  >?
>  >- For more information, see [Unity - Getting the Profile of a Group Member](https://intl.cloud.tencent.com/document/product/1047/50320).
>  >- For other group information such as starting a game after a group is full and members joining or leaving a team, see [Team-based scenarios](#Team_scene). Such information will be notified to the group via callbacks.
>  >- For more information about group selection and other group related information, see [Group System](https://intl.cloud.tencent.com/document/product/1047/33529). For more information about group management, see [Console Guide - Group Management](https://intl.cloud.tencent.com/document/product/1047/34578).
>
>  ### Filtering sensitive information
>
>  Filtering sensitive content is an important feature for games. The implementation scheme is as follows:
>  1. Bind the webhook before sending a group message.
>  2. Identify the message type based on the webhook data and deliver the message data to Tencent Cloud Security or another third-party detection service.
>  3. If the message is an ordinary text message, wait for the detection result of Tencent Cloud Security and return the data packet indicating whether to deliver the message to the Chat backend.
>
>  Sample data of the webhook before sending a message:
>
>  ```json
>  {
>      "CallbackCommand": "Group.CallbackBeforeSendMsg", // Webhook command
>      "GroupId": "@TGS#2J4SZEAEL", // Group ID
>      "Type": "Public", // Group type
>      "From_Account": "jared", // Sender
>      "Operator_Account":"admin", // Request initiator
>      "Random": 123456, // Random number
>      "OnlineOnlyFlag": 1, // The value is `1` if it is an online message and `0` (default) if it’s not. For audio-video groups, the value is `0`.
>      "MsgBody": [ // Message body. For more information, see the `TIMMessage` message object.
>          {
>              "MsgType": "TIMTextElem", // Text
>              "MsgContent":{
>                  "Text": "red packet"
>              }
>          }
>      ],
>      "CloudCustomData": "your cloud custom data"
>  }
>  ```
>
>  >?You can identify the message type based on the `MsgType` field in `MsgBody`. For more information on the fields, see [Before a Group Message Is Sent](https://intl.cloud.tencent.com/document/product/1047/34374).
>
>  You can choose to handle a non-compliant message in a specific way, which can be implemented through the data packet in the webhook returned to the Chat backend.
>
>  ```json
>  {
>      "ActionStatus": "OK",
>      "ErrorInfo": "",
>      "ErrorCode": 0 // Different `ErrorCode` values have different meanings.
>  }
>  ```
>
>  | ErrorCode | Description                                                  |
>  | --------- | ------------------------------------------------------------ |
>  | 0         | Speaking is allowed, and messages can be delivered normally. |
>  | 1         | Speaking is rejected, and the client returns `10016`.        |
>  | 2         | Silent discarding is enabled, and the client returns messages normally. |
>
>  >?You can use them as needed.
>
>  ### Customizing message types (such as props gifting and trading messages)
>
>  Game chats require custom messages in addition to simple messages such as text, emoji, and voice messages. Custom messages allow developers to customize the content format of messages to implement more chat room features such as game props gifting and trading.
>
>  Tencent Cloud Chat provides nine basic message types: text, emoji, geographical location, image, voice, file, user generated short video (UGSV), system notification, and custom messages. The formats of all messages except custom messages are fixed, and users only need to enter corresponding information. For the detailed descriptions of the message types, see [One-to-One Message Types](https://intl.cloud.tencent.com/document/product/1047/33523). For more information on the message formats, see [Message Formats](https://intl.cloud.tencent.com/document/product/1047/33527).
>
>  You can send custom messages to users through server APIs [Sending One-to-One Messages to One User](https://intl.cloud.tencent.com/document/product/1047/34919), [Sending One-to-One Messages to Multiple Users](https://intl.cloud.tencent.com/document/product/1047/34920), and [Sending Ordinary Messages in a Group](https://intl.cloud.tencent.com/document/product/1047/34959). The following is a basic request sample for sending an ordinary message in a group:
>
>  ```json
>  {
>      "GroupId": "@TGS#2C5SZEAEF",
>      "Random": 8912345, // A random number. If the random numbers of two messages are the same within five minutes, they are considered to be the same message.
>      "MsgBody": [ // Message body, which consists of an element array. For details, see the field description.
>          {
>              "MsgType": "TIMTextElem", // Text
>              "MsgContent":{
>                  "Text": "red packet"
>              }
>          },
>          {
>              "MsgType": "TIMFaceElem", // Emoji
>              "MsgContent":{
>              "Index": 6,
>              "Data": "abc\u0000\u0001"
>              }
>          }
>      ],
>      "CloudCustomData": "your cloud custom data",
>      "SupportMessageExtension": 0,
>  }
>  ```
>
>  You can modify `CloudCustomData` to define the custom message data (stored on the cloud) and enter the custom message in `MsgBody` (message body) for sending.
>
>  ### Audio/Video chat in teams
>
>  Audio/Video chat in games is an important feature. Tencent Cloud Chat apps are equipped with real-time audio/video call features by using [Tencent Real-Time Communication (TRTC)](https://www.tencentcloud.com/document/product/647) and TUICallKit.
>
>  >? 
>  >- We provide a 7-day free trial of the audio/video call capability for each SDKAppID. You can obtain only one free trial for each SDKAppID in the Chat [console](https://console.cloud.tencent.com/im).
>  >- For more information on TUICallKit, see [Integration Solution (UI Included) - Audio/Video Call](https://www.tencentcloud.com/document/product/1047/50025).
>
>
>  ### Game chat room types
>
>  Game chat room types are described as follows:
>
>  | Type              | Characteristics                                              |
>  | ----------------- | ------------------------------------------------------------ |
>  | Channel           | A channel usually engages a large number of chat users and does not have a list of fixed members. Users can join and leave a channel at any time. Offline message push is not required. |
>  | Live game lobby   | A live game lobby usually engages a number of chat users. Users can join and leave the live room at any time. Historical message query is supported. |
>  | Team              | A team usually engages a small number of chat users, who do not need to be friends with each other. A team is terminated when a game ends. Offline message push is not required. |
>  | Friend            | One-to-one chat. Chat records are stored. Chat partners can only be friends in the contact list. |
>  | Private message   | One-to-one chat. Chat partners can be strangers.             |
>  | Audio-video group | There is no limit on the number of chat users. Users can join and leave an audio-video group at any time. |
>
>  Chat provides the following types of chat rooms:
>
>  | Type                           | Characteristics                                              |
>  | ------------------------------ | ------------------------------------------------------------ |
>  | Work group (Work)              | A work group allows users to join the group by being invited by a friend who is a member of the group. The invitation does not need to be accepted by the invitee or approved by the group owner. |
>  | Public group (Public)          | A public group allows the group owner to designate group admins. To join the group, a user needs to search for the group ID and send a request, and the request needs to be approved by the group owner or an admin before the user can join the group. |
>  | Meeting group (Meeting)        | A meeting group allows users to join and leave freely and view historical messages sent before they join the group. Meeting groups are ideal for scenarios that integrate Tencent Real-Time Communication (TRTC), such as audio/video conferencing and online education. This group type is the same as chat room (ChatRoom) in earlier versions. |
>  | Audio-video group (AVChatRoom) | An audio-video group allows users to join and exit freely, supports an unlimited number of members, and does not store message history. Audio-video groups can be used with Cloud Streaming Services (CSS) to support on-screen comment chat scenarios. |
>  | Community group (Community)    | A community group allows users to join and exit freely, supports up to 100,000 members, and stores message history. To join the group, a user needs to search for the group ID and send an application, and the application does not need to be approved by an admin before the user can join the group. |
>
>  The following provides some sample solutions based on Chat group characteristics, which can be applied to your games as needed.
>
>  | Type                        | Solution                                                     | Characteristics                                              |
>  | --------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
>  | Channel and live game lobby | Community group                                              | A community group supports a large number of users and allows users to join and leave freely, without approval. |
>  | Friend                      | One-to-one chat+Permission control (allowing only friends to send messages to each other) | Only friends are allowed to send messages to each other.     |
>  | Private message             | One-to-one chat+Permission control (allowing any two users in the app to send one-to-one messages to each other) | Any two strangers can send messages to each other.           |
>  | Team-up                     | Public group (Public) and meeting group (Meeting)            | Only team members in the game can enter the group chat. Audio-video chat is supported. |
>  | Audio-video group           | Audio-video group (AVChatRoom)                               | There is no limit on the number of group members, and users can join or leave an audio-video group at any time. |
>
>  >?
>  >- For more information on the permission control of friend and private one-to-one chats, see [One-to-One Messaging Permission Control](https://intl.cloud.tencent.com/document/product/1047/33523#.E5.8D.95.E8.81.8A.E6.B6.88.E6.81.AF.E6.9D.83.E9.99.90.E6.8E.A7.E5.88.B6%EF%BC%89).
>  >- For more information on the group system, see [Group System](https://intl.cloud.tencent.com/document/product/1047/33529).
