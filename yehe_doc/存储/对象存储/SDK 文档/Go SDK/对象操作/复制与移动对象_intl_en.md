## Overview

This document provides an overview of APIs and SDK code samples for copying and moving an object.

**Simple operations**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881) | Copying an object (modifying object attributes) | Copies a file to a destination path. |

**Multipart operations**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ------------------------ |
| [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746) | Initializing a multipart upload/copy operation | Initializes a multipart upload/copy operation. |
| [Upload Part - Copy](https://intl.cloud.tencent.com/document/product/436/8287) | Copying a part | Copies an object as a part. |
| [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742) | Completing a multipart upload/copy | Completes the multipart upload/copy of an object. |

## Simple Operations

### Copying an object

This API (`PUT Object - Copy`) is used to create a copy of an existing COS object, that is, to copy an object from the source path (object key) to the destination path (object key). During the process, object metadata and ACLs can be modified.
You can use this API to create a copy of an object, modify an object’s metadata (the source object and destination file have the same attributes), and move or rename an object (copy the object first and then call the deletion API).

#### Method prototype

```go
func (s *ObjectService) Copy(ctx context.Context, key, sourceURL string, opt *ObjectCopyOptions) (*ObjectCopyResult, *Response, error)
```

#### Sample 1: copying an object

[//]: # (.cssg-snippet-copy-object)
```go
package main

import (
    "context"
    "fmt"
    "github.com/tencentyun/cos-go-sdk-v5"
    "net/http"
    "net/url"
    "os"
    "strings"
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
    name := "exampleobject"
    // Upload the source object
    f := strings.NewReader("test")
    _, err := client.Object.Put(context.Background(), name, f, nil)

    sourceURL := fmt.Sprintf("examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/%s", name)
    dest := "example_dest"
    // Considering the ACL limit, we recommend you not set an object ACL when uploading an object unless required. The object will then inherit the bucket ACL by default.
    // opt := &cos.ObjectCopyOptions{}
    _, _, err = client.Object.Copy(context.Background(), dest, sourceURL, nil)
    if err != nil{
        panic(err)
    }
}
```

#### Sample 2: moving an object

```go
package main

import (
    "context"
    "fmt"
    "github.com/tencentyun/cos-go-sdk-v5"
    "net/http"
    "net/url"
    "os"
    "strings"
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
    source := "test/oldfile"
    f := strings.NewReader("test")
    // Upload the file
    _, err := client.Object.Put(context.Background(), source, f, nil)
    if err != nil{
        // Error
    }

    // Move the object
    dest := "test/newfile"
    sourceURL := fmt.Sprintf("examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/%s", source)
    _, _, err = client.Object.Copy(context.Background(), dest, sourceURL, nil)
    if err == nil {
        _, err = client.Object.Delete(context.Background(), source, nil)
        if err != nil{
            // Error
        }
    }
}
```

#### Sample 3: modifying storage class

>!You can change STANDARD to STANDARD_IA, INTELLIGENT TIERING, ARCHIVE, or DEEP ARCHIVE. To modify ARCHIVE or DEEP ARCHIVE to other storage classes, you need to call `PostRestore` to restore objects in ARCHIVE or DEEP ARCHIVE first before calling this API. For more information, see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/436/30925).

```go
package main

import (
    "context"
    "fmt"
    "github.com/tencentyun/cos-go-sdk-v5"
    "net/http"
    "net/url"
    "os"
    "strings"
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
    name := "exampleobject"
    // Upload the source object
    f := strings.NewReader("test")
    _, err := client.Object.Put(context.Background(), name, f, nil)

    sourceURL := fmt.Sprintf("%s/%s", client.BaseURL.BucketURL.Host, name)
    opt := &cos.ObjectCopyOptions{
        &cos.ObjectCopyHeaderOptions{
            XCosMetadataDirective: "Replaced",
            XCosStorageClass:      "Archive", // Modify the storage class to ARCHIVE.
        },
        nil,
    }
    _, _, err = client.Object.Copy(context.Background(), name, sourceURL, opt)
    if err != nil{
        panic(err)
    }
}

```

#### Field description

```go
type ObjectCopyOptions struct {
    *ObjectCopyHeaderOptions 
    *ACLHeaderOptions        
}
type ACLHeaderOptions struct {
    XCosACL              string 
    XCosGrantRead        string 
    XCosGrantWrite       string 
    XCosGrantFullControl string 
}
type ObjectCopyHeaderOptions struct {
    XCosMetadataDirective           string 
    XCosCopySourceIfModifiedSince   string 
    XCosCopySourceIfUnmodifiedSince string 
    XCosCopySourceIfMatch           string 
    XCosCopySourceIfNoneMatch       string 
    XCosStorageClass                string 
    // Custom x-cos-meta-* header
    XCosMetaXXX    				    *http.Header 
    XCosCopySource 					string      
}
```

| Parameter | Description | Type | Required |
| ------------------------------- | ------------------------------------------------------------ | ----------- | -------- |
| key  | `ObjectKey` is the unique identifier of an object in a bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the `ObjectKey` is `doc/pic.jpg`. | String | Yes |
| sourceURL | URL of the source file to copy | String | Yes |
| XCosACL | Sets the file ACL, such as `private`, `public-read`, and `public-read-write` | String | No |
| XCosGrantFullControl | Grants full permission in the format: `id="[OwnerUin]"` | String | No |
| XCosGrantRead| Grants the read permission in the format: id="[OwnerUin]" | String | No |
|  XCosMetadataDirective | Valid values:</br><li>`Copy`: copies the source object along with its metadata.</li><li>`Replaced`: copies the source object while replacing its metadata.</li>If the destination path is the same as the source path, this parameter must be set to `Replaced`. | String | Yes |
| XCosCopySourceIfModifiedSince | If the object is modified after the specified time, the operation will be performed; otherwise, 412 will be returned. This parameter can be used together with `XCosCopySourceIfNoneMatch`. If it is used together with other conditions, a conflict will be returned. | String | No |
| XCosCopySourceIfUnmodifiedSince | If the object is not modified after the specified time, the operation will be performed; otherwise, 412 will be returned. This parameter can be used together with `XCosCopySourceIfMatch`. If it is used together with other conditions, a conflict will be returned. | String | No |
| XCosCopySourceIfMatch | If the `ETag` of the object is the same as the specified one, the operation will be performed; otherwise, 412 will be returned. This parameter can be used together with `XCosCopySourceIfUnmodifiedSince`. If it is used together with other conditions, a conflict will be returned. | String | No |
| XCosCopySourceIfNoneMatch | If the `Etag` of the object is different from the specified one, the operation will be performed; otherwise, 412 will be returned. This parameter can be used together with `XCosCopySourceIfModifiedSince`. If it is used together with other conditions, a conflict will be returned. | String | No |
| XCosStorageClass | Sets the object storage class. Valid values: STANDARD (default), STANDARD_IA, ARCHIVE. | String | No |
| XCosMetaXXX | User-defined file metadata. | http.Header | No |
| XCosCopySource | Source file URL. You can specify a historical version using the `versionid` subresource. | String | No |

#### Response description

Attributes of the uploaded file:

```go
type ObjectCopyResult struct {
    ETag         string 
    LastModified string
}
```

| Parameter | Description | Type |
| ------------ | -------------------------- | ------ |
| ETag | MD5 of the copied file | String |
| LastModified | Last modified time of the copied file | String |

### Moving an object

#### Feature description

Object movement involves copying the source object to the target location and deleting the source object.

Since COS uses the bucket name (`Bucket`) and object key (`ObjectKey`) to identify objects, moving an object will change the object identifier. Currently, the PHP SDK does not provide a standalone API to change object identifiers. However, you can still move the object with a combination of basic operations (object copy and object deletion).

For example, if you want to move the `picture.jpg` object to the “doc” directory that is in the same bucket (`mybucket-1250000000`), you can copy the `picture.jpg` to the “doc” directory (making the object key `doc/picture.jpg`) and then delete the source object.

Likewise, if you need to move `picture.jpg` in the `mybucket-1250000000` bucket to another bucket `myanothorbucket-1250000000`, you can copy the object to the `myanothorbucket-1250000000` bucket first and then delete the source object.

#### Sample request

```go
package main

import (
    "context"
    "fmt"
    "github.com/tencentyun/cos-go-sdk-v5"
    "net/http"
    "net/url"
    "os"
    "strings"
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
    source := "test/oldfile"
    f := strings.NewReader("test")
    // Upload the file
    _, err := client.Object.Put(context.Background(), source, f, nil)
    if err != nil{
        // Error
    }
    // Move the object
    dest := "test/newfile"
    sourceURL := fmt.Sprintf("%s/%s", u.Host, source)
    _, _, err = client.Object.Copy(context.Background(), dest, sourceURL, nil)
    if err == nil {
        _, err = client.Object.Delete(context.Background(), source, nil)
        if err != nil{
            // Error
        }
    }
}
```

## Multipart Operations

### Initializing a multipart copy

#### Feature description

This API is used to initialize a multipart copy. After a successful operation, an `upload ID` will be returned, which can be used in the subsequent `Upload Part - Copy` requests.

#### Method prototype

```go
func (s *ObjectService) InitiateMultipartUpload(ctx context.Context, name string, opt *InitiateMultipartUploadOptions) (*InitiateMultipartUploadResult, *Response, error)
```

#### Sample request

```go
package main

import (
    "context"
    "fmt"
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
    name := "exampleobject"
    v, _, err := client.Object.InitiateMultipartUpload(context.Background(), name, nil)
    if err != nil{
        panic(err)
    }
    UploadID := v.UploadID
    fmt.Println(UploadID)
}
```

#### Field description

```go
type InitiateMultipartUploadOptions struct {
    *ACLHeaderOptions       
    *ObjectPutHeaderOptions 
}
type ACLHeaderOptions struct {
    XCosACL              string                           
    XCosGrantRead        string
    XCosGrantWrite       string 
    XCosGrantFullControl string                                           
} 
type ObjectPutHeaderOptions struct {
    CacheControl       string 
    ContentDisposition string 
    ContentEncoding    string 
    ContentType        string 
    ContentLength      int64   
    Expires            string 
    // Custom x-cos-meta-* header
    XCosMetaXXX        *http.Header 
    XCosStorageClass   string      
}

```

| Parameter | Description | Type | Required |
| -------------------- | ------------------------------------------------------------ | ----------- | -------- |
| key  | `ObjectKey` is the unique identifier of an object in a bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the `ObjectKey` is `doc/pic.jpg`. | String | Yes |
| XCosACL | Sets the file ACL, such as `private` or `public-read` | String | No |
| XCosGrantFullControl | Grants full permission in the format: `id="[OwnerUin]"` | String | No |
| XCosGrantRead | Grants read permission in the format: id="[OwnerUin]" | String | No |
| XCosStorageClass | Sets the object storage class. Valid values: STANDARD (default), STANDARD_IA, ARCHIVE | String | No |
| Expires | Sets `Content-Expires` | String | No |
| CacheControl | Cache policy. Sets `Cache-Control` | String | No |
| ContentType | Content Type. Sets `Content-Type` | String | No |
| ContentDisposition | Filename. Sets `Content-Disposition` | String | No |
| ContentEncoding | Encoding format. Sets `Content-Encoding` | String | No |
| ContentLength | Sets the length of the request content | Int64 | No |
| XCosMetaXXX | User-defined file metadata. It must start with x-cos-meta. Otherwise, it will be ignored | http.Header | No |

#### Response description

```go
type InitiateMultipartUploadResult struct {
    Bucket   string
    Key      string
    UploadID string
} 
```

| Parameter | Description | Type |
| -------- | ------------------------------------------------------------ | ------ |
| UploadId | ID that identifies the multipart upload | string |
| Bucket | Bucket name in the format of `BucketName-APPID` | string |
| key  | `ObjectKey` is the unique identifier of an object in a bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the `ObjectKey` is `doc/pic.jpg` | String |

### Copying an object part

#### Feature description

This API (`Upload Part - Copy`) is used to copy a part of an object from the source path to the destination path.

> !To copy an object part, you must first initialize a multipart upload, after which a unique upload ID will be returned. This ID is required in the copy request.

#### Method prototype
```go
func (s *ObjectService) CopyPart(ctx context.Context, key, uploadID string, partNumber int, sourceURL string, opt *ObjectCopyPartOptions) (*CopyPartResult, *Response, error)
```

#### Sample request
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
    // Initialize multipart upload
    name := "exampleobject"
    v, _, err := client.Object.InitiateMultipartUpload(context.Background(), name, nil)
    if err != nil{
        // ERROR
    }
    uploadID := v.UploadID

    // Copying an object part
    sourceUrl := "examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/sourceobject"
    res, _, err := client.Object.CopyPart(context.Background(), name, uploadID, 1, sourceUrl, nil)
    if err != nil{
        // ERROR
    }

    // Complete the multipart upload.
    completeOpt := &cos.CompleteMultipartUploadOptions{}
    completeOpt.Parts = append(completeOpt.Parts, cos.Object{
        PartNumber: 1,
        ETag:       res.ETag,
    })
    _, _, err = client.Object.CompleteMultipartUpload(context.Background(), name, uploadID, completeOpt)
    if err != nil{
        // ERROR
    }
}
```
#### Field description

```go
type ObjectCopyPartOptions struct {
    XCosCopySourceRange
    XCosCopySourceIfModifiedSince
    XCosCopySourceIfUnmodifiedSince
    XCosCopySourceIfMatch
    XCosCopySourceIfNoneMatch
}
```

| Parameter | Description | Type | Required |
| ------------ | ------------------------------------------------------------ | ------ | ---- |
| Key | `Objectkey` (object name) is the unique identifier of an object in a bucket. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| uploadID | To copy an object part, you must first initialize a multipart upload, after which a unique `upload ID` will be returned. This ID is required in the copy request. | String | Yes |
| partNumber | Part number | Int | Yes |
| sourceURL | Source object URL: `<bucketname-appid>.cos.ap-guangzhou.myqcloud.com/<source>`. You can specify a historical version using the `?versionId=<versionId>` parameter. | String | Yes  |
| opt | Part parameter | Struct | No   |
| XCosCopySourceRange | Byte range of the source object. The range value must be in the format of `bytes=first-last`, where both `first` and `last` are offsets starting from 0. For example, `bytes=0-9` means to copy the first 10 bytes of the source object. If this parameter is not specified, the entire object will be copied. | String | No |
| XCosCopySourceIfModifiedSince | Required modification time. The object is copied only if it has been modified after the specified time. Otherwise, `412` will be returned. This parameter can be used together with `x-cos-copy-source-If-None-Match`. Using it together with other conditions may cause a conflict. | String | No |
| XCosCopySourceIfUnmodifiedSince | Required unmodified time. The object is copied only if it hasn’t been modified since the specified time. Otherwise, `412` will be returned. This parameter can be used together with `x-cos-copy-source-If-Match`. Using it together with other conditions may cause a conflict.  | String | No |
| XCosCopySourceIfMatch | `ETag` that must be matched. The part will be copied only if its `ETag` matches the specified value. Otherwise, `412` will be returned. This parameter can be used together with `x-cos-copy-source-If-Unmodified-Since`. Using it together with other conditions may cause a conflict. | String | No |
| XCosCopySourceIfNoneMatch | `ETag` that cannot be matched. The part is copied only if its `ETag` does not match the specified value. Otherwise, `412` will be returned. This parameter can be used together with `x-cos-copy-source-If-Modified-Since`. Using it together with other conditions may cause a conflict. | string | No |

#### Response description

```go
type CopyPartResult struct {
    ETag         string
    LastModified string
}
```

| Parameter | Description | Type |
| -------------- | ------------------------------------------------------------ | -------- |
| ETag | MD5 checksum of the object, such as `"22ca88419e2ed4721c23807c678adbe4c08a7880"`. **Note that double quotation marks are required at the beginning and the end.** | String |
| LastModified | Last modified time of the object, in GMT format | String |


### Completing a multipart copy

#### Feature description

This API is used to complete a multipart copy. After all parts are copied via the `Copy Parts` API, you need to call this API to complete the multipart copy. When using this API, you need to specify the `PartNumber` and `ETag` of each part in the request body for the part information to be verified.
The parts need to be reassembled after they are copied, which takes several minutes. When the assembly starts, COS will immediately return the status code `200` and will periodically return spaces during the process to keep the connection active until the assembly is completed. After that, COS will return the assembled result in the body.

- If any uploaded part is less than 1 MB in size, `400` (EntityTooSmall) will be returned when this API is called.
- If the part numbers are not continuous, "400 InvalidPart" will be returned when this API is called.
- If the part numbers in the request body are not in ascending order, "400 InvalidPartOrder" will be returned when this API is called.
- If the `uploadId` does not exist, `404` (NoSuchUpload) will be returned when this API is called.

> ! We recommend you either complete or abort a multipart copy as early as possible, as the uploaded parts of an incomplete multipart copy will take up storage capacity and incur storage fees.

#### Method prototype

```go
func (s *ObjectService) CompleteMultipartUpload(ctx context.Context, key, uploadID string, opt *CompleteMultipartUploadOptions) (*CompleteMultipartUploadResult, *Response, error)

