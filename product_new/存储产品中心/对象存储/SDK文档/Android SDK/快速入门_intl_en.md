## Download and Installation

### Relevant Resources
**Source code and demos**

- For COS SDK for Android source code, see [here](https://github.com/tencentyun/qcloud-sdk-android).
- For COS SDK for Android demos, see [here](https://github.com/tencentyun/qcloud-sdk-android-samples).

**Changelog**

For COS SDK for Android changelog, see [here](https://github.com/tencentyun/qcloud-sdk-android/blob/master/CHANGELOG.md).

### Environmental Dependency

1. The SDK supports Android 2.2 and higher.
2. The mobile phone has to be connected to the internet (through GPRS, 3G, 4G, or Wi-Fi).
3. Insufficient storage capacity on the mobile phone may make some functions unable to work properly. Please reserve a certain amount of storage capacity.
4. Get the SecretId and SecretKey on the [API Key Management](https://console.cloud.tencent.com/capi) page in the CAM Console and the APPID in the [Account Center](https://console.cloud.tencent.com/developer).

>- For more information on the meanings of parameters such as SecretId, SecretKey, and Bucket contained herein and how to get them, see [COS Glossary](https://intl.cloud.tencent.com/document/product/436/18507).
>- Commonly used packages in the SDK include `com.tencent.cos.xml.*; com.tencent.cos.xml.exception.*; com.tencent.cos.xml.model.*; com.tencent.cos.xml.model.bucket.*; com.tencent.cos.xml.model.object.*; com.tencent.cos.xml.transfer.*; com.tencent.cos.xml.listener.*; and com.tencent.qcloud.core.auth.*`.

### Installing the SDK

#### Configuring Permissions

The use of the SDK requires certain access permissions related to network and storage. You can add the following permission declarations in AndroidManifest.xml (on Android 5.0 and higher, the permissions need to be dynamically obtained):
```html
<uses-permission android:name="android.permission.INTERNET"/>
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE"/>
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE"/>
```

#### Integrating the SDK
You can integrate the SDK in two ways: [automated integration](#step1) or [manual integration](#step2).

<span id="step1"></span>
**Automated integration (recommended)**

1. Add a Maven repository to the build.gradle file in your project's root directory:
```
allprojects {

    repositories {
        ...
        // Add the following Maven repository address
        maven {
            url "https://dl.bintray.com/tencentqcloudterminal/maven"
        }
    }
}
```
2. Add dependencies to build.gradle in the application's root directory:
```
dependencies {
	...
    // Add this line
    compile 'com.tencent.qcloud:cosxml:5.4.25'
}
```
3. If you only need the upload, download, and copy functions, you can use the simplified version of the SDK by changing the dependencies in step 2 above to the following ones:
```
dependencies {
	...
    // Add this line
    compile 'com.tencent.qcloud:cosxml-lite:5.4.25'
}
```
4. In order to continuously track and optimize the SDK quality and deliver a better user experience, we introduced Mobile Tencent Analytics (MTA) into the SDK. If you want to disable this feature, add the following dependencies to build.gradle in the application's root directory:
```
dependencies {
	...
    // Add this line
   compile ('com.tencent.qcloud:cosxml:5.4.25'){
        exclude group:'com.tencent.qcloud', module: 'mtaUtils' // Disable MTA reporting
    }
}
```
The code of the simplified SDK is as follows:
```
dependencies {
	...
    // Add this line
    compile ('com.tencent.qcloud:cosxml-lite:5.4.25'){
        exclude group:'com.tencent.qcloud', module: 'mtaUtils' // Disable MTA reporting
    }
}
```

<span id="step2"></span>

**Manual integration**
The following .jar packages need to be imported into the project and stored in the libs folder:

- cos-android-sdk.jar
- qcloud-foundation.jar
- bolts-tasks.jar
- okhttp.jar (v3.9 and higher)
- okio.jar (v1.13.0 and higher)
- mtaUtils.jar
- mid-sdk.jar
- mta-android-sdk.jar
- logUtils.aar

You can download all the .jar packages [here](https://github.com/tencentyun/qcloud-sdk-android/releases). It is recommended that you use the latest released packages.

## Getting Started
The section below describes how to perform basic operations in the COS SDK for Android, such as initializing a client, creating a bucket, querying bucket list, uploading an object, querying object list, downloading an object, and deleting an object.

### Initialization 

Before executing any COS requests, you need to instantiate a CosXmlService object, which can be done into the following steps:
1. Initialize the configuration class CosXmlServiceConfig.
2. Initialize the authorization class QCloudCredentialProvider.
3. Initialize the COS service class CosXmlService.

#### Initializing the Configuration Class

**CosXmlServiceConfig** is the configuration class of the COS service, which can be initialized using the following code:

```
String region = "bucket region"; 

// Create a CosXmlServiceConfig object and modify the default configuration parameters as needed
CosXmlServiceConfig serviceConfig = new CosXmlServiceConfig.Builder()
       .setRegion(region)
	   .isHttps(true) // Use HTTPS for the request. The default value is HTTP request
       .setDebuggable(true)
       .builder();
```

#### Initializing the Authorization Class

There may be a risk of key leakage if a mobile device is directly authenticated with a permanent key. The COS SDKs for Android and iOS support authorizing request with a temporary key. You only need to set up a service that returns the temporary key and then you can authorize the COS requests initiated on the device. This method is strongly recommended. For more information, see [Best Practices for Direct Uploads from Mobile Apps](https://intl.cloud.tencent.com/document/product/436/30618).

#### Authorizing by a Temporary Key (Recommended)

- Authorization by standard response body

If you have already set up a temporary key service and directly use the JSON data obtained in the SDK for STS as a response body for the service, you can use the following code to create an authorization class in the COS SDK.
```
/**
 * Get the URL address of the authorization service
 */
URL url = null; // URL address of the backend authorization service
try {
    url = new URL("your_auth_server_url");
} catch (MalformedURLException e) {
    e.printStackTrace();
}

/**
 * Initialize the {@link QCloudCredentialProvider} object to provide a temporary key to the SDK
 */
QCloudCredentialProvider credentialProvider = new SessionCredentialProvider(new HttpRequest.Builder<String>()
                .url(url)
                .method("GET")
                .build());
```
> In the authorization by standard response body mode, the start time of the signature is the system time on the mobile phone. Therefore, if the device time difference is large (over ten minutes), a signature error may occur. In this case, the authorization by custom response body mode as described below can be used.

- Authorization by custom response body

If you want more flexibility, such as customizing the HTTP response body of the temporary key service, returning the server time to the device as the signature start time to avoid signature error caused by excessive device time difference, or using other protocols for device-server communication, you can inherit the `BasicLifecycleCredentialProvider` class and implement its `fetchNewCredentials()`:

First, define a `MyCredentialProvider` class:

```java
public class MyCredentialProvider extends BasicLifecycleCredentialProvider {

    @Override
    protected QCloudLifecycleCredentials fetchNewCredentials() throws QCloudClientException {
       
        // First, get the response containing the signature information from your temporary key server
        ....
        
        // Then, parse the response to get the key information
        String tmpSecretId = "COS_SECRETID"; // Temporary key's secretId
        String tmpSecretKey = "COS_SECRETKEY"; // Temporary key's secretKey
        String sessionToken = "TOKEN"; // Temporary key's Token
        long expiredTime = 1556183496L;// End time of validity of the temporary key
        
        // Return server time as the start time of the signature
        long beginTime = 1556182000L; // Start time of validity of the temporary key
         
        // todo something you want
         
        // Finally, return the temporary key information object 
        return new SessionQCloudCredentials(tmpSecretId, tmpSecretKey, sessionToken, beginTime, expiredTime);
    }
}
```

Then, use the `MyCredentialProvider` instance you defined to authorize the request:

```
/**
 * Initialize the {@link QCloudCredentialProvider} object to provide a temporary key to the SDK
 */
QCloudCredentialProvider credentialProvider = new MyCredentialProvider();
```

#### Authorization by a Permanent Key

If you have not set up a temporary key service, you can use a permanent key to initialize the authorization class. Due to the risk of key leakage, **this method is strongly not recommended**. Instead, it should only be used for temporary testing in a secure environment. The code is as follows:

```
String secretId = "COS_SECRETID"; // Permanent key's secretId
String secretKey ="COS_SECRETKEY"; // Permanent key's secretKey

/**
 * Initialize the {@link QCloudCredentialProvider} object to provide a temporary key to the SDK
 */
QCloudCredentialProvider credentialProvider = new ShortTimeCredentialProvider(secretId,
                secretKey, 300);
```


#### Initializing the CosXmlService Service Class

**CosXmlService** is the COS service class that can be used to manipulate various COS services. After you instantiate the configuration class and authorization class, you can easily instantiate a COS service class with the following code:

```java
CosXmlService cosXmlService = new CosXmlService(context, serviceConfig, credentialProvider);
```

### Creating a Bucket
```java
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
PutBucketRequest putBucketRequest = new PutBucketRequest(bucket);
// Send the request
cosXmlService.putBucketAsync(putBucketRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        // todo Put Bucket success
		PutBucketResult putBucketResult = (putBucketResult)result;
    }
    
    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo Put Bucket failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```

### Querying Bucket List
```java
GetServiceRequest getServiceRequest = new GetServiceRequest();
// Send the request
cosXmlService.getServiceAsync(getServiceRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        // todo Put Bucket Lifecycle success
		GetServiceResult getServiceResult = (GetServiceResult)result;
    }
    
    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo Put Bucket Lifecycle failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```

### Uploading an Object

**TransferManager** and **COSXMLUploadTask** encapsulate async requests for simple upload and multipart upload APIs and support pausing, resuming, and canceling upload requests, which are the recommended methods for object upload. The sample code is as follows:

```java

// Initialize TransferConfig
TransferConfig transferConfig = new TransferConfig.Builder().build();
/**
If you have special requirements, you can customize the initialization as follows. For example, for an object >= 2 MB in size, use multipart upload where part size is 1 MB, and for a source object above 5 MB, use multipart copy where part size is 5 MB.
TransferConfig transferConfig = new TransferConfig.Builder()
        .setDividsionForCopy(5 * 1024 * 1024) // Minimum object size for multipart copy
        .setSliceSizeForCopy(5 * 1024 * 1024) // Part size during multipart copy
        .setDivisionForUpload(2 * 1024 * 1024) // Minimum object size for multipart upload
        .setSliceSizeForUpload(1024 * 1024) // Part size during multipart upload
        .build();
*/

// Initialize TransferManager
TransferManager transferManager = new TransferManager(cosXmlService, transferConfig);

String bucket = "bucket name";
String cosPath = "object key"; // This is the absolute path to the object in COS in the format of cosPath = "text.txt";
String srcPath = "absolute path to the local file"; // For example, srcPath=Environment.getExternalStorageDirectory().getPath() + "/text.txt";
String uploadId = null; // If there is an uploadId of an initialized multipart upload, assigning the value of the uploadId here for resumed upload; otherwise, assign null.
// Upload the object
COSXMLUploadTask cosxmlUploadTask = transferManager.upload(bucket, cosPath, srcPath, uploadId);

/**
* If a byte array is to be uploaded, you can call the upload(string, string, byte[]) method of TransferManager to implement;
* byte[] bytes = "this is a test".getBytes(Charset.forName("UTF-8"));
* cosxmlUploadTask = transferManager.upload(bucket, cosPath, bytes);
*/

/**
* If a byte stream is to be uploaded, you can call the upload(String, String, InputStream) method of TransferManager to implement;
* InputStream inputStream = new ByteArrayInputStream("this is a test".getBytes(Charset.forName("UTF-8")));
* cosxmlUploadTask = transferManager.upload(bucket, cosPath, inputStream);
*/


// Set upload progress callback
cosxmlUploadTask.setCosXmlProgressListener(new CosXmlProgressListener() {
            @Override
            public void onProgress(long complete, long target) {
                float progress = 1.0f * complete / target * 100;
                Log.d("TEST",  String.format("progress = %d%%", (int)progress));
            }
        });
// Set return result callback
cosxmlUploadTask.setCosXmlResultListener(new CosXmlResultListener() {
            @Override
            public void onSuccess(CosXmlRequest request, CosXmlResult result) {
				COSXMLUploadTaskResult cOSXMLUploadTaskResult = (COSXMLUploadTaskResult)result;
                Log.d("TEST",  "Success: " + cOSXMLUploadTaskResult.printResult());
            }

            @Override
            public void onFail(CosXmlRequest request, CosXmlClientException exception, CosXmlServiceException serviceException) {
                Log.d("TEST",  "Failed: " + (exception == null ? serviceException.getMessage() : exception.toString()));
            }
        });
// Set task status callback where you can view the task process
cosxmlUploadTask.setTransferStateListener(new TransferStateListener() {
            @Override
            public void onStateChanged(TransferState state) {
                Log.d("TEST", "Task state:" + state.name());
            }
        });

/**
If you have special requirements, you can do the following:
 PutObjectRequest putObjectRequest = new PutObjectRequest(bucket, cosPath, srcPath);
 putObjectRequest.setRegion(region); // Set the bucket region
 putObjectRequest.setNeedMD5(true); // Whether to enable MD5 checksum
 COSXMLUploadTask cosxmlUploadTask = transferManager.upload(putObjectRequest, uploadId);
*/

// Cancel upload
cosxmlUploadTask.cancel();


// Pause upload
cosxmlUploadTask.pause();

// Resume upload
cosxmlUploadTask.resume();

```

### Querying Object List
```java
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID;  
GetBucketRequest getBucketRequest = new GetBucketRequest(bucket);

// Prefix match, used to specify the prefix address of the object returned
getBucketRequest.setPrefix("prefix");

// Maximum number of entries returned at a time; 1,000 by default
getBucketRequest.setMaxKeys(100);

// The delimiter is a symbol. If there is a prefix,
// the identical paths between prefix and delimiter are grouped into one class and defined as common prefixes,
// and then all common prefixes are listed. If there is no prefix, it starts at the beginning of the path
getBucketRequest.setDelimiter('/');

// Send the request
cosXmlService.getBucketAsync(getBucketRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        // todo Get Bucket success
		GetBucketResult getBucketResult = (GetBucketResult)result;
    }
    
    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo Get Bucket failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```

### Downloading an Object
**TransferManager** and **COSXMLDownloadTask** encapsulate async requests for the download API and support pausing, resuming, and canceling download requests. This is the recommended method for object downloading. The sample code is as follows:
```java
Context applicationContext = "application context"; // getApplicationContext()
String bucket = "bucket name"; // Bucket where the object is stored
String cosPath = "object key"; // This is the absolute path to the object in COS in the format of cosPath = "text.txt";
String savedDirPath = "local folder path to the downloaded file";
String savedFileName = "local filename of the downloaded object"；// If this is null, the object name in COS will be used
// Download the object
COSXMLDownloadTask cosxmlDownloadTask = transferManager.download(applicationContext, bucket, cosPath, savedDirPath, savedFileName);
// Set download progress callback
cosxmlDownloadTask.setCosXmlProgressListener(new CosXmlProgressListener() {
            @Override
            public void onProgress(long complete, long target) {
                float progress = 1.0f * complete / target * 100;
                Log.d("TEST",  String.format("progress = %d%%", (int)progress));
            }
        });
// Set return result callback
cosxmlDownloadTask.setCosXmlResultListener(new CosXmlResultListener() {
            @Override
            public void onSuccess(CosXmlRequest request, CosXmlResult result) {
				COSXMLDownloadTaskResult cOSXMLDownloadTaskResult = (COSXMLDownloadTaskResult)result;
                Log.d("TEST",  "Success: " + cOSXMLDownloadTaskResult.printResult());
            }

            @Override
            public void onFail(CosXmlRequest request, CosXmlClientException exception, CosXmlServiceException serviceException) {
                Log.d("TEST",  "Failed: " + (exception == null ? serviceException.getMessage() : exception.toString()));
            }
        });
// Set task status callback where you can view the task process
cosxmlDownloadTask.setTransferStateListener(new TransferStateListener() {
            @Override
            public void onStateChanged(TransferState state) {
                Log.d("TEST", "Task state:" + state.name());
            }
        });

/**
If you have special requirements, you can do the following:
GetObjectRequest getObjectRequest = new GetObjectRequest(bucket, cosPath, localDir, localFileName);
getObjectRequest.setRegion(region); // Set the bucket region
COSXMLDownloadTask cosxmlDownloadTask = transferManager.download(context, getObjectRequest);
*/

// Cancel download
cosxmlDownloadTask.cancel();

// Pause download
cosxmlDownloadTask.pause();

// Resume download
cosxmlDownloadTask.resume();

```

### Deleting an Object
```java
String bucket = "examplebucket-1250000000"; // Bucket in the format of BucketName-APPID
String cosPath = "exampleobject"; // Location of the object in the bucket, i.e., the object key

DeleteObjectRequest deleteObjectRequest = new DeleteObjectRequest(bucket, cosPath);
// Send the request 
cosXmlService.deleteObjectAsync(deleteObjectRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest cosXmlRequest, CosXmlResult cosXmlResult) {
        // todo Delete Object success...
		DeleteObjectResult deleteObjectResult  = (DeleteObjectResult)result;
    }
    
    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo Delete Object failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```
