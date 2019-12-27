## Introduction to the Relationship Chain System

Instant Messaging (IM) can host user relationship chains and offers a complete set of relationship chain solutions. If you do not want to develop or maintain friend relationships for your app users but need features like adding and deleting friends, then you should use IM’s relationship chain hosting service.

- IM can store relationship chains, ensuring that your data has remote disaster recovery, multi-region deployment, and auto-scaling capabilities. This frees you from complex processing flows, such as server downtime, multi-copy master-slave replication, and capacity expansion and reduction.
- IM provides business processing flows that are commonly used in the industry, with which you do not have to worry about relationship chain logic.
- IM provides professional operation processes and teams, ensuring 99.99% annual service quality stability and helping you offer services known for their stability.
- IM provides easy-to-use service APIs and easy-to-access guidelines, with premium services throughout the whole process.

A relationship chain is a set of data used to describe the relationships between one user and other users. The relationship chains supported by IM include friend lists and blacklists.

## Relationship Chain Fields
The IM relationship chain system supports standard and custom relationship chain fields. Relationship chain fields have the following features:

- Relationship chain fields are displayed in key-value format.
- Key is in String format, and its name can only contain uppercase and lowercase letters, numbers, and underscores.
- Value has the following types:
 a. An integer of uint64_t type (not supported for custom relationship chain fields).
 b. A string of string type (the length of string cannot exceed 500 bytes.)
 c. A buffer of bytes type (the length of buffer cannot exceed 500 bytes.)
 d. A string array of string type (the length of each string cannot exceed 500 bytes, and this type is used only for the `Tag_SNS_IM_Group` field of a friend list.)

## Friend Lists
Users can add up to 3,000 friends to their friend lists in IM.
Friend lists support standard friend fields and custom friend fields.

### Standard friend fields
Currently, IM supports the following standard friend fields:

| Field Name | Type | Description |
|---------|---------|---------|
| Tag_SNS_IM_Group | Array | Friend list:<br />1. A maximum of 32 lists are supported.<br />2. The list name cannot be empty.<br />3. The length of a list name cannot exceed 30 bytes.<br />4. One friend can be added to multiple different lists. |
| Tag_SNS_IM_Remark | String | Remark:<br />1. The length of a remark cannot exceed 96 bytes. |
| Tag_SNS_IM_AddSource | String | Source from which a friend is added:<br />1. The source field contains a prefix and keyword.<br />2. The prefix of the source field is AddSource_Type_<br />3. Keyword: must be a combination of letters with a length less than 8 bytes; we recommend that you use an English word or its abbreviation.<br />4. Example: if the source keyword is Android, the source field is AddSource_Type_Android.<br /> |
| Tag_SNS_IM_AddWording | String | Request content:<br />1. The length of a request cannot exceed 256 bytes.<br /> |


### Custom friend fields

