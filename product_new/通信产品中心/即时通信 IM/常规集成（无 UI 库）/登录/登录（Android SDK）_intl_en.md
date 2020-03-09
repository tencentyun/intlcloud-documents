## Login
Users can normally send and receive messages only after they have logged in to the Tencent backend server. To log in to the Tencent backend server, a user needs to provide information including `UserID` and `UserSig`. For more information, see [Login Authentication](https://cloud.tencent.com/document/product/269/31999).

>
>- If the user is forced logout on another terminal, the login attempt fails, and the error code (`ERR_IMSDK_KICKED_BY_OTHERS: 6208`) is returned. In this case, developers must analyze the cause to the login error code `ERR_IMSDK_KICKED_BY_OTHERS`. For details on forcible logout, see [User State Changes](https://cloud.tencent.com/document/product/269/9229#.E7.94.A8.E6.88.B7.E7.8A.B6.E6.80.81.E5.8F.98.E6.9B.B4).
>- If users have saved user tickets, these tickets may expire. If their user tickets expire, `login` returns the error code `70001`. In this case, developers can change the ticket based on the error code.

Login is an asynchronous process, and the result returned by the callback function indicates whether the login was successful. Users can proceed to subsequent operations only after successful login.

**Prototype:**

```
/** Login
 * @param identifier User account
 * @param userSig UserSig, which indicates the user account signature resulting from private key encryption. For details, see the relevant document.
 * @param callback Callback API
 */
public void login(@NonNull String identifier, @NonNull String userSig, @NonNull TIMCallBack callback)
```

**Example:**

```
// identifier indicates the username, and userSig indicates the user login credential.
TIMManager.getInstance().login(identifier, userSig, new TIMCallBack() {
	@Override
	public void onError(int code, String desc) {
		//"code" (error code) and "desc" (error description) can be used to locate the cause of the request failure.
		//For the list of error codes, see the error code table.
		Log.d(tag, "login failed. code: " + code + " errmsg: " + desc);
	}

	@Override
	public void onSuccess() {
		Log.d(tag, "login succ");
	}
});
```

## Logout

To log out or switch to another user, call the logout operation.

**Prototype:**

```
/**
 * Logout
 * @param callback Callback, which is null if it is not needed
 */
public void logout(@Nullable TIMCallBack callback) 
```

**Example:**


```
//Logout
TIMManager.getInstance().logout(new TIMCallBack() {
    @Override
    public void onError(int code, String desc) {
 
        //"code" (error code) and "desc" (error description) can be used to locate the cause of the request failure.
        //For the list of error codes, see the error code table.
        Log.d(tag, "logout failed. code: " + code + " errmsg: " + desc);
    }
 
    @Override
    public void onSuccess() {
        //Successful logout
    }
});
```

## Viewing Messages Without Network Connection

If the current network is abnormal or you want to view user messages without calling `login`, you can call the `initStorage` method of `TIMManager` to initialize storage. After that, you can obtain the conversation list and messages.

>
> * This method is for viewing historical messages only when the login attempt fails or no network connection is available. **To receive and send messages, you must call the login API `login`**.
> * If the login attempt succeeds, the IM SDK automatically initializes local storage, without the need to manually call this API.

**Prototype:**

```
/** Initialize local storage to load local conversations and messages without network connection.
 * @param identifier User ID
 * @param cb Callback
 */
public int initStorage(@NonNull String identifier, @NonNull TIMCallBack cb) 
```

The following example shows how to initialize storage. If the initialization succeeds, the conversation list can be obtained.

**Example:**

```
//Initialize local storage
TIMManager.getInstance().initStorage(identifier, new TIMCallBack() {
	@Override
	public void onError(int code, String desc) {
		Log.e(tag, "initStorage failed, code: " + code + "|descr: " + desc);
	}

	@Override
	public void onSuccess() {
		Log.i(tag, "initStorage succ");
	}
});

//Obtain a conversation instance
TIMConversation conversation = TIMManager.getInstance().getConversation(TIMConversationType.C2C, peer);
//Obtain local messages
conversation.getLocalMessage(5, null, new TIMValueCallBack<List<TIMMessage>>() {
	@Override
	public void onError(int code, String desc) {
		Log.e(tag, "get msgs failed, code: " + code + "|msg: " + desc);
	}

	@Override
	public void onSuccess(List<TIMMessage> timMessages) {
		Log.i(tag, "get msgs succ, size: " + timMessages.size());
	}
});
```

## Obtaining the Currently Logged-in User
The `getLoginUser` method of `TIMManager` can be used to obtain the current username and check whether the user has logged in.

**Prototype:**

```
public String getLoginUser()
```

> The returned value is the username of the currently logged-in user. Note that if the logged-in account is a self-owned account, the username is the same as the `identifier` that was passed in during login. If the user logged in with a third-party account, such as a WeChat or QQ account, an internally converted `identifier` will be generated after login. Subsequent operations, such as searching for friends and joining groups, require the converted `identifier`.


