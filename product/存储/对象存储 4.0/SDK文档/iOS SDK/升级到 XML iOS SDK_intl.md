After comparing JSON iOS SDK and XML iOS SDK documents, you may find XML iOS SDK not only increased the document numbers, but also improved in terms of architecture, availability,  security, usability, robustness and transmission. The following instructions can help you upgrade to XML iOS SDK.

## Feature Comparison

The following table compares the main features of JSON SDK and XML SDK:

| Feature | XML SDK | JSON SDK |
| -------- | :------------: | :------------------:    |
| File upload | Local files, binary data and multipart upload are supported.<br>Existing files are overwritten by default.<br>Intelligent selection of upload mode<br>File size is limited to 5 GB in a simple upload.<br>File size is limited to 48.82 TB (50,000 GB) in a multipart upload. | Only local file upload is supported.<br>You can select whether to overwrite existing files.<br>You need to manually select simple upload or multipart upload.<br>File size is limited to 20 MB in a simple upload.<br>File size is limited to 64 GB in a multipart upload. |
| File deletion | Batch deletion is supported. | Only deletion of a single file is supported |
| Basic operations on buckets | Create a bucket<br>Get a bucket<br>Delete a bucket | Not supported |
| Operations on bucket ACLs | Set bucket ACL<br>Get bucket ACL<br>Delete bucket ACL | Not supported |
| Bucket lifecycle | Create bucket lifecycle<br>Get bucket lifecycle<br>Delete bucket lifecycle | Not supported |
| Directory operations | No APIs are provided separately. | Create a directory<br>Query a directory<br>Delete a directory |

## Upgrade Directions
Upgrade iOS SDK by following the 5 steps below.

**1. Update iOS SDK**
You can integrate SDK via cocoapods or by downloading packaged dynamic libraries. We recommend using cocoapods for import.
-  **Importing using Cocoapods (recommended)**  
In Podfile, use:
```
  pod 'QCloudCOSXML'
```

