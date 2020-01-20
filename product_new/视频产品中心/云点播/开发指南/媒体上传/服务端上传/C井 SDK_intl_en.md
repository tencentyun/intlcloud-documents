VOD provides an SDK for C# for uploading videos from a server. For more information on the upload process, please see [Upload Videos from Server](https://intl.cloud.tencent.com/document/product/266/33912).

## Integration Steps

### Installing via NuGet
1. Install on the command line:
```
dotnet add package VodSDK --version 1.0.1
```
2. Search for VodSDK in Visual Studio's NuGet package manager and install it.

### Installing using source package
If your project does not have NuGet, you can directly download the source code and import it into the project:

* [Access from GitHub](https://github.com/tencentyun/vod-dotnet-sdk)
* Click [here](https://github.com/tencentyun/vod-dotnet-sdk/archive/master.zip) to download the SDK for C#

Download the latest code, decompress and install it in your project's working directory, and open it with Visual Studio 2017 for compiling. As this SDK also depends on external packages, the following SDKs need to be installed too: 
- [TencentCloud API SDK](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)
- [COS SDK](https://github.com/tencentyun/qcloud-sdk-dotnet)

## Simple Upload
### Initializing upload client object
Initialize a `VodUploadClient` instance with a TencentCloud API key.
```
using System;
using VodSDK;

VodUploadClient client = new VodUploadClient("your secretId", "your secretKey");
```

### Constructing upload request object
Set the local media upload path.
```
VodUploadRequest request = new VodUploadRequest();
request.MediaFilePath = "/data/videos/Wildlife.wmv";
```

### Calling upload
Call the upload method and pass in the access point region and upload request.
```
try 
{
    VodUploadResponse response = client.Upload("ap-guangzhou", request);
    // Print the media FileId
    Console.WriteLine(response.FileId);
} 
catch (Exception e) 
{
    // The business team performs troubleshooting
    Console.WriteLine(e);
}
```

>The upload method automatically selects simple upload or multipart upload based on the file size, eliminating your need to take care of every step in multipart upload.

## Advanced Features
### Uploading a cover
```
using System;
using VodSDK;

VodUploadClient client = new VodUploadClient("your secretId", "your secretKey");
VodUploadRequest request = new VodUploadRequest();
request.MediaFilePath = "/data/videos/Wildlife.wmv";
request.CoverFilePath = "/data/videos/Wildlife.jpg";
try 
{
    VodUploadResponse response = client.Upload("ap-guangzhou", request);
    // Print the media FileId
    Console.WriteLine(response.FileId);
} 
catch (Exception e) 
{
    // The business team performs troubleshooting
    Console.WriteLine(e);
}
```

### Specifying a task flow
First, [create a task flow template](https://intl.cloud.tencent.com/document/product/266/14058) and name it. When initiating the task flow, you can set the `Procedure` parameter with the task flow template name, and the task flow will be executed automatically upon upload success.
```
using System;
using VodSDK;

VodUploadClient client = new VodUploadClient("your secretId", "your secretKey");
VodUploadRequest request = new VodUploadRequest();
request.MediaFilePath = "/data/videos/Wildlife.wmv";
request.Procedure = "Your Procedure Name";
try 
{
    VodUploadResponse response = client.Upload("ap-guangzhou", request);
    // Print the media FileId
    Console.WriteLine(response.FileId);
} 
catch (Exception e) 
{
    // The business team performs troubleshooting
    Console.WriteLine(e);
}
```

### Uploading to a subapplication
Pass in a [subapplication](https://intl.cloud.tencent.com/document/product/266/33987) ID. After the upload is successful, the resource will belong only to the specified subapplication.
```
using System;
using VodSDK;

VodUploadClient client = new VodUploadClient("your secretId", "your secretKey");
VodUploadRequest request = new VodUploadRequest();
request.MediaFilePath = "/data/videos/Wildlife.wmv";
request.SubAppId = 101;
try 
{
    VodUploadResponse response = client.Upload("ap-guangzhou", request);
    // Print the media FileId
    Console.WriteLine(response.FileId);
} 
catch (Exception e) 
{
    // The business team performs troubleshooting
    Console.WriteLine(e);
}
```

### Specifying a storage region
In the [console](https://console.cloud.tencent.com/vod), confirm that the target storage region has been activated. If not, you can do so as instructed in [Upload Storage Settings](https://intl.cloud.tencent.com/document/product/266/18874) and then set the [abbreviation](https://intl.cloud.tencent.com/document/product/266/33910) of the storage region through the `StorageRegion` attribute.
```
using System;
using VodSDK;

VodUploadClient client = new VodUploadClient("your secretId", "your secretKey");
VodUploadRequest request = new VodUploadRequest();
request.MediaFilePath = "/data/videos/Wildlife.wmv";
request.StorageRegion = "ap-chongqing";
try 
{
    VodUploadResponse response = client.Upload("ap-guangzhou", request);
    // Print the media FileId
    Console.WriteLine(response.FileId);
} 
catch (Exception e) 
{
    // The business team performs troubleshooting
    Console.WriteLine(e);
}
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
| MediaFilePath | Path to the media file to be uploaded, which must be a local path and does not support URLs. | String | Yes |
| MediaType | Type of the media file to be uploaded. For the valid values, please see [Video Upload Overview](/document/product/266/9760#.E6.96.87.E4.BB.B6.E7.B1.BB.E5.9E.8B). If the `MediaFilePath` path contains a file extension, this parameter can be left empty. | String | No |
| MediaName | Name of the media file after being uploaded. If this parameter is left empty, the filename in `MediaFilePath` will be used by default. | String | No |
| CoverFilePath | Path to the cover file to be uploaded, which must be a local path and does not support URLs. | String | No |
| CoverType | Type of the cover file to be uploaded. For the valid values, please see [Video Upload Overview](/document/product/266/9760#.E5.B0.81.E9.9D.A2.E7.B1.BB.E5.9E.8B). If the `CoverFilePath` path contains a file extension, this parameter can be left empty. | String | No |
| Procedure | Name of the task flow to be automatically executed after upload is completed. This parameter is specified when the task flow is created through the [API](/document/product/266/33897) or [console](https://console.cloud.tencent.com/vod/video-process/taskflow). For more information, please see [Task Flow Overview](https://intl.cloud.tencent.com/document/product/266/33931#.E4.BB.BB.E5.8A.A1.E6.B5.81). | String | No |
| ExpireTime | Expiration time of the media file in ISO 8601 format. For more information, please see [Notes on ISO Date Format](https://intl.cloud.tencent.com/document/product/266/11732#iso-.E6.97.A5.E6.9C.9F.E6.A0.BC.E5.BC.8F). | String | No |
| ClassId | Category ID, which is used to categorize the media for management. A category can be created and its ID can be obtained by using the [category creating](/document/product/266/31772) API. | Integer | No |
| SourceContext | Source context of up to 250 characters, which is used to pass through the user request information and will be returned by the upload callback API. | String | No |
| SubAppId | ID of a [subapplication](https://intl.cloud.tencent.com/document/product/266/33987) in VOD. If you need to access a resource in a subapplication, enter the subapp ID in this field; otherwise, leave it empty. | Integer | No |
| StorageRegion | Storage region, which specifies the region where to store the file. This field should be filled in with a [region abbreviation](https://intl.cloud.tencent.com/document/product/266/33910). | String | No |

Upload response class `VodUploadResponse`

| Attribute Name | Attribute Description | Type |
| --------- | ---------------------- | ------- |
| FileId | Unique ID of the media file. | String |
| MediaUrl | Media playback address. | String |
| CoverUrl | Media cover address. | String |
| RequestId | Unique ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. | String |

Upload method `VodUploadClient.Upload(String region, VodUploadRequest request)`

| Parameter Name | Description | Type | Required |
| --------- | ---------------------- | ------- | ---- |
| region | Access point region, i.e., the region where to request a VOD server. This is different from the storage region. For more information, please see [the list of supported regions](/document/api/266/31756#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8). | String | Yes |
| request | Upload request. | VodUploadRequest | Yes |

## Error Codes
| Status Code | Description |
| ----------- | ----------------- |
| InternalError | Internal error. |
| InvalidParameter.ExpireTime | Incorrect parameter value: Expiration time. |
| InvalidParameterValue.CoverType | Incorrect parameter value: Cover type. |
| InvalidParameterValue.MediaType | Incorrect parameter value: Media type. |
| InvalidParameterValue.SubAppId | Incorrect parameter value: Subapplicationp ID. |
| InvalidParameterValue.VodSessionKey | Incorrect parameter value: VOD session. |
| ResourceNotFound | The resource does not exist. |
