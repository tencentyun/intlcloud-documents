
You can encrypt uploaded objects in the following ways.

#### Using server-side encryption with COS-managed encryption keys (SSE-COS) to protect data

With this method, your master key and data are managed by COS. COS can automatically encrypt your data when written into the IDC and automatically decrypt it when accessed. AES-256 encryption using a COS master key pair is supported.

For Go SDK, you can do so by setting the `XCosServerSideEncryption` member of `ObjectPutHeaderOptions`.

[//]: # (.cssg-snippet-put-object-sse)
```go
	// Download the object. You need to provide the key to download the object. 	 // Download the object. You need to provide the key to download the object. package main

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

func main(){
    // Replace it with your <Bucketname-APPID>
    u, _ := url.Parse("https://<Bucketname-APPID>.cos.ap-guangzhou.myqcloud.com")
    b := &cos.BaseURL{BucketURL: u}
    c := cos.NewClient(b, &http.Client{
            Transport: &cos.AuthorizationTransport{
                    SecretID: os.Getenv("SECRETID"),  // User `SecretId`. We recommend that you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://cloud.tencent.com/document/product/598/37140.
                    SecretKey: os.Getenv("SECRETKEY"),  // User `SecretKey`. We recommend that you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit  https://cloud.tencent.com/document/product/598/37140.
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
    if err != nil{
    	panic(err)
    }
	// Download an object
    getopt := &cos.ObjectGetOptions{}
    var resp *cos.Response
    resp, err = c.Object.Get(context.Background(), name, getopt)
    if err != nil{
    	panic(err)
    }
	// Verify
    bodyBytes, _ := ioutil.ReadAll(resp.Body)
    bodyContent := string(bodyBytes)
    if bodyContent != content {
    	panic(errors.New("Content inconsistency"))
    }
}
```

### Using server-side encryption with customer-provided encryption keys (SSE-C) to protect data

The encryption key is provided by you. When you upload an object, COS will use the encryption key to apply AES-256 encryption to the data. For Go SDK, you can do so by setting the `XCosSSECustomer*` member of `ObjectPutHeaderOptions`.

> !
>- This type of encryption requires using HTTPS requests.
>- customerKey: The key provided by the user. The key must be a 32-bit string that contains digits, letters, and special characters, but not Chinese characters.
>- If this encryption method was used when you uploaded the source file, you should also use it when you GET (download) or HEAD (query) this file.

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

func main(){
    // Replace it with your <Bucketname-APPID>
    u, _ := url.Parse("https://<Bucketname-APPID>.cos.ap-guangzhou.myqcloud.com")
    b := &cos.BaseURL{BucketURL: u}
    c := cos.NewClient(b, &http.Client{
            Transport: &cos.AuthorizationTransport{
                    SecretID: os.Getenv("SECRETID"),  // User `SecretId`. We recommend that you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://cloud.tencent.com/document/product/598/37140.
                    SecretKey: os.Getenv("SECRETKEY"),  // User `SecretKey`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit  https://cloud.tencent.com/document/product/598/37140.
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
    if err != nil{
    	panic(err)
    }
	Download the object. You need to provide the key to download the object.
    getopt := &cos.ObjectGetOptions{
        XCosSSECustomerAglo: "AES256",
        XCosSSECustomerKey: "MDEyMzQ1Njc4OUFCQ0RFRjAxMjM0NTY3ODlBQkNERUY=",
        XCosSSECustomerKeyMD5: "U5L61r7jcwdNvT7frmUG8g==",
    }
    var resp *cos.Response
    resp, err = c.Object.Get(context.Background(), name, getopt)
    if err != nil{
        panic(err)
    }
	// Verify
    bodyBytes, _ := ioutil.ReadAll(resp.Body)
    bodyContent := string(bodyBytes)
    if bodyContent != content {
        panic(errors.New("Content inconsistency"))
    }
}
```
