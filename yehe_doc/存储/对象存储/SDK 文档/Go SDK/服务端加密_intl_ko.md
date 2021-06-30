
업로드한 객체에 암호화가 필요할 경우, 다음과 같은 암호화 방식을 지원합니다.

#### COS에서 호스팅하는 암호화 키를 사용한 서버 암호화(SSE-COS)로 데이터 보호

Tencent Cloud COS에서 마스터 키를 호스팅하고 데이터를 관리합니다. COS는 데이터센터에 데이터를 쓸 때 자동으로 암호화하며, 해당 데이터 사용 시 자동으로 암호화를 해제합니다. 현재 COS의 마스터 키를 사용한 AES-256 데이터 암호화를 지원합니다.

GO SDK는 'ObjectPutHeaderOptions'의 'XCosServerSideEncryption' 멤버 설정을 통해 완료합니다.

[//]: # (.cssg-snippet-put-object-sse)
```go
	// 객체 다운로드, 객체 다운로드 시 사용자 키 제공 필요	// 객체 다운로드, 객체 다운로드 시 사용자 키 package main 제공 필요

import (
	"context"
    "errors"
    "io/ioutil"
    "net/http"
    "net/url"
    "os"
    "strings"

    "github.com/tencentyun/cos-go-sdk-v5"
    "github.com/tencentyun/cos-go-sdk-v5/debug"
)

func main() {
    // 보유한 <Bucketname-APPID>로 변경
    u, _ := url.Parse("https://<Bucketname-APPID>.cos.ap-guangzhou.myqcloud.com")
    b := &cos.BaseURL{BucketURL: u}
    c := cos.NewClient(b, &http.Client{
            Transport: &cos.AuthorizationTransport{
                    SecretID:  os.Getenv("SECRETID"),
                    SecretKey: os.Getenv("SECRETKEY"),
                    Transport: &debug.DebugRequestTransport{
                            RequestHeader: true,
                            // Notice when put a large file and set need the request body, might happend out of memory error.
                            RequestBody:    false,
                            ResponseHeader: true,
                            ResponseBody:   true,
                    },
            },
    })
    opt := &cos.ObjectPutOptions{
            ObjectPutHeaderOptions: &cos.ObjectPutHeaderOptions{
                    ContentType:           "text/html",
    		        XCosServerSideEncryption: "AES256",
            },
            ACLHeaderOptions: &cos.ACLHeaderOptions{},
    }
    name := "PutFromGoWithSSE-COS"
    content := "Put Object From Go With SSE-COS"
    f := strings.NewReader(content)
    _, err := c.Object.Put(context.Background(), name, f, opt)
    if err != nil {
    	panic(err)
    }
	// 객체 다운로드
    getopt := &cos.ObjectGetOptions{}
    var resp *cos.Response
    resp, err = c.Object.Get(context.Background(), name, getopt)
    if err != nil {
    	panic(err)
    }
	// 인증
    bodyBytes, _ := ioutil.ReadAll(resp.Body)
    bodyContent := string(bodyBytes)
    if bodyContent != content {
    	panic(errors.New("Content inconsistency"))
    }
}
```

#### 고객이 제공한 암호화 키를 사용한 서버 암호화(SSE-C)로 데이터 보호

사용자가 암호화 키를 제공하며, 객체 업로드 시 COS가 사용자가 제공한 암호화 키로 사용자 데이터에 대한 AES-256 암호화를 진행합니다. GO SDK는 'ObjectPutHeaderOptions'의 'XCosSSECustomer*' 멤버 설정을 통해 완료합니다.

> !
>- 해당 암호화로 실행되는 서비스는 HTTPS를 사용해 요청해야 합니다.
>- customerKey: 사용자가 제공한 키로 32 바이트의 문자열입니다. 숫자, 알파벳, 문자 조합을 지원하지만 중국어는 지원하지 않습니다.
>- 업로드하는 원본 파일에서 해당 방법을 호출하는 경우 GET(다운로드), HEAD(조회) 사용 시, 원본 객체를 작업할 때도 해당 방법을 호출합니다.

[//]: # (.cssg-snippet-put-object-sse-c)
```go
package main

import (
	"context"
    "net/url"
    "os"
    "strings"
    "errors"
    "io/ioutil"
    "net/http"

    "github.com/tencentyun/cos-go-sdk-v5"
    "github.com/tencentyun/cos-go-sdk-v5/debug"
)

func main() {
    // 보유한 <Bucketname-APPID>로 변경
    u, _ := url.Parse("https://<Bucketname-APPID>.cos.ap-guangzhou.myqcloud.com")
    b := &cos.BaseURL{BucketURL: u}
    c := cos.NewClient(b, &http.Client{
            Transport: &cos.AuthorizationTransport{
                    SecretID:  os.Getenv("SECRETID"),
                    SecretKey: os.Getenv("SECRETKEY"),
                    Transport: &debug.DebugRequestTransport{
                            RequestHeader: true,
                            // Notice when put a large file and set need the request body, might happend out of memory error.
                            RequestBody:    false,
                            ResponseHeader: true,
                            ResponseBody:   true,
                    },
            },
    })
    opt := &cos.ObjectPutOptions{
            ObjectPutHeaderOptions: &cos.ObjectPutHeaderOptions{
                    ContentType: "text/html",
            		XCosSSECustomerAglo: "AES256",
                    XCosSSECustomerKey: "MDEyMzQ1Njc4OUFCQ0RFRjAxMjM0NTY3ODlBQkNERUY=",
                    XCosSSECustomerKeyMD5: "U5L61r7jcwdNvT7frmUG8g==",
                },
            ACLHeaderOptions: &cos.ACLHeaderOptions{},
    }
    name := "PutFromGoWithSSE-C"
    content := "Put Object From Go With SSE-C"
    f := strings.NewReader(content)
    _, err := c.Object.Put(context.Background(), name, f, opt)
    if err != nil {
    	panic(err)
    }
	// 객체 다운로드, 객체 다운로드 시 사용자 키 제공 필요
    getopt := &cos.ObjectGetOptions{
        XCosSSECustomerAglo: "AES256",
        XCosSSECustomerKey: "MDEyMzQ1Njc4OUFCQ0RFRjAxMjM0NTY3ODlBQkNERUY=",
        XCosSSECustomerKeyMD5: "U5L61r7jcwdNvT7frmUG8g==",
    }
    var resp *cos.Response
    resp, err = c.Object.Get(context.Background(), name, getopt)
    if err != nil {
        panic(err)
    }
	// 인증
    bodyBytes, _ := ioutil.ReadAll(resp.Body)
    bodyContent := string(bodyBytes)
    if bodyContent != content {
        panic(errors.New("Content inconsistency"))
    }
}
```
