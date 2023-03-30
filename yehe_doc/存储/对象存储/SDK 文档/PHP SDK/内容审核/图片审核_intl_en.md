## Overview
This document describes how to use the content moderation feature provided by [Cloud Infinite (CI)](https://www.tencentcloud.com/document/product/1045). CI fully integrates the processing capabilities with the COS SDK.

>?To use the content moderation service, you need to have the permission to use CI:
- For root accounts, click [here](https://console.cloud.tencent.com/cam/role/grant?roleName=CI_QCSRole&policyName=QcloudCOSDataFullControl,QcloudAccessForCIRole,QcloudPartAccessForCIRole&principal=eyJzZXJ2aWNlIjoiY2kucWNsb3VkLmNvbSJ9&serviceType=%E6%95%B0%E6%8D%AE%E4%B8%87%E8%B1%A1&s_url=https%3A%2F%2Fconsole.cloud.tencent.com%2Fci) for role authorization.
- For sub-accounts, see [Authorizing Sub-Accounts to Access CI Services](https://www.tencentcloud.com/document/product/1045/33450).

This document provides an overview of APIs and SDK code samples for image moderation.
>! COS PHP SDK v2.4.4 or later is required. Earlier versions may contain bugs and need to be upgraded to the [latest version](https://github.com/tencentyun/cos-php-sdk-v5/releases/) when used.
>

| API | Description |
| ------------- |  ---------------------- |
| [Moderating single image](https://www.tencentcloud.com/document/product/436/48537) | The image moderation API supports both sync and async GET request methods. You can use this API to perform content moderation on an image file. |
| [Batch moderating images](https://www.tencentcloud.com/document/product/436/48538) | The batch image moderation API adopts a sync POST request method. You can use this API to perform content moderation on multiple image files. |


## Single Image Moderation

#### Feature description

The image moderation API supports both sync and async GET request methods. You can use this API to perform content moderation on an image file.

#### Method prototype

```php
public Guzzle\Service\Resource\Model detectImage(array $args = array());
```

#### Request example

#### Example 1: Moderating an image in the specified bucket path
```php
<?php

require dirname(__FILE__) . '/../vendor/autoload.php';

$secretId = "SECRETID"; //Replace it with the actual `SecretId`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi
$secretKey = "SECRETKEY"; //Replace it with the actual `SecretKey`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi
$region = "ap-beijing"; //Replace it with the actual `region`, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket.
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', // `https` must be used during moderation.
        'credentials' => array(
            'secretId'  => $secretId,
            'secretKey' => $secretKey)));
try {
    // Moderate an image in a bucket
    $result = $cosClient->detectImage(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-APPID`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
        'Key' => 'test.png', // File in the bucket
        'ci-process' => 'sensitive-content-recognition',
//        'BizType' => '', // (Optional) Custom policy. If this parameter is not specified, the default policy will be used.
//        'DetectType' => 'porn,ads', // (Optional) Valid values: `porn`, `ads`. Multiple rules can be used. Be sure not to add spaces between them. If this parameter is not specified, the default or custom policy will be used.
//        'Interval' => 5, // (Optional) Frame capturing interval for GIF moderation
//        'MaxFrames' => 5, // (Optional) The maximum number of frames to be captured for GIF image moderation, which must be greater than 0.
//        'LargeImageDetect' => '',
//        'DataId' => '',
//        'Async' => '',
//        'Callback' => '',
    ));
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Example 2: Moderating an image at a specified URL

```php
<?php

require dirname(__FILE__) . '/../vendor/autoload.php';

$secretId = "SECRETID"; //Replace it with the actual `SecretId`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi
$secretKey = "SECRETKEY"; //Replace it with the actual `SecretKey`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi
$region = "ap-beijing"; //Replace it with the actual `region`, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket.
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', // `https` must be used during moderation.
        'credentials' => array(
            'secretId'  => $secretId,
            'secretKey' => $secretKey)));
try {
    // Moderate an image URL
    $imgUrl = 'https://test.jpg';
    $result = $cosClient->detectImage(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-APPID`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
        'Key' => '/', // Enter `/` in case of image resource URL moderation
        'ci-process' => 'sensitive-content-recognition',
        'DetectUrl' => $imgUrl,
//        'BizType' => '', // (Optional) Custom policy. If this parameter is not specified, the default policy will be used.
//        'DetectType' => 'porn,ads', // (Optional) Valid values: `porn`, `ads`. Multiple rules can be used. Be sure not to add spaces between them. If this parameter is not specified, the default or custom policy will be used.
//        'Interval' => 5, // (Optional) Frame capturing interval for GIF moderation
//        'MaxFrames' => 5, // (Optional) The maximum number of frames to be captured for GIF image moderation, which must be greater than 0.
//        'LargeImageDetect' => '',
//        'DataId' => '',
//        'Async' => '',
//        'Callback' => '',
    ));
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameter description for single image moderation

`Request` has the following parameters:

| Parameter | Description | Type | Required |
| :--------------- | :----------------------------------------------------------- | :----- | :------- |
| Key          | Name of the image file in the COS bucket. The COS bucket is specified by `Host`. For example, if the file is `img.jpg` in the `test` directory in the `examplebucket-1250000000` bucket in Beijing, then `Host` is `examplebucket-1250000000.cos.ap-beijing.myqcloud.com`, and `Key` is `test/img.jpg`. | String | No |
| ci-process         | This field identifies the data processing feature, which is `sensitive-content-recognition` for content moderation. | String | Yes |
| BizType | Unique identifier of the moderation policy. You can configure the scenes you want to moderate on the moderation policy page in the console, such as pornographic, advertising, and illegal information. For configuration guidelines, see [Setting Public Moderation Policy](https://intl.cloud.tencent.com/document/product/436/48537#1). You can get `BizType` in the console. If `BizType` is specified, the moderation request will perform moderation based on the scenes configured in the moderation policy. If `BizType` is not specified, the default moderation policy will be used automatically. | String | No |
| DetectType        | The scene to be moderated, such as `Porn` (pornography) and `Ads` (advertising). This parameter will no longer be maintained in the future. You can pass in multiple types and separate them by commas, such as `Porn,Ads`. If you need to moderate more scenes, use the `BizType` parameter. | String | No       |
| DetectUrl         | You can enter a `DetectUrl` value to moderate an image accessible over the public network. <li>If `DetectUrl` is not specified, the backend will moderate by `Key` by default. </li><li>If `DetectUrl` is specified, the backend will moderate by `DetectUrl`, and there is no need to enter `Key`. <br>Sample `detect-url`: http://www.example.com/abc.jpg</li> | String | No       |
| Interval           | For GIF image moderation, you can use this parameter to configure the frame capturing interval. The default value is `5`, indicating to capture a frame every five frames starting from the first frame (included). | Int | No |
| MaxFrames         | The maximum number of frames to be captured for GIF image moderation, which must be greater than 0. The default value is `5`, indicating to capture five frames at most. | Int | No |
| LargeImageDetect | Whether to compress the image that exceeds the size limit before moderation. Valid values: `0` (no), `1` (yes). Default value: `0`. Note: Images up to 32 MB in size can be compressed, and image compression fees will be charged. For large animated images such as GIF, the compression time is long, which may cause the moderation to fail due to timeout. | Int | No |
| DataId | Image ID. This field will return the original content in the result, which can contain up to 512 bytes. | String | No |
| Async    | Request method. Valid values: `0` (returns the result synchronously); `1` (moderates asynchronously). Default value: `0`. | Int | No |
| Callback | Callback address. The moderation result (in `Detail` mode) can be sent to your callback address in the form of a callback. This parameter takes effect only for async moderation. Addresses starting with `http://` or `https://` are supported, such as  `http://www.callback.com`.  | String | No |

#### 

## Batch Image Moderation

#### Feature description

The batch image moderation API adopts a sync POST request method. You can use this API to perform content moderation on multiple image files.

#### Method prototype

```php
public Guzzle\Service\Resource\Model detectImages(array $args = array());
```

#### Request example

```php
<?php

require dirname(__FILE__, 2) . '/vendor/autoload.php';

$secretId = "SECRETID"; //Replace it with the actual `SecretId`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi
$secretKey = "SECRETKEY"; //Replace it with the actual `SecretKey`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi
$region = "ap-beijing"; //Replace it with the actual `region`, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket.
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', // `https` must be used during moderation.
        'credentials' => array(
            'secretId'  => $secretId,
            'secretKey' => $secretKey)));
try {
    // Get the Base64-encoded image file content
//    $localImageFile = '/tmp/test.jpg';
//    $img = file_get_contents($localImageFile);
//    $imgInfo = getimagesize($localImageFile);
//    $imgBase64Content = base64_encode($img);

    $result = $cosClient->detectImages(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-APPID`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
        'Inputs' => array(
            array(
                'Object' => 'test01.png', // Bucket file
//                'Interval' => '', // (Optional) Frame capturing interval for GIF moderation
//                'MaxFrames' => '', // (Optional) The maximum number of frames to be captured for GIF image moderation, which must be greater than 0.
//                'DataId' => 'aaa', // (Optional) Image ID. This field will return the original content in the result, which can contain up to 512 bytes.
            ),
            array(
                'Url' => 'http://example.com/test.png', // Image URL
//                'Interval' => 5, // (Optional) Frame capturing interval for GIF moderation
//                'MaxFrames' => 5, // (Optional) The maximum number of frames to be captured for GIF image moderation, which must be greater than 0.
//                'DataId' => 'bbb', // (Optional) Image ID. This field will return the original content in the result, which can contain up to 512 bytes.
            ),
//            array(
//                'Content' => $imgBase64Content, // Image file content, which needs to be Base64-encoded first
////                'Interval' => 5, // (Optional) Frame capturing interval for GIF moderation
////                'MaxFrames' => 5, // (Optional) The maximum number of frames to be captured for GIF image moderation, which must be greater than 0.
////                'DataId' => 'bbb', // (Optional) Image ID. This field will return the original content in the result, which can contain up to 512 bytes.
//            ),
        ),
//        'Conf' => array(
//        'BizType' => '', // (Optional) Custom policy. If this parameter is not specified, the default policy will be used.
//            'DetectType' => 'Porn,Ads', // (Optional) Valid values: `Porn`, `Ads`. Multiple rules can be used. Be sure not to add spaces between them. If this parameter is not specified, the default or custom policy will be used.
//            'Async' => 0, // (Optional) Whether to moderate asynchronously. Valid values: `0` (returns the result synchronously); `1` (moderates asynchronously). Default value: `0`.
//            'Callback' => '', // (Optional) The moderation result (in `Detail` mode) can be sent to your callback address in the form of a callback.
//        ) // (Optional) If neither `DetectType` nor `BizType` is passed in, the default policy and default moderation scene will be used.
    ));
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameter description for batch moderation

`Request` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :------ | :---------------------------------------------------- | :-------------- | :------- |
| Input | Request | Content to be moderated. If there are multiple images, pass in multiple `Input` structures. | Container Array | Yes |
| Conf | Request | Moderation rule configuration. | Container | Yes |

`Input` has the following sub-nodes, and you need to use only one of these sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :------------ | :----------------------------------------------------------- | :-------- | :------- |
| Object | Request.Input | Name of the image file stored in the COS bucket; for example, if the file is `image.jpg` in the `test` directory, then the filename is `test/image.jpg`. You can select only one parameter among `Content`, `Object`, and `Url` at a time. If more than one parameter is passed in, only one parameter takes effect (in the priority of `Content`, `Object`, and `Url`). | String | No |
| Url | Request.Input | Full URL of the image file, such as `http://a-1250000.cos.ap-shanghai.myqcloud.com/image.jpg`. You can select only one parameter among `Content`, `Object`, and `Url` at a time. If more than one parameter is passed in, only one parameter takes effect (in the priority of `Content`, `Object`, and `Url`). | String | No |
| Content            | Request.Input | Image file content, which needs to be Base64-encoded first. You can select only one parameter among `Content`, `Object`, and `Url` at a time. If more than one parameter is passed in, only one parameter takes effect (in the priority of `Content`, `Object`, and `Url`). | String | No |
| Interval | Request.Input | Frame capturing frequency, which takes effect for GIF images only. The default value is `5`, indicating to capture a frame every five frames starting from the first frame (included). | Int | No |
| MaxFrames | Request.Input | The maximum number of frames to be captured, which takes effect for GIF images only. The default value is `5`, indicating to capture only five frames of the GIF image for moderation. The parameter value must be greater than 0. | Int | No |
| DataId | Request.Input | Image ID. This field will return the original content in the result, which can contain up to 512 bytes. | String | No |
| LargeImageDetect | Whether to compress the image that exceeds the size limit before moderation. Valid values: `0` (no), `1` (yes). Default value: `0`. Note: Images up to 32 MB in size can be compressed, and compression fees will be charged.                                | Int  | No       |
| UserInfo | Request.Input | Business field. | Container | No |

`UserInfo` has the following sub-nodes:

| Node Name (Keyword)  | Description                                                         | Type   | Required |
| :----------------- | :-------------------------------------------------- | :----- | :------- |
| TokenId            | Account information, which can contain up to 128 bytes.           | String | No       |
| Nickname           | Nickname information, which can contain up to 128 bytes.           | String | No       |
| DeviceId           | Device information, which can contain up to 128 bytes.           | String | No       |
| AppId              | Unique app ID, which can contain up to 128 bytes.           | String | No       |
| Room               | Room ID information, which can contain up to 128 bytes.           | String | No       |
| IP                 | IP address information, which can contain up to 128 bytes.           | String | No       |
| Type               | Business type, which can contain up to 128 bytes.           | String | No       |
| ReceiveTokenId     | User account to receive messages, which can contain up to 128 bytes.           | String | No       |
| Gender             | Gender information, which can contain up to 128 bytes.           | String | No       |
| Level              | Level information, which can contain up to 128 bytes.           | String | No       |
| Role               | Role information, which can contain up to 128 bytes.           | String | No       |

`Conf` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :----------- | :----------------------------------------------------------- | :------ | :------- |
| BizType            | Request.Conf | Unique identifier of the moderation policy. You can configure the scenes you want to moderate on the moderation policy page in the console, such as pornographic, advertising, and illegal information. For configuration guidelines, see [Setting Public Moderation Policy](https://intl.cloud.tencent.com/document/product/436/48538#1). You can get `BizType` in the console. If `BizType` is specified, the moderation request will perform moderation based on the scenes configured in the moderation policy. If `BizType` is not specified, the default moderation policy will be used automatically. | String | No |
| DetectType | Request.Conf | The scene to be moderated, such as `Porn` (pornography) and `Ads` (advertising). This parameter will no longer be maintained in the future. You can pass in multiple types and separate them by commas, such as `Porn,Ads`. If you need to moderate more scenes, use the `BizType` parameter. | String | No |
| Async | Request.Conf | Whether to moderate asynchronously. Valid values: `0` (returns the result synchronously); `1` (moderates asynchronously). Default value: `0`.  | Integer | No |
| Callback | Request.Conf | The moderation result (in `Detail` mode) can be sent to your callback address in the form of a callback. This parameter takes effect in async moderation. Addresses starting with `http://` or `https://` are supported, such as `http://www.callback.com`.  | String | No |
