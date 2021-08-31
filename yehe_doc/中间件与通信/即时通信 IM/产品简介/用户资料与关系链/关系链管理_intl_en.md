## Introduction to the Relationship Chain System

Instant Messaging (IM) can host user relationship chains and offers a complete set of relationship chain solutions. If you do not want to develop or maintain friend relationships for your app users but need features like adding and deleting friends, then you should use IM's relationship chain hosting service.

- IM can store relationship chains, ensuring that your data has remote disaster recovery, multi-region deployment, and auto-scaling capabilities. This frees you from complex processing flows, such as server downtime, multi-copy primary-secondary replication, and scaling.
- IM provides business processing flows that are commonly used in the industry, with which you do not have to worry about relationship chain logic.
- IM provides professional operation processes and teams, ensuring 99.99% annual service quality stability and helping you offer services known for their stability.
- IM provides easy-to-use service APIs and easy-to-access guidelines, with premium services throughout the whole process.

A relationship chain is a set of data used to describe the relationships between one user and other users. The relationship chains supported by IM include friend lists and blocklists.

## Relationship Chain Fields[](id:relationship)
The IM relationship chain system supports standard and custom relationship chain fields. Relationship chain fields have the following features:

- Relationship chain fields are displayed in key-value format.
- Key is in string format, and its name can only contain uppercase and lowercase letters, numbers, and underscores.
- Value has the following types:
 a. An integer of uint64_t type (not supported for custom relationship chain fields)
 b. A string of string type (string length cannot exceed 500 bytes.)
 c. A buffer of bytes type (buffer length cannot exceed 500 bytes.)
 d. A string array of string type (the length of each string cannot exceed 500 bytes, and this type is used only for the `Tag_SNS_IM_Group` field of a friend list.)

## Friend Lists
Users can add up to 3,000 friends to their friend lists in IM.
Friend lists support standard friend fields and custom friend fields.

### Standard friend fields
Currently, IM supports the following standard friend fields:

| Field | Type | Description |
|---------|---------|---------|
| Tag_SNS_IM_Group | Array | Friend list:<br />1. A maximum of 32 lists are supported.<br />2. The list name cannot be empty.<br />3. The length of a list name cannot exceed 30 bytes.<br />4. One friend can be added to multiple different lists. |
| Tag_SNS_IM_Remark | String | Remark:<br />1. The length of a remark cannot exceed 96 bytes. |
| Tag_SNS_IM_AddSource | String | Source from which a friend is added:<br />1. The source field contains a prefix and keyword.<br />2. The prefix of the source field is `AddSource_Type_`.<br />3. Keyword: must be a combination of letters with a length no more than 8 bytes. You are advised to use an English word or its abbreviation.<br />4. Example: if the source keyword is Android, the source field is `AddSource_Type_Android`.<br /> |
| Tag_SNS_IM_AddWording | String | Request content:<br />1. The length of a request cannot exceed 256 bytes.<br /> |


### Custom friend fields

