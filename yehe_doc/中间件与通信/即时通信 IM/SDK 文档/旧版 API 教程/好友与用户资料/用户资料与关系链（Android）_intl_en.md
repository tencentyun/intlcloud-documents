
IM provides the **user profile hosting** feature. App developers can use simple APIs to store the user profile. In addition, to facilitate the customization of different users’ profiles, IM also provides custom fields for user profiles.

## User Profiles
### Obtaining your own profile 

- You can use the `getSelfProfile` method of `TIMFriendshipManager` to obtain your own profile that is stored on the server.
- You can use the `querySelfProfile` method of `TIMFriendshipManager` to obtain your own profile that is stored locally.


**Prototype:**

```   
/**
 * Obtain your own profile that is stored on the server
 * @param cb Callback. Parameters in the OnSuccess function return the corresponding {@see TIMUserProfile} for users.
 */
public void getSelfProfile(final @NonNull TIMValueCallBack<TIMUserProfile> cb)

/**
 * Obtains your own profile that is stored locally. If no profile is stored locally, null is returned.
 *
 * @return TIMUserProfile
 */
public TIMUserProfile querySelfProfile()
```

**`TIMUserProfile` provides the following APIs:**

```
/**
 * Obtain the user’s identifier
 * @return User’s identifier
 */
public String getIdentifier()

/**
 * Obtain the user’s nickname
 * @return User’s nickname
 */
public String getNickName()

/**
 * Obtain the user’s profile photo URL
 * @return User’s profile photo URL
 */
public String getFaceUrl()

/**
 * Obtain the user’s personal signature
 * @return User’s personal signature
 */
public String getSelfSignature()

/**
 * Obtain the user’s friend request approval mode
 * @return User’s friend request approval mode. See the constant in TIMFriendAllowType for more information.
 */
public String getAllowType()

/**
 * Obtain the user’s custom information
 * @return Custom information map
 */
public Map<String, byte[]> getCustomInfo()

/**
 * Obtain the user’s custom information
 * @return Custom information map
 */
public Map<String, Long> getCustomInfoUint()

/**
 * Obtains the user’s gender. See the constant definition in TIMFriendGenderType for more information.
 * @return User’s gender
 */
public int getGender()

/**
 * Obtain the user’s birthday
 * @return Birthday
 */
public long getBirthday()

/**
 * Obtain the language
 * @return Language
 */
public long getLanguage()

/**
 * Obtain the location
 * @return Location
 */
public String getLocation()
```

**Example:**

```
//Obtain your own profile that is stored on the server
TIMFriendshipManager.getInstance().getSelfProfile(new TIMValueCallBack<TIMUserProfile>(){
	@Override
	public void onError(int code, String desc){
		//"code" (error code) and "desc" (error description) can be used to locate the cause of the request failure.
		//For the error code list, see the error code table.
        Log.e(tag, "getSelfProfile failed: " + code + " desc");
	}
	
	@Override
	public void onSuccess(TIMUserProfile result){
		Log.e(tag, "getSelfProfile succ");
		Log.e(tag, "identifier: " + result.getIdentifier() + " nickName: " + result.getNickName() 
					 + " allow: " + result.getAllowType());
	}
});

//Obtain your own profile that is stored locally
TIMUserProfile selfProfile = TIMFriendshipManager.getInstance().querySelfProfile();
```

### Obtaining a specified user’s profile

You can use the `getUsersProfile` method of `TIMFriendshipManager` to obtain a friend’s profile. This method can obtain the profile from either sources, the cache or the backend:
- If `forceUpdate = true`, data is forcibly pulled from the backend, and the returned data will be cached.
- If `forceUpdate = false`, the system first searches for the data locally. If no local data can be found, it requests the data from the backend.
   We recommend that data is forcibly pulled only for profile display to reduce the wait time.

You can use the `queryUserProfile` method of `TIMFriendshipManager` to obtain a friend’s profile from the local cache based on the returned value. If none can be found, `null` is returned.

**Prototype:**

```
/**
 * Obtain a specified friend’s profile (excluding remarks and friend groups)
 * @param users  List of the identifiers of users whose profiles are to be obtained
 * @param forceUpdate Forcibly pull data from the backend
 * @param cb Callback. The parameters in the OnSuccess function return the corresponding user’s {@see TIMUserProfile} list.
 */
public void getUsersProfile(@NonNull List<String> users, boolean forceUpdate, @NonNull TIMValueCallBack<List<TIMUserProfile>> cb) 

/**
 * Obtains the local friend’s profile (excluding remarks and friend groups). If none can be found, ‘null’ is returned.
 * @param identifier
 * @return TIMUserProfile
 */
public TIMUserProfile queryUserProfile(String identifier)
```

**Example:**

