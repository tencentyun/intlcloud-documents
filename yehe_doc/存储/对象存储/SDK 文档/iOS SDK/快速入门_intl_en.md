## Relevant Resources

- For the SDK source code, please see [XML SDK for iOS](https://github.com/tencentyun/qcloud-sdk-ios.git).
- For the demos, please see [XML SDK for iOS Demo](https://github.com/tencentyun/qcloud-sdk-ios-samples.git).
- For the SDK API and parameter documentation, please see [SDK API Reference](https://cos-ios-sdk-doc-1253960454.file.myqcloud.com).
- For all code samples in the SDK documentation, please see [SDK Sample Code](https://github.com/tencentyun/cos-snippets/tree/master/iOS).
- For the SDK changelog, please see [Changelog](https://github.com/tencentyun/qcloud-sdk-ios/blob/master/CHANGELOG.md).

## Preparations

1. Prepare an iOS application, which can be your existing project or a new empty project.
2. Make sure that the application is constructed based on the SDK for iOS 8.0 or above.
3. Prepare a remote address that can be used to get the Tencent Cloud temporary key. For more information on the temporary key, please see [Practice of Direct Upload for Mobile Apps](https://intl.cloud.tencent.com/document/product/436/30618).

## Step 1. Install the SDK

### Method 1. Use CocoaPods for integration (recommended)

#### Standard SDK

Add the following content to the `Podfile` file in your project:

```shell
pod 'QCloudCOSXML'
```

#### Disabling MTA reporting

In order to continuously track and optimize the SDK quality and deliver a better user experience, we introduced Mobile Tencent Analytics (MTA) into the SDK.

If you want to disable this feature, add the following content to the `Podfile` file in your project

```shell
pod 'QCloudCOSXML/WithoutMTA'
```

#### Lite SDK

If you use only upload and download features and want to keep the SDK size small, you can use the Lite SDK, which does not have the MTA feature.

The Lite SDK is implemented by using the Subspec feature of CocoaPods, so it can only be automatically integrated. Add the following content to the `Podfile` file in your project:

```shell
pod 'QCloudCOSXML/Transfer'
```

### Method 2. Manually integrate

You can download the latest release package [here](https://cos-sdk-archive-1253960454.file.myqcloud.com/qcloud-sdk-ios/latest/qcloud-sdk-ios.zip). For all release packages on historical versions, please see [SDK Releases](https://github.com/tencentyun/qcloud-sdk-ios/releases).

#### 1. Import the binary library

Drag **`QCloudCOSXML.framework`, `QCloudCore.framework`, and `libmtasdk.a`** to your project.

![](https://main.qcloudimg.com/raw/ce990d8871293daec0aa434f28b152e6.png)  

Add the following dependent libraries:
 - CoreTelephony
 - Foundation
 - SystemConfiguration
 - libc++.tbd

#### 2. Configure the project

Set "Other Linker Flags" in "Build Settings" and add the following parameters:

```shell
-ObjC
-all_load
```

![](https://main.qcloudimg.com/raw/125218fad3f4781cae8f992d9a152057.png)

## Step 2. Start to use

### 1. Import the header file

**Objective-c**

```objective-c
#import <QCloudCOSXML/QCloudCOSXML.h>
```

**swift**

```swift
import QCloudCOSXML
```

For the Lite SDK, import the following:

**Objective-c**

```objective-c
#import <QCloudCOSXML/QCloudCOSXMLTransfer.h>
```

**swift**

```swift
import QCloudCOSXMLTransfer
```

### 2. Create COS service instances

#### Method 1. Get the temporary key to authorize the request (recommended)

We recommend you place the initialization process in `AppDelegate`. The following two protocols need to be implemented:

- QCloudSignatureProvider
- QCloudCredentailFenceQueueDelegate

We provide a `QCloudCredentailFenceQueue` scaffold to cache and reuse the temporary key.

We recommend you design the COS service instances `QCloudCOSXMLService` and `QCloudCOSTransferMangerService` as **program singletons**.

Please see the following complete sample code:

**Objective-c**

```objective-c
//AppDelegate.m
// `AppDelegate` must follow the `QCloudSignatureProvider` and 
// `QCloudCredentailFenceQueueDelegate` protocols

@interface AppDelegate()<QCloudSignatureProvider, QCloudCredentailFenceQueueDelegate>

// Scaffold instance
@property (nonatomic) QCloudCredentailFenceQueue* credentialFenceQueue;

@end

@implementation AppDelegate

- (BOOL)application:(UIApplication * )application 
        didFinishLaunchingWithOptions:(NSDictionary * )launchOptions {
    QCloudServiceConfiguration* configuration = [QCloudServiceConfiguration new];
    QCloudCOSXMLEndPoint* endpoint = [[QCloudCOSXMLEndPoint alloc] init];
    // Service region abbreviation; for example, it is `ap-guangzhou` for the Guangzhou region
    endpoint.regionName = @"COS_REGION";
    // Use HTTPS
    endpoint.useHTTPS = true;
    configuration.endpoint = endpoint;
    // The key is provided by yourself
    configuration.signatureProvider = self;
    // Initialize COS service instances
    [QCloudCOSXMLService registerDefaultCOSXMLWithConfiguration:configuration];
    [QCloudCOSTransferMangerService registerDefaultCOSTransferMangerWithConfiguration:
        configuration];

    // Initialize the temporary key scaffold
    self.credentialFenceQueue = [QCloudCredentailFenceQueue new];
    self.credentialFenceQueue.delegate = self;

    return YES;
}

- (void) fenceQueue:(QCloudCredentailFenceQueue * )queue requestCreatorWithContinue:(QCloudCredentailFenceQueueContinue)continueBlock
{
    // Get the temporary key from the backend server synchronously
    //...

    QCloudCredential* credential = [QCloudCredential new];
    // Temporary key's `SecretId`
    credential.secretID = @"COS_SECRETID";
    // Temporary key's `SecretKey`
    credential.secretKey = @"COS_SECRETKEY";
    // Temporary key's `Token`
    credential.token = @"COS_TOKEN";
    // We strongly recommend you return the server time as the start time of the signature
    // This is to avoid signature errors caused by large deviation of the mobile phone's local time from the server time
    credential.startDate = [[[NSDateFormatter alloc] init] 
        dateFromString:@"startTime"]; // Unit: second
    credential.experationDate = [[[NSDateFormatter alloc] init] 
        dateFromString:@"expiredTime"];

    QCloudAuthentationV5Creator* creator = [[QCloudAuthentationV5Creator alloc]
        initWithCredential:credential];
    continueBlock(creator, nil);
}

// Entry of the method for getting signature. Here shows the process of getting the temporary key and calculating the signature
// You can also customize the signature calculation process
- (void) signatureWithFields:(QCloudSignatureFields*)fileds
                     request:(QCloudBizHTTPRequest*)request
                  urlRequest:(NSMutableURLRequest*)urlRequst
                   compelete:(QCloudHTTPAuthentationContinueBlock)continueBlock
{
    [self.credentialFenceQueue performAction:^(QCloudAuthentationCreator *creator, 
        NSError *error) {
        if (error) {
            continueBlock(nil, error);
        } else {
            QCloudSignature* signature =  [creator signatureForData:urlRequst];
            continueBlock(signature, nil);
        }
    }];
}


@end
```

**Swift**

```swift
//AppDelegate.swift
// `AppDelegate` must follow the `QCloudSignatureProvider` and 
// `QCloudCredentailFenceQueueDelegate` protocols

class AppDelegate: UIResponder, UIApplicationDelegate,
    QCloudSignatureProvider, QCloudCredentailFenceQueueDelegate {

    var credentialFenceQueue:QCloudCredentailFenceQueue?;

    func application(_ application: UIApplication, 
        didFinishLaunchingWithOptions launchOptions: 
        [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
        let config = QCloudServiceConfiguration.init();

        let endpoint = QCloudCOSXMLEndPoint.init();
        // Service region abbreviation; for example, it is `ap-guangzhou` for the Guangzhou region
        endpoint.regionName = "COS_REGION";
        // Use HTTPS
        endpoint.useHTTPS = true;
        config.endpoint = endpoint;
        // The key is provided by yourself
        config.signatureProvider = self;

        // Initialize COS service instances
        QCloudCOSXMLService.registerDefaultCOSXML(with: config);
        QCloudCOSTransferMangerService.registerDefaultCOSTransferManger(
            with: config);

        // Initialize the temporary key scaffold
        self.credentialFenceQueue = QCloudCredentailFenceQueue.init();
        self.credentialFenceQueue?.delegate = self;

        return true
    }

    func fenceQueue(_ queue: QCloudCredentailFenceQueue!, 
        requestCreatorWithContinue continueBlock: 
        QCloudCredentailFenceQueueContinue!) {
        // Get the temporary key from the backend server synchronously
        //...

        let credential = QCloudCredential.init();
        // Temporary key's `SecretId`
        credential.secretID = "COS_SECRETID";
        // Temporary key's `SecretKey`
        credential.secretKey = "COS_SECRETKEY";
        // Temporary key's `Token`
        credential.token = "COS_TOKEN";
        // We strongly recommend you return the server time as the start time of the signature
        // This is to avoid signature errors caused by large deviation of the mobile phone's local time from the server time
        credential.startDate = DateFormatter().date(from: "startTime");
        // Here, the unit of the returned time is second
        credential.experationDate = DateFormatter().date(from: "expiredTime");

        let auth = QCloudAuthentationV5Creator.init(credential: credential);
        continueBlock(auth,nil);
    }

    // Entry of the method for getting signature. Here shows the process of getting the temporary key and calculating the signature
    // You can also customize the signature calculation process
    func signature(with fileds: QCloudSignatureFields!, 
        request: QCloudBizHTTPRequest!, 
        urlRequest urlRequst: NSMutableURLRequest!, 
        compelete continueBlock: QCloudHTTPAuthentationContinueBlock!) {
        self.credentialFenceQueue?.performAction({ (creator, error) in
            if error != nil {
                continueBlock(nil,error!);
            }else{
                let signature = creator?.signature(forData: urlRequst);
                continueBlock(signature,nil);
            }
        })
    }
}
```

>!
>- For the abbreviations of different bucket regions, please see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224).
>- We recommend you request data over HTTPS, but if you want to use HTTP, to ensure that the application can run on iOS 9.0 or above, you need to enable transfer over HTTP for the application. For detailed directions, please see Apple's official document [Preventing Insecure Network Connections](https://developer.apple.com/documentation/security/preventing_insecure_network_connections).

If your `QCloudServiceConfiguration` is changed, you can register a new instance as follows:

```objective-c
+ (QCloudCOSTransferMangerService*) registerCOSTransferMangerWithConfiguration:(QCloudServiceConfiguration*)configuration withKey:(NSString*)key;
```

#### Method 2. Use a permanent key for local debugging

You can use a Tencent Cloud permanent key for local debugging during the development. **As this method may disclose your key, please change to the temporary key method before launching your application.**

Implementation of the `QCloudCredentailFenceQueueDelegate` protocol is optional if you use a permanent key.

**Objective-C**

```objective-c
- (void) signatureWithFields:(QCloudSignatureFields*)fileds
                     request:(QCloudBizHTTPRequest*)request
                  urlRequest:(NSMutableURLRequest*)urlRequst
                   compelete:(QCloudHTTPAuthentationContinueBlock)continueBlock
{
    
    QCloudCredential* credential = [QCloudCredential new];
    credential.secretID = @"COS_SECRETID"; // Permanent key's `SecretId`
    credential.secretKey = @"COS_SECRETKEY"; // Permanent key's `SecretKey`

    // Calculate the signature with a permanent key
    QCloudAuthentationV5Creator* creator = [[QCloudAuthentationV5Creator alloc] 
        initWithCredential:credential];
    QCloudSignature* signature = [creator signatureForData:urlRequst];
    continueBlock(signature, nil);
}
```

**Swift**

```swift
func signature(with fileds: QCloudSignatureFields!, 
                request: QCloudBizHTTPRequest!, 
                urlRequest urlRequst: NSMutableURLRequest!, 
                compelete continueBlock: QCloudHTTPAuthentationContinueBlock!) {
    let credential = QCloudCredential.init();
    credential.secretID = "COS_SECRETID"; // Permanent key's `SecretId`
    credential.secretKey = "COS_SECRETKEY"; // Permanent key's `SecretKey`

    // Calculate the signature with a permanent key
    let auth = QCloudAuthentationV5Creator.init(credential: credential);
    let signature = auth?.signature(forData: urlRequst)
    continueBlock(signature,nil);
}
```

#### Method 3. Use the signature calculated on the backend to authorize the request

Implementation of the `QCloudCredentailFenceQueueDelegate` protocol is optional if the signature is generated on the backend.

**Objective-C**

```objective-c
- (void) signatureWithFields:(QCloudSignatureFields*)fileds
                     request:(QCloudBizHTTPRequest*)request
                  urlRequest:(NSMutableURLRequest*)urlRequst
                   compelete:(QCloudHTTPAuthentationContinueBlock)continueBlock
{
    // Signature expiration time
    NSDate *expiration = [[[NSDateFormatter alloc] init] 
                            dateFromString:@"expiredTime"];
    QCloudSignature *sign = [[QCloudSignature alloc] initWithSignature:
        @"Signature calculated on backend" expiration:expiration];
    continueBlock(signature, nil);
}
```

**Swift**

```swift
func signature(with fileds: QCloudSignatureFields!, 
                request: QCloudBizHTTPRequest!, 
                urlRequest urlRequst: NSMutableURLRequest!, 
                compelete continueBlock: QCloudHTTPAuthentationContinueBlock!) {
    // Signature expiration time
    let expiration = DateFormatter().date(from: "expiredTime");
    let sign = QCloudSignature.init(signature: "signature calculated on backend", 
                expiration: expiration);
    continueBlock(signature,nil);
}
```

## Step 3. Access COS

### Uploading object

The SDK allows you to upload local files and binary data (NSData). The following uses local file upload as an example:

**Objective-C**

```objective-c
QCloudCOSXMLUploadObjectRequest* put = [QCloudCOSXMLUploadObjectRequest new];
// Local file path
NSURL* url = [NSURL fileURLWithPath:@"file URL"];
// Bucket name in the format of `BucketName-APPID`
put.bucket = @"examplebucket-1250000000";
// Object key, which is the full path of the object in COS. If the path contains a directory, its format will be "dir1/object1"
put.object = @"exampleobject";
// Content of the object to be uploaded. You can pass in variables in `NSData*` or `NSURL*` type
put.body =  url;
// Listen on the upload progress
[put setSendProcessBlock:^(int64_t bytesSent,
                            int64_t totalBytesSent,
                            int64_t totalBytesExpectedToSend) {
    //      bytesSent                   Number of sent bytes
    //      totalBytesSent              Total number of bytes sent in this upload
    //      totalBytesExpectedToSend    Target number of bytes for this upload
}];

// Listen on the upload result
[put setFinishBlock:^(id outputObject, NSError *error) {
    // You can get information such as `etag` or custom header in the response from `outputObject`
    NSDictionary * result = (NSDictionary *)outputObject;
}];

[[QCloudCOSTransferMangerService defaultCOSTransferManager] UploadObject:put];
```

>?
>- For more complete samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/TransferUploadObject.m).
>- After an object is uploaded, you can use the same key to generate a file download link as instructed in **Generating Pre-signed Link**. However, please note that if your file is set to private-read, the download link will only be valid for a certain period of time.

**Swift**

```swift
let put:QCloudCOSXMLUploadObjectRequest = QCloudCOSXMLUploadObjectRequest<AnyObject>();
// Bucket name in the format of `BucketName-APPID`
put.bucket = "examplebucket-1250000000";
// Object key, which is the full path of the object in COS. If the path contains a directory, its format will be "dir1/object1"
put.object = "exampleobject";
// Content of the object to be uploaded. You can pass in variables in `NSData*` or `NSURL*` type
put.body = NSURL.fileURL(withPath: "Local File Path") as AnyObject;

// Listen on the upload result
put.setFinish { (result, error) in
    // Get the upload result
    if error != nil{
        print(error!);
    }else{
        print(result!);
    }
}

// Listen on the upload progress
put.sendProcessBlock = { (bytesSent, totalBytesSent,
    totalBytesExpectedToSend) in
    //      bytesSent                   Number of sent bytes
    //      totalBytesSent              Total number of bytes sent in this upload
    //      totalBytesExpectedToSend    Target number of bytes for this upload
};
// Set upload parameters
put.initMultipleUploadFinishBlock = {(multipleUploadInitResult, resumeData) in
    // After the initialization of the multipart upload is completed, this block will be called back, where you can get the `resumeData`
    // `resumeData` can be used to generate a new multipart upload request
    let resumeUploadRequest = QCloudCOSXMLUploadObjectRequest<AnyObject>
        .init(request: resumeData as Data?);
}

QCloudCOSTransferMangerService.defaultCOSTransferManager().uploadObject(put);
```

>?
>- For more complete samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/TransferUploadObject.swift).
>- After an object is uploaded, you can use the same key to generate a file download link as instructed in **Generating Pre-signed Link**. However, please note that if your file is set to private-read, the download link will only be valid for a certain period of time.

### Downloading object

**Objective-C**

```objective-c
QCloudCOSXMLDownloadObjectRequest * request = [QCloudCOSXMLDownloadObjectRequest new];
    
// Bucket name in the format of `BucketName-APPID`
request.bucket = @"examplebucket-1250000000";
// Object key, which is the full path of the object in COS. If the path contains a directory, its format will be "dir1/object1"
request.object = @"exampleobject";

// Set the download path URL; if this is set, the file will be downloaded to the specified path
request.downloadingURL = [NSURL fileURLWithPath:@"Local File Path"];

// Listen on the download result
[request setFinishBlock:^(id outputObject, NSError *error) {
    // `outputObject` contains all HTTP response headers
    NSDictionary* info = (NSDictionary *) outputObject;
}];

// Listen on the download progress
[request setDownProcessBlock:^(int64_t bytesDownload,
                                int64_t totalBytesDownload,
                                int64_t totalBytesExpectedToDownload) {
    //      bytesDownload                   Number of downloaded bytes
    //      totalBytesDownload              Total number of bytes received in this download
    //      totalBytesExpectedToDownload    Target number of bytes for this download
}];

[[QCloudCOSTransferMangerService defaultCOSTransferManager] DownloadObject:request];
```

>?For more complete samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/TransferDownloadObject.m).

**Swift**

```swift
let request : QCloudCOSXMLDownloadObjectRequest = QCloudCOSXMLDownloadObjectRequest();
        
// File bucket
request.bucket = "examplebucket-1250000000";
// Object key
request.object = "exampleobject";

// Set the download path URL; if this is set, the file will be downloaded to the specified path
request.downloadingURL = NSURL.fileURL(withPath: "Local File Path") as URL?;

// Listen on the download progress
request.sendProcessBlock = { (bytesDownload, totalBytesDownload,
    totalBytesExpectedToDownload) in
    //      bytesDownload                   Number of downloaded bytes
    //      totalBytesDownload              Total number of bytes received in this download
    //      totalBytesExpectedToDownload    Target number of bytes for this download
}

// Listen on the download result
request.finishBlock = { (copyResult, error) in
    if error != nil{
        print(error!);
    }else{
        print(copyResult!);
    }
}

QCloudCOSTransferMangerService.defaultCOSTransferManager().downloadObject(request);
```

>?For more complete samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/TransferDownloadObject.swift).

