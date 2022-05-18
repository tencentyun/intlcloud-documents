## Login and Message
Log in to the [IM console](https://console.cloud.tencent.com/im), click the target app card, and select **Feature Configuration** > **Login and Message** on the left sidebar. You can manage login and message related settings according to your business needs.

### Login settings
1. On the **Login and Message** page, click **Edit** in the upper-right corner of the **Login Settings** area.
2. In the pop-up dialog box, select a multi-platform login policy and set the maximum number of concurrent online web instances.
<dx-alert infotype="explain" title="">
If you select multi-platform login for the Flagship Edition, up to 10 concurrent online web clients are supported, and up to 3 online devices are supported for Android, iPhone, iPad, Windows, and Mac platforms.
</dx-alert>
<img src="https://main.qcloudimg.com/raw/9774753fc2c7f4d46f47d0573404bc32.png" />
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
1. On the **Login and Message** page, click **Edit** in the upper-right corner of the **Message History for New Members** area.
2. In the pop-up dialog box, set the number of messages viewable to new members.
3. Click **Confirm**.


>?The feature of message history for new members is **available only for Flagship Edition users**. If you are not a Flagship Edition user, please upgrade your **client SDK** to **v5.9.0 or later** and your **web SDK** to **v2.16.0 or later**.

### Blocklist check
You can enable or disable **Show "Sent successfully" After Sending Messages** in the **Blocklist check** area on the **Login and Message** page.
- Enabled: if you are in the recipient’s blocklist, you will see **Sent successfully** after sending a one-to-one message and the recipient will not receive the message. This is the default setting.
- Disabled: if you are in the recipient’s blocklist, you will see **Failed to send** after sending a one-to-one message.

### Relationship check
You can enable or disable **Check Relationship for One-to-One Messages** in the **Relationship Check** area on the **Login and Message** page.
- Enabled: check relationships before a one-to-one chat starts and only allow sending one-to-one messages to friends. When a user sends a one-to-one message to a stranger, the SDK will receive [error code 20009](https://intl.cloud.tencent.com/document/product/1047/34348).
- Disabled: do not check relationships before a one-to-one chat starts and allow users to send and receive one-to-one messages to and from friends and strangers. This is the default setting.

### Configuring group message read receipts
1. On the **Login and Message** page, click **Edit** in the upper-right corner of the **Group Message Read Receipts** area.
2. In the pop-up **Group Message Read Receipts** dialog box, set the group types that support message receipts.
3. Click **Confirm**.
>?The group message read receipt feature is **available only to Flagship Edition users**. If you are not a Flagship Edition user, please upgrade your package to the Flagship Edition package. The feature is supported by **native SDK v6.1.2155 or later** and is applicable to **work groups (Work)**, **public groups (Public)**, and **meeting groups (Meeting)** that support up to 200 members per group.

### Multi-client synchronization settings

You can enable or disable **Sync Conversation Deletion Across Clients** in the **Multi-client Synchronization Settings** area on the **Login and Message** page.
- Enabled: if multiple clients are online concurrently, deleting a conversation from one client will be synced to other clients (that is, the conversation will also be deleted from other clients).
- Disabled: if multiple clients are online concurrently, deleting a conversation from one client will not be synced to other clients. The feature of syncing conversation deletion across clients is disabled by default.
>?The feature of syncing conversation deletion across clients is available only to **native SDK v5.1.1 and web SDK v2.14.0 or later**. If you are using an earlier SDK version, you need to **upgrade your SDK** before you can use the feature.

### Configuration of the number of recent contacts to pull
In the **Configuration of Recent Contacts to Pull** area on the **Login and Message** page, you can configure the number of recent contacts to be pulled from the cloud. The default number is 100, and you can change the number to up to 500.
>?
>- The feature of configuring the number of recent contacts to pull is available only to **Flagship Edition** users. If you are not a Flagship Edition user, you need to upgrade your package to the Flagship Edition package before you can use the feature.
>- The feature of configuring the number of recent contacts to pull is available only to **native SDK v5.1.1 and web SDK v2.0 or later**. If you are using an earlier SDK version, you need to upgrade your SDK before you can use the feature.

## Friends and Relationship Chain
Setting verification method for adding friends and custom friend fields.
### Verification method for adding friends
1. Log in to the [IM console](https://console.cloud.tencent.com/im) and click the target IM app card.
2. On the left sidebar, choose **Feature Configuration** > **Friend and Relationship**, and click **Edit** in the upper-right corner of the **Default Verification for Adding Friends** area.
![](https://qcloudimg.tencent-cloud.cn/raw/6d5a4de703ec20c4a337c1e504f95de8.png)
3. Select a verification method as needed and click **Confirm**.

### Custom friend fields
>?You can add up to 20 custom friend fields, which cannot be deleted and whose field name and type cannot be modified. Please set the fields properly as needed.

1. Log in to the [IM console](https://console.cloud.tencent.com/im) and click the target IM app card.
2. On the left sidebar, choose **Feature Configuration** > **Friend and Relationship**.
3. Click **Add** in the upper-right corner of the **Custom Friend Fields** area.
4. In the pop-up dialog box, enter a field name and select a field type.

<dx-alert infotype="explain" title="">
The field name must be all letters and cannot exceed eight characters.
</dx-alert>

## Custom User Fields
Log in to the [IM console](https://console.cloud.tencent.com/im), click the target app card, and select **Feature Configuration** > **Custom User Field** on the left sidebar. You can manage custom user fields according to your business needs.
>!You can add up to 20 custom user fields, which cannot be deleted and whose field name and type cannot be modified. Please set the fields properly as needed.

### Adding a custom user field

1. On the **Custom User Field** page, click **Add** in the upper-right corner.
2. In the pop-up dialog box, enter a field name, select a field type, and set read/write permissions.
<dx-alert infotype="explain" title="">
 - The field name must be all letters and cannot exceed eight characters.
 - You need to enable at least one read permission and one read permission
</dx-alert>

![](https://main.qcloudimg.com/raw/95851bca861f45aed20c045a8d09928e.png)
3. Click **Confirm**.

### Modifying the permissions of a custom user field
1. On the **Custom User Field** page, click **Change Permissions** in the row of the target field.
2. In the pop-up dialog box, change the read or write permission.
![](https://main.qcloudimg.com/raw/01081d71fe7ec45b470a249d685696c1.png)
3. Click **Confirm**.

 ![](https://main.qcloudimg.com/raw/271b68191ae3b1acb28fcbb4f7fea63e.png)
4. Click **Confirm**.

## Custom Group Member Fields
Log in to the [IM console](https://console.cloud.tencent.com/im), click the target app card, and select **Feature Configuration** > **Custom Group Member Field** on the left sidebar. You can manage custom group member fields according to your business needs.
>!You can add up to five custom group member fields, which cannot be deleted and whose group type and read/write permissions can be changed. Please set the fields properly as needed.

### Adding a custom group member field
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

### Editing a custom group member field
1. On the **Custom Group Member Field** page, click **Edit** in the row of the target custom group member field.
2. In the pop-up dialog box, modify the read and write permissions of existing group types, or click **Add Group Type** to add a new one and set its parameters. Duplicate group types are not allowed.
 ![](https://main.qcloudimg.com/raw/19532e3441d0de3a1b7c29e2fd0b4a4a.png)
3. Select **I understand that after a custom group member field is added, only the read-write permissions of the added group type can be modified; the group type cannot be reselected or deleted; the field cannot be deleted.**
4. Click **Confirm**.


## Custom Group Fields
Log in to the [IM console](https://console.cloud.tencent.com/im), click the target app card, and select **Feature Configuration** > **Custom Group Field** on the left sidebar. You can manage custom group fields according to your business needs.
>!You can add up to five custom group fields. Once set, these fields cannot be deleted, and only the group types and the corresponding read and write permissions can be modified. Therefore, set these fields properly as needed.

### Adding a custom group field
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

### Editing a custom group field
1. On the **Custom Group Field** page, click **Edit** in the row of the target custom group field.
2. In the pop-up dialog box, modify the read/write permissions of existing group types, or click **Add Group Type** to add a new one and set its parameters. Duplicate group types are not allowed.
 ![](https://main.qcloudimg.com/raw/7ff1658c9fdc8d58e92e378445d1192f.png)
3. Select **I understand that after a custom group member field is added, only the read-write permissions of the added group type can be modified; the group type cannot be reselected or deleted; the field cannot be deleted.**
4. Click **Confirm**.

