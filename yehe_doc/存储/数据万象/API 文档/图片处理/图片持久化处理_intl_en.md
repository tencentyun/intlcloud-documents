## Processing upon Upload
The feature of processing upon upload provided by CI helps you implement image processing when uploading an image. You only need to add Pic-Operations to the request header and set related parameters to implement image processing when uploading an image, and store the input image and processing result in COS. Currently, this feature supports the processing of a file up to 20 MB.

### Request syntax

The image upload request is consistent with that of the simple upload API of COS V5, except that image processing parameters are added to the request header.

```shell
PUT /<ObjectKey> HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
Pic-Operations: <PicOperations>
```

>?
>- For more information about the simple upload API of COS, please see [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749).
>- Authorization: Auth String (For more information, please see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).)
>- The QPS for persistent processing is limited to 100. If you need a higher QPS, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).

### Request content

Pic-Operations is a string in JSON format. Related parameters are described as follows:

| Parameter | Type | Required | Description |
| ----------- | ----- | ---- | -------------------------------------- |
| is_pic_info | Int | No | Whether to return the input image information. 0: not return; 1: return. The default value is 0. |
| rules | Array | No | Processing rules. A rule corresponds to a processing result (currently, up to five rules are supported). If this parameter is not specified, image processing is not performed. |

 Parameters in `rules` (a JSON array) are described as follows:

| Parameter | Type | Required | Description |
| ------ | ------ | ---- | ---------------------------------------- |
| bucket | String | No | Name of the destination bucket to store the result, formatted as `BucketName-APPID`. If this parameter is not specified, the result is stored in the current bucket by default. |
| fileid | String | Yes | Path of the file that contains the processing result. If the path starts with `/`, the result is stored in the specified folder; otherwise, the result is stored in the same directory as the input image file. |
| rule | String | Yes | The processing parameter. For more information, please see the image processing API of CI. If the image needs to be stylized, prefix `style/` to the style name. For example, if the style name is `test`, you can set this parameter to `style/test`. |

### Response content
The response content is described as follows:

| Parameter | Type | Description |
| ---------------- | --------- | ---- |
| UploadResult | Container | Original image information |

 The content of the UploadResult node:

| Parameter | Type | Description |
| -------------- | --------- | ------ |
| OriginalInfo | Container | Original image information |
| ProcessResults | Container | Image processing result |

 The content of the OriginalInfo node:

| Node Name | Type | Description |
| --------- | --------- | ------ |
| Key | String | Name of the input image file |
| Location | String | Path of the image file |
| ImageInfo | Container | Original image information |
| ETag | String | ETag of the input image. If the input image is overwritten, this value is the ETag of the output image. |

 The content of the ImageInfo node:

| Node Name | Type | Description |
| ----------- | ------ | ------ |
| Format | String | Format |
| Width | Int | Image width |
| Height | Int | Image height |
| Quality | Int | Image quality |
| Ave | String | Image average hue |
| Orientation | Int | Image orientation |

 The content of the ProcessResults node:

| Node Name | Type | Description |
| ------ | --------- | --------- |
| Object | Container | Each image processing result |

 The content of the Object node:

| Node Name | Type | Description |
| -------- | ------ | ---- |
| Key | String | File name |
| Location | String | Path of the image file |
| Format | String | Image format |
| Width | Int | Image width |
| Height | Int | Image height |
| Size | Int | Image size |
| Quality | Int | Image quality |
| ETag | String | ETag of the output image |

### Sample
#### Request

```shell
PUT /filename.jpg HTTP/1.1
Host: examplebucket-1250000000.cos.ap-chengdu.myqcloud.com
Date: Wed, 28 Oct 2015 20:32:00 GMT
Authorization:XXXXXXXXXXXX
Pic-Operations: {"is_pic_info":1,"rules":[{"fileid":"test.jpg","rule":"imageView2/format/png"}]}
Content-Length: 64

[Object]
```

#### Response
```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 645
Date: Tue, 03 Apr 2018 09:06:16 GMT
Status: 200 OK
x-cos-request-id: NWFjMzQ0MDZfOTBmYTUwXzZkZV8z****


<UploadResult>
		<OriginalInfo>
			<Key>filename.jpg</Key>
			<Location>examplebucket-1250000000.cos.ap-chengdu.myqcloud.com/filename.jpg</Location>
			<ETag>&quot;580cd6930444576523c25f86ce2af9b1fc2d5484&quot;</ETag>
			<ImageInfo>
				<Format>JPEG</Format>
				<Width>640</Width>
				<Height>427</Height>
				<Quality>100</Quality>
				<Ave>0xa18454</Ave>
				<Orientation>1</Orientation>
			</ImageInfo>
		</OriginalInfo>
		<ProcessResults>
			<Object>
				<Key>test.jpg</Key>
				<Location>examplebucket-1250000000.cos.ap-chengdu.myqcloud.com/test.jpg</Location>
				<Format>png</Format>
				<Width>640</Width>
				<Height>427</Height>
				<Size>463092</Size>
				<Quality>100</Quality>
				<ETag>&quot;eaa4e3d8fd498bbc63be3b71c46b9c61f23e3f0c&quot;</ETag>
			</Object>
		</ProcessResults>
</UploadResult>
```

