## 简介

本文档提供关于文件哈希值计算接口的 API 概览和 SDK 示例代码。

| API           | 操作描述                 |
| ------------- |  ---------------------- |
| [哈希值计算同步请求](https://intl.cloud.tencent.com/document/product/436/53990) | 以同步请求的方式进行文件哈希值计算，实时返回计算得到的哈希值，该接口属于 GET 请求。 |
| [提交哈希值计算任务](https://intl.cloud.tencent.com/document/product/436/53991) | 以提交任务的方式进行文件哈希值计算，异步返回计算得到的哈希值，该接口属于 POST 请求。 |
| [查询哈希值计算结果](https://intl.cloud.tencent.com/document/product/436/53992) | 本接口用于主动查询指定的文件哈希值计算任务结果。 |


## 哈希值计算同步请求

#### 功能说明

以同步请求的方式进行文件哈希值计算，实时返回计算得到的哈希值，该接口属于 GET 请求。

#### 方法原型

```php
public Guzzle\Service\Resource\Model FileJobs4Hash(array $args = array());
```

#### 请求示例

```php
<?php

require dirname(__FILE__, 2) . '/vendor/autoload.php';

$secretId = "SECRETID"; //替换为用户的 secretId，请登录访问管理控制台进行查看和管理，https://console.cloud.tencent.com/cam/capi
$secretKey = "SECRETKEY"; //替换为用户的 secretKey，请登录访问管理控制台进行查看和管理，https://console.cloud.tencent.com/cam/capi
$region = "ap-beijing"; //替换为用户的 region，已创建桶归属的 region 可以在控制台查看，https://console.cloud.tencent.com/cos5/bucket
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', //协议头部，默认为 http
        'credentials'=> array(
            'secretId'  => $secretId ,
            'secretKey' => $secretKey)));
try {
    // https://intl.cloud.tencent.com/document/product/436/53990 哈希值计算同步请求
    $result = $cosClient->FileJobs4Hash(array(
        'Bucket' => 'examplebucket-1250000000', //存储桶名称，由 BucketName-Appid 组成，可以在 COS 控制台查看 https://console.cloud.tencent.com/cos5/bucket
        'Key' => 'for-test.mp4', // 桶文件
        'Type' => 'md5', // 支持的哈希算法类型，有效值：md5、sha1、sha256
//        'AddToHeader' => 'true', // 是否将计算得到的哈希值，自动添加至文件的自定义 header，格式为：x-cos-meta-md5/sha1/sha256; 有效值： true、false，不填则默认为 false。
    ));
    // 请求成功
    print_r($result);
} catch (\Exception $e) {
    // 请求失败
    echo($e);
    /**
     * 可能出现的 Exception
     * 1. Error Message: file processing is not active yet, please apply for file processing service first
     *    解决方式：开通文件处理服务
     */
}
```

#### 参数说明

Request 中的具体数据描述如下：

| 参数名称    | 类型   | 描述                                                         | 是否必填 |
| :---------- | :----- | :----------------------------------------------------------- | :------- |
| Bucket      | String | 存储桶名称，格式：BucketName-APPID                           | 是       |
| Key         | String | 桶文件                                                       | 是       |
| Type        | String | 支持的哈希算法类型，有效值：md5、sha1、sha256                | 是       |
| AddToHeader | String | 是否将计算得到的哈希值，自动添加至文件的自定义header，格式为：x-cos-meta-md5/sha1/sha256; 有效值： true、false，不填则默认为 false。 | 否       |

#### 返回结果示例

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



## 提交哈希值计算任务

#### 功能说明

以提交任务的方式进行文件哈希值计算，异步返回计算得到的哈希值，该接口属于 POST 请求。

#### 方法原型

```php
public Guzzle\Service\Resource\Model createFileHashCodeJobs(array $args = array());
```

#### 请求示例

```php
<?php

require dirname(__FILE__, 2) . '/vendor/autoload.php';

$secretId = "SECRETID"; //替换为用户的 secretId，请登录访问管理控制台进行查看和管理，https://console.cloud.tencent.com/cam/capi
$secretKey = "SECRETKEY"; //替换为用户的 secretKey，请登录访问管理控制台进行查看和管理，https://console.cloud.tencent.com/cam/capi
$region = "ap-beijing"; //替换为用户的 region，已创建桶归属的 region 可以在控制台查看，https://console.cloud.tencent.com/cos5/bucket
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', //协议头部，默认为 http
        'credentials'=> array(
            'secretId'  => $secretId ,
            'secretKey' => $secretKey)));
try {
    // https://intl.cloud.tencent.com/document/product/436/53991 提交哈希值计算任务-异步
    $result = $cosClient->createFileHashCodeJobs(array(
        'Bucket' => 'examplebucket-1250000000', //存储桶名称，由 BucketName-Appid 组成，可以在 COS 控制台查看 https://console.cloud.tencent.com/cos5/bucket
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
    // 请求成功
    print_r($result);
} catch (\Exception $e) {
    // 请求失败
    echo($e);
}
```

#### 参数说明

Request 中的具体数据描述如下：

| 节点名称（关键字） | 父节点  | 描述                                                         | 类型      | 是否必选 |
| :----------------- | :------ | :----------------------------------------------------------- | :-------- | :------- |
| Tag                | Request | 表示任务的类型，哈希值计算默认为：FileHashCode。             | String    | 是       |
| Input              | Request | 包含待操作的文件信息。                                       | Container | 是       |
| Operation          | Request | 包含哈希值计算的处理规则。                                   | Container | 是       |
| QueueId            | Request | 任务所在的队列 ID。                                          | String    | 是       |
| CallBackFormat     | Request | 任务回调格式，JSON 或 XML，默认 XML，优先级高于队列的回调格式。 | String    | 否       |
| CallBackType       | Request | 任务回调类型，Url 或 TDMQ，默认 Url，优先级高于队列的回调类型。 | String    | 否       |
| CallBack           | Request | 任务回调的地址，优先级高于队列的回调地址。                   | String    | 否       |
| CallBackMqConfig   | Request | 任务回调 TDMQ 配置，当 CallBackType 为 TDMQ 时必填。详情见 [CallBackMqConfig](https://intl.cloud.tencent.com/document/product/1045/49945) | Container | 否       |

Container 类型 Input 的具体数据描述如下：

| 节点名称（关键字） | 父节点        | 描述                                         | 类型   | 是否必选 |
| :----------------- | :------------ | :------------------------------------------- | :----- | :------- |
| Object             | Request.Input | 文件名，取值为文件在当前存储桶中的完整名称。 | String | 是       |

Container 类型 Operation 的具体数据描述如下：

| 节点名称（关键字） | 父节点            | 描述                                            | 类型      | 是否必选 |
| :----------------- | :---------------- | :---------------------------------------------- | :-------- | :------- |
| FileHashCodeConfig | Request.Operation | 指定哈希值计算的处理规则。                      | Container | 是       |
| UserData           | Request.Operation | 透传用户信息, 可打印的 ASCII 码, 长度不超过1024 | String    | 否       |

Container 类型 FileHashCodeConfig 的具体数据描述如下：

| 节点名称（关键字） | 父节点                               | 描述                                                         | 类型   | 是否必选 |
| :----------------- | :----------------------------------- | :----------------------------------------------------------- | :----- | :------- |
| Type               | Request.Operation.FileHashCodeConfig | 哈希值的算法类型，有效值：MD5、SHA1、SHA256。                | String | 是       |
| AddToHeader        | Request.Operation.FileHashCodeConfig | 是否将计算得到的哈希值添加至文件自定义header, 有效值：true、false，默认值为 false。 自定义header根据`Type`的值变化，例如`Type`值为MD5时，自定义header为 x-cos-meta-md5。 | String | 否       |

#### 返回结果示例

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



## 查询哈希值计算结果

#### 功能说明

本接口用于主动查询指定的文件哈希值计算任务结果。

#### 方法原型

```php
public Guzzle\Service\Resource\Model getFileHashCodeResult(array $args = array());
```

#### 请求示例

```php
<?php

require dirname(__FILE__, 2) . '/vendor/autoload.php';

$secretId = "SECRETID"; //替换为用户的 secretId，请登录访问管理控制台进行查看和管理，https://console.cloud.tencent.com/cam/capi
$secretKey = "SECRETKEY"; //替换为用户的 secretKey，请登录访问管理控制台进行查看和管理，https://console.cloud.tencent.com/cam/capi
$region = "ap-beijing"; //替换为用户的 region，已创建桶归属的 region 可以在控制台查看，https://console.cloud.tencent.com/cos5/bucket
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', //协议头部，默认为http
        'credentials'=> array(
            'secretId'  => $secretId ,
            'secretKey' => $secretKey)));
try {
    // https://intl.cloud.tencent.com/document/product/436/53992 查询哈希值计算结果
    $result = $cosClient->getFileHashCodeResult(array(
        'Bucket' => 'examplebucket-1250000000', //存储桶名称，由 BucketName-Appid 组成，可以在 COS 控制台查看 https://console.cloud.tencent.com/cos5/bucket
        'Key' => '', // jobId
    ));
    // 请求成功
    print_r($result);
} catch (\Exception $e) {
    // 请求失败
    echo($e);
}
```

#### 参数说明

Request 中的具体数据描述如下：

| 参数名称 | 类型   | 描述                               | 是否必填 |
| :------- | :----- | :--------------------------------- | :------- |
| Bucket   | String | 存储桶名称，格式：BucketName-APPID | 是       |
| Key      | String | jobId                              | 是       |

#### 返回结果示例

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
