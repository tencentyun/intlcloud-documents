If you have carefully compared the documentations of JSON Java SDK and XML Java SDK, you can find that the latter is not simply an incremental update version of the former. XML Java SDK has made great improvements in architecture, availability and security, as well as in usability, robustness and performance. If you want to upgrade to XML Java SDK, refer to the following instructions.

## Feature Comparison

| Feature | XML Java SDK | JSON Java SDK |
| -------- | :------------: | :------------------:    |
| File upload | Upload of local files, byte streams and input streams is supported.<br>Existing files are overwritten by default.<br>Intelligent selection of upload mode: File size is limited to 5 GB in a simple upload;<br>File size is limited to 48.82 TB (50,000 GB) in a multipart upload. | Only local file upload is supported.<br>You can select whether to overwrite existing files.<br>You need to manually select simple upload or multipart upload.<br>File size is limited to 20 MB in a simple upload.<br>File size is limited to 64 GB in a multipart upload. |
| File deletion | Batch deletion is supported. | Only deletion of a single file is supported |
| Basic operations on buckets | Create a bucket<br>Get a bucket<br>Delete a bucket | Not supported |
| Operations on bucket ACLs | Set bucket ACL<br>Get bucket ACL<br>Delete bucket ACL | Not supported |
| Bucket lifecycle | Create bucket lifecycle<br>Get bucket lifecycle<br>Delete bucket lifecycle | Not supported |
| Directory operations | No APIs are provided separately. | Create a directory<br>Query a directory<br>Delete a directory |

## Upgrade Procedure
Upgrade Java SDK by following the steps below.

**1. Update Java SDK**

