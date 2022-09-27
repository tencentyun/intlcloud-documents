You can choose this initialization mode if you want to use the SDK with a device’s built-in camera or if your business involves a lot of interaction with the built-in camera.

[](id:step1)
## Step 1. Import the SDK
```javascript
import { ArSdk } from 'tencentcloud-webar';// The SDK class
```
If your project does not need compilation, you can also import the SDK using the following method:
```html
<script charset="utf-8" src="https://webar-static.tencent-cloud.com/ar-sdk/resources/latest/webar-sdk.umd.js"></script>
```

[](id:step2)
## Step 2. Initialize an Instance
Initialize an SDK instance.
```javascript
// Get the authentication information
const authData = {
	licenseKey: 'xxxxxxxxx',
	appId: 'xxx',
	authFunc: authFunc // For details, see “Configuring and Using a License - Signature”
};

const config = {
    module: { // New in v0.2.0
		beautify: true, // Whether to enable the effect module, which offers beautification and makeup effects as well as stickers
		segmentation: true // Whether to enable the keying module, which allows you to change the background
	},
    auth: authData, // The authentication information
    camera: { // Pass in the camera parameters
        width: 1280,
        height: 720
    },
	beautify: { // The effect parameters for initialization (optional)
		whiten: 0.1,
		dermabrasion: 0.3,
		eye: 0.2,
		chin: 0,
		lift: 0.1,
		shave: 0.2
	}
}
const sdk = new ArSdk(
	// Pass in a config object to initialize the SDK
	config
)

let effectList = [];
let filterList = [];

sdk.on('created', () => {
    // You can display the effect and filter list in the `created` callback. For details, see “SDK Integration - Parameters and APIs”.
    sdk.getEffectList({
        Type: 'Preset',
        Label: 'Makeup',
    }).then(res => {
        effectList = res
    });
    sdk.getCommonFilter().then(res => {
        filterList = res
    })
})

// Call `setBeautify`, `setEffect`, or `setFilter` in the `ready` callback
// For details, see “SDK Integration - Configuring Filters and Effects”
sdk.on('ready', () => {
    // Configuring beautification effects
    sdk.setBeautify({
        whiten: 0.2
    });
    // Configuring special effects
    sdk.setEffect({
        id: effectList[0].EffectId,
        intensity: 0.7
    });
    // Configuring filters
    sdk.setFilter(filterList[0].EffectId, 0.5)
})
```
>! 
>- The loading of the effect and segmentation modules takes time and consumes resources. You can enable only the module you need during initialization. A module not enabled will not be loaded or initialized.
>- If you specify the `camera` parameter of `config`, the video data the SDK captures from the device’s camera will be used as the input. We also offer some basic device management APIs. For details, see [Step 5. Control Devices](#step5).

[](id:step3)
## Step 3. Play the Stream
The SDK offers players for quick preview on a webpage. The players you get in different callbacks vary slightly. Choose the one that fits your needs.

- If you want to display a video image as quickly as possible, get the player in the `cameraReady` callback. Because the SDK hasn’t loaded the resources or completed initialization at this point, the player can only play the original video.
```javascript
sdk.on('cameraReady', async () => {
	// Initialize a player of the SDK. `my-dom-id` is the ID of the player’s container.
    const player = await sdk.initLocalPlayer('my-dom-id')
    // Play the video
    await player.play()
})
```
- If you want to play the video after initialization and effect application, get the player in the `ready` playback.
```javascript
sdk.on('ready', async () => {
    // Initialize a player of the SDK. `my-dom-id` is the ID of the player’s container.
    const player = await sdk.initLocalPlayer('my-dom-id')
    // Play the video
    await player.play()
})
```

>! 
>- The player obtained by `initLocalPlayer` is muted by default. Unmuting the player may result in echoes.
>- The player obtained is integrated with the `sdk.getOutput()` API.

The player object obtained by `initLocalPlayer` is integrated with the following APIs:

| API          | Description                       | Request Parameter        | Return Value           |
| :-------------- | :------------------------- | :---------- | :--------------- |
| play            | Plays the video.                       | -           | Promise;         |
| pause           | Pauses the video. This does not stop the stream, and playback can be resumed. | -           | -                |
| stop            | Stops the video. This stops the stream.       | -           | -                |
| mute            | Mutes playback.                       | -           | -                |
| unmute          | Unmutes playback.                   | -           | -                |
| setMirror       | Sets the mirror mode.                   | true\|false | -                |
| getVideoElement | Gets the built-in video element.       | -           | HTMLVideoElement |
| destroy         | Terminates the instance.                       | -           | -                |

>! The player’s behaviors are affected by [camera settings](#step5). Camera settings prevail over the settings of `LocalPlayer`.
>- For example, after you call `camera.muteVideo` to disable video, playback will not start even if you call `play`.
>- After you call `camera.unmuteVideo` to enable video, the player will resume playback automatically.
> Therefore, if you configure `camera`, you don’t need to manually control `localPlayer`.

[](id:step4)
## Step 4. Get the Output
If you need to publish the stream, call `getOutput` to get the output stream.
After getting the `MediaStream`, you can use a live streaming SDK (for example, TRTC web SDK or LEB web SDK) to publish the stream.

```javascript
const output = await sdk.getOutput()
```
>!
>- If you use the built-in camera, the type of all media returned by `getOutput` is `MediaStream`.
>- The video track of the output stream is processed in real time by the Tencent Effect SDK. The audio track (if any) is kept.
>- `getOutput` is an async API. The output will be returned only after the SDK is finished with initialization and can generate a stream.
>- You can pass an `FPS` parameter to `getOutput` to specify the output frame rate (for example, 15). If you do not pass this parameter, the original frame rate will be kept.

[](id:step5)
## Step 5. Control Devices
You can use an `sdk.camera` instance to enable and disable the camera or perform other camera operations.
```javascript
const output = await sdk.getOutput()
// Your business logic
// ...

// `sdk.camera` will have been initialized after `getOutput`. You can get an instance directly.
const cameraApi = sdk.camera

// Get the device list
const devices = await cameraApi.getDevices()
console.log(devices)
// Disable the video track
// cameraApi.muteVideo()
// Enable the video track
// cameraApi.unmuteVideo()
// Change to a different camera by specifying the device ID (if there are multiple cameras)
// await cameraApi.switchDevices('video', 'your-device-id')
```
If you want to get an `sdk.camera` instance as soon as possible, you can get it in the `cameraReady` callback.
```javascript
// Initialization parameters
// ...
const sdk = new ArSdk(
    config
)

let cameraApi;
sdk.on('cameraReady', async () => {
    cameraApi = sdk.camera
    // Get the device list
    const devices = await cameraApi.getDevices()
    console.log(devices)
    // Disable the video track
    // cameraApi.muteVideo()
    // Enable the video track
    // cameraApi.unmuteVideo()
    // Change to a different camera by specifying the device ID (if there are multiple cameras)
    // await cameraApi.switchDevices('video', 'your-device-id')
})
```
The built-in `camera` offers the following APIs for you to control the camera.
<table>
<thead><tr><th>API</th><th>Description</th><th>Request Parameter</th><th>Return Value</th></tr></thead>
<tbody>
<tr>
<td>getDevices</td>
<td>Gets all the devices.</td>
<td>-</td>
<td>Promise&lt;Array&lt;MediaDeviceInfo&gt;&gt;</td>
</tr><tr>
<td>switchDevice</td>
<td>Changes to a different device.</td>
<td><code>type:string, deviceId:string</code></td>
<td>Promise
</td>
</tr>
<tr>
<td>muteAudio</td>
<td>Mutes the camera stream.</td>
<td>-</td>
<td>-</td>
</tr><tr>
<td>unmuteAudio</td>
<td>Unmutes the camera stream.</td>
<td>-</td>
<td>-</td>
</tr><tr>
<td>muteVideo</td>
<td>Disables the video of the camera stream. This only disables the video track. It does not stop the stream.</td>
<td>-</td>
<td>-</td>
</tr><tr>
<td>unmuteVideo</td>
<td>Enables the video of the camera stream.</td>
<td>-</td>
<td>-</td>
</tr><tr>
<td>stopVideo</td>
<td>Disables the camera. This stops the video stream, but the audio stream is not affected.</td>
<td>-</td>
<td>-</td>
</tr>
<tr>
<td>restartVideo</td>
<td>Enables the camera. This API can only be called after `stopVideo`.</td>
<td>-</td>
<td>Promise</td>
</tr>
<tr>
<td>stop</td>
<td>Disables the camera and the audio device.</td>
<td>-</td>
<td>-</td>
</tr>
</tbody></table>