Custom friend fields are the friend data set by each app based on its own business needs. By using custom friend fields, an app can add additional data to friends and perform read and write operations through existing APIs.
To apply for custom friend fields, the app admin can log in to the [IM console](https://console.cloud.tencent.com/im) and choose **App Configuration** > **Feature Configuration**. After the application is submitted, custom friend fields will take effect in 5 minutes.

The naming requirements for custom friend fields are as follows:
- The name of a custom friend field has two parts: prefix and keyword.
- The prefix of a custom friend field is `Tag_SNS_Custom`.
- Keyword: the keyword must be a string of letters with a length no more than 8 bytes. You are advised to use an English word or its abbreviation as the keyword.
- Example: if the custom friend field to be applied for by an app has the keyword `Test`, the name of the custom friend field is `Tag_SNS_Custom_Test`.

When applying for custom friend fields, you need to submit the following information for each custom friend field:
- The name of the custom friend field (Key).
- The type of the custom friend field (Value). For more information, see [Relationship Chain Fields](#relationship).



### Adding friends

IM supports the following modes for adding friends: adding friends in batches, no approval required, and approval required. For more information, see <a href="https://intl.cloud.tencent.com/document/product/1047/34902">Adding Friends</a>.

Two-way friends: user A's friend list contains user B, and user B's friend list contains user A.
One-way friend: user A's friend list contains user B, but user B's friend list does not contain user A.
Verification method for adding friends: each user can choose the way with which he/she is added as a friend by another user. For more information, see the verification method field for adding friends in <a href="https://intl.cloud.tencent.com/document/product/1047/33520">Standard Profile Fields</a>.
No approval required: if the approval method for friend requests set by account A is `AllowType_Type_AllowAny`, then anyone who wants to add account A as a friend can directly add it. In this scenario, the friend request and acceptance process has one step.
Approval required: if the approval method for friend requests set by account A is `AllowType_Type_NeedConfirm`, then for anyone who wants to add account A as a friend, account A will receive a message asking it to approve the new friend request. Then, account A accepts or rejects the request to complete the process. In this scenario, the friend request and acceptance process has two steps.

### Deleting friends
IM supports two modes for deleting friends: one-way deletion and two-way deletion.


| Deletion Mode | DeleteType | Description |
|---------|---------|---------|
| One-way deletion | Delete_Type_Single | `To_Account` is deleted from the friend list of `From_Account`, but `From_Account` is not deleted from the friend list of `To_Account`. |
| Two-way deletion | Delete_Type_Both | `To_Account` is deleted from the friend list of `From_Account`, and `From_Account` is deleted from the friend list of `To_Account`. |


IM also supports deleting friends in batches. For more information, see <a href="https://intl.cloud.tencent.com/document/product/1047/34905">Deleting Friends</a>.


### Verifying friends

IM supports two friend verification modes: one-way friend verification and two-way friend verification.

| Verification Mode | CheckType | Description |
|---------|---------|---------|
| One-way friend verification | CheckResult_Type_Single | This is used to check whether `To_Account` is in the friend list of `From_Account`, but does not check whether `From_Account` is in the friend list of `To_Account`. |
| Two-way friend verification | CheckResult_Type_Both |This is used to check whether `To_Account` is in the friend list of `From_Account` and also whether `From_Account` is in the friend list of `To_Account`. |


Possible results of one-way friend verification are:

| Relation | Description |
|---------|---------|
| CheckResult_Type_NoRelation | `To_Account` is not in the friend list of `From_Account`, but it cannot determine whether `From_Account` is in the friend list of `To_Account`. |
| CheckResult_Type_AWithB | `To_Account` is in the friend list of `From_Account`, but it cannot determine whether `From_Account` is in the friend list of `To_Account`. |


Possible results of two-way friend verification are:

| Relation | Description |
|---------|---------|
| CheckResult_Type_BothWay | `To_Account` is in the friend list of `From_Account`, and `From_Account` is in the friend list of `To_Account`. |
| CheckResult_Type_AWithB | `To_Account` is in the friend list of `From_Account`, but `From_Account` is not in the friend list of `To_Account`. |
| CheckResult_Type_BWithA | `To_Account` is not in the friend list of `From_Account`, but `From_Account` is in the friend list of `To_Account`. |
| CheckResult_Type_NoRelation | `To_Account` is not in the friend list of `From_Account`, and `From_Account` is not in the friend list of `To_Account`. |

For more information on friend verification, see <a href="https://intl.cloud.tencent.com/document/product/1047/34907">Verifying Friends</a>.

## Blocklists
Each user has a blocklist, which is used to store the accounts blocked by this user.
After user A adds user B to the blocklist, user A will unfriend user B (if they are friends), and users A and B cannot send friend requests to each other in the future.
Each user can add up to 1,000 accounts to their IM blocklist.

### Adding users to the blocklist
IM allows you to add users to the blocklist in batches. For more information, see <a href="https://intl.cloud.tencent.com/document/product/1047/34911">Blocklisting Users</a>.

### Removing users from the blocklist
IM allows you to remove users from the blocklist in batches. For more information, see <a href="https://intl.cloud.tencent.com/document/product/1047/34912">Unblocklisting Users</a>.

### Pulling blocklist
IM supports pulling a full blocklist by page. For more information, see <a href="https://intl.cloud.tencent.com/document/product/1047/34914">Pulling a Blocklist</a>.

### Verifying blocklist
IM supports two blocklist verification modes: one-way verification and two-way verification.


| Verification Mode | CheckType | Description |
|---------|---------|---------|
| One-way verification | BlackCheckResult_Type_Single | This is used to check whether `To_Account` is in the blocklist of `From_Account`, but does not check whether `From_Account` is in the blocklist of `To_Account`. |
| Two-way verification | BlackCheckResult_Type_Both | This is used not only to check whether `To_Account` is in the blocklist of `From_Account`, but also to check whether `From_Account` is in the blocklist of `To_Account`. |

Possible results of one-way blocklist relationship verification are:

| Relation | Description |
|---------|---------|
| BlackCheckResult_Type_AWithB | `To_Account` is in the blocklist of `From_Account`, but it cannot determine whether `From_Account` is in the blocklist of `To_Account`. |
| BlackCheckResult_Type_NO | `To_Account` is not in the blocklist of `From_Account`, but it cannot determine whether `From_Account` is in the blocklist of `To_Account`. |

Possible results of two-way blocklist relationship verification are:

| Relation | Description |
|---------|---------|
| BlackCheckResult_Type_BothWay | `To_Account` is in the blocklist of `From_Account`, and `From_Account` is also in the blocklist of `To_Account`. |
| BlackCheckResult_Type_AWithB | `To_Account` is in the blocklist of `From_Account`, but `From_Account` is not in the blocklist of `To_Account`. |
| BlackCheckResult_Type_BWithA | `To_Account` is not in the blocklist of `From_Account`, but `From_Account` is in the blocklist of `To_Account`. |
| BlackCheckResult_Type_NO | `To_Account` is not in the blocklist of `From_Account`, and `From_Account` is not in the blocklist of `To_Account`. |

For more information on blocklist verification, see <a href="https://intl.cloud.tencent.com/document/product/1047/34913">Verifying Blocklist</a>.


## Relevant Document

- [User Profile and Relationship Chain (Android)](https://intl.cloud.tencent.com/document/product/1047/34332)
- [User Profile and Relationship Chain (iOS)](https://intl.cloud.tencent.com/document/product/1047/36284)
- [Overview (Windows)](https://intl.cloud.tencent.com/document/product/1047/34304)
- [User Profile (Web & Mini Program)](https://intl.cloud.tencent.com/document/product/1047/34334)


