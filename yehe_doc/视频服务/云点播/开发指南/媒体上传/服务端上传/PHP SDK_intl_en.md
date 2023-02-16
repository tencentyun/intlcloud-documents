VOD provides an SDK for PHP for uploading videos from a server. For more information on the upload process, see [Upload from Server Guide](https://intl.cloud.tencent.com/document/product/266/33912).

## Integration Methods

### Importing by using composer
```json
{
    "require": {
        "qcloud/vod-sdk-v5": "v2.4.0"
    }
}
```

### Installing by using source package
1. If the Composer tool is not used for dependency management in the project, you can download the source code from [GitHub](https://github.com/tencentyun/vod-php-sdk-v5) and import it into the project.
2. Decompress the [vod-sdk.zip](https://github.com/tencentyun/vod-php-sdk-v5/tree/master/packages) file into the project and import the `autoload.php` file.

##  Uploading Videos
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

### Calling upload method
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

>?The upload method automatically selects simple upload or multipart upload based on the file size, saving efforts of users.

## Advanced Features
### Uploading thumbnail
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

### Specifying task flow
First, [create a task flow template](https://intl.cloud.tencent.com/document/product/266/14058) and name it. When initiating the task flow, you can set the `Procedure` parameter with the task flow template name, and the task flow will be executed automatically upon upload success.
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

### Uploading to subapplication
Pass in a [subapplication](https://intl.cloud.tencent.com/document/product/266/33987) ID. After the upload is successful, the resource will belong only to the specified subapplication.
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

### Specifying storage region
In the [console](https://console.cloud.tencent.com/vod), confirm that the target storage region has been activated. If not, you can do so as instructed in [Upload Storage Settings](https://intl.cloud.tencent.com/document/product/266/18874) and then set the [abbreviation](https://intl.cloud.tencent.com/document/product/266/9760) of the storage region through the `StorageRegion` attribute.
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

### Uploading with temporary credentials
Pass in the relevant key information of the temporary credentials to use the temporary credentials for authentication and upload.
```
<?php
require 'vendor/autoload.php';

use Vod\VodUploadClient;
use Vod\Model\VodUploadRequest;

$client = new VodUploadClient("Credentials TmpSecretId", "Credentials TmpSecretKey", "Credentials Token");
$req = new VodUploadRequest();
$req->MediaFilePath = "/data/videos/Wildlife.wmv";
try {
    $rsp = $client->upload("ap-guangzhou", $req);
    echo "FileId -> ". $rsp->FileId . "\n";
    echo "MediaUrl -> ". $rsp->MediaUrl . "\n";
} catch (Exception $e) {
    // Handle upload exception
    echo $e;
}
```


### Setting upload proxy
Set an upload proxy, and then the protocol and data involved will be processed by the proxy. In this way, you can use the proxy to upload files to Tencent Cloud over your organization's private network.
```
<?php
require 'vendor/autoload.php';

use Vod\VodUploadClient;
use Vod\Model\VodUploadRequest;
use Vod\Model\VodUploadHttpProfile;

$client = new VodUploadClient("your secretId", "your secretKey");
$uploadHttpProfile = new VodUploadHttpProfile("your proxy addr");
$client->setHttpProfile($uploadHttpProfile);
$req = new VodUploadRequest();
$req->MediaFilePath = "/data/videos/Wildlife.wmv";
try {
    $rsp = $client->upload("ap-guangzhou", $req);
    echo "FileId -> ". $rsp->FileId . "\n";
    echo "MediaUrl -> ". $rsp->MediaUrl . "\n";
} catch (Exception $e) {
    // Handle upload exception
    echo $e;
}
```

### Uploading adaptive bitstream file

The adaptive bitstream formats supported by this SDK for upload include HLS and DASH, and the media files referenced by the `manifest` (M3U8 or MPD) must be relative paths (i.e., URLs and absolute paths cannot be used) and be located in the same-level directory or subdirectory of `manifest` (i.e., `../` cannot be used). When calling the SDK's upload APIs, enter the `manifest` path as the `MediaFilePath` parameter, and the SDK will parse the list of related media files and upload them together.

```
<?php
require 'vendor/autoload.php';

use Vod\VodUploadClient;
use Vod\Model\VodUploadRequest;

$client = new VodUploadClient("your secretId", "your secretKey");
$req = new VodUploadRequest();
$req->MediaFilePath = "/data/videos/prog_index.m3u8";
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
| secretId | The ID of TencentCloud API key | String | Yes |
| secretKey | TencentCloud API key | String | Yes |

Upload request class `VodUploadRequest`

| Attribute Name | Attribute Description | Type | Required |
| --------- | ---------------------- | ------- | ---- |
| MediaFilePath | Path to the media file to be uploaded, which must be a local path and does not support URLs. | String | Yes |
| SubAppId | ID of a [subapplication](https://intl.cloud.tencent.com/document/product/266/33987) in VOD. If you need to access a resource in a subapplication, enter the subapplication ID in this field; otherwise, leave it empty. | Integer | No |
| MediaType | Type of the media file to be uploaded. For the valid values, see [Overview](https://intl.cloud.tencent.com/document/product/266/9760) of media upload. If the `MediaFilePath` path contains a file extension, this parameter can be left empty. | String | No |
| MediaName | Name of the media file after being uploaded. If this parameter is left empty, the filename in `MediaFilePath` will be used by default. | String | No |
| CoverFilePath | Path to the thumbnail file to be uploaded, which must be a local path and does not support URLs. | String | No |
| CoverType | Type of the thumbnail file to be uploaded. For the valid values, see [Overview](https://intl.cloud.tencent.com/document/product/266/9760) of media upload. If the `CoverFilePath` path contains a file extension, this parameter can be left empty. | String | No |
| Procedure | Name of the task flow to be automatically executed after upload is completed. This parameter is specified when the task flow is created through the [API](https://intl.cloud.tencent.com/document/product/266/34167) or [console](https://console.cloud.tencent.com/vod/video-process/taskflow). For more information, see [Task Flow](https://intl.cloud.tencent.com/document/product/266/33931). | String | No |
| ExpireTime | Expiration time of media file in ISO 8601 format. For more information, see [notes on ISO date format](https://intl.cloud.tencent.com/document/product/266/11732). | String | No |
| ClassId | Category ID, which is used to categorize the media for management. A category can be created and its ID can be obtained by using the [category creating](https://intl.cloud.tencent.com/document/product/266/35325) API. | Integer | No |
| SourceContext | Source context of up to 250 characters, which is used to pass through the user request information and will be returned by the upload callback API. | String | No |
| StorageRegion | Storage region, which specifies the region where to store the file. This field should be filled in with a [region abbreviation](https://intl.cloud.tencent.com/document/product/266/9760). | String | No |

Upload response class `VodUploadResponse`

| Attribute Name | Attribute Description | Type |
| --------- | ---------------------- | ------- |
| FileId | Unique ID of the media file. | String |
| MediaUrl | Media playback address. | String |
| CoverUrl | Media thumbnail address. | String |
| RequestId | Unique ID of the request. Each request returns a unique ID. The `RequestId` is required to troubleshoot issues. | String |

Upload method `VodUploadClient.upload(String region, VodUploadRequest request)`

| Parameter | Description                   | Type      | Required   |
| --------- | ---------------------- | ------- | ---- |
| region | Access point region, i.e., the region where to request a VOD server. This is different from the storage region. For more information, see [the list of supported regions](https://intl.cloud.tencent.com/document/product/266/34113). | String | Yes |
| request | Upload request. | VodUploadRequest | Yes |

## Error Codes
| Status Code | Description |
| ----------- | ----------------- |
| InternalError | Internal error. |
| InvalidParameter.ExpireTime | Incorrect parameter value: Expiration time. |
| InvalidParameterValue.CoverType | Incorrect parameter value: Thumbnail type. |
| InvalidParameterValue.MediaType | Incorrect parameter value: Media type. |
| InvalidParameterValue.SubAppId | Incorrect parameter value: Subapplication ID. |
| InvalidParameterValue.VodSessionKey | Incorrect parameter value: VOD session. |
| ResourceNotFound | Resource does not exist. |

