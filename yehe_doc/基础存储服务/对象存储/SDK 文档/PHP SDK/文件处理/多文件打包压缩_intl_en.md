## Overview

This document provides an overview of APIs and SDK code samples for multi-file zipping.

| API | Description |
| ------------- |  ---------------------- |
| [Submitting a multi-file zipping job](https://intl.cloud.tencent.com/document/product/436/53995) | Submits a POST request to zip multiple files into a compressed file such as a ZIP file. You can submit a job to zip multiple files and asynchronously return the compressed file. |
| [Querying the result of a multi-file zipping job](https://intl.cloud.tencent.com/document/product/436/53996)  | Queries the result of a specified multi-file zipping job. |


## Submitting a Multi-File Zipping Job

#### Feature description

The multi-file zipping feature uses a POST request to zip multiple files into a compressed file such as a ZIP file. You can submit a job to zip multiple files and asynchronously return the compressed file.  

#### Method prototype

```php
public Guzzle\Service\Resource\Model createFileCompressJobs(array $args = array());
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
    // https://intl.cloud.tencent.com/document/product/436/53995: Submitting a Multi-File Zipping Job Asynchronously
    $result = $cosClient->createFileCompressJobs(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
        'Tag' => 'FileCompress',
//        'QueueId' => 'pcc3ae89sa9d807fs89dg789sdg',
        'Operation' => array(
            'UserData' => 'xxx',
            'FileCompressConfig' => array(
                'Flatten' => '0',
                'Format' => 'zip',
//                'UrlList' => 'test/index.csv',
//                'Prefix' => 'test/',
                'Keys' => array(
                    'object1', // File in the bucket to be zipped
                    'object2', // File in the bucket to be zipped
                    'object3', // File in the bucket to be zipped
                ),
            ),
            'Output' => array(
                'Region' => $region,
                'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
                'Object' => 'output/test.zip',
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
| Tag                | Request | Job type. It is `FileCompress` for multi-file zipping by default.               | String    | Yes       |
| Operation          | Request | File zipping rule.                                 | Container | Yes       |
| QueueId            | Request | ID of the queue where the job is in                                         | String    | Yes   |
| CallBackFormat     | Request | Job callback format, which can be `JSON` or `XML` (default). It takes priority over that of the queue. | String | No |
| CallBackType       | Request | Job callback type, which can be `Url` (default) or `TDMQ`. It takes priority over that of the queue.                    | String | No |
| CallBack           | Request | Job callback address. It takes priority over that of the queue.                    | String    | No       |
| CallBackMqConfig   | Request | TDMQ configuration for job callback as described in [Structure](https://www.tencentcloud.com/document/product/1045/49945), which is required if `CallBackType` is `TDMQ`.                | Container | No |

`Operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :---------------- | :---------------------------------------------- | :-------- | :------- |
| FileCompressConfig | Request.Operation | File zipping rule                    | Container | Yes       |
| UserData           | Request.Operation | The user information passed through, which is printable ASCII codes of up to 1,024 in length.                  | String    | No |
| Output             | Request.Operation | Address where the compressed file is stored            | Container | Yes       |

`FileCompressConfig` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :----------------------------------- | :----------------------------------------------------------- | :--------- | :------- |
| Flatten            | Request.Operation.FileCompressConfig | Whether to remove the directory structure of the original file during file zipping. Valid values: <li>`0`: No. After file zipping, the original directory structure is retained. <li>`1`: Yes. After file zipping, the original directory structure is removed and all files are at the same level. Assume that the original file URL is `https://domain/source/test.mp4` and the original file directory is `source/test.mp4`. If this parameter is set to `1`, the file directory in the ZIP file is `test.mp4`. If this parameter is set to `0`, the file directory in the ZIP file is `source/test.mp4`. | String     | Yes       |
| Format             | Request.Operation.FileCompressConfig | Zipping type. Valid values: `zip`, `tar`, `tar.gz`                   | String     | Yes       |
| UrlList            | Request.Operation.FileCompressConfig | <li>Files to be zipped can be sorted into an index file. The backend zips the files into a compressed file according to the file URL provided in the index file. The index file must be saved in the current bucket, and this field must provide the object address of the index file, for example, `/test/index.csv`. <li>Index file format: Only CSV files in which one URL occupies one row (only files in the bucket are supported) are supported. If there are multiple columns, the first column is used as the URL by default. The number of files cannot exceed 10,000 and the total size cannot exceed 50 GB. Otherwise, the job will fail. | String     | No       |
| Prefix             | Request.Operation.FileCompressConfig | Files with a specified prefix in the bucket can be zipped. To zip files in a specified directory, add / to the directory. For example, to zip files in the `test` directory, set this parameter to `test/`. The number of files cannot exceed 10,000 and the total size cannot exceed 50 GB. Otherwise, the job will fail. | String     | No       |
| Key                | Request.Operation.FileCompressConfig | Multiple files in the bucket can be zipped. The number of files cannot exceed 1,000 and the total size cannot exceed 50 GB. Otherwise, the job will fail. | String array | No       |

>!
>
> Only one of UrlList, Prefix, and Key can be selected. They cannot all be empty or do not take effect at the same time. If multiple parameters are specified, the parameter with the highest priority prevails according to the priority UrlList > Prefix > Key.

`Output` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :----------------------- | :----------------------- | :----- | :------- |
| Region             | Request.Operation.Output | Bucket region                                                | String | Yes   |
| Bucket             | Request.Operation.Output | Bucket where the compressed file is stored                                             | String | Yes   |
| Object             | Request.Operation.Output | Name of the compressed file                                             | String | Yes   |

#### Sample response

```php
GuzzleHttp\Command\Result Object
(
    [RequestId] => NjNkOGM2NmVfZTYxNmY5MSAASJPOJCIANSIDNAI=
    [ContentType] => application/xml
    [ContentLength] => 827
    [JobsDetail] => Array
        (
            [Progress] => 0
            [Code] => Success
            [Message] => 
            [JobId] => fcd32dbdaa13b11esa9ds8g0d98gd0h85
            [Tag] => FileCompress
            [State] => Submitted
            [CreationTime] => 2023-01-31T16:17:21+0800
            [StartTime] => -
            [EndTime] => -
            [QueueId] => pcc3ae89sa9d807fs89dg789sdg
            [Operation] => Array
                (
                    [JobLevel] => 0
                    [UserData] => xxx
                    [Output] => Array
                        (
                            [Region] => ap-guangzhou
                            [Bucket] => examplebucket-1250000000
                            [Object] => tmp/test.zip
                        )

                    [FileCompressConfig] => Array
                        (
                            [Flatten] => 0
                            [Format] => zip
                            [UrlList] => 
                            [Prefix] => 
                            [Key] => Array
                                (
                                    [0] => test1.png
                                    [1] => test2.jpeg
                                )

                        )

                )

        )

    [Bucket] => examplebucket-1250000000
    [Location] => examplebucket-1250000000.ci.ap-guangzhou.myqcloud.com/file_jobs
)
```



## Querying Multi-File Zipping Result

#### Feature description

This API is used to query the result of a specified multi-file zipping job.

#### Method prototype

```php
public Guzzle\Service\Resource\Model getFileCompressResult(array $args = array());
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
    // https://intl.cloud.tencent.com/document/product/436/53996: Querying Multi-File Zipping Result
    $result = $cosClient->getFileCompressResult(array(
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
    [ContentLength] => 1093
    [JobsDetail] => Array
        (
            [Progress] => 100
            [Code] => Success
            [Message] => success
            [JobId] => fcd32dbdaa13b11esa9ds8g0d98gd0h85
            [Tag] => FileCompress
            [State] => Success
            [CreationTime] => 2023-01-31T16:17:21+0800
            [StartTime] => 2023-01-31T16:17:21+0800
            [EndTime] => 2023-01-31T16:17:22+0800
            [QueueId] => pcc3ae89sa9d807fs89dg789sdg
            [Operation] => Array
                (
                    [JobLevel] => 0
                    [UserData] => xxx
                    [Output] => Array
                        (
                            [Region] => ap-guangzhou
                            [Bucket] => examplebucket-1250000000
                            [Object] => tmp/test.zip
                        )

                    [FileCompressConfig] => Array
                        (
                            [Flatten] => 0
                            [Format] => zip
                            [UrlList] => 
                            [Prefix] => 
                            [Key] => Array
                                (
                                    [0] => test1.png
                                    [1] => test2.jpeg
                                )

                        )

                    [FileCompressResult] => Array
                        (
                            [CompressFileCount] => 2
                            [Region] => ap-guangzhou
                            [Bucket] => examplebucket-1250000000
                            [Object] => tmp/test.zip
                        )

                )

        )

    [Key] => fcd32dbdaa13b11esa9ds8g0d98gd0h85
    [Bucket] => examplebucket-1250000000
    [Location] => examplebucket-1250000000.ci.ap-guangzhou.myqcloud.com/file_jobs/fcd32dbdaa13b11esa9ds8g0d98gd0h85
)
```
