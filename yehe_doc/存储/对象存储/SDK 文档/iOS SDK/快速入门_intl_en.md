## Download and Installation

### Relevant resources

- The COS SDK for iOS can be downloaded [here](https://github.com/tencentyun/qcloud-sdk-ios.git).   
- You can download the packaged SDK in Framework format by selecting the desired version from [Release](https://github.com/tencentyun/qcloud-sdk-ios/releases).
- For more samples, please see the [XML SDK for iOS Demo](https://github.com/tencentyun/qcloud-sdk-ios-samples.git)
- For the changelog of COS XML Edition, please see [XML SDK for iOS  Changelog](https://github.com/tencentyun/qcloud-sdk-ios/blob/master/CHANGELOG.md).

### Environmental dependency

- The SDK supports iOS 8.0 and higher.
- Your mobile phone must be connected to a network (GPRS, 3G, 4G, Wi-Fi, etc.).
- Get the `SecretId` and `SecretKey` on the [API Key Management](https://console.cloud.tencent.com/capi) page in the CAM Console. Get the `APPID` in the [Account Center](https://console.cloud.tencent.com/developer).

> For the definitions of `SecretID`, `SecretKey`, `bucket`, and other terms, please see [COS Glossary](https://intl.cloud.tencent.com/document/product/436/7751).

### Installing the SDK

#### Importing the SDK

You can integrate SDK through CocoaPods or by downloading packaged static libraries. CocoaPods is recommended for import.

- **Import with CocoaPods (recommended)**  
  In Podfile, use:
```shell
pod 'QCloudCOSXML'
```

- **Import with packaged static libraries (manual integration)**  
  Drag **`QCloudCOSXML.framework`, `QCloudCore.framework`, and `libmtasdk.a`** to your project as shown below:
  ![](https://main.qcloudimg.com/raw/ce990d8871293daec0aa434f28b152e6.png)  
  Add the following dependent libraries:
 - CoreTelephony
 - Foundation
 - SystemConfiguration
 - libc++.tbd

#### Project configuration

Set "Other Linker Flags" in "Build Settings" and add the following parameters:

```shell
-ObjC
-all_load
```

See the figure below:
![](https://main.qcloudimg.com/raw/125218fad3f4781cae8f992d9a152057.png)

>
>Tencent Cloud COS XML SDK for iOS uses the HTTP protocol. To run the SDK on iOS, you need to enable transfer over HTTP.
>   You can enable transfer over HTTP in the following two ways:
> - **Configuring manually**
>   Add "App Transport Security Settings" to the "info.plist" file of the project, and then add "Allow Arbitrary Loads" under "App Transport Security Settings", and set its type to "Boolean" and value to "YES".
> - **Configuring through code**
>   You can add the following code in the info.plist of the application integrated with the SDK:
> ```shell
> <key>NSAppTransportSecurity</key>
> <dict>
> <key>NSExceptionDomains</key>
> <dict>
> 	<key>myqcloud.com</key>
> 	<dict>
> 		<key>NSIncludesSubdomains</key>
> 		<true/>
> 		<key>NSTemporaryExceptionAllowsInsecureHTTPLoads</key>
> 		<true/>
> 	</dict>
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

The section below describes how to perform basic operations with COS SDK for iOS, such as initializing a client, creating a bucket, querying bucket list, uploading an object, querying object list, downloading an object, and deleting an object. For more information, please see the [XML SDK for iOS Demo](https://github.com/tencentyun/qcloud-sdk-ios-samples). For API usage, please see the testing files in the demo.

### Prerequisites
You need to apply for an `APPID` of COS in the [Tencent Cloud Console](https://console.cloud.tencent.com/cos5) first.

<span id="step1"></span>
### Initialization

Before using the features of the SDK, you need to import some necessary header files and perform initialization.
Import the header files for the upload SDK:

```objective-c
QCloudCore.h,    
QCloudCOSXML/QCloudCOSXML.h
```

#### Method prototype

Instantiate a `QCloudServiceConfiguration` object:

```
QCloudServiceConfiguration* configuration = [QCloudServiceConfiguration new];
configuration.appID = @"APPID"// Project ID;
```

Instantiate a `QCloudCOSXMLService` object:

<pre>
+ (QCloudCOSXMLService*) registerDefaultCOSXMLWithConfiguration:(QCloudServiceConfiguration*)configuration;
</pre>

Instantiate a `QCloudCOSTransferManagerService` object:

<pre>
+ (QCloudCOSTransferMangerService*) registerDefaultCOSTransferMangerWithConfiguration:(QCloudServiceConfiguration*)configuration;
</pre>

##### `QCloudServiceConfiguration` parameter description

| Parameter Name | Description | Type | Required |
| -------- | ------------------------ | ---------------------- | ---- |
| appID | Project ID, i.e., `APPID` | NSString * | No |
| endpoint | Configures endpoint-related information | QCloudCOSXMLEndPoint * | Yes |

##### `QCloudCOSXMLEndPoint` parameter description

| Parameter Name | Description | Type | Required |
| ----------- | ----------------------------------- | ---------- | ---- |
| regionName  | Service region | NSString * | Yes |
| serviceName | Domain name. Default value: `myqcloud.com`       | NSString * | No |
| useHTTPS    | Indicates whether to use the HTTPS service. Default value: NO | BOOL       | No |
| suffix      | `http://bucketname.suffix` can be customized | NSString   | No   |

#### Initialization sample

The `APPID`, `SecretId`, and `SecretKey` in the samples below can be obtained from the [COS Console](https://console.cloud.tencent.com/cos5).

>
> 1. The `QCloudSignatureProvider` protocol needs to be implemented for the `signatureProvider` object of `QCloudServiceConfiguration`.
> 2. Before using the SDK, instantiate a default cloud service configuration object `QCloudServiceConfiguration`, and then instantiate `QCloudCOSXMLService` and `QCloudCOSTransferManagerService` objects.  
> 3. If `QCloudServiceConfiguration` is changed, you can register a new `QCloudCOSTransferManagerService` with `registerCOSTransferMangerWithConfiguration:(QCloudServiceConfiguration*)configuration withKey:(NSString*)key`, but only one `QCloudCOSTransferManagerService` can be set as default.



[//]: # ".cssg-snippet-objc-global-init"
```objective-c
//AppDelegate.m
// Step 1. Register the default COS service
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    QCloudServiceConfiguration* configuration = [QCloudServiceConfiguration new];
    configuration.appID = @"1250000000";
    configuration.signatureProvider = self;
    QCloudCOSXMLEndPoint* endpoint = [[QCloudCOSXMLEndPoint alloc] init];
    endpoint.regionName = @"COS_REGION";// Service region name. For available regions, please see the comments
    configuration.endpoint = endpoint;
    [QCloudCOSXMLService registerDefaultCOSXMLWithConfiguration:configuration];
    [QCloudCOSTransferMangerService registerDefaultCOSTransferMangerWithConfiguration:configuration];
    return YES;
}

// Step 2. Implement the `QCloudSignatureProvider` protocol
// It is recommended to implement the signing process on the server. For more information, please see the "Generating a Signature" section below.
```

#### Swift sample

[//]: # ".cssg-snippet-swift-global-init"
```swift
//AppDelegate.m
// Step 1. Register the default COS service

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


// Step 2. Implement the `QCloudSignatureProvider` protocol
// It is recommended to implement the signing process on the server. For more information, please see the "Generating a Signature" section below.
```

### Creating a bucket

[//]: # ".cssg-snippet-objc-put-bucket"
```objective-c
QCloudPutBucketRequest* request = [QCloudPutBucketRequest new];
request.bucket = @"examplebucket-1250000000"; //additional actions after finishing
[request setFinishBlock:^(id outputObject, NSError* error) {
    // Get the header information returned by the server from the outputObject
}];
[[QCloudCOSXMLService defaultCOSXML] PutBucket:request];
```

#### Swift sample

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

### Querying bucket list

[//]: # ".cssg-snippet-get-service"
```objective-c
QCloudGetServiceRequest* request = [[QCloudGetServiceRequest alloc] init];
[request setFinishBlock:^(QCloudListAllMyBucketsResult* result, NSError* error) {
    // Get the return information from the result
}];
[[QCloudCOSXMLService defaultCOSXML] GetService:request];
```

#### Swift sample

[//]: # ".cssg-snippet-swift-get-service"
```swift
let getServiceReq = QCloudGetServiceRequest.init();
getServiceReq.setFinish{(result,error) in
    if result == nil {
        print(error!);
    } else {
        // Get the return information from the result
        print(result!);
    }}
QCloudCOSXMLService.defaultCOSXML().getService(getServiceReq);
```

### Uploading an object

Assume that you have applied for a bucket for your business. In fact, all SDK requests have their corresponding request classes. As long as a request is generated and the relevant attributes are set, the request can be passed to the `QCloudCOSTransferMangerService` object to complete the desired operation. For the body part of the request, enter the local URL (in NSURL\* type) of the file to be uploaded.    

The API for uploading objects uses a signature for authentication. A sent request automatically requests a signature from the object specified during initialization that follows the `QCloudSignatureProvider` protocol. For more information on how to generate a signature, please see the [Generating a Signature](#.E7.94.9F.E6.88.90.E7.AD.BE.E5.90.8D) section below.

>The object to which the URL points cannot be changed during upload; otherwise, an error will occur.

#### Sample

[//]: # ".cssg-snippet-objc-transfer-upload-object"
```objective-c
QCloudCOSXMLUploadObjectRequest* put = [QCloudCOSXMLUploadObjectRequest new];
put.object = @"exampleobject";
put.bucket = @"examplebucket-1250000000";
put.body = [@"testFileContent" dataUsingEncoding:NSUTF8StringEncoding];
// Set some parameters of the upload
put.initMultipleUploadFinishBlock = ^(QCloudInitiateMultipartUploadResult * multipleUploadInitResult,
    QCloudCOSXMLUploadObjectResumeData resumeData) {
    // After the initialization of the multipart upload is completed, this block will be called back, where you can get the resumeData
    // resumeData can be used to generate a new multipart upload request
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
// Abort a multipart upload operation and delete the uploaded parts
[put abort:^(id outputObject, NSError *error) {
//
}];

//••• After initialization is completed before upload is completed
NSError* error;
// This is an example of resumetData generated after cancellation is called
QCloudCOSXMLUploadObjectResumeData resumeData = [put cancelByProductingResumeData:&error];
QCloudCOSXMLUploadObjectRequest* request = nil;
if (resumeData) {
    request = [QCloudCOSXMLUploadObjectRequest requestWithRequestData:resumeData];
}
// The request generated for resumption can start an upload directly
[[QCloudCOSTransferMangerService defaultCOSTransferManager] UploadObject:request];
```

#### Swift sample

[//]: # ".cssg-snippet-swift-transfer-upload-object"
```swift
let uploadRequest = QCloudCOSXMLUploadObjectRequest<AnyObject>.init();
let dataBody:NSData? = "wrwrwrwrwrw".data(using: .utf8) as NSData?;
uploadRequest.body = dataBody!;
uploadRequest.bucket = "examplebucket-1250000000";
uploadRequest.object = "exampleobject";
// Set upload parameters
uploadRequest.initMultipleUploadFinishBlock = {(multipleUploadInitResult,resumeData) in
    // After the initialization of the multipart upload is completed, this block will be called back, where you can get the resumeData which can be used to generate a new multipart upload request
    let resumeUploadRequest = QCloudCOSXMLUploadObjectRequest<AnyObject>.init(request: resumeData as Data?);
}
uploadRequest.sendProcessBlock = {(bytesSent , totalBytesSent , totalBytesExpectedToSend) in
    
}
uploadRequest.setFinish { (result, error) in
    if error != nil{
        print(error!)
    }else{
        // Get the request result from `result`
        print(result!);
    }}

QCloudCOSTransferMangerService.defaultCOSTransferManager().uploadObject(uploadRequest);

//••• After initialization is completed before upload is completed
var error:NSError?;
    // This is an example of resumetData generated after cancellation is called
do {
    let resumedData = try uploadRequest.cancel(byProductingResumeData: &error);
        var resumeUploadRequest:QCloudCOSXMLUploadObjectRequest<AnyObject>;
             resumeUploadRequest = QCloudCOSXMLUploadObjectRequest<AnyObject>.init(request: resumedData as Data?);
             // The request generated for resumption can start an upload directly
    if resumeUploadRequest != nil {
        QCloudCOSTransferMangerService.defaultCOSTransferManager().uploadObject(resumeUploadRequest!);
    }
             
} catch  {
    print("resumeData is empty");
    return;
}
```

#### `QCloudCOSXMLUploadObjectRequest` parameter description

| Parameter Name | Description | Type | Required |
| ----------------------------- | ------------------------------------------------------------ | --------------------- | ---- |
| Object | An object key (Key) is a unique ID of an object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`, the object key is `doc/picture.jpg`. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324) | NSString * | Yes |
| bucket   | Bucket name in the format of `&lt;BucketName-APPID&gt;` such as `examplebucket-1250000000`, which can be viewed in the [COS Console](https://console.cloud.tencent.com/cos5/bucket) | NSString * | Yes |
| body | Path to the file to be uploaded. Enter a variable of `NSURL *` type | BodyType | Yes |
| storageClass | Object storage class | QCloudCOSStorageClass | Yes |
| cacheControl | Cache policy defined in RFC 2616 | NSString * | No |
| contentDisposition | Filename as defined in RFC 2616 | NSString * | No |
| expect | If `expect=@"100-Continue"` is used, the request content will be sent only after confirmation from the server is received | NSString * | No|
| expires | File date and time as defined in RFC 2616 | NSString * | No |
| initMultipleUploadFinishBlock | If the request generates a multipart upload request, after the initialization of multipart upload, a callback will be performed through this block. The bucket, key, and `uploadID` after the completion of the multipart upload as well as the ResumeData for resuming subsequent failing upload can be obtained from this callback block. | block | No |
| accessControlList | Defines the ACL attribute of the object. Valid values: private, public-read. Default value: private | NSString * | No |
| grantRead         | Grants the grantee read permission in the format of `id="[OwnerUin]"`                    | NSString * | No |
| grantWrite        | Grants the grantee write permission in the same format as described above                    | NSString * | No   |
| grantFullControl  | Grants the grantee read/write permission in the same format as described above                    | NSString * | No   |

### Querying object list

[//]: # ".cssg-snippet-objc-get-bucket"
```objective-c
QCloudGetBucketRequest* request = [QCloudGetBucketRequest new];
request.bucket = @"examplebucket-1250000000";
request.maxKeys = 1000;

[request setFinishBlock:^(QCloudListBucketResult * result, NSError* error) {
    // `result` returns specific information
}];

[[QCloudCOSXMLService defaultCOSXML] GetBucket:request];
```

#### Swift sample

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
// Set the download path URL; if this is set, the file will be downloaded to a specified path
// Otherwise, the file will be downloaded to the memory and stored in the `outputObject` of the `finishBlock`
request.downloadingURL = [NSURL URLWithString:QCloudTempFilePathWithExtension(@"downding")];
request.object = @"exampleobject";
request.bucket = @"examplebucket-1250000000";

[request setFinishBlock:^(id outputObject, NSError *error) {
    // You can get information such as etag or custom header in the response from `outputObject`
}];
[request setDownProcessBlock:^(int64_t bytesDownload, int64_t totalBytesDownload,
    int64_t totalBytesExpectedToDownload) {
    // Download progress
}];

[[QCloudCOSXMLService defaultCOSXML] GetObject:request];
```

#### Swift sample

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
    // You can get information such as etag or custom header in the response from `outputObject`
}];

[[QCloudCOSXMLService defaultCOSXML] DeleteObject:deleteObjectRequest];
```

#### Swift sample

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

## Generating a Signature

Any request in the SDK requires a signature to authenticate the accessing user and ensure the security of access. If the signature is incorrect, most COS services will be inaccessible and a 403 error will be returned. A signature can be generated in the SDK. For each request, the signature can be requested from the `signatureProvider` object in the `QCloudServiceConfiguration` object. The object for generating signatures can be assigned to the `signatureProvider` at the beginning, which should follow the `QCloudSignatureProvider` protocol and implement the signature generation method:

```objective-c
- (void) signatureWithFields:(QCloudSignatureFields* )fileds    
					request:(QCloudBizHTTPRequest* )request    
					urlRequest:(NSURLRequest* )urlRequst    
					compelete:(QCloudHTTPAuthentationContinueBlock)continueBlock
```

### Connecting to CAM for temporary signature (recommended)

Although the API for generating signatures with permanent `SecretId` and `SecretKey` is provided locally, it should be noted that storing the permanent `SecretId` and `SecretKey` locally is very risky and may cause unnecessary losses due to leakage. Therefore, it is recommended to implement the signing process on the server for the sake of security.

>It is strongly recommended to return the server time as the start time of the signature so as to avoid incorrect signature caused by large deviation of the mobile phone's local time from the server time.

You are recommended to connect to Tencent Cloud's CAM on your own signature server to implement the signing process.

![](https://main.qcloudimg.com/raw/d25267927fcaca9d9e0696f1aba872a5.png)    

For more information on how to set up a signature server and connect it to CAM, please see [Practice of Direct Transfer for Mobile Apps](/document/product/436/9068).

After the signature server is connected to CAM, when a client requests a signature from the server, the server will request a temporary certificate from CAM and return it to the client.
The CAM system will generate temporary `SecretId`, `SecretKey`, and `Token` to calculate a signature based on your permanent `SecretId` and `SecretKey` for maximized security. After receiving the information of these temporary keys, the client will build a `QCloudCredential` object by using the keys to generate a `QCloudAuthentationCreator`, through which it will generate a `QCloudSignature` object containing the signature information. The example below shows the steps:

[//]: # ".cssg-snippet-objc-global-init-signature-sts"
```objective-c
- (void) signatureWithFields:(QCloudSignatureFields*)fileds
                     request:(QCloudBizHTTPRequest*)request
                  urlRequest:(NSMutableURLRequest*)urlRequst
                   compelete:(QCloudHTTPAuthentationContinueBlock)continueBlock
{
    /*Request the temporary `Secret ID`, `Secret Key`, and `Token` from the signature server*/
    QCloudCredential* credential = [QCloudCredential new];
    credential.secretID = @"COS_SECRETID";
    credential.secretKey = @"COS_SECRETKEY";
    credential.token = @"COS_TOKEN";
    /*It is strongly recommended to return the server time as the start time of the signature so as to avoid incorrect signature caused by large deviation of the mobile phone's local time from the server time*/
    credential.startDate = [[[NSDateFormatter alloc] init] dateFromString:@"startTime"]; // Unit: second
    credential.experationDate  = [[[NSDateFormatter alloc] init] dateFromString:@"expiredTime"];
    QCloudAuthentationV5Creator* creator = [[QCloudAuthentationV5Creator alloc] initWithCredential:credential];
    QCloudSignature* signature =  [creator signatureForData:urlRequst];
    continueBlock(signature, nil);
}
```

#### Swift sample

[//]: # ".cssg-snippet-swift-global-init-signature-sts"
```swift

func signature(with fileds: QCloudSignatureFields!, request: QCloudBizHTTPRequest!, urlRequest urlRequst: NSMutableURLRequest!, compelete continueBlock: QCloudHTTPAuthentationContinueBlock!) {
    let cre = QCloudCredential.init();
    cre.secretID = "COS_SECRETID";
    cre.secretKey = "COS_SECRETKEY";
    cre.token = "COS_TOKEN";
    /*It is strongly recommended to return the server time as the start time of the signature so as to avoid incorrect signature caused by large deviation of the mobile phone's local time from the server time*/
    cre.startDate = DateFormatter().date(from: "startTime"); // Unit: second
    cre.experationDate = DateFormatter().date(from: "expiredTime");
    let auth = QCloudAuthentationV5Creator.init(credential: cre);
    let signature = auth?.signature(forData: urlRequst)
    continueBlock(signature,nil);
}
```

### Generating a signature by using a permanent key on the device (not recommended)

>It is not recommended to use a permanent key to generate a signature on the device, as this may cause data leakage.

Below is sample code:

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

#### Swift sample

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

### Managing async signatures with a scaffold

Now you can generate a signature and use the APIs in the SDK. Moreover, a scaffold is provided to make it easier for you to implement a temporary signature and get the information necessary for the temporary signature such as `tempSecretKey` from the server. You can either generate a signature by following the above code or get a temporary signature by using the `QCloudCredentailFenceQueue` scaffold.
`QCloudCredentailFenceQueue` provides a fencing mechanism, which means if you get a signature by using `QCloudCredentailFenceQueue`, any requests that require a signature will not be performed until the signing process is completed. This can eliminate the need to manage the async process.   
To use `QCloudCredentailFenceQueue`, you need to create an instance first.

```objective-c
//AppDelegate.m
// `AppDelegate` must follow the `QCloudCredentailFenceQueueDelegate` protocol
//
- (BOOL)application:(UIApplication * )application didFinishLaunchingWithOptions:(NSDictionary * )launchOptions {
    // init step
    self.credentialFenceQueue = [QCloudCredentailFenceQueue new];
    self.credentialFenceQueue.delegate = self;
    return YES;
}

```

Next, the class that calls `QCloudCredentailFenceQueue` must follow `QCloudCredentailFenceQueueDelegate` and implement the method defined in the protocol:

```objective-c
- (void) fenceQueue:(QCloudCredentailFenceQueue * )queue requestCreatorWithContinue:(QCloudCredentailFenceQueueContinue)continueBlock
```

When you get a signature through `QCloudCredentailFenceQueue`, all the requests in the SDK that need the signature will not be performed until the parameters required for signature calculation are obtained in the method defined by the protocol and a valid signature is generated. For more information, please see the example below:

[//]: # ".cssg-snippet-objc-global-init-fence-queue"
```objective-c
//AppDelegate.m

// Define a member variable here: @property (nonatomic) QCloudCredentailFenceQueue* credentialFenceQueue;

- (void) fenceQueue:(QCloudCredentailFenceQueue * )queue requestCreatorWithContinue:(QCloudCredentailFenceQueueContinue)continueBlock
{
    QCloudCredential* credential = [QCloudCredential new];
    // You can sync the process to get the `secretID`, `secretKey`, `expirationDate`, and `token` parameters needed for the temporary signature from the server
    credential.secretID = @"COS_SECRETID";
    credential.secretKey = @"COS_SECRETKEY";
    /*It is strongly recommended to return the server time as the start time of the signature so as to avoid incorrect signature caused by large deviation of the mobile phone's local time from the server time*/
    credential.startDate = [[[NSDateFormatter alloc] init] dateFromString:@"startTime"]; // Unit: second
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

#### Swift sample

[//]: # ".cssg-snippet-swift-global-init-fence-queue"
```swift
//AppDelegate.m

// Define a member variable here: @property (nonatomic) QCloudCredentailFenceQueue* credentialFenceQueue;

func fenceQueue(_ queue: QCloudCredentailFenceQueue!, requestCreatorWithContinue continueBlock: QCloudCredentailFenceQueueContinue!) {
    let cre = QCloudCredential.init();
    // You can sync the process to get the `secretID`, `secretKey`, `expirationDate`, and `token` parameters needed for the temporary signature from the server
    cre.secretID = "COS_SECRETID";
    cre.secretKey = "COS_SECRETKEY";
    cre.token = "COS_TOKEN";
    /*It is strongly recommended to return the server time as the start time of the signature so as to avoid incorrect signature caused by large deviation of the mobile phone's local time from the server time*/
    cre.startDate = DateFormatter().date(from: "startTime"); // Unit: second
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

At this point, you can generate a temporary signature with the provided scaffold. You can also implement the signature process on your own.

## User Guide on the Simplified SDK

A simplified SDK is provided for users who only use upload and download features and can only install a small SDK. It is half of the complete SDK in terms of size.  

The simplified SDK is implemented by using the Subspec feature of CocoaPods, so it can only be integrated by using CocoaPods. To use it, add the following to Podfile:

```
pod 'QCloudCOSXML/Transfer'
```

>For Mobile Line users, the simplified SDK can be used only when TACStorage is **disabled**; in this case, the official source of [CocoaPods](https://github.com/CocoaPods/Specs) should be placed **in front of all sources** (it is recommended to place it in the first line in Podfile). Other users can ignore this note.

The simplified SDK does not have the `QCloudCOSXML.h` header file. Instead, import the following header files at the time of initialization:

```
#import <QCloudCOSXML/QCloudCOSXMLTransfer.h>
#import <QCloudCore/QCloudCore.h>
```

The initialization and APIs for upload and download of the simplified SDK are the same as those of the complete SDK.
