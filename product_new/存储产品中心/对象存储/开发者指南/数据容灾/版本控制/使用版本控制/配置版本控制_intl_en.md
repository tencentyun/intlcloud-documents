## Use Cases
By enabling versioning, you can store multiple versions of an object in a bucket and retrieve, delete, or restore a specified version.
For more information, see [Versioning Overview](https://cloud.tencent.com/document/product/436/19883).

>Only the root account and authorized sub-accounts can configure the versioning state of a bucket.

## Directions

### Using the REST API

You can use the REST API to configure versioning and manage objects in buckets with different versioning states. For more information, see the following API documentation:
- [PUT Bucket versioning](/document/product/436/19889)
- [GET Buket versioning](/document/product/436/19888)
- [PUT Object](https://cloud.tencent.com/document/product/436/7749)
- [GET Object](https://cloud.tencent.com/document/product/436/7753)
- [DELETE Object](/document/product/436/7743)

### Using the Android SDK

You can find information on this method in COS Android SDK. Please see [Bucket Management](https://cloud.tencent.com/document/product/436/34537) in Android SDK documentation.

#### Configuring Versioning

Steps:
1. Call the `PutBucketVersioningRequest` constructor to instantiate the `PutBucketVersioningRequest` object.
2. Call the `putBucketVersioning(PutBucketVersioningRequest)` sync method of `CosXmlService` to pass in `PutBucketVersioningRequest` and return the `PutBucketVersioningResult` object (or call the `putBucketVersionAsync` method to pass in `PutBucketVersioningRequest` and `CosXmlResultListener` for async callback).

Sample code:
```java
String bucket = "bucket";
PutBucketVersioningRequest request = new PutBucketVersioningRequest(bucket);
request.setEnableVersion(true);// Enable
request.setSign(signDuration,null,null); // Signature
try {
PutBucketVersioningResult result = cosXmlService.putBucketVersioning(request);
Log.w("TEST","success");
} catch (CosXmlClientException e) {
Log.w("TEST","CosXmlClientException =" + e.toString());
} catch (CosXmlServiceException e) {
Log.w("TEST","CosXmlServiceException =" + e.toString());
}
// **Use the async callback to make requests**
/**

cosXmlService.putBucketVersionAsync(request, new CosXmlResultListener() {
@Override
public void onSuccess(CosXmlRequest cosXmlRequest, CosXmlResult cosXmlResult) {
Log.w("TEST","success");
}
@Override
public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException 
serviceException)  {
String errorMsg = clientException != null ? clientException.toString() : serviceException.toString();
Log.w("TEST",errorMsg);
}
});
*/
```
#### Querying Versioning

Steps:
1. Call the `GetBucketVersioningRequest` constructor to instantiate the `GetBucketVersioningRequest` object.
2. Call the `getBucketVersioning(GetBucketVersioningRequest)` sync method of `CosXmlService` to pass in `GetBucketVersioningRequest` and return the `GetBucketVersioningResult` object (or call the `getBucketVersioningAsync` method to pass in `GetBucketVersioningRequest` and `CosXmlResultListener` for async callback).

Sample code:
```java
String bucket = "bucket";
GetBucketVersioningRequest request = new GetBucketVersioningRequest(bucket);
request.setSign(signDuration,null,null); // Signature
try {
GetBucketVersioningResult result = cosXmlService.getBucketVersioning(request);
Log.w("TEST","success");
} catch (CosXmlClientException e) {
Log.w("TEST","CosXmlClientException =" + e.toString());
} catch (CosXmlServiceException e) {
Log.w("TEST","CosXmlServiceException =" + e.toString());
}
// **Use the async callback to make requests**
/**
cosXmlService.getBucketVersioningAsync(request, new CosXmlResultListener() {
@Override
public void onSuccess(CosXmlRequest cosXmlRequest, CosXmlResult cosXmlResult) {
Log.w("TEST","success");
}
@Override
public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException 
serviceException)  {
String errorMsg = clientException != null ? clientException.toString() : serviceException.toString();
Log.w("TEST",errorMsg);
}
});
*/
```

### Using the iOS SDK

You can find information on this method in COS iOS SDK. Please see [Bucket Management](https://cloud.tencent.com/document/product/436/34108) in iOS SDK documentation.

#### Configuring Versioning

Steps:
1. Generate a `QCloudPutBucketVersioningRequest` instance and enter the corresponding configuration to suspend or enable versioning. For specific settings, see the sample code below.
2. Call the `PutBucketVersioning` method of `QCloudCOSXMLService` to initiate a request.

Sample code:
```
QCloudPutBucketVersioningRequest* request = [[QCloudPutBucketVersioningRequest alloc] init];
 request.bucket = @"testBucket-123456789";
 QCloudBucketVersioningConfiguration* configuration = [[QCloudBucketVersioningConfiguration alloc] init];
 request.configuration = configuration;
 configuration.status = QCloudCOSBucketVersioningStatusEnabled;
 [request setFinishBlock:^(id outputObject, NSError* error) {
   // Set the completion callback
 }];
 [[QCloudCOSXMLService defaultCOSXML] PutBucketVersioning:request];

```

#### Querying Versioning

Steps:

1. Generate a `QCloudetBucketVersioningRequest` instance and set the bucket attributes.
2. Call the `GetBucketVersioning` method of `QCloudCOSXMLService` to initiate a request.

Sample code:

```
QCloudGetBucketVersioningRequest* request = [[QCloudGetBucketVersioningRequest alloc] init];
request.bucket = @"testBucket-123456789";
[request setFinishBlock:^(QCloudBucketVersioningConfiguration* result, NSError* error) {
 // Set the completion callback
}];
[[QCloudCOSXMLService defaultCOSXML] GetBucketVersioning:request];
```

#### Uploading an Object

Steps:

1. After versioning is enabled, a VersionID will be automatically generated for an uploaded object.
2. After an object is uploaded successfully, the VersionID will be returned in `QCloudUploadObjectResult`.

Sample code:
```
QCloudCOSXMLUploadObjectRequest* put = [QCloudCOSXMLUploadObjectRequest new];

   NSURL* url = /*file URL*/;
   put.object = @"filename.jpg";
   put.bucket = @"test-123456789";
   put.body =  url;
   [put setSendProcessBlock:^(int64_t bytesSent, int64_t totalBytesSent, int64_t totalBytesExpectedToSend) {
       NSLog(@"upload %lld totalSend %lld aim %lld", bytesSent, totalBytesSent, totalBytesExpectedToSend);
   }];
   [put setFinishBlock:^(QCloudUploadObjectResult* result, NSError* error) {
   if ( nil == error) {
        NSString *versionID = result.versionID;// Get versionID here
      }
   }];
   [[QCloudCOSTransferMangerService defaultCOSTransferManager] UploadObject:put];
```

#### Downloading an Object

Steps:

1. Generate a `QCloudGetObjectRequset` instance and set the corresponding attributes such as bucket and object attributes.
2. Call the `GetBucketVersioning` method of `QCloudCOSXMLService` to initiate a request.

Sample code:
```
QCloudGetObjectRequest* request = [QCloudGetObjectRequest new];
// Set the download path URL; if you set a URL, the file will be downloaded to the specified path; otherwise, the file will be downloaded to the memory and stored in the outputObject of the finishBlock.
request.downloadingURL = [NSURL URLWithString:QCloudTempFilePathWithExtension(@"downding")];
request.object = @"your Object-Key";
request.bucket = @"testBucket-123456789";
request.versionID = @"12345678910";
[request setFinishBlock:^(id outputObject, NSError *error) {
  //additional actions after finishing
}];
  [request setDownProcessBlock:^(int64_t bytesDownload, int64_t totalBytesDownload, int64_t totalBytesExpectedToDownload) {
   // Download progress
  }];
  [[QCloudCOSXMLService defaultCOSXML] GetObject:request];
```

#### Deleting Objects

Steps:

1. Generate a `QCloudDeleteObjectRequest` instance and set the corresponding attributes such as bucket and object attributes.
2. Set the versionID or deleteMarker.
3. Call the `DeleteObject` method of `QCloudCOSXMLService` to initiate a request.

Sample code:
```
QCloudDeleteObjectRequest* deleteObjectRequest = [QCloudDeleteObjectRequest new];
deleteObjectRequest.bucket = <#object#>;
deleteObjectRequest.object = <#bucket#>;
deleteObjectRequest.versionId = @"versionID"
[deleteObjectRequest setFinishBlock:^(id outputObject, NSError *error) {
 if (nil == error) {
    <#success call back#>
} else {
<#fail call back#>
}
}];
[[QCloudCOSXMLService defaultCOSXML] DeleteObject:deleteObjectRequest];
```
