### What is video upload from client?
Video upload from client refers to uploading local videos to VOD by an application user.

### Why cannot I find the video upload module TXUGCPublish?
The video upload feature has been separated from the SDK and made open source in the demo. You need to integrate the UGSV upload feature in the following steps:   
1. Download the [demo](https://cloud.tencent.com/document/product/584/9366).
2. Copy the upload .jar package in the `app\libs\upload` directory to the `..\app\libs\upload` directory of your project.
3. Copy the source code directory `Demo\app\src\main\java\com\tencent\liteav\demo\videoupload` of the UGSV upload feature to your project directory and rename the package in the source code.
4. Add the code that imports the .jar package into `build.gradle` in the `App` directory of the project.
```
dependencies {
  compile fileTree(include: ['*.jar'], dir: 'libs/upload')
}
```
5. Configure the application permissions in `AndroidManifest.xml`.
```
<uses-permission android:name="android.permission.INTERNET"/>
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE"/>
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE"/>
```

### What should I do if upload failed and internal error 1000 was reported?
Please check whether the VOD service is activated.

### What should I do if a UGSV upload parameter is incorrect?
Please check whether the addresses of the video file and image are correct and whether the corresponding files can be found in the specified paths.

### What should I do if the UGSV upload signature is incorrect?
Before a client initiates an upload, it needs to apply to the application server for an upload signature. If the application server allows the client to upload, it will generate an upload signature as described in [Signature for Upload from Client](https://intl.cloud.tencent.com/document/product/266/33922). The signature must be carried by the client, so that VOD can verify whether the upload is authorized.

A signature for upload from client is generated as follows:
1. Get the API key.
2. Concatenate the plaintext string.
3. Convert the plaintext string into the final signature.
4. After building the service, you can use the tool provided by VOD to verify whether the signature is correct:
	- [Signature generation tool](https://video.qcloud.com/signature/ugcgenerate.html?_ga=1.100430424.799380133.1510203220): quickly generates a signature based on the relevant parameters and key.
	- [Signature verification tool](https://video.qcloud.com/signature/ugcdecode.html?_ga=1.100430424.799380133.1510203220): parses a signature to get the parameters used to generate it.

For more information, please see [Signature for Upload from Client](https://intl.cloud.tencent.com/document/product/266/33922).






