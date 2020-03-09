IM provides the relationship chain and user profile hosting features. App developers can use simple APIs to store relationship chains and user profiles. In addition, to facilitate profile customization for different users, IM also provides custom fields for user profiles and relationship chains (user custom fields need to be configured in the console in advance. For details, see [User Custom Fields](https://cloud.tencent.com/document/product/269/38656#.E7.94.A8.E6.88.B7.E8.87.AA.E5.AE.9A.E4.B9.89.E5.AD.97.E6.AE.B5).) APIs described in this section are valid for both independent and hosted accounts. 


## User Profiles

### Obtaining your own profile 

You can use the `getSelfProfile` method of `TIMFriendshipManager` to obtain your own profile.

```
/**
 *  Obtain your own profile
 *
 *  @param succ Success callback, which returns TIMUserProfile
 *  @param fail Failure callback
 *
 *  @return 0 Sent the request successfully
 */
- (int)getSelfProfile:(TIMGetProfileSucc)succ fail:(TIMFail)fail;
```

If the profile is successfully obtained, the succ callback returns the obtained `TIMUserProfile` object. `TIMUserProfile` is defined as follows:

```
/**
 *  User’s profile
 */
@interface TIMUserProfile : TIMCodingModel

/**
 *  User’s identifier
 */
@property(nonatomic,strong) NSString* identifier;

/**
 *  User’s nickname
 */
@property(nonatomic,strong) NSString* nickname;

/**
 *  Approval mode of friend requests
 */
@property(nonatomic,assign) TIMFriendAllowType allowType;

/**
 *  User’s profile photo
 */
@property(nonatomic,strong) NSString* faceURL;

/**
 *  User’s signature
 */
@property(nonatomic,strong) NSData* selfSignature;

/**
 *  User’s gender
 */
@property(nonatomic,assign) TIMGender gender;

/**
 *  User’s birthday
 */
@property(nonatomic,assign) uint32_t birthday;

/**
 *  User’s location
 */
@property(nonatomic,strong) NSData* location;

/**
 *  User’s language
 */
@property(nonatomic,assign) uint32_t language;

/**
 *  Level
 */
@property(nonatomic,assign) uint32_t level;

/**
 *  Role
 */
@property(nonatomic,assign) uint32_t role;

/**
 *  A collection of custom fields. Among them, key is of the NSString type, and value is of the NSData or NSNumber type.
 *  (The key value is determined based on the string configured on the backend.)
 */
@property(nonatomic,strong) NSDictionary* customInfo;

@end
```



### Obtaining a specified user’s profile

You can use the `getUsersProfile` method of `TIMFriendshipManager` to obtain a specified user’s profile. This method supports obtaining the profile from two sources: the cache and the backend. If forceUpdate = YES, data is forcibly fetched from the backend, and the returned data will be cached. If forceUpdate = NO, the system first searches for the data locally. If no local data can be found, it requests the data from the backend. We recommend that you forcibly fetch the data only for profile display to reduce the wait time.


```
/**
 *  Obtain a specified friend’s profile
 *
 *  @param users User ID
 *  @prarm forceUpdate Forcibly fetch data from the backend
 *  @param succ Success callback
 *  @param fail Failure callback
 *
 *  @return 0 Sent the request successfully
 */
- (int)getUsersProfile:(NSArray<NSString *> *)users forceUpdate:(BOOL)forceUpdate succ:(TIMGetProfileArraySucc)succ fail:(TIMFail)fail;
@end
```

Example: obtain the profiles of user [iOS_002] and user [iOS_003]

```
NSMutableArray * arr = [[NSMutableArray alloc] init];
[arr addObject:@"iOS_002"];
[arr addObject:@"iOS_003"];
[[TIMFriendshipManager sharedInstance] getUsersProfile:arr forceUpdate:NO succ:^(NSArray * arr) {
	for (TIMUserProfile * profile in arr) {
		NSLog(@"user=%@", profile);
	}
}fail:^(int code, NSString * err) {
	NSLog(@"GetFriendsProfile fail: code=%d err=%@", code, err);
}];
```

In this example, as forceUpdate is set to No, the system first searches for the users’ profiles in the cache to reduce the wait time. The caching period can be set in TIMFriendProfileOption and defaults to one day.
```
/**
 * Profiles and relationship chains
 */
@interface TIMFriendProfileOption : NSObject

/**
 * Maximum caching period for relationship chains
 * The default caching period is one day. If the time for obtaining profiles and relationship chains exceeds the caching period, the system automatically sends a request to the server.
 */
@property NSInteger expiredSeconds;

@end
```
The method for configuring the expiry time is `-[TIMManager setUserConfig:]`. Sample code:
```
TIMUserConfig *config = ...;
TIMFriendProfileOption *option = [TIMFriendProfileOption new];
option.expiredSeconds = 60*60; //1 hour
config.friendProfileOpt = option;
[[TIMManager sharedInstance] setUserConfig:config];
```

### Modifying your own profile

You can use the `modifySelfProfile` method to modify your own profile.
```
@interface TIMFriendshipManager : NSObject
/**
 *  Set your own profile
 *
 *  @param values Attributes to be updated. Multiple fields can be updated at a time.
 *  @param succ Success callback
 *  @param fail Failure callback
 *
 *  @return 0 Sent the request successfully
 */
- (int)modifySelfProfile:(NSDictionary<NSString *, id> *)values succ:(TIMSucc)succ fail:(TIMFail)fail;
@end
```
Through the values dictionary, you can set multiple fields at a time. For example, the code segment for setting the nickname is as follows:
```
[[TIMFriendshipManager sharedInstance] modifySelfProfile:@{TIMProfileTypeKey_Nick:@"My nickname"} succ:nil fail:nil];
```

Setting a key value that does not exist may lead to failure. The backend defines some common key values.

Key | Value | Description
--- | --- | --
TIMProfileTypeKey_Nick | NSString | Nickname 
TIMProfileTypeKey_FaceUrl | NSString | Profile photo 
TIMProfileTypeKey_AllowType | NSNumber | Friend request
TIMProfileTypeKey_Gender | NSNumber | Gender 
TIMProfileTypeKey_Birthday | NSNumber | Birthday 
TIMProfileTypeKey_Location | NSString | Location 
TIMProfileTypeKey_Language | NSNumber | Language
TIMProfileTypeKey_Level | NSNumber | Level 
TIMProfileTypeKey_Role | NSNumber | Role 
TIMProfileTypeKey_SelfSignature | NSString | Signature 
TIMProfileTypeKey_Custom_Prefix | NSString, NSData, or NSNumber | Prefix of the custom field

For custom fields, you need to add prefixes. For example, to set the `Blood` custom field of the integer type on the backend, use the following code:
```
NSString *key = [TIMProfileTypeKey_Custom_Prefix stringByAppendingString:@"Blood"];
[[TIMFriendshipManager sharedInstance] modifySelfProfile:@{key:@1} succ:nil fail:nil];
```
> If the custom field value is set to an NSString object, the backend converts it to a UTF8 object and saves it in the database. As some user profiles may be in non-UTF8 format during migration, the backend always returns the NSData type of profiles for profile obtaining requests.

## Friend Relationships

### Obtaining all friends

You can use the `getFriendList` method of `TIMFriendshipManager` to obtain the list of all friends.

```
@interface TIMFriendshipManager : NSObject
/**
 *  Obtain the friend list
 *
 *  @param succ Success callback, which returns the friend (TIMFriend) list. 
 *  @param fail Failure callback
 *
 *  @return 0 Sent the request successfully
 */
-(int)getFriendList:(TIMFriendArraySucc)succ fail:(TIMFail)fail;
@end
```

If the friend list is obtained successfully, the succ callback returns the friend list, and friend objects are stored in `TIMFriend`. `TIMFriend` is defined as follows:

```
@interface TIMFriend : TIMCodingModel

/**
 *  Friend’s identifier
 */
@property(nonatomic,strong) NSString *identifier;

/**
 *  Friend’s remarks
 */
@property(nonatomic,strong) NSString *remark;

/**
 *  Group name NSString* list
 */
@property(nonatomic,strong) NSArray *groups;

/**
 *  Request reason
 */
@property(nonatomic,strong) NSString * addWording;

/**
 *  Request source
 */
@property(nonatomic,strong) NSString * addSource;

/**
 *  Addition time
 */
@property(nonatomic,assign) uint64_t addTime;

/**
 * A collection of custom fields. Among them, key is of the NSString type, and value is of the NSData or NSNumber type. The key value is determined based on the string configured on the backend.
 */
@property(nonatomic,strong) NSDictionary* customInfo;

/**
 * Friend’s profile
 */
@property(nonatomic,strong) TIMUserProfile *profile;

@end
```

Sample code
```
[[TIMFriendshipManager sharedInstance] getFriendList:^(NSArray<TIMFriend *> *friends) {
    NSMutableString *msg = [NSMutableString new];
    [msg appendString:@"Friend list:"];
    for (TIMFriend *friend in friends) {
        [msg appendFormat:@"[%@,%@,%d,%@,%@,%@]", friend.identifier, friend.remark, friend.addTime, friend.addSource, friend.addWording, friend.groups];
    }
    self.msgLabel.text = msg;
} fail:^(int code, NSString *msg) {
    self.msgLabel.text = [NSString stringWithFormat:@"Failed: %d, %@", code, msg];
}];
```

### Modifying friends

The `modifyFriend` method can be called to modify friends. This method adopts the NSDictionary mode for modification, and multiple fields can be updated at a time.


```
@interface TIMFriendshipManager : NSObject
/**
 *  Modify friends
 *
 *  @param identifier Friend’s identifier
 *  @param values Attributes to be updated. Multiple fields can be updated at a time. See TIMFriendTypeKey_XXX of TIMFriendshipDefine.h for more information.
 *  @param succ Success callback
 *  @param fail Failure callback
 *
 *  @return 0 Sent the request successfully
 */
- (int)modifyFriend:(NSString *)identifier values:(NSDictionary<NSString *, id> *)values succ:(TIMSucc)succ fail:(TIMFail)fail;
@end
```

Setting a key value that does not exist may lead to failure. The backend defines some common key values.

Key | Value | Description
--- | --- | --
TIMFriendTypeKey_Remark | NSString | Remarks 
TIMFriendTypeKey_Group | NSArray | Group 
TIMFriendTypeKey_Custom_Prefix | NSNumber, NSData | Prefix of the custom field


Example: set the remarks of friend [iOS_002] to [002 remark] 

```
[[TIMFriendshipManager sharedInstance] modifyFriend:@"iOS_002" values:@{ TIMFriendTypeKey_Remark: @"002 remark"} succ:^{
    self.msgLabel.text = @"OK";
} fail:^(int code, NSString *msg) {
    self.msgLabel.text = [NSString stringWithFormat:@"Failed: %d, %@", code, msg];
}];
```

> To modify a friend’s custom information, you must first configure relationship chain custom fields on the server.


### Adding friends

You can use the `addFriend` method of `TIMFriendshipManager` to add friends. 

```
@interface TIMFriendshipManager : NSObject

/**
 *  Add a friend
 *
 *  @param request Friend request
 *  @param succ Success callback (TIMFriendResult)
 *  @param fail Failure callback
 *
 *  @return 0 Sent the request successfully
 */
- (int)addFriend:(TIMFriendRequest *)request succ:(TIMFriendResultSucc)succ fail:(TIMFail)fail;

@end
```

To add a friend, the request parameter needs to be passed in. Its parameter type is defined as follows:
```
/**
 *  Friend request
 */
@interface TIMFriendRequest : TIMCodingModel

/**
 *  User’s identifier
 */
@property(nonatomic,strong) NSString* identifier;

/**
 *  User’s remarks (a maximum of 96 bytes)
 */
@property(nonatomic,strong) NSString* remark;

/**
 *  Request description (a maximum of 120 bytes)
 */
@property(nonatomic,strong) NSString* addWording;

/**
 *  Friend addition source
 *  The source cannot exceed 8 bytes and must be prefixed with "AddSource_Type_".
 */
@property(nonatomic,strong) NSString* addSource;

/**
 *  Group name
 */
@property(nonatomic,strong) NSString* group;

@end
```


The success callback returns the `TIMFriendResult` result for the operating user. Developers can notify the user accordingly. The return codes for adding friends are as follows:

```
typedef NS_ENUM(NSInteger, TIMFriendStatus) {
    /**
     *  Operation succeeded
     */
    TIM_FRIEND_STATUS_SUCC                              = 0,
    /**
     *  Valid for adding friends: the peer is in your blacklist.
     */
    TIM_ADD_FRIEND_STATUS_IN_SELF_BLACK_LIST                = 30515,
    /**
     *  Valid for adding friends: the peer has forbidden friend requests.
     */
    TIM_ADD_FRIEND_STATUS_FRIEND_SIDE_FORBID_ADD            = 30516,
    /**
     *  Valid for adding friends and responding to friends: your number of friends has reached the limit of the system.
     */
    TIM_ADD_FRIEND_STATUS_SELF_FRIEND_FULL                  = 30010,     
    /**
     *  Valid for adding friends: the peer has blacklisted you.
     */
    TIM_ADD_FRIEND_STATUS_IN_OTHER_SIDE_BLACK_LIST          = 30525,    
    /**
     *  Valid for adding friends: the friend request is pending approval.
     */
    TIM_ADD_FRIEND_STATUS_PENDING                           = 30539,
};
```

Sample code

```
TIMFriendRequest *q = [TIMFriendRequest new];
q.identifier = @"abc"; // Add abc as a friend
q.addWording = @"Please approve my request";
q.addSource = @"AddSource_Type_iOS";
q.remark = @"You are abc";
[[TIMFriendshipManager sharedInstance] addFriend:q succ:^(TIMFriendResult *result) {
    if (result.result_code == 0)
        self.msgLabel.text = @"Added as a friend successfully";
    else
        self.msgLabel.text = [NSString stringWithFormat:@"Exception: %ld, %@", (long)result.result_code, result.result_info];
} fail:^(int code, NSString *msg) {
    self.msgLabel.text = [NSString stringWithFormat:@"Failed: %d, %@", code, msg];
}];
```

### Deleting friends

You can use the `deleteFriends` method of `TIMFriendshipManager` to delete friends in batches. 

```
@interface TIMFriendshipManager : NSObject
/**
 *  Delete friends
 *
 *  @param user Identifiers of friends to be deleted
 *  @param delType Type of friends to be deleted (one-way or two-way)
 *  @param succ Success callback ([TIMFriendResult])
 *  @param fail Failure callback
 *
 *  @return 0 Sent the request successfully
 */
- (int)delFriend:(NSString *)user delType:(TIMDelFriendType)delType succ:(TIMHandleFriendArraySucc)succ fail:(TIMFail)fail;
@end
```

The success callback returns the `TIMFriendResult` result for the operating user. Developers can notify the user accordingly. The error codes for deleting friends are as follows:

```
typedef NS_ENUM(NSInteger, TIMFriendStatus) {
    /**
     *  Operation succeeded
     */
    TIM_FRIEND_STATUS_SUCC                              = 0,
    /**
     *  Valid for deleting friends: the friend that you want to delete is not your friend.
     */
    TIM_DEL_FRIEND_STATUS_NO_FRIEND                         = 31704,
};
```

Sample code

```
NSMutableArray * del_users = [[NSMutableArray alloc] init];
// Delete friend iOS_002
[del_users addObject:@"iOS_002"];
// TIM_FRIEND_DEL_BOTH indicates deleting two-way friends.
[[TIMFriendshipManager sharedInstance] deleteFriends:del_users delType:TIM_FRIEND_DEL_BOTH succ:^(NSArray<TIMFriendResult *> *results) {
	for (TIMFriendResult * res in results) {
		if (res.result_code != TIM_FRIEND_STATUS_SUCC) {
			NSLog(@"deleteFriends failed: user=%@ result_code=%d", res.identifier, res.result_code);
		}
		else {
			NSLog(@"deleteFriends succ: user=%@ result_code=%d", res.identifier, res.result_code);
		}
	}
} fail:^(int code, NSString * err) {
	NSLog(@"deleteFriends failed: code=%d err=%@", code, err);
}];
```

### Approving/Rejecting a friend request

You can use the `doResponse` method of `TIMFriendshipManager` to approve or reject friend requests.

```
@interface TIMFriendshipManager : NSObject
/**
 *  Respond to a friend request
 *
 *  @param response Response to the request
 *  @param succ Success callback
 *  @param fail Failure callback
 *
 *  @return 0 Sent the request successfully
 */
- (int)doResponse:(TIMFriendResponse *)response succ:(TIMFriendResultSucc)succ fail:(TIMFail)fail;
@end
```
The `response` parameter is defined as follows:
```
typedef NS_ENUM(NSInteger, TIMFriendResponseType) {
    /**
     *  Approve the friend request (establish a one-way friendship)
     */
    TIM_FRIEND_RESPONSE_AGREE                       = 0,    
    /**
     *  Approve the friend request and add the friend (establish a two-way friendship)
     */
    TIM_FRIEND_RESPONSE_AGREE_AND_ADD               = 1,    
    /**
     *  Reject the friend request
     */
    TIM_FRIEND_RESPONSE_REJECT                      = 2,
};
/**
 * Respond to the friend request
 */
@interface TIMFriendResponse : NSObject

/**
 *  Response type
 */
@property(nonatomic,assign) TIMFriendResponseType responseType;

/**
 *  User’s identifier
 */
@property(nonatomic,strong) NSString* identifier;

/**
 * Friend remarks (optional). You can add remarks if you want to add the user as a friend. The maximum length of the remarks is 96 bytes.
 */
@property(nonatomic,strong) NSString* remark;

@end
```

The success callback returns the `TIMFriendResult` result for the operating user. The error codes for handling friend requests are as follows:
```
typedef NS_ENUM(NSInteger, TIMFriendStatus) {
    /**
     *  Operation succeeded
     */
    TIM_FRIEND_STATUS_SUCC                              = 0,  
    /**
     *  Valid for responding to friend requests: the user has not requested to add you as a friend.
     */
    TIM_RESPONSE_FRIEND_STATUS_NO_REQ                       = 30614,   
    /**
     *  Valid for adding friends and responding to friends: your number of friends has reached the limit of the system.
     */
    TIM_ADD_FRIEND_STATUS_SELF_FRIEND_FULL                  = 30010,      
    /**
     *  Valid for adding friends and responding to friends: the user’s number of friends has reached the limit of the system.
     */
    TIM_ADD_FRIEND_STATUS_THEIR_FRIEND_FULL                 = 30014,
};
```

### Verifying friend relationships

You can use the `checkFriends` method of `TIMFriendshipManager` to verify friend relationships.

```
/**
 *  Check your friend relationship with a specified user
 *
 *  @param checkInfo Friendship check information
 *  @param succ Success callback, which returns the check result
 *  @param fail Failure callback
 *
 *  @return 0 Sent successfully
 */
- (int)checkFriends:(TIMFriendCheckInfo *)checkInfo succ:(TIMCheckFriendResultArraySucc)succ fail:(TIMFail)fail;
```

The `checkInfo` parameter is defined as follows:

```
/**
 *  Friend relationship check
 */
@interface TIMFriendCheckInfo : NSObject
/**
 *  ID list of the users to be checked (NSString*)
 */
@property(nonatomic,strong) NSArray* users;

/**
 *  Check type
 */
@property(nonatomic,assign) TIMFriendCheckType checkType;

@end
```

The `TIMFriendCheckType` parameter is defined as follows:

```
/**
 *  Friend check type
 */
typedef NS_ENUM(NSInteger,TIMFriendCheckType) {
    /**
     *  One-way friend
     */
    TIM_FRIEND_CHECK_TYPE_UNIDIRECTION     = 0x1,
    /**
     *  You are friends of each other.
     */
    TIM_FRIEND_CHECK_TYPE_BIDIRECTION      = 0x2,
};
```

The success callback returns the `TIMCheckFriendResult` list for the operating user. This parameter is defined as follows:

```
@interface TIMCheckFriendResult : NSObject
/**
 *  User ID
 */
@property NSString* identifier;

/**
 * Return code
 */
@property NSInteger result_code;

/**
 * Return information
 */
@property NSString *result_info;

/**
 *  Check result
 */
@property(nonatomic,assign) TIMFriendRelationType resultType;

@end
```

The `TIMFriendRelationType` parameter is defined as follows:

```
/**
 *  Friend relationship type
 */
typedef NS_ENUM(NSInteger,TIMFriendRelationType) {
    /**
     *  You are not friends.
     */
    TIM_FRIEND_RELATION_TYPE_NONE           = 0x0,
    /**
     *  The user is in my friend list.
     */
    TIM_FRIEND_RELATION_TYPE_MY_UNI         = 0x1,
    /**
     *  I am in the user’s friend list.
     */
    TIM_FRIEND_RELATION_TYPE_OTHER_UNI      = 0x2,
    /**
     *  You are friends of each other.
     */
    TIM_FRIEND_RELATION_TYPE_BOTHWAY        = 0x3,
};
```

## Pending Friend Requests

### Obtaining the pending request list
When another user uses the `addFriend` method to request to add you as a friend, a pending record is added on the backend. When you request to add another user as a friend, a pending record is also added on the backend. You can use the `getPendencyList` method to obtain the pending request list.
```
@interface TIMFriendshipManager : NSObject

/**
 *  Obtain the pending request list
 *
 *  @param pendencyRequest Request information. For details, see TIMFriendPendencyRequest.
 *  @param succ Success callback
 *  @param fail Failure callback
 *
 *  @return 0 Sent the request successfully
 */
- (int)getPendencyList:(TIMFriendPendencyRequest *)pendencyRequest succ:(TIMGetFriendPendencyListSucc)succ fail:(TIMFail)fail;
@end
```
As the backend may store multiple pending friend requests that go beyond the display scope of the interface, the API supports paging up and down. In this case, the `pendencyRequest` parameter needs to be passed in. Its definition is as follows:
```
/**
 * Pending request information
 */
@interface TIMFriendPendencyRequest : TIMCodingModel

/**
 * Sequence number of the pending request list
 * We recommend that you save the sequence number and pending request list on the client. The sequence number returned by the server is entered during requests.
 * If the sequence number is the latest on the server, no data is returned.
 */
@property(nonatomic,assign) uint64_t seq;

/**
 * Paging timestamp, which is only used for paging up or down. If the server returns 0, it indicates that no more data is available. Enter 0 for the first request.
 * Note that if the seq returned by the server is different from the entered seq, use the original seq request on the client for paging up or down. The local seq is not updated until the data request is completed.
 */
@property(nonatomic,assign) uint64_t timestamp;

/**
 * Number of data entries per page, that is, the maximum number of returned data entries per request
 */
@property(nonatomic,assign) uint64_t numPerPage;

/**
 * Pending request fetch type
 */
@property(nonatomic,assign) TIMPendencyGetType type;

@end
```
After the operation succeeds, the succ callback returns paging information and pending records.
```
/**
 * Returned pending information
 */
@interface TIMFriendPendencyResponse : TIMCodingModel

/**
 * Sequence number of the pending request list for the current request
 */
@property(nonatomic,assign) uint64_t seq;

/**
 * Paging timestamp for the current request
 */
@property(nonatomic,assign) uint64_t timestamp;

/**
 * Number of unread pending requests
 */
@property(nonatomic,assign) uint64_t unreadCnt;

@end
```

```
/**
 * Pending request
 */
@interface TIMFriendPendencyItem : TIMCodingModel

/**
 * User’s identifier
 */
@property(nonatomic,strong) NSString* identifier;
/**
 * Addition time
 */
@property(nonatomic,assign) uint64_t addTime;
/**
 * Source
 */
@property(nonatomic,strong) NSString* addSource;
/**
 * Friend request postscript
 */
@property(nonatomic,strong) NSString* addWording;

/**
 * Friend request nickname
 */
@property(nonatomic,strong) NSString* nickname;

/**
 * Pending request type
 */
@property(nonatomic,assign) TIMPendencyGetType type;

@end
```

### Deleting pending requests
```
@interface TIMFriendshipManager : NSObject
/**
 *  Delete pending requests
 *
 *  @param type Type of the pending friend request
 *  @param identifiers Pending request list to be deleted
 *  @param succ Success callback
 *  @param fail Failure callback
 *
 *  @return 0 Sent the request successfully
 */
- (int)deletePendency:(TIMPendencyGetType)type users:(NSArray *)identifiers succ:(TIMSucc)succ fail:(TIMFail)fail;
@end 
```

### Reporting that a pending record is read
When users fetch pending records, the pending records can be set as read on the backend.
```
@interface TIMFriendshipManager : NSObject
/**
 *  Report that a pending record is read
 *
 *  @param timestamp Read timestamp. All messages prior to this timestamp are set as read.
 *  @param succ Success callback
 *  @param fail Failure callback
 *
 *  @return 0 Sent the request successfully
 */
- (int)pendencyReport:(uint64_t)timestamp succ:(TIMSucc)succ fail:(TIMFail)fail;
@end
```
After reporting, the number of returned unread records is changed when `getPendencyList` is called again.



## Blacklist

### Adding users to the blacklist

You can blacklist any user. If the user is your friend, after you blacklist the user, your friend relationship with the user is canceled and you can no longer receive any messages from the user.

```
@interface TIMFriendshipManager : NSObject
/**
 *  Add users to the blacklist
 *
 *  @param identifiers User list
 *  @param succ Success callback
 *  @param fail Failure callback
 *
 *  @return 0 Sent the request successfully
 */
- (int)addBlackList:(NSArray *)identifiers succ:(TIMFriendResultArraySucc)succ fail:(TIMFail)fail;
@end
```


### Deleting a user from the blacklist

```
@interface TIMFriendshipManager : NSObject
/**
 *  Delete a user from the blacklist
 *
 *  @param identifiers User list
 *  @param succ Success callback
 *  @param fail Failure callback
 *
 *  @return 0 Sent the request successfully
 */
- (int)deleteBlackList:(NSArray *)identifiers succ:(TIMFriendResultArraySucc)succ fail:(TIMFail)fail;
@end
```


### Obtaining the blacklist

```
@interface TIMFriendshipManager : NSObject
/**
 *  Obtain the blacklist
 *
 *  @param succ Success callback, which returns the NSString* list
 *  @param fail Failure callback
 *
 *  @return 0 Sent the request successfully
 */
- (int)getBlackList:(TIMFriendArraySucc)succ fail:(TIMFail)fail;
@end
```


## Friend Groups

### Creating a friend group

When creating a group, you can select the users to be added to the group. A user can be added to multiple groups.

```
/**
 *  Create a friend group
 *
 *  @param groupNames List of friend group names. It must be a new friend group that does not already exist.
 *  @param identifiers Friends to be added to the friend group
 *  @param succ Success callback
 *  @param fail Failure callback
 *
 *  @return 0 Sent the request successfully
 */
- (int)createFriendGroup:(NSArray *)groupNames users:(NSArray *)identifiers succ:(TIMFriendResultArraySucc)succ fail:(TIMFail)fail;
@end
```

### Deleting a friend group

```
@interface TIMFriendshipManager : NSObject
/**
 *  Delete a friend group
 *
 *  @param groupNames Name list of friend groups to be deleted
 *  @param succ Success callback
 *  @param fail Failure callback
 *
 *  @return 0 Sent the request successfully
 */
- (int)deleteFriendGroup:(NSArray *)groupNames succ:(TIMSucc)succ fail:(TIMFail)fail;
@end
```


### Adding friends to a friend group

```
@interface TIMFriendshipManager : NSObject
/**
 *  Add friends to a friend group
 *
 *  @param groupName Friend group name
 *  @param identifiers Friends to be added to the friend group
 *  @param succ Success callback
 *  @param fail Failure callback
 *
 *  @return 0 Sent the request successfully
 */
- (int)addFriendsToFriendGroup:(NSString *)groupName users:(NSArray *)identifiers succ:(TIMFriendResultArraySucc)succ fail:(TIMFail)fail;
@end
```


### Deleting friends from a friend group


```
@interface TIMFriendshipManager : NSObject
/**
 *  Delete friends from a friend group
 *
 *  @param groupName Friend group name
 *  @param identifiers Friends to be deleted from the friend group
 *  @param succ Success callback
 *  @param fail Failure callback
 *
 *  @return 0 Sent the request successfully
 */
- (int)delFriendsFromFriendGroup:(NSString *)groupName users:(NSArray *)identifiers succ:(TIMFriendResultArraySucc)succ fail:(TIMFail)fail;
@end
```


### Renaming a friend group

```
@interface TIMFriendshipManager : NSObject
/**
 *  Changes the name of a friend group
 *
 *  @param oldName Original name of the friend group
 *  @param newName New name of the friend group
 *  @param succ Success callback
 *  @param fail Failure callback
 *
 *  @return 0 Sent the request successfully
 */
- (int)renameFriendGroup:(NSString*)oldName newName:(NSString*)newName succ:(TIMSucc)succ fail:(TIMFail)fail;
@end
```


### Obtaining a specified friend group

```
@interface TIMFriendshipManager : NSObject
/**
 *  Obtain a specified friend group
 *
 *  @param groupNames Name list of friend groups to be obtained. If ‘null’ is passed in, all friend groups are obtained.
 *  @param succ Success callback, which returns the TIMFriendGroup* list
 *  @param fail Failure callback
 *
 *  @return 0 Sent the request successfully
 */
- (int)getFriendGroups:(NSArray *)groupNames succ:(TIMFriendGroupArraySucc)succ fail:(TIMFail)fail;
@end
```


## System Notifications for Relationship Chain Changes

In `TIMMessage`, `Elem` = `TIMSNSSystemElem` indicates a system notification for a relationship chain change.

**Prototype:**

```
typedef NS_ENUM(NSInteger, TIM_SNS_SYSTEM_TYPE){
    /**
     *  Friend addition message
     */
    TIM_SNS_SYSTEM_ADD_FRIEND                           = 0x01,
    /**
     *  Friend deletion message
     */
    TIM_SNS_SYSTEM_DEL_FRIEND                           = 0x02,
    /**
     *  Adding friend requests
     */
    TIM_SNS_SYSTEM_ADD_FRIEND_REQ                       = 0x03,
    /**
     *  Deleting pending requests
     */
    TIM_SNS_SYSTEM_DEL_FRIEND_REQ                       = 0x04,
};
/**
 * Details of the relationship chain change
 */
@interface TIMSNSChangeInfo : NSObject
/**
 *  User’s identifier
 */
@property(nonatomic,retain) NSString * identifier;
/**
 *  Valid for friend requests: reason for adding the user as a friend
 */
@property(nonatomic,retain) NSString * wording;
/**
 *  Entered for friend requests: user addition source
 */
@property(nonatomic,retain) NSString * source;
@end
/**
 *  Relationship chain change message
 */
@interface TIMSNSSystemElem : TIMElem
/**
 * Operation type
 */
@property(nonatomic,assign) TIM_SNS_SYSTEM_TYPE type;
/**
 * List of operated users: TIMSNSChangeInfo List
 */
@property(nonatomic,retain) NSArray * users;

@end
```

**Member description:**

Member | Description
--- | ---
type | Change type 
users | List of updated users 

In this example, when a user friends or unfriends another user, a log is printed. When a user requests to friend another user, the request reason is printed. **Example:**

```
@interface TIMMessageListenerImpl : NSObject
- (void)onNewMessage:(NSArray*) msgs;
@end
@implementation TIMMessageListenerImpl
- (void)onNewMessage:(NSArray*) msgs {
    for (TIMMessage * msg in msgs) {
		for (int i = 0; i < [msg elemCount]; i++) {
            TIMElem * elem = [msg getElem:i];
            if ([elem isKindOfClass:[TIMSNSSystemElem class]]) {
                TIMSNSSystemElem * system_elem = (TIMSNSSystemElem * )elem;
                switch ([system_elem type]) {
                    case TIM_SNS_SYSTEM_ADD_FRIEND:
                        for (TIMSNSChangeInfo * info in [system_elem users]) {
                            NSLog(@"user %@ become friends", [info identifier]);
                        }
                        break;
                    case TIM_SNS_SYSTEM_DEL_FRIEND:
                        for (TIMSNSChangeInfo * info in [system_elem users]) {
                            NSLog(@"user %@ delete friends", [info identifier]);
                        }
                        break;
                    case TIM_SNS_SYSTEM_ADD_FRIEND_REQ:
                        for (TIMSNSChangeInfo * info in [system_elem users]) {
                            NSLog(@"user %@ request friends: reason=%@", [info identifier], [info wording]);
                        }
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
TIMMessageListenerImpl * impl = [[TIMMessageListenerImpl alloc] init];
[[TIMManager sharedInstance] setMessageListener:impl];
[[TIMManager sharedInstance] initSdk];
TIMLoginParam * login_param = [[TIMLoginParam alloc ]init];
login_param.accountType = @"107";
login_param.identifier = @"iOS_001";
login_param.userSig = @"";
login_param.appidAt3rd = @"123456";
login_param.sdkAppId = 123456;
[[TIMManager sharedInstance] login: login_param succ:^(){
 NSLog(@"login succ");
} fail:^(int code, NSString * err) {
 NSLog(@"login failed: %d->%@", code, err);
}];
```

### System notifications for adding friends

When two users become friends, both of them will receive a system message indicating that they have been added as friends.

**Triggering time:**

When your relationship chain changes by adding a friend, you will receive a message (if the friend is already a one-way friend, the party whose relationship chain does not change will not receive the message.)

**Parameter description:**

Parameter | Description
--- | ---
type | TIM_SNS_SYSTEM_ADD_FRIEND 
users | List of users who become friends 

**`TIMSNSChangeInfo` parameter description:**

Member | Description
--- | ---
identifier | User’s identifier 

### System notifications for deleting friends

When two users unfriend each other, both of them will receive a system message indicating the friend deletion: 

**Triggering time:**

When your relationship chain changes by deleting a friend, you will receive a message (if the deleted friend is a one-way friend, the party whose relationship chain does not change will not receive the message.)

**Parameter description:**

Parameter | Description
type | TIM_SNS_SYSTEM_DEL_FRIEND 
users | List of friends to be deleted 

**`TIMSNSChangeInfo` parameter description:**

Member | Description
--- | ---
identifier | User’s identifier 

### System notifications for friend requests

When you send a friend request to a user and the user requires approval, both of you will receive a friend request system notification.

**Triggering time:** When you send a friend request to a user and the user requires approval, both of you will receive a system notification for friend requests. The user can choose to approve or reject the request, whereas you cannot perform any operations. This is only for the purpose of information synchronization. 

**Parameter description:**

Parameter | Description
--- | ---
type | TIM_SNS_SYSTEM_ADD_FRIEND_REQ 
users | List of friend requests 

**`TIMSNSChangeInfo` parameter description:**

Parameter | Description
--- | ---
identifier | User’s identifier 
wording | Request reason 
source | Request source

### Notifications for deleting pending requests

**Triggering time:** After your friend request to a user is approved or rejected, you will receive a message indicating that the pending request was deleted. 

## System Notifications for User Profile Changes

In `TIMMessage`, `Elem` = `TIMProfileSystemElem` indicates a system message for a user profile change.

```
/**
 * Message element synchronized by backend push after the modification of your own and friend’s profiles
 */
@interface TIMProfileSystemElem : TIMElem
/**
 *  Change type
 */
@property(nonatomic,assign) TIM_PROFILE_SYSTEM_TYPE type;
/**
 *  User whose profile is modified
 */
@property(nonatomic,strong) NSString * fromUser;
/**
 *  Nickname of the modified profile (currently unavailable)
 */
@property(nonatomic,strong) NSString * nickName;
@end
/**
 *  Profile change
 */
typedef NS_ENUM(NSInteger, TIM_PROFILE_SYSTEM_TYPE){
    /**
     Friend profile change
     */
    TIM_PROFILE_SYSTEM_FRIEND_PROFILE_CHANGE        = 0x01,
};
```

When your profile or a friend’s profile is modified, you will receive a system notification message indicating that a user profile change occurred. 
