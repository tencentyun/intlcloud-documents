## 简介

本文档提供关于数字水印任务接口的 API 概览和 SDK 示例代码。

| API           | 操作描述                 |
| ------------- |  ---------------------- |
| [添加数字水印任务](https://intl.cloud.tencent.com/document/product/436/49047) | 提交一个嵌入数字水印任务。 |
| [提取数字水印任务](https://intl.cloud.tencent.com/document/product/436/49048) | 提交一个提取数字水印任务。 |


## 添加数字水印任务

#### 功能说明

提交一个嵌入数字水印任务。

#### 方法原型

```php
public Guzzle\Service\Resource\Model createMediaDigitalWatermarkJobs(array $args = array());
```

#### 请求示例

```php
<?php

require dirname(__FILE__) . '/../vendor/autoload.php';

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
    // 嵌入数字水印任务 https://intl.cloud.tencent.com/document/product/436/49047
    $result = $cosClient->createMediaDigitalWatermarkJobs(array(
        'Bucket' => 'examplebucket-1250000000', //存储桶名称，由 BucketName-Appid 组成，可以在 COS 控制台查看 https://console.cloud.tencent.com/cos5/bucket
        'Tag' => 'DigitalWatermark',
        'QueueId' => 'p81e648af2aee496885707caxxxxxxxxxxxx',
        'Input' => array(
            'Object' => 'video01.mp4'
        ),
        'Operation' => array(
            'DigitalWatermark' => array(
                'Message' => '123456789ab',
                'Type' => 'Text',
                'Version' => 'V1',
            ),
            'Output' => array(
                'Region' => $region,
                'Bucket' => 'examplebucket-1250000000', //存储桶名称，由 BucketName-Appid 组成，可以在 COS 控制台查看 https://console.cloud.tencent.com/cos5/bucket
                'Object' => 'DigitalWatermark.mp4',
            ),
//            'UserData' => 'xxx', // 透传用户信息
//            'JobLevel' => '0', // 任务优先级，级别限制：0 、1 、2。级别越大任务优先级越高，默认为0
        ),
        'CallBack' => '',
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
| Tag                | Request | 创建任务的 Tag：DigitalWatermark                             | String    | 是       |
| Input              | Request | 待操作的媒体信息                                             | Container | 是       |
| Operation          | Request | 操作规则                                                     | Container | 是       |
| QueueId            | Request | 任务所在的队列 ID                                            | String    | 是       |
| CallBackFormat     | Request | 任务回调格式，JSON 或 XML，默认 XML，优先级高于队列的回调格式 | String    | 否       |
| CallBackType       | Request | 任务回调类型，Url 或 TDMQ，默认 Url，优先级高于队列的回调类型 | String    | 否       |
| CallBack           | Request | 任务回调地址，优先级高于队列的回调地址。设置为 no 时，表示队列的回调地址不产生回调 | String    | 否       |
| CallBackMqConfig   | Request | 任务回调 TDMQ 配置，当 CallBackType 为 TDMQ 时必填。详情见 [CallBackMqConfig](https://intl.cloud.tencent.com/document/product/1045/49945) | Container | 否       |

Container 类型 Input 的具体数据描述如下：

| 节点名称（关键字） | 父节点        | 描述       | 类型   | 是否必选 |
| :----------------- | :------------ | :--------- | :----- | :------- |
| Object             | Request.Input | 媒体文件名 | String | 是       |


Container 类型 Operation 的具体数据描述如下：

| 节点名称（关键字） | 父节点            | 描述                                                         | 类型      | 是否必选 |
| :----------------- | :---------------- | :----------------------------------------------------------- | :-------- | :------- |
| Output             | Request.Operation | 结果输出地址                                                 | Container | 是       |
| DigitalWatermark   | Request.Operation | 数字水印配置                                                 | Container | 是       |
| JobLevel           | Request.Operation | 任务优先级，级别限制：0 、1 、2。级别越大任务优先级越高，默认为0 | String    | 否       |
| UserData           | Request.Operation | 透传用户信息，可打印的 ASCII 码, 长度不超过1024              | String    | 否       |

Container 类型 DigitalWatermark 的具体数据类型描述如下：

| 节点名称（关键字） | 父节点                             | 描述                     | 类型   | 是否必选 | 限制                                                |
| :----------------- | :--------------------------------- | :----------------------- | :----- | :------- | :-------------------------------------------------- |
| Message            | Request.Operation.DigitalWatermark | 数字水印嵌入的字符串信息 | string | 是       | 长度不超过64个字符，仅支持中文、英文、数字、_、-和* |
| Type               | Request.Operation.DigitalWatermark | 水印类型                 | String | 是       | Text                                                |
| Version            | Request.Operation.DigitalWatermark | 水印版本                 | String | 是       | V1                                                  |

Container 类型 Output 的具体数据描述如下：

| 节点名称（关键字） | 父节点                   | 描述             | 类型   | 是否必选 |
| :----------------- | :----------------------- | :--------------- | :----- | :------- |
| Region             | Request.Operation.Output | 存储桶的地域     | String | 是       |
| Bucket             | Request.Operation.Output | 存储结果的存储桶 | String | 是       |
| Object             | Request.Operation.Output | 输出结果的文件名 | String | 是       |

#### 返回结果示例

```php
GuzzleHttp\Command\Result Object
(
    [Body] => GuzzleHttp\Psr7\Stream Object
        (
            [stream:GuzzleHttp\Psr7\Stream:private] => Resource id #88
            [size:GuzzleHttp\Psr7\Stream:private] => 
            [seekable:GuzzleHttp\Psr7\Stream:private] => 1
            [readable:GuzzleHttp\Psr7\Stream:private] => 1
            [writable:GuzzleHttp\Psr7\Stream:private] => 1
            [uri:GuzzleHttp\Psr7\Stream:private] => php://temp
            [customMetadata:GuzzleHttp\Psr7\Stream:private] => Array
                (
                )

        )

    [RequestId] => NjI2N2JlMDFfZmNjYAJSDIOAJDOIAJD9lZDYxOA==
    [ContentType] => application/xml
    [ContentLength] => 828
    [Bucket] => examplebucket-1250000000
    [Location] => examplebucket-1250000000.ci.ap-guangzhou.myqcloud.com/jobs
    [Response] => Array
        (
            [JobsDetail] => Array
                (
                    [Code] => Success
                    [CreationTime] => 2022-04-26T17:40:17+0800
                    [EndTime] => -
                    [Input] => Array
                        (
                            [BucketId] => examplebucket-1250000000
                            [Object] => video01.mp4
                            [Region] => ap-guangzhou
                        )

                    [JobId] => je1dc03f0c544as09d8as09d8a09dec25a93
                    [Message] => 
                    [Operation] => Array
                        (
                            [DigitalWatermark] => Array
                                (
                                    [Message] => 123456789ab
                                    [Type] => Text
                                    [Version] => V1
                                )

                            [Output] => Array
                                (
                                    [Bucket] => examplebucket-1250000000
                                    [Object] => DigitalWatermark.mp4
                                    [Region] => ap-guangzhou
                                )
                            [UserData] => xxx
                            [JobLevel] => 0

                        )

                    [QueueId] => p81e648af2aee49688570s8a90d80a9d86
                    [StartTime] => -
                    [State] => Submitted
                    [Tag] => DigitalWatermark
                )

        )

)
```




## 提取数字水印任务

#### 功能说明

提交一个提取数字水印任务。

#### 方法原型

```php
public Guzzle\Service\Resource\Model createMediaExtractDigitalWatermarkJobs(array $args = array());
```

#### 请求示例

```php
<?php

require dirname(__FILE__) . '/../vendor/autoload.php';

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
    // 提取数字水印任务 https://intl.cloud.tencent.com/document/product/436/49048
    $result = $cosClient->createMediaExtractDigitalWatermarkJobs(array(
        'Bucket' => 'examplebucket-1250000000', //存储桶名称，由 BucketName-Appid 组成，可以在 COS 控制台查看 https://console.cloud.tencent.com/cos5/bucket
        'Tag' => 'ExtractDigitalWatermark',
        'QueueId' => 'p81e648af2aee496885707caxxxxxxxxx',
        'Input' => array(
            'Object' => 'DigitalWatermark.mp4'
        ),
        'Operation' => array(
            'ExtractDigitalWatermark' => array(
                'Type' => 'Text',
                'Version' => 'V1',
            ),
//            'UserData' => 'xxx', // 透传用户信息
//            'JobLevel' => '0', // 任务优先级，级别限制：0 、1 、2。级别越大任务优先级越高，默认为0
        ),
        'CallBack' => '',
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
| Tag                | Request | 创建任务的 Tag：ExtractDigitalWatermark                      | String    | 是       |
| Input              | Request | 待操作的媒体信息                                             | Container | 是       |
| Operation          | Request | 操作规则                                                     | Container | 是       |
| QueueId            | Request | 任务所在的队列 ID                                            | String    | 是       |
| CallBackFormat     | Request | 任务回调格式，JSON 或 XML，默认 XML，优先级高于队列的回调格式 | String    | 否       |
| CallBackType       | Request | 任务回调类型，Url 或 TDMQ，默认 Url，优先级高于队列的回调类型 | String    | 否       |
| CallBack           | Request | 任务回调地址，优先级高于队列的回调地址。设置为 no 时，表示队列的回调地址不产生回调 | String    | 否       |
| CallBackMqConfig   | Request | 任务回调 TDMQ 配置，当 CallBackType 为 TDMQ 时必填。详情见 [CallBackMqConfig](https://intl.cloud.tencent.com/document/product/1045/49945) | Container | 否       |

Container 类型 Input 的具体数据描述如下：

| 节点名称（关键字） | 父节点        | 描述       | 类型   | 是否必选 |
| :----------------- | :------------ | :--------- | :----- | :------- |
| Object             | Request.Input | 媒体文件名 | String | 是       |


Container 类型 Operation 的具体数据描述如下：

| 节点名称（关键字）      | 父节点            | 描述                                                         | 类型      | 是否必选 |
| :---------------------- | :---------------- | :----------------------------------------------------------- | :-------- | :------- |
| ExtractDigitalWatermark | Request.Operation | 提取数字水印配置                                             | Container | 是       |
| JobLevel                | Request.Operation | 任务优先级，级别限制：0 、1 、2。级别越大任务优先级越高，默认为0 | String    | 否       |
| UserData                | Request.Operation | 透传用户信息，可打印的 ASCII 码, 长度不超过1024              | String    | 否       |

Container 类型 ExtractDigitalWatermark 的具体数据类型描述如下：

| 节点名称（关键字） | 父节点                                    | 描述     | 类型   | 是否必选 | 限制 |
| :----------------- | :---------------------------------------- | :------- | :----- | :------- | :--- |
| Type               | Request.Operation.ExtractDigitalWatermark | 水印类型 | String | 是       | Text |
| Version            | Request.Operation.ExtractDigitalWatermark | 水印版本 | String | 是       | V1   |

#### 返回结果示例

```php
GuzzleHttp\Command\Result Object
(
    [Body] => GuzzleHttp\Psr7\Stream Object
        (
            [stream:GuzzleHttp\Psr7\Stream:private] => Resource id #88
            [size:GuzzleHttp\Psr7\Stream:private] => 
            [seekable:GuzzleHttp\Psr7\Stream:private] => 1
            [readable:GuzzleHttp\Psr7\Stream:private] => 1
            [writable:GuzzleHttp\Psr7\Stream:private] => 1
            [uri:GuzzleHttp\Psr7\Stream:private] => php://temp
            [customMetadata:GuzzleHttp\Psr7\Stream:private] => Array
                (
                )

        )

    [RequestId] => NjI2OGI4YmZfZmNjYTNiAOISDAOIDUOMjU4ZjE=
    [ContentType] => application/xml
    [ContentLength] => 680
    [Bucket] => examplebucket-1250000000
    [Location] => examplebucket-1250000000.ci.ap-guangzhou.myqcloud.com/jobs
    [Response] => Array
        (
            [JobsDetail] => Array
                (
                    [Code] => Success
                    [CreationTime] => 2022-04-27T11:30:07+0800
                    [EndTime] => -
                    [Input] => Array
                        (
                            [BucketId] => examplebucket-1250000000
                            [Object] => DigitalWatermark.mp4
                            [Region] => ap-guangzhou
                        )

                    [JobId] => j56038a4cc5da1a8s0d98a90sd806cf06
                    [Message] => 
                    [Operation] => Array
                        (
                            [ExtractDigitalWatermark] => Array
                                (
                                    [Type] => Text
                                    [Version] => V1
                                )
                            [UserData] => xxx
                            [JobLevel] => 0
                        )

                    [QueueId] => p81e648af2aee4z9x8c09z8xc09zbe086
                    [StartTime] => -
                    [State] => Submitted
                    [Tag] => ExtractDigitalWatermark
                )

        )

)
```

