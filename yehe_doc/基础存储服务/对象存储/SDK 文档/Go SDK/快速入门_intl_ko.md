## 다운로드 및 설치

#### 관련 리소스
- COS의 XML Go SDK 소스 코드 다운로드 주소: [XML Go SDK](https://github.com/tencentyun/cos-go-sdk-v5)
- 예시 Demo 다운로드 주소:[COS XML Go SDK 예시](https://github.com/tencentyun/cos-go-sdk-v5/tree/master/example).
- 자세한 내용은 [COS Go SDK API](https://godoc.org/github.com/tencentyun/cos-go-sdk-v5) 문서를 참고하십시오.
- SDK 문서의 모든 예시 코드는 [SDK 코드 예시](https://github.com/tencentyun/cos-snippets/tree/master/Go)를 참고하십시오.
- SDK 로그 업데이트는 [ChangeLog](https://github.com/tencentyun/cos-go-sdk-v5/blob/master/CHANGELOG.md)를 참고하십시오.
- SDK FAQ는 [Go SDK FAQ](https://intl.cloud.tencent.com/document/product/436/40774)를 참고하십시오.

>? SDK 사용 시 함수 또는 메소드 없음 등 오류가 발생하였을 경우, 먼저 SDK를 최신 버전으로 업데이트한 후 재시도하십시오.
>

#### 환경 종속
Golang: Go 컴파일 실행 환경을 다운로드 및 설치하는 데 사용합니다. Golang 공식 홈페이지에서 다운로드하십시오.

#### SDK 설치
다음 명령어를 실행하여 COS Go SDK를 설치합니다.
```sh
go get -u github.com/tencentyun/cos-go-sdk-v5
```

## 사용하기
COS Go SDK를 사용한 클라이언트 초기화, 버킷 생성, 버킷 리스트 조회, 객체 업로드, 객체 리스트 조회, 객체 다운로드, 객체 삭제 등의 기본 작업 방법은 아래와 같습니다.

### 초기화
COS 도메인을 사용해 COS GO 클라이언트 구성을 생성합니다.

#### 메소드 프로토타입
```Go
func NewClient(uri *BaseURL, httpClient *http.Client) *Client
```
#### 매개변수 설명
```
// BaseURL로 각 API에 필요한 기본 URL 액세스
type BaseURL struct {
    // bucket, object 관련 API에 액세스하는 기본 URL(path 부분 미포함): https://examplebucket-1250000000.cos.<Region>.myqcloud.com
    BucketURL *url.URL
    // service API에 액세스하는 기본 URL(path 부분 미포함): https://cos.<Region>.myqcloud.com
    ServiceURL *url.URL
    // Batch API에 액세스하는 기본 URL(path 부분 미포함): https://<UIN>.cos-control.<Region>.myqcloud.com
    BatchURL *url.URL
    // CI에 액세스하는 기본 URL(path 부분 미포함): https://examplebucket-1250000000.ci.<Region>.myqcloud.com
    CIURL *url.URL
}
```

| 매개변수 이름  | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| --------- | ------------------------------------------------------------ | ------ | ---- |
| BucketURL | bucket, object 관련 API에 액세스하는 기본 URL(path 부분 미포함)  | string | 예   |
| ServiceURL| service API에 액세스하는 기본 URL(path 부분 미포함)              | string | 아니요   |
| BatchURL  | Batch API에 액세스하는 기본 URL(path 부분 미포함)               | string | 아니요   |
| CIURL     | CI에 액세스하는 기본 URL(path 부분 미포함)                      | string | 아니요   |

#### 요청 예시1: 영구 키 사용

[//]: # (.cssg-snippet-global-init)
```go
// examplebucket-1250000000과 COS_REGION을 실제 정보로 수정합니다.
u, _ := url.Parse("https://examplebucket-1250000000.cos.COS_REGION.myqcloud.com")
// Get Service 쿼리에 사용, 모든 리전 기본값: service.cos.myqcloud.com
su, _ := url.Parse("https://cos.COS_REGION.myqcloud.com")
b := &cos.BaseURL{BucketURL: u, ServiceURL: su}
// 1. 영구 키
client := cos.NewClient(b, &http.Client{
    Transport: &cos.AuthorizationTransport{
        SecretID:  "SECRETID",
        SecretKey: "SECRETKEY",
    },
})
```

#### 요청 예시2: 임시 키 사용

[//]: # (.cssg-snippet-global-init-sts)
```go
// examplebucket-1250000000과 COS_REGION을 실제 정보로 수정합니다.
u, _ := url.Parse("https://examplebucket-1250000000.cos.COS_REGION.myqcloud.com")
b := &cos.BaseURL{BucketURL: u}
// 2. 임시 키
client := cos.NewClient(b, &http.Client{
    Transport: &cos.AuthorizationTransport{
        SecretID:     "SECRETID",
        SecretKey:    "SECRETKEY",
        SessionToken: "SECRETTOKEN",
    },
})
if client != nil {
    // COS 요청 호출
}

```
>? 임시 키 생성 및 사용에 대한 자세한 내용은 [임시 키 생성 및 사용 가이드](https://intl.cloud.tencent.com/document/product/436/14048)를 참고하십시오.
>

#### 요청 예시3: 도메인 설정

BaseURL을 변경하여 직접 사용자 정의 도메인 또는 글로벌 가속 도메인을 사용해 COS에 액세스할 수 있습니다.
```
// 글로벌 가속 도메인으로 COS 액세스
u, _ := url.Parse("http://<BucketName-APPID>.cos.accelerate.myqcloud.com")
b := &cos.BaseURL{BucketURL: u}
// 2. 임시 키
client := cos.NewClient(b, &http.Client{
    Transport: &cos.AuthorizationTransport{
        SecretID:     "SECRETID",
        SecretKey:    "SECRETKEY",
        SessionToken: "SECRETTOKEN",
    },
})
```
#### 요청 예시 4: CRC64 인증

COS Go SDK는 기본적으로 파일 업로드에 대한 CRC64 검사를 활성화합니다.

>! 
>- COS Go SDK는 v0.7.23 이후 버전이어야 합니다.
>- CRC64 검사 비활성화 하지 말 것을 강력히 권장합니다.
```
// examplebucket-1250000000과 COS_REGION을 실제 정보로 수정합니다.
u, _ := url.Parse("https://examplebucket-1250000000.cos.COS_REGION.myqcloud.com")
b := &cos.BaseURL{BucketURL: u}
// 2. 임시 키
client := cos.NewClient(b, &http.Client{
    Transport: &cos.AuthorizationTransport{
        SecretID:     "SECRETID",
        SecretKey:    "SECRETKEY",
        SessionToken: "SECRETTOKEN",
    },
})
// CRC64 인증 비활성화
client.Conf.EnableCRC = false

```

### 버킷 생성

```Go
package main


import (
    "context"
    "net/http"
    "net/url"
    "os"


    "github.com/tencentyun/cos-go-sdk-v5"
)


func main() {
    // examplebucket-1250000000과 COS_REGION을 실제 정보로 수정합니다.
    u, _ := url.Parse("https://examplebucket-1250000000.cos.COS_REGION.myqcloud.com")
    b := &cos.BaseURL{BucketURL: u}
    c := cos.NewClient(b, &http.Client{
        Transport: &cos.AuthorizationTransport{
            SecretID:  "SECRETID",
            SecretKey: "SECRETKEY",
        },
    })


    _, err := c.Bucket.Put(context.Background(), nil)
    if err != nil {
        panic(err)
    }
}
```


### 버킷 리스트 조회
```go
package main


import (
    "context"
    "fmt"
    "net/http"
    "os"


    "github.com/tencentyun/cos-go-sdk-v5"
)


func main() {
    c := cos.NewClient(nil, &http.Client{
        Transport: &cos.AuthorizationTransport{
            SecretID:  "SECRETID",
            SecretKey: "SECRETKEY",
        },
    })


    s, _, err := c.Service.Get(context.Background())
    if err != nil {
        panic(err)
    }


    for _, b := range s.Buckets {
        fmt.Printf("%#v\n", b)
    }
}
```

### 객체 업로드
```Go
package main


import (
    "context"
    "net/http"
    "net/url"
    "os"
    "strings"

    "github.com/tencentyun/cos-go-sdk-v5"
)


func main() {
    // examplebucket-1250000000과 COS_REGION을 실제 정보로 수정합니다.
    u, _ := url.Parse("https://examplebucket-1250000000.cos.COS_REGION.myqcloud.com")
    b := &cos.BaseURL{BucketURL: u}
    c := cos.NewClient(b, &http.Client{
        Transport: &cos.AuthorizationTransport{
            SecretID:  "SECRETID",
            SecretKey: "SECRETKEY",
        },
    })
    // 객체 키(Key)는 버킷 내 객체의 고유 식별자입니다.
    // 예를 들어, 객체의 액세스 도메인 `examplebucket-1250000000.cos.COS_REGION.myqcloud.com/test/objectPut.go`에서 객체 키는 test/objectPut.go입니다.
    name := "test/objectPut.go"
    // 1. 문자열로 객체 업로드
    f := strings.NewReader("test")


    _, err := c.Object.Put(context.Background(), name, f, nil)
    if err != nil {
        panic(err)
    }
    // 2. 로컬 파일로 객체 업로드
    _, err = c.Object.PutFromFile(context.Background(), name, "../test", nil)
    if err != nil {
        panic(err)
    }
    // 3. 파일 스트림으로 객체 업로드
    fd, err := os.Open("./test")
    if err != nil {
        panic(err)
    }
    defer fd.Close()
    _, err = c.Object.Put(context.Background(), name, fd, nil)
    if err != nil {
        panic(err)
    }
}
```

### 객체 리스트 조회
```go
package main


import (
    "context"
    "fmt"
    "net/http"
    "net/url"
    "os"

    "github.com/tencentyun/cos-go-sdk-v5"
)


func main() {
    // examplebucket-1250000000과 COS_REGION을 실제 정보로 수정합니다.
    u, _ := url.Parse("https://examplebucket-1250000000.cos.COS_REGION.myqcloud.com")
    b := &cos.BaseURL{BucketURL: u}
    c := cos.NewClient(b, &http.Client{
        Transport: &cos.AuthorizationTransport{
            SecretID:  "SECRETID",
            SecretKey: "SECRETKEY",
        },
    })


    opt := &cos.BucketGetOptions{
        Prefix:  "test",
        MaxKeys: 3,
    }
    v, _, err := c.Bucket.Get(context.Background(), opt)
    if err != nil {
        panic(err)
    }


    for _, c := range v.Contents {
        fmt.Printf("%s, %d\n", c.Key, c.Size)
    }
}
```

### 객체 다운로드
```Go
package main


import (
    "context"
    "fmt"
    "io/ioutil"
    "net/http"
    "net/url"
    "os"

    "github.com/tencentyun/cos-go-sdk-v5"
)


func main() {
    // examplebucket-1250000000과 COS_REGION을 실제 정보로 수정합니다.
    u, _ := url.Parse("https://examplebucket-1250000000.cos.COS_REGION.myqcloud.com")
    b := &cos.BaseURL{BucketURL: u}
    c := cos.NewClient(b, &http.Client{
        Transport: &cos.AuthorizationTransport{
            SecretID:  "SECRETID",
            SecretKey: "SECRETKEY",
        },
    })
    // 1. 응답 본문으로 객체 가져오기
    name := "test/objectPut.go"
    resp, err := c.Object.Get(context.Background(), name, nil)
    if err != nil {
        panic(err)
    }
    bs, _ := ioutil.ReadAll(resp.Body)
    resp.Body.Close()
    fmt.Printf("%s\n", string(bs))
    // 2. 로컬 파일에 객체 가져오기
    _, err = c.Object.GetToFile(context.Background(), name, "exampleobject", nil)
    if err != nil {
        panic(err)
    }
}
```

### 객체 삭제
```go
package main


import (
    "context"
    "net/http"
    "net/url"
    "os"

    "github.com/tencentyun/cos-go-sdk-v5"
)


func main() {
    // examplebucket-1250000000과 COS_REGION을 실제 정보로 수정합니다.
    u, _ := url.Parse("https://examplebucket-1250000000.cos.COS_REGION.myqcloud.com")
    b := &cos.BaseURL{BucketURL: u}
    c := cos.NewClient(b, &http.Client{
        Transport: &cos.AuthorizationTransport{
            SecretID:  "SECRETID",
            SecretKey: "SECRETKEY",
        },
    })
    name := "test/objectPut.go"
    _, err := c.Object.Delete(context.Background(), name)
    if err != nil {
        panic(err)
    }
}
```