```
//List of users whose profiles are to be obtained
List<String> users = new ArrayList<String>();
users.add("sample_user_1");
users.add("sample_user_2");

//Obtains user profiles
TIMFriendshipManager.getInstance().getUsersProfile(users, true, new TIMValueCallBack<List<TIMUserProfile>>(){
	@Override
	public void onError(int code, String desc){
		//"code" (error code) and "desc" (error description) can be used to locate the cause of the request failure.
		//For the error code list, see the error code table.
        Log.e(tag, "getUsersProfile failed: " + code + " desc");
	}
	
	@Override
	public void onSuccess(List<TIMUserProfile> result){
        Log.e(tag, "getUsersProfile succ");
		for(TIMUserProfile res : result){
	        Log.e(tag, "identifier: " + res.getIdentifier() + " nickName: " + res.getNickName());
		}
	}
});

//Obtain the locally cached user profile
TIMUserProfile userProfile = TIMFriendshipManager.getInstance().queryUserProfile("sample_user_1");
```

The caching time of the `getUsersProfile` API can be set through the `setExpiredSeconds` API of `TIMFriendProfileOption`. The default caching time is one day.

```
TIMUserConfig config = new TIMUserConfig();
TIMFriendProfileOption timFriendProfileOption = new TIMFriendProfileOption();
timFriendProfileOption.setExpiredSeconds(60 * 60); // 1 hour
config.setTIMFriendProfileOption(timFriendProfileOption);
TIMManager.getInstance().setUserConfig(config);
```

### Modifying your own profile

You can use the `modifySelfProfile` method of `TIMFriendshipManager` to modify your own profile (such as your nickname, profile photo, and friend request approval mode).

**Prototype:**

```
/**
 * Modify your own profile
 * @param profileMap Fields to be modified are stored in hashMap, and the key values are the constants defined in TIMFriendshipManager:
 * TIMFriendshipManager.TIM_PROFILE_TYPE_KEY_XXX
 * @param cb Callback
 */
public void modifySelfProfile(@NonNull HashMap<String, Object> profileMap, @NonNull TIMCallBack cb)
```

Through `profileMap`, you can set multiple fields at a time. For example, the code for simultaneously setting the nickname and gender is as follows:

```
HashMap<String, Object> profileMap = new HashMap<>();
profileMap.put(TIMUserProfile.TIM_PROFILE_TYPE_KEY_NICK, "My nickname");
profileMap.put(TIMUserProfile.TIM_PROFILE_TYPE_KEY_GENDER, TIMFriendGenderType.GENDER_MALE);
profileMap.put(TIMUserProfile.TIM_PROFILE_TYPE_KEY_BIRTHDAY, 20190419);
TIMFriendshipManager.getInstance().modifySelfProfile(profileMap, new TIMCallBack() {
    @Override
    public void onError(int code, String desc) {
    	Log.e(tag, "modifySelfProfile failed: " + code + " desc" + desc);
    }

    @Override
    public void onSuccess() {
    	Log.e(tag, "modifySelfProfile success");
    }
});
```

Setting a key value that does not exist may lead to failure. Some common key values are defined in `TIMUserProfile`:

| Key | Value | Description |
| ------------------------------------ | ----------- | -------------- |
| `TIM_PROFILE_TYPE_KEY_NICK` | String | Nickname |
| `TIM_PROFILE_TYPE_KEY_FACEURL` | String | Profile photo |
| `TIM_PROFILE_TYPE_KEY_ALLOWTYPE` | String | Friend request |
| `TIM_PROFILE_TYPE_KEY_GENDER` | int | Gender |
| `TIM_PROFILE_TYPE_KEY_BIRTHDAY` | int | Birthday |
| `TIM_PROFILE_TYPE_KEY_LOCATION` | String | Location |
| `TIM_PROFILE_TYPE_KEY_LANGUAGE` | int | Language |
| `TIM_PROFILE_TYPE_KEY_LEVEL` | int | Level |
| `TIM_PROFILE_TYPE_KEY_ROLE` | int | Role |
| `TIM_PROFILE_TYPE_KEY_SELFSIGNATURE` | String | Signature |
| `TIM_PROFILE_TYPE_KEY_CUSTOM_PREFIX` | String, int | Prefix of the custom field |

For custom fields, you need to add prefixes. For example, to set the `Blood` custom field of the integer type on the backend, use the following code:

```
HashMap<String, Object> profileMap = new HashMap<>();
profileMap.put(TIMUserProfile.TIM_PROFILE_TYPE_KEY_CUSTOM_PREFIX + "Blood", 1);
TIMFriendshipManager.getInstance().modifySelfProfile(profileMap, new TIMCallBack() {
    @Override
    public void onError(int code, String desc) {
    	Log.e(tag, "modifySelfProfile failed: " + code + " desc" + desc);
    }

    @Override
    public void onSuccess() {
    	Log.e(tag, "modifySelfProfile success");
    }
});
```

