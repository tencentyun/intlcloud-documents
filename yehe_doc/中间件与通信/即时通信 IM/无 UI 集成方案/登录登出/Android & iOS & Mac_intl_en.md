## Feature Description
After initializing the IM SDK, you need to call the SDK login API to authenticate your account to get the permissions to use message, conversation, and other features.

<dx-alert infotype="notice" title="">
All SDK feature APIs can be called only after successful login, except the APIs to get the conversation list and pull historical messages. Therefore, **make sure that you have logged in successfully** before using other features.
You can call the APIs to get the conversation list and pull historical messages even if your login failed. In this case, the locally cached conversation list and historical messages will be returned and can be displayed when there is no network connection.
</dx-alert>


## Login
Your first login to an IM account doesn't require signup, as IM will automatically sign the account up after finding out that you are using a new account.
You can call the `login` API ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a73fc0e14c5f2f5fc06a80081479fb416) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a38c42943046acdaf615915c9422af07c)) to log in.

Key parameters of the `login` API are as follows:

| Parameter | Definition     | Description                                                  |
| --------- | -------------- | ------------------------------------------------------------ |
| UserID    | Unique user ID | It can contain up to 32 bytes of letters (a-z and A-Z), digits (0-9), underscores (_), and hyphens (-). |
| UserSig   | Login ticket   | It is calculated by your business server to ensure security. For more information, see [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385). |

You can call the `login` API in the following scenarios:
* You use the features of the IM SDK for the first time after your application is started.
* Your ticket expires on login: The callback of the `login` API returns the `ERR_USER_SIG_EXPIRED (6206)` or `ERR_SVR_ACCOUNT_USERSIG_EXPIRED (70001)` error code. In this case, you need to generate a new `userSig` to log in again.
* Your ticket expires when the user is online: You may receive the `onUserSigExpired` callback ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMSDKListener.html#a55a5d5ee490850d28b7b8a17868c4833) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/protocolV2TIMSDKListener-p.html#a55a5d5ee490850d28b7b8a17868c4833)) when users are online. In this case, you need to generate a new `userSig` to log in again.
* A user is kicked offline: When a user is kicked offline, the IM SDK will notify you through the `onKickedOffline` callback ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMSDKListener.html#a0f56352869133d50d43c060448e208e7) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/protocolV2TIMSDKListener-p.html#a0f56352869133d50d43c060448e208e7)). In this case, you can prompt the user and call `login` to log in again.

You don't need to call the `login` API in the following scenarios:
* After the user's network is disconnected and then reconnected, you don't need to call the `login` function, as the IM SDK will automatically go online.
* The login process is running.

>!
>1. After you call the IM SDK API and log in successfully, DAU calculation will start; therefore, call the login API as needed to avoid a high DAU.
>2. You cannot log in to multiple IM SDK accounts of the same application at the same time; otherwise, only the last logged in account will be online. 


Sample code:
<dx-tabs>
::: Android
```java
String userID = "your user id";
String userSig = "userSig from your server";
V2TIMManager.getInstance().login(userID, userSig, new V2TIMCallback() {
    @Override
    public void onSuccess() {
        Log.i("imsdk", "success");
    }

    @Override
    public void onError(int code, String desc) {
        // The following error codes indicate an expired `userSig`, and you need to generate a new one for login again.
        // 1. ERR_USER_SIG_EXPIRED (6206)
        // 2. ERR_SVR_ACCOUNT_USERSIG_EXPIRED (70001)
        // Note: Do not call the login API in case of other error codes; otherwise, the IM SDK may enter an infinite loop of login.
        Log.i("imsdk", "failure, code:" + code + ", desc:" + desc);
    }
});
```
:::
::: iOS and macOS
```objectivec
NSString *userID = @"your user id";
NSString *userSig = @"userSig from your server";
[[V2TIMManager sharedInstance] login:userID userSig:userSig succ:^{
    NSLog(@"success");
} fail:^(int code, NSString *desc) {
    // The following error codes indicate an expired `userSig`, and you need to generate a new one for login again.
    // 1. ERR_USER_SIG_EXPIRED (6206)
    // 2. ERR_SVR_ACCOUNT_USERSIG_EXPIRED (70001)
    // Note: Do not call the login API in case of other error codes; otherwise, the IM SDK may enter an infinite loop of login.
    NSLog(@"failure, code:%d, desc:%@", code, desc);
}];
```
:::
</dx-tabs>

