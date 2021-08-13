## Overview

This document provides an overview of APIs and SDK code samples related to persistent image processing.

| API | Operation    |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [Persistent Image Processing](https://cloud.tencent.com/document/product/436/54050) | COS supports processing images upon upload. You can also process images that are already stored in COS and save the processed images to COS. |

## Processing upon Upload

#### Feature description

The feature of processing upon upload provided by CI helps you implement image processing when uploading an image. You only need to add Pic-Operations to the request header and set related parameters to implement image processing when uploading an image, and store the input image and processing result in COS. Currently, this feature supports the processing of a file up to 20 MB.

#### Method prototype

```
ci_put_object(self, Bucket, Body, Key, EnableMD5=False, **kwargs)
```

#### Sample request

```python
with open('local.jpg', 'rb') as fp:
	response, data = client.ci_put_object(
		Bucket='examplebucket-1250000000',
        Body=fp,
        Key=ci_file_name,
        # pic operation json struct
        PicOperations='{"is_pic_info":1,"rules":[{"fileid":"format.png","rule":"imageView2/format/png"}]}')
```

#### Sample request with all parameters

```python
response = client.ci_put_object(
    Bucket='examplebucket-1250000000',
    Body=b'bytes'|file,
    Key='exampleobject',
    EnableMD5=False|True,
    ACL='private'|'public-read', # Please be aware that by using this parameter, the maximum of 1000 ACLs may be reached
    GrantFullControl='string',
    GrantRead='string',
    StorageClass='STANDARD'|'STANDARD_IA'|'ARCHIVE',
    Expires='string',
    CacheControl='string',
    ContentType='string',
    ContentDisposition='string',
    ContentEncoding='string',
    ContentLanguage='string',
    ContentLength='123',
    ContentMD5='string',
    Metadata={
        'x-cos-meta-key1': 'value1',
        'x-cos-meta-key2': 'value2'
    },
    TrafficLimit='1048576'
    PicOperations='{"is_pic_info":1,"rules":[{"fileid":"format.png","rule":"imageView2/format/png"}]}'
)
```

#### Parameter description

| Parameter | Description | Type | Required |
| ------------------ | ------------------------------------------------------------ | ---------- | -------- |
| Bucket  | Bucket name in the format of `BucketName-APPID`  | String | Yes  |
| Body  | Content of the uploaded object, which can be file stream or byte stream     | file/bytes | Yes |
| Key | Object key, the unique identifier of an object in a bucket. For example, if the object endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg` | String | Yes |
| PicOperations      | CI image processing parameter. For more information, please see [Persistent Image Processing](https://cloud.tencent.com/document/product/436/54050) | String     | Yes       |
| EnableMD5 | Specifies whether the SDK needs to calculate the Content-MD5 value. This feature is disabled by default. The upload will take longer if it is enabled | Bool | No |
| ACL | Sets the object ACL, such as 'private' or 'public-read'                | String     | No |
| GrantFullControl | Grants the grantee full permission in the format of `id="OwnerUin"` | String | No |
| GrantRead  | Grants the grantee read permission in the format of `id="OwnerUin"`                 | String     | No |
| StorageClass | Storage class of the object. For storage classes such as `STANDARD` (default), `STANDARD_IA`, and `ARCHIVE`, please see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/436/30925). | String     | No |
| Expires            | Sets Expires                                                 | String     | No  |
| CacheControl | Cache policy. Sets Cache-Control. | String | No |
| ContentType | Content Type. Sets Content-Type. | String | No |
| ContentDisposition | Filename. Sets Content-Disposition | String | No |
| ContentEncoding | Encoding format. Sets Content-Encoding. | String | No |
| ContentLanguage | Language type. Sets Content-Language | String | No |
| ContentLength | Sets the length of the request content. | String | No |
| ContentMD5 | Sets the MD5 checksum of the uploaded object | String | No |
| Metadata | User-defined object metadata. This parameter must start with `x-cos-meta`; otherwise, it will be ignored | Dict | No |
|  TrafficLimit | Specifies the bandwidth limit for a single request in bit/s. Value range: 819200 - 838860800, i.e., 100 KB/s - 100 MB/s | String |  No |

`PicOperations` is a JSON string. Its parameters are as follows:

| Parameter | Description | Type | Required |
| ----------- | ------------------------------------------------------------ | ----- | -------- |
| is_pic_info | Whether to return the input image information <br>`0` (default): no <br>`1`: yes    | Int   | No       |
| rules       | Processing rules (up to 5 rules are supported). Each rule corresponds to one processing result. If this parameter is not specified, images will not be processed. | Array | No       |

 Parameters of `rules` (a JSON array) are as follows:

| Parameter | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ------ | -------- |
| bucket   | Name of the destination bucket that stores the results, formatted as `BucketName-APPID`. If this parameter is not specified, the results will be stored in the current bucket. | String | No       |
| fileid   | Path of the processing results. If the value of this parameter starts with a slash (/), the results will be stored in a specified folder. Otherwise, the results will be stored in the directory of the input image. | String | Yes       |
| rule     | The processing parameter. For more information, please see the image processing API of CI. If the image needs to be stylized, prefix `style/` to the style name. For example, if the style name is `test`, you can set this parameter to `style/test`. | String | Yes       |

#### Response description

The response contains the original image and processing information in dict format:

```python
{
	'OriginalInfo': {
		'Key': 'local.jpg',
		'Location': 'examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/local.jpg',
		'ETag': '"aff1b996bcc63a0f0259df0de2fa989f38c5ce7e"',
		'ImageInfo': {
			'Format': 'JPEG',
			'Width': '300',
			'Height': '168',
			'Quality': '74',
			'Ave': '0x1a3451',
			'Orientation': '0'
		}
	},
	'ProcessResults': {
		'Object': {
			'Key': 'format.png',
			'Location': 'examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/format.png',
			'Format': 'png',
			'Width': '300',
			'Height': '168',
			'Size': '77063',
			'Quality': '74',
			'ETag': '"a07dc5bcfa238e7d23d2d5884da4ac328aaaa9c6"'
		}
	}
}
```

Parameters in the response body are as follows:

| Parameter | Type | Description |
| ------------ | --------- | -------- |
| UploadResult | Container | Original image information |

 Content of the `UploadResult` node:

| Parameter | Type | Description |
| -------------- | --------- | ------------ |
| OriginalInfo | Container | Original image information |
| ProcessResults | Container | Image processing results |

 Content of the `OriginalInfo` node:

| Parameter | Type | Description |
| --------- | --------- | ---------------------------------------------------------- |
| Key       | String    | Filename of the original image                                                 |
| Location  | String    | Image path                                                   |
| ImageInfo | Container | Information of the original image                                           |
| ETag | String | ETag of the original image. If the output image overwrites the original image, the value of `etag` will be that of the output image |

 Content of the `ImageInfo` node:

| Parameter | Type | Description |
| ----------- | ------ | ------------ |
| Format | String | Format |
| Width | Int | Image width |
| Height | Int | Image height |
| Quality | Int | Image quality |
| Ave | String | Image average hue |
| Orientation | Int | Image rotation angle |

 Content of the `ProcessResults` node:

| Parameter | Type | Description |
| -------- | --------- | ------------------ |
| Object | Container | Processing result of each image |

 Content of the `Object` node:

| Parameter | Type | Description |
| -------- | ------ | -------------------- |
| Key      | String | Filename               |
| Location | String | Image path |
| Format | String | Image format |
| Width    | Int    | Image width             |
| Height | Int | Image height |
| Size     | Int    | Image size             |
| Quality | Int | Image quality |
| ETag | String | ETag of the output image |

## Processing In-Cloud Data

#### Feature description

The persistent image processing API can process an in-cloud image and save the processing result to COS.

#### Method prototype

```
ci_image_process(self, Bucket, Key, **kwargs)
```

#### Sample request

```python
response, data = client.ci_image_process(
	Bucket='examplebucket-1250000000',
 	Key=ci_file_name,
    # pic operation json struct
    PicOperations='{"is_pic_info":1,"rules":[{"fileid":"format.png","rule":"imageView2/format/png"}]}')
```

#### Sample request with all parameters

```python
response, data = client.ci_image_process(
    Bucket='examplebucket-1250000000',
    Key=ci_file_name,
    # pic operation json struct
    PicOperations='{"is_pic_info":1,"rules":[{"fileid":"format.png","rule":"imageView2/format/png"}]}')
```

#### Parameter description

| Parameter | Description | Type | Required |
| ------------- | ------------------------------------------------------------ | ------ | -------- |
| Bucket  | Bucket name in the format of `BucketName-APPID`  | String | Yes  |
| Key | Object key, the unique identifier of an object in a bucket. For example, if the object endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg` | String | Yes |
| PicOperations      | CI image processing parameter. For more information, please see [Persistent Image Processing](https://cloud.tencent.com/document/product/436/54050) | String     | Yes       |

`PicOperations` is a JSON string. Its parameters are as follows:

| Parameter | Description | Type | Required |
| ----------- | ------------------------------------------------------------ | ----- | -------- |
| is_pic_info | Whether to return the input image information <br>`0` (default): no <br>`1`: yes    | Int   | No       |
| rules       | Processing rules (up to 5 rules are supported). Each rule corresponds to one processing result. If this parameter is not specified, images will not be processed. | Array | No       |

 Parameters of `rules` (a JSON array) are as follows:

| Parameter | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ------ | -------- |
| bucket   | Name of the destination bucket that stores the results, formatted as `BucketName-APPID`. If this parameter is not specified, the results will be stored in the current bucket. | String | No       |
| fileid   | Path of the processing results. If the value of this parameter starts with a slash (/), the results will be stored in a specified folder. Otherwise, the results will be stored in the directory of the input image. | String | Yes       |
| rule | String | Yes | Processing parameters. For more information, please see the image processing API. To process an image using a specified style, the value must start with `style/` with the style name followed. For example, if the style name is `test`, the value of `rule` should be `style/test`. |

#### Response description

The response contains object metadata in dict format:

```python
{
	'OriginalInfo': {
		'Key': 'local.jpg',
		'Location': 'examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/local.jpg',
		'ETag': '"aff1b996bcc63a0f0259df0de2fa989f38c5ce7e"',
		'ImageInfo': {
			'Format': 'JPEG',
			'Width': '300',
			'Height': '168',
			'Quality': '74',
			'Ave': '0x1a3451',
			'Orientation': '0'
		}
	},
	'ProcessResults': {
		'Object': {
			'Key': 'format.png',
			'Location': 'examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/format.png',
			'Format': 'png',
			'Width': '300',
			'Height': '168',
			'Size': '77063',
			'Quality': '74',
			'ETag': '"a07dc5bcfa238e7d23d2d5884da4ac328aaaa9c6"'
		}
	}
}
```

Parameters in the response body are as follows:

| Parameter | Type | Description |
| ------------ | --------- | -------- |
| UploadResult | Container | Original image information |

 Content of the `UploadResult` node:

| Parameter | Type | Description |
| -------------- | --------- | ------------ |
| OriginalInfo | Container | Original image information |
| ProcessResults | Container | Image processing results |

 Content of the `OriginalInfo` node:

| Parameter | Type | Description |
| --------- | --------- | ---------------------------------------------------------- |
| Key       | String    | Filename of the original image                                                 |
| Location  | String    | Image path                                                   |
| ImageInfo | Container | Information of the original image                                           |
| ETag | String | ETag of the original image. If the output image overwrites the original image, the value of `etag` will be that of the output image |

 Content of the `ImageInfo` node:

| Parameter | Type | Description |
| ----------- | ------ | ------------ |
| Format | String | Format |
| Width | Int | Image width |
| Height | Int | Image height |
| Quality | Int | Image quality |
| Ave | String | Image average hue |
| Orientation | Int | Image rotation angle |

 Content of the `ProcessResults` node:

| Parameter | Type | Description |
| -------- | --------- | ------------------ |
| Object | Container | Processing result of each image |

 Content of the `Object` node:

| Parameter | Type | Description |
| -------- | ------ | -------------------- |
| Key      | String | Filename               |
| Location | String | Image path |
| Format | String | Image format |
| Width    | Int    | Image width             |
| Height | Int | Image height |
| Size     | Int    | Image size             |
| Quality | Int | Image quality |
| ETag | String | ETag of the output image |

