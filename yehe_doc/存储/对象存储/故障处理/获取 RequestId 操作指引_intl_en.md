## Overview

Every time a request is sent to COS, the COS server will generate an ID for the request (i.e., `RequestId`). This document describes how to obtain `RequestId` in different scenarios.

## Through the Console

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5) and click **Bucket List** in the left sidebar to enter the bucket list page.
2. Click the name of the desired bucket.
3. Press F12 on the keyboard to open the developer tool of your browser.
4. Select the **Network** tab.
![](https://main.qcloudimg.com/raw/0a201a890f54bfabc4267e9c86c89338.png)
5. Click the **Download** button on the right of the desired object. Then, in the developer tools, enter the filename in the **Filter** text box, select the file, and click **Headers**. You can then find `RequestId` from **Response Headers**.
![](https://main.qcloudimg.com/raw/9da8afe99d7e6c7c5f0b77f3c1c48861.png)

## From an Unsuccessful Access

When you fail to access an object, you can obtain the **RequestId** from the XML file returned.
![](https://main.qcloudimg.com/raw/e0d4149121fb0022640465ff690810e1.png)

You can also obtain it as follows:
1. Press F12 on the keyboard to open the developer tool of your browser.
2. Select the **Network** tab and choose **All**. You can then find `RequestId` from **Response Headers**.
![](https://main.qcloudimg.com/raw/ac6902c6ac615a9ec2978a5999a49073.png)

## Using SDKs

As SDKs contain too many APIs, this document only uses **object upload** as an example for all SDKs to show how to obtain the `RequestId` of the current operation.

### Using the .NET SDK

```
try
{
 string bucket = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID
 string cosPath = "test.cs"; // Object key
 byte[] data = System.Text.Encoding.Default.GetBytes("Hello COS"); // Binary data
 PutObjectRequest putObjectRequest = new PutObjectRequest(bucket, cosPath, data);
 
 PutObjectResult result = cosXml.PutObject(putObjectRequest);
 string requestId = result.responseHeaders.GetValueOrDefault("x-cos-request-id")[0];
 Console.WriteLine(requestId);
}
catch (COSXML.CosException.CosClientException clientEx)
{
 // Request failed
 Console.WriteLine("CosClientException: " + clientEx);
}
catch (COSXML.CosException.CosServerException serverEx)
{
 // Request failed
 Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```

 

### Using the Go SDK

```
package main
 
import (
   "context"
   "net/http"
   "net/url"
   "os"
   "strings"
   "github.com/tencentyun/cos-go-sdk-v5"
)
 
func main() {
   // Replace examplebucket-1250000000 and COS_REGION with the actual information
   u, _ := url.Parse("https://examplebucket-1250000000.cos.COS_REGION.myqcloud.com")
   b := &cos.BaseURL{BucketURL: u}
   c := cos.NewClient(b, &http.Client{
       Transport: &cos.AuthorizationTransport{
           SecretID:  "SECRETID",
           SecretKey:    "SECRETKEY",
       },
   })
   // An object key is the unique identifier of an object in a bucket
   // For example, in the access domain name `examplebucket-1250000000.cos.COS_REGION.myqcloud.com/test.go`, the object key is `test.go`.
   name := "test.go"
   // 1. Upload the object with a string.
   f := strings.NewReader("Hello COS")
 
   _, err := c.Object.Put(context.Background(), name, f, nil)
   if err != nil {
       // The error message contains the RequestId field.
       panic(err)
   }
   requestId := response.Header.Get("X-Cos-Request-Id")
   fmt.Println(requestId)
}
```

### Using the Java SDK

```
// 1. Initialize the user credentials (secretId, secretKey).
String secretId = "SECRETID";
String secretKey = "SECRETKEY";
COSCredentials cred = new BasicCOSCredentials(secretId, secretKey);
// 2. Set the bucket region. For abbreviations of COS regions, please visit https://cloud.tencent.com/document/product/436/6224.
// `clientConfig` contains the set methods to set region, HTTPS (HTTP by default), timeout, and proxy. For detailed usage, please see the source code or the FAQs about the SDK for Java.
Region region = new Region("COS_REGION");
ClientConfig clientConfig = new ClientConfig(region);
// The HTTPS protocol is recommended.
clientConfig.setHttpProtocol(HttpProtocol.https);
// 3. Generate a COS client.
COSClient cosClient = new COSClient(cred, clientConfig);
// Enter the bucket name in the format of `BucketName-APPID`
String bucketName = "examplebucket-1250000000";
 
String content = "Hello COS";
String key = "test.java";
PutObjectResult putObjectResult = cosClient.putObject(bucketName, key, content);
String requestId = putObjectResult.getRequestId();
System.out.println(requestId);
```

 

### Using the JavaScript SDK

```
cos.putObject({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'COS_REGION',    /* Required */
    Key: 'test.js',              /* Required */
    StorageClass: 'STANDARD',
    Body: 'Hello COS',
    onProgress: function(progressData) {
        console.log(JSON.stringify(progressData));
    }
}, function(err, data) {
    var requestId = (err || data).headers['x-cos-request-id'];
    console.log(requestId );
});
```

 

### Using the Node.js SDK

```
var COS = require('cos-nodejs-sdk-v5');
var cos = new COS({
    SecretId: 'SECRETID',
    SecretKey: 'SECRETKEY'
});
 
cos.putObject({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'COS_REGION',    /* Required */
    Key: 'test.nodejs',              /* Required */
    StorageClass: 'STANDARD',
    Body: Buffer.from('Hello COS'),
    onProgress: function(progressData) {
        console.log(JSON.stringify(progressData));
    }
}, function(err, data) {
    var requestId = (err || data).headers['x-cos-request-id'];
    console.log(requestId );
});
```

### Using the WeChat Mini Program SDK

```
var COS = require('cos-wx-sdk-v5');
var cos = new COS({
    SecretId: 'SECRETID',
    SecretKey: 'SECRETKEY'
});
 
cos.putObject({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'COS_REGION',    /* Required */
    Key: 'test.js',              /* Required */
    StorageClass: 'STANDARD',
    Body: 'Hello COS',
    onProgress: function(progressData) {
        console.log(JSON.stringify(progressData));
    }
}, function(err, data) {
    var requestId = (err || data).headers['x-cos-request-id'];
    console.log(requestId );
});
```

 

### Using the PHP SDK

```
$secretId = "SECRETID"; // "SecretId of your Tencent Cloud API key";
$secretKey = "SECRETKEY"; // "SecretKey of your Tencent Cloud API key";
$region = "COS_REGION"; // Set the default bucket region
$cosClient = new Qcloud\Cos\Client(
   array(
       'region' => $region,
       'schema' => 'https', // Protocol header, which is http by default
       'credentials'=> array(
           'secretId'  => $secretId,
           'secretKey' => $secretKey)));
# Upload a file
## putObject (an API that can upload files of up to 5 GB)
### Upload strings in memory
try {
   $bucket = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID
   $key = "test.php"; // Object key, which is the unique identifier of an object in a bucket
   $result = $cosClient->putObject(array(
       'Bucket' => $bucket,
       'Key' => $key,
       'Body' => 'Hello COS'));
   $requestId = $result['RequestId'];
   print_r($requestId);
} catch (\Exception $e) {
   echo "$e\n";
}
```


### Using iOS SDK

```
QCloudCOSXMLUploadObjectRequest* put = [QCloudCOSXMLUploadObjectRequest new];
/** Path of the local file. Ensure that the URL starts with "file://" in the following format:
1. [NSURL URLWithString:@"file:////var/mobile/Containers/Data/Application/DBPF7490-D5U8-4ABF-A0AF-CC49D6A60AEB/Documents/exampleobject"]
2. [NSURL fileURLWithPath:@"/var/mobile/Containers/Data/Application/DBPF7490-D5U8-4ABF-A0AF-CC49D6A60AEB/Documents/exampleobject"]
*/
NSURL* url = [NSURL fileURLWithPath:@"file URL"];
// Bucket name in the format of BucketName-Appid, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
put.bucket = @"examplebucket-1250000000";
// Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "video/xxx/movie.mp4"
put.object = @"exampleobject";
// Content of the object to be uploaded. You can pass variables of the `NSData*` or `NSURL*` type
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
[put setFinishBlock:^(QCloudUploadObjectResult *result, NSError *error) {
    // Obtain requestId
   [result.__originHTTPURLResponse__.allHeaderFields objectForKey:@"x-cos-request-id"]
}];
[put setInitMultipleUploadFinishBlock:^(QCloudInitiateMultipartUploadResult *
                                        multipleUploadInitResult,
                                        QCloudCOSXMLUploadObjectResumeData resumeData) {
    // This block will be called back after the Initiate Multipart Upload operation is complete so you can get resumeData and the uploadId.
    NSString* uploadId = multipleUploadInitResult.uploadId;
}];
[[QCloudCOSTransferMangerService defaultCOSTransferManager] UploadObject:put];
```

