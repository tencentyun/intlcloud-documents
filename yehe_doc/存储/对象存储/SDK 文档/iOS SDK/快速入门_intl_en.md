## Download and Installation

### Relevant resources

- Download the COS iOS SDK source code [here](https://github.com/tencentyun/qcloud-sdk-ios.git).   
- You can download the packaged SDK in Framework format by selecting the desired version from [Releases](https://github.com/tencentyun/qcloud-sdk-ios/releases).
- Find the quick SDK download link [here](https://cos-sdk-archive-1253960454.file.myqcloud.com/qcloud-sdk-ios/latest/qcloud-sdk-ios.zip).
- For more examples, see [here](https://github.com/tencentyun/qcloud-sdk-ios-samples.git).
- For the COS XML version change log, see [here](https://github.com/tencentyun/qcloud-sdk-ios/blob/master/CHANGELOG.md).

### Environmental dependency

- This SDK supports iOS 8.0 or above.
- Your mobile phone must be connected to a network (GPRS, 3G, 4G, Wi-Fi, etc.)
- Log into the CAM Console and get your `SecretId` and `SecretKey` from the [Access Key](https://console.cloud.tencent.com/capi) page and get your APPID from the [Account Center](https://console.cloud.tencent.com/developer).

> ?For the definitions of parameters such as `SecretID`, `SecretKey`, and `Bucket`, see the [COS Glossary](https://intl.cloud.tencent.com/document/product/436/7751).

### Installing SDK

#### Importing the SDK

You can integrate the SDK via `cocoapods` or by downloading packaged static libraries. We recommend you use `cocoapods` for import.

- **Importing using cocoapods (recommended)**  
  In Podfile, use:
```shell
pod 'QCloudCOSXML'
```

- **Importing using a packaged static library (manual integration)**  
  Drag **QCloudCOSXML.framework, QCloudCore.framework and libmtasdk.a** to your project, as shown below:
  ![](https://main.qcloudimg.com/raw/ce990d8871293daec0aa434f28b152e6.png)  
  And add the following dependent libraries:
 - CoreTelephony
 - Foundation
 - SystemConfiguration
 - libc++.tbd

#### Configuring the project

Set up "Other Linker Flags" in "Build Settings" and add these parameters:

```shell
-ObjC
-all_load
```

This is shown in the following figure:
![](https://main.qcloudimg.com/raw/125218fad3f4781cae8f992d9a152057.png)

> !
>The Tencent Cloud COS XML iOS SDK uses HTTP protocol. To run the SDK on iOS, you need to enable transfer over HTTP.
> You can enable transfer over HTTP in the following two ways:
> - **Configuring manually**
> Add "App Transport Security Settings" to the "info.plist" file of the project, and then add "Allow Arbitrary Loads" under "App Transport Security Settings", and set its type to "Boolean" and value to "YES".
> - **Configuring via code**
> You can add the following code in the info.plist of the app integrating the SDK:
> ```shell
> <key>NSAppTransportSecurity</key>
> <dict>
> <key>NSExceptionDomains</key>
> <dict>
> 	<key>myqcloud.com</key>
> <dict>
> 	<key>NSIncludesSubdomains</key>
> <true/>
> 	<key>NSTemporaryExceptionAllowsInsecureHTTPLoads</key>
> <true/>
> </dict>
> </dict>
> </dict>
> ```
> 
> Mobile Tencent Analytics (MTA) is also introduced in the SDK. If you want to disable this feature, follow the steps below:
> - Import the header file
> `#import <QCloudCore/MTAConfig.h>`
> - After registering the default cosxml service, add the following code:
>`[TACMTAConfig getInstance].statEnable = NO;`

## Getting Started

The following describes how to use the COS iOS SDK to complete basic operations, such as initializing a client, creating a bucket, querying a bucket list, uploading an object, querying an object list, downloading an object, and deleting an object. For more details, please refer to the [XML iOS SDK Demo](https://github.com/tencentyun/qcloud-sdk-ios-samples). For how to use the specific APIs, please refer to the unit test file provided in the demo.

#### Prerequisites
You must first apply for the APPID of the COS service on the [Tencent Cloud Console](https://console.cloud.tencent.com/cos5).

<span id="step1"></span>
### Initialization

Before using the SDK features, you need to import certain necessary header files and perform the initialization process.
Import and upload the SDK header files:

```objective-c
QCloudCore.h,    
QCloudCOSXML/QCloudCOSXML.h
```

#### Method prototype

Instantiate QCloudServiceConfiguration object:

```
QCloudServiceConfiguration* configuration = [QCloudServiceConfiguration new];
configuration.appID = @"APPID"  //APPID of your Tencent Cloud account;
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

| Parameter Name | Description |Type | Required |
| -------- | ------------------------ | ---------------------- | ---- |
| appID    | APPID of your Tencent Cloud account; an APPID is a unique user-level resource identifier used to access COS and can be obtained from the [API Key Management](https://console.cloud.tencent.com/capi) page on the console.      | NSString *             | No   |
| endpoint | Configures endpoint related information | QCloudCOSXMLEndPoint * | Yes |

#### QCloudCOSXMLEndPoint parameters

| Parameter Name | Description | Type | Required |
| ----------- | ----------------------------------- | ---------- | ---- |
| regionName  | The service region | NSString * | Yes |
| serviceName | Endpoint. The default endpoint is `myqcloud.com`. | NSString * | No |
| useHTTPS | Indicates whether to use HTTPS services. The default is `No`. | BOOL | No |
| suffix | Supports custom suffixes, e.g. `http://bucketname.suffix` | NSString | No |

#### Sample initialization

The APPID, SecretId and SecretKey in the example below can be obtained from the [COS Console](https://console.cloud.tencent.com/cos5).

> !
> 1. QCloudSignatureProvider protocol needs to be implemented for the signatureProvider object of the QCloudServiceConfiguration.
> 2. Before using the SDK, instantiate a default cloud service configuration object QCloudServiceConfiguration, and then instantiate the QCloudCOSXMLService and QCloudCOSTransferManagerService objects.  
> 3. If the QCloudServiceConfiguration is changed, you can register a new QCloudCOSTransferManagerService with `registerCOSTransferMangerWithConfiguration:(QCloudServiceConfiguration*)configuration withKey:(NSString*)key`, but only one QCloudCOSTransferManagerService can be set as the default.



[//]: # ".cssg-snippet-objc-global-init"
```objective-c
//AppDelegate.m
//Step 1. Register for the default COS service
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    QCloudServiceConfiguration* configuration = [QCloudServiceConfiguration new];
    configuration.appID = @"1250000000";
    configuration.signatureProvider = self;
    QCloudCOSXMLEndPoint* endpoint = [[QCloudCOSXMLEndPoint alloc] init];
    endpoint.regionName = @ "COS_REGION"; //Service region name. See notes for available regions
    configuration.endpoint = endpoint;
    [QCloudCOSXMLService registerDefaultCOSXMLWithConfiguration:configuration];
    [QCloudCOSTransferMangerService registerDefaultCOSTransferMangerWithConfiguration:configuration];
    return YES;
}

//Step 2. Implement the QCloudSignatureProvider protocol
//We recommend that the process of implementing the signature is done on the server. For more information, see the "Generating a signature" section below.
```

#### swift sample

[//]: # ".cssg-snippet-swift-global-init"
```swift
//AppDelegate.m
//Step 1. Register for the default COS service

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


//Step 2. Implement the QCloudSignatureProvider protocol
//We recommend that the process of implementing the signature is done on the server. For more information, see the "Generating a signature" section below.
```

### Creating a bucket

[//]: # ".cssg-snippet-objc-put-bucket"
```objective-c
QCloudPutBucketRequest* request = [QCloudPutBucketRequest new];
request.bucket = @"examplebucket-1250000000"; //additional actions after finishing
[request setFinishBlock:^(id outputObject, NSError* error) {
    //You can get the header information returned by the server from outputObject
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
    //Get the returned information from “result”
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
        //Get the returned information from “result”
        print(result!);
    }}
QCloudCOSXMLService.defaultCOSXML().getService(getServiceReq);
```

### Uploading an object

This example assumes you have applied for a bucket for your business. All SDK requests have corresponding request classes. When a request is generated, the corresponding attributes are set, and the request is passed to the QCloudCOSTransferMangerService object, the desired operation can be completed. For the request body, enter the local URL of the object to be uploaded (NSURL\* type).    

The API for uploading objects uses a signature for identity verification. A request will automatically be sent to request a signature from the object specified during initialization that follows the QCloudSignatureProvider protocol. For more information on how to generate a signature, see the [Generating a signature](#.E7.94.9F.E6.88.90.E7.AD.BE.E5.90.8D) section below.

> !The object included in the URL cannot be changed during upload; otherwise an error may occur.

#### Samples

[//]: # ".cssg-snippet-objc-transfer-upload-object"
```objective-c
QCloudCOSXMLUploadObjectRequest* put = [QCloudCOSXMLUploadObjectRequest new];
put.object = @"exampleobject";
put.bucket = @"examplebucket-1250000000";
put.body = [@"testFileContent" dataUsingEncoding:NSUTF8StringEncoding];
//Set upload parameters
put.initMultipleUploadFinishBlock = ^(QCloudInitiateMultipartUploadResult * multipleUploadInitResult,
    QCloudCOSXMLUploadObjectResumeData resumeData) {
    //This block will be called back after the Initiate Multipart Upload operation is complete so you can get resumeData
    //and can generate a multipart upload request using resumeData.
    QCloudCOSXMLUploadObjectRequest* request = [QCloudCOSXMLUploadObjectRequest
        requestWithRequestData:resumeData];
};
[put setSendProcessBlock:^(int64_t bytesSent, int64_t totalBytesSent,
    int64_t totalBytesExpectedToSend) {
    NSLog(@"upload %lld totalSend %lld aim %lld", bytesSent, totalBytesSent,
        totalBytesExpectedToSend);
}];
[put setFinishBlock:^(QCloudUploadObjectResult *result, NSError* error) {
    //You can get the result from “result”
}];

[[QCloudCOSTransferMangerService defaultCOSTransferManager] UploadObject:put];
//Abort the multipart upload and delete uploaded parts
[put abort:^(id outputObject, NSError *error) {
//
}];

//···When initialization is complete but upload is not complete
NSError* error;
//The following shows how resumeData is generated after you cancel an upload
QCloudCOSXMLUploadObjectResumeData resumeData = [put cancelByProductingResumeData:&error];
QCloudCOSXMLUploadObjectRequest* request = nil;
if (resumeData) {
    request = [QCloudCOSXMLUploadObjectRequest requestWithRequestData:resumeData];
}
//The request generated can be used to directly resume the previous unsuccessful multipart upload
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
//Set the upload parameters
uploadRequest.initMultipleUploadFinishBlock = {(multipleUploadInitResult,resumeData) in
    //This block will be called back after the Initiate Multipart Upload operation is completed so you can get resumeData and use it to generate a new multipart upload request.
    let resumeUploadRequest = QCloudCOSXMLUploadObjectRequest<AnyObject>.init(request: resumeData as Data?);
}
uploadRequest.sendProcessBlock = {(bytesSent , totalBytesSent , totalBytesExpectedToSend) in
    
}
uploadRequest.setFinish { (result, error) in
    if error != nil{
        print(error!)
    }else{
        //Get the request result from “result”
        print(result!);
    }}

QCloudCOSTransferMangerService.defaultCOSTransferManager().uploadObject(uploadRequest);

//···When initialization is complete but upload is not complete
var error:NSError?;
    //The following shows how resumeData is generated after you cancel an upload
do {
    let resumedData = try uploadRequest.cancel(byProductingResumeData: &error);
        var resumeUploadRequest:QCloudCOSXMLUploadObjectRequest<AnyObject>?;
             resumeUploadRequest = QCloudCOSXMLUploadObjectRequest<AnyObject>.init(request: resumedData as Data?);
             //The request generated can be used to directly resume the previous unsuccessful multipart upload
    if resumeUploadRequest != nil {
        QCloudCOSTransferMangerService.defaultCOSTransferManager().uploadObject(resumeUploadRequest!);
    }
             
} catch  {
    print("resumeData is blank");
    return;
}
```

#### QCloudCOSXMLUploadObjectRequest parameters

| Parameter Name                      | Description                                                         | Type                  | Required |
| ----------------------------- | ------------------------------------------------------------ | --------------------- | ---- |
| Object | An object key is the unique identifier of an object in a bucket. For example, if an object's endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`, the object key would be `doc/picture.jpg`. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | NSString * | Yes |
| bucket | Bucket name in the format: &lt;BucketName-APPID>, for example: `examplebucket-1250000000`. The bucket name can also be found on the [COS Console](https://console.cloud.tencent.com/cos5/bucket) | NSString * | Yes |
| body                          | <li>If the file you want to upload is stored on a disk, use the NSURL * type variable to indicate the file path.<br><li>If the file is stored in memory, use the NSData * type variable containing the file’s binary data. | BodyType | Yes    |
| storageClass | Storage class of the object | QCloudCOSStorageClass | Yes |
| cacheControl | Cache policy defined in RFC 2616 | NSString * | No |
| contentDisposition | File name defined in RFC 2616 | NSString * | No |
| expect | When `expect=@"100-Continue"` is used, the request content will not be sent until a response is received from the server. | NSString * | No |
| expires | Expiration time defined in RFC 2616 | NSString * | No |
| initMultipleUploadFinishBlock | Once the Initiate Multipart Upload operation is complete, this block will be used as a callback to return the bucket, key, uploadID, and ResumeData used to resume a subsequent unsuccessful upload | block                 | No   |
| accessControlList | Defines the ACL attribute of an object. Valid values: private, public-read; Default: private | NSString * | No |
| grantRead | Grants read permission in the format: `id="[OwnerUin]"` | NSString * | No |
| grantWrite | Grants write permission in the format: `id="[OwnerUin]"`. | NSString * | No |
| grantFullControl | Grants full permission in the format: `id="[OwnerUin]"`. | NSString * | No |

### Querying an object list

[//]: # ".cssg-snippet-objc-get-bucket"
```objective-c
QCloudGetBucketRequest* request = [QCloudGetBucketRequest new];
request.bucket = @"examplebucket-1250000000";
request.maxKeys = 1000;

[request setFinishBlock:^(QCloudListBucketResult * result, NSError* error) {
    //“result” contains the request result
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
//Set the download URL. Once set, the file will be downloaded to the specified path.
//If this parameter is not set, the file will be downloaded to memory and stored in the outputObject of finishBlock.
request.downloadingURL = [NSURL URLWithString:QCloudTempFilePathWithExtension(@"downding")];
request.object = @"exampleobject";
request.bucket = @"examplebucket-1250000000";

[request setFinishBlock:^(id outputObject, NSError *error) {
    //You can get the etag or custom headers in the outputObject response
}];
[request setDownProcessBlock:^(int64_t bytesDownload, int64_t totalBytesDownload,
    int64_t totalBytesExpectedToDownload) {
    //Download progress
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
    //You can get the etag or custom headers in the outputObject response
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

Any request in the SDK requires a signature to verify user identity and ensure access security. When the signature is invalid, most COS features are inaccessible and a 403 error is returned. For each request, the SDK requests a signature from signatureProvider in the QCloudServiceConfiguration object. You can assign the object responsible for generating signatures to the signatureProvider at the start. The object responsible for generating signatures should follow the QCloudSignatureProvider protocol and implement the following signature generation method:

```objective-c
- (void) signatureWithFields:(QCloudSignatureFields* )fileds    
					request:(QCloudBizHTTPRequest* )request    
					urlRequest:(NSURLRequest* )urlRequst    
					compelete:(QCloudHTTPAuthentationContinueBlock)continueBlock
```

### Connecting to CAM for temporary signatures (recommended)

Although the API for generating a signature with a permanent SecretId and SecretKey is provided locally, please note that storing the permanent SecretId and SecretKey locally is very risky and may cause unnecessary losses due to leakage. Therefore, we recommend that you implement the signature on the server for security purposes.

> !We strongly recommend using the server time as the start time of the signature to avoid signature errors caused by a deviation between your mobile phone's local time and standard time.

We recommended that you connect to CAM (Tencent Cloud's Cloud Access Manager) within your own signature server to implement the signature process.

![](https://main.qcloudimg.com/raw/d25267927fcaca9d9e0696f1aba872a5.png)    

For more information on how to set up a signature server to connect to CAM, see [Direct Upload for Mobile Apps](https://intl.cloud.tencent.com/document/product/436/30618).

After the signature server is connected to CAM, if a client requests a signature from the server, the server will request temporary credentials from CAM and return them to the client.
CAM generates a signature by generating a temporary SecretId, SecretKey, and Token based on your permanent SecretId and SecretKey to maximize security. Once receiving these temporary credentials, the terminal uses them to construct a QCloudCredential object. This object is then used to generate a QCloudAuthenticationCreator, which is in turn used to generate a QCloudSignature object containing the signature, as shown below:

[//]: # ".cssg-snippet-objc-global-init-signature-sts"
```objective-c
- (void) signatureWithFields:(QCloudSignatureFields*)fileds
                     request:(QCloudBizHTTPRequest*)request
                  urlRequest:(NSMutableURLRequest*)urlRequst
                   compelete:(QCloudHTTPAuthentationContinueBlock)continueBlock
{
    //*Request temporary Secret ID, Secret Key and Token from signature server*/
    QCloudCredential* credential = [QCloudCredential new];
    credential.secretID = @"COS_SECRETID";
    credential.secretKey = @"COS_SECRETKEY";
    credential.token = @"COS_TOKEN";
    /*We strongly recommend using the server time as the start time of the signature to avoid signature errors caused by a deviation between your mobile phone's local time and standard time*/
    credential.startDate = [[[NSDateFormatter alloc] init] dateFromString:@"startTime"]; //Measured in seconds
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
    /*We strongly recommend using the server time as the start time of the signature, to avoid signature errors caused by a deviation between your mobile phone's local time and standard time*/
    cre.startDate = DateFormatter().date(from: "startTime"); //Measured in seconds
    cre.experationDate = DateFormatter().date(from: "expiredTime");
    let auth = QCloudAuthentationV5Creator.init(credential: cre);
    let signature = auth?.signature(forData: urlRequst)
    continueBlock(signature,nil);
}
```

### Generating a signature on the terminal using a permanent key (not recommended)

> !We do not recommend that you use a permanent key to generate a signature on the terminal due to data leakage concerns.

The sample code is as follows:

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
`QCloudCredentailFenceQueue` provides a fencing mechanism, which means that if you obtain the signature using `QCloudCredentailFenceQueue`, any request for a signature will not be performed until the signature process is completed. This can eliminate the need to manage asynchronous processes.    
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

//Define a member variable @property (nonatomic) QCloudCredentailFenceQueue* credentialFenceQueue;

- (void) fenceQueue:(QCloudCredentailFenceQueue * )queue requestCreatorWithContinue:(QCloudCredentailFenceQueueContinue)continueBlock
{
    QCloudCredential* credential = [QCloudCredential new];
    //You can synchronize the process of obtaining the secretID, secretKey, expirationDate, and token parameters from the server which are needed to generate a temporary signature.
    credential.secretID = @"COS_SECRETID";
    credential.secretKey = @"COS_SECRETKEY";
    /*We strongly recommend using the server time as the start time of the signature to avoid signature errors caused by a deviation between your mobile phone's local time and standard time*/
    credential.startDate = [[[NSDateFormatter alloc] init] dateFromString:@"startTime"]; //Measured in seconds
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

//Define a member variable @property (nonatomic) QCloudCredentailFenceQueue* credentialFenceQueue;

func fenceQueue(_ queue: QCloudCredentailFenceQueue!, requestCreatorWithContinue continueBlock: QCloudCredentailFenceQueueContinue!) {
    let cre = QCloudCredential.init();
    //You can synchronize the process of obtaining the secretID, secretKey, expirationDate, and token parameters from the server which are needed to generate a temporary signature.
    cre.secretID = "COS_SECRETID";
    cre.secretKey = "COS_SECRETKEY";
    cre.token = "COS_TOKEN";
    /*We strongly recommend using the server time as the start time of the signature to avoid signature errors caused by a deviation between your mobile phone's local time and standard time*/
    cre.startDate = DateFormatter().date(from: "startTime"); //Measured in seconds
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

## User Guide for Simplified SDK

A simplified SDK is provided for users who only use upload and download features and who can only install a small-sized SDK. The simplified SDK is only half the size of the complete SDK.  

The simplified SDK is implemented via the Cocoapods Subspec, so it can only be integrated by using Cocoapods. To use the simplified SDK, add the following content to Podfile:

```
pod 'QCloudCOSXML/Transfer'
```

>For Mobile Line users, the simplified SDK is available only when TACStorage is **disabled** and the official source of [Cocoapods](https://github.com/CocoaPods/Specs) is placed **in front of all sources**. We recommend for it to be placed in the first line of the Podfile. Other users can ignore this note.

The simplified SDK does not use the header file QCloudCOSXML.h. Import the following header files at the time of initialization instead:

```
#import <QCloudCOSXML/QCloudCOSXMLTransfer.h>
#import <QCloudCore/QCloudCore.h>
```

The initialization process as well as APIs for uploading and downloading the simplified SDK are the same as those for the complete SDK.
