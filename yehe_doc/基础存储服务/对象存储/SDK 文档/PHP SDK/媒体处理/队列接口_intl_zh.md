## 简介

本文档提供关于媒体处理队列接口的 API 概览和 SDK 示例代码。

| API           | 操作描述                 |
| ------------- |  ---------------------- |
| 搜索媒体处理队列 | 搜索媒体处理队列。 |
| 更新媒体处理队列 | 更新媒体处理队列。 |


## 搜索媒体处理队列

#### 功能说明

搜索媒体处理队列。

#### 方法原型

```php
public Guzzle\Service\Resource\Model describeMediaQueues(array $args = array());
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
    // https://cloud.tencent.com/document/product/436/54045 搜索媒体处理队列
    $result = $cosClient->describeMediaQueues(array(
        'Bucket' => 'examplebucket-1250000000', //存储桶名称，由 BucketName-Appid 组成，可以在 COS 控制台查看 https://console.cloud.tencent.com/cos5/bucket
//        'QueueIds' => '', // 可选 队列 ID，以“,”符号分割字符串
//        'Category' => 'Transcoding', // 可选 CateAll：所有类型；Transcoding：媒体处理队列；SpeedTranscoding：媒体处理倍速转码队列；默认为 Transcoding。
//        'State' => 'Paused', // 可选 1. Active 表示队列内的作业会被媒体转码服务调度转码执行 2. Paused 表示队列暂停，作业不再会被媒体转码调度转码执行，队列内的所有作业状态维持在暂停状态，已经处于转码中的任务将继续转码，不受影响
//        'PageNumber' => '1', // 可选 第几页
//        'PageSize' => '2', // 可选 每页个数
    ));
    // 请求成功
    print_r($result);
} catch (\Exception $e) {
    // 请求失败
    echo($e);
}
```

#### 参数说明

请求参数描述如下：

| 参数名称（关键字） | 描述                                                         | 类型   | 是否必选 |
| :----------------- | :----------------------------------------------------------- | :----- | :------- |
| QueueIds           | 队列 ID，以“,”符号分割字符串。                               | String | 否       |
| State              | <li> Active 表示队列内的作业会被媒体处理服务调度执行。 <li> Paused 表示队列暂停，作业不再会被媒体处理调度执行，队列内的所有作业状态维持在暂停状态，已经执行中的任务不受影响。 | String | 否       |
| Category           | <li>  CateAll：所有类型。<li> Transcoding：媒体处理队列。<li>  SpeedTranscoding：媒体处理倍速转码队列。 <li> 默认为 Transcoding。 | String | 否       |
| PageNumber         | 第几页，默认值1。                                            | String | 否       |
| PageSize           | 每页个数，默认值10。                                         | String | 否       |

#### 返回结果示例

```php
GuzzleHttp\Command\Result Object
(
    [RequestId] => NjNkOGM2NmVfZTYxNmY5MSAASJPOJCIANSIDNAI=
    [ContentType] => application/xml
    [ContentLength] => 751
    [TotalCount] => 1
    [PageNumber] => 1
    [PageSize] => 10
    [QueueList] => Array
        (
            [0] => Array
                (
                    [BucketId] => examplebucket-1250000000
                    [QueueId] => pcc3ae89sa9d807fs89dg789sdg
                    [Name] => queue-1
                    [State] => Active
                    [MaxSize] => 10000
                    [MaxConcurrent] => 10
                    [Category] => Transcoding
                    [UpdateTime] => 2022-07-13T10:41:34+0800
                    [CreateTime] => 2022-07-13T10:41:34+0800
                    [NotifyConfig] => Array
                        (
                            [Url] => 
                            [State] => Off
                            [Type] => 
                            [Event] => 
                            [ResultFormat] => XML
                        )

                )

        )

    [Bucket] => examplebucket-1250000000
    [Location] => examplebucket-1250000000.ci.ap-guangzhou.myqcloud.com/queue
)
```



## 更新媒体处理队列

#### 功能说明

更新媒体处理队列。

#### 方法原型

