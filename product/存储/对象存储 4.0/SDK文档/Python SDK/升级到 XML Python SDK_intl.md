After comparing  Python SDK V4 and XML Python SDK documents, you may find XML Python SDK not only increased the document numbers, but also improved in terms of architecture, availability,  security, usability, robustness and transmission. The following instructions can help you upgrade to XML Python SDK.

## Feature Comparison

The following table compares the main features of JSON Python SDK and XML Python SDK:

| Feature | XML Python SDK | JSON Python SDK |
| -------- | :------------: | :------------------:    |
| File upload | Upload of local files, byte streams and input streams is supported.<br>Existing files are overwritten by default.<br>Intelligent selection of upload mode, and support for resuming upload from breakpoint.<br>File size is limited to 5 GB in a simple upload.<br>File size is limited to 48.82 TB (50,000 GB) in a multipart upload. | Only local file upload is supported.<br>You can select whether to overwrite existing files.<br>You need to manually select simple upload or multipart upload.<br>File size is limited to 20 MB in a simple upload.<br>File size is limited to 64 GB in a multipart upload. |
| Basic operations on buckets | Create a bucket<br>Get a bucket<br>Delete a bucket | Not supported |
| Operations on bucket ACLs | Set bucket ACL<br>Get bucket ACL<br>Delete bucket ACL | Not supported |
| Bucket lifecycle | Create bucket lifecycle<br>Get bucket lifecycle<br>Delete bucket lifecycle | Not supported |
| Directory operations | No APIs are provided separately. | Create a directory<br>Query a directory<br>Delete a directory |


## Upgrade Procedure
Upgrade Python SDK by following the 4 steps below.
**1. Update Python SDK**

You can easily obtain the latest XML Python SDK using the pip command:
```
 pip uninstall qcloud_cos_v4

 pip install -U cos-python-sdk-v5
```

You can also refer to Python SDK [Getting Started](https://intl.cloud.tencent.com/document/product/436/12269) to select a proper installation method.


**2. Change the SDK initialization method**

XML Python SDK adds a CosConfig object to manage your access to COS configurations. You can easily set up information such as access protocol HTTP/HTTPS, and temporary keys. Initialize the SDK as follows.

JSON Python SDK is initialized as follows:

```
secret_id = u'COS_SECRETID'      # Replaced with user's secretId
secret_key = u'COS_SECRETKEY'      # Replaced with user's secretKey
region = 'sh'                # Replaced with user's Region
appid = 100000               # Replaced with user's appid
cos_client = CosClient(appid, secret_id, secret_key, region=region)
```

XML Python SDK is initialized as follows:

```
# appid has been removed from the configuration. Please include the appid in the parameter Bucket. Bucket is in a format of bucketname-appid.
# 1. Set user configuration, including secretId, secretKey and Region
# -*- coding=utf-8
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client
import sys
import logging

logging.basicConfig(level=logging.INFO, stream=sys.stdout)

secret_id = 'COS_SECRETID'      # Replaced with user's secretId
secret_key = 'COS_SECRETKEY'      # Replaced with user's secretKey
region = 'ap-shanghai'      # Replaced with user's Region
token = None                # Token is required to use a temporary key. It is optional. Default is empty.
scheme = 'https'            # Specify that the http/https protocol is used to access COS. It is optional. Default is https.
config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token, Scheme=scheme)
# 2. Obtain client object
client = CosS3Client(config)
```


**3. Change the bucket name and the abbreviations of available regions**

The bucket name and the abbreviations of available regions in XML Python SDK are different from those in JSON Python SDK. You need to make changes accordingly.

**Bucket**
The name of an XML Python SDK bucket consists of a user-defined string and an APPID that are connected by a dash ("-").
For example, `mybucket1-1250000000`, where `mybucket1` is a user-defined string, and `1250000000` is an APPID.
>APPID is one of the Tencent Cloud account IDs, and is used to associate with cloud resources. After applying for a Tencent Cloud account successfully, you will be assigned an APPID automatically. APPID can be found in **Account Info** on the [Tencent Cloud Console](https://console.cloud.tencent.com/).

Refer to the following sample code to set a bucket:
```
bucket = "examplebucket-1250000000"
file_name = "test.txt"
local_path = 'local.txt'
response = client.upload_file(
    Bucket=bucket,
    LocalFilePath=local_path,
    Key=file_name
)
```


**Abbreviations of available regions for buckets**

The abbreviations of available regions for XML Python SDK buckets have changed. During initializing, set the abbreviation of the bucket region in CosConfig. See the following table for region abbreviations in JSON Python SDK and XML Python SDK:

| Region | Abbreviation in XML Python SDK | Abbreviation in JSON Python SDK |
| -------- | ------------ | ---------------------------------------- |
| Beijing Zone 1 (North China) | ap-beijing-1 | tj |
| Beijing | ap-beijing | bj |
| Shanghai (East China) | ap-shanghai | sh |
| Guangzhou (South China) | ap-guangzhou | gz |
| Chengdu (Southwest China) | ap-chengdu | cd |
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


**4. Change APIs**
After JSON Python SDK is upgraded to XML Python SDK, the APIs for some operations have changed. Make corresponding changes based on your actual needs. In addition, we have encapsulated APIs to make it easier to use the SDK. For more information, see our examples and [API Documentation](https://intl.cloud.tencent.com/document/product/436/12269).
There are four changes of APIs:

**1) No directory API**

No separate directory API is provided in XML SDK. As COS comes with no folders and directories, it will not create a "project" folder for uploading the object `project/a.txt`. To make it easier for you to get started, COS simulates the display mode of "folder" or "directory" in the console and graphical tools such as COS browser. This is realized by creating an empty object with a key value of `project/` and displaying it as a traditional folder.

For example: When you upload the object `project/doc/a.txt`, the delimiter `/` simulates the display mode of "folder", and you can see the folders "project" and "doc" on the console. The folder "doc" is displayed under the folder "project" and contains the file "a.txt".

Therefore, in a use case for file upload only, you can directly upload files without creating a folder first. If a folder is allowed in a use case, the feature of creating a folder should be supported. You can upload a 0 KB file whose path ends with `/`. When you call the API GetBucket, you can use the file as a folder.



**2) Advanced API for upload**

We encapsulate the advanced API for upload in XML SDK. The API supports intelligent selection of simple upload or multipart upload according to the file size. Multipart upload supports resuming upload from breakpoint. You can also set the number of threads to control the upload speed.

The sample code for using the advanced API for upload to resume upload from breakpoint is as follows:

```
response = client.upload_file(
    Bucket='examplebucket-1250000000',
    LocalFilePath='local.txt',
    Key=file_name,
    PartSize=10,
    MAXThread=10
)
```

**3) Signature algorithm**

Generally, you do not need to compute a signature manually. However, if you return an SDK signature to the frontend, note that the signature algorithm has changed. One-time signatures and multiple-time signatures are no longer used. Instead, you can set a validity period of the signature to ensure security. For more information, see [XML Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).

**4) New APIs**

The following APIs are added in XML Python SDK, and they can be called as needed:

* Bucket operations, such as create_bucket, delete_bucket, and list_objects.
* Operations on bucket ACLs, such as put_bucket_acl, and get_bucket_acl.
* Operations on bucket lifecycle, such as put_bucket_lifecycle, and get_bucket_lifecycle.

For more information, see Python SDK [API Documentation](https://intl.cloud.tencent.com/document/product/436/12269).

