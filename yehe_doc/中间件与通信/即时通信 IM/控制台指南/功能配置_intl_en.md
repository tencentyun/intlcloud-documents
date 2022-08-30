## Login and Message
Log in to the [IM console](https://console.cloud.tencent.com/im), click the target app section, and select **Feature Configuration** > **Login and Message** on the left sidebar. You can manage login and message related settings according to your business needs.

### Login settings
1. On the **Login and Message** page, click **Edit** in the upper-right corner of the **Login Settings** area.
2. In the pop-up dialog box, select a multi-device login policy and set the maximum number of concurrent online web instances.
<dx-alert infotype="explain" title="">
If you select multi-platform login for the Ultimate edition, a user can be concurrently online on up to ten clients on the web platform or on up to three clients on the Android, iPhone, iPad, Windows, macOS, or Linux platform.
</dx-alert>
<img src="https://qcloudimg.tencent-cloud.cn/raw/d8473433163172dc01e896580701f79b.png" />
3. Click **Confirm**.

### Historical message storage period settings
Historical messages are stored for seven days by default. **Extending the storage period is a value-added service.** For more information on billing, see [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350). You can modify the storage period once every month.

1. On the **Login and Message** page, click **Edit** in the upper-right corner of the **Historical Message Storage Period Settings** area.
2. In the pop-up dialog box, extend the storage period of historical messages.
3. Click **Confirm** and the configuration will take effect immediately.

### Message recall settings
1. On the **Login and Message** page, click **Edit** in the upper-right corner of the **Message Recall Settings** area.
2. In the pop-up dialog box, set the time limit for message recall.
3. Click **Confirm**.

[](id:liveGroup)
### Message history for new members of an audio-video group
Message history for new members is an important feature to increase the user stickiness in audio-video groups. It enables users to know what was going on before they enter an audio-video group, so they can quickly fit into interactive discussions and feel more involved. This helps deliver an highly immersive live chat experience and increase users' length of stay in live rooms.
1. On the **Login and Message** page, click **Edit** in the upper-right corner of the **Message History for New Members** area.
2. In the pop-up dialog box, set the number of messages viewable to new members.
3. Click **Confirm**.


>?This feature is **available only for the Ultimate edition**. To use it, purchase the Ultimate edition as instructed in [Creating and Upgrading an Application](https://www.tencentcloud.com/document/product/1047/34577). For more information, see [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350?from=17178#.E5.9F.BA.E7.A1.80.E6.9C.8D.E5.8A.A1.E8.AF.A6.E6.83.85). To ensure the proper use of this feature, upgrade the **native SDK** to **v5.9.0 or later** and the **web SDK** to **v2.16.0 or later**.


### Blocklist check
You can enable or disable **Show "Sent successfully" After Sending Messages** in the **Blocklist check** area on the **Login and Message** page.
- Enabled: If you are in the recipient's blocklist, you will see **Sent successfully** after sending a one-to-one message and the recipient will not receive the message. This is the default setting.
- Disabled: If you are in the recipient's blocklist, you will see **Failed to send** after sending a one-to-one message

### Relationship check
You can enable or disable **Check Relationship for One-to-One Messages** in the **Relationship Check** area on the **Login and Message** page.
- Enabled: Check relationships before a one-to-one chat starts and only allow sending one-to-one messages to friends. When a user sends a one-to-one message to a stranger, the SDK will return [error code 20009](https://intl.cloud.tencent.com/document/product/1047/34348).
- Disabled: Do not check relationships before a one-to-one chat starts and allow users to send and receive one-to-one messages to and from friends and strangers. This is the default setting.

### Group message read receipt settings
Group message read receipt is a must-have feature for efficient communication. As a powerful feedback tool, it allows viewing the numbers and details of members who have or have not read the sent messages. This helps teams create a more timely and efficient atmosphere of communication, especially in business and OA scenarios.
1. On the **Login and Message** page, click **Edit** on the right of the **Group Message Read Receipts** area.
2. In the **Group Message Read Receipts** pop-up window, specify a group type for which to support message read receipts.
3. Click **Confirm**.
>?This feature is **available only for the Ultimate edition**. To use it, upgrade your application as instructed in [Creating and Upgrading an Application](https://www.tencentcloud.com/document/product/1047/34577). This feature is supported by the **native SDK on v6.1.2155 or later** and is suitable for **work groups**, **public groups**, and **meeting groups** that can accommodate up to 200 members.

### Multi-client synchronization settings

You can enable or disable **Sync Conversation Deletion Across Clients** in the **Multi-client Synchronization Settings** area on the **Login and Message** page.
- Enabled: If multiple clients are online concurrently, deleting a conversation from one client will be synced to other clients (that is, the conversation will also be deleted from other clients).
- Disabled: If multiple clients are online concurrently, deleting a conversation from one client will not be synced to other clients. The feature of syncing conversation deletion across clients is disabled by default.
>?The feature of syncing conversation deletion across clients is available only to **native SDK v5.1.1 and web SDK v2.14.0 or later**. If you are using an earlier SDK version, you need to **upgrade your SDK** before you can use the feature.

### Configuration of conversations to pull
In the **Configuration of conversations to pull** area on the **Login and Message** page, you can configure the number of conversations to be pulled from the cloud, which is `100` by default and can be changed to up to `500`.
>?
>- This feature is available only for the **Ultimate edition**. To use it, upgrade your application.
>- This feature is available only for the **native SDK on v5.1.1 or later and web SDK on v2.0 or later**. If you are using an earlier SDK version, upgrade your SDK first.

## Friends and Relationship Chain
Setting verification method for adding friends and custom friend fields.
### Verification method for adding friends
1. Log in to the [IM console](https://console.cloud.tencent.com/im) and click the target IM app section.
2. On the left sidebar, choose **Feature Configuration** > **Friend and Relationship**, and click **Edit** in the upper-right corner of the **Default Verification for Adding Friends** area.
![](https://qcloudimg.tencent-cloud.cn/raw/6d5a4de703ec20c4a337c1e504f95de8.png)
3. Select a verification method as needed and click **Confirm**.

### Custom friend fields
>?You can add up to 20 custom friend fields, which cannot be deleted and whose field name and type cannot be modified. Set the fields properly as needed.

1. Log in to the [IM console](https://console.cloud.tencent.com/im) and click the target IM app section.
2. On the left sidebar, choose **Feature Configuration** > **Friend and Relationship**.
3. Click **Add** in the upper-right corner of the **Custom Friend Field** area.
4. In the pop-up dialog box, enter a field name and select a field type.

<dx-alert infotype="explain" title="">
The field name must be all letters and cannot exceed eight characters.
</dx-alert>

## Custom User Fields
Log in to the [IM console](https://console.cloud.tencent.com/im), click the target app section, and select **Feature Configuration** > **Custom User Field** on the left sidebar. You can manage custom user fields according to your business needs.
>!You can add up to 20 custom user fields, which cannot be deleted and whose field name and type cannot be modified. Set the fields properly as needed.

### Adding a custom user field

1. On the **Custom User Field** page, click **Add** in the upper-right corner.
2. In the pop-up dialog box, enter a field name, select a field type, and set read/write permissions.
<dx-alert infotype="explain" title="">
 - The field name must be all letters and cannot exceed eight characters.
 - You need to enable at least one read permission and one write permission
</dx-alert>

![](https://main.qcloudimg.com/raw/95851bca861f45aed20c045a8d09928e.png)
3. Click **Confirm**.

### Modifying the permissions of a custom user field
1. On the **Custom User Field** page, click **Change Permissions** in the row of the target field.
2. In the pop-up dialog box, change the read or write permission.
![](https://main.qcloudimg.com/raw/01081d71fe7ec45b470a249d685696c1.png)
3. Click **Confirm**.

 ![](https://main.qcloudimg.com/raw/271b68191ae3b1acb28fcbb4f7fea63e.png)
5. Click **Confirm**.

## Group Configuration
### Custom group member fields
Log in to the [IM console](https://console.cloud.tencent.com/im), click the target app section, and select **Feature Configuration** > **Custom Group Member Field** on the left sidebar. You can manage custom group member fields according to your business needs.
>!You can add up to five custom group member fields, which cannot be deleted and whose group type and read/write permissions can be changed. Set the fields properly as needed.

#### Adding a custom group member field
1. On the **Custom Group Member Field** page, click **Add** in the upper-right corner.
2. In the pop-up dialog box, enter a field name and set group types and read/write permissions.

<dx-alert infotype="explain" title="">
- The field name can contain up to 16 characters, supporting letters, digits, and underscores (_). It cannot begin with a digit.
- A custom group member field and a custom group field cannot have the same name.
</dx-alert>


 - Click **Add Group Type** to add one group type at a time. Duplicate group types are not allowed.
 - Click **Delete** in the row of the target group type to delete it. However, you must retain at least one group type.
 ![](https://main.qcloudimg.com/raw/3b6bcff0f4156f2340f71d082a29ac45.png)
3. Select **I understand that after a custom group member field is added, only the read-write permissions of the added group type can be modified; the group type cannot be reselected or deleted; the field cannot be deleted.**
4. Click **Confirm**.

#### Editing a custom group member field
1. On the **Custom Group Member Field** page, click **Edit** in the row of the target custom group member field.
2. In the pop-up dialog box, modify the read and write permissions of existing group types, or click **Add Group Type** to add a new one and set its parameters. Duplicate group types are not allowed.
 ![](https://main.qcloudimg.com/raw/19532e3441d0de3a1b7c29e2fd0b4a4a.png)
3. Select **I understand that after a custom group member field is added, only the read-write permissions of the added group type can be modified; the group type cannot be reselected or deleted; the field cannot be deleted.**
4. Click **Confirm**.


### Custom group fields
Log in to the [IM console](https://console.cloud.tencent.com/im), click the target app card, and select **Feature Configuration** > **Custom Group Field** on the left sidebar. You can manage custom group fields according to your business needs.
>!Up to ten custom group fields can be added. These fields only support modifying the group types and the corresponding read and write permissions and cannot be deleted; therefore, set them properly as needed.

#### Adding a custom group field
1. On the **Custom Group Field** page, click **Add** in the upper-right corner.
2. In the pop-up dialog box, enter a field name and set the group types and read/write permissions.

>?
>- The field name can contain up to 16 characters, supporting letters, digits, and underscores (_). It cannot begin with a digit.
>- A custom group field and a custom group member field cannot have the same name.

 - Click **Add Group Type** to add one group type at a time. Duplicate group types are not allowed.
 - Click **Delete** in the row of the target group type to delete it. However, you must retain at least one group type.
 ![](https://main.qcloudimg.com/raw/b529d0ca03ea819db6e619f7e93e9b1e.png)
3. Select **I understand that after a custom group member field is added, only the read-write permissions of the added group type can be modified; the group type cannot be reselected or deleted; the field cannot be deleted.**
4. Click **Confirm**.

#### Editing a custom group field
1. On the **Custom Group Field** page, click **Edit** in the row of the target custom group field.
2. In the pop-up dialog box, modify the read/write permissions of existing group types, or click **Add Group Type** to add a new one and set its parameters. Duplicate group types are not allowed.
 ![](https://main.qcloudimg.com/raw/7ff1658c9fdc8d58e92e378445d1192f.png)
3. Select **I understand that after a custom group member field is added, only the read-write permissions of the added group type can be modified; the group type cannot be reselected or deleted; the field cannot be deleted.**
4. Click **Confirm**.

### Group message configuration
Log in to the [IM console](https://console.cloud.tencent.com/im), click the target application section, select **Feature Configuration** > **Group configuration** > **Group message configuration** on the left sidebar, and configure group messages as needed.

#### Pulling message history before group join
1. On the **Pull message history before group join** page, select a **Group Type** and click **Edit**.
2. In the **Pull message history before group join** pop-up window, select the required configuration items.
>?
>- It takes about ten minutes for the configuration to take effect.
>- Audio-video groups do not support this configuration.

### Group system notification configuration
Log in to the [IM console](https://console.cloud.tencent.com/im), click the target application section, select **Feature Configuration** > **Group configuration** > **Group system notification configuration** on the left sidebar, and configure group system notifications as needed.

#### Notification of group member change
1. On the **Notification of group member change**, select a **Group Type** and click **Edit**.
2. In the **Notification of group member change** pop-up window, select the required configuration items.
>?
>- It takes about ten minutes for the configuration to take effect.
>- Audio-video groups do not support configuring the notification of group member change.


#### Notification of group profile change
1. On the **Notification of group profile change** page, select a **Group Type** and click **Edit**.
2. In the **Notification of group profile change** pop-up window, select the required configuration items.
>?
>- It takes about ten minutes for the configuration to take effect.
>- Audio-video groups do not support configuring the notification of group profile change.


#### Notification of group member profile change
1. On the **Notification of group member profile change** page, select a **Group Type** and click **Edit**.
2. In the **Notification of group member profile change** pop-up window, select the required configuration items.
>?
>
>- It takes about ten minutes for the configuration to take effect.

