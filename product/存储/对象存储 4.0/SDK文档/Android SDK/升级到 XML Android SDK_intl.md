After comparing JSON Android SDK and XML Android SDK documents, you may find XML Android SDK not only increased the document numbers, but also improved in terms of architecture, availability,  security, usability, robustness and transmission. XML Android SDK has made great improvements in architecture, availability and security, as well as in usability, robustness and transmission performance. The following instructions can help you upgrade to XML Android SDK.

## Feature Comparison

The following table compares the main features of JSON Android SDK and XML Android SDK:

| Feature | XML Android SDK | JSON Android SDK |
| -------- | :------------: | :------------------:    |
| File upload | Upload of local files, byte streams and input streams is supported.<br>Existing files are overwritten by default.<br>Intelligent selection of upload mode<br>File size is limited to 5 GB in a simple upload.<br>File size is limited to 48.82 TB (50,000 GB) in a multipart upload. | Only local file upload is supported.<br>You can select whether to overwrite existing files.<br>You need to manually select simple upload or multipart upload.<br>File size is limited to 20 MB in a simple upload.<br>File size is limited to 64 GB in a multipart upload. |
| File deletion | Batch deletion is supported. | Only deletion of a single file is supported |
| Basic operations on buckets | Create a bucket<br>Get a bucket<br>Delete a bucket | Not supported |
| Operations on bucket ACLs | Set bucket ACL<br>Get bucket ACL<br>Delete bucket ACL | Not supported |
| Bucket lifecycle | Create bucket lifecycle<br>Get bucket lifecycle<br>Delete bucket lifecycle | Not supported |
| Directory operations | No APIs are provided separately. | Create a directory<br>Query a directory<br>Delete a directory |

## Upgrade Directions
Upgrade Android SDK by following the steps below.

**1. Update Android SDK**

