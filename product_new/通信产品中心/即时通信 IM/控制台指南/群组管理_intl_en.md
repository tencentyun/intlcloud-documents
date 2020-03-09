Log in to the [IM console](https://console.cloud.tencent.com/im) and click the target app card. In the left sidebar, choose **Group Management**, and you can then manage group custom fields based on your business needs.
You can also manage groups by calling RESTful APIs. For more information, see [Group Management API Documentation](https://cloud.tencent.com/document/product/269/1613).


## Adding Groups
1. On the **Group Management** page, click **Add Group**.
2. Configure the following parameters in the "Add Group" dialog box that appears:
 - Group name: enter the name of the group. This is a required parameter with a maximum length of 30 bytes.
 - Group owner ID: enter the group owner ID. This is an optional parameter and you must enter a registered username.
 - Group type: set the group type. Supported group types are Private, Public, ChatRoom, AVChatRoom, and BChatRoom. For more information, see [Group Types](https://cloud.tencent.com/document/product/269/1502#.E7.BE.A4.E7.BB.84.E5.BD.A2.E6.80.81.E4.BB.8B.E7.BB.8D).
3. Click **OK** to save the settings.
 When group creation is completed, you can see the group ID, group name, group owner, type, and creation time in the group list.

## Viewing Group Details
On the **Group Management** page, click **View details** for the target group to go to the **Group Details** page. On this page, you can view and modify the group’s basic information and manage group members.

### Modifying basic information
1. On the **Group Details** page, click **Edit** in the basic information area.
2. In the dialog box that appears, you can modify the group name and group introduction.
 ![](https://main.qcloudimg.com/raw/8c612029f66338a63551dcdc8ac3924e.png)
3. Click **OK** to save the settings.

### Managing group members
**Add a group member**
1. On the **Group Details** page, click **Add group member** in the group member management area.
2. In the dialog box that appears, enter the username of the user to be added.
 >You must enter a registered username.
 >
![](https://main.qcloudimg.com/raw/ddcea4353e44374607d62e916536940c.png)
3. Click **OK** to save the setting.
 After the user is added, you can see the username, nickname, joining time, sending time of the last message, and role in the group member list.

**Delete a group member**
1. You can delete group members in the following ways on the **Group Details** page:
 - Single deletion: click **Delete** for the target group member.
 - Batch deletion: select all the members that you want to delete and click **Delete group members** above the group member list.
2. In the dialog box that appears, click **Confirm**.
 After deletion, the deleted users are removed from the group.

## Sending Messages
1. You can send messages in the following ways on the **Group Management** page:
 - Send the group message to one group: click **Send message** for the target group.
 - Send the group message to multiple groups: select all the target groups to which you want to send the message, and click **Send message** above the group list.
2. In the "Send Group Message" dialog box that appears, enter the content of the message.
 >The maximum length of the message is 300 words.
 >
3. Click **OK** to send the message.

## Dismissing Groups
**After a group is dismissed, all information for the group will be deleted and cannot be restored.**

1. You can dismiss groups in the following ways on the **Group Management** page:
 - Dismiss a single group: click **Dismiss** for the target group.
 - Dismiss multiple groups: select all the target groups that you want to dismiss, and click **Dismiss groups** above the group list.
2. In the dialog box that appears, click **Confirm**.
 **After a group is dismissed, all information for the group will be deleted and cannot be restored.**
