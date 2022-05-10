### Environment Requirements

The current FaceID SDK for Android is supported by API 19 (Android 4.4) or later.


### Directions

1. Add **huiyansdk_android_1.0.7_release.aar** (the specific version number of the library downloaded from the official website shall prevail) to the `libs` directory of your project.

![](https://ai-sdk-release-1254418846.cos.ap-guangzhou.myqcloud.com/huiyan/image/lib%E4%B8%ADaar.png)

2. Configure **build.gradle** in your project as follows:

```groovy
// Set .so architecture filtering in NDK (using armeabi-v7a as an example)
ndk {
abiFilters 'armeabi-v7a'
}

// Filter out repeatedly defined .so files (using armeabi-v7a as an example)
packagingOptions{
pickFirst 'lib/armeabi-v7a/libc++_shared.so'
}

dependencies {
// Import the FaceID SDK
implementation files("libs/huiyansdk_android_1.0.7_release.aar")
// Third-Party libraries that the FaceID SDK depends on
// gson
implementation 'com.google.code.gson:gson:2.8.5'
}
```


3. Make the necessary permission declaration in the `AndroidManifest.xml` file.

```xml
<!-- Camera permission -->
<uses-permission android:name="android.permission.CAMERA" />
<uses-feature
android:name="android.hardware.camera"
android:required="true" />
<uses-feature android:name="android.hardware.camera.autofocus" />

<!-- Permissions required by the SDK -->
<uses-permission android:name="android.permission.READ_PHONE_STATE" />
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
```

If your app needs to be compatible with Android 6.0 or later, in addition to declaring the above permissions in the "AndroidManifest.xml" file, you also need to add the code **Dynamically apply for permissions**.


### SDK APIs Use Instructions

#### Initialization API

This API is called during app initialization, which is mainly used to perform some initialization operations for the SDK. We recommend you call this API in `Application`.

```java
@Override
public void onCreate() {
super.onCreate();
instance = this;
// Initialize the SDK during app initialization
HuiYanOsApi.init(getApp());
}
```


#### Initializing configuration and pulling parameters

Before using the FaceID SDK, you need to call this method to pass in basic configuration parameters and use the callback to pull the local configuration parameter information.

```java
// HuiYanOs parameters
HuiYanOsConfig huiYanOsConfig = new HuiYanOsConfig();
// The license file is placed in "assets"
huiYanOsConfig.setAuthLicense("YTFaceSDK.license");
// Pull the local configuration parameter information before starting identity verification
HuiYanOsApi.startGetAuthConfigData(huiYanOsConfig, new HuiYanConfigCallback() {
@Override
public void onSuccess(String result) {
// The configuration information is obtained successfully and sent to the server to get the verification start configuration, and the server delivers the light sequence (implemented by yourself).
String lightData = getAuthLightData(result);
// ... Subsequent steps
}

@Override
public void onFail(int errorCode, String errMsg) {
// Failed to get configuration parameters (implemented by yourself)
showError(errorCode, errMsg);
}
});
```

**Note:** You need to contact the customer service to apply for the **"YTFaceSDK.license"**, and then place the license file in the `Assets Folder`.

![](https://ai-sdk-release-1254418846.cos.ap-guangzhou.myqcloud.com/huiyan/image/license%E5%AD%98%E6%94%BE%E8%B7%AF%E5%BE%84.png)


#### Performing subsequent liveness detection steps

After you request the configuration information from the server, pass in `LightData` (identity verification light sequence) delivered by the server through this API to continue the local identity verification.

```java
// Start the verification, where `lightData` is the data of the light sequence obtained from the server in the previous step.
HuiYanOsApi.startAuthByLightData(lightData, new HuiYanResultCallBack() {
@Override
public void onSuccess(byte[] data, String videoPath) {
// 1. Send the local verification data to the server for comparison and verification to get the final result (implemented by yourself)
checkAuthResultByData(data);
// 2. Process the local identity verification video "videoPath" (implemented by yourself)
dealWithAuthVideo(videoPath);
}

@Override
public void onFail(int errorCode, String errMsg) {
// An error occurred. The local identity verification failed.
showError(errorCode, errMsg);
}
});
```


#### API for releasing SDK resources

Before your app exits, you can call the SDK resource release API.

```java
@Override
protected void onDestroy() {
super.onDestroy();
// Release the resources during exit
HuiYanOsApi.release();
}
```


### Setting obfuscation rules

If the obfuscation feature is enabled for your app, add the following to your obfuscation file to ensure the normal running of the SDK:

```java
# The following FaceID SDK obfuscation rules should be added:
-keep class com.tencent.could.huiyansdk.** {*;}
-keep class com.tencent.youtu.** {*;}
-keep class com.tencent.ytcommon.** {*;}
-keep class com.tencent.ytfacetrackpro.** {*;}
-keep class com.tencent.could.component.common.** {*;}
```


## Description of Android APIs

The FaceID SDK mainly involves the following classes: HuiYanOsApi (API class), HuiYanOsConfig (configuration parameter class), and HuiYanConfigCallback and HuiYanResultCallBack (result and callback classes).

### HuiYanOsApi

| API | Feature Description |
| ----------------------------------------------------- | ---------------------------------------------------- |
| [init()](#init()) | Initializes the SDK|
| [release()](#release()) | Releases resources|
| [startGetAuthConfigData()](#startGetAuthConfigData()) | Gets the local configuration information of the FaceID SDK |
| [startAuthByLightData()](#startAuthByLightData())     | Passes in the light sequence obtained from the server to continue the liveness detection for identity verification |

#### init()

```java
public static void init(Context context)
```

Feature:

It is an API for initializing the FaceID SDK.

Input parameters: 

| Parameter Type | Parameter Name | Description |
| -------- | -------- | --------------- |
| context | Context | Context of the app |


#### release()

```java
public static void release() 
```

Feature:

It is an API for releasing FaceID SDK resources.


#### startGetAuthConfigData()

```java
public static void startGetAuthConfigData(HuiYanOsConfig startConfig, HuiYanConfigCallback configCallback) 
```

Feature:

It is a configuration parameter pulled by the FaceID SDK during local detection in order to obtain the light sequence in subsequent steps.

Input parameters:

| Parameter Type | Parameter Name | Description |
| --------------------------------------------- | -------------- | ------------------ |
| [HuiYanOsConfig](#HuiYanOsConfig)             | startConfig    | Configuration parameter |
| [HuiYanConfigCallback](#HuiYanConfigCallback) | configCallback | Callback for configuration result pull |


#### startAuthByLightData()

```java
public static void startAuthByLightData(String lightData, HuiYanResultCallBack resultCallBack) 
```

Feature:

It is an API used to pass in the light sequence data pulled from the server to the FaceID SDK in order to continue the identity verification process for the local detection result.

Input parameters:

| Parameter Type | Parameter Name | Description |
| --------------------------------------------- | -------------- | ------------------------------------ |
| String | lightData | The light sequence pulled from the server and used for starting the identity verification |
| [HuiYanResultCallBack](#HuiYanResultCallBack) | resultCallBack  | Callback for the local identity verification result |


### HuiYanOsConfig

"HuiYanOsConfig" is the configuration entity class during FaceID SDK startup, which mainly covers the following attributes:

| Type | Name | Description | Default Value |
| -------------- | ------------------ | ------------------------------------ | -------------------- |
| PageColorStyle | pageColorStyle | Color pattern of the current face authentication | PageColorStyle.Light |
| String | authLicense | Name of the license file requested for user identity verification | Empty |
| long | authTimeOutMs | Liveness detection timeout period | 10,000 ms (10s) |
| boolean | isDeleteVideoCache | Whether to delete the local cache of the identity verification video | true |


### PageColorStyle

This is the enumeration class of default color patterns on the default identity verification UI. Currently, two color patterns are supported: light and dark patterns.

| PageColorStyle Type   | Description |
| -------------------- | ---------- |
| PageColorStyle.Light | Light pattern |
| PageColorStyle.Dark | Dark pattern |


### HuiYanConfigCallback

Callback class for initialization and acquisition of the local configuration.

```java
/**
* Callback for FaceID SDK initialization and acquisition of the local configuration
*/
public interface HuiYanConfigCallback {

/**
* API for successfully getting configuration
*
* @param result: Configuration information
*/
void onSuccess(String result);

/**
* API for failing to get configuration
*
* @param errorCode: Error code
* @param errMsg: Error message
*/
void onFail(int errorCode, String errMsg);
}
```


### HuiYanResultCallBack

Callback class for local identity verification process and local result acquisition.

```java
/**
* Callback type for identity verification completion
*/
public interface HuiYanResultCallBack {

/**
* Callback success data
*
* @param data: Data for comparison
* @param videoPath: The path of the identity verification video
*/
void onSuccess(byte[] data, String videoPath);

/**
* Callback failure result
*
* @param errorCode: Error code
* @param errMsg: Error message
*/
void onFail(int errorCode, String errMsg);
}
```




### FAQs

1. What should I do if **Invoke-customs are only supported starting with Android O (--min-api 26)** appears after I integrate the FaceID?

   Add the following configuration to the `build.gradle` file:

```groovy
   // Java 1.8 is supported
   compileOptions {
       sourceCompatibility JavaVersion.VERSION_1_8
       targetCompatibility JavaVersion.VERSION_1_8
   }
```

2. If the integrator uses the obfuscation tool AndResGuard, you can add the following obfuscation configuration:

```groovy
	// for HuiYanSDK
	"R.string.ocr_*",
	"R.string.rst_*",
	"R.string.net_*",
	"R.string.msg_*",
	"R.string.fl_*",
```

3. If Android X reports **android.content.res.Resources$NotFoundException:from xml type xml resource ID #0x7f0800c3** on devices with an earlier version of system, you can add dependent vector diagrams.

```groovy
   // Vector diagrams for earlier versions
   implementation 'androidx.vectordrawable:vectordrawable:1.1.0'
```

4. If **Android Support** reports the following errors on devices with an earlier version (v6.0 or earlier) of system:

```java
android.content.res.Resources$NotFoundException: File res/drawable/$txy_face_id_logo__0.xml from color state list resource ID #0x7f070001
           at android.content.res.Resources.loadColorStateListForCookie(Resources.java:2800)
           at android.content.res.Resources.loadColorStateList(Resources.java:2749)
           at android.content.res.TypedArray.getColor(TypedArray.java:441)
           at android.content.res.XResources$XTypedArray.getColor(XResources.java:1286)
           at android.support.v4.content.res.TypedArrayUtils.getNamedColor(TypedArrayUtils.java:124)
           at android.support.graphics.drawable.VectorDrawableCompat$VFullPath.updateStateFromTypedArray(VectorDrawableCompat.java:1746)
           at android.support.graphics.drawable.VectorDrawableCompat$VFullPath.inflate(VectorDrawableCompat.java:1712)
           at android.support.graphics.drawable.VectorDrawableCompat.inflateInternal(VectorDrawableCompat.java:743)
           at android.support.graphics.drawable.VectorDrawableCompat.inflate(VectorDrawableCompat.java:631)
           at android.support.graphics.drawable.VectorDrawableCompat.createFromXmlInner(VectorDrawableCompat.java:590)
           at android.support.v7.widget.AppCompatDrawableManager$VdcInflateDelegate.createFromXmlInner(AppCompatDrawableManager.java:775)
```


	You need to update the support dependencies to the latest version (v28.0.0):

```groovy
implementation 'com.android.support:appcompat-v7:28.0.0'

// A component library compatible with vector diagrams for earlier versions
implementation 'com.android.support:support-vector-drawable:28.0.0'
implementation 'com.android.support:animated-vector-drawable:28.0.0'
```