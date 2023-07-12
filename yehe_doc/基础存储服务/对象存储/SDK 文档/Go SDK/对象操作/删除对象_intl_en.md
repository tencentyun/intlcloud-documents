## Overview

This document provides an overview of APIs and SDK code samples for deleting an object.

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | ---------------------- |
| [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743) | Deleting an object | Deletes an object from a bucket. |
| [DELETE Multiple Objects](https://intl.cloud.tencent.com/document/product/436/8289) | Deleting multiple objects | Deletes multiple objects from a bucket. |

## Deleting a Single Object

#### Feature description

This API is used to delete an object (folder) from a bucket.

#### Method prototype

```go
func (s *ObjectService) Delete(ctx context.Context, key string) (*Response, error)
```

#### Sample 1: deleting an object

[//]: # (.cssg-snippet-delete-object)
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
    key := "exampleobject"
    _, err := client.Object.Delete(context.Background(), key)
    if err != nil{
        panic(err)
    }
}
```

#### Sample 2: deleting a folder

This request does not delete objects in the folder but only the specified key.

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
    key := "folder/"
    _, err := client.Object.Delete(context.Background(), key)
    if err != nil{
        panic(err)
    }
}
```

#### Field description

| Parameter | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ------ | ---- |
| key  | Object key, the unique identifier of an object in a bucket. For example, if the object endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg`. | String | Yes |

## Deleting Multiple Objects

#### Feature description

This API is used to delete multiple objects from a bucket. You can delete up to 1,000 objects in one request.

#### Method prototype

```go
func (s *ObjectService) DeleteMulti(ctx context.Context, opt *ObjectDeleteMultiOptions) (*ObjectDeleteMultiResult, *Response, error)
```

#### Sample 1: deleting multiple specified objects

[//]: # (.cssg-snippet-delete-multi-object)
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
    var objects []string
    objects = append(objects, []string{"a", "b", "c"}...)
    obs := []cos.Object{}
    for _, v := range objects {
        obs = append(obs, cos.Object{Key: v})
    }
    opt := &cos.ObjectDeleteMultiOptions{
        Objects: obs,
        // Boolean, which indicates whether to enable the Quiet or Verbose mode.
        // `true` indicates the Quiet mode and `false` (default) indicates the Verbose mode.
        // Quiet: true,
    }

    _, _, err := client.Object.DeleteMulti(context.Background(), opt)
    if err != nil{
        panic(err)
    }
}
```

#### Sample 2: deleting a folder and the objects contained

COS uses slashes (/) to separate object paths to simulate the effect of a file system. Therefore, deleting a folder in COS means deleting all objects that have a specified prefix. For example, the folder 'prefix/' contains all objects prefixed with 'prefix/'. In other words, you can delete all objects prefixed with 'prefix/' to delete the 'prefix/' folder.
Currently, the COS Go SDK does not provide an API to perform this operation. However, you can still use a combination of basic operations to do so.

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
    dir := "exampledir/"
    var marker string
    opt := &cos.BucketGetOptions{
        Prefix:  dir,
        MaxKeys: 1000,
    }
    isTruncated := true
    for isTruncated {
        opt.Marker = marker
        v, _, err := client.Bucket.Get(context.Background(), opt)
        if err != nil{
            // Error
            break
        }
        for _, content := range v.Contents {
            _, err = client.Object.Delete(context.Background(), content.Key)
            if err != nil{
                // Error
            }
        }
        isTruncated = v.IsTruncated
        marker = v.NextMarker
    }
}
```


#### Field description

```go
type ObjectDeleteMultiOptions struct {
	Quiet   bool
	Objects []Object   
}
// “Object” stores object metadata
type Object struct {
	Key          string
    // Other parameters are not related to this API
}
```

| Parameter | Description | Type | Required |
| -------- | ------------------------------------------------------------ | --------- | ---- |
| Quiet | Indicates whether to enable the Quiet mode for the response result. Valid values:<br><li>`true`: enables the Quiet mode that only returns information on objects that fail</br><li>`false` (default): enables the Verbose mode that returns the deletion result for each object</li> | Boolean | No |
| Objects | Describes each destination object to be deleted | Container | Yes |
| Key | Name of the destination object | String | Yes |

#### Response description

Attributes of the uploaded file:

```go
// “ObjectDeleteMultiResult” saves the DeleteMulti result
type ObjectDeleteMultiResult struct {	
    DeletedObjects []Object
    Errors         []struct {
		    Key     string
		    Code    string
		    Message string
	   }
}
```

| Parameter | Description | Type |
| -------------- | ---------------------------------- | --------- |
| DeletedObjects |Describes each object deleted | Container |
| Errors| Describes objects that failed to be deleted | Container |
| Key | Names of the objects that failed to be deleted | String |
| Code | Error code for the deletion failure | String |
| Message | Error message for the deletion failure | String |
