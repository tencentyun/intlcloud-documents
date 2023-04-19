## Feature Overview

Image compression is the process of downsizing an image as much as possible without sacrificing quality so that it can be stored at a lower cost and accessed more quickly.

Based on [CI](https://www.tencentcloud.com/document/product/1045/33422), COS provides the SVG compression feature, which can delete certain redundant information from an SVG file without compromising the display effect in order to downsize the file.

## Restrictions

- Format: Only SVG images can be used as the input.
- Size: The input image cannot be larger than 32 MB.

## Directions

COS provides the SVG compression feature using CI's `imageMogr2` API.

An image can be processed:

- Upon download
- Upon upload
- In cloud

>? SVG Compression is charged by CI at image advanced compression rates. For detailed pricing, see [Image Processing Fees](https://www.tencentcloud.com/document/product/1045/45582).
>


## API Format

#### 1. Processing upon download

```plaintext
GET /<ObjectKey>?imageMogr2/format/svgc HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: <GMT Date>
Authorization: <Auth String>
```

#### 2. Processing upon upload

```http
PUT /<ObjectKey> HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
Pic-Operations: 
{
"is_pic_info": 1,
"rules": [{
    "fileid": "exampleobject",
    "rule": "imageMogr2/format/svgc"
}]
}
```

>? `Pic-Operations` is a JSON string. Its parameters are as described in [Persistent Image Processing](https://www.tencentcloud.com/document/product/1045/33695).
>

#### 3. Processing in-cloud data

```http
POST /<ObjectKey>?image_process HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Content-length: Size
Authorization: Auth String
Pic-Operations: 
{
"is_pic_info": 1,
"rules": [{
    "fileid": "exampleobject",
    "rule": "imageMogr2/format/svgc"
}]
}
```

>? 
> Authorization: Auth String. For more information, see [Request Signature](https://www.tencentcloud.com/document/product/436/7778).
> - When this feature is used by a sub-account, relevant permissions must be granted as instructed in [Authorization Granularity Details](https://www.tencentcloud.com/document/product/1045/49896).
>

## Parameters

| Parameter | Description |
| :------------------ | :----------------------------------------------------------- |
| ObjectKey  | Object name, such as `folder/sample.jpg`.                           |
| /format/&lt;Format> | Compression format, which is `svgc`                             |

