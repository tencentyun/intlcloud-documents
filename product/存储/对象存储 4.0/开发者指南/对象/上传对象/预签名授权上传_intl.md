## Use Cases

All buckets and objects are private by default. If you want any third party to be able to upload an object to your bucket, but you don't want them to use CAM account or temporary keys, signatures can be provided by pre-signed URLs for temporary upload operations. Anyone who receives a valid pre-signed URL can upload an object.

When creating a pre-signed URL, you can include keys in your signature to specify the allowed path to upload. You can also specify an HTTP method to restrict specific object operations, such as upload, download and deletion. Besides, the validity period of pre-signed URLs can be provided in SDKs to ensure that expired URLs will not be used by any unauthorized party.

## Directions

### Via REST API

You can use the REST API to initiate a GET Object request. See [GET Object Documentation](https://intl.cloud.tencent.com/document/product/436/7753).

### Via Java SDK

This method is provided in the Java SDK for COS. See the [Generating a Pre-Signed URL section in Java SDK API Documentation](https://intl.cloud.tencent.com/document/product/436/12263#.E7.94.9F.E6.88.90.E9.A2.84.E7.AD.BE.E5.90.8D.E9.93.BE.E6.8E.A5).

#### Description

1. Initialize client cosclient.
2. Execute the generatePresignedUrl method to get the upload signature and pass PUT in the http method parameter.

#### Sample codes

The following sample code demonstrates how to generate a pre-signed upload URL and upload objects using the URL:

```java
// 1. Initialize user authentication information (secretId, secretKey).
COSCredentials cred = new BasicCOSCredentials("AKIDXXXXXXXX", "1A2Z3YYYYYYYYYY");
// 2. Set the region where the bucket resides. For the abbreviations of COS regions, see https://cloud.tencent.com/document/product/436/6224.
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing-1"));
// 3. Generate the COS client.
COSClient cosclient = new COSClient(cred, clientConfig);
// The bucket name must contain appid.
String bucketName = "mybucket-1251668577";

String key = "aaa.txt";
Date expirationTime = new Date(System.currentTimeMillis() + 30 * 60 * 1000);
// Generate a pre-signed upload URL.
URL url = cosclient.generatePresignedUrl(bucketName, key, expirationTime, HttpMethodName.PUT);

// Upload a file using a pre-signed URL.
try {
    HttpURLConnection connection = (HttpURLConnection) url.openConnection();
    connection.setDoOutput(true);
    connection.setRequestMethod("PUT");
    OutputStreamWriter out = new OutputStreamWriter(connection.getOutputStream());
    // Write the data to be uploaded. 
    out.write("This text uploaded as object.");
    out.close();
    int responseCode = connection.getResponseCode();
    System.out.println("Service returned response code " + responseCode);
} catch (ProtocolException e) {
    e.printStackTrace();
} catch (IOException e) {
    e.printStackTrace();
}

cosclient.shutdown();
```

### Via Node.js SDK

#### Description

1. Install the npm dependency package:
```shell
npm i cos-nodejs-sdk-v5
```

2. Create the test file test.js, and execute ```node test.js``` in the command line.

#### Sample codes

```javascript
var COS = require('cos-nodejs-sdk-v5');
var request = require('request');

var SecretId = 'AKIDxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx'; // Replaced with user's SecretId
var SecretKey = 'xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx';    // Replaced with user's SecretKey
var Bucket = 'test-1250000000';                        // Replaced with user's Bucket
var Region = 'ap-guangzhou';                           // Replaced with user's Region

var cos = new COS({SecretId: SecretId, SecretKey: SecretKey});
var url = cos.getObjectUrl({
    Bucket: Bucket,
    Region: Region,
    Method: 'PUT',
    Key: '1.jpg', // Replace the URL of a file to be downloaded.
    Expires: 60
});
console.log(url);

// Upload a file
request({
    method: 'PUT',
    url: url,
    body: fs.readFileSync('./1.jpg'),
}, function (err, response, body) {
    console.log(response.statusCode);
    console.log(response.headers.etag);
    console.log(body);
});
```

