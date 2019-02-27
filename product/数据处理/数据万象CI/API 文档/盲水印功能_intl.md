>Note:
The blind watermarking function is currently in public trial, and each user has a free quota of 3,000 watermarks per day for testing, and operations out of the quota will not be processed. If you need a higher quota, please click **Contact Us** on the right or submit a ticket for consultation.

The blind watermarking function is a new watermark mode provided by CI. With this function, a watermark image can be added to the original image in an invisible form without affecting the quality of the original image. In case the original image is stolen, you can perform blind watermark extraction on the suspected stolen resource to claim your ownership to it.

Blind watermarking offers three types of watermarks: semi-blind, completely blind and blind text. A semi-blind watermark has stronger protection capability against multiple kinds of attacks such as cropping, smearing and discoloration, but the original image is needed when extracting the watermark; a completely blind watermark can be extracted without the original image, but its anti-attack capability is relatively low; a blind text watermark can directly add text to the image without using a watermark image, which is suitable for scenarios where different information needs to be added.

>**Note:**
Blind watermarking adds the watermark image to the original image's frequency domain; as a result, the simpler the watermark image, the better the effect, and the watermark image's length and width cannot exceed 1/8 of those of the original image.

## Applicable Scenarios
### 1. Authentication and Accountability
Semi-blind watermarks can be added to your image resources. In case it is found that the resources have been stolen by an attacker, watermark extraction can be performed on the suspected stolen images against the corresponding original images, and if valid watermark images are obtained, your ownership to the resources can be verified.

### 2. Duplication Check for Uploaded Images
To fix the issue where a user repeatedly uploads the same information using resources of other users (such as images of houses, cars or products), completely blind watermark extraction can be performed before the user uploads the image resources, and if a watermark image is successfully extracted from an image, it means that the image comes from an existing resource, and then corresponding actions can be taken (such as reminding the user not to upload resources repeatedly); if there is no completely blind watermark, one can be added to the image resource to protect it from being downloaded and then uploaded repeatedly by other users.

### 3. Resource Leakage Prevention
For image resources shared within your organization, the visitors' identity information can be added as blind text watermarks to images when they are accessed. In case an image is leaked, blind text watermark extraction can be performed on the leaked image to identify the leaker.

## Adding a Blind Watermark

### Adding When Uploading
#### Request Syntax
The request packet for adding a blind watermark when uploading an image is similar to the simple file upload API of COS. Simply replace the host information with CI's domain name, add the image processing parameter Pic-Operations to the request packet header and use the blind watermark parameter. Below is a specific example:

```
POST /files/v2/<Appid>/<Bucket>/<FileName> HTTP/1.1
Host: <Region>.image.myqcloud.com
Content-Type: multipart/form-data
Authorization: <MultiEffectSignature>
Content-Length: <ContentLength>
Pic-Operations: <PicOperations>
```

