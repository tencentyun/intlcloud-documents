## Overview

This document provides an overview of APIs and SDK code samples for image QR codes.


| API | Description |
| ------------------------------------------ | -------------------------- |
| QR code recognition | Recognizes the location and content of valid QR codes in an image, outputs the text information (URL or text) contained in the QR codes, and pixelates the recognized QR codes. |


## QR Code Recognition

The QR code recognition feature recognizes the location and content of valid QR codes in an image, outputs the text information (URL or text) contained in the QR codes, and pixelates the recognized QR codes.

### Recognizing QR code during upload

#### Feature description

The request for recognizing QR codes during image upload is the same as that used to simply upload a file to COS, except that you need to add the image processing parameter `Pic-Operations` to the request header.

#### Sample code

```shell
    # Create a COS client
    example_object = 'example_object.jpg'
    with open(example_object, 'rb') as fp:
        opts = '{"is_pic_info":1,"rules":[{"fileid":"format.jpg","rule":"QRcode/cover/0"}]}'
        response,data = client.ci_put_object_from_local_file_and_get_qrcode(
            Bucket='example-bucket-123456789',
            LocalFilePath=example_object,
            Key='example_key',
            EnableMD5=False,
            PicOperations=opts
        )
        # View the response information and read the specified data as needed
        print(response,data)
```

#### Parameter description

| Parameter | Description | Type | Required |
| ------------------ | ------------------------------------------------------------ | ---------- | -------- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| LocalFilePath      | Image path                         | String | Yes       |
| Key  | Unique identifier of the object in the bucket. For example, if an object's access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its key is `doc/pic.jpg`. | String  |   Yes |
| EnableMD5 | Specifies whether the SDK needs to calculate the `Content-MD5` checksum. It is disabled by default. The upload will take longer if it is enabled. | Bool | No |
| PicOperations      | CI image processing parameters. For more information, see QR Code Recognition. | String     | Yes       |


### Recognizing QR code in the cloud

#### Feature description

This feature recognizes QR codes in an image stored in the cloud and returns the recognition result.

#### Sample code

```shell
    # Create a COS client
    response,data = client.ci_get_object_qrcode(
        Bucket='example_bucket-123456789',
        Key='example_object',
        Cover=0
    )
    # View the response information and read the specified data as needed
    print(response,data)
```

#### Parameter description

| Parameter | Description | Type | Required |
| ------------------ | ------------------------------------------------------------ | ---------- | -------- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Key  | Unique identifier of the object in the bucket. For example, if an object's access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its key is `doc/pic.jpg`. | String  |   Yes |
| Cover              | Whether to pixelate QR codes. For more information, see QR Code Recognition. | Int     | Yes       |

