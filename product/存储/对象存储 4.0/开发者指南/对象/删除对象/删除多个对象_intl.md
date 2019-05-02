## Use Cases

Tencent Cloud COS supports batch deletion of multiple objects. You can delete objects in batches via the console, APIs, and SDKs.

By default, when the deletion task is completed, a null is returned. If an error occurs, an error message is returned.

>Note: A maximum of 1,000 objects can be deleted in a single request. To delete more objects, split the list and send the request separately.

## Directions

### Via the COS Console
You can delete multiple objects in batches on the COS Console. See [Deleting Object](https://cloud.tencent.com/document/product/436/13323) in Console Guide.

### Via REST API

You can use the REST API to initiate a DELETE Multiple Objects request. See [Delete Multiple Objects](https://cloud.tencent.com/document/product/436/8289).

### Via Java SDK

This method is provided in the Java SDK for COS. See the [Delete Object section in Java SDK API Documentation](https://cloud.tencent.com/document/product/436/12263#delete-object).

#### Description

1. Initialize client cosclient.
2. Execute the deleteObjects method to delete objects. The key names of objects to be deleted are required.
3. If the execution is successful, the DeleteObjectsResult object containing all deleted keys is returned. If the execution fails partially (for example, you don't have the permission to delete an object), the MultiObjectDeleteException is returned. If exceptions caused by other failures occur, CosClientException or CosServiceException is returned. For more information, see Description on SDK Exceptions.

#### Sample codes

(1) The following sample codes show how to delete multiple objects (only one version):

```java
// 1. Initialize user authentication information (secretId, secretKey).
COSCredentials cred = new BasicCOSCredentials("AKIDXXXXXXXX", "1A2Z3YYYYYYYYYY");
// 2. Set the region where the bucket resides. For the abbreviations of COS regions, see https://cloud.tencent.com/document/product/436/6224.
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing-1"));
// 3. Generate the COS client.
COSClient cosclient = new COSClient(cred, clientConfig);
// The bucket name must contain appid.
String bucketName = "mybucket-1251668577";

DeleteObjectsRequest deleteObjectsRequest = new DeleteObjectsRequest(bucketName);
// Set the list of keys to be deleted. A maximum of 1,000 keys can be deleted at a time.
ArrayList<KeyVersion> keyList = new ArrayList<>();
// Pass the names of files to be deleted.
keyList.add(new KeyVersion("aaa.txt"));
keyList.add(new KeyVersion("bbb.mp4"));
keyList.add(new KeyVersion("ccc/ddd.jpg"));
deleteObjectsRequest.setKeys(keyList);

// Delete files in batches.
try {
    DeleteObjectsResult deleteObjectsResult = cosclient.deleteObjects(deleteObjectsRequest);
    List<DeletedObject> deleteObjectResultArray = deleteObjectsResult.getDeletedObjects();
} catch (MultiObjectDeleteException mde) { // If the execution fails partially, MultiObjectDeleteException is returned.
    List<DeletedObject> deleteObjects = mde.getDeletedObjects();
    List<DeleteError> deleteErrors = mde.getErrors();
} catch (CosServiceException e) { // If other errors occur, such as parameter error or failed authentication, CosServiceException is thrown.
    e.printStackTrace();
} catch (CosClientException e) { // If a client error occurs, such as COS connection failure
    e.printStackTrace();
}
```

(2) The following sample codes show how to delete multiple objects (multiple versions):

```java
// 1. Initialize user authentication information (secretId, secretKey).
COSCredentials cred = new BasicCOSCredentials("AKIDXXXXXXXX", "1A2Z3YYYYYYYYYY");
// 2. Set the region of the bucket. Visit https://cloud.tencent.com/document/product/436/6224 to learn about COS region abbreviation.
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing-1"));
// 3. Generate the COS client.
COSClient cosclient = new COSClient(cred, clientConfig);
// The bucket name must contain appid.
String bucketName = "mybucket-1251668577";

DeleteObjectsRequest deleteObjectsRequest = new DeleteObjectsRequest(bucketName);
// Set the list of keys to be deleted. A maximum of 1,000 keys can be deleted at a time.
ArrayList<KeyVersion> keyList = new ArrayList<>();
// Pass the names of files to be deleted.
keyList.add(new KeyVersion("aaa.txt", "axbefagagaxxfafa"));
keyList.add(new KeyVersion("bbb.mp4", "awcafa1faxg0lx"));
keyList.add(new KeyVersion("ccc/ddd.jpg", "kafa1kxxaa2ymh"));
deleteObjectsRequest.setKeys(keyList);

// Delete files in batches.
try {
    DeleteObjectsResult deleteObjectsResult = cosclient.deleteObjects(deleteObjectsRequest);
    List<DeletedObject> deleteObjectResultArray = deleteObjectsResult.getDeletedObjects();
} catch (MultiObjectDeleteException mde) { // If the execution fails partially, MultiObjectDeleteException is returned.
    List<DeletedObject> deleteObjects = mde.getDeletedObjects();
    List<DeleteError> deleteErrors = mde.getErrors();
} catch (CosServiceException e) { // If other errors occur, such as parameter error or failed authentication, CosServiceException is thrown.
    e.printStackTrace();
} catch (CosClientException e) { // If a client error occurs, such as COS connection failure
    e.printStackTrace();
}
```



### Via JavaScript SDK

This method is provided in the JavaScript SDK for COS. See the [Delete Object section in JavaScript SDK API Documentation](https://cloud.tencent.com/document/product/436/12260#delete-object).

#### Description

1. Prepare a signature server and provide the auth.php API for the frontend to get the signature. For more information, see [Example of Backend Signature](https://github.com/tencentyun/cos-js-sdk-v5/tree/master/server).

2. Create the test file test.html and write the following code in it. Put the file on the static server and access it with `http://127.0.0.1/test.html`.

#### Sample codes

The following sample codes show how to delete multiple objects:

```html
<script src="cos-js-sdk-v5.min.js"></script>
<script>
var Bucket = 'test-1250000000'; // Replaced with user's Bucket
var Region = 'ap-guangzhou';    // Replaced with user's Region

// Initialize the instance.
var cos = new COS({
    getAuthorization: function (options, callback) {
        // Obtain the signature asynchronously
        var url = 'auth.php?method=' + options.Method.toLowerCase() + '&pathname=' + encodeURIComponent('/' + (options.Key || ''));
        var xhr = new XMLHttpRequest();
        xhr.open('GET', url, true);
        xhr.onload = function (e) {
            callback(e.target.responseText);
        };
        xhr.send();
    }
});

cos.deleteMultipleObject({
    Bucket: Bucket,
    Region: Region,
    Objects: [
        {Key: '1mb.zip'},
        {Key: '3mb.zip'},
    ]
}, function (err, data) {
    console.log(err || data);
});
</script>
```
### Via Node.js SDK

This method is provided in the Node.js SDK for COS. See the [Delete Object section in Node.js SDK API Documentation](https://cloud.tencent.com/document/product/436/12264#delete-object).

#### Description

1. Install the npm dependency package:
```shell
npm i cos-nodejs-sdk-v5
```

2. Create the test file test.js, and execute ```node test.js``` in the command line.

#### Sample codes

The following sample codes show how to delete multiple objects:

```javascript
var COS = require('cos-nodejs-sdk-v5');

var SecretId = 'AKIDxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx'; // Replaced with user's SecretId
var SecretKey = 'xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx';    // Replaced with user's SecretKey
var Bucket = 'test-1250000000';                        // Replaced with user's Bucket
var Region = 'ap-guangzhou';                           // Replaced with user's Region

var cos = new COS({SecretId: SecretId, SecretKey: SecretKey});
cos.deleteMultipleObject({
    Bucket: Bucket,
    Region: Region,
    Objects: [
        {Key: '1mb.zip'},
        {Key: '3mb.zip'},
    ]
}, function (err, data) {
    console.log(err || data);
});
```
### Via PHP SDK

This method is provided in the PHP SDK for COS. See the [Deleting Files section in PHP SDK API Documentation](https://cloud.tencent.com/document/product/436/12267#.E5.88.A0.E9.99.A4.E6.96.87.E4.BB.B6).

#### Description

1. Initialize client cosClient.
2. Execute deleteObjects to delete multiple objects. The bucket name and key names are required.

#### Sample codes

The following sample codes show how to delete multiple objects:

```php
try {
    $result = $cosClient->deleteObjects(array(
        'Bucket' => 'bucket-125000000',
        'Objects' => array(
            array(
                'Key' => 'string',
            ),
            // ... repeated
        ),
    ));
    print_r($result);
} catch (\Exception $e) {
    echo "$e\n";
}
```
### Via Python SDK

This method is provided in the Python SDK for COS. See the [Deleting Files section in Python SDK API Documentation](https://cloud.tencent.com/document/product/436/12270#.E6.96.87.E4.BB.B6.E4.B8.8B.E8.BD.BD).

#### Description

1. Use the CosConfig class for configuration, and initialize client CosS3Client.
2. Execute the delete_objects() method to delete multiple objects. The bucket name and key names are required.

#### Sample codes

The following sample codes show how to delete multiple objects:

```python
# -*- coding=utf-8
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client

secret_id = 'xxxxxxxx'      # Replaced with user's secretId
secret_key = 'xxxxxxx'      # Replaced with user's secretKey
region = 'ap-beijing-1'     # Replaced with user's Region
token = ''                  # Token is required to use a temporary key. It is optional. Default is empty.

config = CosConfig(Secret_id=secret_id, Secret_key=secret_key, Region=region, Token=token)
client = CosS3Client(config)

bucket = 'testbucket-123456789'
response = client.delete_objects(
    Bucket=bucket,
    Delete={
        "Quiet": "true",
        "Object": [
            {
                "Key": "test1.txt"
            },
            {
                "Key": "test2.txt"
            }
        ]
    }    
)
```

If there are multiple versions, you can specify the parameter VersionId to delete the specific version of the object:
```python
bucket = 'testbucket-123456789'
response = client.delete_objects(
    Bucket=bucket,
    Delete={
        "Quiet": "true",
        "Object": [
            {
                "Key": "test1.txt",
                "VersionId": "MTg0NDY3NDI1NjExNjQwNDUxMzU"
            },
            {
                "Key": "test2.txt",
                "VersionId": "MTg0NDY3NDI1NjExNjQwNDUxMzA"
            }
        ]
    }    
)
```

