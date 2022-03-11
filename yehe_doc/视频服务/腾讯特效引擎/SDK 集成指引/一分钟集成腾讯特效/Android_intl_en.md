## Preparations for Integration
**File preparations**:
<table>
<tbody><tr><th>File Type</th><th>Description</th></tr>
<tr>
<td>xmagic-xxx.aar</td><td>SDK (required)</td>
</tr><tr>
<td>../assets/</td><td>Algorithm model and material resource package (required)</td>
</tr><tr>
<td>../jniLibs</td><td>`so` library (required)</td>
</tr></tbody></table>

## Resource Import

### Resources

- Add all the `.aar` files prepared above to the `libs` directory of the app project.
- Copy all resources from the `assets/` directory of the SDK package to the `../src/main/assets` directory.
- Copy the `jniLibs` folder to the `../src/main/jniLibs` directory of the project.

### Method to import
Open the `build.gradle` of the app module to add a dependency reference:

```groovy
android{
    ...
    defaultConfig {
        applicationId "Replace it with the package name bound to the `lic`"
        ....
    }
    packagingOptions {
        pickFirst '**/libc++_shared.so'
    }
}

dependencies{
    ...
    compile fileTree(dir: 'libs', include: ['*.jar','*.aar'])// Add `*.aar`
}
```

[](id:download)
## Guide to Dynamically Downloading `assets`, `so`, and `MotionRes`

To reduce the package size, you can choose to download the `assets` resources, `so` library, and animated effect resources `MotionRes` (unavailable in some basic SDKs) required by the SDK online. After successful download, set the paths of the above files in the SDK.

