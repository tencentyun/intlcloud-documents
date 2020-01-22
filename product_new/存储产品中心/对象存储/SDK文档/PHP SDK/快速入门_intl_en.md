## Download and Installation

### Relevant Resources
- Source code of COS XML SDK for PHP: [XML PHP SDK](https://github.com/tencentyun/cos-php-sdk-v5/releases).
- Demo: [PHP sample](https://github.com/tencentyun/cos-php-sdk-v5/tree/master/sample).

### Environment Requirements

*   PHP 5.6+
    You can run the `php -v` command to view the current PHP version.
>- If your php version is `>=5.3` and `<5.6`, please use [ v1.3 ](https://github.com/tencentyun/cos-php-sdk-v5/tree/1.3).
- cURL extension
You can run the `php -m` command to check whether the cURL extension has been installed properly.
 - On Ubuntu, you can install PHP's cURL extension using the apt-get package manager with the following command:
```shell
sudo apt-get install php-curl
```
 - On CentOS, you can install PHP's cURL extension using the yum package manager.
```shell
sudo yum install php-curl
```

### Installing the SDK
You can install the SDK in three ways, i.e. [Composer method](#composer), [Phar method](#phar), and [source code method](#Source).

<span id="composer"></span>
#### Composer Method
It is recommended to install cos-php-sdk-v5 with Composer, a PHP dependency manager that allows you to declare the dependencies necessary for your project and then automatically installs them into your project.
> You can find more information such as how to install Composer, how to configure auto-load, and other best practices for defining dependencies at [Composer website](https://getcomposer.org/).

**Installation Steps**
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
4. Run the following command to install the SDK with Composer.
```shell
php composer.phar install
```
This command will create a `vendor` folder in the current directory. The folder will contain the SDK's dependency library and an `autoload.php` script file for future call in your project. 
5. Call cos-php-sdk-v5 with the autoloader script.
```shell
require '/path/to/sdk/vendor/autoload.php';
```
Now, you can use COS XML SDK for PHP in your project.

<span id="phar"></span>
#### Phar Method
Install the SDK using the Phar method as instructed below:
1. Download the phar file [here](https://github.com/tencentyun/cos-php-sdk-v5/releases).
2. Import the phar file into your code:
```shell
require  '/path/to/cos-sdk-v5.phar';
```

<span id="Source"></span>
#### Source Code Method
Install the SDK using the source code as instructed below:
1. Download `cos-sdk-v5.tar.gz` compressed file on the [SDK releases page](https://github.com/tencentyun/cos-php-sdk-v5/releases).
> `Source code` compressed file is the code packaged by Github by default. The directory `vendor` is not included.
2. After decompressing it, load the SDK via the `autoload.php` script:
```shell
require '/path/to/sdk/vendor/autoload.php';
```


## Getting Started
The section below describes how to use COS SDK for PHP to perform basic operations, such as initializing a client, creating a bucket, querying the bucket list, uploading an object, querying the object list, downloading an object, and deleting an object.

### Initialization
```php
$secretId = "COS_SECRETID"; //"TencentCloud API key's SecretId";
$secretKey = "COS_SECRETKEY"; //"TencentCloud API key's SecretKey";
$region = "ap-beijing"; // Set a default bucket region
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', // Protocol header; http by default
        'credentials'=> array(
            'secretId'  => $secretId ,
            'secretKey' => $secretKey)));
```

If you initialize a client with a [temporary key](https://intl.cloud.tencent.com/document/product/436/14048), create an instance in the following way.

```php
$tmpSecretId = "COS_SECRETID"; //"Temporary key's SecretId";
$tmpSecretKey = "COS_SECRETKEY"; //"Temporary key's SecretKey";
$tmpToken = "COS_TOKEN"; //"Temporary key's token";
$region = "ap-beijing"; // Set a default bucket region
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', // Protocol header; http by default
        'credentials'=> array(
            'secretId'  => $tmpSecretId,
            'secretKey' => $tmpSecretKey,
            'token' => $tmpToken)));
```

### Creating a Bucket
```php
try {
    $bucket = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID
    $result = $cosClient->createBucket(array('Bucket' => $bucket));
    //Request succeeded
    print_r($result);
} catch (\Exception $e) {
	// Request failed
    echo($e);
}
```

### Querying the Bucket List
```php
try {
    //Request succeeded
    $result = $cosClient->listBuckets();
    print_r($result);
} catch (\Exception $e) {
	// Request failed
    echo($e);
}
```


### Uploading an Object
* Upload a file (up to 5 GB) using the putObject API.
* Upload a file using the Upload API. The Upload API is an advanced API which uses simple upload for small files and multipart upload for large files.

```php
# Upload a file
## putObject (an API which can upload files of up to 5 GB)
### Upload strings in memory
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

### Upload a file stream
try {
    $bucket = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID
    $key = "exampleobject";
    $srcPath = "F:/exampleobject";// Absolute path to the local file
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

### Set headers and metadata
try {
    $bucket = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID
    $key = "exampleobject";
    $result = $cosClient->putObject(array(
        'Bucket' => $bucket,
        'Key' => $key,
        'Body' => 'string | stream',
        'ACL' => 'string',
        'CacheControl' => 'string',
        'ContentDisposition' => 'string',
        'ContentEncoding' => 'string',
        'ContentLanguage' => 'string',
        'ContentLength' => 'int',
        'ContentType' => 'string',
        'Expires' => 'string',
        'GrantFullControl' => 'string',
        'GrantRead' => 'string',
        'GrantWrite' => 'string',
        'Metadata' => array(
            'string' => 'string',
        ),
        'StorageClass' => 'string'));
    print_r($result);
} catch (\Exception $e) {
    echo "$e\n";
}

## Upload (advanced upload API, which can upload files of up to 50 TB with multipart upload)
### Upload strings in memory
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

### Upload a file stream
try {    
    $bucket = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID
    $key = "exampleobject";
    $srcPath = "F:/exampleobject";// Absolute path to the local file
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

### Set headers and metadata
try {
    $bucket = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID
    $key = "exampleobject";
    $result = $cosClient->Upload(
        $bucket= $bucket,
        $key = $key,
        $body = 'string | stream',
        $options = array(
            'ACL' => 'string',
            'CacheControl' => 'string',
            'ContentDisposition' => 'string',
            'ContentEncoding' => 'string',
            'ContentLanguage' => 'string',
            'ContentLength' => 'int',
            'ContentType' => 'string',
            'Expires' => 'string',
            'GrantFullControl' => 'string',
            'GrantRead' => 'string',
            'GrantWrite' => 'string',
            'Metadata' => array(
                'string' => 'string',
            ),
            'StorageClass' => 'string'));
    print_r($result);
} catch (\Exception $e) {
    echo "$e\n";
}
```

### Querying the Object List
```php
try {
    $bucket = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID
    $result = $cosClient->listObjects(array(
        'Bucket' => $bucket
    ));
    // Request succeeded
    foreach ($result['Contents'] as $rt) {
        print_r($rt);
    }
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```
A single call to the `listObjects` API can query up to 1,000 objects. If you want to query all objects, you need to call it repeatedly.
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
        foreach ($result['Contents'] as $rt) {
            // Print key
            echo($rt['Key'] . "\n");
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

### Downloading an Object
* Download a file using the getObject API.
* Get the file download URL using the getObjectUrl API.

```php
# Download a file
## getObject (download file)
### Download to memory
try {
    $bucket = "examplebucket-1250000000"; // Bucket in the format of BucketName-APPID
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

### Download to the local file system
try {
    $bucket = "examplebucket-1250000000"; // Bucket in the format of BucketName-APPID
    $key = "exampleobject"; // Location of the object in the bucket, i.e., the object key
    $localPath = @"F:/exampleobject";// Download to the specified local path
    $result = $cosClient->getObject(array(
        'Bucket' => $bucket,
        'Key' => $key,
        'SaveAs' => $localPath));
} catch (\Exception $e) {
    // Request failed
    echo "$e\n";
}

### Specify the download range
/*
 * Range field is in the format of 'bytes=a-b'
 */
try {
    $bucket = "examplebucket-1250000000"; // Bucket in the format of BucketName-APPID
    $key = "exampleobject"; // Location of the object in the bucket, i.e., the object key
    $localPath = @"F:/exampleobject";// Download to the specified local path
    $result = $cosClient->getObject(array(
        'Bucket' => $bucket,
        'Key' => $key,
        'Range' => 'bytes=0-10',
        'SaveAs' => $localPath));
} catch (\Exception $e) {
    // Request failed
    echo "$e\n";
}

### Set response headers
try {
    $bucket = "examplebucket-1250000000"; // Bucket in the format of BucketName-APPID
    $key = "exampleobject"; // Location of the object in the bucket, i.e., the object key
    $localPath = @"F:/exampleobject";// Download to the specified local path
    $result = $cosClient->getObject(array(
        'Bucket' => $bucket,
        'Key' => $key,
        'ResponseCacheControl' => 'string',
        'ResponseContentDisposition' => 'string',
        'ResponseContentEncoding' => 'string',
        'ResponseContentLanguage' => 'string',
        'ResponseContentType' => 'string',
        'ResponseExpires' => 'mixed type: string (date format)|int (unix timestamp)|\DateTime',
        'SaveAs' => $localPath));
} catch (\Exception $e) {
    // Request failed
    echo "$e\n";
}

## getObjectUrl (get the file URL)
try {    
    $bucket = "examplebucket-1250000000"; // Bucket in the format of BucketName-APPID
    $key = "exampleobject"; // Location of the object in the bucket, i.e., the object key
    $signedUrl = $cosClient->getObjectUrl($bucket, $key, '+10 minutes');
    // Request succeeded
    echo $signedUrl;
} catch (\Exception $e) {
    // Request failed
    print_r($e);
}
```

### Deleting Objects
```php
# Delete an object
## deleteObject
try {
    $bucket = "examplebucket-1250000000"; // Bucket in the format of BucketName-APPID
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
    $bucket = "examplebucket-1250000000"; // Bucket in the format of BucketName-APPID
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
