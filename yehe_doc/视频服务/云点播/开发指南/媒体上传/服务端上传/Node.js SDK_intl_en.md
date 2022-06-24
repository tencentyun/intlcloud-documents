VOD provides an SDK for Node.js for uploading videos from a server. For more information on the upload process, please see [Guide](https://intl.cloud.tencent.com/document/product/266/33912).

## Integration Methods

### Installing by using npm
```
npm i vod-node-sdk --save
```

### Installing through source package
If the npm tool is not used for dependency management in the project, you can download the source code and import it into the project:

* [Access from GitHub](https://github.com/tencentyun/vod-node-sdk)
* Click [here](https://github.com/tencentyun/vod-node-sdk/archive/master.zip) to download the SDK for Node.js

## Simple Video Upload
### Initializing upload object
Initialize a `VodUploadClient` instance with a TencentCloud API key.

```
const { VodUploadClient, VodUploadRequest } = require('vod-node-sdk');

client = new VodUploadClient("your secretId", "your secretKey");
```

### Constructing upload request object
```
let req = new VodUploadRequest();
req.MediaFilePath = "/data/file/Wildlife.mp4";
```

### Calling upload method
Call the upload method, pass in the access point region and upload request, and get the returned information through the callback.
```
client.upload("ap-guangzhou", req, function (err, data) {
    if (err) {
        // Handle business exception
        console.log(err)
    } else {
        // Get information after successful upload
        console.log(data.FileId);
        console.log(data.MediaUrl);
    }
});
```

>?The upload method automatically selects simple upload or multipart upload based on the file size, eliminating your need to take care of every step in multipart upload.

## Advanced Features
### Uploading cover
```
const { VodUploadClient, VodUploadRequest } = require('vod-node-sdk');

client = new VodUploadClient("your secretId", "your secretKey");
let req = new VodUploadRequest();
req.MediaFilePath = "/data/file/Wildlife.mp4";
req.CoverFilePath = "/data/file/Wildlife-cover.png";
client.upload("ap-guangzhou", req, function (err, data) {
    if (err) {
        // Handle business exception
        console.log(err)
    } else {
        // Get information after successful upload
        console.log(data.FileId);
        console.log(data.MediaUrl);
        console.log(data.CoverUrl);
    }
});
```

### Specifying task flow
First, [create a task flow template](https://intl.cloud.tencent.com/document/product/266/14058) and name it. When initiating the task flow, you can set the `Procedure` parameter with the task flow template name, and the task flow will be executed automatically upon upload success.
```
const { VodUploadClient, VodUploadRequest } = require('vod-node-sdk');

client = new VodUploadClient("your secretId", "your secretKey");
let req = new VodUploadRequest();
req.MediaFilePath = "/data/file/Wildlife.mp4";
req.Procedure = "Your Procedure Name";
client.upload("ap-guangzhou", req, function (err, data) {
    if (err) {
        // Handle business exception
        console.log(err)
    } else {
        // Get information after successful upload
        console.log(data.FileId);
        console.log(data.MediaUrl);
    }
});
```

### Uploading to subapplication
Pass in a [subapplication](https://intl.cloud.tencent.com/document/product/266/33987) ID. After the upload is successful, the resource will belong only to the specified subapplication.
```
const { VodUploadClient, VodUploadRequest } = require('vod-node-sdk');

client = new VodUploadClient("your secretId", "your secretKey");
let req = new VodUploadRequest();
req.MediaFilePath = "/data/file/Wildlife.mp4";
req.SubAppId = 101;
client.upload("ap-guangzhou", req, function (err, data) {
    if (err) {
        // Handle business exception
        console.log(err)
    } else {
        // Get information after successful upload
        console.log(data.FileId);
        console.log(data.MediaUrl);
    }
});
```

### Specifying storage region
In the [console](https://console.cloud.tencent.com/vod), confirm that the target storage region has been activated. If not, you can do so as instructed in [Upload Storage Settings](https://intl.cloud.tencent.com/document/product/266/18874) and then set the [abbreviation](https://intl.cloud.tencent.com/document/product/266/9760) of the storage region through the `StorageRegion` attribute.
```
const { VodUploadClient, VodUploadRequest } = require('vod-node-sdk');

client = new VodUploadClient("your secretId", "your secretKey");
let req = new VodUploadRequest();
req.MediaFilePath = "/data/file/Wildlife.mp4";
req.StorageRegion = "ap-chongqing";
client.upload("ap-guangzhou", req, function (err, data) {
    if (err) {
        // Handle business exception
        console.log(err)
    } else {
        // Get information after successful upload
        console.log(data.FileId);
        console.log(data.MediaUrl);
    }
});
```

### Uploading with temporary credentials
Pass in the relevant key information of the temporary credentials to use the temporary credentials for authentication and upload.
```
const { VodUploadClient, VodUploadRequest } = require('vod-node-sdk');

client = new VodUploadClient("Credentials TmpSecretId", "Credentials TmpSecretKey", "Credentials Token");
let req = new VodUploadRequest();
req.MediaFilePath = "/data/file/Wildlife.mp4";
client.upload("ap-guangzhou", req, function (err, data) {
    if (err) {
        // Handle business exception
        console.log(err)
    } else {
        // Get information after successful upload
        console.log(data.FileId);
        console.log(data.MediaUrl);
    }
});
```

### Uploading adaptive bitstream file

The adaptive bitstream formats supported by this SDK for upload include HLS and DASH, and the media files referenced by the `manifest` (M3U8 or MPD) must be relative paths (i.e., URLs and absolute paths cannot be used) and be located in the same-level directory or subdirectory of `manifest` (i.e., `../` cannot be used). When calling the SDK's upload APIs, enter the `manifest` path as the `MediaFilePath` parameter, and the SDK will parse the list of related media files and upload them together.

```
const { VodUploadClient, VodUploadRequest } = require('vod-node-sdk');

client = new VodUploadClient("your secretId", "your secretKey");
let req = new VodUploadRequest();
req.MediaFilePath = "/data/file/prog_index.m3u8";
client.upload("ap-guangzhou", req, function (err, data) {
    if (err) {
        // Handle business exception
        console.log(err)
    } else {
        // Get information after successful upload
        console.log(data.FileId);
        console.log(data.MediaUrl);
    }
});
```

## API Description
Upload client class `VodUploadClient`

| Attribute Name | Attribute Description | Type | Required |
| --------- | ---------------------- | ------- | ---- |
| secretId | TencentCloud API key ID. | String | Yes |
| secretKey | TencentCloud API key. | String | Yes |

Upload request class `VodUploadRequest`

| Attribute Name | Attribute Description | Type | Required |
| --------- | ---------------------- | ------- | ---- |
| MediaFilePath | Path of the media file to be uploaded, which must be a local path (i.e., a path on your server) and does not support URLs. | String | Yes |
| SubAppId | ID of [subapplication](https://intl.cloud.tencent.com/document/product/266/33987) in VOD. If you need to access a resource in a subapplication, enter the subapplication ID in this field; otherwise, leave it empty. | Integer | No |
| MediaType | Type of the media file to be uploaded. For the valid values, please see [Overview](https://intl.cloud.tencent.com/document/product/266/9760) of media upload. If the `MediaFilePath` path contains a file extension, this parameter can be left empty. | String | No |
| MediaName | Name of the media file after being uploaded. If this parameter is left empty, the filename in `MediaFilePath` will be used by default. | String | No |
| CoverFilePath | Path of the cover file to be uploaded, which must be a local path (i.e., a path on your server) and does not support URLs. | String | No |
| CoverType | Type of the cover file to be uploaded. For the valid values, please see [Overview](https://intl.cloud.tencent.com/document/product/266/9760) of media upload. If the `CoverFilePath` path contains a file extension, this parameter can be left empty. | String | No |
| Procedure | Name of the task flow to be automatically executed after upload is completed. This parameter is specified when the task flow is created through the [API](https://intl.cloud.tencent.com/zh/document/product/266/33897) or [console](https://console.cloud.tencent.com/vod/video-process/taskflow). For more information, please see [Task Flow](https://intl.cloud.tencent.com/document/product/266/33931). | String | No |
| ExpireTime | Expiration time of media file in ISO 8601 format. For more information, please see [the notes on ISO date format](https://intl.cloud.tencent.com/document/product/266/11732). | String | No |
| ClassId | Category ID, which is used to categorize the media for management. A category can be created, and its ID can be obtained by using the [CreateClass](https://intl.cloud.tencent.com/document/product/266/35325) API. | Integer | No |
| SourceContext | Source context of up to 250 characters, which is used to pass through the user request information and will be returned by the upload callback API. | String | No |
| StorageRegion | Storage region, which specifies the region where to store the file. This field should be filled in with a [region abbreviation](https://intl.cloud.tencent.com/document/product/266/9760). | String | No |

Upload response class `VodUploadResponse`

| Attribute Name | Attribute Description | Type |
| --------- | ---------------------- | ------- |
| FileId | Unique ID of media file. | String |
| MediaUrl | Media playback address. | String |
| CoverUrl | Media cover address. | String |
| RequestId | Unique ID of request. Each request returns a unique ID. The `RequestId` is required to troubleshoot issues. | String  |

Upload method `VodUploadClient.upload(String region, VodUploadRequest request, function callback)`

| Parameter Name | Description | Type | Required |
| --------- | ---------------------- | ------- | ---- |
| region | Access point region, i.e., the region where to request a VOD server. This is different from the storage region. For more information, please see [the list of supported regions](https://intl.cloud.tencent.com/document/product/266/34113). | String | Yes |
| request | Upload request. | VodUploadRequest | Yes |
| callback   | Upload completion callback function. | function | Yes  |

Upload completion callback function `function(err, data)`

| Parameter Name | Description | Type | Required |
| --------- | ---------------------- | ------- | ---- |
| err   | Error message.       | Exception | Yes    |
| data | Upload response result. | VodUploadResponse | Yes |

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
