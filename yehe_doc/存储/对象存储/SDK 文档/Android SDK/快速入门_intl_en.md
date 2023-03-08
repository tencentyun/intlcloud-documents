## Resources

- Download the XML Android SDK source code [here](https://github.com/tencentyun/qcloud-sdk-android).
- Download the demo [here](https://github.com/tencentyun/qcloud-sdk-android-samples).
- For SDK APIs and parameters, see [SDK API Reference](https://cos-android-sdk-doc-1253960454.file.myqcloud.com).
- For the complete sample code, see [Sample SDK Codes](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg).
- For the SDK changelog, see [ChangeLog](https://github.com/tencentyun/qcloud-sdk-android/blob/master/CHANGELOG.md).
- For SDK FAQs, see [Android SDK FAQs](https://intl.cloud.tencent.com/document/product/436/38955).

>? If you encounter errors such as non-existent functions or methods when using the XML version of the SDK, please update the SDK to the latest version and try again.
>


## Preparations

1. You need an Android app, which can be one of your existing projects or a new one.
2. Make sure that your Android app’s target API level is 15 (Ice Cream Sandwich) or above.
3. You need a remote address where users can obtain your Tencent Cloud temporary key. For more information on temporary keys, see [Direct Upload for Mobile Apps](https://intl.cloud.tencent.com/document/product/436/30618).

## Step 1. Install the SDK

### Method 1. Automatic integration (recommended)

>? As the Bintray repository is no longer available, COS’s SDK has been migrated to Maven Central. The import path is different and thus you need to use the new import path during the update.
>

#### Using the Maven Central repository

Add the following code to the project-level `build.gradle` file (usually in the root directory):
```
repositories {
    google()
    // Add the following line
    mavenCentral()
}
```

#### Standard SDK

Add dependencies to the app-level `build.gradle` file (usually under the App module).
```
dependencies {
	...
    // Add the following line
    implementation 'com.qcloud.cos:cos-android:5.9.+'
}
```


#### Simplified SDK

Add dependencies to the app-level `build.gradle` file (usually under the App module).
```
dependencies {
	...
    // Add the following line
    implementation 'com.qcloud.cos:cos-android-lite:5.9.+'
}
```



#### Disabling beacon reporting

We have introduced the [Tencent Beacon](https://beacon.qq.com/) into the SDK to track down and optimize the SDK quality for a better user experience.
>? DataInsight only monitors the COS request performance and doesn't report any business data.
>

To disable this feature, perform the following operations in the app-level `build.gradle` file (usually under the App module):

For v5.8.0 or later:
Change the dependency of `cos-android` to
```
dependencies {
	...
    // Change to
    implementation 'com.qcloud.cos:cos-android-nobeacon:x.x.x'

    //For lite version, change to
    implementation 'com.qcloud.cos:cos-android-lite-nobeacon:x.x.x'
}
```


For v5.5.8–5.7.9:
Add the beacon removing statement
```
dependencies {
	...
    implementation ('com.qcloud.cos:cos-android:x.x.x'){
        // Add the following line
        exclude group: 'com.tencent.qcloud', module: 'beacon-android-release'
    }
}
```


### Method 2: Manually integrate

#### 1. Download the SDK version

You can directly download the latest SDK version [here](https://cos-sdk-archive-1253960454.file.myqcloud.com/qcloud-sdk-android/latest/qcloud-sdk-android.zip) or find all versions at [SDK Releases](https://github.com/tencentyun/qcloud-sdk-android/releases).

After downloading and decompressing the file, you can see that it contains multiple `JAR` or `AAR` packages as described below. Please choose the ones you want to integrate.

Required libraries:
- cos-android: COS protocol implementation
- qcloud-foundation: foundation library
- [bolts-tasks](https://github.com/BoltsFramework/Bolts-Android): third-party task library
- [okhttp](https://github.com/square/okhttp): third-party networking library
- [okio](https://github.com/square/okio): third-party I/O library

Optional libraries:
- quic: QUIC protocol, required if you transfer data over QUIC
- beacon: mobile beacon analysis to improve the SDK

#### 2. Integrate the SDK into your project

Put your libraries in the app-module `libs` folder and add dependencies to the app-level `build.gradle` file (usually under the App module):

```
dependencies {
	...
    // Add the following line
    implementation fileTree(dir: 'libs', include: ['*.jar', '*.aar'])
}
```

## Step 2. Configure Permissions

### Network permissions

The SDK needs network permission to communicate with the COS server. Please add the following permission declarations to `AndroidManifest.xml` under the app module:

```
<uses-permission android:name="android.permission.INTERNET"/>
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE"/>
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
```

### Storage permissions

If you need to read and write files from external storage, please add the following permission declarations to `AndroidManifest.xml` under the app module:

```
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE"/>
```

>! For Android 6.0 (API level 23) or above, you need to dynamically request storage permissions at runtime.
>

## Step 3. Use the SDK

>!
> - We recommend you use a temporary key as instructed in [Generating and Using Temporary Keys](https://intl.cloud.tencent.com/document/product/436/14048) to call the SDK for security purposes. When you apply for a temporary key, follow the [Notes on Principle of Least Privilege](https://intl.cloud.tencent.com/document/product/436/32972) to avoid leaking resources besides your buckets and objects.
> - If you must use a permanent key, we recommend you follow the [Notes on Principle of Least Privilege](https://intl.cloud.tencent.com/document/product/436/32972) to limit the scope of permission on the permanent key.


### 1. Obtain a temporary key

Implement a `BasicLifecycleCredentialProvider` subclass to request a temporary key and return the result.

```java
public static class MySessionCredentialProvider
        extends BasicLifecycleCredentialProvider {

    @Override
    protected QCloudLifecycleCredentials fetchNewCredentials()
            throws QCloudClientException {

        // First, obtain the response containing the key from your temporary key server

        // Then, parse the response to obtain the temporary key
        String tmpSecretId = "SECRETID"; // SecretId of the temporary key
        String tmpSecretKey = "SECRETKEY"; // SecretKey of the temporary key
        String sessionToken = "SESSIONTOKEN"; // Token of the temporary key
        long expiredTime = 1556183496L;// End timestamp (in seconds) of the effective period of the temporary key

        // To avoid request expiration caused by the large discrepancy between the phone’s local time and the standard time, we recommend that the time returning to the server be used as the signature start time.
        // Time returning to the server as the signature start time
        long startTime = 1556182000L; // Start timestamp (in seconds) of the effective period of the temporary key

        // Finally, return the temporary key object
        return new SessionQCloudCredentials(tmpSecretId, tmpSecretKey,
                sessionToken, startTime, expiredTime);
    }
}
```

The following takes `MySessionCredentialProvider` as the class name example to initialize an instance to provide a key for the SDK.

```java
QCloudCredentialProvider myCredentialProvider = new MySessionCredentialProvider();
```

#### Using a permanent key for local debugging

You can use your Tencent Cloud permanent key for local debugging during the development phase. **Since this method exposes the key to leakage risks, please be sure to replace it with a temporary key before launching your application.**

```java
String secretId = "SECRETID"; // SecretId of the permanent key
String secretKey = "SECRETKEY"; // SecretKey of the permanent key

// keyDuration is the effective duration (in seconds) of the key in your request
QCloudCredentialProvider myCredentialProvider =
    new ShortTimeCredentialProvider(secretId, secretKey, 300);
```

#### Using the server-calculated signature to authorize the request

Implement a subclass of `QCloudSelfSigner` to get the server-side signature and add it to the request authorization.

```java
QCloudSelfSigner myQCloudSelfSigner = new QCloudSelfSigner() {
    /**
     * Sign the request
     *
     * @param request The request to be signed
     * @throws QCloudClientException Client exception
     */
    @Override
    public void sign(QCloudHttpRequest request) throws QCloudClientException {
        // 1. Pass the request parameters to the server to calculate the signature
        String auth = "get auth from server";
        // 2. Add the signature to the request
        request.addHeader(HttpConstants.Header.AUTHORIZATION, auth);
    }
});
```

### 2. Initialize a COS instance

Use your `myCredentialProvider` instance that provides the key or the server-side signed and authorized instance `myQCloudSelfSigner` to initialize a `CosXmlService` instance.

`CosXmlService` provides all APIs for accessing COS. We recommend you use it as an **application singleton**.

```java
// Bucket region abbreviation. For example, "ap-guangzhou" is the abbreviation of the Guangzhou region
String region = "COS_REGION";

// Create a `CosXmlServiceConfig` object and modify the default configuration parameters as needed
CosXmlServiceConfig serviceConfig = new CosXmlServiceConfig.Builder()
        .setRegion(region)
        .isHttps(true) // Use the HTTPS request. HTTP is used by default
        .builder();

// Initialize the COS service to obtain the instance
CosXmlService cosXmlService = new CosXmlService(context,
    serviceConfig, myCredentialProvider);

// Initialize the COS service via the server-side signature authorization to get the instance
CosXmlService cosXmlService = new CosXmlService(context,
    serviceConfig, myQCloudSelfSigner);
```

>? For more information on the abbreviations of the COS bucket regions, see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224).
>

## Step 4. Access COS

### Uploading an object

The SDK supports uploading local files, binary data, URIs, and input streams. The following uses uploading a local file as an example:

[//]: # (.cssg-snippet-transfer-upload-file)
```java
// Initialize TransferConfig. The default configuration is used here. To customize the configuration, see the SDK API documentation.
TransferConfig transferConfig = new TransferConfig.Builder().build();
// Initialize TransferManager.
TransferManager transferManager = new TransferManager(cosXmlService,
        transferConfig);

// Bucket name in the format of `BucketName-APPID` (`APPID` is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
String bucket = "examplebucket-1250000000";
String cosPath = "exampleobject"; // Location identifier of the object in the bucket, i.e., the object key
String srcPath = new File(context.getCacheDir(), "exampleobject")
        .toString(); // Absolute path of the local file
// If there is an uploadId for the initialized multipart upload, assign the value of uploadId here to resume the upload. Otherwise, assign null
String uploadId = null;

// Upload the file
COSXMLUploadTask cosxmlUploadTask = transferManager.upload(bucket, cosPath,
        srcPath, uploadId);

// Set the callback for initializing multipart upload (supported starting from v5.9.7)
cosxmlUploadTask.setInitMultipleUploadListener(new InitMultipleUploadListener() {
    @Override
    public void onSuccess(InitiateMultipartUpload initiateMultipartUpload) {
        //The uploadId required for the subsequent checkpoint restarts
        String uploadId = initiateMultipartUpload.uploadId;
    }
});
// Set the upload progress callback
cosxmlUploadTask.setCosXmlProgressListener(new CosXmlProgressListener() {
    @Override
    public void onProgress(long complete, long target) {
        // todo Do something to update progress...
    }
});
// Set the response callback
cosxmlUploadTask.setCosXmlResultListener(new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        COSXMLUploadTask.COSXMLUploadTaskResult uploadResult =
                (COSXMLUploadTask.COSXMLUploadTaskResult) result;
    }

    // If you use the Kotlin language to call this, please note that the exception in the callback method is nullable; otherwise, the onFail method will not be called back, that is:
    // clientException is of type CosXmlClientException? and serviceException is of type CosXmlServiceException?
    @Override
    public void onFail(CosXmlRequest request,
                       @Nullable CosXmlClientException clientException,
                       @Nullable CosXmlServiceException serviceException) {
        if (clientException != null) {
            clientException.printStackTrace();
        } else{
            serviceException.printStackTrace();
        }
    }
});
// Set the job status callback to view the job progress
cosxmlUploadTask.setTransferStateListener(new TransferStateListener() {
    @Override
    public void onStateChanged(TransferState state) {
        // todo notify transfer state
    }
});
```

>?
>- For the complete sample, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/TransferUploadObject.java).
>- After the upload, you can generate a download URL for the uploaded file with the same key. For detailed directions, see [Generating Pre-signed Links](https://intl.cloud.tencent.com/document/product/436/37680). Please note that for private-read files, the download URL is only valid for a limited period of time.

### Downloading an object

[//]: # (.cssg-snippet-transfer-download-object)
```java
// The advanced download API supports checkpoint restart. Therefore, a HEAD request will be sent before the download to obtain the file information.
// If you are using a temporary key or accessing with a sub-account, ensure that your permission list includes HeadObject.

// Initialize TransferConfig. The default configuration is used here. To customize the configuration, see the SDK API documentation.
TransferConfig transferConfig = new TransferConfig.Builder().build();
// Initialize TransferManager
TransferManager transferManager = new TransferManager(cosXmlService,
        transferConfig);

// Bucket name in the format of `BucketName-APPID` (`APPID` is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
String bucket = "examplebucket-1250000000";
String cosPath = "exampleobject"; // Location identifier of the object in the bucket, i.e., the object key
// Path of the local directory
String savePathDir = context.getExternalCacheDir().toString();
// File name saved locally. If not specified (null), it will be the same as the COS file name
String savedFileName = "exampleobject";

Context applicationContext = context.getApplicationContext(); // application
// context
COSXMLDownloadTask cosxmlDownloadTask =
        transferManager.download(applicationContext,
                bucket, cosPath, savePathDir, savedFileName);

// Set the download progress callback
cosxmlDownloadTask.setCosXmlProgressListener(new CosXmlProgressListener() {
    @Override
    public void onProgress(long complete, long target) {
        // todo Do something to update progress...
    }
});
// Set the response callback
cosxmlDownloadTask.setCosXmlResultListener(new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        COSXMLDownloadTask.COSXMLDownloadTaskResult downloadTaskResult =
                (COSXMLDownloadTask.COSXMLDownloadTaskResult) result;
    }

    // If you use the Kotlin language to call this, please note that the exception in the callback method is nullable; otherwise, the onFail method will not be called back, that is:
    // clientException is of type CosXmlClientException? and serviceException is of type CosXmlServiceException?
    @Override
    public void onFail(CosXmlRequest request,
                       @Nullable CosXmlClientException clientException,
                       @Nullable CosXmlServiceException serviceException) {
        if (clientException != null) {
            clientException.printStackTrace();
        } else{
            serviceException.printStackTrace();
        }
    }
});
// Set the job status callback to view the job progress
cosxmlDownloadTask.setTransferStateListener(new TransferStateListener() {
    @Override
    public void onStateChanged(TransferState state) {
        // todo notify transfer state
    }
});
```


>?
>- For the complete sample, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/TransferDownloadObject.java).
>- The advanced download API supports checkpoint restart. Therefore, a HEAD request will be sent before the download to obtain the file information. If you are using a temporary key or accessing with a sub-account, ensure that your permission list includes `HeadObject`.
