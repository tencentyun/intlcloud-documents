## TIMLogin

This API is used to log in to the Tencent backend server.

**Prototype**

```c
TIM_DECL int TIMLogin(const char* user_id, const char* user_sig, TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type            | Description                                                  |
| --------- | --------------- | ------------------------------------------------------------ |
| user_id   | const char\*    | UserID of a user.                                            |
| user_sig  | const char\*    | UserSig of a user.                                           |
| cb        | TIMCommCallback | Callback function for notifying whether login was successful. If the ticket expires during login, the `ERR_USER_SIG_EXPIRED (6206)` or `ERR_SVR_ACCOUNT_USERSIG_EXPIRED (70001)` error will be returned, and a new `userSig` will be generated for login again. For callback function definition, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data | const void\*    | User-defined data. The IM SDK only transfers the user data to the callback function `cb` without processing the data. |

**Return values**

| Type | Description                                                  |
| ---- | ------------------------------------------------------------ |
| int  | If `TIM_SUCC` is returned, the API was called successfully. (The callback `cb` is called only when the API returns `TIM_SUCC`.) If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

>?Users can send and receive messages only after they have logged in to the Tencent backend server. To log in to the Tencent backend server, a user needs to provide information, including the UserID and UserSig. For more information about these parameters, see [Login Authentication](https://intl.cloud.tencent.com/document/product/1047/33517).


## TIMLogout

This API is used to log out of the Tencent backend server.

**Prototype**

```c
TIM_DECL int TIMLogout(TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type            | Description                                                  |
| --------- | --------------- | ------------------------------------------------------------ |
| cb        | TIMCommCallback | Callback function for indicating whether logout is successful. For more information about the callback function definition, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550). |
| user_data | const void\*    | User-defined data. The IM SDK only transfers the user data to the callback function `cb` without processing the data. |

**Return values**

| Type | Description                                                  |
| ---- | ------------------------------------------------------------ |
| int  | If `TIM_SUCC` is returned, the API was successfully called. (The callback `cb` is called only when the API returns `TIM_SUCC`.) If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

>?Call this API if you need to log out of the server or switch to another user.


## TIMGetLoginStatus

This API is used to get the login status.

**Prototype**

```c
TIM_DECL TIMLoginStatus TIMGetLoginStatus();
```

**Return values**

| Type           | Description                                                  |
| -------------- | ------------------------------------------------------------ |
| TIMLoginStatus | For the definition of each return value, see [TIMLoginStatus](https://intl.cloud.tencent.com/document/product/1047/34551). |

>?If the user is already in the **logged in** or **logging in** state, do not frequently call the login API to log in.


## TIMGetLoginUserID

This API is used to get the UserID of the user.

**Prototype**

```c
TIM_DECL int TIMGetLoginUserID(char* user_id_buffer);
```

**Parameters**

| Parameter      | Type  | Description                                                  |
| -------------- | ----- | ------------------------------------------------------------ |
| user_id_buffer | char* | Buffer where the user ID string is stored. The size of the buffer cannot be less than 128 bytes. After the API is called, a user ID string can be obtained. |

**Return values**

| Type | Description                                                  |
| ---- | ------------------------------------------------------------ |
| int  | If `TIM_SUCC` is returned, the API was called successfully. If other values are returned, the API failed to be called. For more information about the definition of each return value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551). |

**Example**

```c
const size_t kUserIDLength = 128;
char user_id_buffer[kUserIDLength] = {0};
TIMGetLoginUserID(user_id_buffer);
```