Custom friend fields are the friend data set by each app based on its own business needs. By using custom friend fields, an app can add additional data to friends and perform read and write operations through existing APIs.
To apply for custom friend fields, the app admin can log in to IM [Console](https://console.cloud.tencent.com/im) and choose **App Configuration** > **Feature Configuration**. After the application is submitted, custom friend fields will take effect in 5 minutes.

The naming requirements for custom friend fields are as follows:
- The name of a custom friend field is divided into two parts: prefix and keyword.
- The prefix of a custom friend field is: Tag_SNS_Custom.
- Keyword: The keyword must be a string of letters with a length less than 8 bytes. We recommend that you use an English word or its abbreviation as the keyword.
- Example: if the custom friend field to be applied for by an app has the keyword **Test**, the name of the custom friend field is: Tag_SNS_Custom_Test.

When applying for custom friend fields, you need to submit the following information for each custom friend field:
- The name of the custom friend field (Key).
- The type of the custom friend field (Value). For more information, see <a href="https://cloud.tencent.com/document/product/269/1501#.E5.85.B3.E7.B3.BB.E9.93.BE.E5.AD.97.E6.AE.B5">Relationship Chain Fields</a>.



### Adding friends

IM supports the following modes for adding friends: adding friends in batches, no approval required, and approval required. For more information, see <a href="https://cloud.tencent.com/document/product/269/1643">Adding Friends</a>.

Two-way friends: user A's friend list contains user B, and user B's friend list contains user A.
One-way friend: user A's friend list contains user B, but user B's friend list does not contain user A.
Friend request approval method: each user can choose the way in which they are added as a friend of other users. For more information, see the approval method field for new friend requests described in <a href="https://cloud.tencent.com/document/product/269/1500#.E6.A0.87.E9.85.8D.E8.B5.84.E6.96.99.E5.AD.97.E6.AE.B5">Standard Profile Fields</a>.
No approval required: if the approval method for friend requests set by account A is AllowType_Type_AllowAny, then anyone who wants to add account A as a friend can directly add it. In this scenario, the friend request and acceptance process has one step.
Approval required: if the approval method for friend requests set by account A is AllowType_Type_NeedConfirm, then for anyone who wants to add account A as a friend, account A will receive a message asking it to approve the new friend request. Then, account A accepts or rejects the request to complete the process. In this scenario, the friend request and acceptance process has two steps.

### Deleting friends
IM supports two modes for deleting friends: one-way deletion and two-way deletion.


| Deletion Mode | DeleteType | Description |
|---------|---------|---------|
| One-way deletion | Delete_Type_Single | To_Account is deleted from the friend list of From_Account, but From_Account is not deleted from the friend list of To_Account. |
| Two-way deletion | Delete_Type_Both | To_Account is deleted from the friend list of From_Account, and From_Account is deleted from the friend list of To_Account. |


IM also supports deleting friends in batches. For more information, see <a href="https://cloud.tencent.com/document/product/269/1644">Deleting Friends</a>.

### Pulling friends
IM supports the following three modes for pulling friends: incremental pulling without friends, full pulling by page, and pulling with friends. For more information, see <a href="https://cloud.tencent.com/document/product/269/1647">Pulling Friends</a>.

### Verifying friends

IM supports two friend verification modes: one-way friend verification and two-way friend verification.

| Verification Mode | CheckType | Description |
|---------|---------|---------|
| One-way friend verification | CheckResult_Type_Single | This is used to check whether To_Account is in the friend list of From_Account, but does not check whether From_Account is in the friend list of To_Account. |
| Two-way friend verification | CheckResult_Type_Both |This is used to check whether To_Account is in the friend list of From_Account and also whether From_Account is in the friend list of To_Account. |


Possible results of one-way friend verification are:

| Relation | Description |
|---------|---------|
| CheckResult_Type_NoRelation | To_Account is not in the friend list of From_Account, but it cannot determine whether From_Account is in the friend list of To_Account. |
| CheckResult_Type_AWithB | To_Account is in the friend list of From_Account, but it cannot determine whether From_Account is in the friend list of To_Account. |


Possible results for two-way friend verification are:

| Relation | Description |
|---------|---------|
| CheckResult_Type_BothWay | To_Account is in the friend list of From_Account, and From_Account is in the friend list of To_Account. |
| CheckResult_Type_AWithB | To_Account is in the friend list of From_Account, but From_Account is not in the friend list of To_Account. |
| CheckResult_Type_BWithA | To_Account is not in the friend list of From_Account, but From_Account is in the friend list of To_Account. |
| CheckResult_Type_NoRelation | To_Account is not in the friend list of From_Account, and From_Account is not in the friend list of To_Account. |

For more information on friend verification, see <a href="https://cloud.tencent.com/document/product/269/1646">Verifying Friends</a>.

## Blacklists
Each user has a blacklist, which is used to store the accounts blocked by this user.
After user A adds user B to the blacklist, user A will unfriend user B (if they are friends), and users A and B cannot send friend requests to each other in the future.
By default, you can add up to 1,000 accounts to the IM blacklist. If you need a larger blacklist, please contact Tencent Cloud customer service.

### Blacklisting users
IM allows you to blacklist users in batches. For more information, see <a href="https://cloud.tencent.com/document/product/269/3718">Blacklisting Users</a>.

### Removing users from the blacklist
IM allows you to remove users from the blacklist in batches. For more information, see <a href="https://cloud.tencent.com/document/product/269/3719">Removing Users from the Blacklist</a>.

### Pulling blacklists
IM supports pulling a full blacklist by page. For more information, see <a href="https://cloud.tencent.com/document/product/269/3722">Pulling Blacklists</a>.

### Verifying blacklists
IM supports two blacklist verification modes: one-way verification and two-way verification.


| Verification Mode | CheckType | Description |
|---------|---------|---------|
| One-way verification | BlackCheckResult_Type_Single | This is used to check whether To_Account is in the blacklist of From_Account, but does not check whether From_Account is in the blacklist of To_Account. |
| One-way verification | BlackCheckResult_Type_Both | This is used not only to check whether To_Account is in the blacklist of From_Account, but also to check whether From_Account is in the blacklist of To_Account. |

Possible results of one-way blacklist relationship verification are:

| Relation | Description |
|---------|---------|
| BlackCheckResult_Type_AWithB | To_Account is in the blacklist of From_Account, but it cannot determine whether From_Account is in the blacklist of To_Account. |
| BlackCheckResult_Type_NO | To_Account is not in the blacklist of From_Account, but it cannot determine whether From_Account is in the blacklist of To_Account. |

Possible results of two-way blacklist relationship verification are:

| Relation | Description |
|---------|---------|
| BlackCheckResult_Type_BothWay | To_Account is in the blacklist of From_Account, and From_Account is also in the blacklist of To_Account. |
| BlackCheckResult_Type_AWithB | To_Account is in the blacklist of From_Account, but From_Account is not in the blacklist of To_Account. |
| BlackCheckResult_Type_BWithA | To_Account is not in the blacklist of From_Account, but From_Account is in the blacklist of To_Account. |
| BlackCheckResult_Type_NO | To_Account is not in the blacklist of From_Account, and From_Account is not in the blacklist of To_Account. |

For more information on blacklist verification, see <a href="https://cloud.tencent.com/document/product/269/3725">Verifying Blacklists</a>.


## Related Documentation

- [User Profiles and Relationship Chains (Android)](https://cloud.tencent.com/document/product/269/33926)
- [User Profiles and Relationship Chains (iOS)](https://cloud.tencent.com/document/product/269/33927)
- [Overview of Basic Features (Windows)](https://cloud.tencent.com/document/product/269/33490)
- [Relationship Chains (Web SDK)](https://cloud.tencent.com/document/product/269/1600)
- [System Messages - Friends (Web SDK)](https://cloud.tencent.com/document/product/269/5848)
