## Download and Installation

#### Relevant resources
- The COS XML SDK for PHP source code can be downloaded [here](https://github.com/tencentyun/cos-php-sdk-v5/releases).
- Download the XML SDK for PHP [here](https://cos-sdk-archive-1253960454.file.myqcloud.com/cos-php-sdk-v5/latest/cos-php-sdk-v5.zip).
- Download the demo [here](https://github.com/tencentyun/cos-php-sdk-v5/tree/master/sample).
- Find the complete sample code [here](https://github.com/tencentyun/cos-snippets/tree/master/php).
- For the SDK changelog, please see [Changelog](https://github.com/tencentyun/cos-php-sdk-v5/blob/master/CHANGELOG.md).

#### Environmental dependency

*   PHP 5.6+
    You can view the current PHP version by running the `php -v` command.
>!If your PHP version is `>=5.3` and `<5.6`, please use [v1.3](https://github.com/tencentyun/cos-php-sdk-v5/tree/1.3).

-  cURL extension
You can run the `php -m` command to check whether the cURL extension has been installed properly.
 - On Ubuntu, you can install PHP's cURL extension using the apt-get package manager with the following command:
```shell
sudo apt-get install php-curl
```
 - On CentOS, you can install PHP's cURL extension using the yum package manager.
```shell
sudo yum install php-curl
```

#### Installing SDK
There are three methods to install the SDK, i.e., [Composer method](#composer), [Phar method](#phar), and [source code method](#Source).

<span id="composer"></span>
#### Composer method
We recommend you install cos-php-sdk-v5 with Composer, a PHP dependency manager that allows you to declare the dependencies necessary for your project and then automatically installs them into your project.
>?You can find more information such as how to install Composer, how to configure auto-load, and other best practices for defining dependencies at [Composer official website](https://getcomposer.org/).

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
This command will create a `vendor` folder in the current directory. The folder will contain the SDK's dependent library and an `autoload.php` script file for future call in your project.
5. Call cos-php-sdk-v5 with the autoloader script.
```php
require '/path/to/sdk/vendor/autoload.php';
```
Now, you can use COS XML SDK for PHP in your project.

<span id="phar"></span>
#### Phar method
Install the SDK using the Phar method as instructed below:
1. Download the phar file [here](https://github.com/tencentyun/cos-php-sdk-v5/releases).
2. Import the phar file into your code.

```php
require  '/path/to/cos-sdk-v5.phar';
```

<span id="Source"></span>
#### Source code method
The steps to install the SDK in the source code method are as follows:
1. Download the `cos-sdk-v5.tar.gz` package [here](https://github.com/tencentyun/cos-php-sdk-v5/releases).
>!The `Source code` package is the default package compressed by GitHub and does not contain the `vendor` directory.
2. After decompressing it, load the SDK through the `autoload.php` script.

```php
require '/path/to/sdk/vendor/autoload.php';
```


## Getting Started
The section below describes how to use COS SDK for PHP to perform basic operations, such as initializing a client, creating a bucket, querying the bucket list, uploading an object, querying the object list, downloading an object, and deleting an object.

### Initialization

[//]: # ".cssg-snippet-global-init"
```php
$secretId = "COS_SECRETID"; //"TencentCloud API key's SecretId";
$secretKey = "COS_SECRETKEY"; //"TencentCloud API key's SecretKey";
$region = "COS_REGION"; // Set the default bucket region
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', // Protocol header; http by default
        'credentials'=> array(
            'secretId'  => $secretId ,
            'secretKey' => $secretKey)));
```

If you initialize a client with a [temporary key](https://intl.cloud.tencent.com/document/product/436/14048), create an instance in the following way.

[//]: # ".cssg-snippet-global-init-sts"
```php
$tmpSecretId = "COS_SECRETID"; //"Temporary key's SecretId";
$tmpSecretKey = "COS_SECRETKEY"; //"Temporary key's SecretKey";
$tmpToken = "COS_TOKEN"; //"Temporary key's token";
$region = "COS_REGION"; // Set the default bucket region
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', // Protocol header; http by default
        'credentials'=> array(
            'secretId'  => $tmpSecretId,
            'secretKey' => $tmpSecretKey,
            'token' => $tmpToken)));
```

### Creating bucket

[//]: # ".cssg-snippet-put-bucket"
```php
try {
    $bucket = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID
    $result = $cosClient->createBucket(array('Bucket' => $bucket));
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

### Querying bucket list

[//]: # ".cssg-snippet-get-service"
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
>!
* Upload a file (up to 5 GB) by using the `putObject` API.
* Use the `Upload` API to upload files in multiple parts. It is a composite upload API and uses simple upload for small files and multipart upload for large files.
* For parameter descriptions, please see [Object Operations](https://intl.cloud.tencent.com/document/product/436/31542#uploading-an-object-by-using-simple-upload).

[//]: # ".cssg-snippet-put-object-comp"
```php
# Upload a file
## putObject (upload API which supports files of up to 5 GB in size each)
### Uploading in-memory string
try {
    $bucket = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID
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
    $bucket = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID
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
    $bucket = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID
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
    $bucket = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID
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

[//]: # ".cssg-snippet-get-bucket"
```php
try {
    $bucket = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID
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

[//]: # ".cssg-snippet-get-bucket-recursive"
```php
try {
    $bucket = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID
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
            break; // Determine whether the query is complete
        }
    }
} catch (\Exception $e) {
    echo($e);
}
```

### Downloading object
* Download a file using the getObject API.
* Get a file download URL by using the `getObjectUrl` API.

[//]: # ".cssg-snippet-get-object-comp"
```php
# Download a file
## getObject (for file download)
### Download to memory
try {
    $bucket = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID
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

### Download to local file system
try {
    $bucket = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID
    $key = "exampleobject"; // Location of the object in the bucket, i.e., the object key
    $localPath = @"path/to/localFile";// Download to a specific local path
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
    $bucket = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID
    $key = "exampleobject"; // Location of the object in the bucket, i.e., the object key
    $localPath = @"path/to/localFile";// Download to a specific local path
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
    $bucket = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID
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

[//]: # ".cssg-snippet-delete-object-comp"
```php
# Delete an object
## deleteObject
try {
    $bucket = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID
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
    $bucket = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID
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
