## Overview
This document describes how to use the content moderation feature provided by [Cloud Infinite (CI)](https://www.tencentcloud.com/document/product/1045). CI fully integrates the processing capabilities with the COS SDK.

>?To use the content moderation service, you need to have the permission to use CI:
- For root accounts, click [here](https://console.cloud.tencent.com/cam/role/grant?roleName=CI_QCSRole&policyName=QcloudCOSDataFullControl,QcloudAccessForCIRole,QcloudPartAccessForCIRole&principal=eyJzZXJ2aWNlIjoiY2kucWNsb3VkLmNvbSJ9&serviceType=%E6%95%B0%E6%8D%AE%E4%B8%87%E8%B1%A1&s_url=https%3A%2F%2Fconsole.cloud.tencent.com%2Fci) for role authorization.
- For sub-accounts, see [Authorizing Sub-Accounts to Access CI Services](https://intl.cloud.tencent.com/document/product/1045/33450).

This document provides an overview of APIs and SDK code samples for audio moderation.
>! COS PHP SDK v2.4.4 or later is required. Earlier versions may contain bugs and need to be upgraded to the [latest version](https://github.com/tencentyun/cos-php-sdk-v5/releases/) when used.
>

| API | Description |
| :----------------------------------------------------------- | :------------------------- |
|[Submitting audio moderation job](https://intl.cloud.tencent.com/document/product/436/48262) | Submits audio moderation job.   |
|[Querying audio moderation job result](https://intl.cloud.tencent.com/document/product/436/48263)  | Queries the result of specified audio moderation job. |

## Submitting Audio Moderation Job

#### Feature description

This API is used to submit an audio moderation job.

#### Method prototype

```php
public Guzzle\Service\Resource\Model detectAudio(array $args = array());
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
    $result = $cosClient->detectAudio(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
        'Input' => array(
            'Object' => 'sound01.mp3',
        ),
        'Conf' => array(
            'DetectType' => 'Porn,Ads',// Valid values: `Porn`, `Ads`, `Illegal`, `Abuse`. Multiple rules can be used. Be sure not to add spaces between them.
//            'CallbackVersion' => 'Detail', // Structure of the callback content. Valid values: `Simple` (the callback content contains basic information), `Detail` (the callback content contains detailed information). Default value: `Simple`.
//            'Callback' => 'https://example.com/callback',// Callback address
//            'BizType' => '',// Moderation policy
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
| Input | Request | Content to be moderated. | Container | Yes |
| Conf | Request | Moderation rule configuration. | Container | Yes |

`Input` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :------------ | :----------------------------------------------------------- | :-------- | :------- |
| Object | Request.Input | Name of the audio file stored in the COS bucket; for example, if the file is `audio.mp3` in the `test` directory, then the filename is `test/audio.mp3`. Either `Object` or `Url` can be selected at a time. | String | No |
| Url | Request.Input | Full URL of the audio file, such as `http://examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/audio.mp3`. Either `Object` or `Url` can be selected at a time. | String | No |
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
| :----------------- | :----------- | :----------------------------------------------------------- | :----- | :------- |
| BizType | Request.Conf | Unique identifier of the moderation policy. You can configure the scenes you want to moderate on the moderation policy page in the console, such as pornographic, adverting, and illegal information. For configuration guidelines, see [Setting Moderation Policy](https://intl.cloud.tencent.com/document/product/436/48262#1). You can get `BizType` in the console. If `BizType` is specified, the moderation request will perform moderation based on the scenes configured in the moderation policy. If `BizType` is not specified, the default moderation policy will be used automatically. | String | No |
| DetectType | Request.Conf | The scene to be moderated, such as `Porn` (pornography) and `Ads` (advertising). This parameter will no longer be maintained in the future. You can pass in multiple types and separate them by comma, such as `Porn,Ads`. If you need to moderate more scenes, use the `BizType` parameter. | String | No |
| Callback | Request.Conf | The moderation result can be sent to your callback address in the form of a callback. Addresses starting with `http://` or `https://` are supported, such as `http://www.callback.com`.  | String | No |
| CallbackVersion | Request.Conf | Structure of the callback content. Valid values: `Simple` (the callback content contains basic information), `Detail` (the callback content contains detailed information). Default value: `Simple`. | string | No |

#### Sample response

```php
GuzzleHttp\Command\Result Object
(
    [RequestId] => NjEzYTExN2RfNzgwYzdkNjRfMThiOV8zMjY2Zjc=
    [ContentType] => application/xml
    [ContentLength] => 324
    [JobsDetail] => Array
        (
            [Object] => sound01.mp3
            [JobId] => sa19232ce6117511ecb6485254009f6100
            [State] => Submitted
            [CreationTime] => 2021-09-09T21:51:57+08:00
        )

    [Bucket] => examplebucket-1250000000
    [Location] => examplebucket-1250000000.ci.ap-guangzhou.myqcloud.com/audio/auditing
)
```


## Querying Audio Moderation Job

#### Feature description

This API is used to query the status and result of an audio moderation job.

#### Method prototype

```php
public Guzzle\Service\Resource\Model getDetectAudioResult(array $args = array());
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
    $result = $cosClient->getDetectAudioResult(array(
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
    [RequestId] => NjEzYjRjMWRfNzgwYzdkNjRfMThiOV8zNjI5OWI=
    [ContentType] => application/xml
    [ContentLength] => 2328
    [Key] => sa19232ce6117511ecb6485254009f6100
    [Bucket] => examplebucket-1250000000
    [Location] => examplebucket-1250000000.ci.ap-guangzhou.myqcloud.com/audio/auditing/sa19232ce6117511ecb6485254009f6100
    [Response] => Array
        (
            [JobsDetail] => Array
                (
                    [AdsInfo] => Array
                        (
                            [HitFlag] => 0
                            [Label] => Array
                                (
                                )

                            [Score] => 0
                        )

                    [AudioText] => Array
                        (
                            [0] =>   
                        )

                    [CreationTime] => 2021-09-09T21:51:57+08:00
                    [JobId] => sa19232ce6117511ecb6485254009f6100
                    [Object] => sound01.mp3
                    [PornInfo] => Array
                        (
                            [HitFlag] => 0
                            [Label] => Array
                                (
                                )

                            [Score] => 0
                        )

                    [Result] => 0
                    [Section] => Array
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

                                    [Url] => https://audio-auditing-appid.cos.ap-guangzhou.myqcloud.com/_cms_segments%2Fcms%2Faudio%2Fw-audio-YToRfUy_b0-zRwQH%2F0.mp3?q-sign-algorithm=sha1&q-ak=AKIDJLGwMW6NTJ9mNj8DigYDiXOLtVpsbzGJ&q-sign-time=1631276061%3B1631283261&q-key-time=1631276061%3B1631283261&q-header-list=host&q-url-param-list=&q-signature=5b33e65e53f14ea7ba5559e63a40c920b500f109
                                )

                            [1] => Array
                                (
                                    [AdsInfo] => Array
                                        (
                                            [HitFlag] => 0
                                            [Score] => 0
                                        )

                                    [Duration] => 15000
                                    [OffsetTime] => 30000
                                    [PornInfo] => Array
                                        (
                                            [HitFlag] => 0
                                            [Score] => 0
                                        )

                                    [Text] => Array
                                        (
                                        )

                                    [Url] => https://audio-auditing-appid.cos.ap-guangzhou.myqcloud.com/_cms_segments%2Fcms%2Faudio%2Fw-audio-YToRfUy_b0-zRwQH%2F30.mp3?q-sign-algorithm=sha1&q-ak=AKIDJLGwMW6NTJ9mNj8DigYDiXOLtVpsbzGJ&q-sign-time=1631276061%3B1631283261&q-key-time=1631276061%3B1631283261&q-header-list=host&q-url-param-list=&q-signature=f8e6fe3b430eeac93fd5bf5950a09f9c4a570e26
                                )

                        )

                    [State] => Success
                )

            [RequestId] => NjEzYjRjMWRfNzgwYzdkNjRfMThiOV8zNjI5OWI=
        )

)
```

