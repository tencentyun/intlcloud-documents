## Overview
This document describes how to use the content moderation feature provided by [Cloud Infinite (CI)](https://www.tencentcloud.com/document/product/1045). CI fully integrates the processing capabilities with the COS SDK.

>?To use the content moderation service, you need to have the permission to use CI:
- For root accounts, click [here](https://console.cloud.tencent.com/cam/role/grant?roleName=CI_QCSRole&policyName=QcloudCOSDataFullControl,QcloudAccessForCIRole,QcloudPartAccessForCIRole&principal=eyJzZXJ2aWNlIjoiY2kucWNsb3VkLmNvbSJ9&serviceType=%E6%95%B0%E6%8D%AE%E4%B8%87%E8%B1%A1&s_url=https%3A%2F%2Fconsole.cloud.tencent.com%2Fci) for role authorization.
- For sub-accounts, see [Authorizing Sub-Accounts to Access CI Services](https://intl.cloud.tencent.com/document/product/1045/33450).

This document provides an overview of APIs and SDK code samples for file moderation.
>! COS PHP SDK v2.4.4 or later is required. Earlier versions may contain bugs and need to be upgraded to the [latest version](https://github.com/tencentyun/cos-php-sdk-v5/releases/) when used.
>

| API | Description |
| :----------------------------------------------------------- | :------------------------- |
| [Submitting file moderation job](https://intl.cloud.tencent.com/document/product/436/48258) | Submits file moderation job.   |
| [Querying file moderation job result](https://intl.cloud.tencent.com/document/product/436/48259)  | Queries the result of specified file moderation job. |

## Submitting File Moderation Job

#### Feature description

This API is used to submit a file moderation job.

#### Method prototype

```php
public Guzzle\Service\Resource\Model detectDocument(array $args = array());
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
    $result = $cosClient->detectDocument(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
        'Input' => array(
            'Url' => 'https://example.com/test01.docx', // Full URL of the file
            'Type' => 'docx', // File type
        ),
        'Conf' => array(
            'DetectType' => 'Porn,Ads', // Valid values: `Porn`, `Ads`. Multiple rules can be used. Be sure not to add spaces between them.
//            'Callback' => 'https://example.com/callback/', // Callback address
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


#### Parameter description

`Request` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :------ | :------------- | :-------- | :------- |
| Input | Request | Content to be moderated. | Container | Yes |
| Conf | Request | Moderation rule configuration. | Container | Yes |

`Input` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :------------ | :----------------------------------------------------------- | :-------- | :------- |
| Object | Request.Input | Name of the file stored in the COS bucket; for example, if the file is `test.doc` in the `test` directory, then the filename is `test/test.doc`. Either `Object` or `Url` can be selected at a time. | String | No |
| Url | Request.Input | Full URL of the file, such as `http://www.example.com/doctest.doc`. Either `Object` or `Url` can be selected at a time. | String | No |
| Type | Request.Input | File type. If this parameter is not specified, the file extension will be used as the type by default, such as DOC, DOCX, PPT, and PPTX. If the file has no extension, this field must be specified; otherwise, moderation will fail. | String | No |
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
| BizType | Request.Conf | Unique identifier of the moderation policy. You can configure the scenes you want to moderate on the moderation policy page in the console, such as pornographic, adverting, and illegal information. For configuration guidelines, see [Setting Moderation Policy](https://intl.cloud.tencent.com/document/product/436/48258#1). You can get `BizType` in the console. If `BizType` is specified, the moderation request will perform moderation based on the scenes configured in the moderation policy. If `BizType` is not specified, the default moderation policy will be used automatically. | String | No |
| DetectType | Request.Conf | The scene to be moderated, such as `Porn` (pornography) and `Ads` (advertising). This parameter will no longer be maintained in the future. You can pass in multiple types and separate them by comma, such as `Porn,Ads`. If you need to moderate more scenes, use the `BizType` parameter. | String | No |
| Callback | Request.Conf | The moderation result can be sent to your callback address in the form of a callback. Addresses starting with `http://` or `https://` are supported, such as `http://www.callback.com`.  | String | No |

#### Sample response

```php
GuzzleHttp\Command\Result Object
(
    [RequestId] => NjEzZTBjMmRfNzgwYzdkNjRfMThiOV8zZTY4ZGE=
    [ContentType] => application/xml
    [ContentLength] => 357
    [JobsDetail] => Array
        (
            [Url] => https://example.com/test01.pdf
            [JobId] => sd48e1ea1213d411ec953452540024deb5
            [State] => Submitted
            [CreationTime] => 2021-09-12T22:18:21+08:00
        )

    [Bucket] => examplebucket-1250000000
    [Location] => examplebucket-1250000000.ci.ap-guangzhou.myqcloud.com/document/auditing
)
```


## Querying File Moderation Job

#### Feature description

This API is used to query the status and result of a file moderation job.

#### Method prototype

```php
public Guzzle\Service\Resource\Model getDetectDocumentResult(array $args = array());
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
    $result = $cosClient->getDetectDocumentResult(array(
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
| Key | String | ID of the job to be queried. | Yes |

#### Sample response

```php
GuzzleHttp\Command\Result Object
(
    [RequestId] => NjEzZTBjZWRfZmNjYTNiMGFfNGM2M18zZGUzNzc=
    [ContentType] => application/xml
    [ContentLength] => 1725
    [Key] => sd48e1ea1213d411ec953452540024deb5
    [Bucket] => examplebucket-1250000000
    [Location] => examplebucket-1250000000.ci.ap-guangzhou.myqcloud.com/document/auditing/sd48e1ea1213d411ec953452540024deb5
    [Response] => Array
        (
            [JobsDetail] => Array
                (
                    [CreationTime] => 2021-09-12T22:18:21+08:00
                    [JobId] => sd48e1ea1213d411ec953452540024deb5
                    [Labels] => Array
                        (
                            [AdsInfo] => Array
                                (
                                    [HitFlag] => 0
                                    [Score] => 0
                                )

                            [PornInfo] => Array
                                (
                                    [HitFlag] => 0
                                    [Score] => 0
                                )

                        )

                    [PageCount] => 1
                    [PageSegment] => Array
                        (
                            [Results] => Array
                                (
                                    [AdsInfo] => Array
                                        (
                                            [HitFlag] => 0
                                            [Score] => 0
                                            [SubLabel] => Array
                                                (
                                                )

                                        )

                                    [PageNumber] => 1
                                    [PornInfo] => Array
                                        (
                                            [HitFlag] => 0
                                            [Score] => 0
                                            [SubLabel] => Array
                                                (
                                                )

                                        )

                                    [Text] => PDF test file.
                                    [Url] => https://auditing-appid.cos.ap-chongqing.myqcloud.com/%2Fdocument%2F872400-1251668577%2Fsd48e1ea1213d411ec953452540024deb5%2Foutput%2F1.jpg?q-sign-algorithm=sha1&q-ak=AKIDziAUWHqzwb2DsGIJzOD1hHajzyhyglHW&q-sign-time=1631456493%3B1631463693&q-key-time=1631456493%3B1631463693&q-header-list=host&q-url-param-list=&q-signature=870d00e9c5a3e847bff53fa32e30bfc0d06bbcf9
                                )

                        )

                    [State] => Success
                    [Suggestion] => 0
                    [Url] => https://example.com/test01.pdf
                )

            [RequestId] => NjEzZTBjZWRfZmNjYTNiMGFfNGM2M18zZGUzNzc=
        )

)
```

