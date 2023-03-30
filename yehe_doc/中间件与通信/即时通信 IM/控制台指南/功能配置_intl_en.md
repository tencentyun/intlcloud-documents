>## Login and Message
>Log in to the [IM console](https://console.cloud.tencent.com/im), click the target app section, and select **Feature Configuration** > **Login and Message** on the left sidebar. You can manage login and message related settings according to your business needs.
>
>### Login settings
>1. On the **Login and Message** page, click **Edit** in the upper-right corner of the **Login Settings** area.
>2. In the pop-up dialog box, select a multi-device login policy and set the maximum number of concurrent online web instances.
><dx-alert infotype="explain" title="">
>If you select multi-device login for the Ultimate edition, up to 10 concurrent online web clients are supported, and up to 3 online devices are supported for each of the Android, iPhone, iPad, Windows, macOS, and Linux platforms.
></dx-alert>
><img src="https://main.qcloudimg.com/raw/9774753fc2c7f4d46f47d0573404bc32.png" />
>3. Click **Confirm**.
>
>### Historical message storage period settings
>Historical messages are stored for seven days by default. **Extending the storage period is a value-added service.** For more information on billing, see [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350). You can modify the storage period once every month.
>
>1. On the **Login and Message** page, click **Edit** in the upper-right corner of the **Historical Message Storage Period Settings** area.
>2. In the pop-up dialog box, extend the storage period of historical messages.
>3. Click **Confirm** and the configuration will take effect immediately.
>
>### Message recall settings
>1. On the **Login and Message** page, click **Edit** in the upper-right corner of the **Message Recall Settings** area.
>2. In the pop-up dialog box, set the time limit for message recall.
>3. Click **Confirm**.
>
>
>>?This feature is **available only for the Ultimate edition**. To use it, purchase the Ultimate edition as instructed in [Creating and Upgrading an Application](https://www.tencentcloud.com/document/product/1047/34577). For more information, see [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350?from=17178#.E5.9F.BA.E7.A1.80.E6.9C.8D.E5.8A.A1.E8.AF.A6.E6.83.85). To ensure the proper use of this feature, upgrade the **native SDK** to **v5.9.0 or later** and the **web SDK** to **v2.16.0 or later**.
>
>### Multi-client synchronization settings
>
>You can enable or disable **Sync Conversation Deletion Across Clients** in the **Multi-client Synchronization Settings** area on the **Login and Message** page.
>- Enabled: If multiple clients are online concurrently, deleting a conversation from one client will be synced to other clients (that is, the conversation will also be deleted from other clients).
>- Disabled: If multiple clients are online concurrently, deleting a conversation from one client will not be synced to other clients. The feature of syncing conversation deletion across clients is disabled by default.
>>?The feature of syncing conversation deletion across clients is available only to **native SDK v5.1.1 and web SDK v2.14.0 or later**. If you are using an earlier SDK version, you need to **upgrade your SDK** before you can use the feature.
>
>### User status query and status change notification settings
>You can enable the feature of user status query and status change notification in the **Set user status query and status change notification** area on the **Login and Message** page.
>>?The feature of user status query and status change notification is disabled by default. When it is disabled, the error code 72001 will be reported for user status query, subscription, or unsubscription on clients. The feature can be enabled on native SDK v6.3 or later and is available only to Ultimate edition users. You can [click here to upgrade](https://www.tencentcloud.com/document/product/1047/34577).
>
>### Message extension settings
>You can enable message extension in the **Set message extension** area on the **Login and Message** page.
>>?Message extension allows you to configure keys and values for messages to implement features such as polling, group notices, and surveys. For more information, see [here](https://www.tencentcloud.com/document/product/1047/50865). Message extension is available only to Ultimate edition users and is supported only on native SDK Enhanced edition v6.7.3184 or later. If you are using an earlier version, upgrade your SDK.
>
>[](id:all_member_push)
>### "Pushing to all users" settings
>You can enable the feature of pushing to all users in the **Push to all users** area.
><dx-alert infotype="explain" title="">
>Pushing to all users is an excellent tool for application user operations. It not only supports sending specific content to all users, but also can send personalized content to specific user groups based on tags and attributes, such as member events, and regional notifications. This helps effectively attract, convert, and activate users. For more information, see [Pushing to All Users](https://intl.cloud.tencent.com/document/product/1047/37166).
></dx-alert>
>
>
>### Configuration of conversations to pull
>In the **Configuration of conversations to pull** area on the **Login and Message** page, you can configure the number of conversations to be pulled from the cloud. The default number is 100, and you can change the number to up to 500.
>>?
>>- The feature of configuring the number of conversations to pull is available only to **Ultimate edition** users. If you are not an Ultimate edition user, you need to upgrade your package before you can use the feature.
>>- The feature of configuring the number of conversations to pull is available only to **native SDK v5.1.1 and web SDK v2.0 or later**. If you are using an earlier SDK version, you need to upgrade your SDK before you can use the feature.
>
>
>### Blocklist check
>You can enable or disable **Show "Sent successfully" After Sending Messages** in the **Blocklist check** area on the **Login and Message** page.
>- Enabled: If you are in the recipient’s blocklist, you will see **Sent successfully** after sending a one-to-one message and the recipient will not receive the message. This is the default setting.
>- Disabled: If you are in the recipient’s blocklist, you will see **Failed to send** after sending a one-to-one message
>
>### Relationship check
>You can enable or disable **Check Relationship for One-to-One Messages** in the **Relationship Check** area on the **Login and Message** page.
>- Enabled: Check relationships before a one-to-one chat starts and only allow sending one-to-one messages to friends. When a user sends a one-to-one message to a stranger, the SDK will return [error code 20009](https://intl.cloud.tencent.com/document/product/1047/34348).
>- Disabled: Do not check relationships before a one-to-one chat starts and allow users to send and receive one-to-one messages to and from friends and strangers. This is the default setting.
>
>## Friends and Relationship Chain
>Setting verification method for adding friends and custom friend fields.
>### Verification method for adding friends
>1. Log in to the [IM console](https://console.cloud.tencent.com/im) and click the target IM app section.
>2. On the left sidebar, choose **Feature Configuration** > **Friend and Relationship**, and click **Edit** in the upper-right corner of the **Default Verification for Adding Friends** area.
>![](https://qcloudimg.tencent-cloud.cn/raw/6d5a4de703ec20c4a337c1e504f95de8.png)
>3. Select a verification method as needed and click **Confirm**.
>
>### Custom friend fields
>>?You can add up to 20 custom friend fields, which cannot be deleted and whose field name and type cannot be modified. Please set the fields properly as needed.
>
>1. Log in to the [IM console](https://console.cloud.tencent.com/im) and click the target IM app section.
>2. On the left sidebar, choose **Feature Configuration** > **Friend and Relationship**.
>3. Click **Add** in the upper-right corner of the **Custom Friend Field** area.
>4. In the pop-up dialog box, enter a field name and select a field type.
>
><dx-alert infotype="explain" title="">
>The field name must be all letters and cannot exceed eight characters.
></dx-alert>
>
>## Custom User Fields
>Log in to the [IM console](https://console.cloud.tencent.com/im), click the target app section, and select **Feature Configuration** > **Custom User Field** on the left sidebar. You can manage custom user fields according to your business needs.
>>!You can add up to 20 custom user fields, which cannot be deleted and whose field name and type cannot be modified. Please set the fields properly as needed.
>
>### Adding a custom user field
>
>1. On the **Custom User Field** page, click **Add** in the upper-right corner.
>2. In the pop-up dialog box, enter a field name, select a field type, and set read/write permissions.
><dx-alert infotype="explain" title="">
> - The field name must be all letters and cannot exceed eight characters.
> - You need to enable at least one read permission and one write permission
></dx-alert>
><img src="https://main.qcloudimg.com/raw/95851bca861f45aed20c045a8d09928e.png" alt=""> 
>3. Click **Confirm**.
>
>### Modifying the permissions of a custom user field
>1. On the **Custom User Field** page, click **Change Permissions** in the row of the target field.
>2. In the pop-up dialog box, change the read or write permission.
>![](https://main.qcloudimg.com/raw/01081d71fe7ec45b470a249d685696c1.pngg)
>3. Click **Confirm**.
> ![](https://main.qcloudimg.com/raw/271b68191ae3b1acb28fcbb4f7fea63e.png)
>4. Click **Confirm**.
>
>## Group Configuration
>### Custom group member fields
>Log in to the [IM console](https://console.cloud.tencent.com/im), click the target app section, and select **Feature Configuration** > **Custom Group Member Field** on the left sidebar. You can manage custom group member fields according to your business needs.
>>!You can add up to five custom group member fields, which cannot be deleted and whose group type and read/write permissions can be changed. Please set the fields properly as needed.
>
>#### Adding a custom group member field
>1. On the **Custom Group Member Field** page, click **Add** in the upper-right corner.
>2. In the pop-up dialog box, enter a field name and set group types and read/write permissions.
><dx-alert infotype="explain" title="">
>- The field name can contain up to 16 characters, supporting letters, digits, and underscores (_). It cannot begin with a digit.
>- A custom group member field and a custom group field cannot have the same name.
></dx-alert>
><ul>
><li>Click <strong>Add Group Type</strong> to add one group type at a time. Duplicate group types are not allowed.</li>
><li>Click <strong>Delete</strong> in the row of the target group type to delete it. However, you must retain at least one group type.<br><img src="https://main.qcloudimg.com/raw/3b6bcff0f4156f2340f71d082a29ac45.png" alt=""></li>
></ul>
>
>3. Select **I understand that after a custom group member field is added, only the read-write permissions of the added group type can be modified; the group type cannot be reselected or deleted; the field cannot be deleted.**
>4. Click **Confirm**.
>
>#### Editing a custom group member field
>1. On the **Custom Group Member Field** page, click **Edit** in the row of the target custom group member field.
>2. In the pop-up dialog box, modify the read and write permissions of existing group types, or click **Add Group Type** to add a new one and set its parameters. Duplicate group types are not allowed.
> ![](https://main.qcloudimg.com/raw/19532e3441d0de3a1b7c29e2fd0b4a4a.png)
>3. Select **I understand that after a custom group member field is added, only the read-write permissions of the added group type can be modified; the group type cannot be reselected or deleted; the field cannot be deleted.**
>4. Click **Confirm**.
>
>
>### Custom group fields
>Log in to the [IM console](https://console.cloud.tencent.com/im), click the target app card, and select **Feature Configuration** > **Custom Group Field** on the left sidebar. You can manage custom group fields according to your business needs.
>>!You can add up to 10 custom group fields. Once set, these fields cannot be deleted, and only the group types and the corresponding read and write permissions can be modified. Therefore, set these fields properly as needed.
>
>#### Adding a custom group field
>1. On the **Custom Group Field** page, click **Add** in the upper-right corner.
>2. In the pop-up dialog box, enter a field name and set the group types and read/write permissions.
>>?
>>- The field name can contain up to 16 characters, supporting letters, digits, and underscores (_). It cannot begin with a digit.
>>- A custom group field and a custom group member field cannot have the same name.
>>
> - Click **Add Group Type** to add one group type at a time. Duplicate group types are not allowed.
> - Click **Delete** in the row of the target group type to delete it. However, you must retain at least one group type.
> ![](https://main.qcloudimg.com/raw/b529d0ca03ea819db6e619f7e93e9b1e.png)
>3. Select **I understand that after a custom group member field is added, only the read-write permissions of the added group type can be modified; the group type cannot be reselected or deleted; the field cannot be deleted.**
>4. Click **Confirm**.
>
>#### Editing a custom group field
>1. On the **Custom Group Field** page, click **Edit** in the row of the target custom group field.
>2. In the pop-up dialog box, modify the read/write permissions of existing group types, or click **Add Group Type** to add a new one and set its parameters. Duplicate group types are not allowed.
> ![](https://main.qcloudimg.com/raw/7ff1658c9fdc8d58e92e378445d1192f.png)
>3. Select **I understand that after a custom group member field is added, only the read-write permissions of the added group type can be modified; the group type cannot be reselected or deleted; the field cannot be deleted.**
>4. Click **Confirm**.
>
>### Group message configuration
>Log in to the [IM console](https://console.cloud.tencent.com/im), click the target application section, select **Feature Configuration** > **Group configuration** > **Group message configuration** on the left sidebar, and configure group messages as needed.
>
>#### Pulling message history before group join
>1. On the **Pull message history before group join** page, select a **Group Type** and click **Edit**.
>2. In the **Pull message history before group join** pop-up window, select the required configuration items.
>>?
>>- It takes about ten minutes for the configuration to take effect.
>>- Audio-video groups do not support this configuration.
>
>### Group system notification configuration
>Log in to the [IM console](https://console.cloud.tencent.com/im), click the target application section, select **Feature Configuration** > **Group configuration** > **Group system notification configuration** on the left sidebar, and configure group system notifications as needed.
>
>#### Notification of group member change
>1. On the **Notification of group member change**, select a **Group Type** and click **Edit**.
>2. In the **Notification of group member change** pop-up window, select the required configuration items.
>>?
>>- It takes about ten minutes for the configuration to take effect.
>>- Audio-video groups do not support configuring the notification of group member change.
>
>
>#### Notification of group profile change
>1. On the **Notification of group profile change** page, select a **Group Type** and click **Edit**.
>2. In the **Notification of group profile change** pop-up window, select the required configuration items.
>>?
>>- It takes about ten minutes for the configuration to take effect.
>>- Audio-video groups do not support configuring the notification of group profile change.
>
>
>#### Notification of group member profile change
>1. On the **Notification of group member profile change** page, select a **Group Type** and click **Edit**.
>2. In the **Notification of group member profile change** pop-up window, select the required configuration items.
>>?
>>- It takes about ten minutes for the configuration to take effect.
>
>### Group feature configuration
>Log in to the [IM console](https://console.cloud.tencent.com/im), click the target application section, select **Feature Configuration** > **Group configuration** > **Group feature configuration** on the left sidebar, and configure the group feature as needed.
>
>#### Community
>A community is a large group that can hold up to 100,000 users. Once a community is created, it allows users to join or leave freely and supports historical message storage. The community feature is disabled by default. Enabling it allows you to create communities and use associated features.
>
>If you need to use the topic feature, enable it after creating a community. Multiple topics can be created under the same community, and they share the same set of community member relationships. However, different topics have their own message sending and receiving independently and do not interfere with each other.
>
>>?
>>- The community feature is available only for native SDK v5.8.1668 enhanced edition or later and for web SDK v2.17.0 or later. If you are using an earlier SDK version, you need to upgrade your SDK before you can use the feature.
>>- This feature is available only for Ultimate edition users. You can [click here to upgrade](https://www.tencentcloud.com/document/product/1047/34577).
>
>#### List of online audio-video group members
>The feature of "List of online audio-video group members" is disabled by default. You can enable it as needed.
>>?
>>- If the feature is enabled, the list of the 1,000 latest online members of an audio-video group will be stored and the list can be pulled on clients. If the feature is disabled, the list cannot be pulled on clients, and only the list of the 30 latest group members can be pulled.
>>- This feature is available only for native SDK v6.3 or later. If you are using an earlier SDK version, you need to upgrade your SDK before you can use the feature.
>>- This feature is available only for Ultimate edition users. You can [click here to upgrade](https://www.tencentcloud.com/document/product/1047/34577).
>
>#### Broadcast messaging of audio-video group
>Broadcast messaging of audio-video group is disabled by default. You can enable it as needed.
>
>>?
>>- Broadcast messaging of audio-video group is disabled by default and can be enabled on native SDK v6.5 or later.
>>- Enabling this feature allows you to set the call frequency of the broadcast messaging of audio-video group, which defaults to one message per second and can be set to up to five messages per second.
>>- This feature is available only for Ultimate edition users. You can [click here to upgrade](https://www.tencentcloud.com/document/product/1047/34577).
>
>#### Audio-video group member banning
>Once this feature is enabled, audio-video group members can be banned as needed. A banned member cannot receive group messages or rejoin the group during the ban.
>>?
>>- This feature is available only for native SDK v6.6 and web SDK v2.22 or later. If you are using an earlier SDK version, you need to upgrade your SDK before you can use the feature.
>>- This feature is available only for Ultimate edition users. You can [click here to upgrade](https://www.tencentcloud.com/document/product/1047/34577).
>
>[](id:liveGroup)
>#### Message history for new members of an audio-video group
>Message history for new members is an important feature to increase the user stickiness in audio-video groups. It enables users to know what was going on before they enter an audio-video group, so they can quickly fit into interactive discussions and feel more involved. This helps deliver an highly immersive live chat experience and increase users' length of stay in live rooms.
>1. On the **Login and Message** page, click **Edit** in the upper-right corner of the **Message History for New Members** area.
>2. In the pop-up dialog box, set the number of messages viewable to new members.
>3. Click **Confirm**.
>
>
>#### Read receipts for group messages
>Group message read receipt is a must-have feature for efficient communication. As a powerful feedback tool, it allows viewing the numbers and details of members who have or have not read the sent messages. This helps teams create a more timely and efficient atmosphere of communication, especially in business and OA scenarios.
>1. On the **Login and Message** page, click **Edit** in the upper-right corner of **Read receipts for group messages**.
>2. In the pop-up **Read receipts for group messages** dialog box, set the group types that support message receipts.
>3. Click **Confirm**.
>
>>?The group message read receipt feature is **available only for Ultimate edition users**. If you are not an Ultimate edition user, you need to [upgrade](https://www.tencentcloud.com/document/product/1047/34577) before you can use the feature. The feature is supported by **native SDK v6.1.2155 or later** and is applicable to **work groups (Work)**, **public groups (Public)**, and **meeting groups (Meeting)** that support up to 200 members per group.
