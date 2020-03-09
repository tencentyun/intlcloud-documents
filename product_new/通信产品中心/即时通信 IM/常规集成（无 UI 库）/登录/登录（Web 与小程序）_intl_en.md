## Login
Users can normally send and receive messages only after they have logged in to the IM SDK. To log in to the IM SDK, a user needs to provide information including UserID and UserSig. For more information, see [Login Authentication](https://intl.cloud.tencent.com/document/product/1047/33517). After successful login, [sendMessage](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#sendMessage) and other APIs that require authentication can be called only when the SDK state is ready. You can monitor the event [TIM.EVENT.SDK_READY](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-EVENT.html#.SDK_READY) to obtain the SDK state.

> By default, multi-instance login is not supported. If an account that has logged in on another webpage continues to log in on the current webpage and the login succeeds, the account may be forced logout on another webpage. When a user is forced logout, the event `TIM.EVENT.KICKED_OUT` is triggered. Users can perform relevant handling after detecting this event. An example of monitoring multi-instance login is as follows:
```javascript
let onKickedOut = funciton (event) {
  console.log(event.data.type); // mutipleAccount (when the same account is logged in on multiple webpages on the same device, the account is forced logout)
};
tim.on(TIM.EVENT.KICKED_OUT, onKickedOut);
```
To support multi-instance login (that is, allowing the same account to log in on multiple webpages simultaneously), log in to [IM Console](https://console.cloud.tencent.com/im), find the corresponding SDKAppID, and choose **App Configuration** > **Feature Configuration** > **Login and Messages** > **Number of Concurrent Online Web Instances** to set the number of instances. The setting will take effect within 50 minutes.

**API name**

```javascript
tim.login(options)
```

**Request parameters**

| Name | Type | Description |
| --------- | -------- | ------------------------------------------------------------ |
| UserID | String | User ID |
| UserSig | String | Password with which the user logs in to IM. It is essentially the ciphertext resulting from the encryption of UserID and relevant information. <br/>For the detailed generation method, see [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385). |

**Return values**

This API returns the `Promise` object.

**Example**

```javascript
let promise = tim.login({userID: 'your userID', userSig: 'your userSig'});
promise.then(function(imResponse) {
  console.log(imResponse.data); // Login succeeded
}).catch(function(imError) {
  console.warn('login error:', imError); // Information about the login failure
});
```



## Logout
This API is normally called when switching accounts. It can clear the login state and all data in the memory.
>
>- An instance that calls this API triggers the event [SDK_NOT_READY](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-EVENT.html#.SDK_NOT_READY). Then, the instance goes offline and cannot receive or send any messages.
>- If the "Number of Concurrent Online Web Instances" set in [IM Console](https://console.cloud.tencent.com/im) is greater than 1 and the same account has logged in to instances `a1` and `a2` (including mini program instances), after the execution of `a1.logout()`, `a1` goes offline and cannot receive or send any messages, while `a2` is not affected.<br/>
>- Forcible logout for multi-instance login: if the "Number of Concurrent Online Web Instances" is set to 2 and your account has logged in to instances `a1` and `a2`, when this account successfully logs in to the third instance `a3`, either `a1` or `a2` is forced logout (usually, the first login instance is forced logout in this case.) Assuming that `a1` is forced logout, `a1` internally executes the logout process and throws the event [KICKED_OUT](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-EVENT.html#.KICKED_OUT). In this case, the access side can detect this event and jump to the login page when it is triggered. At this time, `a1` goes offline, while `a2` and `a3` continue to run normally.

**API name**

```js
tim.logout();
```

**Request parameters**

None

**Return values**

This API returns the `Promise` object:
- The callback function parameter for `then` is [IMResponse](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMResponse). `IMResponse.data` is a null object, which indicates successful logout.

- The callback function parameter for `catch` is [IMError](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMError).

**Example**

```js
let promise = tim.logout();
promise.then(function(imResponse) {
  console.log(imResponse.data); // Logout succeeded
}).catch(function(imError) {
  console.warn('logout error:', imError);
});
```
