## Overview
This feature allows you to convert audio into Apple ARKit’s 52 blendshapes. For details, see [ARFaceAnchor](https://developer.apple.com/documentation/arkit/arfaceanchor/blendshapelocation). You can perform further development based on the blendshape data. For example, you can pass the data to Unity to drive your model.

## Integration Methods
### Method 1: Integrate the Tencent Effect SDK
The capability of converting audio to expressions is built into the Tencent Effect SDK.
1. Download the complete edition of the [Tencent Effect SDK](https://mediacloud-76607.gzc.vod.tencent-cloud.com/TencentEffect/Android/latest/xmagic_ALL_android_latest.zip).
2. Integrate the SDK. For detailed directions, see [Integrating Tencent Effect SDK](https://intl.cloud.tencent.com/document/product/1143/45385).

### Method 2: Integrate the Audio-to-Expression SDK
If you do not need other Tencent Effect capabilities, you can integrate the Audio-to-Expression SDK, the AAR file of which is about 6 MB. You can contact us to get the SDK.

## Directions

1. **Set the license**. For details, see [Integrating Tencent Effect SDK - Step 1. Authenticate](https://intl.cloud.tencent.com/document/product/1143/45385#.E6.AD.A5.E9.AA.A4.E4.B8.80.EF.BC.9A.E9.89.B4.E6.9D.83).
2. **Configure the model file**: Copy the model files from `assets` to a private directory of your application, such as `context.getFilesDir() + "/my_models_dir/audio2exp"`. Then, call the `init(String modelPath)` API of `Audio2ExpApi`, passing in `context.getFilesDir() + "/my_models_dir"`.
You can find the model files in the SDK package.
![](https://qcloudimg.tencent-cloud.cn/raw/383c572788f49611abd56626266f44a7.png)

## APIs
<table>
<thead>
<tr>
<th>API</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td><code>public int Audio2ExpApi.init(String modelPath);</code></td>
<td>Initializes the SDK. You need to pass in the path of the model files when calling this API. `0` indicates the initialization is successful.</td>
</tr>
<tr>
<td><code>public float[] Audio2ExpApi.parseAudio(float[] inputData);</code></td>
<td>The input is audio, which must be one-channel and have a sample rate of 16 Kbps. The array length is 267 (267 sampling points). The output is a float array with 52 elements, which correspond to 52 blendshapes. The value range of the elements is -1 to 1, and their sequence is specified by <a href="https://developer.apple.com/documentation/arkit/arfaceanchor/blendshapelocation">Apple</a>.</td>
</tr>
<tr>
<td><code>public int Audio2ExpApi.release();</code></td>
<td>Releases the resources. Call this API when you no longer need to use the capability.</td>
</tr>
</tbody></table>

## Integration Code Sample
```
@Override
protected void onCreate(Bundle savedInstanceState) {
		super.onCreate(savedInstanceState);
		setContentView(R.layout.activity_main);
		findViewById(R.id.button).setOnClickListener(new OnClickListener() {
				@Override
				public void onClick(View view) {
						TELicenseCheck.getInstance().setTELicense(MainActivity.this, "https://license.vod2.myqcloud.com/license/v2/1258289294_1/v_cube.license", "3c16909893f53b9600bc63941162cea3", new TELicenseCheckListener() {
								@Override
								public void onLicenseCheckFinish(int errorCode, String s) {
										Log.d(TAG, "onLicenseCheckFinish: errorCode = "+errorCode+",msg="+s);
										if (errorCode == TELicenseCheck.ERROR_OK) {
												//license check success
												Audio2ExpApi audio2ExpApi = new Audio2ExpApi();
												int err = audio2ExpApi.init(MainActivity.this.getFilesDir() +"/models");
												Log.d(TAG, "onLicenseCheckFinish: err="+err);
												//TODO start record and parse audio data
										} else {
												// license check failed
										}
								}
						});
				}
		});
}
```

>? For the full code sample, see [Demos](https://intl.cloud.tencent.com/document/product/1143/45374).
- For audio recording, refer to `com.tencent.demo.avatar.audio.AudioCapturer`.
- For more information on how to use the APIs, see `com.tencent.demo.avatar.activity.Audio2ExpActivity` and its related classes.