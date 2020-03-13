## Download and Installation

### Related resources

Download iOS SDK resources of COS service from: [XML iOS SDK](https://github.com/tencentyun/qcloud-sdk-ios.git).   
- You can download the packaged SDK in Framework format by selecting the desired version from [Release](https://github.com/tencentyun/qcloud-sdk-ios/releases).
- For more examples, see demo in [XML iOS SDK Demo](https://github.com/tencentyun/qcloud-sdk-ios-samples.git).
- For update log of COS XML version, refer to [XML iOS SDK ChangeLog](https://github.com/tencentyun/qcloud-sdk-ios/blob/master/CHANGELOG.md).

### Environment Requirements

SDK supports iOS 8.0 or above.
2. The mobile phone needs to be connected to the Internet (through GPRS, 3G, 4G, or Wi-Fi).
4. Get the SecretId and SecretKey on the [API Key Management](https://console.cloud.tencent.com/capi) page in the CAM Console. Get the APPID in the [Account Center](https://console.cloud.tencent.com/developer).

>- For definitions of SecretId, SecretKey, Bucket and other terms, see [COS Glossary](https://cloud.tencent.com/document/product/436/7751#.E6.9C.AF.E8.AF.AD.E4.BF.A1.E6.81.AF).

### Installing SDK

#### Importing the SDK

You can integrate SDK via cocoapods or by downloading packaged dynamic libraries. We recommend you use cocoapods for import.

-**Importing using Cocoapods (recommended)**  
  In Podfile, use:
```shell
pod 'QCloudCOSXML'
```

-**Importing using the packaged dynamic library (manual integration)**  
  Drag **QCloudCOSXML.framework, QCloudCore.framework and libmtasdk.a** to your project, as shown below:
  ![](https://main.qcloudimg.com/raw/ce990d8871293daec0aa434f28b152e6.png)  
  And add the following dependent libraries:
 > - CoreTelephony
 > - Foundation
 > - SystemConfiguration
 > - libc++.tbd

#### Configure the project

Set up "Other Linker Flags" in "Build Settings" and add the parameter:

```shell
-ObjC
-all_load
```

See the figure below:
![](https://main.qcloudimg.com/raw/125218fad3f4781cae8f992d9a152057.png)

>
>Tencent Cloud COS XML iOS SDK uses HTTP protocol. To run the SDK on iOS, enable transfer over HTTP.
> You can enable transfer over HTTP in the following two ways:
>- **Configuring manually**
> Add "App Transport Security Settings" to the "info.plist" file of the project, and then add "Allow Arbitrary Loads" under "App Transport Security Settings", and set its type to "Boolean", and value to "YES".
>- **Configuring via code**
> You can add the following code in the info.plist of the App integrating SDK:
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
> `[TACMTAConfig getInstance].statEnable = NO;`

## Getting Started

The following describes how to use COS iOS SDK to complete a basic operation, such as initializing a client, creating a bucket, querying the bucket list, uploading an object, querying an object list, downloading an object, and deleting an object. For more details, please refer to [XML iOS SDK Demo](https://github.com/tencentyun/qcloud-sdk-ios-samples). For how to use the specific API, refer to the unit test file provided in the Demo.

### Prerequisites
> !You must apply for the APPID of COS service on the [Tencent Cloud Console](https://console.cloud.tencent.com/cos4/secret) before proceeding with this step.

<span id="step1"></span>
### Initialization

Before using the features of SDK, import some necessary header files and perform initialization.
Import and upload the header files for SDK:

```objective-c
QCloudCore.h,    
QCloudCOSXML/QCloudCOSXML.h
```

#### Method Prototype

Instantiate QCloudServiceConfiguration object:

```
QCloudServiceConfiguration* configuration = [QCloudServiceConfiguration new];
configuration.appID = @""//Project ID;
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
| serviceName | Domain name. Default is myqcloud.com. | NSString * | No |
| useHTTPS | Indicates whether to use the HTTPS service. Default is No. | BOOL | No |
| suffix | Supports custom http://bucketname.suffix | NSString | No |

#### Initialization Example

The appID, SecretId and SecretKey in the example below can be obtained from the [COS v5 Console](https://console.cloud.tencent.com/cos5).

>
> !QCloudSignatureProvider protocol needs to be implemented for the signatureProvider object of QCloudServiceConfiguration.
> 2. Before using the SDK, instantiate a default cloud service configuration object QCloudServiceConfiguration, and then instantiate QCloudCOSXMLService and QCloudCOSTransferManagerService objects.  
> 3. If QCloudServiceConfiguration is changed, you can register a new QCloudCOSTransferManagerService with `registerCOSTransferMangerWithConfiguration:(QCloudServiceConfiguration*)configuration withKey:(NSString*)key`, but only one QCloudCOSTransferManagerService can be set as default.



[//]: # (.cssg-snippet-objc-global-init)
```objective-c
//AppDelegate.m
// Step 1: Register for the default COS service
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
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
The process of implementing signature. We recommend you implement this process on the server. For more information, see the "Generating a signature" section below.
```

#### swift Example

[//]: # (.cssg-snippet-swift-global-init)
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
The process of implementing signature. We recommend you implement this process on the server. For more information, see the "Generating a signature" section below.
```

### Creating a bucket

[//]: # (.cssg-snippet-objc-put-bucket)
```objective-c
QCloudPutBucketRequest* request = [QCloudPutBucketRequest new];
request.bucket = @"examplebucket-1250000000"; //additional actions after finishing
[request setFinishBlock:^(id outputObject, NSError* error) {
    // You can get the header information returned by the server from outputObject
}];
[[QCloudCOSXMLService defaultCOSXML] PutBucketVersioning:request];
```

#### swift Example

[//]: # (.cssg-snippet-swift-put-bucket)
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

### Querying the bucket list

[//]: # (.cssg-snippet-get-service)
```objective-c
QCloudGetServiceRequest* request = [[QCloudGetServiceRequest alloc] init];
[request setFinishBlock:^(QCloudListAllMyBucketsResult* result, NSError* error) {
    // Get the returned information from result
}];
[[QCloudCOSXMLService defaultCOSXML] GetObject:request];
```

#### swift Example

[//]: # (.cssg-snippet-swift-get-service)
```swift
let getServiceReq = QCloudGetServiceRequest.init();
getServiceReq.setFinish{(result,error) in
    if result == nil {
        print(error!);
    } else {
        // Get the returned information from result
        print(result!);
    }}
QCloudCOSXMLService.defaultCOSXML().getService(getServiceReq);
```

### Uploading an object

The example assumes you have applied for a Bucket for your business. In fact, all SDK requests have their Request classes. When a request is generated and the relevant attributes are set, pass the request to the QCloudCOSTransferMangerService object to complete the desired operation. For the body part of the request, enter the local URL of the file to be uploaded (NSURL\* type).    

The API for uploading files uses a signature for authentication. A request sent automatically requests a signature from the object specified during initialization that follows the QCloudSignatureProvider protocol. For more information on how to generate a signature, see the [Generating a Signature](#.E7.94.9F.E6.88.90.E7.AD.BE.E5.90.8D) section below.

> !The object corresponding to the URL cannot be changed during upload, otherwise it will cause an error.

#### Samples

[//]: # (.cssg-snippet-objc-transfer-upload-object)
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
    // You can get the result from result
}];

[[QCloudCOSTransferMangerService defaultCOSTransferManager] UploadObject:put];
// Discard a multipart upload and delete uploaded parts
[put abort:^(id outputObject, NSError *error) {
//
}];

//···When initialization is completed and upload is not completed
NSError* error;
//The following shows how resumeData is generated after the user cancels the upload
QCloudCOSXMLUploadObjectResumeData resumeData = [put cancelByProductingResumeData:&error];
QCloudCOSXMLUploadObjectRequest* request = nil;
if (resumeData) {
    request = [QCloudCOSXMLUploadObjectRequest requestWithRequestData:resumeData];
}
//The generated request for resuming upload can be directly uploaded
[[QCloudCOSTransferMangerService defaultCOSTransferManager] UploadObject:request];
```

#### swift Example

[//]: # (.cssg-snippet-swift-transfer-upload-object)
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
        // Get the result of the request from result
        print(result!);
    }}

QCloudCOSTransferMangerService.defaultCOSTransferManager().uploadObject(uploadRequest);

//···When initialization is completed and upload is not completed
var error:NSError?;
    //The following shows how resumeData is generated after the user cancels the upload
do {
    let resumedData = try uploadRequest.cancel(byProductingResumeData: &error);
        var resumeUploadRequest:QCloudCOSXMLUploadObjectRequest<AnyObject>;
             resumeUploadRequest = QCloudCOSXMLUploadObjectRequest<AnyObject>.init(request: resumedData as Data?);
             //The generated request for resuming upload can be directly uploaded
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
| Object | ObjectKey is the unique identifier of an object in a bucket. For example, in the object's access domain name "bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg", the ObjectKey is "doc1/pic1.jpg". For more information, see [Object Description](https://cloud.tencent.com/document/product/436/13324). | NSString * | Yes |
| bucket | Bucket name, which can be found in the [COS V5 Console](https://console.cloud.tencent.com/cos5/bucket), with a format of &lt;bucketName&gt;-&lt;APPID&gt;, such as testBucket-1253653367. | NSString * | Yes |
| body | The path of the file to be uploaded. Enter a variable of NSURL * type. | BodyType | Yes |
| storageClass | Storage class of an object | QCloudCOSStorageClass | Yes |
| cacheControl | Cache policy defined in RFC 2616 | NSString * | No |
| contentDisposition | File name defined in RFC 2616 | NSString * | No |
| expect | When expect=@"100-Continue" is used, the request content will not be sent until the receipt of response from server. | NSString * | No |
| expires | Expiration time defined in RFC 2616 | NSString * | No |
| initMultipleUploadFinishBlock | If the request generates a multipart upload request, after the initialization of multipart upload, a callback is performed via the block. The bucket, key, and uploadID after the completion of multipart upload, and ResumeData for resuming subsequent failed upload can be obtained from this callback block. | block | No |
| accessControlList | Defines the ACL attribute of an object. Valid values: private, public-read-write, public-read; Default: private | NSString * | No |
| GrantRead | Grants the grantee Read access in the format of `id="[OwnerUin]"` | String | No |
| grantWrite | Grants write permission to the authorized user. The format is the same as above. | NSString * | No |
| grantFullControl | Grants read and write permissions to the authorized user. The format is the same as above. | NSString * | No |

### Querying the object list

[//]: # (.cssg-snippet-objc-get-bucket)
```objective-c
QCloudGetBucketRequest* request = [QCloudGetBucketRequest new];
request.bucket = @"examplebucket-1250000000";
request.maxKeys = 1000;

[request setFinishBlock:^(QCloudListBucketResult * result, NSError* error) {
    // result returns specific information
}];

[[QCloudCOSXMLService defaultCOSXML] GetBucket:request];
```

#### swift Example

[//]: # (.cssg-snippet-swift-get-bucket)
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

[//]: # (.cssg-snippet-objc-get-object)
```objective-c
QCloudGetObjectRequest* request = [QCloudGetObjectRequest new];
// Set the URL for download. If it has been set, the file is downloaded to the specified path.
// If this parameter is not set, the file will be downloaded to memory and stored in the outputObject of finishBlock
request.downloadingURL = [NSURL URLWithString:QCloudTempFilePathWithExtension(@"downding")];
request.object = @"exampleobject";
request.bucket = @"examplebucket-1250000000";

[request setFinishBlock:^(id outputObject, NSError *error) {
    // You can get etag or custom header information in response from outputObject
}];
[request setDownProcessBlock:^(int64_t bytesDownload, int64_t totalBytesDownload,
    int64_t totalBytesExpectedToDownload) {
    // Download Progress
}];

[[QCloudCOSXMLService defaultCOSXML] GetObject:request];
```

#### swift Example

[//]: # (.cssg-snippet-swift-get-object)
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

[//]: # (.cssg-snippet-objc-delete-object)
```objective-c
QCloudDeleteObjectRequest* deleteObjectRequest = [QCloudDeleteObjectRequest new];
deleteObjectRequest.bucket = @"examplebucket-1250000000";
deleteObjectRequest.object = @"exampleobject";

[deleteObjectRequest setFinishBlock:^(id outputObject, NSError *error) {
    // You can get etag or custom header information in response from outputObject
}];

[[QCloudCOSXMLService defaultCOSXML] DeleteObject:deleteObjectRequest];
```

#### swift Example

[//]: # (.cssg-snippet-swift-delete-object)
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

### Connecting to CAM system for temporary signature (recommended)

Although the API for generating a signature with permanent SecretId and SecretKey is provided locally, note that storing the permanent SecretId and SecretKey locally is very risky and may cause unnecessary losses due to leakage. Therefore, it is recommended to implement the signature on the server to ensure security.

>We strongly recommend you use the server return time as the start time of the signature, to avoid incorrect signature caused by deviation of mobile phone's local time from the standard time.

We recommended you connect to Tencent Cloud's CAM (Cloud Access Manager) within your own signature server to implement the signature process.

![](https://main.qcloudimg.com/raw/d25267927fcaca9d9e0696f1aba872a5.png)    

For more information on how to set up a signature server to connect to CAM system, see [Practice of Direct Transfer for Mobile Apps](/document/product/436/9068).

After the signature server is connected to the CAM system, if the client requests a signature from the server, the server requests a temporary certificate from the CAM system and returns it to the client.
After the signature server is connected to the CAM system, if the client requests a signature from the server, the server requests a temporary certificate from the CAM system and returns it to the client. The CAM system generates temporary Secret ID, Secret Key and Token to generate a signature based on your permanent SecretId and SecretKey. By this way, the security is maximized. After receiving the information of these temporary keys, the terminal builds a QCloudCredential object using the keys, generates the QCloudAuthenticationCreator via the QCloudCredentail object, and then generates a QCloudSignature object containing the signature information with this Creator. The example below shows the steps.

[//]: # (.cssg-snippet-objc-global-init-signature-sts)
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
    /*We strongly recommend you use the server return time as the start time of the signature, to avoid incorrect signature caused by deviation of mobile phone's local time from the standard time*/
    credential.startDate = [[[NSDateFormatter alloc] init] dateFromString:@"startTime"]; // unit in seconds
    credential.experationDate  = [[[NSDateFormatter alloc] init] dateFromString:@"expiredTime"];
    QCloudAuthentationV5Creator* creator = [[QCloudAuthentationV5Creator alloc] initWithCredential:credential];
    QCloudSignature* signature =  [creator signatureForData:urlRequst];
    continueBlock(signature, nil);
}
```

#### swift Example

[//]: # (.cssg-snippet-swift-global-init-signature-sts)
```swift

func signature(with fileds: QCloudSignatureFields!, request: QCloudBizHTTPRequest!, urlRequest urlRequst: NSMutableURLRequest!, compelete continueBlock: QCloudHTTPAuthentationContinueBlock!) {
    let cre = QCloudCredential.init();
    cre.secretID = "COS_SECRETID";
    cre.secretKey = "COS_SECRETKEY";
    cre.token = "COS_TOKEN";
    /*We strongly recommend you use the server return time as the start time of the signature, to avoid incorrect signature caused by deviation of mobile phone's local time from the standard time*/
    cre.startDate = DateFormatter().date(from: "startTime"); // unit in seconds
    cre.experationDate = DateFormatter().date(from: "expiredTime");
    let auth = QCloudAuthentationV5Creator.init(credential: cre);
    let signature = auth?.signature(forData: urlRequst)
    continueBlock(signature,nil);
}
```

### Generating a signature using the permanent keys at the terminal (not recommended)

>! We do not recommend you use permanent keys to generate a signature at the terminal. This may cause data leakage.

Sample code is as follows:

[//]: # (.cssg-snippet-objc-global-init-signature)
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

#### swift Example

[//]: # (.cssg-snippet-swift-global-init-signature)
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

### Managing asynchronous signature using a scaffolding tool

Now you can generate a signature and use the APIs in the SDK. Moreover, a scaffolding tool is provided to make it easier for you to implement a temporary signature and obtain the information necessary for the temporary signature such as tempSecretKey from the server. You can either generate a signature by following the above code, or obtain a temporary signature with our scaffolding tool QCloudCredentailFenceQueue. It provides a fencing mechanism, which means if you obtain the signature using QCloudCredentailFenceQueue, any request for a signature will not be performed until the signature process is completed. This can eliminate the need to manage the asynchronous process.
It provides a fencing mechanism, which means that if you obtain the signature using QCloudCredentailFenceQueue, any request for a signature will not be performed until the signature process is completed. This can eliminate the need to manage the asynchronous process.   
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

When you obtain the signature using QCloudCredentailFenceQueue, all the requests in the SDK that need signatures will not be performed until the parameters required for the signature are obtained via the method defined by the protocol and a valid signature is generated. See the example below:

[//]: # (.cssg-snippet-objc-global-init-fence-queue)
```objective-c
//AppDelegate.m

// Define a member variable @property (nonatomic) QCloudCredentailFenceQueue* credentialFenceQueue;

- (void) fenceQueue:(QCloudCredentailFenceQueue * )queue requestCreatorWithContinue:(QCloudCredentailFenceQueueContinue)continueBlock
{
    QCloudCredential* credential = [QCloudCredential new];
    // You can synchronize the process to obtain from the server the secretID, secretKey, expirationDate and token parameters needed for the temporary signature.
    credential.secretID = @"COS_SECRETID";
    credential.secretKey = @"COS_SECRETKEY";
    /*We strongly recommend you use the server return time as the start time of the signature, to avoid incorrect signature caused by deviation of mobile phone's local time from the standard time*/
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

#### swift Example

[//]: # (.cssg-snippet-swift-global-init-fence-queue)
```swift
//AppDelegate.m

// Define a member variable @property (nonatomic) QCloudCredentailFenceQueue* credentialFenceQueue;

func fenceQueue(_ queue: QCloudCredentailFenceQueue!, requestCreatorWithContinue continueBlock: QCloudCredentailFenceQueueContinue!) {
    let cre = QCloudCredential.init();
    // You can synchronize the process to obtain from the server the secretID, secretKey, expirationDate and token parameters needed for the temporary signature.
    cre.secretID = "COS_SECRETID";
    cre.secretKey = "COS_SECRETKEY";
    cre.token = "COS_TOKEN";
    /*We strongly recommend you use the server return time as the start time of the signature, to avoid incorrect signature caused by deviation of mobile phone's local time from the standard time*/
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

At this point, you can generate a temporary signature with the scaffolding tool we provide. You can also implement the signature process by yourself.

## User guide on the simplified SDK

A simplified SDK is provided for users who only use upload and download features and who can only install a small size SDK. The simplified SDK is half of the complete SDK in terms of size.  

The simplified SDK is implemented via Subspec of Cocoapods, so it can only be integrated by using Cocoapods. To use the simplified SDK, add the following content to Podfile:

```
pod 'QCloudCOSXML/Transfer'
```

> !For Mobile Line users, the simplified SDK is available only when TACStorage is **disabled** and the official source of [Cocoapods](https://github.com/CocoaPods/Specs) is placed **in front of all sources**. It is recommended to place it in the first line in Podfile. Other users can ignore this note.

The simplified SDK does not have the header file QCloudCOSXML.h. Import the following header file at the time of initialization:

```
#import <QCloudCOSXML/QCloudCOSXMLTransfer.h>
#import <QCloudCore/QCloudCore.h>
```

The initialization and APIs for upload and download of the simplified SDK are the same with those of the complete SDK.
