## 简介

本文档提供关于视频标签任务接口的 API 概览和 SDK 示例代码。

| API                                                          | 操作描述         |
| ------------------------------------------------------------ | ---------------- |
| [提交视频标签任务](https://intl.cloud.tencent.com/document/product/436/49062) | 提交视频标签任务 |


## 提交视频标签任务

#### 功能说明

提交视频标签任务。

#### 方法原型

```php
public Guzzle\Service\Resource\Model createMediaVideoTagJobs(array $args = array());
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
    // 提交视频标签任务 https://cloud.tencent.com/document/product/436/67202
    $result = $cosClient->createMediaVideoTagJobs(array(
        'Bucket' => 'examplebucket-1250000000', //存储桶名称，由 BucketName-Appid 组成，可以在 COS 控制台查看 https://console.cloud.tencent.com/cos5/bucket
        'Tag' => 'VideoTag',
        'QueueId' => 'p81e648af2aee496885707ca0xxxxxxxxx',
        'Input' => array(
            'Object' => 'video01.mp4'
        ),
        'Operation' => array(
            'VideoTag' => array(
                'Scenario' => 'Stream',
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
| Tag                | Request | 创建任务的 Tag：VideoTag                                     | String    | 是       |
| Input              | Request | 待操作的媒体信息                                             | Container | 是       |
| Operation          | Request | 操作规则                                                     | Container | 是       |
| QueueId            | Request | 任务所在的队列 ID                                            | String    | 是       |
| CallBackFormat     | Request | 任务回调格式，JSON 或 XML，默认 XML，优先级高于队列的回调格式 | String    | 否       |
| CallBackType       | Request | 任务回调类型，Url 或 TDMQ，默认 Url，优先级高于队列的回调类型 | String    | 否       |
| CallBack           | Request | 任务回调地址，优先级高于队列的回调地址。设置为 no 时，表示队列的回调地址不产生回调 | String    | 否       |
| CallBackMqConfig   | Request | 任务回调 TDMQ 配置，当 CallBackType 为 TDMQ 时必填。详情见 [CallBackMqConfig](https://intl.cloud.tencent.com/document/product/1045/49945) | Container | 否       |

Container 类型 Input 的具体数据描述如下：

| 节点名称（关键字） | 父节点        | 描述                                                         | 类型   | 是否必选 |
| :----------------- | :------------ | :----------------------------------------------------------- | :----- | :------- |
| Object             | Request.Input | 执行视频标签任务的媒体文件名，目前支持 mp4、avi、mkv、wmv、rmvb、flv、mov 封装格式，视频时长超过30min的视频请 [提交工单](https://console.cloud.tencent.com/workorder/category) 处理 | String | 是       |


Container 类型 Operation 的具体数据描述如下：

| 节点名称（关键字） | 父节点                        | 描述                                                         | 类型      | 是否必选 |
| :----------------- | :---------------------------- | :----------------------------------------------------------- | :-------- | :------- |
| VideoTag           | Request.Operation             | 指定该 VideoTag 任务参数                                     | Container | 是       |
| JobLevel           | Request.Operation             | 任务优先级，级别限制：0 、1 、2。级别越大任务优先级越高，默认为0 | String    | 否       |
| UserData           | Response.JobsDetail.Operation | 透传用户信息                                                 | String    | 否       |

Container 类型 VideoTag 的具体数据描述如下：

| 节点名称（关键字） | 父节点                     | 描述                                                         | 类型   | 是否必选 | 限制                       |
| :----------------- | :------------------------- | :----------------------------------------------------------- | :----- | :------- | :------------------------- |
| Scenario           | Request.Operation.VideoTag | 场景类型，可选择视频标签的运用场景，不同的运用场景使用的算法、输入输出等都会有所差异 | string | 是       | 当前版本只适配 Stream 场景 |

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

    [RequestId] => NjI2OTI2ZTdfZaOAUSIODUJAIODJAIODViNWQ=
    [ContentType] => application/xml
    [ContentLength] => 610
    [Bucket] => examplebucket-1250000000
    [Location] => examplebucket-1250000000.ci.ap-guangzhou.myqcloud.com/jobs
    [Response] => Array
        (
            [JobsDetail] => Array
                (
                    [Code] => Success
                    [CreationTime] => 2022-04-27T19:20:07+0800
                    [EndTime] => -
                    [Input] => Array
                        (
                            [BucketId] => examplebucket-1250000000
                            [Object] => video01.mp4
                            [Region] => ap-guangzhou
                        )

                    [JobId] => jfe591374c61b11ec9ad8a098sd09asd8aa
                    [Message] => 
                    [Operation] => Array
                        (
                            [VideoTag] => Array
                                (
                                    [Scenario] => Stream
                                )
                            [UserData] => xxx
                            [JobLevel] => 0
                        )

                    [QueueId] => p81e648af2aeea8d90a8s90d8a0de086
                    [StartTime] => -
                    [State] => Submitted
                    [Tag] => VideoTag
                )

        )

)
```



