VOD는 서버에서 비디오를 업로드하기 위한 Go용 SDK를 제공합니다. 업로드 프로세스에 대한 자세한 내용은 [서버 업로드 가이드](https://intl.cloud.tencent.com/document/product/266/33912)를 참고하십시오.

## 통합 방식

### go get을 사용하여 가져오기
```json
go get -u github.com/tencentcloud/tencentcloud-sdk-go
go get -u github.com/tencentyun/cos-go-sdk-v5
go get -u github.com/tencentyun/vod-go-sdk
```

### 소스 패키지를 통해 설치
프로젝트에서 소스 코드를 직접 가져와야 하는 경우 소스 코드를 직접 다운로드하여 프로젝트로 가져올 수 있습니다.

* [GitHub에서 액세스](https://github.com/tencentyun/vod-go-sdk)
* [클릭하여 Go SDK 다운로드](https://github.com/tencentyun/vod-go-sdk/archive/master.zip)

## 비디오 간편 업로드
### 업로드 객체 초기화
TencentCloud API 키로 VodUploadClient 인스턴스를 초기화합니다.

```
import (
	"github.com/tencentyun/vod-go-sdk"
)

client := &vod.VodUploadClient{}
client.SecretId = "your secretId"
client.SecretKey = "your secretKey"
```

### 업로드 요청 객체 생성
```
import (
	"github.com/tencentcloud/tencentcloud-sdk-go/tencentcloud/common"
)

req := vod.NewVodUploadRequest()
req.MediaFilePath = common.StringPtr("/data/video/Wildlife.mp4")
```

### 업로드 메소드 호출
업로드 메소드를 호출하고 액세스 포인트 리전과 업로드 요청을 전달합니다.
```
rsp, err := client.Upload("ap-guangzhou", req)
if err != nil {
    fmt.Println(err)
    return
}
fmt.Println(*rsp.Response.FileId)
fmt.Println(*rsp.Response.MediaUrl)
```

>?업로드 방법은 파일 크기에 따라 간편 업로드 또는 멀티파트 업로드를 자동으로 선택하므로 멀티파트 업로드의 각 단계를 신경 쓸 필요가 없습니다.

## 고급 기능
### 커버 업로드
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

### 태스크 플로우 지정
먼저 [태스크 플로우 템플릿 생성](https://intl.cloud.tencent.com/document/product/266/14058) 완료 후 이름을 지정합니다. 태스크 플로우를 시작할 때 태스크 플로우 템플릿 이름으로 `Procedure` 매개변수를 설정할 수 있으며, 업로드 성공 시 태스크 플로우가 자동으로 실행됩니다.
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

### 서브 애플리케이션에 업로드
[서브 애플리케이션](https://intl.cloud.tencent.com/document/product/266/33987) ID를 전달합니다. 업로드 성공 후 리소스는 지정된 서브 애플리케이션에만 속하게 됩니다.
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

### 스토리지 리전 지정
[콘솔](https://console.cloud.tencent.com/vod)에서 대상 스토리지 리전이 활성화되었는지 확인하고, 활성화되지 않은 경우 [스토리지 설정 업로드](https://intl.cloud.tencent.com/document/product/266/18874)에 따라 수행한 다음, `StorageRegion` 속성을 통해 스토리지 리전의 [영어 약칭](https://intl.cloud.tencent.com/document/product/266/9760)을 설정할 수 있습니다.
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

### 동시 파트 수 지정
동시 파트 수는 대용량 파일을 동시에 여러 파트로 업로드하는 데 적용됩니다. 멀티파트 업로드의 장점은 대용량 파일을 빠르게 업로드할 수 있다는 것입니다. SDK는 파일 크기에 따라 일반 업로드 또는 멀티파트 업로드를 자동으로 선택하므로 멀티파트 업로드의 각 단계를 신경 쓸 필요가 없습니다. 파일의 동시 부분 수는 `ConcurrentUploadNumber` 매개변수로 지정됩니다.
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

### 임시 자격 증명으로 업로드
임시 자격 증명의 관련 키 정보를 전달하여 인증 및 업로드에 임시 자격 증명을 사용합니다.
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


### 업로드 프록시 설정
업로드 프록시를 설정하면 관련된 프로토콜과 데이터가 프록시에 의해 처리되므로 프록시를 사용하여 회사의 내부망을 통해 Tencent Cloud에 파일을 업로드할 수 있습니다.
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

### 어댑티브 비트스트림 파일 업로드
이 SDK가 업로드용으로 지원하는 어댑티브 비트스트림 형식에는 HLS 및 DASH가 포함되며, manifest(M3U8 또는 MPD)에서 참고하는 미디어 파일은 상대 경로여야 하고(즉, URL 및 절대 경로는 사용할 수 없음), manifest의 동일 레벨 디렉터리 또는 서브 디렉터리(예: `../`는 사용할 수 없음)에 위치해야 합니다. SDK의 업로드 API를 호출할 때 `MediaFilePath` 매개변수로 manifest 경로를 입력하면 SDK가 관련 미디어 파일 목록을 파싱하여 함께 업로드합니다.

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

## API 설명
업로드 클라이언트 클래스 `VodUploadClient`

| 속성 이름      | 속성 설명                   | 유형      | 필수 입력   |
| --------- | ---------------------- | ------- | ---- |
| secretId   | Tencent Cloud API 키 ID.        | String | Yes    |
| secretKey | Tencent Cloud API Key. | String  | Yes    |

업로드 요청 클래스 `VodUploadRequest`

| 속성 이름      | 속성 설명                   | 유형&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | 필수 입력   |
| --------- | ---------------------- | ------- | ---- |
| MediaFilePath   | 업로드할 미디어 파일의 경로로, 로컬 경로여야 하며 URL을 지원하지 않습니다.| String 포인터 | Yes    |
| MediaType   | 업로드할 미디어 파일의 유형입니다. 유효 값은 [미디어 업로드 개요](https://intl.cloud.tencent.com/document/product/266/9760)를 참고하십시오. MediaFilePath 경로에 파일 확장자가 포함된 경우 이 매개변수를 비워 둘 수 있습니다.        | String 포인터 | No    |
| MediaName   | 업로드된 미디어 파일의 이름입니다. 이 매개변수를 비워두면 기본적으로 MediaFilePath의 파일 이름이 사용됩니다.      | String 포인터 | No    |
| CoverFilePath   | 업로드할 커버 파일의 경로로, URL을 지원하지 않는 로컬 경로여야 합니다.| String 포인터| No    |
| CoverType   | 업로드할 커버 파일의 유형입니다. 유효한 값은 [비디오 업로드 개요](https://intl.cloud.tencent.com/document/product/266/9760)를 참고하십시오. CoverFilePath 경로에 파일 확장자가 포함된 경우 이 매개변수를 비워 둘 수 있습니다.        | String 포인터 | No    |
| Procedure   | 업로드 완료 후 자동으로 실행될 태스크 플로우의 이름으로, 태스크 플로우([API 방식](https://intl.cloud.tencent.com/document/product/266/33897) 또는 [콘솔 방식](https://console.cloud.tencent.com/vod/video-process/taskflow))를 생성할 때 지정하는 매개변수입니다. 자세한 내용은 [태스크 플로우](https://intl.cloud.tencent.com/document/product/266/33931)를 참고하십시오.       | String 포인터| No    |
| ExpireTime   | ISO 8601 형식의 미디어 파일 만료 시간입니다. 자세한 내용은 [ISO 날짜 형식](https://intl.cloud.tencent.com/document/product/266/11732)을 참고하십시오.        | String 포인터 | No    |
| ClassId   | 관리할 미디어를 분류하는 데 사용되는 클래스 ID로, [CreateClass](https://intl.cloud.tencent.com/document/product/266/35325) API를 사용하여 클래스를 생성하고, 클래스 ID를 얻을 수 있습니다.        | int64 포인터 | No    |
| SourceContext   | 최대 250자의 소스 컨텍스트로, 사용자 요청 정보를 전달하는 데 사용되며 업로드 콜백 API에서 반환됩니다.        | String 포인터 | No    |
| SubAppId   | VOD의 [서브 애플리케이션](https://intl.cloud.tencent.com/document/product/266/33987) ID입니다. 서브 애플리케이션의 리소스에 액세스하려면 이 필드에 서브 애플리케이션 ID를 입력하고, 그렇지 않으면 비워 둡니다.        | uint64 포인터 | No    |
| StorageRegion   | 파일을 저장할 스토리지 리전입니다. 이 필드는 리전 [영어 약칭](https://intl.cloud.tencent.com/document/product/266/9760)을 입력합니다.        | String 포인터| No    |
| ConcurrentUploadNumber   | 대용량 파일이 여러 파트로 업로드될 때 유효한 동시 파트 수입니다.        | Integer | No    |

업로드 응답 클래스 `VodUploadResponse`

| 속성 이름      | 속성 설명                   | 유형      |
| --------- | ---------------------- | ------- |
| Response   | 결과 정보 업로드 및 반환        | struct |
| Response.FileId   | 미디어 파일의 고유 ID.            | String 포인터 |
| Response.MediaUrl | 미디어 재생 주소. | String 포인터  |
| Response.CoverUrl | 미디어 커버 주소. | String 포인터  |
| Response.RequestId | 요청의 고유 ID. 각 요청은 고유한 ID를 반환합니다. 문제를 해결하려면 RequestId가 필요합니다.  | String 포인터  |

업로드 메소드 `VodUploadClient.Upload(region string, request *VodUploadRequest)`

| 매개변수 이름     | 매개변수 설명                    | 유형     | 필수 입력 |
| --------- | ---------------------- | ------- | ---- |
| region   | VOD 서버를 요청하는 액세스 포인트 리전으로 스토리지 리전과 다릅니다. 자세한 내용은 [지원 리전 리스트](https://intl.cloud.tencent.com/document/product/266/34113)를 참고하십시오.        | String | Yes    |
| request   | 업로드 요청.        | VodUploadRequest 포인터 | Yes    |

## 오류 코드

| 상태 코드         | 설명               |
| ----------- | ----------------- |
| InternalError       | 내부 오류. |
| InvalidParameter.ExpireTime       | 잘못된 매개변수 값: 만료 시간. |
| InvalidParameterValue.CoverType       | 잘못된 매개변수 값: 커버 유형.     |
| InvalidParameterValue.MediaType       | 잘못된 매개변수 값: 미디어 유형.           |
| InvalidParameterValue.SubAppId       | 잘못된 매개변수 값: 서브 애플리케이션 ID.              |
| InvalidParameterValue.VodSessionKey       | 잘못된 매개변수 값: VOD 세션              |
| ResourceNotFound       | 리소스가 존재하지 않음.              |
