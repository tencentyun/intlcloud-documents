## Processed During Uploading
The Processed During Uploading feature provided by the CI service helps you process images when you upload them. You can implement image processing during image uploading simply by adding the Pic-Operations option to the request packet header and setting the corresponding parameters. You can also store the original images and processing results to the COS. Currently, processing is only supported for files smaller than 20 MB.

### Request syntax

The request packet for uploading an image is the same as that of the API for simply uploading a COS V5 file. The only difference is that image processing parameters are added to the request packet header.

```shell
PUT /<ObjectKey> HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
Pic-Operations: <PicOperations>
```

>
>- API for simply uploading a COS file. For more information, see COS [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749).
> Authorization: Auth String. For more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).
>- The QPS for persistency is limited to 100. For if you require a higher QPS, [submit a ticket](https://console.cloud.tencent.com/workorder/category).

### Request content

Pic-Operations is a string of the json format. The parameters are as follows:

| Parameter Name | Type | Required | Description |
| ----------- | ----- | ---- | -------------------------------------- |
| is_pic_info | Int | No | Indicates whether to return original image information. The value 0 indicates original image information will not be returned. The value 1 indicates original image information will be returned. The default value is 0. |
| rules | Array | No | Indicates processing rules. Each rule is mapped to one processing result, and five rules are supported currently. If this parameter is not set, no image will be processed. |

 The parameters in rules (a json array) are as follows:

| Parameter Name | Type | Required | Description |
| ------ | ------ | ---- | ---------------------------------------- |
| bucket | String | No | Indicates the name of the destination bucket that is used to store the results. The value is in the format of BucketName-APPID. If this parameter is not set, the results will be stored to the current bucket. |
| fileid | String | Yes | Indicates the path name of the processing result file. If the path starts with `/`, the file will be stored to a specified folder. If not, the file will be stored to the directory that stores the original image file. |
| rule | String | Yes | Indicates the processing parameter. For more information, see the API for processing CI images. If you want to process images based on a specified style, the value must start with `style/`, followed by the style name. For example, if the style name is `test`, the value of the rule parameter is `style/test`. |

### Response content
The response packet body is as follows:

| Parameter Name | Type | Description |
| ---------------- | --------- | ---- |
| UploadResult | Container | Original image information |

 The content of the UploadResult node is as follows:

| Parameter Name | Type | Description |
| -------------- | --------- | ------ |
| OriginalInfo | Container | Original image information |
| ProcessResults | Container | Image processing result |

 The content of the OriginalInfo node is as follows:

| Parameter Name | Type | Description |
| --------- | --------- | ------ |
| Key | String | Name of the original image file |
| Location | String | Image path |
| ImageInfo | Container | Original image information |

 The content of the ImageInfo node is as follows:

| Parameter Name | Type | Description |
| ----------- | ------ | ------ |
| Format | String | Format |
| Width | Int | Image width |
| Height | Int | Image height |
| Quality | Int | Image quality |
| Ave | String | Average hue of an image |
| Orientation | Int | Image rotation angle |

 The content of the ProcessResults node is as follows:

| Parameter Name | Type | Description |
| ------ | --------- | --------- |
| Object | Container | Processing result of each image |

 The content of the Object node is as follows:

| Parameter Name | Type | Description |
| -------- | ------ | ---- |
| Key | String | File name |
| Location | String | Image path |
| Format | String | Image format |
| Width | Int | Image width |
| Height | Int | Image height |
| Size | Int | Image size |
| Quality | Int | Image quality |


### Example
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

>The Processed During Uploading feature supports multipart uploading of COS V5 files. When you use the [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742) API, you only need to add the Pic-Operations option to the request packet header for image processing.


```shell
POST /<ObjectKey>uploadId=UploadId HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Content-length: Size
Authorization: Auth String
Pic-Operations: <PicOperations>
```

> For more information on the COS API, see COS [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742).


## Processing Cloud Data

The image processing API provided by the CI service is used to process images that are stored in COS and to store the processing results to the COS.

### Request syntax
```shell
POST /<ObjectKey>image_process HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Content-length: Size
Authorization: Auth String
Pic-Operations: <PicOperations>
```

### Request content
Pic-Operations is a string of the json format. The parameters are as follows:

| Parameter Name | Type | Required | Description |
| ----------- | ----- | ---- | -------------------------------------- |
| is_pic_info | Int | No | Indicates whether to return the original image information. The value 0 indicates the original image information will not be returned. The value 1 indicates the original image information will be returned. The default value is 0. |
| rules | Array | No | Indicates processing rules. Each rule is mapped to one processing result, and five rules are currently supported. If this parameter is not set, no image will be processed. |

 The parameters in rules (a json array) are as follows:

| Parameter Name | Type | Required | Description |
| ------ | ------ | ---- | ---------------------------------------- |
| bucket | String | No | Indicates the name of the destination bucket that is used to store the results. The value is in the format of BucketName-APPID. If this parameter is not set, the results will be stored to the current bucket. |
| fileid | String | Yes | Indicates the path name of the processing result file. If the path starts with `/`, the file will be stored to a specified folder. If not, the file will be stored to the directory that stores the original image file. |
| rule | String | Yes | Indicates the processing parameter. For more information, see the API for processing CI images. If you want to process images based on a specified style, the value must start with `style/`, followed by the style name. For example, if the style name is `test`, the rule field is `style/test`. |

### Response content
The response packet body is as follows:

| Parameter Name | Type | Description |
| ---------------- | --------- | ---- |
| UploadResult | Container | Original image information |

 The content of the UploadResult node is as follows:

| Parameter Name | Type | Description |
| -------------- | --------- | ------ |
| OriginalInfo | Container | Original image information |
| ProcessResults | Container | Image processing result |

 The content of the OriginalInfo node is as follows:

| Parameter Name | Type | Description |
| --------- | --------- | ------ |
| Key | String | Name of the original image file |
| Location | String | Image path |
| ImageInfo | Container | Original image information |

 The content of the ImageInfo node is as follows:

| Parameter Name | Type | Description |
| ----------- | ------ | ------ |
| Format | String | Format |
| Width | Int | Image width |
| Height | Int | Image height |
| Quality | Int | Image quality |
| Ave | String | Average hue of an image |
| Orientation | Int | Image rotation angle |

 The content of the ProcessResults node is as follows:

| Parameter Name | Type | Description |
| ------ | --------- | --------- |
| Object | Container | Processing result of each image |

 The content of the Object node is as follows:

| Parameter Name | Type | Description |
| -------- | ------ | ---- |
| Key | String | File name |
| Location | String | Image path |
| Format | String | Image format |
| Width | Int | Image width |
| Height | Int | Image height |
| Size | Int | Image size |
| Quality | Int | Image quality |


### Example

#### Request

 ```shell
POST /filename.jpg?image_process HTTP/1.1
Host: examplebucket-1250000000.cos.ap-chengdu.myqcloud.com
Date: Wed，18 Jan 2017 16:17:03 GMT
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
