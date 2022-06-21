

## Overview

This document provides an overview of APIs and SDK code samples for blind watermarking.

| API | Description |
| ------------------------------------------------------------ | ---------------------------------------- |
| Blind watermarking | Adds blind watermark to or extracts blind watermark from local image and uploads it to bucket |

## Blind Watermark

#### Feature description

Blind watermark is a new type of watermark based on CI.

#### Method prototype

```
def ci_put_object_from_local_file(self, Bucket, LocalFilePath, Key, EnableMD5=False, **kwargs)
```

#### Sample request

[//]: #	".cssg-snippet-ci-put-object-from-local-file"

```py
# Add a blind watermark
watermark_url = 'http://{bucket}.cos.{region}.myqcloud.com/watermark.png'.format(bucket='examplebucket-1250000000', region=region)
watermark_url_base64 = bytes.decode(base64.b64encode(str.encode(watermark_url)))
print(watermark_url_base64)
response, data = client.ci_put_object_from_local_file(
    Bucket='examplebucket-1250000000',
    LocalFilePath='sample.png',
    Key="sample.png",
    # pic operation json struct
    PicOperations='{"is_pic_info":1,"rules":[{"fileid": "format.png","rule": "watermark/3/type/1/image/' +
                  watermark_url_base64 + '" }]}'
)

# Extract a blind watermark
sample_url = 'http://{bucket}.cos.{region}.myqcloud.com/sample.png'.format(bucket='examplebucket-1250000000', region=region)
sample_url_base64 = bytes.decode(base64.b64encode(str.encode(sample_url)))
response, data = client.ci_put_object_from_local_file(
    Bucket='examplebucket-1250000000',
    LocalFilePath='format.png',
    Key="format.png",
    # pic operation json struct
    PicOperations='{"is_pic_info":1,"rules":[{"fileid": "watermark.png","rule": "watermark/4/type/1/image/' +
                  sample_url_base64 + '" }]}'
)
```

#### Parameter description

| Parameter | Description | Type | Required |
| ------------- | ------------------------------------------------------------ | ------ | -------- |
| Bucket        | Bucket name in the format of `BucketName-APPID`. For more information, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312). | String | Yes |
| LocalFilePath | Path of the local image to be processed                                       | String | Yes       |
| Key | Object key. It can contain up to 128 bytes of letters, digits, spaces, plus signs, minus signs, underscores, equal signs, dots, colons, and slashes. | String | Yes |
| EnableMD5     | Enables MD5 check for uploaded objects                                      | Bool   | No       |

#### Response description

This API returns the response header and body.
