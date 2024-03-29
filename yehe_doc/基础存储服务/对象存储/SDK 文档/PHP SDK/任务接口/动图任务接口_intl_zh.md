## 简介

本文档提供关于提交动图任务的 API 概览和 SDK 示例代码。

| API           | 操作描述                 |
| ------------- |  ---------------------- |
| [提交动图任务](https://intl.cloud.tencent.com/document/product/436/49045) | 提交一个动图任务 |


## 提交动图任务

#### 功能说明

用于提交一个动图任务。

#### 方法原型

```php
public Guzzle\Service\Resource\Model createMediaAnimationJobs(array $args = array());
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
    $result = $cosClient->createMediaAnimationJobs(array(
        'Bucket' => 'examplebucket-1250000000', //存储桶名称，由 BucketName-Appid 组成，可以在 COS 控制台查看 https://console.cloud.tencent.com/cos5/bucket
        'Tag' => 'Animation',
        'QueueId' => 'p81e648af2aee49688xxxxxxxxxxxxxxxx',
        'Input' => array(
            'Object' => 'video01.mp4'
        ),
        'Operation' => array(
            'TemplateId' => 't1de276cbdab16xxxxxxxxxxxxxxxxxxxxx',
            'Output' => array(
                'Region' => $region,
                'Bucket' => 'examplebucket-1250000000', //存储桶名称，由 BucketName-Appid 组成，可以在 COS 控制台查看 https://console.cloud.tencent.com/cos5/bucket
                'Object' => 'Animation.gif',
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
    $result = $cosClient->createMediaAnimationJobs(array(
        'Bucket' => 'examplebucket-1250000000', //存储桶名称，由 BucketName-Appid 组成，可以在 COS 控制台查看 https://console.cloud.tencent.com/cos5/bucket
        'Tag' => 'Animation',
        'QueueId' => 'p81e648af2aee49688xxxxxxxxxxxxxxxx',
        'Input' => array(
            'Object' => 'video01.mp4'
        ),
        'Operation' => array(
            'Animation' => array(
                'Container' => array(
                    'Format' => '',
                ),
                'Video' => array(
                    'Codec' => '',
                    'Width' => '',
                    'Height' => '',
                    'Fps' => '',
                    'AnimateOnlyKeepKeyFrame' => '',
                    'AnimateTimeIntervalOfFrame' => '',
                    'AnimateFramesPerSecond' => '',
                    'Quality' => '',
                ),
                'TimeInterval' => array(
                    'Start' => '',
                    'Duration' => '',
                ),
            ),
            'Output' => array(
                'Region' => $region,
                'Bucket' => 'examplebucket-1250000000', //存储桶名称，由 BucketName-Appid 组成，可以在 COS 控制台查看 https://console.cloud.tencent.com/cos5/bucket
                'Object' => 'Animation.gif',
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
| Tag                | Request | 创建任务的 Tag：Animation                                    | String    | 是       |
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
| Animation          | Request.Operation | 指定该任务的参数                                             | Container | 否       |
| TemplateId         | Request.Operation | 指定的模板 ID                                                | String    | 否       |
| Output             | Request.Operation | 结果输出地址                                                 | Container | 是       |
| UserData           | Request.Operation | 透传用户信息, 可打印的 ASCII 码, 长度不超过1024              | String    | 否       |
| JobLevel           | Request.Operation | 任务优先级，级别限制：0 、1 、2。级别越大任务优先级越高，默认为0 | String    | 否       |

>!
>
> 优先使用 TemplateId，无 TemplateId 时使用 Animation。

Container 类型 Animation 的具体数据描述如下：

| 节点名称（关键字） | 父节点                      | 描述                                                         | 类型      | 是否必选 |
| :----------------- | :-------------------------- | :----------------------------------------------------------- | :-------- | :------- |
| Container          | Request.Operation.Animation | 同动图模板 [CreateMediaTemplate](https://intl.cloud.tencent.com/document/product/1045/49906) 接口中的 Request.Container | Container | 否       |
| Video              | Request.Operation.Animation | 同动图模板 [CreateMediaTemplate](https://intl.cloud.tencent.com/document/product/1045/49906) 接口中的 Request.Video | Container | 否       |
| TimeInterval       | Request.Operation.Animation | 同动图模板 [CreateMediaTemplate](https://intl.cloud.tencent.com/document/product/1045/49906) 接口中的 Request.TimeInterval | Container | 否       |

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

    [RequestId] => NjI2MTQHOAIHDOIDUOIA7879ADJOIMDc2YTk=
    [ContentType] => application/xml
    [ContentLength] => 797
    [Bucket] => examplebucket-1250000000
    [Location] => examplebucket-1250000000.ci.ap-beijing.myqcloud.com/jobs
    [Response] => Array
        (
            [JobsDetail] => Array
                (
                    [Code] => Success
                    [CreationTime] => 2022-04-21T19:29:36+0800
                    [EndTime] => -
                    [Input] => Array
                        (
                            [BucketId] => examplebucket-1250000000
                            [Object] => video01.mp4
                            [Region] => ap-beijing
                        )

                    [JobId] => j5318zx9c890zx8c0z98c0fa6355174de
                    [Message] => 
                    [Operation] => Array
                        (
                            [Output] => Array
                                (
                                    [Bucket] => examplebucket-1250000000
                                    [Object] => Animation.gif
                                    [Region] => ap-beijing
                                )

                            [TemplateId] => t1de276cbdz78xcz09xc80zx901af71
                            [TemplateName] => Animation-gif-1
                            [UserData] => xxx
                            [JobLevel] => 0
                        )

                    [QueueId] => p81e648af2aeez87c6z78xc7z98xc79ca86
                    [StartTime] => -
                    [State] => Submitted
                    [Tag] => Animation
                )

        )

)
```

