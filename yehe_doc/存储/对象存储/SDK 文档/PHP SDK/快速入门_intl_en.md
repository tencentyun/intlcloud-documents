## Download and Installation

#### Relevant resources
- The COS XML SDK for PHP source code can be downloaded [here](https://github.com/tencentyun/cos-php-sdk-v5/releases).
- SDK download address: [XML SDK for PHP](https://cos-sdk-archive-1253960454.file.myqcloud.com/cos-php-sdk-v5/latest/cos-php-sdk-v5.zip).
- Demo download address: [PHP sample](https://github.com/tencentyun/cos-php-sdk-v5/tree/master/sample).
- For all code samples in the SDK documentation, please see [SDK Sample Code](https://github.com/tencentyun/cos-snippets/tree/master/php).

#### Environmental dependency

*   PHP 5.6+
    You can view the current PHP version by running the `php -v` command.
>!If your PHP version is `>=5.3` and `<5.6`, please use [v1.3](https://github.com/tencentyun/cos-php-sdk-v5/tree/1.3).
- cURL extension
You can check whether the cURL extension has been installed properly by running the `php -m` command.
 - On Ubuntu, you can install PHP's cURL extension by using the apt-get package manager with the following command:
```shell
sudo apt-get install php-curl
```
 - On CentOS, you can install PHP's cURL extension by using the yum package manager.
```shell
sudo yum install php-curl
```

#### Installing SDK
There are three methods to install the SDK, i.e., [Composer method](#composer), [Phar method](#phar), and [source code method](#Source).

<span id="composer"></span>
#### Composer method
We recommend you install cos-php-sdk-v5 by using Composer, a PHP dependency management tool that allows you to declare the dependencies required by your project and then automatically installs them into your project.
>?You can find more best practices about how to install Composer, configure auto-load, and define dependencies at [Composer official website](https://getcomposer.org/).

**Installation steps**
1. Start the terminal.
2. Download Composer and run the following command.
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
4. Run the following command for installation with Composer.
```shell
php composer.phar install
```
After this command is executed, a `vendor` folder will be created in the current directory, which contains the SDK's dependency library and an `autoload.php` script for easy call in your project.
5. Call cos-php-sdk-v5 with the autoloader script.
```php
require '/path/to/sdk/vendor/autoload.php';
```
At this point, your project is ready to use the COS XML SDK for PHP.

<span id="phar"></span>
#### Phar method
The steps to install the SDK in the Phar method are as follows:
1. Download the appropriate phar file [here](https://github.com/tencentyun/cos-php-sdk-v5/releases).
2. Import the phar file into your code:

```php
require  '/path/to/cos-sdk-v5.phar';
```

<span id="Source"></span>
#### Source code method
The steps to install the SDK in the source code method are as follows:
1. Download the `cos-sdk-v5.tar.gz` package [here](https://github.com/tencentyun/cos-php-sdk-v5/releases).
>!The `Source code` package is the default package compressed by GitHub and does not contain the `vendor` directory.
2. After decompressing it, load the SDK through the `autoload.php` script:

```php
require '/path/to/sdk/vendor/autoload.php';
```


## Getting Started
The section below describes how to perform basic operations in the COS SDK for PHP, such as initializing a client, creating a bucket, querying bucket list, uploading an object, querying object list, downloading an object, and deleting an object.

### Initialization

[//]: # (.cssg-snippet-global-init)
```php
$secretId = "COS_SECRETID"; //"TencentCloud API key's SecretId";
$secretKey = "COS_SECRETKEY"; //"TencentCloud API key's SecretKey";
$region = "COS_REGION"; // Set a default bucket region
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', // Protocol header, which is `http` by default
        'credentials'=> array(
            'secretId'  => $secretId ,
            'secretKey' => $secretKey)));
```

If you initialize the service with a [temporary key](https://intl.cloud.tencent.com/document/product/436/14048), create an instance in the following way.

[//]: # (.cssg-snippet-global-init-sts)
```php
$tmpSecretId = "COS_SECRETID"; //"Temporary key's SecretId";
$tmpSecretKey = "COS_SECRETKEY"; //"Temporary key's SecretKey";
$tmpToken = "COS_TOKEN"; //"Temporary key's token";
$region = "COS_REGION"; // Set a default bucket region
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', // Protocol header, which is `http` by default
        'credentials'=> array(
            'secretId'  => $tmpSecretId,
            'secretKey' => $tmpSecretKey,
            'token' => $tmpToken)));
```

### Creating bucket

[//]: # (.cssg-snippet-put-bucket)
```php
try {
    $bucket = "examplebucket-1250000000"; // Bucket name in the format of `BucketName-APPID`
    $result = $cosClient->createBucket(array('Bucket' => $bucket));
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

### Querying bucket list

[//]: # (.cssg-snippet-get-service)
```php
try {
    // Request succeeded
    $result = $cosClient->listBuckets();
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```


### Uploading object
* Upload a file (up to 5 GB) by using the `putObject` API.
* Use the `Upload` API to upload files in multiple parts. It is a composite upload API and uses simple upload for small files and multipart upload for large files.

[//]: # (.cssg-snippet-put-object-comp)
```php
# Upload a file
## putObject (upload API which supports files of up to 5 GB in size each)
### Uploading in-memory string
try {
    $bucket = "examplebucket-1250000000"; // Bucket name in the format of `BucketName-APPID`
    $key = "exampleobject";
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
    $key = "exampleobject";
    $srcPath = "path/to/localFile";// Absolute path of the local file
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

## Upload (advanced upload API, which uses multipart upload by default and supports files of up to 50 TB in size each)
### Uploading in-memory string
try {    
    $bucket = "examplebucket-1250000000"; // Bucket name in the format of `BucketName-APPID`
    $key = "exampleobject";
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
    $key = "exampleobject";
    $srcPath = "path/to/localFile";// Absolute path of the local file
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

[//]: # (.cssg-snippet-get-bucket)
```php
try {
    $bucket = "examplebucket-1250000000"; // Bucket name in the format of `BucketName-APPID`
    $result = $cosClient->listObjects(array(
        'Bucket' => $bucket
    ));
    // Request succeeded
    if (isset($result['Contents'])) {
        foreach ($result['Contents'] as $rt) {
            print_r($rt);
        }
    }
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

A single call of the `listObjects` API can query up to 1,000 objects. If you want to query all objects, you need to call it repeatedly.

[//]: # (.cssg-snippet-get-bucket-recursive)
```php
try {
    $bucket = "examplebucket-1250000000"; // Bucket name in the format of `BucketName-APPID`
    $prefix = ''; // Prefix of the objects to be listed
    $marker = ''; // End marker in the last list
    while (true) {
        $result = $cosClient->listObjects(array(
            'Bucket' => $bucket,
            'Marker' => $marker,
            'MaxKeys' => 1000 // Set the maximum number of entries to be listed in one single query, which is up to 1,000
        ));
        if (isset($result['Contents'])) {
            foreach ($result['Contents'] as $rt) {
                // Print key
                echo($rt['Key'] . "\n");
            }
        }
        $marker = $result['NextMarker']; // Set a new end marker
        if (!$result['IsTruncated']) {
            break; // Determine whether the query is completed
        }
    }
} catch (\Exception $e) {
    echo($e);
}
```

### Downloading object
* Download a file by using the `getObject` API.
* Get a file download URL by using the `getObjectUrl` API.

[//]: # (.cssg-snippet-get-object-comp)
```php
# Download a file
## getObject (for file download)
### Downloading to memory
try {
    $bucket = "examplebucket-1250000000"; // Bucket in the format of `BucketName-APPID`
    $key = "exampleobject"; // Location of the object in the bucket, i.e., the object key
    $result = $cosClient->getObject(array(
        'Bucket' => $bucket,
        'Key' => $key));
    // Request succeeded
    echo($result['Body']);
} catch (\Exception $e) {
    // Request failed
    echo "$e\n";
}

### Downloading to local file system
try {
    $bucket = "examplebucket-1250000000"; // Bucket in the format of `BucketName-APPID`
    $key = "exampleobject"; // Location of the object in the bucket, i.e., the object key
    $localPath = @"path/to/localFile";// Download to the specified local path
    $result = $cosClient->getObject(array(
        'Bucket' => $bucket,
        'Key' => $key,
        'SaveAs' => $localPath));
} catch (\Exception $e) {
    // Request failed
    echo "$e\n";
}

### Specifying download range
/*
 * Range field is in the format of 'bytes=a-b'
 */
try {
    $bucket = "examplebucket-1250000000"; // Bucket in the format of `BucketName-APPID`
    $key = "exampleobject"; // Location of the object in the bucket, i.e., the object key
    $localPath = @"path/to/localFile";// Download to the specified local path
    $result = $cosClient->getObject(array(
        'Bucket' => $bucket,
        'Key' => $key,
        'Range' => 'bytes=0-10',
        'SaveAs' => $localPath));
} catch (\Exception $e) {
    // Request failed
    echo "$e\n";
}

## getObjectUrl (for getting file URL)
try {    
    $bucket = "examplebucket-1250000000"; // Bucket in the format of `BucketName-APPID`
    $key = "exampleobject"; // Location of the object in the bucket, i.e., the object key
    $signedUrl = $cosClient->getObjectUrl($bucket, $key, '+10 minutes');
    // Request succeeded
    echo $signedUrl;
} catch (\Exception $e) {
    // Request failed
    print_r($e);
}
```

### Deleting object

[//]: # (.cssg-snippet-delete-object-comp)
```php
# Delete one object
## deleteObject
try {
    $bucket = "examplebucket-1250000000"; // Bucket in the format of `BucketName-APPID`
    $key = "exampleobject"; // Location of the object in the bucket, i.e., the object key
    $result = $cosClient->deleteObject(array(
        'Bucket' => $bucket,
        'Key' => $key,
        'VersionId' => 'string'
    ));
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
# Delete multiple objects
## deleteObjects
try {
    $bucket = "examplebucket-1250000000"; // Bucket in the format of `BucketName-APPID`
    $key1 = "exampleobject1"; // Location of the object in the bucket, i.e., the object key
    $key2 = "exampleobject2"; // Location of the object in the bucket, i.e., the object key
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
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```
