VOD provides an SDK for Go for uploading videos from a server. For more information on the upload process, please see [Guide](https://intl.cloud.tencent.com/document/product/266/33912).

## Integration Methods

### Importing by using `go get`
```json
go get -u github.com/tencentcloud/tencentcloud-sdk-go
go get -u github.com/tencentyun/cos-go-sdk-v5
go get -u github.com/tencentyun/vod-go-sdk
```

### Installing through source package
If you need to directly import the source code in your project, you can directly download the source code and import it into the project:

* [Access from GitHub](https://github.com/tencentyun/vod-go-sdk)
* Click [here](https://github.com/tencentyun/vod-go-sdk/archive/master.zip) to download the SDK for Go

## Simple Video Upload
### Initializing upload object
Initialize a `VodUploadClient` instance with a TencentCloud API key.

```
import (
	"github.com/tencentyun/vod-go-sdk"
)

client := &vod.VodUploadClient{}
client.SecretId = "your secretId"
client.SecretKey = "your secretKey"
```

### Constructing upload request object
```
import (
	"github.com/tencentcloud/tencentcloud-sdk-go/tencentcloud/common"
)

req := vod.NewVodUploadRequest()
req.MediaFilePath = common.StringPtr("/data/video/Wildlife.mp4")
```

### Calling upload method
Call the upload method and pass in the access point region and upload request.
```
rsp, err := client.Upload("ap-guangzhou", req)
if err != nil {
    fmt.Println(err)
    return
}
fmt.Println(*rsp.Response.FileId)
fmt.Println(*rsp.Response.MediaUrl)
```

>?The upload method automatically selects simple upload or multipart upload based on the file size, eliminating your need to take care of every step in multipart upload.

## Advanced Features
### Uploading cover
```
package main

import (
	"github.com/tencentcloud/tencentcloud-sdk-go/tencentcloud/common"
	"github.com/tencentyun/vod-go-sdk"
	"fmt"
)

func main() {
    client := &vod.VodUploadClient{}
    client.SecretId = "your secretId"
    client.SecretKey = "your secretKey"
    
    req := vod.NewVodUploadRequest()
    req.MediaFilePath = common.StringPtr("/data/video/Wildlife.mp4")
    req.CoverFilePath = common.StringPtr("/data/video/Wildlife-cover.png")
    
    rsp, err := client.Upload("ap-guangzhou", req)
    if err != nil {
        fmt.Println(err)
        return
    }
    fmt.Println(*rsp.Response.FileId)
    fmt.Println(*rsp.Response.MediaUrl)
    fmt.Println(*rsp.Response.CoverUrl)
}
```

### Specifying task flow
First, [create a task flow template](https://intl.cloud.tencent.com/document/product/266/14058) and name it. When initiating the task flow, you can set the `Procedure` parameter with the task flow template name, and the task flow will be executed automatically upon upload success.
```
package main

import (
	"github.com/tencentcloud/tencentcloud-sdk-go/tencentcloud/common"
	"github.com/tencentyun/vod-go-sdk"
	"fmt"
)

func main() {
    client := &vod.VodUploadClient{}
    client.SecretId = "your secretId"
    client.SecretKey = "your secretKey"
    
    req := vod.NewVodUploadRequest()
    req.MediaFilePath = common.StringPtr("/data/video/Wildlife.mp4")
    req.Procedure = common.StringPtr("Your Proceducre Name")
    
    rsp, err := client.Upload("ap-guangzhou", req)
    if err != nil {
        fmt.Println(err)
        return
    }
    fmt.Println(*rsp.Response.FileId)
    fmt.Println(*rsp.Response.MediaUrl)
}
```

### Uploading to subapplication
Pass in a [subapplication](https://intl.cloud.tencent.com/document/product/266/33987) ID. After the upload is successful, the resource will belong only to the specified subapplication.
```
package main

import (
	"github.com/tencentcloud/tencentcloud-sdk-go/tencentcloud/common"
	"github.com/tencentyun/vod-go-sdk"
	"fmt"
)

func main() {
    client := &vod.VodUploadClient{}
    client.SecretId = "your secretId"
    client.SecretKey = "your secretKey"
    
    req := vod.NewVodUploadRequest()
    req.MediaFilePath = common.StringPtr("/data/video/Wildlife.mp4")
    req.SubAppId = common.Uint64Ptr(101)
    
    rsp, err := client.Upload("ap-guangzhou", req)
    if err != nil {
        fmt.Println(err)
        return
    }
    fmt.Println(*rsp.Response.FileId)
    fmt.Println(*rsp.Response.MediaUrl)
}
```

### Specifying storage region
In the [console](https://console.cloud.tencent.com/vod), confirm that the target storage region has been activated. If not, you can do so as instructed in [Upload Storage Settings](https://intl.cloud.tencent.com/document/product/266/18874) and then set the [abbreviation](https://intl.cloud.tencent.com/document/product/266/9760) of the storage region through the `StorageRegion` attribute.
```
package main

import (
	"github.com/tencentcloud/tencentcloud-sdk-go/tencentcloud/common"
	"github.com/tencentyun/vod-go-sdk"
	"fmt"
)

func main() {
    client := &vod.VodUploadClient{}
    client.SecretId = "your secretId"
    client.SecretKey = "your secretKey"
    
    req := vod.NewVodUploadRequest()
    req.MediaFilePath = common.StringPtr("/data/video/Wildlife.mp4")
    req.StorageRegion = common.StringPtr("ap-chongqing")
    
    rsp, err := client.Upload("ap-guangzhou", req)
    if err != nil {
        fmt.Println(err)
        return
    }
    fmt.Println(*rsp.Response.FileId)
    fmt.Println(*rsp.Response.MediaUrl)
}
```

### Specifying the number of concurrent parts
The number of concurrent parts is applicable to uploading a large file in multiple parts simultaneously. The advantage of multipart upload lies in that a large file can be uploaded quickly. The SDK automatically selects simple upload or multipart upload based on the file size, eliminating your need to take care of every step in multipart upload. The number of concurrent parts of the file is specified by the `ConcurrentUploadNumber` parameter.
```
package main

import (
	"github.com/tencentcloud/tencentcloud-sdk-go/tencentcloud/common"
	"github.com/tencentyun/vod-go-sdk"
	"fmt"
)

func main() {
    client := &vod.VodUploadClient{}
    client.SecretId = "your secretId"
    client.SecretKey = "your secretKey"
    
    req := vod.NewVodUploadRequest()
    req.MediaFilePath = common.StringPtr("/data/video/Wildlife.mp4")
    req.ConcurrentUploadNumber = common.Uint64Ptr(5)
    
    rsp, err := client.Upload("ap-guangzhou", req)
    if err != nil {
        fmt.Println(err)
        return
    }
    fmt.Println(*rsp.Response.FileId)
    fmt.Println(*rsp.Response.MediaUrl)
}
```

### Uploading with temporary credentials
Pass in the relevant key information of the temporary credentials to use the temporary credentials for authentication and upload.
```
package main

import (
	"github.com/tencentcloud/tencentcloud-sdk-go/tencentcloud/common"
	"github.com/tencentyun/vod-go-sdk"
	"fmt"
)

func main() {
    client := &vod.VodUploadClient{}
    client.SecretId = "Credentials TmpSecretId"
    client.SecretKey = "Credentials TmpSecretKey"
    client.Token = "Credentials Token"
    
    req := vod.NewVodUploadRequest()
    req.MediaFilePath = common.StringPtr("/data/video/Wildlife.mp4")
    
    rsp, err := client.Upload("ap-guangzhou", req)
    if err != nil {
        fmt.Println(err)
        return
    }
    fmt.Println(*rsp.Response.FileId)
    fmt.Println(*rsp.Response.MediaUrl)
}
```


### Setting upload proxy
Set an upload proxy, and then the protocol and data involved will be processed by the proxy. In this way, you can use the proxy to upload files to Tencent Cloud over your organization's private network.
```
package main

import (
	"github.com/tencentcloud/tencentcloud-sdk-go/tencentcloud/common"
	"github.com/tencentyun/vod-go-sdk"
	"fmt"
    "net/http"
    "net/url"
)

func main() {
    client := &vod.VodUploadClient{}
    client.SecretId = "your secretId"
    client.SecretKey = "your secretKey"
    proxyUrl, _ := url.Parse("your proxy url")
	client.Transport = &http.Transport{
		Proxy: http.ProxyURL(proxyUrl),
	}
    
    req := vod.NewVodUploadRequest()
    req.MediaFilePath = common.StringPtr("/data/video/Wildlife.mp4")
    
    rsp, err := client.Upload("ap-guangzhou", req)
    if err != nil {
        fmt.Println(err)
        return
    }
    fmt.Println(*rsp.Response.FileId)
    fmt.Println(*rsp.Response.MediaUrl)
}
```

### Uploading adaptive bitstream file
The adaptive bitstream formats supported by this SDK for upload include HLS and DASH, and the media files referenced by the `manifest` (M3U8 or MPD) must be relative paths (i.e., URLs and absolute paths cannot be used) and be located in the same-level directory or subdirectory of `manifest` (i.e., `../` cannot be used). When calling the SDK's upload APIs, enter the `manifest` path as the `MediaFilePath` parameter, and the SDK will parse the list of related media files and upload them together.

```
package main

import (
	"github.com/tencentcloud/tencentcloud-sdk-go/tencentcloud/common"
	"github.com/tencentyun/vod-go-sdk"
	"fmt"
)

func main() {
    client := &vod.VodUploadClient{}
    client.SecretId = "your secretId"
    client.SecretKey = "your secretKey"
    
    req := vod.NewVodUploadRequest()
    req.MediaFilePath = common.StringPtr("/data/video/prog_index.m3u8")
    
    rsp, err := client.Upload("ap-guangzhou", req)
    if err != nil {
        fmt.Println(err)
        return
    }
    fmt.Println(*rsp.Response.FileId)
    fmt.Println(*rsp.Response.MediaUrl)
    fmt.Println(*rsp.Response.CoverUrl)
}
```

## API Description
Upload client class `VodUploadClient`

| Attribute Name | Attribute Description | Type | Required |
| --------- | ---------------------- | ------- | ---- |
| SecretId | TencentCloud API key ID. | String | Yes |
| SecretKey | TencentCloud API key. | String | Yes |

Upload request class `VodUploadRequest`

| Attribute Name | Attribute Description | Type | Required |
| --------- | ---------------------- | ------- | ---- |
| MediaFilePath | Path of the media file to be uploaded, which must be a local path and does not support URLs. | String pointer | Yes |
| SubAppId | ID of [subapplication](https://intl.cloud.tencent.com/document/product/266/33987) in VOD. If you need to access a resource in a subapplication, enter the subapplication ID in this field; otherwise, leave it empty. | uint64 pointer | No |
| MediaType | Type of the media file to be uploaded. For the valid values, please see [Overview](https://intl.cloud.tencent.com/document/product/266/9760) of media upload. If the `MediaFilePath` path contains a file extension, this parameter can be left empty. | String pointer | No |
| MediaName | Name of the media file after being uploaded. If this parameter is left empty, the filename in `MediaFilePath` will be used by default. | String pointer | No |
| CoverFilePath | Path of the cover file to be uploaded, which must be a local path and does not support URLs. | String pointer | No |
| CoverType | Type of the cover file to be uploaded. For the valid values, please see [Overview](https://intl.cloud.tencent.com/document/product/266/9760) of media upload. If the `CoverFilePath` path contains a file extension, this parameter can be left empty. | String pointer | No |
| Procedure | Name of the task flow to be automatically executed after upload is completed. This parameter is specified when the task flow is created through the [API](https://intl.cloud.tencent.com/document/product/266/33897) or [console](https://console.cloud.tencent.com/vod/video-process/taskflow). For more information, please see [Task Flow](https://intl.cloud.tencent.com/document/product/266/33931). | String pointer | No |
| ExpireTime | Expiration time of media file in ISO 8601 format. For more information, please see [the notes on ISO date format](https://intl.cloud.tencent.com/document/product/266/11732). | String pointer | No |
| ClassId | Category ID, which is used to categorize the media for management. A category can be created, and its ID can be obtained by using the [CreateClass](https://intl.cloud.tencent.com/document/product/266/35325) API. | int64 pointer | No |
| SourceContext | Source context of up to 250 characters, which is used to pass through the user request information and will be returned by the upload callback API. | String pointer | No |
| StorageRegion | Storage region, which specifies the region where to store the file. This field should be filled in with a [region abbreviation](https://intl.cloud.tencent.com/document/product/266/9760). | String pointer | No |
| ConcurrentUploadNumber | Number of concurrent parts, which is valid when a large file is uploaded in multiple parts. | Integer | No |

Upload response class `VodUploadResponse`

| Attribute Name | Attribute Description | Type |
| --------- | ---------------------- | ------- |
| Response | Upload return result information. | struct |
| Response.FileId | Unique ID of media file. | String pointer |
| Response.MediaUrl | Media playback address. | String pointer |
| Response.CoverUrl | Media cover address. | String pointer |
| Response.RequestId | Unique ID of request. Each request returns a unique ID. The `RequestId` is required to troubleshoot issues. | String pointer |

Upload method `VodUploadClient.Upload(region string, request *VodUploadRequest)`

| Parameter Name | Description | Type | Required |
| --------- | ---------------------- | ------- | ---- |
| region | Access point region, i.e., the region where to request a VOD server. This is different from the storage region. For more information, please see [the list of supported regions](https://intl.cloud.tencent.com/document/product/266/34113). | String | Yes |
| request | Upload request. | VodUploadRequest pointer | Yes |

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
