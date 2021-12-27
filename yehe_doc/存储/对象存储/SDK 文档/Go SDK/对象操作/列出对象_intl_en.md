## Overview

This document provides an overview of APIs and SDK code samples related to listing objects.

| API                                                          | Operation                   | Description                                       |
| ------------------------------------------------------------ | ------------------------ | ---------------------------------------------- |
| [GET Bucket (List Objects)](https://intl.cloud.tencent.com/document/product/436/30614) | Querying objects | Queries some or all the objects in a bucket. |
| [GET Bucket Object Versions](https://intl.cloud.tencent.com/document/product/436/31551) | Querying objects and their version history | Queries some or all the objects in a bucket and their version history. |

## Querying an Object List

#### Description

This API is used to query some or all the objects in a bucket.

#### Method prototype

```go
func (s *BucketService) Get(ctx context.Context, opt *BucketGetOptions) (*BucketGetResult, *Response, error)
```

#### Sample 1: requesting the object list

[//]: #	".cssg-snippet-get-bucket"
```go
opt := &cos.BucketGetOptions{
    Prefix:  "test",
    MaxKeys: 100,
}
_, _, err := client.Bucket.Get(context.Background(), opt)
if err != nil {
    panic(err)
}
```

#### Sample 2: listing all objects in a directory
COS does not have the concept of folder, but you can use slashes (/) as the delimiter to stimulate folders.

[//]: # ".cssg-snippet-get-bucket2"
```go
var marker string
opt := &cos.BucketGetOptions{
    Prefix:  "folder/",  // "prefix" indicates the directory to query.
    Delimiter: "/", // Set the delimiter to "/" to list objects in the current directory. To list all objects, leave this parameter empty.
    MaxKeys: 1000,       // Set the maximum number of traversed objects (up to 1,000 per `listobject` request).
}
isTruncated := true
for isTruncated {
    opt.Marker = marker
    v, _, err := c.Bucket.Get(context.Background(), opt)
    if err != nil {
        fmt.Println(err)
        break
    }
    for _, content := range v.Contents {
        fmt.Printf("Object: %v\n", content.Key)
    }
    // A common prefix indicates paths that end with the delimiter. If the delimiter is set to "/", the common prefix indicates the paths of all subdirectories.
    for _, commonPrefix := range v.CommonPrefixes {
        fmt.Printf("CommonPrefixes: %v\n", commonPrefix)
    }
    isTruncated = v.IsTruncated    // Whether any data still exists
    marker = v.NextMarker          // Set the start key for the next request
}
```

#### Parameter description

```go
type BucketGetOptions struct {
    Prefix       string 
    Delimiter    string 
    EncodingType string 
    Marker       string 
    MaxKeys      int    
}
```

| Parameter | Description | Type | Required |
| ------------ | ------------------------------------------------------------ | ------ | ---- |
| Prefix | Filters the object keys prefixed with the value of this parameter. It is left empty by default. | String | No |
| Delimiter | A separator that is left empty by default. For example, you can specify it as `/` to indicate folders. | String | No |
| EncodingType | Specifies the encoding method of the returned value. It is left empty by default. Valid value: url. | string | No |
| Marker | Marks the starting point of the returned object list. Entries are listed in UTF-8 binary order by default. | String | No |
| MaxKeys | Maximum number of returned objects. Defaults to `1000`. | Int | No |

#### Response description

```go
type BucketGetResult struct {
    Name           string
    Prefix         string 
    Marker         string 
    NextMarker     string 
    Delimiter      string 
    MaxKeys        int
    IsTruncated    bool
    Contents       []Object 
    CommonPrefixes []string 
    EncodingType   string   
}
```

| Parameter | Description | Type |
| -------------- | ------------------------------------------------------------ | -------- |
| Name | Bucket name in the format of `BucketName-APPID`, such as `examplebucket-1250000000`. | String |
| Prefix | Filters the object keys prefixed with the value of this parameter. It is left empty by default. | String |
| Marker | Marks the starting point of the returned object list. Entries are listed in UTF-8 binary order by default. | String |
| NextMarker | Specifies the object after which the next listing should begin if `IsTruncated` is set to `true`. | String |
| Delimiter | A separator that is left empty by default. For example, you can specify it as `/` to indicate folders. | String |
| MaxKeys | Maximum number of returned objects. It defaults to 1000. | Int |
| IsTruncated | Indicates whether the returned objects are truncated | bool |
| Contents | Lists the metadata of all objects, including ETag, StorageClass, Key, Owner, LastModified, and Size. | []Object |
| CommonPrefixes | Groups all keys starting with `Prefix` and ending with `Delimiter` as a common prefix. | []string |
| EncodingType | Encoding type of the returned value. The returned value is not encoded by default. Valid value: `url` | String |

## Querying an Object Version List

#### Description

This API is used to query some or all objects in a versioning-enabled bucket.

#### Method prototype
```go
func (s *BucketService) GetObjectVersions(ctx context.Context, opt *BucketGetObjectVersionsOptions) (*BucketGetObjectVersionsResult, *Response, error)
```

#### Sample: querying an object version list

[//]: #".cssg-snippet-list-objects-versioning"

```
keyMarker := ""
versionIdMarker := ""
isTruncated := true
opt := &cos.BucketGetObjectVersionsOptions{}
for isTruncated {
    opt.KeyMarker = keyMarker
    opt.VersionIdMarker = versionIdMarker
    v, _, err := c.Bucket.GetObjectVersions(context.Background(), opt)
    if err != nil {
        // ERROR
        break
    }
    for _, vc := range v.Version {
        fmt.Printf("Version: %v, %v, %v, %v\n", vc.Key, vc.Size, vc.VersionId, vc.IsLatest)
    }
    for _, dc := range v.DeleteMarker {
        fmt.Printf("DeleteMarker: %v, %v, %v\n", dc.Key, dc.VersionId, dc.IsLatest)
    }
    keyMarker = v.NextKeyMarker
    versionIdMarker = v.NextVersionIdMarker
    isTruncated = v.IsTruncated
}
```

#### Parameter description
```go
type BucketGetObjectVersionsOptions struct {
    Prefix          string
    Delimiter       string
    EncodingType    string
    KeyMarker       string
    VersionIdMarker string
    MaxKeys         int
}
```

| Field |  Description | Type | Required |
| :---------------- | :----------------------------------------------------------- | :----- | :------- |
| prefix | Key prefix to query objects by | string | No   |
| delimiter | Character delimiter used to group object keys. Keys that contain identical paths between the prefix (or, if no prefix is specified, the beginning of the string) and the first delimiter are grouped and defined as a `Prefix` node under `CommonPrefixes`. The grouped object keys will no longer appear in the subsequent object list. For specific scenarios and usage, see the samples below. | string | No |
| encoding-type | Encoding type of the returned value. Valid value: `url`, meaning that the returned object keys are URL-encoded (percent-encoded) values. For example, "Tencent Cloud" will be encoded to `%E8%85%BE%E8%AE%AF%E4%BA%91`. | string | No |
| key-marker | Marker for the starting object key. Object version entries after this marker will be returned in UTF-8 lexicographical order. | string | No |
| version-id-marker | Marker for the starting version ID. Object version entries after this marker will be returned. If `NextVersionIdMarker` is empty in the last `ListVersionsResult` response, leave this parameter empty. | string | No |
| max-keys | Maximum number (up to 1,000) of keys returned in a response. Defaults to `1000`. **Note**: This parameter limits the maximum number of keys (the sum of `CommonPrefixes`, `Version`, and `DeleteMarker’) COS can return in each `ListVersionsResult` response. If not all objects are listed in a single response, COS will return the `NextKeyMarker` and `NextVersionIdMarker` nodes, the values of which can be used to specify `key-marker` and `version-id-marker`, respectively, so that the remaining versions can be listed in your next request. | int | No |

#### Response description

```go
type BucketGetObjectVersionsResult struct {
    Name                string
    EncodingType        string
    Prefix              string
    KeyMarker           string
    VersionIdMarker     string
    MaxKeys             int
    Delimiter           string
    IsTruncated         bool
    NextKeyMarker       string
    NextVersionIdMarker string
    CommonPrefixes      []string
    Version             []ListVersionsResultVersion
    DeleteMarker        []ListVersionsResultDeleteMarker
}
type ListVersionsResultVersion struct {
    Key          string
    VersionId    string
    IsLatest     bool
    LastModified string
    ETag         string
    Size         int
    StorageClass string
    Owner        *Owner
}
type ListVersionsResultDeleteMarker struct {
    Key          string
    VersionId    string
    IsLatest     bool
    LastModified string
    Owner        *Owner
}
```

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----- | :--------------------------------------------- | :-------- |
| ListVersionsResult | None | Stores the result of `GET Bucket Object versions`. | Container |

**Content of `ListVersionsResult`**:

| Node Name (Keyword) | Parent Node | Description | Type |
| :------------------ | :----------------- | :----------------------------------------------------------- | :-------- |
| EncodingType | ListVersionsResult | Encoding type, which corresponds to the `encoding-type` parameter in the request. This node will be returned only when the `encoding-type` parameter is specified in the request. | string |
| Name | ListVersionsResult | Bucket name, formatted as `<BucketName-APPID>`, such as `examplebucket-1250000000` | string |
| Prefix              | ListVersionsResult | Filters the object keys prefixed with the value of this parameter.                     | string    |
| KeyMarker | ListVersionsResult | Marks the object key to start with. Object version entries after the marker will be returned in UTF-8 lexicographical order. This node corresponds to the `key-marker` parameter in the request. | string |
| VersionIdMarker | ListVersionsResult | Marks the version ID to start with. Object version entries after the marker will be returned. This node corresponds to the `version-id-marker` parameter in the request. | string |
| MaxKeys | ListVersionsResult | Maximum number of keys returned in a single response. This node corresponds to the `max-keys` parameter in the request. | integer |
| IsTruncated | ListVersionsResult | Indicates whether the returned list is truncated. Valid values: `true`, `false` | boolean |
| NextKeyMarker | ListVersionsResult | This node will be returned only if the returned list is truncated (i.e., the value of `IsTruncated` is `true`). The value of this node is the last object key in the current response. If you need to request subsequent entries, the value can be passed in as the value of the `key-marker` parameter in the next request. | string |
| NextVersionIdMarker | ListVersionsResult | This node will be returned only if the returned list is truncated (i.e., the value of  `IsTruncated` is `true`). The value of this node is the last version ID in the current response. If you need to request subsequent entries, the value can be passed in as the value of the `version-id-marker` parameter in the next request. If this node is left empty, `version-id-marker` in the next request should also be left empty. | string |
| Delimiter | ListVersionsResult | Delimiter, which corresponds to the `delimiter` parameter in the request and will be returned only if the `delimiter` parameter is specified in the request. | string |
| CommonPrefixes | ListVersionsResult | The identical paths between the prefix (or, if no prefix is specified, the beginning of the string) and the first delimiter are grouped and defined as a common prefix. This node will be returned only if the `delimiter` parameter is specified in the request. | Container |
| Version             | ListVersionsResult | Object version entry.                                                 | Container |
| DeleteMarker        | ListVersionsResult | Object delete marker entry.                                             | Container |

**Content of `CommonPrefixes`:**

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :-------------------------------- | :------------------------ | :----- |
| Prefix | ListVersionsResult.CommonPrefixes | A single common prefix | string |

**Content of `Version`**:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------------------------- | :----------------------------------------------------------- | :-------- |
| Key                | ListVersionsResult.Version | Object key.                                                       | string    |
| VersionId | ListVersionsResult.Version | Version ID of the object. If versioning is disabled, the value of this node is an empty string. If versioning is enabled, the value of this node is `null` for an object uploaded before you enable versioning. If versioning is suspended, the value of this node is `null` for an object uploaded after you suspend versioning. Note that each object can have only one object version whose ID is `null`. | string |
| IsLatest           | ListVersionsResult.Version | Whether the current version is the latest one of the object.                               | boolean   |
| LastModified | ListVersionsResult.Version | Last modified time of the current version, in ISO 8601 format (for example, 2019-05-24T10:56:40Z) | date |
| ETag | ListBucketResult.Contents | Entity tag of the object. It indicates the content of the object when it is created and can be used to verify whether the object content is changed. Example: "8e0b617ca298a564c3331da28dcb50df". The value of `ETag` is not necessarily the MD5 checksum of the object. The value will be different if the uploaded object is encrypted. | string |
| Size               | ListVersionsResult.Version | Object size, in bytes.                                        | integer   |
| StorageClass | ListVersionsResult.Version | Object storage class, such as `STANDARD_IA` or `ARCHIVE`. For enumerated values, please see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/436/30925). | Enum |
| StorageTier | ListVersionsResult.Version | Access tier (for INTELLIGENT TIERING) the object is currently stored in. Enumerated values: `FREQUENT`, `INFREQUENT`. This node is returned only when `StorageClass` is set to `INTELLIGENT_TIERING`. | Enum |
| Owner              | ListVersionsResult.Version | Information of the object owner.                                               | Container |

**Content of `Version.Owner`**:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------------------------------- | :----------------- | :----- |
| ID | ListVersionsResult.Version.Owner | `APPID` of the object owner | string |
| DisplayName | ListVersionsResult.Version.Owner | Name of the object owner | string |

**Content of `DeleteMarker`**:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------------------------------ | :----------------------------------------------------------- | :-------- |
| Key                | ListVersionsResult.DeleteMarker | Object key.                                                       | string    |
| VersionId          | ListVersionsResult.DeleteMarker | Version ID of the object delete marker.                                      | string    |
| IsLatest           | ListVersionsResult.DeleteMarker | Whether the current delete marker is the latest one of the object.                           | boolean   |
| LastModified | ListVersionsResult.DeleteMarker | Last modified time of the current delete marker, in ISO 8601 format (for example, 2019-05-24T10:56:40Z) | date |
| Owner              | ListVersionsResult.DeleteMarker | Information of the object owner.                                               | Container |

**Content of `DeleteMarker.Owner`**:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------------------------------------ | :----------------- | :----- |
| ID | ListVersionsResult.DeleteMarker.Owner | `APPID` of the object owner | string |
| DisplayName | ListVersionsResult.DeleteMarker.Owner | Name of the object owner | string |
