VOD provides an SDK for PHP for uploading videos from a server. For more information on the upload process, please see [Upload Videos from Server](/document/product/266/9759).

## Integration Steps

### Importing by using composer
```json
{
    "require": {
        "qcloud/vod-sdk-v5": "v2.2.0"
    }
}
```

### Installing by using source package
If your project does not use Composer for dependency management, you can directly download the source code and import it into the project:

* [Access from GitHub](https://github.com/tencentyun/vod-php-sdk-v5)
* Click [here](https://github.com/tencentyun/vod-php-sdk-v5/raw/master/packages/vod-sdk.zip) to download the SDK for PHP

Decompress the vod-sdk.zip file into the project and import the autoload.php file.

## Simple Video Upload
### Initializing upload object
Initialize a `VodUploadClient` instance with a TencentCloud API key.

**Import by using composer**
```
<?php
require 'vendor/autoload.php';

use Vod\VodUploadClient;

$client = new VodUploadClient("your secretId", "your secretKey");
```

**Import by using source code**
```php
<?php
require 'vod-sdk-v5/autoload.php';

use Vod\VodUploadClient;

$client = new VodUploadClient("your secretId", "your secretKey");
```

### Constructing upload request object
```
use Vod\Model\VodUploadRequest;

$req = new VodUploadRequest();
$req->MediaFilePath = "/data/videos/Wildlife.wmv";
```

### Calling upload
Call the upload method and pass in the access point region and upload request.
```
try {
    $rsp = $client->upload("ap-guangzhou", $req);
    echo "FileId -> ". $rsp->FileId . "\n";
    echo "MediaUrl -> ". $rsp->MediaUrl . "\n";
} catch (Exception $e) {
    // Handle upload exception
    echo $e;
}
```

>The upload method automatically selects simple upload or multipart upload based on the file size, eliminating your need to take care of every step in multipart upload.

## Advanced Features
### Uploading a cover
```
<?php
require 'vendor/autoload.php';

use Vod\VodUploadClient;
use Vod\Model\VodUploadRequest;

$client = new VodUploadClient("your secretId", "your secretKey");
$req = new VodUploadRequest();
$req->MediaFilePath = "/data/videos/Wildlife.wmv";
$req->CoverFilePath = "/data/videos/Wildlife-Cover.png";
try {
    $rsp = $client->upload("ap-guangzhou", $req);
    echo "FileId -> ". $rsp->FileId . "\n";
    echo "MediaUrl -> ". $rsp->MediaUrl . "\n";
    echo "CoverUrl -> ". $rsp->CoverUrl . "\n";
} catch (Exception $e) {
    // Handle upload exception
    echo $e;
}
```

### Specifying a task flow
First, [create a task flow template](https://cloud.tencent.com/document/product/266/33819) and name it. When initiating the task flow, you can set the `Procedure` parameter with the task flow template name, and the task flow will be executed automatically upon upload success.
```
<?php
require 'vendor/autoload.php';

use Vod\VodUploadClient;
use Vod\Model\VodUploadRequest;

$client = new VodUploadClient("your secretId", "your secretKey");
$req = new VodUploadRequest();
$req->MediaFilePath = "/data/videos/Wildlife.wmv";
$req->Procedure = "Your Procedure Name";
try {
    $rsp = $client->upload("ap-guangzhou", $req);
    echo "FileId -> ". $rsp->FileId . "\n";
    echo "MediaUrl -> ". $rsp->MediaUrl . "\n";
} catch (Exception $e) {
    // Handle upload exception
    echo $e;
}
```

### Uploading to a subapplication
Pass in a [subapplication](/document/product/266/14574) ID. After the upload is successful, the resource will belong only to the specified subapplication.
```
<?php
require 'vendor/autoload.php';

use Vod\VodUploadClient;
use Vod\Model\VodUploadRequest;

$client = new VodUploadClient("your secretId", "your secretKey");
$req = new VodUploadRequest();
$req->MediaFilePath = "/data/videos/Wildlife.wmv";
$req->SubAppId = 101;
try {
    $rsp = $client->upload("ap-guangzhou", $req);
    echo "FileId -> ". $rsp->FileId . "\n";
    echo "MediaUrl -> ". $rsp->MediaUrl . "\n";
} catch (Exception $e) {
    // Handle upload exception
    echo $e;
}
```

### Specifying a storage region
In the [console](https://console.cloud.tencent.com/vod), confirm that the target storage region has been activated. If not, you can do so as instructed in [Upload Storage Settings](/document/product/266/14059) and then set the [abbreviation](/document/product/266/9760#.E4.B8.8A.E4.BC.A0.E5.AD.98.E5.82.A8) of the storage region through the `StorageRegion` attribute.
```
<?php
require 'vendor/autoload.php';

use Vod\VodUploadClient;
use Vod\Model\VodUploadRequest;

$client = new VodUploadClient("your secretId", "your secretKey");
$req = new VodUploadRequest();
$req->MediaFilePath = "/data/videos/Wildlife.wmv";
$req->StorageRegion = "ap-chongqing";
try {
    $rsp = $client->upload("ap-guangzhou", $req);
    echo "FileId -> ". $rsp->FileId . "\n";
    echo "MediaUrl -> ". $rsp->MediaUrl . "\n";
} catch (Exception $e) {
    // Handle upload exception
    echo $e;
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
| Procedure | Name of the task flow to be automatically executed after upload is completed. This parameter is specified when the task flow is created through the [API](/document/product/266/33897) or [console](https://console.cloud.tencent.com/vod/video-process/taskflow). For more information, please see [Task Flow Overview](https://cloud.tencent.com/document/product/266/33475#.E4.BB.BB.E5.8A.A1.E6.B5.81). | String | No |
| ExpireTime | Expiration time of the media file in ISO 8601 format. For more information, please see [Notes on ISO Date Format](https://cloud.tencent.com/document/product/266/11732#iso-.E6.97.A5.E6.9C.9F.E6.A0.BC.E5.BC.8F). | String | No |
| ClassId | Category ID, which is used to categorize the media for management. A category can be created and its ID can be obtained by using the [category creating](/document/product/266/31772) API. | Integer | No |
| SourceContext | Source context of up to 250 characters, which is used to pass through the user request information and will be returned by the upload callback API. | String | No |
| SubAppId | ID of a [subapplication](/document/product/266/14574) in VOD. If you need to access a resource in a subapplication, enter the subapplication ID in this field; otherwise, leave it empty. | Integer | No |
| StorageRegion | Storage region, which specifies the region where to store the file. This field should be filled in with a [region abbreviation](/document/product/266/9760#.E4.B8.8A.E4.BC.A0.E5.AD.98.E5.82.A8). | String | No |

Upload response class `VodUploadResponse`

| Attribute Name | Attribute Description | Type |
| --------- | ---------------------- | ------- |
| FileId | Unique ID of the media file. | String |
| MediaUrl | Media playback address. | String |
| CoverUrl | Media cover address. | String |
| RequestId | Unique ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. | String |

Upload method `VodUploadClient.upload(String region, VodUploadRequest request)`

| Parameter Name | Description | Type | Required |
| --------- | ---------------------- | ------- | ---- |
| region | Access point region, i.e., the region where to request a VOD server. This is different from the storage region. For more information, please see [the list of supported regions](/document/api/266/31756#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8). | String | Yes |
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
