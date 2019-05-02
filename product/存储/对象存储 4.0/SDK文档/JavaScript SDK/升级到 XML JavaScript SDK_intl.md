If you have carefully compared the documentations of JSON JavaScript SDK and XML JavaScript SDK, you can find that the latter is not simply an incremental update version of the former. XML JavaScript SDK has made great improvements in architecture, availability and security, as well as in usability, robustness and performance. If you want to upgrade to XML JavaScript SDK, refer to the following instructions.

## Feature Comparison

| Feature | XML JavaScript SDK | JSON JavaScript SDK |
| -------------- | :----------------------------------------------------------: | :----------------------------------------------------------: |
| File upload | Upload of local files and string contents is supported.<br>Existing files are overwritten by default.<br/>Batch upload is supported for multipart upload.<br>Intelligent selection of upload mode: File size is limited to 5 GB in a simple upload;<br>File size is limited to 48.82 TB (50,000 GB) in a multipart upload. | Only local file upload is supported.<br>You can select whether to overwrite existing files.<br/>Simple upload is used for files smaller than or equal to 20 MB. Otherwise, multipart upload is used.<br>File size is limited to 20 MB in a simple upload.<br>File size is limited to 64 GB in a multipart upload. |
| File deletion | Batch deletion is supported. | Only deletion of a single file is supported. |
| Basic operations on buckets | Create a bucket<br>Get a bucket<br>Delete a bucket | Not supported |
| Operations on bucket ACLs | Set bucket ACL<br>Get bucket ACL<br>Delete bucket ACL | Not supported |
| Bucket lifecycle | Create bucket lifecycle<br>Get bucket lifecycle<br>Delete bucket lifecycle | Not supported |
| Directory operations | No APIs are provided separately. | Create a directory<br>Query a directory<br>Delete a directory |
| Use temporary keys | Temporary keys are supported and recommended. | Temporary keys are not supported. |

## Upgrade Procedure

#### 1. Update JavaScript SDK

