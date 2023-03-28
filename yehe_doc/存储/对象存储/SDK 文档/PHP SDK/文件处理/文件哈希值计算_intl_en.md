## Overview

This document provides an overview of APIs and SDK code samples for hash calculation.

| API | Description |
| ------------- |  ---------------------- |
| [Submitting a sync request for hash calculation](https://intl.cloud.tencent.com/document/product/436/53990)   | Uses a sync GET request to perform hash calculation and return a calculated hash value in real time.   |
| [Submitting a hash calculation job](https://intl.cloud.tencent.com/document/product/436/53991) | Submits a hash calculation job through a POST request. You can submit a job to perform hash calculation and asynchronously return a calculated hash value. |
| [Querying the result of a hash calculation job](https://intl.cloud.tencent.com/document/product/436/53992)  | Queries the result of a specified hash calculation job. |


## Sync Request for Hash Calculation

#### Feature description

This API uses a sync GET request to perform hash calculation and return a calculated hash value in real time.

#### Method prototype

```php
public Guzzle\Service\Resource\Model FileJobs4Hash(array $args = array());
```

#### Sample request

```php
<?php

require dirname(__FILE__, 2) . '/vendor/autoload.php';

$secretId = "SECRETID"; //Replace it with the actual `SecretId`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi
$secretKey = "SECRETKEY"; //Replace it with the actual `SecretKey`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi
$region = "ap-beijing"; //Replace it with the actual `region`, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket.
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', // Protocol, which is `http` by default
        'credentials'=> array(
            'secretId'  => $secretId ,
            'secretKey' => $secretKey)));
try {
    // https://intl.cloud.tencent.com/document/product/436/53990: Sync Request for Hash Calculation
    $result = $cosClient->FileJobs4Hash(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
        'Key' => 'for-test.mp4', // File in the bucket
        'Type' => 'md5', // Supported hash algorithm. Valid values: `md5`, `sha1`, `sha256`
//        'AddToHeader' => 'true', // Whether to automatically add the calculated hash value to the custom header in the file. Format: x-cos-meta-md5/sha1/sha256. Valid values: `true`, `false`. If this parameter is left empty, it is `false` by default.
    ));
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
    /**
     * Possible exceptions
     * 1. Error Message: file processing is not active yet, please apply for file processing service first
     *    Solution: Activate the file processing service.
     */
}
```

#### Parameter description

`Request` has the following sub-nodes:

| Parameter | Type | Description | Required |
| :---------- | :----- | :----------------------------------------------------------- | :------- |
| Bucket | String | Bucket name in the format of `BucketName-APPID` | Yes |
| Key | String | File in the bucket | Yes |
| Type        | String | Supported hash algorithm. Valid values: `md5`, `sha1`, `sha256`                | Yes       |
| AddToHeader | String | Whether to automatically add the calculated hash value to the custom header in the file. Format: x-cos-meta-md5/sha1/sha256. Valid values: `true`, `false`. If this parameter is left empty, it is `false` by default. | No       |

#### Sample response

```php
GuzzleHttp\Command\Result Object
(
    [RequestId] => NjNkOGM2NmVfZTYxNmY5MSAASJPOJCIANSIDNAI
    [ContentType] => application/xml
    [ContentLength] => 421
    [FileHashCodeResult] => Array
        (
            [Etag] => "1f3ede740849eaa2e79e9b269ea3db2a"
            [LastModified] => 2023-01-29T11:31:02+0000
            [MD5] => 1f3ede740849eaa2e79e9b269ea3db2a
            [FileSize] => 42120
        )

    [Input] => Array
        (
            [Region] => ap-guangzhou
            [Bucket] => examplebucket-1250000000
            [Object] => sound01.mp3
        )

    [Key] => sound01.mp3
    [Bucket] => examplebucket-1250000000
    [Location] => examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/sound01.mp3
)
```



## Submitting a Hash Calculation Job

#### Feature description

This API adopts a POST request method. You can submit a job to perform hash calculation and asynchronously return a calculated hash value.

#### Method prototype

```php
public Guzzle\Service\Resource\Model createFileHashCodeJobs(array $args = array());
```

#### Sample request

```php
<?php

require dirname(__FILE__, 2) . '/vendor/autoload.php';

$secretId = "SECRETID"; //Replace it with the actual `SecretId`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi
$secretKey = "SECRETKEY"; //Replace it with the actual `SecretKey`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi
$region = "ap-beijing"; //Replace it with the actual `region`, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket.
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', // Protocol, which is `http` by default
        'credentials'=> array(
            'secretId'  => $secretId ,
            'secretKey' => $secretKey)));
try {
    // https://intl.cloud.tencent.com/document/product/436/53991: Submitting a Hash Calculation Job Asynchronously
    $result = $cosClient->createFileHashCodeJobs(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
        'Tag' => 'FileHashCode',
//        'QueueId' => 'pcc3ae89sa9d807fs89dg789sdg',
        'Input' => array(
            'Object' => 'test.mp4',
        ),
        'Operation' => array(
            'UserData' => 'xxx',
            'FileHashCodeConfig' => array(
                'Type' => 'MD5',
                'AddToHeader' => 'true',
            ),
        ),
//        'CallBackFormat' => '',
//        'CallBackType' => '',
//        'CallBack' => '',
//        'CallBackMqConfig' => array(
//            'MqRegion' => '',
//            'MqMode' => '',
//            'MqName' => '',
//        ),
    ));
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameter description

`Request` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :------ | :----------------------------------------------------------- | :-------- | :------- |
| Tag                | Request | Job type. It is `FileHashCode` for hash calculation by default.             | String    | Yes       |
| Input              | Request | Information about the file to be operated                                         | Container | Yes   |
| Operation          | Request | Hash calculation rule                                   | Container | Yes       |
| QueueId            | Request | ID of the queue where the job is in                                         | String    | Yes   |
| CallBackFormat     | Request | Job callback format, which can be `JSON` or `XML` (default). It takes priority over that of the queue. | String | No |
| CallBackType       | Request | Job callback type, which can be `Url` (default) or `TDMQ`. It takes priority over that of the queue.                    | String | No |
| CallBack           | Request | Job callback address. It takes priority over that of the queue.                    | String    | No       |
| CallBackMqConfig   | Request | TDMQ configuration for job callback as described in [Structure > CallBackMqConfig](https://www.tencentcloud.com/document/product/1045/49945), which is required if `CallBackType` is `TDMQ`.                | Container | No |

`Input` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :------------ | :------------------------------------------- | :----- | :------- |
| Object             | Request.Input | File name, which is the full name of the file in the bucket.  | String | Yes       |

`Operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :---------------- | :---------------------------------------------- | :-------- | :------- |
| FileHashCodeConfig | Request.Operation | Hash calculation rule                      | Container | Yes       |
| UserData           | Request.Operation | The user information passed through, which is printable ASCII codes of up to 1,024 in length.                  | String    | No |

`FileHashCodeConfig` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :----------------------------------- | :----------------------------------------------------------- | :----- | :------- |
| Type               | Request.Operation.FileHashCodeConfig | Hash algorithm. Valid values: `MD5`, `SHA1`, `SHA256`                | String | Yes       |
| AddToHeader        | Request.Operation.FileHashCodeConfig | Whether to add the calculated hash value to the custom header in the file. Valid values: `true`, `false` (default). The custom header varies depending on `Type`. For example, if `Type` is `MD5`, the custom header is `x-cos-meta-md5`. | String | No       |

#### Sample response

```php
GuzzleHttp\Command\Result Object
(
    [RequestId] => NjNkOGM2NmVfZTYxNmY5MSAASJPOJCIANSIDNAI=
    [ContentType] => application/xml
    [ContentLength] => 738
    [JobsDetail] => Array
        (
            [Progress] => 0
            [Code] => Success
            [Message] => 
            [JobId] => fcd32dbdaa13b11esa9ds8g0d98gd0h85
            [Tag] => FileHashCode
            [State] => Submitted
            [CreationTime] => 2023-01-31T15:49:33+0800
            [StartTime] => -
            [EndTime] => -
            [QueueId] => pcc3ae89sa9d807fs89dg789sdg
            [Input] => Array
                (
                    [BucketId] => examplebucket-1250000000
                    [Region] => ap-guangzhou
                    [Object] => sound01.mp3
                )

            [Operation] => Array
                (
                    [JobLevel] => 0
                    [UserData] => xxx
                    [FileHashCodeConfig] => Array
                        (
                            [Type] => MD5
                            [AddToHeader] => true
                        )

                )

        )

    [Bucket] => examplebucket-1250000000
    [Location] => examplebucket-1250000000.ci.ap-guangzhou.myqcloud.com/file_jobs
)
```



## Querying Hash Calculation Result

#### Feature description

This API is used to query the result of a specified hash calculation job.

#### Method prototype

```php
public Guzzle\Service\Resource\Model getFileHashCodeResult(array $args = array());
```

#### Sample request

```php
<?php

require dirname(__FILE__, 2) . '/vendor/autoload.php';

$secretId = "SECRETID"; //Replace it with the actual `SecretId`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi
$secretKey = "SECRETKEY"; //Replace it with the actual `SecretKey`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi
$region = "ap-beijing"; //Replace it with the actual `region`, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket.
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', //Protocol, which is http by default
        'credentials'=> array(
            'secretId'  => $secretId ,
            'secretKey' => $secretKey)));
try {
    // https://intl.cloud.tencent.com/document/product/436/53992: Querying Hash Calculation Result
    $result = $cosClient->getFileHashCodeResult(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
        'Key' => '', // jobId
    ));
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameter description

`Request` has the following sub-nodes:

| Parameter | Type | Description | Required |
| :------- | :----- | :--------------------------------- | :------- |
| Bucket | String | Bucket name in the format of `BucketName-APPID` | Yes |
| Key      | String | jobId                              | Yes       |

#### Sample response

```php
GuzzleHttp\Command\Result Object
(
    [RequestId] => NjNkOGM2NmVfZTYxNmY5MSAASJPOJCIANSIDNAI=
    [ContentType] => application/xml
    [ContentLength] => 1048
    [JobsDetail] => Array
        (
            [Progress] => 100
            [Code] => Success
            [Message] => success
            [JobId] => fcd32dbdaa13b11esa9ds8g0d98gd0h85
            [Tag] => FileHashCode
            [State] => Success
            [CreationTime] => 2023-01-31T15:49:33+0800
            [StartTime] => 2023-01-31T15:49:33+0800
            [EndTime] => 2023-01-31T15:49:34+0800
            [QueueId] => pcc3ae89sa9d807fs89dg789sdg
            [Input] => Array
                (
                    [BucketId] => examplebucket-1250000000
                    [Region] => ap-guangzhou
                    [Object] => sound01.mp3
                )

            [Operation] => Array
                (
                    [JobLevel] => 0
                    [UserData] => xxx
                    [FileHashCodeConfig] => Array
                        (
                            [Type] => MD5
                            [AddToHeader] => true
                        )

                    [FileHashCodeResult] => Array
                        (
                            [MD5] => 1f3ede740849eaa2e79e9b269ea3db2a
                            [LastModified] => 2023-01-29T11:31:02+0000
                            [Etag] => "1f3ede740849eaa2e79e9b269ea3db2a"
                            [FileSize] => 42120
                        )

                )

        )

    [Key] => fcd32dbdaa13b11esa9ds8g0d98gd0h85
    [Bucket] => examplebucket-1250000000
    [Location] => examplebucket-1250000000.ci.ap-guangzhou.myqcloud.com/file_jobs/fcd32dbdaa13b11esa9ds8g0d98gd0h85
)
```
