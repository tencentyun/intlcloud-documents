## Overview
This document describes how to use the content moderation feature provided by [Cloud Infinite (CI)](https://www.tencentcloud.com/document/product/1045). CI fully integrates the processing capabilities with the COS SDK.

>?To use the content moderation service, you need to have the permission to use CI:
- For root accounts, click [here](https://console.cloud.tencent.com/cam/role/grant?roleName=CI_QCSRole&policyName=QcloudCOSDataFullControl,QcloudAccessForCIRole,QcloudPartAccessForCIRole&principal=eyJzZXJ2aWNlIjoiY2kucWNsb3VkLmNvbSJ9&serviceType=%E6%95%B0%E6%8D%AE%E4%B8%87%E8%B1%A1&s_url=https%3A%2F%2Fconsole.cloud.tencent.com%2Fci) for role authorization.
- For sub-accounts, see [Authorizing Sub-Accounts to Access CI Services](https://intl.cloud.tencent.com/document/product/1045/33450).

This document provides an overview of APIs and SDK code samples for video moderation.
>! COS PHP SDK v2.4.4 or later is required. Earlier versions may contain bugs and need to be upgraded to the [latest version](https://github.com/tencentyun/cos-php-sdk-v5/releases/) when used.
>

| API | Description |
| :----------------------------------------------------------- | :------------------------- |
|[Submitting video moderation job](https://intl.cloud.tencent.com/document/product/436/48249) | Submits video moderation job.   |
|[Querying video moderation job result](https://intl.cloud.tencent.com/document/product/436/48250)  | Queries the result of specified video moderation job. |


## Submitting Video Moderation Job

#### Feature description

This API is used to submit a video moderation job.

#### Method prototype

```php
public Guzzle\Service\Resource\Model detectVideo(array $args = array());
```

#### Sample request

```php
<?php

require dirname(__FILE__) . '/../vendor/autoload.php';

$secretId = "SECRETID"; // Replace it with your actual `secretId`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi.
$secretKey = "SECRETKEY"; // Replace it with your actual `secretKey`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi.
$region = "ap-beijing"; // Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket.
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', // `https` must be used during moderation.
        'credentials'=> array(
            'secretId'  => $secretId ,
            'secretKey' => $secretKey)));

try {
    $result = $cosClient->detectVideo(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
        'Input' => array(
            'Object' => 'movie.mp4',
        ),
        'Conf' => array(
            'DetectType' => 'Porn,Ads',// Valid values: `Porn`, `Ads`. Multiple rules can be used. Be sure not to add spaces between them.
//            'Callback' => 'https://example.com/callback', // Callback address
//            'BizType' => '', // Moderation policy
//            'DetectContent' => 1, // Whether to moderate the video sound. Default value: `0`.
//            'CallbackVersion' => 'Detail', // Callback content structure. Valid values: `Simple`, `Detail`. Default value: `Simple`.
            'Snapshot' => array(
//                'Mode' => 'Average', // Frame capturing mode. Valid values: `Interval`, `Average`, `Fps`.
//                'TimeInterval' => 50, // Number of captured frames
                'Count' => '3', // Video frame capturing frequency
            ),// Screenshot
        ),
    ));
    // The request succeeded.
    print_r($result);
} catch (\Exception $e) {
    // The request failed.
    echo($e);
}
```


#### Parameter description

`Request` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :------ | :--------------- | :-------- | :------- |
| Input | Request | Video to be moderated. | Container | Yes |
| Conf | Request | Moderation rule configuration. | Container | Yes |

`Input` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :------------ | :----------------------------------------------------------- | :-------- | :------- |
| Object | Request.Input | Name of the video file stored in the COS bucket; for example, if the file is `video.mp4` in the `test` directory, then the filename is `test/video.mp4`. | String | No |
| Url | Request.Input | Full URL of the video file, such as `http://examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/test.mp4`. Either `Object` or `Url` can be selected at a time. | String | No |
| DataId | Request.Input | This field will return the original content in the moderation result, which can contain up to 512 bytes. You can use this field to uniquely identify the data to be moderated in your business. | String | No |
| UserInfo | Request.Input | Business field. | Container | No |

`UserInfo` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :--------------------- | :------------------------------------- | :----- | :------- |
| TokenId           | Request.Input.UserInfo | Business `TokenId`, which can contain up to 128 bytes.                      | String | No       |
| Nickname          | Request.Input.UserInfo | Business `Nickname`, which can contain up to 128 bytes.                     | String | No       |
| DeviceId          | Request.Input.UserInfo | Business `DeviceId`, which can contain up to 128 bytes.                     | String | No       |
| AppId             | Request.Input.UserInfo | Business `AppId`, which can contain up to 128 bytes.                         | String | No       |
| Room              | Request.Input.UserInfo | Business `Room`, which can contain up to 128 bytes.                          | String | No       |
| IP                | Request.Input.UserInfo | Business `IP`, which can contain up to 128 bytes.                            | String | No       |
| Type              | Request.Input.UserInfo | Business `Type`, which can contain up to 128 bytes.                          | String | No       |

`Conf` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :----------- | :----------------------------------------------------------- | :-------- | :------- |
| BizType | Request.Conf | Unique identifier of the moderation policy. You can configure the scenes you want to moderate on the moderation policy page in the console, such as pornographic, adverting, and illegal information. For configuration guidelines, see [Setting Moderation Policy](https://intl.cloud.tencent.com/document/product/436/48249#1). You can get `BizType` in the console. If `BizType` is specified, the moderation request will perform moderation based on the scenes configured in the moderation policy. If `BizType` is not specified, the default moderation policy will be used automatically. | String | No |
| DetectType | Request.Conf | The scene to be moderated, such as `Porn` (pornography) and `Ads` (advertising). This parameter will no longer be maintained in the future. You can pass in multiple types and separate them by comma, such as `Porn,Ads`. If you need to moderate more scenes, use the `BizType` parameter. | String | No |
| Snapshot           | Request.Conf | Video image moderation is implemented by taking a certain number of screenshots based on the video frame capturing capability and then moderating the screenshots one by one. This parameter is used to specify the configuration of video frame capturing. | Container | Yes |
| Callback           | Request.Conf | Callback address, which must start with `http://` or `https://`.              | String    | No       |
| CallbackVersion | Request.Conf | Structure of the callback content. Valid values: `Simple` (the callback content contains basic information), `Detail` (the callback content contains detailed information). Default value: `Simple`. | String | No |
| DetectContent | Request.Conf | Whether to moderate video sound. Valid values: `0` (moderates the video image only), `1` (moderates both the video image and video sound). Default value: `0`. | Integer | No |

`Snapshot` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :-------------------- | :----------------------------------------------------------- | :------ | :------- |
| Mode               | Request.Conf.Snapshot | Frame capturing mode. Valid values: `Interval` (interval mode), `Average` (average mode), `Fps` (fixed frame rate mode). Default value: `Interval`. `Interval` mode: The `TimeInterval` and `Count` parameters take effect. If `Count` is set but `TimeInterval` is not, all frames will be captured to generate a total of `Count` images. `Average` mode: The `Count` parameter takes effect, indicating to capture a total of `Count` images at an average interval in the entire video. `Fps` mode: `TimeInterval` indicates how many frames to capture per second. If `TimeInterval` is not set, all frames will be captured to generate a total of `Count` images. | String | No |
| Count              | Request.Conf.Snapshot | The number of captured frames. Value range: (0, 10000]. | Integer | Yes |
| TimeInterval       | Request.Conf.Snapshot | Video frame capturing frequency. Value range: (0.000, 60.000] seconds. The value supports the float format, accurate to the millisecond. | Float  | No |

#### Sample response

```php
GuzzleHttp\Command\Result Object
(
    [RequestId] => NjEzYTA4YTlfZmNjYTNiMGFfNGM2MV8zMTM1ODQ=
    [ContentType] => application/xml
    [ContentLength] => 322
    [JobsDetail] => Array
        (
            [Object] => movie.mp4
            [JobId] => avd61e00d8116f11ec953452540024deb5
            [State] => Submitted
            [CreationTime] => 2021-09-09T21:14:17+08:00
        )

    [Bucket] => examplebucket-1250000000
    [Location] => examplebucket-1250000000.ci.ap-guangzhou.myqcloud.com/video/auditing
)
```


## Querying Video Moderation Job

#### Feature description

This API is used to query the status and result of a video moderation job.

#### Method prototype

```php
public Guzzle\Service\Resource\Model getDetectVideoResult(array $args = array());
```

#### Sample request

```php
<?php

require dirname(__FILE__) . '/../vendor/autoload.php';

$secretId = "SECRETID"; // Replace it with your actual `secretId`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi.
$secretKey = "SECRETKEY"; // Replace it with your actual `secretKey`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi.
$region = "ap-beijing"; // Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket.
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', // `https` must be used during moderation.
        'credentials'=> array(
            'secretId'  => $secretId ,
            'secretKey' => $secretKey)));
            
try {
    $result = $cosClient->getDetectVideoResult(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
        'Key' => 'examplejobid', // JobId
    ));
    // The request succeeded.
    print_r($result);
} catch (\Exception $e) {
    // The request failed.
    echo($e);
}
```

#### Parameter description

| Parameter | Type | Description | Required |
| ---------- | ------------------------------------------------------------ | ------ |-----|
| Bucket | String | Bucket name in the format of `BucketName-APPID` | Yes |
| Key | String | ID of the job to be queried | Yes |

#### Sample response

```php
GuzzleHttp\Command\Result Object
(
    [RequestId] => NjEzYTBjMGVfZmNjYTNiMGFfNGM2Ml8zMTdjYjM=
    [ContentType] => application/xml
    [ContentLength] => 4941
    [Key] => avd61e00d8116f11ec953452540024deb5
    [Bucket] => examplebucket-1250000000
    [Location] => examplebucket-1250000000.ci.ap-guangzhou.myqcloud.com/video/auditing/avd61e00d8116f11ec953452540024deb5
    [Response] => Array
        (
            [JobsDetail] => Array
                (
                    [AdsInfo] => Array
                        (
                            [Count] => 0
                            [HitFlag] => 0
                        )

                    [AudioSection] => Array
                        (
                            [0] => Array
                                (
                                    [AdsInfo] => Array
                                        (
                                            [HitFlag] => 0
                                            [Score] => 0
                                        )

                                    [Duration] => 30000
                                    [OffsetTime] => 0
                                    [PornInfo] => Array
                                        (
                                            [HitFlag] => 0
                                            [Score] => 0
                                        )

                                    [Text] => Array
                                        (
                                        )

                                    [Url] => https://audio-auditing-appid.cos.ap-guangzhou.myqcloud.com/_cms_segments%2Fcms%2Faudio%2Fw-audio-YToIq75SmCBmUefo%2F0.mp3?q-sign-algorithm=sha1&q-ak=AKIDJLGwMW6NTJ9mNj8DigYDiXOLtVpsbzGJ&q-sign-time=1631194126%3B1631201326&q-key-time=1631194126%3B1631201326&q-header-list=host&q-url-param-list=&q-signature=65af69dedc0cea3702059c7b124914311d73b1e7
                                )

                            [1] => Array
                                (
                                    [AdsInfo] => Array
                                        (
                                            [HitFlag] => 0
                                            [Score] => 0
                                        )

                                    [Duration] => 30000
                                    [OffsetTime] => 30000
                                    [PornInfo] => Array
                                        (
                                            [HitFlag] => 0
                                            [Score] => 0
                                        )

                                    [Text] => Array
                                        (
                                        )

                                    [Url] => https://audio-auditing-appid.cos.ap-guangzhou.myqcloud.com/_cms_segments%2Fcms%2Faudio%2Fw-audio-YToIq75SmCBmUefo%2F30.mp3?q-sign-algorithm=sha1&q-ak=AKIDJLGwMW6NTJ9mNj8DigYDiXOLtVpsbzGJ&q-sign-time=1631194126%3B1631201326&q-key-time=1631194126%3B1631201326&q-header-list=host&q-url-param-list=&q-signature=ce3e8856e97b155a661108b0ae970f8fcfddf143
                                )

                            [2] => Array
                                (
                                    [AdsInfo] => Array
                                        (
                                            [HitFlag] => 0
                                            [Score] => 0
                                        )

                                    [Duration] => 2000
                                    [OffsetTime] => 60000
                                    [PornInfo] => Array
                                        (
                                            [HitFlag] => 0
                                            [Score] => 0
                                        )

                                    [Text] => Array
                                        (
                                        )

                                    [Url] => https://audio-auditing-appid.cos.ap-guangzhou.myqcloud.com/_cms_segments%2Fcms%2Faudio%2Fw-audio-YToIq75SmCBmUefo%2F60.mp3?q-sign-algorithm=sha1&q-ak=AKIDJLGwMW6NTJ9mNj8DigYDiXOLtVpsbzGJ&q-sign-time=1631194126%3B1631201326&q-key-time=1631194126%3B1631201326&q-header-list=host&q-url-param-list=&q-signature=019cf7a9250473e57e45e5d8eb3e569d4d2ecfe2
                                )

                        )

                    [CreationTime] => 2021-09-09T21:14:17+08:00
                    [JobId] => avd61e00d8116f11ec953452540024deb5
                    [Object] => movie.mp4
                    [PornInfo] => Array
                        (
                            [Count] => 0
                            [HitFlag] => 0
                        )

                    [Result] => 0
                    [Snapshot] => Array
                        (
                            [0] => Array
                                (
                                    [AdsInfo] => Array
                                        (
                                            [HitFlag] => 0
                                            [Label] => Array
                                                (
                                                )

                                            [Score] => 0
                                            [SubLabel] => Array
                                                (
                                                )

                                        )

                                    [PornInfo] => Array
                                        (
                                            [HitFlag] => 0
                                            [Label] => Array
                                                (
                                                )

                                            [Score] => 0
                                            [SubLabel] => Array
                                                (
                                                )

                                        )

                                    [SnapshotTime] => 0
                                    [Text] => Array
                                        (
                                        )

                                    [Url] => https://auditing-appid.cos.ap-chongqing.myqcloud.com/%2F872400-1251668577%2Fmovie.mp4%2Fjd634e582116f11eca3594388b5008703%2F0%2F0.jpg?q-sign-algorithm=sha1&q-ak=AKIDziAUWHqzwb2DsGIJzOD1hHajzyhyglHW&q-sign-time=1631194126%3B1631201326&q-key-time=1631194126%3B1631201326&q-header-list=host&q-url-param-list=&q-signature=d440335fccc8a6db8c278982b8b3fdda9719f970
                                )

                            [1] => Array
                                (
                                    [AdsInfo] => Array
                                        (
                                            [HitFlag] => 0
                                            [Label] => Array
                                                (
                                                )

                                            [Score] => 0
                                            [SubLabel] => Array
                                                (
                                                )

                                        )

                                    [PornInfo] => Array
                                        (
                                            [HitFlag] => 0
                                            [Label] => Array
                                                (
                                                )

                                            [Score] => 0
                                            [SubLabel] => Array
                                                (
                                                )

                                        )

                                    [SnapshotTime] => 50000
                                    [Text] => Array
                                        (
                                        )

                                    [Url] => https://auditing-appid.cos.ap-chongqing.myqcloud.com/%2F872400-1251668577%2Fmovie.mp4%2Fjd634e582116f11eca3594388b5008703%2F50000%2F1.jpg?q-sign-algorithm=sha1&q-ak=AKIDziAUWHqzwb2DsGIJzOD1hHajzyhyglHW&q-sign-time=1631194126%3B1631201326&q-key-time=1631194126%3B1631201326&q-header-list=host&q-url-param-list=&q-signature=f93ae84af5bf5f6730ffeae9edb3332285b8169d
                                )

                        )

                    [SnapshotCount] => 2
                    [State] => Success

                )

            [RequestId] => NjEzYTBjMGVfZmNjYTNiMGFfNGM2Ml8zMTdjYjM=
        )

)
```
