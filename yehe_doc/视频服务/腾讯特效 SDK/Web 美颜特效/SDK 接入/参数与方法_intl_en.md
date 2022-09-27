## Initialization Parameters
`Config` of the SDK supports the following initialization parameters:
<table>
<thead><tr><th>Parameter</th><th>Description</th><th width=200px>Type</th><th>Required</th></tr></thead>
<tbody>
<tr>
<td>module</td>
<td>The module configuration.</td>
<td><pre style="color:white">
type ModuleConfig = {
  beautify: boolean // The default is `true`.
  segmentation: boolean // The default is `false`.
}
</pre></td>
<td>No. Default value: <code>{beautify: true, segmentation: false}</code>.</td></tr>
<tr>
<td>auth</td>
<td>The authentication information.</td>
<td><pre style="color:white;margin:0;">
type AuthConfig = {
  licenseKey: string // View in <a href="https://console.cloud.tencent.com/vcube/web"><strong> Web Licenses</strong></a> of the console.
  appId: string // View in <a href="https://console.cloud.tencent.com/developer"><strong>Account Information</strong></a> &gt; <strong>Basic Information</strong> of the console.
  authFunc:() => Promise<{
    signature:string,
    timestamp:string
  }> // See <a href="https://cloud.tencent.com/document/product/616/71370">Configuring and Using a License</a>
}
</pre></td>
<td>Yes</td></tr><tr>
<td>input</td>
<td>The input.</td>
<td>MediaStream|HTMLImageElement|String</td>
<td>No</td></tr>
<tr>
<td>camera</td>
<td>The built-in camera configuration.</td>
<td><pre style="color:white;margin:0">
type CameraConfig = {
	width: number, // The video width.
	height: number, // The video height.
	mirror: boolean, // Whether to horizontally flip the video.
    frameRate: number // The capturing frame rate.
}
</pre></td>
<td>No</td></tr><tr>
<td>beautify</td>
<td>The beautification effects.</td>
<td><pre style="color:white;margin:0">
type BeautifyOptions = {
	whiten?: number, // The brightening effect. Value range: 0-1.
	dermabrasion?: number // The smooth skin effect. Value range: 0-1.
	lift?: number // The slim face effect. Value range: 0-1.
	shave?: number // The face width. Value range: 0-1.
	eye?: number // The big eyes effect. Value range: 0-1.
	chin?: number // The chin effect. Value range: 0-1.
}
</pre></td>
<td>No</td></tr>
<tr>
<td>background</td>
<td>The background configuration.</td>
<td><pre style="color:white">
type BackgroundOptions = {
	type: 'image' | 'blur' | 'transparent', 
	src?: string
}
</pre></td>
<td>No</td>
</tr>
<tr>
<td>loading</td>
<td>The configuration of the built-in loading icon.</td>
<td><pre style="color:white;margin:0">
type loadingConfig = {
	enable: boolean,
	size?: number
	lineWidth?: number
	strokeColor?: number
}
</pre></td>
<td>No</td>
</tr>
</tbody>
</table>

## Callbacks
```javascript
let effectList = [];
let filterList = [];
// Using the callbacks of the SDK
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
sdk.on('cameraReady', async () => {
	// By getting the output stream in the `cameraReady` callback, you can display a video image sooner, but the initialization parameters have not taken effect at this point.
	// You can choose this method if you want to display a video image as soon as possible but do not need to apply effects to the video the moment it is displayed.
	// You don’t need to update the stream after the effects start to work.
	const arStream = await ar.getOutput();
	// Play the stream locally
	// localVideo.srcObject = arStream

})
sdk.on('ready', () => {
	// Get the output stream in the `ready` callback. The initialization parameters have taken effect at this point.
	// You can get the output stream in `ready` if you want your video to show effects the moment it is displayed but do not expect it to be displayed as soon as possible.
	// Between the two methods, choose the one that fits your needs.
	const arStream = await ar.getOutput();
	// Play the stream locally
	// localVideo.srcObject = arStream

	// Call `setBeautify`, `setEffect`, or `setFilter` in the `ready` callback
	sdk.setBeautify({
		whiten: 0.3
	});
	sdk.setEffect({
		id: effectList[0].EffectId,
		intensity: 0.7
	});
	sdk.setEffect({
		id: effectList[0].EffectId,
		intensity: 0.7,
		filterIntensity: 0.5 // In v0.1.18 and later, you can use this parameter to set the filter strength of a special effect. If you do not pass this parameter, the strength specified for the effect will be used.
	});
	sdk.setFilter(filterList[0].EffectId, 0.5)
})

```

| Callback  | Description                            | Return Value |
| ----- |-------------------------------| --------- |
| created | The SDK completed authentication and an instance was created.            | -         |
| cameraReady | The SDK generated a video output (the video is not yet processed). | -         |
| ready | Detection has been initialized. Effects are now applied to the output video. You can change the effect settings.           | -         |
| error | The SDK encountered an error.                   | The error object. |


