## Feature Description

Blind watermarking is a brand-new watermarking feature based on Tencent Cloud CI. It allows you to add a watermark to the input image information without displaying the watermark or significantly affecting the image quality. If you think your image might have been stolen, you can extract the blind watermark from the suspected image to check whether the image belongs to you.

You can call this API to:
<ul  style="margin: 0;">
	<li>Add a blind watermark to an image during upload.</li>
	<li>Add a blind watermark to an image during download.</li>
	<li>Add a blind watermark to an image stored in COS.</li>
</ul>
You can also extract a blind watermark (if any) from an image.


## Adding Blind Watermark

### Request 1: Adding a blind watermark during upload

The request for adding a blind watermark to an image during upload is the same as that in a [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) call, except that you need to add the image processing parameter `Pic-Operations` to the request header and use the blind watermark parameter.

#### Sample request

```shell
PUT /<ObjectKey> HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
Pic-Operations: <PicOperations>

[Object Content]
```

>?Authorization: Auth String (for more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778)).

#### Request headers

This API only uses common request headers. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

Add the image processing parameter `Pic-Operations` (a JSON string) to the request header. Its parameters are as follows:

| Parameter Name | Description | Type | Required | 
| ----------- | ----- | ---- | ------------------------------------------------------------ |
| is_pic_info | Whether to return the input image information. Valid values: `0` (no), `1` (yes). Default value: `0`. | Int   | No   |
| rules       |  Processing rules (up to five rules are supported). Each rule corresponds to one processing result. If this parameter is not specified, images will not be processed. |Array | No   |

Parameters of `rules` (a JSON array) are as follows:

| Parameter | Description | Type | Required | 
| -------- | ------ | ----- | ------------------------------------------------------------ |
| bucket   | Name of the destination bucket to store the results in the format of `BucketName-APPID`. If this parameter is not specified, the results will be stored in the current bucket by default. | String | No       |
| fileid   | Storage path and name of the output file. <br>Naming rules are as follows (assume the input file is `/p1/test1.jpg`):<br>1. A value starting with a slash (/) indicates an absolute path. For example, if `fileid` is set to `/p2/test2.jpg`, the `test2.jpg` file will be stored in the `p2` folder. <br>2. A value not starting with a slash indicates a relative path. For example, if `fileid` is set to `p2/test2.jpg`, a folder named `p2` will be created in the `p1` folder, and the `test2.jpg` file will be stored in the `p2` folder.<br>3. Note: Do not end the value with a slash; otherwise, an empty filename will be generated.    | String | Yes |
| rule | Processing parameters. For more information, see the image processing API. To process an image by using a specified style, the value must start with `style/`, with the style name followed. For example, if the style name is `test`, the value of `rule` should be `style/test`. | String | Yes |

To use blind watermarking, add the watermarking parameter `watermark` to `rule` as follows:

```shell
watermark/3/type/<type>/image/<imageUrl>/text/<text>/level/<level>
```

The parameters are as follows:

| Parameter | Description | Type | Required |
| ----- | ------ | ---- | ------------------------------------------------------------ |
| type         | Blind watermark type. Valid values: `1` (semi-blind watermark), `2` (blind watermark), `3` (text blind watermark). | Int    | Yes |
| image | URL of the blind watermark image, which must be URL-safe Base64-encoded. This parameter is required if `type` is set to `1` or `2` and does not take effect if `type` is set to `3`. The image watermark must: <br>1. Be stored in the same bucket as the input image. <br>2. Have a URL that starts with `http://`. Note that "http://" cannot be omitted or changed to "https://". For example, the following watermark URLs are invalid: <li> examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/watermark.png <li>https://examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/watermark.png | String | No  |
| text  | Blind watermark text, which must be URL-safe Base64-encoded. This parameter is required if `type` is set to `3` and does not take effect if `type` is set to `1` or `2`. | String |  No  |
| level    | Blind watermark level, which only takes effect if `type` is set to `2`. Valid values: `1` (default value), `2`, `3`. The larger the value, the better the blind watermarking effect. | Int  |  No |


#### Request parameters

This API has no request parameters.


#### Request body

The request body of this API is the content of the input image.



### Response

#### Response headers

This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).


#### Response body

Parameters in the response body are as follows:

| Parameter | Description | Type |
| ------------------------- | ------------------ | --------- |
| UploadResult              | Input image information | Container |

