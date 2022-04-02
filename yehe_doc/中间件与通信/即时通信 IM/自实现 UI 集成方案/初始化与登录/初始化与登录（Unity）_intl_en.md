## Initialization

You need to initialize and log in to the IM Unity SDK before use. The SDK is initialized with the following code in Unity after integration:

```c#
public static void Init() {
        SdkConfig sdkConfig = new SdkConfig();

        sdkConfig.sdk_config_config_file_path = Application.persistentDataPath + "/TIM-Config";

        sdkConfig.sdk_config_log_file_path = Application.persistentDataPath + "/TIM-Log";

        if (sdkappid == "")
        {
            return;
        }

        TIMResult res = TencentIMSDK.Init(long.Parse(sdkappid), sdkConfig);
}
```

### SDKAppID

`SDKAppID` is the unique ID that the IM service uses to identify a customer account. We recommend you apply for a new `SDKAppID` for every independent app to automatically isolate messages between `SDKAppIDs`.
You can view all `SDKAppIDs` in the [IM console](https://console.cloud.tencent.com/im) or click **Create Application** to create an `SDKAppID`.

### sdkConfig

It is used to configure the storage path of IM running logs and data.

### sdk_config_config_file_path

Storage path of local IM data.
>! The app needs to have read-write access to this path.

### sdk_config_log_file_path

Routine storage path of IM data.
>! The app needs to have read-write access to this path.

### TIMResult

It is used to display the result returned when the SDK is called. When `res` is `TIMResult.TIM_SUCC = 0`, the API call is successful.

### Others

After the SDK is successfully initialized, add required listeners to avoid missing messages.

## Login

```c#
public static void Login() {
        if (userid == "" || user_sig == "")
        {
            return;
        }
        // You can replace with your own sdkappid
        TIMResult res = TencentIMSDK.Login(userid, user_sig, (int code, string desc, string json_param, string user_data)=>{
          
        });
}
```

## UserID

The unique ID for user login. You are advised to enter only letters (a-z and A-Z), digits (0-9), underscores (_), and hyphens (-). Its length cannot exceed 32 bytes.

## UserSig

Login ticket of the IM SDK. It is calculated by your business server to ensure security. For more information on the calculation method, see [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385).

### Login scenarios

- When you use features of the IM SDK for the first time after the app is started.
- When the IM SDK triggers a `onUserSigExpired` callback. That is, when the `UserSig` expires, you need to use a new `UserSig` for login.
- When the IM SDK triggers an `onKickedOffline` callback. That is, when the current user is kicked offline, the "You have already logged in to the SDK on another device using the current account. Are you sure you want to log in again?" message can be displayed on the UI. In this case, you can select "Yes" to log in again.

### Scenarios where login is not required

- When your network is disconnected and then reconnected, you do not need to call the `login` function because the SDK automatically goes online.
- When a login process is running, you do not need to log in to the SDK again.

### Multi-client login

You cannot use the same account to log in on two mobile phones of the same model. For example, you cannot use the same account for login on two iPhones. However, one Android phone and one iPhone are considered as two different devices, and you can use the same account to log in on these two devices. For more information on configurations related to multi-client login, see the **Login settings** section in [Feature Configuration](https://intl.cloud.tencent.com/document/product/1047/34419).

### Logout

To log out, call the `Logout` function.

```c#
public static void Logout() {
        TIMResult res = TencentIMSDK.Logout((int code, string desc, string json_param, string user_data)=>{
        
        });
}
```



### Others

After you log in successfully by calling `IM SDK Login`, DAU will be calculated. Use `IM SDK Login` appropriately according to the business scenarios to avoid an excessively high DAU.
