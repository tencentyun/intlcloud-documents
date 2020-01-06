## Description

Blind watermarking is a brand new watermarking mode provided by Tencent Cloud CI. In this mode, you can add a watermark image to an original image in an invisible manner so that the quality of the original image is not affected. If the image is stolen, you can extract the blind watermark from the suspected stolen resources to verify the ownership of the image.

The blind watermarking feature provided by Tencent Cloud CI is available in three types: semi-blind, fully blind, and text blind watermarks.

| Watermark Type | Characteristics | Use Case |
| ----------------- | ----------------------------------------- | ----------------------- |
| Semi-blind watermark (type1) | It delivers strong anti-attack performance, but the extraction of the watermark requires the original image. | Small-size images (less than 640 x 640) |
| Fully blind watermark (type2) | It is easy to extract, and the extraction of the watermark requires only the watermark image without needing to compare with the original image. | Batch addition or batch verification |
| Text blind watermark (type3) | Text messages can be directly added to images. | Addition of terminal information |

Blind watermarking is a paid service. To use this service, you must activate it on the corresponding bucket configuration page. Each account is provided with a free trial quota of 3,000 images, and will be charged after the trial quota is run out. For more information about the billing, see the [Purchase Guide](https://intl.cloud.tencent.com/document/product/1045/33431).

>
- When using the blind watermarking feature, ensure that the width and height of the watermark image do not exceed 1/8 those of the original image.
- To ensure the proper effect of the blind watermarking, use a white image with a black background as the watermark image.
- Each account is provided with a free trial quota of 3,000 images per month and will be charged normally after the trial quota is run out. The unused quota will not be extended to the next month.
- The text blind watermark currently supports numbers [0-9], upper-case letters [A-Z], and lower-case letters [a-z].


## Use Cases

### Authentication and accountability

You can add a semi-blind watermark to your image. If you find that a malicious attacker has stolen your image, you can retrieve the suspected stolen image, and perform blind watermark extraction in combination with the original image. If an effective watermark image can be extracted, your ownership of the image is proved.

### Upload duplication check

Some users may use other users’ resources to repeatedly upload same information, such as real estate images, vehicle images, and commodity images. To solve this problem, fully blind watermark extraction can be performed on an image uploaded by a user. If watermark image information can be extracted, it proves that the image comes from a previously existing resource, and a corresponding action can be taken, for example, reminding the user not to upload the image repeatedly. If no fully blind watermark can be extracted, a fully blind watermark is added to protect the image from being downloaded and then uploaded by other users.

### Resource leakage prevention

For an internally shared image, you can add visitor information to the image as a text blind watermark when a visitor requests for the image. If the image is leaked, you can extract the blind watermark from the leaked image to learn information about the leaking party.



## Adding a Blind Watermark

### Adding a blind watermark upon upload

#### Request syntax
The request for adding a blind watermark when uploading an image is consistent with that of the PUT Object API of COS, except that the image processing parameter Pic-Operations is added to the header of the request packet and the blind watermark parameter is used. For example, to add a blind watermark upon COS upload, use the following request:

```
PUT /<ObjectKey> HTTP/1.1
Host: <BucketName-APPID>.pic.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
Pic-Operations: <PicOperations>
```

>
- For more information about the PUT Object API of COS, see [COS Documentation](https://intl.cloud.tencent.com/document/product/436/7749).
- Authorization: Auth String (For more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).)


#### Request content
Pic-Operations is a string in JSON format. Related parameters are described as follows:

| Parameter Name | Type | Required | Description |
| ----------- | ----- | ---- | ------------------------------------------------------------ |
| is_pic_info | Int | No | Whether to return the original image information. 0: no. 1: yes. The default value is 0. |
| rules | Array | No | Processing rules. One rule corresponds to one processing result (currently a maximum of five rules are supported). If this parameter is not specified, image processing is not performed. |

Parameters in rules (a JSON array) are described as follows:

| Parameter Name | Type | Required | Description |
| -------- | ------ | ---- | ------------------------------------------------------------ |
| bucket | String | No | The name of the target bucket in which the result is stored. The format is BucketName-APPID. If this parameter is not specified, the result is saved in the current bucket by default. |
| fileid | String | Yes    | Path of the file that stores the processing result. If the path starts with ’/’, the result is stored in the specified folder; otherwise, the result is stored in the same directory as the original image file. |
| rule | String | Yes | The processing parameter. For more information, see the image processing API of CI. If the image needs to be processed according to a specified style, this parameter starts with **style/**, followed by a style name. For example, if the style name is **test**, the value of this parameter is **style/test**. |

To use a blind watermark, you need to add the watermark image parameter (watermark) to rule as follows:

```
watermark/3/type/<type>/image/<imageUrl>/text/<text>
```

**Parameter description**

| Parameter | Type | Required | Description |
| ----- | ------ | ---- | ------------------------------------------------------------ |
| type | Int | Yes | The type of the blind watermark. Valid values: 1 (semi-blind), 2 (fully blind), and 3 (text). |
| image | String | No | The address of the blind watermark image, which must be URL-safe Base64 encoded. This parameter must be specified when type is set to 1 or 2, and is invalid when type is set to 3. The specified watermark image must meet all the following conditions: <br>1. The blind watermark image and the original image must be located in the same bucket. <br>2. The URL must be the domain name of a CI origin server (and cannot be a CDN acceleration or COS origin server domain name). For example, 'examplebucket-1250000000.image.myqcloud.com' is a CDN acceleration domain name, and therefore cannot be used as a watermark URL. <br>3. The URL must start with `http://`, and the HTTP header cannot be omitted or replaced with an HTTPS header. For example, `examplebucket-1250000000.picsh.myqcloud.com/shuiyin_2.png` and `https://examplebucket-1250000000.picsh.myqcloud.com/shuiyin_2.png` are invalid watermark URLs. |
| text | String | Yes | The text of the blind watermark, which must be URL-safe Base64 encoded. This parameter must be specified when type is set to 3, and is invalid when type is set to 1 or 2. |

#### Response

The content of the response body is described as follows:

| Parameter Name | Type | Description |
| ------------ | --------- | -------- |
| UploadResult | Container | Original Image Information |

The content of the UploadResult node:

| Parameter Name | Type | Description |
| -------------- | --------- | ------------ |
| OriginalInfo | Container | Original image information |
| ProcessResults | Container | Image processing result |

The content of the OriginalInfo node:

| Node Name | Type | Description |
| --------- | --------- | ------------ |
| Key | String | Name of the original image file  |
| Location | String | Path of the image file |
| ImageInfo | Container | Original image information |

The content of the ImageInfo node:

| Node Name | Type | Description |
| ----------- | ------ | ------------ |
| Format | String | Format |
| Width | Int | Image width |
| Height | Int | Image height |
| Quality | Int | Image quality |
| Ave | String | Image average hue |
| Orientation | Int | Image orientation |

The content of the ProcessResults node:

| Node Name | Type | Description |
| -------- | --------- | ------------------ |
| Object | Container | Each image processing result |

The content of the Object node:

| Node Name | Type | Description |
| -------- | ------ | -------- |
| Key | String | File name |
| Location | String | Path of the image file |
| Format | String | Image format |
| Width | Int | Image width |
| Height | Int | Image height |
| Size | Int | Image size |
| Quality | Int | Image quality |


> By default, Tencent Cloud COS generates an access URL (access_url) for each resource to allow access to the resource through CDN. If CDN is not activated on the business side, this URL can be obtained but is inaccessible.

**Example**
Request

```shell
PUT /exampleobject HTTP/1.1
Host: examplebucket-1250000000.pic.ap-chengdu.myqcloud.com
Date: Tue, 03 Apr 2018 09:06:15 GMT
Authorization: XXXXXXXXXXXX
Pic-Operations:
{
	"is_pic_info": 1,
	"rules": [{
		"fileid": "exampleobject",
		"rule": "watermark/3/type/1/image/aHR0cDovL2V4YW1wbGVzLTEyNTEwMDAwMDQucGljc2gubXlxY2xvdWQuY29tL3NodWl5aW4uanBn"
	}]
}
Content-Length: 64

[Object]
```

Response packet body

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 645
Date: Tue, 03 Apr 2018 09:06:16 GMT
Status: 200 OK
x-cos-request-id: NWFjMzQ0MDZfOTBmYTUwXzZkZV8zMQ==

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

>
- The `filecontent` field in the request packet body indicates the content of the original image. In the `rule` field of the Pic-Operations request header, `imageUrl` indicates the address of the watermark image.
- In the response packet, URL in the `process_results` field indicates the address of the image containing the blind watermark.

### Adding a blind watermark upon download

Upon image download, adding a blind watermark is the same as adding a common watermark. You need to use watermark parameter after the image URL as follows:

```
watermark/3/type/<type>/image/<imageUrl>/text/<text>
```

**Parameter description**

| Parameter | Type | Required | Description |
| ----- | ------ | ---- | ------------------------------------------------------------ |
| type | Int | Yes | The type of the blind watermark. Valid values: 1 (semi-blind), 2 (fully blind), and 3 (text). |
| image | String | No | The address of the blind watermark image, which must be URL-safe Base64 encoded. This parameter must be specified when type is set to 1 or 2, and is invalid when type is set to 3. The specified watermark image must meet all the following conditions: <br>1. The blind watermark image and the original image must be located in the same bucket. <br>2. The URL must be the domain name of a CI origin server (and cannot be a CDN acceleration or COS origin server domain name). For example, 'examplebucket-1250000000.image.myqcloud.com' is a CDN acceleration domain name, and therefore cannot be used as a watermark URL. <br>3. The URL must start with `http://`, and the HTTP header cannot be omitted or replaced with an HTTPS header. For example, `examplebucket-1250000000.picsh.myqcloud.com/shuiyin_2.png` and `https://examplebucket-1250000000.picsh.myqcloud.com/shuiyin_2.png` are invalid watermark URLs. |
| text | String | Yes | The text of the blind watermark, which must be URL-safe Base64 encoded. This parameter must be specified when type is set to 3, and is invalid when type is set to 1 or 2. |

**Example**

```
http://examplebucket-1250000000.picsh.myqcloud.com/sample.jpeg?watermark/3/type/3/text/ dGVuY2VudCBjbG91ZA==
```

## Extracting a Blind Watermark

#### Request syntax

The request packet for extracting a blind watermark is consistent with that of the PUT Object API of COS, except that the image processing parameter Pic-Operations is added to the header of the request packet and the blind watermark extraction parameter (watermark/4) is used. For example:

```
PUT /<ObjectKey> HTTP/1.1
Host: <BucketName-APPID>.pic.<Region>.myqcloud.com
Date: GMT Date
Authorization: XXXXXXXXXXXX
Pic-Operations: <PicOperations>
```

>
- For more information about the PUT Object API of COS, see [COS Documentation](https://intl.cloud.tencent.com/document/product/436/7749).
- Authorization: Auth String (For more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).)

#### Request content

Pic-Operations is a string in JSON format. Related parameters are described as follows:

| Parameter Name | Type | Required | Description |
| ----------- | ----- | ---- | ------------------------------------------------------------ |
| is_pic_info | Int | No | Whether to return the original image information. 0: no. 1: yes. The default value is 0. |
| rules | Array | No | Processing rules. One rule corresponds to one processing result (currently a maximum of five rules are supported). If this parameter is not specified, image processing is not performed. |

Parameters in rules (a JSON array) are described as follows:

| Parameter Name | Type | Required | Description |
| -------- | ------ | ---- | ------------------------------------------------------------ |
| bucket | String | No | The name of the target bucket in which the result is stored. The format is BucketName-APPID. If this parameter is not specified, the result is stored in the current bucket by default. |
| fileid | String | Yes | The path of the file that stores the processing result. If the path starts with ’/’, the result is stored in the specified folder; otherwise, the result is stored in the same directory as the original image file. |
| rule | String | Yes | The processing parameter. For more information, see the image processing API of CI. If the image needs to be processed according to a specified style, this parameter starts with **style/**, followed by a style name. For example, if the style name is **test**, the value of the rule field is **style/test**. |

To extract a blind watermark, you need to add the watermark image parameter (watermark) to `rule` as follows:

```
watermark/4/type/<type>/image/<imageUrl>/text/<text>
```

**Parameter description**

| Parameter | Type | Required | Description |
| ----- | ------ | ---- | ------------------------------------------------------------ |
| type | Int | Yes | The type of the blind watermark. Valid values: 1 (semi-blind), 2 (fully blind), and 3 (text). **The value of this parameter must be consistent with the type set when the blind watermark is added.** |
| image | String | No | The image address. This parameter must be specified when type is set to 1 or 2, and is invalid when type is set to 3. **When type is set to 1, this parameter specifies the address of the original image. When type is set to 2, this parameter specifies the address of the watermark image.** This parameter must be URL-safe Base64 encoded. The specified watermark image must meet all the following conditions: <br>1. This image and the watermarked image must be located in the same bucket. <br>2. The URL must be a domain name of a CI origin server (and cannot be a CDN acceleration or COS origin server domain name). For example, 'examplebucket-1250000000.image.myqcloud.com' is a CDN acceleration domain name, and therefore cannot be used as a watermark URL. <br>3. The URL must start with `http://`, and the HTTP header cannot be omitted or replaced with an HTTPS header. For example, `examplebucket-1250000000.picsh.myqcloud.com/shuiyin_2.png` and `https://examplebucket-1250000000.picsh.myqcloud.com/shuiyin_2.png` are invalid watermark URLs. |

#### Response

The WatermarkStatus parameter is added to the UploadResult-ProcessResults-Object field in the response. This parameter is returned when type in the blind watermark extraction request is set to 2, and is not returned in other cases.

| Parameter | Type | Parent Node | Description |
| --------------- | ---- | ------ | ------------------------------------------------------------ |
| WatermarkStatus | Int | Object | This parameter is returned when type in the blind watermark extraction request is set to 2. It indicates the confidence level of the extracted fully blind watermark. Value range: 0-100. If the value is greater than 75, the blind watermark does exist. If the value ranges from 60 to 75, the blind water may exist. If the value is less than 60, it can be considered that no blind watermark is extracted. |

**Example**
Request

```shell
PUT /exampleobject1 HTTP/1.1
Host: examplebucket-1250000000.pic.ap-chengdu.myqcloud.com
Date: Tue, 03 Apr 2018 09:06:15 GMT
Authorization: XXXXXXXXXXXX
Pic-Operations:
{
	"is_pic_info": 1,
	"rules": [{
		"fileid": "exampleobject2",
		"rule": "watermark/4/type/1/image/aHR0cDovL2V4YW1wbGVzLTEyNTEwMDAwMDQucGljc2gubXlxY2xvdWQuY29tL2ZpbGVuYW1lLmpwZWc="
	}]
}
Content-Length: 64

[Object]
```

Response packet body

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 645
Date: Tue, 03 Apr 2018 09:06:16 GMT
Status: 200 OK
x-cos-request-id: NWFjMzQ0MDZfOTBmYTUwXzZkZV8zMQ==

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
</Object>
</ProcessResults>
</UploadResult>
```

>
- If type in the request is set to 1, `imageUrl` in the `rule` field of the Pic-Operations request header indicates the address of the original image without the blind watermark. If type in the request is set to 2, `imageUrl` in the `rule` field of the Pic-Operations request header indicates the address of the watermark image.
- URL in the `ProcessResults` field of the response packet indicates the address of the extracted watermark image.