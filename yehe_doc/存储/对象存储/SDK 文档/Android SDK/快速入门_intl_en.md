## Download and Installation

#### Relevant Resources

**Source code and demos**

- Source code of COS Android SDK: [COS Android SDK](https://github.com/tencentyun/qcloud-sdk-android).
- Demo: [COS Android SDK Samples](https://github.com/tencentyun/qcloud-sdk-android-samples).

#### Changelog

For the changelog of COS Android SDK, see [COS Android SDK Changelog](https://github.com/tencentyun/qcloud-sdk-android/blob/master/CHANGELOG.md).

#### Environmental Requirements

1. The SDK supports Android 2.2 and higher.
2. The mobile phone needs to be connected to the Internet (through GPRS, 3G, 4G, or Wi-Fi).
3. Make sure the mobile has sufficient storage capacity, otherwise some of the features may not work properly. 
4. Obtain your APPID, SecretId, and SecretKey on the [API Key Management](https://console.cloud.tencent.com/cam/capi) page in the CAM Console. 


>
> For the definitions of parameters such as SecretId, SecretKey, and Bucket, see [COS Glossary](https://cloud.tencent.com/document/product/436/7751).
>- Common packages in the SDK include `com.tencent.cos.xml.*; com.tencent.cos.xml.exception.*; com.tencent.cos.xml.model.*; com.tencent.cos.xml.model.bucket.*; com.tencent.cos.xml.model.object.*; com.tencent.cos.xml.transfer.*; com.tencent.cos.xml.listener.*; and com.tencent.qcloud.core.auth.*`.

#### Installing the SDK

#### Configuring Permissions

To use the SDK, you need to have certain access permissions for network, storage, etc. Please add the following permission declarations in AndroidManifest.xml (for Android 5.0 and higher, the permissions need to be obtained dynamically):
```
<uses-permission android:name="android.permission.INTERNET"/>
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE"/>
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE"/>
```

#### Integrating the SDK

You can integrate the SDK in two ways: [automated integration](#step1) or [manual integration](#step2).

<span id="step1"></span>
#### Automated Integration (Recommended)

1. Add a dependency to the build.gradle file in the app's root directory:
```
dependencies {
	...
    // Add this line
    compile 'com.tencent.qcloud:cosxml:5.4.31'
}
```
2. If you only need the upload, download, and copy features, you can use the simplified version of the SDK:
First, add a Maven repository to the build.gradle file in the root directory of your project:
```
allprojects {
    repositories {
        // Add a Maven repository
        maven {
            url "https://dl.bintray.com/tencentqcloudterminal/maven"
        }
        google()
        jcenter()
    }
}
```
> You need to temporarily add a Maven repository address, it will later sync with to jcenter repository

	Modify step 1 above to the below dependencies:
	```
	dependencies {
	 ...
	 // Add this line
	 compile 'com.tencent.qcloud:cosxml-lite:5.4.31'
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
#### Manual integration
The following JAR files need to be imported into the project and stored in the libs folder:
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

### Initializing the service

#### Method 1: Authorizing via a Temporary Key (Recommended)

There is a risk of key leakage if a mobile device is authenticated with a permanent key. The COS SDKs for Android and iOS support authorizing requests with a temporary key. You only need to set up a service to return the temporary key before you can authorize the COS requests initiated on the device. This method is strongly recommended. For more information, see [Practice of Direct Transfer for Mobile Apps](https://intl.cloud.tencent.com/document/product/436/30618).

If you have already set up a temporary key service and use the JSON data obtained in the STS SDK as the response body, you can use the following code to create an authorization class in the COS SDK.

[//]: # (.cssg-snippet-global-init)
```java
String region = "COS_REGION";

CosXmlServiceConfig serviceConfig = new CosXmlServiceConfig.Builder()
        .setRegion(region)
        .isHttps(true) // Use HTTPS request. The default is HTTP request.
        .builder();

URL url = null;
try {
    // The url address of the temporary key. For how to create a temporary key, see https://cloud.tencent.com/document/product/436/14048
    url = new URL("https://your_auth_server_url");
} catch (MalformedURLException e) {
    e.printStackTrace();
    return;
}

/**
 * Initialize the {@link QCloudCredentialProvider} object to provide a temporary key to the SDK.
 */
QCloudCredentialProvider credentialProvider = new SessionCredentialProvider(new HttpRequest.Builder<String>()
        .url(url)
        .method("GET")
        .build());

CosXmlService cosXmlService = new CosXmlService(context, serviceConfig, credentialProvider);
```

#### Method 2: Authorizing with a Custom Response Body

For higher flexibility, you can inherit the `BasicLifecycleCredentialProvider` class and implement its `fetchNewCredentials()` for custom configurations. For example, you can customize the HTTP response body for the temporary key service to return the server time to the device as the signature start time so as to avoid signature error caused by big device time difference. You can also choose to use other protocols for the communication between the end device and the service side. 

First, define a `MyCredentialProvider` class:

[//]: # (.cssg-snippet-global-init-custom-provider)
```java
public static class MyCredentialProvider extends BasicLifecycleCredentialProvider {

    @Override
    protected QCloudLifecycleCredentials fetchNewCredentials() throws QCloudClientException {

        // First, get the response containing the signature information from your temporary key server

        // Then, parse the response to get the key information
        String tmpSecretId = "COS_SECRETID"; // the secretId of the temporary key
        String tmpSecretKey = "COS_SECRETKEY"; // the secretKey of the temporary key
        String sessionToken = "TOKEN"; // the token of the temporary key
        long expiredTime = 1556183496L;// End of the validity period of the temporary key in seconds

        /*We strongly recommend you use the server return time as the start time of the signature, to avoid incorrect signature caused by deviation of mobile phone's local time from the standard time*/
        // Return server time as the start time of the signature
        long startTime = 1556182000L; // Start of the validity period of the temporary key in seconds

        // todo something you want

        // Finally return the temporary key information object
        return new SessionQCloudCredentials(tmpSecretId, tmpSecretKey, sessionToken, startTime, expiredTime);
    }
}
```

Then, use the `MyCredentialProvider` instance you defined to authorize the request:

[//]: # (.cssg-snippet-global-init-custom)
```java
String region = "COS_REGION";

// Create a CosXmlServiceConfig object to modify the default configuration parameter as needed
CosXmlServiceConfig serviceConfig = new CosXmlServiceConfig.Builder()
        .setRegion(region)
        .isHttps(true) // Use HTTPS request. The default is HTTP request.
        .builder();

/**
 * Initialize the {@link QCloudCredentialProvider} object to provide a temporary key to the SDK.
 */
QCloudCredentialProvider credentialProvider = new MyCredentialProvider();

CosXmlService cosXmlService = new CosXmlService(context, serviceConfig, credentialProvider);
```

#### Method 3: Authorization via a Permanent Key (Not recommended)

If you have not set up a temporary key service, you can use a permanent key to initialize the authorization class. Due to the risk of key leakage, **we do not recommend this method**. It should only be used for temporary testing in a secure environment. 

[//]: # (.cssg-snippet-global-init-secret)
```java
String region = "COS_REGION";

// Create a CosXmlServiceConfig object to modify the default configuration parameter as needed
CosXmlServiceConfig serviceConfig = new CosXmlServiceConfig.Builder()
        .setRegion(region)
        .isHttps(true) // Use HTTPS request. The default is HTTP request.
        .builder();

String secretId = "COS_SECRETID"; // the secretId of the permanent key
String secretKey ="COS_SECRETKEY"; // the secretKey of the permanent key

/**
 * Initialize the {@link QCloudCredentialProvider} object to provide a temporary key to the SDK.
 * @parma secretId permanent key secretId
 * @param secretKey permanent key secretKey
 * @param keyDuration permanent key validity period in seconds
 */
QCloudCredentialProvider credentialProvider = new ShortTimeCredentialProvider(secretId, secretKey, 300);

CosXmlService cosXmlService = new CosXmlService(context, serviceConfig, credentialProvider);
```

### Creating a Bucket

[//]: # (.cssg-snippet-put-bucket)
```java
String bucket = "examplebucket-1250000000";
PutBucketRequest putBucketRequest = new PutBucketRequest(bucket);

// Define the ACL attribute of the bucket. Valid values: private, public-read-write, public-read; Default: private
putBucketRequest.setXCOSACL("private");

// Grant read permission to the authorized user
ACLAccount readACLS = new ACLAccount();
readACLS.addAccount("100000000001", "100000000001");
putBucketRequest.setXCOSGrantRead(readACLS);

// Grant write permission to the authorized user
ACLAccount writeACLS = new ACLAccount();
writeACLS.addAccount("100000000001", "100000000001");
putBucketRequest.setXCOSGrantWrite(writeACLS);

// Grant read and write permissions to the authorized user
ACLAccount writeandReadACLS = new ACLAccount();
writeandReadACLS.addAccount("100000000001", "100000000001");
putBucketRequest.setXCOSReadWrite(writeandReadACLS);
// Set signature verification Host, verify all Headers by default
Set<String> headerKeys = new HashSet<>();
headerKeys.add("Host");
putBucketRequest.setSignParamsAndHeaders(null, headerKeys);
// Use the sync method
try {
    PutBucketResult putBucketResult = cosXmlService.putBucket(putBucketRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// Use the async callback to make requests
cosXmlService.putBucketAsync(putBucketRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        PutBucketResult putBucketResult = (PutBucketResult) result;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException) {
        // todo Put Bucket failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```

### Querying Bucket List
[//]: # (.cssg-snippet-get-service)
```java
GetServiceRequest getServiceRequest = new GetServiceRequest();
// Set signature verification Host, verify all Headers by default
Set<String> headerKeys = new HashSet<>();
headerKeys.add("Host");
getServiceRequest.setSignParamsAndHeaders(null, headerKeys);
// Use the sync method
try {
    GetServiceResult result = cosXmlService.getService(getServiceRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// Use the async callback to make requests
cosXmlService.getServiceAsync(getServiceRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        GetServiceResult getServiceResult = (GetServiceResult) result;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException) {
        // todo Put Bucket Lifecycle failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```

### Upload an Object

**TransferManager** and **COSXMLUploadTask** encapsulate async requests for simple upload and multipart upload APIs and support pausing, resuming, and canceling upload requests. This is recommended for object upload. The sample code is as follows:

[//]: # (.cssg-snippet-transfer-upload-object)
```java
// Initialize TransferConfig
TransferConfig transferConfig = new TransferConfig.Builder().build();

If you have special requirements, you can customize the initialization as follows. For example, for an object >= 2 MB in size, use multipart upload where the size of each part is 1 MB. For a source object larger than 5 MB, use multipart copying where the size of each part is 5 MB.
transferConfig = new TransferConfig.Builder()
        .setDividsionForCopy(5 * 1024 * 1024) // Minimum object size for multipart copying
        .setSliceSizeForCopy(5 * 1024 * 1024) // The size of each part for multipart copying
        .setDivisionForUpload(2 * 1024 * 1024) // Minimum object size for multipart upload
        .setSliceSizeForUpload(1024 * 1024) // The size of each part for multipart upload
        .build();

// Initialize TransferManager
TransferManager transferManager = new TransferManager(cosXmlService, transferConfig);

String bucket = "examplebucket-1250000000"; // Bucket in the format of BucketName-APPID
String cosPath = "exampleobject"; // Identifies the location of the object in the bucket, i.e., the object key
String srcPath = new File(context.getExternalCacheDir(), "exampleobject").toString(); // Absolute path of the local file
String uploadId = null; // If there is an uploadId for initialized multipart upload, assign the value of the uploadId here for resuming upload; otherwise, assign null.
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
        // todo Do something to update progress...
    }
});
// Set return result callback
cosxmlUploadTask.setCosXmlResultListener(new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        COSXMLUploadTask.COSXMLUploadTaskResult cOSXMLUploadTaskResult = (COSXMLUploadTask.COSXMLUploadTaskResult) result;
    }

    @Override
    public void onFail(CosXmlRequest request, CosXmlClientException exception, CosXmlServiceException serviceException) {
        // todo Upload failed because of CosXmlClientException or CosXmlServiceException...
    }
});
// Set task status callback where you can view the task process
cosxmlUploadTask.setTransferStateListener(new TransferStateListener() {
    @Override
    public void onStateChanged(TransferState state) {
        // todo notify transfer state
    }
});

/**
 If you have special requirements, you can write the following codes:
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

[//]: # (.cssg-snippet-get-bucket)
```java
String bucketName = "examplebucket-1250000000";  // Format: BucketName-APPID;
GetBucketRequest getBucketRequest = new GetBucketRequest(bucketName);

// Prefix match used to specify the prefix address of the object returned
getBucketRequest.setPrefix("prefix");

// If this is the first request, you do not need to set a marker. COS will list the objects from the beginning
// If you need to list another page of objects, then you need to set the marker with the GetBucketResult.listBucket.nextMarker value returned from the last request
// If the returned GetBucketResult.listBucket.isTruncated value is false, this indicates that all the objects that satisfies the conditions have been listed.
// getBucketRequest.setMarker(marker);

// Maximum number of entries returned at a time. Default is 1,000
getBucketRequest.setMaxKeys(100);

// The delimiter is a sign. If Prefix exists,
// the same paths between Prefix and delimiter are grouped as the same type and defined as Common Prefix,
// and then all common prefixes are listed. If there is no prefix, the listing starts from the beginning of the path
getBucketRequest.setDelimiter('/');

// Set signature verification Host, verify all Headers by default
Set<String> headerKeys = new HashSet<>();
headerKeys.add("Host");
getBucketRequest.setSignParamsAndHeaders(null, headerKeys);
// Use the sync method
try {
    GetBucketResult getBucketResult = cosXmlService.getBucket(getBucketRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// Use the async callback to make requests
cosXmlService.getBucketAsync(getBucketRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        GetBucketResult getBucketResult = (GetBucketResult) result;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException) {
        // todo Get Bucket failed because of CosXmlClientException or CosXmlServiceException...
    }
});

// If you need to list all objects, see the reference code below:

bucketName = "examplebucket-1250000000";
getBucketRequest = new GetBucketRequest(bucketName);

// Prefix indicates that the object keys to be listed begin with prefix
getBucketRequest.setPrefix("images/");
// The delimiter indicates the separator. Set "/" to list objects in the current directory; set to null to list all objects.
getBucketRequest.setDelimiter("/");
// Set the maximum number of objects to be traversed, which can be up to 1,000 in one listobject operation
getBucketRequest.setMaxKeys(100);
GetBucketResult getBucketResult = null;
do {
    try {
        getBucketResult = cosXmlService.getBucket(getBucketRequest);
    } catch (CosXmlClientException e) {
        e.printStackTrace();
        return;
    } catch (CosXmlServiceException e) {
        e.printStackTrace();
        return;
    }
    // commonPrefixs indicates the path truncated by delimiter. If the delimiter is set to "/", the commonPrefixs indicates the paths of subdirectories.
    List<ListBucket.CommonPrefixes> commonPrefixs = getBucketResult.listBucket.commonPrefixesList;

    // contents indicates the object list
    List<ListBucket.Contents> contents = getBucketResult.listBucket.contentsList;

    String nextMarker = getBucketResult.listBucket.nextMarker;
    getBucketRequest.setMarker(nextMarker);
} while (getBucketResult.listBucket.isTruncated);
```

### Downloading an Object

**TransferManager** and **COSXMLDownloadTask** encapsulate async requests for the download API and support pausing, resuming, and canceling download requests. It also supports resuming interrupted downloads. This is the recommended method for object download. The sample code is as follows:

[//]: # (.cssg-snippet-transfer-download-object)
```java
Context applicationContext = context.getApplicationContext(); // application context
String bucket = "examplebucket-1250000000"; // Bucket in the format of BucketName-APPID
String cosPath = "exampleobject"; // Identifies the location of the object in the bucket, i.e., the object key
String savePathDir = context.getExternalCacheDir().toString(); // Local directory path
String savedFileName = "exampleobject";// Filename of the file saved locally. If left blank (null), then the COS filename will be used by default
// Download the object
TransferConfig transferConfig = new TransferConfig.Builder().build();
// Initialize TransferManager
TransferManager transferManager = new TransferManager(cosXmlService, transferConfig);
COSXMLDownloadTask cosxmlDownloadTask = transferManager.download(applicationContext, bucket, cosPath, savePathDir, savedFileName);
// Set download progress callback
cosxmlDownloadTask.setCosXmlProgressListener(new CosXmlProgressListener() {
    @Override
    public void onProgress(long complete, long target) {
        // todo Do something to update progress...
    }
});
// Set return result callback
cosxmlDownloadTask.setCosXmlResultListener(new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        COSXMLDownloadTask.COSXMLDownloadTaskResult cOSXMLDownloadTaskResult = (COSXMLDownloadTask.COSXMLDownloadTaskResult) result;
    }

    @Override
    public void onFail(CosXmlRequest request, CosXmlClientException exception, CosXmlServiceException serviceException) {
        // todo Download failed because of CosXmlClientException or CosXmlServiceException...
    }
});
// Set task status callback where you can view the task process
cosxmlDownloadTask.setTransferStateListener(new TransferStateListener() {
    @Override
    public void onStateChanged(TransferState state) {
        // todo notify transfer state
    }
});

/**
 If you have special requirements, you can write the following codes:
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

> Advanced download APIs support resuming interrupted downloads. HEAD requests will be sent to obtain file information before download. If you are using a temporary key or accessing with a sub-account, please make sure that you have HeadObject permissions.  

### Deleting an object

[//]: # (.cssg-snippet-delete-object)
```java
String bucket = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID
String cosPath = "exampleobject"; // Identifies the location of the object in the bucket, i.e., the object key

DeleteObjectRequest deleteObjectRequest = new DeleteObjectRequest(bucket, cosPath);
// Set signature verification Host, verify all Headers by default
Set<String> headerKeys = new HashSet<>();
headerKeys.add("Host");
deleteObjectRequest.setSignParamsAndHeaders(null, headerKeys);
//  Delete using sync method
try {
    DeleteObjectResult deleteObjectResult = cosXmlService.deleteObject(deleteObjectRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// Use the async callback to make requests
cosXmlService.deleteObjectAsync(deleteObjectRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest cosXmlRequest, CosXmlResult result) {
        DeleteObjectResult deleteObjectResult = (DeleteObjectResult) result;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException) {
        // todo Delete Object failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```
