## Overview

Image compression is the process of downsizing an image as much as possible without sacrificing quality so that it can be stored at a lower cost and accessed more quickly.

[CI](https://intl.cloud.tencent.com/document/product/1045/33422) has launched the SVG compression feature, which can delete certain redundant information from an SVG file without compromising the display effect in order to downsize the file.

## Restrictions

- Format: Only SVG images can be used as the input.
- Size: The input image cannot be larger than 32 MB.

## Directions

CI uses the `imageMogr2` API to provide the SVG compression feature.

An image can be processed:

- Upon download
- Upon upload
- In cloud

>?  SVG compression is billed at image advanced compression prices. For detailed pricing, see [Image Processing Fees](https://intl.cloud.tencent.com/document/product/1045/45582).
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

>? `Pic-Operations` is a JSON string. Its parameters are as described in [Persistent Image Processing](https://intl.cloud.tencent.com/document/product/1045/33695).
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
> - Authorization: Auth String (See [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for details.)
> - When this feature is used by a sub-account, relevant permissions must be granted as instructed in [Authorization Granularity Details](https://intl.cloud.tencent.com/document/product/1045/49896).
>

## Parameters

| Parameter | Description |
| :------------------ | :----------------------------------------------------------- |
| ObjectKey  | Object name, such as `folder/sample.jpg`.                           | 
| /format/&lt;Format> | Compression format, which is `svgc` here.                                       |
