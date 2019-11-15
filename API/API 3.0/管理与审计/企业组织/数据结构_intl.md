## OrgInvitation

Describes the Tencent Cloud Organization invitation

Referenced by: ListOrganizationInvitations.

| Name | Type | Description |
|------|------|-------|
| Id | Integer | Invitation ID |
| Uin | Integer | UIN of the invitee |
| HostUin | Integer | UIN of the creator |
| HostName | String | Name of the creator |
| HostMail | String | Email of the creator |
| Status | Integer | Status of the invitation. -1: Expired. 0: Normal. 1: Accepted. 2: Invalid. 3: Cancelled |
| Name | String | Name |
| Remark | String | Remarks |
| OrgType | Integer | Organization type |
| InviteTime | Timestamp | Invitation time |
| ExpireTime | Timestamp | Expiration time |

## OrgMember

Describes the Tencent Cloud organization member

Referenced by: ListOrganizationMembers, ListOrganizationNodeMembers.

| Name | Type | Description |
|------|------|-------|
| Uin | Integer | UIN |
| Name | String | Name |
| Remark | String | Remarks |
| JoinTime | Timestamp | Joined date |

## OrgNode

Describes the Tencent Cloud organizational units

Referenced by: ListOrganizationNodes.

| Name | Type | Description |
|------|------|-------|
| NodeId | Integer | Organizational unit ID |
| Name | String | Name |
| ParentNodeId | Integer | Parent organizational unit ID |
| MemberCount | Integer | Number of members |

