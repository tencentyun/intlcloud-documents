## Feature Description

Image compression is the process of downsizing an image as much as possible without sacrificing quality so that it can be stored at a lower cost and accessed more quickly.

COS launched the WebP compression feature based on [CI](https://intl.cloud.tencent.com/document/product/1045/33422) to convert images to .webp format, which is superior to .jpg in terms of compression. A .webp image is over 25% smaller than a .jpg image with the same quality. This format is suitable for multi-terminal use cases.

## Restrictions

- Format: Images in JPG, PNG, BMP, GIF, HEIF, or AVIF format can be converted to WebP format.
- Size: The input image cannot be larger than 32 MB, with its width and height not exceeding 30,000 pixels respectively, and the total number of pixels not exceeding 250 million. The width and height of the output image cannot exceed 9,999 pixels respectively. For an animated input image, the total number of pixels (width * height * number of frames) cannot exceed 250 million.
- Frames (for animated images): For GIF images, the number of frames cannot exceed 300.

## Directions

COS uses CI's `imageMogr2` API to provide the WebP compression feature.

This feature supports processing:

- During download
- During upload
- In the cloud

>?
>- WebP compression is a paid service charged by CI at the basic image processing prices. For detailed pricing, see [Image Processing Fees](https://intl.cloud.tencent.com/document/product/1045/45582).
>- If an image is converted to WebP format, some browsers may not be able to read its EXIF data. As a result, the image cannot be rotated. You can add the `auto-orient` parameter to rotate the input image first before compressing it (see [Rotation](https://intl.cloud.tencent.com/document/product/436/36368)) .
>- WebP compression inherits the quality parameters of the input image by default. You can adjust the compression ratio by modifying the image quality as instructed in [Quality Change](https://intl.cloud.tencent.com/document/product/436/36370).
>



## API Sample

#### 1. Processing during download

```plaintext
GET /<ObjectKey>?imageMogr2/format/webp HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: <GMT Date>
Authorization: <Auth String>
```

#### 2. Processing during upload

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
    "rule": "imageMogr2/format/webp"
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
    "rule": "imageMogr2/format/webp"
}]
}
```

>? 
> - Authorization: Auth String (for more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778)).
> - When this feature is used by a sub-account, relevant permissions must be granted. For more information, see [Authorization Granularity Details](https://intl.cloud.tencent.com/document/product/1045/49896).



## Parameters

| Parameter | Description |
| :--------------- | :----------------------------------------------------------- |
| ObjectKey  | Object name, such as `folder/sample.jpg`.                           |
| /format/&lt;Format> | Compression format, which is `webp` here.                             |

## Samples

>? **Processing during download** is used as an example here, which does not store the output image in a bucket. If you need to store the output image, use **processing during upload** or **processing in-cloud data** instead.
>

Assume the input image is a 1,335.2 KB image in PNG format.
![img](https://example-1258125638.cos.ap-shanghai.myqcloud.com/sample.png)

You can convert the image to WebP format by using the following request URL:

```plaintext
http://example-1258125638.cos.ap-shanghai.myqcloud.com/sample.png?imageMogr2/format/webp
```

Output:
![img](https://example-1258125638.cos.ap-shanghai.myqcloud.com/sample.png?imageMogr2/format/webp)

**Compression ratio comparison**

| Format | Image Size |
| :---------- | :------------------- |
| PNG (input image) | 1,335.2 KB |
| WebP | 65 KB (compression ratio: 95.13%) |
