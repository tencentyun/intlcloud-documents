## Overview

The blind watermark feature allows you to add an invisible watermark to an image, which does not affect the look and feel and retains the originality of the image. If you suspect that your image has been stolen, you can extract the invisible watermark through [blind watermark extraction](https://intl.cloud.tencent.com/document/product/1045/43029) to prove your ownership of the image.
You can call this API to:
- Add or extract a blind watermark to or from an image during upload.
- Add or extract a blind watermark to or from an image stored in COS.
- Add a blind watermark to an image during download.

CI introduces three blind watermarking types: semi-blind watermarking, perfectly blind watermarking, and text blind watermarking.

| Blind Watermarking Type | Feature | Applicable Scenario |
| ----------------- | ----------------------------------------- | ----------------------- |
| Semi-blind watermarking (type 1) | Has strong anti-theft effects but requires the input image for watermark extraction | Images smaller than 640x640 |
| Perfectly blind watermarking (type 2) | Is easy to extract and requires only the watermarked image for watermark extraction | Batch adding and verification  |
| Text blind watermarking (type 3) | Adds text to the image | Adding terminal information  |

- Blind watermarking is a paid service, which needs to be activated on the bucket's configuration page. For detailed pricing, see [Image Processing Fees](https://intl.cloud.tencent.com/document/product/1045/45582).

>?
> - Currently, you cannot add a blind watermark to animated images such as GIF.
> - Both the width and height of the image watermark must not be greater than 1/8 of the input image.
> - You need to choose a white watermark with a black background for the effect of blind watermarking.
> - Text watermarks can contain digits and letters.
> - Blind watermarking protects your images against various theft attacks such as cropping, smudging, and color change. The anti-theft effect is affected by the size of the input image and the attack intensity. For details, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).
> - Blind watermarking is supported in all regions of CI. For more information, see [Regions and Domain Names](https://intl.cloud.tencent.com/document/product/1045/33423).

## Use Cases

### Authentication and accountability

By adding semi-blind watermarks to your images, you can claim your images when they are stolen and extract blind watermarks using the corresponding input images to prove that you own the images.

### Checking duplicates upon upload

Sometimes, other users might upload duplicate images (such as real estate images, car images, and product images). To solve this problem, you can perform perfectly blind watermark extraction before the upload, and if you can extract a blind watermark from an image, it has been uploaded before. In this case, you can perform corresponding operations, such as telling the user not to upload duplicate images. If an image does not contain a blind watermark, you can add one to it to prevent duplicate uploads.

### Avoiding image leakage

For internal images, you can add information about the requester to the images by using text blind watermarks. In this way, when an image is leaked, you can extract the blind watermark and get information about the leaker.



## Adding Blind Watermarks

### Request 1: adding a blind watermark upon upload

The request is the same as that in a [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) call, except that you need to add the image processing parameter `Pic-Operations` to the request header and use blind watermarking parameters.

#### Sample request

```shell
PUT /<ObjectKey> HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
Pic-Operations: <PicOperations>

[Object Content]
```


>? 
> - Authorization: Auth String (See [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for details.)
> - When this feature is used by a sub-account, relevant permissions must be granted as instructed in [Authorization Granularity Details](https://intl.cloud.tencent.com/document/product/1045/49896).
> 

#### Request headers

This API uses [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

Add the image processing parameter `Pic-Operations` (a JSON string) to the request header. Its parameters are as follows:

| Parameter | Description | Type | Required |
| ----------- | ----- | ---- | ------------------------------------------------------------ |
| is_pic_info | Whether to return the input image information <br>`0` (default): no <br>`1`: yes | Int | No |
| rules       | Processing rules (up to five rules are supported). Each rule corresponds to one processing result. If this parameter is not specified, images will not be processed. | Array | No       |

Parameters of `rules` (a JSON array) are as follows:

| Parameter | Description | Type | Required |
| -------- | ------ | ----- | ------------------------------------------------------------ |
| bucket | Name of the destination bucket to store the results, formatted as `BucketName-APPID`. If this parameter is not specified, the results will be stored in the current bucket. | String | No |
| fileid   | Storage path and name of the output file. <br>Naming rules are as follows (assume the input file is `/p1/test1.jpg`):<br>1. A value starting with a slash (/) indicates an absolute path. For example, if `fileid` is set to `/p2/test2.jpg`, the `test2.jpg` file will be stored in the `p2` folder. <br>2. A value not starting with a slash indicates a relative path. For example, if `fileid` is set to `p2/test2.jpg`, a folder named `p2` will be created in the `p1` folder, and the `test2.jpg` file will be stored in the `p2` folder.<br>3. Note: Do not end the value with a slash; otherwise, an empty filename will be generated.    | String | Yes |
| rule | Processing parameters. For more information, see the image processing API. To process an image by using a specified style, the value must start with `style/`, with the style name followed. For example, if the style name is `test`, the value of `rule` should be `style/test`. | String | Yes |

To use blind watermarking, add the watermarking parameter `watermark` to `rule` as follows:

```shell
watermark/3/type/<type>/image/<imageUrl>/text/<text>/level/<level>
```

The parameters are as follows:

| Parameter | Description | Type | Required |
| ----- | ------ | ---- | ------------------------------------------------------------ |
| type         | Blind watermarking type. Valid values: `1` (semi-blind watermarking), `2` (perfectly blind watermarking), `3` (text blind watermarking) | Int    | Yes |
| image | URL of the blind image watermark, which must be URL-safe Base64 encoded. This parameter is required if `type` is set to `1` or `2`, and does not take effect if `type` is set to `3`. The image watermark must:<br>1. Be stored in the same bucket as the input image. <br>2. Have a URL that starts with `http://`. Note that "http://" cannot be omitted or changed to "https://". For example, the following watermark URLs are invalid: <li> `examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/watermark.png` </li><li>`https://examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/watermark.png`</li> | String | No  |
| text  | Text watermark, which must be URL-safe Base64-encoded. This parameter is required if `type` is set to `3` and does not take effect if `type` is set to `1` or `2`. |String |  No  |
| level    | Perfectly blind watermarking level, which only takes effect when `type` is set to `2`. Valid values: `1` (default), `2`, `3`. The larger the value, the better the watermarking effects. | Int  |  No |


#### Request parameters

This API has no request parameter.


#### Request body

The request body of this API is the content of the input image.



### Response

#### Response headers

This API only returns [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).


#### Response body

Parameters in the response body are as follows:

| Parameter | Description | Type |
| ------------------------- | ------------------ | --------- |
| UploadResult              | Upload results | Container |

Content of `UploadResult`: 

| Parameter | Description | Type |
| ------------------------- | ------------------ | --------- |
| OriginalInfo              | Information about the input image     | Container |
| ProcessResults            | Processing results    | Container |

Content of `OriginalInfo`:

| Parameter | Description | Type |
| ------------------------- | ------------------ | --------- |
| Key     | Name of the input image      | String    |
| Location | Image location  | String    |
| ImageInfo                 | Information about the input image | Container |

Content of `ImageInfo`:

| Parameter | Description | Type |
| ------------------------- | ------------------ | --------- |
| Format                    | Image format  | String    |
| Width                     | Image width      | Int       |
| Height                    | Image height       | Int       |
| Quality                   | Image quality         | Int       |
| Ave                       | Image average hue    | String    |
| Orientation               | Image rotation angle | Int       |

Content of `ProcessResults`:

| Parameter | Description | Type |
| ------------------------- | ------------------ | --------- |
| Object                    | Processing results of each image | Container |

Content of `Object`:

| Parameter | Description | Type |
| ------------------------- | ------------------ | --------- |
| Key  | Filename | String  |
| Location | Image location  | String    |
| Format  | Image format  | String  |
| Width                     | Image width      | Int       |
| Height                    | Image height       | Int       |
| Size                      | Image size   | Int       |
| Quality                   | Image quality         | Int       |





### Example

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
> - [Object Content] in the request body is the binary string of the input image, and `imageUrl` in `rule` in the request header `Pic-Operations` is the URL of the image watermark.
> - `Location` in `ProcessResults` in the response body is the URL of the image with a blind watermark.
>


### Request 2: adding a blind watermark upon download

You can add a blind watermark upon download in the same way as adding a regular watermark, except that you need to use the `watermark` parameter after the image URL.

#### Sample request

```plaintext
GET /<ObjectKey>?watermark/3/type/<type>/image/<imageUrl>/text/<text> HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: <GMT Date>
Authorization: <Auth String>
```

#### Request parameters

The request parameters are as follows:

| Parameter | Description | Type |Required |
| ------------ | ------------------------------------------------------------ | ------ | -------- |
| ObjectKey | Object name, such as `folder/sample.jpg`. | String  | Yes |
| type         | Blind watermarking type. Valid values: `1` (semi-blind watermarking), `2` (perfectly blind watermarking), `3` (text blind watermarking) | Int    | Yes |
| image | URL of the blind image watermark, which must be URL-safe Base64 encoded. This parameter is required if `type` is set to `1` or `2`, and does not take effect if `type` is set to `3`. The image watermark must:<br>1. Be stored in the same bucket as the input image. <br>2. Have a URL that starts with `http://`. Note that "http://" cannot be omitted or changed to "https://". For example, the following watermark URLs are invalid: <li> `examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/watermark.png` </li><li>`https://examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/watermark.png`</li> | String | No  |
| text  | Text watermark, which must be URL-safe Base64-encoded. This parameter is required if `type` is set to `3` and does not take effect if `type` is set to `1` or `2`. |String |  No  |
| level    | Perfectly blind watermarking level, which only takes effect when `type` is set to `2`. Valid values: `1` (default), `2`, `3`. The larger the value, the better the watermarking effects. | Int  |  No |

### Example

```shell
https://examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/sample.jpeg?watermark/3/type/3/text/dGVuY2VudCBjbG91ZA==
```

### Request 3: adding a blind watermark to an image stored in COS

You can call this API to add a blind watermark to an image stored in COS and save the result to COS.

#### Sample request

```shell
POST /<ObjectKey>?image_process HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
Pic-Operations: <PicOperations>
```

>? 
> - Authorization: Auth String (See [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for details.)
> - When this feature is used by a sub-account, relevant permissions must be granted as instructed in [Authorization Granularity Details](https://intl.cloud.tencent.com/document/product/1045/49896).
> 

#### Request headers

This API uses [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

Add the image processing parameter `Pic-Operations` (a JSON string) to the request header. Its parameters are as follows:

| Parameter | Description | Type | Required |
| ----------- | ------------------------------------------------------------ | ----- | -------- |
| is_pic_info | Whether to return the input image information <br>`0` (default): no <br>`1`: yes    | Int   | No       |
| rules       | Processing rules (up to five rules are supported). Each rule corresponds to one processing result. If this parameter is not specified, images will not be processed. | Array | No       |

Parameters of `rules` (a JSON array) are as follows:

| Parameter | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ------ | -------- |
| bucket | Name of the destination bucket to store the results, formatted as `BucketName-APPID`. If this parameter is not specified, the results will be stored in the current bucket. | String | No |
| fileid   | Storage path and name of the output file. <br>Naming rules are as follows (assume the input file is `/p1/test1.jpg`):<br>1. A value starting with a slash (/) indicates an absolute path. For example, if `fileid` is set to `/p2/test2.jpg`, the `test2.jpg` file will be stored in the `p2` folder. <br>2. A value not starting with a slash indicates a relative path. For example, if `fileid` is set to `p2/test2.jpg`, a folder named `p2` will be created in the `p1` folder, and the `test2.jpg` file will be stored in the `p2` folder.<br>3. Note: Do not end the value with a slash; otherwise, an empty filename will be generated.    | String | Yes |
| rule | Processing parameters. For more information, see the image processing API. To process an image by using a specified style, the value must start with `style/`, with the style name followed. For example, if the style name is `test`, the value of `rule` should be `style/test`. | String | Yes |

To use blind watermarking, add the watermarking parameter `watermark` to `rule` as follows:

```shell
watermark/3/type/<type>/image/<imageUrl>/text/<text>/level/<level>
```

The parameters are as follows:

| Parameter | Description | Type |Required |
| ----- | ------------------------------------------------------------ | ------ | -------- |
| type         | Blind watermarking type. Valid values: `1` (semi-blind watermarking), `2` (perfectly blind watermarking), `3` (text blind watermarking) | Int    | Yes |
| image | URL of the blind image watermark, which must be URL-safe Base64-encoded. This parameter is required if `type` is set to `1` or `2`, and does not take effect if `type` is set to `3`. The image watermark must:<br>1. Be stored in the same bucket as the input image. <br>2. Have a URL that starts with `http://`. Note that "http://" cannot be omitted or changed to "https://". For example, the following watermark URLs are invalid: <li> `examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/watermark.png` </li> <li>`https://examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/watermark.png`</li> | String | No  |
| text  | Text watermark, which must be URL-safe Base64-encoded. This parameter is required if `type` is set to `3` and does not take effect if `type` is set to `1` or `2`. |String |  No  |
| level    | Perfectly blind watermarking level, which only takes effect when `type` is set to `2`. Valid values: `1` (default), `2`, `3`. The larger the value, the better the watermarking effects. | Int  |  No |


#### Request parameters

This API has no request parameter.


#### Request body

This API does not have a request body.



### Response

#### Response headers

This API only returns [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).


#### Response body

Parameters in the response body are as follows:

| Parameter | Description | Type |
| ------------ | -------- | --------- |
| UploadResult              | Upload results | Container |

Content of `UploadResult`: 

| Parameter | Description | Type |
| -------------- | ------------ | --------- |
| OriginalInfo              | Information about the input image     | Container |
| ProcessResults            | Processing results    | Container |

Content of `OriginalInfo`: 

| Parameter | Description | Type |
| --------- | ------------ | --------- |
| Key      | Name of the input image      | String    |
| location       | Location of the input image | String  |
| ImageInfo                 | Information about the input image | Container |

Content of `ImageInfo`: 

| Parameter | Description | Type |
| ----------- | ------------ | ------ |
| Format      | Image format | String |
| Width                     | Image width      | Int       |
| Height                    | Image height       | Int       |
| Quality                   | Image quality         | Int       |
| Ave                       | Image average hue    | String    |
| Orientation               | Image rotation angle | Int       |

Content of `ProcessResults`:

| Parameter | Description | Type |
| -------- | ------------------ | --------- |
| Object                    | Processing results of each image | Container |

Content of `Object`:

| Parameter | Description | Type |
| -------- | -------- | ------ |
| Key  | Filename | String  |
| location       | Location of the input image | String  |
| Format      | Image format | String |
| Width                     | Image width      | Int       |
| Height                    | Image height       | Int       |
| Size                      | Image size   | Int       |
| Quality                   | Image quality         | Int       |




### Example

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

## Extracting Blind Watermarks

### Example 1: Extracting upon upload

#### Sample request

The request for uploading an image with the blind watermark extracted is the same as that in a [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) call, except that you need to add the image processing parameter `Pic-Operations` to the request header and use the watermark extraction parameter `watermark/4`.

```shell
PUT /<ObjectKey> HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization:XXXXXXXXXXXX
Pic-Operations: <PicOperations>

[Object Content]
```

>? 
> - Authorization: Auth String (See [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for details.)
> - When this feature is used by a sub-account, relevant permissions must be granted as instructed in [Authorization Granularity Details](https://intl.cloud.tencent.com/document/product/1045/49896).
> 

#### Request headers

This API uses [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

Add the image processing parameter `Pic-Operations` (a JSON string) to the request header. Its parameters are as follows:

| Parameter | Description | Type | Required |
| :---------- | :----------------------------------------------------------- | :---- | :------- |
| is_pic_info | Whether to return the input image information <br>`0` (default): no <br>`1`: yes    | Int   | No       |
| rules       | Processing rules (up to five rules are supported). Each rule corresponds to one processing result. If this parameter is not specified, images will not be processed. | Array | No       |

Parameters of `rules` (a JSON array) are as follows:

| Parameter | Description | Type | Required |
| :------- | :----------------------------------------------------------- | :----- | :------- |
| bucket | Name of the destination bucket to store the results, formatted as `BucketName-APPID`. If this parameter is not specified, the results will be stored in the current bucket. | String | No |
| fileid   | Storage path and name of the output file. <br>Naming rules are as follows (assume the input file is `/p1/test1.jpg`):<br>1. A value starting with a slash (/) indicates an absolute path. For example, if `fileid` is set to `/p2/test2.jpg`, the `test2.jpg` file will be stored in the `p2` folder. <br>2. A value not starting with a slash indicates a relative path. For example, if `fileid` is set to `p2/test2.jpg`, a folder named `p2` will be created in the `p1` folder, and the `test2.jpg` file will be stored in the `p2` folder.<br>3. Note: Do not end the value with a slash; otherwise, an empty filename will be generated.    | String | Yes |
| rule | Processing parameters. For more information, see the image processing API. To process an image by using a specified style, the value must start with `style/`, with the style name followed. For example, if the style name is `test`, the value of `rule` should be `style/test`. | String | Yes |

To extract a blind watermark, you need to add the `watermark` parameter to `rule` as follows:

```shell
watermark/4/type/<type>/image/<imageUrl>
```

The parameters are as follows:

| Parameter | Description | Type |Required |
| :---- | :----------------------------------------------------------- | :----- | :------- |
| type         | Blind watermarking type. Valid values: `1` (semi-blind watermarking), `2` (perfectly blind watermarking), `3` (text blind watermarking). **The value must be the same as that used when the blind watermark was added**. | Int    | Yes |
| image | Image URL, which should be specified according to the value of `type`. If the value of `type` is: <br><li>`1`, `image` is required and is the URL of the input image. <br><li>`2`, `image` is required and is the URL of the image watermark. <br><li>`3`, `image` does not need to be specified and will not take effect. <br>The value of `image` must be URL-safe Base64-encoded, and the image must: <br>1. Be stored in the same bucket as the image with the blind watermark. <br>2. Have a URL that starts with `http://`. Note that "http://" cannot be omitted or changed to "https://". For example, the following watermark URLs are invalid: <li> `examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/watermark.png`</li><li>`https://examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/watermark.png`</li> | String | No  |

#### Request parameters

This API has no request parameter.

#### Request body

The request body of the API is the binary string of the image.



### Response

#### Response headers

This API only returns [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Response body

`WatermarkStatus` will be added to the `UploadResult.ProcessResults.Object` node only if `type` is set to `2` in the request body of the blind watermark extraction request.

| Parameter | Parent Node | Description | Type |
| :-------------- | :----- | :----------------------------------------------------------- | :--- |
| WatermarkStatus | Object | This parameter is returned if `type` is set to `2` to indicate the confidence of the watermark extracted. Value range: 0–100. <br>If the value is greater than 75, there is a blind watermark. <br>If the value falls in the range of 60−75, there is a suspected blind watermark. <br>If the value is smaller than 60, no blind watermark is extracted. | Int  |

### Example

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
>- If `type` is set to `1` in the request, `imageUrl` in `rule` in `Pic-Operations` is the URL of the input image without a blind watermark added. If `type` is set to `2` in the request, `imageUrl` is the URL of the image watermark.
>- `url` in `ProcessResults` in the response body is the URL of the image watermark extracted.
>


### Example 2: Extracting from an image stored in COS

The request for extracting a blind watermark from an image stored in COS is the same as that used to [Process In-Cloud Data](https://intl.cloud.tencent.com/document/product/436/40592), except that you need to add the image processing parameter `Pic-Operations` to the request header and use the watermark extraction parameter `watermark/4`.

​	
