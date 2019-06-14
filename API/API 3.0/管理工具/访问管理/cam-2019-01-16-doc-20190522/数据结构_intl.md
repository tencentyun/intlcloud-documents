## AttachEntityOfPolicy

Information of the entity associated with a policy

Referenced by: ListEntitiesForPolicy.

| Name | Type | Description |
|------|------|-------|
| Id | String | Entity ID |
| Name | String | Entity name <br/>Note: This field may return null, indicating that no valid values can be obtained. |
| Uin | Integer | Entity uin <br/>Note: This field may return null, indicating that no valid values can be obtained. |
| RelatedType | Integer | Association type. 1: user association; 2: user group association |

## AttachPolicyInfo

Information of the associated policy

Referenced by: ListAttachedGroupPolicies, ListAttachedUserPolicies.

| Name | Type | Description |
|------|------|-------|
| PolicyId | Integer | Policy ID |
| PolicyName | String | Policy name <br/>Note: This field may return null, indicating that no valid values can be obtained. |
| AddTime | Timestamp | Creation time <br/>Note: This field may return null, indicating that no valid values can be obtained. |
| CreateMode | Integer | Source of creation. 1: created in console; 2: created by policy syntax. <br/>Note: This field may return null, indicating that no valid values can be obtained. |
| PolicyType | String | Value range: user and QCS <br/>Note: This field may return null, indicating that no effective values can be obtained. |

## GroupIdOfUidInfo

Information of the association between a sub-user and a user group

Referenced by: AddUserToGroup, RemoveUserFromGroup.

| Name | Type | Required | Description |
|------|------|----------|------|
| Uid | Integer | Yes | Sub-user UID |
| GroupId | Integer | Yes | User group ID |

## GroupInfo

User group information

Referenced by: ListGroups, ListGroupsForUser.

| Name | Type | Description |
|------|------|-------|
| GroupId | Integer | User group ID. |
| GroupName | String | Name of the user group. |
| CreateTime | String | Creation time of the user group. |
| Remark | String | Description of the user group. |

## GroupMemberInfo

User information in a user group

Referenced by: GetGroup, ListUsersForGroup.

| Name | Type | Description |
|------|------|-------|
| Uid | Integer | Sub-user UID. |
| Uin | Integer | Sub-user Uin. |
| Name | String | Sub-user name. |
| PhoneNum | String | Mobile number. |
| CountryCode | String | Country code. |
| PhoneFlag | Integer | Whether the mobile number has been verified. |
| Email | String | Email address. |
| EmailFlag | Integer | Whether the email address has been verified. |
| UserType | Integer | User type. |
| CreateTime | String | Creation time. |
| IsReceiverOwner | Integer | Whether it is the main message recipient. |

## SAMLProviderInfo

SAML identity provider

Referenced by: ListSAMLProviders.

| Name | Type | Required | Description |
|------|------|----------|------|
| Name | String | Yes | SAML identity provider name |
| Description | String | Yes | Description of the SAML identity provider |
| CreateTime | String | Yes | Creation time of the SAML identity provider |
| ModifyTime | String | Yes | Last modified time of the SAML identity provider |

## StrategyInfo

Policy information

Referenced by: ListPolicies.

| Name | Type | Description |
|------|------|-------|
| PolicyId | Integer | Policy ID. |
| PolicyName | String | Policy name. |
| AddTime | Timestamp | Creation time of the policy. <br/>Note: This field may return null, indicating that no valid values can be obtained. |
| Type | Integer | Policy type. 1: custom policy; 2: predefined policy. |
| Description | String | Policy description. <br/>Note: This field may return null, indicating that no valid values can be obtained. |
| CreateMode | Integer | Source of creation. 1: created in console; 2: created by policy syntax. |
| Attachments | Integer | Number of associated users |
| ServiceType | String | Product associated with the policy <br/>Note: This field may return null, indicating that no valid values can be obtained. |

## SubAccountInfo

Sub-user information

Referenced by: ListUsers.

| Name | Type | Description |
|------|------|-------|
| Uin | Integer | Sub-user ID |
| Name | String | Sub-user name |
| Uid | Integer | Sub-user UID |
| Remark | String | Sub-user remarks |
| ConsoleLogin | Integer | Whether the sub-user can log in to the console |
| PhoneNum | String | Mobile number |
| CountryCode | String | Country code |
| Email | String | Email address |
