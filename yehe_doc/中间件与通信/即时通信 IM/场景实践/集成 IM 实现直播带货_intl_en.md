The live e-commerce broadcasting component is the result of secondary encapsulation of IM capabilities used in product promotion livestreaming scenarios. Capabilities, such as likes, gifts, product push, and coupon claiming, are encapsulated specifically for the product promotion livestreaming scenario. For information on how to download the related SDK, see [SDK Download](https://intl.cloud.tencent.com/document/product/1047/33996).

## Prerequisites for Using the Component

- **You have created an IM app.**
- **The following group custom field is created:**
  - attent: records the anchors that you have followed.
- **You have created the following group member custom fields:**
  - add_goods: lists newly released products on the backend in the live room.
  - room_status: controls the status of the live room.

## SDK Access
- Introduce the IM SDK.
```
npm i tim-js-sdk --save
```
- Introduce the product promotion livestreaming SDK.
```
npm i im-live-sells --save
```

## Component Parameters

| Parameter | Description |
| -------- | ------------------------------------------------------------ |
| SDKAppID | ID of the IM application. The SDKAppID can be created in the [IM console](https://console.cloud.tencent.com/im). You can obtain the SDKAppID from the basic information module of the application. The initially created application is a trial edition that can always be used for free. However, the trial edition is not suitable for use in a formal environment due to its low configuration. We recommend that you purchase the Pro or Flagship edition if you need to use the application in a formal environment. |
| userSig | UserSig of the IM user. It is required for logging in to the IM SDK. A UserSig can be generated at the business backend and then sent to the frontend for use. For more information on the methods and code for generating a UserSig, see [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385). |
| roomID | ID of the live room. It is the ID of the audio-video live chat room (AVChatRoom) created in IM. The AVChatRoom room supports an unlimited number of members. You can create an AVChatRoom room in [Group Management](https://console.cloud.tencent.com/im-detail/qun-manage) or by calling the [RESTful API](https://intl.cloud.tencent.com/document/product/1047/34620). |
| TIM | IM SDK. You need to use **tim-wx-sdk* in a Mini Program environment and **tim-js-sdk** in a web environment. |
| userName | It is consistent with the userName of the generated userSig. |



## Initialization Example

```javascript
import TLS from 'im-live-sells'
import TIM from 'tim-js-sdk' // Web environment
// The code is "import TIM from 'tim-wx-sdk'" in the Mini Program environment.
const tls = new TIMLiveSell({
      SDKAppID: 1400***803,
      roomID: '@TGS#E****NVLGE',
      userSig: 'eJwtzM9****-reWMQw_',
      userName: 'Ho***st',
      TIM: TIM
})
```

## Component Callbacks

### TLS.EVENT.SDK_READY

This callback is triggered when the initialization of the component is completed. This event corresponds to `TIM.EVENT.SDK_READY` of the IM SDK. You can call the SDK methods only after this callback is triggered.

```javascript
tls.on(TLS.EVENT.SDK_READY, async() => {
  
})
```

### TLS.EVENT.ROOM_STATUS_CHANGE

This callback is triggered when the room status changes, for example, when the anchor goes online or offline or pauses the stream.

```javascript
tls.on(TLS.EVENT.ROOM_STATUS_CHANGE, async(data) => {
  
}
```

### TLS.EVENT.JOIN_GROUP

This callback is triggered when a user joins the group chat.

```javascript
tls.on(TLS.EVENT.JOIN_GROUP, async(data) => {
  const {nick,avatar,userID} = data
})
```

### TLS.EVENT.EXIT_GROUP

This callback is triggered when a user quits the group chat.

```javascript
tls.on(TLS.EVENT.EXIT_GROUP, async(data) => {
  const {nick,avatar,userID} = data
})
```

### TLS.EVENT.NOTIFACATION

This callback is triggered when the notification is changed.

```javascript
tls.on(TLS.EVENT.NOTIFACATION, async(data) => {
  const { notification } = data
})
```

### TLS.EVENT.MESSAGE

This callback is triggered when a user sends a group message.

> Messages that you send are excluded from this callback. To display messages that you sent on the screen, use the data returned by the sendMessage method. The implementation logic here is consistent with that in the IM SDK.

```javascript
tls.on(TLS.EVENT.MESSAGE, async(data) => {
  const { nick,avatar,message,userID } = data
})
```

### TLS.EVENT.LIKE

This callback is triggered when a user gives a like to the anchor.

```javascript
tls.on(TLS.EVENT.LIKE, async(data) => {
  const { nick,avatar,value,userID } = data
})
```

### TLS.EVENT.SEND_GIFT

This callback is triggered when a user sends a gift to the anchor.

```javascript
tls.on(TLS.EVENT.SEND_GIFT, async(data) => {
  const { nick,avatar,value,userID } = data
})
```

### TLS.EVENT.ATTENT

This callback is triggered when a user follows the anchor.

```javascript
tls.on(TLS.EVENT.ATTENT, async(data) => {
  const { nick,avatar,value,userID } = data
})
```

### TLS.EVENT.BUY_GOODS

This callback is triggered when a user purchases a product.

```javascript
tls.on(TLS.EVENT.BUY_GOODS, async(data) => {
  const { nick,avatar,value,userID } = data
})
```

### TLS.EVENT.USE_COUPON

This callback is triggered when a user claims a coupon.

```javascript
tls.on(TLS.EVENT.USE_COUPON, async(data) => {
  const { nick,avatar,value,userID } = data
})
```

### TLS.EVENT.ADD_GOODS

This callback is triggered when the product recommended in the live stream changes.

```javascript
tls.on(TLS.EVENT.ADD_GOODS, async(data) => {
  const { nick,avatar,value } = data
})
```

### TLS.EVENT.KICKED

This callback is triggered when the account is used for login elsewhere.

```javascript
tls.on(TLS.EVENT.KICKED, async() => {
  
})
```

### TLS.EVENT.NETWORK_CHANGE

This callback is triggered when the network changes.

```javascript
tls.on(TLS.EVENT.NETWORK_CHANGE, async() => {
  
})
```

### TLS.EVENT.SDK_NOT_READY

This callback is triggered when the SDK is not ready.

```javascript
tls.on(TLS.EVENT.SDK_NOT_READY, async() => {
  
})
```

### TLS.EVENT.PROFILE_UPDATE

This callback is triggered when the personal profile is updated.

```javascript
tls.on(TLS.EVENT.PROFILE_UPDATE, async() => {
  
})
```

### TLS.EVENT.ERROR

This callback is triggered when the SDK encounters an error.

```javascript
tls.on(TLS.EVENT.ERROR, async(error) => {
  
})
```

### ${type}

This is the same-name event that is triggered when a custom message is called.

```javascript
tls.on(`${type}`, async(error) => {
  
})
```



## Component Methods

### sendMessage(message:string)

This method is used to send an on-screen comment.

```javascript
/**
 * When this method is called to send an on-screen comment, all group members can receive this text message.
 * @method sendMessage
 * @for TLS
 * @param msg - Required, which indicates the on-screen comment
 * @returns Promise
 */
const {nick,avatar,message} = await tls.sendMessage(msg);

```

### like(extension?:string)

This method is used to give the anchor a like.

> `extension` indicates the additional information when a like is given, for example, the user level.

```javascript
/**
 * When this method is called to give the anchor a like, all group members can receive this like message.
 * @method like
 * @for TLS
 * @param extension - Optional, which indicates the additional information when a like is given
 * @returns Promise
 */
const {nick,avatar} = await tls.like(extension);
```

### gift(extension?:string)

This method is used to send a gift to the anchor.

> `extension` indicates the additional information when a gift is sent, for example, the gift information.

```javascript
/**
 * When this method is called to send a gift to the anchor, all group members can receive this gift message.
 * @method gift
 * @for TLS
 * @param msg - Optional, which indicates the additional information when a gift is sent
 * @returns Promise
 */
const {nick,avatar} = await tls.gift(extension);
```

### exitRoom()

This method is used to exit the live room.

```javascript
/**
 * The anchor (group owner) cannot exit the live room.
 * @method exitRoom
 * @for TLS
 * @param 
 * @returns Promise
 */
const {status} = await tls.exitRoom();
```

### joinRoom()

This method is used to join a live room.

```javascript
/**
 * Join a live room.
 * @method joinRoom
 * @for TLS
 * @param 
 * @returns Promise
 */
const {userInfo,groupInfo} = await tls.joinRoom();
const { ownerInfo } = groupInfo;// Obtain the anchor information.
const { userID,nick,avatar } = ownerInfo
```

### getRoomInfo()

This method is used to obtain information about the live room.

```javascript
/**
 * Obtain basic information about the live room.
 * @method getRoomInfo
 * @for TLS
 * @param 
 * @returns Promise
 */
const {...ownerInfo} = await tls.getRoomInfo();
// `ownerInfo` indicates the anchor information.
const { userID,nick,avatar } = ownerInfo
```

### attention()

This method is used to follow the anchor.

```javascript
/**
 * Follow the anchor.
 * @method attention
 * @for TLS
 * @param 
 * @returns Promise
 */
const {nick,avatar} = await tls.attention();
```

### cancelAttention()

This method is used to unfollow the anchor.

```javascript
/**
 * Unfollow the anchor.
 * @method cancelAttention
 * @for TLS
 * @param 
 * @returns Promise
 */
const {nick,avatar} = await tls.cancelAttention();
```

### destroy()

This method is used to destroy the component.

```javascript
/**
 * Destroy the component.
 * @method destroy
 * @for TLS
 * @param 
 * @returns Promise
 */
tls.destroy(); 
```

### sendCustomMsgAndEmitEvent(eventName: string, extension?: string)

This method is used to send a custom message and trigger the callback event of the specified type.

>
> - eventName: event name
> - extension: additional information about the custom message sender

```javascript
/**
 * Send a custom message and trigger an event with the same name.
 * @method destroy
 * @for TLS
 * @param eventName: event name, someExtension: additional information
 * @returns Promise
 */
await tls.sendCustomMsgAndEmitEvent('eventName','someExtension')
```

## Built-in Objects

Built-in objects are created by TIM using `TIM.create`. They can use all TIM methods.

## Events

| Event | Description |
| ----------------------------------------------------- | ------------------------------------------------------------ |
| [TLS.EVENT.SDK_READY](#tls.event.sdk_ready) | This event is triggered when the initialization of the component is completed. This event corresponds to `TIM.EVENT.SDK_READY` of the IM SDK. You can call the SDK methods only after this event is triggered. |
| [TLS.EVENT.JOIN_GROUP](#tls.event.join_group) | This event is triggered when a user joins the group chat. |
| [TLS.EVENT.EXIT_GROUP](#tls.event.join_group) | This event is triggered when a user quits the group chat. |
| [TLS.EVENT.NOTIFACATION](#tls.event.notifacation) | This event is triggered when the notification is changed. |
| [TLS.EVENT.MESSAGE](#tls.event.message) | This event is triggered when a user sends a group message. |
| [TLS.EVENT.PROFILE_UPDATE](#tls.event.profile_update) | This event is triggered when the personal profile is updated. |
| [TLS.EVENT.ERROR](#tls.event.error) | This event is triggered when the SDK encounters an error. |
| [TLS.EVENT.KICKED](#tls.event.kicked) | This event is triggered when the account is used for login elsewhere. |
| [TLS.EVENT.NETWORK_CHANGE](#tls.event.network_change) | This event is triggered when the network is changed. |
| [TLS.EVENT.SDK_NOT_READY](#tls.event.sdk_not_ready) | This event is triggered when the SDK is not ready. |
| [TLS.EVENT.LIKE](#tls.event.like) | This event is triggered when a user gives a like to the anchor. |
| [TLS.EVENT.BUY_GOODS](#tls.event.buy_goods) | This event is triggered when a user purchases a product. |
| [TLS.EVENT.SEND_GIFT](#tls.event.send_gift) | This event is triggered when a user sends a gift to the anchor. |
| [TLS.EVENT.ATTENT](#tls.event.attent) | This event is triggered when a user follows the anchor. |
| [TLS.EVENT.ADD_GOODS](#tls.event.add_goods) | This event is triggered when a user unfollows the anchor. |
| [TLS.EVENT.USE_COUPON](#tls.event.use_coupon) | This event is triggered when a user claims a coupon. |

