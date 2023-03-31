## Feature Description
After initializing the IM SDK, you need to call the SDK login API to authenticate your account to get the permissions to use message, conversation, and other features.

<dx-alert infotype="notice" title="">
Only the conversation acquisition API can be called immediately after you call the login API, and other APIs can be called only after you have successfully logged in to the SDK. Therefore, **make sure that you have logged in successfully** before using other features; otherwise, such features may become abnormal or unavailable.
</dx-alert>


## Login
You don't need to sign up on your first login, as you will automatically sign up if the login is successful.
You can call the `Login` API ([Details](https://comm.qq.com/im/doc/unity/en/api/loginOrlogout/Login.html)) to log in.

Key parameters of the `Login` API are as follows:

| Parameter | Description    | Remarks                                                      |
| --------- | -------------- | ------------------------------------------------------------ |
| user_id   | Unique user ID | It can contain up to 32 bytes of letters (a-z and A-Z), digits (0-9), underscores (_), and hyphens (-). |
| user_sig  | Login ticket   | It is calculated by your business server to ensure security. For more information, see [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385). |
| callback  | Async callback | It can be [NullValueCallback](https://comm.qq.com/im/doc/unity/en/callback/NullValueCallback.html) or [ValueCallback`<String>`](https://comm.qq.com/im/doc/unity/en/callback/ValueCallback.html). |

You can call the `Login` API in the following scenarios:
* You use the features of the IM SDK for the first time after your application is started.
* Your ticket expires on login: The callback of the `Login` API returns the `ERR_USER_SIG_EXPIRED (6206)` or `ERR_SVR_ACCOUNT_USERSIG_EXPIRED (70001)` error code. In this case, you need to generate a new `user_sig` to log in again.
* Your ticket expires when the user is online: You might receive the `UserSigExpiredCallback` callback ([Details](https://comm.qq.com/im/doc/unity/en/callback/UserSigExpiredCallback.html)) when users are online. In this case, you need to generate a new `user_sig` to log in again.
* A user is kicked offline: When a user is kicked offline, the IM SDK will notify you through the `KickedOfflineCallback` callback ([Details](https://comm.qq.com/im/doc/unity/en/callback/KickedOfflineCallback.html)). In this case, you can prompt the user and call `Login` to log in again.

You don't need to call the `Login` API in the following scenarios:
* After the user's network is disconnected and then reconnected, you don't need to call the `Login` function, as the IM SDK will automatically go online.
* The login process is running.

>!1. After you call the IM SDK API and log in successfully, DAU calculation will start; therefore, call the login API as needed to avoid a high DAU.
>2. You cannot log in to multiple IM SDK accounts of the same application at the same time; otherwise, only the last logged in account will be online.

Sample code:


```c#
public static void Login() {
  if (userid == "" || user_sig == "")
  {
      return;
  }
  TIMResult res = TencentIMSDK.Login(userid, user_sig, (int code, string desc, string json_param, string user_data)=>{
    // Process the login callback logic
  });
```


### Getting the UserID

After logging in successfully, call `GetLoginUserID` ([Details](https://comm.qq.com/im/doc/unity/en/api/loginOrlogout/GetLoginUserID.html)) to get the `UserID`.
If the login fails, the `UserID` will be empty.

Sample code:


```c#
public static void GetLoginUserID()
  {
    StringBuilder userId = new StringBuilder(128);

    TIMResult res = TencentIMSDK.GetLoginUserID(userId);

    Debug.Log(userId.ToString());
  }
```



### Getting the login status

Call `GetLoginStatus` ([Details](https://comm.qq.com/im/doc/unity/en/api/loginOrlogout/GetLoginStatus.html)) to get the login status. If a user is logged in or logging in, don't call the login API frequently. The IM SDK supports the following login statuses:

| Login Status              | Description   |
| ------------------------- | ------------- |
| kTIMLoginStatus_Logined   | Logged in     |
| kTIMLoginStatus_Logining  | Logging in    |
| kTIMLoginStatus_Logouting | Logging out   |
| kTIMLoginStatus_UnLogined | Not logged in |

Sample code:


```c#
 public static void GetLoginStatus()
  {
    TIMLoginStatus res = TencentIMSDK.GetLoginStatus();
  }
```

## Multi-Client Login and Mutual Kickout
You can configure multi-client login policies for the IM SDK in the Tencent Cloud console.
There are multiple multi-client login policies, such as **A user can be concurrently online on a mobile or desktop platform and the web platform** or **A user can be concurrently online on all platforms**.
For more information on the configuration, see [Feature Configuration](https://intl.cloud.tencent.com/document/product/1047/34419).

You can configure the **Max Login Instances per User per Platform** for the IM SDK in the Tencent Cloud console, that is, the maximum number of instances on the same platform that can be concurrently online.
This feature is available only for the Ultimate edition. A user can be concurrently online on up to ten clients on the web platform or on up to three clients on the Android, iPhone, iPad, Windows, or macOS platform (the maximum number of clients that can be concurrently online on Flutter is subject to the actual compilation result).
For more information on the configuration, see [Feature Configuration](https://intl.cloud.tencent.com/document/product/1047/34419).

When you call the `Login` API ([Details](https://comm.qq.com/im/doc/unity/en/api/loginOrlogout/Login.html)) to log in, if the limit specified by the multi-client login policy for your account is exceeded, a newly logged in instance will kick out an earlier one.
The one kicked out will receive `KickedOfflineCallback` ([Details](https://comm.qq.com/im/doc/unity/en/callback/KickedOfflineCallback.html)).


## Logout
Generally, if your application's lifecycle is the same as the IM SDK's lifecycle, there is no need to log out before exiting the application.
In special cases, for example, if you use the IM SDK only after entering a specific UI and no longer use it after exiting the UI, you can call the `Logout` API ([Details](https://comm.qq.com/im/doc/unity/en/api/loginOrlogout/Logout.html)) to log out of the SDK, after which you will no longer receive new messages. Note that in this case, you also need to call `Uninit` ([Details](https://comm.qq.com/im/doc/unity/en/api/IMSDKInit/Uninit.html)) after the logout to uninitialize the SDK.

Sample code:


```c#
public static void Logout()
  {
    TIMResult res = TencentIMSDK.Logout((int code, string desc, string json_param, string user_data)=>{
    // Process the logout callback logic
    });
  }
```


## Account Switch
Call `Login` ([Details](https://comm.qq.com/im/doc/unity/en/api/loginOrlogout/Login.html)) to switch between accounts in the application.

For example, to switch the logged-in user from `Alice` to `Bob`, just call `Login bob`. You don't need to explicitly call `logout alice`, as this operation will be handled automatically inside the IM SDK.

[](id:qa)

## FAQs

[](id:qa1)

### 1. What should I do if error code 6013 is returned along with the description "not initialized" when I call the login or another API?