Content of `UploadResult`: 

| Parameter | Description | Type |
| ------------------------- | ------------------ | --------- |
| OriginalInfo              | Input image information     | Container |
| ProcessResults            | Image processing result    | Container |

Content of `OriginalInfo`: 

| Node Name | Description | Type |
| ------------------------- | ------------------ | --------- |
| Key     | Input image name     | String    |
| Location | Image path | String    |
| ImageInfo                 | Input image information       | Container |

Content of `ImageInfo`: 

| Node Name | Description | Type |
| ------------------------- | ------------------ | --------- |
| Format                    | Format  | String    |
| Width                     | Image width      | Int       |
| Height                    | Image height       | Int       |
| Quality                   | Image quality         | Int       |
| Ave                       | Image average hue    | String    |
| Orientation               | Image rotation angle | Int       |

Content of `ProcessResults`:

| Node Name | Description | Type |
| ------------------------- | ------------------ | --------- |
| Object                    | Processing result of each image | Container |

Content of `Object`:

| Node Name | Description | Type |
| ------------------------- | ------------------ | --------- |
| Key  | Filename | String  |
| Location | Image path | String    |
| Format  | Image format  | String  |
| Width                     | Image width      | Int       |
| Height                    | Image height       | Int       |
| Size                      | Image size   | Int       |
| Quality                   | Image quality         | Int       |




### Samples

#### Request

```shell
PUT /exampleobject HTTP/1.1
Host: examplebucket-1250000000.cos.ap-chengdu.myqcloud.com
Date: Tue, 03 Apr 2018 09:06:15 GMT
Authorization:XXXXXXXXXXXX

Pic-Operations:
{
    "is_pic_info": 1,
    "rules": [{
        "fileid": "exampleobject",
        "rule": "watermark/3/type/1/image/aHR0cDovL2V4YW1wbGVzLTEyNTEwMDAwMDQucGljc2gubXlxY2xvdWQuY29tL3NodWl5aW4uanBn"
    }]
}
Content-Length: 64

[Object Content]
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
              <Key>exampleobject</Key>
              <Location>examplebucket-1250000000.cos.ap-chengdu.myqcloud.com/exampleobject</Location>
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
                   <Key>exampleobject</Key>
                   <Location>examplebucket-1250000000.cos.ap-chengdu.myqcloud.com/exampleobject</Location>
                   <Format>png</Format>
                   <Width>640</Width>
                   <Height>427</Height>
                   <Size>463092</Size>
                   <Quality>100</Quality>
              </Object>
          </ProcessResults>
</UploadResult>
```

>!
>- The [Object Content] field in the request body is the binary string of the input image, and `imageUrl` in `rule` in the request header `Pic-Operations` is the URL of the watermark image.
>- The `Location` field in `ProcessResults` in the response body is the URL of the image with a blind watermark.


### Request 2: Adding a blind watermark during download

You can add a blind watermark during download in the same way as adding a regular watermark, except that you need to add the `watermark` parameter after the image URL.

#### Sample request

```plaintext
GET /<ObjectKey>?watermark/3/type/<type>/image/<imageUrl>/text/<text> HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: <GMT Date>
Authorization: <Auth String>
```


#### Request parameters

The request parameters are as follows:

| Parameter | Description | Type | Required |
| ------------ | ------------------------------------------------------------ | ------ | -------- |
| download_url | File URL in the format of http(s)://`<BucketName-APPID>.cos.<Region>.myqcloud.com/<picture name>`, such as `examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/picture.jpeg`. | String       | Yes         |
| type         | Blind watermark type. Valid values: `1` (semi-blind watermark), `2` (blind watermark), `3` (text blind watermark). | Int    | Yes |
| image | URL of the blind watermark image, which must be URL-safe Base64-encoded. This parameter is required if `type` is set to `1` or `2` and does not take effect if `type` is set to `3`. The image watermark must: <br>1. Be stored in the same bucket as the input image. <br>2. Have a URL that starts with `http://`. Note that "http://" cannot be omitted or changed to "https://". For example, the following watermark URLs are invalid: <li> examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/watermark.png <li>https://examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/watermark.png | String | No  |
| text  | Blind watermark text, which must be URL-safe Base64-encoded. This parameter is required if `type` is set to `3` and does not take effect if `type` is set to `1` or `2`. | String |  No  |
| level    | Blind watermark level, which only takes effect if `type` is set to `2`. Valid values: `1` (default value), `2`, `3`. The larger the value, the better the blind watermarking effect. | Int  |  No |

