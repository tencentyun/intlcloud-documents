## `TUICallKit` APIs

`TUICallKit` is an audio/video call component that **includes UI elements**. You can use its APIs to quickly implement an audio/video call application similar to WeChat. For directions on integration, see [Integrating TUICallKit](https://www.tencentcloud.com/document/product/647/50993).

## Overview

| API                                                          | Description                                |
| ------------------------------------------------------------ | ----------------------------------- |
| [init](#init) | Initializes `TUICallKit`.                   |
| [call](#call) | Makes a one-to-one call.                       |
| [groupCall](#groupcall) | Makes a group call.                        |
| [destroyed](#destroyed) | Terminates `TUICallKit`. |

## Details

### init

This API is used to initialize `TUICallKit`. It must be called before `call` and `groupCall`.

```javascript
import { TUICallKitServer } from "./src/components/TUICallKit/Web";
TUICallKitServer.init({
  SDKAppID,
  userID, 
  userSig,
  tim, 
});
```

The parameters are described below:

| Parameter    | Type   | Description                                                                                                                    |
| -------- | ------ | ------------------------------------------------------------ |
| SDKAppID | Number | The SDKAppID of the IM application.                                        |
| userID | String | The ID of the current user, which is a string that can contain only letters (a-z and A-Z), numbers (0-9), hyphens (-), and underscores (_). |
| userSig | String | Tencent Cloud's proprietary security signature. For how to obtain it, see [UserSig](https://www.tencentcloud.com/document/product/647/35166). |
| TIM instance | Any    | If you already have TIM instances, you can use this parameter (optional) to guarantee the uniqueness of a TIM instance. |

### call

This API is used to make a (one-to-one) call.


```javascript
import { TUICallKitServer } from "./src/components/TUICallKit/Web";
TUICallKitServer.call({
  userID: 'jack',
  type: 1,
});
```

The parameters are described below:

| Parameter       | Type                            | Description  |
| ------ | ------ | ------------------------------------------------------ |
| userID | String | The ID of the user to call.                                      |
| type   | Number | The call type. 1: Audio call; 2: Video call. |

### groupCall

This API is used to make a group call.

```javascript
import { TUICallKitServer } from "./src/components/TUICallKit/Web";
TUICallKitServer.groupCall({
  userIDList: ['jack', 'tom'],
  groupID: 'xxx',
  type: 1,
});
```

The parameters are described below:

| Parameter       | Type                            | Description  |
| ---------- | ------------- | ------------------------------------------------------ |
| userIDList | Array<String> | The IDs of the users to call.                                       |
| groupID    | String        | The group ID.                                             |
| type   | Number | The call type. 1: Audio call; 2: Video call. |


### destroyed

This API is used to terminate `TUICallKit`.

```javascript
import { TUICallKitServer } from "./src/components/TUICallKit/Web";
TUICallKitServer.destroyed();
```
