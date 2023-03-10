## Download and Installation

#### Related resources
- Download the COS XML PHP SDK source code from [GitHub](https://github.com/tencentyun/cos-php-sdk-v5/releases).
- Download the XML PHP SDK from [GitHub](https://cos-sdk-archive-1253960454.file.myqcloud.com/cos-php-sdk-v5/latest/cos-php-sdk-v5.zip).
- Download the demo from [GitHub](https://github.com/tencentyun/cos-php-sdk-v5/tree/master/sample).
- For all the code samples, visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/php).
- For the SDK changelog, see [Changelog](https://github.com/tencentyun/cos-php-sdk-v5/blob/master/CHANGELOG.md).
- For SDK FAQs, see [PHP SDK](https://intl.cloud.tencent.com/document/product/436/40543).


>? If you encounter errors such as non-existent functions or methods when using the XML SDK, update the SDK to the latest version and try again.

#### Environmental dependencies

- PHP 5.6+
You can run the `php -v` command to view the current PHP version.
>! If your PHP version is 5.3 or later and earlier than 5.6, use the [SDK v1.3](https://github.com/tencentyun/cos-php-sdk-v5/tree/1.3).
>
- cURL extension
- XML extension
- DOM extension
- MBstring extension
- JSON extension
You can run the `php -m` command to check whether the above extensions have been installed properly.
 - On Ubuntu, you can install PHP's extensions through the apt-get package manager with the following command:
```shell
sudo apt-get install php-curl php-xml php-dom php-mbstring php-json
```
 - On CentOS, you can install PHP's cURL extension through the yum package manager.
```shell
sudo yum install php-curl php-xml php-dom php-mbstring php-json
```

#### Installing SDK
You can install the SDK through [Composer](#composer), [PHAR](#phar), or the [source code](#Source).

<span id="composer"></span>

#### Composer

We recommend you install `cos-php-sdk-v5` through Composer, a PHP dependency manager that allows you to declare the dependencies necessary for your project and then automatically installs them into your project.

>? You can find more information such as how to install Composer, how to configure automatic load, and other best practices for defining dependencies at the [Composer website](https://getcomposer.org/).
>

**Directions**

1. Open the terminal.
2. Run the following command to download Composer:
```shell
curl -sS https://getcomposer.org/installer | php
```
3. Create a file named `composer.json` with the following content:
```json
{
    "require": {
        "qcloud/cos-sdk-v5": ">=2.0"
    }
}
```
4. Run the following command to install the SDK with Composer:
```shell
php composer.phar install
```
This command will create a `vendor` folder in the current directory. The folder will contain the SDK's dependency library and an `autoload.php` script file for future calls in your project.
>! Composer will download Guzzle 6 or Guzzle 7 based on the PHP version. Guzzle 7 supports the Laravel 8 framework. If the PHP version is 7.2.5 or later, Guzzle 7 will be downloaded by default; otherwise, Guzzle 6 will be downloaded.
>
5. Run the `autoloader` script to call `cos-php-sdk-v5` and import the `autoload.php` file into your code.
```php
require '/path/to/sdk/vendor/autoload.php';
```
>! After running the Composer installation command, you need to change the path here to the path of the `autoload.php` file; otherwise, relevant methods cannot be called. For example, if your installation path is `/Users/username/project`, you should set the referenced path in the project to `/Users/username/project/vendor/autoload.php`.
>

At this point, you can use the COS XML PHP SDK in your project.

<span id="phar"></span>
#### PHAR
Install the SDK through PHAR as instructed below:
1. Download the PHAR file from [GitHub](https://github.com/tencentyun/cos-php-sdk-v5/releases).
>? 
> - If your PHP version is 5.6 or later and earlier than 7.2.5, download `cos-sdk-v5-6.phar` to use Guzzle 6.
> - If your PHP version is 7.2.5 or later, download `cos-sdk-v5-7.phar` to use Guzzle 7.
> 
2. Import the PHAR file into your code.
```php
require  '/path/to/cos-sdk-v5-x.phar';
```

<span id="Source"></span>
#### Source code
Install the SDK through the source code as instructed below:
1. Download the `cos-sdk-v5.tar.gz` compressed file from [GitHub](https://github.com/tencentyun/cos-php-sdk-v5/releases).
>? 
> - If your PHP version is 5.6 or later and earlier than 7.2.5, download `cos-sdk-v5-6.tar.gz` to use Guzzle 6.
> - If your PHP version is 7.2.5 or later, download `cos-sdk-v5-7.tar.gz` to use Guzzle 7.
> 
2. Decompress the file and run the `autoload.php` script to load the SDK and import the `autoload.php` file into your code:
```php
require '/path/to/sdk/vendor/autoload.php';
```
>! `Source code` is the default GitHub-compressed code package, which does not include the `vendor` directory. Note that you should download the release package (cos-sdk-v5-x.tar.gz) rather than the source package. You should not clone the entire repository; otherwise, `index.php` and the `vendor` package will be missing.
>

## Getting Started
The section below describes how to use the COS PHP SDK to perform basic operations, such as initializing a client, creating a bucket, querying a bucket list, uploading an object, querying an object list, downloading an object, or deleting an object. For more information on the parameters involved in the samples, see [Bucket Operations](https://www.tencentcloud.com/document/product/436/48242) and [Object Operations](https://www.tencentcloud.com/document/product/436/43310).

### Initialization
If you use a permanent key to initialize a `COSClient`, you need to get your `SecretId` and `SecretKey` on the [Manage API Key](https://console.cloud.tencent.com/cam/capi) page in the CAM console. A permanent key is suitable for most application scenarios.

[//]: # ".cssg-snippet-global-init"
```php
// Log in to the CAM console to view and manage the `SECRETID` and `SECRETKEY` of your project.
$secretId = "SECRETID"; // Replace it with your actual `secretId`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi.
$secretKey = "SECRETKEY"; // Replace it with your actual `secretKey`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi.
$region = "ap-beijing"; // Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', // Protocol header, which is `http` by default.
        'credentials'=> array(
            'secretId'  => $secretId ,
            'secretKey' => $secretKey)));
```

>! If no HTTPS certificate is configured, you need to delete the `schema` parameter or enter `'schema' => 'http'`. If you enter `https`, a certificate problem will be reported. To configure an HTTPS certificate, see [PHP SDK](https://intl.cloud.tencent.com/document/product/436/40543).
>

If you initialize a client with a [temporary key](https://intl.cloud.tencent.com/document/product/436/14048), create an instance in the following way.

[//]: # ".cssg-snippet-global-init-sts"
```php
$tmpSecretId = "SECRETID"; // Replace it with your actual `secretId`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi.
$tmpSecretKey = "SECRETKEY"; // Replace it with your actual `secretKey`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi.
$tmpToken = "COS_TOKEN"; // This is required for temporary keys. For more information on how to generate and use a temporary key, visit https://intl.cloud.tencent.com/document/product/436/14048
$region = "COS_REGION"; // Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', // Protocol header, which is `http` by default.
        'credentials'=> array(
            'secretId'  => $tmpSecretId,
            'secretKey' => $tmpSecretKey,
            'token' => $tmpToken)));
```

### Creating bucket

[//]: # ".cssg-snippet-put-bucket"
```php
try {
    $bucket = "examplebucket-1250000000"; // Bucket name in the format of `BucketName-APPID`
    $result = $cosClient->createBucket(array('Bucket' => $bucket));
    // The request succeeded.
    print_r($result);
} catch (\Exception $e) {
    // The request failed.
    echo($e);
}
```

### Querying bucket list

[//]: # ".cssg-snippet-get-service"
```php
try {
    // The request succeeded.
    $result = $cosClient->listBuckets();
    print_r($result);
} catch (\Exception $e) {
    // The request failed.
    echo($e);
}
```


### Uploading object
>!
> - Upload a file (up to 5 GB) by using the `putObject` API.
> - Upload a file in multiple parts by using the `Upload` API. This API is a composition API that uses simple upload for small files and uses multipart upload for large files.
> - For parameter descriptions, see [Object Operations](https://www.tencentcloud.com/document/product/436/43310#.E7.AE.80.E5.8D.95.E4.B8.8A.E4.BC.A0.E5.AF.B9.E8.B1.A1).
> 

[//]: # ".cssg-snippet-put-object-comp"
```php
# Uploading File
## putObject (this API can upload a file of up to 5 GB)
### Uploading strings in memory
try {
    $bucket = "examplebucket-1250000000"; // Bucket name in the format of `BucketName-APPID`
    $key = "exampleobject"; // Object key, which is the unique identifier of an object in a bucket
    $result = $cosClient->putObject(array(
        'Bucket' => $bucket,
        'Key' => $key,
        'Body' => 'Hello World!'));
    print_r($result);
} catch (\Exception $e) {
    echo "$e\n";
}

### Uploading file stream
try {
    $bucket = "examplebucket-1250000000"; // Bucket name in the format of `BucketName-APPID`
    $key = "exampleobject"; // Object key, which is the unique identifier of an object in a bucket
    $srcPath = "path/to/localFile";// Absolute path to the local file
    $file = fopen($srcPath, "rb");
    if ($file) {
        $result = $cosClient->putObject(array(
            'Bucket' => $bucket,
            'Key' => $key,
            'Body' => $file));
        print_r($result);
    }
} catch (\Exception $e) {
    echo "$e\n";
}

## Upload (this advanced upload API can upload a file of up to 50 TB with multipart upload)
### Uploading strings in memory
try {    
    $bucket = "examplebucket-1250000000"; // Bucket name in the format of `BucketName-APPID`
    $key = "exampleobject"; // Object key, which is the unique identifier of an object in a bucket
    $result = $cosClient->Upload(
        $bucket = $bucket,
        $key = $key,
        $body = 'Hello World!');
    print_r($result);
} catch (\Exception $e) {
    echo "$e\n";
}

### Uploading file stream
try {    
    $bucket = "examplebucket-1250000000"; // Bucket name in the format of `BucketName-APPID`
    $key = "exampleobject"; // Object key, which is the unique identifier of an object in a bucket
    $srcPath = "path/to/localFile";// Absolute path to the local file
    $file = fopen($srcPath, 'rb');
    if ($file) {
        $result = $cosClient->Upload(
            $bucket = $bucket,
            $key = $key,
            $body = $file);
    }
    print_r($result);
} catch (\Exception $e) {
    echo "$e\n";
}
```

### Querying object list

[//]: # ".cssg-snippet-get-bucket"
```php
try {
    $bucket = "examplebucket-1250000000"; // Bucket name in the format of `BucketName-APPID`
    $result = $cosClient->listObjects(array(
        'Bucket' => $bucket
    ));
    // The request succeeded.
    if (isset($result['Contents'])) {
        foreach ($result['Contents'] as $rt) {
            print_r($rt);
        }
    }
} catch (\Exception $e) {
    // The request failed.
    echo($e);
}
```

A single call to the `listObjects` API can query up to 1,000 objects. To query all objects, call it repeatedly.

[//]: # ".cssg-snippet-get-bucket-recursive"
```php
try {
    $bucket = "examplebucket-1250000000"; // Bucket name in the format of `BucketName-APPID`
    $prefix = ''; // Prefix of the objects to be listed
    $marker = ''; // End marker in the last list
    while (true) {
        $result = $cosClient->listObjects(array(
            'Bucket' => $bucket,
            'Marker' => $marker,
            'MaxKeys' => 1000 // Set the maximum number of entries to be listed in one single query, which is up to 1,000.
        ));
        if (isset($result['Contents'])) {
            foreach ($result['Contents'] as $rt) {
                // Print the key
                echo($rt['Key'] . "\n");
            }
        }
        $marker = $result['NextMarker']; // Set a new end marker
        if (!$result['IsTruncated']) {
            break; // Check whether the query is complete
        }
    }
} catch (\Exception $e) {
    echo($e);
}
```

### Downloading object
- Download a file by using the `getObject` API.
- Get a file download URL by using the `getObjectUrl` API.

[//]: # ".cssg-snippet-get-object-comp"
```php
# Downloading File
## getObject (for file download)
### Downloading to memory
try {
    $bucket = "examplebucket-1250000000"; // Bucket name in the format of `BucketName-APPID`
    $key = "exampleobject";  // Object key, which is the unique identifier of an object in a bucket
    $result = $cosClient->getObject(array(
        'Bucket' => $bucket,
        'Key' => $key));
    // The request succeeded.
    echo($result['Body']);
} catch (\Exception $e) {
    // The request failed.
    echo "$e\n";
}

### Downloading to local file system
try {
    $bucket = "examplebucket-1250000000"; // Bucket name in the format of `BucketName-APPID`
    $key = "exampleobject";  // Object key, which is the unique identifier of an object in a bucket
    $localPath = @"path/to/localFile";// Download to the specified local path
    $result = $cosClient->getObject(array(
        'Bucket' => $bucket,
        'Key' => $key,
        'SaveAs' => $localPath));
} catch (\Exception $e) {
    // The request failed.
    echo "$e\n";
}

### Specifying download range
/*
 * The `Range` field is in the format of 'bytes=a-b'.
 */
try {
    $bucket = "examplebucket-1250000000"; // Bucket name in the format of `BucketName-APPID`
    $key = "exampleobject";  // Object key, which is the unique identifier of an object in a bucket
    $localPath = @"path/to/localFile";// Download to the specified local path
    $result = $cosClient->getObject(array(
        'Bucket' => $bucket,
        'Key' => $key,
        'Range' => 'bytes=0-10',
        'SaveAs' => $localPath));
} catch (\Exception $e) {
    // The request failed.
    echo "$e\n";
}

## getObjectUrl (for getting file URL)
try {    
    $bucket = "examplebucket-1250000000"; // Bucket name in the format of `BucketName-APPID`
    $key = "exampleobject";  // Object key, which is the unique identifier of an object in a bucket
    $signedUrl = $cosClient->getObjectUrl($bucket, $key, '+10 minutes');
    // The request succeeded.
    echo $signedUrl;
} catch (\Exception $e) {
    // The request failed.
    print_r($e);
}
```

### Deleting object

[//]: # ".cssg-snippet-delete-object-comp"
```php
# Deleting Object
## deleteObject
try {
    $bucket = "examplebucket-1250000000"; // Bucket name in the format of `BucketName-APPID`
    $key = "exampleobject";  // Object key, which is the unique identifier of an object in a bucket
    $result = $cosClient->deleteObject(array(
        'Bucket' => $bucket,
        'Key' => $key,
        'VersionId' => 'string'
    ));
    // The request succeeded.
    print_r($result);
} catch (\Exception $e) {
    // The request failed.
    echo($e);
}
# Deleting Multiple Objects
## deleteObjects
try {
    $bucket = "examplebucket-1250000000"; // Bucket name in the format of `BucketName-APPID`
    $key1 = "exampleobject1";  // Object key, which is the unique identifier of an object in a bucket
    $key2 = "exampleobject2";  // Object key, which is the unique identifier of an object in a bucket
    $result = $cosClient->deleteObjects(array(
        'Bucket' => $bucket,
        'Objects' => array(
            array(
                'Key' => $key1,
            ),
            array(
                'Key' => $key2,
            ),
            //...
        ),
    ));
    // The request succeeded.
    print_r($result);
} catch (\Exception $e) {
    // The request failed.
    echo($e);
}
```
