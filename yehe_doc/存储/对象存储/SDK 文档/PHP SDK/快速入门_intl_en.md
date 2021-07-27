## Download and Installation

#### Related resources
- Download the source code for the COS XML PHP SDK [here](https://github.com/tencentyun/cos-php-sdk-v5/releases).
- Download the XML PHP SDK [here](https://cos-sdk-archive-1253960454.file.myqcloud.com/cos-php-sdk-v5/latest/cos-php-sdk-v5.zip).
- Download the PHP demo [here](https://github.com/tencentyun/cos-php-sdk-v5/tree/master/sample).
- For the complete sample code, please see [SDK Sample Code](https://github.com/tencentyun/cos-snippets/tree/master/php).
- For the SDK changelog, please see [Changelog](https://github.com/tencentyun/cos-php-sdk-v5/blob/master/CHANGELOG.md).
- For SDK FAQs, please see [PHP SDK FAQs](https://intl.cloud.tencent.com/document/product/436/40543).


>? If you encounter errors such as non-existent functions or methods when using the XML version of the SDK, please update the SDK to the latest version and try again.
>

#### Environment dependencies

-   PHP 5.6+
    You can run the `php -v` command to view the current PHP version.
>!If your PHP version is `>=5.3` and `<5.6`, please use [v1.3](https://github.com/tencentyun/cos-php-sdk-v5/tree/1.3).
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

#### Installing SDKs
You can install the SDK using [Composer](#composer), [Phar](#phar), or the [source code](#Source).

<span id="composer"></span>
#### Composer
It is recommended to install cos-php-sdk-v5 with Composer, a PHP dependency manager that allows you to declare the dependencies necessary for your project and then automatically installs them into your project.
>!You can find more information such as how to install Composer, how to configure auto-load, and other best practices for defining dependencies at [Composer official website](https://getcomposer.org/).

**Installation steps**
1. Start the terminal.
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
4. Run the following command to install the SDK with Composer.
```shell
php composer.phar install
```
This command will create a `vendor` folder in the current directory. The folder will contain the SDK's dependent library and an `autoload.php` script file for future calls in your project.
5. Call cos-php-sdk-v5 with the autoloader script.
```php
require '/path/to/sdk/vendor/autoload.php';
```
Now, you can use COS XML SDK for PHP in your project.

<span id="phar"></span>
#### Phar
Install the SDK using the Phar method as instructed below:
1. Download the phar file [here](https://github.com/tencentyun/cos-php-sdk-v5/releases).
2. Import the phar file into your code.

```php
require  '/path/to/cos-sdk-v5.phar';
```

<span id="Source"></span>
#### Source code
Install the SDK using the source code as instructed below:
1. Download `cos-sdk-v5.tar.gz` compressed file on the [SDK releases page](https://github.com/tencentyun/cos-php-sdk-v5/releases).
>!`Source code` is packaged by GitHub by default. The `vendor` directory is not included.
>
>2.  After decompressing it, load the SDK through the `autoload.php` script.

```php
require '/path/to/sdk/vendor/autoload.php';
```


## Getting Started
The following describes how to use the PHP SDK of COS to perform basic operations, such as initializing the client, creating a bucket, querying the bucket list, uploading an object, querying the object list, downloading an object, and deleting an object. For more information about the parameters involved in the samples, please see [Bucket Operations](https://intl.cloud.tencent.com/document/product/436/31470) and [Object Operations](https://intl.cloud.tencent.com/document/product/436/31542).

### Initialization

[//]: # ".cssg-snippet-global-init"
```php
$secretId = "COS_SECRETID"; //"TencentCloud API key's SecretId";
$secretKey = "COS_SECRETKEY"; // "SecretKey of your Tencent Cloud API key";
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
$tmpToken = "COS_TOKEN"; // "Token of the temporary key";
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

### Creating a bucket

[//]: # ".cssg-snippet-put-bucket"
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

### Querying a bucket list

[//]: # ".cssg-snippet-get-service"
```php
try {
    // Request successful 
    $result = $cosClient->listBuckets();
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```


### Uploading an object
>!
>* Upload a file (up to 5 GB) using the putObject API.
>* Upload a file using the Upload API. The Upload API is a composition API that uses simple upload for small files and uses multipart upload for large files.
>* For the parameter description, please see [Object Operations](https://intl.cloud.tencent.com/document/product/436/31542#.E7.AE.80.E5.8D.95.E4.B8.8A.E4.BC.A0.E5.AF.B9.E8.B1.A1).

[//]: # ".cssg-snippet-put-object-comp"
```php
# Upload a file.
## putObject (an API that can upload files of up to 5 GB)
### Upload strings in memory
try {
    $bucket = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID
    $key = "exampleobject"; // Object key, the unique identifier of the object in the bucket
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
    $key = "exampleobject"; // Object key, the unique identifier of the object in the bucket
    $srcPath = "path/to/localFile";// Absolute path to local file
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

## Upload (advanced upload API, which can upload files of up to 50 TB with multipart upload)
### Upload strings in memory
try {    
    $bucket = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID
    $key = "exampleobject"; // Object key, the unique identifier of the object in the bucket
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
    $key = "exampleobject"; // Object key, the unique identifier of the object in the bucket
    $srcPath = "path/to/localFile";// Absolute path to local file
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

### Querying an object list

[//]: # ".cssg-snippet-get-bucket"
```php
try {
    $bucket = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID
    $result = $cosClient->listObjects(array(
        'Bucket' => $bucket
    ));
    // Request successful
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

A single call to the `listObjects` API can query up to 1,000 objects. If you want to query all objects, you need to call it repeatedly.

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

### Downloading an object
* Download a file using the getObject API.
* Get the file download URL using the getObjectUrl API.

[//]: # ".cssg-snippet-get-object-comp"
```php
# Download a file.
## getObject (download file)
### Download to memory
try {
    $bucket = "examplebucket-1250000000"; // Bucket in the format of BucketName-APPID
    $key = "exampleobject";  // Object key, the unique identifier of the object in the bucket
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
    $key = "exampleobject";  // Object key, the unique identifier of the object in the bucket
    $localPath = @"path/to/localFile";// Download to a specific local path
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
    $key = "exampleobject";  // Object key, the unique identifier of the object in the bucket
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

## getObjectUrl (get the file URL)
try {    
    $bucket = "examplebucket-1250000000"; // Bucket in the format of BucketName-APPID
    $key = "exampleobject";  // Object key, the unique identifier of the object in the bucket
    $signedUrl = $cosClient->getObjectUrl($bucket, $key, '+10 minutes');
    // Request successful
    echo $signedUrl;
} catch (\Exception $e) {
    // Request failed
    print_r($e);
}
```

### Deleting an object

[//]: # ".cssg-snippet-delete-object-comp"
```php
# Delete an object.
## deleteObject
try {
    $bucket = "examplebucket-1250000000"; // Bucket in the format of BucketName-APPID
    $key = "exampleobject";  // Object key, the unique identifier of the object in the bucket
    $result = $cosClient->deleteObject(array(
        'Bucket' => $bucket,
        'Key' => $key,
        'VersionId' => 'string'
    ));
    // Request successful
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
# Delete multiple objects.
## deleteObjects
try {
    $bucket = "examplebucket-1250000000"; // Bucket in the format of BucketName-APPID
    $key1 = "exampleobject1";  // Object key, the unique identifier of the object in the bucket
    $key2 = "exampleobject2";  // Object key, the unique identifier of the object in the bucket
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
    // Request successful
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```
