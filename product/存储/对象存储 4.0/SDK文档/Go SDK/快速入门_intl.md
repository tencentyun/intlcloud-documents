## Preparations for Development

### Related resources
Download XML Go SDK resources of COS service from [XML Go SDK](https://github.com/tencentyun/cos-go-sdk-v5). For more information, see [COS Go SDK API](https://godoc.org/github.com/tencentyun/cos-go-sdk-v5).

### Environment dependencies

[Golang](https://golang.org/doc/install/source?spm=a2c4g.11186623.2.11.168ec486fb1eQK) is used to download and install the Go compilation and runtime environments. After Go is installed, create a system variable GOPATH and point it to your code directory.
>For more information on the definitions of SecretId, SecretKey, Bucket and other terms and how to obtain them, see [COS Glossary](https://cloud.tencent.com/document/product/436/7751).

### Install SDK

Execute the following command to install COS Go SDK:
```
 go get -u github.com/tencentyun/cos-go-sdk-v5/
```

## Getting Started
This section describes how to get started with COS Go SDK and perform common operations such as initializing the client, creating a bucket, and uploading/downloading a file.
The use cases of each API can be found in the [example](https://github.com/tencentyun/cos-go-sdk-v5/tree/master/example) directory.
### Initialize the client

The COS GO client structure is generated using the COS domain name.

#### Method prototype
```Go
func NewClient(uri *BaseURL, httpClient *http.Client) *Client
```
#### Request example
```go
//Replace <bucketname>, <appid> and <region> with true information.
//For example: http://test-1253846586.cos.ap-guangzhou.myqcloud.com
u, _ := url.Parse("http://<bucketname>-<appid>.cos.<region>.myqcloud.com")
b := &cos.BaseURL{BucketURL: u}
client := cos.NewClient(b, &http.Client{
	Transport: &cos.AuthorizationTransport{
		//Enter the user ID and key, or set them as environment variables.
		SecretID:  os.Getenv("COS_SECRETID"),                         
		SecretKey: os.Getenv("COS_SECRETKEY"),                      
	},                                 
})
```
#### Parameters
```go
type AuthorizationTransport struct {
	SecretID     string
	SecretKey    string
	SessionToken string
	// Validity period of the signature
	Expire time.Duration         
}
```
#### Returned result
The returned client contains the Service, Bucket and Object structures that are used to call their API functions respectively. To make it simple, the client initialization process is not introduced in the examples of the SDK API documentation.

### Create a bucket

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
	//Replace <bucketname>, <appid> and <region> with true information.
	//For example: http://test-1253846586.cos.ap-guangzhou.myqcloud.com
	u, _ := url.Parse("http://<bucketname>-<appid>.cos.<region>.myqcloud.com")
	b := &cos.BaseURL{BucketURL: u}
	c := cos.NewClient(b, &http.Client{
		Transport: &cos.AuthorizationTransport{
			//Enter the account ID and key, or set them as environment variables.
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

### Upload a file

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
	//Replace <bucketname>, <appid> and <region> with true information.
	//For example: http://test-1253846586.cos.ap-guangzhou.myqcloud.com
	u, _ := url.Parse("http://<bucketname>-<appid>.cos.<region>.myqcloud.com")
	b := &cos.BaseURL{BucketURL: u}
	c := cos.NewClient(b, &http.Client{
		Transport: &cos.AuthorizationTransport{
            //Enter the account ID and key, or set them as environment variables.
			SecretID:  os.Getenv("COS_SECRETID"),
			SecretKey: os.Getenv("COS_SECRETKEY"),
		},
	})
    //Object key is the unique identifier of the object in the bucket.
	//For example, in the object's access domain name `bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/test/objectPut.go`, the object key is test/objectPut.go.
	name := "test/objectPut.go"
	//Local file
	f := strings.NewReader("test")

	_, err := c.Object.Put(context.Background(), name, f, nil)
	if err != nil {
		panic(err)
	}
}
```

### Download a file

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
	//Replace <bucketname>, <appid> and <region> with true information.
	//For example: http://test-1253846586.cos.ap-guangzhou.myqcloud.com
	u, _ := url.Parse("http://<bucketname>-<appid>.cos.<region>.myqcloud.com")
	b := &cos.BaseURL{BucketURL: u}
	c := cos.NewClient(b, &http.Client{
		Transport: &cos.AuthorizationTransport{
			//Enter the account ID and key, or set them as environment variables.
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

