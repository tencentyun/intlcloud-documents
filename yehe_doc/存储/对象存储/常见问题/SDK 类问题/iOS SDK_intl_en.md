### What should I do if the error `[__NSCFConstantString matchesRegularExpression:]: unrecognized selector sent to instance xxx` is thrown after I manually integrate the SDK and set `regionName` for the `QCloudCOSXMLEndPoint` instance?

**Cause**: `matchesRegularExpression` is a method in the `NSString` category. Objective-C does not define linker symbols for each method, but for each class. The SDK is a static library. If a category has been defined for an existing class in the static library, the system assumes that the class already exists and will not integrate the code of the class and category. As a result, methods in the category will be missing in the executable code.

**Solution**:
1. Select the target, click **Build Settings** > **All** > **Other Linker Flags**, and add the `-Objc` and `-all_load` parameters.
2. `-ObjC` loads the classes and categories in the static library to the executable file. If there are only categories but no classes in the library, `-ObjC` will not take effect. In this case, `-all_load` is needed to load all object files to the executable file.
3. If the problem persists, disable Bitcode.

### What should I do if the error `Default OCR configuration is not set/Key is not set to 'xxx' in the OCR configuration. Call this method after it is configured` is thrown after I integrated the SDK and sent a request?

**Cause**: All SDK requests depend on `QCloudCOSXMLService` and `QCloudCOSTransferMangerService` (advanced upload APIs depend on this instance). If the corresponding service is not registered before the request is sent, this error will be thrown.

**Solution**: Use the following code to register the service instance required by the request. Ensure that the instance exists before you send a request.

```iOS
    QCloudServiceConfiguration *configuration = [QCloudServiceConfiguration new];
    configuration.appID = "AppId";
    configuration.signatureProvider = self;
    QCloudCOSXMLEndPoint *endpoint = [[QCloudCOSXMLEndPoint alloc] init];
    endpoint.regionName = @"region";
    endpoint.useHTTPS = YES;
    configuration.endpoint = endpoint;

    [QCloudCOSXMLService registerDefaultCOSXMLWithConfiguration:configuration];
    [QCloudCOSTransferMangerService registerDefaultCOSTransferMangerWithConfiguration:configuration];
```

### What should I do if the error `Default COSXMLService already exists. To use new configurations, re-register using registerCOSXMLWithConfiguration:withKey:` is thrown after I integrated the SDK?

**Cause**: In the SDK, different `COSXMLService` instances correspond to different configurations (for the configurations, see relevant attributes). For example, setting `regionName` to `guangzhou` and `beijing` indicates two different configurations, where two services need to be registered. If you already used `ap-guangzhou` to register a service and then set `region` to `ap-guangzhou` to register again, this error will occur.

**Solution**:
1. The default service uses `registerDefaultCOSXMLWithConfiguration:` and the key does not need to be specified.
2. Use the following code to register a new service:
```iOS
// Determine whether the key to register exists.
    if(![QCloudCOSXMLService hasServiceForKey:@"Key to register"]){
    // If the key does not exist, register a new service.
        [QCloudCOSXMLService registerCOSXMLWithConfiguration:configuration withKey:@"Key to register"]
    }
```

### What should I do if the `- (void)signatureWithFields:(QCloudSignatureFields *)fileds request:urlRequest:compelete:` proxy is not called after I run the SDK?

**Cause**: This proxy method obtains the key/signature. To give full play to the key validity (calling the signature earlier will cause it to expire sooner), the SDK calls the key only before the request is sent (`task resume`).

**Solution**:
1. Ensure that the class where the proxy method belongs is not terminated before the request is sent. You are advised to implement the proxy method in a singleton class.
2. Check whether `signatureProvider` is configured (for example, configured as `configuration.signatureProvider = self`, in which `self` is the class where the proxy method belongs) after the `QCloudServiceConfiguration` instance is created.
3. After checking the two points above, check whether the request is sent.

### Can the SDK cache or reuse the key? How can I request a new key when the key expires?

