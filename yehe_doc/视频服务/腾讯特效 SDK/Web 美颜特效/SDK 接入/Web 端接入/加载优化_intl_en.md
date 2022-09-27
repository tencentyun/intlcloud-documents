[](id:normal)
## Regular Mode
In regular mode, if you call `getOutput` to get the output stream in the `cameraReady` callback, because the effects are not working yet at this point, the stream obtained will be the same as the input stream fed into the SDK. After the effects start to work, the SDK will apply them to the output stream automatically. You don’t need to call `getOutput` again. You can use this method if you want to display a video image as soon as possible but do not need to apply effects to the video the moment it is played.

In contrast, if you call `getOutput` in the `ready` callback, the output stream obtained will have been processed. Because the `ready` callback occurs later than `cameraReady`, you can call `getOutput` in the `ready` callback if you want to apply effects to the video the moment it is displayed, but do not expect the video to be played as soon as possible.
![](https://qcloudimg.tencent-cloud.cn/raw/38365734db212ba293fbd283cdcbf3a9.jpg)

Sample code:

```javascript
// Get the authentication information
const authData = {
	licenseKey: 'xxxxxxxxx',
	appId: 'xxx',
	authFunc: authFunc // For details, see “Configuring and Using a License - Signature”
};

// When initializing the SDK in regular mode, pass in the input or camera parameters
const config = {
	auth: authData, // The authentication information
    beautify: { // The effect parameters
        whiten: 0.1,
        dermabrasion: 0.5,
        lift: 0,
        shave: 0,
        eye: 0.2,
        chin: 0,
    },
    input: inputStream // Prepare the stream data fed into the SDK as the input. For details, see “SDK Integration - Parameters and APIs”.
}
const sdk = new ArSdk(
	// Pass in a config object to initialize the SDK
	config
)
// After authentication succeeds, the SDK will trigger the `created` callback immediately
sdk.on('created', () => {
    // Pull and display the filter and effect list in the `created` callback
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

// The data you get by calling `getOutput` in different callbacks vary slightly. Choose the one that fits your needs.
sdk.on('cameraReady', async () => {
	const output = await sdk.getOutput() // The effect parameters have not taken effect
    // Play the stream
    ...
})
sdk.on('ready', async () => {
    const output = await sdk.getOutput() // The effect parameters have taken effect
    // Play the stream
    ...
    // Call `setBeautify`, `setEffect`, or `setFilter` in the `ready` callback
})

```

[](id:preliminary)
## Pre-Initialization (supported since v0.2.0)
When the SDK is loaded for the first time, it needs to download static resources in order to initialize the detection module. As a result, the loading of the SDK is affected by network conditions. Given that in some scenarios, you may want to display a video image as soon as possible, we offer a pre-initialization plan that loads static resources in advance.

**Use cases for pre-initialization**
- Case 1: The effect SDK is not needed when the webpage is initialized. A video is displayed only after the user performs certain operation.
- Case 2: Effects are needed for page B, and page B is directed from page A.
In such cases, you can load resources in advance (as early as possible), feed an input stream to the SDK when necessary, and then get a processed output stream.

For example, in case 1, you can load resources when the webpage is initialized; in case 2, you can get an SDK instance on page A and pass it to page B.
![](https://qcloudimg.tencent-cloud.cn/raw/6cc0d286584d1a10db1e5764b167f092.jpg)

**The code below works for case 1**
```html
<button id="start">Enable the camera</button>
```
```javascript
// Get the authentication information
const authData = {
	licenseKey: 'xxxxxxxxx',
	appId: 'xxx',
	authFunc: authFunc // For details, see “Configuring and Using a License - Signature”
};

// Do not pass in the input or camera parameters when initializing the SDK. After an instance is obtained, the SDK will start loading the necessary resources.
const config = {
	auth: authData, // The authentication information
    beautify: { // The effect parameters
        whiten: 0.1,
        dermabrasion: 0.5,
        lift: 0,
        shave: 0,
        eye: 0.2,
        chin: 0,
    },
}
const sdk = new ArSdk(
	// Pass in a config object to initialize the SDK
	config
)
// After authentication succeeds, the SDK will trigger the `created` callback immediately
sdk.on('created', () => {
    // Pull and display the filter and effect list in the `created` callback
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
// `resourceReady` indicates that the necessary resources are ready. After receiving this callback, you can call `initCore` to feed an input stream to the SDK.
sdk.on('resourceReady', () => {
})
// In this mode, the SDK will trigger the `ready` callback only after `initCore` is called.
sdk.on('ready', async () => {
	const output = await sdk.getOutput() // The effects have been applied.
    // Play the stream
    ...
    // Call `setBeautify`, `setEffect`, or `setFilter` in the `ready` callback
})
// Feed stream data to the SDK when the user turns the camera on
document.getElementById('start').onclick = async function(){
    const devices = await navigator.mediaDevices.enumerateDevices()
    const cameraDevice = devices.find(d=>d.kind === 'videoinput')
    navigator.mediaDevices.getUserMedia({
        audio: false,
        video: {
            deviceId: cameraDevice.deviceId
            ... // Other configuration
        }
    }).then(mediaStream => {
        // In this mode, make sure you call `initCore` after the `resourceReady` callback.
        sdk.initCore({
            input: mediaStream // Prepare the stream data fed into the SDK as the input. For details, see “SDK Integration - Parameters and APIs”.
        })
    })    
}
```

