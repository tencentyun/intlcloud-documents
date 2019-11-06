## Download and Installation

#### Relevant Resources
- The COS XML SDK for Go source code can be downloaded [here](https://github.com/tencentyun/cos-go-sdk-v5).
- The sample demo can be download [here](https://github.com/tencentyun/cos-go-sdk-v5/tree/master/example).
- For more information, see [COS SDK for Go](https://godoc.org/github.com/tencentyun/cos-go-sdk-v5).

#### Environmental Dependency
- Go: Used to download and install the Go environment, which can be downloaded from Go's official website

#### Installing the SDK
You can install the COS SDK for Go by running the following command:
```
go get -u github.com/tencentyun/cos-go-sdk-v5/
```

## Getting Started
The section below describes how to perform basic operations with COS Go SDK, such as initializing a client, creating a bucket, querying bucket list, uploading an object, querying object list, downloading an object, and deleting an object.

### Initialization
You can use a COS domain name to generate a COS client structure for Go.

#### Method Prototype
```Go
func NewClient(uri *BaseURL, httpClient *http.Client) *Client
```

#### Sample Request
```go
// Replace <BucketName-APPID> and <region> with your own information
// For example: http://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com
u, _ := url.Parse("http://<BucketName-APPID>.cos.<region>.myqcloud.com")
b := &cos.BaseURL{BucketURL: u}
// 1. Permanent key
client := cos.NewClient(b, &http.Client{
	Transport: &cos.AuthorizationTransport{
		SecretID: "COS_SECRETID",
        SecretKey: "COS_SECRETKEY",                      
	},                                 
})
// 2. Temporary key
client := cos.NewClient(b, &http.Client{
	Transport: &cos.AuthorizationTransport{
		SecretID: "COS_SECRETID",
        SecretKey: "COS_SECRETKEY",    
        SessionToken："COS_SECRETTOKEN",
	},                                 
})
```

### Creating a Bucket

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
	// Replace <BucketName-APPID> and <region> with your own information
	// For example: http://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com
	u, _ := url.Parse("http://<BucketName-APPID>.cos.<region>.myqcloud.com")
	b := &cos.BaseURL{BucketURL: u}
	c := cos.NewClient(b, &http.Client{
		Transport: &cos.AuthorizationTransport{
			SecretID: "COS_SECRETID",
        	SecretKey: "COS_SECRETKEY",  
		},
	})
	
	_, err := c.Bucket.Put(context.Background(), nil)
	if err != nil {
		panic(err)
	}
}
```


### Querying the Bucket List
```go
package main

import (
	"context"
	"fmt"
	"os"
	"net/http"

	"github.com/tencentyun/cos-go-sdk-v5"
)

func main() {
	c := cos.NewClient(nil, &http.Client{
		Transport: &cos.AuthorizationTransport{
			SecretID: "COS_SECRETID",
        	SecretKey: "COS_SECRETKEY",  
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

### Uploading an Object
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
	// Replace <BucketName-APPID> and <region> with your own information
	// For example: http://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com
	u, _ := url.Parse("http://<BucketName-APPID>.cos.<region>.myqcloud.com")
	b := &cos.BaseURL{BucketURL: u}
	c := cos.NewClient(b, &http.Client{
		Transport: &cos.AuthorizationTransport{
			SecretID: "COS_SECRETID",
        	SecretKey: "COS_SECRETKEY",  
		},
	})
    	// An object key is the unique identifier of an object in a bucket.
	// For example, in the access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/test/objectPut.go`, the object key is test/objectPut.go
	name := "test/objectPut.go"
	// 1.Normal put string content
	f := strings.NewReader("test")

	_, err := c.Object.Put(context.Background(), name, f, nil)
	if err != nil {
		panic(err)
	}
	// 2.Put object by local file path
	_, err = c.Object.PutFromFile(context.Background(), name, "./test", nil)
	if err != nil {
		panic(err)
	}
}
```

### Querying the Object List
```go
package main

import (
	"context"
	"fmt"
	"os"
	"net/url"
	"net/http"

	"github.com/tencentyun/cos-go-sdk-v5"
)

func main() {
// Replace <BucketName-APPID> and <region> with your own information
	// For example: http://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com
	u, _ := url.Parse("http://<BucketName-APPID>.cos.<region>.myqcloud.com")
	b := &cos.BaseURL{BucketURL: u}
	c := cos.NewClient(b, &http.Client{
		Transport: &cos.AuthorizationTransport{
			SecretID: "COS_SECRETID",
        	SecretKey: "COS_SECRETKEY",  
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

### Downloading an Object
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
	// Replace <BucketName-APPID> and <region> with your own information
	// For example: http://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com
	u, _ := url.Parse("http://<BucketName-APPID>.cos.<region>.myqcloud.com")
	b := &cos.BaseURL{BucketURL: u}
	c := cos.NewClient(b, &http.Client{
		Transport: &cos.AuthorizationTransport{
			SecretID: "COS_SECRETID",
        	SecretKey: "COS_SECRETKEY",  
		},
	})
    // 1.Get object content by resp body.
	name := "test/hello.txt"
	resp, err := c.Object.Get(context.Background(), name, nil)
	if err != nil {
		panic(err)
	}
	bs, _ := ioutil.ReadAll(resp.Body)
	resp.Body.Close()
	fmt.Printf("%s\n", string(bs))
	// 2.Get object to local file path.
	_, err = c.Object.GetToFile(context.Background(), name, "example", nil)
	if err != nil {
		panic(err)
	}
}
```

### Deleting an Object
```go
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
	// Replace <BucketName-APPID> and <region> with your own information
	// For example: http://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com
	u, _ := url.Parse("http://<BucketName-APPID>.cos.<region>.myqcloud.com")
	b := &cos.BaseURL{BucketURL: u}
	c := cos.NewClient(b, &http.Client{
		Transport: &cos.AuthorizationTransport{
			SecretID: "COS_SECRETID",
        	SecretKey: "COS_SECRETKEY",  
		},
	})
	name := "test_object"
	_, err := c.Object.Delete(context.Background(), name)
	if err != nil {
    	panic(err)
    }
}
```
