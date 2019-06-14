## Preparations for Development

### Obtain the SDK 

- Download iOS SDK resources of COS service from: [XML iOS SDK](https://github.com/tencentyun/qcloud-sdk-ios.git).   
- You can download the packaged SDK in the Framework format by selecting the desired version from [Release](https://github.com/tencentyun/qcloud-sdk-ios/releases).
- For more examples, see Demo: [XML iOS SDK Demo](https://github.com/tencentyun/qcloud-sdk-ios-samples.git).
- For the changes of each COS XML version, see [XML iOS  SDK  ChangeLog](https://github.com/tencentyun/qcloud-sdk-ios/blob/master/CHANGELOG.md) 。.

### Preparations for development

- SDK supports iOS 8.0 or above.
- Your mobile phone must be connected to a network (GPRS, 3G, Wi-Fi, etc.).
- Obtain the APPID, SecretId, and SecretKey from the [COS V5 Console](https://console.cloud.tencent.com/cos5).

> ?For more information on the definitions of SecretID, SecretKey, Bucket and other terms and how to obtain them, see [COS Glossary](https://cloud.tencent.com/document/product/436/7751).

### Configure the SDK

#### Import the SDK

You can integrate SDK via cocoapods or by downloading packaged dynamic libraries. We recommend using cocoapods for import.

-  **Importing using Cocoapods (recommended)**  
  In Podfile, use:

```
  pod 'QCloudCOSXML'
```

-  **Importing using the packaged dynamic library (manual integration)**  
  Drag **QCloudCOSXML.framework, QCloudCore.framework and libmtasdk.a** to your project, as shown below:
  ![](https://main.qcloudimg.com/raw/ce990d8871293daec0aa434f28b152e6.png)  
  And add the following dependent libraries:

> 1. CoreTelephony
> 2. Foundation
> 3. SystemConfiguration
> 4. libc++.tbd

#### Configure the project

Set up "Other Linker Flags" in "Build Settings" and add the parameter:

```shell
-ObjC
-all_load
```

See the figure below:
![](https://main.qcloudimg.com/raw/2736ab0172191942e41e3268838a1e88.png)


> - Tencent Cloud COS XML iOS SDK uses HTTP protocol. To run the SDK on iOS, enable transfer over HTTP.
> You can enable transfer over HTTP in the following two ways:
>    - **Configuring manually**
> Add "App Transport Security Settings" to the "info.plist" file of the project, and then add "Allow Arbitrary Loads" under "App Transport Security Settings", and set its type to "Boolean", and value to "YES".
>    - **Configuring via code**
> You can add the following code in the info.plist of the App integrating SDK:
>   ```
> <key>NSAppTransportSecurity</key>
>  <dict>
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
>- Mobile Tencent Analytics (MTA) is also introduced in the SDK. If you want to disable this feature, follow the steps below:
>  - Import the header file ` #import <QCloudCore/MTAConfig.h>`
>  - After registering the default cosxml service, add the following code:
> `[TACMTAConfig getInstance].statEnable = NO;`

### Initialization  

Before using the features of SDK, import some necessary header files and perform initialization.
Import and upload the header files for SDK:

```objective-c
QCloudCore.h,    
QCloudCOSXML/QCloudCOSXML.h
```



> 1. Before using the SDK, instantiate a default cloud service configuration object QCloudServiceConfiguration, and then instantiate QCloudCOSXMLService and QCloudCOSTransferManagerService objects.  
>2. If QCloudServiceConfiguration is changed, you can register a new QCloudCOSTransferManagerService with `registerCOSTransferMangerWithConfiguration:(QCloudServiceConfiguration*)configuration withKey:(NSString*)key`, but only one QCloudCOSTransferManagerService can be set as default.

#### Method prototype

Instantiate QCloudServiceConfiguration object:

```
 QCloudServiceConfiguration* configuration = [QCloudServiceConfiguration new];
 configuration.appID = @""//Project ID.
```

Instantiate QCloudCOSXMLService object:

```
+ (QCloudCOSXMLService*) registerDefaultCOSXMLWithConfiguration:(QCloudServiceConfiguration*)configuration;
```

Instantiate QCloudCOSTransferManagerService object:

```
+ (QCloudCOSTransferMangerService*) registerDefaultCOSTransferMangerWithConfiguration:(QCloudServiceConfiguration*)configuration;
```

#### QCloudServiceConfiguration parameters

| Parameter Name | Description | Type | Required |
| -------- | ------------------------ | ---------------------- | ---- |
| appID | Project ID, i.e. APPID. | NSString * | No |
| endpoint | Configures endpoint related information | QCloudCOSXMLEndPoint * | Yes |

#### QCloudCOSXMLEndPoint parameters

| Parameter Name | Description | Type | Required |
| ----------- | -------------------------------- | ---------- | ---- |
| regionName  | The region of the service | NSString * | Yes |
| serviceName | Domain name. Default is myqcloud.com.       | NSString * | No |
| useHTTPS    | Indicates whether to use the HTTPS service. Default is No. | BOOL       | No |
| suffix    | Supports custom http://bucketname.suffix | NSString       | No |


#### Example of initialization
The appID, SecretId and SecretKey in the example below can be obtained from the [COS v5 Console](https://console.cloud.tencent.com/cos5).

```objective-c
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

## Getting Started

The examples below show the basic process of upload and download. For more information, see [XML iOS SDK Demo](https://github.com/tencentyun/qcloud-sdk-ios-samples). For how to use each API, see the unit test files provided in Demo.

> You must apply for the APPID of COS service on the [Tencent Cloud Console](https://console.cloud.tencent.com/cos4/secret) before proceeding with this step.

### Initialization

> QCloudSignatureProvider protocol needs to be implemented for the signatureProvider object of QCloudServiceConfiguration.

#### Step 1:

```objective-c
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

#### Step 2:

```objective-c
//AppDelegate.m
- (void) signatureWithFields:(QCloudSignatureFields*)fileds
                     request:(QCloudBizHTTPRequest*)request
                  urlRequest:(NSURLRequest*)urlRequst
                   compelete:(QCloudHTTPAuthentationContinueBlock)continueBlock
{
//The process of implementing signature. We recommend implementing this process on the server. For more information, see the "Generating a Signature" section below.
}
```

### Upload a file

The example assumes you have applied for a Bucket for your business. In fact, all SDK requests have their Request classes. When a request is generated and the relevant attributes are set, pass the request to the QCloudCOSTransferMangerService object to complete the desired operation. For the body part of the request, enter the local URL of the file to be uploaded (NSURL\* type).    

The API for uploading files uses a signature for authentication. A request sent automatically requests a signature from the object specified during initialization that follows the QCloudSignatureProvider protocol. For more information on how to generate a signature, see the [Generating a Signature](#.E7.94.9F.E6.88.90.E7.AD.BE.E5.90.8D) section below.

> The file to which the URL points cannot be changed during upload, otherwise it will cause an error.

#### Example

```objective-c
    QCloudCOSXMLUploadObjectRequest* put = [QCloudCOSXMLUploadObjectRequest new];
    NSURL* url = [NSURL fileURLWithPath:@"filePathString"] /*URL of file*/;
    put.object = @"filename.jpg";
    put.bucket = @"test-123456789";
    put.body =  url;
    [put setSendProcessBlock:^(int64_t bytesSent, int64_t totalBytesSent, int64_t totalBytesExpectedToSend) {
        NSLog(@"upload %lld totalSend %lld aim %lld", bytesSent, totalBytesSent, totalBytesExpectedToSend);
    }];
    [put setFinishBlock:^(id outputObject, NSError* error) {

    }];
    [[QCloudCOSTransferMangerService defaultCOSTransferManager] UploadObject:put];
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
| grantRead | Grants read permission to the authorized user. Format: id=" ",id=" ". For authorization to a subaccount, id="qcs::cam::uin/&lt;OwnerUin>:uin/&lt;SubUin>"; for authorization to the root account, id="qcs::cam::uin/&lt;OwnerUin>:uin/&lt;OwnerUin>", where OwnerUin refers to the ID of the root account and SubUin refers to the ID of the subaccount. | NSString * | No |
| grantWrite | Grants write permission to the authorized user. The format is the same as above. | NSString * | No |
| grantFullControl | Grants read and write permissions to the authorized user. The format is the same as above. | NSString * | No |

### Download a file

#### Example

```objective-c
  QCloudGetObjectRequest* request = [QCloudGetObjectRequest new];
  //Set the URL for download. If it has been set, the file is downloaded to the specified path.
  request.downloadingURL = [NSURL URLWithString:QCloudTempFilePathWithExtension(@"downding")];
  request.object = @“Your Object-Key”;
  request.bucket = @"test-123456789";
  [request setFinishBlock:^(id outputObject, NSError \*error) {
    //additional actions after finishing
}];
[request setDownProcessBlock:^(int64_t bytesDownload, int64_t totalBytesDownload, int64_t totalBytesExpectedToDownload) {
	 //Progress of download
	}];
[[QCloudCOSXMLService defaultCOSXML] GetObject:request];
```

## Generating a Signature

Any request in the SDK requires a signature to verify the identity of the accessing user and to ensure the security of access. When the signature is incorrect, most COS services are inaccessible and a 403 error is returned. A signature can be generated in the SDK. For each request, the signature can be requested from the signatureProvider object in the QCloudServiceConfiguration object. The object for generating signatures can be assigned to the signatureProvider at the beginning, and should follow the QCloudSignatureProvider protocol and implement the signature generation method:

```objective-c
- (void) signatureWithFields:(QCloudSignatureFields* )fileds    
                     request:(QCloudBizHTTPRequest* )request    
                  urlRequest:(NSURLRequest* )urlRequst    
                   compelete:(QCloudHTTPAuthentationContinueBlock)continueBlock
```

### Connect to CAM system for temporary signature (recommended)

Although the API for generating a signature with permanent SecretId and SecretKey is provided locally, note that storing the permanent SecretId and SecretKey locally is very risky and may cause unnecessary losses due to leakage. Therefore, it is recommended to implement the signature on the server to ensure security.

>It is strongly recommended to return the server time as the start time of the signature, to avoid incorrect signature caused by large deviation of mobile phone's local time from the standard time.

It is recommended to connect to Tencent Cloud's CAM (Cloud Access Manager) within your own signature server to implement the signature process.

![](https://main.qcloudimg.com/raw/d25267927fcaca9d9e0696f1aba872a5.png)      

For more information on how to set up a signature server to connect to CAM system, see [Practice of Direct Transfer for Mobile Apps](https://intl.cloud.tencent.com/document/product/436/30618).

After the signature server is connected to the CAM system, if the client requests a signature from the server, the server requests a temporary certificate from the CAM system and returns it to the client. The CAM system generates temporary Secret ID, Secret Key and Token to generate a signature based on your permanent SecretId and SecretKey. By this way, the security is maximized. After receiving the information of these temporary keys, the terminal builds a QCloudCredential object using the keys, generates the QCloudAuthenticationCreator via the QCloudCredentail object, and then generates a QCloudSignature object containing the signature information with this Creator. The example below shows the steps.

```objective-c
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

```

### Generate a signature using the permanent keys at the terminal (not recommended)

>It is not recommend that you use permanent keys to generate a signature at the terminal. This may cause data leakage.

Sample code is as follows:

```objective-c
- (void) signatureWithFields:(QCloudSignatureFields*)fileds
                     request:(QCloudBizHTTPRequest*)request
                  urlRequest:(NSMutableURLRequest*)urlRequst
                   compelete:(QCloudHTTPAuthentationContinueBlock)continueBlock
{

    QCloudCredential* credential = [QCloudCredential new];
    credential.secretID = @"Permanent SecretID";
    credential.secretKey = @"Permanent SecretKey";
    QCloudAuthentationV5Creator* creator = [[QCloudAuthentationV5Creator alloc] initWithCredential:credential];
    QCloudSignature* signature =  [creator signatureForData:urlRequst];
    continueBlock(signature, nil);
}

```

### Manage asynchronous signature using a scaffolding tool

Now you can generate a signature and use the APIs in the SDK. Moreover, a scaffolding tool is provided to make it easier for you to implement a temporary signature and obtain the information necessary for the temporary signature such as tempSecretKey from the server. You can either generate a signature by following the above code, or obtain a temporary signature with our scaffolding tool QCloudCredentailFenceQueue. It provides a fencing mechanism, which means if you obtain the signature using QCloudCredentailFenceQueue, any request for a signature will not be performed until the signature process is completed. This can eliminate the need to manage the asynchronous process.   
To use QCloudCredentailFenceQueue, generate an instance first.

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

Next, the class that calls QCloudCredentailFenceQueue must follow QCloudCredentailFenceQueueDelegate and implement the method defined in the protocol:

```objective-c
- (void) fenceQueue:(QCloudCredentailFenceQueue * )queue requestCreatorWithContinue:(QCloudCredentailFenceQueueContinue)continueBlock
```

When you obtain the signature using QCloudCredentailFenceQueue, all the requests in the SDK that need signatures will not be performed until the parameters required for the signature are obtained via the method defined by the protocol and a valid signature is generated. See the example below:

```objective-c
//AppDelegate.m
- (void) fenceQueue:(QCloudCredentailFenceQueue * )queue requestCreatorWithContinue:(QCloudCredentailFenceQueueContinue)continueBlock
{
   QCloudCredential* credential = [QCloudCredential new];
   //You can synchronize the process to obtain from the server the secretID, secretKey, expirationDate and token parameters needed for the temporary signature.
   credential.secretID = @"****";
   credential.secretKey = @"****";
   /*It is strongly recommended to return the server time as the start time of the signature, to avoid incorrect signature caused by large deviation of mobile phone's local time from the standard time.*/ 
   credential.startDate =[NSDate dateWithTimeIntervalSince1970:@"Returned server time"]
   credential.experationDate = [NSDate dateWithTimeIntervalSince1970:1504183628];
   credential.token = @"****";
   QCloudAuthentationV5Creator* creator = [[QCloudAuthentationV5Creator alloc] initWithCredential:credential];
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

At this point, you can generate a temporary signature with the scaffolding tool we provide. You can also implement the signature process by yourself.

## User Guide on the Simplified SDK

A simplified SDK is provided for users who only use upload and download features and who can only install a small size SDK. The simplified SDK is half of the complete SDK in terms of size.  

The simplified SDK is implemented via Subspec of Cocoapods, so it can only be integrated by using Cocoapods. To use the simplified SDK, add the following content to Podfile:

```
pod 'QCloudCOSXML/Transfer'
```

> For Mobile Line users, the simplified SDK is available only when TACStorage is **disabled** and the official source of [Cocoapods](https://github.com/CocoaPods/Specs) is placed **in front of all sources**. It is recommended to place it in the first line in Podfile. Other users can ignore this note.

The simplified SDK does not have the header file QCloudCOSXML.h. Import the following header file at the time of initialization:

```
#import <QCloudCOSXML/QCloudCOSXMLTransfer.h>
#import <QCloudCore/QCloudCore.h>
```

The initialization and APIs for upload and download of the simplified SDK are the same with those of the complete SDK.

