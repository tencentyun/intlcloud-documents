### Development Preparations

1. Sign up for a Tencent Cloud account and log in to the eKYC console to activate the service.
2. Download the eKYC SDK at the SDK download address and integrate it locally.
3. Apply for and download the license.



### eKYC SDK for Android Integration Process

SDK provides the files **huiyansdk_android_overseas_1.0.9.6_release.aar**, **tencent-ai-sdk-youtu-base-1.0.1.39-release.aar**, **tencent-ai-sdk-common-1.1.36-release.aar**, and **tencent-ai-sdk-aicamera-1.0.22-release.aar** (the specific version numbers of the files downloaded from the official website shall prevail). The files are encapsulated with the face liveness detection feature.



#### Environment Requirements

The current eKYC SDK for Android is supported by API 19 (Android 4.4) or later.



#### Directions

1. Add the files **huiyansdk_android_overseas_1.0.9.6_release.aar**, **tencent-ai-sdk-youtu-base-1.0.1.39-release.aar**, **tencent-ai-sdk-common-1.1.36-release.aar**, and **tencent-ai-sdk-aicamera-1.0.22-release.aar** (the specific version numbers of the files downloaded from the official website shall prevail) to the **libs** directory of your project. 

   ![](https://ai-sdk-release-1254418846.cos.ap-guangzhou.myqcloud.com/SDK%E6%96%87%E6%A1%A3%E5%9B%BE%E5%BA%8A/tuyong/oversea_lib.png)

2. Configure **build.gradle** in your project as follows:

```groovy
// Set .so architecture filtering in NDK (using armeabi-v7a as an example)
ndk{
    abiFilters 'armeabi-v7a'
}

dependencies {
    // Import the eKYC SDK
    implementation files("libs/huiyansdk_android_overseas_1.0.9.5_release.aar")
    // eKYC general algorithm SDK
    implementation files("libs/tencent-ai-sdk-youtu-base-1.0.1.32-release.aar")
    // Common capability components
    implementation files("libs/tencent-ai-sdk-common-1.1.27-release.aar")
    implementation files("libs/tencent-ai-sdk-aicamera-1.0.18-release.aar")

  	// Third-Party libraries that the eKYC SDK depends on
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
<uses-permission android:name="android.permission.INTERNET" />
<!-- Optional permissions for the SDK -->
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
```

   If your app needs to be compatible with Android 6.0 or later, in addition to declaring the above permissions in the "AndroidManifest.xml" file, you also need to add the code **Dynamically apply for permissions**.



#### SDK APIs Use Instructions

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



#### I. Full integration mode

In this mode, you can get the data of each step and you should be responsible for data forwarding.

The following diagram shows the overall logic of interaction between the SDK, client, and server in the full integration mode. (**You can select full integration or simplified integration as needed.**)

![](https://ai-sdk-release-1254418846.cos.ap-guangzhou.myqcloud.com/huiyan/image/%E6%B5%B7%E5%A4%96%E7%89%88%E4%BA%A4%E4%BA%92%E5%9B%BEv2.png)





##### 1. Initialize the configuration and pull configuration parameters

	Before using the eKYC SDK, you need to call this method to pass in basic configuration parameters and use the callback to pull the local configuration parameter information.

```java
// HuiYanOs parameters
HuiYanOsConfig huiYanOsConfig = new HuiYanOsConfig();
// The license file is placed in "assets"
huiYanOsConfig.setAuthLicense("YTFaceSDK.license");
// Pull the local configuration parameter information before starting identity verification
HuiYanOsApi.startGetAuthConfigData(huiYanOsConfig, new HuiYanConfigCallback() {
		@Override
		public void onSuccess(String result) {
			// The configuration information is obtained successfully and sent to the server to get the verification start configuration, and the server delivers the light sequence (implemented by yourself via step 4 as shown in the figure above).
			String reflectSequence = getAuthLightData(result);
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



> Note: If you need to stop the verification process (such as when the light sequence network is abnormal or an error occurs), you can call **HuiYanOsApi.startAuthByLightData (null, HuiYanResultCallBack)** and pass in `null` to terminate the process.

##### 2. Complete the remaining steps of liveness verification

After you obtain the configuration information from the server, you need to call this API to pass in the `reflectSequence` delivered by the server, i.e., the light sequence for identity verification, so as to complete the local identity verification.

```java
// Start identity verification. `reflectSequence` is the light sequence data obtained from the server.
HuiYanOsApi.startAuthByLightData(reflectSequence, new HuiYanResultCallBack() {
		@Override
		public void onSuccess(byte[] data, String videoPath) {
			// 1. Send the local verification data to the server for comparison and verification to get the final result (implemented by yourself via step 9 as shown in the figure above)
			checkAuthResultByData(data);
			// 2. Process the local identity verification video `videoPath` (implemented by yourself)
			dealWithAuthVideo(videoPath);
		}

		@Override
		public void onFail(int errorCode, String errMsg) {
			// An error occurred. The local identity verification failed.
			showError(errorCode, errMsg);
		}
});
```



#### Supplementary description of interactions between the frontend and the backend

**Step 4 shown in the figure above** needs to be implemented in callback of **startGetAuthConfigData#onSuccess** in SDK by yourself. DeviceData is needed by Tencent Cloud API [GenerateReflectSequence](https://www.tencentcloud.com/document/product/1061/47646?lang=en&from_wecom=1).  

You need to send DeviceData obtained through SDK to a storage platform such as COS and ensure that the platform is accessible through external networks. The input parameter **DeviceDataUrl** of [GenerateReflectSequence](https://www.tencentcloud.com/document/product/1061/47646?lang=en&from_wecom=1) is the URL on the storage platform where data is uploaded. Tencent Cloud API gets DeviceData generated by SDK, where DeviceDataMd5 is the MD5 value of data and is used by Tencent Cloud services to verify data integrity.

In **step 9 shown in the figure above**, you need to upload LiveData in callback of **startAuthByLightData #onSuccess** in SDK. LiveData is needed by Tencent Cloud API [DetectReflectLivenessAndCompare](https://www.tencentcloud.com/document/product/1061/44246?lang=en&from_wecom=1). 

You need to send LiveData obtained through SDK to a storage platform such as COS and ensure that the platform is accessible through external networks. The input parameter **LiveDataUrl** of [DetectReflectLivenessAndCompare](https://www.tencentcloud.com/document/product/1061/44246?lang=en&from_wecom=1) is the URL on the storage platform where data is uploaded. Tencent Cloud API gets LiveData generated by SDK, where LiveDataMd5 is the MD5 value of data and is used by Tencent Cloud services to verify data integrity. (Similarly, the preceding description is also applicable to input parameters **ImageUrl** and **ImageMd5** of [DetectReflectLivenessAndCompare](https://www.tencentcloud.com/document/product/1061/44246?lang=en&from_wecom=1).)



#### II. Simplified integration mode

You only need to pass in the token and start the corresponding liveness detection method to complete liveness detection and return the result. (**You can select full integration or simplified integration as needed.**)

For details on how to obtain the token, see Tencent Cloud API [ApplyLivenessToken](https://www.tencentcloud.com/document/product/1061/49955?lang=en&from_wecom=1).

The following diagram shows the overall logic of interaction between the SDK, client, and server in the simplified integration mode.

![](https://ai-sdk-release-1254418846.cos.ap-guangzhou.myqcloud.com/huiyan/image/%E6%85%A7%E7%9C%BC%E7%A7%81%E6%9C%89%E5%8C%96%E7%B2%BE%E7%AE%80%E6%B5%81%E7%A8%8B%E5%9B%BE.png)



##### Start simplified liveness verification

```java
// HuiYanOs parameters
HuiYanOsConfig huiYanOsConfig = new HuiYanOsConfig();
// The license file is placed in "assets"
huiYanOsConfig.setAuthLicense("YTFaceSDK.license");
if (compatCheckBox.isChecked()) {
    huiYanOsConfig.setPageColorStyle(PageColorStyle.Dark);
}
// Whether to return the best frame
if (needBestImageCB.isChecked()) {
    huiYanOsConfig.setNeedBestImage(true);
}
// Start simplified liveness verification. `currentToken` is the token distributed by the backend.
HuiYanOsApi.startHuiYanAuth(currentToken, huiYanOsConfig, new HuiYanOsAuthCallBack() {
    @Override
    public void onSuccess(HuiYanOsAuthResult authResult) {
        showToast("Liveness verification passed.");
        if (!TextUtils.isEmpty(authResult.getBestImage())) {
           CommonUtils.decryptBestImgBase64(authResult.getBestImage(), false);
        }
    }

    @Override
    public void onFail(int errorCode, String errorMsg, String token) {
        String msg = "Liveness verification failed " + "code: " + errorCode + " msg: " + errorMsg + " token: " + token;
        Log.e(TAG, "onFail" + msg);
        showToast(msg);
    }
});
```

[HuiYanOsAuthResult](#HuiYanOsAuthResult) is the result returned for successful liveness verification.

**Note:** You need to contact the customer service to apply for the **"YTFaceSDK.license"**, and then place the license file in the `Assets Folder`.



#### API for releasing SDK resources

Before your app exits, you can call the API to release SDK resources.

```java
@Override
protected void onDestroy() {
    super.onDestroy();
    // Release the resources before exit
    HuiYanOsApi.release();
}
```



#### Setting obfuscation rules

  If the obfuscation feature is enabled for your app, add the following to your obfuscation file to ensure the normal running of the SDK:

```java
# The following eKYC SDK obfuscation rules should be added:
-keep class com.tencent.could.huiyansdk.** {*;}
-keep class com.tencent.could.aicamare.** {*;}
-keep class com.tencent.could.component.** {*;}
-keep class com.tencent.youtu.** {*;}
-keep class com.tenpay.utils.SMUtils {*;}
```



### FAQs About Integration

1. What should I do if **Invoke-customs are only supported starting with Android O (--min-api 26)** appears after I integrate the eKYC?

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





## API Description

The eKYC SDK mainly involves the following classes: HuiYanOsApi (API class), HuiYanOsConfig (configuration parameter class), and HuiYanConfigCallback and HuiYanResultCallBack (result and callback classes).

### HuiYanOsApi

| API                                                   | Feature Description                                             |
| ----------------------------------------------------- | ------------------------------------------------------------ |
| [init()](#init())                                     | Initializes eKYC SDK                                        |
| [release()](#release())                               | Releases resources                                         |
| [startGetAuthConfigData()](#startGetAuthConfigData()) | Gets the local configuration information of the eKYC SDK                        |
| [startAuthByLightData()](#startAuthByLightData())     | Passes in the light sequence obtained from the server to continue the liveness detection for identity verification |
| [startHuiYanAuth()](#startHuiYanAuth())               | Simplified identity verification API, which can be called to complete the entire verification process |



#### init()

```java
public static void init(Context context)
```

Feature:

	It is an API for initializing the eKYC SDK.

Input parameters:	

| Parameter Type | Parameter Name | Description        |
| -------- | -------- | --------------- |
| context | Context | Context of the app |



#### release()

```java
public static void release() 
```

Feature:

	It is an API for releasing eKYC SDK resources.



#### startGetAuthConfigData()

```java
public static void startGetAuthConfigData(HuiYanOsConfig startConfig, HuiYanConfigCallback configCallback) 
```

Feature:

It is a configuration parameter pulled by the eKYC SDK during local detection in order to obtain the light sequence in subsequent steps.

Input parameters:

| Parameter Type | Parameter | Description        |
| --------------------------------------------- | -------------- | ------------------ |
| [HuiYanOsConfig](#HuiYanOsConfig)             | startConfig    | Configuration parameter         |
| [HuiYanConfigCallback](#HuiYanConfigCallback) | configCallback | Callback for configuration result pull |



#### startAuthByLightData()

```java
public static void startAuthByLightData(String reflectSequence, HuiYanResultCallBack resultCallBack) 
```

Feature:

​	It is an API used to pass in the light sequence data pulled from the server to the eKYC SDK in order to continue the identity verification process for the local detection result.

Input parameters:

| Parameter Type | Parameter | Description        |
| --------------------------------------------- | --------------- | ------------------------------------ |
| String                                        | reflectSequence | Light sequence obtained from the server to start identity verification |
| [HuiYanResultCallBack](#HuiYanResultCallBack) | resultCallBack  | Callback for the local identity verification result                   |



#### startHuiYanAuth()

```java
public static void startHuiYanAuth(final String startToken, final HuiYanOsConfig startConfig, HuiYanOsAuthCallBack authCallBack)
```

Feature:

Simplified identity verification API, which can be called to complete the entire verification process.

Input parameters:

| Parameter Type | Parameter Name | Description        |
| --------------------------------------------- | ------------ | ------------------------------------- |
| String                                        | startToken   | Business token requested from the server for starting identity verification |
| [HuiYanOsConfig](#HuiYanOsConfig)             | startConfig    | Configuration parameter         |
| [HuiYanOsAuthCallBack](#HuiYanOsAuthCallBack) | authCallBack | Callback for the liveness detection result                        |




### HuiYanOsConfig

"HuiYanOsConfig" is the configuration entity class during eKYC SDK startup, which mainly covers the following attributes:

| Type           | Name               | Description                                 | Default Value               |
| --------------------------------- | ------------------ | -------------------------------------------- | -------------------- |
| [PageColorStyle](#PageColorStyle)       | pageColorStyle              | Color pattern used for face verification                                       | PageColorStyle.Light  |
| String         | authLicense        | Name of the license file requested for user identity verification | Empty                   |
| long                          | authTimeOutMs      | Liveness detection timeout period               | 10000 milliseconds (10 seconds) |
| boolean        | isDeleteVideoCache | Specifies whether to delete the local cache of the video for identity verification           | true                 |
| boolean                           | isShowGuidePage    | Specifies whether to open the guide page for identity verification                         | true                 |
| boolean                           | isNeedBestImage    | Specifies whether to return the best frame (for the simplified process only) | false                |
| LanguageStyle | languageStyle    | Language type | Same as the system language |
| String| languageCode    | Language code (see **Language codes for Android**), which is used together with languageStyle |   Empty|



### PageColorStyle

This is the enumeration class of default color patterns on the default identity verification UI. Currently, two color patterns are supported: light and dark patterns.

| PageColorStyle Type   | Description       |
| -------------------- | ---------- |
| PageColorStyle.Light | Light pattern |
| PageColorStyle.Dark  | Dark pattern |

### LanguageStyle

| LanguageStyle  | Description       |
| -------------------- | ---------- |
| LanguageStyle.AUTO | Auto  |
| LanguageStyle.ENGLISH  | English |
| LanguageStyle.SIMPLIFIED_CHINESE  | Simplified Chinese          |
| LanguageStyle.TRADITIONAL_CHINESE | Traditional Chinese         |
| LanguageStyle.CUSTOMIZE_LANGUAGE  | Custom language   |



### HuiYanOsAuthResult

The result type corresponding to the callback for successful simplified liveness verification.

| Type   | Name      | Description                       | Default Value |
| ------ | --------- | -------------------------- | ------ |
| String | token     | Token used in the current liveness verification process  | Empty     |
| String | bestImage | Base64-encoded data of the best frame image for liveness verification | Empty     |



### Error Codes

Below are the current error codes in the eKYC SDK (global edition) in failure callbacks and their meaning:

| Error Code                                | Value | Description               |
| ------------------------------------- | -------- | ------------------------------------------------------------ |
| HY_NETWORK_ERROR                      | 210      | Network request exception.                                             |
| HY_LOCAL_REF_FAILED_ERROR                | 211      | Check failed during local SDK initialization. Common exceptions are non-existent or expired license file. |
| HY_USER_CANCEL_ERROR                     | 212      | The user actively canceled the identity verification process.                                         |
| HY_INNER_ERROR_CODE                      | 213      | An internal exception occurred in the SDK, causing the identity verification process to be stopped.                            |
| HY_DO_NOT_CHANGE_ERROR                   | 214      | The app was switched during identity verification, causing the process to be stopped.                       |
| HY_CAMERA_PERMISSION_ERROR               | 215      | An exception occurred while getting the camera.                                     |
| HY_INIT_SDK_ERROR                        | 216      | The liveness detection method was directly called before the "init()" method was called.                                 |
| HY_VERIFY_LOCAL_ERROR                    | 217      | Local face detection failed.                                             |
| HY_PERMISSION_CHECK_ERROR                | 218      | The permissions required by the local SDK were insufficient.                                      |
| HY_APP_STOP_ERROR                     | 219      | If `reflectSequence` of `startAuthByLightData` is `null`, the integrator actively stopped the identity verification process. |
| HY_CHECK_LIVE_DATA_ERROR                 | 220      | Failed to verify the light sequence that was passed in.                     |
| HY_INITIALIZATION_PARAMETER_EXCEPTION    | 221      | An exception occurred while directly calling the method for setting light sequence parameters without getting the device configuration. |
| HY_VERIFY_LOCAL_TIME_OUT                 | 222      | Local motion detection timed out.                                         |
| HY_PREPARE_TIME_OUT                      | 223      | The preparation process (between camera launch and the first detection of face) timed out.       |
| HY_CHECK_PERMISSION_ERROR                | 224      | Failed to apply for the camera permission inside the SDK.                                      |





### HuiYanConfigCallback

Callback class for initialization and acquisition of the local configuration. 

```java
/**
 * Callback for eKYC SDK initialization and acquisition of the local configuration
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



### HuiYanOsAuthCallBack

Callback API for the simplified liveness verification process

```java
/**
 * Callback for the simplified liveness verification result 
 *
 * @author jerrydong
 * @since 2022/6/10 
 */
public interface HuiYanOsAuthCallBack { 

    /**
     * Callback for successful liveness verification 
     *
     * @param authResult Result 
     */
    void onSuccess(HuiYanOsAuthResult authResult); 

    /**
     * Liveness verification failed 
     *
     * @param errorCode: Error code
     @param errorMsg: Error message
     * @param token The token used in the current verification process 
     */
    void onFail(int errorCode, String errorMsg, String token);
}
```



### Adding a Language

To add a language, perform the following two steps:

1. Add the corresponding language folder to the project in the main module (which integrates the eKYC SDK).

2. Copy **hy_customer_string.xml** to the language folder and modify the value content.

   ![](https://ai-sdk-release-1254418846.cos.ap-guangzhou.myqcloud.com/huiyan/image/%E6%96%B0%E5%A2%9E%E8%AF%AD%E8%A8%80.png)

3. Specify the target language code in the code (with Thai as an example).

```java
huiYanOsConfig.setLanguageStyle(LanguageStyle.CUSTOMIZE_LANGUAGE);
huiYanOsConfig.setLanguageCode("th-TH");
```


#### Language codes for Android

Some of language codes for Android are provided for reference.

| Language Code     |  Language - Country/Region  |
| ---------- | -------------------------- |
| **af-ZA**  | **Afrikaans - South Africa**      |
| **sq-AL**  | **Albanian - Albania** |
| **ar-DZ**  | **Arabic - Algeria**   |
| **ar-BH**  | **Arabic - Bahrain**         |
| **ar-EG**  | **Arabic - Egypt**         |
| **ar-IQ**  | **Arabic - Iraq**       |
| **ar-JO**  | **Arabic - Jordan**         |
| **ar-KW**  | **Arabic - Kuwait**       |
| **ar-LB**  | **Arabic - Lebanon**       |
| **ar-LY**  | **Arabic - Libya**       |
| **ar-MA**  | **Arabic - Morocco**       |
| **ar-OM**  | **Arabic - Oman**         |
| **ar-QA**  | **Arabic - Qatar**       |
| **eu-ES**  | **Basque - Basque**         |
| **be-BY**  | **Belarusian - Belarus**    |
| **bg-BG**  | **Bulgarian - Bulgaria**     |
| **ca-ES**  | **Catalan - Catalonia** |
| **zh-HK**  | **Chinese - Hong Kong (China)**        |
| **zh-MO**  | **Chinese - Macao (China)**        |
| **zh-CN**  | **Chinese - China**             |
| **zh-SG**  | **Chinese - Singapore**           |
| **zh-TW**  | **Chinese - Taiwan (China)**        |
| **zh-CHS** | **Simplified Chinese**          |
| **zh-CHT** | **Traditional Chinese**          |
| **hr-HR**  | **Croatian - Croatia** |
| **cs-CZ**  | **Czech - Czech Republic**            |
| **da-DK**  | **Danish - Denmark**           |
| **div-MV** | **Dhivehi - Maldives**       |
| **nl-BE**  | **Dutch - Belgium**           |
| **nl-NL**  | **Dutch - Netherlands**            |
| **en-AU**  | **English - Australia**             |
| **en-CA**  | **English - Canada**           |
| **en-ZA**  | **English - South Africa**            |
| **en-PH**  | **English - Philippines**     |
| **en-NZ**  | **English - New Zealand**          |
| **en-GB**  | **English - UK**            |
| **en-US**  | **English - US**            |
| **fa-IR**  | **Persian - Iran**       |
| **fi-FI**  | **Finnish - Finland**           |
| **fr-FR**  | **French - France**             |
| **fr-BE**  | **French - Belgium**           |
| **fr-MC**  | **French - Monaco**           |
| **fr-CH**  | **French - Switzerland**             |
| **gl-ES**  | **Galician - Galicia**     |
| **ka-GE**  | **Georgian - Georgia** |
| **de-DE**  | **German - Germany**             |
| **de-LU**  | **German - Luxembourg**           |
| **de-CH**  | **German - Switzerland**             |
| **el-GR**  | **Greek - Greece**             |
| **gu-IN**  | **Gujarati - India**          |
| **he-IL**  | **Hebrew - Israel**         |
| **hi-IN**  | **Hindi - India**         |
| **hu-HU**  | **Hungarian - Hungary**       |
| **is-IS**  | **Icelandic - Iceland**           |
| **it-IT**  | **Italian - Italy**         |
| **ja-JP**  | **Japanese - Japan**             |
| **kk-KZ**  | **Kazakh - Kazakhstan**          |
| **kn-IN**  | **Kannada - India**         |
| **ko-KR**  | **Korean - South Korea**             |
| **lv-LV**  | **Latvian - Latvia**   |
| **lt-LT**  | **Lithuanian - Lithuania**         |
| **ms-BN**  | **Malay - Brunei**             |
| **ms-MY**  | **Malay - Malaysia**         |
| **mr-IN**  | **Marathi - India**         |
| **mn-MN**  | **Mongolian - Mongolia**             |
| **nn-NO**  | **Nynorsk - Norway**   |
| **pl-PL**  | **Polish - Poland**             |
| **pt-BR**  | **Portuguese - Brazil**           |
| **pt-PT**  | **Portuguese - Portugal**         |
| **ro-RO**  | **Romanian - Romania**   |
| **sa-IN**  | **Sanskrit - India**             |
| **ru-RU**  | **Russian - Russia**             |
| **sk-SK**  | **Slovak - Slovakia**     |
| **es-AR**  | **Spanish - Argentina**         |
| **es-ES**  | **Spanish - Spain**         |
| **sv-SE**  | **Swedish - Sweden**             |
| **th-TH**  | **Thai - Thailand**             |
| **tr-TR**  | **Turkish - Türkiye**       |
| **uk-UA**  | **Ukrainian - Ukraine**         |
| **ur-PK**  | **Urdu - Pakistan**          |
| **vi-VN**  | **Vietnamese - Vietnam**             |