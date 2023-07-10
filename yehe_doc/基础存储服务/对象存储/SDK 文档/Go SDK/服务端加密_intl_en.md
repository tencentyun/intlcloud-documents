
You can encrypt objects uploaded to COS in the following ways.

#### Using server-side encryption with COS-managed encryption keys (SSE-COS) to protect data

With this method, your master key and data are managed by COS. COS can automatically encrypt your data when written into the IDC and automatically decrypt it when accessed. Currently, COS supports AES-256 encryption using a COS master key pair.

In this SDK, you need to configure the encryption by specifying the `XCosServerSideEncryption` member in `ObjectPutHeaderOptions`.

[//]: # (.cssg-snippet-put-object-sse)
```go
	// Download an object, which requires the customer-provided key                                    package main

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
    // Replace with your own Bucketname-APPID
    u, _ := url.Parse("https://<Bucketname-APPID>.cos.ap-guangzhou.myqcloud.com")
    b := &cos.BaseURL{BucketURL: u}
    c := cos.NewClient(b, &http.Client{
            Transport: &cos.AuthorizationTransport{
                    SecretID:  os.Getenv("SECRETID"),
                    SecretKey: os.Getenv("SECRETKEY"),
                    Transport: &debug.DebugRequestTransport{
                            RequestHeader: true,
                            // Note that when a large file is uploaded and a request body is used, an error may occur due to insufficient memory.
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
	// Download an object
    getopt := &cos.ObjectGetOptions{}
    var resp *cos.Response
    resp, err = c.Object.Get(context.Background(), name, getopt)
    if err != nil {
    	panic(err)
    }
	// Validate
    bodyBytes, _ := ioutil.ReadAll(resp.Body)
    bodyContent := string(bodyBytes)
    if bodyContent != content {
    	panic(errors.New("Content inconsistency"))
    }
}
```

### Using server-side encryption with customer-provided encryption keys (SSE-C) to protect data

With this method, the encryption key is provided by the customer. When you upload an object, COS will apply AES-256 encryption to your data using the customer-provided encryption key pair. In this SDK, you need to configure the encryption by specifying the `XCosSSECustomer*` member in `ObjectPutHeaderOptions`.

> !
>- This type of encryption requires using HTTPS requests.
>- customerKey: the key provided by the user; this key should be a 32-byte string that contains numbers, letters, and special characters, but not Chinese characters.
>- If this encryption method was used when you uploaded a file, you should also use it when you GET (download) or HEAD (query) this file.

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
    // Replace with your own Bucketname-APPID
    u, _ := url.Parse("https://<Bucketname-APPID>.cos.ap-guangzhou.myqcloud.com")
    b := &cos.BaseURL{BucketURL: u}
    c := cos.NewClient(b, &http.Client{
            Transport: &cos.AuthorizationTransport{
                    SecretID:  os.Getenv("SECRETID"),
                    SecretKey: os.Getenv("SECRETKEY"),
                    Transport: &debug.DebugRequestTransport{
                            RequestHeader: true,
                            // Note that when a large file is uploaded and a request body is used, an error may occur due to insufficient memory.
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
	// Download an object, which requires the customer-provided key
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
	// Validate
    bodyBytes, _ := ioutil.ReadAll(resp.Body)
    bodyContent := string(bodyBytes)
    if bodyContent != content {
        panic(errors.New("Content inconsistency"))
    }
}
```
