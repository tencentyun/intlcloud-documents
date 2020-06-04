## Download and Installation

### Relevant resources

- Download the COS iOS SDK source code [here] (https://github.com/tencentyun/qcloud-sdk-ios.git).   
- You can download the packaged SDK in Framework format by selecting the desired version from [Releases](https://github.com/tencentyun/qcloud-sdk-ios/releases).
- Find the quick SDK download link [here](https://cos-sdk-archive-1253960454.file.myqcloud.com/qcloud-sdk-ios/latest/qcloud-sdk-ios.zip).
- For more examples, see [here](https://github.com/tencentyun/qcloud-sdk-ios-samples.git).
- For the COS XML version change log, see [here] (https://github.com/tencentyun/qcloud-sdk-ios/blob/master/CHANGELOG.md).

### Environmental dependency

- This SDK supports iOS 8.0 or above.
- Your mobile phone must be connected to a network (GPRS, 3G, 4G, Wi-Fi, etc.)
- Log into the CAM Console and get your `SecretId` and `SecretKey` from the [Access Key] (https://console.cloud.tencent.com/capi) page and get your APPID from the [Account Center](https://console.cloud.tencent.com/developer).

>For the definitions of parameters such as `SecretID`, `SecretKey`, and `Bucket`, see the [COS Glossary](https://intl.cloud.tencent.com/document/product/436/7751).

### Installing the SDK

#### Importing the SDK

You can integrate the SDK via `cocoapods` or by downloading packaged static libraries. We recommend you use `cocoapods` for import.

-**Importing using cocoapods (recommended)**  
  In Podfile, use:
```shell
pod 'QCloudCOSXML'
```

-**Importing using a packaged static library (manual integration)**  
  Drag **QCloudCOSXML.framework, QCloudCore.framework and libmtasdk.a** to your project, as shown below:
  ![](https://main.qcloudimg.com/raw/ce990d8871293daec0aa434f28b152e6.png)  
  And add the following dependent libraries:
 - CoreTelephony
 - Foundation
 - SystemConfiguration
 - libc++.tbd

#### Configuring the project

Set up "Other Linker Flags" in "Build Settings" and add the parameter:

```shell
-ObjC
-all_load
```

See the figure below:
![](https://main.qcloudimg.com/raw/125218fad3f4781cae8f992d9a152057.png)

>
>The Tencent Cloud COS XML iOS SDK uses HTTP protocol. To run the SDK on iOS, enable transfer over HTTP.
> You can enable transfer over HTTP in the following two ways:
>- **Configuring manually**
> Add "App Transport Security Settings" to the "info.plist" file of the project, and then add "Allow Arbitrary Loads" under "App Transport Security Settings", and set its type to "Boolean", and value to "YES".
>- **Configuring via code**
> You can add the following code in the info.plist of the app integrating the SDK:
> ```shell
> <key>NSAppTransportSecurity</key>
> <dict>
> <key>NSExceptionDomains</key>
> <dict>
> 	<key>myqcloud.com</key>
> <dict>
> 		<key>NSIncludesSubdomains</key>
> <true/>
> 		<key>NSTemporaryExceptionAllowsInsecureHTTPLoads</key>
> <true/>
> </dict>
> </dict>
> </dict>
> ```
> 
> Mobile Tencent Analytics (MTA) is also introduced in the SDK. If you want to disable this feature, follow the steps below:
>- Import the header file
> `#import <QCloudCore/MTAConfig.h>`
>- After registering the default cosxml service, add the following code:
>`[TACMTAConfig getInstance].statEnable = NO;`

## Getting started

The following describes how to use the COS iOS SDK to complete basic operations, such as initializing a client, creating a bucket, querying a bucket list, uploading an object, querying an object list, downloading an object, and deleting an object. For more details, please refer to [XML iOS SDK Demo] (https://github.com/tencentyun/qcloud-sdk-ios-samples). For how to use the specific APIs, please refer to the unit test file provided in the demo.

### Prerequisites
You must first apply for the APPID of the COS service on the [Tencent Cloud Console](https://console.cloud.tencent.com/cos5).

<span id="step1"></span>
### Initialization

Before using the SDK features, import some necessary header files and perform initialization.
Import and upload the SDK header files:

```objective-c
QCloudCore.h,    
QCloudCOSXML/QCloudCOSXML.h
```

#### Method prototype

Instantiate QCloudServiceConfiguration object:

```
QCloudServiceConfiguration* configuration = [QCloudServiceConfiguration new];
configuration.appID = @"APPID"//Project ID;
```

Instantiate QCloudCOSXMLService object:

<pre>
+ (QCloudCOSXMLService*) registerDefaultCOSXMLWithConfiguration:(QCloudServiceConfiguration*)configuration;
</pre>

Instantiate QCloudCOSTransferManagerService object:

<pre>
+ (QCloudCOSTransferMangerService*) registerDefaultCOSTransferMangerWithConfiguration:(QCloudServiceConfiguration*)configuration;
</pre>

#### QCloudServiceConfiguration parameters

| Parameter Name | Description | Type | Required |
| -------- | ------------------------ | ---------------------- | ---- |
| appID | Project ID, i.e. APPID. | NSString * | No |
| endpoint | Configures endpoint related information | QCloudCOSXMLEndPoint * | Yes |

#### QCloudCOSXMLEndPoint parameters

| Parameter Name | Description | Type | Required |
| ----------- | ----------------------------------- | ---------- | ---- |
| regionName  | The region of the service | NSString * | Yes |
| serviceName | Domain name. The default is `myqcloud.com`. | NSString * | No |
| useHTTPS | Indicates whether to use the HTTPS service. The default is `No`. | BOOL | No |
| suffix | Supports custom `http://bucketname.suffix` | NSString | No |

#### Sample initialization

The APPID, SecretId and SecretKey in the example below can be obtained from the [COS Console](https://console.cloud.tencent.com/cos5).

>
> 1. QCloudSignatureProvider protocol needs to be implemented for the signatureProvider object of the QCloudServiceConfiguration.
> 2. Before using the SDK, instantiate a default cloud service configuration object QCloudServiceConfiguration, and then instantiate QCloudCOSXMLService and QCloudCOSTransferManagerService objects.  
> 3. If the QCloudServiceConfiguration is changed, you can register a new QCloudCOSTransferManagerService with `registerCOSTransferMangerWithConfiguration:(QCloudServiceConfiguration*)configuration withKey:(NSString*)key`, but only one QCloudCOSTransferManagerService can be set as the default.



[//]: # ".cssg-snippet-objc-global-init"
```objective-c
//AppDelegate.m
// Step 1: Register for the default COS service
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    QCloudServiceConfiguration* configuration = [QCloudServiceConfiguration new];
    configuration.appID = @"1250000000";
    configuration.signatureProvider = self;
    QCloudCOSXMLEndPoint* endpoint = [[QCloudCOSXMLEndPoint alloc] init];
    endpoint.regionName = @ "COS_REGION"; // Service region name, refer to notes for available regions
    configuration.endpoint = endpoint;
    [QCloudCOSXMLService registerDefaultCOSXMLWithConfiguration:configuration];
    [QCloudCOSTransferMangerService registerDefaultCOSTransferMangerWithConfiguration:configuration];
    return YES;
}

// Step 2: Implement the QCloudSignatureProvider protocol
We recommend that the process of implementing the signature is done on the server. For more information, see the "Generating a signature" section below.
```

#### swift sample

[//]: # ".cssg-snippet-swift-global-init"
```swift
//AppDelegate.m
// Step 1: Register for the default COS service

func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
    let config = QCloudServiceConfiguration.init();
    config.signatureProvider = self;
    config.appID = "appId";
    let endpoint = QCloudCOSXMLEndPoint.init();
    endpoint.regionName = "region";
    endpoint.useHTTPS = true;
    config.endpoint = endpoint;
    QCloudCOSXMLService.registerDefaultCOSXML(with: config);
    QCloudCOSTransferMangerService.registerDefaultCOSTransferManger(with: config);
    return true;
}


// Step 2: Implement the QCloudSignatureProvider protocol
We recommend that the process of implementing the signature is done on the server. For more information, see the "Generating a signature" section below.
```

### Creating a bucket

[//]: # ".cssg-snippet-objc-put-bucket"
```objective-c
QCloudPutBucketRequest* request = [QCloudPutBucketRequest new];
request.bucket = @"examplebucket-1250000000"; //additional actions after finishing
[request setFinishBlock:^(id outputObject, NSError* error) {
    // You can get the header information returned by the server from outputObject
}];
[[QCloudCOSXMLService defaultCOSXML] PutBucket:request];
```

#### swift sample

[//]: # ".cssg-snippet-swift-put-bucket"
```swift
let putBucketReq = QCloudPutBucketRequest.init();
putBucketReq.bucket = "examplebucket-1250000000";
putBucketReq.finishBlock = {(result,error) in
    if error != nil {
        print(error!);
    } else {
        print(result!);
    }}
QCloudCOSXMLService.defaultCOSXML().putBucket(putBucketReq);
```

### Querying a bucket list

[//]: # ".cssg-snippet-get-service"
```objective-c
QCloudGetServiceRequest* request = [[QCloudGetServiceRequest alloc] init];
[request setFinishBlock:^(QCloudListAllMyBucketsResult* result, NSError* error) {
    // Get the returned information from `result`
}];
[[QCloudCOSXMLService defaultCOSXML] GetService:request];
```

#### swift sample

[//]: # ".cssg-snippet-swift-get-service"
```swift
let getServiceReq = QCloudGetServiceRequest.init();
getServiceReq.setFinish{(result,error) in
    if result == nil {
        print(error!);
    } else {
        // Get the returned information from `result`
        print(result!);
    }}
QCloudCOSXMLService.defaultCOSXML().getService(getServiceReq);
```

### Uploading an object

This example assumes you have applied for a bucket for your business. All SDK requests have corresponding request classes. When a request is generated, the corresponding attributes are set, and the request is passed to the QCloudCOSTransferMangerService object, the desired operation can be completed. For the request body, enter the local URL of the object to be uploaded (NSURL\* type).    

The API for uploading objects uses a signature for identity verification. A request will automatically be sent to request a signature from the object specified during initialization that follows the QCloudSignatureProvider protocol. For more information on how to generate a signature, see the [Generating a signature](#.E7.94.9F.E6.88.90.E7.AD.BE.E5.90.8D) section below.

>The object corresponding to the URL cannot be changed during upload, otherwise it will cause an error.

#### Samples

[//]: # ".cssg-snippet-objc-transfer-upload-object"
```objective-c
QCloudCOSXMLUploadObjectRequest* put = [QCloudCOSXMLUploadObjectRequest new];
put.object = @"exampleobject";
put.bucket = @"examplebucket-1250000000";
put.body = [@"testFileContent" dataUsingEncoding:NSUTF8StringEncoding];
// Set some upload parameters
put.initMultipleUploadFinishBlock = ^(QCloudInitiateMultipartUploadResult * multipleUploadInitResult,
    QCloudCOSXMLUploadObjectResumeData resumeData) {
    // This block will be called back after the initial multipart upload is complete, so you can get resumeData,
    // and can generate a multipart upload request through resumeData
    QCloudCOSXMLUploadObjectRequest* request = [QCloudCOSXMLUploadObjectRequest
        requestWithRequestData:resumeData];
};
[put setSendProcessBlock:^(int64_t bytesSent, int64_t totalBytesSent,
    int64_t totalBytesExpectedToSend) {
    NSLog(@"upload %lld totalSend %lld aim %lld", bytesSent, totalBytesSent,
        totalBytesExpectedToSend);
}];
[put setFinishBlock:^(QCloudUploadObjectResult *result, NSError* error) {
    // You can get the result from `result`
}];

[[QCloudCOSTransferMangerService defaultCOSTransferManager] UploadObject:put];
// Discard a multipart upload and delete uploaded parts
[put abort:^(id outputObject, NSError *error) {
//
}];

//···When initialization is complete and upload is not complete
NSError* error;
//The following shows how resumeData is generated after the user cancels the upload
QCloudCOSXMLUploadObjectResumeData resumeData = [put cancelByProductingResumeData:&error];
QCloudCOSXMLUploadObjectRequest* request = nil;
if (resumeData) {
    request = [QCloudCOSXMLUploadObjectRequest requestWithRequestData:resumeData];
}
// The request generated for resuming the upload can be uploaded directly
[[QCloudCOSTransferMangerService defaultCOSTransferManager] UploadObject:request];
```

#### swift sample

[//]: # ".cssg-snippet-swift-transfer-upload-object"
```swift
let uploadRequest = QCloudCOSXMLUploadObjectRequest<AnyObject>.init();
let dataBody:NSData? = "wrwrwrwrwrw".data(using: .utf8) as NSData?;
uploadRequest.body = dataBody!;
uploadRequest.bucket = "examplebucket-1250000000";
uploadRequest.object = "exampleobject";
// Set upload parameters
uploadRequest.initMultipleUploadFinishBlock = {(multipleUploadInitResult,resumeData) in
    // This block will be called back after the initial multipart upload is completed, so you can get resumeData and generate a multipart upload request through resumeData
    let resumeUploadRequest = QCloudCOSXMLUploadObjectRequest<AnyObject>.init(request: resumeData as Data?);
}
uploadRequest.sendProcessBlock = {(bytesSent , totalBytesSent , totalBytesExpectedToSend) in
    
}
uploadRequest.setFinish { (result, error) in
    if error != nil{
        print(error!)
    }else{
        // Get the result of the request from `result`
        print(result!);
    }}

QCloudCOSTransferMangerService.defaultCOSTransferManager().uploadObject(uploadRequest);

//···When initialization is complete and upload is not complete
var error:NSError?;
    //The following shows how resumeData is generated after the user cancels the upload
do {
    let resumedData = try uploadRequest.cancel(byProductingResumeData: &error);
        var resumeUploadRequest:QCloudCOSXMLUploadObjectRequest<AnyObject>;
             resumeUploadRequest = QCloudCOSXMLUploadObjectRequest<AnyObject>.init(request: resumedData as Data?);
             // The request generated for resuming the upload can be uploaded directly
    if resumeUploadRequest != nil {
        QCloudCOSTransferMangerService.defaultCOSTransferManager().uploadObject(resumeUploadRequest!);
    }
             
} catch  {
    print("resumeData is blank");
    return;
}
```

#### QCloudCOSXMLUploadObjectRequest parameters

| Parameter Name | Description | Type | Required |
| ----------------------------- | ------------------------------------------------------------ | --------------------- | ---- |
| Object | Object key is the unique identifier of an object in a bucket. For example, if the object's access domain name is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`, the object key would be `doc/picture.jpg`. For more information, see [Object Overview] (https://intl.cloud.tencent.com/document/product/436/13324). | NSString * | Yes |
| bucket | Bucket name in the format &lt;BucketName-APPID>, for example: `examplebucket-1250000000`. The bucket name can be found in the [COS Console](https://console.cloud.tencent.com/cos5/bucket) | NSString* | Yes |
| body | If a file is stored in the disk, you need to enter the path of the file to be uploaded and a NSURL * type variable<br><li>. If a file is stored in memory, you can enter a NSData * type variable that contains the file binary data. | BodyType | Yes |
| storageClass | Storage class of an object | QCloudCOSStorageClass | Yes |
| cacheControl | Cache policy defined in RFC 2616 | NSString * | No |
| contentDisposition | File name defined in RFC 2616 | NSString * | No |
| expect | When expect=@"100-Continue" is used, the request content will not be sent until the receipt of a response from server. | NSString * | No |
| expires | Expiration time defined in RFC 2616 | NSString * | No |
| initMultipleUploadFinishBlock | If the request generates a multipart upload request, after the initialization of the multipart upload, a callback will be performed via the block. The bucket, key, and uploadID of the completed multipart upload and the ResumeData for resuming subsequent failed uploads can be obtained from this callback block. | block | No |
| accessControlList | Defines the ACL attribute of an object. Valid values: private, public-read; Default: private | NSString * | No |
| grantRead | Grants read access in the format: `id="[OwnerUin]"` | NSString * | No |
| grantWrite | Grants write access in the format: `id="[OwnerUin]"`. | NSString * | No |
| grantFullControl | Grants full access in the format: `id="[OwnerUin]"`. | NSString * | No |

### Querying an object list

[//]: # ".cssg-snippet-objc-get-bucket"
```objective-c
QCloudGetBucketRequest* request = [QCloudGetBucketRequest new];
request.bucket = @"examplebucket-1250000000";
request.maxKeys = 1000;

[request setFinishBlock:^(QCloudListBucketResult * result, NSError* error) {
    // result returns specific information
}];

[[QCloudCOSXMLService defaultCOSXML] GetBucket:request];
```

#### swift sample

[//]: # ".cssg-snippet-swift-get-bucket"
```swift
let getBucketReq = QCloudGetBucketRequest.init();
getBucketReq.bucket = "examplebucket-1250000000";
getBucketReq.maxKeys = 1000;
getBucketReq.setFinish { (result, error) in
    if error != nil{
        print(error!);
    }else{
        print( result!.commonPrefixes);
    }}
QCloudCOSXMLService.defaultCOSXML().getBucket(getBucketReq);
```

### Downloading an object

[//]: # ".cssg-snippet-objc-get-object"
```objective-c
QCloudGetObjectRequest* request = [QCloudGetObjectRequest new];
// Set the URL for download. If it has been set, the file is downloaded to the specified path.
// If this parameter is not set, the file will be downloaded to memory and stored in the outputObject of finishBlock
request.downloadingURL = [NSURL URLWithString:QCloudTempFilePathWithExtension(@"downding")];
request.object = @"exampleobject";
request.bucket = @"examplebucket-1250000000";

[request setFinishBlock:^(id outputObject, NSError *error) {
    // You can get the etag or custom header information in the response from outputObject
}];
[request setDownProcessBlock:^(int64_t bytesDownload, int64_t totalBytesDownload,
    int64_t totalBytesExpectedToDownload) {
    // Download progress
}];

[[QCloudCOSXMLService defaultCOSXML] GetObject:request];
```

#### swift sample

[//]: # ".cssg-snippet-swift-get-object"
```swift
let getObject = QCloudGetObjectRequest.init();
getObject.bucket = "examplebucket-1250000000";
getObject.object = "exampleobject";
getObject.downloadingURL = URL.init(string: NSTemporaryDirectory())!.appendingPathComponent(getObject.object);
getObject.finishBlock = {(result,error) in
    if error != nil{
        print(error!);
    }else{
        print(result!);
    }};
getObject.downProcessBlock = {(bytesDownload, totalBytesDownload,  totalBytesExpectedToDownload) in
    print("totalBytesDownload:\(totalBytesDownload) totalBytesExpectedToDownload:\(totalBytesExpectedToDownload)");
}
QCloudCOSXMLService.defaultCOSXML().getObject(getObject);
```

### Deleting an object

[//]: # ".cssg-snippet-objc-delete-object"
```objective-c
QCloudDeleteObjectRequest* deleteObjectRequest = [QCloudDeleteObjectRequest new];
deleteObjectRequest.bucket = @"examplebucket-1250000000";
deleteObjectRequest.object = @"exampleobject";

[deleteObjectRequest setFinishBlock:^(id outputObject, NSError *error) {
    // You can get the etag or custom header information in the response from outputObject
}];

[[QCloudCOSXMLService defaultCOSXML] DeleteObject:deleteObjectRequest];
```

#### swift sample

[//]: # ".cssg-snippet-swift-delete-object"
```swift
let deleteObject = QCloudDeleteObjectRequest.init();
deleteObject.bucket = "examplebucket-1250000000";
deleteObject.object = "exampleobject";
deleteObject.finishBlock = {(result,error)in
    if error != nil{
        print(error!);
    }else{
        print(result!);
    }}
QCloudCOSXMLService.defaultCOSXML().deleteObject(deleteObject);
```

## Generating a signature

Any request in the SDK requires a signature to verify the user identity and ensure access security. When the signature is incorrect, most COS services are inaccessible and a 403 error is returned. A signature can be generated in the SDK. For each request, the signature can be requested from the signatureProvider object in the QCloudServiceConfiguration object. The object for generating signatures can be assigned to the signatureProvider at the beginning, and should follow the QCloudSignatureProvider protocol and implement the signature generation method:

```objective-c
- (void) signatureWithFields:(QCloudSignatureFields* )fileds    
					request:(QCloudBizHTTPRequest* )request    
					urlRequest:(NSURLRequest* )urlRequst    
					compelete:(QCloudHTTPAuthentationContinueBlock)continueBlock
```

### Connecting to CAM for temporary signatures (recommended)

Although the API for generating a signature with permanent SecretId and SecretKey is provided locally, please note that storing the permanent SecretId and SecretKey locally is very risky and may cause unnecessary losses due to leakage. Therefore, we recommend that you implement the signature on the server to ensure security.

>We strongly recommend you use the server return time as the start time of the signature, to avoid signature errors caused by a deviation between your mobile phone's local time and standard time.

We recommended you connect to Tencent Cloud's CAM (Cloud Access Manager) within your own signature server to implement the signature process.

![](https://main.qcloudimg.com/raw/d25267927fcaca9d9e0696f1aba872a5.png)    

For more information on how to set up a signature server to connect to CAM, see [Practice of Direct Upload for Mobile Apps](https://intl.cloud.tencent.com/document/product/436/30618).

After the signature server is connected to CAM, if a client requests a signature from the server, the server will request temporary credentials from CAM and return it to the client. 
CAM generates a signature by generating a temporary SecretId, SecretKey, and Token based on your permanent SecretId and SecretKey. In this way, the system is able to maximize security. After receiving the temporary key information, the terminal builds a QCloudCredential object using the keys; it then generates a QCloudAuthenticationCreator via the QCloudCredentail object, and then, using this creator, it generates a QCloudSignature object containing the signing information as shown below:

[//]: # ".cssg-snippet-objc-global-init-signature-sts"
```objective-c
- (void) signatureWithFields:(QCloudSignatureFields*)fileds
                     request:(QCloudBizHTTPRequest*)request
                  urlRequest:(NSMutableURLRequest*)urlRequst
                   compelete:(QCloudHTTPAuthentationContinueBlock)continueBlock
{
    // *Request temporary Secret ID, Secret Key and Token from signature server
    QCloudCredential* credential = [QCloudCredential new];
    credential.secretID = @"COS_SECRETID";
    credential.secretKey = @"COS_SECRETKEY";
    credential.token = @"COS_TOKEN";
    /*We strongly recommend you use the server return time as the start time of the signature, to avoid signature errors caused by a deviation between your mobile phone's local time and standard time*/
    credential.startDate = [[[NSDateFormatter alloc] init] dateFromString:@"startTime"]; // unit in seconds
    credential.experationDate  = [[[NSDateFormatter alloc] init] dateFromString:@"expiredTime"];
    QCloudAuthentationV5Creator* creator = [[QCloudAuthentationV5Creator alloc] initWithCredential:credential];
    QCloudSignature* signature =  [creator signatureForData:urlRequst];
    continueBlock(signature, nil);
}
```

#### swift sample

[//]: # ".cssg-snippet-swift-global-init-signature-sts"
```swift

func signature(with fileds: QCloudSignatureFields!, request: QCloudBizHTTPRequest!, urlRequest urlRequst: NSMutableURLRequest!, compelete continueBlock: QCloudHTTPAuthentationContinueBlock!) {
    let cre = QCloudCredential.init();
    cre.secretID = "COS_SECRETID";
    cre.secretKey = "COS_SECRETKEY";
    cre.token = "COS_TOKEN";
    /*We strongly recommend you use the server return time as the start time of the signature, to avoid signature errors caused by a deviation between your mobile phone's local time and standard time*/
    cre.startDate = DateFormatter().date(from: "startTime"); // unit in seconds
    cre.experationDate = DateFormatter().date(from: "expiredTime");
    let auth = QCloudAuthentationV5Creator.init(credential: cre);
    let signature = auth?.signature(forData: urlRequst)
    continueBlock(signature,nil);
}
```

### Generating a signature using permanent keys at the terminal (not recommended)

>We do not recommend you use permanent keys to generate a signature at the terminal. This may cause data leakage.

Sample code is as follows:

[//]: # ".cssg-snippet-objc-global-init-signature"
```objective-c
- (void) signatureWithFields:(QCloudSignatureFields*)fileds
                     request:(QCloudBizHTTPRequest*)request
                  urlRequest:(NSMutableURLRequest*)urlRequst
                   compelete:(QCloudHTTPAuthentationContinueBlock)continueBlock
{
    
    QCloudCredential* credential = [QCloudCredential new];
    credential.secretID = @"COS_SECRETID";
    credential.secretKey = @"COS_SECRETKEY";
    QCloudAuthentationV5Creator* creator = [[QCloudAuthentationV5Creator alloc] initWithCredential:credential];
    QCloudSignature* signature =  [creator signatureForData:urlRequst];
    continueBlock(signature, nil);
}
```

#### swift sample

[//]: # ".cssg-snippet-swift-global-init-signature"
```swift

func signature(with fileds: QCloudSignatureFields!, request: QCloudBizHTTPRequest!, urlRequest urlRequst: NSMutableURLRequest!, compelete continueBlock: QCloudHTTPAuthentationContinueBlock!) {
    let cre = QCloudCredential.init();
    cre.secretID = "COS_SECRETID";
    cre.secretKey = "COS_SECRETKEY";
    let auth = QCloudAuthentationV5Creator.init(credential: cre);
    let signature = auth?.signature(forData: urlRequst)
    continueBlock(signature,nil);
}
```

### Managing asynchronous signatures using a scaffolding tool

At this point, you are now able to generate a signature and use the APIs in the SDK. For your convenience, a scaffolding tool is provided to make it easier for you to implement a temporary signature and obtain required information such as the `tempSecretKey` from the server. You can either generate a signature by following the code above, or obtain a temporary signature through our scaffolding tool `QCloudCredentailFenceQueue`.
`QCloudCredentailFenceQueue` provides a fencing mechanism, which means that if you obtain the signature using `QCloudCredentailFenceQueue`, any request for a signature will not be performed until the signature process is completed. This can eliminate the need to manage the asynchronous processes.    
To use QCloudCredentailFenceQueue, you need to first create an instance.

```objective-c
//AppDelegate.m
//AppDelegate must follow QCloudCredentailFenceQueueDelegate protocol
//
- (BOOL)application:(UIApplication * )application didFinishLaunchingWithOptions:(NSDictionary * )launchOptions {
    // init step
    self.credentialFenceQueue = [QCloudCredentailFenceQueue new];
    self.credentialFenceQueue.delegate = self;
    return YES;
}

```

Next, to call the QCloudCredentailFenceQueue class, you must follow QCloudCredentailFenceQueueDelegate and implement the method defined in the protocol:

```objective-c
- (void) fenceQueue:(QCloudCredentailFenceQueue * )queue requestCreatorWithContinue:(QCloudCredentailFenceQueueContinue)continueBlock
```

When you obtain the signature using `QCloudCredentailFenceQueue`, all the requests in the SDK that need signatures will not be performed until the parameters required for the signature are obtained via the method defined by the protocol and a valid signature is generated. See the example below:

[//]: # ".cssg-snippet-objc-global-init-fence-queue"
```objective-c
//AppDelegate.m

// Define a member variable @property (nonatomic) QCloudCredentailFenceQueue* credentialFenceQueue;

- (void) fenceQueue:(QCloudCredentailFenceQueue * )queue requestCreatorWithContinue:(QCloudCredentailFenceQueueContinue)continueBlock
{
    QCloudCredential* credential = [QCloudCredential new];
    // You can synchronize the process to obtain from the server the secretID, secretKey, expirationDate and token parameters needed for the temporary signature.
    credential.secretID = @"COS_SECRETID";
    credential.secretKey = @"COS_SECRETKEY";
    /*We strongly recommend you use the server return time as the start time of the signature, to avoid signature errors caused by a deviation between your mobile phone's local time and standard time*/
    credential.startDate = [[[NSDateFormatter alloc] init] dateFromString:@"startTime"]; // unit in seconds
    credential.experationDate = [[[NSDateFormatter alloc] init] dateFromString:@"expiredTime"];
    credential.token = @"COS_TOKEN";
    QCloudAuthentationV5Creator* creator = [[QCloudAuthentationV5Creator alloc]
        initWithCredential:credential];
    continueBlock(creator, nil);
}

- (void) signatureWithFields:(QCloudSignatureFields*)fileds
                     request:(QCloudBizHTTPRequest*)request
                  urlRequest:(NSMutableURLRequest*)urlRequst
                   compelete:(QCloudHTTPAuthentationContinueBlock)continueBlock
{
    [self.credentialFenceQueue performAction:^(QCloudAuthentationCreator *creator, NSError *error) {
        if (error) {
            continueBlock(nil, error);
        } else {
            QCloudSignature* signature =  [creator signatureForData:urlRequst];
            continueBlock(signature, nil);
        }
    }];
}
```

#### swift sample

[//]: # ".cssg-snippet-swift-global-init-fence-queue"
```swift
//AppDelegate.m

// Define a member variable @property (nonatomic) QCloudCredentailFenceQueue* credentialFenceQueue;

func fenceQueue(_ queue: QCloudCredentailFenceQueue!, requestCreatorWithContinue continueBlock: QCloudCredentailFenceQueueContinue!) {
    let cre = QCloudCredential.init();
    // You can synchronize the process to obtain from the server the secretID, secretKey, expirationDate and token parameters needed for the temporary signature.
    cre.secretID = "COS_SECRETID";
    cre.secretKey = "COS_SECRETKEY";
    cre.token = "COS_TOKEN";
    /*We strongly recommend you use the server return time as the start time of the signature, to avoid signature errors caused by a deviation between your mobile phone's local time and standard time*/
    cre.startDate = DateFormatter().date(from: "startTime"); // unit in seconds
    cre.experationDate = DateFormatter().date(from: "expiredTime");
    let auth = QCloudAuthentationV5Creator.init(credential: cre);
    continueBlock(auth,nil);
}

func signature(with fileds: QCloudSignatureFields!, request: QCloudBizHTTPRequest!, urlRequest urlRequst: NSMutableURLRequest!, compelete continueBlock: QCloudHTTPAuthentationContinueBlock!) {
    self.credentialFenceQueue?.performAction({ (creator, error) in
        if error != nil {
            continueBlock(nil,error!);
        }else{
            let signature = creator?.signature(forData: urlRequst);
            continueBlock(signature,nil);
        }
    })
}
```

At this point, you are able to generate a temporary signature with the scaffolding tool provided. You can also implement the signature process by yourself.

## User guide for the simplified SDK

A simplified SDK is provided for users who only use upload and download features and who can only install a small size SDK. The simplified SDK is half the size of the complete SDK.  

The simplified SDK is implemented via the Subspec of Cocoapods, so it can only be integrated by using Cocoapods. To use the simplified SDK, add the following content to Podfile:

```
pod 'QCloudCOSXML/Transfer'
```

>For Mobile Line users, the simplified SDK is available only when TACStorage is **disabled** and the official source of [Cocoapods](https://github.com/CocoaPods/Specs) is placed **in front of all sources**. It is recommended to place it in the first line of the Podfile. Other users can ignore this note.

The simplified SDK does not use the header file QCloudCOSXML.h. Import the following header files at the time of initialization instead:

```
#import <QCloudCOSXML/QCloudCOSXMLTransfer.h>
#import <QCloudCore/QCloudCore.h>
```

The initialization and APIs for uploading and downloading the simplified SDK are the same as those for the complete SDK.
