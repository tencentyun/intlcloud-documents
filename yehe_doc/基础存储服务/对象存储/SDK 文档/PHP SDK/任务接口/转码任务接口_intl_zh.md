## 简介

本文档提供关于提交转码任务的 API 概览和 SDK 示例代码。

| API           | 操作描述                 |
| ------------- |  ---------------------- |
| [提交转码任务](https://www.tencentcloud.com/document/product/436/49058) | 提交转码任务 |


## 提交转码任务

#### 功能说明

提交转码任务。

#### 方法原型

```php
public Guzzle\Service\Resource\Model createMediaTranscodeJobs(array $args = array());
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
    $result = $cosClient->createMediaTranscodeJobs(array(
        'Bucket' => 'examplebucket-1250000000', //存储桶名称，由 BucketName-Appid 组成，可以在 COS 控制台查看 https://console.cloud.tencent.com/cos5/bucket
        'Tag' => 'Transcode',
        'QueueId' => 'paaf4fce5521a40888a3034a5de80f6ca',
        'Input' => array(
            'Object' => 'example.mp4'
        ),
        'Operation' => array(
            'TemplateId' => 't04e1ab86554984f1aa17c062fbf6c007c',
//            'UserData' => 'xxx', // 透传用户信息
//            'JobLevel' => '0', // 任务优先级，级别限制：0 、1 、2。级别越大任务优先级越高，默认为0
            'Output' => array(
                'Region' => $region,
                'Bucket' => 'examplebucket-1250000000', //存储桶名称，由 BucketName-Appid 组成，可以在 COS 控制台查看 https://console.cloud.tencent.com/cos5/bucket
                'Object' => 'video02.mp4',
            ),
            'Watermark' => array(
                array(
                    'Type' => 'Text',
                    'LocMode' => 'Absolute',
                    'Dx' => '64',
                    'Dy' => '64',
                    'Pos' => 'TopRight',
                    'Text' => array(
                        'Text' => '第一个水印',
                        'FontSize' => '30',
                        'FontType' => 'simfang.ttf',
                        'FontColor' => '#99ff00',
                        'Transparency' => '100', // 不透明度
                     ),
                ),
                array(
                    'Type' => 'Text',
                    'LocMode' => 'Absolute',
                    'Dx' => '64',
                    'Dy' => '64',
                    'Pos' => 'TopLeft',
                    'Text' => array(
                        'Text' => '第二个水印',
                        'FontSize' => '30',
                        'FontType' => 'simfang.ttf',
                        'FontColor' => '#99ff00',
                        'Transparency' => '100', // 不透明度
                     ),
                ),
            ),
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
        'schema' => 'https', //协议头部，默认为http
        'credentials'=> array(
            'secretId'  => $secretId ,
            'secretKey' => $secretKey)));
try {
    $result = $cosClient->createMediaTranscodeJobs(array(
        'Bucket' => 'examplebucket-1250000000', //存储桶名称，由 BucketName-Appid 组成，可以在 COS 控制台查看 https://console.cloud.tencent.com/cos5/bucket
        'Tag' => 'Transcode',
        'QueueId' => 'asdadadfafsdkjhfjghdfjg',
        'CallBack' => 'https://example.com/callback',
        'Input' => array(
            'Object' => 'video01.mp4'
        ),
        'Operation' => array(
//            'UserData' => 'xxx', // 透传用户信息
//            'JobLevel' => '0', // 任务优先级，级别限制：0 、1 、2。级别越大任务优先级越高，默认为0
            'Output' => array(
                'Region' => $region,
                'Bucket' => 'examplebucket-1250000000', //存储桶名称，由 BucketName-Appid 组成，可以在 COS 控制台查看 https://console.cloud.tencent.com/cos5/bucket
                'Object' => 'video01.mkv',
            ),
            'Transcode' => array(
                'Container' => array(
                    'Format' => 'mp4'
                ),
                'Video' => array(
                    'Codec' => 'H.264',
                    'Profile' => 'high',
                    'Bitrate' => '1000',
                    'Preset' => 'medium',
                    'Width' => '1280',
                    'Fps' => '30',
                ),
                'Audio' => array(
                    'Codec' => 'aac',
                    'Samplerate' => '44100',
                    'Bitrate' => '128',
                    'Channels' => '4',
                ),
                'TransConfig' => array(
                    'AdjDarMethod' => 'scale',
                    'IsCheckReso' => 'false',
                    'ResoAdjMethod' => '1',
                ),
                'TimeInterval' => array(
                    'Start' => '0',
                    'Duration' => '60',
                ),
            ),
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
| Tag                | Request | 创建任务的 Tag：Transcode                                    | String    | 是       |
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

| 节点名称（关键字）  | 父节点            | 描述                                                         | 类型      | 是否必选 |
| :------------------ | :---------------- | :----------------------------------------------------------- | :-------- | :------- |
| TemplateId          | Request.Operation | 指定的模板 ID                                                | String    | 否       |
| Transcode           | Request.Operation | 指定转码模板参数                                             | Container | 否       |
| WatermarkTemplateId | Request.Operation | 指定的水印模板 ID，可以传多个水印模板 ID                     | String    | 否       |
| Watermark           | Request.Operation | 指定水印模板参数，同创建水印模板 [CreateMediaTemplate](https://intl.cloud.tencent.com/document/product/1045/49917) 接口中的 Request.Watermark | Container | 否       |
| RemoveWatermark     | Request.Operation | 指定去除水印参数, H265暂不支持次参数                         | Container | 否       |
| DigitalWatermark    | Request.Operation | 指定数字水印参数                                             | Container | 否       |
| Output              | Request.Operation | 结果输出地址                                                 | Container | 是       |
| UserData            | Request.Operation | 透传用户信息, 可打印的 ASCII 码, 长度不超过1024              | String    | 否       |
| JobLevel            | Request.Operation | 任务优先级，级别限制：0 、1 、2。级别越大任务优先级越高，默认为0 | String    | 否       |

>?
>
> 对于转码参数，优先使用优先使用 TemplateId，无 TemplateId 时使用 Transcode；对于水印参数，可以使用 WatermarkTemplateId 或 Watermark 设置，WatermarkTemplateId 优先级更高。

Container 类型 Transcode 的具体数据描述如下：

| 节点名称（关键字） | 父节点                      | 描述                                                         | 类型          | 必选 |
| :----------------- | :-------------------------- | :----------------------------------------------------------- | :------------ | :--- |
| TimeInterval       | Request.Operation.Transcode | 同创建转码模板 [CreateMediaTemplate](https://intl.cloud.tencent.com/document/product/1045/49911) 接口中的 Request.TimeInterval | Container     | 否   |
| Container          | Request.Operation.Transcode | 同创建转码模板 [CreateMediaTemplate](https://intl.cloud.tencent.com/document/product/1045/49911) 接口中的 Request.Container | Container     | 否   |
| Video              | Request.Operation.Transcode | 同创建转码模板 [CreateMediaTemplate](https://intl.cloud.tencent.com/document/product/1045/49911) 接口中的 Request.Video | Container     | 否   |
| Audio              | Request.Operation.Transcode | 同创建转码模板 [CreateMediaTemplate](https://intl.cloud.tencent.com/document/product/1045/49911) 接口中的 Request.Audio | Container     | 否   |
| TransConfig        | Request.Operation.Transcode | 同创建转码模板 [CreateMediaTemplate](https://intl.cloud.tencent.com/document/product/1045/49911) 接口中的 Request.TransConfig | Container     | 否   |
| AudioMix           | Request.Operation.Transcode | 混音参数，详情见[AudioMix](https://intl.cloud.tencent.com/document/product/1045/49945) | Container数组 | 否   |

Container 类型 RemoveWatermark 的具体数据描述如下：

| 节点名称（关键字） | 父节点                            | 描述                                   | 类型   | 必选 |
| :----------------- | :-------------------------------- | :------------------------------------- | :----- | :--- |
| Dx                 | Request.Operation.RemoveWatermark | 距离左上角原点 x 偏移，范围为[1, 4096] | string | 是   |
| Dy                 | Request.Operation.RemoveWatermark | 距离左上角原点 y 偏移，范围为[1, 4096] | string | 是   |
| Width              | Request.Operation.RemoveWatermark | 宽，范围为[1, 4096]                    | string | 是   |
| Height             | Request.Operation.RemoveWatermark | 高，范围为[1, 4096]                    | string | 是   |

Container 类型 DigitalWatermark 的具体数据描述如下：

| 节点名称（关键字） | 父节点                             | 描述                                                         | 类型   | 必选 |
| :----------------- | :--------------------------------- | :----------------------------------------------------------- | :----- | :--- |
| Message            | Request.Operation.DigitalWatermark | 数字水印嵌入的字符串信息，长度不超过64个字符，仅支持中文、英文、数字、_、-和* | string | 是   |
| Type               | Request.Operation.DigitalWatermark | 水印类型，当前仅可设置为 Text                                | String | 是   |
| Version            | Request.Operation.DigitalWatermark | 水印版本，当前仅可设置为 V1                                  | String | 是   |
| IgnoreError        | Request.Operation.DigitalWatermark | 当添加水印失败是否忽略错误继续执行任务，限制为 true/false，默认为false | string | 是   |

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

    [RequestId] => NjI2MTAzasdaHUISDHUINzE3YV8xZWVmNjU=
    [ContentType] => application/xml
    [ContentLength] => 1554
    [Bucket] => examplebucket-1250000000
    [Location] => examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/jobs
    [Response] => Array
        (
            [JobsDetail] => Array
                (
                    [Code] => Success
                    [CreationTime] => 2022-04-21T15:10:15+0800
                    [EndTime] => -
                    [Input] => Array
                        (
                            [BucketId] => examplebucket-1250000000
                            [Object] => video01.mp4
                            [Region] => ap-beijing
                        )

                    [JobId] => j1815a4c81h2kj31231gh31kj2f9e223404e
                    [Message] => Array
                        (
                        )

                    [Operation] => Array
                        (
                            [Output] => Array
                                (
                                    [Bucket] => examplebucket-1250000000
                                    [Object] => Transcode.flv
                                    [Region] => ap-beijing
                                )

                            [TemplateId] => t0b612860as90d8a09sd65dca38
                            [TemplateName] => FLV-SD
                            [UserData] => xxx
                            [JobLevel] => 0
                            [Watermark] => Array
                                (
                                    [0] => Array
                                        (
                                            [Dx] => 64
                                            [Dy] => 64
                                            [EndTime] => Array
                                                (
                                                )

                                            [LocMode] => Absolute
                                            [Pos] => TopRight
                                            [StartTime] => Array
                                                (
                                                )

                                            [Text] => Array
                                                (
                                                    [FontColor] => #99ff00
                                                    [FontSize] => 30
                                                    [FontType] => simfang.ttf
                                                    [Text] => 第一个水印
                                                    [Transparency] => 100
                                                )

                                            [Type] => Text
                                        )

                                    [1] => Array
                                        (
                                            [Dx] => 64
                                            [Dy] => 64
                                            [EndTime] => Array
                                                (
                                                )

                                            [LocMode] => Absolute
                                            [Pos] => TopLeft
                                            [StartTime] => Array
                                                (
                                                )

                                            [Text] => Array
                                                (
                                                    [FontColor] => #99ff00
                                                    [FontSize] => 30
                                                    [FontType] => simfang.ttf
                                                    [Text] => 第二个水印
                                                    [Transparency] => 100
                                                )

                                            [Type] => Text
                                        )

                                )

                        )

                    [Progress] => 0
                    [QueueId] => p81e648a7s9d88a09sd89a0757be086
                    [StartTime] => -
                    [State] => Submitted
                    [Tag] => Transcode
                )

        )

)
```

