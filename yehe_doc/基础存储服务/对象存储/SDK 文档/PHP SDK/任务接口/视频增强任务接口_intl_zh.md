## 简介

本文档提供关于提交视频增强任务的 API 概览和 SDK 示例代码。

| API           | 操作描述                 |
| ------------- |  ---------------------- |
| [提交视频增强任务](https://intl.cloud.tencent.com/document/product/436/49061) | 提交一个视频增强任务 |


## 提交视频增强任务

#### 功能说明

用于提交一个视频增强任务。

#### 方法原型

```php
public Guzzle\Service\Resource\Model createMediaVideoProcessJobs(array $args = array());
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
    $result = $cosClient->createMediaVideoProcessJobs(array(
        'Bucket' => 'examplebucket-1250000000', //存储桶名称，由 BucketName-Appid 组成，可以在 COS 控制台查看 https://console.cloud.tencent.com/cos5/bucket
        'Tag' => 'VideoProcess',
        'QueueId' => 'p81e648afxxxxxxxxxxxxxxxxx',
        'Input' => array(
            'Object' => 'video01.mp4'
        ),
        'Operation' => array(
            'TemplateId' => 't13466f1ea41a14c0xxxxxxxxxxxxx', // 视频增强模板 ID
            'TranscodeTemplateId' => 't0b6a845f5e42847bd81xxxxxxxxxxxxx', // 转码模板 ID
            'WatermarkTemplateId' => 't185e2e24551b24259a0xxxxxxxxxxxxx', // 水印模板 ID
            'Output' => array(
                'Region' => $region,
                'Bucket' => 'examplebucket-1250000000', //存储桶名称，由 BucketName-Appid 组成，可以在 COS 控制台查看 https://console.cloud.tencent.com/cos5/bucket
                'Object' => 'VideoProcess.flv',
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
    $result = $cosClient->createMediaVideoProcessJobs(array(
        'Bucket' => 'examplebucket-1250000000', //存储桶名称，由 BucketName-Appid 组成，可以在 COS 控制台查看 https://console.cloud.tencent.com/cos5/bucket
        'Tag' => 'VideoProcess',
        'QueueId' => 'p81e648afxxxxxxxxxxxxxxxxx',
        'Input' => array(
            'Object' => 'video01.mp4'
        ),
        'Operation' => array(
            'VideoProcess' => array(
                'ColorEnhance' => array(
                    'Enable' => '',
                    'Contrast' => '',
                    'Correction' => '',
                    'Saturation' => '',
                ),
                'MsSharpen' => array(
                    'Enable' => '',
                    'SharpenLevel' => '',
                ),
            ),
            'Transcode' => array(
                'Tag' => '',
                'Name' => '',
                'Container' => array(
                    'Format' => '',
                ),
                'Video' => array(
                    'Codec' => '',
                    'Width' => '',
                    'Height' => '',
                    'Fps' => '',
                    'Remove' => '',
                    'Profile' => '',
                    'Bitrate' => '',
                    'Crf' => '',
                    'Gop' => '',
                    'Preset' => '',
                    'Bufsize' => '',
                    'Maxrate' => '',
                    'HlsTsTime' => '',
                    'Pixfmt' => '',
                    'LongShortMode' => '',
                ),
                'TimeInterval' => array(
                    'Start' => '',
                    'Duration' => '',
                ),
                'Audio' => array(
                    'Codec' => '',
                    'Samplerate' => '',
                    'Bitrate' => '',
                    'Channels' => '',
                    'Remove' => '',
                    'KeepTwoTracks' => '',
                    'SwitchTrack' => '',
                    'SampleFormat' => '',
                ),
                'TransConfig' => array(
                    'AdjDarMethod' => '',
                    'IsCheckReso' => '',
                    'ResoAdjMethod' => '',
                    'IsCheckVideoBitrate' => '',
                    'VideoBitrateAdjMethod' => '',
                    'IsCheckAudioBitrate' => '',
                    'AudioBitrateAdjMethod' => '',
                    'DeleteMetadata' => '',
                    'IsHdr2Sdr' => '',
                    'HlsEncrypt' => array(
                        'IsHlsEncrypt' => '',
                        'UriKey' => '',
                    ),
                ),
            ),
            'Watermark' => array(
                'Type' => '',
                'Pos' => '',
                'LocMode' => '',
                'Dx' => '',
                'Dy' => '',
                'StartTime' => '',
                'EndTime' => '',
                'Image' => array(
                    'Url' => '',
                    'Mode' => '',
                    'Width' => '',
                    'Height' => '',
                    'Transparency' => '',
                    'Background' => '',
                ),
                'Text' => array(
                    'FontSize' => '',
                    'FontType' => '',
                    'FontColor' => '',
                    'Transparency' => '',
                    'Text' => '',
                ),
            ),
            'Output' => array(
                'Region' => $region,
                'Bucket' => 'examplebucket-1250000000', //存储桶名称，由 BucketName-Appid 组成，可以在 COS 控制台查看 https://console.cloud.tencent.com/cos5/bucket
                'Object' => 'VideoProcess.flv',
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
| Tag                | Request | 创建任务的 Tag：VideoProcess                                 | String    | 是       |
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

| 节点名称（关键字）  | 父节点            | 描述                                                         | 类型           | 是否必选 |
| :------------------ | :---------------- | :----------------------------------------------------------- | :------------- | :------- |
| VideoProcess        | Request.Operation | 指定视频增强模板参数，不能与 TemplateId 同时为空             | Container      | 否       |
| TemplateId          | Request.Operation | 指定的模板 ID ，不能与 VideoProcess 同时为空                 | String         | 否       |
| Transcode           | Request.Operation | 指定转码模板参数，不能与 TranscodeTemplateId 同时为空        | Container      | 否       |
| TranscodeTemplateId | Request.Operation | 指定的转码模板 ID，优先使用模板 ID，不能与 Transcode 同时为空 | String 数组    | 否       |
| Watermark           | Request.Operation | 指定水印模板参数，同创建水印模板 [CreateMediaTemplate](https://intl.cloud.tencent.com/document/product/1045/49917) 接口的 Request.Watermark, 最多传3个 | Container 数组 | 否       |
| WatermarkTemplateId | Request.Operation | 指定的水印模板 ID，可以传多个水印模板 ID，最多传3个，优先使用模板 ID | String         | 否       |
| DigitalWatermark    | Request.Operation | 指定数字水印参数                                             | Container      | 否       |
| Output              | Request.Operation | 结果输出地址                                                 | Container      | 是       |
| JobLevel            | Request.Operation | 任务优先级，级别限制：0 、1 、2。级别越大任务优先级越高，默认为0 | String         | 否       |

>?
>
> 提交视频增强任务必须传入转码参数。对于视频增强参数，优先使用 TemplateId，无 TemplateId 时使用 VideoProcess；对于转码参数，优先使用 TranscodeTemplateId，无 TranscodeTemplateId 时使用 Transcode；对于水印参数，可以使用 WatermarkTemplateId 或 Watermark 设置，WatermarkTemplateId 优先级更高。

Container 类型 VideoProcess 的具体数据描述如下：

| 节点名称（关键字） | 父节点                         | 描述                                                         |
| :----------------- | :----------------------------- | :----------------------------------------------------------- |
| ColorEnhance       | Request.Operation.VideoProcess | 同创建视频增强模板 [CreateMediaTemplate](https://intl.cloud.tencent.com/document/product/1045/49915) 接口中的 Request.ColorEnhance |
| MsSharpen          | Request.Operation.VideoProcess | 同创建视频增强模板 [CreateMediaTemplate](https://intl.cloud.tencent.com/document/product/1045/49915) 接口中的 Request.MsSharpen |

Container 类型 Transcode 的具体数据描述如下：

| 节点名称（关键字） | 父节点                      | 描述                                                         | 类型           | 必选 |
| :----------------- | :-------------------------- | :----------------------------------------------------------- | :------------- | :--- |
| TimeInterval       | Request.Operation.Transcode | 同创建转码模板 [CreateMediaTemplate](https://intl.cloud.tencent.com/document/product/1045/49911) 接口中的 Request.TimeInterval | Container      | 否   |
| Container          | Request.Operation.Transcode | 同创建转码模板 [CreateMediaTemplate](https://intl.cloud.tencent.com/document/product/1045/49911) 接口中的 Request.Container | Container      | 否   |
| Video              | Request.Operation.Transcode | 同创建转码模板 [CreateMediaTemplate](https://intl.cloud.tencent.com/document/product/1045/49911) 接口中的 Request.Video | Container      | 否   |
| Audio              | Request.Operation.Transcode | 同创建转码模板 [CreateMediaTemplate](https://intl.cloud.tencent.com/document/product/1045/49911) 接口中的 Request.Audio | Container      | 否   |
| TransConfig        | Request.Operation.Transcode | 同创建转码模板 [CreateMediaTemplate](https://intl.cloud.tencent.com/document/product/1045/49911) 接口中的 Request.TransConfig | Container      | 否   |
| AudioMix           | Request.Operation.Transcode | 混音参数，详情见 [AudioMix](https://intl.cloud.tencent.com/document/product/1045/49945) | Container 数组 | 否   |

Container 类型 DigitalWatermark 的具体数据描述如下：

| 节点名称（关键字） | 父节点                             | 描述                                                         | 类型   | 必选 |
| :----------------- | :--------------------------------- | :----------------------------------------------------------- | :----- | :--- |
| Message            | Request.Operation.DigitalWatermark | 数字水印嵌入的字符串信息，长度不超过64个字符，仅支持中文、英文、数字、_、-和* | string | 是   |
| Type               | Request.Operation.DigitalWatermark | 水印类型，当前仅可设置为 Text                                | String | 是   |
| Version            | Request.Operation.DigitalWatermark | 水印版本，当前仅可设置为 V1                                  | String | 是   |
| IgnoreError        | Request.Operation.DigitalWatermark | 当添加水印失败是否忽略错误继续执行任务，限制为 true/false，默认为 false | string | 是   |

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

    [RequestId] => NjI2MjNjYHAOIHDOIADJHOIA18yMjFlMWE=
    [ContentType] => application/xml
    [ContentLength] => 965
    [Bucket] => examplebucket-1250000000
    [Location] => examplebucket-1250000000.ci.ap-beijing.myqcloud.com/jobs
    [Response] => Array
        (
            [JobsDetail] => Array
                (
                    [Code] => Success
                    [CreationTime] => 2022-04-22T11:19:15+0800
                    [EndTime] => -
                    [Input] => Array
                        (
                            [BucketId] => examplebucket-1250000000
                            [Object] => video01.mp4
                            [Region] => ap-beijing
                        )

                    [JobId] => jfd27519z8zx90c8z90c7809z9f35eb
                    [Message] => 
                    [Operation] => Array
                        (
                            [Output] => Array
                                (
                                    [Bucket] => examplebucket-1250000000
                                    [Object] => VideoProcess.flv
                                    [Region] => ap-beijing
                                )

                            [TemplateId] => t13466f1eazx08c09zx8c09zx8e9cd
                            [TemplateName] => video-process-1
                            [TranscodeTemplateId] => t0b612860z087xc09zx8c09xz8c095dca38
                            [WatermarkTemplateId] => t185e2e24zxc780z8c0z98c323c6428a19c
                            [UserData] => xxx
                            [JobLevel] => 0
                        )

                    [QueueId] => p81e648af2aee496885zx098c09z8xc09zxc086
                    [StartTime] => -
                    [State] => Submitted
                    [Tag] => VideoProcess
                )

        )

)
```