### Samples

```shell
https://examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/sample.jpeg?watermark/3/type/3/text/dGVuY2VudCBjbG91ZA==
```

### Request 3: Adding a blind watermark to an image stored in COS

You can call this API to add a blind watermark to an image stored in COS and save the result to COS.

#### Sample request

```shell
POST /<ObjectKey>?image_process HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
Pic-Operations: <PicOperations>
```

>?Authorization: Auth String (for more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778)).

#### Request headers

This API only uses common request headers. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

Add the image processing parameter `Pic-Operations` (a JSON string) to the request header. Its parameters are as follows:

| Parameter | Description | Type | Required |
| ----------- | ------------------------------------------------------------ | ----- | -------- |
| is_pic_info | Whether to return the input image information. Valid values: `0` (no), `1` (yes). Default value: `0`. | Int   | No   |
| rules       |  Processing rules (up to five rules are supported). Each rule corresponds to one processing result. If this parameter is not specified, images will not be processed. | Array | No   |

Parameters of `rules` (a JSON array) are as follows:

| Parameter | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ------ | -------- |
| bucket   | Name of the destination bucket to store the results in the format of `BucketName-APPID`. If this parameter is not specified, the results will be stored in the current bucket by default. | String | No       |
| fileid   | Storage path and name of the output file. <br>Naming rules are as follows (assume the input file is `/p1/test1.jpg`):<br>1. A value starting with a slash (/) indicates an absolute path. For example, if `fileid` is set to `/p2/test2.jpg`, the `test2.jpg` file will be stored in the `p2` folder. <br>2. A value not starting with a slash indicates a relative path. For example, if `fileid` is set to `p2/test2.jpg`, a folder named `p2` will be created in the `p1` folder, and the `test2.jpg` file will be stored in the `p2` folder.<br>3. Note: Do not end the value with a slash; otherwise, an empty filename will be generated.    | String | Yes |
| rule | Processing parameters. For more information, see the image processing API. To process an image by using a specified style, the value must start with `style/`, with the style name followed. For example, if the style name is `test`, the value of `rule` should be `style/test`. | String | Yes |

To use blind watermarking, add the watermarking parameter `watermark` to `rule` as follows:

```shell
watermark/3/type/<type>/image/<imageUrl>/text/<text>/level/<level>
```

The parameters are as follows:

| Parameter | Description | Type | Required |
| ----- | ------------------------------------------------------------ | ------ | -------- |
| type         | Blind watermark type. Valid values: `1` (semi-blind watermark), `2` (blind watermark), `3` (text blind watermark). | Int    | Yes |
| image | URL of the blind watermark image, which must be URL-safe Base64-encoded. This parameter is required if `type` is set to `1` or `2` and does not take effect if `type` is set to `3`. The image watermark must: <br>1. Be stored in the same bucket as the input image. <br>2. Have a URL that starts with `http://`. Note that "http://" cannot be omitted or changed to "https://". For example, the following watermark URLs are invalid: <li> examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/watermark.png <li>https://examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/watermark.png | String | No  |
| text  | Blind watermark text, which must be URL-safe Base64-encoded. This parameter is required if `type` is set to `3` and does not take effect if `type` is set to `1` or `2`. | String |  No  |
| level    | Blind watermark level, which only takes effect if `type` is set to `2`. Valid values: `1` (default value), `2`, `3`. The larger the value, the better the blind watermarking effect. | Int  |  No |


#### Request parameters

This API has no request parameters.


#### Request body

This API does not have a request body.



### Response

#### Response headers

This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).


#### Response body

Parameters in the response body are as follows:

| Parameter | Description | Type |
| ------------ | -------- | --------- |
| UploadResult              | Input image information | Container |

Content of `UploadResult`: 

| Parameter | Description | Type |
| -------------- | ------------ | --------- |
| OriginalInfo              | Input image information     | Container |
| ProcessResults            | Image processing result    | Container |

Content of `OriginalInfo`: 

| Node Name | Description | Type |
| --------- | ------------ | --------- |
| Key     | Input image name     | String    |
| Location | Image path | String    |
| ImageInfo                 | Input image information       | Container |