```

#### Sample request

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
    // Initialize multipart upload
    name := "exampleobject"
    v, _, err := client.Object.InitiateMultipartUpload(context.Background(), name, nil)
    if err != nil{
        // ERROR
    }
    uploadID := v.UploadID

    // Copying an object part
    sourceUrl := "examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/sourceobject"
    res, _, err := client.Object.CopyPart(context.Background(), name, uploadID, 1, sourceUrl, nil)
    if err != nil{
        // ERROR
    }

    // Complete the multipart upload.
    completeOpt := &cos.CompleteMultipartUploadOptions{}
    completeOpt.Parts = append(completeOpt.Parts, cos.Object{
        PartNumber: 1,
        ETag:       res.ETag,
    })
    _, _, err = client.Object.CompleteMultipartUpload(context.Background(), name, uploadID, completeOpt)
    if err != nil{
        // ERROR
    }
}
```

#### Field description

```go
type CompleteMultipartUploadOptions struct {
    Parts   []Object 
}
type Object struct { 
    ETag         string 
    PartNumber   int     
}
```

| Parameter | Description | Type | Required |
| ------------------------------ | ------------------------------------------------------------ | ------ | -------- |
| key | `ObjectKey` is the unique identifier of an object in a bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the `ObjectKey` is `doc/pic.jpg` | String | Yes |
| UploadId | ID that identifies the multipart upload; generated by `InitiateMultipartUpload` | String | Yes |
| CompleteMultipartUploadOptions | Information on all parts, including `ETag` and `PartNumber` | Struct | Yes |

#### Response description

```go
type CompleteMultipartUploadResult struct {
    Location string
    Bucket   string
    Key      string
    ETag     string
}

```

| Parameter | Description | Type |
| -------- | ------------------------------------------------------------ | ------ |
| Location | URL | String |
| Bucket               | Bucket name in the format of `BucketName-APPID`, for example, `examplebucket-1250000000` | String |
| Key | Object key, the unique identifier of an object in a bucket. For example, if the object endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg` | string |
| ETag | Unique tag of a merged object. This value does not represent the MD5 checksum of the object content, but is used only to verify the uniqueness of the object as a whole. To verify the object content, you can check the `ETag` of each part during the upload process | String |
