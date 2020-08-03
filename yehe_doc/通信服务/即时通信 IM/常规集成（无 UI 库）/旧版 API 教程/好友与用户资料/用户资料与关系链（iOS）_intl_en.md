Instant Messaging (IM) provides the relationship chain and user profile hosting features. App developers can use simple APIs to store relationship chains and user profiles. In addition, to allow users conveniently customize profiles, IM also provides custom fields for user profiles and relationship chains. These fields must be configured in the console in advance. For more information, see [User Custom Fields](https://intl.cloud.tencent.com/document/product/1047/34419). The APIs described in this document are valid for both independent accounts and hosted accounts. 


## User Profile

### Obtaining your own profile 

You can use the `getSelfProfile` method of `TIMFriendshipManager` to obtain your own profile.

```
/**
 *  Obtaining your own profile
 *
 *  @param succ  Success callback. TIMUserProfile is returned.
 *  @param fail  Failure callback
 *
 *  @return 0 The request was sent successfully.
 */
- (int)getSelfProfile:(TIMGetProfileSucc)succ fail:(TIMFail)fail;
```

If the profile is obtained successfully, the succ callback returns the obtained `TIMUserProfile` object. `TIMUserProfile` is defined as follows:

```
/**
 *  User's profile
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
 *  Friend request approval mode
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
 *  User's location
 */
@property(nonatomic,strong) NSData* location;

/**
 *  User's language
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
 *  A set of custom fields. Key is of the NSString type, and value is of the NSData type or NSNumber type.
 *  (The key value is determined based on the character string configured on the backend.)
 */
@property(nonatomic,strong) NSDictionary* customInfo;

@end
```



### Obtaining the profile of a specified user

You can use the `getUsersProfile` method of `TIMFriendshipManager` to obtain the profile of a specified user. This method supports obtaining the profile from two sources: the cache and the backend. If forceUpdate = YES, data is fetched forcibly from the backend, and the returned data is cached. If forceUpdate = NO, the system first searches for the data locally. If no data is found locally, it requests data from the backend. We recommend that data be forcibly fetched only for profile display, thus reducing the wait time.


```
/**
 *  Obtain the profile of a specified friend
 *
 *  @param users User ID
 *  @prarm forceUpdate Forcibly fetches data from the backend
 *  @param succ  Success callback
 *  @param fail   Failure callback
 *
 *  @return 0 The request was sent successfully.
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

In this example, as forceUpdate is set to No, the system first searches for the two users’ profiles in the cache, thus reducing the wait time. The cache time is specified by TIMFriendProfileOption, and is 1 day by default.
```
/**
 * Profiles and relationship chains
 */
@interface TIMFriendProfileOption : NSObject

/**
 * Maximum cache time for relationship chains
 * The default cache time is 1 day. If the time used for obtaining profiles and relationship chains exceeds the cache time, the system automatically sends a request to the server.
 */
@property NSInteger expiredSeconds;

@end
```
The method for configuring the expiry time is `-[TIMManager setUserConfig:]`. Sample code:
```
TIMUserConfig *config = ...;
TIMFriendProfileOption *option = [TIMFriendProfileOption new];
option.expiredSeconds = 60*60; // 1 hour
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
 *  @param values    Attributes to be updated. Multiple fields can be updated at a time.
 *  @param succ  Success callback
 *  @param fail   Failure callback
 *
 *  @return 0 The request was sent successfully.
 */
- (int)modifySelfProfile:(NSDictionary<NSString *, id> *)values succ:(TIMSucc)succ fail:(TIMFail)fail;
@end
```
Through the values dictionary, you can set multiple fields at a time. For example, the code for setting the nickname is as follows:
```
[[TIMFriendshipManager sharedInstance] modifySelfProfile:@{TIMProfileTypeKey_Nick:@"My nickname"} succ:nil fail:nil];
```

Setting a non-existing key value may lead to a failure. The backend defines some common key values.

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
TIMProfileTypeKey_Custom_Prefix | NSString, NSData, or NSNumber | Custom field prefix

For custom fields, you need to add our prefixes. For example, if you want to set a custom field `Blood` of the integer type on the backend, the code is as follows:
```
NSString *key = [TIMProfileTypeKey_Custom_Prefix stringByAppendingString:@"Blood"];
[[TIMFriendshipManager sharedInstance] modifySelfProfile:@{key:@1} succ:nil fail:nil];
```
> If the custom field value is set to an NSString object, the backend converts it into a UTF8 object and saves it in the database. Because some migrated user profiles may not use the UTF8 format, the backend always returns the NSData type of the profile for profile requests.

## Friend Relationships

### Obtaining all friends

You can use the `getFriendList` method of `TIMFriendshipManager` to obtain the list of all friends.

```
@interface TIMFriendshipManager : NSObject
/**
 *  Obtain the friend list
 *
 *  @param succ Success callback. The friend (TIMFriend) list was returned. 
 *  @param fail   Failure callback
 *
 *  @return 0 The request was sent successfully.
 */
-(int)getFriendList:(TIMFriendArraySucc)succ fail:(TIMFail)fail;
@end
```

If the friend list is obtained successfully, the succ callback returns the friend list, and friend objects are stored in `TIMFriend`. `TIMFriend` is defined as follows:

```
@interface TIMFriend : TIMCodingModel

/**
 *  Friend identifier
 */
@property(nonatomic,strong) NSString *identifier;

/**
 *  Friend remark
 */
@property(nonatomic,strong) NSString *remark;

/**
 *  Friend list name NSString* list
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
 *  Creation time
 */
@property(nonatomic,assign) uint64_t addTime;

/**
 * A set of custom fields. `key` is of the NSString type, and `value` is of the NSData type or NSNumber type. The key value is determined based on the character string configured on the backend.
 */
@property(nonatomic,strong) NSDictionary* customInfo;

/**
 * Friend profile
 */
@property(nonatomic,strong) TIMUserProfile *profile;

@end
```

Sample code
```
[[TIMFriendshipManager sharedInstance] getFriendList:^(NSArray<TIMFriend *> *friends) {
    NSMutableString *msg = [NSMutableString new];
    [msg appendString:@"Friend list: "];
    for (TIMFriend *friend in friends) {
        [msg appendFormat:@"[%@,%@,%d,%@,%@,%@]", friend.identifier, friend.remark, friend.addTime, friend.addSource, friend.addWording, friend.groups];
    }
    self.msgLabel.text = msg;
} fail:^(int code, NSString *msg) {
    self.msgLabel.text = [NSString stringWithFormat:@"Failed: %d, %@", code, msg];
}];
```

### Modifying a friend

You can use the `modifyFriend` method to modify a friend's profile, which is similar to the method for modifying your own profile. This method adopts the NSDictionary mode for modification, and multiple fields can be updated at a time.


```
@interface TIMFriendshipManager : NSObject
/**
 *  Modify a friend
 *
 *  @param identifier Friend’s identifier
 *  @param values  Attributes to be updated. Multiple fields can be updated at a time. For more information, see TIMFriendTypeKey_XXX of TIMFriendshipDefine.h.
 *  @param succ  Success callback
 *  @param fail   Failure callback
 *
 *  @return 0 The request was sent successfully.
 */
- (int)modifyFriend:(NSString *)identifier values:(NSDictionary<NSString *, id> *)values succ:(TIMSucc)succ fail:(TIMFail)fail;
@end
```

Setting a non-existing key value may lead to a failure. The backend defines some common key values.

Key | Value | Description
--- | --- | --
TIMFriendTypeKey_Remark | NSString | Remarks 
TIMFriendTypeKey_Group | NSArray | Friend list 
TIMFriendTypeKey_Custom_Prefix | NSNumber, NSData | Custom field prefix


Example: set the remark of friend [iOS_002] to [002 remark] 

```
[[TIMFriendshipManager sharedInstance] modifyFriend:@"iOS_002" values:@{ TIMFriendTypeKey_Remark: @"002 remark"} succ:^{
    self.msgLabel.text = @"OK";
} fail:^(int code, NSString *msg) {
    self.msgLabel.text = [NSString stringWithFormat:@"Failed: %d, %@", code, msg];
}];
```

> To modify a friend’s custom information, you need to first configure the relationship chain custom fields on the server.


### Adding a friend

You can use the `addFriend` method of `TIMFriendshipManager` to add a friend. 

```
@interface TIMFriendshipManager : NSObject

/**
 * Add a friend
 *
 *  @param request  Friend request
 *  @param succ  Success callback (TIMFriendResult)
 *  @param fail  Failure callback
 *
 *  @return 0 The request was sent successfully.
 */
- (int)addFriend:(TIMFriendRequest *)request succ:(TIMFriendResultSucc)succ fail:(TIMFail)fail;

@end
```

The `request` parameter must be passed in to add a friend. Its parameter type is defined as follows:
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
 *  Source for adding a friend
 *  The source cannot exceed 8 bytes and must have the “AddSource_Type_” prefix.
 */
@property(nonatomic,strong) NSString* addSource;

/**
 *  Group name
 */
@property(nonatomic,strong) NSString* group;

@end
```


When the callback is successful, the `TIMFriendResult` result is returned for the operating user. Developers can notify the user accordingly. The return code for adding a friend is as follows:

```
typedef NS_ENUM(NSInteger, TIMFriendStatus) {
    /**
     *  Successful operation
     */
    TIM_FRIEND_STATUS_SUCC                              = 0,
    /**
     *  Valid when adding a friend: the user that you want to add as a friend is in your blocklist.
     */
    TIM_ADD_FRIEND_STATUS_IN_SELF_BLACK_LIST                = 30515,
    /**
     *  Valid when adding a friend: the user that you want to add as a friend has forbidden friend requests.
     */
    TIM_ADD_FRIEND_STATUS_FRIEND_SIDE_FORBID_ADD            = 30516,
    /**
     *  Valid when adding a friend and responding to a friend: your number of friends has reached the limit set by the system.
     */
    TIM_ADD_FRIEND_STATUS_SELF_FRIEND_FULL                  = 30010,     
    /**
     *  Valid when adding a friend: the user that you want to add as a friend has added you to the blocklist.
     */
    TIM_ADD_FRIEND_STATUS_IN_OTHER_SIDE_BLACK_LIST          = 30525,    
    /**
     *  Valid when adding a friend: the friend request is pending approval.
     */
    TIM_ADD_FRIEND_STATUS_PENDING                           = 30539,
};
```

Sample code

```
TIMFriendRequest *q = [TIMFriendRequest new];
q.identifier = @"abc"; // Add abc as a friend.
q.addWording = @"Please approve my request";
q.addSource = @"AddSource_Type_iOS";
q.remark = @"You are abc";
[[TIMFriendshipManager sharedInstance] addFriend:q succ:^(TIMFriendResult *result) {
    if (result.result_code == 0)
        self.msgLabel.text = @"Friend added successfully";
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
 *  @param user  Identifiers of friends to be deleted
 *  @param delType  Deletion type (one-way friend or two-way friend)
 *  @param succ  Success callback ([TIMFriendResult])
 *  @param fail  Failure callback
 *
 *  @return 0 The request was sent successfully.
 */
- (int)delFriend:(NSString *)user delType:(TIMDelFriendType)delType succ:(TIMHandleFriendArraySucc)succ fail:(TIMFail)fail;
@end
```

The success callback returns the `TIMFriendResult` result for the operating user. Developers can notify the user accordingly. The error codes for deleting friends are as follows:

```
typedef NS_ENUM(NSInteger, TIMFriendStatus) {
    /**
     *  Successful operation
     */
    TIM_FRIEND_STATUS_SUCC                              = 0,
    /**
     *  Valid when deleting friends: the user that you want to delete is not your friend.
     */
    TIM_DEL_FRIEND_STATUS_NO_FRIEND                         = 31704,
};
```

Sample code

```
NSMutableArray * del_users = [[NSMutableArray alloc] init];
// Delete the friend iOS_002.
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

### Approving or rejecting a friend request

You can use the `doResponse` method of `TIMFriendshipManager` to approve or reject a friend request.

```
@interface TIMFriendshipManager : NSObject
/**
 *  Respond to a friend request
 *
 *  @param response  Response to the request
 *  @param succ      Success callback
 *  @param fail      Failure callback
 *
 *  @return 0 The request was sent successfully.
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
     *  Approve the friend request and add the user as a friend (establish a two-way friendship)
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
 *  Friend remark (optional, if you want to add the user as your friend). The maximum length of the remark is 96 bytes.
 */
@property(nonatomic,strong) NSString* remark;

@end
```

The success callback returns the `TIMFriendResult` result for the operating user. The error codes for handling friend requests are as follows:
```
typedef NS_ENUM(NSInteger, TIMFriendStatus) {
    /**
     *  Successful operation
     */
    TIM_FRIEND_STATUS_SUCC                              = 0,  
    /**
     *  Valid when responding to friend requests: the user has not requested to add you as a friend.
     */
    TIM_RESPONSE_FRIEND_STATUS_NO_REQ                       = 30614,   
    /**
     *  Valid when adding a friend and responding to a friend: your number of friends has reached the limit set by the system.
     */
    TIM_ADD_FRIEND_STATUS_SELF_FRIEND_FULL                  = 30010,      
    /**
     *  Valid when adding a friend and responding to a friend: the user’s number of friends has reached the limit set by the system.
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
 *  @param checkInfo  Friend check information
 *  @param succ  Success callback. The check result was returned.
 *  @param fail  Failure callback
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
     *  Two-way friend
     */
    TIM_FRIEND_CHECK_TYPE_BIDIRECTION      = 0x2,
};
```

The success callback returns the `TIMCheckFriendResult` list for the operating user. The parameter is defined as follows:

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
 * Return message
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
     *  Non-friend
     */
    TIM_FRIEND_RELATION_TYPE_NONE           = 0x0,
    /**
     *  The user is in my friend list
     */
    TIM_FRIEND_RELATION_TYPE_MY_UNI         = 0x1,
    /**
     *  I am in the user’s friend list
     */
    TIM_FRIEND_RELATION_TYPE_OTHER_UNI      = 0x2,
    /**
     *  Two-way friend
     */
    TIM_FRIEND_RELATION_TYPE_BOTHWAY        = 0x3,
};
```

## Pending Friend Requests

### Obtaining the pending request list
When another user uses the `addFriend` method to send a friend request to you, a pending record will be added on the backend. When you send a friend request to another user, a pending record will also be added on the backend. The `getPendencyList` method can be used to obtain the pending request list.
```
@interface TIMFriendshipManager : NSObject

/**
 *  Obtain the pending list
 *
 *  @param pendencyRequest  Request information. For more information, see TIMFriendPendencyRequest.
 *  @param succ  Success callback
 *  @param fail   Failure callback
 *
 *  @return 0 The request was sent successfully.
 */
- (int)getPendencyList:(TIMFriendPendencyRequest *)pendencyRequest succ:(TIMGetFriendPendencyListSucc)succ fail:(TIMFail)fail;
@end
```
The backend may store multiple pending friend requests that cannot be fully displayed on the screen. Therefore, this API allows you to page up or down the pending list. In this case, the `pendencyRequest` parameter must be passed in. This parameter is defined is as follows:
```
/**
 * Pending request information
 */
@interface TIMFriendPendencyRequest : TIMCodingModel

/**
 * `seq`, which is the sequence number of the pending request list
 *    We recommend that you save `seq` and the pending request list on the client. You need to enter `seq` returned by the server when sending a request.
 *    If `seq` is the latest one on the server, no data is returned.
 */
@property(nonatomic,assign) uint64_t seq;

/**
 * Paging timestamp, only used for paging up or down. If the server returns 0, there is no more data. Enter 0 for the first request.
 * Note that, if `seq` returned by the server is different from the entered `seq`, use the original `seq` on the client for paging up or down. The local `seq` is not updated until the data request is completed.
 */
@property(nonatomic,assign) uint64_t timestamp;

/**
 * Amount of data per page, that is, the maximum amount of data returned per request
 */
@property(nonatomic,assign) uint64_t numPerPage;

/**
 * Pending request fetching type
 */
@property(nonatomic,assign) TIMPendencyGetType type;

@end
```
After the operation succeeds, the `succ` callback returns the paging information and pending records.
```
/**
 * Pending information returned
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
 * User ID
 */
@property(nonatomic,strong) NSString* identifier;
/**
 * Add time
 */
@property(nonatomic,assign) uint64_t addTime;
/**
 * Source
 */
@property(nonatomic,strong) NSString* addSource;
/**
 * Remarks of the friend request
 */
@property(nonatomic,strong) NSString* addWording;

/**
 * Nickname of the added friend
 */
@property(nonatomic,strong) NSString* nickname;

/**
 * Type of the pending request
 */
@property(nonatomic,assign) TIMPendencyGetType type;

@end
```

### Deleting a pending record
```
@interface TIMFriendshipManager : NSObject
/**
 * Delete a pending record
 *
 *  @param type  Type of the friend request
 *  @param identifiers  Pending list to be deleted
 *  @param succ  Success callback
 *  @param fail  Failure callback
 *
 *  @return 0 The request was sent successfully.
 */
- (int)deletePendency:(TIMPendencyGetType)type users:(NSArray *)identifiers succ:(TIMSucc)succ fail:(TIMFail)fail;
@end 
```

### Marking a pending record as read
When users fetch pending records, the pending records can be marked as read on the backend.
```
@interface TIMFriendshipManager : NSObject
/**
 *  Mark a pending record as read
 *
 * @param timestamp  Read timestamp. All messages prior to this timestamp will be set to the read state.
 *  @param succ  Success callback
 *  @param fail  Failure callback
 *
 *  @return 0 The request was sent successfully.
 */
- (int)pendencyReport:(uint64_t)timestamp succ:(TIMSucc)succ fail:(TIMFail)fail;
@end
```
After a pending record is marked as read, the unread count returned is changed the next time `getPendencyList` is called.



## Blocklist

### Adding a user to the blocklist

You can block any user. If the user is your friend, after you block the user, your friend relationship with the user is terminated and you cannot receive messages from this user.

```
@interface TIMFriendshipManager : NSObject
/**
 *  Add a user to the blocklist
 *
 *  @param identifiers  User list
 *  @param succ  Success callback
 *  @param fail  Failure callback
 *
 *  @return 0 The request was sent successfully.
 */
- (int)addBlackList:(NSArray *)identifiers succ:(TIMFriendResultArraySucc)succ fail:(TIMFail)fail;
@end
```


### Deleting a user from the blocklist

```
@interface TIMFriendshipManager : NSObject
/**
 *  Delete a user from the blocklist
 *
 *  @param identifiers  User list
 *  @param succ  Success callback
 *  @param fail  Failure callback
 *
 *  @return 0 The request was sent successfully.
 */
- (int)deleteBlackList:(NSArray *)identifiers succ:(TIMFriendResultArraySucc)succ fail:(TIMFail)fail;
@end
```


### Obtaining the blocklist

```
@interface TIMFriendshipManager : NSObject
/**
 *  Obtain the blocklist
 *
 *  @param succ Success callback. The NSString* list is returned.
 *  @param fail   Failure callback
 *
 *  @return 0 The request was sent successfully.
 */
- (int)getBlackList:(TIMFriendArraySucc)succ fail:(TIMFail)fail;
@end
```


## Friend List

### Creating a friend list

While creating a friend list, you can select the users to be added to the list. A user can be added to multiple friend lists.

```
/**
 *  Create a friend list
 *
 *  @param groupNames  Name of the friend list. It must be a new friend list that currently does not exist.
 *  @param identifiers  Friends to be added to the friend list
 *  @param succ  Success callback
 *  @param fail  Failure callback
 *
 *  @return 0 The request was sent successfully.
 */
- (int)createFriendGroup:(NSArray *)groupNames users:(NSArray *)identifiers succ:(TIMFriendResultArraySucc)succ fail:(TIMFail)fail;
@end
```

### Deleting a friend list

```
@interface TIMFriendshipManager : NSObject
/**
 *  Delete a friend list
 *
 *  @param groupNames  Name of the friend list to be deleted
 *  @param succ  Success callback
 *  @param fail  Failure callback
 *
 *  @return 0 The request was sent successfully.
 */
- (int)deleteFriendGroup:(NSArray *)groupNames succ:(TIMSucc)succ fail:(TIMFail)fail;
@end
```


### Adding a friend to a friend list

```
@interface TIMFriendshipManager : NSObject
/**
 *  Add a friend to a friend list
 *
 *  @param groupName   Friend list name
 *  @param identifiers  Friend to be added to the friend list
 *  @param succ  Success callback
 *  @param fail  Failure callback
 *
 *  @return 0 The request was sent successfully.
 */
- (int)addFriendsToFriendGroup:(NSString *)groupName users:(NSArray *)identifiers succ:(TIMFriendResultArraySucc)succ fail:(TIMFail)fail;
@end
```


### Deleting a friend from a friend list


```
@interface TIMFriendshipManager : NSObject
/**
 *  Delete a friend from a friend list
 *
 *  @param groupName   Friend list name
 * @param identifiers  Friend to be deleted from the friend list
 *  @param succ  Success callback
 *  @param fail  Failure callback
 *
 *  @return 0 The request was sent successfully.
 */
- (int)delFriendsFromFriendGroup:(NSString *)groupName users:(NSArray *)identifiers succ:(TIMFriendResultArraySucc)succ fail:(TIMFail)fail;
@end
```


### Renaming a friend list

```
@interface TIMFriendshipManager : NSObject
/**
 *  Modify the name of a friend list
 *
 * @param oldName  Original name of the friend list
 * @param newName  New name of the friend list
 *  @param succ  Success callback
 *  @param fail  Failure callback
 *
 *  @return 0 The request was sent successfully.
 */
- (int)renameFriendGroup:(NSString*)oldName newName:(NSString*)newName succ:(TIMSucc)succ fail:(TIMFail)fail;
@end
```


### Obtaining a specified friend list

```
@interface TIMFriendshipManager : NSObject
/**
 *  Obtain a specified friend list
 *
 *  @param groupNames      Name of the friend list to be obtained. If `nil` is passed in, all friend lists are obtained.
 *  @param succ Success callback. The TIMFriendGroup* list is returned.
 *  @param fail  Failure callback
 *
 *  @return 0 The request was sent successfully.
 */
- (int)getFriendGroups:(NSArray *)groupNames succ:(TIMFriendGroupArraySucc)succ fail:(TIMFail)fail;
@end
```


## System Notification for Relationship Chain Change

In `TIMMessage`, `Elem` = `TIMSNSSystemElem` indicates a system notification for a relationship chain change.

**Prototype:**

```
typedef NS_ENUM(NSInteger, TIM_SNS_SYSTEM_TYPE){
    /**
     *  Friend adding message
     */
    TIM_SNS_SYSTEM_ADD_FRIEND                           = 0x01,
    /**
     *  Friend deleting message
     */
    TIM_SNS_SYSTEM_DEL_FRIEND                           = 0x02,
    /**
     *  Friend adding request
     */
    TIM_SNS_SYSTEM_ADD_FRIEND_REQ                       = 0x03,
    /**
     *  Pending request deleting request
     */
    TIM_SNS_SYSTEM_DEL_FRIEND_REQ                       = 0x04,
};
/**
 *  Details of the relationship chain change
 */
@interface TIMSNSChangeInfo : NSObject
/**
 *  User’s identifier
 */
@property(nonatomic,retain) NSString * identifier;
/**
 *  Valid when requesting to add a friend. It is used to add the cause.
 */
@property(nonatomic,retain) NSString * wording;
/**
 *  Entered to add the source when sending a friend request
 */
@property(nonatomic,retain) NSString * source;
@end
/**
 *  Relationship chain change message
 */
@interface TIMSNSSystemElem : TIMElem
/**
 *  Operation type
 */
@property(nonatomic,assign) TIM_SNS_SYSTEM_TYPE type;
/**
 * Operated user list: TIMSNSChangeInfo list
 */
@property(nonatomic,retain) NSArray * users;

@end
```

**Member description**

Member | Description
--- | ---
type | The type of modification. 
users | The list of changed users. 

In this example, when a user adds another user as a friend or deletes a friend, a log is printed. When a user requests to become the friend of another user, the request reason is printed. **Example:**

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

### System notification for adding a friend

When two users become friends, they both receive a system notification indicating that they are mutually added as friends.

**Triggering time:**

When you add a friend and your relationship chain changes accordingly, you will receive a message. If you are already a one-way friend of this added friend, the party whose relationship chain does not change will not receive a message.

**Parameter description:**

| Parameter | Description |
--- | ---
type | TIM_SNS_SYSTEM_ADD_FRIEND 
users | The list of users who become friends. 

**`TIMSNSChangeInfo` parameter description:**

Member | Description
--- | ---
identifier | The user's identifier. 

### System notification for deleting a friend

When two users terminate the friend relationship with each other, they both receive a system notification indicating that a friend has been deleted. 

**Triggering time:**

When you delete a friend and your relationship chain changes accordingly, you will receive a message. If the deleted friend is a one-way friend, the party whose relationship chain does not change will not receive the message.

**Parameter description:**

| Parameter | Description |
type | TIM_SNS_SYSTEM_DEL_FRIEND 
users | The list of deleted users. 

**`TIMSNSChangeInfo` parameter description:**

Member | Description
--- | ---
identifier | The user's identifier. 

### System notification for a friend request

When you send a friend request to a user and the user requires verification, you and the user will receive a friend request system notification.

**Triggering time:** when you send a friend request to a user and the user requires verification, you and the user will receive a system notification for the friend request. The user can choose to approve or reject the request, whereas you cannot perform any operation. The system notification is only used for information synchronization. 

**Parameter description:**

| Parameter | Description |
--- | ---
type | TIM_SNS_SYSTEM_ADD_FRIEND_REQ 
users | The list of friend requests. 

**`TIMSNSChangeInfo` parameter description:**

| Parameter | Description |
--- | ---
identifier | The user's identifier. 
wording | The request reason. 
source | The request source.

### Notification for deleting a pending request

**Triggering time:** After your request to add a user as your friend is approved or rejected, you will receive a message indicating that the pending request was deleted. 

## System Notification for User Profile Change

In `TIMMessage`, `Elem` = `TIMProfileSystemElem` indicates a system message for a user profile change.

```
/**
 * Message element pushed by the backend after your own profile or a friend's profile is changed
 */
@interface TIMProfileSystemElem : TIMElem
/**
 *  Change type
 */
@property(nonatomic,assign) TIM_PROFILE_SYSTEM_TYPE type;
/**
 *  User whose profile is changed
 */
@property(nonatomic,strong) NSString * fromUser;
/**
 *  Nickname of the changed profile (not yet implemented)
 */
@property(nonatomic,strong) NSString * nickName;
@end
/**
 *  Profile change
 */
typedef NS_ENUM(NSInteger, TIM_PROFILE_SYSTEM_TYPE){
    /**
     Change of a friend's profile
     */
    TIM_PROFILE_SYSTEM_FRIEND_PROFILE_CHANGE        = 0x01,
};
```

When your profile or a friend’s profile is changed, you will receive a system notification indicating that a user profile is changed.