## Friend Relationships
### Obtaining all friends
You can use the `getFriendList` method of `TIMFriendshipManager` to obtain the list of all friends.

```
/**
 * Obtain the friend list
 * @param cb  Callback for the TIMFriend list
 */
public void getFriendList(@NonNull TIMValueCallBack<List<TIMFriend>> cb)
```
The obtained friend list is returned, and friend objects are stored in `TIMFriend`. `TIMFriend` is defined as follows:
```
/**
 * Obtain the user’s identifier
 * @return User’s identifier
 */
public String getIdentifier()

/**
 * Obtain the friend’s remarks
 * @return Friend’s remarks
 */
public String getRemark()

/**
 * Obtain the reason of the friend request
 * @return Reason of the friend request
 */
public String getAddWording()

/**
 * Obtain the source of the friend request
 * @return Source of the friend request
 */
public String getAddSource()

/**
 * Obtain the friend group name
 * @return List of friend group names
 */
public List<String> getGroupNames()

/**
 * Obtains the friend’s custom information. The key value is based on the character string configured on the backend, excluding the TIM_FRIEND_PROFILE_TYPE_KEY_CUSTOM_PREFIX prefix.
 * @return Custom information map
 */
public Map<String, byte[]> getCustomInfo()

/**
 * Obtains the friend’s custom information of the uint type. The key value is based on the character string configured on the backend, excluding the 
 * TIM_FRIEND_PROFILE_TYPE_KEY_CUSTOM_PREFIX prefix.
 * @return Custom information map
 */
public Map<String, byte[]> getCustomInfoUint()

/**
 * Obtain the friend’s profile
 * @return User profile
 */
public TIMUserProfile getTimUserProfile()()
```
Sample code
```
TIMFriendshipManager.getInstance().getFriendList(new TIMValueCallBack<List<TIMFriend>>() {
            @Override
            public void onError(int code, String desc) {
                QLog.e(TAG, "getFriendList err code = " + code);
            }

            @Override
            public void onSuccess(List<TIMFriend> timFriends) {
                StringBuilder stringBuilder = new StringBuilder();
                for (TIMFriend timFriend : timFriends){
                    stringBuilder.append(timFriend.toString());
                }
                QLog.i(TAG, "getFriendList success result = " + stringBuilder.toString());
            }
        });
```

### Modifying friends

The `modifyFriend` method can be called to modify friends. Similar to modifying your own profile, multiple fields can be updated at a time.
```
/**
 * Modify a friend’s profile
 * @param identifier  Friend’s identifier
 * @param profileMap Fields to be modified. See TIM_FRIEND_PROFILE_TYPE_KEY_XXX in TIMFriend for more information.
 * @param cb Callback
 */
public void modifyFriend(@NonNull String identifier, @NonNull HashMap<String, Object> profileMap, @NonNull TIMCallBack cb)
```
Setting a key value that does not exist may lead to failure. The backend defines some common key values.

Key | Value | Description
--- | --- | --
TIM_FRIEND_PROFILE_TYPE_KEY_REMARK | String | Remarks 
TIM_FRIEND_PROFILE_TYPE_KEY_GROUP | List< String > | Friend group 
TIM_FRIEND_PROFILE_TYPE_KEY_CUSTOM_PREFIX | String, int | Prefix of the custom field

Example: set remarks for the friend [Android_002] to [002 remark] 

```
String identifier = "Android_002";
HashMap<String, Object> hashMap = new HashMap<>();
hashMap.put(TIMFriend.TIM_FRIEND_PROFILE_TYPE_KEY_REMARK, "002 remark");
TIMFriendshipManager.getInstance().modifyFriend(identifier, hashMap, new TIMCallBack() {
            @Override
            public void onError(int i, String s) {
                Log.e(TAG, "modifyFriend err code = " + i + ", desc = " + s);
            }

            @Override
            public void onSuccess() {
                Log.i(TAG, "modifyFriend success");
            }
        });
```

> To modify a friend’s custom information, you must first configure the relationship chain custom fields on the server.

### Adding friends

You can use the `addFriend` method of `TIMFriendshipManager` to add friends. 

```
/**
 * Add a friend
 * @param timFriendRequest Friend request
 * @param cb Callback
 */
public void addFriend(@NonNull TIMFriendRequest timFriendRequest, @NonNull TIMValueCallBack<TIMFriendResult> cb)
```

To add a friend, the request parameter needs to be passed in. Its parameter type is defined as follows:
```
/**
 *  User’s identifier
 */
private String identifier = "";

/**
 *  User’s remarks (a maximum of 96 bytes)
 */
private String remark = "";

/**
 *  Request description (a maximum of 120 bytes)
 */
private String addWording = "";

/**
 *  Friend addition source
 *  The source cannot exceed 8 bytes and must be prefixed with "AddSource_Type_".
 */
private String addSource = "";

/**
 *  Group name
 */
private String friendGroup = "";

```

