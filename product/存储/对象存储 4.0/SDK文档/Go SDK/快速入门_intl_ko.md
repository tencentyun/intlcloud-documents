## 개발 준비

### 관련 리소스
COS의 XML Go SDK 리소스 다운로드 주소: [XML Go SDK](https://github.com/tencentyun/cos-go-sdk-v5). 더 자세한 내용은 [COS Go SDK API](https://godoc.org/github.com/tencentyun/cos-go-sdk-v5) 문서를 참조하십시오

### 환경 의존

[Golang](https://golang.org/doc/install/source?spm=a2c4g.11186623.2.11.168ec486fb1eQK) Go 컴파일 실행 환경을 다운로드하고 설치하는 데 사용됩니다. Go 설치가 완료되면 시스템 변수 GOPATH를 새로 만들고, 이를 코드 디렉터리로 가리킵니다.
>?문서에서 나오는 SecretId, SecretKey, Bucket 같은 명칭의 함의 및 획득 방법은 [COS 용어집](https://cloud.tencent.com/document/product/436/7751)을 참조하십시오.

### SDK 설치

다음 명령을 실행하여 COS Go SDK 설치하기:
```
 go get -u github.com/tencentyun/cos-go-sdk-v5/
```

## 시작 가이드
이 섹션에서는 COS Go SDK를 사용하여 클라이언트 초기화, 버킷 생성, 파일 업로드 및 다운로드 등의 일반적인 작업을 수행하는 방법을 설명합니다.
각 API는 [example](https://github.com/tencentyun/cos-go-sdk-v5/tree/master/example) 디렉터리에 해당하는 사용 사례가 나옵니다.
### 클라이언트 초기화

COS 도메인 이름을 사용하여 COS GO Client 구조를 생성합니다.

#### 방식 프로토타입
```Go
func NewClient(uri *BaseURL, httpClient *http.Client) *Client
```
#### 요청 예시
```go
//<bucketname>, <appid> 및 <region>을 실제 정보로 수정합니다
//예: http://test-1253846586.cos.ap-guangzhou.myqcloud.com
u, _ := url.Parse("http://<bucketname>-<appid>.cos.<region>.myqcloud.com")
b := &cos.BaseURL{BucketURL: u}
client := cos.NewClient(b, &http.Client{
	Transport: &cos.AuthorizationTransport{
		//사용자 계정의 키 정보를 입력하고 환경 변수로 설정할 수도 있습니다.
		SecretID:  os.Getenv("COS_SECRETID"),                         
		SecretKey: os.Getenv("COS_SECRETKEY"),                      
	},                                 
})
```
#### 매개변수 설명
```go
type AuthorizationTransport struct {
	SecretID     string
	SecretKey    string
	SessionToken string
	// 서명 만료 기간
	Expire time.Duration         
}
```
#### 반환 결과 설명
반환된 클라이언트에 Service, Bucket 및 Object 구조가 포함됩니다. 이 구조들은 각 API 함수를 호출하는 데 사용됩니다. 설명을 단순화하기 위해 SDK API 문서의 예시에서 클라이언트 초기화는 생략되었습니다.

### 버킷 생성

```Go
package main
import (
	"context"
	"io/ioutil"
	"net/http"
	"net/url"
	"os"
	"time"
	
	"github.com/tencentyun/cos-go-sdk-v5"
)

func main() {
	//<bucketname>, <appid> 및 <region>을 실제 정보로 수정합니다
	//예: http://test-1253846586.cos.ap-guangzhou.myqcloud.com
	u, _ := url.Parse("http://<bucketname>-<appid>.cos.<region>.myqcloud.com")
	b := &cos.BaseURL{BucketURL: u}
	c := cos.NewClient(b, &http.Client{
		Transport: &cos.AuthorizationTransport{
			//계정 및 키를 제대로 입력하고, 환경 변수로 설정할 수도 있습니다.
			SecretID:  os.Getenv("COS_SECRETID"),
			SecretKey: os.Getenv("COS_SECRETKEY"),
		},
	})
	
	_, err := c.Bucket.Put(context.Background(), nil)
	if err != nil {
		panic(err)
	}
}
```

### 파일 업로드

```Go
package main
import (
	"context"
	"net/url"
	"os"
	"strings"
	"net/http"

	"github.com/tencentyun/cos-go-sdk-v5"
)

func main() {
	//<bucketname>, <appid> 및 <region>을 실제 정보로 수정합니다
	//예: http://test-1253846586.cos.ap-guangzhou.myqcloud.com
	u, _ := url.Parse("http://<bucketname>-<appid>.cos.<region>.myqcloud.com")
	b := &cos.BaseURL{BucketURL: u}
	c := cos.NewClient(b, &http.Client{
		Transport: &cos.AuthorizationTransport{
            //계정 및 키를 제대로 입력하고, 환경 변수로 설정할 수도 있습니다
			SecretID:  os.Getenv("COS_SECRETID"),
			SecretKey: os.Getenv("COS_SECRETKEY"),
		},
	})
    //객체 키(Key)는 객체의 버킷에 있는 고유 식별자입니다.
	//예를 들어, 객체의 액세스 도메인 이름 ` bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/test/objectPut.go` 중, 객체 키는 test/objectPut.go입니다.
	name := "test/objectPut.go"
	//Local file
	f := strings.NewReader("test")

	_, err := c.Object.Put(context.Background(), name, f, nil)
	if err != nil {
		panic(err)
	}
}
```

### 파일 다운로드

```Go
package main

import (
	"context"
	"fmt"
	"net/url"
	"os"
	"io/ioutil"
	"net/http"

	"github.com/tencentyun/cos-go-sdk-v5"
)

func main() {
	//<bucketname>, <appid> 및 <region>을 실제 정보로 수정합니다
	//예: http://test-1253846586.cos.ap-guangzhou.myqcloud.com
	u, _ := url.Parse("http://<bucketname>-<appid>.cos.<region>.myqcloud.com")
	b := &cos.BaseURL{BucketURL: u}
	c := cos.NewClient(b, &http.Client{
		Transport: &cos.AuthorizationTransport{
			//계정 및 키를 제대로 입력하고, 환경 변수로 설정할 수도 있습니다
			SecretID:  os.Getenv("COS_SECRETID"),
			SecretKey: os.Getenv("COS_SECRETKEY"),
		},
	})
    //Object key
	name := "test/hello.txt"
	resp, err := c.Object.Get(context.Background(), name, nil)
	if err != nil {
		panic(err)
	}
	bs, _ := ioutil.ReadAll(resp.Body)
	resp.Body.Close()
	fmt.Printf("%s\n", string(bs))
}
```

