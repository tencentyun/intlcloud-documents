## Group Overview

Instant Messaging (IM) supports multiple group types. For more information on their characteristics and limits, see [Group System](https://intl.cloud.tencent.com/document/product/1047/33529). A group is identified by a unique ID that enables different operations.

## Group Messages

Group messages and C2C (one-to-one) messages are the same except for the conversation type obtained through Conversation. For more information, see [Sending Messages](https://intl.cloud.tencent.com/document/product/1047/34320).

## Group Management

Operations related to groups are performed after login through `TIMGroupManager`.

**Prototype for getting a singleton:**

```
/** Get instance
 * @return TIMGroupManager instance
 */
public static TIMGroupManager getInstance()

```

### Creating a group

IM has the following built-in group types: **private group (Private), public group (Public), chat room (ChatRoom), audio-video chat room (AVChatRoom), and broadcasting chat room (BChatRoom)**. For more information, please see [Group Types](https://intl.cloud.tencent.com/document/product/1047/33529#.E7.BE.A4.E7.BB.84.E5.BD.A2.E6.80.81.E4.BB.8B.E7.BB.8D).

- **Audio-video chat room (AVChatRoom):** this is also called a live-streaming group, which can support an unlimited number of members but does not support features such as adding members or querying the total number of members.
- You can create groups through `createGroup` in `TIMGroupManager`. When creating a group, you can specify certain group profile information, such as the group type, name, introduction, list of users to be added to the group, and even the group ID. The group ID is returned after the group is created and can be used to get Conversation to receive and send messages.

> You need to follow certain rules when defining group IDs. For more information, see [Custom Group IDs](https://intl.cloud.tencent.com/document/product/1047/33529#.E8.87.AA.E5.AE.9A.E4.B9.89.E7.BE.A4.E7.BB.84-id).

**Prototype:**

```
/**
 * Create a group
 * @param param Information set that is needed for creating a group, see {@see CreateGroupParam}
 * @param cb Callback. The parameter of the OnSuccess function returns the ID of the group that is created.
 */
public void createGroup(@NonNull CreateGroupParam param, @NonNull TIMValueCallBack<String> cb)
```

**`TIMGroupManager.CreateGroupParam` provides the following APIs:**
```
/**
 * Create constructor of group parameters
 * @param type Group type. The group types currently supported include private group (Private), public group (Public),
 *             chat room (ChatRoom), audio-video chat room (AVChatRoom), and broadcasting chat room (BChatRoom).
 * @param name Group name
 */
public CreateGroupParam(@NonNull String type, @NonNull String name)

/**
 * Set the group ID for the group to be created
 * @param groupId Group ID
 */
public CreateGroupParam setGroupId(String groupId)

/**
 * Set the group announcement for the group to be created
 * @param notification Group announcement
 */
public CreateGroupParam setNotification(String notification)

/**
 * Set the group introduction for the group to be created
 *  @param introduction     Group introduction
 */
public CreateGroupParam setIntroduction(String introduction)

/**
 * Set the group profile photo URL for the group to be created
 * @param url Group profile photo URL
 */
public CreateGroupParam setFaceUrl(String url)

/**
 * Set the option for joining the group
 * @param option Option for joining the group
 */
public CreateGroupParam setAddOption(TIMGroupAddOpt option)

/**
 * Set the maximum number of group members supported by the group to be created
 * @param maxMemberNum Maximum number of group members
 */
public CreateGroupParam setMaxMemberNum(long maxMemberNum)

/**
 * Set the custom information for the group to be created
 * @param key Key of custom information, up to 16 bytes
 * @param value Value of custom information, up to 512 bytes
 */
public CreateGroupParam setCustomInfo(String key, byte[] value)

/**
 * Set the initial members of the group to be created
 * @param infos List of initial member information
 */
public CreateGroupParam setMembers(List<TIMGroupMemberInfo> infos)
```

**Example:**
```
//Create a public group without customizing the group ID
TIMGroupManager.CreateGroupParam param = new TIMGroupManager.CreateGroupParam("Public", "test_group");
//Specify group introduction
param.setIntroduction("hello world");
//Specify group notification
param.setNotification("welcome to our group");

//Add group member
List<TIMGroupMemberInfo> infos = new ArrayList<TIMGroupMemberInfo>();
TIMGroupMemberInfo member = new TIMGroupMemberInfo("cat");
infos.add(member);
param.setMembers(infos);

//Set group custom field (configure the key in the console first)
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

You can add (invite) users to a group through `inviteGroupMember` of `TIMGroupManager`.

**Permission description:**

For more information, see [Differences in group member operations](https://intl.cloud.tencent.com/document/product/1047/33529#.E7.BE.A4.E6.88.90.E5.91.98.E6.93.8D.E4.BD.9C.E5.B7.AE.E5.BC.82). 

**Prototype:**

```
/**
 * Invite to group
 * @param groupId Group ID
 * @param memList List of IDs of the users to be added to the group
 * @param cb Callback. The parameter of the OnSuccess function returns the accounts of users who have been added to the group
 */
public void inviteGroupMember(@NonNull String groupId, @NonNull List<String> memList,
							  @NonNull TIMValueCallBack<List<TIMGroupMemberResult>> cb)
```

**`TIMGroupMemberResult` is defined as follows:**

```
/**
 * Get operation result
 * @return Operation result: 0: failed. 1: successful. 2: the user was already a group member when added, or the user was not a group member when deleted.
 */
public long getResult()

/**
 * Get user account
 * @return User account
 */
public String getUser()
```


**Example:**

```
//Create a list of members to be added to the group
ArrayList list = new ArrayList();

String user = "";

//Add users
user = "sample_user_1";
list.add(user);
user = "sample_user_2";
list.add(user);
user = "sample_user_3";
list.add(user);

//Callback
TIMValueCallBack<List<TIMGroupMemberResult>> cb = new TIMValueCallBack<List<TIMGroupMemberResult>>() {
    @Override
    public void onError(int code, String desc) {
    }

    @Override
    public void onSuccess(List<TIMGroupMemberResult> results) { //Group member operation results
        for(TIMGroupMemberResult r : results) {
            Log.d(tag, "result: " + r.getResult()  //Operation result: 0: failed to add. 1: added successfully. 2: already a group member.
                    + " user: " + r.getUser());    //User account
        }
    }
};

//Add the users in the list to the group
TIMGroupManager.getInstance().inviteGroupMember(
        groupId,   //Group ID
        list,      //List of users to be added to the group
        cb);       //Callback
```

### Applying to join a group

`applyJoinGroup` of `TIMGroupManager` allows users to apply to join a group. This operation is valid only for public groups, chat rooms, and audio-video chat rooms.

**Permission description:**

For more information, see [Differences in group member operations](https://intl.cloud.tencent.com/document/product/1047/33529#.E7.BE.A4.E6.88.90.E5.91.98.E6.93.8D.E4.BD.9C.E5.B7.AE.E5.BC.82).

**Prototype:**

```
/**
 * Join group
 * @param groupId Group ID
 * @param reason Reason for the application (optional)
 * @param cb Callback
 */
public void applyJoinGroup(@NonNull String groupId, String reason, @NonNull TIMCallBack cb)
```

In the following example, a user applies to join group “@TGS#1JYSZEAEQ” and the reason for the application is “some reason”. **Example:**

```
TIMGroupManager.getInstance().applyJoinGroup("@TGS#1JYSZEAEQ", "some reason", new TIMCallBack() {
    @java.lang.Override
    public void onError(int code, String desc) {
        //The API returns "code" (error code) and "desc" (error description) which can be used as the cause
        //For a list of error codes, see the Error Code Table
        Log.e(tag, "applyJoinGroup err code = " + code + ", desc = " + desc);
    }

    @java.lang.Override
    public void onSuccess() {
        Log.i(tag, "applyJoinGroup success");
    }
});
```

### Quitting a group

Group members can quit a group through the API provided by `TIMGroupManager`.

**Permission description:**

- **Private group:** every member can quit the group.
- **Public group, chat room, and live-streaming group:** the group owner cannot quit the group.

For more information, see [Differences in group member operations](https://intl.cloud.tencent.com/document/product/1047/33529#.E7.BE.A4.E6.88.90.E5.91.98.E6.93.8D.E4.BD.9C.E5.B7.AE.E5.BC.82).

**Prototype:**

```
/**
 * Quit a group
 * @param groupId Group ID
 * @param cb Callback
 */
public void quitGroup(@NonNull String groupId, @NonNull TIMCallBack cb)
```

**Example:**

```
//Create callback
TIMCallBack cb = new TIMCallBack() {
    @Override
    public void onError(int code, String desc) {
            //"code" (error code) and "desc" (error description) can be used to locate the cause of the request failure
            //For the meaning of the error code, please see the Error Code Table
    }

    @Override
    public void onSuccess() {
        Log.e(tag, "quit group succ");
    }
};

//Quit a group
TIMGroupManager.getInstance().quitGroup(
        groupId,  //Group ID
        cb);      //Callback
```

### Deleting group members

This function’s parameters are the same as those of joining a group. The API to delete group members is provided by `TIMGroupManager`.

**Permission description:**
For more information, see [Differences in group member operations](https://intl.cloud.tencent.com/document/product/1047/33529#.E7.BE.A4.E6.88.90.E5.91.98.E6.93.8D.E4.BD.9C.E5.B7.AE.E5.BC.82).

**Prototype:**

```
/**
 * Deleting group members
 * @param param Parameter for deleting group members
 * @param cb Callback. The parameter of the OnSuccess function returns a list of group members that have been deleted.
 */
public void deleteGroupMember(@NonNull DeleteMemberParam param,
							  @NonNull TIMValueCallBack<List<TIMGroupMemberResult>> cb)
```

**`DeleteMemberParam` is defined as follows:**
```
/**
 * Construct parameter
 * @param groupId Group ID
 * @param members List of user IDs
 */
public DeleteMemberParam(@NonNull String groupId, @NonNull List<String> members)

/**
 * Set the reason for deleting the group members (optional)
 * @param reason  Reason for deleting
 */
public DeleteMemberParam setReason(@NonNull String reason)
```

**Example:**

```
//Create a list of group members to be deleted
ArrayList list = new ArrayList();

String user = "";
//Add users
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
	public void onSuccess(List<TIMGroupMemberResult> results) { //Group member operation results
		for(TIMGroupMemberResult r : results) {
			Log.d(tag, "result: " + r.getResult()  //Operation result: 0: failed to delete. 1: deleted successfully. 2: not a group member.
					+ " user: " + r.getUser());    //User account
		}
	}
});
```

### Getting group member list

The API to get a list of group members is `getGroupMembers`. Built-in fields and custom fields are pulled by default. Go to [IM Console](https://console.cloud.tencent.com/im) -> **Feature Configuration** -> **Group member custom fields** to configure the keys and permissions for custom fields, which take effect after 5 minutes.

**Permission description:**

- **Any type of group:** member list can be obtained.
- **Live-streaming group:** the member list only contains the group owner, admin, and some members.

For more information, see [Differences in group operations](https://intl.cloud.tencent.com/document/product/1047/33529#.E7.BE.A4.E7.BB.84.E6.93.8D.E4.BD.9C.E5.B7.AE.E5.BC.82). 

**Prototype:**

```
/**
 * Get group member list
 * @param groupId Group ID
 * @param cb Callback. The parameter of the OnSuccess function returns the list of group members.
 */
public void getGroupMembers(@NonNull String groupId, @NonNull TIMValueCallBack<List<TIMGroupMemberInfo>> cb)
```

**Example:**

```
//Create callback
TIMValueCallBack<List<TIMGroupMemberInfo>> cb = new TIMValueCallBack<List<TIMGroupMemberInfo>> () {
    @Override
    public void onError(int code, String desc) {
    }

    @Override
    public void onSuccess(List<TIMGroupMemberInfo> infoList) {//The parameter returns group member information

        for(TIMGroupMemberInfo info : infoList) {
            Log.d(tag, "user: " + info.getUser() +
            "join time: " + info.getJoinTime() +
            "role: " + info.getRole());
        }
    }
};

//Get group member information
TIMGroupManager.getInstance().getGroupMembers(
        groupId,   //Group ID
        cb);     //Callback
```

### Getting the list of groups the user has joined

You can get the list of groups the current user has joined through `TIMGroupManager`. The returned information contains only part of the basic information. To get detailed group information, see [Get group profiles of group members](https://intl.cloud.tencent.com/document/product/1047/34328).

**Permission description:**

- **Private group, public group, and chat room:** this API allows you to get the information of public groups, chat rooms, and activated private groups the user has joined.
- **Audio-video chat room and broadcasting chat room:** these two types of groups will not be obtained through this API due to the differences in internal implementation.

**Prototype:**

```
/**
 * Get the list of groups the user has joined
 * @param cb Callback. The parameter of the OnSuccess function returns the groups the user has joined
 */
public void getGroupList(@NonNull TIMValueCallBack<List<TIMGroupBaseInfo>> cb)
```

**`TIMGroupBaseInfo` provides the following methods:**
```
/**
 * Get group ID
 * @return Group ID
 */
public String getGroupId()

/**
 * Get group name
 * @return Group name
 */
public String getGroupName()

/**
 * Get group type
 * @return Group type
 */
public String getGroupType()

/**
 * Get group profile photo URL
 * @return Group profile photo URL
 */
public String getFaceUrl()

/**
 * Get whether the current group has set Mute All or not
 * @return true - Mute All has been set
 * @since 3.1.1
 */
public boolean isSilenceAll()
```

**Example:**

```
//Create callback
TIMValueCallBack<List<TIMGroupBaseInfo>> cb = new TIMValueCallBack<List<TIMGroupBaseInfo>>() {
    @Override
    public void onError(int code, String desc) {
        //"code" (error code) and "desc" (error description) can be used to locate the cause of the request failure
        //For the meaning of the error code, please see the Error Code Table
        Log.e(tag, "get group list failed: " + code + " desc");
    }

    @Override
    public void onSuccess(List<TIMGroupBaseInfo> timGroupInfos) {//The parameter returns the basic information of each group
        Log.d(tag, "get group list succ");

        for(TIMGroupBaseInfo info : timGroupInfos) {
            Log.d(tag, "group id: " + info.getGroupId() +
            " group name: " + info.getGroupName() +
            " group type: " + info.getGroupType());
        }
    }
};

//Get the list of groups the user has joined
TIMGroupManager.getInstance().getGroupList(cb);
```

### Disbanding groups

 The API to disband groups is provided by `TIMGroupManager`.

**Permission description:**
For more information, see [Differences in group operations](https://intl.cloud.tencent.com/document/product/1047/33529#.E7.BE.A4.E7.BB.84.E6.93.8D.E4.BD.9C.E5.B7.AE.E5.BC.82). 

**Prototype:**

```
/**
 * Delete group
 * @param groupId Group ID
 * @param cb Callback
 */
public void deleteGroup(@NonNull String groupId, @NonNull TIMCallBack cb)
```

**Example:**

```
//Disbanding groups
TIMGroupManager.getInstance().deleteGroup(groupId, new TIMCallBack() {
    @Override
    public void onError(int code, String desc) {

        //"code" (error code) and "desc" (error description) can be used to locate the cause of the request failure
        //For a list of error codes, see the Error Code Table
        Log.d(tag, "login failed. code: " + code + " errmsg: " + desc);
    }

    @Override
    public void onSuccess() {
        //Group disbanded successfully
    }
});
```

### Transferring a group

The API to transfer groups is provided by `TIMGroupManager`.

**Permission description:**

Only the **group owner** can transfer a group.

**Prototype:**

```
/**
 * Change the group owner
 * @param groupId Group ID
 * @param identifier The identifier of the new group owner
 * @param cb Callback
 */
public void modifyGroupOwner(@NonNull String groupId, @NonNull String identifier, @NonNull TIMCallBack cb)
```

### Other APIs

**The API to get specified types of members (to pull group admins, group owners, and group members respectively) is defined as follows:**

```
/**
 * Get the group member list according to filter conditions (the list can be pulled by field and in pages)
 * @param groupId Group ID
 * @param flags The flag of profiles to be pulled, such as {@see TIMGroupManager#TIM_GET_GROUP_MEM_INFO_FLAG_NAME_CARD} or any combination of them
 * @param filter Role filter, see {@see TIMGroupMemberRoleFilter}
 * @param custom The list of custom keys to get
 * @param nextSeq     The flag for pulling in pages. Enter 0 for the first request. If the success callback returns a value that is not 0, then the list will be pulled in pages. Pass this parameter to pull again until the value becomes 0.
 * @param cb Callback
 */
public void getGroupMembersByFilter(@NonNull String groupId, long flags, @NonNull TIMGroupMemberRoleFilter filter,
									List<String> custom, long nextSeq, TIMValueCallBack<TIMGroupMemberSucc> cb)
```

## Getting Group Profiles

### Getting group profiles

You can use the `getGroupInfo` method provided by `TIMGroupManager` to get group profiles stored on the server and use the `queryGroupInfo` method to pull group profiles cached locally. Group members can pull group information. Non-members cannot pull private groups’ information and can only pull public fields of other types of groups, `groupId\groupName\groupOwner\groupType\createTime\memberNum\maxMemberNum\onlineMemberNum\groupIntroduction\groupFaceUrl\addOption\custom`.

**Note:**

Basic profile and custom fields are pulled by default. Go to the [IM Console](https://console.cloud.tencent.com/im) -> **Feature Configuration** -> **Group custom fields** to configure the keys and permissions for custom fields, which take effect after 5 minutes.

**Prototype:**

```
/**
 * Get the group information stored on the server
 * @param groupIdList The list of groups of which the detailed information is to be pulled. Up to 50 groups can be pulled at a time.
 * @param cb Callback. The parameter of the OnSuccess function returns the list of group information {@see TIMGroupDetailInfo}
 */
public void getGroupInfo(@NonNull List<String> groupIdList,
							   @NonNull TIMValueCallBack<List<TIMGroupDetailInfo>> cb)
/**
 * Get the group information stored locally
 * @param groupId The IDs of the groups of which the detailed information is to be pulled
 * @return Group information. null is returned if the group information is not stored locally.
 */
 public TIMGroupDetailInfo queryGroupInfo(@NonNull String groupId)
```

**`TIMGroupDetailInfo` is defined as follows:**
```
/**
 * Get group ID
 * @return Group ID
 */
public String getGroupId()

/**
 * Get group name
 * @return Group name
 */
public String getGroupName()

/**
 * Get group creator account
 * @return Group creator account
 */
public String getGroupOwner()

/**
 * Get group creation time
 * @return Group creation time
 */
public long getCreateTime()

/**
 * Get the last modified time of group information
 * @return The last modified time of group information
 */
public long getLastInfoTime()

/**
 * Get the time of the last group message
 * @return The time of the last group message
 */
public long getLastMsgTime()

/**
 * Get the number of group members
 * @return The number of group members
 */
public long getMemberNum()

/**
 * The maximum number of group members supported
 * @return The maximum number of group members
 */
public long getMaxMemberNum()

/**
 * Get group introduction
 * @return Group introduction
 */
public String getGroupIntroduction()

/**
 * Get group announcement
 * @return Group announcement
 */
public String getGroupNotification()

/**
 * Get group profile photo URL
 * @return Group profile photo URL
 */
public String getFaceUrl()

/**
 * Get group type
 * @return Group type
 */
public String getGroupType()

/**
 * Get the option for joining the group
 * @return The option for joining the group
 */
public TIMGroupAddOpt getGroupAddOpt()

/**
 * Get the last message in the group
 * @return The last message in the group
 */
public TIMMessage getLastMsg()

/**
 * Get the group custom field map
 * @return The group custom field map
 */
public Map<String, byte[]> getCustom()

/**
 * Get whether this group has set Mute All or not
 * @return true - Mute All has been set for the group
 * @since 3.1.1
 */
public boolean isSilenceAll()
```

**Example:**

```
//Create a list of group IDs for which you want to get information
ArrayList<String> groupList = new ArrayList<String>();

//Create callback
TIMValueCallBack<List<TIMGroupDetailInfo>> cb = new TIMValueCallBack<List<TIMGroupDetailInfo>>() {
    @Override
    public void onError(int code, String desc) {
            //"code" (error code) and "desc" (error description) can be used to locate the cause of the request failure
            //For a list of error codes, see the Error Code Table
    }

    @Override
    public void onSuccess(List<TIMGroupDetailInfo> infoList) { //The parameter returns the list of group information
        for(TIMGroupDetailInfo info : infoList) {
            Log.d(tag, "groupId: " + info.getGroupId()           //Group ID
            + " group name: " + info.getGroupName()              //Group name
            + " group owner: " + info.getGroupOwner()            //Group creator account
            + " group create time: " + info.getCreateTime()      //Group creation time
            + " group last info time: " + info.getLastInfoTime() //Last modified time of group information
            + " group last msg time: " + info.getLastMsgTime()  //The time of the last group message
            + " group member num: " + info.getMemberNum());      //The number of group members
        }
    }
};

//Add group ID
String groupId = "TGID1EDABEAEO";
groupList.add(groupId);

//Get group information stored on the server
TIMGroupManager.getInstance().getGroupInfo(
        groupList, //List of group IDs for which you want to get information
        cb);       //Callback

//Get group information cached locally
TIMGroupDetailInfo timGroupDetailInfo = TIMGroupManager.getInstance().queryGroupInfo(groupId);
```

### Getting your own profile in a group

You can obtain your own profile in a group when the list of groups you have joined is pulled. See [Getting group list](#.E8.8E.B7.E5.8F.96.E5.8A.A0.E5.85.A5.E7.9A.84.E7.BE.A4.E7.BB.84.E5.88.97.E8.A1.A8). If you want to get your profile in a single group, use `getSelfInfo` of `TIMGroupManager` as shown below. If the app needs to get a group list, we recommend that you get the profiles in groups when getting the group list instead of calling the following API.

**Permission description:**

**Live-streaming groups** do not support getting your own profile in the group.

**Prototype:**

```
/**
 * Get your own information in the group
 * @param groupId Group ID
 * @param cb Callback. The parameter of the OnSuccess function returns your own information
 */
public void getSelfInfo(@NonNull String groupId, @NonNull TIMValueCallBack<TIMGroupSelfInfo> cb)
```

### Getting the profiles of specified group members

The API to get group member profiles is provided by `TIMGroupManager`. Basic profiles are pulled by default.

**Permission description:**

For a **live-streaming group**, only the profiles of some members can be pulled, including the group owner, admin, and some members.

**Prototype:**
```
/**
 * Get the profiles of specified members in the group
 @param groupId ID of the group you specify
 * @param identifiers Up to 100 identifiers of specified group members
 * @param cb Callback. The parameter of the OnSuccess function returns the group member list
 */
public void getGroupMembersInfo(@NonNull String groupId, @NonNull List<String> identifiers,
								@NonNull TIMValueCallBack<List<TIMGroupMemberInfo>> cb)
```


## Modifying the Group Profile

The API to modify the group profile is provided by `TIMGroupManager`, which allows you to modify information such as the group name, introduction, and announcement.

**Prototype:**

```
/**
 * Modify group basic information
 * @param param Parameter class
 * @param cb Callback
 */
public void modifyGroupInfo(@NonNull ModifyGroupInfoParam param, @NonNull TIMCallBack cb)
```

**`TIMGroupManager.ModifyGroupInfoParam` is defined as follows:**

```
/**
 * Construct parameter instance
 * @param groupId Group ID
 */
public ModifyGroupInfoParam(@NonNull String groupId)

/**
 * Set the modified group name
 * @param groupName Group name
 */
public ModifyGroupInfoParam setGroupName(@NonNull String groupName)

/**
 * Set the modified group announcement
 * @param notification Group announcement
 */
public ModifyGroupInfoParam setNotification(@NonNull String notification)

/**
 * Set the modified group introduction
 * @param introduction Group introduction
 */
public ModifyGroupInfoParam setIntroduction(@NonNull String introduction)

/**
 * Set the modified group profile photo URL
 * @param faceUrl Group profile photo URL
 */
public ModifyGroupInfoParam setFaceUrl(@NonNull String faceUrl)

/**
 * Set the option for joining the group
 * @param addOpt Option for joining the group
 */
public ModifyGroupInfoParam setAddOption(@NonNull TIMGroupAddOpt addOpt)

/**
 * Set the maximum number of group members
 * @param maxMemberNum The maximum number of group members
 */
public ModifyGroupInfoParam setMaxMemberNum(long maxMemberNum)

/**
 * Set whether group members are visible to users outside the group
 * @param visable Whether group members are visible to users outside the group
 */
public ModifyGroupInfoParam setVisable(boolean visable)

/**
 * Set group custom field
 * @param customInfos Group custom field dictionary
 */
public ModifyGroupInfoParam setCustomInfo(@NonNull Map<String, byte[]> customInfos)

/**
 * Set Mute All
 * @param silenceAll true - Mute All, false - Unmute All
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
- **Private group:** users can join the group only through invitation and not application.

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

### Modifying group custom fields

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

The API to modify group member profiles is provided by `TIMGroupManager`, which allows you to modify group members’ roles and name cards and mute group members.

**Prototype:**

```
/**
 * Modify group member profiles
 * @param param The parameter for modifying a group member profile
 * @param cb Callback
 */
public void modifyMemberInfo(@NonNull ModifyMemberInfoParam param, @NonNull TIMCallBack cb)
```

**`TIMGroupManager.ModifyMemberInfoParam` is defined as follows:**

```
/**
 * Construct parameter for modifying a group member profile
 * @param groupId The group ID
 * @param identifier The user ID of the group member whose profile is to be modified
 */
public ModifyMemberInfoParam(@NonNull String groupId, @NonNull String identifier)

/**
 * Modify a group member’s name card
 * @param nameCard Group name card
 */
public ModifyMemberInfoParam setNameCard(@NonNull String nameCard)

/**
 * Modify the option for receiving group messages
 * @param receiveMessageOpt The option for receiving group messages. See {@see TIMGroupReceiveMessageOpt}
 */
public ModifyMemberInfoParam setReceiveMessageOpt(@NonNull TIMGroupReceiveMessageOpt receiveMessageOpt)

/**
 * Modify a group member’s role (only the group owner and admins can modify roles)
 * @param roleType The type of the role. Cannot be changed to group owner. See {@see TIMGroupMemberRoleType}
 */
public ModifyMemberInfoParam setRoleType(TIMGroupMemberRoleType roleType)

/**
 * Set the duration of muting (only the group owner and admin can set this)
 * @param silence Duration of muting
 */
public ModifyMemberInfoParam setSilence(long silence)

/**
 * Set group custom field
 * @param customInfo Group custom field dictionary
 */
public ModifyMemberInfoParam setCustomInfo(Map<String, byte[]> customInfo)
```

### Modifying a member’s role in the group

**Permission description:**

- **Only the group owner or admin** can modify group members’ roles.
- **Live-streaming group** does not support modifying group members’ roles.

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

You can mute group members and set the duration of muting through `modifyMemberInfoParam.setSilence()`.

**Permission description:**

- **Only the group owner or admin** can mute group members.

**Example:**

```
//Mute for 100 seconds
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

### Modifying a member’s name card in a group


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
//Do not receive group messages and the server does not forward them
TIMGroupReceiveMessageOpt.NotReceive

//Receive group messages but do not push offline messages when offline
TIMGroupReceiveMessageOpt.ReceiveNotNotify

//Receive group messages and push offline messages when offline
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
 * Get group ID
 * @return Group ID
 */
public String getGroupId()

/**
 * Get the identifier of the requester, who is the requester for “apply to join” requests and the inviter for “invited to join” requests.
 * @return The requester’s identifier
 */
public String getFromUser()

/**
 * Get the identifier of the handler. The identifier is 0 if it is an “apply to join” request and the invitee if it is an “invited to join” request.
 * @return The handler’s identifier
 */
public String getToUser()

/**
 * Get the time the group pending request is added
 * @return The time the group pending request is added
 */
public long getAddTime()

/**
 * Get the type of the group pending request
 * @return The type of the group pending request. See TIMGroupPendencyGetType for details
 */
public TIMGroupPendencyGetType getPendencyType()

/**
 * Get the processing status of the group pending request
 * @return The processing status of the group pending request. See {@see TIMGroupPendencyHandledStatus}
 */
public TIMGroupPendencyHandledStatus getHandledStatus()

/**
 * Get the processing type of the group pending request. Only valid when the processing status is not {@see TIMGroupPendencyHandledStatus#NOT_HANDLED}.
 * @return The processing type of the group pending request. See {@see TIMGroupPendencyOperationType}
 */
public TIMGroupPendencyOperationType getOperationType()

/**
 * Get the additional information added by the requester
 * @return The additional information added by the requester
 */
public String getRequestMsg()

/**
 * Get the custom information added by the requester
 * @return The custom information added by the requester
 */
private String getRequestUserData()

/**
 * Get the additional information added by the handler. Only valid when the processing status is not {@see TIMGroupPendencyHandledStatus#NOT_HANDLED}.
 * @return The additional information added by the handler
 */
public String getHandledMsg()

/**
 * Get the custom information added by the handler. Only valid when the processing status is not {@see TIMGroupPendencyHandledStatus#NOT_HANDLED}.
 * @return The custom information added by the handler
 */
private String getHandledUserData()

/**
 * Approve the request. Only valid for “apply to join” and “invited to join” messages.
 *
 * @param msg Reason for approval (optional)
 * @param cb Callback
 */
public void accept(String msg, TIMCallBack cb)

/**
 * Reject the request. Only valid for “apply to join” and “invited to join” messages.
 *
 * @param msg Reason for approval (optional)
 * @param cb Callback
 */
public void refuse(String msg, TIMCallBack cb)
```

### Pulling a list of group pending requests

You can pull information related to group pending requests through the `getGroupPendencyList` API of `TIMGroupManager`. A message can be pulled through this API even after it has been approved or rejected. In this case, the message pulled has a “processed” flag.

**Permission description:**

**Only the approver** has permission to pull the information.

> For example:
>- If user A applies to join group A, the group admin can obtain information related to this pending request. As user A does not have approval permission, user A does not need to obtain information related to this pending request.
>- If admin A invites user A to join group A, user A can obtain the information related to this pending request because this pending request needs to be approved by user A.

**Prototype:**

```
/**
 * Get group pending requests in pages
 * @param param The parameter for getting a list of group pending requests. See {@see TIMGroupPendencyGetParam}
 * @param cb Callback. The parameter of onSuccess returns the list of group pending requests and metadata. See {@see TIMGroupPendencyMeta} and {@see TIMGroupPendencyItem}
 */
public void getGroupPendencyList(@NonNull TIMGroupPendencyGetParam param,
								 @NonNull TIMValueCallBack<TIMGroupPendencyListGetSucc> cb)
```

**`TIMGroupPendencyGetParam` is defined as follows:**

```
/**
 * Set the paging timestamp. Enter 0 for the first request and subsequent values according to the timestamps in {@see TIMGroupPendencyMeta} returned by the server
 * @param timestamp Paging timestamp
 */
public void setTimestamp(long timestamp)

/**
 * Set the number of requests per page (this is a suggested value which does not indicate completion; the server can return more or less requests)
 * @param numPerPage The number of requests per page
 */
public void setNumPerPage(long numPerPage)
```

**Example:**

```
TIMGroupPendencyGetParam param = new TIMGroupPendencyGetParam();
param.setTimestamp(0);//Enter 0 for the first request
param.setNumPerPage(10);

TIMGroupManager.getInstance().getGroupPendencyList(param, new TIMValueCallBack<TIMGroupPendencyListGetSucc>() {
    @Override
    public void onError(int code, String desc) {

    }

    @Override
    public void onSuccess(TIMGroupPendencyListGetSucc timGroupPendencyListGetSucc) {
        //If the nextStartTimestamp in meta is not 0, then save it
        //as the parameter in TIMGroupPendencyGetParam for getting the next page of data
        TIMGroupPendencyMeta meta = timGroupPendencyListGetSucc.getPendencyMeta();
        Log.d(tag, meta.getNextStartTimestamp()
                + "|" + meta.getReportedTimestamp() + "|" + meta.getUnReadCount());

        List<TIMGroupPendencyItem> pendencyItems = timGroupPendencyListGetSucc.getPendencies();
        for(TIMGroupPendencyItem item : pendencyItems){
            //Operate on group pending requests, such as view, approve, or reject a request
        }
    }
});
```

### Reporting that group pending requests are read

Report that the current pending request and all the pending requests before it have been read through `reportGroupPendency` of `TIMGroupManager`. After the report, you can still pull these pending requests and determine whether they are read through the read timestamp.

**Prototype:**

```
/**
 * Report that group pending requests are read
 * @param timestamp Read timestamp in seconds. Group pending requests before this timestamp are set as read.
 * @param cb Callback
 */
public void reportGroupPendency(long timestamp, @NonNull TIMCallBack cb)
```


### Processing group pending requests

Get a list of group pending requests (`TIMGroupPendencyItem`) through `getGroupPendencyList` and process the requests through the `accept/refuse` API in the `TIMGroupPendencyItem` class. Requests that have been processed cannot be processed again.

**Prototype:**

```
/**
 * Approve the request. Only valid for “apply to join” and “invited to join” messages.
 *
 * @param msg Reason for approval (optional)
 * @param cb Callback
 */
public void accept(String msg, TIMCallBack cb)

/**
 * Reject the request. Only valid for “apply to join” and “invited to join” messages.
 *
 * @param msg Reason for approval (optional)
 * @param cb Callback
 */
public void refuse(String msg, TIMCallBack cb)
```

## Group Event Messages

When a user is invited to join a group or is removed from a group, a tip message is displayed in the group. The caller can choose to display the tip message or ignore it. A tip message is identified by a special `Elem` and returned by the new message callback (see [New message notification](/doc/product/269/9229#.E6.96.B0.E6.B6.88.E6.81.AF.E9.80.9A.E7.9F.A5)). To get group event messages, in addition to relying on new message notifications, you can also set group event listeners to listen to different events through `setGroupEventListener` of `TIMUserConfig` **before login** (see [Initialization (Android)](https://intl.cloud.tencent.com/document/product/1047/34312)).

> The group event messages of chat rooms (ChatRoom) and audio-video chat rooms (AVChatRoom) are not delivered by new message notifications. Therefore, you must register group event listeners to listen to different group events.

The following figure shows an event message for group name modification.
![](https://main.qcloudimg.com/raw/78865ba68ed75700137e5afbd2ac3e43.jpg)


**`TIMGroupTipsElem` member methods:**

```
//Get the list of messages for group profile modifications. Only valid when the value of tipsType is TIMGroupTipsType.ModifyGroupInfo.
java.util.List<TIMGroupTipsElemGroupInfo> getGroupInfoList()

//Get group name
java.lang.String    getGroupName()

//Get the list of messages for group member modifications. Only valid when the value of tipsType is TIMGroupTipsType.ModifyMemberInfo.
java.util.List<TIMGroupTipsElemMemberInfo>    getMemberInfoList()

//Get the operator
java.lang.String    getOpUser()

//Get the type of the group event notification
TIMGroupTipsType    getTipsType()

//Get the list of accounts on which to operate
java.util.List<java.lang.String>  getUserList()
```

**`TIMGroupTipsType` prototype:**

```
//Cancel admin
CancelAdmin

//Join group
Join

//Kick group member out
Kick

//Modify group profile
ModifyGroupInfo

//Modify member information
ModifyMemberInfo

//Quit group
Quit

//Set admin
SetAdmin
```

### Notification for a user joining the group

**Trigger:** when a user joins a group through application or invitation, the system sends a message in the group. The developer can choose a display style and update the group member list. The type of the message received is `TIMGroupTipsType.Join`.

**Description of the responses of `TIMGroupTipsElem` member methods:**

Method | Response Description
---|---
getType | TIMGroupTipsType.Join
getOpUser | Apply to join: the applicant</br>Invited to join: the inviter
getGroupName | Group name
getUserList | List of users that are added to the group

### User quits the group

**Trigger:** when a user quits a group, the system sends a notification in the group. You can choose to update the group member list. The type of the message received is `TIMGroupTipsType.Quit`.

**Description of the responses of `TIMGroupTipsElem` member methods:**

Method | Response Description
---|---
getType | TIMGroupTipsType.Quit
getOpUser | The identifier of the user who quits the group
getGroupName | Group name

### User is kicked out of the group

**Trigger:** when a user is kicked out of the group, the system sends a notification in the group. You can choose to update the group member list. The type of the message received is `TIMGroupTipsType.Kick`.

**Description of the responses of `TIMGroupTipsElem` member methods:**

Method | Response Description
---|---
getType | TIMGroupTipsType.Kick
getOpUser | The identifier of the user who kicks out members
getGroupName | Group name
getUserList | List of users who are kicked out

### Group admin is set/canceled

**Trigger:** when a user is set or cancelled as an admin, the system sends a notification in the group. If the UI shows whether a user is an admin, you can update the admin flag. The message types are `TIMGroupTipsType.SetAdmin` and `TIMGroupTipsType.CancelAdmin`.

**Description of the responses of `TIMGroupTipsElem` member methods:**

Method | Response Description
---|---
getType | Set: TIMGroupTipsType.SetAdmin<br>Cancelled: TIMGroupTipsType.CancelAdmin
getOpUser | The identifier of the operator
getGroupName | Group name
getUserList | List of users who are set or canceled as admins

### Group profile modifications

**Trigger:** when group profile information, such as the group name and group introduction, is modified, the system sends a message. You can update the related display fields, or selectively display the message to users.

**Description of the responses of `TIMGroupTipsElem` member methods:**

Method | Response Description
---|---
getType | TIMGroupTipsType.ModifyGroupInfo
getOpUser | The identifier of the operator
getGroupName | Group name
getGroupInfoList | The modified group profile information. It is a TIMGroupTipsElemGroupInfo structure list.

**`TIMGroupTipsElemGroupInfo` prototype:**

```
// Get the message content
java.lang.String    getContent()

//Get the type of the group profile modification message
TIMGroupTipsGroupInfoType   getType()
```

**`TIMGroupTipsGroupInfoType` prototype:**
```
//Modify profile photo URL
ModifyFaceUrl

//Modify group introduction
ModifyIntroduction

//Modify group name
ModifyName

//Modify group announcement
ModifyNotification

//Change group owner
ModifyOwner
```

### Group member profile modifications

**Trigger:** when a group member’s profile related to the group is modified, such as when the member has been muted or the member’s role in the group has changed, the system sends a message. You can update related display fields, or selectively display the message to users.

>
>- **The profile mentioned here includes only information related to the group, such as muting duration and member role change. Information related to the user, such as the user’s nickname, is not included**. For groups that have too many members, we recommend that you display the information in the message body instead of updating it in real time. For more information, see [Message sender and related profile](/doc/product/269/9232#.E6.B6.88.E6.81.AF.E5.8F.91.E9.80.81.E8.80.85.E5.8F.8A.E5.85.B6.E7.9B.B8.E5.85.B3.E8.B5.84.E6.96.99).
>- If the user profile is stored locally, you can determine whether a change has occurred according to the information in the message body and update the profile after receiving a message from this user.

**Description of the responses of `TIMGroupTipsElem` member methods:**

Method | Response Description
---|---
getType | TIMGroupTipsType.ModifyMemberInfo
getOpUser | The identifier of the operator
getGroupName | Group name
getMemberInfoList | The modified group member profile information. It is a TIMGroupTipsElemMemberInfo structure list.

**`TIMGroupTipsElemMemberInfo` prototype:**

```
//Get the identifier of the muted group member
java.lang.String    getIdentifier()

//Get muting duration
long    getShutupTime()
```

## Group System Messages

When a user applies to join a group, the group admin receives a system message on the application. The admin can accept or reject the application, and the corresponding group system message will be displayed to the user.

**Group system message types:**

```
//Application to join the group is approved (received only by the applicant)
TIM_GROUP_SYSTEM_ADD_GROUP_ACCEPT_TYPE

//Application to join the group is rejected (received only by the applicant)
TIM_GROUP_SYSTEM_ADD_GROUP_REFUSE_TYPE

//Apply to join the group (received only by the admin)
TIM_GROUP_SYSTEM_ADD_GROUP_REQUEST_TYPE

//Admin status canceled (received only by the canceled admin)
TIM_GROUP_SYSTEM_CANCEL_ADMIN_TYPE

//Group created (received only by the initial members)
TIM_GROUP_SYSTEM_CREATE_GROUP_TYPE

//Group disbanded (received by all members)
TIM_GROUP_SYSTEM_DELETE_GROUP_TYPE

//Group admin set (received by the new group admin)
TIM_GROUP_SYSTEM_GRANT_ADMIN_TYPE

//Invited to join the group (received by the invitee)
TIM_GROUP_SYSTEM_INVITED_TO_GROUP_TYPE

//Kicked out of the group by the admin (received by the user who is kicked out)
TIM_GROUP_SYSTEM_KICK_OFF_FROM_GROUP_TYPE

//Quit the group (received by the user who quits the group)
TIM_GROUP_SYSTEM_QUIT_GROUP_TYP

//Group is revoked (received by all members)
TIM_GROUP_SYSTEM_REVOKE_GROUP_TYPE

//Group invitation request (received by the invitee)
TIM_GROUP_SYSTEM_INVITE_TO_GROUP_REQUEST_TYPE

//Group invitation request approved (received only by the inviter)
TIM_GROUP_SYSTEM_INVITATION_ACCEPTED_TYPE

//Group invitation request rejected (only received by the inviter)
TIM_GROUP_SYSTEM_INVITATION_REFUSED_TYPE
```

**`TIMGroupSystemElem` member methods are defined as follows:**

```
/**
 *  Operator’s platform
 *  Valid values: iOS, Android, Windows, Mac, Web, RESTful API, Unknown
 * @return The platform of the operator
 */
public String getPlatform()

/**
 * Get the subtype of the message
 * @return The subtype of the group system message
 */
public TIMGroupSystemElemType getSubtype()

/**
 * Get group ID
 * @return
 */
public String getGroupId()

/**
 * Get operator
 * @return The operator’s identifier
 */
public String getOpUser()

/**
 * Get the reason for the operation
 * @return The reason for the operation
 */
public String getOpReason()

/**
 * Get custom notification
 * @return Custom notification
 */
public byte[] getUserData()

/**
 * Get operator’s user profile
 * @return Operator’s user profile
 */
public TIMUserProfile getOpUserInfo()

/**
 * Get operator’s profile in the group
 * @return Operator’s profile in the group
 */
public TIMGroupMemberInfo getOpGroupMemberInfo()
```

### User applies to join a group

**Trigger:** when a user applies to join a group, the group admin receives a message about the user applying to join the group. You can display the message to the user for the user to decide whether to accept the application. The message type is `TIM_GROUP_SYSTEM_ADD_GROUP_REQUEST_TYPE`.

**Description of the responses of TIMGroupSystemElem member methods:**

Method | Response Description
---|---
getSubtype | TIM_GROUP_SYSTEM_ADD_GROUP_REQUEST_TYPE
getGroupId | The ID of the target group of the application
getOpUser | The applicant
getOpReason | Reason for the application (optional)


### “Apply to join” request is approved/rejected

**Trigger:** when an admin approves an application to join the group, the applicant receives an approval notification message, and when the admin rejects the application, the applicant receives a rejection notification message.

**Description of the responses of `TIMGroupSystemElem` member methods:**

Method | Response Description
---|---
getSubtype | Approve: TIM_GROUP_SYSTEM_ADD_GROUP_ACCEPT_TYPE<br>Reject: TIM_GROUP_SYSTEM_ADD_GROUP_REFUSE_TYPE
getGroupId | The ID of the group for which the request is approved/rejected
getOpUser | The identifier of the admin who processed the request
getOpReason | Reason for approval or rejection (optional)

### “Invited to join” request

**Trigger:** when a user is invited to join a group (**the user is not a group member and needs to approve the invitation**), the user receives an invitation message.

> When a group is created, the initial members are added to the group without invitation.

**Description of the responses of `TIMGroupSystemElem` member methods:**

Method | Response Description
---|---
getSubtype | TIM_GROUP_SYSTEM_INVITE_TO_GROUP_REQUEST_TYPE
getGroupId | The ID of the group the user is invited to join
getOpUser | The operator, who is the inviter in this case


### “Invited to join” request is approved/rejected

**Trigger:** when the invitee approves the invitation, the inviter receives an approval notification method, and when the invitee rejects the invitation, the inviter receives a rejection notification message.

**Description of the responses of `TIMGroupSystemElem` member methods:**

Method | Response Description
---|---
getSubtype | Approve: TIM_GROUP_SYSTEM_INVITATION_ACCEPTED_TYPE<br>Reject: TIM_GROUP_SYSTEM_INVITATION_REFUSED_TYPE
getGroupId | The ID of the group for which the request is approved/rejected
getOpUser | The identifier of the admin who processed the request
getOpReason | Reason for approval or rejection (optional)


### Kicked out by admin

**Trigger:** when a user is kicked out of a group by the admin, the user receives a kicked out notification message.

**Description of the responses of `TIMGroupSystemElem` member methods:**

Method | Response Description
---|---
getSubtype | TIM_GROUP_SYSTEM_KICK_OFF_FROM_GROUP_TYPE
getGroupId | The ID of the group from which the user is kicked out
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

If a user calls the method to create a group and the success callback is returned, then the group was created successfully. This message serves the purpose of multi-client synchronization. When receiving this message, the other clients can update the group list, while the current client can choose to ignore it.

**Description of the responses of `TIMGroupSystemElem` member methods:**

Method | Response Description
---|---
getSubtype | TIM_GROUP_SYSTEM_CREATE_GROUP_TYPE
getGroupId | The ID of the group that is created
getOpUser | The creator, who is the user in this case

### “Invited to join” request

**Trigger:** when a user is invited to join a group (**the user has been added to the group at this time**), the user receives an invitation notification message.

> When a group is created, the initial members are added to the group without invitation.

**Description of the responses of `TIMGroupSystemElem` member methods:**

Method | Response Description
---|---
getSubtype | TIM_GROUP_SYSTEM_INVITED_TO_GROUP_TYPE
getGroupId | The ID of the group the user is invited to join
getOpUser | The operator, who is the inviter in this case

### Quit group

**Trigger:** when a user quits a group, the user receives a quit notification message, and only the user who quit will receive the message.

If a user calls `QuitGroup` and the success callback is returned, then the user has quit the group successfully. This message is used for multi-client synchronization. When receiving this message, the other clients can update the group list, while the current client can choose to ignore it.

**Description of the responses of `TIMGroupSystemElem` member methods:**

Method | Response Description
---|---
getSubtype | TIM_GROUP_SYSTEM_QUIT_GROUP_TYPE
getGroupId | The ID of the group that the user quits
getOpUser | The operator, who is the user in this case

### Admin is set/cancelled

**Trigger:** when a user is set or canceled as a group admin, the user receives a corresponding notification.

**Description of the responses of `TIMGroupSystemElem` member methods:**

Method | Response Description
---|---
getSubtype | Admin role is cancelled: TIM_GROUP_SYSTEM_GRANT_ADMIN_TYPE<br>Admin role is granted: TIM_GROUP_SYSTEM_CANCEL_ADMIN_TYPE
getGroupId | The ID of the group in which the event occurs
getOpUser | The operator

### Group is revoked

**Trigger:** when a group is revoked by the system, all members receive a message notifying that the group was revoked.

**Description of the responses of `TIMGroupSystemElem` member methods:**

Method | Response Description
---|---
getSubtype | TIM_GROUP_SYSTEM_REVOKE_GROUP_TYPE
getGroupId | The ID of the group that is revoked