The success callback returns the `TIMFriendResult` result for the operating user. Developers can notify the user accordingly. The return code for adding friends is as follows:

```
public class TIMFriendStatus {
    /**
     *  Operation succeeded
     */
    public static final int TIM_FRIEND_STATUS_SUCC                            = 0;
		
		/**
     * The request parameter is incorrect. Check whether the request is correct based on the error description.
     */
    public static final int TIM_FRIEND_PARAM_INVALID                          = 30001;
		
		/**
     *  Valid for adding friends and responding to friends: your number of friends has reached the limit of the system.
     */
    public static final int TIM_ADD_FRIEND_STATUS_SELF_FRIEND_FULL            = 30010;
		
		/**
     *  Valid for adding friends and responding to friends: the peer’s number of friends has reached the limit of the system.
     */
    public static final int TIM_ADD_FRIEND_STATUS_THEIR_FRIEND_FULL           = 30014;
		
    /**
     *  Valid for adding friends: the peer is already in your blacklist.
     */
    public static final int TIM_ADD_FRIEND_STATUS_IN_SELF_BLACK_LIST          = 30515;
		
    /**
     *  Valid for adding friends: the peer has forbidden friend requests.
     */
    public static final int TIM_ADD_FRIEND_STATUS_FRIEND_SIDE_FORBID_ADD      = 30516;
		
    /**
     *  Valid for adding friends: the peer has blacklisted you.
     */
    public static final int TIM_ADD_FRIEND_STATUS_IN_OTHER_SIDE_BLACK_LIST    = 30525;
    /**
     *  Valid for adding friends: the friend request is pending approval.
     */
    public static final int TIM_ADD_FRIEND_STATUS_PENDING                     = 30539;
};
```

Sample code

```
TIMFriendRequest timFriendRequest = new TIMFriendRequest("test_id");
timFriendRequest.setAddWording("it's me!");
timFriendRequest.setAddSource("android");
TIMFriendshipManager.getInstance().addFriend(timFriendRequest, new TIMValueCallBack<TIMFriendResult>() {
		@Override
		public void onError(int i, String s) {
				QLog.e(TAG, "addFriend err code = " + i + ", desc = " + s);
		}

		@Override
		public void onSuccess(TIMFriendResult timFriendResult) {
				QLog.i(TAG, "addFriend success result = " + timFriendResult.toString());
		}
});
```

### Deleting friends

You can use the `deleteFriends` method of `TIMFriendshipManager` to delete friends in batches. 

```
/**
 * Delete friends
 * @param identifiers Friend list
 * @param delFriendType Deletion type
 * @param cb Callback
 */
public void deleteFriends(@NonNull List<String> identifiers, @NonNull int delFriendType, @NonNull TIMValueCallBack<List<TIMFriendResult>> cb)
```

The success callback returns the `TIMFriendResult` result for the operating user. Developers can notify the user accordingly. The error codes for deleting friends are as follows:

```
public class TIMFriendStatus {
    /**
     *  Operation succeeded
     */
    public static final int TIM_FRIEND_STATUS_SUCC             = 0;
    /**
     *  Valid for deleting friends: the friend that you want to delete is not your friend.
     */
    public static final int TIM_DEL_FRIEND_STATUS_NO_FRIEND    = 31704;
};
```

Sample code

```
List<String> identifiers = new ArrayList<>();
identifiers.add("test_id");
TIMFriendshipManager.getInstance().deleteFriends(identifiers, TIMDelFriendType.TIM_FRIEND_DEL_SINGLE, new TIMValueCallBack<List<TIMFriendResult>>() {
		@Override
		public void onError(int i, String s) {
				QLog.e(TAG, "deleteFriends err code = " + i + ", desc = " + s);
		}

		@Override
		public void onSuccess(List<TIMFriendResult> timUserProfiles) {
				QLog.i(TAG, "deleteFriends success");
		}
});
```

### Approving or rejecting friend requests

You can use the `doResponse` method of `TIMFriendshipManager` to approve or reject friend requests.

```
/**
 * Handle a friend request
 * @param response Request parameter, including the friend ID, prior remarks, and response type
 * @param cb
 */
public void doResponse(TIMFriendResponse response, @NonNull TIMValueCallBack<TIMFriendResult> cb)
```

