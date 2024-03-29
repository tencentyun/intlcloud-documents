## 简介

本文档提供关于提交人声分离任务的 API 概览和 SDK 示例代码。

| API           | 操作描述                 |
| ------------- |  ---------------------- |
| [提交人声分离任务](https://intl.cloud.tencent.com/document/product/436/49063) | 提交一个人声分离任务 |


## 提交人声分离任务

#### 功能说明

用于提交一个人声分离任务。

#### 方法原型

```php
public Guzzle\Service\Resource\Model createMediaVoiceSeparateJobs(array $args = array());
```

#### 请求示例

#### 示例一： 使用模板

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
    $result = $cosClient->createMediaVoiceSeparateJobs(array(
        'Bucket' => 'examplebucket-1250000000', //存储桶名称，由 BucketName-Appid 组成，可以在 COS 控制台查看 https://console.cloud.tencent.com/cos5/bucket
        'Tag' => 'VoiceSeparate',
        'QueueId' => '',
        'CallBack' => '',
        'Input' => array(
            'Object' => 'test.mp3'
        ),
        'Operation' => array(
            'TemplateId' => '',
            'Output' => array(
                'Region' => $region,
                'Bucket' => 'examplebucket-1250000000', //存储桶名称，由 BucketName-Appid 组成，可以在 COS 控制台查看 https://console.cloud.tencent.com/cos5/bucket
                'Object' => 'VoiceSeparate01.mp3',
                'AuObject' => 'VoiceSeparate02.mp3',
            ),
//            'UserData' => 'xxx', // 透传用户信息
//            'JobLevel' => '0', // 任务优先级，级别限制：0 、1 、2。级别越大任务优先级越高，默认为0
        ),
    ));
    // 请求成功
    print_r($result);
} catch (\Exception $e) {
    // 请求失败
    echo($e);
}
```

#### 示例二： 自定义参数

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
    $result = $cosClient->createMediaVoiceSeparateJobs(array(
        'Bucket' => 'examplebucket-1250000000', //存储桶名称，由 BucketName-Appid 组成，可以在 COS 控制台查看 https://console.cloud.tencent.com/cos5/bucket
        'Tag' => 'VoiceSeparate',
        'QueueId' => '',
        'CallBack' => '',
        'Input' => array(
            'Object' => 'test.mp3'
        ),
        'Operation' => array(
            'Output' => array(
                'Region' => $region,
                'Bucket' => 'examplebucket-1250000000', //存储桶名称，由 BucketName-Appid 组成，可以在 COS 控制台查看 https://console.cloud.tencent.com/cos5/bucket
                'Object' => 'VoiceSeparate01.mp3',
                'AuObject' => 'VoiceSeparate02.mp3',
            ),
            'VoiceSeparate' => array(
                'AudioMode' => 'AudioAndBackground',
                'AudioConfig' => array(
                    'Codec' => 'mp3',
                    'Samplerate' => '11025',
                    'Bitrate' => '256',
                    'Channels' => '2',
                ),
            ),
//            'UserData' => 'xxx', // 透传用户信息
//            'JobLevel' => '0', // 任务优先级，级别限制：0 、1 、2。级别越大任务优先级越高，默认为0
        ),
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
| Tag                | Request | 创建任务的 Tag：VoiceSeparate                                | String    | 是       |
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
| VoiceSeparate      | Request.Operation | 指定转码模板参数                                             | Container | 否       |
| TemplateId         | Request.Operation | 指定的模板 ID                                                | String    | 否       |
| Output             | Request.Operation | 结果输出地址                                                 | Container | 是       |
| JobLevel           | Request.Operation | 任务优先级，级别限制：0 、1 、2。级别越大任务优先级越高，默认为0 | String    | 否       |

>!
>
> 优先使用 TemplateId，无 TemplateId 时使用 VoiceSeparate。

Container 类型 VoiceSeparate 的具体数据描述如下：

| 节点名称（关键字） | 父节点                          | 描述                                                         | 类型      | 是否必选 |
| :----------------- | :------------------------------ | :----------------------------------------------------------- | :-------- | :------- |
| AudioMode          | Request.Operation.VoiceSeparate | 同创建人声分离模板 [CreateMediaTemplate](https://intl.cloud.tencent.com/document/product/1045/49916) 接口中的 Request.AudioMode | Container | 否       |
| AudioConfig        | Request.Operation.VoiceSeparate | 同创建人声分离模板 [CreateMediaTemplate](https://intl.cloud.tencent.com/document/product/1045/49916) 接口中的 Request.AudioConfig | Container | 否       |

Container 类型 Output 的具体数据描述如下：

| 节点名称（关键字） | 父节点                     | 描述                                       | 类型   | 是否必选 |
| :----------------- | :------------------------- | :----------------------------------------- | :----- | :------- |
| Region             | Request.Operation.Output   | 存储桶的地域                               | String | 是       |
| Bucket             | Request.Operation.Output   | 存储结果的存储桶                           | String | 是       |
| Object             | Request.Operation.Output   | 背景音结果文件名，不能与 AuObject 同时为空 | String | 否       |
| AuObject           | Request.Operation.AuObject | 人声结果文件名，不能与 Object 同时为空     | String | 否       |

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

    [RequestId] => NjI2MjIyOTHADOHDOADJHOjQ0OV8yMmU0OWM=
    [ContentType] => application/xml
    [ContentLength] => 857
    [Bucket] => examplebucket-1250000000
    [Location] => examplebucket-1250000000.ci.ap-beijing.myqcloud.com/jobs
    [Response] => Array
        (
            [JobsDetail] => Array
                (
                    [Code] => Success
                    [CreationTime] => 2022-04-22T11:35:47+0800
                    [EndTime] => -
                    [Input] => Array
                        (
                            [BucketId] => examplebucket-1250000000
                            [Object] => test.mp3
                            [Region] => ap-beijing
                        )

                    [JobId] => j4c70446zxc780z98xc09zxc6eb232
                    [Message] => 
                    [Operation] => Array
                        (
                            [Output] => Array
                                (
                                    [AuObject] => VoiceSeparate02.mp3
                                    [Bucket] => examplebucket-1250000000
                                    [Object] => VoiceSeparate01.mp3
                                    [Region] => ap-beijing
                                )

                            [TemplateId] => t1456ea89fczx8c0z8c09z8c0985
                            [TemplateName] => VoiceSeparate-1
                            [UserData] => xxx
                            [JobLevel] => 0
                        )

                    [QueueId] => p81e648af2azc709zx8c09z8xc0z7be086
                    [StartTime] => -
                    [State] => Submitted
                    [Tag] => VoiceSeparate
                )

        )

)
```

