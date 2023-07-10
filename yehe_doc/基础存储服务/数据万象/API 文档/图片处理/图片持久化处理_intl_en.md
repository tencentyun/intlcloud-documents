## Processing During Upload
CI allows you to process images during upload. To enable this, add `Pic-Operations` to the request header and set relevant parameters. You can also save the input images and processing results to COS. Currently, images within 32 MB can be processed.

### Request syntax

The request during image upload is the same as that used to simply upload a file to COS v5, except that you need to add the image processing parameter to the request header.

```shell
PUT /<ObjectKey> HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
Pic-Operations: <PicOperations>
```

>?
> - For more information on COS' simple upload API, see [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749).
> - Authorization: Auth String (for more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778)).
> - When this feature is used by a sub-account, relevant permissions must be granted as instructed in [Authorization Granularity Details](https://intl.cloud.tencent.com/document/product/1045/49896).
> - The QPS for persistent processing can be up to 100. If you need a higher QPS, [contact us](https://intl.cloud.tencent.com/document/product/1045/42350).
>

### Request content

`Pic-Operations` is a JSON string. Its parameters are as follows:

| Parameter | Type | Required | Description |
| ----------- | ----- | ---- | -------------------------------------- |
| is_pic_info | Int   | No    | Whether to return the input image information. Valid values: `0` (no); `1` (yes). Default value: `0`.         |
| rules       | Array | No    | Processing rules (up to five rules are supported). Each rule corresponds to one processing result. If this parameter is not specified, images will not be processed. |

 Parameters of `rules` (a JSON array) are as follows:

| Parameter | Type | Required | Description |
| ------ | ------ | ---- | ---------------------------------------- |
| bucket | String | No   | Name of the destination bucket to store the results in the format of `BucketName-APPID`. If this parameter is not specified, the results will be stored in the current bucket by default. |
| fileid   | String | Yes       |    Storage path and name of the output file. <br>Naming rules are as follows (assume the input file is `/p1/test1.jpg`):<br>1. A value starting with a slash (/) indicates an absolute path. For example, if `fileid` is set to `/p2/test2.jpg`, the `test2.jpg` file will be stored in the `p2` folder. <br>2. A value not starting with a slash indicates a relative path. For example, if `fileid` is set to `p2/test2.jpg`, a folder named `p2` will be created in the `p1` folder, and the `test2.jpg` file will be stored in the `p2` folder.<br>3. Note: Do not end the value with a slash; otherwise, an empty filename will be generated.    |
| rule   | String | Yes    | Processing parameters. For more information, see CI's image processing API. To process an image by using a specified style, the value must start with `style/`, with the style name followed. For example, if the style name is `test`, the value of `rule` should be `style/test`. |

### Response content
The response body is as described below:

| Parameter | Type | Description |
| ---------------- | --------- | ---- |
| UploadResult | Container | Input image information |

 Content of `UploadResult`:

| Parameter | Type | Description |
| -------------- | --------- | ------ |
| OriginalInfo   | Container | Input image information   |
| ProcessResults | Container | Image processing result |

 Content of `OriginalInfo`:

| Node Name | Type | Description |
| --------- | --------- | ------ |
| Key       | String    | Input image name  |
| Location | String | Image path |
| ImageInfo | Container | Input image information |
| ETag      | String    | `ETag` of the input image. If the output image overwrites the input image, the value of `ETag` will be that of the output image. |

 Content of `ImageInfo`:

| Node Name | Type | Description |
| ----------- | ------ | ------ |
| Format      | String | Format     |
| Width       | Int    | Image width   |
| Height      | Int    | Image height   |
| Quality     | Int    | Image quality   |
| Ave         | String | Image average hue  |
| Orientation | Int | Image rotation angle |

 Content of `ProcessResults`:

| Node Name | Type | Description |
| ------ | --------- | --------- |
| Object | Container | Processing result of each image |

 Content of `Object`:

| Node Name | Type | Description |
| -------- | ------ | ---- |
| Key      | String | Filename |
| Location | String | Image path |
| Format   | String | Image format |
| Width    | Int    | Image width |
| Height      | Int    | Image height   |
| Size     | Int    | Image size |
| Quality     | Int    | Image quality   |
|  ETag      | String | `ETag` information of the output image |

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

>!Processing during upload is supported for the multipart upload feature of COS v5. To implement image processing, you only need to add the `Pic-Operations` parameter in the request header when calling the [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742) API.


```shell
POST /<ObjectKey>?uploadId=UploadId HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Content-length: Size
Authorization: Auth String
Pic-Operations: <PicOperations>
```

>?For more information, see [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742).


## Processing In-Cloud Data

CI's image processing API can process an image stored in COS and save the processing result to COS.

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
`Pic-Operations` is a JSON string. Its parameters are as follows:

| Parameter | Type | Required | Description |
| ----------- | ----- | ---- | -------------------------------------- |
| is_pic_info | Int   | No    | Whether to return the input image information. Valid values: `0` (no); `1` (yes). Default value: `0`.         |
| rules       | Array | No    | Processing rules (up to five rules are supported). Each rule corresponds to one processing result. If this parameter is not specified, images will not be processed. |

 Parameters of `rules` (a JSON array) are as follows:

| Parameter | Type | Required | Description |
| ------ | ------ | ---- | ---------------------------------------- |
| bucket | String | No   | Name of the destination bucket to store the results in the format of `BucketName-APPID`. If this parameter is not specified, the results will be stored in the current bucket by default. |
| fileid   | String | Yes       |    Storage path and name of the output file. <br>Naming rules are as follows (assume the input file is `/p1/test1.jpg`):<br>1. A value starting with a slash (/) indicates an absolute path. For example, if `fileid` is set to `/p2/test2.jpg`, the `test2.jpg` file will be stored in the `p2` folder. <br>2. A value not starting with a slash indicates a relative path. For example, if `fileid` is set to `p2/test2.jpg`, a folder named `p2` will be created in the `p1` folder, and the `test2.jpg` file will be stored in the `p2` folder.<br>3. Note: Do not end the value with a slash; otherwise, an empty filename will be generated.    |
| rule   | String | Yes    | Processing parameters. For more information, see [Basic Image Processing](https://www.tencentcloud.com/document/product/1045/33694). To process an image by using a specified style, the value must start with `style/`, with the style name followed. For example, if the style name is `test`, the value of `rule` should be `style/test`. |

### Response content
The response body is as described below:

| Parameter | Type | Description |
| ---------------- | --------- | ---- |
| UploadResult| Container | Input image information |

 Content of `UploadResult`:

| Parameter | Type | Description |
| -------------- | --------- | ------ |
| OriginalInfo   | Container | Input image information   |
| ProcessResults | Container | Image processing result |

 Content of `OriginalInfo`:

| Node Name | Type | Description |
| --------- | --------- | ------ |
| Key       | String    | Input image name  |
| Location | String | Image path |
| ImageInfo | Container | Input image information |
| ETag      | String    | `ETag` of the input image. If the output image overwrites the input image, the value of `ETag` will be that of the output image. |

 Content of `ImageInfo`:

| Node Name | Type | Description |
| ----------- | ------ | ------ |
| Format      | String | Format     |
| Width       | Int    | Image width   |
| Height      | Int    | Image height   |
| Quality     | Int    | Image quality   |
| Ave         | String | Image average hue  |
| Orientation | Int | Image rotation angle |

 Content of `ProcessResults`:

| Node Name | Type | Description |
| ------ | --------- | --------- |
| Object | Container | Processing result of each image |

 Content of `Object`:

| Node Name | Type | Description |
| -------- | ------ | ---- |
| Key      | String | Filename |
| Location | String | Image path |
| Format   | String | Image format |
| Width    | Int    | Image width |
| Height      | Int    | Image height   |
| Size     | Int    | Image size |
| Quality     | Int    | Image quality   |
| ETag | String | `ETag` of the output image |

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
