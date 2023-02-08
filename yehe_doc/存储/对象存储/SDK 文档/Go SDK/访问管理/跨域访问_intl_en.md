## Overview

This document provides an overview of APIs and SDK sample codes for cross-origin resource sharing (CORS).

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | ------------------------------ |
| [PUT Bucket cors](https://intl.cloud.tencent.com/document/product/436/8279) | Setting CORS configuration | Sets the CORS permissions of bucket |
| [GET Bucket cors](https://intl.cloud.tencent.com/document/product/436/8274) | Querying CORS configuration | Queries the CORS configuration of a bucket |
| [DELETE Bucket cors](https://intl.cloud.tencent.com/document/product/436/8283) | Deleting CORS configuration | Deletes the CORS configuration of a bucket |

## Setting CORS Configuration

#### Feature description

This API is used to set the CORS configuration of a specified bucket.

#### Method prototype
```go
func (s *BucketService) PutCORS(ctx context.Context, opt *BucketPutCORSOptions) (*Response, error)
```

#### Sample request
[//]: # (.cssg-snippet-put-bucket-cors)
```go
package main

import (
    "context"
    "github.com/tencentyun/cos-go-sdk-v5"
    "net/http"
    "net/url"
    "os"
)

func main(){
    // Bucket name in the format of `BucketName-APPID` (`APPID` is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
    // Replace it with your region, which can be viewed in the COS console at https://console.cloud.tencent.com/. For more information about regions, visit https://intl.cloud.tencent.com/document/product/436/6224.
    u, _ := url.Parse("https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com")
    b := &cos.BaseURL{BucketURL: u}
    client := cos.NewClient(b, &http.Client{
        Transport: &cos.AuthorizationTransport{
            // Get the key from environment variables
            // Environment variable `SECRETID` refers to the user's `SecretId`, which can be viewed in the CAM console at https://console.cloud.tencent.com/cam/capi.
            SecretID: os.Getenv("SECRETID"),  // User `SecretId`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://cloud.tencent.com/document/product/598/37140.
            // Environment variable `SECRETKEY` refers to the user's `SecretKey`, which can be viewed in the CAM console at https://console.cloud.tencent.com/cam/capi.
            SecretKey: os.Getenv("SECRETKEY"),  // User `SecretKey`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit  https://cloud.tencent.com/document/product/598/37140.
        },
    })
    opt := &cos.BucketPutCORSOptions{
        Rules: []cos.BucketCORSRule{
            {
                AllowedOrigins: []string{"http://www.qq.com"},
                AllowedMethods: []string{"PUT", "GET"},
                AllowedHeaders: []string{"x-cos-meta-test", "x-cos-xx"},
                MaxAgeSeconds:  500,
                ExposeHeaders:  []string{"x-cos-meta-test1"},
            },
            {
                ID:             "1234",
                AllowedOrigins: []string{"http://www.baidu.com", "twitter.com"},
                AllowedMethods: []string{"PUT", "GET"},
                MaxAgeSeconds:  500,
            },
        },
    }
    _, err := client.Bucket.PutCORS(context.Background(), opt)
    if err != nil{
        panic(err)
    }
}
```

#### Field description

```go
type BucketCORSRule struct {
	ID             string   
	AllowedMethods []string 
	AllowedOrigins []string 
	AllowedHeaders []string 
	MaxAgeSeconds  int      
	ExposeHeaders  []string 
}
```

| Parameter | Description | Type | Required |
| -------------- | ------------------------------------------------------------ | -------- | ---- |
| BucketCORSRule | CORS rules, including `ID`, `MaxAgeSeconds`, `AllowedOrigin`, `AllowedMethod`, `AllowedHeader`, and `ExposeHeader` | struct | Yes |
| ID | Rule ID | string | No |
| AllowedMethods | Allowed methods, including GET, PUT, HEAD, POST, and DELETE | []string | Yes |
| AllowedOrigins | Allowed access sources, such as `"http://cloud.tencent.com"`. Asterisks (*) are supported. | []string | Yes |
| AllowedHeaders | Allowed custom HTTP request headers that can be used by requests. Asterisks (*) are supported. | []string | No |
| MaxAgeSeconds | Validity period of the `OPTIONS` request result | int | No |
| ExposeHeaders | Custom header information that can be received by the browser from the server | []string | No |


## Querying CORS Configuration

#### Feature description

This API is used to query the CORS configuration of a bucket.

#### Method prototype
```go
func (s *BucketService) GetCORS(ctx context.Context) (*BucketGetCORSResult, *Response, error)
```

#### Sample request
[//]: # (.cssg-snippet-get-bucket-cors)
```go
package main

import (
    "context"
    "github.com/tencentyun/cos-go-sdk-v5"
    "net/http"
    "net/url"
    "os"
)

func main(){
    // Bucket name in the format of `BucketName-APPID` (`APPID` is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
    // Replace it with your region, which can be viewed in the COS console at https://console.cloud.tencent.com/. For more information about regions, visit https://intl.cloud.tencent.com/document/product/436/6224.
    u, _ := url.Parse("https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com")
    b := &cos.BaseURL{BucketURL: u}
    client := cos.NewClient(b, &http.Client{
        Transport: &cos.AuthorizationTransport{
            // Get the key from environment variables
            // Environment variable `SECRETID` refers to the user's `SecretId`, which can be viewed in the CAM console at https://console.cloud.tencent.com/cam/capi.
            SecretID: os.Getenv("SECRETID"),  // User `SecretId`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://cloud.tencent.com/document/product/598/37140.
            // Environment variable `SECRETKEY` refers to the user's `SecretKey`, which can be viewed in the CAM console at https://console.cloud.tencent.com/cam/capi.
            SecretKey: os.Getenv("SECRETKEY"),  // User `SecretKey`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit  https://cloud.tencent.com/document/product/598/37140.
        },
    })
    _, _, err := client.Bucket.GetCORS(context.Background())
    if err != nil{
        panic(err)
    }
}
```

#### Response description
The result of the request is returned through `GetBucketCORSResult`.

```go
type BucketCORSRule struct {
	ID             string   
	AllowedMethods []string 
	AllowedOrigins []string 
	AllowedHeaders []string 
	MaxAgeSeconds  int      
	ExposeHeaders  []string 
}
```

| Parameter | Description | Type | Required |
| -------------- | ------------------------------------------------------------ | -------- | ---- |
| BucketCORSRule | CORS rules, including `ID`, `MaxAgeSeconds`, `AllowedOrigin`, `AllowedMethod`, `AllowedHeader`, and `ExposeHeader` | struct | Yes |
| ID | Rule ID | string | No |
| AllowedMethods | Allowed methods, including GET, PUT, HEAD, POST, and DELETE | []string | Yes |
| AllowedOrigins | Allowed access sources, such as `"http://cloud.tencent.com"`. Asterisks (*) are supported. | []string | Yes |
| AllowedHeaders | Allowed custom HTTP request headers that can be used by requests. Asterisks (*) are supported. | []string | No |
| MaxAgeSeconds | Validity period of the `OPTIONS` request result | int | No |
| ExposeHeaders | Custom header information that can be received by the browser from the server | []string | No |

## Deleting CORS Configuration

#### Feature description

This API is used to delete the CORS configuration of a bucket.

#### Method prototype

```go
func (s *BucketService) DeleteCORS(ctx context.Context) (*Response, error)
```

#### Sample request
[//]: # (.cssg-snippet-delete-bucket-cors)
```go
package main

import (
    "context"
    "github.com/tencentyun/cos-go-sdk-v5"
    "net/http"
    "net/url"
    "os"
)

func main(){
    // Bucket name in the format of `BucketName-APPID` (`APPID` is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
    // Replace it with your region, which can be viewed in the COS console at https://console.cloud.tencent.com/. For more information about regions, visit https://intl.cloud.tencent.com/document/product/436/6224.
    u, _ := url.Parse("https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com")
    b := &cos.BaseURL{BucketURL: u}
    client := cos.NewClient(b, &http.Client{
        Transport: &cos.AuthorizationTransport{
            // Get the key from environment variables
            // Environment variable `SECRETID` refers to the user's `SecretId`, which can be viewed in the CAM console at https://console.cloud.tencent.com/cam/capi.
            SecretID: os.Getenv("SECRETID"),  // User `SecretId`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://cloud.tencent.com/document/product/598/37140.
            // Environment variable `SECRETKEY` refers to the user's `SecretKey`, which can be viewed in the CAM console at https://console.cloud.tencent.com/cam/capi.
            SecretKey: os.Getenv("SECRETKEY"),  // User `SecretKey`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit  https://cloud.tencent.com/document/product/598/37140.
        },
    })
    _, err := client.Bucket.DeleteCORS(context.Background())
    if err != nil{
        panic(err)
    }
}
```