The `response` parameter is defined as follows:
```
public class TIMFriendResponse {
    /**
     *  Approve the friend request (establish a one-way friendship)
     */
    public static final int TIM_FRIEND_RESPONSE_AGREE = 0;

    /**
     *  Approve the friend request and add the friend (establish a two-way friendship)
     */
    public static final int TIM_FRIEND_RESPONSE_AGREE_AND_ADD = 1;

    /**
     *  Reject the friend request
     */
    public static final int TIM_FRIEND_RESPONSE_REJECT  = 2;

    /**
     * Response type
     */
    private int responseType = TIM_FRIEND_RESPONSE_AGREE;

    /**
     * Friend ID for response
     */
    private String identifier = ""; // Friend ID for response

    /**
     * Friend remarks (optional). You can add remarks if you want to add the user as a friend. The maximum length of the remarks is 96 bytes.
     */
    private String remark = "";
    
    .......The get and set methods are omitted here.
}
```

The success callback returns the `TIMFriendResult` result for the operating user. The error codes for handling friend requests are as follows:
```
public class TIMFriendStatus {
    /**
     *  Operation succeeded
     */
    public static final int TIM_FRIEND_STATUS_SUCC                    = 0;
		
    /**
     *  Valid for adding friends and responding to friends: your number of friends has reached the limit of the system.
     */
    public static final int TIM_ADD_FRIEND_STATUS_SELF_FRIEND_FULL    = 30010;
		
    /**
     *  Valid for adding friends and responding to friends: the user’s number of friends has reached the limit of the system.
     */
    public static final int TIM_ADD_FRIEND_STATUS_THEIR_FRIEND_FULL   = 30014;
		
    /**
     *  Valid for responding to friend requests: the peer has not initiated a friend request.
     */
    public static final int TIM_RESPONSE_FRIEND_STATUS_NO_REQ         = 30614;
};
```

### Verifying friend relationships

You can use the `checkFriends` method of `TIMFriendshipManager` to verify friend relationships.

```
/**
 * Verify friends
 * @param checkInfo Friend verification parameter
 * @param cb Callback
 */
public void checkFriends(@NonNull TIMFriendCheckInfo checkInfo, @NonNull TIMValueCallBack<List<TIMCheckFriendResult>> cb)
```

The `checkInfo` parameter is defined as follows:

```
public class TIMFriendCheckInfo {
	private List<String> users = new ArrayList<>();
    private int checkType = TIMFriendCheckType.TIM_FRIEND_CHECK_TYPE_UNIDIRECTION;
    
    /**
     * Set the ID of the friend to be checked
     *
     * @param users
     */
    public void setUsers(List<String> users);
    
    /**
     * Sets the type of the relationship to be checked. See the constant defined in TIMFriendCheckType for more information.
     *
     * @param type
     */
    public void setCheckType(int type);
}
```

The `TIMFriendCheckType` parameter is defined as follows:

```
public class TIMFriendCheckType {
    /**
     * One-way friendship
     */
    public static final int TIM_FRIEND_CHECK_TYPE_UNIDIRECTION     = 1;

    /**
     * Two-way friendship
     */
    public static final int TIM_FRIEND_CHECK_TYPE_BIDIRECTION      = 2;
}
```

The success callback returns the `TIMCheckFriendResult` list for the operating user. This parameter is defined as follows:

```
public class TIMCheckFriendResult {
    private String identifier = "";
    private int resultCode;
    private String resultInfo = "";
    private int resultType;

    /**
     * Obtain the friend ID
     *
     * @return Friend ID
     */
    public String getIdentifier();

    /**
     * Obtain the return code
     *
     * @return Return code
     */
    public int getResultCode();

    /**
     * Obtain the returned result description
     *
     * @return Result description
     */
    public String getResultInfo();

    /**
     * Obtains the friend relationship type to be checked. See the constant defined in TIMFriendRelationType for more information.
     *
     * @return Friend relationship type
     */
    public int getResultType();
}
```

The `TIMFriendRelationType` parameter is defined as follows:

```
public class TIMFriendRelationType {
    /**
     *  You are not friends.
     */
    public static final int TIM_FRIEND_RELATION_TYPE_NONE           = 0;

    /**
     *  The peer is in my friend list.
     */
    public static final int TIM_FRIEND_RELATION_TYPE_MY_UNI         = 1;

    /**
     *  I am in the peer’s friend list.
     */
    public static final int TIM_FRIEND_RELATION_TYPE_OTHER_UNI      = 2;

    /**
     *  You are friends for each other.
     */
    public static final int TIM_FRIEND_RELATION_TYPE_BOTH_WAY       = 3;

}
```






## Pending Friend Requests

### Obtaining the pending request list
When another user uses the `addFriend` method to request to add you as a friend, a pending record is added on the backend. When you request to add another user as a friend, a pending record is also added on the backend. You can use the `getPendencyList` method to obtain the pending request list.
```
/**
 * Obtain the pending request list
 * 
 * @param timFriendPendencyRequest
 * @param cb
 */
public void getPendencyList(TIMFriendPendencyRequest timFriendPendencyRequest, @NonNull TIMValueCallBack<TIMFriendPendencyResponse> cb)
```

