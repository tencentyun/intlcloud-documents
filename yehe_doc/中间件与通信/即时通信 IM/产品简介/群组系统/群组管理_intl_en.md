Based on common use cases, Instant Messaging (IM) supports the following group types by default: work group (Work), public group (Public), meeting group (Meeting), and audio-video chat room (AVChatRoom). For more information, see [Group Types](https://intl.cloud.tencent.com/document/product/1047/33529).

You can perform the following operations on groups:

| Group Operation | Description | Notes |
| -------- | -------------- | ---------------- |
| Create a group | This operation creates a new group. You can specify the group type, name, and a list of users to add to the group. After the group is created, the group ID is returned, which uniquely identifies the group and is used to send and receive messages. | The daily limit of net group consumption is 10,000 per app. |
| Transfer a group | This operation changes the group owner. | The app admin can transfer a group through the RESTful API. The only other role that can transfer a group is the group owner. |
| Disband a group | This operation disbands a group that has been created on the app. When the group is disbanded, all group members receive a system message stating that the group has been disbanded. | App admin can call the RESTful API to disband any group. The permission to disband groups on the app is limited by member roles:<br>For a public group, meeting group, or AVChatRoom, only the group owner can disband the group.<br>For a work group, no one in the group can disband the group. |

>!
> - When you create a group, IM assigns a default group ID that begins with @TGS#. You can also specify a group ID. For more information, see [Custom Group IDs](https://intl.cloud.tencent.com/document/product/1047/33529).
> - After the group is created, a system message about the group creation is sent to the group owner's device to ensure synchronization across multiple devices (once a group is created on 1 device, all devices instantly perceive the created group.)



### Group Profile Management

The group profile includes properties that are specific to a single group, such as the group name, overview, announcement, and group owner, as well as custom group fields.

| Group Profile Management | Description | Notes |
| ------------ | ---------------------- | ------------- |
| Obtain the group profile | Pull basic group information. If you want to pull custom information, configure APIs for the custom fields that you want to pull. | **Group members obtain the group profile**: group members can obtain the group profile.<br>**Non-members obtain the group profile**: non-members can only obtain the group profile that has been made public.<br>**Obtain the personal profile in the group**: users can obtain their own profiles in all groups, or in a single group.<br>**Obtain the profile of a group member**: in an AVChatRoom, only some members' profiles are available, including the group owner, admins, and some group members. |
| Modify the group profile | You can modify the group name, introduction, announcement, profile photo, group name card, membership application option, group-level custom fields, roles of group members, member-level custom fields, and group message receiving options. | Currently, you can configure callbacks for group name, introduction, announcement, and profile photo URL changes for the app in the console. To enable callbacks for changes in other group information, including group-level custom fields, [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=29&level2_id=40&source=0&data_title=%E4%BA%91%E9%80%9A%E4%BF%A1%20%20IM&step=1). |



### Group Member/Group Management

Group member management involves 2 aspects:
- Obtain and modify personal information in the group. This information can be obtained and set only by users themselves, for example, message receiving options.
- Obtain and modify other group members' information, including the role, joining time, time of the last message, group name card, and member-level custom information.

| Group Member Management | Description | Notes |
| --------------------- | ------------------- | -------------------- |
| Obtain group member information | Obtain personal information or other group members' information. | Available information includes role, joining time, time of last message, group name card, and member-level custom information. |
| Modify a group member's profile | The group owner, admins, and members can modify group member profiles. | <ul style="margin:0;"><li>The group owner and admins can modify the profiles of other group members, including modifying roles of members (setting or canceling admins), muting members, and modifying the group name card and member-level custom fields.</li><li>Group members can modify their personal profiles in the group, including the message receiving options, group name card, and member-level custom fields.</li></ul> |
| Invite to a group | Add non-members to a group. | <ul style="margin:0;"><li>For a work group, any group member can invite non-members to the group, and invitees are added to the group without confirmation.</li><li>For a public group or meeting group, only the app admin can invite non-members to the group by default.</li><li>For an AVChatRoom, no member can invite others to the group.</li></ul> |
| Apply to join a group | A user proactively applies to join a group through the IM SDK. | <ul style="margin:0;"><li>Work groups disallow non-members to join, and an error will be returned.</li><li>For other built-in group types, the result of the membership application depends on the `ApplyJoinOption` field in the group profile.</li></ul> |
| Delete a group member | The group owner or a group admin removes a group member from the group. | When a group member is removed from the group by the group owner or a group admin, the member receives a system message announcing the removal, and other members in the group also receive an event message about the removal. |
| Quit a group | A group member initiates the quit operation. | When a group member quits the group, the leaving member receives a system message stating that he or she has left the group, and other members in the group also receive an event message about the member quitting the group. |
| Obtain the list of groups a user has joined | Pull the list of groups that the current user has joined. The returned result contains only part of the basic information. | To obtain detailed group information, use the **group members obtain the group profile** feature. |
| List of pending group messages | A group's pending messages include all group operations that require approval. | You can pull the list of pending group messages, report pending read messages, and process pending group messages (approve or reject). |

