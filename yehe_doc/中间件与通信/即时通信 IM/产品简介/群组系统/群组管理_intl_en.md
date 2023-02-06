Based on common use cases, Chat provides the following default group types: work group (Work), public group (Public), meeting group (Meeting), audio-video group (AVChatRoom), and Community group (Community). For more information, see [Group Types](https://intl.cloud.tencent.com/document/product/1047/33529).

You can perform the following operations on groups:

| Group Operation | Description | Remarks |
| -------- | -------------- | ---------------- |
| Create a group | This operation creates a new group. You can specify the group type, name, and a list of users to add to the group. After the group is created, the group ID is returned, which is the unique identifier of the group and can be used to perform other group operations such as message sending and receiving. | The daily limit of net group consumption is 10,000 per app.      |
| Transfer a group | This operation transfers a group and changes the group owner to another user. | The app admin can transfer a group through the RESTful API. The only other role that can transfer a group is the group owner. |
| Disband a group | This operation disbands a group that has been created on the app. When the group is disbanded, all group members receive a system message stating that the group has been disbanded. | The app admin can call the RESTful API to disband any group. The permission to disband a group on an app varies depending on the member role:<br>For a public group (Public), meeting group (Meeting), audio-video group (AVChatRoom), or community group (Community), only the group owner can disband the group.<br>For a work group (Work), no one in the group can disband the group. |

>!
> - When you create a group, Chat assigns a default group ID that begins with @TGS#. You can also manually specify a group ID. For more information, see [Custom Group IDs](https://intl.cloud.tencent.com/document/product/1047/33529).
- After the group is created, a system message about the group creation is sent to the group owner‘s device to ensure synchronization across multiple devices (once a group is created on one device, all devices instantly perceive the created group.)



### Group Profile Management

The group profile includes properties that are specific to a single group, such as the group name, introduction, announcement, and group owner, as well as custom group fields.

| Group Profile Management | Description | Remarks |
| ------------ | ---------------------- | ------------- |
| Get the group profile | Pull basic group information. If you want to pull custom information, configure APIs for the custom fields that you want to pull. | **Group members obtain the group profile**: Group members can obtain the group profile.<br>**Non-members obtain the group profile**: Non-members can only obtain the group profile if it is made public.<br>**Obtain the personal profile in the group**: users can obtain their own profiles in all groups, or in a single group.<br>**Obtain the profile of a group member**: An audio-video group (AVChatRoom) does not store group member information and does not support obtaining the profile of a group member. |
| Modify the group profile | You can modify the group name, introduction, announcement, profile photo, group name card, membership request options, group-level custom fields, in-group roles of members, member-level custom fields, and group message receiving options. | Currently, you can configure callbacks for group name, introduction, announcement, and profile photo URL changes for the app in the console. To enable callbacks for changes in other group information, including group-level custom fields, please [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=29&level2_id=40&source=0&data_title=%E4%BA%91%E9%80%9A%E4%BF%A1%20%20IM&step=1). |



### Group Member/Group Management

Group member management involves two aspects:
- Obtain and modify user profile in the group. This information can be obtained and set only by users themselves, for example, message receiving options.
- Obtain and modify other group members’ information, including the role, joining time, time of last message, group name card, and member-level custom information.

| Group Member Management | Description | Remarks |
| --------------------- | ------------------- | -------------------- |
| Obtain group member information | Obtain user profile or other group members’ information | Available information includes the role, joining time, time of last message, group name card, and member-level custom information. |
| Modify a group member’s profile | The group owner, admins, and members can modify group member profiles. | <ul style="margin:0;"><li>The group owner and admins can modify in-group roles (set or cancel admins), mute members, and modify the group name card and member-level custom fields.</li><li>Group members can modify their personal profiles in the group, including the message receiving options, group name card, and member-level custom fields.</li></ul> |
| Invite to a group              | Invite non-members to a group.    | <ul style="margin:0;"><li>For a work group, any group member can invite non-members to the group, and invitees are added to the group without confirmation.</li><li>For a public group or meeting group, only the app admin can invite non-members to the group by default.</li><li>For an audio-video group, no member is allowed to invite any user to the group.</li><li>For a community group, any group member can invite non-members to the group, and invitees are added to the group without confirmation.</li></ul> |
| Apply to join a group              | A user proactively applies to join a group through the Chat SDK.    | <ul style="margin:0;"><li>Work groups disallow non-members to join, and an error will be returned.</li><li>Community groups allow non-members to join without approval.</li><li>For other built-in group types, the result of the membership application depends on the `ApplyJoinOption` field in the group profile.</li></ul> |
| Delete a group member | The group owner or a group admin removes a group member from the group | When a group member is removed from the group by the group owner or a group admin, the deleted member receives a system message stating the removal, and other members in the group also receive an event message about the removal. |
| Quit a group | A group member initiates the quit operation | When a group member quits the group, the leaving member receives a system message stating that he/she has left the group, and other members in the group also receive an event message about the member quitting the group. |
| Obtain the list of groups a user has joined | Pull the list of groups that the current user has joined. The returned result contains only part of the basic information. | To obtain detailed group information, use the **group members obtain the group profile** feature. |
| List of pending group messages | A group’s pending message includes all group operations that require approval. | You can pull the list of pending group messages, report pending read messages, and process pending group messages (approve or reject). For a single user, the list of pending group messages can contain up to 50 messages. |



