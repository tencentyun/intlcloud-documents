## Overview
This document describes how to use the content moderation feature provided by [Cloud Infinite (CI)](https://www.tencentcloud.com/document/product/1045). CI fully integrates the processing capabilities with the COS SDK.

>?To use the content moderation service, you need to have the permission to use CI:
- For root accounts, click [here](https://console.cloud.tencent.com/cam/role/grant?roleName=CI_QCSRole&policyName=QcloudCOSDataFullControl,QcloudAccessForCIRole,QcloudPartAccessForCIRole&principal=eyJzZXJ2aWNlIjoiY2kucWNsb3VkLmNvbSJ9&serviceType=%E6%95%B0%E6%8D%AE%E4%B8%87%E8%B1%A1&s_url=https%3A%2F%2Fconsole.cloud.tencent.com%2Fci) for role authorization.
- For sub-accounts, see [Authorizing Sub-Accounts to Access CI Services](https://intl.cloud.tencent.com/document/product/1045/33450).

This document provides an overview of APIs and SDK code samples for image moderation.
<table>
	<tr><th width=13%>API</th><th>Description</th></tr>
	<tr><td><a href="https://intl.cloud.tencent.com/document/product/436/48537"> Single image moderation</a></td><td>The existing data scan feature of image moderation leverages CI's persistent processing API to scan existing data stored in COS for pornographic, illegal, and advertising images. Content moderation requests are `GET` requests.</td></tr>
	<tr><td><a href="https://intl.cloud.tencent.com/document/product/436/48538">Batch image moderation</a></td><td>The batch image moderation API adopts a sync POST request method. You can use this API to perform content moderation on multiple image files.</td></tr>
</table>



## Single Image Moderation

#### Feature description

This API is used to moderate images in COS, including pornographic, illegal, and advertising images. 

#### Sample code

```shell
    """Test the CI's API for moderating content in a single image"""
    from qcloud_cos import CosConfig
    from qcloud_cos import CosS3Client
    from qcloud_cos.cos_comm import CiDetectType
    # Create a COS client
    response = client.get_object_sensitive_content_recognition(
        Bucket=test_bucket,
        Key=test_object,
        DetectUrl='https://examplebucket-1250000000.cos.ap-chongqing.myqcloud.com/tttt.jpg',
        DetectType=(CiDetectType.PORN | CiDetectType.ADS)
    )
    print(response)
```

#### Parameter description

The `get_object_sensitive_content_recognition` function is called. Specific request parameters are as follows:

| Parameter | Description | Type | Required |
| --------- | ------------------------------------------------------------ | ------ | -------- |
| Key | Object name, such as `picture.jpg`.                                 | String  | Yes      |
| BizType | Unique identifier of the moderation policy. You can configure the scenes you want to moderate on the moderation policy page in the console, such as pornographic, adverting, and illegal information. For configuration guidelines, see [Setting Public Moderation Policy](https://intl.cloud.tencent.com/document/product/436/52095). You can get `BizType` in the console. If `BizType` is specified, the moderation request will perform moderation based on the scenes configured in the moderation policy. If `BizType` is not specified, the default moderation policy will be used automatically. | String | No |
| DetectType      | Moderation type. Valid values: `CiDetectType.PORN` (pornography), `CiDetectType.ADS` (advertising). You can select multiple types. For example, `CiDetectType.PORN \| CiDetectType.ADS` indicates to moderate the image for pornographic and advertising information. If you need more moderation scenes, use the `BizType` parameter.  | enum | No        |
| Interval | Frame capturing frequency, which takes effect for GIF/long images only. The default value is `0`, indicating to detect only the first frame of the GIF/long image.                               | Int  | No       |
| MaxFrames | The maximum number of frames to be captured, which takes effect for GIF/long images only. The default value is `1`, indicating to capture only the first frame of the GIF image for moderation, or that the long image will not be split.                                | Int  | No       |
| DetectUrl         | You can enter a `detect-url` value to moderate an image accessible over the public network. If `detect-url` is not specified, the backend will moderate by `ObjectKey` by default. If `detect-url` is specified, the backend will moderate by `detect-url`, and there is no need to enter `ObjectKey`. Sample `detect-url`: http://www.example.com/abc.jpg | String | No       |
| LargeImageDetect | Whether to compress the image that exceeds the size limit before moderation. Valid values: `0` (no), `1` (yes). Default value: `0`. Note: Images up to 32 MB in size can be compressed, and compression fees will be charged.                                | Int  | No       |
| dataid | Image ID. This field will return the original content in the result, which can contain up to 512 bytes. | String | No |

#### Response parameters

Calling the `get_object_sensitive_content_recognition` function will convert the XML returned in the API into a `dict` value. For specific response parameters, see [Single Image Moderation](https://intl.cloud.tencent.com/document/product/436/48537).

## Batch Image Moderation

#### Feature description

This API is used to moderate multiple images in COS, including pornographic, illegal, and advertising images.

#### Sample code

```shell
    """Test the CI's API for batch moderating content in images"""
    from qcloud_cos import CosConfig
    from qcloud_cos import CosS3Client
    from qcloud_cos.cos_comm import CiDetectType
    # Create a COS client
    response = client.ci_auditing_image_batch(
        Bucket=bucket_name,
        DetectType=CiDetectType.PORN,
        Input=[{
            'Url':'https://examplebucket-1250000000.cos.ap-chongqing.myqcloud.com/porn_ocr.png',
            'DataId': 'testdataid-111111',
            'UserInfo':{
            'TokenId': 'token',
            'Nickname': 'test',
            'DeviceId': 'DeviceId-test',
            'AppId': 'AppId-test',
            'Room': 'Room-test',
            'IP': 'IP-test',
            'Type': 'Type-test',
        },
        },{
            'Object':'test-0.jpg',
            'LargeImageDetect' :1,
        },{
            'Url':'https://examplebucket-1250000000.cos.ap-chongqing.myqcloud.com/pron_plitics_ads_terrism.png',
        }]
    )
    print(response)
```

#### Parameter description

The `ci_auditing_image_batch` function is called. Specific request parameters are as follows:

| Parameter | Description | Type | Required |
| --------- | ------------------------------------------------------------ | ------ | -------- |
| Bucket | Bucket name.                                 | String  | Yes       |
| BizType | Unique identifier of the moderation policy. It is automatically generated by the backend and corresponds to the `Biztype` value in the console.                                 | String  | No       |
| DetectType      | Moderation type. Valid values: `CiDetectType.PORN` (pornography), `CiDetectType.ADS` (advertising). You can select multiple types. For example, `CiDetectType.PORN \| CiDetectType.ADS` indicates to moderate the image for pornographic and advertising information. If you need more moderation scenes, use the `BizType` parameter.  | enum | No        |
| Input | Information of the image to be moderated. Each array element is of the dict type. The following parameters are supported:<br>**Object**: Name of the image file stored in the COS bucket. For example, if the file is `image.jpg` in the `test` directory, the file name is `test/image.jpg`. Either `Object` or `Url` can be selected at a time. <br>`Url`: URL of the image file, for example, `http://a-1250000.cos.ap-shanghai.tencentcos.cn/image.jpg`. Either `Object` or `Url` can be selected at a time. <br>`Interval`: Frame capturing frequency, which takes effect for GIF images only. The default value is `5`, indicating to capture a frame every five frames starting from the first frame (included). <br>`MaxFrames`: The maximum number of frames to be captured, which takes effect for GIF images only. The default value is `5`, indicating to capture only five frames of the GIF image for moderation. The parameter value must be greater than 0. <br>`DataId`: Image identifier. This field will return the original content in the result, which can contain up to 512 bytes. <br>`LargeImageDetect`: Whether to compress the image that exceeds the size limit before moderation. Valid values: `0` (no), `1` (yes). Default value: `0`. Note: Images up to 32 MB in size can be compressed, and compression fees will be charged. <br>`UserInfo`: Business field.                                 | Array  | No       |

#### Response parameters

Calling the `ci_auditing_image_batch` function will convert the XML returned in the API into a `dict` value. For specific response parameters, see [Batch Image Moderation](https://intl.cloud.tencent.com/document/product/436/48538).
