# Introduction

`TUICallKit` is an audio/video call component that **includes UI elements**. You can use its APIs to quickly implement an audio/video call application similar to WeChat. For directions on integration, see [Integrating TUICallKit](https://www.tencentcloud.com/document/product/647/50993).

## Overview

- [`<TUICallKit/>`](#tuicallkit-api-details): The call component.
- [`<TUICallKitMini/>`](#tuicallkitmini-api-details): The floating call window. If `<TUICallKit/>` `allowedMinimized` is `true`, `<TUICallKitMini/>` is required.
- [`TUICallKitServer`](#tuicallkitserver-api-details): The call instance, which has the following APIs:
  - [init](#init): Initializes `TUICallKit`. 
  - [call](#call): Makes a one-to-one call. 
  - [groupCall](#groupcall): Makes a group call. 
  - [destroyed](#destroyed): Terminates `TUICallKit`. 


## `<TUICallKit/>` API details

### Attributes

| Parameter | Description | Type | Required | Default Value |
| -----|-----|-----|-----|-----|
| allowedMinimized | Whether to allow window minimization. If this is `true`, <TUICallKitMini /> is required. If this is `false`, the minimize button will be hidden. | boolean | No | false |
| allowedFullScreen | Whether to allow full screen. If this is `false`, the full screen button will be hidden. | boolean | No | true |

### Methods 

| Method | Description | Type | Required | Default Value |
| -----|-----|-----|-----|-----|
| beforeCalling | This is executed when the user makes or receives a call. | function(type, error) | No | - |
| afterCalling | This is executed after a call ends. | function() | No | - |
| onMinimized | This is executed when the component is minimized. | function(oldStatus, newStatus) | No | - |

## `<TUICallKitMini/>` API details 

None

## Sample code 

```javascript
/**
* beforeCalling 
 * @param { string } type: Valid values: "invited" ｜ "call" ｜ "groupCall". You can use this to determine whether a call is an outgoing call or incoming call.
 * @param { number } error.code: The error code.
 * @param { string } error.type: The error type.
 * @param { string } error.code: The error message.
 */
function beforeCalling(type, error) {
  console.log("This is executed when a call is made. Type:", type, error); 
}
function afterCalling() {
  console.log("This is executed after a call.");
}
/**
 * onMinimized 
 * @param { boolean } oldStatus 
 * @param { boolean } newStatus 
 */
function onMinimized(oldStatus, newStatus) {
  if (newStatus === true) {
    console.log("TUICallKit is minimized");
  } else {
    console.log("TUICallKit is no longer minimized");
  }
}
```

```html
<TUICallKit
  :allowedMinimized="true"
  :allowedFullScreen="true"
  :beforeCalling="beforeCalling"
  :afterCalling="afterCalling"
  :onMinimized="onMinimized"
/>
<TUICallKitMini />
```
## TUICallKitServer API details

### init

This API is used to initialize `TUICallKit`. It must be called before `call` and `groupCall`.

```javascript
import { TUICallKitServer } from "./components/TUICallKit/Web";
TUICallKitServer.init({
  SDKAppID,
  userID, 
  userSig,
  tim, 
});
```

The parameters are described below:

| Parameter | Type | Required | Description  |
|-----|-----|-----|-----|
| SDKAppID | Number | Yes |The SDKAppID of the IM application.                                        |
| userID | String | Yes |The ID of the current user, which is a string that can contain only letters (a-z and A-Z), numbers (0-9), hyphens (-), and underscores (_). |
| userSig | String | Yes |Tencent Cloud's proprietary security signature. For how to obtain it, see [UserSig](https://intl.cloud.tencent.com/document/product/647/35166). |
| TIM instance | Any | No | If you already have TIM instances, you can use this parameter to guarantee the uniqueness of a TIM instance. |

### call
This API is used to make a one-to-one call.

```javascript
import { TUICallKitServer } from "./components/TUICallKit/Web";
TUICallKitServer.call({
  userID: 'jack',
  type: 1,
});
```

The parameters are described below:

| Parameter | Type | Required | Description  |
|-----|-----|-----|-----|
| userID | String | Yes | The ID of the user to call.                                      |
| type   | Number | Yes | The call type. 1: Audio call; 2: Video call. |
| timeout | Number | No | The timeout period (seconds). `0` indicates the call will not time out. The default value is `30`. |
| offlinePushInfo | Object | No | The custom offline push message. This is valid only if your `tsignaling` version is 0.8.0 or later. |

offlinePushInfo 

| Parameter | Type | Required | Description  |
|-----|-----|-----|-----|
| offlinePushInfo.title | String | No | The message title. |
| offlinePushInfo.description | String | No | The message content. |
| offlinePushInfo.androidOPPOChannelID | String | No | The channel ID for the offline push message on OPPO phones in v8.0 or later. |
| offlinePushInfo.extension | String | No | The pass-through content. This is valid only if your `tsignaling` version is 0.9.0 or later. |

### groupCall
This API is used to make a group call.

```javascript
import { TUICallKitServer } from "./components/TUICallKit/Web";
TUICallKitServer.groupCall({
  userIDList: ['jack', 'tom'],
  groupID: 'xxx',
  type: 1,
});
```

The parameters are described below:

| Parameter | Type | Required | Description  |
|-----|-----|-----|-----|
| userIDList | Array<String> | Yes |The IDs of the users to call.                                       |
| type   | Number | Yes | The call type. 1: Audio call; 2: Video call. |
| groupID | String | Yes |The group ID.                                             |
| timeout | Number | No | The timeout period (seconds). `0` indicates the call will not time out. The default value is `30`. |
| offlinePushInfo | Object | No | The custom offline push message. This is valid only if your `tsignaling` version is 0.8.0 or later. |

For the parameters of `offlinePushInfo`, see above.

### destroyed
This API is used to terminate `TUICallKit`.

```javascript
import { TUICallKitServer } from "./components/TUICallKit/Web";
TUICallKitServer.destroyed();
```