## APIs
<table>
<thead><tr><th>API</th><th width=200px>Request Parameters</th><th>Response Parameters</th>
<th>　　　　Description　　　　</th></tr></thead>
<tbody><tr>
<td>async getOutput(fps)</td>
<td>- fps (optional): The output frame rate.</td>
<td>MediaStream|String</td>
<td>This API is only available in the web SDK.</td>
</tr>
<tr>
<td>setBeautify(options)</td>
<td>options: The beautification settings.
<pre style="color: white;margin: 0px;overflow: scroll;display: block;width: 300px;">
type BeautifyOptions = {
  whiten?: number, // The brightening effect. Value range: 0-1.
  dermabrasion?: number // The smooth skin effect. Value range: 0-1.
  lift?: number // The slim face effect. Value range: 0-1.
  shave?: number // The face width. Value range: 0-1.
  eye?: number // The big eyes effect. Value range: 0-1.
  chin?: number // The chin effect. Value range: 0-1.
}</pre>
</td>
<td>-</td>
<td>To configure beautification effects, you need to enable the effect module.</td>
</tr>
<tr>
<td>setEffect(effects, callback)</td>
<td><ul style="margin:0">
   <li>effects: Effect ID | Effect object | Effect ID / An effect array
	<pre style="color: white;margin: 0px;overflow: scroll;display: block;width: 300px;">
effect:{
	id: string,
	intensity: number, // The effect strength. Value range: 0-1. Default: 1.
	filterIntensity: number // The filter strength of an effect (supported in v0.1.18 and later). Value range: 0-1. By default, this parameter is the same as `intensity`.
}</pre>
	<li>callback: The callback for successful configuration.</ul></td>
<td>-</td>
<td>To configure special effects, you need to enable the effect module.</td>
</tr>
<tr>
<td>setBackground(options)</td>
<td><pre style="color:white;margin:0">
{
	type: 'image|blur|transparent',
	src: string // This parameter is required only if `type` is `image`.
}</pre>
</td>
<td>-</td>
<td>To configure the background, you need to enable the keying module.</td>
</tr>
<tr>
<td>setFilter(id, intensity, callback)</td>
<td>
   <li>id: The filter ID.
   <li>intensity: The filter strength. Value range: 0-1.
   <li>callback: The callback for successful configuration.</td>
<td>-</td>
<td>This API is used to set the filter.</td>
</tr>
<tr>
<td>getEffectList(params)</td>
<td><pre style="color:white;margin:0">
{
	PageNumber: number,
	PageSize: number,
	Name: '',
	Label: Array,
	Type: 'Custom|Preset'
}</pre>
</td>
<td>A list of effects.</td>
<td>This API is used to get a list of effects.</td>
</tr>
<tr>
<td>getEffect(effectId)</td>
<td>effectId: The effect ID.</td>
<td>The information of the effect queried.</td>
<td>This API is used to get the information of a specific effect.</td>
</tr>
<tr>
<td>getCommonFilter()</td>
<td>-</td>
<td>A list of the built-in filters.</td>
<td>This API is used to get the built-in filters.</td>
</tr>
<tr>
<td>async updateInputStream(src:MediaStream) <br><b>(supported since v0.1.19)</b></td>
<td>src: The new input stream (`MediaStream`).</td>
<td>-</td>
<td>This API is used to update the input stream.</td>
</tr>
<tr>
<td>disable()</td>
<td>-</td>
<td></td>
<td>This API is used to disable facial detection, which can reduce CPU usage. After it’s disabled, the original stream will be returned.</td>
</tr>
<tr>
<td>enable()</td>
<td>-</td>
<td></td>
<td>This API is used to enable facial detection. After it’s enabled, the stream returned will have been processed.</td>
</tr>
<tr>
<td>destroy()</td>
<td>-</td>
<td>-
</td>
<td>This API is used to terminate the SDK instance and clear its texture resources.</td>
</tr>
</tbody></table>


## Error Handling
The error object returned by the error callback includes the error code and error message, which facilitate troubleshooting.
```javascript
sdk.on('error', (error) => {
	// Handle an error in the error callback
	const {code, message} = error
	...
})
```

| Error Code  | Description                | Remarks  |
| ----- | ------------------- | --------- |
| 10000001 | Unsupported browser.  | Chrome, Firefox, or Safari is recommended.      |
| 10000002 | Missing render context. | - |
| 10000003 | Rendering taking too long. | Consider reducing the resolution or disabling some features. |
| 10000005 | Input parsing error. | -       |
| 10001101 | Error configuring special effects. | -         |
| 10001102 | Error configuring filters.   | - |
| 10001103 | Invalid effect strength.   | - |
| 10001201 | Failed to start the camera.   | - |
| 10001202 | The camera stopped.   | - |
| 20002001 | Missing authentication parameter. | - |
| 20001001 | Authentication failed.   | Make sure you have created a license and the signature is correct. |
| 20001002 | API request failed. | The error callback will return the data returned by the API. For details, see [API Error Codes](https://intl.cloud.tencent.com/document/product/1143/50107). |

### Handling the missing render context error
On some computers, if the SDK is in the background for a long time, the `contextlost` error may occur. In such cases, you can call `ArSdk.prototype.resetCore(input: MediaStream)` to resume rendering.
```JavaScript
sdk.on('error', async (error) => {
	if (error.code === 10000002) {
		const newInput = await navigator.mediaDevices.getUserMedia({...})
		await sdk.resetCore(newInput)
	}
})
```