We recommend you reuse the download logic of the demo. You can also use your existing download service. For detailed directions of dynamic download, see [Instructions on Dynamically Downloading Tencent Effect SDK Resources (Android)](https://docs.qq.com/doc/DWHRlU0dlcHlGR3V4). 

## Overall Process

[](id:step1)
### Step 1. Authenticate

1. Apply for a license and get the `License URL` and `License KEY` as instructed in [License Guide](https://intl.cloud.tencent.com/document/product/1143/45380).
> ! Under normal circumstances, as long as the app is successfully connected to the internet once, the authentication process can be completed, so you **don't need** to put the license file in the `assets` directory. However, if your app needs to use the SDK features when it is never connected to the internet, you can download the license file and put it in the `assets` directory. In this case, the license file must be named `v_cube.license`.
2. Set the `URL` and `KEY` in the initialization code of the relevant business module to trigger the license download. Avoid downloading it just before use. You can also trigger the download in the `onCreate` method of the `Application`, but this is not recommended as the download is very likely to fail if there is no network permission or connection.
```
// If you just want to trigger the download or update the license but don't care about the authentication result, you can pass in `null` for the fourth parameter.
TELicenseCheck.getInstance().setXMagicLicense(context, URL, KEY, null);
```
3. Authenticate when you need to use the beauty filter feature (for example, in the `LaunchActivity.java` of the demo):
```java
// If your `so` library is downloaded from the internet, set the `so` path before calling `TELicenseCheck.getInstance().setTELicense`; otherwise, authentication will fail.
// XmagicApi.setLibPathAndLoad(validLibsDirectory);
// If your `so` library is built into the APK package, you don't need to call the above method.
TELicenseCheck.getInstance().setTELicense(context, URL, KEY, new TELicenseCheckListener() {

            @Override
            public void onLicenseCheckFinish(int errorCode, String msg) {
                // Note: this callback is not necessarily in the call thread
                if (errorCode == TELicenseCheck.ERROR_OK) {
                    // Authentication succeeded
                } else {
                    // Authentication failed
                }
            }
        });
```
**Authentication `errorCode` description:**
<table>
<thead>
<tr>
<th>Error Code</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>0</td>
<td>Success.</td>
</tr>
<tr>
<td>-1</td>
<td>The input parameter is invalid; for example, the `URL` or `KEY` is empty.</td>
</tr>
<tr>
<td>-3</td>
<td>Download failed. Check the network settings.</td>
</tr>
<tr>
<td>-4</td>
<td>The Tencent Effect SDK authorization information read from the local system is empty, which may be caused by an I/O failure.</td>
</tr>
<tr>
<td>-5</td>
<td>The content of read VCUBE TEMP license file is empty, which may be caused by an I/O failure.</td>
</tr>
<tr>
<td>-6</td>
<td>The JSON field in the <code>v_cube.license</code> file is incorrect. Contact Tencent Cloud for assistance.</td>
</tr>
<tr>
<td>-7</td>
<td>Signature verification failed. Contact Tencent Cloud for assistance.</td>
</tr>
<tr>
<td>-8</td>
<td>Decryption failed. Contact Tencent Cloud for assistance.</td>
</tr>
<tr>
<td>-9</td>
<td>The JSON field in the `TELicense` field is incorrect. Contact Tencent Cloud for assistance.</td>
</tr>
<tr>
<td>-10</td>
<td>The Tencent Effect SDK authorization information parsed online is empty. Contact Tencent Cloud for assistance.</td>
</tr>
<tr>
<td>-11</td>
<td>Failed to write the Tencent Effect SDK authorization information to the local file, which may be caused by an I/O failure.</td>
</tr>
<tr>
<td>-12</td>
<td>Failed to download and failed to parse local assets.</td>
</tr>
<tr>
<td>-13</td>
<td>Authentication failed. Check whether the `so` file is in the package or the `so` path has been set correctly.</td>
</tr>
<tr>
<td>3004/3005</td>
<td>The authorization is invalid. Contact Tencent Cloud for assistance.</td>
</tr>
<tr>
<td>3015</td>
<td>`Bundle ID` and `Package Name` mismatch. Check whether the `Bundle ID` or `Package Name` used by your app is the same as the one applied for and whether the correct license file is used.</td>
</tr>
<tr>
<td>3018</td>
<td>The license file has expired. You need to apply to Tencent Cloud for renewal.</td>
</tr>
<tr>
<td>Others</td>
<td>Contact Tencent Cloud for assistance.</td>
</tr>
</tbody></table>

[](id:step2)
### Step 2. Copy resources
1. If your resource files are built into the `assets` directory, you need to copy them to the app's private directory before use. You can copy them in advance or in the callback of successful authentication in the previous step. The sample code is in the `LaunchActivity.java` of the demo.
```
XmagicResParser.setResPath(new File(getFilesDir(), "xmagic").getAbsolutePath());
//loading

// Copy the resource files to the private directory, which only need to be copied once
XmagicResParser.copyRes(getApplicationContext());
```
2. If your resource files are downloaded [dynamically from the internet](#download), after the download succeeds, you need to set the resource file path. The sample code is in the `LaunchActivity.java` of the demo.
```
XmagicResParser.setResPath(local path of downloaded resource files);
```

[](id:step3)
### Step 3. Initialize and use the SDK

The following is the lifecycle of using Tencent Effect SDK:
1. Build the beauty filter UI data as instructed in the `XmagicResParser.java,XmagicUIProperty.java,XmagicPanelDataManager.java` code of the demo project.
2. Add the `GLSurfaceView` to the preview layout.  
```java
<android.opengl.GLSurfaceView
android:id="@+id/camera_gl_surface_view"
android:layout_width="match_parent"
android:layout_height="match_parent" />
```
3. (Optional) Quickly implement the camera feature.
Copy the `com.tencent.demo.camera` directory from the demo project to the project. Use the `PreviewMgr` class to quickly implement the camera feature. For more information, see `MainActivity.java` of the demo project.
```java
// Initialize the camera
mPreviewMgr = new PreviewMgr();
// Pass the `GlSurfaceView` example of the layout into the camera tool class
mPreviewMgr.onCreate(mGlSurfaceView,false);
// Register the callback function to preview texture data
mPreviewMgr.setCustomTextureProcessor((textureId, textureWidth, textureHeight) -> {
	if (mXmagicApi == null) {
			return textureId;
	}
	// Call the beauty filter SDK for rendering
	int outTexture = mXmagicApi.process(textureId, textureWidth, textureHeight);
	return outTexture;
});

// Enable the camera in the `onResume` method of `Activity`
mPreviewMgr.onResume(this, 1280, 720);
```
4. Initialize the beauty filter SDK. We recommend you put it in the `onResume()` method of `Activity`.
```java
mXmagicApi = new XmagicApi(this, XmagicResParser.getResPath(),new XmagicApi.OnXmagicPropertyErrorListener()); 
```
- **Parameters**
 <table>
 <tr><th>Parameter</th><th>Description</th></tr><tr><td>Context context</td><td>Context</td>
 </tr><tr>
 <td>String resDir</td><td>Resource file directory as detailed in <a href="#step2">Step 2</a></td>
 </tr><tr>
 <td>OnXmagicPropertyErrorListener errorListener</td><td>Callback function implementation class</td>
 </tr></table>
- **Response**
 Error codes and descriptions:
 <table>
 <tr><th>Error Code</th><th>Description</th></tr><tr>
 <td>-1</td><td>An unknown error occurred.</td>
 </tr><tr>
 <td>-100</td><td>Failed to initialize the 3D SDK resources.</td>
 </tr><tr>
 <td>-200</td><td>GAN materials are not supported.</td>
 </tr><tr>
 <td>-300</td><td>This material component is not supported by the device.</td>
 </tr><tr>
 <td>-400</td><td>The template JSON content is empty.</td>
 </tr><tr>
 <td>-500</td><td>The SDK version is too low.</td>
 </tr><tr>
 <td>-600</td><td>Keying is not supported.</td>
 </tr><tr>
 <td>-700</td><td>OpenGL is not supported.</td>
 </tr><tr>
 <td>-800</td><td>The script is not supported.</td>
 </tr><tr>
 <td>5000</td><td>The resolution of the background image to be keyed exceeds 2160*3840.</td>
 </tr><tr>
 <td>5001</td><td>The memory required by background image keying is insufficient.</td>
 </tr><tr>
 <td>5002</td><td>Failed to parse the background video to be keyed.</td>
 </tr><tr>
 <td>5003</td><td>The background video to be keyed exceeds 200 seconds.</td>
 </tr><tr>
 <td>5004</td><td>The format of the background video to be keyed is not supported.</td>
 </tr>
 </tbody></table>
5. Add the callback function for material prompt (method callbacks may run in child threads). Some materials will prompt the user to nod, stretch out their palms, or make a finger heart, and this callback is used to display the prompts.
```
mXmagicApi.setTipsListener(new XmagicTipsListener() {
	final XmagicToast mToast = new XmagicToast();
	@Override
	public void tipsNeedShow(String tips, String tipsIcon, int type, int duration) {
		mToast.show(MainActivity.this, tips, duration);
	}

	@Override
	public void tipsNeedHide(String tips, String tipsIcon, int type) {
		mToast.dismiss();
	}
});
```
6. The beauty filter SDK processes each frame of data and returns the processing results.
```
int outTexture = mXmagicApi.process(textureId, textureWidth, textureHeight);
```
7. Update the value of the beauty filter effect of a specified type.
```java
// Available attributes of the input parameters can be obtained from `XmagicResParser.parseRes()`
mXmagicApi.updateProperty(XmagicProperty<?> p);
```
8. Pause the beauty filter SDK. We recommend you bind it to the `onPause()` lifecycle of `Activity`.
```java
// When called upon `onPause` of `Activity`, it needs to be called in the `OpenGL` thread
mXmagicApi.onPause();
```
9. Release the beauty filter SDK. We recommend you bind it to the `onDestroy()` lifecycle of `Activity`.
```java
// Note that this method needs to be called in the GL thread
mXmagicApi.onDestroy()
```