XML JavaScript SDK is published in the [npm](https://www.npmjs.com/package/cos-js-sdk-v5) repository. You are recommended to install a dependency package using npm.

```js
npm install cos-js-sdk-v5
```

You can also download the js file in the github source code [dist/cos-js-sdk-v5.min.js](https://github.com/tencentyun/cos-js-sdk-v5/tree/master/dist), and add page HTML through a script tag.

```html
<script src="./cos-js-sdk-v5.min.js"></script>
```

#### 2. Change the bucket name and the abbreviations of available regions

The bucket name and the abbreviations of available regions in XML JavaScript SDK are different from those in JSON JavaScript SDK. You need to make changes accordingly.

#### Bucket

The name of an XML JavaScript SDK bucket consists of a user-defined string and an APPID that are connected by a dash ("-").
For example, `examplebucket-1250000000`, where `examplebucket` is a user-defined string, and `1250000000` is an APPID.

> ?APPID is one of the Tencent Cloud account IDs, and is used to associate with cloud resources. After applying for a Tencent Cloud account successfully, you will be assigned an APPID automatically. APPID can be found in **Account Info** on the [Tencent Cloud Console](https://console.cloud.tencent.com/).

Refer to the following sample code to set a bucket:

```js
cos.getBucket({
    Bucket: 'examplebucket-1250000000',
    Region: 'ap-beijing',
}, function (err, data) {
    console.log(err || data);
});
```

#### Abbreviations of available regions for buckets

The abbreviations of available regions for XML JavaScript SDK buckets have changed. See the following table for region abbreviations in JSON JavaScript SDK and XML JavaScript SDK:

| Region | Abbreviation in XML SDK | Abbreviation in JSON SDK |
| ---------------- | ---------------- | ----------- |
| Beijing Zone 1 (North China) | ap-beijing-1 | tj |
| Beijing | ap-beijing | bj |
| Shanghai (East China) | ap-shanghai | sh |
| Guangzhou (South China) | ap-guangzhou | gz |
| Chengdu (Southwest) | ap-chengdu | cd |
| Chongqing | ap-chongqing | None |
| Singapore | ap-singapore | sgp |
| Hong Kong | ap-hongkong | hk |
| Toronto | na-toronto | ca |
| Frankfurt | eu-frankfurt | ger |
| Mumbai | ap-mumbai | None |
| Seoul | ap-seoul | None |
| Silicon Valley | na-siliconvalley | None |
| Virginia | na-ashburn | None |
| Bangkok | ap-bangkok | None |
| Moscow | eu-moscow | None |

You can also refer to [Region and Access Domain Name](https://cloud.tencent.com/document/product/436/6224).

When calling each method, set the abbreviation of the region where the bucket resides in the parameter `Region`:

```java
cos.headBucket({
    Bucket: 'examplebucket-1250000000,
    Region: 'ap-beijing',
}, function (err, data) {
    console.log(err || data);
});
```

#### 3. Change APIs

After JSON JavaScript SDK is upgraded to XML JavaScript SDK, the APIs for some operations have changed. Make corresponding changes based on your actual needs.

In addition, we have encapsulated APIs to make it easier to use the SDK. For more information, see [Sample Code](https://github.com/tencentyun/cos-js-sdk-v5/tree/master/demo) and [API documentation](https://cloud.tencent.com/document/product/436/12260).

Here are the main changes of APIs:

**1) No directory API**

No separate directory API is provided in XML SDK. As COS comes with no folders and directories, it will not create a "project" folder for uploading the object `project/a.txt`. To make it easier for you to get started, COS simulates the display mode of "folder" or "directory" in the console and graphical tools such as COSBrowser. This is realized by creating an empty object with a key value of `project/` and displaying it as a traditional folder.

For example: When you upload the object `project/doc/a.txt`, the delimiter `/` simulates the display mode of "folder", and you can see the folders "project" and "doc" on the console. The folder "doc" is displayed under the folder "project" and contains the file "a.txt".

Therefore, in a use case for file upload only, you can directly upload files without creating a folder first. If a folder is allowed in a use case, the feature of creating a folder should be supported. You can upload a 0 KB file whose path ends with `/`. When you call the API GetBucket, you can use the file as a folder.

**2) Temporary keys are used for authentication**

As there is a security risk in putting a key in the frontend code and the permission granted to the frontend is not well controlled if the signature is computed in the backend, XML JavaScript SDK recommends that you use a temporary key. For specific code, see the following example:

```js
var Bucket = 'examplebucket-1250000000';
var Region = 'ap-beijing';
var cos = new COS({
    getAuthorization: function (options, callback) {
        var url = 'http://example.com/sts.php';
        var xhr = new XMLHttpRequest();
        xhr.open('GET', url, true);
        xhr.onload = function (e) {
            try {
                var data = JSON.parse(e.target.responseText);
                var credentials = date.credentials;
            } catch (e) {
            }
            callback({
                TmpSecretId: credentials.tmpSecretId,
                TmpSecretKey: credentials.tmpSecretKey,
                XCosSecurityToken: credentials.sessionToken,
                ExpiredTime: data.expiredTime,
            });
        };
        xhr.send();
    }
});
cos.putObject({
    Bucket: Bucket,
    Region: Region,
    Key: file.name,
    Body: file,
    onProgress: function (progressData) {
        console.log('Uploading', JSON.stringify(progressData));
    },
}, function (err, data) {
    console.log(err, data);
});
```

If you still compute the signature manually in the backend and return it to the frontend, note that the signature algorithm has changed. One-time signatures and multiple-time signatures are no longer used. Instead, you can set a validity period of the signature to ensure security. For more information, see [XML Request Signature](https://cloud.tencent.com/document/product/436/7778).

**3) Parameters and uniform format of returned results**

A parameter is an object. Except for some tool-based methods, the returned results for APIs are an error message or a success result obtained through a callback, as shown in the following example:

```js
cos.putObject({
    Bucket: 'examplebucket-1250000000',
    Region: 'ap-beijing-1',
    Key: '1.txt',
}, function (err, data) {
    console.log(err || data);
});
```

**4) New APIs**

The following APIs are added in XML JavaScript SDK, and they can be called as needed:

- Bucket operations, such as getService, putBucket, and getBucket.
- Operations on bucket ACLs, such as getBucketAcl, and putBucketAcl.
- Operations on bucket policies, such as putBucketPolicy, getBucketPolicy and deleteBucketPolicy.
- Operations on bucket lifecycle, such as putBucketLifecycle, getBucketLifecycle and deleteBucketLifecycle.
- Operations on object ACLs: getObjectAcl, and putObjectAcl.
- Object replication operations: putObjectCopy, and sliceCopyFile.
- Tool-based method: getObjectUrl.
- Object upload queue: pauseTask, restartTask, cancelTask, getTaskList methods and list-update event.

For more information, see [JavaScript SDK API documentation](https://cloud.tencent.com/document/product/436/12260).

