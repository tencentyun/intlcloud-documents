
## Group Overview

Instant Messaging (IM) supports multiple group types. For more information on their characteristics and limits, see [Group System](https://intl.cloud.tencent.com/document/product/1047/33529). A group is identified by a unique ID that enables different operations.

## Group Chat Messages

Group messages and C2C (one-to-one) messages are the same except for the conversation type obtained through ‘Conversation’. For more information, see [Sending Messages](https://intl.cloud.tencent.com/document/product/1047/34321).

## Group Management

Operations related to groups are performed after login through `TIMGroupManager`.

**Prototype for getting a singleton:**

```
@interface TIMGroupManager : NSObject
+ (TIMGroupManager*)sharedInstance;
@end
```

### Creating built-in group types

Instant Messaging (IM) supports the following group types by default: **private group (Private), public group (Public), chat room (ChatRoom), audio-video chat room (AVChatRoom), and broadcasting chat room (BChatRoom)**. For more information, please see [Group Types](https://intl.cloud.tencent.com/document/product/1047/33529#.E7.BE.A4.E7.BB.84.E5.BD.A2.E6.80.81.E4.BB.8B.E7.BB.8D). You can specify the group name and the list of users to add. After the group is created, the group ID is returned, which allows you to receive and send messages through `Conversation`.

**Description of group creation:**

| Method | Description |
| --- | --- |
| CreatePrivateGroup | Creates a private group |
| CreatePublicGroup | Creates a public group |
| CreateChatRoomGroup | Creates a chat room |
| CreateAVChatRoomGroup | Creates a live-streaming group. A live-streaming group supports an unlimited number of members but does not support features such as adding members or querying the total number of members. |

**Prototype:**

```
@interface TIMGroupManager : NSObject
/**
 *  Create a private group
 *
 *  @param members   Group members, NSString* array
 *  @param groupName Group name
 *  @param succ      Success callback
 *  @param fail      Failure callback
 *
 *  @return 0 Successful
 */
- (int)createPrivateGroup:(NSArray*)members groupName:(NSString*)groupName succ:(TIMCreateGroupSucc)succ fail:(TIMFail)fail;
/**
 *  Create a public group
 *
 *  @param members   Group members, NSString* array
 *  @param groupName Group name
 *  @param succ      Success callback
 *  @param fail      Failure callback
 *
 *  @return 0 Successful
 */
- (int)createPublicGroup:(NSArray*)members groupName:(NSString*)groupName succ:(TIMCreateGroupSucc)succ fail:(TIMFail)fail;
/**
 *  Create a chat room
 *
 *  @param members   Group members, NSString* array
 *  @param groupName Group name
 *  @param succ      Success callback
 *  @param fail      Failure callback
 *
 *  @return 0 Successful
 */
- (int)createChatRoomGroup:(NSArray*)members groupName:(NSString*)groupName succ:(TIMCreateGroupSucc)succ fail:(TIMFail)fail;
/**
 *  Create an audio-video chat room (ultra-large groups are supported, see the wiki documentation)
 *
 *  @param groupName Group name
 *  @param succ      Success callback
 *  @param fail      Failure callback
 *
 *  @return 0 Successful
 */
- (int)createAVChatRoomGroup:(NSString*)groupName succ:(TIMCreateGroupSucc)succ fail:(TIMFail)fail;
@end
```

**Parameter description:**

Parameter | Description
---|---
members | A NSString list of members to be added to the group. The creator is added by default. Public, Private, and ChatRoom groups support up to 6,000 members. AVChatRoom groups can support an unlimited number of members.
groupName | The group name is of NSString type and its length is up to 30 bytes
groupId | The group ID that you specified, NSString type
succ | Success callback that returns the group ID
fail | Failure callback

The following example creates a private group and adds user “iOS_002” to the group. **Example:**

>
>- There is no need to explicitly specify the creator as the creator is added to the group by default.
>- The methods and parameters of public groups and chat rooms are identical but have different method names.

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

### Creating group with specified properties

When creating a group, you can set default members and the group name as well as the group announcement and group introduction.

```
/**
 *  Create group parameters
 */
@interface TIMCreateGroupInfo : TIMCodingModel
/**
 *  The group ID. If nil, use the system’s default ID.
 */
@property(nonatomic,retain) NSString* group;
/**
 *  Group name
 */
@property(nonatomic,retain) NSString* groupName;
/**
 *  Group type: Private, Public, ChatRoom, AVChatRoom
 */
@property(nonatomic,retain) NSString* groupType;
/**
 *  Whether to set the option for joining the group. Set to false for private groups.
 */
@property(nonatomic,assign) BOOL setAddOpt;
/**
 *  Option for joining group
 */
@property(nonatomic,assign) TIMGroupAddOpt addOpt;
/**
 *  The maximum number of members. If 0 is entered, then the system uses the default value.
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
 *  Collection of custom fields. Key is of NSString* type and value is of NSData* type.
 */
@property(nonatomic,retain) NSDictionary* customInfo;
/**
 *  Create a list of members (TIMCreateGroupMemberInfo*)
 */
@property(nonatomic,retain) NSArray* membersInfo;
@end

@interface TIMGroupManager : NSObject
/**
 *  Create group
 *
 *  @param groupInfo Group information
 *  @param succ      Success callback
 *  @param fail      Failure callback
 *
 *  @return 0 Successful
 */
- (int)createGroup:(TIMCreateGroupInfo*)groupInfo succ:(TIMCreateGroupSucc)succ fail:(TIMFail)fail;
@end
```

**Parameter description:**

Parameter | Description
---|---
groupInfo | Group ID, group name, group type, option for joining group, maximum number of members, group announcement, group introduction, and group profile photo
succ | Success callback
fail | Failure callback

The following example creates a private group with specified properties and adds user “iOS_001” to the group. You do not need to explicitly specify the creator as the creator is added to the group by default. **Example:**

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
 *  Create group
 *
 *  @param type      Group type: Private, Public, ChatRoom, AVChatRoom
 *  @param groupId    The custom group ID. The system automatically assigns a group ID if it is empty.
 *  @param groupName  Group name
 *  @param succ       Success callback
 *  @param fail       Failure callback
 *
 *  @return 0 Successful
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
groupId | The custom group ID
succ | Success callback
fail | Failure callback

### Inviting users to a group

You can invite users to a group through `inviteGroupMember` of `TIMGroupManager`.

**Permission description:**

For more information, see [Differences in group member operations](https://intl.cloud.tencent.com/document/product/1047/33529#.E7.BE.A4.E6.88.90.E5.91.98.E6.93.8D.E4.BD.9C.E5.B7.AE.E5.BC.82). 

**Prototype:**

```
@interface TIMGroupManager : NSObject
/**
 *  Invite friends to a group
 *
 *  @param group   Group ID
 *  @param members The list of users who will be added to the group (NSString* array)
 *  @param succ    Success callback
 *  @param fail    Failure callback
 *
 *  @return 0 Successful
 */
- (int)inviteGroupMember:(NSString*)group members:(NSArray*)members succ:(TIMGroupMemberSucc)succ fail:(TIMFail)fail;
@end
```

**Parameter description:**

Parameter | Description
---|---
group | The group ID, which is of NSString type
members | NSString list of users who will be added to the group
succ | The success callback that returns the list of members who are added to the group successfully and the success status. It is a TIMGroupMemberResult array.
fail | Failure callback

The following example invites user “iOS_002” to join the group with the group ID of “TGID1JYSZEAEQ” and returns the operation list and success status after the operation succeeds. `result.status` indicates whether the current user’s operation was successful. **Example:**

```
NSMutableArray * members = [[NSMutableArray alloc] init];
// Add user iOS_002
[members addObject:@"iOS_002"];
// @"TGID1JYSZEAEQ" is the group ID
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
	Operation failed.
	*/
	TIM_GROUP_MEMBER_STATUS_FAIL              = 0,
	/**
	*  Successful operation
	*/
	TIM_GROUP_MEMBER_STATUS_SUCC              = 1,
	/**
	*  Operation is invalid. The user is already a group member when added to the group, or the user is not a group member when removed from the group
	*/
	TIM_GROUP_MEMBER_STATUS_INVALID           = 2,
    /**
    *  Pending processing. Wait for the invitee to process.
    */
    TIM_GROUP_MEMBER_STATUS_PENDING           = 3,
};
```

### Applying to join a group

`joinGroup` of `TIMGroupManager` allows users to apply to join a group. This operation is valid only for public groups, chat rooms, and audio-video chat rooms.

**Permission description:**
For more information, see [Differences in group member operations](https://intl.cloud.tencent.com/document/product/1047/33529#.E7.BE.A4.E6.88.90.E5.91.98.E6.93.8D.E4.BD.9C.E5.B7.AE.E5.BC.82).

**Prototype:**

```
@interface TIMGroupManager : NSObject
/**
 *  Apply to join group
 *
 *  @param group The ID of the target group
 *  @param msg   Application message
 *  @param succ  Success callback (application succeeds, pending approval)
 *  @param fail  Failure callback
 *
 *  @return 0 Successful
 */
- (int)joinGroup:(NSString*)group msg:(NSString*)msg succ:(TIMSucc)succ fail:(TIMFail)fail;
@end
```

**Parameter description:**

Parameter | Description
---|---
group | The group ID, which is of NSString type
msg | Reason for application
succ | Success callback
fail | Failure callback

In the following example, a user applies to join the group “TGID1JYSZEAEQ” and the reason for application is “Apply Join Group”. **Example:**

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

- **Private group:** every member can quit the group.
- **Public group, chat room, and live-streaming group:** the group owner cannot quit the group.

For more information, see [Differences in group member operations](https://intl.cloud.tencent.com/document/product/1047/33529#.E7.BE.A4.E6.88.90.E5.91.98.E6.93.8D.E4.BD.9C.E5.B7.AE.E5.BC.82).

**Prototype:**

```
@interface TIMGroupManager : NSObject
/**
 *  Quit group
 *
 *  @param group            Group ID
 *  @param succ  Success callback
 *  @param fail  Failure callback
 *
 *  @return 0 Successful
 */
- (int)quitGroup:(NSString*)group succ:(TIMSucc)succ fail:(TIMFail)fail;
@end
```

**Parameter description:**

Parameter | Description
---|---
group | The group ID, which is of NSString type
succ | Success callback
fail | Failure callback

In the following example, a user quits the group “TGID1JYSZEAEQ”. **Example:**

```
// @"TGID1JYSZEAEQ" is the group ID
[[TIMGroupManager sharedInstance] quitGroup:@"TGID1JYSZEAEQ" succ:^() {
	NSLog(@"succ");
} fail:^(int code, NSString* err) {
	NSLog(@"failed code: %d %@", code, err);
}];
```

### Deleting group members

Group members can delete other members. The parameters of this function are the same as the parameters for joining a group.

**Permission description:**
For more information, see [Differences in group member operations](https://intl.cloud.tencent.com/document/product/1047/33529#.E7.BE.A4.E6.88.90.E5.91.98.E6.93.8D.E4.BD.9C.E5.B7.AE.E5.BC.82).

**Prototype:**

```
@interface TIMGroupManager : NSObject
/**
 *  Delete group members
 *
 *  @param group   Group ID
 * @param reason  Reason for deleting
 *  @param members List of members to be deleted
 *  @param succ    Success callback
 *  @param fail    Failure callback
 *
 *  @return 0 Successful
 */
- (int)deleteGroupMemberWithReason:(NSString*)group reason:(NSString*)reason members:(NSArray*)members succ:(TIMGroupMemberSucc)succ fail:(TIMFail)fail;
@end
```

**Parameter description:**

Parameter | Description
---|---
group | The group ID, which is of NSString type
reason | The reason, which is of NSString type
members | List of members who are operated on. It is an `NSString*` array.
succ | The success callback that returns the list of members who are added to the group successfully and the success status. It is a `TIMGroupMemberResult` array.
fail | Failure callback

The following example deletes user “iOS_002” from group “TGID1JYSZEAEQ” and returns the operation list and operation status after the deletion succeeds. **Example:**

```
NSMutableArray * members = [[NSMutableArray alloc] init];
// Add user iOS_002
[members addObject:@"iOS_002"];
// @"TGID1JYSZEAEQ" is the group ID
[[TIMGroupManager sharedInstance] deleteGroupMemberWithReason:@"TGID1JYSZEAEQ" reason:@"broke group rules" members:members succ:^(NSArray* arr) {
	for (TIMGroupMemberResult * result in arr) {
		NSLog(@"user %@ status %d", result.member, result.status);
	}
} fail:^(int code, NSString* err) {
	NSLog(@"failed code: %d %@", code, err);
}];
```

### Obtaining the group member list

Get a group member list through the `getGroupMembers` method.

**Permission description:**

- **Any type of group:** the list of members can be obtained.
- **Live-streaming group:** only some of the members are pulled, including the group owner, admin, and some members.

For more information, see [Differences in group operations](https://intl.cloud.tencent.com/document/product/1047/33529#.E7.BE.A4.E7.BB.84.E6.93.8D.E4.BD.9C.E5.B7.AE.E5.BC.82). 

**Prototype:**

```
/**
 *  Returned values of group member operations
 */
@interface TIMGroupMemberInfo : TIMCodingModel
/**
 *  The member that is operated on
 */
@property(nonatomic,retain) NSString* member;
/**
 *  Group name card
 */
@property(nonatomic,retain) NSString* nameCard;
/**
 *  The time of joining the group
 */
@property(nonatomic,assign) time_t joinTime;
/**
 *  Member’s role in the group
 */
@property(nonatomic,assign) TIMGroupMemberRole role;
/**
 *  Muting duration (the remaining seconds)
 */
@property(nonatomic,assign) uint32_t silentUntil;
/**
 *  Collection of custom fields. Key is of NSString* type and value is of NSData* type.
 */
@property(nonatomic,retain) NSDictionary* customInfo;
@end

@interface TIMGroupManager : NSObject
/**
 *  Get group member list
 *
 *  @param group            Group ID
 *  @param succ  Success callback (TIMGroupMemberInfo list)
 *  @param fail  Failure callback
 *
 *  @return 0 Successful
 */
- (int)getGroupMembers:(NSString*)groupId succ:(TIMGroupMemberSucc)succ fail:(TIMFail)fail;
@end
```

**Parameter description:**

Parameter | Description
---|---
group | The group ID, which is of NSString\* type
succ | Success callback that returns a TIMGroupMemberInfo\* array
fail | Failure callback

This example gets the member list of group “TGID1JYSZEAEQ”. `list` is `TIMGroupMemberInfo*` data and stores member information. **Example:**

```
// @"TGID1JYSZEAEQ" is the group ID
[[TIMGroupManager sharedInstance] getGroupMembers:@"TGID1JYSZEAEQ" succ:^(NSArray* list) {
	for (TIMGroupMemberInfo * info in list) {
		NSLog(@"user=%@ joinTime=%lu role=%d", info.member, info.joinTime, info.role);
	}
} fail:^(int code, NSString * err) {
	NSLog(@"failed code: %d %@", code, err);
}];
```

If a group has too many members, use the **paging API**. **Prototype:**

```
@interface TIMGroupManager : NSObject
/**
 *  Get the list of members whose type you specify (the list can be pulled by field and in pages)
 *
 *  @param group      Group ID: NSString* list
 *  @param filter     Group member role filter
 *  @param flags      The flag of the profile to be pulled
 *  @param custom     The list of custom keys (NSString*) to get
 * @param nextSeq     The flag for pulling in pages. Enter 0 for the first request. If the success callback returns a value that is not 0, then the list will be pulled in pages. Pass this parameter to pull again until the value becomes 0.
 *  @param succ       Success callback
 *  @param fail       Failure callback
 */
- (int)getGroupMembers:(NSString*)group ByFilter:(TIMGroupMemberFilter)filter flags:(TIMGetGroupMemInfoFlag)flags custom:(NSArray*)custom nextSeq:(uint64_t)nextSeq succ:(TIMGroupMemberSuccV2)succ fail:(TIMFail)fail;
@end
```

### Obtaining your group list

Get the list of groups the current user has joined through `getGroupList`.

**Permission description:**

- Get the list of groups you have joined. The returned `TIMGroupInfo` contains only `group`, `groupName`, and `groupType`.
- Only some of the live-streaming groups the user has joined can be obtained.

**Prototype:**

```
@interface TIMGroupManager : NSObject
/**
 *  Get group list
 *
 *  @param succ Success callback. The NSArray list is TIMGroupInfo. The structure contains only group\groupName\groupType\faceUrl\selfInfo.
 *  @param fail   Failure callback
 *
 *  @return 0 Successful
 */
- (int)getGroupList:(TIMGroupListSucc)succ fail:(TIMFail)fail;
@end
```

**Parameter description:**

Parameter | Description
---|---
succ | Success callback that returns the list of group IDs. It is a TIMGroupInfo array.
fail | Failure callback

The following example gets a group list and prints group IDs, group types (Private, Public, ChatRoom), and group names. **Example:**

```
[[TIMGroupManager sharedInstance] getGroupList:^(NSArray * list) {
	for (TIMGroupInfo * info in list) {
		NSLog(@"group=%@ type=%@ name=%@", info.group, info.groupType, info.groupName);
	}
} fail:^(int code, NSString* err) {
	NSLog(@"failed code: %d %@", code, err);
}];
```

### Disbanding groups

Disband groups through `DeleteGroup`.

**Permission description:**

For more information, see [Differences in group operations](https://intl.cloud.tencent.com/document/product/1047/33529#.E7.BE.A4.E7.BB.84.E6.93.8D.E4.BD.9C.E5.B7.AE.E5.BC.82). 


**Prototype:**

```
@interface TIMGroupManager : NSObject

/**
 *  Disband group
 *
 *  @param group            Group ID
 *  @param succ  Success callback
 *  @param fail  Failure callback
 *
 *  @return 0 Successful
 */
- (int)deleteGroup:(NSString*)group succ:(TIMSucc)succ fail:(TIMFail)fail;

@end
```

**Parameter description:**

Parameter | Description
---|---
group | Group ID
succ | Success callback that returns group ID list. It is an NSString array.
fail | Failure callback

The following example disbands the group “TGID1JYSZEAEQ”. **Example:**

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
 *  Transfer group to a new group owner
 *
 *  @param group      Group ID
 *  @param identifier The ID of the new group owner
 *  @param succ       Success callback
 *  @param fail       Failure callback
 *
 *  @return 0 Successful
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

The following example transfers group “TGID1JYSZEAEQ” to user “iOS_001”. **Example:**

```
[[TIMGroupManager sharedInstance] modifyGroupOwner:@"TGID1JYSZEAEQ" user:@"iOS_001" succ:^() {
	NSLog(@"set new owner succ");
}fail:^(int code, NSString* err) {
	NSLog(@"failed code: %d %@", code, err);
}];
```

### Muting all members

Set Mute All through `modifyGroupAllShutup`.

**Permission description:**

- The **group owner and admin** can mute all members.
- **All group types** support muting all members.

**Prototype:**

```
@interface TIMGroupManager : NSObject
/**
 *  Modify Mute All property
 *
 *  @param group   Group ID
 *  @param shutup  Whether to mute or not
 *  @param succ    Success callback
 *  @param fail    Failure callback
 *
 *  @return 0 Successful
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

This example sets Mute All for the group “TGID1JYSZEAEQ”. Get the Mute All property on the client through `getGroupList` and `getGroupInfo`. **Example:**

```
[[TIMGroupManager sharedInstance] modifyGroupAllShutup:@"TGID1JYSZEAEQ" shutup:YES succ:^() {
	NSLog(@"set all shutup succ");
}fail:^(int code, NSString* err) {
	NSLog(@"failed code: %d %@", code, err);
}];
```

## Getting Group Profiles

### Getting group profiles

You can use the `getGroupInfo` method of `TIMGroupManager` to get group profiles stored on the server and use the `queryGroupInfo` method to get group profiles cached locally. Group profiles are defined by `TIMGroupInfo`.  

**Permission description:**

- The group members of public and private groups can pull group profiles.
- For a public group, non-members can pull profile fields including group, groupName, owner, groupType, createTime, maxMemberNum, memberNum, introduction, faceURL, addOpt, onlineMemberNum, and customInfo. For a private group, non-members cannot pull any group profile information.

**Prototype:**

```
/**
 *  Group profile information
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
 *  Group creator/admin
 */
@property(nonatomic,retain) NSString * owner;
/**
 *  Group type: Private, Public, and ChatRoom
 */
@property(nonatomic,retain) NSString* groupType;
/**
 *  The time the group was created
 */
@property(nonatomic,assign) uint32_t createTime;
/**
 *  The time the group profile was last modified
 */
@property(nonatomic,assign) uint32_t lastInfoTime;
/**
 *  The time the last group message was sent
 */
@property(nonatomic,assign) uint32_t lastMsgTime;
/**
 *  The maximum number of members
 */
@property(nonatomic,assign) uint32_t maxMemberNum;
/**
 *  The number of group members
 */
@property(nonatomic,assign) uint32_t memberNum;
/**
 *  The option for joining group
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
 *  The last message
 */
@property(nonatomic,retain) TIMMessage* lastMsg;
/**
 *  The number of online members
 */
@property(nonatomic,assign) uint32_t onlineMemberNum;
/**
 *  Whether or not the group can be searched for
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
 *  Collection of custom fields. Key is of NSString* type and value is of NSData* type.
 */
@property(nonatomic,retain) NSDictionary* customInfo;
@end

@interface TIMGroupManager : NSObject
/**
 *  Get group profiles stored on the server
 *
 *  @param groups List of group IDs
 *  @param succ Success callback with selfInfo excluded
 *  @param fail   Failure callback
 *
 *  @return 0 Successful
 */
- (int)getGroupInfo:(NSArray*)groups succ:(TIMGroupListSucc)succ fail:(TIMFail)fail;
/**
 *  Get group profiles stored locally
 *
 *  @param group            Group ID
 *
 *  @return Group profile
 */
- (TIMGroupInfo *)queryGroupInfo:(NSString *)group;
@end
```

**Parameter description:**

Parameter | Description
---|---
groups | List of groups for which profiles are to be obtained, NSString array
succ | Success callback that returns the list of group profiles. It is a TIMGroupInfo array.
fail | Failure callback

The following example gets the detailed information of the group “TGID1JYSZEAEQ”. **Example:**

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

### Getting your own profile in a group

**Permission description:**

**Live-streaming group:** your own profile cannot be pulled.

**Prototype:**

```
@interface TIMGroupManager : NSObject
/**
 *  Get your own member information in the group
 *
 *  @param group            Group ID
 * @param succ Success callback that returns the information
 *  @param fail  Failure callback
 *
 *  @return 0 Successful
 */
- (int)getGroupSelfInfo:(NSString*)groupId succ:(TIMGroupSelfSucc)succ fail:(TIMFail)fail;
@end
```

**Parameter description:**

Parameter | Description
---|---
groupId | Group ID
succ | Success callback that returns your own profile in the group
fail | Failure callback

### Getting the profiles of specified members in the group

**Permission description:**

- ***Live-streaming group:** only the profiles of some members can be pulled, including the group owner, admin, and some members.

**Prototype:**

```
@interface TIMGroupManager : NSObject
/**
 *
 *  To get the profiles of specified members in the group, you need to set members. For information on other limits, please see getGroupMembers.
 *
 *  @param groupId Group ID
 *  @param members List of member IDs (NSString*)
 *  @param succ    Success callback (TIMGroupMemberInfo list)
 *  @param fail    Failure callback
 *
 *  @return 0: successful. 1: failed.
 */
- (int)getGroupMembersInfo:(NSString*)groupId members:(NSArray<NSString *>*)members succ:(TIMGroupMemberSucc)succ fail:(TIMFail)fail;
@end
```

**Parameter description:**

Parameter | Description
---|---
groupId | Group ID
members | List of member IDs
succ | Success callback that returns the list of group member profiles
fail | Failure callback

## Modifying the Group Profile

### Modifying the group name

Modify the group name through `modifyGroupName`.

**Permission description:**

- **Public group, chat room, and live-streaming group:** only the group owner or admin can modify the group name.
- **Private group:** any member can modify the group name.

**Prototype:**

```
@interface TIMGroupManager : NSObject
/**
 *  Modify the group name
 *
 *  @param group     Group ID
 *  @param groupName The new group name
 *  @param succ      Success callback
 *  @param fail      Failure callback
 *
 *  @return 0 Successful
 */
- (int)modifyGroupName:(NSString*)group groupName:(NSString*)groupName succ:(TIMSucc)succ fail:(TIMFail)fail;
@end
```

**Parameter description:**

Parameter | Description
---|---
group | Group ID
groupName | The modified group name
succ | Success callback
fail | Failure callback

The following example changes the name of group “TGID1JYSZEAEQ” to “ModifyGroupName”. **Example:**

```
[[TIMGroupManager sharedInstance] modifyGroupName:@"TGID1JYSZEAEQ" groupName:@"ModifyGroupName" succ:^() {
	NSLog(@"modify group name succ");
}fail:^(int code, NSString* err) {
	NSLog(@"failed code: %d %@", code, err);
}];
```

### Modifying the group introduction

Modify the group introduction through `modifyGroupIntroduction`.

**Permission description:**

- **Public group, chat room, and live-streaming group:** only the group owner or admin can modify the group introduction.
- **Private group:** any member can modify the group introduction.

**Prototype:**

```
@interface TIMGroupManager : NSObject

/**
 *  Modify group introduction
 *
 *  @param group            Group ID
 *  @param introduction     Group introduction
 *  @param succ             Success callback
 *  @param fail             Failure callback
 *
 *  @return 0 Successful
 */
- (int)modifyGroupIntroduction:(NSString*)group introduction:(NSString*)introduction succ:(TIMSucc)succ fail:(TIMFail)fail;

@end
```

**Parameter description:**

Parameter | Description
---|---
group | Group ID
introduction | Group introduction, the length cannot exceed 120 bytes
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

Modify group announcement through `modifyGroupNotification`.

**Permission description:**

- **Public, ChatRoom, and BChatRoom groups:** only the group owner or admin can modify the group announcement.
- **Private group:** any member can modify the group announcement.

**Prototype:**

```
@interface TIMGroupManager : NSObject
/**
 *  Modify group announcement
 *
 *  @param group            Group ID
 *  @param notification     Group notification, the length cannot exceed 150 bytes
 *  @param succ             Success callback
 *  @param fail             Failure callback
 *
 *  @return 0 Successful
 */
- (int)modifyGroupNotification:(NSString*)group notification:(NSString*)notification succ:(TIMSucc)succ fail:(TIMFail)fail;
@end
```

**Parameter description:**

Parameter | Description
---|---
group | Group ID
notification | Group notification, the length cannot exceed 150 bytes
succ | Success callback
fail | Failure callback

The following example changes the notification of group “TGID1JYSZEAEQ” to “test notification”. **Example:**

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

- **Public, ChatRoom, and BChatRoom groups:** only the group owner or admin can modify the group profile photo.
- **Private group:** any member can modify the group profile photo.

**Prototype:**

```
@interface TIMGroupManager : NSObject
/**
 *  Modify group profile photo
 *
 *  @param group            Group ID
 *  @param url              URL of the group profile photo (cannot exceed 100 bytes)
 *  @param succ             Success callback
 *  @param fail             Failure callback
 *
 *  @return 0 Successful
 */
- (int)modifyGroupFaceUrl:(NSString*)group url:(NSString*)url succ:(TIMSucc)succ fail:(TIMFail)fail;
@end
```

**Parameter description:**

Parameter | Description
---|---
group | Group ID
url | URL of the group profile photo (cannot exceed 100 bytes)
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

### Modifying the option for joining the group

You can modify the option for joining a group through `modifyGroupAddOpt`.

**Permission description:**

- **Public group, chat room, and live-streaming group:** only the group owner or admin can modify the option for joining the group.
- **Private group:** users can join the group only through invitation and not application.

**Prototype:**

```
@interface TIMGroupManager : NSObject

/**
 *  Modify the option for joining group
 *
 *  @param group            Group ID
 *  @param opt              Option for joining group, see TIMGroupAddOpt
 *  @param succ             Success callback
 *  @param fail             Failure callback
 *
 *  @return 0 Successful
 */
- (int)modifyGroupAddOpt:(NSString*)group opt:(TIMGroupAddOpt)opt succ:(TIMSucc)succ fail:(TIMFail)fail;
@end
```

**Parameter description:**

Parameter | Description
---|---
group | Group ID
opt | The option for joining the group, which can be set to one of the following: allow anyone to join, approval required, forbid anyone to join
succ | Success callback
fail | Failure callback

The following example sets the option for joining the group “TGID1JYSZEAEQ” to “forbid anyone to join”. **Example:**

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
 *  Modify a collection of group custom fields
 *
 *  @param group      Group ID
 *  @param customInfo Collection of custom fields. Key is of NSString* type and value is of NSData* type.
 *  @param succ       Success callback
 *  @param fail       Failure callback
 *
 *  @return 0 Successful
 */
- (int)modifyGroupCustomInfo:(NSString*)group customInfo:(NSDictionary*)customInfo succ:(TIMSucc)succ fail:(TIMFail)fail;
@end
```

**Parameter description:**

Parameter | Description
---|---
group | Group ID
customInfo | Collection of custom fields. Key is of NSString\* type and value is of NSData\* type.
succ | Success callback
fail | Failure callback

The following example sets the option for joining the group “TGID1JYSZEAEQ” to “forbid anyone to join”. **Example:**

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

### Modifying a member’s role in the group

You can modify a member’s role in the group through `modifyGroupMemberInfoSetRole`.

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
identifier | The ID of the group member whose name card is to be modified
role | The modified role, which can not be the group owner
succ | Success callback
fail | Failure callback

The following example sets user “iOS_001” as the admin of group “TGID1JYSZEAEQ”. **Example:**

```
[[TIMGroupManager sharedInstance] modifyGroupMemberInfoSetRole:@"TGID1JYSZEAEQ" user:@"iOS_001" role:TIM_GROUP_MEMBER_ADMIN succ:^() {
	NSLog(@"modify group member role succ");
}fail:^(int code, NSString* err) {
	NSLog(@"failed code: %d %@", code, err);
}];
```



### Muting group members

You can mute group members and set the duration of muting through `modifyGroupMemberInfoSetSilence`.

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
identifier | The ID of the group member to be muted
stime | Muting duration in seconds
succ | Success callback
fail | Failure callback

The following example mutes member “iOS_001” in group “TGID1JYSZEAEQ” for 120 seconds. **Example:**

```
[[TIMGroupManager sharedInstance] modifyGroupMemberInfoSetSilence:@"TGID1JYSZEAEQ" user:@"iOS_001" stime:120 succ:^() {
	NSLog(@"modify group member silence succ");
}fail:^(int code, NSString* err) {
	NSLog(@"failed code: %d %@", code, err);
}];
```

### Modifying a group member’s name card

You can modify a member’s name card in the group through `modifyGroupMemberInfoSetNameCard`.

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
identifier | The ID of the group member whose name card is to be modified
nameCard | The name card to be modified
succ | Success callback
fail | Failure callback

The following example sets the name card of user “iOS_001” in group “TGID1JYSZEAEQ” to “iOS_001_namecard”. **Example:**

```
[[TIMGroupManager sharedInstance] modifyGroupMemberInfoSetNameCard:@"TGID1JYSZEAEQ" user:@"iOS_001" nameCard:@"iOS_001_namecard" succ:^() {
	NSLog(@"modify group member namecard succ");
}fail:^(int code, NSString* err) {
	NSLog(@"failed code: %d %@", code, err);
}];
```



### Modifying group member custom fields

Modify group member custom fields through `modifyGroupMemberInfoSetCustomInfo`.

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
identifier | The ID of the group member for whom you want to set a custom property
customInfo | Collection of custom fields. Key is of NSString\* type and value is of NSData\* type.
succ | Success callback
fail | Failure callback

The following example sets a custom property for user “iOS_001” in group “TGID1JYSZEAEQ”. **Example:**

```
[[TIMGroupManager sharedInstance] modifyGroupMemberInfoSetCustomInfo:@"TGID1JYSZEAEQ" user:@"iOS_001" customInfo:customInfo succ:^() {
	NSLog(@"modify group member customInfo succ");
}fail:^(int code, NSString* err) {
	NSLog(@"failed code: %d %@", code, err);
}];
```

### Modifying the option for receiving group messages

You can set the option for receiving group messages through `modifyReceiveMessageOpt`. By default, public and private groups receive and push group messages offline. Chat rooms and live-streaming groups receive but do not push group messages offline.

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
opt | The option for receiving messages
succ | Success callback
fail | Failure callback

The following example sets the option for receiving messages in the group “TGID1JYSZEAEQ” to receive online messages and not receive offline push. **Example:**

```
[[TIMGroupManager sharedInstance] modifyReciveMessageOpt:@"TGID1JYSZEAEQ" opt:TIM_GROUP_RECEIVE_NOT_NOTIFY_MESSAGE succ:^() {
	NSLog(@"modify receive group message option succ");
}fail:^(int code, NSString* err) {
	NSLog(@"failed code: %d %@", code, err);
}];
```

## Group Pending Requests

### Pulling group pending requests

You can pull group pending requests through `getPendencyFromServer`. Group pending requests are group-related operations that require approval, such as pending “apply to join” requests and pending “invited to join” requests. Even after a pending request is approved or rejected, the information can still be pulled through this API. In this case, the message pulled has a “processed” flag.

**Permission description:**

The **approver** has the permission to pull the information.

>?
>- If user A applies to join group A, the group admin can obtain information related to this pending request. As user A does not have approval permission, user A does not need to pull information related to this pending request.
>- If admin A invites user A to join group A, user A can obtain the information related to this pending request because this pending request needs to be approved by user A.

**Prototype:**

```
@interface TIMGroupManager : NSObject
/**
 *  Get the list of group pending requests
 *
 *  @param option Pending parameter configuration
 *  @param succ   Success callback that returns the list of pending requests
 *  @param fail   Failure callback
 *
 *  @return 0 Successful
 */
- (int)getPendencyFromServer:(TIMGroupPendencyOption*)option succ:(TIMGetGroupPendencyListSucc)succ fail:(TIMFail)fail;
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
| timestamp | The start timestamp for pulling. If pending items are pulled from the latest one, enter 0 or leave it empty. In the event of paging, the callback returns the start timestamp of the next page. |
| numPerPage | The number of items pulled at a time. This parameter is used for paging. |

**Callback prototype:**

```
/**
 *  Getting the list of group pending requests succeeds
 *
 *  @param meta       Metadata of pending request
 *  @param pendencies Array of pending request list (TIMGroupPendencyItem)
 */
typedef void (^TIMGetGroupPendencyListSucc)(TIMGroupPendencyMeta * meta, NSArray * pendencies);
```

**Callback parameter description:**

Parameter | Description
---|---
meta | Information returned by the pull operation, including paging information and pulling status
pendencies | Array of pending items that are pulled

**Property description:**

Property | Description
---|---
nextStartTime | The start timestamp for pulling the next page. If the value is 0, there are no more pages.
readTimeSeq | The read timestamp for determining whether a pending item has been read or not
unReadCnt | The number of unread items, not limited to the current page

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
  *  The ID of the requester, who is the requester for an “apply to join” request and the inviter for an “invited to join” request.
  */
@property(nonatomic,retain) NSString* fromUser;
/**
  *  The ID of the handler. The ID is 0 for an “apply to join” request and the invitee for an “invited to join” request.
  */
@property(nonatomic,retain) NSString* toUser;
/**
  *  The time the pending request was added
  */
@property(nonatomic,assign) uint64_t addTime;
/**
  *  The type of the pending request
  */
@property(nonatomic,assign) TIMGroupPendencyGetType getType;
/**
  *  “Processed” flag
  */
@property(nonatomic,assign) TIMGroupPendencyHandleStatus handleStatus;
/**
  *  Processing result
  */
@property(nonatomic,assign) TIMGroupPendencyHandleResult handleResult;
/**
  ** Additional information of application or invitation
  */
@property(nonatomic,retain) NSString* requestMsg;
/**
  *  Processing information: approval or rejection information
  */
@property(nonatomic,retain) NSString* handledMsg;
/**
  *  Approve application
  *
  *  @param msg      Reason for approval (optional)
  *  @param succ     Success callback
  *  @param fail     Failure callback, which returns the error code and error description
  */
-(void) accept:(NSString*)msg succ:(TIMSucc)succ fail:(TIMFail)fail;
/**
  *  Reject application
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
fromUser | The ID of the pending request initiator
toUser | The ID of the pending request handler
addTime | The time the pending request was added
getType | Enumerate pending request types: apply to join, invited to join
handleStatus | Enumerates the pending request status: pending, processed by another user, processed by handler (for example, when user A applies to join the group and admin A approves the application, the status of this pending item pulled by admin B is “processed by another user”.)
handleResult | Enumerates the processing result: approve, reject
requestMsg/handleMsg | The message left during application or processing

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

The IM SDK can report that the current pending request and all the pending requests before it have been read. After the report, you can still pull these pending requests and determine whether they are read through the read timestamp.

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
 *  @return 0 Successful
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
 *  Approve application
 *
 *  @param msg      Reason for approval (optional)
 *  @param succ     Success callback
 *  @param fail     Failure callback, which returns the error code and error description
 */
- (void)accept:(NSString*)msg succ:(TIMSucc)succ fail:(TIMFail)fail;
/**
 *  Reject application
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

When a user is invited to join a group or is removed from a group, a tips message is displayed in the group. The caller can decide whether to display and how to display the tips message (for example, ignore it or display it to users as needed). A tips message is identified by a special `Elem` and returned by the new message callback. Please see [New message notification](/doc/product/269/9148#.E6.96.B0.E6.B6.88.E6.81.AF.E9.80.9A.E7.9F.A5). 



**Message prototype:**

```
/**
 *  Group tips type
 */
typedef NS_ENUM(NSInteger, TIM_GROUP_TIPS_TYPE){
    /**
     *  Invited to join group (opUser & groupName & userList)
     */
    TIM_GROUP_TIPS_TYPE_INVITE              = 0x01,
    /**
     *  Quit group (opUser & groupName & userList)
     */
    TIM_GROUP_TIPS_TYPE_QUIT_GRP            = 0x02,
    /**
     *  Kicked out of group (opUser & groupName & userList)
     */
    TIM_GROUP_TIPS_TYPE_KICKED              = 0x03,
    /**
     *  Admin is set (opUser & groupName & userList)
     */
    TIM_GROUP_TIPS_TYPE_SET_ADMIN           = 0x04,
    /**
     *  Admin is cancelled (opUser & groupName & userList)
     */
    TIM_GROUP_TIPS_TYPE_CANCEL_ADMIN        = 0x05,
    /**
     *  Group profile is modified (opUser & groupName & introduction & notification & faceUrl & owner)
     */
    TIM_GROUP_TIPS_TYPE_INFO_CHANGE         = 0x06,
    /**
     *  Group member profile is modified (opUser & groupName & memberInfoList)
     */
    TIM_GROUP_TIPS_TYPE_MEMBER_INFO_CHANGE         = 0x07,
};
/**
 *  Group Tips
 */
@interface TIMGroupTipsElem : TIMElem
/**
  *  Group ID
  */
@property(nonatomic,strong) NSString * group;
/**
  *  Group tips type
  */
@property(nonatomic,assign) TIM_GROUP_TIPS_TYPE type;
/**
  *  The user name of the operator
  */
@property(nonatomic,strong) NSString * opUser;
/**
  *  List of users who are operated on, NSString* array
  */
@property(nonatomic,strong) NSArray * userList;
/**
  *  The modified group name, otherwise it is nil
  */
@property(nonatomic,strong) NSString * groupName;
/**
  *  Group information modifications: valid at TIM_GROUP_TIPS_TYPE_INFO_CHANGE, TIMGroupTipsElemGroupInfo structure list
  */
@property(nonatomic,strong) NSArray * groupChangeList;
/**
  *  Member changes: valid at TIM_GROUP_TIPS_TYPE_MEMBER_INFO_CHANGE, TIMGroupTipsElemMemberInfo structure list
  */
@property(nonatomic,strong) NSArray * memberChangeList;
/**
  *  The user profile of the operator
  */
@property(nonatomic,strong) TIMUserProfile * opUserInfo;
/**
  *  The group member profile of the operator
  */
@property(nonatomic,strong) TIMGroupMemberInfo * opGroupMemberInfo;
/**
  *  Modify member’s user profile
  */
@property(nonatomic,strong) NSDictionary * changedUserInfo;
/**
  *  Modify member’s profile in the group
  */
@property(nonatomic,strong) NSDictionary * changedGroupMemberInfo;
/**
  *  Current number of group members: valid at TIM_GROUP_TIPS_TYPE_INVITE, TIM_GROUP_TIPS_TYPE_QUIT_GRP,
  *             TIM_GROUP_TIPS_TYPE_KICKED
  */
@property(nonatomic,assign) uint32_t memberNum;
/**
  *  Operator’s platform
  *  Valid values: iOS, Android, Windows, Mac, Web, RESTful API, Unknown
  */
@property(nonatomic,strong) NSString * platform;
@end
```

The following example registers a new message callback and prints event notifications for users joining and leaving the group. The usage of other event notifications is the same. **Example:**

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

### User joins the group

**Trigger:** when a user joins a group through application or invitation, the system sends a message in the group. The developer can choose a display style and update the group list. The type of the message received is `TIM_GROUP_TIPS_TYPE_INVITE`.

**`TIMGroupTipsElem` parameter description:**

Parameter | Description
---|---
type | TIM_GROUP_TIPS_TYPE_INVITE
opUser | Apply to join: the applicant / Invited to join: the inviter
groupName | Group name
userList | The list of users who are added to the group

### User quits the group

**Trigger:** when a user quits a group, the system sends a notification in the group. You can choose to update the group member list. The type of the message received is `TIM_GROUP_TIPS_TYPE_QUIT_GRP`.

**`TIMGroupTipsElem` parameter description:**

Parameter | Description
---|---
type | TIM_GROUP_TIPS_TYPE_QUIT_GRP
opUser | The identifier of the user who quits the group
groupName | Group name

### User is kicked out of the group

**Trigger:** when a user is kicked out of the group, the system sends a notification in the group. You can choose to update the group member list. The type of the message received is `TIM_GROUP_TIPS_TYPE_KICKED`.

**`TIMGroupTipsElem` parameter description:**

Parameter | Description
---|---
type | TIM_GROUP_TIPS_TYPE_KICKED
opUser | The identifier of the user who is kicked out of the group
groupName | Group name

### Group admin is set/canceled

**Trigger:** when a user is set or canceled as an admin, the system sends a notification in the group. If the UI shows whether a user is an admin, you can update the admin flag. The message types are `TIM_GROUP_TIPS_TYPE_SET_ADMIN` and `TIM_GROUP_TIPS_TYPE_CANCEL_ADMIN`.

**`TIMGroupTipsElem` parameter description:**

Parameter | Description
---|---
type | Set: TIM_GROUP_TIPS_TYPE_SET_ADMIN
Cancelled | TIM_GROUP_TIPS_TYPE_CANCEL_ADMIN
opUser | The identifier of the operator
groupName | Group name
userList | The list of users who are set or canceled as admins

### Group profile modifications

**Trigger:** when group profile information, such as the group name and group introduction, is modified, the system sends a message. You can update the related display fields, or selectively display the message to users.

**`TIMGroupTipsElem` parameter description:**

Parameter | Description
---|---
type | TIM_GROUP_TIPS_TYPE_INFO_CHANGE
opUser | The identifier of the operator
groupName | Group name
groupChangeInfo | The modified group profile information. It is a TIMGroupTipsElemGroupInfo structure list.

**`TIMGroupTipsElemGroupInfo` prototype:**

```
/**
  *  Group tips, the modified group information
  */
@interface TIMGroupTipsElemGroupInfo : NSObject
/**
  *  Type of modification
  */
@property(nonatomic, assign) TIM_GROUP_INFO_CHANGE_TYPE type;

/**
  *  Represents different meanings based on the modification type
  */
@property(nonatomic,strong) NSString * value;
@end
```

**Parameter description:**

Parameter | Description
---|---
type | The type of modification
value | The modified value, which represents different meanings based on the modification type

### Group member profile modifications

**Trigger:** when a group member’s profile related to the group is modified, such as when the member has been muted or the member’s role in the group has changed, the system sends a message. You can update related display fields, or selectively display the message to users.

>
>- The profile mentioned here includes only information related to the group, such as muting duration and member role change. Information related to the user such as the user’s nickname is not included. For groups that have too many members, we recommend that you display the information in the message body instead of updating it in real time. For more information, please see [Message sender and related profile](/doc/product/269/9150#.E6.B6.88.E6.81.AF.E5.8F.91.E9.80.81.E8.80.85.E4.BB.A5.E5.8F.8A.E7.9B.B8.E5.85.B3.E8.B5.84.E6.96.99).
>- If the user profile is stored locally, you can determine whether a change has occurred according to the information in the message body and update the profile after receiving a message from this user.

**`TIMGroupTipsElem` parameter description:**

Parameter | Description
---|---
type | TIM_GROUP_TIPS_TYPE_MEMBER_INFO_CHANGE
opUser | The identifier of the operator
groupName | Group name
memberInfoList | The modified group member profile information. It is a `TIMGroupTipsElemMemberInfo` structure list.

**`TIMGroupTipsElemMemberInfo` prototype:**

```
/**
 *  Group tips, modified member information
 */
@interface TIMGroupTipsElemMemberInfo : NSObject
/**
 *  The user whose profile is modified
 */
@property(nonatomic,retain) NSString * identifier;
/**
 *  Muting duration in seconds
 */
@property(nonatomic,assign) uint32_t shutupTime;
@end
```

**Parameter description:**

Parameter | Description
---|---
identifier | The identifier of the user whose profile is modified
shutupTime | Muting duration

### Group event message listeners

The group event messages of chat rooms and live-streaming groups are obtained by registering listeners in TIMManager -> setUserConfig -> TIMUserConfig -> groupEventListener. The `Elem` of the message contains the number of group members.

```
/**
 *  Group event notification callback
 */
@protocol TIMGroupEventListener <NSObject>
@optional
/**
 *  Group tips callback
 *
 *  @param elem  Group tips message
 */
- (void)onGroupTipsEvent:(TIMGroupTipsElem*)elem {
    // Group ID
    NSString *groupID = elem.group;
    // The operator
    NSString *opUser = elem.opUser;
    // The user operated on
    NSArray *userList = elem.userList;
    switch (elem.type) {
        case TIM_GROUP_TIPS_TYPE_INVITE:
            // userList joined the group. For a private group, the message can be displayed as "opUser invites userList to join the group".
            // For other types of groups, the message can be displayed as "userList joined the group".
            break;
        case TIM_GROUP_TIPS_TYPE_QUIT_GRP:
            // opUser quits the group
            break;
        case TIM_GROUP_TIPS_TYPE_KICKED:
            // opUser kicks userList out of the group
            break;
        case TIM_GROUP_TIPS_TYPE_SET_ADMIN:
            // opUser sets userList as admin
            break;
        case TIM_GROUP_TIPS_TYPE_CANCEL_ADMIN:
            // opUser cancels userList as admin
            break;
        case TIM_GROUP_TIPS_TYPE_INFO_CHANGE:
            // groupID group profile information is changed
            break;
        case TIM_GROUP_TIPS_TYPE_MEMBER_INFO_CHANGE:
            // groupID member group profile information is changed
            break;
        default:
            break;
    }
}
@end
```

## Group System Messages

When a user applies to join a group, the group admin receives a system message on the application. The admin can accept or reject the application, and the corresponding group system message will be displayed to the user.

**Group system message types:**

```
/**
 *  Group system message type
 */
typedef NS_ENUM(NSInteger, TIM_GROUP_SYSTEM_TYPE){
    /**
     *  Request to join group (received only by the admin)
     */
    TIM_GROUP_SYSTEM_ADD_GROUP_REQUEST_TYPE              = 0x01,
    /**
     *  Application to join group is approved (received only by the applicant)
     */
    TIM_GROUP_SYSTEM_ADD_GROUP_ACCEPT_TYPE               = 0x02,
    /**
     *  Application to join group is rejected (received only by the applicant)
     */
    TIM_GROUP_SYSTEM_ADD_GROUP_REFUSE_TYPE               = 0x03,
    /**
     *  Kicked out of the group by the admin (received by the user who is kicked out)
     */
    TIM_GROUP_SYSTEM_KICK_OFF_FROM_GROUP_TYPE            = 0x04,
    /**
     *  Group disbanded (received by all members)
     */
    TIM_GROUP_SYSTEM_DELETE_GROUP_TYPE                   = 0x05,
    /**
     *  Group created (received only by the creator)
     */
    TIM_GROUP_SYSTEM_CREATE_GROUP_TYPE                   = 0x06,
    /**
     *  Invited to join group (received by the invitee)
     */
    TIM_GROUP_SYSTEM_INVITED_TO_GROUP_TYPE               = 0x07,
    /**
     *  Quit group (received by the user who quits group)
     */
    TIM_GROUP_SYSTEM_QUIT_GROUP_TYPE                     = 0x08,
    /**
     *  Group admin set (received by the new group admin)
     */
    TIM_GROUP_SYSTEM_GRANT_ADMIN_TYPE                    = 0x09,
    /**
     *  Admin status canceled (received only by the canceled admin)
     */
    TIM_GROUP_SYSTEM_CANCEL_ADMIN_TYPE                   = 0x0a,
    /**
     *  Group revoked (received by all members)
     */
    TIM_GROUP_SYSTEM_REVOKE_GROUP_TYPE                   = 0x0b,
    /**
     *  Group invitation request (received by the invitee)
     */
    TIM_GROUP_SYSTEM_INVITE_TO_GROUP_REQUEST_TYPE        = 0x0c,
    /**
     *  Group invitation request approved (received only by the inviter)
     */
    TIM_GROUP_SYSTEM_INVITE_TO_GROUP_ACCEPT_TYPE         = 0x0d,
    /**
     *  Group invitation request rejected (received only by the inviter)
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
  *  Message identifier, irrelevant to the client
  */
@property(nonatomic,assign) uint64_t msgKey;
/**
  *  Message identifier, irrelevant to the client
  */
@property(nonatomic,strong) NSData * authKey;
/**
  *  Custom pass-through message body (valid when type ＝ TIM_GROUP_SYSTEM_CUSTOM_INFO)
  */
@property(nonatomic,strong) NSData * userData;
/**
  *  The user profile of the operator
  */
@property(nonatomic,strong) TIMUserProfile * opUserInfo;
/**
  *  The group member profile of the operator
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
user | The operator
msg | The reason for the operation
msgKey & authKey | Message identifiers that are irrelevant to the client. They are read by the IM SDK in the event of accept and refuse

The following example processes group system messages that are received. Applications to join the group are approved by default and messages notifying that the group was disbanded are printed. Other types of messages are parsed in the same way. **Example:**

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

### User applies to join a group

**Trigger:** when a user applies to join a group, the group admin receives a message about the user applying to join the group. You can display the message to the user for the user to decide whether to accept the application. The message type is `TIM_GROUP_SYSTEM_ADD_GROUP_REQUEST_TYPE`.

**Parameter description:**

Parameter | Description
---|---
type | TIM_GROUP_SYSTEM_ADD_GROUP_REQUEST_TYPE
group | The ID of the group that the user applies to join
user | The applicant
msg | The reason for application (optional)

**Method description:**

- To accept the application, call the accept method.
- To reject the application, call the refuse method.

### “Apply to join” request is approved/rejected

**Trigger:** when an admin approves an application to join the group, the applicant receives an approval notification message, and when the admin rejects the application, the applicant receives a rejection notification message.

**Parameter description:**

Parameter | Description
---|---
type | Approve: TIM_GROUP_SYSTEM_ADD_GROUP_ACCEPT_TYPE<br>Reject: TIM_GROUP_SYSTEM_ADD_GROUP_REFUSE_TYPE
group | The ID of the group for which the request is approved/rejected
user | The identifier of the admin who processed the request
msg | Reason for approval or rejection (optional)

### “Invited to join” request

**Trigger:** when invited to join a group, the invitee receives an invitation message. If the invitee approves the invitation, the accept method is called. Otherwise, the refuse method is called. The message type is `TIM_GROUP_SYSTEM_INVITE_TO_GROUP_REQUEST_TYPE`.

**Parameter description:**

Parameter | Description
---|---
type | TIM_GROUP_SYSTEM_INVITE_TO_GROUP_REQUEST_TYPE
group | The ID of the group that the user is invited to join
user | The inviter

**Method description:**

- To accept the application, call the accept method.
- To reject the application, call the refuse method.

### “Invited to join” request is approved/rejected

**Trigger:** when the invitee approves the invitation, the inviter receives an approval notification message, and when the invitee rejects the invitation, the inviter receives a rejection notification message.

**Parameter description:**

Parameter | Description
---|---
type | Approve: TIM_GROUP_SYSTEM_INVITE_TO_GROUP_ACCEPT_TYPE<br>Reject: TIM_GROUP_SYSTEM_INVITE_TO_GROUP_REFUSE_TYPE
group | The ID of the group for which the request is approved/rejected
user | The identifier of the user who processed the request
msg | Reason for approval or rejection (optional)

### Kicked out by admin

**Trigger:** when a user is kicked out of a group by the admin, the user receives a kicked out notification message.

**Parameter description:**

Parameter | Description
---|---
type | TIM_GROUP_SYSTEM_KICK_OFF_FROM_GROUP_TYPE
group | The ID of the group from which the user is kicked out
user | The identifier of the admin who performed the action

### Group is disbanded

**Trigger:** when a group is disbanded, all members receive a message notifying them that the group is disbanded.

**Parameter description:**

Parameter | Description
---|---
type | TIM_GROUP_SYSTEM_DELETE_GROUP_TYPE
group | The ID of the group that is disbanded
user | The identifier of the admin who performed the action

### Group is created

**Trigger:** when a group is created, the creator receives a creation notification message. If a user calls the method to create a group and the success callback is returned, then the group was created successfully. This message is used for multi-client synchronization. When receiving this message, the other clients can update the group list, while the current client can choose to ignore it.

**Parameter description:**

Parameter | Description
---|---
type | TIM_GROUP_SYSTEM_CREATE_GROUP_TYPE
group | The ID of the group that is created
user | The creator, who is the user in this case

### Invited to join group

**Trigger:** when a user is invited to join a group, the user receives an invitation message. **Initial members are added to the group without invitation when the group is created.**

**Parameter description:**

Parameter | Description
---|---
type | TIM_GROUP_SYSTEM_INVITED_TO_GROUP_TYPE
group | The ID of the group that the user is invited to join
user | The operator, who is the inviter in this case

**Method description:**

- To accept the application, call the accept method.
- To reject the application, call the refuse method.

### Quit group

**Trigger:** when a user quits a group, the user receives a quit notification message, and only the user who quit will receive the message. If the user calls `QuitGroup` and the success callback is returned, then the user has quit the group successfully. This message serves the purpose of multi-client synchronization. When receiving this message, the other clients can update the group list, while the current client can choose to ignore it.

**Parameter description:**

Parameter | Description
---|---
type | TIM_GROUP_SYSTEM_QUIT_GROUP_TYPE
group | The ID of the group that the user quits
user | The operator, who is the user who quits the group in this case

### Admin is set/cancelled

**Trigger:** when a user is set or canceled as a group admin, the user receives a corresponding notification.

**Parameter description:**

Parameter | Description
---|---
type | Admin role is cancelled: TIM_GROUP_SYSTEM_GRANT_ADMIN_TYPE<br>Admin role is granted: TIM_GROUP_SYSTEM_CANCEL_ADMIN_TYPE
group | The ID of the group in which the event occurs
user | The operator

### Group is revoked

**Trigger:** when a group is revoked by the system, all members receive a message notifying that the group was revoked.

**Parameter description:**

Parameter | Description
---|---
type | TIM_GROUP_SYSTEM_REVOKE_GROUP_TYPE
group | The ID of the group that is revoked

