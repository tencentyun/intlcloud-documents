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
           SecretKey: "SECRETKEY",
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
// Enter the bucket name in the format of BucketName-APPID.
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
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',    /* Required */
    Key: 'test.js',              /* Required */
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

 

### Using the Node.js SDK

```
var COS = require('cos-nodejs-sdk-v5');
var cos = new COS({
    SecretId: 'SECRETID',
    SecretKey: 'SECRETKEY'
});
 
cos.putObject({
    Bucket: 'examplebucket-1250000000', /*Required*/
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

 

### Using the PHP SDK

```
$secretId = "SECRETID"; // "SecretId of your Tencent Cloud API key";
$secretKey = "SECRETKEY"; // "SecretKey of your Tencent Cloud API key";
$region = "COS_REGION"; // Set the default bucket region
$cosClient = new Qcloud\Cos\Client(
   array(
       'region' => $region,
       'schema' => 'https', // Protocol header; http by default
       'credentials'=> array(
           'secretId'  => $secretId ,
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


### Using the Python SDK

```
# -*- coding=utf-8
# APPID has been removed from the configuration. Please add the APPID to the Bucket parameter in the format of BucketName-APPID.
# 1. Set user configuration, including secretId, secretKey, and region.
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client
import sys
import logging
logging.basicConfig(level=logging.INFO, stream=sys.stdout)
secret_id = 'SECRETID'      # Replace it with your secretId.
secret_key = 'SECRETKEY'      # Replace it with your secretKey.
region = 'COS_REGION'     # Replace it with your region.
token = None                # If a temporary key is used, token needs to be passed in. This is optional and is left empty by default.
scheme = 'https'            # Specify whether to use HTTP or HTTPS protocol to access COS. This is optional and is https by default.
config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token, Scheme=scheme)
# 2. Get the client object.
client = CosS3Client(config)
# Upload a byte stream with simple upload.
response = client.put_object(
   Bucket='examplebucket-1250000000',     # Replace it with your bucket name.
   Body=b'Hello COS',
   Key='test.py',
   EnableMD5=False
)
request_id = response['X-Cos-Request-Id']
print(request_id)
```
