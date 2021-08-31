## Group Overview

Instant Messaging (IM) supports multiple group types. For more information on their characteristics and limits, see [Group System](https://intl.cloud.tencent.com/document/product/1047/33529). A group is identified by a unique ID that enables different operations.

## Group Messages

Group messages and C2C (one-to-one) messages are the same except for the conversation type obtained through Conversation. For more information, see [Sending Messages](https://intl.cloud.tencent.com/document/product/1047/36401).

## Group Management

Group-related operations are all implemented by `TIMGroupManager`. You must log in before performing such operations.

**Getting a singleton prototype:**

```
/** Getting an instance
 * @return TIMGroupManager instance
 */
public static TIMGroupManager getInstance()

```

### Creating a group

IM provides built-in group types including **private group (Private), public group (Public), chat room (ChatRoom), audio-video group (AVChatRoom), and broadcasting chat room (BChatRoom)**. For more information, see [Group Types](https://intl.cloud.tencent.com/document/product/1047/33529#GroupType).

- **Audio-video groups (AVChatRoom):** support an unlimited number of members but do not support features such as adding members or querying the total number of members.
- You can create a group by calling the `createGroup` API in `TIMGroupManager`. During creation, you can specify the group profile (such as the group type, group name, group introduction, list of members, and even the group ID). After the group is created, the group ID is returned, and you can use it to obtain Conversation for receiving and sending messages.

>! You need to follow certain rules when defining group IDs. For more information, see [Custom Group IDs](https://intl.cloud.tencent.com/document/product/1047/33529#.E8.87.AA.E5.AE.9A.E4.B9.89.E7.BE.A4.E7.BB.84-id).

**Prototype:**

```
/**
 * Create a group
 * @param param Creates the information set needed for the group. For more information, see {@see CreateGroupParam}
 * @param cb Callback. The group ID of the created group will be returned in a parameter of the OnSuccess function.
 */
public void createGroup(@NonNull CreateGroupParam param, @NonNull TIMValueCallBack<String> cb)
```

**`TIMGroupManager.CreateGroupParam` provides the following APIs:**
```
/**
 * Create a constructor for group parameters
 * @param type Group type, which currently supports private group (Private), public group (Public),
 *             chat room (ChatRoom), audio-video group (AVChatRoom), and broadcasting chat room (BChatRoom).
 * @param name Group name
 */
public CreateGroupParam(@NonNull String type, @NonNull String name)

/**
 * Set the group ID of the group to be created
 * @param groupId Group ID
 */
public CreateGroupParam setGroupId(String groupId)

/**
 * Set the group notice of the group to be created
 * @param notification Group notice
 */
public CreateGroupParam setNotification(String notification)

/**
 * Set the group introduction of the group to be created
 * @param introduction Group introduction
 */
public CreateGroupParam setIntroduction(String introduction)

/**
 * Set the group profile photo URL for the group to be created
 * @param url Group profile photo URL
 */
public CreateGroupParam setFaceUrl(String url)

/**
 * Set the group joining option for the group to be created
 * @param option Group joining option
 */
public CreateGroupParam setAddOption(TIMGroupAddOpt option)

/**
 * Set the maximum number of members allowed for the group to be created
 * @param maxMemberNum Maximum number of members
 */
public CreateGroupParam setMaxMemberNum(long maxMemberNum)

/**
 * Set the custom information of the group to be created
 * @param key Custom information key, with a maximum length of 16 bytes
 * @param value Custom information value, with a maximum length of 512 bytes
 */
public CreateGroupParam setCustomInfo(String key, byte[] value)

/**
 * Set the initial members of the group to be created
 * @param infos Information list of initial members
 */
public CreateGroupParam setMembers(List<TIMGroupMemberInfo> infos)
```

**Example:**
```
//Create a public group without specifying the group ID
TIMGroupManager.CreateGroupParam param = new TIMGroupManager.CreateGroupParam("Public", "test_group");
//Specify the group introduction
param.setIntroduction("hello world");
//Specify the group notice
param.setNotification("welcome to our group");

//Add group members
List<TIMGroupMemberInfo> infos = new ArrayList<TIMGroupMemberInfo>();
TIMGroupMemberInfo member = new TIMGroupMemberInfo("cat");
infos.add(member);
param.setMembers(infos);

//Set custom group fields. Before that, you need to configure the corresponding keys in the console.
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

The `inviteGroupMember` API of `TIMGroupManager` can be used to invite users to a group.

**Permission notes:**

For more information, see [Differences in Joining a Group](https://intl.cloud.tencent.com/document/product/1047/33529#.E5.8A.A0.E7.BE.A4.E6.96.B9.E5.BC.8F.E5.B7.AE.E5.BC.82). 

**Prototype:**

```
/**
 * Invite users to a group
 * @param groupId Group ID
 * @param memList List of IDs of the users to be added to the group
 * @param cb Callback. The user accounts successfully added to the group are returned in a parameter of the OnSuccess function.
 */
public void inviteGroupMember(@NonNull String groupId, @NonNull List<String> memList,
							  @NonNull TIMValueCallBack<List<TIMGroupMemberResult>> cb)
```

**`TIMGroupMemberResult` is defined as follows:**

```
/**
 * Get the operation result
 * @return Operation result: 0: failed. 1: successful. 2: the user was already a group member when added, or the user was not a group member when deleted.
 */
public long getResult()

/**
 * Get user accounts
 * @return User accounts
 */
public String getUser()
```


**Example:**

```
//Create a list of the users to be added to the group
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

//Add the listed users to the group
TIMGroupManager.getInstance().inviteGroupMember(
        groupId,   //Group ID
        list,      //List of the users to be added to the group
        cb);       //Callback
```

### Applying to join a group

The `applyJoinGroup` API of `TIMGroupManager` can be used to apply to join a group. This operation is valid only for public groups, chat rooms, and audio-video groups.

**Permission notes:**

For more information, see [Differences in Joining a Group](https://intl.cloud.tencent.com/document/product/1047/33529#.E5.8A.A0.E7.BE.A4.E6.96.B9.E5.BC.8F.E5.B7.AE.E5.BC.82).

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

In the following example, a user applies to join the group [@TGS#1JYSZEAEQ] for the reason of [some reason]. **Example:**

```
TIMGroupManager.getInstance().applyJoinGroup("@TGS#1JYSZEAEQ", "some reason", new TIMCallBack() {
    @java.lang.Override
    public void onError(int code, String desc) {
        //The API returns "code" (error code) and "desc" (error description), which can be used to identify request failure causes.
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

Group members can quit their groups. The API for quitting a group is provided by `TIMGroupManager`.

**Permission notes:**

- **Private group:** all members can quit the group.
- **Public group, chat room, and audio-video group:** the group owner cannot quit the group.

For more information, see [Differences in Member Management Capabilities](https://intl.cloud.tencent.com/document/product/1047/33529#.E6.88.90.E5.91.98.E7.AE.A1.E7.90.86.E8.83.BD.E5.8A.9B.E5.B7.AE.E5.BC.82).

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
            //For the meanings of error codes, see the Error Code Table
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

The function parameter information for deleting group members is the same as that for joining a group. The API for deleting group members is provided by `TIMGroupManager.

**Permission notes:**
For more information, see [Differences in Member Management Capabilities](https://intl.cloud.tencent.com/document/product/1047/33529#.E6.88.90.E5.91.98.E7.AE.A1.E7.90.86.E8.83.BD.E5.8A.9B.E5.B7.AE.E5.BC.82).

**Prototype:**

```
/**
 * Deleting group members
 * @param param Parameter for deleting group members
 * @param cb Callback. The list of deleted group members is returned in a parameter of the OnSuccess function.
 */
public void deleteGroupMember(@NonNull DeleteMemberParam param,
							  @NonNull TIMValueCallBack<List<TIMGroupMemberResult>> cb)
```

**`DeleteMemberParam` is defined as follows:**
```
/**
 * Construct parameters
 * @param groupId Group ID
 * @param members List of user IDs
 */
public DeleteMemberParam(@NonNull String groupId, @NonNull List<String> members)

/**
 * Set the reason for deleting group members (optional)
 * @param reason Reason for deletion
 */
public DeleteMemberParam setReason(@NonNull String reason)
```

**Example:**

```
//Create a list of users to be removed from the group
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

The `getGroupMembers` API can be used to get the group member list. By default, built-in fields and custom fields are pulled. For custom fields, you can configure the corresponding keys and permissions in **Feature Configuration** > **Custom Group Member Fields** in the [IM console](https://console.cloud.tencent.com/im). The configuration will take effect in 5 minutes.

**Permission notes:**

- **An group type:** the member list can be obtained.
- **Audio-video group:** only a partial list of group members can be pulled, including the group owner, admin, and some members.

For more information, see [Differences in Basic Group Capabilities](https://intl.cloud.tencent.com/document/product/1047/33529#.E7.BE.A4.E7.BB.84.E5.9F.BA.E7.A1.80.E8.83.BD.E5.8A.9B.E6.93.8D.E4.BD.9C.E5.B7.AE.E5.BC.82). 

**Prototype:**

```
/**
 * Get the group member list
 * @param groupId Group ID
 * @param cb Callback. The group member list is returned in a parameter of the OnSuccess function.
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
    public void onSuccess(List<TIMGroupMemberInfo> infoList) {//The group member information is returned in the parameter

        for(TIMGroupMemberInfo info : infoList) {
            Log.d(tag, "user: " + info.getUser() +
            "join time: " + info.getJoinTime() +
            "role: " + info.getRole());
        }
    }
};

//Get group member information
TIMGroupManager.getInstance().getGroupMembers(
        groupId, //Group ID
        cb);     //Callback
```

### Obtaining your group list

You can get the list of groups the current user has joined through `TIMGroupManager`. The returned information contains only part of the basic information. To get detailed group information, see [Group Members Obtain Group Profiles](https://intl.cloud.tencent.com/document/product/1047/36271).

**Permission notes:**

- **Private groups, public groups, and chat rooms:** you can use this API to get information about the public groups, chat rooms, and activated private groups that you have joined.
- **Audio-video groups and broadcasting chat rooms:** these two types of groups were not obtained through this API due to the differences in internal implementation.

**Prototype:**

```
/**
 * Get the list of groups the user has joined
 * @param cb Callback. Information about the groups that the current user has joined is returned in a parameter of the OnSuccess function.
 */
public void getGroupList(@NonNull TIMValueCallBack<List<TIMGroupBaseInfo>> cb)
```

**`TIMGroupBaseInfo` provides the following method:**
```
/**
 * Get the group ID
 * @return Group ID
 */
public String getGroupId()

/**
 * Get the group name
 * @return Group name
 */
public String getGroupName()

/**
 * Get the group type
 * @return Group type
 */
public String getGroupType()

/**
 * Get the group profile photo URL
 * @return Group profile photo URL
 */
public String getFaceUrl()

/**
 * Get whether the current group has muted all members
 * @return true - All members are muted
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
        //For the meanings of error codes, see the Error Code Table
        Log.e(tag, "get group list failed: " + code + " desc");
    }

    @Override
    public void onSuccess(List<TIMGroupBaseInfo> timGroupInfos) {//Basic information about each group is returned in the parameter
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

### Deleting groups

 The API for deleting groups is provided by `TIMGroupManager`.

**Permission notes:**
For more information, see [Differences in Basic Group Capabilities](https://intl.cloud.tencent.com/document/product/1047/33529#.E7.BE.A4.E7.BB.84.E5.9F.BA.E7.A1.80.E8.83.BD.E5.8A.9B.E6.93.8D.E4.BD.9C.E5.B7.AE.E5.BC.82). 

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
//Deleting a group
TIMGroupManager.getInstance().deleteGroup(groupId, new TIMCallBack() {
    @Override
    public void onError(int code, String desc) {

        //"code" (error code) and "desc" (error description) can be used to locate the cause of the request failure
        //For a list of error codes, see the Error Code Table
        Log.d(tag, "login failed. code: " + code + " errmsg: " + desc);
    }

    @Override
    public void onSuccess() {
        //The group was deleted successfully
    }
});
```

### Transferring a group

The API for transferring a group is provided by `TIMGroupManager`.

**Permission notes:**

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

**The API for obtaining a specified type of member (admin, group owner, or ordinary member) is defined as follows:**

```
/**
 * You can obtain the group member list based on filter conditions (for example, by field or by page)
 * @param groupId Group ID
 * @param flags Profile pull flag. It can be a flag or combination bitmap, for example, {@see TIMGroupManager#TIM_GET_GROUP_MEM_INFO_FLAG_NAME_CARD}.
 * @param filter Role filter type. For more information, see {@see TIMGroupMemberRoleFilter}.
 * @param custom List of custom keys to be obtained
 * @param nextSeq Pulling-by-page flag. It is set to 0 when the information is pulled for the first time. If the callback succeeds and the result is not 0, pagination is needed. The value of this field is passed in for the next pull until the value becomes 0.
 * @param cb Callback
 */
public void getGroupMembersByFilter(@NonNull String groupId, long flags, @NonNull TIMGroupMemberRoleFilter filter,
									List<String> custom, long nextSeq, TIMValueCallBack<TIMGroupMemberSucc> cb)
```

## Getting Group Profiles

### Getting group profiles

The `getGroupInfo` method of `TIMGroupManager` can be used to obtain group information from the server. The `queryGroupInfo` method can be used to obtain locally cached group information. Group members can pull group information. Non-members are not allowed to pull the information of private groups. For other group types, non-members can only pull public fields: `groupId\groupName\groupOwner\groupType\createTime\memberNum\maxMemberNum\onlineMemberNum\groupIntroduction\groupFaceUrl\addOption\custom`.

**Note:**

By default, basic information and custom fields are pulled. For custom fields, you need to configure the corresponding keys and permissions in **Feature Configuration** > **Custom Group Fields** in the [IM console](https://console.cloud.tencent.com/im). The configuration will take effect in 5 minutes.

**Prototype:**

```
/**
 * Get group information from the server
 * @param groupIdList List of group IDs of the groups for which you want to pull detailed information. A maximum of 50 group IDs can be listed at a time.
 * @param cb Callback. The group information {@see TIMGroupDetailInfo} list is returned in a parameter of the OnSuccess function.
 */
public void getGroupInfo(@NonNull List<String> groupIdList,
							   @NonNull TIMValueCallBack<List<TIMGroupDetailInfo>> cb)
/**
 * Get locally stored group information 
 * @param groupId ID of the group for which you want to pull detailed information
 * @return Group information. If no group information is stored locally, ‘null’ is returned.
 */
 public TIMGroupDetailInfo queryGroupInfo(@NonNull String groupId)
```

**The `TIMGroupDetailInfo` API is defined as follows:**
```
/**
 * Get the group ID
 * @return Group ID
 */
public String getGroupId()

/**
 * Get the group name
 * @return Group name
 */
public String getGroupName()

/**
 * Get the group creator’s account
 * @return Group creator’s account
 */
public String getGroupOwner()

/**
 * Get the group creation time
 * @return Group creation time
 */
public long getCreateTime()

/**
 * Get the last time that the group information was modified
 * @return Last time that the group information was modified
 */
public long getLastInfoTime()

/**
 * Get the time of the latest group message
 * @return Time of the latest group message
 */
public long getLastMsgTime()

/**
 * Get the number of group members
 * @return Number of group members
 */
public long getMemberNum()

/**
 * Get the maximum number of group members allowed
 * @return Maximum number of group members
 */
public long getMaxMemberNum()

/**
 * Get the group introduction
 * @return Group introduction
 */
public String getGroupIntroduction()

/**
 * Get the group notice
 * @return Group notice
 */
public String getGroupNotification()

/**
 * Get the group profile photo URL
 * @return Group profile photo URL
 */
public String getFaceUrl()

/**
 * Get the group type
 * @return Group type
 */
public String getGroupType()

/**
 * Get the group joining option
 * @return Group joining option
 */
public TIMGroupAddOpt getGroupAddOpt()

/**
 * Get the last message in the group
 * @return Last message in the group
 */
public TIMMessage getLastMsg()

/**
 * Get the custom group field map
 * @return Custom group field map
 */
public Map<String, byte[]> getCustom()

/**
 * Get whether the group has muted all members
 * @return true - All members are muted
 * @since 3.1.1
 */
public boolean isSilenceAll()
```

**Example:**

```
//Create a list of IDs of the groups for which you want to get information
ArrayList<String> groupList = new ArrayList<String>();

//Create callback
TIMValueCallBack<List<TIMGroupDetailInfo>> cb = new TIMValueCallBack<List<TIMGroupDetailInfo>>() {
    @Override
    public void onError(int code, String desc) {
            //"code" (error code) and "desc" (error description) can be used to locate the cause of the request failure
            //For a list of error codes, see the Error Code Table
    }

    @Override
    public void onSuccess(List<TIMGroupDetailInfo> infoList) { //The group information list is returned in the parameter
        for(TIMGroupDetailInfo info : infoList) {
            Log.d(tag, "groupId: " + info.getGroupId()           //Group ID
            + " group name: " + info.getGroupName()              //Group name
            + " group owner: " + info.getGroupOwner()            //Group creator’s account
            + " group create time: " + info.getCreateTime()      //Group creation time
            + " group last info time: " + info.getLastInfoTime() //Last time the group information was modified
            + " group last msg time: " + info.getLastMsgTime()  //Time of the last group message
            + " group member num: " + info.getMemberNum());      //Number of group members
        }
    }
};

//Add the group ID
String groupId = "TGID1EDABEAEO";
groupList.add(groupId);

//Get the server group information
TIMGroupManager.getInstance().getGroupInfo(
        groupList, //List of group IDs for which you want to get information
        cb);       //Callback

//Get group information cached locally
TIMGroupDetailInfo timGroupDetailInfo = TIMGroupManager.getInstance().queryGroupInfo(groupId);
```

### Getting your own profile in a group

You can obtain your own profile in a group when the list of groups you have joined is pulled. See [Getting group list](#.E8.8E.B7.E5.8F.96.E5.8A.A0.E5.85.A5.E7.9A.84.E7.BE.A4.E7.BB.84.E5.88.97.E8.A1.A8). If you want to get your profile in a single group, use `getSelfInfo` of `TIMGroupManager` as shown below. If the app needs to get a group list, we recommend that you get the profiles in groups when getting the group list instead of calling the following API.

**Permission notes:**

**Audio-video group:** you cannot get your own profile in the group.

**Prototype:**

```
/**
 * Get your own information in a group
 * @param groupId Group ID
 * @param cb Callback. Your own profile is returned in a parameter of the onSuccess function.
 */
public void getSelfInfo(@NonNull String groupId, @NonNull TIMValueCallBack<TIMGroupSelfInfo> cb)
```

### Getting a group member’s profile

The API for getting a group member’s profile is provided by `TIMGroupManager`. By default, the basic profile is pulled.

**Permission notes:**

**Audio-video group:** only the profiles of some members can be obtained, including the group owner, admin, and some group members.

**Prototype:**
```
/**
 * Get a specified group member’s information in the group
 * @param groupId Specified group ID
 * @param identifiers Identifiers of specified group members. A maximum of 100 identifiers can be specified at a time.
 * @param cb Callback. The group member list is returned in a parameter of the OnSuccess function.
 */
public void getGroupMembersInfo(@NonNull String groupId, @NonNull List<String> identifiers,
								@NonNull TIMValueCallBack<List<TIMGroupMemberInfo>> cb)
```


## Modifying Group Profiles

The API for modifying group profiles is provided by `TIMGroupManager`. You can modify the group name, group introduction, group notice, and other information.

**Prototype:**

```
/**
 * Modify the basic group information
 * @param param Parameters
 * @param cb Callback
 */
public void modifyGroupInfo(@NonNull ModifyGroupInfoParam param, @NonNull TIMCallBack cb)
```

**`TIMGroupManager.ModifyGroupInfoParam` is defined as follows:**

```
/**
 * Construct parameter instances
 * @param groupId Group ID
 */
public ModifyGroupInfoParam(@NonNull String groupId)

/**
 * Set the new group name
 * @param groupName Group name
 */
public ModifyGroupInfoParam setGroupName(@NonNull String groupName)

/**
 * Set the modified group notice
 * @param notification Group notice
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
 * Set the group joining option
 * @param addOpt Group joining option
 */
public ModifyGroupInfoParam setAddOption(@NonNull TIMGroupAddOpt addOpt)

/**
 * Set the maximum number of group members
 * @param maxMemberNum Maximum number of group members
 */
public ModifyGroupInfoParam setMaxMemberNum(long maxMemberNum)

/**
 * Set whether group members are visible to external users
 * @param visable Whether group members are visible to external users
 */
public ModifyGroupInfoParam setVisable(boolean visable)

/**
 * Set custom group fields
 * @param customInfos Custom group field dictionary
 */
public ModifyGroupInfoParam setCustomInfo(@NonNull Map<String, byte[]> customInfos)

/**
 * Set whether to mute all group members
 * @param silenceAll true: mute all group members. false: unmute all group members.
 * @since 3.1.1
 */
public ModifyGroupInfoParam setSilenceAll(boolean silenceAll)
```

### Changing the group name

**Permission notes:**

- **Public groups, chat rooms, and audio-video groups:** only the group owner or admin can change the group name.
- **Private groups:** any member can change the group name.

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

**Permission notes:**

- **Public groups, chat rooms, and audio-video groups:** only the group owner or admin can modify the group introduction.
- **Private groups:** any member can modify the group introduction.

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

### Modifying the group notice

**Permission notes:**

- **Public groups, chat rooms, and audio-video groups:** only the group owner or admin can modify the group notice.
- **Private groups:** any member can modify the group notice.

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

**Permission notes:**

- **Public groups, chat rooms, and audio-video groups:** only the group owner or admin can modify the group profile photo.
- **Private groups:** any member can modify the group profile photo.


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

### Modifying the group joining option

**Permission notes:**

- **Public groups, chat rooms, and audio-video groups:** only the group owner or admin can modify the group joining option.
- **Private groups:** users can only be invited to join the group and cannot apply to join the group.

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

### Modifying custom group fields

**Permission notes:**

- You need to configure relevant keys and permissions on the backend.

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

**Permission notes:**

- **Only the group owner or admin** has the permission to mute all members.
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

The API for modifying group member profiles is provided by `TIMGroupManager`. You can modify group member roles and group name cards and mute group members.

**Prototype:**

```
/**
 * Modify group member profiles
 * @param param Parameter for modifying group member profiles
 * @param cb Callback
 */
public void modifyMemberInfo(@NonNull ModifyMemberInfoParam param, @NonNull TIMCallBack cb)
```

**`TIMGroupManager.ModifyMemberInfoParam` is defined as follows:**

```
/**
 * Construct parameters for modifying group member profiles
 * @param groupId ID of the group to which the group member belongs
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
 * @param receiveMessageOpt The option for receiving group messages. See {@see TIMGroupReceiveMessageOpt}
 */
public ModifyMemberInfoParam setReceiveMessageOpt(@NonNull TIMGroupReceiveMessageOpt receiveMessageOpt)

/**
 * Modify a group member’s role (only the group owner and admins can modify roles)
 * @param roleType The type of the role. Cannot be changed to group owner. See {@see TIMGroupMemberRoleType}
 */
public ModifyMemberInfoParam setRoleType(TIMGroupMemberRoleType roleType)

/**
 * Set the muting duration for group members (only the group owner and admin can do this)
 * @param silence Muting duration
 */
public ModifyMemberInfoParam setSilence(long silence)

/**
 * Set custom group fields
 * @param customInfo Custom group field dictionary
 */
public ModifyMemberInfoParam setCustomInfo(Map<String, byte[]> customInfo)
```

### Modifying a user’s role in the group

**Permission notes:**

- **Only the group owner or admin** can modify group member roles.
- The roles of members in an **audio-video group** cannot be modified.

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

You can mute group members and set the muting duration through `modifyMemberInfoParam.setSilence()`.

**Permission notes:**

- **Only the group owner or admin** can mute group members.

**Example:**

```
//Mute a member for 100s
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

### Modifying a group member’s name card


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

### Modifying custom group member fields

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

**Permission notes:**

- **Public groups and private groups:** the default option is to receive and push group messages offline.
- **Chat rooms and audio-video groups:** the default option is to receive but not push group messages offline.

**`TIMGroupReceiveMessageOpt` is defined as follows:**

```
//Do not receive group messages, and the server will not forward them
TIMGroupReceiveMessageOpt.NotReceive

//Receive group messages, but offline messages will not be pushed if users are offline
TIMGroupReceiveMessageOpt.ReceiveNotNotify

//Receive group messages, and offline messages will be pushed if users are offline
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

Group pending requests are requests that need to be approved, such as pending requests to join a group and requests to invite users to a group. Group pending requests are indicated by the `TIMGroupPendencyItem` class.

**`TIMGroupPendencyItem` provides the following methods:**
```
/**
 * Get the group ID
 * @return Group ID
 */
public String getGroupId()

/**
 * Get the requester’s identifier. For a request to join a group, it refers to the requester’s identifier. For a request to invite users to a group, it refers to the inviter’s identifier.
 * @return Requester’s identifier
 */
public String getFromUser()

/**
 * Get the identifier of the handler. The identifier is 0 if it is an “apply to join” request and the invitee if it is an “invited to join” request.
 * @return Handler’s identifier
 */
public String getToUser()

/**
 * Get the time when the group pending request was added
 * @return Time when the group pending request was added
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
 * @return Additional information added by the requester
 */
public String getRequestMsg()

/**
 * Get the custom information added by the requester
 * @return Custom information added by the requester
 */
private String getRequestUserData()

/**
 * Get the additional information added by the handler. Only valid when the processing status is not {@see TIMGroupPendencyHandledStatus#NOT_HANDLED}.
 * @return Additional information added by the handler
 */
public String getHandledMsg()

/**
 * Get the custom information added by the handler. Only valid when the processing status is not {@see TIMGroupPendencyHandledStatus#NOT_HANDLED}.
 * @return Custom information added by the handler
 */
private String getHandledUserData()

/**
 * Approve the request. Currently, this is valid only for group joining application/invitation messages.
 *
 * @param msg Reason for approval (optional)
 * @param cb Callback
 */
public void accept(String msg, TIMCallBack cb)

/**
 * Reject the request. Currently, this is valid only for group joining application/invitation messages.
 *
 * @param msg Reason for approval (optional)
 * @param cb Callback
 */
public void refuse(String msg, TIMCallBack cb)
```

### Pulling the list of group pending requests

The `getGroupPendencyList` API provided by `TIMGroupManager` can be used to pull group pending requests. Even after being approved or rejected, pending requests can still be pulled, but in that case, a flag is carried to indicate that the requests have been processed.

**Permission notes:**

**Only the approver** has the permission to pull relevant information.

> Example:
>- When User A applies to join Group A, the group admin can pull the pending request. As User A does not have the approval permission, User A does not need to pull the pending request.
>- If Admin A invites User A to Group A, User A can pull this pending request, because the pending request needs to be approved by User A.

**Prototype:**

```
/**
 * Get the list of group pending requests by page
 * @param param The parameter for getting a list of group pending requests. See {@see TIMGroupPendencyGetParam}
 * @param cb Callback. The parameter of onSuccess returns the list of group pending requests and metadata. See {@see TIMGroupPendencyMeta} and {@see TIMGroupPendencyItem}
 */
public void getGroupPendencyList(@NonNull TIMGroupPendencyGetParam param,
								 @NonNull TIMValueCallBack<TIMGroupPendencyListGetSucc> cb)
```

**`TIMGroupPendencyGetParam` is defined as follows:**

```
/**
 * Set the page turning timestamp, which is only used to turn pages. Enter 0 for the first request. Subsequently, enter the corresponding value based on the timestamp in {@see TIMGroupPendencyMeta} returned by the server.
 * @param timestamp Page turning timestamp
 */
public void setTimestamp(long timestamp)

/**
 * Set the number of requests per page (this is a suggested value which does not indicate completion; the server can return more or less requests)
 * @param numPerPage Number of requests per page
 */
public void setNumPerPage(long numPerPage)
```

**Example:**

```
TIMGroupPendencyGetParam param = new TIMGroupPendencyGetParam();
param.setTimestamp(0);//Specify 0 for the first pull
param.setNumPerPage(10);

TIMGroupManager.getInstance().getGroupPendencyList(param, new TIMValueCallBack<TIMGroupPendencyListGetSucc>() {
    @Override
    public void onError(int code, String desc) {

    }

    @Override
    public void onSuccess(TIMGroupPendencyListGetSucc timGroupPendencyListGetSucc) {
        //If the value of nextStartTimestamp in meta is not 0, you can save it first
        // Enter the value into TIMGroupPendencyGetParam as the parameter for obtaining the next page of data
        TIMGroupPendencyMeta meta = timGroupPendencyListGetSucc.getPendencyMeta();
        Log.d(tag, meta.getNextStartTimestamp()
                + "|" + meta.getReportedTimestamp() + "|" + meta.getUnReadCount());

        List<TIMGroupPendencyItem> pendencyItems = timGroupPendencyListGetSucc.getPendencies();
        for(TIMGroupPendencyItem item : pendencyItems){
            //Perform an operation on group pending requests. For example, view, approve, or reject a pending request.
        }
    }
});
```

###  Reporting that group pending requests are read

You can use the `reportGroupPendency` API of `TIMGroupManager` to report that a pending request and all other pending requests before it have been read. After reporting, you can still pull these pending requests and determine whether they have been read based on the read timestamp.

**Prototype:**

```
/**
 * Report that group pending requests are read
 * @param timestamp Read timestamp (in seconds). All group pending requests before this timestamp will be set as read.
 * @param cb Callback
 */
public void reportGroupPendency(long timestamp, @NonNull TIMCallBack cb)
```


### Processing group pending requests

Through `getGroupPendencyList`, a group pending request list (`TIMGroupPendencyItem`) is obtained. Each element on the list can be processed through the `accept/refuse` API of the `TIMGroupPendencyItem` class as a group pending request. Pending requests that have been successfully processed cannot be processed again.

**Prototype:**

```
/**
 * Approve the request. Currently, this is valid only for group joining application/invitation messages.
 *
 * @param msg Reason for approval (optional)
 * @param cb Callback
 */
public void accept(String msg, TIMCallBack cb)

/**
 * Reject the request. Currently, this is valid only for group joining application/invitation messages.
 *
 * @param msg Reason for approval (optional)
 * @param cb Callback
 */
public void refuse(String msg, TIMCallBack cb)
```

## Group Event Messages

When a user is invited to join a group or is removed from a group, a tip message is displayed in the group. The caller can choose to display the tip message to group users or ignore it. A tip message is identified by a special `Elem` and returned by the new message callback (see [New message notification](https://intl.cloud.tencent.com/document/product/1047/36255#.E6.96.B0.E6.B6.88.E6.81.AF.E9.80.9A.E7.9F.A5)). To get group event messages, in addition to relying on new message notifications, you can also set group event listeners to listen to different events through `setGroupEventListener` of `TIMUserConfig` **before login** (see [Initialization (Android)](https://intl.cloud.tencent.com/document/product/1047/36255)).

>! The group event messages of chat rooms (ChatRoom) and audio-video groups (AVChatRoom) are not delivered by new message notifications. Therefore, you must register group event listeners to listen to different group events.




**`TIMGroupTipsElem` provides the following methods:**

```
//Get the group profile change information list. This is valid only when the value of tipsType is TIMGroupTipsType.ModifyGroupInfo.
java.util.List<TIMGroupTipsElemGroupInfo> getGroupInfoList()

//Get the group name
java.lang.String    getGroupName()

//Get the group member change information list. This is valid only when the value of tipsType is TIMGroupTipsType.ModifyMemberInfo.
java.util.List<TIMGroupTipsElemMemberInfo>    getMemberInfoList()

//Get the operator
java.lang.String    getOpUser()

//Get the group event notification type
TIMGroupTipsType    getTipsType()

//Get the list of accounts to be operated on
java.util.List<java.lang.String>  getUserList()
```

**`TIMGroupTipsType` prototype:**

```
//Cancel an admin
CancelAdmin

//Join a group
Join

//Remove from a group
Kick

//Modify group profiles
ModifyGroupInfo

//Modify member information
ModifyMemberInfo

//Quit a group
Quit

//Set an admin
SetAdmin
```

### Group joining notification

**Trigger:** when a user joins a group (through application or invitation), the system sends a notification in the group. Developers can choose the display mode and can update the group member list. The message type is `TIMGroupTipsType.Join`.

<b>`TIMGroupTipsElem` methods and return description: <b/>

Method | Return Description
---|---
getType |TIMGroupTipsType.Join
getOpUser | Application to join a group: applicant</br>Invitation to a group: inviter
getGroupName | Group name
getUserList | List of users to join the group

### Group departure notification

**Trigger:** when a user chooses to leave a group, the system sends a notification in the group. You can choose to update the group member list. The message type is `TIMGroupTipsType.Quit`.

<b>`TIMGroupTipsElem` methods and return description: <b/>

Method | Return Description
---|---
getType|TIMGroupTipsType.Quit
getOpUser | Identifier of the user who leaves the group
getGroupName | Group name

### Member removal notification

**Trigger:** when a user is removed from a group, the system sends a notification. You can update the group member list. The message type is `TIMGroupTipsType.Kick`.

<b>`TIMGroupTipsElem` methods and return description: <b/>

Method | Return Description
---|---
getType|TIMGroupTipsType.Kick
getOpUser | Identifier of the user who removes members from the group
getGroupName | Group name
getUserList | List of users removed from the group

### Admin setting/cancellation notifications

**Trigger:** when a user is set or canceled as an admin, the system sends a notification in the group. If the UI shows whether a user is an admin, you can update the admin flag. The message types are `TIMGroupTipsType.SetAdmin` and `TIMGroupTipsType.CancelAdmin`.

<b>`TIMGroupTipsElem` methods and return description: <b/>

Method | Return Description
---|---
getType | Setting: TIMGroupTipsType.SetAdmin<br>Cancellation: TIMGroupTipsType.CancelAdmin
getOpUser | Identifier of the user who performs the operation
getGroupName | Group name
getUserList | List of users who are set or canceled as admins

### Group profile change notification

**Trigger:** when the group profile changes, for example, when the group name or introduction changes, the system sends a notification. You can update relevant display fields or choose to display the message to users.

<b>`TIMGroupTipsElem` methods and return description: <b/>

Method | Return Description
---|---
getType | TIMGroupTipsType.ModifyGroupInfo
getOpUser | Identifier of the user who performs the operation
getGroupName | Group name
getGroupInfoList | Specific profile information of the group whose profile changes. It’s the TIMGroupTipsElemGroupInfo structure list.

**`TIMGroupTipsElemGroupInfo` Prototype:**

```
//Get the message content
java.lang.String    getContent()

//Get the group profile change message type
TIMGroupTipsGroupInfoType   getType()
```

**`TIMGroupTipsGroupInfoType` Prototype:**
```
//Modify the group profile photo URL
ModifyFaceUrl

//Modify the group introduction
ModifyIntroduction

//Change the group name
ModifyName

//Modify the group notice
ModifyNotification

//Change the group owner
ModifyOwner
```

### Group member profile change notification

**Trigger:** when a group member’s group member profile changes, including the role and whether the member is muted, the system sends a notification. You can update relevant displayed fields or choose to display the message to users.

>!
>- **The profile mentioned here includes only information related to the group, such as muting duration and member role change. Information related to the user, such as the user’s nickname, is not included**. For groups that have too many members, we recommend that you display the information in the message body instead of updating it in real time. For more information, see [Message sender and related profile](https://intl.cloud.tencent.com/document/product/1047/36401).
>- If the user’s profile is stored locally, determine whether the locally stored profile changes based on the message body information. If yes, update the profile after receiving a message from the user.

<b>`TIMGroupTipsElem` methods and return description: <b/>

Method | Return Description
---|---
getType|TIMGroupTipsType.ModifyMemberInfo
getOpUser | Identifier of the user who performs the operation
getGroupName | Group name
getMemberInfoList | Specific profile information of the group member whose profile changes. It’s the TIMGroupTipsElemMemberInfo structure list.

**`TIMGroupTipsElemMemberInfo` prototype:**

```
//Get the identifier of the muted member
java.lang.String    getIdentifier()

//Get the muting duration
long    getShutupTime()
```

## Group System Messages

When a group event occurs, for example, when a user applies to join a group, the admin will receive a corresponding group system message. Users can determine whether to accept or reject the request. Relevant messages are displayed to users through group system messages.

**Group system message type definitions:**

```
//Application to join the group is approved (received only by the applicant)
TIM_GROUP_SYSTEM_ADD_GROUP_ACCEPT_TYPE

//Application to join the group is rejected (received only by the applicant)
TIM_GROUP_SYSTEM_ADD_GROUP_REFUSE_TYPE

//Application is submitted for joining the group (received only by the admin)
TIM_GROUP_SYSTEM_ADD_GROUP_REQUEST_TYPE

//Admin status canceled (received only by the canceled admin)
TIM_GROUP_SYSTEM_CANCEL_ADMIN_TYPE

//Group created (received only by initial members)
TIM_GROUP_SYSTEM_CREATE_GROUP_TYPE

//Group deleted (received by all members)
TIM_GROUP_SYSTEM_DELETE_GROUP_TYPE

//Admin status set (received only by the set admin)
TIM_GROUP_SYSTEM_GRANT_ADMIN_TYPE

//Invited to join a group (received only by the invitee)
TIM_GROUP_SYSTEM_INVITED_TO_GROUP_TYPE

//Removed from the group by the admin (received only by the removed user)
TIM_GROUP_SYSTEM_KICK_OFF_FROM_GROUP_TYPE

//Group departure (received only by the user who leaves the group)
TIM_GROUP_SYSTEM_QUIT_GROUP_TYP

//Group repossessed (received by all members)
TIM_GROUP_SYSTEM_REVOKE_GROUP_TYPE

//Invited to join a group (received only by the invitee)
TIM_GROUP_SYSTEM_INVITE_TO_GROUP_REQUEST_TYPE

//Group invitation request approved (received only by the inviter)
TIM_GROUP_SYSTEM_INVITATION_ACCEPTED_TYPE

//Group invitation request rejected (received only by the inviter)
TIM_GROUP_SYSTEM_INVITATION_REFUSED_TYPE
```

**`TIMGroupSystemElem` methods are defined as follows:**

```
/**
 *  Operator platform information
 *  Values: iOS, Android, Windows, Mac, Web, RESTAPI, Unknown
 * @return Operator platform information returned
 */
public String getPlatform()

/**
 * Get the message sub-type
 * @return Group system message sub-type
 */
public TIMGroupSystemElemType getSubtype()

/**
 * Get the group ID of the message
 * @return
 */
public String getGroupId()

/**
 * Get the operator
 * @return Operator’s identifier
 */
public String getOpUser()

/**
 * Get the reason for the operation
 * @return Reason for the operation
 */
public String getOpReason()

/**
 * Get custom notification
 * @return Custom notification
 */
public byte[] getUserData()

/**
 * Get the operator’s profile
 * @return Operator’s profile
 */
public TIMUserProfile getOpUserInfo()

/**
 * Get the operator’s group member profile
 * @return Operator’s group member profile
 */
public TIMGroupMemberInfo getOpGroupMemberInfo()
```

### Group joining application request

**Trigger:** when a user applies to join a group, the group admin receives a group joining application request and can determine whether to approve the request. Message type: `TIM_GROUP_SYSTEM_ADD_GROUP_REQUEST_TYPE`.

**TIMGroupSystemElem methods and return description:**

Method | Return Description
---|---
getSubtype | TIM_GROUP_SYSTEM_ADD_GROUP_REQUEST_TYPE
getGroupId | The ID of the group for which the application was sent
getOpUser | Applicant
getOpReason | Reason for application (optional)


### Group joining application approval/rejection notifications

**Trigger:** when an admin approves a group joining application, the applicant receives an application approval notification. When the admin rejects the application, the applicant receives an application rejection notification.

**`TIMGroupSystemElem` methods and return description:**

Method | Return Description
---|---
getSubtype | Approval: TIM_GROUP_SYSTEM_ADD_GROUP_ACCEPT_TYPE<br>Rejection: TIM_GROUP_SYSTEM_ADD_GROUP_REFUSE_TYPE
getGroupId | ID of the group for which the request is approved/rejected
getOpUser | Identifier of the admin who processed the request
getOpReason | Reason for approval or rejection (optional)

### Group invitation request

**Trigger:** when a user is invited to join a group (**assuming the user has not yet joined the group and needs to process the invitation**), the user receives an invitation request message.

>! During the creation of a group, initial members can join it directly without the need of an invitation.

**`TIMGroupSystemElem` methods and return description:**

Method | Return Description
---|---
getSubtype | TIM_GROUP_SYSTEM_INVITE_TO_GROUP_REQUEST_TYPE
getGroupId | ID of the group that the invitee is invited to join
getOpUser | Operator, i.e., the inviter


### Group invitation acceptance/rejection notifications

**Trigger:** when the invitee accepts a group invitation, the inviter receives a group invitation acceptance notification. When the invitee rejects the invitation, the inviter receives a group invitation rejection notification.

**`TIMGroupSystemElem` methods and return description:**

Method | Return Description
---|---
getSubtype | Acceptance: TIM_GROUP_SYSTEM_INVITATION_ACCEPTED_TYPE<br>Rejection: TIM_GROUP_SYSTEM_INVITATION_REFUSED_TYPE
getGroupId | ID of the group for which the request is approved/rejected
getOpUser | Identifier of the admin who processed the request
getOpReason | Reason for acceptance or rejection (optional)


### Group member removal notification

**Trigger:** when a user is removed from a group by a group admin, the user receives a corresponding notification.

**`TIMGroupSystemElem` methods and return description:**

Method | Return Description
---|---
getSubtype | TIM_GROUP_SYSTEM_KICK_OFF_FROM_GROUP_TYPE
getGroupId | ID of the group from which the user is removed
getOpUser | Identifier of the admin who performed the operation


### Group deletion notification

**Trigger:** when a group is deleted, all group members receive a corresponding notification.

**`TIMGroupSystemElem` methods and return description:**

Method | Return Description
---|---
getSubtype | TIM_GROUP_SYSTEM_DELETE_GROUP_TYPE
getGroupId | ID of the deleted group
getOpUser | Identifier of the admin who performed the operation

### Group creation notification

**Trigger:** when a group is created, the creator receives a creation notification message.

When the callback for calling the group creation method succeeds, a group is created. This message is mainly used for multi-client synchronization. If other clients are also logged in, this message can be used to time group list updates. You can choose to ignore this message on the current client.

**`TIMGroupSystemElem` methods and return description:**

Method | Return Description
---|---
getSubtype | TIM_GROUP_SYSTEM_CREATE_GROUP_TYPE
getGroupId | ID of the created group
getOpUser | Creator, i.e., the user who performed the operation

### Group invitation notification

**Trigger:** when a user is invited to join a group (**the user has been added to the group at this time**), the user receives an invitation notification message.

>! During the creation of a group, initial members can join it directly without the need of an invitation.

**`TIMGroupSystemElem` methods and return description:**

Method | Return Description
---|---
getSubtype | TIM_GROUP_SYSTEM_INVITED_TO_GROUP_TYPE
getGroupId | ID of the group that the invitee is invited to join
getOpUser | Operator, i.e., the inviter

### Group departure notification

**Trigger:** when a user chooses to leave a group, only the user himself/herself receives a corresponding notification.

If a user calls `QuitGroup` and the success callback is returned, then the user has quit the group successfully. This message is used for multi-client synchronization. When receiving this message, the other clients can update the group list, while the current client can choose to ignore it.

**`TIMGroupSystemElem` methods and return description:**

Method | Return Description
---|---
getSubtype | TIM_GROUP_SYSTEM_QUIT_GROUP_TYPE
getGroupId | ID of the group that the user quits
getOpUser | Operator, i.e., the user who performed the operation

### Admin setting/cancellation notifications

**Trigger:** when a user is set or canceled as a group admin, the user receives a corresponding notification.

**`TIMGroupSystemElem` methods and return description:**

Method | Return Description
---|---
getSubtype | Admin role is canceled: TIM_GROUP_SYSTEM_GRANT_ADMIN_TYPE<br>Admin role is granted: TIM_GROUP_SYSTEM_CANCEL_ADMIN_TYPE
getGroupId | ID of the group where this event occurred
getOpUser | Operator

### Group repossessing notification

**Trigger:** when a group is repossessed by the system, all group members receive a corresponding notification.

**`TIMGroupSystemElem` methods and return description:**

Method | Return Description
---|---
getSubtype | TIM_GROUP_SYSTEM_REVOKE_GROUP_TYPE
getGroupId | ID of the repossessed group