```php
public Guzzle\Service\Resource\Model updateMediaQueue(array $args = array());
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
    // https://cloud.tencent.com/document/product/436/54046 更新媒体处理队列
    $result = $cosClient->updateMediaQueue(array(
        'Bucket' => 'examplebucket-1250000000', //存储桶名称，由 BucketName-Appid 组成，可以在 COS 控制台查看 https://console.cloud.tencent.com/cos5/bucket
        'Key' => 'xxx', // queueId
        'Name' => '', // 模板名称, 长度限制100字符
        'State' => 'Active', // 管道状态
        'NotifyConfig' => array(
            'State' => 'Off',
//            'Event' => '',
//            'ResultFormat' => '',
//            'Type' => '',
//            'Url' => '',
//            'MqMode' => '',
//            'MqRegion' => '',
//            'MqName' => '',
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

| 节点名称（关键字） | 父节点  | 描述                                                         | 类型      | 是否必选 | 默认值 | 限制 |
| :----------------- | :------ | :----------------------------------------------------------- | :-------- | :------- | :----- | :--- |
| Name               | Request | 队列名称，长度不超过128                                      | String    | 是       | 无     | 无   |
| State              | Request |<li> Active 表示队列内的作业会被媒体处理服务调度执行 <li>  Paused 表示队列暂停，作业不再会被媒体处理调度执行，队列内的所有作业状态维持在暂停状态，已经执行中的任务不受影响 | String    | 是       | 无     | 无   |
| NotifyConfig       | Request | 回调配置                                                     | Container | 是       | 无     | 无   |

Container 节点 NotifyConfig 的内容：

| 节点名称（关键字） | 父节点               | 描述             | 类型   | 是否必选                           | 默认值 | 限制                                                         |
| :----------------- | :------------------- | :--------------- | :----- | :--------------------------------- | :----- | :----------------------------------------------------------- |
| State              | Request.NotifyConfig | 回调开关，Off/On | String | 否                                 | Off    | On/Off                                                       |
| Event              | Request.NotifyConfig | 回调事件         | String | 当 State=On 时, 必选               | 无     | 任务完成：TaskFinish；工作流完成：WorkflowFinish             |
| ResultFormat       | Request.NotifyConfig | 回调格式         | String | 否                                 | XML    | JSON/XML                                                     |
| Type               | Request.NotifyConfig | 回调类型         | String | 当 State=On 时, 必选               | 无     | Url 或 TDMQ                                                  |
| Url                | Request.NotifyConfig | 回调地址         | String | 当 State=On, 且 Type=Url 时, 必选  | 无     | 不能为内网地址                                               |
| MqMode             | Request.NotifyConfig | TDMQ 使用模式    | String | 当 State=On, 且 Type=TDMQ 时, 必选 | Queue  | 主题订阅：Topic 队列服务: Queue                              |
| MqRegion           | Request.NotifyConfig | TDMQ 所属园区    | String | 当 State=On, 且 Type=TDMQ 时, 必选 | 无     | 目前支持园区 sh（上海）、bj（北京）、gz（广州）、cd（成都）、hk（中国香港） |
| MqName             | Request.NotifyConfig | TDMQ 主题名称    | String | 当 State=On, 且 Type=TDMQ 时, 必选 | 无     | 无                                                           |

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

    [RequestId] => NjNkOGM2NmVfZTYxNmY5MSAASJPOJCIANSIDNAI=
    [ContentType] => application/xml
    [ContentLength] => 668
    [Key] => fcd32dbdaa13b11esa9ds8g0d98gd0h85
    [Bucket] => examplebucket-1250000000
    [Location] => examplebucket-1250000000.ci.ap-guangzhou.myqcloud.com/queue/fcd32dbdaa13b11esa9ds8g0d98gd0h85
    [Response] => Array
        (
            [RequestId] => NjNkOGM2NmVfZTYxNmY5MSAASJPOJCIANSIDNAI=
            [Queue] => Array
                (
                    [QueueId] => fcd32dbdaa13b11esa9ds8g0d98gd0h85
                    [Name] => media-queue-1
                    [State] => Active
                    [NotifyConfig] => Array
                        (
                            [Url] => 
                            [Event] => 
                            [Type] => 
                            [State] => Off
                            [ResultFormat] => XML
                            [MqMode] => 
                            [MqName] => 
                            [MqRegion] => 
                        )

                    [MaxSize] => 10000
                    [MaxConcurrent] => 10
                    [CreateTime] => 2022-07-13T10:41:34+0800
                    [UpdateTime] => 2023-01-31T17:32:18+0800
                    [BucketId] => examplebucket-1250000000
                    [Category] => Transcoding
                )

        )

)
```
