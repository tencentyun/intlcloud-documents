## Relevant Resources

- Download the Android SDK source code [here](https://github.com/tencentyun/qcloud-sdk-android).
- Download the demo [here](https://github.com/tencentyun/qcloud-sdk-android-samples).
- For the SDK API and parameter documentation, please see [SDK API Reference](https://cos-android-sdk-doc-1253960454.file.myqcloud.com).
- For the SDK changelog, please see [Changelog](https://github.com/tencentyun/qcloud-sdk-android/blob/master/CHANGELOG.md).

## Preparations

1. Prepare an Android application; this can be an existing project or a new empty project.
2. Please make sure that your target Android application is API level 15 (Ice Cream Sandwich) or above.
3. Prepare a remote address that can be used to get your Tencent Cloud temporary key. For more information on temporary keys, please see [Practice of Direct Upload for Mobile Apps](https://intl.cloud.tencent.com/document/product/436/30618).

## Step 1. Install the SDK

### Method 1. Automatic integration (recommended)

#### Standard SDK

Add the following dependencies to `build.gradle` at the application level (generally in the `app` module):
```
dependencies {
	...
    // Add this line
    implementation 'com.tencent.qcloud:cosxml:5.5.3'
}
```

If you use Kotlin to develop your project, you can add our KTX extension package, which provides friendlier APIs:

```
dependencies {
	...
    // Add this line
    implementation 'com.tencent.qcloud:cosxml-ktx:5.5.0'
}
```

#### Simplified SDK

If you use only basic object features such as upload, download, and copy and have strict limitations on packet size, you can use the simplified SDK.

First, add the Bintray repository address to the `build.gradle` file at the project level:

```
allprojects {
 repositories {
     ...
     // Add the Maven repository:
     maven {
         url "https://dl.bintray.com/tencentqcloudterminal/maven"
     }
 }
}
```

Then, change the dependencies to `cosxml-lite` in `build.gradle` at the application level (generally in the `app` module):

```
dependencies {
	...
    // Add this line
    implementation 'com.tencent.qcloud:cosxml-lite:5.5.3'
}
```

#### Disabling MTA reporting

We have introduced Tencent Mobile Analytics (TMA) capabilities into the SDK to keep track of and optimize SDK quality for a better user experience.

To disable this feature, please add the statements for removing MTA to `build.gradle` at the application level (generally in the `app` module):

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

#### 1. Download an archive file

You can download the latest version of the SDK [here](https://cos-sdk-archive-1253960454.file.myqcloud.com/qcloud-sdk-android/latest/qcloud-sdk-android.zip), or you can find all of the versions [here](https://github.com/tencentyun/qcloud-sdk-android/releases).

After the package is downloaded and decompressed, you will see multiple `JAR` or `AAR` packages, which are detailed below. Please select the packages to be integrated as needed.

Required libraries:

- cosxml: COS protocol implementation
- qcloud-foundation: basic library
- [Bolts - Tasks](https://github.com/BoltsFramework/Bolts-Android): third-party task library
- [OkHttp](https://github.com/square/okhttp): third-party networking library
- [Okio](https://github.com/square/okio): third-party I/O library

Optional libraries:

- mtaUtils: MTA library for SDK improvement
- mid-sdk: MTA library for SDK improvement
- mta-android-sdk: MTA library for SDK improvement
- LogUtils: log module for SDK improvement
- quic: QUIC protocol, which is required if you transfer data over QUIC protocol

#### 2. Integrate the SDK into your project

Place the needed packages in the `libs` folder in your application module and add the following dependencies to the `build.gradle` file at the application level (generally in the `app` module):

```
dependencies {
	...
    // Add this line
    implementation fileTree(dir: 'libs', include: ['*.jar', '*.aar'])
}
```

## Step 2. Configure permissions

### Network permissions

The SDK needs network permission to communicate with the COS server. Please add the following permission declarations to `AndroidManifest.xml` in the application module:

```
<uses-permission android:name="android.permission.INTERNET"/>
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE"/>
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
```

### Storage permissions

If your application needs to read/write files from/to external storage, please add the following permission declarations to `AndroidManifest.xml` in the application module:

```
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE"/>
```

Please note that on Android 6.0 (API level 23) or above, the storage permissions need to be requested at runtime.

## Step 3. Begin Using the SDK

### 1. Get a temporary key

Implement a subclass of `BasicLifecycleCredentialProvider` to request a temporary key and return the result.

```java
public static class MySessionCredentialProvider
        extends BasicLifecycleCredentialProvider {

    @Override
    protected QCloudLifecycleCredentials fetchNewCredentials() 
            throws QCloudClientException {

        // First, get the response containing the key information from your temporary key server

        // Then, parse the response to get the temporary key information
        String tmpSecretId = "COS_SECRETID"; // Temporary key's `SecretId`
        String tmpSecretKey = "COS_SECRETKEY"; // Temporary key's `SecretKey`
        String sessionToken = "COS_SESSIONTOKEN"; // Temporary key's `Token`
        long expiredTime = 1556183496L;// End timestamp of the validity period of the temporary key in seconds

        // We recommend using the server time as the start time of the signature so as to avoid request expiration caused by a large discrepancy between the mobile phone's local time and the server time
        // Use the server time as the start time of the signature
        long startTime = 1556182000L; // Start timestamp of the validity period of the temporary key in seconds

        // Finally, return the temporary key information object
        return new SessionQCloudCredentials(tmpSecretId, tmpSecretKey,
                sessionToken, startTime, expiredTime);
    }
}
```

Here, suppose the class name is `MySessionCredentialProvider`. Initialize an instance to provide a key for the SDK.

```java
QCloudCredentialProvider myCredentialProvider = new MySessionCredentialProvider();
```

#### Using a permanent key for local debugging

You can use a Tencent Cloud permanent key for local debugging during the development. **As this method may disclose your key, please change to the temporary key method before launching your application.**

```java
String secretId = "COS_SECRETID"; // The SecretId of the permanent key
String secretKey = "COS_SECRETKEY"; // The SecretKey of the permanent key

// `keyDuration` is the key validity period in the request in seconds
QCloudCredentialProvider myCredentialProvider = 
    new ShortTimeCredentialProvider(secretId, secretKey, 300);
```

### 2. Initialize the COS service

Use the `myCredentialProvider` instance that provides the key to initialize a `CosXmlService` instance.

`CosXmlService` provides all APIs for accessing COS. We recommend using it as an **application singleton**.

```java
// Bucket region abbreviation; for example, `ap-guangzhou` is the abbreviation for the Guangzhou region
String region = "COS_REGION";

// Create a `CosXmlServiceConfig` object and modify the default configuration parameters as needed
CosXmlServiceConfig serviceConfig = new CosXmlServiceConfig.Builder()
        .setRegion(region)
        .isHttps(true) // Use HTTPS for the request. The default value is HTTP
        .builder();

// Initialize the COS service to get the instance
CosXmlService cosXmlService = new CosXmlService(context, 
    serviceConfig, myCredentialProvider);
```

>? For the abbreviations of different bucket regions, please see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224).

#### Using the KTX package to initialize a COS service

If you use KTX, the simplified initialization code will be as follows:

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

The SDK allows you to upload local files, binary data, URIs, and input streams. The following uses local file upload as an example:

[//]: # ".cssg-snippet-transfer-upload-file"
```java
// Initialize `TransferConfig`. The default configuration is used here. If you need to customize it, please see the SDK API documentation.
TransferConfig transferConfig = new TransferConfig.Builder().build();
// Initialize `TransferManager`
TransferManager transferManager = new TransferManager(cosXmlService,
        transferConfig);

String bucket = "examplebucket-1250000000"; // Bucket in the format of `BucketName-APPID`
String cosPath = "exampleobject"; // Location identifier of the object in the bucket, i.e., the object key.
String srcPath = new File(context.getCacheDir(), "exampleobject")
        .toString(); // Absolute path of local file
// If there is an `uploadId` for an initialized multipart upload, assign the value of the `uploadId` here to resume the upload; otherwise, assign `null`.
String uploadId = null; 

// Uploading the file
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

#### Using KTX package to upload object

If you use KTX, please see the following sample code for upload:

```kotlin
// Here, the `viewModel` KTX extension is used
// `viewModelScope` is the built-in coroutine scope in `viewModel`
viewModelScope.launch {
    val `object` = cosObject {
        bucket = cosBucket {
            service = cos
            name = "examplebucket-1250000000"
        }
        key = "exampleObject"
    }
    // Local sample file
    val sourceFile = File(appContext.externalCacheDir, "sourceFile")

    try {
        // The upload method is `suspend function`
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
>- For more complete samples, please visit [GitHub](https://github.com/tencentyun/qcloud-sdk-android/tree/master/Demo/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/TransferObject.java).
>- After an object is uploaded, you can use the same key to generate a file download link as instructed in [Generating a Pre-signed Link](https://intl.cloud.tencent.com/document/product/436/37680). However, please note that if your file is set to private-read, the download link will only be valid for a certain period of time.

### Downloading an object

[//]: # ".cssg-snippet-transfer-download-object"
```java
// Advanced download APIs support checkpoint restart; therefore, a `HEAD` request will be sent to get file information before download.
// If you are using a temporary key or accessing with a sub-account, please make sure that you have `HeadObject` permission.

// Initialize `TransferConfig`. The default configuration is used here. If you need to customize it, please see the SDK API documentation.
TransferConfig transferConfig = new TransferConfig.Builder().build();
// Initialize `TransferManager`
TransferManager transferManager = new TransferManager(cosXmlService,
        transferConfig);

String bucket = "examplebucket-1250000000"; // Bucket in the format of `BucketName-APPID`
String cosPath = "exampleobject"; // Location identifier of the object in the bucket, i.e., the object key.
// Local directory path
String savePathDir = context.getExternalCacheDir().toString();
// Name of the locally saved file; if this is null, the COS filename will be used
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

#### Using the KTX package to download an object

If you use KTX, please see the following sample code for download:

```kotlin
// Here, the `viewModel` KTX extension is used
// `viewModelScope` is the built-in coroutine scope in `viewModel`
viewModelScope.launch {
    val `object` = cosObject {
        bucket = cosBucket {
            service = cos
            name = "examplebucket-1250000000"
        }
        key = "exampleObject"
    }

    try {
        // The download method is `suspend function`
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
>- For more complete samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/TransferDownloadObject.java).
>- Advanced download APIs support checkpoint restart; therefore, a `HEAD` request will be sent to get file information before download. If you are using a temporary key or accessing with a sub-account, please make sure that you have `HeadObject` permission.