The SDK provides `QCloudCredentailFenceQueue` to cache or reuse the key. For more information, see [Getting Started](https://intl.cloud.tencent.com/document/product/436/11280).

### What can I do if the SDK advanced API `QCloudCOSXMLUploadObjectRequest` throws the error `Body of this type is not supported. Supported types are NSData, QCloudFileOffsetBody, and NSURL`?

Currently, the SDK supports the following three types of bodies:
1. NSURL: Local path of the file. The URL is initialized through `[NSURL fileURLWithPath:@"Local path of the object"]`
2. NSData: binary data
3. QCloudFileOffsetBody: multipart body. Since it is the body type for internal use by SDK advanced APIs, you can ignore this type in most cases.

### What should I do if I use the SDK advanced API `QCloudCOSXMLUploadObjectRequest` to upload videos or files from the system photo library, but checkpoint restart fails, throwing the error `The specified Content-Length is zero`?

The SDK supports checkpoint restart only for files in the sandbox. To use the checkpoint restart feature, move your files to the sandbox first.

### What should I do if the size of the file uploaded through an API is different from that of the local file after I integrated the SDK?

Ensure that the local file is not modified after you set the body. For example, if the upload API is called when the file is still being compressed or file write is not completed yet, the SDK will upload the file (using multipart upload) according to the size at the time of upload, causing a file size inconsistency between the COS file and the local file.

### What should I do if I integrate the SDK and call the upload API, but the error “URL in the body is not a local URL” is reported?

**Solution**:
Ensure that the URL starts with “file://”. You can initialize in either of the following two ways:
1. `[NSURL URLWithString:@"file:////var/mobile/Containers/Data/Application/DBPF7490-D5U8-4ABF-A0AF-CC49D6A60AEB/Documents/exampleobject"]`
2. `[NSURL fileURLWithPath:@"/var/mobile/Containers/Data/Application/DBPF7490-D5U8-4ABF-A0AF-CC49D6A60AEB/Documents/exampleobject"]`


### What should I do if I integrate the SDK and call the upload API, but the size of the successfully uploaded file is 0?

**Solution**:
1. If the path of the system photo library is used, check whether you have read permission on the file. An example is that the path `file:///var/mobile/Media/DCIM/101APPLE/` cannot be accessed directly. Photos in this path can only be obtained using the request method in the Photos framework.
2. To make your app compatible with iOS 11, call the `[[PHImageManager defaultManager] requestPlayerItemForVideo:asset options:option resultHandler:^(AVPlayerItem *playerItem, NSDictionary *info) {
    // Move the file to the sandbox in time or save the playerItem.
    }];` method to save the obtained `playerItem`, or move the desired files to the App Sandbox during the callback. The cause of this error is that for iOS11, when `playerItem` is released, read permission on the file specified in `playerItem` will expire, making the size of the uploaded file 0.
3. If the uploaded file is in the App Sandbox, check whether the file is stored in the `tmp` directory (e.g., `/var/mobile/Containers/Data/Application/0BFBB3FE-0FD0-46CB-ADDE-DDE08F6D62C3/tmp/`). Files in `tmp` will be cleared by the system any time. You can move your files to a securer directory in case they are cleared during the upload. For more information about sandbox, see [File System Basics](https://developer.apple.com/library/archive/documentation/FileManagement/Conceptual/FileSystemProgrammingGuide/FileSystemOverview/FileSystemOverview.html).

### What should I do if I use an SDK advanced API for upload, but the error `The MD5 checksum is inconsistent with the local file. Check whether the file is modified during the upload. During multipart uploads, the MD5 checksum of each uploaded part will be verified against the local file. Any inconsistency will cause an error` is reported?

**Cause**: If you use the SDK to upload a file greater than 1 MB, the file will be divided into multiple 1-MB parts and uploaded using multipart upload. After all parts are uploaded, the value of the backend-returned `ETag` will be compared with that of local parts. If there is any inconsistency, this error will be thrown.

**Solution**: Check whether the file is modified during the upload.


### Can I access the SDK with a CDN acceleration endpoint?

Yes. For detailed directions, see the SDK documentation for your programming language.

### How can I set the request timeout in the SDK?

**Solution**: SDK 5.7.0 and later versions support customizing request timeout as follows:
1. Initialize `QCloudServiceConfiguration *config = [QCloudServiceConfiguration new]`.
2. Set the `timeoutInterval` attribute of `config`, for example, `.timeoutInterval = 30;`.


### What should I do if the iOS SDK crashes?

Check whether you are using the latest version. If not, we recommend you update to the latest SDK version. For the latest iOS SDK, see [qcloud-sdk-ios](https://github.com/tencentyun/qcloud-sdk-ios).

### What should I do if the `Undefined symbols for architecture arm64: "_ne10 init dsp", referenced from:` error is reported?

See [Compilation error: Undefined symbols for architecture arm64](https://github.com/LiteAVSDK/Player_iOS/issues/277).
