## Processing upon Upload
The feature of processing upon upload provided by CI helps you implement image processing when uploading an image. You only need to add Pic-Operations to the request header and set related parameters to implement image processing when uploading an image, and store the original image and processing result in COS. Currently, this feature supports the processing of a file up to 20 MB in size.

### Request syntax
The image upload request is consistent with that of the simple upload API of COS V5, except that image processing parameters are added to the request header.

```
PUT /<ObjectKey> HTTP/1.1
Host: <BucketName-APPID>.pic.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
Pic-Operations: <PicOperations>
```

>
- For more information about the simple upload API of COS, see [COS Documentation](https://intl.cloud.tencent.com/document/product/436/7749).
- Authorization: Auth String (For more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778)).

### Request content
Pic-Operations is a string in JSON format. Related parameters are described as follows:

| Parameter Name | Type | Required | Description |
| ----------- | ----- | ---- | -------------------------------------- |
| is_pic_info | Int | No | Whether to return the original image information. 0: The original image information is not returned. 1: The original image information is returned. The default value is 0. |
| rules | Array | No | Processing rules. A rule corresponds to a processing result (currently, up to five rules are supported.) If this parameter is not specified, image processing is not performed. |

 Parameters in rules (a JSON array) are described as follows:

| Parameter Name | Type | Required | Description |
| ------ | ------ | ---- | ---------------------------------------- |
| bucket | String | No | The name of the destination bucket where the result is stored. The format is bucketName-appid. If this parameter is not specified, the result is saved in the current bucket by default. |
| fileid | String | Yes | The path of the file that stores the processing result. If the path starts with **/**, the result is stored in the specified folder; otherwise, the result is stored in the same directory as the original image file. |
| rule | String | Yes | The processing parameter. For more information, see the image processing API of CI. If the image needs to be processed according to the specified style, this parameter starts with **style/**, followed by a style name. For example, if the style name is **test**, the value of this parameter is **style/test**. |

### Response content
The response content is described as follows:

| Parameter Name | Type | Description |
| ---------------- | --------- | ---- |
| UploadResult | Container | Original image information |

 The content of the UploadResult node:

| Parameter Name | Type | Description |
| -------------- | --------- | ------ |
| OriginalInfo | Container | Original image information |
| ProcessResults | Container | Image processing result |

 The content of the OriginalInfo node:

| Node Name | Type | Description |
| --------- | --------- | ------ |
| Key | String | Name of the original image file  |
| Location | String | Path of the image file |
| ImageInfo | Container | Original image information |

 The content of the ImageInfo node:

| Node Name | Type | Description |
| ----------- | ------ | ------ |
| Format | String | Format |
| Width | Int | Image width |
| Height | Int | Image height |
| Quality | Int | Image quality |
| Ave | String | Image average |
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


### Sample
#### Request

```
PUT /filename.jpg HTTP/1.1
Host: examplebucket-1250000000.pic.ap-chengdu.myqcloud.com
Date: Wed, 28 Oct 2015 20:32:00 GMT
Authorization:XXXXXXXXXXXX
Pic-Operations: {"is_pic_info":1,"rules":[{"fileid":"test.jpg","rule":"imageView2/format/png"}]}
Content-Length: 64

[Object]
```

#### Response
```
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 645
Date: Tue, 03 Apr 2018 09:06:16 GMT
Status: 200 OK
x-cos-request-id: NWFjMzQ0MDZfOTBmYTUwXzZkZV8zMQ==

<UploadResult>
<OriginalInfo>
<Key>filename.jpg</Key>
<Location>examplebucket-1250000000.cos.ap-chengdu.myqcloud.com/filename.jpg</Location>
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
</Object>
</ProcessResults>
</UploadResult>
```

> The feature of processing upon upload supports multipart upload of COS V5. When you are using the Complete Multipart Upload API of COS V5, you only need to add Pic-Operations to the request header to realize image processing.


```
POST /<ObjectKey>uploadId=UploadId HTTP/1.1
Host: <BucketName-APPID>.pic.<Region>.myqcloud.com
Date: GMT Date
Content-length: Size
Authorization: Auth String
Pic-Operations: <PicOperations>
```

For more information about COS APIs, see [COS Documentation](https://intl.cloud.tencent.com/document/product/436/7749).

## Cloud Data Processing
The image processing APIs of CI allow you to process images that are already stored in COS and save the results to COS.

### Request syntax
```
POST /<ObjectKey>image_process HTTP/1.1
Host: <BucketName>-<APPID>.pic.<Region>.myqcloud.com
Date: GMT Date
Content-length: Size
Authorization: Auth String
Pic-Operations: <PicOperations>
```

### Request content
Pic-Operations is a string in JSON format. Related parameters are described as follows:

| Parameter Name | Type | Required | Description |
| ----------- | ----- | ---- | -------------------------------------- |
| is_pic_info | Int | No | Whether to return the original image information. 0: The original image information is not returned. 1: The original image information is returned. The default value is 0. |
| rules | Array | No | Processing rules. A rule corresponds to a processing result (currently, up to five rules are supported.) If this parameter is not specified, image processing is not performed. |

 Parameters in rules (a JSON array) are described as follows:

| Parameter Name | Type | Required | Description |
| ------ | ------ | ---- | ---------------------------------------- |
| bucket | String | No | The name of the target bucket where the result is stored. The format is bucketName-appid. If this parameter is not specified, the result is stored in the current bucket by default. |
| fileid | String | Yes | The path of the file that stores the processing result. If the path starts with **/**, the result is stored in the specified folder; otherwise, the result is stored in the same directory as the original image file. |
| rule | String | Yes | The processing parameter. For more information, see the image processing API of CI. If the image needs to be processed according to the specified style, this parameter starts with **style/**, followed by a style name. For example, if the style name is **test**, the value of this parameter is **style/test**. |

### Response content
The response content is described as follows:

| Parameter Name | Type | Description |
| ---------------- | --------- | ---- |
| UploadResult | Container | Original image information |

 The content of the UploadResult node:

| Parameter Name | Type | Description |
| -------------- | --------- | ------ |
| OriginalInfo | Container | Original image information |
| ProcessResults | Container | Image processing result |

 The content of the OriginalInfo node:

| Node Name | Type | Description |
| --------- | --------- | ------ |
| Key | String | Name of the original image file |
| Location | String | Path of the image file |
| ImageInfo | Container | Original image information |

 The content of the ImageInfo node:

| Node Name | Type | Description |
| ----------- | ------ | ------ |
| Format | String | Format |
| Width | Int | Image width |
| Height | Int | Image height |
| Quality | Int | Image quality |
| Ave | String | Image average |
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


### Sample
#### Request
 ```
POST /filename.jpg?image_process HTTP/1.1
Host: examplebucket-1250000000.pic.ap-chengdu.myqcloud.com
Date: Wed, 18 Jan 2017 16:17:03 GMT
Authorization: XXXXXXXXXX
Pic-Operations: {"is_pic_info":1,"rules":[{"fileid":"test.jpg","rule":"imageView2/format/png"}]}
Content-Length: XX
 ```

#### Response
```
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 645
Date: Tue, 03 Apr 2018 09:06:16 GMT
Status: 200 OK
x-cos-request-id: NWFjMzQ0MDZfOTBmYTUwXzZkZV8zMQ==

<UploadResult>
<OriginalInfo>
<Key>filename.jpg</Key>
<Location>examplebucket-1250000000.cos.ap-chengdu.myqcloud.com/filename.jpg</Location>
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
</Object>
</ProcessResults>
</UploadResult>
```