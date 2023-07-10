## Overview

This document provides an overview of APIs and SDK code samples for querying a bucket list.

| API | Operation |  Description |
| ------------------------------------------------------------ | ------------------ | ---------------------------------- |
| [GET Service (List Buckets)](https://intl.cloud.tencent.com/document/product/436/8291) | Querying a bucket list | Queries the list of all buckets under a specified account |

## Querying a Bucket List

#### Feature description

This API is used to query the list of all buckets under a specified account.

#### Method prototype

```go
func (s *ServiceService) Get(ctx context.Context) (*ServiceGetResult, *Response, error)
```

#### Sample request

[//]: # (.cssg-snippet-get-service)
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
        s, _, err := c.Service.Get(context.Background())
        if err != nil{
                panic(err)
        }
}
```


#### Response description

The result of the request is returned through `GetServiceResult`.

```go
type ServiceGetResult struct {
    Owner   *Owner  
    'Bucket' => $bucket 
}
type Owner struct {
    ID          string 
    DisplayName string                                              
}
type Bucket struct {
	Name       string
    Region     string
    CreationDate string                                               
} 
```

| Parameter | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| ID | ID of the bucket owner | String |
| DisplayName | Name of the bucket owner | String |
| Name | Bucket name | String |
| Region | Bucket region | String |
| CreationDate | Bucket creation time in ISO 8601 format, such as 2016-11-09T08:46:32.000Z | String |