Content of `ImageInfo`: 

| Node Name | Description | Type |
| ----------- | ------------ | ------ |
| Format  | Format  | String  |
| Width                     | Image width      | Int       |
| Height                    | Image height       | Int       |
| Quality                   | Image quality         | Int       |
| Ave                       | Image average hue    | String    |
| Orientation               | Image rotation angle | Int       |

Content of `ProcessResults`:

| Node Name | Description | Type |
| -------- | ------------------ | --------- |
| Object                    | Processing result of each image | Container |

Content of `Object`:

| Node Name | Description | Type |
| -------- | -------- | ------ |
| Key  | Filename | String  |
| Location | Image path | String    |
| Format  | Image format  | String  |
| Width                     | Image width      | Int       |
| Height                    | Image height       | Int       |
| Size                      | Image size   | Int       |
| Quality                   | Image quality         | Int       |




### Samples

#### Request

```shell
POST /exampleobject?image_process HTTP/1.1
Host: examplebucket-1250000000.cos.ap-chengdu.myqcloud.com
Date: Tue, 03 Apr 2018 09:06:15 GMT
Authorization:XXXXXXXXXXXX

Pic-Operations:
{
    "is_pic_info": 1,
    "rules": [{
        "fileid": "exampleobject",
        "rule": "watermark/3/type/1/image/aHR0cDovL2V4YW1wbGVzLTEyNTEwMDAwMDQucGljc2gubXlxY2xvdWQuY29tL3NodWl5aW4uanBn"
    }]
}
Content-Length: 64
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
              <Key>exampleobject</Key>
              <Location>examplebucket-1250000000.cos.ap-chengdu.myqcloud.com/exampleobject</Location>
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
                   <Key>exampleobject</Key>
                   <Location>examplebucket-1250000000.cos.ap-chengdu.myqcloud.com/exampleobject</Location>
                   <Format>png</Format>
                   <Width>640</Width>
                   <Height>427</Height>
                   <Size>463092</Size>
                   <Quality>100</Quality>
              </Object>
          </ProcessResults>
</UploadResult>
```

## Extracting Blind Watermark

### Request 1: Extracting a blind watermark during upload

#### Sample request

The request for uploading an image with the blind watermark extracted is the same as that in a [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) call, except that you need to add the image processing parameter `Pic-Operations` to the request header and use the blind watermark extraction parameter `watermark/4`.

```shell
PUT /<ObjectKey> HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization:XXXXXXXXXXXX
Pic-Operations: <PicOperations>

[Object Content]
```

>?Authorization: Auth String (for more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778)).

#### Request headers

This API only uses common request headers. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

Add the image processing parameter `Pic-Operations` (a JSON string) to the request header. Its parameters are as follows:

| Parameter | Description | Type | Required |
| :---------- | :----------------------------------------------------------- | :---- | :------- |
| is_pic_info | Whether to return the input image information. Valid values: `0` (no), `1` (yes). Default value: `0`. | Int   | No   |
| rules       |  Processing rules (up to five rules are supported). Each rule corresponds to one processing result. If this parameter is not specified, images will not be processed. | Array | No   |

Parameters of `rules` (a JSON array) are as follows:

| Parameter | Description | Type | Required |
| :------- | :----------------------------------------------------------- | :----- | :------- |
| bucket   | Name of the destination bucket to store the results in the format of `BucketName-APPID`. If this parameter is not specified, the results will be stored in the current bucket by default. | String | No       |
| fileid   | Storage path and name of the output file. <br>Naming rules are as follows (assume the input file is `/p1/test1.jpg`):<br>1. A value starting with a slash (/) indicates an absolute path. For example, if `fileid` is set to `/p2/test2.jpg`, the `test2.jpg` file will be stored in the `p2` folder. <br>2. A value not starting with a slash indicates a relative path. For example, if `fileid` is set to `p2/test2.jpg`, a folder named `p2` will be created in the `p1` folder, and the `test2.jpg` file will be stored in the `p2` folder.<br>3. Note: Do not end the value with a slash; otherwise, an empty filename will be generated.    | String | Yes |
| rule | Processing parameters. For more information, see the image processing API. To process an image by using a specified style, the value must start with `style/`, with the style name followed. For example, if the style name is `test`, the value of `rule` should be `style/test`. | String | Yes |