XML Java SDK is published in the [maven](https://mvnrepository.com/artifact/com.qcloud/cos_api) central repository. We recommend that you introduce the SDK using maven's automatic dependency management.

Add the following dependency to the "pom.xml" file of the maven project:

```xml
<!-- https://mvnrepository.com/artifact/com.qcloud/cos_api -->
<dependency>
    <groupId>com.qcloud</groupId>
    <artifactId>cos_api</artifactId>
    <version>5.x.x</version>
</dependency>

```

You can also directly download a jar package of applicable version in [maven](https://mvnrepository.com/artifact/com.qcloud/cos_api) central repository, and add it manually to your project.


**2. Change the bucket name and the abbreviations of available regions**

The bucket name and the abbreviations of available regions in XML Java SDK are different from those in JSON Java SDK. You need to make changes accordingly.

**Bucket**

The name of an XML SDK bucket consists of a user-defined string and an APPID that are connected by a dash ("-").
For example, `examplebucket-1250000000`, where `examplebucket` is a user-defined string, and `1250000000` is an APPID.

>APPID is one of the Tencent Cloud account IDs, and is used to associate with cloud resources. After applying for a Tencent Cloud account successfully, you will be assigned an APPID automatically. APPID can be found in **Account Info** on the [Tencent Cloud Console](https://console.cloud.tencent.com/).

Refer to the following sample code to set a bucket:

```java
COSCredentials cred = new BasicCOSCredentials("COS_SECRETID", "COS_SECRETKEY");
// The new region name is used. For the list of available regions, you can refer to the official documentation, or see the region mapping table of XML SDK and JSON SDK below.
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing-1"));
COSClient cosclient = new COSClient(cred, clientConfig);
// The bucket name must contain appid.
String bucketName = "examplebucket-1250000000";

// The following is an example of uploading a file to this bucket.
String key = "docs/exampleobject.doc";
File localFile = new File("src/test/resources/len10M.txt");
PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, localFile);
// Set the storage type: Standard (default) and standard_ia.
putObjectRequest.setStorageClass(StorageClass.Standard_IA);
try {
	PutObjectResult putObjectResult = cosclient.putObject(putObjectRequest);
	// The file etag is returned by putobjectResult.
    String etag = putObjectResult.getETag();
} catch (CosServiceException e) {
	e.printStackTrace();
} catch (CosClientException e) {
	e.printStackTrace();
}

// Shut down the client
cosclient.shutdown();

```

**Abbreviations of available regions for buckets**
The abbreviations of available regions for XML SDK buckets have changed. See the following table for region abbreviations in JSON SDK and XML SDK:

| Region | Abbreviation in XML SDK | Abbreviation in JSON SDK |
| -------- | ------------ | ---------------------------------------- |
| Beijing Zone 1 (North China) | ap-beijing-1 | tj |
| Beijing | ap-beijing | bj |
| Shanghai (East China) | ap-shanghai | sh |
| Guangzhou (South China) | ap-guangzhou | gz |
| Chengdu (Southwest) | ap-chengdu | cd |
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

When initializing `COSClient`, set the abbreviation of the region where the bucket resides in `ClientConfig`:

```java
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing-1"));
COSClient cosclient = new COSClient(cred, clientConfig);

```

**3. Change APIs**
After JSON Java SDK is upgraded to XML Java SDK, the APIs for some operations have changed. Make corresponding changes based on your actual needs. In addition, we have encapsulated the APIs to make it easier to use the SDK. For more information, see our examples and [API Documentation](https://intl.cloud.tencent.com/document/product/436/10199).

Here are the main changes:

**1) No directory API**

No separate directory API is provided in XML SDK. As COS comes with no folders and directories, it will not create a "project" folder for uploading the object `project/a.txt`. To make it easier for you to get started, COS simulates the display mode of "folder" or "directory" in the console and graphical tools such as COS browser. This is realized by creating an empty object with a key value of `project/` and displaying it as a traditional folder.

For example: When you upload the object `project/doc/a.txt`, the delimiter `/` simulates the display mode of "folder", and you can see the folders "project" and "doc" on the console. The folder "doc" is displayed under the folder "project" and contains the file "a.txt".

Therefore, in a use case for file upload only, you can directly upload files without creating a folder first. If a folder is allowed in a use case, the feature of creating a folder should be supported. You can upload a 0 KB file whose path ends with `/`. When you call the API GetBucket, you can use the file as a folder.

**2) TransferManager**

In XML Java SDK, we encapsulate the upload, download and copy operations into `TransferManager`, and optimize API design and transmission performance. You can use it directly.

The main features of `TransferManager` include:

- Suspending and resuming the upload/download process.
- Selecting simple upload or multipart upload according to the file size. A threshold can be set.
- Listening the task status.

The sample code for using `TransferManager` for upload:

```java
TransferManager transferManager = new TransferManager(cosclient, threadPool);

String key = "docs/exampleobject.doc";
File localFile = new File("src/test/resources/len30M.txt");
PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, localFile);
try {
    // Return an asynchronous result Upload. You can synchronously call waitForUploadResult to wait for upload to end. If upload is successful, UploadResult is returned, and if it fails, an exception will be thrown.
    Upload upload = transferManager.upload(putObjectRequest);
    Thread.sleep(10000);
    // Suspend the task
    PersistableUpload persistableUpload = upload.pause();
    // Resume upload
    upload = transferManager.resumeUpload(persistableUpload);
    // Display upload progress
    showTransferProgress(upload);
    // Wait for the upload task to complete
    UploadResult uploadResult = upload.waitForUploadResult();
    System.out.println(uploadResult.getETag());

    // Canceling upload tasks is also supported
    transferManager.cancel();
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
} catch (InterruptedException e) {
    e.printStackTrace();
}

ransferManager.shutdownNow();
cosclient.shutdown();

```

**3) Signature algorithm**

Generally, you do not need to compute a signature manually. However, if you return an SDK signature to the frontend, note that the signature algorithm has changed. One-time signatures and multiple-time signatures are no longer used. Instead, you can set a validity period of the signature to ensure security. For more information, see [XML Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).

**4) New APIs**

The following APIs are added in XML Java SDK, and they can be called as needed:

* Bucket operations, such as createBucket, GetBucket (List Objects), and ListBuckets.
* Operations on bucket ACLs, such as getBucketAcl, and setBucketAcl.
* Operations on bucket lifecycle, such as setBucketLifecycleConfiguration, getBucketLifecycleConfiguration, and deleteBucketLifecycleConfiguration.

For more information, see [Java SDK API documentation](https://intl.cloud.tencent.com/document/product/436/10199).

