## Group Overview

Instant Messaging (IM) supports multiple group types. For more information on their characteristics and limits, see the [Group System](https://cloud.tencent.com/document/product/269/1502). A group is identified by a unique ID that enables different operations.

## Group Messages

Group messages and C2C (one-to-one) chat messages are the same except for the conversation type obtained through Conversation. For more information, see [Sending Messages](https://cloud.tencent.com/document/product/269/9232#.E6.B6.88.E6.81.AF.E5.8F.91.E9.80.81).

## Group Management

Group-related operations are performed after login through `TIMGroupManager`.

**Prototype for obtaining a singleton:**

```
/** Obtain an instance
 * @return TIMGroupManager Instance
 */
public static TIMGroupManager getInstance()

```

### Creating a group

IM has the following built-in group types: **private group (Private), public group (Public), chatroom (ChatRoom), audio-and-video chat room (AVChatRoom), and broadcasting chatroom (BChatRoom)**. For more information, see [Group Types](https://cloud.tencent.com/document/product/269/1502#.E7.BE.A4.E7.BB.84.E5.BD.A2.E6.80.81.E4.BB.8B.E7.BB.8D).

- **AVChatRoom:** it is also called a live-streaming group, which supports an unlimited number of members, but does not support features such as adding members or querying the total number of members.
- You can create groups through `createGroup` in `TIMGroupManager`. When creating a group, you can specify certain group information, such as the group type, name, introduction, list of group members, and even the group ID. The group ID is returned after the group is created and can be used to obtain Conversation to receive and send messages.

>You need to follow certain rules when defining group IDs. For more information, see [Custom Group IDs](https://cloud.tencent.com/document/product/269/1502#.E8.87.AA.E5.AE.9A.E4.B9.89.E7.BE.A4.E7.BB.84-id).

**Prototype:**

```
/**
 * Create a group
 * @param param Information set that is required for creating a group. See {@see CreateGroupParam} for details.
 * @param cb Callback. The parameter of the OnSuccess function returns the ID of the created group.
 */
public void createGroup(@NonNull CreateGroupParam param, @NonNull TIMValueCallBack<String> cb)
```

**`TIMGroupManager.CreateGroupParam` provides the following APIs:**
```
/**
 * Create a constructor of group parameters
 * @param type Group type. Currently supported group types are Private, Public,
 * ChatRoom, AVChatRoom, and BChatRoom.
 * @param name Group name
 */
public CreateGroupParam(@NonNull String type, @NonNull String name)

/**
 * Set the ID for the group to be created
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
 * @param introduction Group introduction
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
 * Set custom information for the group to be created
 * @param key Key of custom information, whose length is up to 16 bytes
 * @param value Value of custom information, whose length is up to 512 bytes
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
//Specify the group introduction
param.setIntroduction("hello world");
//Specify the group announcement
param.setNotification("welcome to our group");

//Add group members
List<TIMGroupMemberInfo> infos = new ArrayList<TIMGroupMemberInfo>();
TIMGroupMemberInfo member = new TIMGroupMemberInfo("cat");
infos.add(member);
param.setMembers(infos);

//Set the group custom field (configure the corresponding key in the console first)
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

For more information, see [Differences in Group Member Operations](https://cloud.tencent.com/document/product/269/1502#.E7.BE.A4.E6.88.90.E5.91.98.E6.93.8D.E4.BD.9C.E5.B7.AE.E5.BC.82). 

**Prototype:**

```
/**
 * Invite users to a group
 * @param groupId Group ID
 * @param memList List of the IDs of the users to be added to the group
 * @param cb Callback. The parameter of the OnSuccess function returns the accounts of users who have been added to the group.
 */
public void inviteGroupMember(@NonNull String groupId, @NonNull List<String> memList,
							  @NonNull TIMValueCallBack<List<TIMGroupMemberResult>> cb)
```

**`TIMGroupMemberResult` is defined as follows:**

```
/**
 * Obtain the operation result
 * @return Operation result: 0: failed. 1: succeeded. 2: the user is already a group member when added, or the user is not a group member when deleted.
 */
public long getResult()

/**
 * Obtain the user account
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
    public void onSuccess(List<TIMGroupMemberResult> results) { //Group member operation result
        for(TIMGroupMemberResult r : results) {
            Log.d(tag, "result: " + r.getResult()  //Operation result: 0: failed to add. 1: added successfully. 2: the target user is already a group member.
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

`applyJoinGroup` of `TIMGroupManager` allows users to apply to join a group. This operation is valid only for Public and ChatRoom groups.

**Permission description:**

For more information, see [Differences in Group Member Operations](https://cloud.tencent.com/document/product/269/1502#.E7.BE.A4.E6.88.90.E5.91.98.E6.93.8D.E4.BD.9C.E5.B7.AE.E5.BC.82).

**Prototype:**

```
/**
 * Join a group
 * @param groupId Group ID
 * @param reason Application reason (optional)
 * @param cb Callback
 */
public void applyJoinGroup(@NonNull String groupId, String reason, @NonNull TIMCallBack cb)
```

In the following example, a user applies to join group "@TGS#1JYSZEAEQ", and the reason for the application is "some reason". **Example:**

```
TIMGroupManager.getInstance().applyJoinGroup("@TGS#1JYSZEAEQ", "some reason", new TIMCallBack() {
    @java.lang.Override
    public void onError(int code, String desc) {
        //The API returns "code" (error code) and "desc" (error description), which can be used as the cause.
        //For the list of error codes, see the error code table.
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

- **Private:** any member can quit the group.
- **Public, ChatRoom, and AVChatRoom:** the group owner cannot quit the group.

For more information, see [Differences in Group Member Operations](https://cloud.tencent.com/document/product/269/1502#.E7.BE.A4.E6.88.90.E5.91.98.E6.93.8D.E4.BD.9C.E5.B7.AE.E5.BC.82).

**Prototype:**

```
/**
 * Quit the group
 * @param groupId Group ID
 * @param cb Callback
 */
public void quitGroup(@NonNull String groupId, @NonNull TIMCallBack cb)
```

**Example:**

```
//Create a callback
TIMCallBack cb = new TIMCallBack() {
    @Override
    public void onError(int code, String desc) {
            //"code" (error code) and "desc" (error description) can be used to locate the cause of the request failure.
            //For the meaning of the error code, see the error code table.
    }

    @Override
    public void onSuccess() {
        Log.e(tag, "quit group succ");
    }
};

//Quit the group
TIMGroupManager.getInstance().quitGroup(
        groupId,  //Group ID
        cb);      //Callback
```

### Deleting group members

This function’s parameters are the same as those of joining a group. The API for deleting group members is provided by `TIMGroupManager`.

**Permission description:**
For more information, see [Differences in Group Member Operations](https://cloud.tencent.com/document/product/269/1502#.E7.BE.A4.E6.88.90.E5.91.98.E6.93.8D.E4.BD.9C.E5.B7.AE.E5.BC.82).

**Prototype:**

```
/**
 * Delete group members
 * @param param Parameter for deleting group members
 * @param cb Callback. The parameter of the OnSuccess function returns the list of deleted group members.
 */
public void deleteGroupMember(@NonNull DeleteMemberParam param,
							  @NonNull TIMValueCallBack<List<TIMGroupMemberResult>> cb)
```

**`DeleteMemberParam` provides the following APIs:**
```
/**
 * Construct parameters
 * @param groupId Group ID
 * @param members List of user IDs
 */
public DeleteMemberParam(@NonNull String groupId, @NonNull List<String> members)

/**
 * Set the reason for deleting the group members (optional)
 * @param reason Deletion reason
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
	public void onSuccess(List<TIMGroupMemberResult> results) { //Group member operation result
		for(TIMGroupMemberResult r : results) {
			Log.d(tag, "result: " + r.getResult()  //Operation result. 0: failed to delete. 1: deleted successfully. 2: the target user is not a group member.
					+ " user: " + r.getUser());    //User account
		}
	}
});
```

### Obtaining the list of group members

The API for obtaining the list of group members is `getGroupMembers`. Built-in fields and custom fields are pulled by default. Go to the [IM console](https://console.cloud.tencent.com/im) and navigate to **Feature Configuration** > **Group Member Custom Fields** to configure the keys and permissions for custom fields, which take effect after 5 minutes.

**Permission description:**

- **Any type of group:** the member list can be obtained.
- **Live-streaming group:** the member list only contains the group owner, admin, and some members.

For more information, see [Differences in Group Operations](https://cloud.tencent.com/document/product/269/1502#.E7.BE.A4.E7.BB.84.E6.93.8D.E4.BD.9C.E5.B7.AE.E5.BC.82). 

**Prototype:**

```
/**
 * Obtain the group member list
 * @param groupId Group ID
 * @param cb Callback. The parameter of the OnSuccess function returns the list of group members.
 */
public void getGroupMembers(@NonNull String groupId, @NonNull TIMValueCallBack<List<TIMGroupMemberInfo>> cb)
```

**Example:**

```
//Create a callback
TIMValueCallBack<List<TIMGroupMemberInfo>> cb = new TIMValueCallBack<List<TIMGroupMemberInfo>> () {
    @Override
    public void onError(int code, String desc) {
    }

    @Override
    public void onSuccess(List<TIMGroupMemberInfo> infoList) {//The parameter returns group member information.

        for(TIMGroupMemberInfo info : infoList) {
            Log.d(tag, "user: " + info.getUser() +
            "join time: " + info.getJoinTime() +
            "role: " + info.getRole());
        }
    }
};

//Obtain group member information
TIMGroupManager.getInstance().getGroupMembers(
        groupId, //Group ID
        cb);     //Callback
```

### Obtaining the list of groups the user has joined

You can obtain the list of groups that the current user has joined through `TIMGroupManager`. The returned information contains only part of the basic information. To obtain detailed group information, see [Obtaining Group Information by Group Members](https://cloud.tencent.com/document/product/269/9236#.E8.8E.B7.E5.8F.96.E7.BE.A4.E7.BB.84.E8.B5.84.E6.96.992).

**Permission description:**

- **Private, Public, and ChatRoom:** this API allows you to obtain the information of Public, ChatRoom, and active Private groups that the user has joined.
- **AVChatRoom and BChatRoom:** both types of groups cannot be obtained through this API due to the differences in internal implementation.

**Prototype:**

```
/**
 * Obtain the list of groups the user has joined
 * @param cb Callback. The parameter of the OnSuccess function returns the groups that the user has joined.
 */
public void getGroupList(@NonNull TIMValueCallBack<List<TIMGroupBaseInfo>> cb)
```

**`TIMGroupBaseInfo` provides the following methods:**
```
/**
 * Obtain the group ID
 * @return Group ID
 */
public String getGroupId()

/**
 * Obtain the group name
 * @return Group name
 */
public String getGroupName()

/**
 * Obtain the group type
 * @return Group type
 */
public String getGroupType()

/**
 * Obtain the group profile photo URL
 * @return Group profile photo URL
 */
public String getFaceUrl()

/**
 * Check whether Mute All is set for the current group or not
 * @return true - Mute All has been set
 * @since 3.1.1
 */
public boolean isSilenceAll()
```

**Example:**

```
//Create a callback
TIMValueCallBack<List<TIMGroupBaseInfo>> cb = new TIMValueCallBack<List<TIMGroupBaseInfo>>() {
    @Override
    public void onError(int code, String desc) {
        //"code" (error code) and "desc" (error description) can be used to locate the cause of the request failure.
        //For the meaning of the error code, see the error code table.
        Log.e(tag, "get gruop list failed: " + code + " desc");
    }

    @Override
    public void onSuccess(List<TIMGroupBaseInfo> timGroupInfos) {//The parameter returns the basic information of each group.
        Log.d(tag, "get gruop list succ");

        for(TIMGroupBaseInfo info : timGroupInfos) {
            Log.d(tag, "group id: " + info.getGroupId() +
            " group name: " + info.getGroupName() +
            " group type: " + info.getGroupType());
        }
    }
};

//Obtain the list of groups the user has joined
TIMGroupManager.getInstance().getGroupList(cb);
```

### Dismissing a group

 The API for dismissing groups is provided by `TIMGroupManager`.

**Permission description:**
For more information, see [Differences in Group Operations](https://cloud.tencent.com/document/product/269/1502#.E7.BE.A4.E7.BB.84.E6.93.8D.E4.BD.9C.E5.B7.AE.E5.BC.82). 

**Prototype:**

```
/**
 * Delete a group
 * @param groupId Group ID
 * @param cb Callback
 */
public void deleteGroup(@NonNull String groupId, @NonNull TIMCallBack cb)
```

**Example:**

```
//Dismiss a group
TIMGroupManager.getInstance().deleteGroup(groupId, new TIMCallBack() {
    @Override
    public void onError(int code, String desc) {

        //"code" (error code) and "desc" (error description) can be used to locate the cause of the request failure.
        //For the list of error codes, see the error code table.
        Log.d(tag, "login failed. code: " + code + " errmsg: " + desc);
    }

    @Override
    public void onSuccess() {
        //Dismissed the group successfully
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
 * Change the group owner
 * @param groupId Group ID
 * @param identifier Identifier of the new group owner
 * @param cb Callback
 */
public void modifyGroupOwner(@NonNull String groupId, @NonNull String identifier, @NonNull TIMCallBack cb)
```

### Other APIs

**The API for obtaining specified types of members (to pull group admins, group owners, and group members respectively) is defined as follows:**

```
/**
 * Obtain the group member list according to filter conditions (the list can be pulled by field and in pages)
 * @param groupId Group ID
 * @param flags Flag of information to be pulled, such as {@see TIMGroupManager#TIM_GET_GROUP_MEM_INFO_FLAG_NAME_CARD} or any combination of them
 * @param filter Role filter. See {@see TIMGroupMemberRoleFilter} for more information
 * @param custom List of custom keys to be obtained
 * @param nextSeq Flag for pagination pulling. Enter 0 for the first request. If the success callback returns a non-zero value, the list will be pulled in pages. In this case, pass in this parameter to pull again until the value becomes 0.
 * @param cb Callback
 */
public void getGroupMembersByFilter(@NonNull String groupId, long flags, @NonNull TIMGroupMemberRoleFilter filter,
									List<String> custom, long nextSeq, TIMValueCallBack<TIMGroupMemberSucc> cb)
```

## Obtaining Group Information

### Obtaining group information

You can use the `getGroupInfo` method provided by `TIMGroupManager` to obtain group information stored on the server and use the `queryGroupInfo` method to pull the locally cached group information. Group members can pull group information. Non-members cannot pull Private groups’ information and can only pull public fields of other types of groups, that are, `groupId\groupName\groupOwner\groupType\createTime\memberNum\maxMemberNum\onlineMemberNum\groupIntroduction\groupFaceUrl\addOption\custom`.

**Note:**

Basic information and custom fields are pulled by default. To configure keys and permissions for custom fields, go to the [IM console](https://console.cloud.tencent.com/im) and navigate to **Feature Configuration** > **Group Custom Fields**, which take effect after 5 minutes.

**Prototype:**

```
/**
 * Obtain the group information stored on the server
 * @param groupIdList List of groups whose detailed information is to be pulled. Up to 50 groups can be pulled at a time.
 * @param cb Callback. The parameter of the OnSuccess function returns the list of group information {@see TIMGroupDetailInfo}.
 */
public void getGroupInfo(@NonNull List<String> groupIdList,
							   @NonNull TIMValueCallBack<List<TIMGroupDetailInfo>> cb)
/**
 * Obtain the locally stored group information
 * @param groupId IDs of the groups whose detailed information is to be pulled
 * @return Group information. Null is returned if the group information is not stored locally.
 */
 public TIMGroupDetailInfo queryGroupInfo(@NonNull String groupId)
```

**`TIMGroupDetailInfo` is defined as follows:**
```
/**
 * Obtain the group ID
 * @return Group ID
 */
public String getGroupId()

/**
 * Obtain the group name
 * @return Group name
 */
public String getGroupName()

/**
 * Obtain the group creator account
 * @return Group creator account
 */
public String getGroupOwner()

/**
 * Obtain the group creation time
 * @return Group creation time
 */
public long getCreateTime()

/**
 * Obtain the last modification time of group information
 * @return Last modification time of group information
 */
public long getLastInfoTime()

/**
 * Obtain the time of the last group message
 * @return Time of the last group message
 */
public long getLastMsgTime()

/**
 * Obtain the number of group members
 * @return Number of group members
 */
public long getMemberNum()

/**
 * Supported maximum number of group members
 * @return Maximum number of group members
 */
public long getMaxMemberNum()

/**
 * Obtain the group introduction
 * @return Group introduction
 */
public String getGroupIntroduction()

/**
 * Obtain the group announcement
 * @return Group announcement
 */
public String getGroupNotification()

/**
 * Obtain the group profile photo URL
 * @return Group profile photo URL
 */
public String getFaceUrl()

/**
 * Obtain the group type
 * @return Group type
 */
public String getGroupType()

/**
 * Obtain the option for joining the group
 * @return Option for joining the group
 */
public TIMGroupAddOpt getGroupAddOpt()

/**
 * Obtain the last message in the group
 * @return Last message in the group
 */
public TIMMessage getLastMsg()

/**
 * Obtain the group custom field map
 * @return Group custom field map
 */
public Map<String, byte[]> getCustom()

/**
 * Obtain the number of online group members. To receive valid returned values after enabling this feature, submit a ticket. You cannot apply to enable this feature for AVChatRoom groups.
 * @return Number of online group members
 */
public long getOnlineMemberNum()

/**
 * Check whether Mute All is set for this group or not
 * @return true - Mute All has been set for the group
 * @since 3.1.1
 */
public boolean isSilenceAll()
```

**Example:**

```
//Create a list of group IDs for which you want to obtain information
ArrayList<String> groupList = new ArrayList<String>();

//Create a callback
TIMValueCallBack<List<TIMGroupDetailInfo>> cb = new TIMValueCallBack<List<TIMGroupDetailInfo>>() {
    @Override
    public void onError(int code, String desc) {
            //"code" (error code) and "desc" (error description) can be used to locate the cause of the request failure.
            //For the list of error codes, see the error code table.
    }

    @Override
    public void onSuccess(List<TIMGroupDetailInfo> infoList) { //The parameter returns the list of group information.
        for(TIMGroupDetailInfo info : infoList) {
            Log.d(tag, "groupId: " + info.getGroupId()           //Group ID
            + " group name: " + info.getGroupName()              //Group name
            + " group owner: " + info.getGroupOwner()            //Group creator account
            + " group create time: " + info.getCreateTime()      //Group creation time
            + " group last info time: " + info.getLastInfoTime() //Last modification time of group information
            + " group last msg time: " + info.getLastMsgTime()  //Time of the last group message
            + " group member num: " + info.getMemberNum());      //Number of group members
        }
    }
};

//Add a group ID
String groupId = "TGID1EDABEAEO";
groupList.add(groupId);

//Obtain group information stored on the server
TIMGroupManager.getInstance().getGroupInfo(
        groupList, //List of group IDs for which you want to obtain information
        cb);       //Callback

* Obtain the locally cached group information
TIMGroupDetailInfo timGroupDetailInfo = TIMGroupManager.getInstance().queryGroupInfo(groupId);
```

### Obtaining your own profile in a group

You can obtain your own profile in a group when the list of groups that you have joined is pulled. See [Getting group list](#.E8.8E.B7.E5.8F.96.E5.8A.A0.E5.85.A5.E7.9A.84.E7.BE.A4.E7.BB.84.E5.88.97.E8.A1.A8) for more information. To obtain your profile in a single group, use `getSelfInfo` of `TIMGroupManager`, as shown below. If the app needs to obtain a group list, we recommend that you obtain your profile in a group when obtaining the group list instead of calling the following API.

**Permission description:**

**Live-streaming groups** do not support obtaining your own profile in a group.

**Prototype:**

```
/**
 * Obtain your own information in a group
 * @param groupId Group ID
 * @param cb Callback. The parameter of the OnSuccess function returns your own profile.
 */
public void getSelfInfo(@NonNull String groupId, @NonNull TIMValueCallBack<TIMGroupSelfInfo> cb)
```

### Obtaining the profiles of specified group members

The API for obtaining group member profiles is provided by `TIMGroupManager`. In this case, basic information is pulled by default.

**Permission description:**

For a **live-streaming group**, only the profiles of certain members can be pulled, including the group owner, admin, and some members.

**Prototype:**
```
/**
 * Obtain the profiles of specified members in a group
 @param groupId ID of the target group
 * @param identifiers Identifiers of specified group members, which count up to 100 for each request
 * @param cb Callback. The parameter of the OnSuccess function returns the group member list.
 */
public void getGroupMembersInfo(@NonNull String groupId, @NonNull List<String> identifiers,
								@NonNull TIMValueCallBack<List<TIMGroupMemberInfo>> cb)
```


## Modifying Group Information

The API for modifying group profile is provided by `TIMGroupManager`. It allows you to modify information such as the group name, introduction, and announcement.

**Prototype:**

```
/**
 * Modify group basic information
 * @param param Parameter class
 * @param cb Callback
 */
public void modifyGroupInfo(@NonNull ModifyGroupInfoParam param, @NonNull TIMCallBack cb)
```

**`TIMGroupManager.ModifyGroupInfoParam` provides the following APIs:**

```
/**
 * Construct a parameter instance
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
 * @param maxMemberNum Maximum number of group members
 */
public ModifyGroupInfoParam setMaxMemberNum(long maxMemberNum)

/**
 * Set whether group members are visible to users outside the group
 * @param visable Whether group members are visible to users outside the group
 */
public ModifyGroupInfoParam setVisable(boolean visable)

/**
 * Set the group custom field
 * @param customInfos Group custom field dictionary
 */
public ModifyGroupInfoParam setCustomInfo(@NonNull Map<String, byte[]> customInfos)

/**
 * Set Mute All for the group
 * @param silenceAll true: mute all. false: unmute all.
 * @since 3.1.1
 */
public ModifyGroupInfoParam setSilenceAll(boolean silenceAll)
```

### Modifying the group name

**Permission description:**

- **Public, ChatRoom, and BChatRoom:** only the group owner or admin can modify the group name.
- **Private:** any member can modify the group name.

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

- **Public, ChatRoom, and BChatRoom:** only the group owner or admin can modify the group introduction.
- **Private:** any member can modify the group introduction.

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

- **Public, ChatRoom, and BChatRoom:** only the group owner or admin can modify the group announcement.
- **Private:** any member can modify the group announcement.

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

- **Public, ChatRoom, and BChatRoom:** only the group owner or admin can modify the group profile photo.
- **Private:** any member can modify the group profile photo.


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

- **Public, ChatRoom, and BChatRoom:** only the group owner or admin can modify the option for joining the group.
- **Private:** users can join the group only through invitation, and user application is not supported.

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

The API for modifying group member profiles is provided by `TIMGroupManager`. It allows you to modify group members’ roles and name cards and mute group members.

**Prototype:**

```
/**
 * Modify a group member’s profile
 * @param param Parameter for modifying a group member’s profile
 * @param cb Callback
 */
public void modifyMemberInfo(@NonNull ModifyMemberInfoParam param, @NonNull TIMCallBack cb)
```

**`TIMGroupManager.ModifyMemberInfoParam` provides the following APIs:**

```
/**
 * Construct a parameter for modifying group member profiles
 * @param groupId Group ID of the group member whose profile is to be modified
 * @param identifier User ID of the group member whose profile is to be modified
 */
public ModifyMemberInfoParam(@NonNull String groupId, @NonNull String identifier)

/**
 * Modify a group member’s name card
 * @param nameCard Group name card
 */
public ModifyMemberInfoParam setNameCard(@NonNull String nameCard)

/**
 * Modify the option for receiving group messages
 * @param receiveMessageOpt Option for receiving group messages. See {@see TIMGroupReceiveMessageOpt} for more information.
 */
public ModifyMemberInfoParam setReceiveMessageOpt(@NonNull TIMGroupReceiveMessageOpt receiveMessageOpt)

/**
 * Modify a group member’s role (only the group owner and admin can do so)
 * @param roleType Type of the role, which cannot be changed to the group owner. See {@see TIMGroupMemberRoleType} for details.
 */
public ModifyMemberInfoParam setRoleType(TIMGroupMemberRoleType roleType)

/**
 * Set the muting period (only the group owner and admin can do so)
 * @param silence Muting period
 */
public ModifyMemberInfoParam setSilence(long silence)

/**
 * Set the group custom field
 * @param customInfo Group custom field dictionary
 */
public ModifyMemberInfoParam setCustomInfo(Map<String, byte[]> customInfo)
```

### Modifying a member’s role in a group

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

You can mute group members and set the muting period through `modifyMemberInfoParam.setSilence()`.

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

- **Public and Private:** the default option is to receive and push group messages offline.
- **ChatRoom and AVChatRoom:** the default option is to receive but not push group messages offline.

**`TIMGroupReceiveMessageOpt` provides the following APIs:**

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

Group pending requests are group-related operations that require approval, such as pending "apply to join" requests and pending "invited to join" requests. Group pending information is represented by the `TIMGroupPendencyItem` class.

**The member methods of `TIMGroupPendencyItem` are as follows:**
```
/**
 * Obtain the group ID
 * @return Group ID
 */
public String getGroupId()

/**
 * Obtain the identifier of the requester, who is the requester for "apply to join" requests and the inviter for "invited to join" requests.
 * @return Requester’s identifier
 */
public String getFromUser()

/**
 * Obtain the identifier of the handler. The identifier is 0 if it is an "apply to join" request and the inviter if it is an "invited to join" request.
 * @return Handler’s identifier
 */
public String getToUser()

/**
 * Obtain the addition time of the group pending request
 * @return Addition time of the group pending request
 */
public long getAddTime()

/**
 * Obtain the type of the group pending request
 * @return Type of the group pending request. See TIMGroupPendencyGetType for details.
 */
public TIMGroupPendencyGetType getPendencyType()

/**
 * Obtain the processing state of the group pending request
 * @return Processing state of the group pending request. See {@see TIMGroupPendencyHandledStatus} for details.
 */
public TIMGroupPendencyHandledStatus getHandledStatus()

/**
 * Obtain the processing type of the group pending request. This is valid only when the processing state is not {@see TIMGroupPendencyHandledStatus#NOT_HANDLED}.
 * @return Processing type of the group pending request. See {@see TIMGroupPendencyOperationType} for details.
 */
public TIMGroupPendencyOperationType getOperationType()

/**
 * Obtain the additional information added by the requester
 * @return Additional information added by the requester
 */
public String getRequestMsg()

/**
 * Obtain the custom information added by the requester
 * @return Custom information added by the requester
 */
private String getRequestUserData()

/**
 * Obtain the additional information added by the handler. This is valid only when the processing state is not {@see TIMGroupPendencyHandledStatus#NOT_HANDLED}.
 * @return Additional information added by the handler
 */
public String getHandledMsg()

/**
 * Obtain the custom information added by the handler. This is valid only when the processing state is not {@see TIMGroupPendencyHandledStatus#NOT_HANDLED}.
 * @return Custom information added by the handler
 */
private String getHandledUserData()

/**
 * Approve the request. This is valid only for "apply to join" and "invited to join" messages.
 *
 * @param msg Reason for approval (optional)
 * @param cb Callback
 */
public void accept(String msg, TIMCallBack cb)

/**
 * Reject the request. This is valid only for "apply to join" and "invited to join" messages.
 *
 * @param msg Reason for rejection (optional)
 * @param cb Callback
 */
public void refuse(String msg, TIMCallBack cb)
```

### Pulling a list of group pending requests

You can pull information related to group pending requests through the `getGroupPendencyList` API of `TIMGroupManager`. A message can be pulled through this API even after it has been approved or rejected. In this case, the pulled message has a "processed" flag.

**Permission description:**

**Only the approver** has the permission to pull the information.

>For example:
>- If user A applies to join group A, the group admin can obtain information related to this pending request. As user A does not have the approval permission, user A does not need to obtain information related to this pending request.
>- If admin A invites user A to group A, user A can obtain the information related to this pending request because this pending request needs to be approved by user A.

**Prototype:**

```
/**
 * Obtain group pending requests in pages
 * @param param Parameter for obtaining the list of group pending requests. See {@see TIMGroupPendencyGetParam} for details.
 * @param cb Callback. The parameter of onSuccess returns the list of group pending requests and metadata. See {@see TIMGroupPendencyMeta} and {@see TIMGroupPendencyItem} for details.
 */
public void getGroupPendencyList(@NonNull TIMGroupPendencyGetParam param,
								 @NonNull TIMValueCallBack<TIMGroupPendencyListGetSucc> cb)
```

**`TIMGroupPendencyGetParam` is defined as follows:**

```
/**
 * Set the paging timestamp. Enter 0 for the first request. For subsequent requests, enter a value according to the timestamps in {@see TIMGroupPendencyMeta} returned by the server.
 * @param timestamp Paging timestamp
 */
public void setTimestamp(long timestamp)

/**
 * Set the number of requests per page (this is a suggested value that does not indicate completion, and the server can return more or less requests.)
 * @param numPerPage Number of requests per page
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
        //as the parameter in TIMGroupPendencyGetParam for obtaining the next page of data.
        TIMGroupPendencyMeta meta = timGroupPendencyListGetSucc.getPendencyMeta();
        Log.d(tag, meta.getNextStartTimestamp()
                + "|" + meta.getReportedTimestamp() + "|" + meta.getUnReadCount());

        List<TIMGroupPendencyItem> pendencyItems = timGroupPendencyListGetSucc.getPendencies();
        for(TIMGroupPendencyItem item : pendencyItems){
            //Handle group pending requests, such as view, approve, or reject a request.
        }
    }
});
```

### Reporting that group pending requests are read

Report that the current pending request and all the pending requests before it have been read through `reportGroupPendency` of `TIMGroupManager`. After the reporting, you can still pull these pending requests and determine whether they are read through the read timestamp.

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

Obtain a list of group pending requests (`TIMGroupPendencyItem`) through `getGroupPendencyList` and process the requests through the `accept/refuse` API in the `TIMGroupPendencyItem` class. Requests that have been processed cannot be processed again.

**Prototype:**

```
/**
 * Approve the request. This is valid only for "apply to join" and "invited to join" messages.
 *
 * @param msg Reason for approval (optional)
 * @param cb Callback
 */
public void accept(String msg, TIMCallBack cb)

/**
 * Reject the request. This is valid only for "apply to join" and "invited to join" messages.
 *
 * @param msg Reason for rejection (optional)
 * @param cb Callback
 */
public void refuse(String msg, TIMCallBack cb)
```

## Group Event Messages

When a user is invited to a group or is removed from a group, a prompt message is displayed in the group. The caller can choose to display the prompt message or ignore it. A prompt message is identified by a special `Elem` and returned by the new message callback (see [New Message Notifications](/doc/product/269/9229#.E6.96.B0.E6.B6.88.E6.81.AF.E9.80.9A.E7.9F.A5)). To obtain group event messages, in addition to relying on new message notifications, you can also set group event listeners to monitor different events through `setGroupEventListener` of `TIMUserConfig` **before login** (see [Initialization (Android)](https://cloud.tencent.com/document/product/269/9229#.E7.94.A8.E6.88.B7.E9.85.8D.E7.BD.AE)).

> The group event messages of ChatRoom and AVChatRoom groups are not delivered by new message notifications. Therefore, you must register group event listeners to monitor different group events.

The following figure shows an event message for group name modification.
![](https://main.qcloudimg.com/raw/78865ba68ed75700137e5afbd2ac3e43.jpg)


**`TIMGroupTipsElem` member methods:**

```
//Obtain the list of messages for group information modifications. This is valid only when the value of tipsType is TIMGroupTipsType.ModifyGroupInfo.
java.util.List<TIMGroupTipsElemGroupInfo> getGroupInfoList()

//Obtain the group name
java.lang.String    getGroupName()

//Obtain the list of messages for group member modifications. This is valid only when the value of tipsType is TIMGroupTipsType.ModifyMemberInfo.
java.util.List<TIMGroupTipsElemMemberInfo>    getMemberInfoList()

//Obtain the operator
java.lang.String    getOpUser()

//Obtain the type of the group event notification
TIMGroupTipsType    getTipsType()

//Obtain the list of accounts to be operated
java.util.List<java.lang.String>  getUserList()
```

**`TIMGroupTipsType` prototype:**

```
//Cancel an admin
CancelAdmin

//Join a group
Join

//Remove a group member
Kick

//Modify group information
ModifyGroupInfo

//Modify member information
ModifyMemberInfo

//Quit a group
Quit

//Set an admin
SetAdmin
```

### Notifications for a user joining the group

**Trigger:** when a user joins a group through application or invitation, the system sends a message in the group. The developer can choose a display style and update the group member list. The type of the received message is `TIMGroupTipsType.Join`.

**Description of the responses of `TIMGroupTipsElem` member methods:**

Method | Response Description
---|---
getType | TIMGroupTipsType.Join
getOpUser | Apply to join: the applicant</br>Invited to join: the inviter
getGroupName | Group name
getUserList | List of users that are added to the group

### Quitting a group by a user

**Trigger:** when a user quits a group, the system sends a notification in the group. You can choose to update the group member list. The type of the received message is `TIMGroupTipsType.Quit`.

**Description of the responses of `TIMGroupTipsElem` member methods:**

Method | Response Description
---|---
getType | TIMGroupTipsType.Quit
getOpUser | Identifier of the user who quits the group
getGroupName | Group name

### Removing a user from a group

**Trigger:** when a user is removed from a group, the system sends a notification in the group. You can choose to update the group member list. The type of the received message is `TIMGroupTipsType.Kick`.

**Description of the responses of `TIMGroupTipsElem` member methods:**

Method | Response Description
---|---
getType | TIMGroupTipsType.Kick
getOpUser | Identifier of the user who removes members
getGroupName | Group name
getUserList | List of removed users

### Setting or canceling an admin

**Trigger:** when a user is set or canceled as an admin, the system sends a notification in the group. If the UI shows whether a user is an admin, you can update the admin flag. The message types are `TIMGroupTipsType.SetAdmin` and `TIMGroupTipsType.CancelAdmin`.

**Description of the responses of `TIMGroupTipsElem` member methods:**

Method | Response Description
---|---
getType | Set: TIMGroupTipsType.SetAdmin<br>Canceled: TIMGroupTipsType.CancelAdmin
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
//Get message content
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
>- **The profile mentioned here includes only information related to the group, such as muting duration and member role change. Information related to the user, such as the user’s nickname is not included**. For groups that have too many members, we recommend that you display the information in the message body instead of updating it in real time. For more information, see [Message sender and related profile](/doc/product/269/9232#.E6.B6.88.E6.81.AF.E5.8F.91.E9.80.81.E8.80.85.E5.8F.8A.E5.85.B6.E7.9B.B8.E5.85.B3.E8.B5.84.E6.96.99).
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

When a user applies to join a group, the group admin receives a system message about the application. The admin can accept or reject the application, and the corresponding group system message will be displayed to the user.

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

//Group invitation request is rejected (received only by the inviter)
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
getGroupId | The ID of the group for which the request is approved or rejected
getOpUser | The identifier of the admin who processed the request
getOpReason | Reason for approval or rejection (optional)

### “Invited to join” request

**Trigger:** when a user is invited to join a group (**the user is not a group member and needs to approve the invitation**), the user receives an invitation message.

>When a group is created, the initial members are added to the group without invitation.

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
getGroupId | The ID of the group for which the request is approved or rejected
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

**Trigger:** when a group is created, the creator receives a creation notification method.

If a user calls the method to create a group and the success callback is returned, then the group was created successfully. This message serves the purpose of multi-client synchronization. When receiving this message, the other clients can update the group list, while the current client can choose to ignore it.

**Description of the responses of `TIMGroupSystemElem` member methods:**

Method | Response Description
---|---
getSubtype | TIM_GROUP_SYSTEM_CREATE_GROUP_TYPE
getGroupId | The ID of the group that is created
getOpUser | The creator, who is the user in this case

### “Invited to join” request

**Trigger:** when a user is invited to join a group (**the user has been added to the group at this time**), the user receives an inviation notification method.

>When a group is created, the initial members are added to the group without invitation.

**Description of the responses of `TIMGroupSystemElem` member methods:**

Method | Response Description
---|---
getSubtype | TIM_GROUP_SYSTEM_INVITED_TO_GROUP_TYPE
getGroupId | The ID of the group the user is invited to join
getOpUser | The operator, who is the inviter in this case

### Quit group

**Trigger:** when a user quits a group, the user receives a quit notification message, and only the user who quit will receive the message.

If a user calls `QuitGroup` and the success callback is returned, then the user has quit the group successfully. This message serves the purpose of multi-client synchronization. When receiving this message, the other clients can update the group list, while the current client can choose to ignore it.

**Description of the responses of `TIMGroupSystemElem` member methods:**

Method | Response Description
---|---
getSubtype | TIM_GROUP_SYSTEM_QUIT_GROUP_TYPE
getGroupId | The ID of the group that the user quits
getOpUser | The operator, who is the user in this case

### Admin is set/canceled

**Trigger:** when a user is set or canceled as a group admin, the user receives an event notification method.

**Description of the responses of `TIMGroupSystemElem` member methods:**

Method | Response Description
---|---
getSubtype | Admin role is canceled: TIM_GROUP_SYSTEM_GRANT_ADMIN_TYPE<br>Admin role is granted: TIM_GROUP_SYSTEM_CANCEL_ADMIN_TYPE
getGroupId | The ID of the group in which the event occurs
getOpUser | The operator

### Group is revoked

**Trigger:** when a group is revoked by the system, all members receive a message notifying that the group was revoked.

**Description of the responses of `TIMGroupSystemElem` member methods:**

Method | Response Description
---|---
getSubtype | TIM_GROUP_SYSTEM_REVOKE_GROUP_TYPE
getGroupId | The ID of the group that is revoked
