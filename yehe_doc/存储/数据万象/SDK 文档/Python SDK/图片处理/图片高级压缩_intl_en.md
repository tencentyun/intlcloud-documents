

## Overview

This document provides an overview of APIs and SDK code samples for image advanced compression.

| API | Description    |
| ------------------------------------------------------------ | -------- |
| [Image advanced compression](https://intl.cloud.tencent.com/document/product/1045/40108) |   Compresses an image in a specified bucket.   |

## Image Advanced Compression

#### Feature description

CI uses the `imageMogr2` API to provide the image advanced compression feature.

#### Method prototype

```
ci_download_compress_image(self, Bucket, Key, DestImagePath, CompressType, **kwargs)
```

#### Sample request

[//]: #	".cssg-snippet-ci-download-compress-image"

```py
# TPG compression
response = client.ci_download_compress_image(
    Bucket='examplebucket-1250000000',
    Key='sample.png',
    DestImagePath='sample.tpg',
    CompressType='tpg'
)

# HEIF compression
response = client.ci_download_compress_image(
    Bucket='examplebucket-1250000000',
    Key='sample.png',
    DestImagePath='sample.heif',
    CompressType='heif'
)
```

#### Parameter description

| Parameter | Description | Type | Required |
| ------------- | ------------------------------------------------------------ | ------ | -------- |
| Bucket        | Bucket name in the format of `BucketName-APPID`. For more information, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312). | String | Yes |
| Key | Object key. It can contain up to 128 bytes of letters, digits, spaces, plus signs, minus signs, underscores, equal signs, dots, colons, and slashes. | String | Yes |
| DestImagePath | Local path to save the compressed image                                 | String | Yes       |
| CompressType  | Compression format, which can be TPG or HEIF.                                   | String | Yes       |

#### Response description

This API returns the response header.
