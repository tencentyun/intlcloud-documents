VOD provides an SDK for Python for uploading videos from a server. For more information on the upload process, please see [Guide](https://intl.cloud.tencent.com/document/product/266/33912).

## Integration Methods

### Installing by using pip
```
pip install vod-python-sdk
```

### Installing through source package
If pip is not used in your project, you can directly download the source code and import it into the project:

* [Access from GitHub](https://github.com/tencentyun/vod-python-sdk)
* Click [here](https://github.com/tencentyun/vod-python-sdk/archive/master.zip) to download the SDK for Python

Download the latest code and decompress:
```
$ cd vod-python-sdk
$ python setup.py install
```

## Simple Video Upload
### Initializing upload object
Initialize a `VodUploadClient` instance with a TencentCloud API key.

```
from qcloud_vod.vod_upload_client import VodUploadClient

client = VodUploadClient("your secretId", "your secretKey")
```

### Constructing upload request object
```
from qcloud_vod.model import VodUploadRequest

request = VodUploadRequest()
request.MediaFilePath = "/data/file/Wildlife.mp4"
```

### Calling upload method
Call the upload method and pass in the access point region and upload request.
```
try:
    response = client.upload("ap-guangzhou", request)
    print(response.FileId)
    print(response.MediaUrl)
except Exception as err:
    # Handle business exception
    print(err)
```

>?The upload method automatically selects simple upload or multipart upload based on the file size, eliminating your need to take care of every step in multipart upload.

## Advanced Features
### Uploading cover
```
from qcloud_vod.vod_upload_client import VodUploadClient
from qcloud_vod.model import VodUploadRequest

client = VodUploadClient("your secretId", "your secretKey")
request = VodUploadRequest()
request.MediaFilePath = "/data/file/Wildlife.mp4"
request.CoverFilePath = "/data/file/Wildlife-Cover.png"
try:
    response = client.upload("ap-guangzhou", request)
    print(response.FileId)
    print(response.MediaUrl)
    print(response.CoverUrl)
except Exception as err:
    # Handle business exception
    print(err)
```

### Specifying task flow
First, [create a task flow template](https://intl.cloud.tencent.com/document/product/266/14058) and name it. When initiating the task flow, you can set the `Procedure` parameter with the task flow template name, and the task flow will be executed automatically upon upload success.
```
from qcloud_vod.vod_upload_client import VodUploadClient
from qcloud_vod.model import VodUploadRequest

client = VodUploadClient("your secretId", "your secretKey")
request = VodUploadRequest()
request.MediaFilePath = "/data/file/Wildlife.mp4"
request.Procedure = "Your Procedure Name"
try:
    response = client.upload("ap-guangzhou", request)
    print(response.FileId)
    print(response.MediaUrl)
except Exception as err:
    # Handle business exception
    print(err)
```

### Uploading to subapplication
Pass in a [subapplication](https://intl.cloud.tencent.com/document/product/266/33987) ID. After the upload is successful, the resource will belong only to the specified subapplication.
```
from qcloud_vod.vod_upload_client import VodUploadClient
from qcloud_vod.model import VodUploadRequest

client = VodUploadClient("your secretId", "your secretKey")
request = VodUploadRequest()
request.MediaFilePath = "/data/file/Wildlife.mp4"
request.SubAppId = 101
try:
    response = client.upload("ap-guangzhou", request)
    print(response.FileId)
    print(response.MediaUrl)
except Exception as err:
    # Handle business exception
    print(err)
```

### Specifying storage region
In the [console](https://console.cloud.tencent.com/vod), confirm that the target storage region has been activated. If not, you can do so as instructed in [Upload Storage Settings](https://intl.cloud.tencent.com/document/product/266/18874) and then set the [abbreviation](https://intl.cloud.tencent.com/document/product/266/9760) of the storage region through the `StorageRegion` attribute.
```
from qcloud_vod.vod_upload_client import VodUploadClient
from qcloud_vod.model import VodUploadRequest

client = VodUploadClient("your secretId", "your secretKey")
request = VodUploadRequest()
request.MediaFilePath = "/data/file/Wildlife.mp4"
request.StorageRegion = "ap-chongqing"
try:
    response = client.upload("ap-guangzhou", request)
    print(response.FileId)
    print(response.MediaUrl)
except Exception as err:
    # Handle business exception
    print(err)
```

### Specifying the number of concurrent parts
The number of concurrent parts is applicable to uploading a large file in multiple parts simultaneously. The advantage of multipart upload lies in that a large file can be uploaded quickly. The SDK automatically selects simple upload or multipart upload based on the file size, eliminating your need to take care of every step in multipart upload. The number of concurrent parts of the file is specified by the `ConcurrentUploadNumber` parameter.
```
from qcloud_vod.vod_upload_client import VodUploadClient
from qcloud_vod.model import VodUploadRequest

client = VodUploadClient("your secretId", "your secretKey")
request = VodUploadRequest()
request.MediaFilePath = "/data/file/Wildlife.mp4"
request.ConcurrentUploadNumber = 5
try:
    response = client.upload("ap-guangzhou", request)
    print(response.FileId)
    print(response.MediaUrl)
except Exception as err:
    # Handle business exception
    print(err)
```

### Uploading with temporary credentials
Pass in the relevant key information of the temporary credentials to use the temporary credentials for authentication and upload.
```
from qcloud_vod.vod_upload_client import VodUploadClient
from qcloud_vod.model import VodUploadRequest

client = VodUploadClient("Credentials TmpSecretId", "Credentials TmpSecretKey", "Credentials Token")
request = VodUploadRequest()
request.MediaFilePath = "/data/file/Wildlife.mp4"
try:
    response = client.upload("ap-guangzhou", request)
    print(response.FileId)
    print(response.MediaUrl)
except Exception as err:
    # Handle business exception
    print(err)
```

### Uploading adaptive bitstream file

The adaptive bitstream formats supported by this SDK for upload include HLS and DASH, and the media files referenced by the `manifest` (M3U8 or MPD) must be relative paths (i.e., URLs and absolute paths cannot be used) and be located in the same-level directory or subdirectory of `manifest` (i.e., `../` cannot be used). When calling the SDK's upload APIs, enter the `manifest` path as the `MediaFilePath` parameter, and the SDK will parse the list of related media files and upload them together.

```
from qcloud_vod.vod_upload_client import VodUploadClient
from qcloud_vod.model import VodUploadRequest

client = VodUploadClient("your secretId", "your secretKey")
request = VodUploadRequest()
request.MediaFilePath = "/data/file/prog_index.mp4"
try:
    response = client.upload("ap-guangzhou", request)
    print(response.FileId)
    print(response.MediaUrl)
except Exception as err:
    # Handle business exception
    print(err)
```

## API Description
Upload client class `VodUploadClient`:

| Attribute Name | Attribute Description | Type | Required |
| --------- | ---------------------- | ------- | ---- |
| secretId | TencentCloud API key ID. | String | Yes |
| secretKey | TencentCloud API key. | String | Yes |

Upload request class `VodUploadRequest`:

| Attribute Name | Attribute Description | Type | Required |
| --------- | ---------------------- | ------- | ---- |
| MediaFilePath | Path of the media file to be uploaded, which must be a local path and does not support URLs. | String | Yes |
| SubAppId | ID of [subapplication](https://intl.cloud.tencent.com/document/product/266/33987) in VOD. If you need to access a resource in a subapplication, enter the subapplication ID in this field; otherwise, leave it empty. | Integer | No |
| MediaType | Type of the media file to be uploaded. For the valid values, please see [Overview](https://intl.cloud.tencent.com/document/product/266/9760) of media upload. If the `MediaFilePath` path contains a file extension, this parameter can be left empty. | String | No |
| MediaName | Name of the media file after being uploaded. If this parameter is left empty, the filename in `MediaFilePath` will be used by default. | String | No |
| CoverFilePath | Path of the cover file to be uploaded, which must be a local path and does not support URLs. | String | No |
| CoverType | Type of the cover file to be uploaded. For the valid values, please see [Overview](https://intl.cloud.tencent.com/document/product/266/9760) of media upload. If the `CoverFilePath` path contains a file extension, this parameter can be left empty. | String | No |
| Procedure | Name of the task flow to be automatically executed after upload is completed. This parameter is specified when the task flow is created through the [API](https://intl.cloud.tencent.com/document/product/266/33897) or [console](https://console.cloud.tencent.com/vod/video-process/taskflow). For more information, please see [Task Flow](https://intl.cloud.tencent.com/document/product/266/33931). | String | No |
| ExpireTime | Expiration time of media file in ISO 8601 format. For more information, please see [the notes on ISO date format](https://intl.cloud.tencent.com/document/product/266/11732). | String | No |
| ClassId | Category ID, which is used to categorize the media for management. A category can be created, and its ID can be obtained by using the [CreateClass](https://intl.cloud.tencent.com/document/product/266/35325) API. | Integer | No |
| SourceContext | Source context of up to 250 characters, which is used to pass through the user request information and will be returned by the upload callback API. | String | No |
| StorageRegion | Storage region, which specifies the region where to store the file. This field should be filled in with a [region abbreviation](https://intl.cloud.tencent.com/document/product/266/9760). | String | No |
| ConcurrentUploadNumber | Number of concurrent parts, which is valid when a large file is uploaded in multiple parts. | Integer | No |

Upload response class `VodUploadResponse`

| Attribute Name | Attribute Description | Type |
| --------- | ---------------------- | ------- |
| FileId | Unique ID of media file. | String |
| MediaUrl | Media playback address. | String |
| CoverUrl | Media cover address. | String |
| RequestId | Unique ID of request. Each request returns a unique ID. The `RequestId` is required to troubleshoot issues. | String  |

Upload method `VodUploadClient.upload(String region, VodUploadRequest request)`

| Parameter Name | Description | Type | Required |
| --------- | ---------------------- | ------- | ---- |
| region | Access point region, i.e., the region where to request a VOD server. This is different from the storage region. For more information, please see [the list of supported regions](https://intl.cloud.tencent.com/document/product/266/34113). | String | Yes |
| request | Upload request. | VodUploadRequest | Yes |

## Error Codes

| Status Code | Description |
| ----------- | ----------------- |
| InternalError | Internal error. |
| InvalidParameter.ExpireTime | Incorrect parameter value: expiration time. |
| InvalidParameterValue.CoverType | Incorrect parameter value: cover type. |
| InvalidParameterValue.MediaType | Incorrect parameter value: media type. |
| InvalidParameterValue.SubAppId | Incorrect parameter value: subapplication ID. |
| InvalidParameterValue.VodSessionKey | Incorrect parameter value: VOD session. |
| ResourceNotFound | The resource does not exist. |
