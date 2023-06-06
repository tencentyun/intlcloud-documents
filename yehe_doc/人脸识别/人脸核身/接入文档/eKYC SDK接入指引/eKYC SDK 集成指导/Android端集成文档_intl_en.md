### Development Preparations

1. Sign up for a Tencent Cloud account and log in to the eKYC console to activate the service.
2. Download the required version of SDK via the eKYC SDK download link and integrate it locally.
3. Contact sales rep or customer service to get the license file of your version.



### Integrating the eKYC SDK for Android

#### Environment Requirements

The current eKYC SDK for Android is supported by API 19 (Android 4.4) or later.

[The current eKYC SDK only supports the eKYC process in Hong Kong, China.]



#### Directions

1. Add **ekyc_android_1.0.x.x_release.aar**, **huiyansdk_android_1.0.x.x_release.aar**, and **tencen-ai-sdk-common-base-1.0.x.x-release.aar** (the version numbers of the libraries downloaded from the official site shall prevail) to the `libs` directory of your project.

   ![](https://ai-sdk-release-1254418846.cos.ap-guangzhou.myqcloud.com/EKYC/%E5%9B%BE%E5%BA%8A/ekyc_common.png)

2. Configure **build.gradle** in your project as follows:

```groovy
// Set .so architecture filtering in NDK (using armeabi-v7a as an example)
ndk {
    abiFilters 'armeabi-v7a'
}

dependencies {
    // eKYC repository
    implementation files("libs/ekyc_android_1.0.x.x_release.aar")
    // Identity verification components
    implementation files("libs/huiyansdk_android_1.0.x.x_release.aar")
    // Common components
    implementation files("libs/tencen-ai-sdk-common-base-1.0.x.x-release.aar")
    // Imported `gson` library
    implementation 'com.google.code.gson:gson:2.8.5'
}
```



3. Permission Declarations

You also need to make the necessary permission declaration in the `AndroidManifest.xml` file.

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



#### SDK APIs Use Instructions

##### Initialization API

This API is called during app initialization, which is mainly used to perform some initialization operations for the SDK. We recommend you call this API in `Application`.

```java
 @Override
    public void onCreate() {
        super.onCreate();
        EkycHySdk.init(this);
    }
```



##### API for starting the eKYC process

When you need to start the eKYC process, call the function EkycHySdk.startEkycCheck(), and pass in the `sdkToken` required for this eKYC process, configuration information, and the callback for listening for the result.

```java
// Set startup configurations
EkycHyConfig ekycHyConfig = new EkycHyConfig();
// Set the license name
ekycHyConfig.setLicenseName("ekycLicense.license");
ekycHyConfig.setVerAutoTimeOut(20000);
ekycHyConfig.setOcrType(OcrRegionType.);
// Customize UI configurations
OcrUiConfig config = new OcrUiConfig();
ekycHyConfig.setOcrUiConfig(config);
// Set specific startup verification logic
// `sdkToken` is the unique credential obtained from the server for this process
EkycHySdk.startEkycCheck(sdkToken, ekycHyConfig, new EkycHyCallBack() {
  @Override
  public void onSuccess(EkycHyResult result) {
    Log.e(TAG, "result: " + result.toString());
    showToast ("Identity verification succeeded:" + result.toString());
  }

  @Override
  public void onFail(int errorCode, String errorMsg, String ekycToken) {
    Log.e(TAG, "code: " + errorCode + " msg: " + errorMsg + " token: " + ekycToken);
    showToast ("Identity verification failed:" + "code: " + errorCode + " msg: " + errorMsg + " token: " + ekycToken);
  }
});
```

**sdkToken** is the unique credential obtained from the server for this eKYC process.

**Note:** The file **"ekycLicense.license"** is the license file obtained from the business or customer service, and you need to place the license file into the `Assets Folder`.

![](https://ai-sdk-release-1254418846.cos.ap-guangzhou.myqcloud.com/EKYC/%E5%9B%BE%E5%BA%8A/ekyclicense.png)



##### API for releasing SDK resources

Before your app exits, you can call the API to release SDK resources.

```java
@Override
protected void onDestroy() {
  EkycHySdk.release();
  super.onDestroy();
}
```



#### Setting obfuscation rules

  If the obfuscation feature is enabled for your app, add the following to your obfuscation file to ensure the normal running of the SDK:

```java
# Objects to be obfuscated
-keep class com.google.gson.** {*;}
-keep class com.tencent.could.** {*;}
-keep class com.tencent.youtu.** {*;}
-keep class com.tencent.cloud.ocr.** {*;}
-keep class com.tencent.cloud.ekyc.** {*;}
```



### FAQs

1. What should I do if **Invoke-customs are only supported starting with Android O (--min-api 26)** appears?

   Add the following configuration to the `build.gradle` file:

   ```groovy
   // Java 1.8 is supported
   compileOptions {
       sourceCompatibility JavaVersion.VERSION_1_8
       targetCompatibility JavaVersion.VERSION_1_8
   }
   ```

2. If the obfuscation tool AndResGuard is used, you can add the following obfuscation configuration:

```groovy
// for EKYC SDK
"R.string.ocr_*",
"R.string.rst_*",
"R.string.net_*",
"R.string.msg_*",
"R.string.fl_*",
```