>!Processing upon upload supports the multipart upload feature of COS V5. To process images upon upload, add ` Pic-Operations` in the request header when you call the [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742) API.


```shell
POST /<ObjectKey>?uploadId=UploadId HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Content-length: Size
Authorization: Auth String
Pic-Operations: <PicOperations>
```

>?For more information about this COS API, please see [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742).


## Cloud Data Processing

The image processing APIs of CI allow you to process images that are already stored in COS and save the results to COS.

### Request syntax
```shell
POST /<ObjectKey>?image_process HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Content-length: Size
Authorization: Auth String
Pic-Operations: <PicOperations>
```

### Request content
Pic-Operations is a string in JSON format. Related parameters are described as follows:

| Parameter | Type | Required | Description |
| ----------- | ----- | ---- | -------------------------------------- |
| is_pic_info | Int | No | Whether to return the input image information. 0: not return; 1: return. The default value is 0. |
| rules | Array | No | Processing rules. A rule corresponds to a processing result (currently, up to five rules are supported). If this parameter is not specified, image processing is not performed. |

 Parameters in `rules` (a JSON array) are described as follows:

| Parameter | Type | Required | Description |
| ------ | ------ | ---- | ---------------------------------------- |
| bucket | String | No | Name of the destination bucket to store the result, formatted as `BucketName-APPID`. If this parameter is not specified, the result is stored in the current bucket by default. |
| fileid | String | Yes | Path of the file that contains the processing result. If the path starts with `/`, the result is stored in the specified folder; otherwise, the result is stored in the same directory as the input image file. |
| rule | String | Yes | The processing parameter. For more information, please see the image processing API of CI. If the image needs to be stylized, prefix `style/` to the style name. For example, if the style name is `test`, you can set this parameter to `style/test`. |

### Response content
The response content is described as follows:

| Parameter | Type | Description |
| ---------------- | --------- | ---- |
| UploadResult | Container | Original image information |

 The content of the UploadResult node:

| Parameter | Type | Description |
| -------------- | --------- | ------ |
| OriginalInfo | Container | Original image information |
| ProcessResults | Container | Image processing result |

 The content of the OriginalInfo node:

| Node Name | Type | Description |
| --------- | --------- | ------ |
| Key | String | Name of the input image file |
| Location | String | Path of the image file |
| ImageInfo | Container | Original image information |
| ETag | String | ETag of the input image. If the input image is overwritten, this value is the ETag of the output image. |

 The content of the ImageInfo node:

| Node Name | Type | Description |
| ----------- | ------ | ------ |
| Format | String | Format |
| Width | Int | Image width |
| Height | Int | Image height |
| Quality | Int | Image quality |
| Ave | String | Image average hue |
| Orientation | Int | Image orientation |

 The content of the ProcessResults node:

| Node Name | Type | Description |
| ------ | --------- | --------- |
| Object | Container | Each image processing result |

 The content of the Object node:

| Node Name | Type | Description |
| -------- | ------ | ---- |
| Key | String | File name |
| Location | String | Path of the image file |
| Format | String | Image format |
| Width | Int | Image width |
| Height | Int | Image height |
| Size | Int | Image size |
| Quality | Int | Image quality |
| ETag | String | ETag of the output image |

### Sample

#### Request

 ```shell
POST /filename.jpg?image_process HTTP/1.1
Host: examplebucket-1250000000.cos.ap-chengdu.myqcloud.com
Date: Wed, 18 Jan 2017 16:17:03 GMT
Authorization: XXXXXXXXXX
Pic-Operations: {"is_pic_info":1,"rules":[{"fileid":"test.jpg","rule":"imageView2/format/png"}]}
Content-Length: XX
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 645
Date: Tue, 03 Apr 2018 09:06:16 GMT
Status: 200 OK
x-cos-request-id: NWFjMzQ0MDZfOTBmYTUwXzZkZV8z****



<UploadResult>
			<OriginalInfo>
				<Key>filename.jpg</Key>
				<Location>examplebucket-1250000000.cos.ap-chengdu.myqcloud.com/filename.jpg</Location>
				<ETag>&quot;eaa4e3d8fd498bbc63be3b71c46b9c61f23e3f0c&quot;</ETag>
				<ImageInfo>
					<Format>JPEG</Format>
					<Width>640</Width>
					<Height>427</Height>
					<Quality>100</Quality>
					<Ave>0xa18454</Ave>
					<Orientation>1</Orientation>
				</ImageInfo>
			</OriginalInfo>
			<ProcessResults>
				<Object>
					<Key>test.jpg</Key>
					<Location>examplebucket-1250000000.cos.ap-chengdu.myqcloud.com/test.jpg</Location>
					<Format>png</Format>
					<Width>640</Width>
					<Height>427</Height>
					<Size>463092</Size>
					<Quality>100</Quality>
					<ETag>&quot;eaa4e3d8fd498bbc63be3b71c46b9c61f23e3f0c&quot;</ETag>
				</Object>
			</ProcessResults>
</UploadResult>
```