COS XML Android SDK is released on the Maven package management platform of [Bintray](https://bintray.com). It is recommended that you update Android SDK by means of auto integration.

Add the Maven repository to the build.gradle file in your project's root directory using the following code:

```
allprojects {

    repositories {
        ...
        // Add the following Maven repository URL
        maven {
            url "https://dl.bintray.com/tencentqcloudterminal/maven"
        }
    }
}
```

Add dependencies to the build.gradle file in your project's root directory using the following code:

```
dependencies {
	...
    // Add the following line
    compile 'com.tencent.qcloud:cosxml:5.4.+'
}
```

You can also continue to manually add jar packages. All the jar packages can be downloaded from [COS XML Android SDK-release](https://github.com/tencentyun/qcloud-sdk-android/releases).

**2. Change the SDK authentication method**

JSON Android SDK requires you to compute a signature by yourself in the application server and then return it to the client. JSON Android SDK requires you to compute a signature by yourself in the application server and then return it to the client. XML SDK adopts new authentication algorithms, and we strongly recomend integrating the temporary key (STS) solution in your application server. This solution does not require understanding of signature computing process. You can just integrate CAM in your server to get a temporary key and return it to the client, and then configure it in SDK so that SDK can manage the key and compute the signature. The temporary key will automatically expire after a period of time, while the permanent key will not be disclosed.
You can also control access permissions at different granularities. For more information, see [Practice of Direct Transfer for Mobile Apps](https://intl.cloud.tencent.com/document/product/436/30618) and [Temporary Key Generation and Usage Guide](https://intl.cloud.tencent.com/document/product/436/14048).

If you still compute a signature manually in the application server and return it to the client for use, note that the signature algorithm has changed. One-time signatures and multiple-time signatures are no longer used. Instead, you can set a validity period of the signature to ensure security. For more information, see [XML Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).

**3. Change the SDK initialization method**

The initialization APIs in XML Android SDK have changed:

* For easy differentiation, `COSClientConfig` is replaced with `CosXmlServiceConfig`, and `COSClient` with `CosXmlService`, but their functions are the same.
* You need to instantiate a key provider `QCloudCredentialProvider` during initialization to provide a valid key, and a temporary key is recommended.

**JSON SDK is initialized as follows:**

```
//Create a COSClientConfig object to modify the default configuration parameters as needed
COSClientConfig config = new COSClientConfig();
//Set the region
config.setEndPoint(COSEndPoint.COS_GZ);

Context context = getApplicationContext()；
String appid =  "APPID registered with Tencent Cloud";
String peristenceId = "Persistence ID";

//Create a COSlient object to perform operations on COS
COSClient cos = new COSClient(context,appid,config,peristenceId);
```

**XML SDK is initialized as follows:**

```
String appid = "1250000000";
String region = "ap-guangzhou"; 

//Create a CosXmlServiceConfig object to modify the default configuration parameter as needed
CosXmlServiceConfig serviceConfig = new CosXmlServiceConfig.Builder()
       .setAppidAndRegion(appid, region)
       .builder();
       
/**
 * Get the URL of the authorization service
 */
URL url = null; 
try {
    url = new URL("your_auth_server_url"); //URL of the authorization service in the application server
} catch (MalformedURLException e) {
    e.printStackTrace();
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


**4. Change the bucket name and the abbreviations of available regions**

The bucket name and the abbreviations of available regions in XML SDK are different from those in JSON SDK. You need to make changes accordingly.

**Bucket**

The name of an XML Android SDK bucket consists of a user-defined string and an APPID that are connected by a dash ("-"). For example, `examplebucket-1250000000`, where `examplebucket` is a user-defined string and `1250000000` is an APPID.

>APPID is one of the Tencent Cloud account IDs, and is used to associate with cloud resources. After applying for a Tencent Cloud account successfully, you will be assigned an APPID automatically. APPID can be found in **Account Info** on the [Tencent Cloud Console](https://console.cloud.tencent.com/).

Refer to the following sample code to set a bucket:

```
String bucket = "examplebucket-1250000000";
String cosPath = "exampleobject.doc";
String srcPath = Environment.getExternalStorageDirectory().getPath() + "/exampleobject.doc";
//Upload a file
COSXMLUploadTask cosxmlUploadTask = transferManager.upload(bucket, cosPath, srcPath, uploadId);
```

**Abbreviations of available regions for buckets**

The abbreviations of available regions for buckets in XML Android SDK are different from those in JSON Android SDK, as shown in the following table:

| Region | Abbreviation in XML Android SDK | Abbreviation in JSON Android SDK |
| -------- | ------------ | ---------------------------------------- |
| Beijing Zone 1 (North China) | ap-beijing-1 | tj |
| Beijing | ap-beijing | bj |
| Shanghai (East China) | ap-shanghai | sh |
| Guangzhou (South China) | ap-guangzhou | gz |
| Chengdu (Southwest China) | ap-chengdu | cd |
| Chongqing | ap-chongqing | None |
| Singapore | ap-singapore | sgp |
| Hong Kong | ap-hongkong | hk |
| Toronto | na-toronto | ca |
| Frankfurt | eu-frankfurt | ger |
| Mumbai | ap-mumbai | None |
| Seoul | ap-seoul | None |
| Silicon Valley | na-siliconvalley | None |
| Virginia | na-ashburn | None |
| Bangkok | ap-bangkok | None |
| Moscow | eu-moscow | None |

During initialization, set the abbreviation of the region where the bucket locates in `CosXmlServiceConfig`:

```
String appid = "1250000000";
String region = "ap-guangzhou"; 

CosXmlServiceConfig serviceConfig = new CosXmlServiceConfig.Builder()
       .setAppidAndRegion(appid, region)
       .builder();
```

**5. Change APIs**

After JSON SDK is upgraded to XML SDK, the APIs for some operations have changed. Make the corresponding changes based on your actual needs. In addition, we have encapsulated the APIs to make it easier to use the SDK. For more information, see our examples and [API Documentation](https://intl.cloud.tencent.com/document/product/436/12159).

There are three changes:

**1) No directory API**

No separate directory API is provided in XML SDK. As COS comes with no folders and directories, it will not create a "project" folder for uploading the object "project/a.txt".
To make it easier for you to get started, COS simulates the display mode of "folder" or "directory" in the console and graphical tools such as COS browser. This is realized by creating an empty object with a key value of "project/" and displaying it as a traditional folder.

For example: When you upload the object "project/doc/a.txt", the delimiter "/" simulates the display mode of "folder", and you can see the folders "project" and "doc" on the console. The folder "doc" is displayed under the folder "project" and contains the file "a.txt".

Therefore, in a use case for file upload only, you can directly upload files without creating a folder first.

If a folder is allowed in a use case, the feature of creating a folder should be supported. You can upload a 0 KB file whose path ends with '/'. When you call the API `GetBucket`, you can use the file as a folder.


**2) TransferManager**

In XML SDK, we encapsulate the upload, download and copy operations into `TransferManager` which can be used directly, and optimize API design and transmission performance. The main features of `TransferManager` include:

* Suspending and resuming the upload/download process.
* Selecting simple upload or multipart upload according to the file size. A threshold can be set.
* Listening the task status.

The sample code for using `TransferManager` for upload:

```
// Initialize TransferConfig
TransferConfig transferConfig = new TransferConfig.Builder().build();
/**
If you have special requirements, you can customize the initialization. For example, when the file is larger than or equal to 2 MB, the multipart upload is enabled, and the part size is 1 MB. When the source file is larger than 5 MB, the multipart copy is enabled, and the part size is 5 MB.
TransferConfig transferConfig = new TransferConfig.Builder()
        .setDividsionForCopy(5 * 1024 * 1024) // The minimum file size to determine whether to enable multipart copy
        .setSliceSizeForCopy(5 * 1024 * 1024) // Part size for multipart copy
        .setDivisionForUpload(2 * 1024 * 1024) // The minimum file size to determine whether to enable multipart upload
        .setSliceSizeForCopy(1024 * 1024) // Part size for multipart upload
        .build();
*/

// Initialize TransferManager
TransferManager transferManager = new TransferManager(cosXml, transferConfig);

String bucket = "Bucket name";
String cosPath = "ObjectKey"; // The absolute path on COS, for example: cosPath = "exampleobject.doc";
String srcPath = "Absolute path to the local file"; // For example, srcPath=Environment.getExternalStorageDirectory().getPath() + "/exampleobject.doc";
String uploadId = "UploadId for multipart upload";// Used to resume upload. If multipart upload is not enabled, it is null.
// Upload files
COSXMLUploadTask cosxmlUploadTask = transferManager.upload(bucket, cosPath, srcPath, uploadId);
// Set callback for upload progress
cosxmlUploadTask.setCosXmlProgressListener(new CosXmlProgressListener() {
            @Override
            public void onProgress(long complete, long target) {
                float progress = 1.0f * complete / target * 100;
                Log.d("TEST",  String.format("progress = %d%%", (int)progress));
            }
        });
// Set callback for result
cosxmlUploadTask.setCosXmlResultListener(new CosXmlResultListener() {
            @Override
            public void onSuccess(CosXmlRequest request, CosXmlResult result) {
                Log.d("TEST",  "Success: " + result.printResult());
            }

            @Override
            public void onFail(CosXmlRequest request, CosXmlClientException exception, CosXmlServiceException serviceException) {
                Log.d("TEST",  "Failed: " + (exception == null ? serviceException.getMessage() : exception.toString()));
            }
        });
// Set callback for task status to check the task process
cosxmlUploadTask.setTransferStateListener(new TransferStateListener() {
            @Override
            public void onStateChanged(TransferState state) {
                Log.d("TEST", "Task state:" + state.name());
            }
        });

/**
If you have special requirements, you can write the following codes:
 PutObjectRequest putObjectRequest = new PutObjectRequest(bucket, cosPath, srcPath);
 putObjectRequest.setRegion(region); // Set the region where the bucket resides
 putObjectRequest.setSign(600); // Set the validity period of signature
 putObjectRequest.setNeedMD5(true); // Set whether to enable Md5 check
 COSXMLUploadTask cosxmlUploadTask = transferManager.upload(putObjectRequest, uploadId);
*/

// Cancel upload task
cosxmlUploadTask.cancel();


// Suspend upload task
cosxmlUploadTask.pause();

// Resume upload task
cosxmlUploadTask.resume();
```

**3) New APIs**

The following APIs are added in XML Android SDK, which can be called as needed:

* Bucket operations, such as PutBucketRequest, GetBucketRequest, and ListBucketRequest.
* Operations on Bucket ACLs, such as PutBucketACLRequest, and GetBucketACLRequest.
* Operations on bucket lifecycle, such as PutBucketLifecycleRequest, and GetBucketLifecycleRequest.

For more information, see [Android SDK API Documentation](https://intl.cloud.tencent.com/document/product/436/12159).

