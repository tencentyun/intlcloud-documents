### I. Preparations for Development

1. Sign up for a Tencent Cloud account and log in to the eKYC console to activate the service.
2. Download the eKYC SDK at the SDK download address and integrate it locally.
3. Apply for and download the license file.



### II. eKYC SDK for Android Integration Process

The SDK provides the **huiyansdk_android_1.0.7_release.aar** file (as actually downloaded from the official website), which encapsulates the liveness detection feature.



#### 1. Dependent environment

The current eKYC SDK for Android is applicable to API 19 (Android 4.4) and above.



#### 2. Integration steps

1. Add **huiyansdk_android_1.0.7_release.aar** (as actually downloaded from the official website) to the `libs` directory of your project.

   ![](https://ai-sdk-release-1254418846.cos.ap-guangzhou.myqcloud.com/huiyan/image/lib%E4%B8%ADaar.png)

   

2. Configure **build.gradle** in your project as follows:

```groovy
// Set .so architecture filtering in NDK (using armeabi-v7a as an example)
ndk {
    abiFilters 'armeabi-v7a'
}

dependencies {
    // Import the eKYC SDK
    implementation files("libs/huiyansdk_android_1.0.7_release.aar")
    // Import third-party libraries that the eKYC SDK needs to depend on
    // gson
    implementation 'com.google.code.gson:gson:2.8.5'
}
```



3. You also need to make the necessary declaration in the `AndroidManifest.xml` file.

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

   If your app needs to be compatible with Android 6.0 or above, in addition to declaring the above permissions in the `AndroidManifest.xml` file, you also need to use code to dynamically apply for them.



#### 3. Overall flowchart

The following diagram shows the overall logic of interaction between the SDK, client, and server.

![](https://ai-sdk-release-1254418846.cos.ap-guangzhou.myqcloud.com/huiyan/image/%E6%B5%B7%E5%A4%96%E7%89%88%E4%BA%A4%E4%BA%92%E5%9B%BEv2.png)





#### 4. SDK API use instructions

##### 4.1 Initialization

	We recommend you call this API in `Application` during the initialization of your app to initialize the SDK.

```java
@Override
public void onCreate() {
    super.onCreate();
    instance = this;
    // The SDK needs to be initialized during `Application` initialization
    HuiYanOsApi.init(getApp());
}
```



##### 4.2 Initializing configuration and pulling configuration parameters

	Before using the eKYC SDK, you need to call this method to pass in basic configuration parameters and pull the local configuration parameters through the callback as detailed below:

1. Set the launch parameter information.

2. Call the **startGetAuthConfigData** API to get the identity verification configuration data.
3. Get the returned configuration information in the callback of **onSuccess**.
4. Call the TencentCloud API **GenerateReflectSequence** to get the light sequence by using the configuration information returned by **result**.


```java
// `HuiYanOs` parameters
HuiYanOsConfig huiYanOsConfig = new HuiYanOsConfig();
// The license file is placed in `assets`
huiYanOsConfig.setAuthLicense("YTFaceSDK.license");
// Pull the local configuration parameter information before starting identity verification
HuiYanOsApi.startGetAuthConfigData(huiYanOsConfig, new HuiYanConfigCallback() {
		@Override
		public void onSuccess(String result) {
			// The configuration information is obtained successfully and sent to the server to get the verification start configuration and the light sequence delivered by the server (implemented on your own)
			String reflectSequence = getAuthLightData(result);
      // ... remaining steps
		}

		@Override
		public void onFail(int errorCode, String errMsg) {
			// Failed to get configuration parameters (implemented on your own)
			showError(errorCode, errMsg);
		}
});
```

**Note:** you need to contact customer service to apply for the current **"YTFaceSDK.license"** file and place it in the `assets` folder.

![](https://ai-sdk-release-1254418846.cos.ap-guangzhou.myqcloud.com/huiyan/image/license%E5%AD%98%E6%94%BE%E8%B7%AF%E5%BE%84.png)



##### 4.3 Performing remaining liveness detection steps

​	After you obtain the configuration information from the server, you need to call this API to pass in the `reflectSequence` delivered by the server, i.e., the light sequence for identity verification, so as to complete the local identity verification process as detailed below:

1. Get the **reflectSequence** light sequence obtained from TencentCloud API in the previous step.
2. Call the **startAuthByLightData** API and pass in **reflectSequence** as a parameter to start the subsequent verification process.
3. Get the in-process identity verification **data** and the file address of the video recorded in the main verification process from **onSuccess**.
4. Finally, call the **DetectReflectLivenessAndCompare** API to compare the identity verification **data** and get the final comparison result.

```java
// Start identity verification. `reflectSequence` is the light sequence data obtained from the server.
HuiYanOsApi.startAuthByLightData(reflectSequence, new HuiYanResultCallBack() {
		@Override
		public void onSuccess(byte[] data, String videoPath) {
			// 1. Send the local verification data to the server for comparison and verification to get the final result (implemented on your own)
			checkAuthResultByData(data);
			// 2. Process the local identity verification video `videoPath` (implemented on your own)
			dealWithAuthVideo(videoPath);
		}

		@Override
		public void onFail(int errorCode, String errMsg) {
			// Get the local identity verification failure when an error occurs
			showError(errorCode, errMsg);
		}
});
```



##### 4.4 Releasing SDK resources

	Before your app exits, you can call the SDK resource release API.

```java
@Override
protected void onDestroy() {
    super.onDestroy();
    // Release the resources upon exit
    HuiYanOsApi.release();
}
```



#### 5. Configuring obfuscation rules

  If the obfuscation feature is enabled for your app, add the following part to your obfuscation file to ensure the normal use of the SDK.

```java
# The following eKYC SDK obfuscation rules should be added:
-keep class com.tencent.could.huiyansdk.** {*;}
-keep class com.tencent.youtu.** {*;}
-keep class com.tencent.ytcommon.** {*;}
-keep class com.tencent.could.component.common.** {*;}
```



### III. FAQs About Integration

1. What should I do if I receive the **Invoke-customs are only supported starting with Android O (--min-api 26)** error after integrating eKYC?

   You need to add the following configuration in `build.gradle`:

```groovy
   // Java 1.8 is supported
   compileOptions {
       sourceCompatibility JavaVersion.VERSION_1_8
       targetCompatibility JavaVersion.VERSION_1_8
   }
```

2. If you use the obfuscation tool "AndResGuard", you can add the following obfuscation configuration:

```groovy
// for HuiYanSDK
"R.string.ocr_*",
"R.string.rst_*",
"R.string.net_*",
"R.string.msg_*",
"R.string.fl_*",
```

