
## TIMLogin

This API is used to log in to the Tencent backend server.

**Prototype**

```c
TIM_DECL int TIMLogin(const char* user_id, const char* user_sig, TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| user_id | const char\* | The identifier of the user. |
| user_sig | const char\* | The signature of the user. |
| cb | TIMCommCallback | The callback for notifying whether the login succeeded or failed. For the definition of the callback function, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34551#timcommcallback). |
| user_data | const void\* | User-defined data. The IM SDK is only responsible for returning the user data to the callback function cb without processing the data. |

**Returned values**

| Type | Description |
|-----|-----|
| int | If TIM_SUCC is returned, the API was successfully invoked (the callback will be invoked only when the API returns TIM_SUCC.) If other values are returned, the API failed to be invoked. For the definition of each returned value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551#timresult). |

> Users can normally send and receive messages only after they have logged in to the Tencent backend server. To log in to the Tencent backend server, the user needs to provide information including UserID and UserSig. For the definitions of these parameters, see [Login Authentication](https://intl.cloud.tencent.com/document/product/1047/33517).


## TIMLogout

This API is used to log out of the Tencent backend server.

**Prototype**

```c
TIM_DECL int TIMLogout(TIMCommCallback cb, const void* user_data);
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| cb | TIMCommCallback | The callback for notifying whether the logout succeeded or failed. For the definition of the callback function, see [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34551#timcommcallback). |
| user_data | const void\* | User-defined data. The IM SDK is only responsible for returning the user data to the callback function cb without processing the data. |

**Returned values**

| Type | Description |
|-----|-----|
| int | If TIM_SUCC is returned, the API was successfully invoked (the callback will be invoked only when the API returns TIM_SUCC.) If other values are returned, the API failed to be invoked. For the definition of each returned value, see [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551#timresult). |

> Invoke this API if you need to log out of the server or switch to another account.