### Getting the UserID

After logging in successfully, call `getLoginUser` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#ad4b2e5a7df5e786ba369054ac582007f) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a78ca7f39bca860e46620f8f766508fb0)) to get the `UserID`.
If the login fails, the `UserID` will be empty.

Sample code:
<dx-tabs>
::: Android
```java
// Get the `UserID` of the logged-in user
String loginUserID = V2TIMManager.getInstance().getLoginUser();
```
:::
::: iOS and macOS
```objectivec
// Get the `UserID` of the logged-in user
NSString *loginUserID = [[V2TIMManager sharedInstance] getLoginUser];
```
:::
</dx-tabs>


### Getting the login status

Call `getLoginStatus` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a1836146275265b2a120412f18961db95) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#acfd2f6366780badf80ebf66d95550f89)) to get the login status. If a user is logged in or logging in, don't call the login API frequently. The IM SDK supports the following login statuses:

| Login Status          | Description   |
| --------------------- | ------------- |
| V2TIM_STATUS_LOGINED  | Logged in     |
| V2TIM_STATUS_LOGINING | Logging in    |
| V2TIM_STATUS_LOGOUT   | Not logged in |

Sample code:
<dx-tabs>
::: Android
```java
int loginStatus = V2TIMManager.getInstance().getLoginStatus();
```
:::
::: iOS and macOS
```objectivec
V2TIMLoginStatus loginStatus = [[V2TIMManager sharedInstance] getLoginStatus];
```
:::
</dx-tabs>


## Multi-Client Login and Kickout
You can configure multi-client login policies for the IM SDK in the Tencent Cloud console.
There are multiple multi-client login policies, such as **A user can be concurrently online on a mobile or desktop platform and the web platform** or **A user can be concurrently online on all platforms**.
For more information on the configuration, see [Feature Configuration](https://intl.cloud.tencent.com/document/product/1047/34419).

You can configure the **Max Login Instances per User per Platform** for the IM SDK in the Tencent Cloud console, that is, the maximum number of instances on the same platform that can be concurrently online.
This feature is only available for Ultimate edition. The value for **Web** and **Android, iPhone, iPad, Windows, Mac** is 10 or 3 respectively.
For more information on the configuration, see [Feature Configuration](https://intl.cloud.tencent.com/document/product/1047/34419).

When you call the `login` API to log in, if the limit specified by the multi-client login policy for your account is exceeded, a newly logged in instance will kick out an earlier one.
If you have called `addIMSDKListener` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a2f0297e96d365013e7923275ce2a5d4e) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#ac569656a58908afba491710a8cb3c8d9)) during the initialization to add the SDK listener, an earlier login instance will receive the `onKickedOffline` callback ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMSDKListener.html#a0f56352869133d50d43c060448e208e7) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/protocolV2TIMSDKListener-p.html#a0f56352869133d50d43c060448e208e7)).


## Logout
Generally, if your application's lifecycle is the same as the IM SDK's lifecycle, there is no need to log out before exiting the application.
In special cases, for example, if you use the IM SDK only after entering a specific UI and no longer use it after exiting the UI, you can call the `logout` API ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a0398924fa1b62a8f5cc9b51673273b48) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a20b495d7f7a231ea33507ca4a79f811f)) to log out of the SDK, after which you will no longer receive new messages. Note that in this case, you also need to call `unInitSDK` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a8ac73b4f71f9d9a1ca01551c919d3cdd) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a286e5358ec4cd0a8f9c66f4d2d7d4544)) after the logout to uninitialize the SDK.


Sample code:
<dx-tabs>
::: Android
```java
V2TIMManager.getInstance().logout(new V2TIMCallback() {
    @Override
    public void onSuccess() {
        Log.i("imsdk", "success");
    }

    @Override
    public void onError(int code, String desc) {
        Log.i("imsdk", "failure, code:" + code + ", desc:" + desc);
    }
});
```
:::
::: iOS and macOS
```objectivec
[[V2TIMManager sharedInstance] logout:^{
    NSLog(@"success");
} fail:^(int code, NSString *desc) {
    NSLog(@"failure, code:%d, desc:%@", code, desc);
}];
```
:::
</dx-tabs>

## Account Switch
Call `login` to switch between accounts in the application.

For example, to switch the logged-in user from `alice` to `bob`, just log bob in. You don't need to explicitly call `logout alice`, as this operation will be handled automatically inside the IM SDK.
