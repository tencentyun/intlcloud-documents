## Integrating the SDK
[](id:step1)
### Step 1. Import the SDK
```javascript
import { ArSdk } from 'tencentcloud-webar';// The SDK class
```
If your project does not need compilation, you can also import the SDK using the following method:
```html
<script charset="utf-8" src="https://webar-static.tencent-cloud.com/ar-sdk/resources/latest/webar-sdk.umd.js"></script>
```

[](id:step2)
### Step 2. Initialize an instance
1. Initialize an SDK instance.
```javascript
// Get the authentication information
const authData = {
	licenseKey: 'xxxxxxxxx',
	appId: 'xxx',
	authFunc: authFunc // For details, see “Configuring and Using a License - Signature”
};
// The input stream
const stream = await navigator.mediaDevices.getUserMedia({
	audio: true,
	video: { width: w, height: h }
})

const config = {
    module: { // New in v0.2.0
		beautify: true, // Whether to enable the effect module, which offers beautification and makeup effects as well as stickers
		segmentation: true // Whether to enable the keying module, which allows you to change the background
	},
	auth: authData, // The authentication information
    input: stream, // The input stream
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
```
>! The loading of the effect and segmentation modules takes time and consumes resources. You can enable only the module you need during initialization. A module not enabled will not be loaded or initialized, nor can you use its features.

2. For `input`, you can also pass in `string|HTMLImageElement` to process images.
```javascript
const config = {
	auth: authData, // The authentication information
    input: 'https://xxx.png', // The input stream
}
const sdk = new ArSdk(
	// Pass in a config object to initialize the SDK
	config
)

// You can display the effect and filter list in the `created` callback. For details, see “SDK Integration - Parameters and APIs”.
sdk.on('created', () => {
    // Get the built-in makeup effects
    sdk.getEffectList({
        Type: 'Preset',
        Label: 'Makeup',
    }).then(res => {
        effectList = res
    });
    // Get the built-in filters
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

[](id:step3)
### Step 3. Play the stream
Call `ArSdk.prototype.getOutput` to get the output stream.
The output streams you get in different callbacks vary slightly. Choose the one that fits your needs.

- If you want to display a video image as quickly as possible, get and play the stream in the `cameraReady` callback. Because the SDK hasn’t loaded the resources or completed initialization, only the original video can be played.
```javascript
sdk.on('cameraReady', async () => {
	// By getting the output stream in the `cameraReady` callback, you can display a video image sooner. However, because the initialization parameters have not taken effect at this point, the output stream obtained will be the same as the original stream.
	// You can choose this method if you want to display a video image as soon as possible but do not need to apply effects to the video the moment it is displayed.
	// You don’t need to update the stream after the effects start to work.
	const output = await ar.getOutput();
    // Use `video` to preview the output stream
	const video = document.createElement('video')
    video.setAttribute('playsinline', '');
    video.setAttribute('autoplay', '');
    video.srcObject = output
    document.body.appendChild(video)
    video.play()
})
```
- If you want to play the video after initialization and effect application, get and play the output stream in the `ready` playback.
```javascript
sdk.on('ready', async () => {
    // If you get the output stream in the `ready` callback, because the initialization parameters have taken effect at this point, the output stream obtained will show effects.
	// The `ready` callback occurs later than `cameraReady`. You can get the output stream in `ready` if you want your video to show effects the moment it is displayed but do not expect it to be displayed as soon as possible.
	const output = await ar.getOutput();
    // Use `video` to preview the output stream
    const video = document.createElement('video')
    video.setAttribute('playsinline', '');
    video.setAttribute('autoplay', '');
    video.srcObject = output
    document.body.appendChild(video)
    video.play()
})
```

[](id:step4)
### Step 4. Get the output
After getting the `MediaStream`, you can use a live streaming SDK (for example, TRTC web SDK or LEB web SDK) to publish the stream.
```javascript
const output = await sdk.getOutput()
```


>!
>- If the input passed in is an image, a string-type data URL will be returned. Otherwise, `MediaStream` will be returned.
>- The video track of the output stream is processed in real time by the Tencent Effect SDK. The audio track (if any) is kept.
>- `getOutput` is an async API. The output will be returned only after the SDK is finished with initialization and can generate a stream.
>- You can pass an `FPS` parameter to `getOutput` to specify the output frame rate (for example, 15). If you do not pass this parameter, the original frame rate will be kept.
>- You can call `getOutput` multiple times to generate streams of different frame rates for different scenarios (for example, you may use a high frame rate for preview and a low frame rate for stream publishing).

[](id:step5)
### Step 5. Configuring filters and effects
See [Configuring Filters and Effects](https://intl.cloud.tencent.com/document/product/1143/50104).

## Updating the Input Stream (supported since v0.1.19)
If you want to feed a new input stream to the SDK after changing the device or enabling/disabling the camera, you don’t need to initialize the SDK again. Just call `sdk.updateInputStream` to update the input stream.
The following code shows you how to use `updateInputStream` to update the input stream after switching from the computer’s default camera to an external camera.

```javascript

async function getVideoDeviceList(){
    const devices = await navigator.mediaDevices.enumerateDevices()
    const videoDevices = []
    devices.forEach((device)=>{
        if(device.kind === 'videoinput'){
            videoDevices.push({
                label: device.label,
                id: device.deviceId
            })
        }
    })
    return videoDevices
}

async function initDom(){
    const videoDeviceList = await getVideoDeviceList()
    let dom = ''
    videoDeviceList.forEach(device=>{
        dom = `${dom}
        <button id=${device.id} onclick='toggleVideo("${device.id}")'>${device.label}<nbutton>
        `
    })
    const div = document.createElement('div');
    div.id = 'container';
    div.innerHTML = dom;
    document.body.appendChild(div);
}

async function toggleVideo(deviceId){
    const stream = await navigator.mediaDevices.getUserMedia({
        video: {
            deviceId,
            width: 1280,
            height: 720,
          }
    })
	// Call an API provided by the SDK to change the input stream. The SDK will stop the existing tracks.
	// After the input stream is updated, you don’t need to call `getOutput` again. The SDK will get the output.
    sdk.updateInputStream(stream) 
}

initDom()

```

## Pausing and Resuming Detection
You can call `disable` and `enable` to manually pause and resume detection. Pausing detection can reduce CPU usage.
```html
<button id="disable">Disable detection</button>
<button id="enable">Enable detection</button>
```
```javascript
// Disable detection and output the original stream
disableButton.onClick = () => {
    sdk.disable()
}
// Enable detection and output a processed stream
enableButton.onClick = () => {
    sdk.enable()
}
```
