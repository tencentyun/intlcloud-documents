## Relevant Resources

- Download the COS XML Android SDK source code [here](https://github.com/tencentyun/qcloud-sdk-android).
- Download Demo [here](https://github.com/tencentyun/qcloud-sdk-android-samples).
- For SDK APIs and their parameters, see [SDK API Reference](https://cos-android-sdk-doc-1253960454.file.myqcloud.com).
- For the complete code, see [SDK Sample Code](https://github.com/tencentyun/cos-snippets/tree/master/Android).
- For the SDK change log, see [ChangeLog](https://github.com/tencentyun/qcloud-sdk-android/blob/master/CHANGELOG.md).

## Preparations

1. You need an Android application; this can be one of your existing projects or a new project.
2. Make sure that your Android application has a target API level of 15 (Ice Cream Sandwich) or above.
3. You need a remote address where users can obtain your Tencent Cloud temporary key. For more information on temporary keys, see [Practice of Direct Upload for Mobile Apps](https://intl.cloud.tencent.com/document/product/436/30618).

## Step 1. Install the SDK

### Method 1. Automatic integration (recommended)

#### Standard SDK

Add dependencies to `build.gradle` at the application level (usually under the application module).
```
dependencies {
	...
    // Add this line
    implementation 'com.tencent.qcloud:cosxml:5.5.5'
}
```

If you are using Kotlin for development in your project, you can add our KTX extension package, which provides more user-friendly APIs.

```
dependencies {
	...
    // Add this line
    implementation 'com.tencent.qcloud:cosxml-ktx:5.5.0'
}
```

#### Simplified SDK

If you need access only to the basic COS features, such as upload, download, and replication, as well as a minimal SDK size, you may want to use the simplified SDK.

First, add the Bintray repository location to your `build.gradle` file at the project level.

```
allprojects {
 repositories {
     ...
     // Add a Maven repository
     maven {
         url "https://dl.bintray.com/tencentqcloudterminal/maven"
     }
 }
}
```

Then, add dependencies to `build.gradle` at the application level (usually under the application module).

```
dependencies {
	...
    // Add this line
    implementation 'com.tencent.qcloud:cosxml-lite:5.5.5'
}
```

#### Disabling MTA reporting

We have introduced Tencent Mobile Analytics (TMA) capabilities into the SDK to track down and optimize the SDK quality for a better user experience.

To disable the MTA feature, add the following statement to `build.gradle` at the application level (usually under the application module):

```
dependencies {
	...
    implementation ('com.tencent.qcloud:cosxml:x.x.x'){
        // Add this line
        exclude group:'com.tencent.qcloud', module: 'mtaUtils'
    }
}
```

### Method 2. Manual integration

#### 1. Download SDK version

You can directly download the latest SDK version [here](https://cos-sdk-archive-1253960454.file.myqcloud.com/qcloud-sdk-android/latest/qcloud-sdk-android.zip), or you can find all of the versions at [SDK Releases](https://github.com/tencentyun/qcloud-sdk-android/releases).

After downloading and decompressing the file, you can see that it contains multiple `JAR` or `AAR` packages which are described as follows. Please choose the ones you want to integrate.

Required libraries:

- cosxml: COS protocol implementation
- qcloud-foundation: foundation library
- [bolts-tasks](https://github.com/BoltsFramework/Bolts-Android): third-party task library
- [okhttp](https://github.com/square/okhttp): third-party networking library
- [okio](https://github.com/square/okio): third-party IO library

Optional libraries:

- mtaUtils: MTA library for improving the SDK
- mid-sdk: MTA library for improving the SDK
- mta-android-sdk: MTA library for improving the SDK
- LogUtils: log module for improving the SDK
- quic: QUIC protocol; required if you transfer data over QUIC

#### 2. Integrate the SDK into your project

Put your libraries in the `libs` folder under your application module, and add dependencies to the `build.gradle` file at the application level (usually under the application module):

```
dependencies {
	...
    // Add this line
    implementation fileTree(dir: 'libs', include: ['*.jar', '*.aar'])
}
```

## Step 2. Configure Permissions

### Network permission

The SDK needs network permission to communicate with the COS server. Please add the following permission statements to the `AndroidManifest.xml` under your application module:

```
<uses-permission android:name="android.permission.INTERNET"/>
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE"/>
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
```

### Storage permission

If you need to read and write files from external storage, please add the following permission statements to the `AndroidManifest.xml` under your application module:

```
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE"/>
```

Note that you need to request dynamic storage permissions at runtime for Android 6.0 (API level 23) or above.

## Step 3. Use the SDK

### 1. Obtain a temporary key

Implement a subclass `BasicLifecycleCredentialProvider` to request a temporary key and return the result.

```java
public static class MySessionCredentialProvider
        extends BasicLifecycleCredentialProvider {

    @Override
    protected QCloudLifecycleCredentials fetchNewCredentials() 
            throws QCloudClientException {

        // First, get the response containing a signature from your temporary key server

        // Then, parse the response to get a temporary key
        String tmpSecretId = "COS_SECRETID"; // SecretId of the temporary key
        String tmpSecretKey = "COS_SECRETKEY"; // SecretKey of the temporary key
        String sessionToken = "TOKEN"; // Token of the temporary key
        long expiredTime = 1556183496L;// End timestamp in seconds of the validity period of the temporary key

        // We strongly recommend returning the server time as the start time of the signature to avoid request expiration due a large difference between your mobile phone's local time and standard time
        // Return the server time as the start time of the signature
        long startTime = 1556182000L; // Start timestamp in seconds of the validity period of the temporary key

        // Finally, return the temporary key object
        return new SessionQCloudCredentials(tmpSecretId, tmpSecretKey,
                sessionToken, startTime, expiredTime);
    }
}
```

Assumed a class named `MySessionCredentialProvider`. Now, initialize an instance to provide the key for the SDK.

```java
QCloudCredentialProvider myCredentialProvider = new MySessionCredentialProvider();
```

#### Using a permanent key for local debugging

You can use your Tencent Cloud permanent key for local debugging during the development phase. **Since this method exposes the key to leakage risks, please be sure to replace it with a temporary key before before launching your application.**

```java
String secretId = "COS_SECRETID"; // The secretId of the permanent key
String secretKey ="COS_SECRETKEY"; // The secretKey of the permanent key

// keyDuration is the valid duration in seconds of the key in your request
QCloudCredentialProvider myCredentialProvider = 
    new ShortTimeCredentialProvider(secretId, secretKey, 300);
```

### 2. Initialize a COS Instance

Use your instance `myCredentialProvider` for providing keys to initialize a `CosXmlService` instance.

`CosXmlService` provides all APIs for accessing COS. We recommend you use it as an **application singleton**.

```java
// Bucket region abbreviation, e.g. ap-guangzhou
String region = "COS_REGION";

// Create a `CosXmlServiceConfig` object, and modify the default configuration parameters as needed
CosXmlServiceConfig serviceConfig = new CosXmlServiceConfig.Builder()
        .setRegion(region)
        .isHttps(true) // Set HTTPS as the default request method
        .builder();

// Initialize the COS instance
CosXmlService cosXmlService = new CosXmlService(context, 
    serviceConfig, myCredentialProvider);
```

>? For the COS bucket region abbreviations, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224).

#### Using the KTX package to initialize a COS instance

The code is shorter for initialization using KTX as shown below:

```kotlin
val cos = cosService(context = application.applicationContext) {

    configuration {
        setRegion("ap-guangzhou")
        isHttps(true)
    }

    credentialProvider {
        lifecycleCredentialProvider {
            // fetch credential from backend
            // ...
            return@lifecycleCredentialProvider SessionQCloudCredentials(
                    "temp_secret_id",
                    "temp_secret_key",
                    "session_token",
                    1556183496
            )
        }
    }
}
```

## Step 4. Access COS

### Uploading an object

The SDK supports uploading local files, binary data, URIs, and input streams. The following is an example of uploading a local file.

[//]: # (.cssg-snippet-transfer-upload-file)
```java
// Initialize `TransferConfig`. The default configuration is used here. If you need to customize the configuration, please see the SDK API documentation.
TransferConfig transferConfig = new TransferConfig.Builder().build();
// Initialize TransferManager
TransferManager transferManager = new TransferManager(cosXmlService,
        transferConfig);

String bucket = "examplebucket-1250000000"; // Bucket in the format: BucketName-APPID
String cosPath = "exampleobject"; // The location identifier of the object in the bucket, i.e. the object key
String srcPath = new File(context.getCacheDir(), "exampleobject")
        .toString(); // The absolute path of the local file
// If there is an uploadId for the initialized multipart upload, assign the value of the uploadId here to resume the upload; otherwise, assign null
String uploadId = null; 

// Upload a file
COSXMLUploadTask cosxmlUploadTask = transferManager.upload(bucket, cosPath,
        srcPath, uploadId);

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
        COSXMLUploadTask.COSXMLUploadTaskResult cOSXMLUploadTaskResult =
                (COSXMLUploadTask.COSXMLUploadTaskResult) result;
    }

    @Override
    public void onFail(CosXmlRequest request,
                        CosXmlClientException clientException,
                        CosXmlServiceException serviceException) {
        if (clientException != null) {
            clientException.printStackTrace();
        } else {
            serviceException.printStackTrace();
        }
    }
});
// Set the job status callback where you can view the job progress
cosxmlUploadTask.setTransferStateListener(new TransferStateListener() {
    @Override
    public void onStateChanged(TransferState state) {
        // todo notify transfer state
    }
});
```

#### Using the KTX package to upload an object

The following sample code shows how to upload using KTX:

```kotlin
// Use the KTX extension of ViewModel
// viewModelScope is the built-in coroutine scope of ViewModel
viewModelScope.launch {
    val `object` = cosObject {
        bucket = cosBucket {
            service = cos
            name = "examplebucket-1250000000"
        }
        key = "exampleObject"
    }
    // Local file example
    val sourceFile = File(appContext.externalCacheDir, "sourceFile")

    try {
        // Call the “suspend” function to upload
        val result = `object`.upload(
            localFile = sourceFile,
            progressListener = { complete, target ->
                Log.d("cosxmlktx", "upload onProgress:" +
                                " $complete / $target")
            },
            transferStateListener = { state ->
                Log.d("cosxmlktx", "upload state is : $state")
            }
        )

    } catch (e : Exception ) {
        e.printStackTrace()
    }

}
```

>?
>- For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/TransferUploadObject.java).
>- You can generate a download URL for the uploaded file using the same key. For detailed directions, see [Generating a Pre-Signed Link](https://intl.cloud.tencent.com/document/product/436/37680). Please note that for private-read files, the download URL is only valid for a limited period of time.

### Downloading an object

[//]: # (.cssg-snippet-transfer-download-object)
```java
// The advanced download API supports checkpoint restart. To do so, a `HEAD` request will be sent first to get file information before download.
// If you are using a temporary key or accessing with a sub-account, please make sure that your access permission list includes HeadObject.

// Initialize `TransferConfig`. The default configuration is used here. If you need to customize the configuration, please see the SDK API documentation.
TransferConfig transferConfig = new TransferConfig.Builder().build();
// Initialize TransferManager
TransferManager transferManager = new TransferManager(cosXmlService,
        transferConfig);

String bucket = "examplebucket-1250000000"; // Bucket in the format: BucketName-APPID
String cosPath = "exampleobject"; // The location identifier of the object in the bucket, i.e. the object key
// Local directory path
String savePathDir = context.getExternalCacheDir().toString();
// The file name saved locally. If not specified (null), it will be the same as the COS file name
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
        COSXMLDownloadTask.COSXMLDownloadTaskResult cOSXMLDownloadTaskResult =
                (COSXMLDownloadTask.COSXMLDownloadTaskResult) result;
    }

    @Override
    public void onFail(CosXmlRequest request,
                        CosXmlClientException clientException,
                        CosXmlServiceException serviceException) {
        if (clientException != null) {
            clientException.printStackTrace();
        } else {
            serviceException.printStackTrace();
        }
    }
});
// Set the job status callback where you can view the job progress
cosxmlDownloadTask.setTransferStateListener(new TransferStateListener() {
    @Override
    public void onStateChanged(TransferState state) {
        // todo notify transfer state
    }
});
```

#### Use the KTX package to download an object

The following sample code shows how to download using KTX:

```kotlin
// Use the KTX extension of ViewModel
// viewModelScope is the built-in coroutine scope of ViewModel
viewModelScope.launch {
    val `object` = cosObject {
        bucket = cosBucket {
            service = cos
            name = "examplebucket-1250000000"
        }
        key = "exampleObject"
    }

    try {
        // Call the “suspend” function to download
        val result = `object`.download(
            context = appContext,
            destDirectory = appContext.externalCacheDir!!,
            progressListener = { complete, target ->
                Log.d("cosxmlktx", "download onProgress: " +
                        "$complete / $target")
            },
            transferStateListener = { state ->
                Log.d("cosxmlktx", "download state is : $state")
            }
        )

    } catch (e : Exception ) {
        e.printStackTrace()
    }

}
```

>?
>- For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/TransferDownloadObject.java).
>- The advanced download API supports checkpoint restart; therefore, a `HEAD` request will be sent to get file information before download. If you are using a temporary key or accessing with a sub-account, please make sure that your access permission list includes HeadObject.
