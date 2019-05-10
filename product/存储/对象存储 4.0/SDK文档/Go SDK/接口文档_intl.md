The COS Go SDK (XML API) operation returns the Result structure of the corresponding API and the [Response](https://golang.org/pkg/net/http/#Response) structure of the Golang standard HTTP library.

> ?For more information on the definitions of SecretId, SecretKey, Bucket and other terms and how to obtain them, see [COS Glossary](https://cloud.tencent.com/document/product/436/7751).

## Service API

### Get the bucket list

#### Feature

This API is used to obtain all bucket lists of the requester.

#### Method prototype

```go
func (s *ServiceService) Get(ctx context.Context) (*ServiceGetResult, *Response, error)
```

#### Request example

```go
s, resp, err := c.Service.Get(context.Background()) 
```

#### Returned result

```go
type ServiceGetResult struct {
    Owner   *Owner  
    Buckets []Bucket 
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

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| ID | ID of the bucket owner | string |
| DisplayName | Name of the bucket owner | string |
| Name | Bucket name | string |
| Region | The region of the bucket | string |
| CreationDate | Time when the bucket was created, in ISO8601 format, such as 2016-11-09T08:46:32.000Z | string |

## Bucket APIs

### Create a bucket

#### Feature

This API is used to create a bucket under the specified account. An error is returned if a bucket exists.

#### Method prototype

```go
func (s *BucketService) Put(ctx context.Context, opt *BucketPutOptions) (*Response, error)
```

#### Request example

```go
opt := &cos.BucketPutOptions{
	XCosACL: "public-read",
}
resp, err := client.Bucket.Put(context.Background(), opt)
```

#### Parameters

```go
type BucketPutOptions struct {
	XCosACL              string 
	XCosGrantRead        string  
	XCosGrantWrite       string  
	XCosGrantFullControl string 
}
```

| Parameter Name | Description | Type | Required |
| -------------------- | ------------------------------------------------------------ | ------ | ---- |
| XCosACL | Sets the bucket ACL, such as private, public-read, and public-read-write. | string | No |
| XCosGrantFullControl | Grants the specified account the permission to read and write buckets. Format: `id=" ",id=" "`. For authorization to a sub-account, `id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`; for authorization to a root account, `id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`. For example: `id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"` | string | No |
| XCosGrantRead | Grants the specified account the permission to read buckets. Format: `id=" ",id=" "`. For authorization to a sub-account, `id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`; for authorization to a root account, `id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`. For example: `id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"` | string | No |
| XCosGrantWrite | Grants the specified account the permission to write buckets. Format: `id=" ",id=" "`. For authorization to a sub-account, `id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`; for authorization to a root account, `id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`. For example: `id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"` | string | No |

### Delete a bucket

#### Feature

This API is used to delete an existing bucket under the specified account. The bucket must be empty before it can be deleted.

#### Method prototype

```go
func (s *BucketService) Delete(ctx context.Context) (*Response, error)
```

#### Request example

```go
resp, err := client.Bucket.Delete(context.Background())
```

### Search for a bucket and the access to it

#### Feature

This API is used to query whether a bucket exists or whether you have the access to it.

#### Method prototype

```go
func (s *BucketService) Head(ctx context.Context) (*Response, error)
```

#### Request example

```go
resp, err := client.Bucket.Head(context.Background())
```

### Obtain the region information

#### Feature

This API is used to query the information on the region in which a bucket resides.

#### Method prototype

```go
func (s *BucketService) GetLocation(ctx context.Context) (*BucketGetLocationResult, *Response, error)
```

#### Request example

```go
v, resp, err := client.Bucket.GetLocation(context.Background())
```

#### Returned result

```go
type BucketGetLocationResult struct {
	Location string                                      
}
```

```go
{
    'Location': 'ap-beijing-1'|'ap-beijing'|'ap-shanghai'|'ap-guangzhou'|'ap-chengdu'|'ap-chongqing'|'ap-singapore'|'ap-hongkong'|'na-toronto'|'eu-frankfurt'|'ap-mumbai'|'ap-seoul'|'na-siliconvalley'|'na-ashburn'
}
```

| Parameter Name | Description | Type |
| -------- | --------------------- | ------ |
| Location | The location of the bucket | string |

### Get the object list

#### Feature

This API is used to get all objects under the specified bucket.

#### Method prototype

```go
func (s *BucketService) Get(ctx context.Context, opt *BucketGetOptions) (*BucketGetResult, *Response, error)
```

#### Request example

```go
opt := &cos.BucketGetOptions{
	Prefix:  "test",
	MaxKeys: 100,                                
}
v, resp, err := client.Bucket.Get(context.Background(), opt)
```

#### Parameters

```go
type BucketGetOptions struct {
	Prefix       string 
	Delimiter    string 
	EncodingType string 
	Marker       string 
	MaxKeys      int    
}
```

| Parameter Name | Description | Type | Required |
| ------------ | ------------------------------------------------------------ | ------ | ---- |
| Prefix | Filters the keys of objects by matching the objects prefixed with this parameter. It is left empty by default. | string | No |
| Delimiter | Sets a delimiter ("/") to simulate a folder. It is left empty by default. | string | No |
| EncodingType | Indicates the encoding method of the returned value. The value is not encoded by default. Available value: url | string | No |
| Marker | Marks the starting point of the list of returned objects. Entries are listed using UTF-8 binary order by default. | string | No |
| MaxKeys | The maximum number of returned objects. It defaults to 1000. | int | No |

#### Returned result

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

| Parameter Name | Description | Type |
| -------------- | ------------------------------------------------------------ | -------- |
| Name | Bucket name, which is in a format of bucketname-appid. | string |
| Prefix | Filters the keys of objects by matching the objects prefixed with this parameter. It is left empty by default. | string |
| Marker | Marks the starting point of the list of returned objects. Entries are listed using UTF-8 binary order by default. | string |
| NextMarker | Marks the starting point of the next list of returned objects if IsTruncated is true. | string |
| Delimiter | Sets a delimiter ("/") to simulate a folder. It is left empty by default. | string |
| MaxKeys | The maximum number of returned objects. It defaults to 1000. | int |
| IsTruncated | Indicates whether the returned objects are truncated | bool |
| Contents | The list containing the meta information of all objects, including ETag, StorageClass, Key, Owner, LastModified, and Size. | []Object |
| CommonPrefixes | All keys starting with Prefix and ending with Delimiter are grouped into the same type | []string |
| EncodingType | Indicates the encoding method of the returned value. The value is not encoded by default. Available value: url | string |

### Query multipart upload

#### Feature

This API is used to query all multipart uploads in progress under the specified bucket.

#### Method prototype

```go
func (s *BucketService) ListMultipartUploads(ctx context.Context, opt *ListMultipartUploadsOptions) (*ListMultipartUploadsResult, *Response, error)
```

#### Request example

```go
opt := &cos.ListMultipartUploadsOptions{
	Prefix: "test",
}
v, resp, err := client.Bucket.ListMultipartUploads(context.Background(), opt)
```

#### Parameters

```go
type ListMultipartUploadsOptions struct {
	Delimiter      string 
	EncodingType   string 
	Prefix         string 
	MaxUploads     int    
	KeyMarker      string 
	UploadIDMarker string 
}
```

| Parameter Name | Description | Type | Required |
| -------------- | ------------------------------------------------------------ | ------ | ---- |
| Delimiter | Sets a delimiter. It is left empty by default. | string | No |
| EncodingType | Indicates the encoding method of the returned value. The value is not encoded by default. Available value: url | string | No |
| Prefix | Filters the keys of multipart uploads by matching the multipart uploads prefixed with this parameter. It is left empty by default. | string | No |
| MaxUploads | The maximum number of returned multipart uploads. It defaults to 1000. | int | No |
| KeyMarker | Marks the starting point of a multipart upload task. It is used with UploadIdMarker. | string | No |
| UploadIdMarker | Marks the starting point of a multipart upload task. It is used with KeyMarker. If KeyMarker is not specified, UploadIdMarker will be ignored. | string | No |

#### Returned result

```go
type ListMultipartUploadsResult struct {
	Bucket             string   
	EncodingType       string   
	KeyMarker          string
	UploadIDMarker     string 
	NextKeyMarker      string
	NextUploadIDMarker string 
	MaxUploads         int
	IsTruncated        bool
	Uploads            []struct {
        Key          string
        UploadID     string 
        StorageClass string
        Initiator    *Initiator
        Owner        *Owner
        Initiated    string
	} 
	Prefix         string
	Delimiter      string   
	CommonPrefixes []string 
}
```

| Parameter Name | Description | Type |
| ------------------ | ------------------------------------------------------------ | -------- |
| Bucket | Bucket name, which is in a format of bucketname-appid. | string |
| EncodingType | Indicates the encoding method of the returned value. The value is not encoded by default. Available value: url | string |
| KeyMarker | Marks the starting point of the list of keys for multipart uploads. It is used with UploadIdMarker. | string |
| UploadIdMarker | Marks the starting point of the list of uploadids for multipart uploads. It is used with KeyMarker. If KeyMarker is not specified, UploadIdMarker will be ignored. | string |
| NextKeyMarker | Marks the starting point of the next list of keys for multipart uploads if IsTruncated is true. | string |
| NextUploadIDMarker | Marks the starting point of the next list of uploadids for multipart uploads if IsTruncated is true. | string |
| MaxUploads | The maximum number of returned multipart uploads. It defaults to 1000. | int |
| IsTruncated | Indicates whether the returned multipart uploads are truncated | bool |
| Upload | The list containing information of all multipart uploads, including UploadId, StorageClass, Key, Owner, Initiator, and Initiated. | []struct |
| Prefix | Filters the keys of multipart uploads by matching the multipart uploads prefixed with this parameter. It is left empty by default. | string |
| Delimiter | Sets a delimiter. It is left empty by default. | string |
| CommonPrefixes | All keys starting with Prefix and ending with Delimiter are grouped into the same type | []string |

### Set a bucket ACL

#### Feature

This API is used to set the bucket ACL information by passing header through XCosACL, XCosGrantFullControl, XCosGrantRead and XCosGrantWrite or by passing body thruogh ACLXML. You can only use one of these two methods, otherwise a conflict is returned.

#### Method prototype

```go
func (s *BucketService) PutACL(ctx context.Context, opt *BucketPutACLOptions) (*Response, error)
```

#### Request example

Set a bucket ACL through header.

```go
opt := &cos.BucketPutACLOptions{
	Header: &cos.ACLHeaderOptions{
		//private，public-read，public-read-write
		XCosACL: "private",
	},
}
resp, err := client.Bucket.PutACL(context.Background(), opt)
```

Set a bucket ACL through body.

```go
opt = &cos.BucketPutACLOptions{
    Body: &cos.ACLXml{
        Owner: &cos.Owner{
            ID: "qcs::cam::uin/100000760461:uin/100000760461",
        },
        AccessControlList: []cos.ACLGrant{
            {
                Grantee: &cos.ACLGrantee{
                    Type: "RootAccount",
                    ID:"qcs::cam::uin/100000760461:uin/100000760461",
                },
                Permission: "FULL_CONTROL",
            },
        },
    },
}
resp, err := client.Bucket.PutACL(context.Background(), opt)
```

#### Parameters

```go
type ACLHeaderOptions struct {
	XCosACL              string 
	XCosGrantRead        string 
	XCosGrantWrite       string 
	XCosGrantFullControl string 
}
```

| Parameter Name | Description | Type | Required |
| -------------------- | ------------------------------------------------------------ | ------ | ---- |
| XCosACL | Sets the bucket ACL, such as private, public-read, and public-read-write. | string | No |
| XCosGrantFullControl | Grants the specified account the permission to read and write buckets. Format: `id=" ",id=" "`. For authorization to a sub-account, `id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`; for authorization to a root account, `id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`. For example: `id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"` | string | No |
| XCosGrantRead | Grants the specified account the permission to read buckets. Format: `id=" ",id=" "`. For authorization to a sub-account, `id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`; for authorization to a root account, `id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`. For example: `id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"` | string | No |
| XCosGrantWrite | Grants the specified account the permission to write buckets. Format: `id=" ",id=" "`. For authorization to a sub-account, `id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`; for authorization to a root account, `id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`. For example: `id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"` | string | No |
| ACLXML | Grants the specified account the access to buckets. For more information on the format, see the response for "get bucket acl". | struct | No |



### Get the bucket ACL

#### Feature

This API is used to get the ACL information of the specified bucket.

#### Method prototype

```go
func (s *BucketService) GetACL(ctx context.Context) (*BucketGetACLResult, *Response, error)
```

#### Request example

```go
v, resp, err := client.Bucket.GetACL(context.Background())
```

#### Returned result

```go
type ACLXml struct {
	Owner             *Owner
	AccessControlList []ACLGrant 
}
type Owner struct { 
	ID          string 
	DisplayName string
}
type ACLGrant struct {
	Grantee    *ACLGrantee
	Permission string
}
type ACLGrantee struct {
	Type        string 
	ID          string 
	DisplayName string
    UIN         string 
}
```

| Parameter Name | Description | Type |
| ----------------- | ------------------------------------------------------------ | ------ |
| Owner | Information of the bucket owner, including DisplayName and ID | struct |
| AccessControlList | Information of the user granted the bucket permissions, including Grantee and Permission | struct |
| Grantee | Information of grantee, including DisplayName, Type, ID and UIN | struct |
| Type | Type of grantee: CanonicalUser or Group | string |
| ID | ID of grantee when Type is CanonicalUser | string |
| DisplayName | Name of grantee | string |
| UIN | UIN of grantee when Type is Group | string |
| Permission | Bucket permissions of grantee. Available values: FULL_CONTROL (read and write permissions), WRITE (write permission), and READ (read permission) | string |

### Set cross-origin configuration

#### Feature

This API is used to set the cross-origin resource configuration for the specified bucket.

#### Method prototype

```go
func (s *BucketService) PutCORS(ctx context.Context, opt *BucketPutCORSOptions) (*Response, error)
```

#### Request example

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
resp, err := client.Bucket.PutCORS(context.Background(), opt)
```

#### Parameters

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

| Parameter Name | Description | Type | Required |
| -------------- | ------------------------------------------------------------ | -------- | ---- |
| BucketCORSRule | Sets the appropriate cross-origin rules, including ID, MaxAgeSeconds, AllowedOrigin, AllowedMethod, AllowedHeader, and ExposeHeader | struct | Yes |
| ID | Sets rule ID. | string | No |
| AllowedMethods | Sets allowed methods, including GET, PUT, HEAD, POST and DELETE | []string | Yes |
| AllowedOrigins | Sets allowed access sources, such as `"http://cloud.tencent.com"`. The wildcard "*" is supported. | []string | Yes |
| AllowedHeaders | Sets the custom HTTP request headers that can be used by requests. The wildcard "*" is supported. | []string | No |
| MaxAgeSeconds | Sets the validity period of the results obtained by OPTIONS | int | No |
| ExposeHeaders | Sets the custom header information that can be received by the browser from the server end | []string | No |

### Get cross-origin configuration

#### Feature

This API is used to get the cross-origin configuration of the specified bucket.

#### Method prototype

```go
func (s *BucketService) GetCORS(ctx context.Context) (*BucketGetCORSResult, *Response, error)
```

#### Request example

```go
v, resp, err := client.Bucket.GetCORS(context.Background())
```

#### Returned result

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

| Parameter Name | Description | Type | Required |
| -------------- | ------------------------------------------------------------ | -------- | ---- |
| BucketCORSRule | Sets the appropriate cross-origin rules, including ID, MaxAgeSeconds, AllowedOrigin, AllowedMethod, AllowedHeader, and ExposeHeader | struct | Yes |
| ID | Sets rule ID. | string | No |
| AllowedMethods | Sets allowed methods, including GET, PUT, HEAD, POST and DELETE | []string | Yes |
| AllowedOrigins | Sets allowed access sources, such as `"http://cloud.tencent.com"`. The wildcard "*" is supported. | []string | Yes |
| AllowedHeaders | Sets the custom HTTP request headers that can be used by requests. The wildcard "*" is supported. | []string | No |
| MaxAgeSeconds | Sets the validity period of the results obtained by OPTIONS | int | No |
| ExposeHeaders | Sets the custom header information that can be received by the browser from the server end | []string | No |

### Delete cross-origin configuration

#### Feature

This API is used to delete the cross-origin configuration of the specified bucket.

#### Method prototype

```go
func (s *BucketService) DeleteCORS(ctx context.Context) (*Response, error)
```

#### Request example

```go
resp, err := client.Bucket.DeleteCORS(context.Background())
```

### Set the lifecycle

#### Feature

This API is used to set the lifecycle configuration of the specified bucket.

#### Method prototype

```go
func (s *BucketService) PutLifecycle(ctx context.Context, opt *BucketPutLifecycleOptions) (*Response, error)
```

#### Request example

```go
lc := &cos.BucketPutLifecycleOptions{
    Rules: []cos.BucketLifecycleRule{
        {
            ID:     "1234",
            Filter: &cos.BucketLifecycleFilter{Prefix: "test"},
            Status: "Enabled",
            Transition: &cos.BucketLifecycleTransition{
                Days:         10,
                StorageClass: "Standard",
            },
        },
        {
            ID:     "123422",
            Filter: &cos.BucketLifecycleFilter{Prefix: "gg"},
            Status: "Disabled",
            Expiration: &cos.BucketLifecycleExpiration{
                Days: 10,
            },
        },
    },
}
resp, err := client.Bucket.PutLifecycle(context.Background(), lc)
```

#### Parameters

```go
type BucketLifecycleRule struct {
	ID                             string
	Status                         string
	Filter                         *BucketLifecycleFilter
	Transition                     *BucketLifecycleTransition
	Expiration                     *BucketLifecycleExpiration
	AbortIncompleteMultipartUpload  *BucketLifecycleAbortIncompleteMultipartUpload 
}
type BucketLifecycleFilter struct {
	Prefix       string 
}
type BucketLifecycleTransition struct {
	Date         string 
	Days         int    
	StorageClass string
}
type BucketLifecycleExpiration struct {
	Date string 
	Days int    
}
type BucketLifecycleAbortIncompleteMultipartUpload struct {
	DaysAfterInitiation string 
}
```

| Parameter Name | Description | Type | Required |
| ------------------------------ | ------------------------------------------------------------ | ------ | ---- |
| Rule | Sets the appropriate rules, including ID, Filter, Status, Expiration, Transition, and AbortIncompleteMultipartUpload | List | Yes |
| ID | Sets rule ID. | string | No |
| Status | Sets whether Rule is enabled. Available values: Enabled or Disabled | string | Yes |
| Filter | Describes a collection of objects that are subject to the rules. To set rules for all objects in the bucket, leave Prefix empty. | struct | Yes |
| Transition | Sets the rule for changing the storage type of the object. You can specify the number of days (Days) or a specified date (Date). The format of Date must be GMT ISO 8601. Available values for StorageClass: Standard_IA and Archive. Multiple rules can be set at a time. | struct | No |
| Expiration | Sets the expiration rule for the object. You can specify the number of days (Days) or a specified date (Date). The format of Date must be GMT ISO 8601. | struct | No |
| AbortIncompleteMultipartUpload | Indicates the number of days within which the multipart upload must be completed after the upload starts | struct | No |

### Query the lifecycle

#### Feature

This API is used to query the lifecycle configuration of the specified bucket.

#### Method prototype

```go
func (s *BucketService) GetLifecycle(ctx context.Context) (*BucketGetLifecycleResult, *Response, error)
```

#### Request example

```go
v, resp, err := client.Bucket.GetLifecycle(context.Background()) 
```

#### Returned result

```go
type BucketLifecycleRule struct {
	ID                             string
	Status                         string
	Filter                         *BucketLifecycleFilter
	Transition                     *BucketLifecycleTransition
	Expiration                     *BucketLifecycleExpiration
	AbortIncompleteMultipartUpload  *BucketLifecycleAbortIncompleteMultipartUpload 
}
type BucketLifecycleFilter struct {
	Prefix       string 
}
type BucketLifecycleTransition struct {
	Date         string 
	Days         int    
	StorageClass string
}
type BucketLifecycleExpiration struct {
	Date string 
	Days int    
}
type BucketLifecycleAbortIncompleteMultipartUpload struct {
	DaysAfterInitiation string 
}
```

| Parameter Name | Description | Type | Required |
| ------------------------------ | ------------------------------------------------------------ | ------ | ---- |
| Rule | Sets the appropriate rules, including ID, Filter, Status, Expiration, Transition, and AbortIncompleteMultipartUpload | List | Yes |
| ID | Sets rule ID. | string | No |
| Status | Sets whether Rule is enabled. Available values: Enabled or Disabled | string | Yes |
| Filter | Describes a collection of objects that are subject to the rules. To set rules for all objects in the bucket, leave Prefix empty. | struct | Yes |
| Transition | Sets the rule for changing the storage type of the object. You can specify the number of days (Days) or a specified date (Date). The format of Date must be GMT ISO 8601. Available values for StorageClass: Standard_IA and Archive. Multiple rules can be set at a time. | struct | No |
| Expiration | Sets the expiration rule for the object. You can specify the number of days (Days) or a specified date (Date). The format of Date must be GMT ISO 8601. | struct | No |
| AbortIncompleteMultipartUpload | Indicates the number of days within which the multipart upload must be completed after the upload starts | struct | No |

### Delete the lifecycle

#### Feature

This API is used to delete the lifecycle configuration of the specified bucket.

#### Method prototype

```go
func (s *BucketService) DeleteLifecycle(ctx context.Context) (*Response, error)
```

#### Request example

```go
resp, err := client.Bucket.DeleteLifecycle(context.Background())
```

## Object APIs

### Upload an object

#### Feature

This API is used to upload a local file or an input stream to the specified bucket. It is recommended to upload small files not larger than 20 MB. The file size for a single upload is limited to 5 GB. Use multipart upload to upload large files.

> !The number of access policies is up to 1000. Do not set object ACL control when you upload an object if it is not required. The object inherits the bucket permissions by default.

#### Method prototype

```go
func (s *ObjectService) Put(ctx context.Context, key string, r io.Reader, opt *ObjectPutOptions) (*Response, error)
```

#### Request example

```go	
    key := "put_option.go"
	f := strings.NewReader("test xxx")
	opt := &cos.ObjectPutOptions{
		ObjectPutHeaderOptions: &cos.ObjectPutHeaderOptions{
			ContentType: "text/html",
		},
		ACLHeaderOptions: &cos.ACLHeaderOptions{
			XCosACL: "private",
		},
	}
resp, err = client.Object.Put(context.Background(), key, f, opt)
```

#### Parameters

```go
type ObjectPutOptions struct {
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
	ContentLength      int   
	Expires            string 
	// Custom x-cos-meta-* header
	XCosMetaXXX        *http.Header 
	XCosStorageClass   string      
}
```

| Parameter Name | Description | Type | Required |
| -------------------- | ------------------------------------------------------------ | ----------- | ---- |
| r | The content of the uploaded file, which can be a file stream or a byte stream. When r is not bytes.Buffer/bytes.Reader/strings.Reader, opt.ObjectPutHeaderOptions.ContentLength must be specified. | io.Reader | Yes |
| key | ObjectKey is the unique identifier of the object in the bucket. For example, in the object's access domain name `bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg`, the ObjectKey is doc1/pic1.jpg. | string | Yes |
| XCosACL | Sets the file ACL, such as private, public-read, and public-read-write | string | No |
| XCosGrantFullControl | Grants the specified account the permission to read and write files. Format: `id=" ",id=" "`. For authorization to a sub-account, `id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`; for authorization to a root account, `id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`. For example: `id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"` | string | No |
| XCosGrantRead | Grants the specified account the permission to read files. Format: `id=" ",id=" "`. For authorization to a sub-account, `id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`; for authorization to a root account, `id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`. For example: `id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"` | string | No |
| XCosGrantWrite | Grants the specified account the permission to write files. Format: `id=" ",id=" "`. For authorization to a sub-account, `id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`; for authorization to a root account, `id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`. For example: `id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"` | string | No |
| XCosStorageClass | Sets file storage type: STANDARD and STANDARD_IA. Default: STANDARD | string | No |
| Expires | Sets Content-Expires. | string | No |
| CacheControl | Cache policy. Sets Cache-Control. | string | No |
| ContentType | Content Type. Sets Content-Type. | string | No |
| ContentDisposition | File name. Sets Content-Disposition. | string | No |
| ContentEncoding | Encoding format. Sets Content-Encoding. | string | No |
| ContentLength | Sets transmission length | string | No |
| XCosMetaXXX | User-defined file meta information. It must start with x-cos-meta. Otherwise, it will be ignored. | http.Header | No |

#### Returned result

```go
{
    'ETag': 'string',
    'x-cos-expiration': 'string'
}
```

| Parameter Name | Description | Type |
| ---------------- | -------------------------------- | ------ |
| ETag | MD5 of the upload File | string |
| x-cos-expiration | After the lifecycle is set, the file expiration rule is returned. | string |

### Get objects

#### Feature

This API is used to download the files of the specified bucket locally.

#### Method prototype

```go
func (s *ObjectService) Get(ctx context.Context, key string, opt *ObjectGetOptions) (*Response, error)
```

#### Request example

```go
	key := "test/hello.txt"
	opt := &cos.ObjectGetOptions{
		ResponseContentType: "text/html",
		Range:               "bytes=0-3",
	}
	//"opt" is optional. It can be set to nil unless otherwise specified.
	resp, err = client.Object.Get(context.Background(), key, opt)
	bs, _ = ioutil.ReadAll(resp.Body)
	resp.Body.Close()
	fmt.Printf("%s\n", string(bs))
```

#### Parameters

```go
type ObjectGetOptions struct {
	ResponseContentType        string 
	ResponseContentLanguage    string 
	ResponseExpires            string 
	ResponseCacheControl       string 
	ResponseContentDisposition string 
	ResponseContentEncoding    string 
	Range                      string 
	IfModifiedSince            string 
}
```

| Parameter Name | Description | Type | Required |
| -------------------------- | ------------------------------------------------------------ | ------ | ---- |
| key | ObjectKey is the unique identifier of the object in the bucket. For example, in the object's access domain name `bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg`, the ObjectKey is doc1/pic1.jpg. | string | Yes |
| ResponseContentType | Sets the Content-Type in the response header | string | No |
| ResponseContentLanguage | Sets the Content-Language in the response header | string | No |
| ResponseExpires | Sets the Content-Expires in the response header | string | No |
| ResponseCacheControl | Sets the Cache-Control in the response header | string | No |
| ResponseContentDisposition | Sets the Content-Disposition in the response header | string | No |
| ResponseContentEncoding | Sets the Content-Encoding in the response header | string | No |
| Range | Sets the range of bytes of the file to be downloaded in the format of bytes=first-last | string | No |
| IfModifiedSince | The file is returned after it has been modified since the specified time | string | No |

#### Returned result

```go
{
    'Body': '',
    'Accept-Ranges': 'bytes',
    'Content-Type': 'application/octet-stream',
    'Content-Length': '16807',
    'Content-Disposition': 'attachment; filename="filename.jpg"',
    'Content-Range': 'bytes 0-16086/16087',
    'ETag': '"9a4802d5c99dafe1c04da0a8e7e166bf"',
    'Last-Modified': 'Wed, 28 Oct 2014 20:30:00 GMT',
    'X-Cos-Request-Id': 'NTg3NzQ3ZmVfYmRjMzVfMzE5N182NzczMQ=='
}
```

| Parameter Name | Description | Type |
| ---------- | ------------------------------------------------------------ | ---------- |
| Body | The content of the downloaded file | StreamBody |
| File meta information | The meta information of the downloaded file, including Etag and X-Cos-Request-Id. The meta information of the configured file is also returned. | string |

### Delete a single object

#### Feature

This API is used to delete a file in a bucket.

#### Method prototype

```go
func (s *ObjectService) Delete(ctx context.Context, key string) (*Response, error)
```

#### Request example

```go
key := "test/objectPut.go"
resp, err := client.Object.Delete(context.Background(), name)
```

#### Parameters

| Parameter Name | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ------ | ---- |
| key | ObjectKey is the unique identifier of the object in the bucket. For example, in the object's access domain name `bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg`, the ObjectKey is doc1/pic1.jpg. | string | Yes |

### Delete multiple objects

#### Feature

This API is used to delete the files in the specified bucket in batch.

#### Method prototype

```go
func (s *ObjectService) DeleteMulti(ctx context.Context, opt *ObjectDeleteMultiOptions) (*ObjectDeleteMultiResult, *Response, error)
```

#### Request example

```go
var keys = []string{"a","b","c"}
obs := []cos.Object{}
for _, v := range keys {
    obs = append(obs, cos.Object{Key: v})
}
opt := &cos.ObjectDeleteMultiOptions{
    Objects: obs,
    Quiet: true,
}
v, resp, err := client.Object.DeleteMulti(ctx, opt)
```

#### Parameters

```go
type ObjectDeleteMultiOptions struct {
	Quiet   bool     
	Objects []Object 
}
type Object struct {
	Key		string 
}
```

| Parameter Name | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ------ | ---- |
| Objects | Provides the information of each target object to be deleted | List | Yes |
| Key | ObjectKey is the unique identifier of the object in the bucket. For example, in the object's access domain name `bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg`, the ObjectKey is doc1/pic1.jpg. | string | No |
| Quiet | Indicates the method by which the result is returned for the deletion. Available values: true and false. Defaults to false. If it is set to true, only error message for failed deletion is returned. If it is set to false, messages indicating successful and failed deletion are returned. | bool | No |

#### Returned result

```go
type ObjectDeleteMultiResult struct {
	DeletedObjects []Object
	Errors         []struct {
		Key     string
		Code    string
		Message string
	}
}
type Object struct {
	Key		string 
}
```

| Parameter Name | Description | Type |
| -------------- | -------------------------------- | -------- |
| DeletedObjects | The information of the object that has been deleted | []struct |
| Errors | The information of the object that failed to be deleted | string |
| Key | The path of the object that failed to be deleted | string |
| Code | The error code for the object that failed to be deleted | string |
| Message | The error message for the object that failed to be deleted | string |

### Obtain object metadata

#### Feature

This API is used to obtain the meta information of the specified file.

#### Method prototype

```go
func (s *ObjectService) Head(ctx context.Context, key string, opt *ObjectHeadOptions) (*Response, error)
```

#### Request example

```go
key := "test/hello.txt"
resp, err := client.Object.Head(context.Background(), key, nil)
```

#### Parameters

```go
type ObjectHeadOptions struct {
	IfModifiedSince string 
}
```

| Parameter Name | Description | Type | Required |
| --------------- | ------------------------------------------------------------ | ------ | ---- |
| key | ObjectKey is the unique identifier of the object in the bucket. For example, in the object's access domain name `bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg`, the ObjectKey is doc1/pic1.jpg. | string | Yes |
| IfModifiedSince | The file is returned after it has been modified since the specified time. | string | No |

#### Returned result

```go
{
    'Content-Type': 'application/octet-stream',
    'Content-Length': '16807',
    'ETag': '"9a4802d5c99dafe1c04da0a8e7e166bf"',
    'Last-Modified': 'Wed, 28 Oct 2014 20:30:00 GMT',
    'X-Cos-Request-Id': 'NTg3NzQ3ZmVfYmRjMzVfMzE5N182NzczMQ=='
}
```

| Parameter Name | Description | Type |
| ---------- | ------------------------------------------------------------ | ------ |
| File meta information | The meta information of the file obtained, including Etag and X-Cos-Request-Id. The meta information of the configured file is also included. | string |

### Initialize multipart upload

#### Feature

This API is used to create a new multipart upload task. UploadId is returned.

#### Method prototype

```go
func (s *ObjectService) InitiateMultipartUpload(ctx context.Context, name string, opt *InitiateMultipartUploadOptions) (*InitiateMultipartUploadResult, *Response, error)
```

#### Request example

```go
name := "test_multipart"
// "opt" is optional.
v, resp, err := client.Object.InitiateMultipartUpload(context.Background(), name, nil）
```

#### Parameters

```go
type ObjectPutOptions struct {
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
	ContentLength      int   
	Expires            string 
	// Custom x-cos-meta-* header
	XCosMetaXXX        *http.Header 
	XCosStorageClass   string      
}
```

| Parameter Name | Description | Type | Required |
| -------------------- | ------------------------------------------------------------ | ----------- | ---- |
| r | The content of the uploaded file, which can be a file stream or a byte stream. When r is not bytes.Buffer/bytes.Reader/strings.Reader, opt.ObjectPutHeaderOptions.ContentLength must be specified. | io.Reader | Yes |
| key | ObjectKey is the unique identifier of the object in the bucket. For example, in the object's access domain name `bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg`, the ObjectKey is doc1/pic1.jpg. | string | Yes |
| XCosACL | Sets the file ACL, such as private, public-read, and public-read-write | string | No |
| XCosGrantFullControl | Grants the specified account the permission to read and write files. Format: `id=" ",id=" "`. For authorization to a sub-account, `id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`; for authorization to a root account, `id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`. For example: `id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"` | string | No |
| XCosGrantRead | Grants the specified account the permission to read files. Format: `id=" ",id=" "`. For authorization to a sub-account, `id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`; for authorization to a root account, `id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`. For example: `id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"` | string | No |
| XCosGrantWrite | Grants the specified account the permission to write files. Format: `id=" ",id=" "`. For authorization to a sub-account, `id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`; for authorization to a root account, `id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`. For example: `id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"` | string | No |
| XCosStorageClass | Sets file storage type: STANDARD and STANDARD_IA. Default: STANDARD | string | No |
| Expires | Sets Content-Expires. | string | No |
| CacheControl | Cache policy. Sets Cache-Control. | string | No |
| ContentType | Content Type. Sets Content-Type. | string | No |
| ContentDisposition | File name. Sets Content-Disposition. | string | No |
| ContentEncoding | Encoding format. Sets Content-Encoding. | string | No |
| ContentLength | Sets transmission length | string | No |
| XCosMetaXXX | User-defined file meta information. It must start with x-cos-meta. Otherwise, it will be ignored. | http.Header | No |

#### Returned result

```go
type InitiateMultipartUploadResult struct {
	Bucket   string
	Key      string
	UploadID string                   
} 
```

| Parameter Name | Description | Type |
| -------- | ------------------------------------------------------------ | ------ |
| UploadId | Indicates the ID of multipart upload | string |
| Bucket | Bucket name, which is in a format of bucket-appid | string |
| Key | ObjectKey is the unique identifier of the object in the bucket. For example, in the object's access domain name `bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg`, the ObjectKey is doc1/pic1.jpg. | string |

### Terminate multipart upload

#### Feature

This API is used to abort a multipart upload task, and all uploaded parts are deleted.

#### Method prototype

```go
func (s *ObjectService) AbortMultipartUpload(ctx context.Context, key, uploadID string) (*Response, error)
```

#### Request example

```go
key := "test_multipart.txt"
v, _, err := client.Object.InitiateMultipartUpload(context.Background(), key, nil)
// Abort
resp, err := client.Object.AbortMultipartUpload(context.Background(), key, v.UploadID)
```

#### Parameters

| Parameter Name | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ------ | ---- |
| key | ObjectKey is the unique identifier of the object in the bucket. For example, in the object's access domain name `bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg`, the ObjectKey is doc1/pic1.jpg. | string | Yes |
| UploadId | Indicates the ID of multipart upload | string | Yes |

### Upload a part

#### Feature

This API is used to upload a part to the specified UploadId. The size of a part is limited to 5 GB.

#### Method prototype

```go
func (s *ObjectService) UploadPart(ctx context.Context, key, uploadID string, partNumber int, r io.Reader, opt *ObjectUploadPartOptions) (*Response, error)
```

#### Request example

```go
// Note: The maximum number of parts to be uploaded is 10,000.
key := "test/test_multi_upload.go"
f := strings.NewReader("test heoo")
// "opt" is optional.
_, err := client.Object.UploadPart(
    context.Background(), key, uploadID, 1, f, nil,
)
```

#### Parameters

```go
type ObjectUploadPartOptions struct {
    ContentLength   int                                      
}
```

| Parameter Name | Description | Type | Required |
| ------------- | ------------------------------------------------------------ | --------- | ---- |
| key | ObjectKey is the unique identifier of the object in the bucket. For example, in the object's access domain name `bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg`, the ObjectKey is doc1/pic1.jpg. | string | Yes |
| UploadId | Indicates the ID of multipart upload, which is generated by InitiateMultipartUpload. | string | Yes |
| PartNumber | Indicates the number of the uploaded part | int | Yes |
| r | The content of the uploaded part, which can be a local file stream or an input stream. When r is not bytes.Buffer/bytes.Reader/strings.Reader, opt.ContentLength must be specified. | io.Reader | Yes |
| ContentLength | Sets transmission length. | int | No |

#### Returned result

```go
{
    'ETag': 'string'
}
```

| Parameter Name | Description | Type |
| -------- | ------------------- | ------ |
| ETag | MD5 of the uploaded part | string |

### List parts 

#### Feature

This API is used to list the information of the uploaded parts in the specified UploadId.

#### Method prototype

```go
func (s *ObjectService) ListParts(ctx context.Context, name, uploadID string) (*ObjectListPartsResult, *Response, error)
```

#### Request example

```go
key := "test/test_list_parts.go"
v, resp, err := client.Object.ListParts(context.Background(), key, uploadID) 
```

#### Parameters

| Parameter Name | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ------ | ---- |
| key | ObjectKey is the unique identifier of the object in the bucket. For example, in the object's access domain name `bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg`, the ObjectKey is doc1/pic1.jpg. | string | Yes |
| UploadId | Indicates the ID of multipart upload, which is generated by InitiateMultipartUpload. | string | Yes |

#### Returned result

```go
type ObjectListPartsResult struct {
	Bucket               string
	EncodingType         string 
	Key                  string
	UploadID             string     
	Initiator            *Initiator 
	Owner                *Owner     
	StorageClass         string
	PartNumberMarker     int
	NextPartNumberMarker int 
	MaxParts             int
	IsTruncated          bool
	Parts                []Object 
}
type Initiator struct {
	UIN         string
	ID          string 
	DisplayName string                                
}
type Owner struct {
	UIN         string
	ID          string 
	DisplayName string                                
}
type Object struct {
	Key          string 
	ETag         string 
	Size         int    
	PartNumber   int    
	LastModified string 
	StorageClass string 
	Owner        *Owner
}
```

| Parameter Name | Description | Type |
| -------------------- | ------------------------------------------------------------ | ------ |
| Bucket | Bucket name, which is in a format of bucketname-appid. | string |
| EncodingType | Indicates the encoding method of the returned value. The value is not encoded by default. Available value: url | string |
| Key | ObjectKey is the unique identifier of the object in the bucket. For example, in the object's access domain name `bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg`, the ObjectKey is doc1/pic1.jpg. | string |
| UploadId | Indicates the ID of multipart upload, which is generated by InitiateMultipartUpload. | string |
| Initiator | Creator of the multipart upload, including DisplayName, UIN and ID | struct |
| Owner | Information of the file owner, including DisplayName, UIN and ID | struct |
| StorageClass | Sets file storage type: STANDARD and STANDARD_IA. Default: STANDARD | string |
| PartNumberMarker | Indicates that the parts are listed from the one following PartNumberMarker. It defaults to 0, which means the parts are listed from the first one. | int |
| NextPartNumberMarker | Marks the starting point of the next list of parts | int |
| MaxParts | The maximum number of returned parts. It defaults to 1000. | int |
| IsTruncated | Indicates whether the returned parts are truncated | bool |
| Part | Information of the uploaded part, including ETag, PartNumber, Size, and LastModified | struct |

### Complete multipart upload

#### Feature

This API is used to construct all parts in the specified UploadId into a complete file. The size of the resulting file must be larger than 1 MB, otherwise an error is returned.

#### Method prototype

```go
func (s *ObjectService) CompleteMultipartUpload(ctx context.Context, key, uploadID string, opt *CompleteMultipartUploadOptions) (*CompleteMultipartUploadResult, *Response, error)
```

#### Request example

```go
key := "test/test_complete_upload.go"
v, resp, err := client.Object.InitiateMultipartUpload(context.Background(), key, nil)
uploadID := v.UploadID
blockSize := 1024 * 1024 * 3

opt := &cos.CompleteMultipartUploadOptions{}
for i := 1; i < 5; i++ {
    etag := uploadPart(c, key, uploadID, blockSize, i)
    opt.Parts = append(opt.Parts, cos.Object{
        PartNumber: i, ETag: etag},
    )
}

v, resp, err = client.Object.CompleteMultipartUpload(
    context.Background(), key, uploadID, opt,
)
```

#### Parameters

```go
type CompleteMultipartUploadOptions struct {
	Parts   []Object 
}
type Object struct { 
	ETag         string 
	PartNumber   int     
}
```

| Parameter Name | Description | Type | Required |
| ------------------------------ | ------------------------------------------------------------ | ------ | ---- |
| key | ObjectKey is the unique identifier of the object in the bucket. For example, in the object's access domain name `bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg`, the ObjectKey is doc1/pic1.jpg. | string | Yes |
| UploadId | Indicates the ID of multipart upload, which is generated by InitiateMultipartUpload. | string | Yes |
| CompleteMultipartUploadOptions | ETag and PartNumber information for all parts | struct | Yes |

#### Returned result

```go
type CompleteMultipartUploadResult struct {
	Location string
	Bucket   string
	Key      string
	ETag     string
}
```

| Parameter Name | Description | Type |
| -------- | ------------------------------------------------------------ | ------ |
| Location | URL address | string |
| Bucket | Bucket name, which is in a format of bucketname-appid. | string |
| Key | ObjectKey is the unique identifier of the object in the bucket. For example, in the object's access domain name `bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg`, the ObjectKey is doc1/pic1.jpg. | string |
| ETag | The unique tag of the resulting object. It is not the MD5 check value for the object content, but is only used to check the uniqueness of the object. To verify the file content, you can check the ETag of each part during the process of upload. | string |

### Set the object ACL

#### Feature

This API is used to set the file ACL information by passing header through XCosACL, XCosGrantFullControl, XCosGrantRead and XCosGrantWrite or by passing body thruogh ACLXML. You can only use one of these two methods, otherwise a conflict is returned.

> !The number of access policies is up to 1000. Do not set object ACL control if it is not required. The object inherits the bucket permissions by default.

#### Method prototype

```go
func (s *ObjectService) PutACL(ctx context.Context, key string, opt *ObjectPutACLOptions) (*Response, error)
```

#### Request example

Set an object ACL through Header.

```go
opt := &cos.ObjectPutACLOptions{
    Header: &cos.ACLHeaderOptions{
        XCosACL: "private",
    },
}
key := "test/hello.txt"
resp, err := client.Object.PutACL(context.Background(), key, opt)
```

Set an object ACL through Body.

```go
opt = &cos.ObjectPutACLOptions{
    Body: &cos.ACLXml{
        Owner: &cos.Owner{
            ID: "qcs::cam::uin/100000760461:uin/100000760461",
        },
        AccessControlList: []cos.ACLGrant{
            {
                Grantee: &cos.ACLGrantee{
                    Type: "RootAccount",
                    ID:   "qcs::cam::uin/100000760461:uin/100000760461",
                },

                Permission: "FULL_CONTROL",
            },
        },
    },
}

resp, err = client.Object.PutACL(context.Background(), key, opt)
```

#### Parameters

```go
type ACLHeaderOptions struct {
	XCosACL              string 
	XCosGrantRead        string 
	XCosGrantWrite       string 
	XCosGrantFullControl string 
}
```

| Parameter Name | Description | Type | Required |
| -------------------- | ------------------------------------------------------------ | ------ | ---- |
| key | ObjectKey is the unique identifier of the object in the bucket. For example, in the object's access domain name `bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg`, the ObjectKey is doc1/pic1.jpg. | string | Yes |
| XCosACL | Sets the bucket ACL, such as private, public-read, and public-read-write. | string | No |
| XCosGrantFullControl | Grants the specified account the permission to read and write buckets. Format: `id=" ",id=" "`. For authorization to a sub-account, `id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`; for authorization to a root account, `id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`. For example: `id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"` | string | No |
| XCosGrantRead | Grants the specified account the permission to read buckets. Format: `id=" ",id=" "`. For authorization to a sub-account, `id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`; for authorization to a root account, `id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`. For example: `id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"` | string | No |
| XCosGrantWrite | Grants the specified account the permission to write buckets. Format: `id=" ",id=" "`. For authorization to a sub-account, `id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`; for authorization to a root account, `id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`. For example: `id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"` | string | No |
| ACLXML | Grants the specified account the access to buckets. For more information on the format, see the response for "get object acl". | struct | No |

### Get the object ACL

#### Feature

This API is used to get the ACL information of the specified file.

#### Method prototype

```go
func (s *ObjectService) GetACL(ctx context.Context, key string) (*ObjectGetACLResult, *Response, error)
```

#### Request example

```go
key := "test/hello.txt"
v, resp, err := client.Object.GetACL(context.Background(), key)
```

#### Parameters

| Parameter Name | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ------ | ---- |
| key | ObjectKey is the unique identifier of the object in the bucket. For example, in the object's access domain name `bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg`, the ObjectKey is doc1/pic1.jpg. | string | Yes |

#### Returned result

```go
type ACLXml struct {
	Owner             *Owner
	AccessControlList []ACLGrant 
}
type Owner struct { 
	ID          string 
	DisplayName string
}
type ACLGrant struct {
	Grantee    *ACLGrantee
	Permission string
}
type ACLGrantee struct {
	Type        string 
	ID          string 
	DisplayName string
    UIN         string 
}
```

| Parameter Name | Description | Type |
| ----------------- | ------------------------------------------------------------ | ------ |
| Owner | Information of the bucket owner, including DisplayName and ID | struct |
| AccessControlList | Information of the user granted the bucket permissions, including Grantee and Permission | struct |
| Grantee | Information of grantee, including DisplayName, Type, ID and UIN | struct |
| Type | Type of grantee: CanonicalUser or Group | string |
| ID | ID of grantee when Type is CanonicalUser | string |
| DisplayName | Name of grantee | string |
| UIN | UIN of grantee when Type is Group | string |
| Permission | Bucket permissions of grantee. Available values: FULL_CONTROL (read and write permissions), WRITE (write permission), and READ (read permission) | string |

### Set object replication

#### Feature

This API is used to copy a file from source path to destination path. The recommended file size is 1 MB to 5 GB. For any file greater than 5 GB, use multipart upload (Upload - Copy). In the process of copying, file meta-attributes and ACLs can be modified. You can use this API to move or rename a file, modify file attributes, and create a copy.
>!For cross-account replication, set the public-read permission to the copied files first, or grant the target account this permission. It is not required under the same account.

#### Method prototype

```go
func (s *ObjectService) Copy(ctx context.Context, key, sourceURL string, opt *ObjectCopyOptions) (*ObjectCopyResult, *Response, error)
```

#### Request example

```go
u, _ := url.Parse("http://test-1253846586.cos.ap-guangzhou.myqcloud.com")
source := "test/objectMove_src"
soruceURL := fmt.Sprintf("%s/%s", u.Host, source)
dest := "test/objectMove_dest"
//opt := &cos.ObjectCopyOptions{}
r, resp, err := client.Object.Copy(context.Background(), dest, soruceURL, nil)
```

#### Parameters

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

| Parameter Name | Description | Type | Required |
| ------------------------------- | ------------------------------------------------------------ | ----------- | ---- |
| key | ObjectKey is the unique identifier of the object in the bucket. For example, in the object's access domain name `bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg`, the ObjectKey is doc1/pic1.jpg. | string | Yes |
| sourceURL | The URL of the copied source file | string | Yes |
| XCosACL | Sets the file ACL, such as private, public-read, and public-read-write | string | No |
| XCosGrantFullControl | Grants the specific account the permission to read and write files. Format: id=" ",id=" ". For authorization to a sub-account, `id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`; for authorization to a root account, `id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`. For example: `id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"` | string | No |
| XCosGrantRead | Grants the specified account the permission to read files. Format: `id=" ",id=" "`. For authorization to a sub-account, `id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`; for authorization to a root account, `id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`. For example: `id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"` | string | No |
| XCosGrantWrite | Grants the specified account the permission to write files. Format: `id=" ",id=" "`. For authorization to a sub-account, `id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`; for authorization to a root account, `id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`. For example: `id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"` | string | No |
| XCosMetadataDirective | Available values: Copy and Replaced. When it is set to Copy, ignore the configured user metadata information and copy the file directly. When it is set to Replaced, modify the metadata according to the configured meta information. If the destination path is identical to the source path, it must be set to Replaced. | string | Yes |
| XCosCopySourceIfModifiedSince | The operation is performed if the object is modified after the specified time, otherwise error code 412 is returned. It can be used with XCosCopySourceIfNoneMatch. Using it with other conditions can cause a conflict. | string | No |
| XCosCopySourceIfUnmodifiedSince | The operation is performed if the object is not modified after the specified time, otherwise error code 412 is returned. It can be used with XCosCopySourceIfMatch. Using it with other conditions can cause a conflict. | string | No |
| XCosCopySourceIfMatch | The operation is performed if the Etag of the object is the same as the given one, otherwise error code 412 is returned. It can be used with XCosCopySourceIfUnmodifiedSince. Using it with other conditions can cause a conflict. | string | No |
| XCosCopySourceIfNoneMatch | The operation is performed if the Etag of the object is different from the given one, otherwise error code 412 is returned. It can be used with XCosCopySourceIfModifiedSince. Using it with other conditions can cause a conflict. | string | No |
| XCosStorageClass | Sets file storage type: STANDARD and STANDARD_IA. Default: STANDARD | string | No |
| XCosMetaXXX | User-defined file meta information | http.Header | No |
| XCosCopySource | Source file URL path. You can specify the history version with the versionid subresource. | string | No |

#### Returned result

Attributes of the uploaded file:

```go
type ObjectCopyResult struct {
    ETag         string 
    LastModified string
}
```

| Parameter Name | Description | Type |
| ------------ | -------------------------- | ------ |
| ETag | MD5 of the copied file | string |
| LastModified | The time when the copied file was last modified | string |

## Exception Description

The Response returned by the API is the [Response](https://golang.org/pkg/net/http/#Response) type of Golang standard HTTP library.
You can get the error message via err.Error(), which provides the message returned by the server. For more information on error codes, see [Error Codes](https://cloud.tencent.com/document/product/436/7730).

