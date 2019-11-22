## Download and Installation

### Relevant Resources
**Source code and demos**

- For source code related to COS Android SDK, see [COS Android SDK Github](https://github.com/tencentyun/qcloud-sdk-android).
- For demos, see [COS Android SDK Samples](https://github.com/tencentyun/qcloud-sdk-android-samples).

**Changelog**

For the changelog of COS Android SDK, see [COS Android SDK Changelog](https://github.com/tencentyun/qcloud-sdk-android/blob/master/CHANGELOG.md).

### Environment Requirements

1. The SDK supports Android 2.2 and higher.
2. The mobile phone needs to be connected to the Internet (through GPRS, 3G, 4G, or Wi-Fi).
3. Make sure the mobile has sufficient storage capacity, otherwise some of the features may not work properly. 
4. Get the SecretId and SecretKey on the [API Key Management](https://console.cloud.tencent.com/capi) page in the CAM Console. Get the APPID in the [Account Center](https://console.cloud.tencent.com/developer).

>- For the definitions of “SecretId”, “SecretKey”, “Bucket” and other terms, see [COS Glossary](https://intl.cloud.tencent.com/document/product/436/18507).
>- Common packages in the SDK include `com.tencent.cos.xml.*; com.tencent.cos.xml.exception.*; com.tencent.cos.xml.model.*; com.tencent.cos.xml.model.bucket.*; com.tencent.cos.xml.model.object.*; com.tencent.cos.xml.transfer.*; com.tencent.cos.xml.listener.*; and com.tencent.qcloud.core.auth.*`.

### Installing the SDK

#### Configuring Permissions

To use the SDK, you need to have certain access permissions for network, storage, etc. Please add the following permission declarations in AndroidManifest.xml (for Android 5.0 and higher, the permissions need to be obtained dynamically):
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
**Automated Integration (Recommended)**


1. Add a dependency to the build.gradle file in the app's root directory:
```
dependencies {
 ...
    // Add this line
 compile 'com.tencent.qcloud:cosxml:5.4.30'
}
```
2. If you only need the upload, download, and copy features, you can use the simplified version of the SDK by changing the dependency in step 1 to the following one:
```
dependencies {
	...
    // Add this line
    compile 'com.tencent.qcloud:cosxml-lite:5.4.30'
}
```
3. In order to continuously track and optimize the SDK quality for a better user experience, we introduced Mobile Tencent Analytics (MTA) into the SDK. If you want to disable the feature, please add the following dependency to the build.gradle file in the app's root directory:
```
dependencies {
	...
    // Add this line
   compile ('com.tencent.qcloud:cosxml:5.4.30'){
        exclude group:'com.tencent.qcloud', module: 'mtaUtils' // Disable MTA reporting
    }
}
```
The code of the simplified SDK is as follows:
```
dependencies {
	...
    // Add this line
    compile ('com.tencent.qcloud:cosxml-lite:5.4.30'){
        exclude group:'com.tencent.qcloud', module: 'mtaUtils' // Disable MTA reporting
    }
}
```

<span id="step2"></span>

**Manual Integration**
The following .jar packages need to be imported into the project and stored in the libs folder:

- cos-android-sdk.jar
- qcloud-foundation.jar
- bolts-tasks.jar
- okhttp.jar (v3.9 and higher)
- okio.jar (v1.13.0 and higher)
- mtaUtils.jar
- mid-sdk.jar
- mta-android-sdk.jar
- LogUtils.aar

You can download all the .jar packages [here](https://github.com/tencentyun/qcloud-sdk-android/releases). It is recommended that you use the latest released packages.

## Getting Started
The section below describes how to use COS Android SDK to perform basic operations, such as initializing a client, creating a bucket, querying the bucket list, uploading an object, querying the object list, downloading an object, and deleting an object.

### Initialization 

Before executing any request related to COS service, you need to instantiate a CosXmlService object as instructed below:
1. Initialize the configuration class CosXmlServiceConfig.
2. Initialize the authorization class QCloudCredentialProvider.
3. Initialize the COS service class CosXmlService.

#### Initializing the Configuration Class

**CosXmlServiceConfig** is the configuration class of the COS service, which can be initialized using the following code:

```
String region = "The region where the bucket resides"; 

// Create a CosXmlServiceConfig object and modify the default configuration parameters as needed
CosXmlServiceConfig serviceConfig = new CosXmlServiceConfig.Builder()
       .setRegion(region)
	   .isHttps(true) // Use HTTPS request. The default is HTTP request.
       .setDebuggable(true)
       .builder();
```

#### Initializing the Authorization Class

There is a risk of key leakage if a mobile device is authenticated with a permanent key. The COS SDKs for Android and iOS support authorizing requests with a temporary key. You only need to set up a service to return the temporary key before you can authorize the COS requests initiated on the device. This method is strongly recommended. For more information, see [Practice of Direct Transfer for Mobile Apps](https://intl.cloud.tencent.com/document/product/436/30618).

#### Authorizing via a Temporary Key (Recommended)

- Authorization with the standard response body

If you have already set up a temporary key service and use the JSON data obtained in the STS SDK as the response body, you can use the following code to create an authorization class in the COS SDK.
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
> When the standard response body is used, the start time of the signature is the system time on the mobile phone. Therefore, if there is a big difference (over ten minutes) between the device time, a signature error may occur. In such case, you can use a custom response body for the authorization as described below.

- Authorization with a custom response body

For higher flexibility, you can inherit the `BasicLifecycleCredentialProvider` class and implement its `fetchNewCredentials()` for custom configurations. For example, you can customize the HTTP response body for the temporary key service to return the server time to the device as the signature start time so as to avoid signature error caused by big device time difference. You can also choose to use other protocols for the communication between the end device and the service side. 

First, define a `MyCredentialProvider` class:

```java
public class MyCredentialProvider extends BasicLifecycleCredentialProvider {

    @Override
    protected QCloudLifecycleCredentials fetchNewCredentials() throws QCloudClientException {
       
        // First, get the response containing the signature information from your temporary key server
        ....
        
        // Then, parse the response to get the key information
        String tmpSecretId = "COS_SECRETID"; // the secretId of the temporary key
        String tmpSecretKey = "COS_SECRETKEY"; // the secretKey of the temporary key
        String sessionToken = "TOKEN"; // the token of the temporary key
        long expiredTime = 1556183496L;// End of the validity period of the temporary key
        
        // Return server time as the start time of the signature
        long beginTime = 1556182000L; // Start of the validity period of the temporary key
         
        // todo something you want
         
        // Finally return the temporary key information object 
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

#### Authorization via a Permanent Key(Not recommended)

If you have not set up a temporary key service, you can use a permanent key to initialize the authorization class. Due to the risk of key leakage, **we do not recommend this method**. It should only be used for temporary testing in a secure environment. The code is as follows:

```
String secretId = "COS_SECRETID"; // the secretId of the permanent key
String secretKey ="COS_SECRETKEY"; // the secretKey of the permanent key

/**
 * Initialize the {@link QCloudCredentialProvider} object to provide a temporary key to the SDK
 */
QCloudCredentialProvider credentialProvider = new ShortTimeCredentialProvider(secretId,
                secretKey, 300);
```


#### Initializing the CosXmlService Service Class

**CosXmlService** is the COS service class that can be used to operate various COS services. After you instantiate the configuration class and authorization class, you can easily instantiate a COS service class with the following code:

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
		PutBucketResult putBucketResult = (PutBucketResult)result;
    }
    
    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo Put Bucket failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```

### Querying the Bucket List
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

**TransferManager** and **COSXMLUploadTask** encapsulate async requests for simple upload and multipart upload APIs and support pausing, resuming, and canceling upload requests. This is recommended for object upload. The sample code is as follows:

```java

// Initialize TransferConfig
TransferConfig transferConfig = new TransferConfig.Builder().build();
/**
If you have special requirements, you can customize the initialization as follows. For example, for an object >= 2 MB in size, use multipart upload where the size of each part is 1 MB, and for a source object larger than 5 MB, use multipart copying where the size of each part is 5 MB.
TransferConfig transferConfig = new TransferConfig.Builder()
        .setDividsionForCopy(5 * 1024 * 1024) // Minimum object size for multipart copying
        .setSliceSizeForCopy(5 * 1024 * 1024) // The size of each part for multipart copying
        .setDivisionForUpload(2 * 1024 * 1024) // Minimum object size for multipart upload
        .setSliceSizeForUpload(1024 * 1024) // The size of each part for multipart upload
        .build();
*/

// Initialize TransferManager
TransferManager transferManager = new TransferManager(cosXmlService, transferConfig);

String bucket = "bucket name";
String cosPath = "object key"; // This is the absolute path to the object in COS in the format of cosPath = "text.txt";
String srcPath = "absolute path to the local file"; // For example, srcPath=Environment.getExternalStorageDirectory().getPath() + "/text.txt";
String uploadId = null; // If there is an uploadId for initialized multipart upload, assigning the value of the uploadId here for resuming upload; otherwise, assign null.
// Upload the object
COSXMLUploadTask cosxmlUploadTask = transferManager.upload(bucket, cosPath, srcPath, uploadId);

/**
* To upload a byte array, you can call the upload(string, string, byte[]) method of TransferManager:
* byte[] bytes = "this is a test".getBytes(Charset.forName("UTF-8"));
* cosxmlUploadTask = transferManager.upload(bucket, cosPath, bytes);
*/

/**
* To upload a byte stream, you can call the upload(String, String, InputStream) method of TransferManager:
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
 putObjectRequest.setRegion(region); // Set the region where the bucket resides
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

### Querying the Object List
```java
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID;  
GetBucketRequest getBucketRequest = new GetBucketRequest(bucket);

// Prefix match used to specify the prefix address of the object returned
getBucketRequest.setPrefix("prefix");

// Maximum number of entries returned at a time; 1,000 by default
getBucketRequest.setMaxKeys(100);

// The delimiter is a symbol. If there is a prefix,
// the identical paths between prefix and delimiter are grouped into one class and defined as common prefixes,
// and then all common prefixes are listed. If there is no prefix, the listing starts from the beginning of the path
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
**TransferManager** and **COSXMLDownloadTask** encapsulate async requests for the download API and support pausing, resuming, and canceling download requests. This is the recommended method for object download. The sample code is as follows:
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
getObjectRequest.setRegion(region); // Set the region where the bucket resides
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
    public void onSuccess(CosXmlRequest cosXmlRequest, CosXmlResult result) {
        // todo Delete Object success...
		DeleteObjectResult deleteObjectResult  = (DeleteObjectResult)result;
    }
    
    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo Delete Object failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```
