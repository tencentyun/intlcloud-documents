## Resources

- Download the iOS SDK source code [here](https://github.com/tencentyun/qcloud-sdk-ios.git).
- Access the demo [here](https://github.com/tencentyun/qcloud-sdk-ios-samples.git).
- For the SDK APIs and their parameters, see [SDK API Reference](https://cos-ios-sdk-doc-1253960454.file.myqcloud.com).
- For the complete sample code, see [SDK Sample Code](https://github.com/tencentyun/cos-snippets/tree/master/iOS).
- For the SDK changelog, see [Changelog](https://github.com/tencentyun/qcloud-sdk-ios/blob/master/CHANGELOG.md).
- For SDK FAQs, see [iOS SDK FAQs](https://intl.cloud.tencent.com/document/product/436/38957).

>? If you encounter errors such as non-existent functions or methods when using the XML version of the SDK, please update the SDK to the latest version and try again.
>

## Preparations

1. Prepare an iOS application; this can be an existing project or a new empty project.
2. Make sure that the application is built using an SDK running on iOS 8.0 or above.
3. You need a remote address where users can obtain your Tencent Cloud temporary key. For more information on temporary keys, see [Direct Upload for Mobile Apps](https://intl.cloud.tencent.com/document/product/436/30618).

## Step 1. Install the SDK

### Method 1: Integration using CocoaPods (recommended)

#### Standard SDK

Add the following content to the `Podfile` of your project:

```shell
pod 'QCloudCOSXML'
```
#### Simplified SDK

If you only need to perform upload and download operations and want a smaller sized SDK, you can use the simplified version.

The simplified SDK is implemented through the CocoaPods subspec feature, so it currently can only be integrated automatically. Add the following content to the `Podfile` of your project:

```shell
pod 'QCloudCOSXML/Transfer'
```

### Method 2: Manually integrate

You can directly download the latest version of the SDK [here](https://cos-sdk-archive-1253960454.file.myqcloud.com/qcloud-sdk-ios/latest/qcloud-sdk-ios.zip) or you can find all of the versions [here](https://github.com/tencentyun/qcloud-sdk-ios/releases).

#### 1. Import binary libraries

Drag `QCloudCOSXML.framework`, `QCloudCore.framework`, `BeaconAPI_Base.framework`, and `QimeiSDK.framework` into the project.

![](https://qcloudimg.tencent-cloud.cn/raw/a461545c9de56424126943fc16a3d381.png)  

Then, add the following dependent libraries:
 - CoreTelephony
 - Foundation
 - SystemConfiguration
 - libc++.tbd

#### 2. Configure your project

Configure "Other Linker Flags" in "Build Settings" by adding this parameter:

```shell
-ObjC
-all_load
```

![](https://main.qcloudimg.com/raw/125218fad3f4781cae8f992d9a152057.png)


>? The SDK provides a packaging script that supports self-packaging according to business requirements. (The packaging script depends on CocoaPods. Please make sure CocoaPods is installed in your development environment first.) The packaging procedure is as follows:
> 1. Download the source code: `git clone https://github.com/tencentyun/qcloud-sdk-ios`.
> 2. Run the packaging script: `source package.sh`.
> 3. Drag and drop the packaging result to the project and perform manual integration as described above.
>  - iOS: drag and drop the packaging result in the `ios` folder to the project.
>  - macOS: drag and drop the packaging result in the `osx` folder to the project.
![](https://main.qcloudimg.com/raw/631ae93aab3955149e5d0d8023eeac1b.png)


## Step 2. Begin Using the SDK

### 1. Import the header file

**Objective-c**

```objective-c
#import <QCloudCOSXML/QCloudCOSXML.h>
```

**swift**

```swift
import QCloudCOSXML
```

For the simplified SDK, import the following:

**Objective-c**

```objective-c
#import <QCloudCOSXML/QCloudCOSXMLTransfer.h>
```

**swift**

```swift
import QCloudCOSXMLTransfer
```

### 2. Initialize the COS service and implement the signature protocol

>!
> - We recommend you use a temporary key as instructed in [Generating and Using Temporary Keys](https://intl.cloud.tencent.com/document/product/436/14048) to call the SDK for security purposes. When you apply for a temporary key, follow the [Notes on Principle of Least Privilege](https://intl.cloud.tencent.com/document/product/436/32972) to avoid leaking resources besides your buckets and objects.
> - If you must use a permanent key, we recommend you follow the [Notes on Principle of Least Privilege](https://intl.cloud.tencent.com/document/product/436/32972) to limit the scope of permission on the permanent key.


#### Method 1: Obtaining a temporary key pair to authenticate requests (recommended)

The SDK needs to get a temporary key to calculate the signature before sending a request. Therefore, you need to implement the 'QCloudSignatureProvider' protocol to obtain the key and call back the key to the SDK through the 'continueBlock' parameter.

It is recommended to place the initialization process in 'AppDelegate' or **application singleton**.

For the detailed procedure, see the following sample code:

**Objective-c**

```objective-c
//AppDelegate.m
// `AppDelegate` must follow `QCloudSignatureProvider` 
@interface AppDelegate()<QCloudSignatureProvider>
@end

@implementation AppDelegate

- (BOOL)application:(UIApplication * )application 
        didFinishLaunchingWithOptions:(NSDictionary * )launchOptions {

    QCloudServiceConfiguration* configuration = [QCloudServiceConfiguration new];
    QCloudCOSXMLEndPoint* endpoint = [[QCloudCOSXMLEndPoint alloc] init];
    
    // Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket
    // For the list of regions supported by COS, see https://www.qcloud.com/document/product/436/6224
    endpoint.regionName = @"COS_REGION";
    // Use HTTPS
    endpoint.useHTTPS = true;
    configuration.endpoint = endpoint;
    // You are the key provider
    configuration.signatureProvider = self;
    // Initialize the COS instances
    [QCloudCOSXMLService registerDefaultCOSXMLWithConfiguration:configuration];
    [QCloudCOSTransferMangerService registerDefaultCOSTransferMangerWithConfiguration:
        configuration];
    return YES;
}


// Getting the signature: Here you can see how to get the temporary key and calculate the signature
// You can also customize the signature calculation process
- (void) signatureWithFields:(QCloudSignatureFields*)fields
                     request:(QCloudBizHTTPRequest*)request
                  urlRequest:(NSMutableURLRequest*)urlRequst
                   compelete:(QCloudHTTPAuthentationContinueBlock)continueBlock
{
        // Here, get the temporary key from the background server synchronously. It is highly recommended that the logic for getting a temporary key be placed here to maximize the availability of the key
    //...
    QCloudCredential* credential = [QCloudCredential new];

    // Temporary key SecretId 
    // Replace secret_id with the actual SecretId, which can be viewed at https://console.cloud.tencent.com/cam/capi
    credential.secretID = @"SECRETID";
    // Temporary key SecretKey
    // Replace secret_key with the actual SecretKey, which can be viewed at https://console.cloud.tencent.com/cam/capi
    credential.secretKey = @"SECRETKEY";
    // Temporary key token
    // Token is required for temporary keys but not permanent keys. For more information about how to generate and use a temporary key, see https://intl.cloud.tencent.com/document/product/436/14048
    credential.token = @"TOKEN";
    /** You are advised to use the returned server time as the start time of the signature, to avoid signature errors caused by the large deviation between your phone’s local time and the system time (the unit of `startTime` and `expiredTime` is second).
    */
    credential.startDate = [NSDate dateWithTimeIntervalSince1970:startTime]; // Unit: second
    credential.expirationDate = [NSDate dateWithTimeIntervalSince1970:expiredTime]]; // Unit: second
  
    QCloudAuthentationV5Creator* creator = [[QCloudAuthentationV5Creator alloc]
        initWithCredential:credential];
    // Note: Do not perform the copy or mutableCopy operation on `urlRequst`
    QCloudSignature *signature = [creator signatureForData:urlRequst];
    continueBlock(signature, nil);
}


@end
```

**Swift**

```swift
//AppDelegate.swift
// `AppDelegate` must follow `QCloudSignatureProvider` 

class AppDelegate: UIResponder, UIApplicationDelegate,
    QCloudSignatureProvider {

    func application(_ application: UIApplication, 
        didFinishLaunchingWithOptions launchOptions: 
        [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
        let config = QCloudServiceConfiguration.init();

        let endpoint = QCloudCOSXMLEndPoint.init();

        // Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket
        // For the list of regions supported by COS, see https://www.qcloud.com/document/product/436/6224
        endpoint.regionName = "COS_REGION";
        // Use HTTPS
        endpoint.useHTTPS = true;
        config.endpoint = endpoint;
        // You are the key provider
        config.signatureProvider = self;

        // Initialize the COS instances
        QCloudCOSXMLService.registerDefaultCOSXML(with: config);
        QCloudCOSTransferMangerService.registerDefaultCOSTransferManger(
            with: config);
        return true
    }


    // Getting the signature: Here you can see how to get the temporary key and calculate the signature
    // You can also customize the signature calculation process
    func signature(with fileds: QCloudSignatureFields!, 
        request: QCloudBizHTTPRequest!, 
        urlRequest urlRequst: NSMutableURLRequest!, 
        compelete continueBlock: QCloudHTTPAuthentationContinueBlock!) {
        
                // Get the temporary key from the backend server synchronously
        //...

        let credential = QCloudCredential.init();
        // Temporary key SecretId 
        // Replace secret_id with the actual SecretId, which can be viewed at https://console.cloud.tencent.com/cam/capi
        credential.secretID = "SECRETID";
        // Temporary key SecretKey
        // Replace secret_key with the actual SecretKey, which can be viewed at https://console.cloud.tencent.com/cam/capi
        credential.secretKey = "SECRETKEY";
        // Temporary key token
        // Token is required for temporary keys but not permanent keys. For more information about how to generate and use a temporary key, see https://intl.cloud.tencent.com/document/product/436/14048
        credential.token = "TOKEN";
        /** You are advised to use the returned server time as the start time of the signature, to avoid signature errors caused by the large deviation between your phone’s local time and the system time (the unit of `startTime` and `expiredTime` is second).
        */
        credential.startDate = Date.init(timeIntervalSince1970: TimeInterval(startTime)!) DateFormatter().date(from: "startTime");
        credential.expirationDate = Date.init(timeIntervalSince1970: TimeInterval(expiredTime)!) 

        let creator = QCloudAuthentationV5Creator.init(credential: credential);
        // Note: Do not perform the copy or mutableCopy operation on `urlRequst`
        let signature = creator?.signature(forData: urlRequst);
        continueBlock(signature,nil);
        
    }
}
```

>! 
>- APPID is a permanent unique application ID assigned to you after you sign up for a Tencent Cloud account. You can view your APPID on the [Account Information](https://console.cloud.tencent.com/developer) page.
>- SecretId and SecretKey, collectively referred to as the cloud API key, are the security credential used for authentication when a user accesses a Tencent Cloud API and can be viewed in [Manage API Key](https://console.cloud.tencent.com/cam/capi) of the console. SecretKey is the key used to encrypt the signature string and server-side authentication signature string, and SecretId identifies an API caller. Multiple cloud API keys can be created under an APPID.
>

The SDK provides the `QCloudCredentailFenceQueue` scaffolding tool for you to cache and reuse your temporary key. After a key expires, the scaffolding tool will call the protocol again to retrieve the new key until the key expiration time is later than the current device time.

>! The scaffolding tool determines whether a key can be reused based only on whether the key expiration time is later than the current device time. If you set up a complex policy when requesting a key, the scaffolding tool is not recommended.

It is recommended to place the initialization process in 'AppDelegate' or **application singleton**. You need to implement the following two protocols to use the scaffolding tool:

- QCloudSignatureProvider
- QCloudCredentailFenceQueueDelegate


The following is the sample code:


**Objective-c**

```objective-c
//AppDelegate.m
// `AppDelegate` needs to follow the `QCloudSignatureProvider` and 
// `QCloudCredentailFenceQueueDelegate` protocols

@interface AppDelegate()<QCloudSignatureProvider, QCloudCredentailFenceQueueDelegate>

// Scaffolding tool instance
@property (nonatomic) QCloudCredentailFenceQueue* credentialFenceQueue;

@end

@implementation AppDelegate

- (BOOL)application:(UIApplication * )application 
        didFinishLaunchingWithOptions:(NSDictionary * )launchOptions {
    QCloudServiceConfiguration* configuration = [QCloudServiceConfiguration new];
    QCloudCOSXMLEndPoint* endpoint = [[QCloudCOSXMLEndPoint alloc] init];

    // Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket
    // For the list of regions supported by COS, see https://www.qcloud.com/document/product/436/6224
    endpoint.regionName = @"COS_REGION";
    // Use HTTPS
    endpoint.useHTTPS = true;
    configuration.endpoint = endpoint;
    // You are the key provider
    configuration.signatureProvider = self;
    // Initialize the COS instances
    [QCloudCOSXMLService registerDefaultCOSXMLWithConfiguration:configuration];
    [QCloudCOSTransferMangerService registerDefaultCOSTransferMangerWithConfiguration:
        configuration];

    // Initialize the temporary key scaffolding tool
    self.credentialFenceQueue = [QCloudCredentailFenceQueue new];
    self.credentialFenceQueue.delegate = self;

    return YES;
}

- (void) fenceQueue:(QCloudCredentailFenceQueue * )queue requestCreatorWithContinue:(QCloudCredentailFenceQueueContinue)continueBlock
{
    // Here, get the temporary key from the background server synchronously. It is highly recommended that the logic for getting a temporary key be placed here to maximize the availability of the key
    //...

    QCloudCredential* credential = [QCloudCredential new];
    // Temporary key SecretId 
    // Replace secret_id with the actual SecretId, which can be viewed at https://console.cloud.tencent.com/cam/capi
    credential.secretID = @"SECRETID";
    // Temporary key SecretKey
    // Replace secret_key with the actual SecretKey, which can be viewed at https://console.cloud.tencent.com/cam/capi
    credential.secretKey = @"SECRETKEY";
    // Temporary key token
    // Token is required for temporary keys but not permanent keys. For more information about how to generate and use a temporary key, see https://intl.cloud.tencent.com/document/product/436/14048
    credential.token = @"TOKEN";
    /** You are advised to use the returned server time as the start time of the signature, to avoid signature errors caused by the large deviation between your phone’s local time and the system time (the unit of `startTime` and `expiredTime` is second).
    */
    credential.startDate = [NSDate dateWithTimeIntervalSince1970:startTime]; // Unit: second
    credential.expirationDate = [NSDate dateWithTimeIntervalSince1970:expiredTime]]; // Unit: second

    QCloudAuthentationV5Creator* creator = [[QCloudAuthentationV5Creator alloc]
        initWithCredential:credential];
    continueBlock(creator, nil);
}

// Getting the signature: Here you can see how to get the temporary key and calculate the signature
// You can also customize the signature calculation process
- (void) signatureWithFields:(QCloudSignatureFields*)fields
                     request:(QCloudBizHTTPRequest*)request
                  urlRequest:(NSMutableURLRequest*)urlRequst
                   compelete:(QCloudHTTPAuthentationContinueBlock)continueBlock
{
    [self.credentialFenceQueue performAction:^(QCloudAuthentationCreator *creator, 
        NSError *error) {
        if (error){
            continueBlock(nil, error);
        } else {
            // Note: Do not perform the copy or mutableCopy operation on `urlRequst`
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
// `AppDelegate` needs to follow the `QCloudSignatureProvider` and 
// `QCloudCredentailFenceQueueDelegate` protocols

class AppDelegate: UIResponder, UIApplicationDelegate,
    QCloudSignatureProvider, QCloudCredentailFenceQueueDelegate {

    var credentialFenceQueue:QCloudCredentailFenceQueue?;

    func application(_ application: UIApplication, 
        didFinishLaunchingWithOptions launchOptions: 
        [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
        let config = QCloudServiceConfiguration.init();

        let endpoint = QCloudCOSXMLEndPoint.init();

        // Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket
        // For the list of regions supported by COS, see https://www.qcloud.com/document/product/436/6224
        endpoint.regionName = "COS_REGION";
        // Use HTTPS
        endpoint.useHTTPS = true;
        config.endpoint = endpoint;
        // You are the key provider
        config.signatureProvider = self;

        // Initialize the COS instances
        QCloudCOSXMLService.registerDefaultCOSXML(with: config);
        QCloudCOSTransferMangerService.registerDefaultCOSTransferManger(
            with: config);

        // Initialize the temporary key scaffolding tool
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
        // Temporary key SecretId 
        // Replace secret_id with the actual SecretId, which can be viewed at https://console.cloud.tencent.com/cam/capi
        credential.secretID = "SECRETID";
        // Temporary key SecretKey
        // Replace secret_key with the actual SecretKey, which can be viewed at https://console.cloud.tencent.com/cam/capi
        credential.secretKey = "SECRETKEY";
        // Temporary key token
        // Token is required for temporary keys but not permanent keys. For more information about how to generate and use a temporary key, see https://intl.cloud.tencent.com/document/product/436/14048
        credential.token = "TOKEN";
        /** You are advised to use the returned server time as the start time of the signature, to avoid signature errors caused by the large deviation between your phone’s local time and the system time (the unit of `startTime` and `expiredTime` is second).
        */
        credential.startDate = Date.init(timeIntervalSince1970: TimeInterval(startTime)!) DateFormatter().date(from: "startTime");
        credential.expirationDate = Date.init(timeIntervalSince1970: TimeInterval(expiredTime)!) 

        let auth = QCloudAuthentationV5Creator.init(credential: credential);
        continueBlock(auth,nil);
    }

    // Getting the signature: Here you can see how to get the temporary key and calculate the signature
    // You can also customize the signature calculation process
    func signature(with fileds: QCloudSignatureFields!, 
        request: QCloudBizHTTPRequest!, 
        urlRequest urlRequst: NSMutableURLRequest!, 
        compelete continueBlock: QCloudHTTPAuthentationContinueBlock!) {
        self.credentialFenceQueue?.performAction({ (creator, error) in
            if error != nil {
                continueBlock(nil,error!);
            }else{
                // Note: Do not perform the copy or mutableCopy operation on `urlRequst`
                let signature = creator?.signature(forData: urlRequst);
                continueBlock(signature,nil);
            }
        })
    }
}
```

>!
> - For more information on the abbreviations of the COS bucket regions, see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224).
> - We recommend requesting data over HTTPS. However, if you want to use HTTP protocol, you need to enable HTTP transfer for your application so that it can run on iOS 9.0 or above. For detailed directions, see Apple's official documentation [Preventing Insecure Network Connections](https://developer.apple.com/documentation/security/preventing_insecure_network_connections).
> 


If your `QCloudServiceConfiguration` has changed, you can register a new instance by using the following method:

```objective-c
+ (QCloudCOSTransferMangerService*) registerCOSTransferMangerWithConfiguration:(QCloudServiceConfig

```
#### Method 2: Using a permanent key for local debugging

You can use your Tencent Cloud permanent key for local debugging during the development phase. **Since this method exposes the key to leakage risks, please be sure to replace it with a temporary key before launching your application.**

When using a permanent key, you can choose not to implement the `QCloudCredentailFenceQueueDelegate` protocol.

**Objective-C**

```objective-c
- (void) signatureWithFields:(QCloudSignatureFields*)fields
                     request:(QCloudBizHTTPRequest*)request
                  urlRequest:(NSMutableURLRequest*)urlRequst
                   compelete:(QCloudHTTPAuthentationContinueBlock)continueBlock
{
    
    QCloudCredential* credential = [QCloudCredential new];
    
    // secretID of the permanent key 
    // Replace secret_id with the actual SecretId, which can be viewed at https://console.cloud.tencent.com/cam/capi
    credential.secretID = @"SECRETID";
    // SecretKey of the permanent key
    // Replace secret_key with the actual SecretKey, which can be viewed at https://console.cloud.tencent.com/cam/capi
    credential.secretKey = @"SECRETKEY"; 
    // Use the permanent key to calculate the signature
    QCloudAuthentationV5Creator* creator = [[QCloudAuthentationV5Creator alloc] 
        initWithCredential:credential];
    // Note: Do not perform the copy or mutableCopy operation on `urlRequst`
    QCloudSignature* signature =  [creator signatureForData:urlRequst];
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
    
    // secretID of the permanent key 
    // Replace secret_id with the actual SecretId, which can be viewed at https://console.cloud.tencent.com/cam/capi
    credential.secretID = "SECRETID";
    // SecretKey of the permanent key
    // Replace secret_key with the actual SecretKey, which can be viewed at https://console.cloud.tencent.com/cam/capi
    credential.secretKey = "SECRETKEY"; 

    // Use the permanent key to calculate the signature
    let auth = QCloudAuthentationV5Creator.init(credential: credential);
    // Note: Do not perform the copy or mutableCopy operation on `urlRequst`
    let signature = auth?.signature(forData: urlRequst)
    continueBlock(signature,nil);
}
```

#### Method 3: Using a backend-calculated signature to authenticate requests

When the signature is generated on the backend, you can choose not to implement the `QCloudCredentailFenceQueueDelegate` protocol

**Objective-C**

```objective-c
- (void) signatureWithFields:(QCloudSignatureFields*)fields
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

### Uploading an object

The SDK allows you to upload local files and binary data in NSData format. The following uses local file upload as an example:

**Objective-C**

```objective-c
QCloudCOSXMLUploadObjectRequest* put = [QCloudCOSXMLUploadObjectRequest new];
// Local file path
NSURL* url = [NSURL fileURLWithPath:@"file URL"];
// Bucket name in the format of BucketName-APPID, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
put.bucket = @"examplebucket-1250000000";
// Object key, i.e., the full path of a COS object. If the object is in a directory, the path should be "video/xxx/movie.mp4"
put.object = @"exampleobject";
// Content of the object to be uploaded. You can pass in variables in `NSData*` or `NSURL*` format
put.body =  url;
// Monitor the upload progress
[put setSendProcessBlock:^(int64_t bytesSent,
                            int64_t totalBytesSent,
                            int64_t totalBytesExpectedToSend) {
    //      bytesSent                 Number of bytes to send in this request (a large file may require multiple requests)
    //      totalBytesSent            Total number of bytes sent so far
    //      totalBytesExpectedToSend  Total number of bytes expected to send, i.e. the size of the file
}];

// Monitor the upload result
[put setFinishBlock:^(id outputObject, NSError *error) {
    // outputObject contains information such as the ETag or custom headers in the response.
    NSDictionary * result = (NSDictionary *)outputObject;
}];

[[QCloudCOSTransferMangerService defaultCOSTransferManager] UploadObject:put];
```

>?
>- For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/TransferUploadObject.m).
>- You can generate a download URL for the uploaded file using the same key. For detailed directions, see [Generating a Pre-Signed Link](https://intl.cloud.tencent.com/document/product/436/37680). Please note that for private-read files, the download URL is only valid for a limited period of time.

**Swift**

```swift
let put:QCloudCOSXMLUploadObjectRequest = QCloudCOSXMLUploadObjectRequest<AnyObject>();
// Bucket name in the format of BucketName-APPID, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
put.bucket = "examplebucket-1250000000";
// Object key, i.e., the full path of a COS object. If the object is in a directory, the path should be "video/xxx/movie.mp4"
put.object = "exampleobject";
// Content of the object to be uploaded. You can pass in variables in `NSData*` or `NSURL*` format
put.body = NSURL.fileURL(withPath: "Local File Path") as AnyObject;

// Monitor the upload result
put.setFinish { (result, error) in
    // Get the upload result
    if error != nil{
        print(error!);
    }else{
        print(result!);
    }
}

// Monitor the upload progress
put.sendProcessBlock = { (bytesSent, totalBytesSent,
    totalBytesExpectedToSend) in
    //      bytesSent                 Number of bytes to send in this request (a large file may require multiple requests)
    //      totalBytesSent            Total number of bytes sent so far
    //      totalBytesExpectedToSend  Total number of bytes expected to send, i.e. the size of the file
};
// Set the upload parameters
put.initMultipleUploadFinishBlock = {(multipleUploadInitResult, resumeData) in
    // This block will be called back after the Initiate Multipart Upload operation is complete so you can get resumeData
    // and can generate a multipart upload request using resumeData.
    let resumeUploadRequest = QCloudCOSXMLUploadObjectRequest<AnyObject>
        .init(request: resumeData as Data?);
}

QCloudCOSTransferMangerService.defaultCOSTransferManager().uploadObject(put);
```

>?
>- For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/TransferUploadObject.swift).
>- You can generate a download URL for the uploaded file using the same key. For detailed directions, see [Generating a Pre-Signed Link](https://intl.cloud.tencent.com/document/product/436/37680). Please note that for private-read files, the download URL is only valid for a limited period of time.

### Downloading an object

**Objective-C**

```objective-c
QCloudCOSXMLDownloadObjectRequest * request = [QCloudCOSXMLDownloadObjectRequest new];
    
// Bucket name in the format of BucketName-APPID, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
request.bucket = @"examplebucket-1250000000";
// Object key, i.e., the full path of a COS object. If the object is in a directory, the path should be "video/xxx/movie.mp4"
request.object = @"exampleobject";

// Set the download URL. Once set, the file will be downloaded to the specified path
request.downloadingURL = [NSURL fileURLWithPath:@"Local File Path"];

// Monitor the download result
[request setFinishBlock:^(id outputObject, NSError *error) {
    // `outputObject` contains all HTTP response headers
    NSDictionary* info = (NSDictionary *) outputObject;
}];

// Monitor the download progress
[request setDownProcessBlock:^(int64_t bytesDownload,
                                int64_t totalBytesDownload,
                                int64_t totalBytesExpectedToDownload) {
    //      bytesDownload                   Number of bytes to download in this request (a large file may require multiple requests)
    //      totalBytesDownload              Number of bytes downloaded so far
    //      totalBytesExpectedToDownload    Total number of bytes expected to download, i.e. the size of the file
}];

[[QCloudCOSTransferMangerService defaultCOSTransferManager] DownloadObject:request];
```

>?For the complete sample, please go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/TransferDownloadObject.m).

**Swift**

```swift
let request : QCloudCOSXMLDownloadObjectRequest = QCloudCOSXMLDownloadObjectRequest();
        
// Bucket name in the format of BucketName-APPID, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
request.bucket = "examplebucket-1250000000";
// Object key
request.object = "exampleobject";

// Set the download URL. Once set, the file will be downloaded to the specified path
request.downloadingURL = NSURL.fileURL(withPath: "Local File Path") as URL?;

// Monitor the download progress
request.sendProcessBlock = { (bytesDownload, totalBytesDownload,
    totalBytesExpectedToDownload) in
    //      bytesDownload                   Number of bytes to download in this request (a large file may require multiple requests)
    //      totalBytesDownload              Number of bytes downloaded so far
    //      totalBytesExpectedToDownload    Total number of bytes expected to download, i.e. the size of the file
}

// Monitor the download result
request.finishBlock = { (copyResult, error) in
    if error != nil{
        print(error!);
    }else{
        print(copyResult!);
    }
}

QCloudCOSTransferMangerService.defaultCOSTransferManager().downloadObject(request);
```

>?For the complete sample, please go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/TransferDownloadObject.swift).