-  **Importing using the packaged dynamic library (manual integration)**  
You can download the desired version from [Release](https://github.com/tencentyun/qcloud-sdk-ios/releases).  
Drag **QCloudCOSXML.framework, QCloudCore.framework and libmtasdk.a** to your project, as shown below:
![](https://main.qcloudimg.com/raw/14c8f5773ea19bc681b7f862dd6384fb.png)  

	And add the following dependent libraries:
> - CoreTelephony
> - Foundation
> - SystemConfiguration
> - libc++.tbd

**Configure the project**
Set up "Other Linker Flags" in "Build Settings" and add the parameters:
```shell
-ObjC
-all_load
```

See the figure below:
![](https://main.qcloudimg.com/raw/3bee5d2c3cb7e7f80b94c5f6bbe2ce5e.png)

**2. Change the SDK authentication method**

JSON SDK requires you to compute a signature by yourself in the application server and then return it to the client. XML SDK adopts new authentication algorithms, and we strongly recomend integrating the temporary key (STS) solution in your application server. This solution does not require understanding of signature computing process. You can just integrate CAM in your server to get a temporary key and return it to the client, and then configure it in SDK so that SDK can manage the key and compute the signature. The temporary key will automatically expire after a period of time, while the permanent key will not be disclosed.
You can also control access permissions at different granularities. For more information, see [Practice of Direct Transfer for Mobile Apps](https://intl.cloud.tencent.com/document/product/436/30618) and [Temporary Key Generation and Usage Guide](https://intl.cloud.tencent.com/document/product/436/14048).

If you still compute a signature manually in the application server and return it to the client for use, note that the signature algorithm has changed. One-time signatures and multiple-time signatures are no longer used. Instead, you can set a validity period of the signature to ensure security. For more information, see [XML Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).

**3. Change the SDK initialization method**

XML SDK makes some changes about initialization APIs:

- `COSClient` is replaced by `QCloudCOSXMLService`, but their functions are the same. `QCloudServiceConfiguration` is added to configure more information.
- You need to instantiate a key provider `QCloudAuthentationV5Creator` during initialization to provide a valid key, and a temporary key is recommended.

**JSON SDK is initialized as follows:**

```
COSClient *client= [[COSClient alloc] initWithAppId:appId withRegion:@“sh”];
```

**XML SDK is initialized as follows:**
>In the sample code, a temporary key is used to get a signature. It is strongly recommended to return the server time as the start time of the signature, to avoid incorrect signature caused by large deviation of mobile phone's local time from the standard time.

```
- (void) signatureWithFields:(QCloudSignatureFields*)fileds
                     request:(QCloudBizHTTPRequest*)request
                  urlRequest:(NSURLRequest*)urlRequst
                   compelete:(QCloudHTTPAuthentationContinueBlock)continueBlock
{
  /*Request the temporary Secret ID, Secret Key and Token from signature server*/
   QCloudCredential* credential = [QCloudCredential new];
   credential.secretID = @"The temporary Secret ID obtained from the CAM system";
   credential.secretKey = @"The temporary Secret Key obtained from the CAM system";
   credential.token = @"The Token (session ID) returned from the CAM system"
   /*It is strongly recommended to return the server time as the start time of the signature, to avoid incorrect signature caused by large deviation of mobile phone's local time from the standard time. */
   credential.startDate = /*Returned server time*/
   credential.expiretionDate	 = /*Signature expiration time*/
   QCloudAuthentationV5Creator* creator = [[QCloudAuthentationV5Creator alloc] initWithCredential:credential];
   QCloudSignature* signature =  [creator signatureForData:urlRequst];
   continueBlock(signature, nil);

}

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
     QCloudServiceConfiguration* configuration = [QCloudServiceConfiguration new];
     configuration.appID = @"*****";
     configuration.signatureProvider = self;
     QCloudCOSXMLEndPoint* endpoint = [[QCloudCOSXMLEndPoint alloc] init];
     endpoint.regionName = @"ap-beijing";//Service region name. See the notes for available regions.
     configuration.endpoint = endpoint;

     [QCloudCOSXMLService registerDefaultCOSXMLWithConfiguration:configuration];
     [QCloudCOSTransferMangerService registerDefaultCOSTransferMangerWithConfiguration:configuration];

}
```


**4. Change the bucket name and the abbreviations of available regions**

The bucket name and the abbreviations of available regions in XML SDK are different from those in JSON SDK. You need to make changes accordingly.


**Bucket**
The name of an XML SDK bucket consists of a user-defined string and an APPID that are connected by a dash ("-"). For example, `exampleobject-1250000000`, where `exampleobject` is a user-defined string and `1250000000` is an APPID.

>APPID is one of the Tencent Cloud account IDs, and is used to associate with cloud resources. After applying for a Tencent Cloud account successfully, you will be assigned an APPID automatically. APPID can be found in **Account Info** on the [Tencent Cloud Console](https://console.cloud.tencent.com/).

Refer to the following sample code to set a bucket:
```
NSString *bucket = "exampleobject-1250000000";
```

**Abbreviations of available regions for buckets**
The abbreviations of available regions for XML SDK buckets have changed. The following table lists region abbreviations in JSON SDK and XML SDK:

| Region | Abbreviation in XML SDK | Abbreviation in JSON SDK |
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

During initialization, set the abbreviation of the region where the bucket locates in `regionName` of `QCloudServiceConfiguration`:

```
//AppDelegate.m

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
     QCloudServiceConfiguration* configuration = [QCloudServiceConfiguration new];
     configuration.appID = @"*****";
     configuration.signatureProvider = self;
     QCloudCOSXMLEndPoint* endpoint = [[QCloudCOSXMLEndPoint alloc] init];
     endpoint.regionName = @"ap-beijing";//Service region name. See the notes for available regions.
     configuration.endpoint = endpoint;

     [QCloudCOSXMLService registerDefaultCOSXMLWithConfiguration:configuration];
     [QCloudCOSTransferMangerService registerDefaultCOSTransferMangerWithConfiguration:configuration];

}
```

**5. Change APIs**

After JSON iOS SDK is upgraded to XML iOS SDK, the APIs for some operations have changed. Make corresponding changes according to your actual needs. In addition, we have encapsulated the APIs to make it easier to use the SDK. For more information, see our examples and [API Documentation](https://intl.cloud.tencent.com/document/product/436/11280).

There are three changes:

**1) No directory API**

No separate directory API is provided in XML SDK. As COS comes with no folders and directories, it will not create a "project" folder for uploading the object "project/a.txt". To make it easier for you to get started, COS simulates the display mode of "folder" or "directory" in the console and graphical tools such as COS browser. This is realized by creating an empty object with a key value of "project/" and displaying it as a traditional folder.

For example: When you upload the object "project/doc/a.txt", the delimiter "/" simulates the display mode of "folder", and you can see the folders "project" and "doc" on the console. The folder "doc" is displayed under the folder "project" and contains the file "a.txt".

Therefore, in a use case for file upload only, you can directly upload files without creating a folder first.

If a folder is allowed in a use case, the feature of creating a folder should be supported. You can upload a 0 KB file whose path ends with '/'. When you call the API `GetBucket`, you can use the file as a folder.


**2) QCloudCOSTransferMangerService**

In XML SDK, we encapsulate an operation named `QCloudCOSTransferMangerService` which can intelligently select simple upload (copy) or multipart upload (copy), and optimize API design and transmission performance. You can use the operation directly. The main features of `QCloudCOSTransferMangerService` include:

* Resuming upload from breakpoint.
* Selecting simple upload (copy) or multipart upload (copy) according to the file size.

The sample code for using `QCloudCOSTransferMangerService` for upload:

```
  QCloudCOSXMLUploadObjectRequest* put = [QCloudCOSXMLUploadObjectRequest new];
  NSURL* url = /*URL of file*/;
  put.object = @"filename.jpg";
  put.bucket = @"exampleobject-1250000000";
  put.body =  url;
  [put setSendProcessBlock:^(int64_t bytesSent, int64_t totalBytesSent, int64_t totalBytesExpectedToSend) {
      NSLog(@"upload %lld totalSend %lld aim %lld", bytesSent, totalBytesSent, totalBytesExpectedToSend);
  }];
  [put setFinishBlock:^(id outputObject, NSError* error) {

  }];
  [[QCloudCOSTransferMangerService defaultCOSTransferManager] UploadObject:put];

```
The sample code for using `QCloudCOSTransferMangerService` to resume upload from breakpoint:

```
QCloudCOSXMLUploadObjectRequest* put = [QCloudCOSXMLUploadObjectRequest new];
  //···Set some parameters for upload
  put.initMultipleUploadFinishBlock = ^(QCloudInitiateMultipartUploadResult * multipleUploadInitResult, QCloudCOSXMLUploadObjectResumeData resumeData) {
	//Call back the block after you initialize multipart upload, in which you can obtain resumeData for generating a multipart upload request
	 QCloudCOSXMLUploadObjectRequest* request = [QCloudCOSXMLUploadObjectRequest requestWithRequestData:resumeData];
  };

  [[QCloudCOSTransferMangerService defaultCOSTransferManager] UploadObject:put];
  //···When initialization is completed and upload is not completed
  NSError* error;
  //The following shows how resumeData is generated after the user cancels the upload
  resumeData = [put cancelByProductingResumeData:&error];
  if (resumeData) {
    QCloudCOSXMLUploadObjectRequest* request = [QCloudCOSXMLUploadObjectRequest requestWithRequestData:resumeData];
  }
  //The generated request for resuming upload can be directly uploaded
  [[QCloudCOSTransferMangerService defaultCOSTransferManager] UploadObject:request];

```
>The multipart upload uses the serial mode where parts must be uploaded in sequence. Under the following circumstances, resuming upload from breakpoint cannot be used.
 - The file to be uploaded is smaller than 1 MB and multipart upload is not used.
 - The simple upload API rather than the QCloudCOSXMLUploadObjectRequest class is used to upload files.
 - Multipart upload initialization is not completed (the callback for completed upload initialization is yet to be called) when you cancel the generation of resumeData.

**3) New APIs**

The following APIs are added in XML SDK, and they can be called as needed:
* Bucket operations, such as QCloudPutBucketRequest, QCloudGetBucketRequest, and QCloudListBucketRequest.
* Operations on Bucket ACLs, such as QCloudPutBucketACLRequest, and QCloudGetBucketACLRequest.
* Operations on bucket lifecycle, such as PQCloudutBucketLifecycleRequest, and QCloudGetBucketLifecycleRequest.

For more information, see [iOS SDK API Documentation](https://intl.cloud.tencent.com/document/product/436/11280).

