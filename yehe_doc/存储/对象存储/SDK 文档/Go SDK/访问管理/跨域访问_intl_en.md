## Overview

This document provides an overview of APIs and SDK sample codes related to cross-origin access.

| API | Operation Name | Description |
| ------------------------------------------------------------ | ------------ | ------------------------------ |
| [PUT Bucket cors](https://intl.cloud.tencent.com/document/product/436/8279) | Setting CORS configuration | Sets CORS permissions for a bucket |
| [GET Bucket cors](https://intl.cloud.tencent.com/document/product/436/8274) | Querying CORS configuration | Queries the CORS configuration of a bucket |
| [DELETE Bucket cors](https://intl.cloud.tencent.com/document/product/436/8283) | Deleting CORS configuration | Deletes the CORS configuration of a bucket |

## Setting CORS

#### Feature description

This API (PUT Bucket cors) is used to set CORS for a bucket.

#### Method prototype
```go
func (s *BucketService) PutCORS(ctx context.Context, opt *BucketPutCORSOptions) (*Response, error)
```

#### Sample request
[//]: # ".cssg-snippet-put-bucket-cors"
```go
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
if err != nil {
    panic(err)
}
```

#### Parameter description

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


## Querying a CORS Configuration

#### Feature description

This API (GET Bucket cors) is used to query the CORS configuration of a bucket.

#### Method prototype
```go
func (s *BucketService) GetCORS(ctx context.Context) (*BucketGetCORSResult, *Response, error)
```

#### Sample request
[//]: # ".cssg-snippet-get-bucket-cors"
```go
_, _, err := client.Bucket.GetCORS(context.Background())
if err != nil {
    panic(err)
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

This API (DELETE Bucket cors) is used to delete the CORS configuration of a bucket.

#### Method prototype

```go
func (s *BucketService) DeleteCORS(ctx context.Context) (*Response, error)
```

#### Sample request
[//]: # ".cssg-snippet-delete-bucket-cors"
```go
_, err := client.Bucket.DeleteCORS(context.Background())
if err != nil {
    panic(err)
}
```
