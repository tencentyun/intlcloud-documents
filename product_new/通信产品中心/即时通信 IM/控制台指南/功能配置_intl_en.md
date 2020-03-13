## Login and Messages
Log in to [IM Console](https://console.cloud.tencent.com/im) and click the target app card. In the left sidebar, choose **Feature Configuration** > **Login and Messages**. On the page that appears, you can manage login and message configuration according to your business needs.

### Login settings
1. On the **Login and Messages** page, click **Edit** for **Login settings**.
2. In the "Login Settings" dialog that appears, select multi-client login and set the number of concurrent online web instances.

3. Click **OK** to save the settings.

### Setting the retention period of historical messages
Historical messages are retained for 7 days by default. **Increasing the retention period of historical messages is a value-added service**. For more information on billing, see [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350). You can modify the setting once every calendar month.

1. On the **Login and Messages** page, click **Edit** for **Historical message retention period settings**.
2. In the "Historical Message Retention Period Settings" dialog that appears, increase the retention period.
3. Click **OK** to save the setting, which takes effect immediately.

### Message recall settings
1. On the **Login and Messages** page, click **Edit** for **Message recall settings**.
2. In the "Message Recall Settings" dialog that appears, set the message recallable period.
3. Click **OK** to save the setting.

### Blacklist check
You can enable or disable "Show "sent the message" after sending message" in the **Blacklist Check** area on the **Login and Messages** page.
- On: if you are in the recipient’s blacklist, you will see "sent the message" after sending a one-to-one chat message and the recipient will not receive the message. This is the default setting.
- Off: if you are in the recipient’s blacklist, you will see "failed to send the message" after sending a one-to-one chat message.

### Friend relationship check
You can enable or disable "Check relationship chain before sending one-to-one chat messages" in the **Friend relationship check** area on the **Login and Messages** page.
- On: check friend relationships before a one-to-one chat starts and only allow friends to send one-to-one messages. When a stranger sends a one-to-one chat message, the SDK will receive [error code 20009](https://intl.cloud.tencent.com/document/product/1047/34348#.E6.B6.88.E6.81.AF.E9.94.99.E8.AF.AF.E7.A0.812).
- Off: do not check friend relationships before a one-to-one chat starts and allow users to send and receive one-to-one chat messages to and from friends and strangers. This is the default setting.

## User Custom Fields
Log in to [IM Console](https://console.cloud.tencent.com/im) and click the target app card. In the left sidebar, choose **Feature Configuration** > **User Custom Fields**. On the page that appears, you can manage user custom fields according to your business needs.
>You can add up to 20 user custom fields. Once set, these fields cannot be deleted, and their names and types cannot be modified. Therefore, plan these fields with caution according to your business needs.

### Adding user custom fields

1. On the **User Custom Fields** page, click **Add user custom field**.
2. In the "User Custom Field" dialog that appears, enter a name for the custom field and set the field type and read and write permissions.
 >
 >- The field name must consist of letters with a maximum length of 8 characters.
 >- You must set at least one read permission and one write permission.
 >

3. Click **OK** to save the settings.

### Modifying the permissions of a user custom field
1. On the **Login and Messages** page, click **Modify permissions** in the row of the target custom field.
2. In the "User Custom Field" dialog that appears, modify the read and write permissions.

3. Click **OK** to save the settings.

## Friend Custom Fields
>You can add up to 20 friend custom fields. Once set, these fields cannot be deleted, and their names and types cannot be modified. Therefore, plan these fields with caution according to your business needs.

1. Log in to [IM Console](https://console.cloud.tencent.com/im) and click the target app card.
2. In the left sidebar, choose **Feature Configuration** > **Friend Custom Fields**.
3. Click **Add friend custom fields**.
4. In the "Friend Custom Field" dialog that appears, enter a name for the custom field and set the field type.
 >The field name must consist of letters with a maximum length of 8 characters.
 >

5. Click **OK** to save the settings.

## Group Member Custom Fields
Log in to [IM Console](https://console.cloud.tencent.com/im) and click the target app card. In the left sidebar, choose **Feature Configuration** > **Group Member Custom Fields**. On the page that appears, you can manage group member custom fields according to your business needs.
>You can add up to 5 group member custom fields. Once set, these fields cannot be deleted, and only the group type and the corresponding read and write permissions can be modified. Therefore, plan these fields with caution according to your business needs.

### Adding group member custom fields
1. On the **Group Member Custom Fields** page, click **Add group member custom field**.
2. In the "Group Member Custom Field" dialog that appears, enter a name for the custom field and set the group type and read and write permissions.
  >
  >- The field name can only contain letters, numbers, and underscores (\_), and cannot begin with a number. The maximum length of the name is 16 characters.
  >- A group member custom field and a group custom field cannot have the same name.
  >
 - Click **Add group type** to add one group type at a time. Duplicate group types are not allowed.
 - Click **Delete** in the row of the target group type parameter to delete it. However, you must retain at least one group type parameter.

3. Select **I understand that once added, custom fields and group types cannot be deleted and only the read and write permissions of group types can be modified.**
4. Click **OK** to save the setting.

### Editing group member custom fields
1. On the **Group Member Custom Fields** page, click **Edit** in the row of the target group member custom field.
2. In the "Group Member Custom Field" dialog that appears, modify the read and write permissions of the selected group type, or click **Add group type** to add a group type and set its parameters. Duplicate group types are not allowed.

3. Select **I understand that once added, custom fields and group types cannot be deleted and only the read and write permissions of group types can be modified.**
4. Click **OK** to save the setting.


## Group Custom Fields
Log in to [IM Console](https://console.cloud.tencent.com/im) and click the target app card. In the left sidebar, choose **Feature Configuration** > **Group Custom Fields**. On the page that appears, you can manage group custom fields according to your business needs.
>You can add up to 5 group custom fields. Once set, these fields cannot be deleted, and only the group type and the corresponding read and write permissions can be modified. Therefore, plan these fields with caution according to your business needs.

### Adding group custom fields
1. On the **Group Custom Fields** page, click **Add group custom fields**.
2. In the "Group Custom Field" dialog that appears, enter a name for the custom field and set the group type and read and write permissions.
  >
  >- The field name can only contain letters, numbers, and underscores (\_), and cannot begin with a number. The maximum length of the name is 16 characters.
  >- A group custom field and a group member custom field cannot have the same name.
  >
 - Click **Add group type** to add one group type at a time. Duplicate group types are not allowed.
 - Click **Delete** in the row of the target group type parameter to delete it. However, you must retain at least one group type parameter.

3. Select **I understand that once added, custom fields and group types cannot be deleted and only the read and write permissions of group types can be modified.**
4. Click **OK** to save the setting.

### Editing group custom fields
1. On the **Group Custom Fields** page, click **Edit** in the row of the target group custom field.
2. In the "Group Custom Field" dialog, modify the read and write permissions of the selected group type, or click **Add group type** to add a group type and set its parameters. Duplicate group types are not allowed.

3. Select **I understand that once added, custom fields and group types cannot be deleted and only the read and write permissions of group types can be modified.**
4. Click **OK** to save the setting.
