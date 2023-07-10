## Overview
This document describes how to use the content moderation feature provided by [Cloud Infinite (CI)](https://www.tencentcloud.com/document/product/1045). CI fully integrates the processing capabilities with the COS SDK.

>?To use the content moderation service, you need to have the permission to use CI:
- For root accounts, click [here](https://console.cloud.tencent.com/cam/role/grant?roleName=CI_QCSRole&policyName=QcloudCOSDataFullControl,QcloudAccessForCIRole,QcloudPartAccessForCIRole&principal=eyJzZXJ2aWNlIjoiY2kucWNsb3VkLmNvbSJ9&serviceType=%E6%95%B0%E6%8D%AE%E4%B8%87%E8%B1%A1&s_url=https%3A%2F%2Fconsole.cloud.tencent.com%2Fci) for role authorization.
- For sub-accounts, see [Authorizing Sub-Accounts to Access CI Services](https://intl.cloud.tencent.com/document/product/1045/33450).

This document provides an overview of APIs and SDK code samples for text moderation.
>! COS PHP SDK v2.4.4 or later is required. Earlier versions may contain bugs and need to be upgraded to the [latest version](https://github.com/tencentyun/cos-php-sdk-v5/releases/) when used.
>

| API | Description |
| :----------------------------------------------------------- | :------------------------- |
|[Submitting text moderation job](https://intl.cloud.tencent.com/document/product/436/48188)  | Submits text moderation job.   |
|[Querying text moderation job result](https://intl.cloud.tencent.com/document/product/436/48189)  | Queries the result of specified text moderation job. |


## Submitting Text Moderation Job

#### Feature description

This API is used to submit a text moderation job.

#### Method prototype

```php
public Guzzle\Service\Resource\Model detectText(array $args = array());
```

#### Sample request

#### Sample 1: Moderating text content
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
    $content = 'Sensitive word';
    $result = $cosClient->detectText(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
        'Input' => array(
            'Content' => base64_encode($content) // The text needs to be Base64-encoded.
        ),
        'Conf' => array(
            'DetectType' => 'Porn,Ads,Illegal,Abuse', // `Porn,Ads,Illegal,Abuse` type
//            'BizType' => '', // Moderation policy
        ),
    ));
    // The request succeeded.
    print_r($result);
} catch (\Exception $e) {
    // The request failed.
    echo($e);
}
```

#### Sample 2: Moderating a text file in the specified bucket path
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
    $result = $cosClient->detectText(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
        'Input' => array(
            'Object' => 'test01.txt'// Object name. Be sure to check whether the object exists.
        ),
        'Conf' => array(
            'DetectType' => 'Porn,Ads,Illegal,Abuse',// `Porn,Ads,Illegal,Abuse` type
//            'Callback' => 'https://example.callback.com/test/', // Callback URL
//            'CallbackVersion' => 'Detail', // Structure of the callback content. Valid values: `Simple` (the callback content contains basic information), `Detail` (the callback content contains detailed information). Default value: `Simple`.
//            'BizType' => '', // Moderation policy
        ),
    ));
    // The request succeeded.
    print_r($result);
}  catch (\Exception $e) {
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
| Object | Request.Input | Name of the text file stored in the current COS bucket; for example, if the file is `test.txt` in the `test` directory, then the filename is `test/test.txt`. Only text files in UTF-8 and GBK encodings are supported, and the file size cannot exceed 1 MB. | String | No |
| Content | Request.Input | When the input content is plain text, it needs to be Base64-encoded first. The length of the original text before encoding cannot exceed 10,000 UTF-8 characters. If the length limit is exceeded, the API will report an error. | String | No |
| Url | Request.Input | Full URL of the text file, such as `https://www.test.com/test.txt`. | String | No |
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

>!
> - Only one of `Object`, `Content`, and `Url` can be used for a single request.
> - If `Object` or `Url` is selected, the moderation result will be returned asynchronously, which can be obtained through the API for [submitting text moderation job](https://intl.cloud.tencent.com/document/product/436/48188#3).
> - If `Content` is selected, the moderation result will be returned synchronously, which can be viewed in the [response body](https://intl.cloud.tencent.com/document/product/436/48188#1).
>- Currently, only Chinese, English, and Arabic numerals can be detected and moderated.
> 

`Conf` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :----------- | :----------------------------------------------------------- | :----- | :------- |
| BizType | Request.Conf | Unique identifier of the moderation policy. You can configure the scenes you want to moderate on the moderation policy page in the console, such as pornographic, adverting, and illegal information. For configuration guidelines, see [Setting Moderation Policy](https://intl.cloud.tencent.com/document/product/436/48188#4). You can get `BizType` in the console. If `BizType` is specified, the moderation request will perform moderation based on the scenes configured in the moderation policy. If `BizType` is not specified, the default moderation policy will be used automatically. | String | No |
| DetectType | Request.Conf | The scene to be moderated, such as `Porn` (pornography) and `Ads` (advertising). This parameter will no longer be maintained in the future. You can pass in multiple types and separate them by comma, such as `Porn,Ads`. If you need to moderate more scenes, use the `BizType` parameter. | String | No |
| Callback | Request.Conf | The moderation result can be sent to your callback address in the form of a callback. Addresses starting with `http://` or `https://` are supported, such as `http://www.callback.com`. If `Input` is `Content`, this parameter will not take effect, and the result will be returned directly. | String | No |
| CallbackVersion | Request.Conf | Structure of the callback content. Valid values: `Simple` (the callback content contains basic information), `Detail` (the callback content contains detailed information). Default value: `Simple`. | String | No |

#### Sample response

#### Sample 1: Moderating text content
```php
// If `Content` is selected, the moderation result will be returned synchronously, which can be viewed in the response body.
GuzzleHttp\Command\Result Object
(
    [RequestId] => NjEzYjUxMDhfZmNjYTNiMGFfNGM2NF8zNWY4Njg=
    [ContentType] => application/xml
    [ContentLength] => 878
    [JobsDetail] => Array
        (
            [Code] => Success
            [Message] => Array
                (
                )

            [JobId] => st8ffc0551123311eca33f525400f3e40d
            [State] => Success
            [CreationTime] => 2021-09-10T20:35:20+08:00
            [Content] => 5pWP5oSf6K+N
            [Result] => 0
            [SectionCount] => 1
            [PornInfo] => Array
                (
                    [HitFlag] => 0
                    [Count] => 0
                )

            [AdsInfo] => Array
                (
                    [HitFlag] => 0
                    [Count] => 0
                )

            [IllegalInfo] => Array
                (
                    [HitFlag] => 0
                    [Count] => 0
                )

            [AbuseInfo] => Array
                (
                    [HitFlag] => 0
                    [Count] => 0
                )

            [Section] => Array
                (
                    [0] => Array
                        (
                        )

                )

        )

    [Bucket] => examplebucket-1250000000
    [Location] => examplebucket-1250000000.ci.ap-guangzhou.myqcloud.com/text/auditing
)
```

#### Sample 2: Moderating a text file in the specified bucket path
```php
// If `Object` is selected, the moderation result will be returned asynchronously, which can be obtained through the API for querying text moderation job result.
GuzzleHttp\Command\Result Object
(
    [RequestId] => NjEzYjUxY2VfZmNjYTNiMGFfNGM0MF8zNTE0OWI=
    [ContentType] => application/xml
    [ContentLength] => 324
    [JobsDetail] => Array
        (
            [Object] => exampleobject
            [JobId] => st05c02c3c123411ec953452540024deb5
            [State] => Submitted
            [CreationTime] => 2021-09-10T20:38:38+08:00
        )

    [Bucket] => examplebucket-1250000000
    [Location] => examplebucket-1250000000.ci.ap-guangzhou.myqcloud.com/text/auditing
)
```

## Querying Text Moderation Job

#### Feature description

This API is used to query the status and result of a text moderation job.

#### Method prototype

```php
public Guzzle\Service\Resource\Model getDetectTextResult(array $args = array());
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
    $result = $cosClient->getDetectTextResult(array(
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
    [RequestId] => NjEzYjU0NDhfNzgwYzdkNjRfMThiOV8zNjQ0Y2Q=
    [ContentType] => application/xml
    [ContentLength] => 725
    [JobsDetail] => Array
        (
            [Code] => Success
            [Message] => 
            [JobId] => st7a813188123511ecb6485254009f6100
            [State] => Success
            [CreationTime] => 2021-09-10T20:49:03+08:00
            [Object] => exampleobject
            [SectionCount] => 1
            [Result] => 0
            [PornInfo] => Array
                (
                    [HitFlag] => 0
                    [Count] => 0
                )

            [AdsInfo] => Array
                (
                    [HitFlag] => 0
                    [Count] => 0
                )

            [Section] => Array
                (
                    [0] => Array
                        (
                        )

                )

        )

    [Key] => st7a813188123511ecb6485254009f6100
    [Bucket] => examplebucket-1250000000
    [Location] => examplebucket-1250000000.ci.ap-guangzhou.myqcloud.com/text/auditing/st7a813188123511ecb6485254009f6100
)
```