As the backend may store multiple pending friend requests that go beyond the display scope of the interface, the API allows you to page up or down to browse all requests. In this case, the `timFriendPendencyRequest` parameter needs to be passed in. The definition of the parameter is as follows:
```
/**
 * Sequence number of the pending request list. We recommend that you save the sequence number and pending request list on the client. Enter the sequence number returned by the server when sending the request. If the sequence number is the latest on the server, no data is returned.
 * 
 * @param seq Sequence number
 */
public void setSeq(long seq)

/**
 * Paging timestamp, which is only used for paging up or down. If the server returns 0, it indicates that no more data is available. Enter 0 for the first request.
 * Note that if the sequence number returned by the server is different from the entered sequence number, use the original seq request on the client for paging up or down. The local seq is not updated until the data request is completed.
 * 
 * @param timestamp Paging timestamp
 */
public void setTimestamp(long timestamp)

/**
 * Number of requests per page, which is valid for requests
 * 
 * @param numPerPage Number of requests per page
 */
public void setNumPerPage(int numPerPage)

/**
 * Fetch type of pending requests. See the constant defined in TIMPendencyType for more information. 
 * 
 * @param timPendencyType Fetch type of pending requests
 */
public void setTimPendencyGetType(int timPendencyType)
```

After the operation succeeds, the callback returns the paging information and pending records `TIMFriendPendencyResponse`.
```
/**
 * Obtain the sequence number of the pending request list for the current request
 * @return Sequence number
 */
public long getSeq()

/**
 * Obtain the paging timestamp for the current request
 * 
 * @return Timestamp
 */
public long getTimestamp()

/**
 * Obtain the number of unread pending requests
 * 
 * @return Number of unread pending requests
 */
public long getUnreadCnt()

/**
 * Obtain the pending information list
 * 
 * @return Information list
 */
public List<TIMFriendPendencyItem> getItems()
```

`TIMFriendPendencyItem` is defined as follows:

```
/**
 * Obtain the user’s ID
 * 
 * @return id
 */
public String getIdentifier()

/**
 * Obtain the addition time
 * 
 * @return Time
 */
public long getAddTime()

/**
 * Obtain the source
 * 
 * @return Source
 */
public String getAddSource()

/**
 * Obtain friend request remarks
 * 
 * @return Friend request remarks
 */
public String getAddWording()

/**
 * Obtain the friend’s nickname
 * 
 * @return Nickname
 */
public String getNickname()

/**
 * Obtains the pending request type. See the constant defined in TIMPendencyType for more information.
 * 
 * @return Pending request type
 */
public int getType()
```

`TIMPendencyType` is defined as follows:
```
public class TIMPendencyType {
    /**
     * Pending requests from other users
     */
    public static final int TIM_PENDENCY_COME_IN    = 1;

    /**
     * Pending requests to other users
     */
    public static final int TIM_PENDENCY_SEND_OUT   = 2;

    /**
     * Pending requests from other users and pending requests to other users, which are valid only during fetching
     */
    public static final int TIM_PENDENCY_BOTH       = 3;

}
```


### Deleting pending requests
```
/**
 * Delete pending requests
 * 
 * @param pendencyType Pending request type. See TIMPendencyType for more information. Only pending requests of the TIM_PENDENCY_COME_IN and TIM_PENDENCY_SEND_OUT types can be deleted.
 * @param users ID list of pending users to be deleted
 * @param cb Callback
 */
public void deletePendency(int pendencyType, List<String> users, @NonNull TIMValueCallBack<List<TIMFriendResult>> cb)
```

### Reporting that a pending record is read
When a user fetches pending records, they can be set as read on the backend.
```
/**
 * Report that a pending record is read
 * 
 * @param timestamp Read timestamp. All messages prior to this timestamp are set to read.
 * @param cb Callback
 */
public void pendencyReport(long timestamp, @NonNull TIMCallBack cb)
```
After reporting, the returned count of unread records is changed when `getPendencyList` is called again.

## Blacklist

### Adding users to the blacklist

You can blacklist any user. If the user is your friend, after you blacklist the user, your friend relationship with the user is canceled and you cannot no longer receive any messages from the user.

```
/**
 * Add a user to the blacklist
 * 
 * @param users User list
 * @param cb Callback
 */
public void addBlackList(List<String> users, @NonNull TIMValueCallBack<List<TIMFriendResult>> cb)
```

### Deleting a user from the blacklist

```
/**
 * Delete a user from the blacklist
 * 
 * @param users User list
 * @param cb Callback
 */
public void deleteBlackList(List<String> users, @NonNull TIMValueCallBack<List<TIMFriendResult>> cb)
```

