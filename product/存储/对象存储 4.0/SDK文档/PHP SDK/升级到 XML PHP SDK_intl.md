If you have carefully compared the documentations of JSON PHP SDK and XML PHP SDK, you can find that the latter is not simply an incremental update version of the former. XML PHP SDK has made great improvements in architecture, availability and security, as well as in usability, robustness and transmission performance. If you want to upgrade to XML PHP SDK, refer to the following instructions.

## Feature Comparison

The following table compares the main features of JSON PHP SDK and XML PHP SDK:

| Feature | XML PHP SDK | JSON PHP SDK |
| -------- | :------------: | :------------------:    |
| File upload | Upload of local files, byte streams and input streams is supported.<br>Existing files are overwritten by default.<br>Intelligent selection of upload mode<br>File size is limited to 5 GB in a simple upload.<br>File size is limited to 48.82 TB (50,000 GB) in a multipart upload. | Only local file upload is supported.<br>You can select whether to overwrite existing files.<br>You need to manually select simple upload or multipart upload.<br>File size is limited to 20 MB in a simple upload.<br>File size is limited to 64 GB in a multipart upload. |
| File deletion | Batch deletion is supported. | Only deletion of a single file is supported |
| Basic operations on buckets | Create a bucket<br>Get a bucket<br>Delete a bucket | Not supported |
| Operations on bucket ACLs | Set bucket ACL<br>Get bucket ACL<br>Delete bucket ACL | Not supported |
| Bucket lifecycle | Create bucket lifecycle<br>Get bucket lifecycle<br>Delete bucket lifecycle | Not supported |
| Directory operations | No APIs are provided separately. | Create a directory<br>Query a directory<br>Delete a directory |


## Upgrade Procedure
Upgrade PHP SDK by following the 4 steps below.

**1. Update PHP SDK**

COS XML PHP SDK can be installed in the following ways:
* Composer method.
* Phar method.
* Source code method.

**Composer method**
It is recommended to install COS XML PHP SDK using Composer. Composer is a PHP dependency management tool, which allows you to declare the dependencies required by your project and installs them in your project automatically.

>You can visit the [Composer official website](https://getcomposer.org/) to find more information about how to install Composer and configure auto-loading, and other best practices for defining dependencies.

Here are the steps for installing XML PHP SDK using Composer:
1) Open the terminal.
2) Download Composer by executing the following command:
```
curl -sS https://getcomposer.org/installer | php
```
3) Create a file named `composer.json` which contains the following content:
```
{
    "require": {
        "qcloud/cos-sdk-v5": "1.*"
    }
}
```
4) Install by Composer by executing the following command:
```
php composer.phar install
```
After this command is executed, a vendor folder will be created in the current directory. The folder contains the dependent libraries of the SDK, and an autoload.php script used to call the SDK in your own project.

5) Call XML PHP SDK via the autoloader script.
```
require '/path/to/sdk/vendor/autoload.php';
```

Now, you can use COS XML PHP SDK in your project.


**Phar method**
Here are the steps for installing XML PHP SDK using the Phar method:

1) Download the desired phar file on the [Github release page](https://github.com/tencentyun/cos-php-sdk-v5/releases).

2) Introduce the Phar file in the code:
```
require  '/path/to/cos-sdk-v5.phar';
```

**Source code method**
Here are the steps for installing XML PHP SDK using the source code:

1) Download the desired cos-sdk-v5.tar.gz compressed file on the [Github release page](https://github.com/tencentyun/cos-php-sdk-v5/releases).

2) Decompress the downloaded file and load the SDK via the autoload.php script.
```
require '/path/to/sdk/vendor/autoload.php';
```

**2. Change the SDK initialization method**

The initialization APIs in XML PHP SDK have changed. You need to make changes accordingly.

JSON PHP SDK is initialized as follows:

```
require('cos-php-sdk-v4/include.php'); 
use Qcloud\Cos\Api;
//Create a COSClientConfig object to modify the default configuration parameters as needed
$config = array(
    'app_id' => '',
    'secret_id' => '',
    'secret_key' => '',
    'region' => 'gz',
    'timeout' => 60
);
//Create a cosApi object to implement COS operations
$cosApi = new Api($config);
```

XML PHP SDK is initialized as follows:

```
require '/path/to/sdk/vendor/autoload.php';
$cosClient = new Qcloud\Cos\Client(array('region' => getenv('COS_REGION'),
    'credentials'=> array(
        'secretId'    => getenv(' COS_SECRETID'),
        'secretKey' => getenv(' COS_SECRETKEY'))));
```


**3. Change the bucket name and the abbreviations of available regions**

The bucket name and the abbreviations of available regions in XML PHP SDK are different from those in JSON PHP SDK. You need to make changes accordingly.

**Bucket**
The name of an XML PHP SDK bucket consists of a user-defined string and an APPID that are connected by a dash ("-").
For example, `examplebucket-1250000000`, where `examplebucket` is a user-defined string, and `1250000000` is an APPID.

>APPID is one of the Tencent Cloud account IDs, and is used to associate with cloud resources. After applying for a Tencent Cloud account successfully, you will be assigned an APPID automatically. APPID can be found in **Account Info** on the [Tencent Cloud Console](https://console.cloud.tencent.com/).

**Abbreviations of available regions for buckets**
The abbreviations of available regions for XML PHP SDK buckets have changed. During initialization, enter the region field according to the table below.

| Region | Abbreviation in XML PHP SDK | Abbreviation in JSON PHP SDK |
| -------- | ------------ | ---------------------------------------- |
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


**4. Change APIs**
After JSON PHP SDK is upgraded to XML PHP SDK, the APIs for some operations have changed. Make corresponding changes based on your actual needs. In addition, we have encapsulated APIs to make it easier to use the SDK. For more information, see our examples and [API Documentation](https://intl.cloud.tencent.com/document/product/436/12266).

There are three changes:

**1) No directory API**

No separate directory API is provided in XML SDK. As COS comes with no folders and directories, it will not create a "project" folder for uploading the object `project/a.txt`. To make it easier for you to get started, COS simulates the display mode of "folder" or "directory" in the console and graphical tools such as COS browser. This is realized by creating an empty object with a key value of `project/` and displaying it as a traditional folder.

For example: When you upload the object `project/doc/a.txt`, the delimiter `/` simulates the display mode of "folder", and you can see the folders "project" and "doc" on the console. The folder "doc" is displayed under the folder "project" and contains the file "a.txt".

Therefore, in a use case for file upload only, you can directly upload files without creating a folder first. If a folder is allowed in a use case, the feature of creating a folder should be supported. You can upload a 0 KB file whose path ends with `/ `. When you call the API `GetBucket`, you can use the file as a folder.

**2) Signature algorithm**

Generally, you do not need to compute a signature manually. However, if you return an SDK signature to the frontend, note that the signature algorithm has changed. One-time signatures and multiple-time signatures are no longer used. Instead, you can set a validity period of the signature to ensure security. For more information, see [XML Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).


**3) New APIs**

The following APIs are added in XML PHP SDK:
* Bucket operations, such as PutBucketRequest, GetBucketRequest, and ListBucketRequest.
* Operations on Bucket ACLs, such as PutBucketACLRequest, and GetBucketACLRequest.
* Operations on bucket lifecycle, such as PutBucketLifecycleRequest, and GetBucketLifecycleRequest.

For more information, see PHP SDK [API documentation](https://intl.cloud.tencent.com/document/product/436/12266).




