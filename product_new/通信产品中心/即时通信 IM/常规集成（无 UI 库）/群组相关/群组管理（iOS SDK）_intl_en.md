
## Group Overview

Instant Messaging (IM) supports multiple group types. For more information on their characteristics and limits, see the [Group System](https://intl.cloud.tencent.com/document/product/1047/33529). A group is identified by a unique ID, which allows for different operations.

## Group Chat Messages

Group and C2C (one-to-one) chat messages are the same except for the conversation type obtained through `Conversation`. For more information, see [Sending Messages](https://intl.cloud.tencent.com/document/product/1047/34320#.E6.B6.88.E6.81.AF.E5.8F.91.E9.80.81).

## Group Management

Group-related operations are performed after login through `TIMGroupManager`.

**Prototype for obtaining a singleton:**

```
@interface TIMGroupManager : NSObject
+ (TIMGroupManager*)sharedInstance;
@end
```

### Creating built-in group types

IM supports the following group types by default: private group (Private), public group (Public), chat room (ChatRoom), audio-and-video chat room (AVChatRoom), and broadcasting chat room (BChatRoom). For more information, see [Group Types](https://intl.cloud.tencent.com/document/product/1047/33529#.E7.BE.A4.E7.BB.84.E5.BD.A2.E6.80.81.E4.BB.8B.E7.BB.8D). You can specify the group name and the list of users to be added. After the group is created, the group ID is returned, which allows you to receive and send messages through `Conversation`.

**Description of group creation:**

| Method | Description |
| --- | --- |
| CreatePrivateGroup | Create a private group |
| CreatePublicGroup | Create a public group |
| CreateChatRoomGroup | Create a chat room |
| CreateAVChatRoomGroup | Creates a live-streaming group. A live-streaming group supports an unlimited number of members, but does not support features such as adding members or querying the total number of members. |

**Prototype:**

```
@interface TIMGroupManager : NSObject
/**
 *  Create a private group
 *
 *  @param members Group members, which is an NSString* array
 *  @param groupName Group name
 *  @param succ Success callback
 *  @param fail Failure callback
 *
 *  @return 0 Succeeded
 */
- (int)createPrivateGroup:(NSArray*)members groupName:(NSString*)groupName succ:(TIMCreateGroupSucc)succ fail:(TIMFail)fail;
/**
 *  Create a public group
 *
 *  @param members Group members, which is an NSString* array
 *  @param groupName Group name
 *  @param succ Success callback
 *  @param fail Failure callback
 *
 *  @return 0 Succeeded
 */
- (int)createPublicGroup:(NSArray*)members groupName:(NSString*)groupName succ:(TIMCreateGroupSucc)succ fail:(TIMFail)fail;
/**
 *  Create a chat room
 *
 *  @param members  Group members, which is an NSString* array
 *  @param groupName Group name
 *  @param succ Success callback
 *  @param fail Failure callback
 *
 *  @return 0 Succeeded
 */
- (int)createChatRoomGroup:(NSArray*)members groupName:(NSString*)groupName succ:(TIMCreateGroupSucc)succ fail:(TIMFail)fail;
/**
 *  Create an audio-and-video chat room (ultra-large groups are supported; see Wiki documentation for details)
 *
 *  @param groupName Group name
 *  @param succ Success callback
 *  @param fail Failure callback
 *
 *  @return 0 Succeeded
 */
- (int)createAVChatRoomGroup:(NSString*)groupName succ:(TIMCreateGroupSucc)succ fail:(TIMFail)fail;
@end
```

**Parameter description:**

Parameter | Description
---|---
members | A NSString list of members to be added to the group. The creator is added by default. A Public, Private, or ChatRoom group supports up to 6,000 members. AVChatRoom groups support an unlimited number of members.
groupName | Group name, which is of the NSString type with a length up to 30 bytes
groupId | Specified group ID of the NSString type
succ | Success callback that returns the group ID
fail | Failure callback

The following example shows how to create a private group and add user "iOS_002" to the group. **Example:**

>
>- There is no need to explicitly specify the creator as the creator is added to the group by default.
>- The methods and parameters of Public and ChatRoom groups are identical except that both groups have different method names.

```
NSMutableArray * members = [[NSMutableArray alloc] init];
// Add user iOS_002
[members addObject:@"iOS_002"];
[[TIMGroupManager sharedInstance] createPrivateGroup:members groupName:@"GroupName" succ:^(NSString * group) {
	NSLog(@"create group succ, sid=%@", group);
} fail:^(int code, NSString* err) {
	NSLog(@"failed code: %d %@", code, err);
}];
```

### Creating a group with specified properties

When creating a group, you can set default members and the group name as well as the group announcement and group introduction.

```
/**
 *  Create group parameters
 */
@interface TIMCreateGroupInfo : TIMCodingModel
/**
 *  Group ID. If the ID is nil, the system’s default ID is used.
 */
@property(nonatomic,retain) NSString* group;
/**
 *  Group name
 */
@property(nonatomic,retain) NSString* groupName;
/**
 *  Group type: Private, Public, ChatRoom, or AVChatRoom
 */
@property(nonatomic,retain) NSString* groupType;
/**
 *  Whether to set the option for joining groups. Set to false for private groups.
 */
@property(nonatomic,assign) BOOL setAddOpt;
/**
 *  Option for joining groups
 */
@property(nonatomic,assign) TIMGroupAddOpt addOpt;
/**
 *  Maximum number of members. If you enter 0, the system uses the default value.
 */
@property(nonatomic,assign) uint32_t maxMemberNum;
/**
 *  Group announcement
 */
@property(nonatomic,retain) NSString* notification;
/**
 *  Group introduction
 */
@property(nonatomic,retain) NSString* introduction;
/**
 *  Group profile photo
 */
@property(nonatomic,retain) NSString* faceURL;
/**
 *  Collection of custom fields. Among them, key is of the NSString* type and value is of the NSData* type.
 */
@property(nonatomic,retain) NSDictionary* customInfo;
/**
 *  Create a list of members (TIMCreateGroupMemberInfo*)
 */
@property(nonatomic,retain) NSArray* membersInfo;
@end

@interface TIMGroupManager : NSObject
/**
 *  Create a group
 *
 *  @param groupInfo Group information
 *  @param succ Success callback
 *  @param fail Failure callback
 *
 *  @return 0 Succeeded
 */
- (int)createGroup:(TIMCreateGroupInfo*)groupInfo succ:(TIMCreateGroupSucc)succ fail:(TIMFail)fail;
@end
```

**Parameter description:**

Parameter | Description
---|---
groupInfo | Group ID, group name, group type, option for joining groups, maximum number of members, group announcement, group introduction, and group profile photo
succ | Success callback
fail | Failure callback

The following example shows how to create a private group with specified properties and add user "iOS_001" to the group. You do not need to explicitly specify the creator as the creator is added to the group by default. **Example:**

```
// Create group information
TIMCreateGroupInfo *groupInfo = [[TIMCreateGroupInfo alloc] init];
groupInfo.group = nil;
groupInfo.groupName = @"group_private";
groupInfo.groupType = @"Private";
groupInfo.addOpt = TIM_GROUP_ADD_FORBID;
groupInfo.maxMemberNum = 3;
groupInfo.notification = @"this is a notification";
groupInfo.introduction = @"this is a introduction";
groupInfo.faceURL = nil;
// Create group member information
TIMCreateGroupMemberInfo *memberInfo = [[TIMCreateGroupMemberInfo alloc] init];
memberInfo.member = @"iOS_001";
memberInfo.role = TIM_GROUP_MEMBER_ROLE_ADMIN;
// Add group member information
NSMutableArray *membersInfo = [[NSMutableArray alloc] init];
[membersInfo addObject:memberInfo];
groupInfo.membersInfo = membersInfo;
// Create a group with specified properties
[[TIMGroupManager sharedInstance] createGroup:groupInfo succ:^(NSString * group) {
	NSLog(@"create group succ, sid=%@", group);
} fail:^(int code, NSString* err) {
	NSLog(@"failed code: %d %@", code, err);
}];
```

### Creating a group with a custom group ID

By default, the IM server generates a unique ID when a group is created. If a custom group ID is needed, the user can specify an ID when the group is created. A custom group ID can also be obtained by [creating a group with specified properties](#.E5.88.9B.E5.BB.BA.E6.8C.87.E5.AE.9A.E5.B1.9E.E6.80.A7.E7.BE.A4.E7.BB.84).

```
@interface TIMGroupManager : NSObject
/**
 *  Create a group
 *
 *  @param type Group type: Private, Public, ChatRoom, or AVChatRoom
 *  @param groupId Custom group ID. The system automatically assigns a group ID if it is empty.
 *  @param groupName Group name
 *  @param succ Success callback
 *  @param fail Failure callback
 *
 *  @return 0 Succeeded
 */
- (int)createGroup:(NSString*)type groupId:(NSString*)groupId groupName:(NSString*)groupName succ:(TIMCreateGroupSucc)succ fail:(TIMFail)fail;
@end
```

**Parameter description:**

Parameter | Description
---|---
type | Group type
members | List of initial group members
groupName | Group name
groupId | Custom group ID
succ | Success callback
fail | Failure callback

### Inviting users to a group

You can invite users to a group through `inviteGroupMember` of `TIMGroupManager`.

**Permission description:**

For more information, see [Differences in Group Member Operations](https://intl.cloud.tencent.com/document/product/1047/33529#.E7.BE.A4.E6.88.90.E5.91.98.E6.93.8D.E4.BD.9C.E5.B7.AE.E5.BC.82). 

**Prototype:**

```
@interface TIMGroupManager : NSObject
/**
 *  Invite friends to a group
 *
 *  @param group   Group ID
 *  @param members List of users to be added to the group (an NSString* array)
 *  @param succ Success callback
 *  @param fail Failure callback
 *
 *  @return 0 Succeeded
 */
- (int)inviteGroupMember:(NSString*)group members:(NSArray*)members succ:(TIMGroupMemberSucc)succ fail:(TIMFail)fail;
@end
```

**Parameter description:**

Parameter | Description
---|---
group | Group ID, which is of the NSString type
members | NSString list of users to be added to the group
succ | The success callback that returns the list of members who are added to the group successfully and the success status. It is a TIMGroupMemberResult array.
fail | Failure callback

The following example shows how to invite user "iOS_002" to the group whose ID is "TGID1JYSZEAEQ" and returns the operation list and success status after the operation succeeds. `result.status` indicates whether the current user operation was successful. **Example:**

```
NSMutableArray * members = [[NSMutableArray alloc] init];
// Add user iOS_002
[members addObject:@"iOS_002"];
// @"TGID1JYSZEAEQ" indicates the group ID
[[TIMGroupManager sharedInstance] inviteGroupMember:@"TGID1JYSZEAEQ" members:members succ:^(NSArray* arr) {
	for (TIMGroupMemberResult * result in arr) {
		NSLog(@"user %@ status %d", result.member, result.status);
	}
} fail:^(int code, NSString* err) {
	NSLog(@"failed code: %d %@", code, err);
}];
```

**`result.status` prototype:**

```
/**
*  Group operation result
*/
typedef NS_ENUM(NSInteger, TIMGroupMemberStatus) {
	/**
	*  Operation failed
	*/
	TIM_GROUP_MEMBER_STATUS_FAIL              = 0,
	/**
	*  Operation succeeded
	*/
	TIM_GROUP_MEMBER_STATUS_SUCC              = 1,
	/**
	*  The operation is invalid. The user is already a group member when added to the group, or the user is not a group member when removed from the group.
	*/
	TIM_GROUP_MEMBER_STATUS_INVALID           = 2,
    /**
    *  The invitation is pending processing. In this case, wait for the invitee to process.
    */
    TIM_GROUP_MEMBER_STATUS_PENDING           = 3,
};
```

### Applying to join a group

Use `joinGroup` of `TIMGroupManager` to apply to join a group. This operation is valid only for Public and ChatRoom groups.

**Permission description:**
For more information, see [Differences in Group Member Operations](https://intl.cloud.tencent.com/document/product/1047/33529#.E7.BE.A4.E6.88.90.E5.91.98.E6.93.8D.E4.BD.9C.E5.B7.AE.E5.BC.82).

**Prototype:**

```
@interface TIMGroupManager : NSObject
/**
 *  Apply to join a group
 *
 *  @param group ID of the target group
 *  @param msg Application message
 *  @param succ Success callback (the application succeeds and is pending approval)
 *  @param fail Failure callback
 *
 *  @return 0 Succeeded
 */
- (int)joinGroup:(NSString*)group msg:(NSString*)msg succ:(TIMSucc)succ fail:(TIMFail)fail;
@end
```

**Parameter description:**

Parameter | Description
---|---
group | Group ID, which is of the NSString type
msg | Reason for application
succ | Success callback
fail | Failure callback

In the following example, a user applies to join the group "TGID1JYSZEAEQ" and the reason for application is "Apply Join Group". **Example:**

```
[[TIMGroupManager sharedInstance] joinGroup:@"TGID1JYSZEAEQ" msg:@"Apply Join Group" succ:^(){
	NSLog(@"Join Succ");
}fail:^(int code, NSString * err) {
	NSLog(@"code=%d, err=%@", code, err);
}];
```

### Quitting a group

Group members can quit a group.

**Permission description:**

- **Private:** any member can quit the group.
- **Public, ChatRoom, and BChatRoom:** the group owner cannot quit the group.

For more information, see [Differences in Group Member Operations](https://intl.cloud.tencent.com/document/product/1047/33529#.E7.BE.A4.E6.88.90.E5.91.98.E6.93.8D.E4.BD.9C.E5.B7.AE.E5.BC.82).

**Prototype:**

```
@interface TIMGroupManager : NSObject
/**
 *  Quit a group
 *
 *  @param group Group ID
 *  @param succ Success callback
 *  @param fail Failure callback
 *
 *  @return 0 Succeeded
 */
- (int)quitGroup:(NSString*)group succ:(TIMSucc)succ fail:(TIMFail)fail;
@end
```

**Parameter description:**

Parameter | Description
---|---
group | Group ID, which is of the NSString type
succ | Success callback
fail | Failure callback

In the following example, a user quits the group "TGID1JYSZEAEQ". **Example:**

```
// @"TGID1JYSZEAEQ" indicates the group ID
[[TIMGroupManager sharedInstance] quitGroup:@"TGID1JYSZEAEQ" succ:^() {
	NSLog(@"succ");
} fail:^(int code, NSString* err) {
	NSLog(@"failed code: %d %@", code, err);
}];
```

### Deleting group members

Group members can delete other members. The function’s parameters are the same as the function for joining a group.

**Permission description:**
For more information, see [Differences in Group Member Operations](https://intl.cloud.tencent.com/document/product/1047/33529#.E7.BE.A4.E6.88.90.E5.91.98.E6.93.8D.E4.BD.9C.E5.B7.AE.E5.BC.82).

**Prototype:**

```
@interface TIMGroupManager : NSObject
/**
 *  Delete group members
 *
 *  @param group Group ID
 * @param reason Deletion reason
 *  @param members List of members to be deleted
 *  @param succ Success callback
 *  @param fail Failure callback
 *
 *  @return 0 Succeeded
 */
- (int)deleteGroupMemberWithReason:(NSString*)group reason:(NSString*)reason members:(NSArray*)members succ:(TIMGroupMemberSucc)succ fail:(TIMFail)fail;
@end
```

**Parameter description:**

Parameter | Description
---|---
group | Group ID, which is of the NSString type
reason | Reason, which is of the NSString type
members | List of target members, which is an `NSString*` array
succ | The success callback that returns the list of members who are added to the group successfully and the success status. It is a `TIMGroupMemberResult` array.
fail | Failure callback

The following example shows how to delete the user "iOS_002" from the group "TGID1JYSZEAEQ" and returns the operation list and operation status after the deletion succeeds. **Example:**

```
NSMutableArray * members = [[NSMutableArray alloc] init];
// Add user iOS_002
[members addObject:@"iOS_002"];
// @"TGID1JYSZEAEQ" indicates the group ID
[[TIMGroupManager sharedInstance] deleteGroupMemberWithReason:@"TGID1JYSZEAEQ" reason:@"Violated group rules" members:members succ:^(NSArray* arr) {
	for (TIMGroupMemberResult * result in arr) {
		NSLog(@"user %@ status %d", result.member, result.status);
	}
} fail:^(int code, NSString* err) {
	NSLog(@"failed code: %d %@", code, err);
}];
```

### Obtaining a list of group members

Obtain a group member list through the `getGroupMembers` method.

**Permission description:**

- **Any type of group:** the list of members always can be obtained.
- **Live-streaming group:** only some members are pulled, including the group owner, admin, and some members.

For more information, see [Differences in Group Operations](https://intl.cloud.tencent.com/document/product/1047/33529#.E7.BE.A4.E7.BB.84.E6.93.8D.E4.BD.9C.E5.B7.AE.E5.BC.82). 

**Prototype:**

```
/**
 *  Returned values of group member operations
 */
@interface TIMGroupMemberInfo : TIMCodingModel
/**
 *  Target member
 */
@property(nonatomic,retain) NSString* member;
/**
 *  Group name card
 */
@property(nonatomic,retain) NSString* nameCard;
/**
 *  Time of joining the group
 */
@property(nonatomic,assign) time_t joinTime;
/**
 *  Member’s role in the group
 */
@property(nonatomic,assign) TIMGroupMemberRole role;
/**
 *  Muting period (the remaining seconds)
 */
@property(nonatomic,assign) uint32_t silentUntil;
/**
 *  Collection of custom fields. Among them, key is of the NSString* type and value is of the NSData* type.
 */
@property(nonatomic,retain) NSDictionary* customInfo;
@end

@interface TIMGroupManager : NSObject
/**
 *  Obtain the group member list
 *
 *  @param group Group ID
 *  @param succ Success callback (TIMGroupMemberInfo list)
 *  @param fail Failure callback
 *
 *  @return 0 Succeeded
 */
- (int)getGroupMembers:(NSString*)groupId succ:(TIMGroupMemberSucc)succ fail:(TIMFail)fail;
@end
```

**Parameter description:**

Parameter | Description
---|---
group | Group ID, which is of the NSString\* type
succ | Success callback that returns a TIMGroupMemberInfo\* array
fail | Failure callback

This example shows how to obtain the member list of the group "TGID1JYSZEAEQ". `list` is `TIMGroupMemberInfo*` data and stores member information. **Example:**

```
// @"TGID1JYSZEAEQ" indicates the group ID
[[TIMGroupManager sharedInstance] getGroupMembers:@"TGID1JYSZEAEQ" succ:^(NSArray* list) {
	for (TIMGroupMemberInfo * info in list) {
		NSLog(@"user=%@ joinTime=%lu role=%d", info.member, info.joinTime, info.role);
	}
} fail:^(int code, NSString * err) {
	NSLog(@"failed code: %d %@", code, err);
}];
```

If a group has too many members, use the **pagination API**. **Prototype:**

```
@interface TIMGroupManager : NSObject
/**
 *  Obtain the list of members of the specified type (the list can be pulled by field and in pages)
 *
 *  @param group      Group ID: NSString* list
 *  @param filter     Group member role filter
 *  @param flags      Flag of the information to be pulled
 *  @param custom    List of custom keys (NSString*) to obtain
 * @param nextSeq     Flag for pagination pulling. Enter 0 for the first request. If the success callback returns a non-zero value, the list will be pulled in pages. In this case, pass in this parameter to pull again until the value becomes 0.
 *  @param succ       Success callback
 *  @param fail       Failure callback
 */
- (int)getGroupMembers:(NSString*)group ByFilter:(TIMGroupMemberFilter)filter flags:(TIMGetGroupMemInfoFlag)flags custom:(NSArray*)custom nextSeq:(uint64_t)nextSeq succ:(TIMGroupMemberSuccV2)succ fail:(TIMFail)fail;
@end
```

### Obtaining the list of groups the user has joined

Obtain the list of groups that the current user has joined through `getGroupList`.

**Permission description:**

- Obtain the list of groups that you have joined. The returned `TIMGroupInfo` contains only `group`, `groupName`, and `groupType`.
- Only some of the live-streaming groups the user has joined can be obtained.

**Prototype:**

```
@interface TIMGroupManager : NSObject
/**
 *  Obtain the group list
 *
 *  @param succ Success callback. The NSArray list is TIMGroupInfo. The structure contains only group\groupName\groupType\faceUrl\selfInfo.
 *  @param fail Failure callback
 *
 *  @return 0 Succeeded
 */
- (int)getGroupList:(TIMGroupListSucc)succ fail:(TIMFail)fail;
@end
```

**Parameter description:**

Parameter | Description
---|---
succ | Success callback that returns the list of group IDs, which is a TIMGroupInfo array
fail | Failure callback

The following example shows how to obtain a group list and prints group IDs, group types (Private, Public, and ChatRoom), and group names. **Example:**

```
[[TIMGroupManager sharedInstance] getGroupList:^(NSArray * list) {
	for (TIMGroupInfo * info in list) {
		NSLog(@"group=%@ type=%@ name=%@", info.group, info.groupType, info.groupName);
	}
} fail:^(int code, NSString* err) {
	NSLog(@"failed code: %d %@", code, err);
}];
```

### Dismissing a group

Dismiss groups through `DeleteGroup`.

**Permission description:**

For more information, see [Differences in Group Operations](https://intl.cloud.tencent.com/document/product/1047/33529#.E7.BE.A4.E7.BB.84.E6.93.8D.E4.BD.9C.E5.B7.AE.E5.BC.82). 


**Prototype:**

```
@interface TIMGroupManager : NSObject

/**
 *  Dismiss a group
 *
 *  @param group Group ID
 *  @param succ Success callback
 *  @param fail Failure callback
 *
 *  @return 0 Succeeded
 */
- (int)deleteGroup:(NSString*)group succ:(TIMSucc)succ fail:(TIMFail)fail;

@end
```

**Parameter description:**

Parameter | Description
---|---
group | Group ID
succ | Success callback that returns the list of group IDs, which is an NSString array
fail | Failure callback

The following example shows how to dismiss the group "TGID1JYSZEAEQ". **Example:**

```
[[TIMGroupManager sharedInstance] deleteGroup:@"TGID1JYSZEAEQ" succ:^() {
	NSLog(@"delete group succ");
}fail:^(int code, NSString* err) {
	NSLog(@"failed code: %d %@", code, err);
}];
```

### Transferring a group

You can transfer groups through `modifyGroupOwner`.

**Permission description:**

- Only the **group owner** has the permission to transfer the group ownership.
- The ownership of **live-streaming groups** cannot be transferred.

**Prototype:**

```
@interface TIMGroupManager : NSObject
/**
 *  Transfer a group to a new group owner
 *
 *  @param group Group ID
 *  @param identifier ID of the new group owner
 *  @param succ Success callback
 *  @param fail Failure callback
 *
 *  @return 0 Succeeded
 */
- (int)modifyGroupOwner:(NSString*)group user:(NSString*)identifier succ:(TIMSucc)succ fail:(TIMFail)fail;
@end
```

**Parameter description:**

Parameter | Description
---|---
group | Group ID
user | User ID
succ | Success callback
fail | Failure callback

The following example shows how to transfer the group "TGID1JYSZEAEQ" to the user "iOS_001". **Example:**

```
[[TIMGroupManager sharedInstance] modifyGroupOwner:@"TGID1JYSZEAEQ" user:@"iOS_001" succ:^() {
	NSLog(@"set new owner succ");
}fail:^(int code, NSString* err) {
	NSLog(@"failed code: %d %@", code, err);
}];
```

### Muting all members

You can mute all members through `modifyGroupAllShutup`.

**Permission description:**

- The **group owner and admin** can mute all members.
- **All group types** support muting all members.

**Prototype:**

```
@interface TIMGroupManager : NSObject
/**
 *  Modify the Mute All property
 *
 *  @param group   Group ID
 *  @param shutup  Whether to mute or not
 *  @param succ    Success callback
 *  @param fail    Failure callback
 *
 *  @return 0 Succeeded
 */
- (int)modifyGroupAllShutup:(NSString*)group shutup:(BOOL)shutup succ:(TIMSucc)succ fail:(TIMFail)fail;
@end
```

**Parameter description:**

Parameter | Description
---|---
group | Group ID
shutup | Whether to mute or not
succ | Success callback
fail | Failure callback

The following example shows how to set Mute All for the group "TGID1JYSZEAEQ". Obtain the Mute All property on the client through `getGroupList` and `getGroupInfo`. **Example:**

```
[[TIMGroupManager sharedInstance] modifyGroupAllShutup:@"TGID1JYSZEAEQ" shutup:YES succ:^() {
	NSLog(@"set all shutup succ");
}fail:^(int code, NSString* err) {
	NSLog(@"failed code: %d %@", code, err);
}];
```

## Obtaining Group Information

### Obtaining group information

You can use the `getGroupInfo` method of `TIMGroupManager` to obtain group information stored on the server and use the `queryGroupInfo` method to obtain the locally cached group information. Group information is defined by `TIMGroupInfo`.  

**Permission description:**

- The group members of Public and Private groups can pull group information.
- For a Public group, non-members can pull information fields including group, groupName, owner, groupType, createTime, maxMemberNum, memberNum, introduction, faceURL, addOpt, onlineMemberNum, and customInfo. For a Private group, non-members cannot pull any group information.

**Prototype:**

```
/**
 *  Group information
 */
@interface TIMGroupInfo : TIMCodingModel
/**
 *  Group ID
 */
@property(nonatomic,retain) NSString* group;
/**
 *  Group name
 */
@property(nonatomic,retain) NSString* groupName;
/**
 *  Group creator or admin
 */
@property(nonatomic,retain) NSString * owner;
/**
 *  Group type: Private, Public, and ChatRoom
 */
@property(nonatomic,retain) NSString* groupType;
/**
 *  Group creation time
 */
@property(nonatomic,assign) uint32_t createTime;
/**
 *  Last modification time of group information
 */
@property(nonatomic,assign) uint32_t lastInfoTime;
/**
 *  Sending time of the last group message
 */
@property(nonatomic,assign) uint32_t lastMsgTime;
/**
 *  Maximum number of members
 */
@property(nonatomic,assign) uint32_t maxMemberNum;
/**
 *  Number of group members
 */
@property(nonatomic,assign) uint32_t memberNum;
/**
 *  Option for joining groups
 */
@property(nonatomic,assign) TIMGroupAddOpt addOpt;
/**
 *  Group announcement
 */
@property(nonatomic,retain) NSString* notification;
/**
 *  Group introduction
 */
@property(nonatomic,retain) NSString* introduction;
/**
 *  Group profile photo
 */
@property(nonatomic,retain) NSString* faceURL;
/**
 *  Last message
 */
@property(nonatomic,retain) TIMMessage* lastMsg;
/**
 *  Number of online members
 */
@property(nonatomic,assign) uint32_t onlineMemberNum;
/**
 *  Whether the group can be searched for or not
 */
@property(nonatomic,assign) TIMGroupSearchableType isSearchable;
/**
 *  Whether group members are visible
 */
@property(nonatomic,assign) TIMGroupMemberVisibleType isMemberVisible;
/**
 * Whether all members are muted
 */
@property(nonatomic,assign) BOOL allShutup;
/**
 *  Your own information in the group
 */
@property(nonatomic,retain) TIMGroupSelfInfo* selfInfo;
/**
 *  Collection of custom fields. Among them, key is of the NSString* type and value is of the NSData* type.
 */
@property(nonatomic,retain) NSDictionary* customInfo;
@end

@interface TIMGroupManager : NSObject
/**
 ** Obtain group information stored on the server
 *
 *  @param groups List of group IDs
 *  @param succ Success callback without selfInfo
 *  @param fail Failure callback
 *
 *  @return 0 Succeeded
 */
- (int)getGroupInfo:(NSArray*)groups succ:(TIMGroupListSucc)succ fail:(TIMFail)fail;
/**
 ** Obtain locally stored group information
 *
 *  @param group Group ID
 *
 *  @return Group information
 */
- (TIMGroupInfo *)queryGroupInfo:(NSString *)group;
@end
```

**Parameter description:**

Parameter | Description
---|---
groups | List of groups whose information is to be obtained, which is an NSString array
succ | Success callback that returns the list of group information, which is a TIMGroupInfo array
fail | Failure callback

The following example shows how to obtain the detailed information of the group "TGID1JYSZEAEQ". **Example:**

```
NSMutableArray * groupList = [[NSMutableArray alloc] init];
[groupList addObject:@"TGID1JYSZEAEQ"];
[[TIMGroupManager sharedInstance] getGroupInfo:groupList succ:^(NSArray * groups) {
	for (TIMGroupInfo * info in groups) {
		NSLog(@"get group succ, infos=%@", info);
	}
} fail:^(int code, NSString* err) {
	NSLog(@"failed code: %d %@", code, err);
}];
```

### Obtaining your own information in a group

**Permission description:**

**Live-streaming group:** your own information cannot be pulled.

**Prototype:**

```
@interface TIMGroupManager : NSObject
/**
 *  Obtain your own member information in the group
 *
 *  @param group Group ID
 * @param succ Success callback that returns the information
 *  @param fail Failure callback
 *
 *  @return 0 Succeeded
 */
- (int)getGroupSelfInfo:(NSString*)groupId succ:(TIMGroupSelfSucc)succ fail:(TIMFail)fail;
@end
```

**Parameter description:**

Parameter | Description
---|---
groupId | Group ID
succ | Success callback that returns your information in the group
fail | Failure callback

### Obtaining the information of specified members in the group

**Permission description:**

- ***Live-streaming group:** only the information of some members can be pulled, including the group owner, admin, and some members.

**Prototype:**

```
@interface TIMGroupManager : NSObject
/**
 *
 *  To get the profiles of specified members in the group, you need to set members. For information on other limits, see getGroupMembers.
 *
 *  @param groupId Group ID
 *  @param members List of member IDs (NSString*)
 *  @param succ    Success callback (TIMGroupMemberInfo list)
 *  @param fail    Failure callback
 *
 *  @return 0: succeeded. 1: failed.
 */
- (int)getGroupMembersInfo:(NSString*)groupId members:(NSArray<NSString *>*)members succ:(TIMGroupMemberSucc)succ fail:(TIMFail)fail;
@end
```

**Parameter description:**

Parameter | Description
---|---
groupId | Group ID
members | List of member IDs
succ | Success callback that returns the list of group member information
fail | Failure callback

## Modifying Group Information

### Modifying the group name

You can modify the group name through `modifyGroupName`.

**Permission description:**

- **Public, ChatRoom, and BChatRoom:** only the group owner or admin can modify the group name.
- **Private:** any member can modify the group name.

**Prototype:**

```
@interface TIMGroupManager : NSObject
/**
 *  Modify the group name
 *
 *  @param group     Group ID
 *  @param groupName New group name
 *  @param succ      Success callback
 *  @param fail      Failure callback
 *
 *  @return 0 Succeeded
 */
- (int)modifyGroupName:(NSString*)group groupName:(NSString*)groupName succ:(TIMSucc)succ fail:(TIMFail)fail;
@end
```

**Parameter description:**

Parameter | Description
---|---
group | Group ID
groupName | Modified group name
succ | Success callback
fail | Failure callback

The following example shows how to changes the name of the group "TGID1JYSZEAEQ" to "ModifyGroupName". **Example:**

```
[[TIMGroupManager sharedInstance] modifyGroupName:@"TGID1JYSZEAEQ" groupName:@"ModifyGroupName" succ:^() {
	NSLog(@"modify group name succ");
}fail:^(int code, NSString* err) {
	NSLog(@"failed code: %d %@", code, err);
}];
```

### Modifying the group introduction

You can modify the group introduction through `modifyGroupIntroduction`.

**Permission description:**

- **Public, ChatRoom, and BChatRoom:** only the group owner or admin can modify the group introduction.
- **Private:** any member can modify the group introduction.

**Prototype:**

```
@interface TIMGroupManager : NSObject

/**
 *  Modify the group introduction
 *
 *  @param group            Group ID
 *  @param introduction     Group introduction
 *  @param succ             Success callback
 *  @param fail             Failure callback
 *
 *  @return 0 Succeeded
 */
- (int)modifyGroupIntroduction:(NSString*)group introduction:(NSString*)introduction succ:(TIMSucc)succ fail:(TIMFail)fail;

@end
```

**Parameter description:**

Parameter | Description
---|---
group | Group ID
introduction | Group introduction with a maximum length of 120 bytes
succ | Success callback
fail | Failure callback

**Example:**

```
[[TIMGroupManager sharedInstance] modifyGroupIntroduction:@"TGID1JYSZEAEQ" introduction :@"this is one group" succ:^() {
	NSLog(@"modify group introduction succ");
}fail:^(int code, NSString* err) {
	NSLog(@"failed code: %d %@", code, err);
}];
```

### Modifying the group announcement

You can modify the group announcement through `modifyGroupNotification`.

**Permission description:**

- **Public, ChatRoom, and BChatRoom:** only the group owner or admin can modify the group announcement.
- **Private:** any member can modify the group announcement.

**Prototype:**

```
@interface TIMGroupManager : NSObject
/**
 *  Modify the group announcement
 *
 *  @param group            Group ID
 *  @param notification     Group announcement with a maximum length of 150 bytes
 *  @param succ             Success callback
 *  @param fail             Failure callback
 *
 *  @return 0 Succeeded
 */
- (int)modifyGroupNotification:(NSString*)group notification:(NSString*)notification succ:(TIMSucc)succ fail:(TIMFail)fail;
@end
```

**Parameter description:**

Parameter | Description
---|---
group | Group ID
notification | Group announcement with a maximum length of 150 bytes
succ | Success callback
fail | Failure callback

The following example shows how to change the notification of the group "TGID1JYSZEAEQ" to "test notification". **Example:**

```
[[TIMGroupManager sharedInstance] modifyGroupNotification:@"TGID1JYSZEAEQ" notification:@"test notification" succ:^() {
	NSLog(@"modify group notification succ");
}fail:^(int code, NSString* err) {
	NSLog(@"failed code: %d %@", code, err);
}];
```

### Modifying the group profile photo

You can modify the group profile photo through `modifyGroupFaceUrl`.

**Permission description:**

- **Public, ChatRoom, and BChatRoom:** only the group owner or admin can modify the group profile photo.
- **Private:** any member can modify the group profile photo.

**Prototype:**

```
@interface TIMGroupManager : NSObject
/**
 *  Modify the group profile photo
 *
 *  @param group            Group ID
 *  @param url              URL of the group profile photo with a maximum length of 100 bytes
 *  @param succ             Success callback
 *  @param fail             Failure callback
 *
 *  @return 0 Succeeded
 */
- (int)modifyGroupFaceUrl:(NSString*)group url:(NSString*)url succ:(TIMSucc)succ fail:(TIMFail)fail;
@end
```

**Parameter description:**

Parameter | Description
---|---
group | Group ID
url | URL of the group profile photo with a maximum length of 100 bytes
succ | Success callback
fail | Failure callback

**Example:**

```
[[TIMGroupManager sharedInstance] modifyGroupFaceUrl:@"TGID1JYSZEAEQ" notification:@"http://test/x.jpg" succ:^() {
	NSLog(@"modify group face url succ");
}fail:^(int code, NSString* err) {
	NSLog(@"failed code: %d %@", code, err);
}];
```

### Modifying the option for joining groups

You can modify the option for joining groups through `modifyGroupAddOpt`.

**Permission description:**

- **Public, ChatRoom, and BChatRoom:** only the group owner or admin can modify the option for joining groups.
- **Private:** users can join a group only through invitation, and user application is not supported.

**Prototype:**

```
@interface TIMGroupManager : NSObject

/**
 *  Modify the option for joining groups
 *
 *  @param group            Group ID
 *  @param opt              Option for joining groups; see TIMGroupAddOpt for details
 *  @param succ             Success callback
 *  @param fail             Failure callback
 *
 *  @return 0 Succeeded
 */
- (int)modifyGroupAddOpt:(NSString*)group opt:(TIMGroupAddOpt)opt succ:(TIMSucc)succ fail:(TIMFail)fail;
@end
```

**Parameter description:**

Parameter | Description
---|---
group | Group ID
opt | Option for joining groups, which can be set to one of the following: allow anyone to join, approval required, and disallow anyone to join
succ | Success callback
fail | Failure callback

The following example shows how to set the option for joining the group "TGID1JYSZEAEQ" to "disallow anyone to join". **Example:**

```
[[TIMGroupManager sharedInstance] modifyGroupAddOpt:@"TGID1JYSZEAEQ" opt:TIM_GROUP_ADD_FORBID succ:^() {
	NSLog(@"modify group opt succ");
}fail:^(int code, NSString* err) {
	NSLog(@"failed code: %d %@", code, err);
}];
```

### Modifying group custom fields

You can modify group custom fields through `modifyGroupCustomInfo`.

**Permission description:**

- Relevant keys and permissions need to be configured at the backend.

**Prototype:**

```
@interface TIMGroupManager : NSObject
/**
 *  Modify a collection of custom fields
 *
 *  @param group      Group ID
 *  @param customInfo Collection of custom fields. Among them, key is of the NSString* type and value is of the NSData* type.
 *  @param succ       Success callback
 *  @param fail       Failure callback
 *
 *  @return 0 Succeeded
 */
- (int)modifyGroupCustomInfo:(NSString*)group customInfo:(NSDictionary*)customInfo succ:(TIMSucc)succ fail:(TIMFail)fail;
@end
```

**Parameter description:**

Parameter | Description
---|---
group | Group ID
customInfo | Collection of custom fields. Among them, key is of the NSString\* type and value is of the NSData\* type.
succ | Success callback
fail | Failure callback

The following example shows how to set the option for joining the group "TGID1JYSZEAEQ" to "disallow anyone to join". **Example:**

```
// Configure custom data
NSMutalbeDictionary *customInfo = [[NSMutableDictionary alloc] init];
NSString *key = @"custom key";
NSData *data = [NSData dataWithBytes:"custom value" length:13];
[customInfo setObject:data forKey:key];
[[TIMGroupManager sharedInstance] modifyGroupCustomInfo:@"TGID1JYSZEAEQ" customInfo:customInfo succ:^() {
	NSLog(@"modify group customInfo succ");
}fail:^(int code, NSString* err) {
	NSLog(@"failed code: %d %@", code, err);
}];
```

### Modifying a member’s role in a group

You can modify a member’s role in a group through `modifyGroupMemberInfoSetRole`.

**Permission description:**

- The **group owner and admin** can modify group members’ roles.
- **Live-streaming group** does not support modifying group members’ roles.

**Prototype:**

```
@interface TIMGroupManager : NSObject
- (int)modifyGroupMemberInfoSetRole:(NSString*)group user:(NSString*)identifier role:(TIMGroupMemberRole)role succ:(TIMSucc)succ fail:(TIMFail)fail;
@end
```

**Parameter description:**

Parameter | Description
---|---
group | Group ID
identifier | ID of the group member whose role is to be modified
role | Modified role, which can not be the group owner
succ | Success callback
fail | Failure callback

The following example shows how to set the user "iOS_001" as the admin of the group "TGID1JYSZEAEQ". **Example:**

```
[[TIMGroupManager sharedInstance] modifyGroupMemberInfoSetRole:@"TGID1JYSZEAEQ" user:@"iOS_001" role:TIM_GROUP_MEMBER_ADMIN succ:^() {
	NSLog(@"modify group member role succ");
}fail:^(int code, NSString* err) {
	NSLog(@"failed code: %d %@", code, err);
}];
```



### Muting group members

You can mute group members and set the muting period through `modifyGroupMemberInfoSetSilence`.

**Permission description:**

The **group owner and admin** can mute group members.

**Prototype:**

```
@interface TIMGroupManager : NSObject
- (int)modifyGroupMemberInfoSetSilence:(NSString*)group user:(NSString*)identifier stime:(uint32_t)stime succ:(TIMSucc)succ fail:(TIMFail)fail;
@end
```

**Parameter description:**

Parameter | Description
---|---
group | Group ID
identifier | ID of the group member to be muted
stime | Muting period in seconds
succ | Success callback
fail | Failure callback

The following example shows how to mute the member "iOS_001" in the group "TGID1JYSZEAEQ" for 120 seconds. **Example:**

```
[[TIMGroupManager sharedInstance] modifyGroupMemberInfoSetSilence:@"TGID1JYSZEAEQ" user:@"iOS_001" stime:120 succ:^() {
	NSLog(@"modify group member silence succ");
}fail:^(int code, NSString* err) {
	NSLog(@"failed code: %d %@", code, err);
}];
```

### Modifying a member’s name card in a group

You can modify a member’s name card in a group through `modifyGroupMemberInfoSetNameCard`.

**Prototype:**

```
@interface TIMGroupManager : NSObject
- (int)modifyGroupMemberInfoSetNameCard:(NSString*)group user:(NSString*)identifier nameCard:(NSString*)nameCard succ:(TIMSucc)succ fail:(TIMFail)fail;
@end
```

**Parameter description:**

Parameter | Description
---|---
group | Group ID
identifier | ID of the group member whose name card is to be modified
nameCard | Name card to be modified
succ | Success callback
fail | Failure callback

The following example shows how to set the name card of the user "iOS_001" in the group "TGID1JYSZEAEQ" to "iOS_001_namecard". **Example:**

```
[[TIMGroupManager sharedInstance] modifyGroupMemberInfoSetNameCard:@"TGID1JYSZEAEQ" user:@"iOS_001" nameCard:@"iOS_001_namecard" succ:^() {
	NSLog(@"modify group member namecard succ");
}fail:^(int code, NSString* err) {
	NSLog(@"failed code: %d %@", code, err);
}];
```



### Modifying group member custom fields

You can modify group member custom fields through `modifyGroupMemberInfoSetCustomInfo`.

**Prototype:**

```
@interface TIMGroupManager : NSObject
- (int)modifyGroupMemberInfoSetCustomInfo:(NSString*)group user:(NSString*)identifier customInfo:(NSDictionary<NSString*,NSData*> *)customInfo succ:(TIMSucc)succ fail:(TIMFail)fail;
@end
```

**Parameter description:**

Parameter | Description
---|---
group | Group ID
identifier | ID of the group member for whom you want to set a custom property
customInfo | Collection of custom fields. Among them, key is of the NSString\* type and value is of the NSData\* type.
succ | Success callback
fail | Failure callback

The following example shows how to set a custom property for the user "iOS_001" in the group "TGID1JYSZEAEQ". **Example:**

```
[[TIMGroupManager sharedInstance] modifyGroupMemberInfoSetCustomInfo:@"TGID1JYSZEAEQ" user:@"iOS_001" customInfo:customInfo succ:^() {
	NSLog(@"modify group member customInfo succ");
}fail:^(int code, NSString* err) {
	NSLog(@"failed code: %d %@", code, err);
}];
```

### Modifying the option for receiving group messages

You can set the option for receiving group messages through `modifyReceiveMessageOpt`. By default, Public and Private groups receive and push group messages offline. ChatRoom and BChatRoom groups receive but do not push group messages offline.

**Prototype:**

```
@interface TIMGroupManager : NSObject
- (int)modifyReceiveMessageOpt:(NSString*)group opt:(TIMGroupReceiveMessageOpt)opt succ:(TIMSucc)succ fail:(TIMFail)fail;
@end
```

**Parameter description:**

Parameter | Description
---|---
group | Group ID
opt | Option for receiving messages
succ | Success callback
fail | Failure callback

The following example shows how to set the option for receiving messages in the group "TGID1JYSZEAEQ" to receive online messages but not to push messages offline. **Example:**

```
[[TIMGroupManager sharedInstance] modifyReciveMessageOpt:@"TGID1JYSZEAEQ" opt:TIM_GROUP_RECEIVE_NOT_NOTIFY_MESSAGE succ:^() {
	NSLog(@"modify receive group message option succ");
}fail:^(int code, NSString* err) {
	NSLog(@"failed code: %d %@", code, err);
}];
```

## Group Pending Requests

### Pulling group pending requests

You can pull group pending requests through `getPendencyFromServer`. Group pending requests are group-related operations that require approval, such as pending "apply to join" requests and pending "invited to join" requests. Even after a pending request is approved or rejected, the information can still be pulled through this API. In this case, the pulled message has a "processed" flag.

**Permission description:**

The **approver** has the permission to pull the information.

>
>- If user A applies to join group A, the group admin can obtain information related to this pending request. As user A does not have the approval permission, user A does not need to pull information related to this pending request.
>- If admin A invites user A to group A, user A can obtain the information related to this pending request because this pending request needs to be approved by user A.

**Prototype:**

```
@interface TIMGroupManager : NSObject
/**
 *  Obtain the list of group pending requests
 *
 *  @param option Pending parameter configuration
 *  @param succ   Success callback that returns the list of pending requests
 *  @param fail   Failure callback
 *
 *  @return 0 Succeeded
 */
- (int)getPendencyFromServer:(TIMGroupPendencyOption*)option succ:(TIMObtainGroupPendencyListSucc)succ fail:(TIMFail)fail;
@end
```

**Parameter description:**

Parameter | Description
---|---
option | Pending parameter configuration
succ | Success callback that returns the list of pending requests
fail | Failure callback

 **option parameter description:**

| Parameter | Description |
| --- | --- |
| timestamp | Start timestamp for pulling. If the pull starts from the latest one, enter 0 or leave this parameter empty. In the case of pagination, the callback returns the start timestamp of the next page. |
| numPerPage | Number of pulled items at a time. This parameter is used for pagination. |

**Callback prototype:**

```
/**
 *  Obtaining the list of group pending requests succeeds
 *
 *  @param meta       Metadata of pending requests
 *  @param pendencies Array of pending requests (TIMGroupPendencyItem)
 */
typedef void (^TIMObtainGroupPendencyListSucc)(TIMGroupPendencyMeta * meta, NSArray * pendencies);
```

**Callback parameter description:**

Parameter | Description
---|---
meta | Information returned by the pull, including the pagination information and pulling status
pendencies | Array of pulled pending items

**Property description:**

Property | Description
---|---
nextStartTime | Start timestamp for pulling the next page. If the value is 0, no more pages exist.
readTimeSeq | Read timestamp for determining whether a pending item has been read or not
unReadCnt | Number of unread items, not limited to the current page

**Properties associated with pending items:**

```
/**
  *  Pending application
  */
@interface TIMGroupPendencyItem : TIMCodingModel
/**
 *  Group ID
 */
@property(nonatomic,retain) NSString* groupId;
/**
  *  ID of the requester, who is the requester for an "apply to join" request and the inviter for an "invited to join" request.
  */
@property(nonatomic,retain) NSString* fromUser;
/**
  *  ID of the handler, which is 0 for an "apply to join" request and the inviter for an "invited to join" request.
  */
@property(nonatomic,retain) NSString* toUser;
/**
  *  Addition time of the pending request
  */
@property(nonatomic,assign) uint64_t addTime;
/**
  *  Type of the pending request
  */
@property(nonatomic,assign) TIMGroupPendencyObtainType getType;
/**
  *  "Processed" flag
  */
@property(nonatomic,assign) TIMGroupPendencyHandleStatus handleStatus;
/**
  *  Processed result
  */
@property(nonatomic,assign) TIMGroupPendencyHandleResult handleResult;
/**
  ** Additional information of the application or invitation
  */
@property(nonatomic,retain) NSString* requestMsg;
/**
  *  Approval information: approval or rejection information
  */
@property(nonatomic,retain) NSString* handledMsg;
/**
  *  Approve the application
  *
  *  @param msg      Reason for approval (optional)
  *  @param succ     Success callback
  *  @param fail     Failure callback, which returns the error code and error description
  */
-(void) accept:(NSString*)msg succ:(TIMSucc)succ fail:(TIMFail)fail;
/**
  *  Reject the application
  *
  *  @param msg      Reason for rejection (optional)
  *  @param succ     Success callback
  *  @param fail     Failure callback, which returns the error code and error description
  */
-(void) refuse:(NSString*)msg succ:(TIMSucc)succ fail:(TIMFail)fail;
/**
  *  Your own ID
  */
@property(nonatomic,strong) NSString* selfIdentifier;
@end
```

**Property description:**

Property | Description
---|---
groupId | Group ID
fromUser | ID of the pending request initiator
toUser | ID of the pending request handler
addTime | Addition time of the pending request
getType | Enumerate pending request types: apply to join and invited to join
handleStatus | Enumerate the pending request status: pending, processed by another user, processed by handler (for example, when user A applies to join the group and admin A approves the application, the status of this pending item pulled by admin B is "processed by another user")
handleResult | Enumerate processing results: approved and rejected
requestMsg/handleMsg | Message left during application or approval

**Example:**

```
  TIMGroupPendencyOption option = [[TIMGroupPendencyOption alloc] init];
  option.timestamp = 0;
  option.numPerPage = 10;
  [[TIMGroupManager sharedInstance] getPendencyFromServer:option succ:^(TIMGroupPendencyMeta *meta, NSArray *pendencies) {
      NSLog(@"get pendencies succ");
  } fail:^(int code, NSString *msg) {
      NSLog(@"get pendencies failed: %d->%@", code, msg);
  }];
```

### Reporting that group pending requests are read

The IM SDK can report that the current pending request and all the pending requests before it have been read. After the reporting, you can still pull these pending requests and determine whether they are read through the read timestamp.

**Prototype:**

```
@interface TIMGroupManager : NSObject
/**
 *  Report that group pending requests are read
 *
 *  @param timestamp Read report timestamp
 *  @param succ      Success callback
 *  @param fail      Failure callback
 *
 *  @return 0 Succeeded
 */
- (int)pendencyReport:(uint64_t)timestamp succ:(TIMSucc)succ fail:(TIMFail)fail;
@end
```

**Parameter description:**

Parameter | Description
---|---
timestamp | Read report timestamp. For a single pending message, the timestamp is included in its property.
succ | Success callback
fail | Failure callback

**Example:**

```
[[TIMGroupManager sharedInstance] pendencyReport:timestamp succ:^{
        NSLog(@"pendency report succ");
    } fail:^(int code, NSString *msg) {
        NSLog(@"pendency report failed: %d->%@", code, msg);
    }];
```

### Processing group pending requests

The IM SDK provides an API for handling group pending requests. The handler can select a single pending request and approve or reject it. Pending requests that have been successfully handled cannot be handled again.

**Prototype:**

```
@interface TIMGroupPendencyItem: NSObject
/**
 *  Approve the application
 *
 *  @param msg      Reason for approval (optional)
 *  @param succ     Success callback
 *  @param fail     Failure callback, which returns the error code and error description
 */
- (void)accept:(NSString*)msg succ:(TIMSucc)succ fail:(TIMFail)fail;
/**
 *  Reject the application
 *
 *  @param msg      Reason for rejection (optional)
 *  @param succ     Success callback
 *  @param fail     Failure callback, which returns the error code and error description
 */
- (void)refuse:(NSString*)msg succ:(TIMSucc)succ fail:(TIMFail)fail;
@end
```

**Example:**

```
TIMGroupPendencyItem *item = [pendencies firstObject];
[item accept:@"thanks for inviting" succ:^{
    NSLog(@"accept succ");
} fail:^(int code, NSString *msg) {
    NSLog(@"accept fail: %d->%@", code, msg);
}];
[item refuse:@"i dont want to join" succ:^{
    NSLog(@"refuse succ");
} fail:^(int code, NSString *msg) {
    NSLog(@"refuse fail: %d->%@", code, msg);
}];
```

## Group Event Messages

When a user is invited to a group or is removed from a group, a prompt message is displayed in the group. The caller can decide whether to display and how to display the prompt message (for example, ignore it or display it to users as needed.) A prompt message is identified by a special `Elem` and returned by the new message callback. For more information, see [New Message Notifications](/doc/product/269/9148#.E6.96.B0.E6.B6.88.E6.81.AF.E9.80.9A.E7.9F.A5). The following figure shows an event message for group name modification.


**Message prototype:**

```
/**
 *  Group prompt message type
 */
typedef NS_ENUM(NSInteger, TIM_GROUP_TIPS_TYPE){
    /**
     *  Invited to join a group (opUser & groupName & userList)
     */
    TIM_GROUP_TIPS_TYPE_INVITE              = 0x01,
    /**
     *  Quit a group (opUser & groupName & userList)
     */
    TIM_GROUP_TIPS_TYPE_QUIT_GRP            = 0x02,
    /**
     *  Removed from a group (opUser & groupName & userList)
     */
    TIM_GROUP_TIPS_TYPE_KICKED              = 0x03,
    /**
     *  Admin is set (opUser & groupName & userList)
     */
    TIM_GROUP_TIPS_TYPE_SET_ADMIN           = 0x04,
    /**
     *  Admin is canceled (opUser & groupName & userList)
     */
    TIM_GROUP_TIPS_TYPE_CANCEL_ADMIN        = 0x05,
    /**
     *  Group information is modified (opUser & groupName & introduction & notification & faceUrl & owner)
     */
    TIM_GROUP_TIPS_TYPE_INFO_CHANGE         = 0x06,
    /**
     *  Group member information is modified (opUser & groupName & memberInfoList)
     */
    TIM_GROUP_TIPS_TYPE_MEMBER_INFO_CHANGE         = 0x07,
};
/**
 *  Group prompt message
 */
@interface TIMGroupTipsElem : TIMElem
/**
  *  Group ID
  */
@property(nonatomic,strong) NSString * group;
/**
  *  Group prompt message type
  */
@property(nonatomic,assign) TIM_GROUP_TIPS_TYPE type;
/**
  *  Username of the operator
  */
@property(nonatomic,strong) NSString * opUser;
/**
  *  List of target users, which is an NSString* array
  */
@property(nonatomic,strong) NSArray * userList;
/**
  *  Modified group name, otherwise it is nil in other cases
  */
@property(nonatomic,strong) NSString * groupName;
/**
  *  Group information modification: valid for TIM_GROUP_TIPS_TYPE_INFO_CHANGE and is a TIMGroupTipsElemGroupInfo structure list
  */
@property(nonatomic,strong) NSArray * groupChangeList;
/**
  *  Member change: valid for TIM_GROUP_TIPS_TYPE_MEMBER_INFO_CHANGE and is a TIMGroupTipsElemMemberInfo structure list
  */
@property(nonatomic,strong) NSArray * memberChangeList;
/**
  *  User profile of the operator
  */
@property(nonatomic,strong) TIMUserProfile * opUserInfo;
/**
  *  Group member information of the operator
  */
@property(nonatomic,strong) TIMGroupMemberInfo * opGroupMemberInfo;
/**
  *  Modify a member’s information
  */
@property(nonatomic,strong) NSDictionary * changedUserInfo;
/**
  *  Modify a member’s information in the group
  */
@property(nonatomic,strong) NSDictionary * changedGroupMemberInfo;
/**
  *  Current number of group members: valid for TIM_GROUP_TIPS_TYPE_INVITE, TIM_GROUP_TIPS_TYPE_QUIT_GRP,
  *            and TIM_GROUP_TIPS_TYPE_KICKED
  */
@property(nonatomic,assign) uint32_t memberNum;
/**
  *  Operator’s platform
  *  Valid values: iOS, Android, Windows, Mac, Web, RESTful API, Unknown
  */
@property(nonatomic,strong) NSString * platform;
@end
```

The following example shows how to register a new message callback and print event notifications for users joining and quitting the group. The usage of other event notifications is the same. **Example:**

```
@interface TIMMessageListenerImpl : NSObject
- (void)onNewMessage:(NSArray*) msgs;
@end
@implementation TIMMessageListenerImpl
- (void)onNewMessage:(NSArray*) msgs {
    for (TIMMessage * msg in msgs) {
        TIMConversation * conversation = [msg getConversation];

        for (int i = 0; i < [msg elemCount]; i++) {
            TIMElem * elem = [msg getElem:i];
            if ([elem isKindOfClass:[TIMGroupTipsElem class]]) {
                TIMGroupTipsElem * tips_elem = (TIMGroupTipsElem * )elem;
                switch ([tips_elem type]) {
                    case TIM_GROUP_TIPS_TYPE_INVITE:
                        NSLog(@"invite %@ into group %@", [tips_elem userList], [conversation getReceiver]);
                        break;
                    case TIM_GROUP_TIPS_TYPE_QUIT_GRP:
                        NSLog(@"%@ quit group %@", [tips_elem userList], [conversation getReceiver]);
                        break;
                    default:
                        NSLog(@"ignore type");
                        break;
                }
            }
        }
    }
}
@end
```

### Joining a group by a user

**Trigger:** when a user joins a group through application or invitation, the system sends a message in the group. In this case, the developer can choose a display style and update the group list. The type of the received message is `TIM_GROUP_TIPS_TYPE_INVITE`.

**`TIMGroupTipsElem` parameter description:**

Parameter | Description
---|---
type | TIM_GROUP_TIPS_TYPE_INVITE
opUser | Apply to join: the applicant / Invited to join: the inviter
groupName | Group name
userList | List of joined users

### Quitting a group by a user

**Trigger:** when a user quits a group, the system sends a notification in the group. In this case, you can choose to update the group member list. The type of the received message is `TIM_GROUP_TIPS_TYPE_QUIT_GRP`.

**`TIMGroupTipsElem` parameter description:**

Parameter | Description
---|---
type | TIM_GROUP_TIPS_TYPE_QUIT_GRP
opUser | Identifier of the user who quits the group
groupName | Group name

### Removing a user from a group

**Trigger:** when a user is removed from a group, the system sends a notification in the group. In this case, you can choose to update the group member list. The type of the received message is `TIM_GROUP_TIPS_TYPE_KICKED`.

**`TIMGroupTipsElem` parameter description:**

Parameter | Description
---|---
type | TIM_GROUP_TIPS_TYPE_KICKED
opUser | Identifier of the removed user
groupName | Group name

### Setting or canceling an admin

**Trigger:** when a user is set or canceled as an admin, the system sends a notification in the group. If the UI shows whether the user is an admin or not, you can update the admin flag. The type of received messages is `TIM_GROUP_TIPS_TYPE_SET_ADMIN` or `TIM_GROUP_TIPS_TYPE_CANCEL_ADMIN`.

**`TIMGroupTipsElem` parameter description:**

Parameter | Description
---|---
type | Set TIM_GROUP_TIPS_TYPE_SET_ADMIN
Canceled | TIM_GROUP_TIPS_TYPE_CANCEL_ADMIN
opUser | Identifier of the operator
groupName | Group name
userList | List of users who are set or canceled as admins

### Group profile modifications

**Trigger:** when group information, such as the group name or group introduction, is modified, the system sends a message. You can update relevant display fields or display the message to users as needed.

**`TIMGroupTipsElem` parameter description:**

Parameter | Description
---|---
type | TIM_GROUP_TIPS_TYPE_INFO_CHANGE
opUser | Identifier of the operator
groupName | Group name
groupChangeInfo | Modified group information, which is a TIMGroupTipsElemGroupInfo structure list

**`TIMGroupTipsElemGroupInfo` prototype:**

```
/**
  *  Group prompt message, which is group modification information
  */
@interface TIMGroupTipsElemGroupInfo : NSObject
/**
  *  Modification type
  */
@property(nonatomic, assign) TIM_GROUP_INFO_CHANGE_TYPE type;

/**
  *  Have different meanings based on the modification type
  */
@property(nonatomic,strong) NSString * value;
@end
```

**Parameter description:**

Parameter | Description
---|---
type | Modification type
value | Modified value, which has different meanings based on the modification type

### Group member information modifications

**Trigger:** when a group member’s information in a group is modified, such as when the member has been muted or the member’s role in the group has been changed, the system sends a message. You can update relevant display fields or display the message to users as needed.

>
>- The information mentioned here includes only group-related information, such as the muting period and member role change. Information related to users such as the user’s nickname is not included. For groups that have too many members, we recommend that you display the information in the message body instead of updating it in real time. For more information, see [Message sender and related profile](https://intl.cloud.tencent.com/document/product/1047/34321).
>- If the user information is stored locally, you can determine whether a change has occurred according to the information in the message body and update the information after receiving a message from this user.

**`TIMGroupTipsElem` parameter description:**

Parameter | Description
---|---
type | TIM_GROUP_TIPS_TYPE_MEMBER_INFO_CHANGE
opUser | Identifier of the operator
groupName | Group name
memberInfoList | Modified group member information, which is a `TIMGroupTipsElemMemberInfo` structure list

**`TIMGroupTipsElemMemberInfo` prototype:**

```
/**
 *  Group prompt message, which is member modification information
 */
@interface TIMGroupTipsElemMemberInfo : NSObject
/**
 *  User whose information is modified
 */
@property(nonatomic,retain) NSString * identifier;
/**
 *  Muting period in seconds
 */
@property(nonatomic,assign) uint32_t shutupTime;
@end
```

**Parameter description:**

Parameter | Description
---|---
identifier | Identifier of the user whose information is modified
shutupTime | Muting period

### Group event message listeners

The group event messages of ChatRoom and BChatRoom groups are obtained by registering listeners in TIMManager > setUserConfig > TIMUserConfig > groupEventListener. The `Elem` of the message contains the number of group members.

```
/**
 *  Group event notification callback
 */
@protocol TIMGroupEventListener <NSObject>
@optional
/**
 *  Group prompt message callback
 *
 *  @param elem  Group prompt message
 */
- (void)onGroupTipsEvent:(TIMGroupTipsElem*)elem;
@end
```

## Group System Messages

When a user applies to join a group, the group admin receives a system message about the application. The admin can accept or reject the application, and the corresponding group system message will be returned to the user.

**Group system message types:**

```
/**
 *  Group system message type
 */
typedef NS_ENUM(NSInteger, TIM_GROUP_SYSTEM_TYPE){
    /**
     *  Request to join a group (received only by the admin)
     */
    TIM_GROUP_SYSTEM_ADD_GROUP_REQUEST_TYPE              = 0x01,
    /**
     *  Application to join the group is approved (received only by the applicant)
     */
    TIM_GROUP_SYSTEM_ADD_GROUP_ACCEPT_TYPE               = 0x02,
    /**
     *  Application to join the group is rejected (received only by the applicant)
     */
    TIM_GROUP_SYSTEM_ADD_GROUP_REFUSE_TYPE               = 0x03,
    /**
     *  Removed from the group by the admin (received only by the removed user)
     */
    TIM_GROUP_SYSTEM_KICK_OFF_FROM_GROUP_TYPE            = 0x04,
    /**
     *  Group is dismissed (received by all members)
     */
    TIM_GROUP_SYSTEM_DELETE_GROUP_TYPE                   = 0x05,
    /**
     *  A group is created (received only by the creator)
     */
    TIM_GROUP_SYSTEM_CREATE_GROUP_TYPE                   = 0x06,
    /**
     *  Invited to join a group (received by the invitee)
     */
    TIM_GROUP_SYSTEM_INVITED_TO_GROUP_TYPE               = 0x07,
    /**
     *  Quit the group (received by the user who quits the group)
     */
    TIM_GROUP_SYSTEM_QUIT_GROUP_TYPE                     = 0x08,
    /**
     *  An admin is set (received by the new group admin)
     */
    TIM_GROUP_SYSTEM_GRANT_ADMIN_TYPE                    = 0x09,
    /**
     *  Admin role is canceled (received only by the canceled admin)
     */
    TIM_GROUP_SYSTEM_CANCEL_ADMIN_TYPE                   = 0x0a,
    /**
     *  Group is revoked (received by all members)
     */
    TIM_GROUP_SYSTEM_REVOKE_GROUP_TYPE                   = 0x0b,
    /**
     *  Group invitation request (received by the invitee)
     */
    TIM_GROUP_SYSTEM_INVITE_TO_GROUP_REQUEST_TYPE        = 0x0c,
    /**
     *  Group invitation request is approved (received only by the inviter)
     */
    TIM_GROUP_SYSTEM_INVITE_TO_GROUP_ACCEPT_TYPE         = 0x0d,
    /**
     *  Group invitation request is rejected (received only by the inviter)
     */
    TIM_GROUP_SYSTEM_INVITE_TO_GROUP_REFUSE_TYPE         = 0x0e,
    /**
    *  Custom notification (received by all members by default)
    */
    TIM_GROUP_SYSTEM_CUSTOM_INFO                         = 0xff,
 };
/**
 *  Group system message
 */
@interface TIMGroupSystemElem : TIMElem
/**
  * Operation type
  */
@property(nonatomic,assign) TIM_GROUP_SYSTEM_TYPE type;
/**
  * Group ID
  */
@property(nonatomic,strong) NSString * group;
/**
  * Operator
  */
@property(nonatomic,strong) NSString * user;
/**
  * The reason for operation
  */
@property(nonatomic,strong) NSString * msg;
/**
  *  Message identifier, which is irrelevant to the client
  */
@property(nonatomic,assign) uint64_t msgKey;
/**
  *  Message identifier, which is irrelevant to the client
  */
@property(nonatomic,strong) NSData * authKey;
/**
  *  Custom pass-through message body (valid when type ＝ TIM_GROUP_SYSTEM_CUSTOM_INFO)
  */
@property(nonatomic,strong) NSData * userData;
/**
  *  User information of the operator
  */
@property(nonatomic,strong) TIMUserProfile * opUserInfo;
/**
  *  Group member information of the operator
  */
@property(nonatomic,strong) TIMGroupMemberInfo * opGroupMemberInfo;
/**
  *  Operator’s platform
  *  Valid values: iOS, Android, Windows, Mac, Web, RESTful API, Unknown
  */
@property(nonatomic,strong) NSString * platform;
@end
```

**Parameter description:**

Parameter | Description
---|---
type | Message type
group | Group ID
user | Operator
msg | Reason for the operation
msgKey & authKey | Message identifiers that are irrelevant to the client. They are read by the IM SDK in the event of accept and refuse.

The following example shows how to process received group system messages. Applications to join the group are approved by default, and messages notifying that the group was dismissed are printed. **Example:**

```
@interface TIMMessageListenerImpl : NSObject
- (void)onNewMessage:(NSArray*) msgs;
@end
@implementation TIMMessageListenerImpl
- (void)onNewMessage:(NSArray*) msgs {
    for (TIMMessage * msg in msgs) {
        for (int i = 0; i < [msg elemCount]; i++) {
            TIMElem * elem = [msg getElem:i];
            if ([elem isKindOfClass:[TIMGroupSystemElem class]]) {
                TIMGroupSystemElem * system_elem = (TIMGroupSystemElem * )elem;
                switch ([system_elem type]) {
                    case TIM_GROUP_SYSTEM_ADD_GROUP_REQUEST_TYPE:
                        NSLog(@"user %@ request join group  %@", [system_elem user], [system_elem group]);
                        break;
                    case TIM_GROUP_SYSTEM_DELETE_GROUP_TYPE:
                        NSLog(@"group %@ deleted by %@", [system_elem group], [system_elem user]);
                        break;
                    default:
                        NSLog(@"ignore type");
                        break;
                }
            }
        }
    }
}
@end
```

### Applying to join a group by a user

**Trigger:** when a user applies to join a group, the group admin receives a message about the user applying to join the group. You can display the message to the user for the user to decide whether to accept the application. The type of the message is `TIM_GROUP_SYSTEM_ADD_GROUP_REQUEST_TYPE`.

**Parameter description:**

Parameter | Description
---|---
type | TIM_GROUP_SYSTEM_ADD_GROUP_REQUEST_TYPE
group | ID of the group that the user applies to join
user | Applicant
msg | Reason for application (optional)

**Method description:**

- To accept the application, call the accept method.
- To reject the application, call the refuse method.

### Messages for approving or rejecting "apply to join" requests

**Trigger:** when an admin approves an application to join the group, the applicant receives an approval notification message. When the admin rejects the application, the applicant receives a rejection notification message.

**Parameter description:**

Parameter | Description
---|---
type | Approve: TIM_GROUP_SYSTEM_ADD_GROUP_ACCEPT_TYPE<br>Reject: TIM_GROUP_SYSTEM_ADD_GROUP_REFUSE_TYPE
group | ID of the group for which the request is approved or rejected
user | Identifier of the admin who processed the request
msg | Reason for approval or rejection (optional)

### Messages for "invited to join" requests

**Trigger:** when invited to a group, the invitee receives an invitation message. If the invitee approves the invitation, the accept method is called, otherwise the refuse method is called. The type of the message is `TIM_GROUP_SYSTEM_INVITE_TO_GROUP_REQUEST_TYPE`.

**Parameter description:**

Parameter | Description
---|---
type | TIM_GROUP_SYSTEM_INVITE_TO_GROUP_REQUEST_TYPE
group | ID of the group that the user is invited to
user | Inviter

**Method description:**

- To accept the application, call the accept method.
- To reject the application, call the refuse method.

### Messages for approving or rejecting "invited to join" requests

**Trigger:** when the invitee approves the invitation, the inviter receives an approval notification message. When the invitee rejects the invitation, the inviter receives a rejection notification message.

**Parameter description:**

Parameter | Description
---|---
type | Approve: TIM_GROUP_SYSTEM_INVITE_TO_GROUP_ACCEPT_TYPE<br>Reject: TIM_GROUP_SYSTEM_INVITE_TO_GROUP_REFUSE_TYPE
group | ID of the group for which the request is approved or rejected
getOpUser | Identifier of the user who processed the request
msg | Reason for approval or rejection (optional)

### Messages for removing a user by the admin

**Trigger:** when a user is removed from a group by the admin, the user receives a removal notification message.

**Parameter description:**

Parameter | Description
---|---
type | TIM_GROUP_SYSTEM_KICK_OFF_FROM_GROUP_TYPE
group | ID of the group from which the user is removed
user | Identifier of the operating admin

### Messages for dismissing a group

**Trigger:** when a group is dismissed, all members receive a message notifying them that the group is dismissed.

**Parameter description:**

Parameter | Description
---|---
type | TIM_GROUP_SYSTEM_DELETE_GROUP_TYPE
group | The ID of the group that is disbanded
user | Identifier of the operating admin

### Messages for creating a group

**Trigger:** when a group is created, the creator receives a creation notification message. If a user calls the method to create a group and the success callback is returned, the group was created successfully. This message serves the purpose of multi-client synchronization. When receiving this message, the other clients can update the group list, while the current client can choose to ignore it.

**Parameter description:**

Parameter | Description
---|---
type | TIM_GROUP_SYSTEM_CREATE_GROUP_TYPE
group | ID of the created group
user | Creator, who is the user in this case

### Messages for inviting a user to a group

**Trigger:** when a user is invited to a group, the user receives the invitation message. **Initial members are added to the group without invitation when the group is created.**

**Parameter description:**

Parameter | Description
---|---
type | TIM_GROUP_SYSTEM_INVITED_TO_GROUP_TYPE
group | ID of the group that the user is invited to
user | Operator, who is the inviter in this case

**Method description:**

- To accept the application, call the accept method.
- To reject the application, call the refuse method.

### Messages for quitting a group

**Trigger:** when a user quits a group, the user receives a quit notification message, and only the user who quit will receive the message. If the user calls `QuitGroup` and the success callback is returned, the user has quit the group successfully. This message serves the purpose of multi-client synchronization. When receiving this message, the other clients can update the group list, while the current client can choose to ignore it.

**Parameter description:**

Parameter | Description
---|---
type | TIM_GROUP_SYSTEM_QUIT_GROUP_TYPE
group | ID of the group that the user quits
user | Operator, who is the user who quits the group in this case

### Messages for setting or canceling an admin

**Trigger:** when a user is set or canceled as a group admin, the user receives the corresponding notification message.

**Parameter description:**

Parameter | Description
---|---
type | Admin role is canceled: TIM_GROUP_SYSTEM_GRANT_ADMIN_TYPE<br>Admin role is granted: TIM_GROUP_SYSTEM_CANCEL_ADMIN_TYPE
group | ID of the group in which the event occurs
user | Operator

### Messages for revoking a group

**Trigger:** when a group is revoked by the system, all members receive a message notifying that the group was revoked.

**Parameter description:**

Parameter | Description
---|---
type | TIM_GROUP_SYSTEM_REVOKE_GROUP_TYPE
group | ID of the revoked group

