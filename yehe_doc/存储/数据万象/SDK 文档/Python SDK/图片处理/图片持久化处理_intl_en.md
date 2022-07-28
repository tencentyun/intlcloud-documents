## Overview

This document provides an overview of APIs and SDK code samples for persistent image processing.

| API | Description    |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [Persistent image processing](https://intl.cloud.tencent.com/document/product/436/40592) | Processes an image during upload, or processes an image stored in COS and saves the processing result to COS. |

## Processing During Upload

#### Feature description

CI allows you to process images during upload. To enable this, add `Pic-Operations` to the request header and set relevant parameters. You can also save the input images and processing results to COS. Currently, images within 20 MB can be processed.

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
    ACL='private'|'public-read',  # Note that the maximum number of allowed ACLs (1,000) may be reached if you use this parameter.
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
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Body               | Content of the uploaded object, which can be a file stream or a byte stream.                         | file/bytes | Yes       |
| Key  | Unique identifier of the object in the bucket. For example, if an object's access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its key is `doc/pic.jpg`. | String  |   Yes |
| PicOperations      | CI image processing parameters. For more information, see [Persistent Image Processing](https://intl.cloud.tencent.com/document/product/436/40592). | String     | Yes       |
| EnableMD5 | Specifies whether the SDK needs to calculate the `Content-MD5` checksum. It is disabled by default. The upload will take longer if it is enabled. | Bool | No |
| ACL | Sets the object ACL, such as `private` or `public-read`.                | String     | No |
| GrantFullControl | Grants the grantee full permission in the format of `id="OwnerUin"` | String | No |
| GrantRead  | Grants the grantee read permission in the format of `id="OwnerUin"`                 | String     | No |
| StorageClass | Storage class of the object, such as `STANDARD` (default), `STANDARD_IA`, and `ARCHIVE`. For more information, see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/436/30925). | String     | No |
| Expires            | Sets `Expires`.                                                 | String     | No  |
| CacheControl | Cache policy. Sets `Cache-Control`. | String | No |
| ContentType | Content type. `Sets Content-Type`. | String | No |
| ContentDisposition | Object name. Sets `Content-Disposition`. | String | No |
| ContentEncoding | Encoding format. Sets `Content-Encoding`. | String | No |
| ContentLanguage  | Language type. Sets `Content-Language`. |  String |  No |
| ContentLength | Sets the length of the request content. | String | No |
| ContentMD5 | Sets the MD5 checksum of the uploaded object for verification. | String | No |
| Metadata           | User-defined object metadata. It must start with `x-cos-meta`; otherwise, it will be ignored. | Dict       | No       |
|  TrafficLimit | Bandwidth limit for a single request in bit/s. Value range: 819200-838860800, i.e., 100 KB/s–100 MB/s. | String |  No |

`PicOperations` is a JSON string. Its parameters are as follows:

| Parameter | Description | Type | Required |
| ----------- | ------------------------------------------------------------ | ----- | -------- |
| is_pic_info | Whether to return the input image information <br>0 (default): no <br>1: yes    | Int   | No       |
| rules       |  Processing rules (up to five rules are supported). Each rule corresponds to one processing result. If this parameter is not specified, images will not be processed. | Array | No   |

 Parameters of `rules` (a JSON array) are as follows:

| Parameter | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ------ | -------- |
| bucket   | Name of the destination bucket to store the results in the format of `BucketName-APPID`. If this parameter is not specified, the results will be stored in the current bucket by default. | String | No       |
| fileid    | Path of the processing result file. If the path starts with `/`, the result file will be stored in the specified folder; otherwise, it will be stored in the same directory as the input image file. | String | Yes |
| rule | Processing parameters. For more information, see CI's image processing API. To process an image by using a specified style, the value must start with `style/`, with the style name followed. For example, if the style name is `test`, the value of `rule` should be `style/test`. | String | Yes |

#### Response description

The response contains the input image and processing information in `dict` type:

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

The response body is as described below:

| Parameter | Type | Description |
| ------------ | --------- | -------- |
| UploadResult | Container | Input image information |

 Content of `UploadResult`:

| Parameter | Type | Description |
| -------------- | --------- | ------------ |
| OriginalInfo | Container | Input image information |
| ProcessResults | Container | Image processing result |

 Content of `OriginalInfo`:

| Parameter | Type | Description |
| --------- | --------- | ---------------------------------------------------------- |
| Key       | String    | Input image filename                                                |
| Location  | String    | Image path                                                   |
| ImageInfo | Container | Input image information |
| ETag      | String    | `ETag` of the input image. If the output image overwrites the input image, the value of `ETag` will be that of the output image. |

 Content of `ImageInfo`:

| Parameter | Type | Description |
| ----------- | ------ | ------------ |
| Format | String | Format |
| Width | Int | Image width |
| Height | Int | Image height |
| Quality | Int | Image quality |
| Ave | String | Image average hue |
| Orientation | Int | Image rotation angle |

 Content of `ProcessResults`:

| Parameter | Type | Description |
| -------- | --------- | ------------------ |
| Object | Container | Processing result of each image |

 Content of `Object`:

| Parameter | Type | Description |
| -------- | ------ | -------------------- |
| Key      | String | Filename               |
| Location | String | Image path |
| Format | String | Image format |
| Width    | Int    | Image width             |
| Height | Int | Image height |
| Size     | Int    | Image size             |
| Quality | Int | Image quality |
| ETag | String | `ETag` of the output image |

## Processing In-Cloud Data

#### Feature description

The persistent image processing API can process an image stored in COS and save the processing result to COS.

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
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Key  | Unique identifier of the object in the bucket. For example, if an object's access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its key is `doc/pic.jpg`. | String  |   Yes |
| PicOperations      | CI image processing parameters. For more information, see [Persistent Image Processing](https://intl.cloud.tencent.com/document/product/436/40592). | String     | Yes       |

`PicOperations` is a JSON string. Its parameters are as follows:

| Parameter | Description | Type | Required |
| ----------- | ------------------------------------------------------------ | ----- | -------- |
| is_pic_info | Whether to return the input image information <br>0 (default): no <br>1: yes    | Int   | No       |
| rules       |  Processing rules (up to five rules are supported). Each rule corresponds to one processing result. If this parameter is not specified, images will not be processed. | Array | No   |

 Parameters of `rules` (a JSON array) are as follows:

| Parameter | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ------ | -------- |
| bucket   | Name of the destination bucket to store the results in the format of `BucketName-APPID`. If this parameter is not specified, the results will be stored in the current bucket by default. | String | No       |
| fileid    | Path of the processing result file. If the path starts with `/`, the result file will be stored in the specified folder; otherwise, it will be stored in the same directory as the input image file. | String | Yes |
| rule | Processing parameters. For more information, see the image processing API. To process an image by using a specified style, the value must start with `style/` with the style name followed. For example, if the style name is `test`, the value of `rule` should be `style/test`. | String | Yes | 

#### Response description

The response contains object metadata in `dict` type:

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

The response body is as described below:

| Parameter | Type | Description |
| ------------ | --------- | -------- |
| UploadResult | Container | Input image information |

 Content of `UploadResult`:

| Parameter | Type | Description |
| -------------- | --------- | ------------ |
| OriginalInfo | Container | Input image information |
| ProcessResults | Container | Image processing result |

 Content of `OriginalInfo`:

| Parameter | Type | Description |
| --------- | --------- | ---------------------------------------------------------- |
| Key       | String    | Input image filename                                                |
| Location  | String    | Image path                                                   |
| ImageInfo | Container | Input image information |
| ETag      | String    | `ETag` of the input image. If the output image overwrites the input image, the value of `ETag` will be that of the output image. |

 Content of `ImageInfo`:

| Parameter | Type | Description |
| ----------- | ------ | ------------ |
| Format | String | Format |
| Width | Int | Image width |
| Height | Int | Image height |
| Quality | Int | Image quality |
| Ave | String | Image average hue |
| Orientation | Int | Image rotation angle |

 Content of `ProcessResults`:

| Parameter | Type | Description |
| -------- | --------- | ------------------ |
| Object | Container | Processing result of each image |

 Content of `Object`:

| Parameter | Type | Description |
| -------- | ------ | -------------------- |
| Key      | String | Filename               |
| Location | String | Image path |
| Format | String | Image format |
| Width    | Int    | Image width             |
| Height | Int | Image height |
| Size     | Int    | Image size             |
| Quality | Int | Image quality |
| ETag | String | `ETag` of the output image |