For details of the simple file upload API of COS, see [COS documentation](https://cloud.tencent.com/document/product/436/6066).

#### Request
Pic-Operations is a string in .json format with specific parameters as follows:

| Parameter name | Type | Required | Description |
| ----------- | ----- | ---- | ---------------------------------------- |
| is_pic_info | Int | No | Whether to return the original image information; 0 - no, 1 - yes, 0 by default |
| rules | Array | No | Processing rules; one rule corresponds to one processing result (currently, up to five rules are supported); if left blank, no image processing will be performed |

The specific parameters in rules (.json array) are as follows:

| Parameter name | Type | Required | Description |
| ------ | ------ | ---- | ---------------------------------------- |
| bucket | String | No | Name of the destination bucket that stores the result in the form of bucketName-appid; if not specified, the result will be saved to the current bucket by default |
| fileid | String | Yes | File pathname of the processing result; if it starts with '/', the result will be stored in the specified folder; otherwise, the result will be stored in the same directory as the original image file |
| rule | String | Yes | Processing parameter; for details, see CI's image processing API. If it is to process according to the specified style, this parameter should start with "style/" followed by the style name; for example, if the style name is "test", the rule field will be "style/test" |

To use blind watermarking, a watermark parameter (watermark) needs to be added to the rule. For details, see below:

```
watermark/3/type/<type>/image/<imageUrl>/text/<text>
```

| Parameter | Type | Required | Description |
| ----- | ------ | ---- | ---------------------------------------- |
| type | Int | Yes | Blind watermark type; valid values: 1 - semi-blind, 2 - completely blind, 3 - text |
| image | String | No | Blind watermark image address; URL-safe Base64 encoding is necessary. Required when type is 1 or 2; invalid when type is 3. The specified watermark image must satisfy all the following three conditions: 1. The blind watermark image and the original image must be in the same object bucket; 2. The URL needs to use CI's real server domain name (CDN's and COS' real server domain names are not supported), for example, v2test-10000812.image.myqcloud.com is a CDN domain name and thus cannot be used as the watermark URL; 3. The URL must `start with http:// (the http header cannot be omitted`, and the HTTPS header is not supported), for example, `tengxunyun-10004486.picsh.myqcloud.com/shuiyin_2.png and https://tengxunyun-10004486.picsh.myqcloud.com/shuiyin_2.png are invalid watermark URLs. ` |
| text | String | Yes | Blind watermark text; URL-safe Base64 encoding is necessary. Required when type is 3, invalid when type is 1 or 2. |

#### Return

| Parameter name | Type | Description |
| ---------- | ------ | ---------------------------------------- |
| code | Number | Server error code; if no error occurred, the value is **0**; if an error occurred, this parameter refers to the specific error code. Error codes related to the COS service can be found in [COS Error Codes](https://cloud.tencent.com/document/product/436/8432) |
| message | String | Server prompt; if an error occurred, this field details the error.           |
| request_id | String | Unique id of the request |
| data | Object | The response data returned by the server, which represents the specific business data returned by the API.           |

Description of the data parameter

| Parameter name | Type | Description |
| ------------- | ------ | ---------------------------------------- |
| access_url | String | Access the file's resource link via CDN (faster) |
| resource_path | String | The relative pathname of this file in COS, which can be used as its ID. Format: /&lt;APPID&gt;/&lt;BucketName&gt;/&lt;ObjectName&gt;. It is recommended that the business side store the resource_path and then flexibly splice the resource url based on actual business needs (the url for accessing the COS resource via CDN is different from that for directly accessing the COS resource). |
| source_url | String | Directly access the COS resource link without CDN |
| url | String | url of the file to be operated. The business side can perform further operations on the file by using the url as the request address, i.e., the request address in the following APIs: file properties, file update, file deletion and file moving. |
| image_info | Object | Image processing result |
| timecost      | Number | Time consumed in ms                                  |

Description of the image_info parameter

| Parameter name | Type | Description |
| --------------- | ------ | ---------------- |
| original_info   | Object | Original image information; present if it is specified to return the original image information |
| process_results | Array | Image processing result |

Description of the original_info parameter

| Parameter name | Type | Description |
| ----------- | ------ | ------ |
| format | String | Format |
| width | Number | Image width |
| height | Number | Image height |
| ave | String | Image's main tone |
| orientation | Number | Image's rotation angle |
| quality | Number | Image quality |

Description of the parameters in the process_results array

| Parameter name | Type | Description |
| ---------------- | ------ | ---------------------------------------- |
| watermark_status | number | When the blind watermark state (type) is set to 2 (completely blind), this parameter will return whether a watermark image is successfully extracted; 0 - not extracted, 1 - extracted. |
| file_id | String | Filename |
| format | String | Format |
| width | Number | Image width |
| height | Number | Image height |
| size | Number | Image size |
| quality | Number | Image quality |
| access_url | String | Access the file's resource link via CDN (faster) |
| resource_path | String | The relative pathname of this file in COS, which can be used as its ID. Format: ¸ñÊ½/&lt;APPID&gt; /&lt;BucketName&gt; /&lt;ObjectName&gt;. It is recommended that the business side store the resource_path and then flexibly splice the resource url based on actual business needs (the url for accessing the COS resource via CDN is different from that for directly accessing the COS resource). |
| source_url | String | Directly access the COS resource link without CDN |
| url | String | url of the file to be operated. The business side can perform further operations on the file by using the url as the request address, i.e., the request address in the following APIs: file properties, file update, file deletion and file moving. |

>**Note:**
Tencent Cloud COS will generate a CDN access link "access_url" for each resource by default. Even if the business side has not activated CDN yet, the link can still be obtained, but it cannot be accessed.

#### Example
Request

```
POST /files/v2/appid/bucket/sample_file.jpg HTTP/1.1
Host: cd.image.myqcloud.com
Connection: keep-alive
Accept-Encoding: gzip, deflate
Accept: */*
User-Agent: cos-python-sdk-v4
Authorization: XXXXXXXXXXXXXXXXXXXXXXXXXX
Content-Length: XXXXX
Pic-Operations: '{"rules":[{"fileid":"test1.jpg ","rule":" watermark/3/type/1/image/<imageUrl>"}]}'
Content-Type: multipart/form-data; boundary=6815dbc897af4706bd5a39f49b157928

--6815dbc897af4706bd5a39f49b157928
Content-Disposition: form-data; name="op"; 

upload
--6815dbc897af4706bd5a39f49b157928
Content-Disposition: form-data; name="filecontent"; filename="filecontent"
```

#### Response Packet

```
{
"code":0,
"message":"SUCCESS",
"request_id":"NTlhNDBhZGVfOTYyMjViNjRfMTc3Ml8yYWQ5NWU=",
"data":
{
"access_url":"http://bucket-appid.file.myqcloud.com/sample_file.jpg",
"resource_path":"/appid/bucket/sample_file.jpg",
"source_url":"http://bucket-appid.cosgz.myqcloud.com /sample_file.jpg",
"url":"http://gz.file.myqcloud.com/files/v2/appid/bucket/sample_file.jpg",
image_info:
{
      process_results:
  [ 
{
    "access_url":"http://bucket-appid.file.myqcloud.com/test1.jpg",
"resource_path":"/appid/bucket/test1.jpg",
"source_url":"http://bucket-appid.cosgz.myqcloud.com/test1. jpg ",
"url":"http://gz.file.myqcloud.com/files/v2/appid/bucket/test1. jpg ",
"vid":"value",
"file_id":"test1. jpg ",
"format":"JPG",
"height":50,
"width":200,
"size":100200
}
]
}
}

```

>**Note:**
The filecontent field of the request packet is the image content of the original image. In the rule field of the packet header Pic-Operations, imageUrl is the watermark image address.
The url in the process_results field of the return packet is the address of the image carrying the blind watermark.

## Extracting a Blind Watermark
The request packet for blind watermark extraction is similar to that for adding a blind watermark. Simply modify the image processing parameters in Pic-Operations of the request packet header. Below is a specific example:

Image processing parameters for extracting the blind watermark:
```
watermark/4/type/<type>/image/<imageUrl>
```

#### Parameter Descriptions

| Parameter | Type | Required | Description |
| ----- | ------ | ---- | ---------------------------------------- |
| type | Int | Yes | Blind watermark type; valid values: 1 - semi-blind, 2 - completely blind, 3 - text; this must be the same as the type of the blind watermark |
| image | String | No | Image address; required if type is 1 or 2, invalid if type is 3; when type is 1, it is the original image address; when type is 2, it is the watermark image address; URL-safe Base64 encoding is necessary. The specified image must satisfy all the following three conditions: 1. The image and the watermarked image must be in the same object bucket; 2. The URL needs to use CI's real server domain name (CDN's and COS' real server domain names are not supported), for example, v2test-10000812.image.myqcloud.com is a CDN domain name and thus cannot be used as the watermark URL; 3. The URL must `start with http:// (the http header cannot be omitted, and the HTTPS header is not supported), for example, tengxunyun-10004486.picsh.myqcloud.com/shuiyin_2.png and https://tengxunyun-10004486.picsh.myqcloud.com/shuiyin_2.png are invalid watermark URLs. ` |

#### Example
Request

```
POST /files/v2/appid/bucket/test1.jpg HTTP/1.1
Host: cd.image.myqcloud.com
Connection: keep-alive
Accept-Encoding: gzip, deflate
Accept: */*
User-Agent: cos-python-sdk-v4
Authorization: XXXXXXXXXXXXXXXXXXXXXXXXXX
Content-Length: XXXXX
Pic-Operations: '{"rules":[{"fileid":"test2.png ","rule":" 
watermark/4/type/1/image/<imageUrl>"}]}'
Content-Type: multipart/form-data; boundary=6815dbc897af4706bd5a39f49b157928

--6815dbc897af4706bd5a39f49b157928
Content-Disposition: form-data; name="op"; 

upload
--6815dbc897af4706bd5a39f49b157928
Content-Disposition: form-data; name="filecontent"; filename="filecontent"
```

#### Response Packet

```
{
"code":0,
"message":"SUCCESS",
"request_id":"NTlhNDBhZGVfOTYyMjViNjRfMTc3Ml8yYWQ5NWU=",
"data":
{
"access_url":"http://bucket-appid.file.myqcloud.com/test1.jpg",
"resource_path":"/appid/bucket/test1.jpg",
"source_url":"http://bucket-appid.cosgz.myqcloud.com /test1.jpg",
"url":"http://gz.file.myqcloud.com/files/v2/appid/bucket/test1.jpg",
image_info:
{
      process_results:
  [ 
{
    "access_url":"http://bucket-appid.file.myqcloud.com/test2.png ",
"resource_path":"/appid/bucket/test2.png ",
"source_url":"http://bucket-appid.cosgz.myqcloud.com/test2.png ",
"url":"http://gz.file.myqcloud.com/files/v2/appid/bucket/test2.png ",
"vid":"value",
"file_id":"test2.png ",
"format":"PNG",
"height":50,
"width":200,
"size":100200
"watermark_status":100
}
]
}
}
```

>**Note:**
The filecontent field of the request packet is the image content of the watermarked image. In the rule field of the packet header Pic-Operations, imageUrl is the address of the original image without the blind watermark.
The url in the process_results field of the return packet is the address of the extracted watermark image.
