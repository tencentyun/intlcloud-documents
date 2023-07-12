## Overview

This document provides an overview of APIs and SDK code samples for file decompression.

| API | Description |
| ------------- |  ---------------------- |
| [Submitting a file decompression job](https://intl.cloud.tencent.com/document/product/436/53993) | Submits a file decompression job through a POST request. You can submit a job to perform file decompression and asynchronously return decompressed files. |
| [Querying the result of a file decompression job](https://intl.cloud.tencent.com/document/product/436/53994)  | Queries the result of a specified file decompression job. |


## Submitting a File Decompression Job

#### Feature description

This API adopts a POST request method. You can submit a job to perform file decompression and asynchronously return decompressed files.

#### Method prototype

```php
public Guzzle\Service\Resource\Model createFileUncompressJobs(array $args = array());
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
    // https://intl.cloud.tencent.com/document/product/436/53993: Submitting a File Decompression Job Asynchronously
    $result = $cosClient->createFileUncompressJobs(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
        'Tag' => 'FileUncompress',
//        'QueueId' => 'pcc3ae89sa9d807fs89dg789sdg',
        'Input' => array(
            'Object' => 'test.zip',
        ),
        'Operation' => array(
            'UserData' => 'xxx',
            'FileUncompressConfig' => array(
                'Prefix' => 'prefix',
                'PrefixReplaced' => '1',
            ),
            'Output' => array(
                'Region' => $region,
                'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
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
| Tag                | Request | Job type. It is `FileUncompress` for file decompression by default.               | String    | Yes       |
| Input              | Request | Information about the file to be operated                                         | Container | Yes   |
| Operation          | Request | File decompression rule.                                 | Container | Yes       |
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
| :------------------- | :---------------- | :---------------------------------------------- | :-------- | :------- |
| FileUncompressConfig | Request.Operation | File decompression rule                        | Container | Yes       |
| UserData           | Request.Operation | The user information passed through, which is printable ASCII codes of up to 1,024 in length.                  | String    | No |
| Output             | Request.Operation | Information about the bucket where the decompressed file is stored            | Container | Yes       |

`FileUncompressConfig` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :------------------------------------- | :----------------------------------------------------------- | :----- | :------- |
| Prefix             | Request.Operation.FileUncompressConfig | Prefix of the input file after decompression. If this parameter is left empty, the file is stored in the root directory of the bucket by default.     | String | No       |
| PrefixReplaced     | Request.Operation.FileUncompressConfig | Whether to replace the prefix of the directory of the decompressed file. Valid values: <li>`0`: No additional prefix is added. The decompressed files are saved in the directory specified by `Prefix` (the name of the compressed package is not retained, and the file in the compressed package is saved to the specified directory only). <li>`1`: The name of the compressed package is used as the prefix. The decompressed files are saved in the directory specified by `Prefix`. <li>`2`: The full directory of the compressed package is used as the prefix. If `Prefix` is not specified, the file is decompressed to the current directory (including the name of the compressed package) of the compressed package. <li>Default value: `0` | String | No       |

>?If the compressed package is named `test.zip`, contains the `image.jpg` file, and is stored in the `123` directory in bucket A, the full directory of the compressed package is `123/test.zip`.
> Decompress the package to bucket A with `Prefix` set to `456`. The storage directory of the decompressed file varies depending on the value of `PrefixReplaced`:
- `0`: The `image.jpg` file is stored in the `456` directory and its full directory is `456/image.jpg`.
- `1`: The `image.jpg` file is stored in the `456` directory with prefix `test` and its full directory is `456/test/image.jpg`.
- `2`: The `image.jpg` file is stored in the `456` directory with prefix `123/test` and its full directory is `456/123/test/image.jpg`.

`Output` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :----------------------- | :----------------------- | :----- | :------- |
| Region             | Request.Operation.Output | Bucket region                                                | String | Yes   |
| Bucket             | Request.Operation.Output | Bucket where the decompressed files are stored                                             | String | Yes   |

#### Sample response

```php
GuzzleHttp\Command\Result Object
(
    [RequestId] => NjNkOGM2NmVfZTYxNmY5MSAASJPOJCIANSIDNAI=
    [ContentType] => application/xml
    [ContentLength] => 872
    [JobsDetail] => Array
        (
            [Progress] => 0
            [Code] => Success
            [Message] => 
            [JobId] => fcd32dbdaa13b11esa9ds8g0d98gd0h85
            [Tag] => FileUncompress
            [State] => Submitted
            [CreationTime] => 2023-01-31T16:05:31+0800
            [StartTime] => -
            [EndTime] => -
            [QueueId] => pcc3ae89sa9d807fs89dg789sdg
            [Input] => Array
                (
                    [BucketId] => examplebucket-1250000000
                    [Region] => ap-guangzhou
                    [Object] => test.zip
                )

            [Operation] => Array
                (
                    [JobLevel] => 0
                    [UserData] => xxx
                    [Output] => Array
                        (
                            [Region] => ap-guangzhou
                            [Bucket] => examplebucket-1250000000
                        )

                    [FileUncompressConfig] => Array
                        (
                            [Prefix] => prefix
                            [PrefixReplaced] => 1
                        )

                )

        )

    [Bucket] => examplebucket-1250000000
    [Location] => examplebucket-1250000000.ci.ap-guangzhou.myqcloud.com/file_jobs
)
```



## Querying File Decompression Result

#### Feature description

This API is used to query the result of a specified file decompression job.

#### Method prototype

```php
public Guzzle\Service\Resource\Model getFileUncompressResult(array $args = array());
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
    // https://intl.cloud.tencent.com/document/product/436/53994: Querying File Decompression Result
    $result = $cosClient->getFileUncompressResult(array(
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
    [ContentLength] => 1092
    [JobsDetail] => Array
        (
            [Progress] => 100
            [Code] => Success
            [Message] => success
            [JobId] => fcd32dbdaa13b11esa9ds8g0d98gd0h85
            [Tag] => FileUncompress
            [State] => Success
            [CreationTime] => 2023-01-31T16:05:31+0800
            [StartTime] => 2023-01-31T16:05:31+0800
            [EndTime] => 2023-01-31T16:05:31+0800
            [QueueId] => pcc3ae89sa9d807fs89dg789sdg
            [Input] => Array
                (
                    [BucketId] => examplebucket-1250000000
                    [Region] => ap-guangzhou
                    [Object] => test.zip
                )

            [Operation] => Array
                (
                    [JobLevel] => 0
                    [UserData] => xxx
                    [Output] => Array
                        (
                            [Region] => ap-guangzhou
                            [Bucket] => examplebucket-1250000000
                        )

                    [FileUncompressConfig] => Array
                        (
                            [Prefix] => prefix
                            [PrefixReplaced] => 1
                        )

                    [FileUncompressResult] => Array
                        (
                            [Region] => ap-guangzhou
                            [Bucket] => examplebucket-1250000000
                            [FileCount] => 6
                        )

                )

        )

    [Key] => fcd32dbdaa13b11esa9ds8g0d98gd0h85
    [Bucket] => examplebucket-1250000000
    [Location] => examplebucket-1250000000.ci.ap-guangzhou.myqcloud.com/file_jobs/fcd32dbdaa13b11esa9ds8g0d98gd0h85
)
```
