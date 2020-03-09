## Login

Users can normally send and receive messages only after they have logged in to the Tencent backend server. To log in to the Tencent backend server, a user needs to provide `UserID` and `UserSig`. If users have saved user tickets, these tickets may expire. If their user tickets expire, `login` returns the error code `6206`. In this case, developers can change the ticket based on the error code. Login is an asynchronous process, and the result returned by the callback function indicates whether the login was successful. Users can proceed to subsequent operations only after successful login. The `succ` and `fail` blocks are used for the callback upon successful or failed login, respectively.

>
>- If the user is forced logout on another terminal, the login attempt fails, and the error code (`ERR_IMSDK_KICKED_BY_OTHERS: 6208`) is returned. In this case, developers must analyze the cause to the login error code `ERR_IMSDK_KICKED_BY_OTHERS`. For details on forcible logout, see [User State Changes](https://cloud.tencent.com/document/product/269/9148#.E7.94.A8.E6.88.B7.E7.8A.B6.E6.80.81.E5.8F.98.E6.9B.B4).
>- After successful login, as long as users do not log out or are not forced logout and automatic network reconnection upon connectivity change is supported, developers need not be concerned. However, they should pay special attention to situations where users are forced logout. Therefore, the [callback for a user state change](https://cloud.tencent.com/document/product/269/9148#.E7.94.A8.E6.88.B7.E7.8A.B6.E6.80.81.E5.8F.98.E6.9B.B4) must be registered, otherwise no notification can be received when forcible logout occurs.

**Prototype:**

```
/**
 * Login information
 */
@interface TIMLoginParam : NSObject
/**
 * Username
 */
@property(nonatomic,retain) NSString* identifier;
/**
 *  Authentication token
 */
@property(nonatomic,retain) NSString* userSig;
/**
 *  App Appid assigned by the OAuth authorization system
 */
@property(nonatomic,retain) NSString* appidAt3rd;
@end
```

For self-owned accounts, the `appidAt3rd` field is the same as the `SDKAppID` field. For other fields, such as `UserID` and `UserSig`, enter the corresponding content.

```
/**
 *  Login
 *
 *  @param param Login parameter
 *  @param succ Success callback
 *  @param fail Failure callback
 *
 *  @return 0 Request succeeded
 */
- (int)login:(TIMLoginParam*)param succ:(TIMLoginSucc)succ fail:(TIMFail)fail;
@end
```

**Parameter description:**

Parameter | Description
---|---
param | Login parameter. For details, see the description of the TIMLoginParam structure.
succ | Callback for successful login
fail | Callback for failed login

**Example:**

```
TIMLoginParam * login_param = [[TIMLoginParam alloc ]init];
// identifier Username
login_param.identifier = @"iOS_001";
//userSig User login credential
login_param.userSig = @"usersig";
//appidAt3rd Appid assigned by the OAuth authorization system for the app user. For private accounts, enter the same content as SDKAppID.
login_param.appidAt3rd = @"123456";
[[TIMManager sharedInstance] login: login_param succ:^(){
    NSLog(@"Login Succ");
} fail:^(int code, NSString * err) {
    NSLog(@"Login Failed: %d->%@", code, err);
}];
```
For the correct method of issuing UserSig, see [Login Authentication](https://cloud.tencent.com/document/product/269/31999).
## Logout

To log out or switch to another user, call the logout operation.

**Prototype:**

```
@interface TIMManager : NSObject
/**
 *  Logout
 *
 *  @param succ Success callback, which indicates that the logout succeeded
 *  @param fail Failure callback, in which case the error code and error information are returned
 *
 *  @return 0 Logout package was sent successfully, and the callback is pending
 */
- (int)logout:(TIMLoginSucc)succ fail:(TIMFail)fail; 
@end
```

**Example:**

> **Note:**
> When you need to switch to another account, `login` can be called again only after the `logout` callback succeeds or fails. Otherwise, `login` may fail.

```
[[TIMManager sharedInstance] logout:^() {
    NSLog(@"logout succ");
} fail:^(int code, NSString * err) {
    NSLog(@"logout fail: code=%d err=%@", code, err);
}];
```

## Viewing Messages Without Network Connection

If the current network is abnormal or you want to view user messages without calling `login`, you can call the `initStorage` method to initialize storage. After that, you can obtain the conversation list and messages.

**Prototype:**

```
@interface TIMManager : NSObject
/**
 * Initializes storage. This is only for viewing historical messages. For operations such as receiving or sending messages, this function does not need to be called if login succeeded.
 *
 *  @param userID Username
 *  @param succ Success callback. You can obtain the conversation list and messages when receiving this callback.
 *  @param fail  Failure callback
 *
 *  @return 0 Request succeeded
 */
- (int)initStorage:(NSString*)userID succ:(TIMLoginSucc)succ fail:(TIMFail)fail; 
@end
```

**Parameter description:**

| Parameter | Description |
| --- | --- |
| userID | Username |
| succ | Success callback, in which case you can obtain the conversation list and perform further login |
| fail | Failure callback |

The following sample shows how to initialize storage. If the initialization succeeds, the conversation list can be obtained. **Example:**

```
TIMLoginParam * login_param = [[TIMLoginParam alloc ]init]; 
[[TIMManager sharedInstance] initStorage: @"iOS_001" succ:^(){
    NSLog(@"Init Succ");
} fail:^(int code, NSString * err) {
    NSLog(@"Init Failed: %d->%@", code, err);
}];
```

## Obtaining the Currently Logged-in User

The `getLoginUser` method of `TIMManager` can be used to obtain the current username and check whether the user has logged in. The return value is the username of the currently logged-in user. Note that if the logged-in account is a self-owned account, the username is the same as the `UserID` that was passed in during login. If the user logged in with a third-party account, such as a WeChat or QQ account, an internally converted `UserID` will be generated after login. Subsequent operations, such as searching for friends and joining groups, require the converted `UserID`.

**Prototype:**

```
@interface TIMManager : NSObject
 
/**
 *  Obtain the currently logged-in user
 *
 *  @return Return the logged-in user’s identifier. If no user is logged in, ‘nil’ is returned.
 */
- (NSString*)getLoginUser;
 
@end
```

## Synchronizing Offline Messages by the IM SDK

The IM SDK automatically synchronizes offline messages and recent contacts after startup. If offline messages are not needed, you can send messages by referring to [sending online messages](/doc/product/269/9150#.E5.9C.A8.E7.BA.BF.E6.B6.88.E6.81.AF). By default, after login, the IM SDK asynchronously obtains offline messages and synchronizes profile data (if this feature is enabled, and you can see the section about relationship chain profiles for more information). After the synchronization is completed, the IM SDK notifies users of UI updates through the `onRefresh` callback. After receiving the notification, users can update the UI, for example, to view unread messages in the conversation list.

```
@interface TIMUserConfig : NSObject
/**
 *  Conversation refreshment listener
 */
@property(nonatomic,retain) id<TIMRefreshListener> refreshListener;
@end
```