### Obtaining the blacklist

```
/**
 * Obtain the blacklist
 * 
 * @param cb Callback
 */
public void getBlackList(@NonNull TIMValueCallBack<List<TIMFriend>> cb)
```

## Friend List

### Creating a friend list

When creating a list, you can select users to be added to the list. A user can be added to multiple lists.

```
/**
 * Create a friend group
 * 
 * @param groupNames List of friend group names. The friend group to be created must be a new group that does not already exist.
 * @param identifiers Friends to be added to the friend group
 * @param cb Callback
 */
public void createFriendGroup(List<String> groupNames, List<String> identifiers, @NonNull TIMValueCallBack<List<TIMFriendResult>> cb)
```

### Deleting a friend group

```
/**
 * Delete a friend group
 * 
 * @param groupNames Name list of friend groups to be deleted
 * @param cb Callback
 */
public void deleteFriendGroup(List<String> groupNames, @NonNull TIMCallBack cb)
```

### Adding friends to a friend group

```
/**
 * Add friends to a friend group
 *
 * @param groupName Friend group name
 * @param identifiers List of friends to be added to the friend group
 * @param cb Callback
 */
public void addFriendsToFriendGroup(String groupName, List<String> identifiers, @NonNull TIMValueCallBack<List<TIMFriendResult>> cb)
```

### Deleting friends from a friend group

```
/**
 * Delete friends from a friend group
 * 
 * @param groupName Friend group name
 * @param identifiers Friends to be deleted from the friend group
 * @param cb Callback
 */
public void deleteFriendsFromFriendGroup(String groupName, List<String> identifiers, @NonNull TIMValueCallBack<List<TIMFriendResult>> cb)
```

### Renaming a friend group

```
/**
 * Rename a friend group
 * 
 * @param oldName  Original name of the friend group
 * @param newName  New name of the friend group
 * @param cb Callback
 */
public void renameFriendGroup(String oldName, String newName, @NonNull TIMCallBack cb)
```

### Obtaining a friend group

```
/**
 * Obtains a specified friend group. If ‘null’ is passed in, all friend groups are obtained.
 * @param groupNames Name list of friend groups to be obtained
 * @param cb Callback
 */
public void getFriendGroups(List<String> groupNames, @NonNull TIMValueCallBack<List<TIMFriendGroup>> cb)
```

## System Notifications for Relationship Chain Changes

In `TIMMessage`, `Elem` = `TIMSNSSystemElem` indicates a system notification for a relationship chain change.

```
/**
 * Message elements synchronized through backend push after relevant operations on relationship chains are completed
 *
 */
public class TIMSNSSystemElem extends TIMElem {
    private int subType = 0;
    
    // subType corresponds to TIMSNSSystemType.TIM_SNS_SYSTEM_ADD_FRIEND.
    private List<String> requestAddFriendUserList = new ArrayList<>();
    
    // subType corresponds to TIMSNSSystemType.TIM_SNS_SYSTEM_DEL_FRIEND.
    private List<String> delRequestAddFriendUserList = new ArrayList<>();
    
    // subType corresponds to TIMSNSSystemType.TIM_SNS_SYSTEM_ADD_BLACKLIST.
    private List<String> addBlacklistUserList = new ArrayList<>();
    
    // subType corresponds to TIMSNSSystemType.TIM_SNS_SYSTEM_DEL_BLACKLIST.
    private List<String> delBlacklistUserList = new ArrayList<>();

    // subType corresponds to TIMSNSSystemType.TIM_SNS_SYSTEM_ADD_FRIEND_REQ.
    private List<TIMFriendPendencyInfo> friendAddPendencyList = new ArrayList<>();
    
    // subType corresponds to TIMSNSSystemType.TIM_SNS_SYSTEM_DEL_FRIEND_REQ.
    private List<String> delFriendAddPendencyList = new ArrayList<>();
    
    // subType corresponds to TIMSNSSystemType.TIM_SNS_SYSTEM_SNS_PROFILE_CHANGE.
    private List<TIMSNSChangeInfo>  changeInfoList = new ArrayList<>();
		
    public TIMSNSSystemElem() { type = TIMElemType.SNSTips; }
    public int getSubType();	
    public List<String> getRequestAddFriendUserList();
    public List<String> getDelRequestAddFriendUserList();
    public List<String> getAddBlacklistUserList();
    public List<String> getDelBlacklistUserList();
    public List<TIMFriendPendencyInfo> getFriendAddPendencyList();
    public List<String> getDelFriendAddPendencyList();
    public List<TIMSNSChangeInfo> getChangeInfoList();
}


/**
 * System notification type for the relationship chain change
 */
public class TIMSNSSystemType {
    /**
     * Friend addition message
     */
    public static final int TIM_SNS_SYSTEM_ADD_FRIEND         = 0x01;

    /**
     * Friend deletion message
     */
    public static final int TIM_SNS_SYSTEM_DEL_FRIEND         = 0x02;

    /**
     * Add friend requests
     */
    public static final int TIM_SNS_SYSTEM_ADD_FRIEND_REQ     = 0x03;

    /**
     * Delete pending requests
     */
    public static final int TIM_SNS_SYSTEM_DEL_FRIEND_REQ     = 0x04;
		
		    /**
     * Add users to the blacklist
     */
    public static final int TIM_SNS_SYSTEM_ADD_BLACKLIST      = 0x05;

    /**
     * Delete users from the blacklist
     */
    public static final int TIM_SNS_SYSTEM_DEL_BLACKLIST      = 0x06;

    /**
     *  Report that a pending record is read
     */
    public static final int TIM_SNS_SYSTEM_PENDENCY_REPORT    = 0x07;

    /**
     *  Relationship chain information is changed
     */
    public static final int TIM_SNS_SYSTEM_SNS_PROFILE_CHANGE = 0x08;
};

/**
 * Details of the relationship chain change
 *
 */
public class TIMSNSChangeInfo {
    /**
     * User ID for the profile change
     */
    private String updateUser = "";

    /**
     * Profile change information
     */
    private Map<String, Object> itemMap = new HashMap<>();

    public String getUpdateUser() {
        return updateUser;
    }

    public Map<String, Object> getItemMap() {
        return itemMap;
    }
}
```

