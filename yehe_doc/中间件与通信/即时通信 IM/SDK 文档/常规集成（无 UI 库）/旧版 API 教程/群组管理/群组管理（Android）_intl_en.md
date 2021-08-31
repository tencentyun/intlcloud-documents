## Group Overview

Instant Messaging (IM) supports multiple group types. For more information on their characteristics and limits, see [Group System](https://intl.cloud.tencent.com/document/product/1047/33529). A group is identified by a unique ID that enables different operations.

## Group Messages

Group messages and C2C (one-to-one) messages are the same except for the conversation type obtained through Conversation. For more information, see [Sending Messages](https://intl.cloud.tencent.com/document/product/1047/34320).

## Group Management

Operations related to groups are performed after login through `TIMGroupManager`.

**Prototype for getting a singleton:**

```
/** Get an instance
 * @return a TIMGroupManager instance
 */
public static TIMGroupManager getInstance()

```

### Creating a group

IM has the following built-in group types: **private group (Private), public group (Public), chat room (ChatRoom), audio-video chat room (AVChatRoom), and broadcasting chat room (BChatRoom)**. For more information, see [Group Types](https://intl.cloud.tencent.com/document/product/1047/33529#.E7.BE.A4.E7.BB.84.E5.BD.A2.E6.80.81.E4.BB.8B.E7.BB.8D).

- **Audio-video chat room (AVChatRoom):** it is also called a live-streaming group, which can support an unlimited number of members but does not support features such as adding members or querying the total number of members.
- Groups can be created through `createGroup` in `TIMGroupManager`. When creating a group, you can specify certain group profile information, such as the group type, name, introduction, list of users to add, and even the group ID. The group ID is returned after the group is created and can be used to get Conversation to receive and send messages.

> You need to follow certain rules when defining group IDs. For more information, see [Custom Group IDs](https://intl.cloud.tencent.com/document/product/1047/33529#.E8.87.AA.E5.AE.9A.E4.B9.89.E7.BE.A4.E7.BB.84-id).

**Prototype:**

```
/**
 * Create a Group
 * @param param The set of information needed for creating a group, see {@see CreateGroupParam}.
 * @param cb The callback. The parameter of the OnSuccess function returns the ID of the group that is created.
 */
public void createGroup(@NonNull CreateGroupParam param, @NonNull TIMValueCallBack<String> cb)
```

**`TIMGroupManager.CreateGroupParam` provides the following APIs:**
```
/**
 * The constructor for CreateGroupParam class.
 * @param type The group type. The group types currently supported include private group (Private), public group (Public),
 *             chat room (ChatRoom), audio-video chat room (AVChatRoom), and broadcasting chat room (BChatRoom).
 * @param name The group name.
 */
public CreateGroupParam(@NonNull String type, @NonNull String name)

/**
 * Set the group ID for the group to be created.
 * @param groupId The group ID.
 */
public CreateGroupParam setGroupId(String groupId)

/**
 * Set the group announcement for the group to create.
 * @param notification The group announcement.
 */
public CreateGroupParam setNotification(String notification)

/**
 * Set the group introduction for the group to create.
 * @param introduction The group introduction.
 */
public CreateGroupParam setIntroduction(String introduction)

/**
 * Set the group profile photo URL for the group to create.
 * @param url The group profile photo URL.
 */
public CreateGroupParam setFaceUrl(String url)

/**
 * Set the option for joining the group.
 * @param option The option for joining the group.
 */
public CreateGroupParam setAddOption(TIMGroupAddOpt option)

/**
 * Set the maximum number of group members supported by the group to create.
 * @param maxMemberNum The maximum number of group members.
 */
public CreateGroupParam setMaxMemberNum(long maxMemberNum)

/**
 * Set the custom information for the group to create.
 * @param key Key of custom information, up to 16 bytes.
 * @param value Value of custom information, up to 512 bytes.
 */
public CreateGroupParam setCustomInfo(String key, byte[] value)

/**
 * Set the initial members of the group to create.
 * @param infos The list of initial member information
 */
public CreateGroupParam setMembers(List<TIMGroupMemberInfo> infos)
```

**Example:**
```
//Create a public group without customizing the group ID
TIMGroupManager.CreateGroupParam param = new TIMGroupManager.CreateGroupParam("Public", "test_group");
//Specify the group introduction.
param.setIntroduction("hello world");
//Specify the group notification.
param.setNotification("welcome to our group");

//Add a group member.
List<TIMGroupMemberInfo> infos = new ArrayList<TIMGroupMemberInfo>();
TIMGroupMemberInfo member = new TIMGroupMemberInfo("cat");
infos.add(member);
param.setMembers(infos);

//Set a group custom field (configure the key in the console first)
try {
    param.setCustomInfo("GroupKey1", "wildcat".getBytes("utf-8"));
} catch (UnsupportedEncodingException e) {
    e.printStackTrace();
}

//Create a group
TIMGroupManager.getInstance().createGroup(param, new TIMValueCallBack<String>() {
    @Override
    public void onError(int code, String desc) {
        Log.d(tag, "create group failed. code: " + code + " errmsg: " + desc);
    }

    @Override
    public void onSuccess(String s) {
        Log.d(tag, "create group succ, groupId:" + s);
    }
});
```

### Inviting users to a group

The `inviteGroupMember` of `TIMGroupManager` is used to add (invite) users to a group.

**Permission description:**

For more information, see [Differences in group member operations](https://intl.cloud.tencent.com/document/product/1047/33529#.E7.BE.A4.E6.88.90.E5.91.98.E6.93.8D.E4.BD.9C.E5.B7.AE.E5.BC.82). 

**Prototype:**

```
/**
 * Invite to group.
 * @param groupId The group ID.
 * @param memList The list of IDs of the users to add to the group.
 * @param cb The callback. The parameter of the OnSuccess function returns the accounts of users who have been added to the group.
 */
public void inviteGroupMember(@NonNull String groupId, @NonNull List<String> memList,
							  @NonNull TIMValueCallBack<List<TIMGroupMemberResult>> cb)
```

**`TIMGroupMemberResult` is defined as follows:**

```
/**
 * Get the operation result
 * @return The operation result: 0: failed. 1: successful. 2: the user was already a group member when added, or the user was not a group member when deleted.
 */
public long getResult()

/**
 * Get user accounts.
 * @return User accounts
 */
public String getUser()
```


**Example:**

```
//Create the list of members to add to the group.
ArrayList list = new ArrayList();

String user = "";

//Add users.
user = "sample_user_1";
list.add(user);
user = "sample_user_2";
list.add(user);
user = "sample_user_3";
list.add(user);

//The callback.
TIMValueCallBack<List<TIMGroupMemberResult>> cb = new TIMValueCallBack<List<TIMGroupMemberResult>>() {
    @Override
    public void onError(int code, String desc) {
    }

    @Override
    public void onSuccess(List<TIMGroupMemberResult> results) { //The group member operation result.
        for(TIMGroupMemberResult r : results) {
            Log.d(tag, "result: " + r.getResult()  //The operation result: 0: failed to add. 1: added successfully. 2: already a group member.
                    + " user: " + r.getUser());    //User accounts.
        }
    }
};

//Add the users in the list to the group.
TIMGroupManager.getInstance().inviteGroupMember(
        groupId,   //The group ID.
        list,      //The list of users to add to the group.
        cb);       //The callback.
```

### Applying to join a group

`applyJoinGroup` of `TIMGroupManager` allows users to apply to join a group. This operation is valid only for public groups, chat rooms, and audio-video chat rooms.

**Permission description:**

For more information, see [Differences in group member operations](https://intl.cloud.tencent.com/document/product/1047/33529#.E7.BE.A4.E6.88.90.E5.91.98.E6.93.8D.E4.BD.9C.E5.B7.AE.E5.BC.82).

**Prototype:**

```
/**
 * Join a group.
 * @param groupId The group ID.
 * @param reason The reason for the application (optional).
 * @param cb The callback.
 */
public void applyJoinGroup(@NonNull String groupId, String reason, @NonNull TIMCallBack cb)
```

In the following example, a user applies to join group “@TGS#1JYSZEAEQ” and the reason for the application is “some reason”. **Example:**

```
TIMGroupManager.getInstance().applyJoinGroup("@TGS#1JYSZEAEQ", "some reason", new TIMCallBack() {
    @java.lang.Override
    public void onError(int code, String desc) {
        //The API returns "code" (error code) and "desc" (error description), which can be used as the cause.
        //For a list of error codes, see the Error Code Table.
        Log.e(tag, "applyJoinGroup err code = " + code + ", desc = " + desc);
    }

    @java.lang.Override
    public void onSuccess() {
        Log.i(tag, "applyJoinGroup success");
    }
});
```

### Quitting a group

`TIMGroupManager` provides the API which is used to let group members quit a group.

**Permission description:**

- **Private group:** every member can quit the group.
- **Public group, chat room, and live-streaming group:** the group owner cannot quit the group.

For more information, see [Differences in group member operations](https://intl.cloud.tencent.com/document/product/1047/33529#.E7.BE.A4.E6.88.90.E5.91.98.E6.93.8D.E4.BD.9C.E5.B7.AE.E5.BC.82).

**Prototype:**

```
/**
 * Quit a group.
 * @param groupId The group ID.
 * @param cb The callback.
 */
public void quitGroup(@NonNull String groupId, @NonNull TIMCallBack cb)
```

**Example:**

```
//Create a callback.
TIMCallBack cb = new TIMCallBack() {
    @Override
    public void onError(int code, String desc) {
            //"code" (error code) and "desc" (error description) can be used to locate the cause of the request failure.
            //For the meaning of the error code, see the Error Code Table.
    }

    @Override
    public void onSuccess() {
        Log.e(tag, "quit group succ");
    }
};

//Quit a group.
TIMGroupManager.getInstance().quitGroup(
        groupId,  //The group ID.
        cb);       //The callback.
```

### Deleting group members

This function’s parameters are the same as those for joining a group. The API for deleting group members is provided by `TIMGroupManager`.

**Permission description:**
For more information, see [Differences in group member operations](https://intl.cloud.tencent.com/document/product/1047/33529#.E7.BE.A4.E6.88.90.E5.91.98.E6.93.8D.E4.BD.9C.E5.B7.AE.E5.BC.82).

**Prototype:**

```
/**
 * Deleting group members.
 * @param param The parameter for deleting group members.
 * @param cb The callback. The parameter of the OnSuccess function returns a list of group members that have been deleted.
 */
public void deleteGroupMember(@NonNull DeleteMemberParam param,
							  @NonNull TIMValueCallBack<List<TIMGroupMemberResult>> cb)
```

**`DeleteMemberParam` is defined as follows:**
```
/**
 * Constructor parameters.
 * @param groupId The group ID.
 * @param members The list of user IDs.
 */
public DeleteMemberParam(@NonNull String groupId, @NonNull List<String> members)

/**
 * Set the reason for deleting the group members (optional).
 * @param reason The reason for deleting.
 */
public DeleteMemberParam setReason(@NonNull String reason)
```

**Example:**

```
//Create the list of group members to delete.
ArrayList list = new ArrayList();

String user = "";
//Add users.
user = "sample_user_1";
list.add(user);
user = "sample_user_2";
list.add(user);
user = "sample_user_3";
list.add(user);

TIMGroupManager.DeleteMemberParam param = new TIMGroupManager.DeleteMemberParam(groupId, list);
param.setReason("some reason");

TIMGroupManager.getInstance().deleteGroupMember(param, new TIMValueCallBack<List<TIMGroupMemberResult>>() {
	@Override
	public void onError(int code, String desc) {
		Log.e(tag, "deleteGroupMember onErr. code: " + code + " errmsg: " + desc);
	}

	@Override
	public void onSuccess(List<TIMGroupMemberResult> results) { //The group member operation result.
		for(TIMGroupMemberResult r : results) {
			Log.d(tag, "result: " + r.getResult()  //The operation result: 0: failed to delete. 1: deleted successfully. 2: not a group member.
					+ " user: " + r.getUser());    //User accounts.
		}
	}
});
```

### Getting a list of group members

`getGroupMembers` is used to get a list of group members. Built-in fields and custom fields are pulled by default. Go to the [IM Console](https://console.cloud.tencent.com/im) -> **Feature Configuration** -> **Group Member Custom Field** to configure the key and permission for custom fields, which take effect after 5 minutes.

**Permission description:**

- **Any type of group:** member list can be obtained.
- **Live-streaming group:** the member list only contains the group owner, admin, and some members.

For more information, see [Differences in group operations](https://intl.cloud.tencent.com/document/product/1047/33529#.E7.BE.A4.E7.BB.84.E6.93.8D.E4.BD.9C.E5.B7.AE.E5.BC.82). 

**Prototype:**

```
/**
 * Get the group member list.
 * @param groupId The group ID.
 * @param cb The callback. The parameter of the OnSuccess function returns the list of group members.
 */
public void getGroupMembers(@NonNull String groupId, @NonNull TIMValueCallBack<List<TIMGroupMemberInfo>> cb)
```

**Example:**

```
//Create a callback.
TIMValueCallBack<List<TIMGroupMemberInfo>> cb = new TIMValueCallBack<List<TIMGroupMemberInfo>> () {
    @Override
    public void onError(int code, String desc) {
    }

    @Override
    public void onSuccess(List<TIMGroupMemberInfo> infoList) {//The parameter returns the group member information.

        for(TIMGroupMemberInfo info : infoList) {
            Log.d(tag, "user: " + info.getUser() +
            "join time: " + info.getJoinTime() +
            "role: " + info.getRole());
        }
    }
};

//Get the group member information.
TIMGroupManager.getInstance().getGroupMembers(
        groupId, //The group ID.
        cb);     //The callback.
```

### Getting a list of groups a user has joined

The API for getting the list of groups the current user has joined is provided by `TIMGroupManager`. The returned information contains only part of the basic information. To get detailed group information, see [Getting group profiles](https://intl.cloud.tencent.com/document/product/1047/34328).

**Permission description:**

- **Private group, public group, and chat room:** this API can be used to get the information of public groups, chat rooms, and activated private groups a user has joined.
- **Audio-video chat room and broadcasting chat room:** these two types of groups will not be obtained through this API due to the differences in internal implementation.

**Prototype:**

```
/**
 * Get the list of groups the user has joined.
 * @param cb The callback. The parameter of the OnSuccess function returns the groups the user has joined.
 */
public void getGroupList(@NonNull TIMValueCallBack<List<TIMGroupBaseInfo>> cb)
```

**`TIMGroupBaseInfo` provides the following methods:**
```
/**
 * Get the group ID.
 * @return the group ID.
 */
public String getGroupId()

/**
 * Get the group name.
 * @return the group name.
 */
public String getGroupName()

/**
 * Get the group type.
 * @return The group type.
 */
public String getGroupType()

/**
 * Get the group profile photo URL.
 * @return The group profile photo URL.
 */
public String getFaceUrl()

/**
 * Get whether or not the current group has set Mute All.
 * @return true - Mute All has been set.
 * @since 3.1.1
 */
public boolean isSilenceAll()
```

**Example:**

```
//Create a callback.
TIMValueCallBack<List<TIMGroupBaseInfo>> cb = new TIMValueCallBack<List<TIMGroupBaseInfo>>() {
    @Override
    public void onError(int code, String desc) {
        //"code" (error code) and "desc" (error description) can be used to locate the cause of the request failure.
        //For the meaning of the error code, see the Error Code Table.
        Log.e(tag, "get group list failed: " + code + " desc");
    }

    @Override
    public void onSuccess(List<TIMGroupBaseInfo> timGroupInfos) {//The parameter returns the basic information of each group.
        Log.d(tag, "get group list succ");

        for(TIMGroupBaseInfo info : timGroupInfos) {
            Log.d(tag, "group id: " + info.getGroupId() +
            " group name: " + info.getGroupName() +
            " group type: " + info.getGroupType());
        }
    }
};

//Get the list of groups the user has joined.
TIMGroupManager.getInstance().getGroupList(cb);
```

### Disbanding a group

 The API for disbanding groups is provided by `TIMGroupManager`.

**Permission description:**
For more information, see [Differences in group operations](https://intl.cloud.tencent.com/document/product/1047/33529#.E7.BE.A4.E7.BB.84.E6.93.8D.E4.BD.9C.E5.B7.AE.E5.BC.82). 

**Prototype:**

```
/**
 * Delete a group.
 * @param groupId The group ID.
 * @param cb The callback.
 */
public void deleteGroup(@NonNull String groupId, @NonNull TIMCallBack cb)
```

**Example:**

```
//Disband a group.
TIMGroupManager.getInstance().deleteGroup(groupId, new TIMCallBack() {
    @Override
    public void onError(int code, String desc) {

        //"code" (error code) and "desc" (error description) can be used to locate the cause of the request failure.
        //For a list of error codes, see the Error Code Table.
        Log.d(tag, "login failed. code: " + code + " errmsg: " + desc);
    }

    @Override
    public void onSuccess() {
        //Group disbanded successfully.
    }
});
```

### Transferring a group

The API for transferring groups is provided by `TIMGroupManager`.

**Permission description:**

Only the **group owner** can transfer a group.

**Prototype:**

```
/**
 * Change the group owner.
 * @param groupId The group ID.
 * @param identifier The identifier of the new group owner.
 * @param cb The callback.
 */
public void modifyGroupOwner(@NonNull String groupId, @NonNull String identifier, @NonNull TIMCallBack cb)
```

### Other APIs

**The API for getting specified types of members (to pull group admins, group owners, and group members respectively) is defined as follows:**

```
/**
 * Get a list of group members based on filter conditions (the list can be pulled by field and in pages).
 * @param groupId The group ID.
 * @param flags The flag of profiles to pull, such as {@see TIMGroupManager#TIM_GET_GROUP_MEM_INFO_FLAG_NAME_CARD} or any combination of them.
 * @param filter The Role filter, see {@see TIMGroupMemberRoleFilter}.
 * @param custom The list of custom keys to get.
 * @param nextSeq The flag for pulling in pages. Enter 0 for the first request. If the success callback returns a value that is not 0, then the list will be pulled in pages. Pass this parameter to pull again until the value becomes 0.
 * @param cb The callback.
 */
public void getGroupMembersByFilter(@NonNull String groupId, long flags, @NonNull TIMGroupMemberRoleFilter filter,
									List<String> custom, long nextSeq, TIMValueCallBack<TIMGroupMemberSucc> cb)
```

## Getting Group Profiles

### Getting group profiles

The `getGroupInfo` method provided by `TIMGroupManager` is used to get group profiles stored on the server and the `queryGroupInfo` method is used to pull group profiles cached locally. Group members can pull group information. Non-members cannot pull private groups’ information and can only pull public fields of other types of groups, `groupId\groupName\groupOwner\groupType\createTime\memberNum\maxMemberNum\onlineMemberNum\groupIntroduction\groupFaceUrl\addOption\custom`.

**Note:**

Basic profile and custom fields are pulled by default. Go to the [IM Console](https://console.cloud.tencent.com/im) -> **Feature Configuration** -> **Group-level Custom Fields** to configure the key and permission for custom fields, which take effect after 5 minutes.

**Prototype:**

```
/**
 * Get the group information stored on the server.
 * @param groupIdList The list of groups of which the detailed information is to be pulled. Up to 50 groups can be pulled at a time.
 * @param cb The callback. The parameter of the OnSuccess function returns the list of group information {@see TIMGroupDetailInfo}.
 */
public void getGroupInfo(@NonNull List<String> groupIdList,
							   @NonNull TIMValueCallBack<List<TIMGroupDetailInfo>> cb)
/**
 * Get the group information stored locally.
 * @param groupId The IDs of the groups of which the detailed information is to be pulled.
 * @return The group information, or null if the group information is not stored locally.
 */
 public TIMGroupDetailInfo queryGroupInfo(@NonNull String groupId)
```

**`TIMGroupDetailInfo` is defined as follows:**
```
/**
 * Get the group ID.
 * @return the group ID.
 */
public String getGroupId()

/**
 * Get the group name.
 * @return the group name.
 */
public String getGroupName()

/**
 * Get the group creator account.
 * @return The group creator account.
 */
public String getGroupOwner()

/**
 * Get the group creation time.
 * @return The group creation time.
 */
public long getCreateTime()

/**
 * Get the last modified time of group information.
 * @return The last modified time of group information.
 */
public long getLastInfoTime()

/**
 * Get the time of the last group message.
 * @return The time of the last group message.
 */
public long getLastMsgTime()

/**
 * Get the number of group members.
 * @return The number of group members.
 */
public long getMemberNum()

/**
 * Get the maximum number of group members supported.
 * @return The maximum number of group members.
 */
public long getMaxMemberNum()

/**
 * Get the group introduction.
 * @return The group introduction.
 */
public String getGroupIntroduction()

/**
 * Get the group announcement.
 * @return The group announcement.
 */
public String getGroupNotification()

/**
 * Get the group profile photo URL.
 * @return The group profile photo URL.
 */
public String getFaceUrl()

/**
 * Get the group type.
 * @return The group type.
 */
public String getGroupType()

/**
 * Get the option for joining the group.
 * @return The option for joining the group.
 */
public TIMGroupAddOpt getGroupAddOpt()

/**
 * Get the last message in the group.
 * @return The last message in the group.
 */
public TIMMessage getLastMsg()

/**
 * Get the group custom field map.
 * @return The group custom field map.
 */
public Map<String, byte[]> getCustom()

/**
 * Get whether or not this group is set with Mute All.
 * @return true - The group is set with Mute All.
 * @since 3.1.1
 */
public boolean isSilenceAll()
```

**Example:**

```
//Create a list of group IDs for which you want to get information.
ArrayList<String> groupList = new ArrayList<String>();

//Create a callback.
TIMValueCallBack<List<TIMGroupDetailInfo>> cb = new TIMValueCallBack<List<TIMGroupDetailInfo>>() {
    @Override
    public void onError(int code, String desc) {
            //"code" (error code) and "desc" (error description) can be used to locate the cause of the request failure.
            //For a list of error codes, see the Error Code Table.
    }

    @Override
    public void onSuccess(List<TIMGroupDetailInfo> infoList) { //The parameter returns the list of group information.
        for(TIMGroupDetailInfo info : infoList) {
            Log.d(tag, "groupId: " + info.getGroupId()           //The group ID.
            + " group name: " + info.getGroupName()              //The group name.
            + " group owner: " + info.getGroupOwner()            //The group creator account.
            + " group create time: " + info.getCreateTime()      //The group creation time.
            + " group last info time: " + info.getLastInfoTime() //The last modified time of group information.
            + " group last msg time: " + info.getLastMsgTime()  //The time of the last group message.
            + " group member num: " + info.getMemberNum());      //The number of group members.
        }
    }
};

//Add group IDs.
String groupId = "TGID1EDABEAEO";
groupList.add(groupId);

//Get the group information stored on the server.
TIMGroupManager.getInstance().getGroupInfo(
        groupList, //The list of group IDs for which you want to get information.
        cb);       //The callback.

//Get the group information cached locally.
TIMGroupDetailInfo timGroupDetailInfo = TIMGroupManager.getInstance().queryGroupInfo(groupId);
```

### Getting your own profile in a group

You can obtain your own profile in a group when the list of groups you have joined is pulled. See [Getting group list](#.E8.8E.B7.E5.8F.96.E5.8A.A0.E5.85.A5.E7.9A.84.E7.BE.A4.E7.BB.84.E5.88.97.E8.A1.A8). If you want to get your profile in a single group, use `getSelfInfo` of `TIMGroupManager` as shown below. If the app needs to get a group list, we recommend that you get the profiles in groups when getting the group list instead of calling the following API.

**Permission description:**

**Live-streaming groups** do not support getting your own profile in the group.

**Prototype:**

```
/**
 * Get your own information in a group.
 * @param groupId The group ID.
 * @param cb The callback. The parameter of the OnSuccess function returns your own information
 */
public void getSelfInfo(@NonNull String groupId, @NonNull TIMValueCallBack<TIMGroupSelfInfo> cb)
```

### Getting the profiles of group members

The API for getting group member profiles is provided by `TIMGroupManager`. Basic profiles are pulled by default.

**Permission description:**

For a **live-streaming group**, only the profiles of some members can be pulled, including the group owner, admin, and some members.

**Prototype:**
```
/**
 * Get the profiles of specified members in a group.
 @param groupId The ID of the specified group.
 * @param identifiers Up to 100 group identifiers can be specified at a time.
 * @param cb The callback. The parameter of the OnSuccess function returns a group member list.
 */
public void getGroupMembersInfo(@NonNull String groupId, @NonNull List<String> identifiers,
								@NonNull TIMValueCallBack<List<TIMGroupMemberInfo>> cb)
```


## Modifying Group Profile

The API for modifying group profiles is provided by `TIMGroupManager`, which allows information such as the group name, introduction, and announcement to be modified.

**Prototype:**

```
/**
 * Modify group basic information.
 * @param param The parameter class.
 * @param cb The callback.
 */
public void modifyGroupInfo(@NonNull ModifyGroupInfoParam param, @NonNull TIMCallBack cb)
```

**`TIMGroupManager.ModifyGroupInfoParam` is defined as follows:**

```
/**
 * Construct a parameter instance.
 * @param groupId The group ID.
 */
public ModifyGroupInfoParam(@NonNull String groupId)

/**
 * Set the modified group name.
 * @param groupName The group name.
 */
public ModifyGroupInfoParam setGroupName(@NonNull String groupName)

/**
 * Set the modified group announcement.
 * @param notification The group announcement.
 */
public ModifyGroupInfoParam setNotification(@NonNull String notification)

/**
 * Set the modified group introduction.
 * @param introduction The group introduction.
 */
public ModifyGroupInfoParam setIntroduction(@NonNull String introduction)

/**
 * Set the modified group profile photo URL.
 * @param faceUrl The group profile photo URL.
 */
public ModifyGroupInfoParam setFaceUrl(@NonNull String faceUrl)

/**
 * Set the option for joining the group.
 * @param addOpt The option for joining the group.
 */
public ModifyGroupInfoParam setAddOption(@NonNull TIMGroupAddOpt addOpt)

/**
 * Set the maximum number of group members.
 * @param maxMemberNum The maximum number of group members.
 */
public ModifyGroupInfoParam setMaxMemberNum(long maxMemberNum)

/**
 * Set whether or not group members are visible to users outside the group.
 * @param visable Whether or not group members are visible to users outside the group.
 */
public ModifyGroupInfoParam setVisable(boolean visable)

/**
 * Set a group custom field.
 * @param customInfos The group custom field dictionary.
 */
public ModifyGroupInfoParam setCustomInfo(@NonNull Map<String, byte[]> customInfos)

/**
 * Set Mute All.
 * @param silenceAll true - Mute All, false - Unmute All.
 * @since 3.1.1
 */
public ModifyGroupInfoParam setSilenceAll(boolean silenceAll)
```

### Modifying the group name

**Permission description:**

- **Public group, chat room, and live-streaming group:** only the group owner or admin can modify the group name.
- **Private group:** any member can modify the group name.

**Example:**

```
TIMGroupManager.ModifyGroupInfoParam param = new TIMGroupManager.ModifyGroupInfoParam(getGroupId());
param.setGroupName("Great Team")
TIMGroupManager.getInstance().modifyGroupInfo(param, new TIMCallBack() {
	@Override
	public void onError(int code, String desc) {
		Log.e(tag, "modify group info failed, code:" + code +"|desc:" + desc);
	}

	@Override
	public void onSuccess() {
		Log.e(tag, "modify group info succ");
	}
});
```

### Modifying the group introduction

**Permission description:**

- **Public group, chat room, and live-streaming group:** only the group owner or admin can modify the group introduction.
- **Private group:** any member can modify the group introduction.

**Example:**

```
TIMGroupManager.ModifyGroupInfoParam param = new TIMGroupManager.ModifyGroupInfoParam(getGroupId());
param.setIntroduction("this is a introduction");
TIMGroupManager.getInstance().modifyGroupInfo(param, new TIMCallBack() {
	@Override
	public void onError(int code, String desc) {
		Log.e(tag, "modify group info failed, code:" + code +"|desc:" + desc);
	}

	@Override
	public void onSuccess() {
		Log.e(tag, "modify group info succ");
	}
});
```

### Modifying the group announcement

**Permission description:**

- **Public group, chat room, and live-streaming group:** only the group owner or admin can modify the group announcement.
- **Private group:** any member can modify the group announcement.

**Example:**

```
TIMGroupManager.ModifyGroupInfoParam param = new TIMGroupManager.ModifyGroupInfoParam(getGroupId());
param.setNotification("this is a notification");
TIMGroupManager.getInstance().modifyGroupInfo(param, new TIMCallBack() {
	@Override
	public void onError(int code, String desc) {
		Log.e(tag, "modify group info failed, code:" + code +"|desc:" + desc);
	}

	@Override
	public void onSuccess() {
		Log.e(tag, "modify group info succ");
	}
});
```

### Modifying the group profile photo

**Permission description:**

- **Public group, chat room, and live-streaming group:** only the group owner or admin can modify the group profile photo.
- **Private group:** any member can modify the group profile photo.


**Example:**

```
TIMGroupManager.ModifyGroupInfoParam param = new TIMGroupManager.ModifyGroupInfoParam(getGroupId());
param.setFaceUrl("http://faceurl");
TIMGroupManager.getInstance().modifyGroupInfo(param, new TIMCallBack() {
	@Override
	public void onError(int code, String desc) {
		Log.e(tag, "modify group info failed, code:" + code +"|desc:" + desc);
	}

	@Override
	public void onSuccess() {
		Log.e(tag, "modify group info succ");
	}
});
```

### Modifying the option for joining the group

**Permission description:**

- **Public group, chat room, and live-streaming group:** only the group owner or admin can modify the option for joining the group.
- **Private group:** users can join the group only through invitation, not by application.

**Example:**

```
TIMGroupManager.ModifyGroupInfoParam param = new TIMGroupManager.ModifyGroupInfoParam(getGroupId());
param.setAddOption(TIMGroupAddOpt.TIM_GROUP_ADD_ANY);
TIMGroupManager.getInstance().modifyGroupInfo(param, new TIMCallBack() {
	@Override
	public void onError(int code, String desc) {
		Log.e(tag, "modify group info failed, code:" + code +"|desc:" + desc);
	}

	@Override
	public void onSuccess() {
		Log.e(tag, "modify group info succ");
	}
});
```

### Modifying group-level custom fields

**Permission description:**

- Relevant keys and permissions need to be configured at the backend.

**Example:**

```
TIMGroupManager.ModifyGroupInfoParam param = new TIMGroupManager.ModifyGroupInfoParam(getGroupId());
Map<String, byte[]> customInfo = new HashMap<String, byte[]>();
try {
	customInfo.put("Test", "Test_value".getBytes("utf-8"));
	param.setCustomInfo(customInfo);
} catch (UnsupportedEncodingException e) {
	e.printStackTrace();
}

TIMGroupManager.getInstance().modifyGroupInfo(param, new TIMCallBack() {
	@Override
	public void onError(int code, String desc) {
		Log.e(tag, "modify group info failed, code:" + code +"|desc:" + desc);
	}

	@Override
	public void onSuccess() {
		Log.e(tag, "modify group info succ");
	}
});
```

### Muting all members

**Permission description:**

- **Only the group owner and admin** can mute all members.
- **All group types** support muting all members.

**Example:**

```
TIMGroupManager.ModifyGroupInfoParam param = new TIMGroupManager.ModifyGroupInfoParam(groupId);
param.setSilenceAll(true);
TIMGroupManager.getInstance().modifyGroupInfo(param, new TIMCallBack() {
	@Override
	public void onError(int code, String desc) {
		Log.e(tag, "modify group info failed, code:" + code +"|desc:" + desc);
	}

	@Override
	public void onSuccess() {
		Log.e(tag, "modify group info succ");
	}
});
```

## Modifying Group Member Profiles

The API for modifying group member profiles is provided by `TIMGroupManager`, which allows group members’ roles and name cards to be modified and group members to be muted.

**Prototype:**

```
/**
 * Modify group member profiles.
 * @param param The parameter for modifying group member profiles.
 * @param cb The callback.
 */
public void modifyMemberInfo(@NonNull ModifyMemberInfoParam param, @NonNull TIMCallBack cb)
```

**`TIMGroupManager.ModifyMemberInfoParam` is defined as follows:**

```
/**
 * Construct the parameters for modifying group member profiles.
 * @param groupId The group ID.
 * @param identifier The user ID of the group member whose profile is to be modified.
 */
public ModifyMemberInfoParam(@NonNull String groupId, @NonNull String identifier)

/**
 * Modify a group member’s name card
 * @param nameCard The group name card.
 */
public ModifyMemberInfoParam setNameCard(@NonNull String nameCard)

/**
 * Modify the option for receiving group messages.
 * @param receiveMessageOpt The option for receiving group messages. See {@see TIMGroupReceiveMessageOpt}.
 */
public ModifyMemberInfoParam setReceiveMessageOpt(@NonNull TIMGroupReceiveMessageOpt receiveMessageOpt)

/**
 * Modify a group member’s role (only the group owner and admins can modify roles).
 * @param roleType The type of the role. It cannot be changed to group owner. See {@see TIMGroupMemberRoleType}.
 */
public ModifyMemberInfoParam setRoleType(TIMGroupMemberRoleType roleType)

/**
 * Set the duration of muting (only the group owner and admin can set this).
 * @param silence The duration of muting.
 */
public ModifyMemberInfoParam setSilence(long silence)

/**
 * Set a group custom field.
 * @param customInfo The group custom field dictionary.
 */
public ModifyMemberInfoParam setCustomInfo(Map<String, byte[]> customInfo)
```

### Modifying a member’s role in the group

**Permission description:**

- **Only the group owner or admin** can modify group members’ roles.
- **Live-streaming groups** do not support modifying group members’ roles.

**Example:**

```
TIMGroupManager.ModifyMemberInfoParam param = new TIMGroupManager.ModifyMemberInfoParam(groupId, identifier);
param.setRoleType(TIMGroupMemberRoleType.Admin);

TIMGroupManager.getInstance().modifyMemberInfo(param, new TIMCallBack() {
	@Override
	public void onError(int code, String desc) {
		Log.e(tag, "modifyMemberInfo failed, code:" + code + "|msg: " + desc);
	}

	@Override
	public void onSuccess() {
		Log.d(tag, "modifyMemberInfo succ");
	}
});
```

### Muting group members

`modifyMemberInfoParam.setSilence()` is used to mute group members and set the duration of muting.

**Permission description:**

- **Only the group owner or admin** can mute group members.

**Example:**

```
//Mute for 100 seconds.
TIMGroupManager.ModifyMemberInfoParam param = new TIMGroupManager.ModifyMemberInfoParam(groupId, identifier);
param.setSilence(100);

TIMGroupManager.getInstance().modifyMemberInfo(param, new TIMCallBack() {
	@Override
	public void onError(int code, String desc) {
		Log.e(tag, "modifyMemberInfo failed, code:" + code + "|msg: " + desc);
	}

	@Override
	public void onSuccess() {
		Log.d(tag, "modifyMemberInfo succ");
	}
});
```

### Modifying a member’s name card in the group


**Example:**

```
TIMGroupManager.ModifyMemberInfoParam param = new TIMGroupManager.ModifyMemberInfoParam(groupId, identifier);
param.setNameCard("cat");

TIMGroupManager.getInstance().modifyMemberInfo(param, new TIMCallBack() {
	@Override
	public void onError(int code, String desc) {
		Log.e(tag, "modifyMemberInfo failed, code:" + code + "|msg: " + desc);
	}

	@Override
	public void onSuccess() {
		Log.d(tag, "modifyMemberInfo succ");
	}
});
```

### Modifying group member custom fields

**Example:**

```
TIMGroupManager.ModifyMemberInfoParam param = new TIMGroupManager.ModifyMemberInfoParam(groupId, identifier);
Map<String, byte[]> customInfo = new HashMap<>();
try {
	customInfo.put("Test", "Custom".getBytes("utf-8"));
	param.setCustomInfo(customInfo);
} catch (UnsupportedEncodingException e) {
	e.printStackTrace();
}

TIMGroupManager.getInstance().modifyMemberInfo(param, new TIMCallBack() {
	@Override
	public void onError(int code, String desc) {
		Log.e(tag, "modifyMemberInfo failed, code:" + code + "|msg: " + desc);
	}

	@Override
	public void onSuccess() {
		Log.d(tag, "modifyMemberInfo succ");
	}
});
```

### Modifying the option for receiving group messages

**Permission description:**

- **Public group and private group:** the default option is to receive and push group messages offline.
- **Chat room and audio-video chat room:** the default option is to receive but not push group messages offline.

**`TIMGroupReceiveMessageOpt` is defined as follows:**

```
//Do not receive group messages and the server does not forward the messages.
TIMGroupReceiveMessageOpt.NotReceive

//Receive group messages but do not push offline messages when offline.
TIMGroupReceiveMessageOpt.ReceiveNotNotify

//Receive group messages and push offline messages when offline.
TIMGroupReceiveMessageOpt.ReceiveAndNotify
```

**Example:**

```
TIMGroupManager.ModifyMemberInfoParam param = new TIMGroupManager.ModifyMemberInfoParam(groupId, identifier);
param.setReceiveMessageOpt(TIMGroupReceiveMessageOpt.ReceiveAndNotify);

TIMGroupManager.getInstance().modifyMemberInfo(param, new TIMCallBack() {
	@Override
	public void onError(int code, String desc) {
		Log.e(tag, "modifyMemberInfo failed, code:" + code + "|msg: " + desc);
	}

	@Override
	public void onSuccess() {
		Log.d(tag, "modifyMemberInfo succ");
	}
});
```

## Group Pending Requests

Group pending requests are group-related operations that require approval, such as pending “apply to join” requests and pending “invited to join” requests. Group pending information is represented by the `TIMGroupPendencyItem` class.

**The following are member methods of `TIMGroupPendencyItem`:**
```
/**
 * Get the group ID.
 * @return the group ID.
 */
public String getGroupId()

/**
 * Get the identifier of the requester, who is the requester of an “apply to join” request and the inviter of an “invited to join” request.
 * @return The requester’s identifier.
 */
public String getFromUser()

/**
 * Get the identifier of the handler. The identifier is 0 if it is an “apply to join” request, and the invitee if it is an “invited to join” request.
 * @return The handler’s identifier.
 */
public String getToUser()

/**
 * Get the time the group pending request is added.
 * @return The time the group pending request is added.
 */
public long getAddTime()

/**
 * Get the type of the group pending request.
 * @return The type of the group pending request. See TIMGroupPendencyGetType for details.
 */
public TIMGroupPendencyGetType getPendencyType()

/**
 * Get the processing status of the group pending request.
 * @return The processing status of the group pending request. See {@see TIMGroupPendencyHandledStatus}.
 */
public TIMGroupPendencyHandledStatus getHandledStatus()

/**
 * Get the processing type of the group pending request. Only valid when the processing status is not {@see TIMGroupPendencyHandledStatus#NOT_HANDLED}.
 * @return The processing type of the group pending request. See {@see TIMGroupPendencyOperationType}.
 */
public TIMGroupPendencyOperationType getOperationType()

/**
 * Get the additional information added by the requester.
 * @return The additional information added by the requester.
 */
public String getRequestMsg()

/**
 * Get the custom information added by the requester.
 * @return The custom information added by the requester.
 */
private String getRequestUserData()

/**
 * Get the additional information added by the handler. Only valid when the processing status is not {@see TIMGroupPendencyHandledStatus#NOT_HANDLED}.
 * @return The additional information added by the handler.
 */
public String getHandledMsg()

/**
 * Get the custom information added by the handler. Only valid when the processing status is not {@see TIMGroupPendencyHandledStatus#NOT_HANDLED}.
 * @return The custom information added by the handler.
 */
private String getHandledUserData()

/**
 * Approve the request. Only valid for “apply to join” and “invited to join” messages.
 *
 * @param msg The reason for approval (optional).
 * @param cb The callback.
 */
public void accept(String msg, TIMCallBack cb)

/**
 * Reject the request. Only valid for “apply to join” and “invited to join” messages.
 *
 * @param msg The reason for approval (optional).
 * @param cb The callback.
 */
public void refuse(String msg, TIMCallBack cb)
```

### Pulling a list of group pending requests

The `getGroupPendencyList` API of `TIMGroupManager` is used to pull information related to group pending requests. A message can be pulled through this API even after it has been approved or rejected. In this case, the message pulled has a “processed” flag.

**Permission description:**

**Only the approver** has permission to pull the information.

>For example:
>- If user A applies to join group A, the group admin can obtain information related to this pending request. As user A does not have approval permission, user A does not need to obtain information related to this pending request.
>- If admin A invites user A to join group A, user A can obtain the information related to this pending request because this pending request needs to be approved by user A.

**Prototype:**

```
/**
 * Get group pending requests in pages.
 * @param param The parameter for getting a list of group pending requests. See {@see TIMGroupPendencyGetParam}.
 * @param cb The callback. The parameter of onSuccess returns the list of group pending requests and metadata. See {@see TIMGroupPendencyMeta} and {@see TIMGroupPendencyItem}.
 */
public void getGroupPendencyList(@NonNull TIMGroupPendencyGetParam param,
								 @NonNull TIMValueCallBack<TIMGroupPendencyListGetSucc> cb)
```

**`TIMGroupPendencyGetParam` is defined as follows:**

```
/**
 * Set the paging timestamp. Enter 0 for the first request and the appropriate values according to the timestamps in {@see TIMGroupPendencyMeta} returned by the server.
 * @param timestamp The paging timestamp.
 */
public void setTimestamp(long timestamp)

/**
 * Set the number of requests per page (this is a suggested value which does not indicate completion; the server can return more or less requests as needed).
 * @param numPerPage The number of requests per page.
 */
public void setNumPerPage(long numPerPage)
```

**Example:**

```
TIMGroupPendencyGetParam param = new TIMGroupPendencyGetParam();
param.setTimestamp(0);//Enter 0 for the first request.
param.setNumPerPage(10);

TIMGroupManager.getInstance().getGroupPendencyList(param, new TIMValueCallBack<TIMGroupPendencyListGetSucc>() {
    @Override
    public void onError(int code, String desc) {

    }

    @Override
    public void onSuccess(TIMGroupPendencyListGetSucc timGroupPendencyListGetSucc) {
        //If the nextStartTimestamp in meta is not 0, pass it
        //as an argument to TIMGroupPendencyGetParam for getting the next page of data.
        TIMGroupPendencyMeta meta = timGroupPendencyListGetSucc.getPendencyMeta();
        Log.d(tag, meta.getNextStartTimestamp()
                + "|" + meta.getReportedTimestamp() + "|" + meta.getUnReadCount());

        List<TIMGroupPendencyItem> pendencyItems = timGroupPendencyListGetSucc.getPendencies();
        for(TIMGroupPendencyItem item : pendencyItems){
            //Operate on group pending requests, such as view, approve, or reject a request.
        }
    }
});
```

### Reporting that group pending requests are read

`reportGroupPendency` of `TIMGroupManager` is used to report that the current pending request and all the pending requests before it have been read. After the report, you can still pull these pending requests and determine whether they are read through the read timestamp.

**Prototype:**

```
/**
 * Report that group pending requests are read.
 * @param timestamp The read timestamp in seconds. Group pending requests before this timestamp are set as read.
 * @param cb The callback.
 */
public void reportGroupPendency(long timestamp, @NonNull TIMCallBack cb)
```


### Processing group pending requests

`getGroupPendencyList` is used to get a list of group pending requests (`TIMGroupPendencyItem`) and the `accept/refuse` API in the `TIMGroupPendencyItem` class is used to process the requests in the list. Requests that have been processed cannot be processed again.

**Prototype:**

```
/**
 * Approve the request. Only valid for “apply to join” and “invited to join” messages.
 *
 * @param msg The reason for approval (optional).
 * @param cb The callback.
 */
public void accept(String msg, TIMCallBack cb)

/**
 * Reject the request. Only valid for “apply to join” and “invited to join” messages.
 *
 * @param msg The reason for approval (optional).
 * @param cb The callback.
 */
public void refuse(String msg, TIMCallBack cb)
```

## Group Event Messages

After a user is invited to a group or removed from a group, a group tips message is generated. The caller has the option to display the tips message to group members or ignore it. Group tips messages are identified by a special `Elem` and returned by the callback for new messages. Alternatively, a listener that listens to the corresponding events can be set through the `setGroupEventListener` API of `TIMUserConfig` **before login**. See [Initialization (Android)](https://intl.cloud.tencent.com/document/product/1047/34312).

> The group event messages of chat rooms (ChatRoom) and audio-video chat rooms (AVChatRoom) are not delivered by new message notifications. Therefore, you must register group event listeners to listen to different group events.




**`TIMGroupTipsElem` member methods:**

```
//Get the list of messages for group profile modifications. Only valid when the value of tipsType is TIMGroupTipsType.ModifyGroupInfo.
java.util.List<TIMGroupTipsElemGroupInfo> getGroupInfoList()

//Get the group name.
java.lang.String    getGroupName()

//Get the list of messages for group member modifications. Only valid when the value of tipsType is TIMGroupTipsType.ModifyMemberInfo.
java.util.List<TIMGroupTipsElemMemberInfo>    getMemberInfoList()

//Get the operator.
java.lang.String    getOpUser()

//Get the type of the group event tips.
TIMGroupTipsType    getTipsType()

//Get the list of accounts on which to operate.
java.util.List<java.lang.String>  getUserList()
```

**`TIMGroupTipsType` prototype:**

```
//Admin is canceled.
CancelAdmin

//Member joins group.
Join

//Member is removed from group.
Kick

//Group profile is modified.
ModifyGroupInfo

//Member information is modified.
ModifyMemberInfo

//Member quits group.
Quit

//Admin is set.
SetAdmin
```

### Tips Message for user joining the group

**Trigger:** when a user joins a group through application or invitation, the system sends a tips message in the group. The developer can choose a display style and update the group member list. The type of the message received is `TIMGroupTipsType.Join`.

**Description of the responses of `TIMGroupTipsElem` member methods:**

Method | Response Description
---|---
getType | TIMGroupTipsType.Join
getOpUser | Apply to join: the applicant</br>Invited to join: the inviter
getGroupName | The group name
getUserList | The list of users that are added to the group

### User quits the group

**Trigger:** when a user quits a group, the system sends a tips message in the group. You can choose to update the group member list. The type of the message received is `TIMGroupTipsType.Quit`.

**Description of the responses of `TIMGroupTipsElem` member methods:**

Method | Response Description
---|---
getType | TIMGroupTipsType.Quit
getOpUser | The identifier of the user who quits the group
getGroupName | The group name

### User is removed from the group

**Trigger:** when a user is removed from a group, the system sends a tips message in the group. You can choose to update the group member list. The type of the message received is `TIMGroupTipsType.Kick`.

**Description of the responses of `TIMGroupTipsElem` member methods:**

Method | Response Description
---|---
getType | TIMGroupTipsType.Kick
getOpUser | The identifier of the user who removes members
getGroupName | The group name
getUserList | The list of users who are removed

### Group admin is set/cancelled

**Trigger:** when a user is set or canceled as an admin, the system sends a tips message in the group. If the UI shows whether a user is an admin, you can update the admin flag. The message types are `TIMGroupTipsType.SetAdmin` and `TIMGroupTipsType.CancelAdmin`.

**Description of the responses of `TIMGroupTipsElem` member methods:**

Method | Response Description
---|---
getType | Set: TIMGroupTipsType.SetAdmin<br>Cancelled: TIMGroupTipsType.CancelAdmin
getOpUser | The identifier of the operator
getGroupName | The group name
getUserList | The list of users who are set or canceled as admins

### Group profile modifications

**Trigger:** when group profile information, such as the group name and group introduction, is modified, the system sends a tips message. You can update the related display fields, or selectively display the message to users.

**Description of the responses of `TIMGroupTipsElem` member methods:**

Method | Response Description
---|---
getType | TIMGroupTipsType.ModifyGroupInfo
getOpUser | The identifier of the operator
getGroupName | The group name
getGroupInfoList | The modified group profile information. It is a list of TIMGroupTipsElemGroupInfo structs.

**`TIMGroupTipsElemGroupInfo` prototype:**

```
// Get the message content
java.lang.String    getContent()

//Get the type of the group profile modification message
TIMGroupTipsGroupInfoType   getType()
```

**`TIMGroupTipsGroupInfoType` prototype:**
```
//The profile photo URL is modified.
ModifyFaceUrl

//The group introduction is modified.
ModifyIntroduction

//The group name is modified.
ModifyName

//The group announcement is modified.
ModifyNotification

//The group owner is changed.
ModifyOwner
```

### Group member profile modifications

**Trigger:** when a group member’s profile related to the group is modified, such as when the member is muted or the member’s role in the group is changed, the system sends a tips message. You can update related display fields, or selectively display the message to users.

>
>- **The profile here refers to the information related to the group, such as muting duration and member role change, not the profile information about the user itself, such as the nickname**. Since the group may have many members, real-time update is not a best practice. Instead, we recommend you directly display the profile information contained in the message body.
>- If the user profile is stored locally, you can determine whether a change has occurred according to the information in the message body and update the profile after receiving a message from this user.

**Description of the responses of `TIMGroupTipsElem` member methods:**

Method | Response Description
---|---
getType | TIMGroupTipsType.ModifyMemberInfo
getOpUser | The identifier of the operator
getGroupName | The group name
getMemberInfoList | The modified group member profile information. It is a list of TIMGroupTipsElemMemberInfo structs.

**`TIMGroupTipsElemMemberInfo` prototype:**

```
//Get the identifier of the muted group member.
java.lang.String    getIdentifier()

//Get the muting duration.
long    getShutupTime()
```

## Group System Messages

When a user applies to join a group, the group admin receives a system message about the application. The admin can accept or reject the application, and the corresponding group system message will be displayed to the user.

**Group system message types:**

```
//Application to join the group is approved (received only by the applicant).
TIM_GROUP_SYSTEM_ADD_GROUP_ACCEPT_TYPE

//Application to join the group is rejected (received only by the applicant).
TIM_GROUP_SYSTEM_ADD_GROUP_REFUSE_TYPE

//Request to join the group (received only by the admin).
TIM_GROUP_SYSTEM_ADD_GROUP_REQUEST_TYPE

//Admin role is canceled (received only by the canceled admin).
TIM_GROUP_SYSTEM_CANCEL_ADMIN_TYPE

//Group is created (received only by the initial members).
TIM_GROUP_SYSTEM_CREATE_GROUP_TYPE

//Group is disbanded (received by all members).
TIM_GROUP_SYSTEM_DELETE_GROUP_TYPE

//Group admin is set (received by the new group admin).
TIM_GROUP_SYSTEM_GRANT_ADMIN_TYPE

//Invited to join the group (received by the invitee).
TIM_GROUP_SYSTEM_INVITED_TO_GROUP_TYPE

//Removed from the group by the admin (received by the user who is removed).
TIM_GROUP_SYSTEM_KICK_OFF_FROM_GROUP_TYPE

//Quit the group (received by the user who quits the group).
TIM_GROUP_SYSTEM_QUIT_GROUP_TYP

//Group is revoked (received by all members).
TIM_GROUP_SYSTEM_REVOKE_GROUP_TYPE

//Group invitation request (received by the invitee).
TIM_GROUP_SYSTEM_INVITE_TO_GROUP_REQUEST_TYPE

//Group invitation request accepted (received only by the inviter).
TIM_GROUP_SYSTEM_INVITATION_ACCEPTED_TYPE

//Group invitation request is rejected (only received by the inviter).
TIM_GROUP_SYSTEM_INVITATION_REFUSED_TYPE
```

**`TIMGroupSystemElem` member methods are defined as follows:**

```
/**
 *  Operator’s platform
 *  Valid values: iOS, Android, Windows, Mac, Web, RESTAPI, Unknown.
 * @return The platform of the operator.
 */
public String getPlatform()

/**
 * Get the subtype of the message.
 * @return The subtype of the group system message.
 */
public TIMGroupSystemElemType getSubtype()

/**
 * Get the group ID.
 * @return
 */
public String getGroupId()

/**
 * Get the operator.
 * @return The operator’s identifier.
 */
public String getOpUser()

/**
 * Get the reason for the operation.
 * @return The reason for the operation.
 */
public String getOpReason()

/**
 * Get the custom notification.
 * @return The custom notification.
 */
public byte[] getUserData()

/**
 * Get operator’s user profile.
 * @return Operator’s user profile.
 */
public TIMUserProfile getOpUserInfo()

/**
 * Get operator’s profile in the group.
 * @return Operator’s profile in the group.
 */
public TIMGroupMemberInfo getOpGroupMemberInfo()
```

### Application to join the group

**Trigger:** when a user applies to join a group, the group admin receives a message about the application. The message can be displayed to the user for the user to decide whether to approve the application. The message type is `TIM_GROUP_SYSTEM_ADD_GROUP_REQUEST_TYPE`.

**Description of the responses of TIMGroupSystemElem member methods:**

Method | Response Description
---|---
getSubtype | TIM_GROUP_SYSTEM_ADD_GROUP_REQUEST_TYPE
getGroupId | The ID of the target group of the application
getOpUser | The applicant
getOpReason | The reason for the application (optional)


### “Apply to join” request is approved/rejected

**Trigger:** if the admin approves an application to join the group, the applicant receives an approval notification message, and if the admin rejects the application, the applicant receives a rejection notification message.

**Description of the responses of `TIMGroupSystemElem` member methods:**

Method | Response Description
---|---
getSubtype | Approved: TIM_GROUP_SYSTEM_ADD_GROUP_ACCEPT_TYPE<br>Rejected: TIM_GROUP_SYSTEM_ADD_GROUP_REFUSE_TYPE
getGroupId | The ID of the group for which the application is approved/rejected
getOpUser | The identifier of the admin who processed the request
getOpReason | The reason for approval or rejection (optional)

### “Invited to join” request

**Trigger:** when a user is invited to join a group (**the user is not a group member and needs to approve the invitation**), the user receives an invitation message.

>When a group is created, the initial members are added to the group without invitation.

**Description of the responses of `TIMGroupSystemElem` member methods:**

Method | Response Description
---|---
getSubtype | TIM_GROUP_SYSTEM_INVITE_TO_GROUP_REQUEST_TYPE
getGroupId | The ID of the group the user is invited to join
getOpUser | The operator, who is the inviter in this case


### “Invited to join” request is accepted/rejected

**Trigger:** if the invitee accepts the invitation, the inviter receives an acceptance notification method, and if the invitee rejects the invitation, the inviter receives a rejection notification message.

**Description of the responses of `TIMGroupSystemElem` member methods:**

Method | Response Description
---|---
getSubtype | Accepted: TIM_GROUP_SYSTEM_INVITATION_ACCEPTED_TYPE<br>Rejected: TIM_GROUP_SYSTEM_INVITATION_REFUSED_TYPE
getGroupId | The ID of the group for which the application is approved/rejected
getOpUser | The identifier of the admin who processed the request
getOpReason | The reason for approval or rejection (optional)


### Member removed by admin

**Trigger:** when a user is removed from a group by the admin, the user receives a removal notification message.

**Description of the responses of `TIMGroupSystemElem` member methods:**

Method | Response Description
---|---
getSubtype | TIM_GROUP_SYSTEM_KICK_OFF_FROM_GROUP_TYPE
getGroupId | The ID of the group from which the user is removed
getOpUser | The identifier of the admin who performed the action


### Group is disbanded

**Trigger:** when a group is disbanded, all members receive a message notifying them that the group is disbanded.

**Description of the responses of `TIMGroupSystemElem` member methods:**

Method | Response Description
---|---
getSubtype | TIM_GROUP_SYSTEM_DELETE_GROUP_TYPE
getGroupId | The ID of the group that is disbanded
getOpUser | The identifier of the admin who performed the action

### Group is created

**Trigger:** when a group is created, the creator receives a creation notification message.

If a user calls the method to create a group and the success callback is returned, then the group was created successfully. This message is used for multi-client synchronization. When receiving this message, the other clients can update the group list, while the current client can choose to ignore it.

**Description of the responses of `TIMGroupSystemElem` member methods:**

Method | Response Description
---|---
getSubtype | TIM_GROUP_SYSTEM_CREATE_GROUP_TYPE
getGroupId | The ID of the group that is created
getOpUser | The creator, who is the user itself in this case

### “Invited to join” request

**Trigger:** when a user is invited to join a group (**the user has been added to the group at this time**), the user receives an invitation notification message.

>When a group is created, the initial members are added to the group without invitation.

**Description of the responses of `TIMGroupSystemElem` member methods:**

Method | Response Description
---|---
getSubtype | TIM_GROUP_SYSTEM_INVITED_TO_GROUP_TYPE
getGroupId | The ID of the group the user is invited to join
getOpUser | The operator, who is the inviter in this case

### Quits group

**Trigger:** when a user quits a group, the user receives a quit notification message, and only the user who quits will receive the message.

If a user calls `QuitGroup` and the success callback is returned, then the user has quit the group successfully. This message is used for multi-client synchronization. When receiving this message, the other clients can update the group list, while the current client can choose to ignore it.

**Description of the responses of `TIMGroupSystemElem` member methods:**

Method | Response Description
---|---
getSubtype | TIM_GROUP_SYSTEM_QUIT_GROUP_TYPE
getGroupId | The ID of the group that the user quits
getOpUser | The operator, who is the user itself in this case

### Admin is set/canceled

**Trigger:** when a user is set or canceled as the group admin, the user receives a corresponding notification.

**Description of the responses of `TIMGroupSystemElem` member methods:**

Method | Response Description
---|---
getSubtype | Admin role is cancelled: TIM_GROUP_SYSTEM_GRANT_ADMIN_TYPE<br>Admin role is granted: TIM_GROUP_SYSTEM_CANCEL_ADMIN_TYPE
getGroupId | The ID of the group in which the event occurs
getOpUser | The operator

### Group is revoked

**Trigger:** when a group is revoked by the system, all members receive a message notifying them that the group has been revoked.

**Description of the responses of `TIMGroupSystemElem` member methods:**

Method | Response Description
---|---
getSubtype | TIM_GROUP_SYSTEM_REVOKE_GROUP_TYPE
getGroupId | The ID of the group that is revoked
