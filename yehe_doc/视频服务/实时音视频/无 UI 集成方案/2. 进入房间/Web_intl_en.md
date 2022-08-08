This document describes how to enter a TRTC room. Only after entering an audio/video room can a user subscribe to the audio/video streams of other users in the room or publish his or her own audio/video streams.
![](https://qcloudimg.tencent-cloud.cn/raw/d7353029f13bf9950d4ada0b05de7077.png)

You will encounter two types of objects while using the TRTC web SDK:
- Client object, which represents a local client. The [Client](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html) class provides APIs for room entry, local stream publishing, remote stream subscription, etc.
- Stream object, which represents an audio/video stream object. There are local stream objects ([LocalStream](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html)) and remote stream objects ([RemoteStream](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/RemoteStream.html)). The `Stream` class provides APIs for stream-related actions, including audio/video playback control.

[](id:step1)
## Step 1. Create a client object
Create a [client](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html) object using [TRTC.createClient()](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/TRTC.html#createClient). Set the parameters as follows:

| Parameter | Description | Notes | Data Type | Example | Default Value | Remarks |
|---------|---------|---------|---------|---------|---------|---------|
| mode | The application scenario. | The `rtc` mode is for one-to-one audio/video calls or conferences with up to 300 participants.<br> The `live` mode is for live streaming to up to 100,000 people. | string | rtc | rtc | -|
| SDKAppID | The application ID. | You can view your application ID in the <a href="https://console.cloud.tencent.com/trtc/app">TRTC console</a>. If you don’t have an application yet, click **Create application** to create one.| Number | 1400000123 | - | Required |
| userId | The user ID. | It can contain only letters, digits, underscores, and hyphens. <br>**Note**: In TRTC, a user cannot use the same user ID to enter the same room on two different devices at the same time. | String | `denny` or `123321`| - | Required |
| userSig | The authentication ticket needed to enter a room. | For how to calculate `UserSig`, see [UserSig](https://intl.cloud.tencent.com/document/product/647/35166). | String |eJyrVareCeYrSy1SslI... | - | Required |
| useStringRoomId | Whether to use string type room IDs. | Specifies whether to use room IDs whose data type is string. |boolean| true | false | - |

For more information on the parameters, see [TRTC.createClient()](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/TRTC.html#createClient). 

```javascript
// Create a client object in the call mode
const client = TRTC.createClient({
  mode: 'rtc',
  sdkAppId,
  userId,
  userSig
});

// Create a client object in the live streaming mode
const client = TRTC.createClient({
  mode: 'live',
  sdkAppId,
  userId,
  userSig
});
```

[](id:step2)
## Step 2. Enter a room

Call [Client.join()](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#join) to enter a TRTC room. Below are the request parameters:

| Parameter | Description | Notes | Data Type | Example | Default Value | Remarks |
|---------|---------|---------|---------|---------|---------|---------|
| roomId | The room ID. | The data type is number by default. If you want to use string type room IDs, set the `useStringRoomId` parameter of `createClient()` to `true`.<br> - A numeric room ID must be an integer from 1 to 4294967294.<br> - A string type room ID cannot be longer than 64 bytes and can contain only the following characters:<br> Letters (a-z and A-Z), digits (0-9), spaces, and !#$%&()+-:;<=.>?@[]^_{}\|~, |   number/string  | 3364 or class-room | - | Required |
| role | The user role. | This parameter is required only if `mode` is set to `live`. Two roles are supported currently: `anchor` and `audience`. | string | anchor |  audience | - |

For more information on the parameters, see [Client.join()](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#join). 

```javascript
// Using the Promise syntax
client
  .join({ roomId })
  .then(() => {
    console.log('Entered the room successfully');
  })
  .catch(error => {
    console.error('Failed to enter the room. Please try again later.' + error);
  });

// We recommend you use the async/await syntax
try {
  await client.join({ roomId });
  console.log('Entered the room successfully');
} catch (error) {
  console.error('Failed to enter the room. Please try again later.' + error);
}

// Enter the room as an anchor
try {
  await client.join({ 
    roomId,
    role: 'anchor' 
  });
  console.log('Entered the room successfully');
} catch (error) {
  console.error('Failed to enter the room. Please try again later.' + error);
}
```
