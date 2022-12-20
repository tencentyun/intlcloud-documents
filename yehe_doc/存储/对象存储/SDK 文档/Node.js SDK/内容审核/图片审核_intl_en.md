## Overview
This document describes how to use the content moderation feature provided by [Cloud Infinite (CI)](https://www.tencentcloud.com/document/product/1045). CI fully integrates the processing capabilities with the COS SDK.

>?To use the content moderation service, you need to have the permission to use CI:
- For root accounts, click [here](https://console.cloud.tencent.com/cam/role/grant?roleName=CI_QCSRole&policyName=QcloudCOSDataFullControl,QcloudAccessForCIRole,QcloudPartAccessForCIRole&principal=eyJzZXJ2aWNlIjoiY2kucWNsb3VkLmNvbSJ9&serviceType=%E6%95%B0%E6%8D%AE%E4%B8%87%E8%B1%A1&s_url=https%3A%2F%2Fconsole.cloud.tencent.com%2Fci) for role authorization.
- For sub-accounts, see [Authorizing Sub-Accounts to Access CI Services](https://intl.cloud.tencent.com/document/product/1045/33450).

This document provides an overview of APIs and SDK code samples for image moderation.
>! The COS Node.js SDK version must be at least v2.11.2.
>

| API | Description |
| ------------- |  ---------------------- |
| [Moderating single image](https://intl.cloud.tencent.com/document/product/436/48537) |  Scans existing data stored in COS for pornographic, illegal, and advertising images. |
| [Batch moderating images](https://intl.cloud.tencent.com/document/product/436/48538) |  Moderates multiple images in batches. |


## Single Image Moderation

#### Feature description

The existing data scan feature of image moderation leverages CI's persistent processing API to scan existing data stored in COS for pornographic, illegal, and advertising images.

#### Sample code

```js
var config = {
  // Replace with your own bucket information
  Bucket: 'examplebucket-1250000000', /* Bucket (required) */
  Region: 'COS_REGION', /* Bucket region (required) */
};
function getImageAuditing() {
  cos.request({
      Bucket: config.Bucket,
      Region: config.Region,
      Method: 'GET',
      Key: '1.png',  /* Image file in the bucket (required) */
      Query: {
          'ci-process': 'sensitive-content-recognition', /** Fixed value (required) */
          'biz-type': '', /** Moderation type (optional) */
          'detect-type': 'porn,ads', /** Moderation policy (optional). If this parameter is not specified, the default policy will be used. */
          'detect-url': '', /** URL of any image accessible over the public network (optional) */
          'interval': 5, /** Frame capturing interval for GIF image moderation (optional) */
          'max-frames': 5,  /** Maximum number of frames to be captured for GIF image moderation (optional) */
          'large-image-detect': '0', /** Whether to compress the image first before moderation (optional) */
          'dataid': '123', /** Custom image ID (optional) */
      },
  },
  function(err, data){
      console.log(err || data);
  });
}
```


#### Parameter description

`Query` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------- | -------------------------------------------------------- | --------- | ---- |
| biz-type    | Query| Moderation policy. If this parameter is not specified, the default policy will be used. The policy can be configured in the console. For more information, see [Setting Moderation Policy](https://intl.cloud.tencent.com/document/product/1045/52107). | String | No |
| detect-type | Query | Moderation type. Valid values: `porn`, `ads`. You can specify multiple types and separate them by comma. | String    | No |
| object-key | Query | Location of the image in the bucket. | String    | Yes   |
| detect-url  | Query| You can enter a `detect-url` value to moderate an image accessible over the public network. <ul  style="margin: 0;"><li>If `detect-url` is not specified, the backend will moderate by `ObjectKey` by default. </li><li>If `detect-url` is specified, the backend will moderate by `detect-url`, and there is no need to enter `ObjectKey`. Sample `detect-url`: http://www.example.com/abc.jpg.</li></ul> | String | No       |
| interval   | Query | For GIF image moderation, you can use this parameter to configure the frame capturing interval. The default value is `5`, indicating to capture a frame every five frames starting from the first frame (included). | Int    | No       |
| max-frames | Query | The maximum number of frames to be captured for GIF image moderation, which must be greater than 0. The default value is `5`, indicating to capture five frames at most. | Int    | No       |
| large-image-detect    | Query| Whether to compress the image that exceeds the size limit before moderation. Valid values: `0` (no), `1` (yes). Default value: `0`. <br>Note: Images up to 32 MB in size can be compressed, and compression fees will be charged. | String | No       |
| dataid    | Query| Image ID. This field will return the original content in the result, which can contain up to 512 bytes. 	| String | No |


#### Response description

For more information, see [Single Image Moderation](https://intl.cloud.tencent.com/document/product/436/48537#.E5.93.8D.E5.BA.94).

## Batch Image Moderation

#### Feature description

The batch image moderation API adopts a sync POST request method. You can use this API to perform content moderation on multiple image files.

#### Sample request

```js
var config = {
  // Replace with your own bucket information
  Bucket: 'examplebucket-1250000000', /* Bucket (required) */
  Region: 'COS_REGION', /* Bucket region (required) */
};
function postImagesAuditing() {
  var host = config.Bucket + '.ci.' + config.Region + '.myqcloud.com';
  var url = 'https://' + host + '/image/auditing';
  var body = COS.util.json2xml({
    Request: {
      Input: [{
        Object: '1.png', /* Path of the image to be moderated in the bucket */
      }, {
        Object: 'a/6.png', /* Path of the image to be moderated in the bucket */
      }],
      Conf: {
        BizType: '', /* If this parameter is not specified, the default policy will be used. */
        DetectType: 'Porn' /* Checks for pornographic information only */
      }
    }
  });
  cos.request({
      Bucket: config.Bucket,
      Region: config.Region,
      Method: 'POST',
      Url: url,
      Key: '/image/auditing', /** Fixed value (required) */
      ContentType: 'application/xml', /** Fixed value (required) */
      Body: body
  },
  function(err, data){
      console.log(err || data);
  });
}
```


#### Parameter description

`request` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :----- | :------------------------- | :-------- | :--- |
| Request | None | Batch image moderation configuration. | Container | Yes |

`Request` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :------ | :-------------------------------------------------- | :-------------- | :--- |
| Input | Request | Content to be moderated. If there are multiple images, pass in multiple `Input` structures. | Container Array | Yes |
| Conf | Request | Moderation rule configuration. | Container | Yes |

`Input` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :------------ | :----------------------------------------------------------- | :----- | :--- |
| Object | Request.Input | Name of the image file stored in the COS bucket; for example, if the file is `image.jpg` in the `test` directory, then the filename is `test/image.jpg`. Either `Object` or `Url` can be selected at a time. | String | No |
| Url | Request.Input | Full URL of the image file, such as `http://a-1250000.cos.ap-shanghai.myqcloud.com/image.jpg`. Either `Object` or `Url` can be selected at a time. | String | No |
| Interval | Request.Input | Frame capturing frequency, which takes effect for GIF images only. The default value is `5`, indicating to capture a frame every five frames starting from the first frame (included). | Int | No |
| MaxFrames | Request.Input | The maximum number of frames to be captured, which takes effect for GIF images only. The default value is `5`, indicating to capture only five frames of the GIF image for moderation. The parameter value must be greater than 0. | Int | No |
| DataId | Request.Input | Image ID. This field will return the original content in the result, which can contain up to 512 bytes. | String | No |

`Conf` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :----------- | :----------------------------------------------------------- | :----- | :--- |
| DetectType | Request.Conf | The scene to be moderated, such as `Porn` (pornography) and `Ads` (advertising). You can pass in multiple types and separate them by comma, such as `Porn,Ads`. | String | Yes |
| BizType            | Request.Conf | Moderation policy. If this parameter is not specified, the default policy will be used. The policy can be configured in the console. For more information, see [Setting Moderation Policy](https://intl.cloud.tencent.com/document/product/436/52095). | String | No |


>!
> - Moderation through `Object` is a private network operation and will not generate public network traffic.
> - Moderation through `Url` will generate public network traffic with regard to the origin where the image resides.
> 

#### Response description

For more information, see [Batch Image Moderation](https://intl.cloud.tencent.com/document/product/436/48538#.E5.93.8D.E5.BA.94).

