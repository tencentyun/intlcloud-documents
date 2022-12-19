## Preparations
1. Download and decompress the [SDK package](https://intl.cloud.tencent.com/document/product/1143/45377).
2. **Prepare the following files:**
<table>
<tbody><tr><th>File</th><th>Description</th></tr>
<tr>
<td>xmagic-xxx.aar</td><td>The SDK (required).</td>
</tr><tr>
<td>../assets/</td><td>The algorithm model and resource package (required).</td>
</tr><tr>
<td>../jniLibs</td><td>The SO libraries (required).</td>
</tr></tbody></table>

## Importing Resources
<dx-tabs>
::: Manual
#### Integration
- Add all the AAR files prepared above to the `libs` directory of your application project.
- Copy all the files in `assets/` of the SDK package to `../src/main/assets`. If there are files in the `MotionRes` folder, also copy them to `../src/main/assets`.
- Copy the `jniLibs` folder to the `../src/main/jniLibs` directory of your project.

#### Import
Open the `build.gradle` of the app module to add a dependency reference:

```groovy
android{
    ...
    defaultConfig {
        applicationId "Set this to the package name bound to your license"
        ....
    }
    packagingOptions{
        pickFirst '**/libc++_shared.so'
    }
}

dependencies {
    ...
    compile fileTree(dir: 'libs', include: ['*.jar','*.aar'])//Add *.aar
}
```

<dx-alert infotype="notice">If your project is not integrated with Google’s Gson, you also need to add the following dependency.
```groovy
dependencies {
    implementation 'com.google.code.gson:gson:2.8.2'
}
```
</dx-alert>
:::
::: Maven
The Tencent Effect SDK has been released to Maven Central Repository. You can use Gradle to download the updates automatically.

1. Add the SDK dependency to `dependencies`.
```groovy
dependencies {
	// For example, to add the dependency of S1 - 04, use the code below:
	implementation 'com.tencent.mediacloud:TencentEffect_S1-04:latest.release'
}
```
2. In `defaultConfig`, specify the CPU architecture to be used by your application.
```
defaultConfig {
	ndk {
		abiFilters "armeabi-v7a", "arm64-v8a"
	}
}
```
<dx-alert infotype="explain"> Currently, the SDK supports armeabi-v7a, and arm64-v8a.</dx-alert>

3. Click ![](https://main.qcloudimg.com/raw/d6b018054b535424bb23e42d33744d03.png) to automatically download the SDK and integrate it into your project.
4. If your SDK edition includes animated effects and filters, you need to [download](https://intl.cloud.tencent.com/document/product/1143/45377) the corresponding SDK package and add the resources for animated effects and filters to the following directories of your project:
	- Animated effects: `../assets/MotionRes`.      
	- Filters: `../assets/lut`.

#### Maven addresses of different Tencent Effect packages

| Edition    | Maven Address                                                    |
| ------- | ------------------------------------------------------------ |
| A1 - 01 | implementation 'com.tencent.mediacloud:TencentEffect_A1-01:latest.release' |
| A1 - 02 | implementation 'com.tencent.mediacloud:TencentEffect_A1-02:latest.release' |
| A1 - 03 | implementation 'com.tencent.mediacloud:TencentEffect_A1-03:latest.release' |
| A1 - 04 | implementation 'com.tencent.mediacloud:TencentEffect_A1-04:latest.release' |
| A1 - 05 | implementation 'com.tencent.mediacloud:TencentEffect_A1-05:latest.release' |
| A1 - 06 | implementation 'com.tencent.mediacloud:TencentEffect_A1-06:latest.release' |
| S1 - 00 | implementation 'com.tencent.mediacloud:TencentEffect_S1-00:latest.release' |
| S1 - 01 | implementation 'com.tencent.mediacloud:TencentEffect_S1-01:latest.release' |
| S1 - 02 | implementation 'com.tencent.mediacloud:TencentEffect_S1-02:latest.release' |
| S1 - 03 | implementation 'com.tencent.mediacloud:TencentEffect_S1-03:latest.release' |
| S1 - 04 | implementation 'com.tencent.mediacloud:TencentEffect_S1-04:latest.release' |
:::
::: Dynamic download and integration
#### Dynamically downloading `assets`, SO libraries, and `MotionRes`
To reduce your application package size, you can download `assets`, the SO libraries, and `MotionRes` (unavailable in some basic SDK packages) from the internet and, after successful download, specify the paths of the files in the SDK.

You can use your existing download service, but we recommend you use the download logic of the demo. For detailed directions on implementing dynamic download, see [Reducing SDK Size](https://www.tencentcloud.com/document/product/1143/47831).
:::
</dx-tabs>


## Overall Process

[](id:step1)
### Step 1. Authenticate

1. Apply for a license and get the `License URL` and `License KEY`.
>! Under normal circumstances, the authentication process can be completed by connecting your app to the internet one time, so you **don't need** to put the license file in the `assets` directory. However, if your app needs to use the SDK features without ever connecting to the internet, you can download the license file and put it in the `assets` directory. In this case, the license file must be named `v_cube.license`.

2. Set the URL and key in the initialization code of a business module to download the license. Avoid downloading it just before use. You can also trigger the download in `onCreate` of `Application`, but this is not recommended because the SDK may not have network permission and the likelihood of it failing to connect to the internet is high.
```
// If you call this API simply to download or update the license, pass `null` for the fourth parameter.
TELicenseCheck.getInstance().setXMagicLicense(context, URL, KEY, null);
```
3. Authenticate only when you need to use the features of the Tencent Effect SDK (for example, in `LaunchActivity.java` of the demo):
```java
// If your SO libraries are downloaded from the internet, set their path before calling `TELicenseCheck.getInstance().setTELicense`; otherwise, authentication will fail.
// XmagicApi.setLibPathAndLoad(validLibsDirectory);
// If So libraries are included in your APK, you don't need to call `setLibPathAndLoad`.
TELicenseCheck.getInstance().setTELicense(context, URL, KEY, new TELicenseCheckListener() {

            @Override
            public void onLicenseCheckFinish(int errorCode, String msg) {
                // Note: This callback is not necessarily in the call thread
                if (errorCode == TELicenseCheck.ERROR_OK) {
                    // Authentication succeeded
                } else {
                    // Authentication failed
                }
            }
        });
```
**Error codes:**
<table>
<thead>
<tr>
<th>Error Code</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>0</td>
<td>Successful</td>
</tr>
<tr>
<td>-1</td>
<td>Invalid input parameter (for example, the URL or key is empty).</td>
</tr>
<tr>
<td>-3</td>
<td>Download failed. Check the network settings.</td>
</tr>
<tr>
<td>-4</td>
<td>Unable to obtain any Tencent Effect authentication information from the local system, which may be caused by an I/O failure.</td>
</tr>
<tr>
<td>-5</td>
<td>The VCUBE TEMP license file is empty, which may be caused by an I/O failure.</td>
</tr>
<tr>
<td>-6</td>
<td>The JSON field in the <code>v_cube.license</code> file is incorrect. Please contact Tencent Cloud team for help.</td>
</tr>
<tr>
<td>-7</td>
<td>Signature verification failed. Please contact Tencent Cloud team for help.</td>
</tr>
<tr>
<td>-8</td>
<td>Decryption failed. Please contact Tencent Cloud team for help.</td>
</tr>
<tr>
<td>-9</td>
<td>The JSON field in `TELicense` is incorrect. Please contact Tencent Cloud team for help.</td>
</tr>
<tr>
<td>-10</td>
<td>The Tencent Effect authentication information parsed online is empty. Please contact Tencent Cloud team for help.</td>
</tr>
<tr>
<td>-11</td>
<td>Failed to write Tencent Effect SDK authentication information to the local file, which may be caused by an I/O failure.</td>
</tr>
<tr>
<td>-12</td>
<td>Download failed, and failed to parse local assets.</td>
</tr>
<tr>
<td>-13</td>
<td>Authentication failed. Check whether your package includes the SO files and whether the path of the SO files is set correctly.</td>
</tr>
<tr>
<td>3004/3005</td>
<td>The authorization is invalid. Please contact Tencent Cloud team for help.</td>
</tr>
<tr>
<td>3015</td>
<td>Bundle ID and package name mismatch. Check whether the bundle ID or package name used by your application is the same as that bound to your license and check whether the correct license file is used.</td>
</tr>
<tr>
<td>3018</td>
<td>The license file has expired. You need to apply to Tencent Cloud for renewal.</td>
</tr>
<tr>
<td>Others</td>
<td>Please contact Tencent Cloud team for help.</td>
</tr>
</tbody></table>

[](id:step2)
### Step 2. Copy resources
1. If you want to include the resource files in your application’s `assets` directory, you need to copy them to the directory. You can do so in advance or in the callback for successful authentication in the previous step. You can find the sample code in `LaunchActivity.java` of the demo.
```
XmagicResParser.setResPath(new File(getFilesDir(), "xmagic").getAbsolutePath());
//loading

// Copy the resource files to the directory, which only needs to be done once
XmagicResParser.copyRes(getApplicationContext());
```
2. If your resource files are downloaded [dynamically from the internet](#download), after the download succeeds, you need to set the resource file path. The sample code is in the `LaunchActivity.java` of the demo.
```
XmagicResParser.setResPath(local path of downloaded resource files);
```

[](id:step3)
### Step 3. Initialize and use the SDK

The following is the process of using the Tencent Effect SDK:
1. Construct the UI data. For details, see the code in `XmagicResParser.java,XmagicUIProperty.java,XmagicPanelDataManager.java` of the demo.
2. Add the `GLSurfaceView` to the preview layout.  
```java
<android.opengl.GLSurfaceView
android:id="@+id/camera_gl_surface_view"
android:layout_width="match_parent"
android:layout_height="match_parent" />
```
3. Implement the camera feature (optional).
Copy the `com.tencent.demo.camera` directory from the demo to your project, and use the `PreviewMgr` class to quickly implement the camera feature. For more information, see `MainActivity.java` of the demo.
```java
// Initialize the camera
mPreviewMgr = new PreviewMgr();
// Pass the `GlSurfaceView` example of the layout into the camera tool class
mPreviewMgr.onCreate(mGlSurfaceView,false);
// Register the callback of texture data for preview
mPreviewMgr.setCustomTextureProcessor((textureId, textureWidth, textureHeight) -> {
	if (mXmagicApi == null) {
			return textureId;
	}
	// Call the Tencent Effect SDK to render the data
	int outTexture = mXmagicApi.process(textureId, textureWidth, textureHeight);
	return outTexture;
});

// Enable the camera in `onResume` of `Activity`
mPreviewMgr.onResume(this, 1280, 720);
```
4. Initialize the Tencent Effect SDK. We recommend you put the code in `onResume()` of `Activity`.
```java
mXmagicApi = new XmagicApi(this, XmagicResParser.getResPath(),new XmagicApi.OnXmagicPropertyErrorListener()); 
```

- **Parameters**
 <table>
 <tr><th>Parameter</th><th>Description</th></tr><tr><td>Context context</td><td>The context.</td>
 </tr><tr>
 <td>String resDir</td><td>The resource file directory. For details, see <a href="#step2">Step 2</a>.</td>
 </tr><tr>
 <td>OnXmagicPropertyErrorListener errorListener</td><td>The callback implementation class.</td>
 </tr></table>

- **Response**
 For information about the error codes, see [API Documentation](https://intl.cloud.tencent.com/document/product/1143/45399).
5. Add the callback for tips (the callback may run in a child thread). For some materials, you may need to ask users to nod, show their palms, or make finger hearts. This callback is used to show such tips.
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
6. The Tencent Effect SDK processes each frame of data and returns the processing results.
```
int outTexture = mXmagicApi.process(textureId, textureWidth, textureHeight);
```
7. Update the value of an effect.
```java
// You can use `XmagicResParser.parseRes()` to get the properties that can be used as the request parameter
mXmagicApi.updateProperty(XmagicProperty<?> p);
```
8. Pause the Tencent Effect SDK. We recommend you bind it to `onPause()` of `Activity`.
```java
// Call this API when `onPause` of `Activity` is invoked. It needs to be called in an OpenGL thread.
mXmagicApi.onPause();
```
9. Release the Tencent Effect SDK. We recommend you bind it to `onDestroy()` of `Activity`.
```java
// This needs to be called in an OpenGL thread.
mXmagicApi.onDestroy()
```