### System notifications for adding friends

When two users become friends, both of them receive a system message indicating that they have been added as friends.

**Triggering time:**

When your relationship chain changes by adding a friend, you will receive a message (if the friend is already a one-way friend, the party whose relationship chain does not change will not receive the message.)

**Parameter description:**

Parameter | Description
--- | ---
subType | TIM_SNS_SYSTEM_ADD_FRIEND 
requestAddFriendUserList | List of users who become friends 

### System notifications for deleting friends

When two users unfriend each other, they both receive a system message indicating that their friendship is canceled: 

**Triggering time:**

When your relationship chain changes by deleting a friend, you will receive a message (if the deleted friend is a one-way friend, the party whose relationship chain does not change will not receive the message.)

**Parameter description:**

Parameter | Description
--- | ---
subType | TIM_SNS_SYSTEM_DEL_FRIEND 
delRequestAddFriendUserList | List of deleted friends 

### System notifications for friend requests

When you send a friend request to a user and the user requires approval, both of you will receive a friend request system notification.

**Triggering time:**

When you send a friend request to a user and the user requires approval, both of you will receive a system notification for friend requests. The user can choose to approve or reject the request, whereas you cannot perform any operations. This is only for the purpose of information synchronization. 

**Parameter description:**

Parameter | Description
--- | ---
subType | TIM_SNS_SYSTEM_ADD_FRIEND_REQ 
friendAddPendencyList | List of pending friend requests

**`TIMFriendPendencyInfo` parameter description:**

Parameter | Description
--- | ---
fromUser | Friend addition operator
addSource | Friend addition source 
fromUserNickName | Nickname of the friend addition operator
addWording | Postscript to the friend request

### Notifications for deleting pending requests

**Triggering time:**

After your friend request to a user is approved or rejected, you will receive a message indicating that the pending request was deleted.

**Parameter description:**

Parameter | Description
--- | ---
subType | TIM_SNS_SYSTEM_DEL_FRIEND_REQ 
delFriendAddPendencyList | List of approved or rejected friend requests

## System Notifications for User Profile Changes

In `TIMMessage`, `Elem` = `TIMProfileSystemElem` indicates a system message for a user profile change.

```
/**
 * Message element synchronized by backend push after the modification of your own and the friend’s profiles
 */
public class TIMProfileSystemElem extends TIMElem {
    private int subType; //Profile modification type: TIMProfileSystemType
    private String fromUser; //Profile modification source (the modifier)
    private Map<String, Object> itemMap; //User’s profile
  
    public int getSubType();
    public String getFromUser();
    public Map<String, Object> getItemMap();
}

/**
 * System notification type for the user profile change
 */
public class TIMProfileSystemType {
    /**
     * Invalid value
     */
    public static final int INVALID = 0;
    
    /**
     * Friend profile change
     */
    public static final int TIM_PROFILE_SYSTEM_FRIEND_PROFILE_CHANGE = 1;
}

```

When your profile or a friend’s profile is modified, you will receive a system notification message indicating that the user profile is modified. For example, if a friend changes his or her profile photo, then in `TIMProfileSystemElem`, `key` in `itemMap` will be `Tag_Profile_IM_Image`, and `value` will be the `url` of the profile photo. The constant value of `key` is defined in `TIMUserProfile`.