To extract a blind watermark, add the watermarking parameter `watermark` to `rule` as follows:

```shell
watermark/4/type/<type>/image/<imageUrl>
```

The parameters are as follows:

| Parameter | Description | Type | Required |
| :---- | :----- | :------- | :----------------------------------------------------------- |
| type         | Blind watermark type. Valid values: `1` (semi-blind watermark), `2` (blind watermark), `3` (text blind watermark). **The value must be the same as that used when the blind watermark was added**. | Int    | Yes |
| image | Image URL, which should be specified according to the value of `type`. <br><li>If `type` is `1`, `image` is required and is the URL of the input image. <br><li>If `type` is `2`, `image` is required and is the URL of the watermark image. <br><li>If `type` is `3`, `image` is invalid and does not need to be entered. <br>The value of `image` must be URL-safe Base64-encoded, and the image must: <br>1. Be stored in the same bucket as the image with the blind watermark. <br>2. Have a URL that starts with `http://`. Note that "http://" cannot be omitted or changed to "https://". For example, the following watermark URLs are invalid: <li> examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/watermark.png <li>https://examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/watermark.png | String | No  |

#### Request parameters

This API has no request parameters.

#### Request body

The request body of this API is the image content.



### Response

#### Response headers

This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Response body

`WatermarkStatus` will be added to the `UploadResult.ProcessResults.Object` field in the response body only if `type` is set to `2` in the body of the blind watermark extraction request.

| Parameter | Parent Node | Description | Type |
| :-------------- | :--- | :----- | :----------------------------------------------------------- |
| WatermarkStatus | Object | This field will be returned if `type` is set to `2` to indicate the confidence of the extracted blind watermark. Value range: 0–100. If the value is above 75, there is a confirmed blind watermark. If the value is between 60 and 75, there is a suspected blind watermark. If the value is below 60, no blind watermark is extracted. | Int  |

### Samples

#### Request

```shell
PUT /exampleobject1 HTTP/1.1
Host: examplebucket-1250000000.cos.ap-chengdu.myqcloud.com
Date: Tue, 03 Apr 2018 09:06:15 GMT
Authorization:XXXXXXXXXXXX

Pic-Operations:
{
    "is_pic_info": 1,
    "rules": [{
        "fileid": "exampleobject2",
        "rule": "watermark/4/type/2/image/aHR0cDovL2V4YW1wbGVzLTEyNTEwMDAwMDQucGljc2gubXlxY2xvdWQuY29tL2ZpbGVuYW1lLmpwZWc="
    }]
}
Content-Length: 64

[Object Content]
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
          <Key>exampleobject1</Key>
          <Location>examplebucket-1250000000.cos.ap-chengdu.myqcloud.com/exampleobject1</Location>
          <ImageInfo>
                <Format>JPEG</Format>
                <Width>640</Width>
                <Height>427</Height>
                <Quality>100</Quality>
                <Ave>0xa18454</Ave>
                <Orientation>1</Orientation>
				<FrameCount>1</FrameCount>
          </ImageInfo>
      </OriginalInfo>
      <ProcessResults>
          <Object>
                <Key>exampleobject2</Key>
                <Location>examplebucket-1250000000.cos.ap-chengdu.myqcloud.com/exampleobject2</Location>
                <Format>png</Format>
                <Width>640</Width>
                <Height>427</Height>
                <Size>463092</Size>
                <Quality>100</Quality>
				<FrameCount>1</FrameCount>
				<WatermarkStatus>86</WatermarkStatus>
          </Object>
      </ProcessResults>
</UploadResult>
```

>!
>
>- If `type` is set to `1` in the request, `imageUrl` in the `rule` field in the `Pic-Operations` request header will be the URL of the input image without a blind watermark added. If `type` is set to `2` in the request, `imageUrl` will be the URL of the watermark image.
>- `url` in the `ProcessResults` field in the response body is the URL of the extracted watermark image.


### Request 2: Extracting a blind watermark from an image stored in COS

The request for extracting a blind watermark from an image stored in COS is the same as that used to process in-cloud data as instructed in [Persistent Image Processing](https://intl.cloud.tencent.com/document/product/436/40592), except that you need to add the image processing parameter `Pic-Operations` to the request header and use the blind watermark extraction parameter `watermark/4`.

	
