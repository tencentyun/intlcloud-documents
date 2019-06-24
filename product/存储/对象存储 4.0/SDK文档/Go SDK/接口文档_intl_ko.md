COS Go SDK(XML API) 작업은 해당 API의 Result 구조와 Golang HTTP 표준 라이브러리의 [Response](https://golang.org/pkg/net/http/#Response) 구조를 반환합니다.

> ?문서에서 나오는 SecretId, SecretKey, Bucket 등과 같은 명칭의 함의 및 획득 방법은 [COS 용어집](https://cloud.tencent.com/document/product/436/7751)을 참조하십시오.

## Service API 설명

### 버킷 리스트 획득

#### 기능 설명

요청자 이름 하의 모든 저장 공간 리스트(Bucket list)를 획득하는 데 사용합니다.

#### 방식 프로토타입

```go
func (s *ServiceService) Get(ctx context.Context) (*ServiceGetResult, *Response, error)
```

#### 요청 예시

```go
s, resp, err := c.Service.Get(context.Background())
```

#### 반환 결과 설명

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

| 매개변수 이름 | 매개변수 설명 | 유형 |
| ------------ | ------------------------------------------------------------ | ------ |
| ID           | 버킷 소유자 ID                                           | string |
| DisplayName  | 버킷 소유자 이름                                      | string |
| Name         | 버킷 이름                                                | string |
| Region       | 버킷 소재 지역                                              | string |
| CreationDate | 버킷 생성 시간. ISO8601 형식, 예: 2016-11-09T08:46:32.000Z | string |

## Bucket API 설명

### 버킷 생성

#### 기능 설명

지정 계정 하에 하나의 새로운 버킷을 생성합니다. 버킷이 이미 있을 경우 오류를 반환합니다.

#### 방식 프로토타입

```go
func (s *BucketService) Put(ctx context.Context, opt *BucketPutOptions) (*Response, error)
```

#### 요청 예시

```go
opt := &cos.BucketPutOptions{
	XCosACL: "public-read",
}
resp, err := client.Bucket.Put(context.Background(), opt)
```

#### 매개변수 설명

```go
type BucketPutOptions struct {
	XCosACL              string
	XCosGrantRead        string  
	XCosGrantWrite       string  
	XCosGrantFullControl string
}
```

| 매개변수 이름             | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| -------------------- | ------------------------------------------------------------ | ------ | ---- |
| XCosACL              | 버킷의 ACL 설정, 예: private, public-read, public-read-write | string | 아니요   |
| XCosGrantFullControl | 지정 계정에 버킷에 대한 읽기/쓰기 권한을 부여합니다. 형식은 `id=" ",id=" "` 서브 계정에 권한을 부여해야 할 경우, 형식은 `id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"` 루트 계정에 권한을 부여해야 할 경우, 형식은 `id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"` 예: `id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"` | string | 아니요   |
| XCosGrantRead        | 지정 계정에 버킷에 대한 읽기 권한을 부여합니다. 형식은 `id=" ",id=" "` 서브 계정에 권한을 부여해야 할 경우, 형식은 `id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"` 루트 계정에 권한을 부여해야 할 경우, 형식은 `id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"` 예: `id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"` | string | 아니요   |
| XCosGrantWrite       | 지정 계정에 버킷에 대한 쓰기 권한을 부여합니다. 형식은 `id=" ",id=" "` 서브 계정에 권한을 부여해야 할 경우, 형식은 `id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"` 루트 계정에 권한을 부여해야 할 경우, 형식은 `id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"` 예: `id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"` | string | 아니요   |

### 버킷 삭제

#### 기능 설명

지정 계정에서 이미 존재하는 버킷을 삭제하고, 삭제 시 버킷은 비어있어야 합니다.

#### 방식 프로토타입

```go
func (s *BucketService) Delete(ctx context.Context) (*Response, error)
```

#### 요청 예시

```go
resp, err := client.Bucket.Delete(context.Background())
```

### 버킷 및 해당 권한 조회

#### 기능 설명

버킷이 존재하는지 또는 액세스 권한이 있는지를 조회합니다.

#### 방식 프로토타입

```go
func (s *BucketService) Head(ctx context.Context) (*Response, error)
```

#### 요청 예시

```go
resp, err := client.Bucket.Head(context.Background())
```

### 지역 정보 획득

#### 기능 설명

버킷이 위치한 지역의 정보를 조회합니다.

#### 방식 프로토타입

```go
func (s *BucketService) GetLocation(ctx context.Context) (*BucketGetLocationResult, *Response, error)
```

#### 요청 예시

```go
v, resp, err := client.Bucket.GetLocation(context.Background())
```

#### 반환 결과 설명

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

| 매개변수 이름 | 매개변수 설명 | 유형 |
| -------- | --------------------- | ------ |
| Location | 버킷 소재 지역의 정보 | string |

### 객체 리스트 획득

#### 기능 설명

지정 버킷의 모든 객체를 획득합니다.

#### 방식 프로토타입

```go
func (s *BucketService) Get(ctx context.Context, opt *BucketGetOptions) (*BucketGetResult, *Response, error)
```

#### 요청 예시

```go
opt := &cos.BucketGetOptions{
	Prefix:  "test",
	MaxKeys: 100,                                
}
v, resp, err := client.Bucket.Get(context.Background(), opt)
```

#### 매개변수 설명

```go
type BucketGetOptions struct {
	Prefix       string
	Delimiter    string
	EncodingType string
	Marker       string
	MaxKeys      int    
}
```

| 매개변수 이름             | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| ------------ | ------------------------------------------------------------ | ------ | ---- |
| Prefix       | 기본적으로 비어있습니다. 객체의 키에 대해 필터링을 진행하여, prefix에 매칭되는 접두사를 가진 객체를 나열합니다 | string | 아니요   |
| Delimiter    | 기본적으로 비어있습니다. 구분 기호를 설정합니다. 예를 들어 / 설정으로 폴더를 시뮬레이션합니다                  | string | 아니요   |
| EncodingType | 기본으로 인코딩하지 않음, 반환값의 인코딩 방식을 지정합니다. 선택 가능값: url                | String | 아니요   |
| Marker       | 기본으로 UTF-8 이진법 순서로 항목을 나열하고, 반환된 객체의 릴스트의 시작 위치를 표시합니다 | string | 아니요   |
| MaxKeys      | 반환되는 객체의 최대 수량, 기본값은 1000                    | int    | 아니요   |

#### 반환 결과 설명

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

| 매개변수 이름 | 매개변수 설명 | 유형 |
| -------------- | ------------------------------------------------------------ | -------- |
| Name           | 버킷 이름, bucketname-appid으로 구성                        | string   |
| Prefix         | 기본적으로 비어있습니다. 객체의 키에 대해 필터링을 진행하여, prefix에 매칭되는 접두사를 가진 객체를 나열합니다 | string |
| Marker         | 기본으로 UTF-8 이진법 순서로 항목을 나열하고, 반환된 객체의 리스트의 시작 위치를 표시합니다 | string |
| NextMarker     | IsTruncated가 true일 경우, 다음의 반환된 객체의 리스트 시작 위치를 표시합니다 | string   |
| Delimiter      | 기본적으로 비어 있습니다. 구분 기호를 설정합니다. 예를 들어 / 설정으로 폴더를 시뮬레이션합니다                  | string |
| MaxKeys        | 반환되는 객체의 최대 수량, 기본값은 1000                    | int    |
| IsTruncated    | 반환된 객체가 잘렸는지 여부를 표시합니다                                  | bool     |
| Contents       | 모든 객체의 메타 정보를 포함한 리스트. 각 객체 유형에는 ETag, StorageClass, Key, Owner, LastModified, Size 등의 정보가 포함됩니다 | []Object |
| CommonPrefixes | Prefix 접두어로 시작하고 Delimiter로 끝나는 키는 같은 종류로 분류됩니다      | []string |
| EncodingType   | 기본으로 인코딩하지 않음, 반환값의 인코딩 방식을 지정합니다. 선택 가능값: url                | String   |

### 멀티파트 업로드 조회

#### 기능 설명

지정된 버킷에서 진행 중인 모든 멀티파트 업로드를 조회합니다.

#### 방식 프로토타입

```go
func (s *BucketService) ListMultipartUploads(ctx context.Context, opt *ListMultipartUploadsOptions) (*ListMultipartUploadsResult, *Response, error)
```

#### 요청 예시

```go
opt := &cos.ListMultipartUploadsOptions{
	Prefix: "test",
}
v, resp, err := client.Bucket.ListMultipartUploads(context.Background(), opt)
```

#### 매개변수 설명

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

| 매개변수 이름             | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| -------------- | ------------------------------------------------------------ | ------ | ---- |
| Delimiter    | 기본적으로 비어있습니다. 구분 기호를 설정합니다                 | string | 아니요   |
| EncodingType   | 기본으로 인코딩하지 않음, 반환값의 인코딩 방식을 지정합니다. 선택 가능값: url                | String | 아니요   |
| Prefix       | 기본적으로 비어있습니다. 멀티파트 업로드의 키에 대해 필터링을 진행하여, prefix에 매칭되는 접두사를 가진 멀티파트 업로드를 나열합니다 | string | 아니요   |
| MaxUploads     | 멀티파트 업로드의 최대 반환 수량, 기본값은 1000                   | int    | 아니요   |
| KeyMarker      | UploadIdMarker와 함께 사용하며, 멀티파트 업로드의 시작 위치를 나타냅니다       | string | 아니요   |
| UploadIdMarker | KeyMarker와 함께 사용하며, 멀티파트 업로드의 시작 위치를 나타냅니다. KeyMarker를 지정하지 않으면, UploadIdMarker는 무시됩니다 | string | 아니요   |

#### 반환 결과 설명

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

| 매개변수 이름 | 매개변수 설명 | 유형 |
| ------------------ | ------------------------------------------------------------ | -------- |
| Bucket             | 버킷 이름, bucketname-appid으로 구성                        | string   |
| EncodingType       | 기본으로 인코딩하지 않음, 반환값의 인코딩 방식을 지정합니다. 선택 가능값: url                | String   |
| KeyMarker          | UploadIdMarker와 함께 사용하며, 멀티파트 업로드의 키 시작 위치를 나타냅니다       | string |
| UploadIdMarker     | KeyMarker와 함께 사용하며, 멀티파트 업로드의 uploadid 시작 위치를 나타냅니다. KeyMarker를 지정하지 않으면, UploadIdMarker는 무시됩니다 | string |
| NextKeyMarker      | IsTruncated가 true일 경우, 다음 멀티파트 업로드의 키 시작 위치를 표시합니다 | string   |
| NextUploadIDMarker | IsTruncated가 true일 경우, 다음 멀티파트 업로드의 uploadid 시작 위치를 표시합니다 | string   |
| MaxUploads         | 멀티파트 업로드의 최대 반환 수량, 기본값은 1000                   | int    |
| IsTruncated    | 반환된 멀티파트가 잘렸는지 여부를 표시합니다                                  | bool     |
| Upload             | 모든 멀티파트를 포함한 리스트, UploadId, storageClass, Key, Owner, Initiator, Initiated 등의 정보가 포함됩니다 | []struct |
| Prefix             | 기본적으로 비어있습니다. 멀티파트 업로드의 키에 대해 필터링을 진행하여, prefix에 매칭되는 접두사를 가진 멀티파트 업로드를 나열합니다 | string |
| Delimiter          | 기본적으로 비어있습니다. 구분 기호를 설정합니다                 | string |
| CommonPrefixes | Prefix로 시작하고 Delimiter로 끝나는 키는 같은 종류로 분류됩니다      | []string |

### 버킷 ACL 설정

#### 기능 설명

버킷의 ACL 정보를 설정하고, XCosACL, XCosGrantFullControl, XCosGrantRead, XCosGrantWrite를 통해 헤더를 입력하는 방식으로 ACL을 설정하거나 ACLXML를 통해 본문을 입력하여 ACL을 설정합니다. 두 방식 중 하나만 선택할 수 있으며 그렇지 않으면 충돌이 반환됩니다.

#### 방식 프로토타입

```go
func (s *BucketService) PutACL(ctx context.Context, opt *BucketPutACLOptions) (*Response, error)
```

#### 요청 예시

헤더를 통한 버킷 ACL 설정

```go
opt := &cos.BucketPutACLOptions{
	Header: &cos.ACLHeaderOptions{
		//private, public-read, public-read-write
		XCosACL: "private",
	},
}
resp, err := client.Bucket.PutACL(context.Background(), opt)
```

본문을 통한 버킷 ACL 설정

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

#### 매개변수 설명

```go
type ACLHeaderOptions struct {
	XCosACL              string
	XCosGrantRead        string
	XCosGrantWrite       string
	XCosGrantFullControl string
}
```

| 매개변수 이름             | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| -------------------- | ------------------------------------------------------------ | ------ | ---- |
| XCosACL              | 버킷의 ACL 설정, 예: private, public-read, public-read-write | string | 아니요   |
| XCosGrantFullControl | 지정 계정에 버킷에 대한 읽기/쓰기 권한을 부여합니다. 형식은 `id=" ",id=" "` 서브 계정에 권한을 부여해야 할 경우, 형식은 `id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"` 루트 계정에 권한을 부여해야 할 경우, 형식은 `id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"` 예: `id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"` | string | 아니요   |
| XCosGrantRead        | 지정 계정에 버킷에 대한 읽기 권한을 부여합니다. 형식은 `id=" ",id=" "` 서브 계정에 권한을 부여해야 할 경우, 형식은 `id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"` 루트 계정에 권한을 부여해야 할 경우, 형식은 `id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"` 예: `id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"` | string | 아니요   |
| XCosGrantWrite       | 지정 계정에 버킷에 대한 쓰기 권한을 부여합니다. 형식은 `id=" ",id=" "` 서브 계정에 권한을 부여해야 할 경우, 형식은 `id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"` 루트 계정에 권한을 부여해야 할 경우, 형식은 `id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"` 예: `id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"` | string | 아니요   |
| ACLXML               | 지정 계정에 버킷에 대한 액세스 권한을 부여하며, 구체적인 형식은 get bucket acl 반환 결과 설명을 참조하십시오 | struct | 아니요   |



### 버킷 ACL 획득

#### 기능 설명

지정 버킷의 ACL 정보를 획득합니다.

#### 방식 프로토타입

```go
func (s *BucketService) GetACL(ctx context.Context) (*BucketGetACLResult, *Response, error)
```

#### 요청 예시

```go
v, resp, err := client.Bucket.GetACL(context.Background())
```

#### 반환 결과 설명

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

| 매개변수 이름 | 매개변수 설명 | 유형 |
| ----------------- | ------------------------------------------------------------ | ------ |
| Owner             | 버킷 소유자의 정보, DisplayName 및 ID가 포함됩니다                  | struct |
| AccessControlList | 버킷 권한 부여자의 정보, Grantee 및 Permission이 포함됩니다           | struct |
| Grantee           | 권한 부여자의 정보, DisplayName, Type, ID 및 UIN이 포함됩니다          | struct |
| Type              | 권한 부여자의 종류, 유형은 CanonicalUser 또는 Group입니다            | string |
| ID                | 유형이 CanonicalUser일 경우, 해당 권한 부여자의 ID                | string |
| DisplayName       | 권한 부여자의 이름                                             | string |
| UIN               | 유형이 Group일 때, 해당 권한 부여자의 UIN                       | string |
| Permission        | 부여자가 소유한 버킷의 권한, 선택 가능 값은 FULL_CONTROL, WRITE, READ이며, 각각 읽기/쓰기 권한, 쓰기 권한, 읽기 권한에 대응합니다 | string |

### 크로스 도메인 설정

#### 기능 설명

지정 버킷의 CORS 구성을 설정합니다.

#### 방식 프로토타입

```go
func (s *BucketService) PutCORS(ctx context.Context, opt *BucketPutCORSOptions) (*Response, error)
```

#### 요청 예시

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

#### 매개변수 설명

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

| 매개변수 이름             | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| -------------- | ------------------------------------------------------------ | -------- | ---- |
| BucketCORSRule | 해당하는 CORS 규칙을 설정하며, ID, MaxAgeSeconds, AllowedOrigin, AllowedMethod, AllowedHeader, ExposeHeader 등이 포함됩니다 | struct   | 예   |
| ID             | 규칙 ID를 설정합니다                                                | string   | 아니요   |
| AllowedMethods | 허용 방법을 설정합니다, 예: GET, PUT, HEAD, POST, DELETE              | []string | 예   |
| AllowedOrigins | 허용된 액세스 소스를 설정합니다. 예: `"http://cloud.tencent.com"`, 와일드카드 *를 지원합니다 | []string | 예   |
| AllowedHeaders | 요청이 어떠한 사용자 지정 HTTP 요청 헤더를 사용할 수 있도록 설정하며, 와일드카드 *를 지원합니다     | []string | 아니요   |
| MaxAgeSeconds  | OPTIONS 요청이 얻은 결과의 유효기간 설정                            | int      | 아니요   |
| ExposeHeaders  |브라우저가 수신할 수 있는 서버의 사용자 지정 헤더 정보 설정 |String| 아니요   |

### CORS 구성 획득

#### 기능 설명

지정 버킷의 CORS 구성을 획득합니다.

#### 방식 프로토타입

```go
func (s *BucketService) GetCORS(ctx context.Context) (*BucketGetCORSResult, *Response, error)
```

#### 요청 예시

```go
v, resp, err := client.Bucket.GetCORS(context.Background())
```

#### 반환 결과 설명

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

| 매개변수 이름             | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| -------------- | ------------------------------------------------------------ | -------- | ---- |
| BucketCORSRule | 해당하는 CORS 규칙을 설정하며, ID, MaxAgeSeconds, AllowedOrigin, AllowedMethod, AllowedHeader, ExposeHeader 등이 포함됩니다 | struct   | 예   |
| ID             | 규칙 ID를 설정합니다                                                | string   | 아니요   |
| AllowedMethods | 허용 방법을 설정합니다, 예: GET, PUT, HEAD, POST, DELETE              | []string | 예   |
| AllowedOrigins | 허용된 액세스 소스를 설정합니다. 예: `"http://cloud.tencent.com"`, 와일드카드 *를 지원합니다 | []string | 예   |
| AllowedHeaders | 요청이 어떠한 사용자 지정 HTTP 요청 헤더를 사용할 수 있도록 설정하며, 와일드카드 *를 지원합니다     | []string | 아니요   |
| MaxAgeSeconds  | OPTIONS 요청이 얻은 결과의 유효기간 설정                            | int      | 아니요   |
| ExposeHeaders  |브라우저가 수신할 수 있는 서버의 사용자 지정 헤더 정보 설정 |String| 아니요   |

### CORS 구성 삭제

#### 기능 설명

지정 버킷의 CORS 구성을 삭제합니다.

#### 방식 프로토타입

```go
func (s *BucketService) DeleteCORS(ctx context.Context) (*Response, error)
```

#### 요청 예시

```go
resp, err := client.Bucket.DeleteCORS(context.Background())
```

### 수명 주기 설정

#### 기능 설명

지정 버킷의 수명 주기 구성을 설정합니다.

#### 방식 프로토타입

```go
func (s *BucketService) PutLifecycle(ctx context.Context, opt *BucketPutLifecycleOptions) (*Response, error)
```

#### 요청 예시

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

#### 매개변수 설명

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

| 매개변수 이름             | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| ------------------------------ | ------------------------------------------------------------ | ------ | ---- |
| BucketLifecycleRule            | 해당 규칙을 설정하며, ID, Filter, Status, Expiration, Transition, AbortIncompleteMultipartUpload 등이 포함됩니다 | List   | 예   |
| ID                             | 규칙 ID를 설정합니다                                                | string | 아니요   |
| Status                         | 규칙을 사용할지를 설정하며, 선택 가능 값은 Enabled 또는 Disabled입니다           | string | 예   |
| Filter                         | 규칙이 영향을 미치는 객체 집합을 설명하는 데 사용되며, 버킷의 모든 객체를 설정해야 할 경우, Prefix는 비워두기로 설정하십시오 | struct | 예   |
| Transition                     | 객체 스토리지 클래스 전환 규칙을 설정하며, 일수 Days 또는 날짜 Date를 지정할 수 있습니다. Date의 형식은 반드시 GMT ISO 8601이어야 합니다. StorageClass는 Standard_IA, Archive를 선택할 수 있으며, 해당 클래스의 규칙을 동시에 여러개 설정할 수 있습니다 | struct | 아니요   |
| Expiration                     | 객체 만료 규칙을 설정하며, 일수 Days 또는 날짜 Date를 지정할 수 있습니다. Date의 형식은 반드시 GMT ISO 8601이어야 합니다. | struct | 아니요   |
| AbortIncompleteMultipartUpload | 멀티파트 업로드 시작 후 몇 일이 내에 업로드가 완료되어야 하는지 지정합니다                       | struct | 아니요   |

### 수명 주기 조회

#### 기능 설명

지정 버킷의 수명 주기 구성을 조회합니다.

#### 방식 프로토타입

```go
func (s *BucketService) GetLifecycle(ctx context.Context) (*BucketGetLifecycleResult, *Response, error)
```

#### 요청 예시

```go
v, resp, err := client.Bucket.GetLifecycle(context.Background())
```

#### 반환 결과 설명

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

| 매개변수 이름             | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| ------------------------------ | ------------------------------------------------------------ | ------ | ---- |
| BucketLifecycleRule            | 해당 규칙을 설정하며, ID, Filter, Status, Expiration, Transition, AbortIncompleteMultipartUpload 등이 포함됩니다 | List   | 예   |
| ID                             | 규칙 ID를 설정합니다                                                | string | 아니요   |
| Status                         | 규칙을 사용할지를 설정하며, 선택 가능 값은 Enabled 또는 Disabled입니다           | string | 예   |
| Filter                         | 규칙이 영향을 미치는 객체 집합을 설명하는 데 사용되며, 버킷의 모든 객체를 설정해야 할 경우, Prefix는 비워두기로 설정하십시오 | struct | 예   |
| Transition                     | 객체 스토리지 클래스 전환 규칙을 설정하며, 일수 Days 또는 날짜 Date를 지정할 수 있습니다. Date의 형식은 반드시 GMT ISO 8601이어야 합니다. StorageClass는 Standard_IA, Archive를 선택할 수 있으며, 해당 클래스의 규칙을 동시에 여러개 설정할 수 있습니다 | struct | 아니요   |
| Expiration                     | 객체 만료 규칙을 설정하며, 일수 Days 또는 날짜 Date를 지정할 수 있습니다. Date의 형식은 반드시 GMT ISO 8601이어야 합니다. | struct | 아니요   |
| AbortIncompleteMultipartUpload | 멀티파트 업로드 시작 후 몇 일이 내에 업로드가 완료되어야 하는지 지정합니다                       | struct | 아니요   |

### 수명 주기 삭제

#### 기능 설명

지정 버킷의 수명 주기 구성을 삭제합니다.

#### 방식 프로토타입

```go
func (s *BucketService) DeleteLifecycle(ctx context.Context) (*Response, error)
```

#### 요청 예시

```go
resp, err := client.Bucket.DeleteLifecycle(context.Background())
```

## Object API 설명

### 업로드 객체

#### 기능 설명

지정된 버킷에 로컬 파일 또는 입력 스트림 업로드를 지원합니다. 20MB 미만의 작은 파일을 업로드하는 것이 좋으며, 1회 업로드 크기는 5GB로 제한됩니다. 큰 파일 업로드는 멀티파트 업로드를 사용하십시오.

> !현재 액세스 정책 항목은 1000으로 제한되어 있습니다. 객체에 대해 ACL 제어가 필요하지 않은 경우 업로드 시 설정하지 마십시오. 기본으로 버킷 권한은 계승됩니다.

#### 방식 프로토타입

```go
func (s *ObjectService) Put(ctx context.Context, key string, r io.Reader, opt *ObjectPutOptions) (*Response, error)
```

#### 요청 예시

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

#### 매개변수 설명

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
	// 사용자 지정 x-cos-meta-* header
	XCosMetaXXX        *http.Header
	XCosStorageClass   string      
}
```

| 매개변수 이름             | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| -------------------- | ------------------------------------------------------------ | ----------- | ---- |
| r                    | 업로드 파일의 콘텐츠, 파일 스트림이나 바이트 스트림이 될 수 있습니다. r이 bytes.Buffer/bytes.Reader/strings.Reader가 아닐 경우, opt.ObjectPutHeaderOptions.ContentLength를 지정해야 합니다 | io.Reader   | 예   |
| key                  | 객체 키(Key)이며, 버킷에서 객체의 유일한 식별자입니다. 예를 들어, 객체의 액세스 도메인 이름 ` bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg ` 중, 객체 키는 doc1/pic1.jpg입니다 | string      | 예   |
| XCosACL              | 파일의 ACL 설정, 예: private, public-read, public-read-write    | string      | 아니요   |
| XCosGrantFullControl | 지정 계정에 파일에 대한 읽기/쓰기 권한을 부여합니다. 형식은 `id=" ",id=" "` 서브 계정에 권한을 부여해야 할 경우, 형식은 `id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"` 루트 계정에 권한을 부여해야 할 경우, 형식은 `id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"` 예: `id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"` | string      | 아니요   |
| XCosGrantRead        | 지정 계정에 파일에 대한 읽기 권한을 부여합니다. 형식은 `id=" ",id=" "` 서브 계정에 권한을 부여해야 할 경우, 형식은 `id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"` 루트 계정에 권한을 부여해야 할 경우, 형식은 `id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"` 예: `id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"` | string      | 아니요   |
| XCosGrantWrite       | 지정 계정에 파일에 대한 쓰기 권한을 부여합니다. 형식은 `id=" ",id=" "` 서브 계정에 권한을 부여해야 할 경우, 형식은 `id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"` 루트 계정에 권한을 부여해야 할 경우, 형식은 `id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"` 예: `id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"` | string | 아니요   |
| XCosStorageClass     | 파일의 스토리지 클래스를 설정하며, 가능한 값은 STANDARD, STANDARD_IA입니다. 기본값은 STANDARD   | string      | 아니요   |
| Expires              | Content-Expires를 설정합니다                                         | string      | 아니요   |
| CacheControl         | 캐시 정책, Cache-Control을 설정합니다                                 | string      | 아니요   |
| ContentType          | 콘텐츠 유형, Content-Type을 설정합니다                                  | string      | 아니요   |
| ContentDisposition   | 파일 이름, Content-Disposition을 설정합니다                           | string      | 아니요   |
| ContentEncoding      | 인코딩 형식, Content-Encoding을 설정합니다                              | string      | 아니요   |
| ContentLength        | 전송 길이 설정                                                 | string      | 아니요   |
| XCosMetaXXX          | 사용자 지정의 파일 메타 정보, x-cos-meta로 시작해야 하며, 그렇지 않으면 무시됩니다 | http.Header | 아니요   |

#### 반환 결과 설명

```go
{
    'ETag': 'string',
    'x-cos-expiration': 'string'
}
```

| 매개변수 이름 | 매개변수 설명 | 유형 |
| ---------------- | -------------------------------- | ------ |
| ETag             | 업로드 파일의 MD5 값                | string |
| x-cos-expiration | 수명 주기 설정 후, 파일 만료 시간 규칙을 반환합니다 | string |

### 객체 획득

#### 기능 설명

지정 버킷의 파일을 로컬로 다운로드합니다.

#### 방식 프로토타입

```go
func (s *ObjectService) Get(ctx context.Context, key string, opt *ObjectGetOptions) (*Response, error)
```

#### 요청 예시

```go
	key := "test/hello.txt"
	opt := &cos.ObjectGetOptions{
		ResponseContentType: "text/html",
		Range:               "bytes=0-3",
	}
	//opt 선택 가능, 특별히 설정하지 않으면 nil입니다
	resp, err = client.Object.Get(context.Background(), key, opt)
	bs, _ = ioutil.ReadAll(resp.Body)
	resp.Body.Close()
	fmt.Printf("%s\n", string(bs))
```

#### 매개변수 설명

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

| 매개변수 이름             | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| -------------------------- | ------------------------------------------------------------ | ------ | ---- |
| key                        | 객체 키(Key)이며, 버킷에서 객체의 유일한 식별자입니다. 예를 들어, 객체의 액세스 도메인 이름 ` bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg ` 중, 객체 키는 doc1/pic1.jpg입니다 | string | 예   |
| ResponseContentType        | 응답 헤더, Content-Type을 설정합니다                                  | string      | 아니요   |
| ResponseContentLanguage    | 응답 헤더 Content-Language를 설정합니다                                | string | 아니요   |
| ResponseExpires            | 응답 헤더 Content-Expires를 설정합니다                                 | string | 아니요   |
| ResponseCacheControl       | 응답 헤더 Cache-Control을 설정합니다                                   | string | 아니요   |
| ResponseContentDisposition | 응답 헤더 Content-Disposition을 설정합니다                             | string | 아니요   |
| ResponseContentEncoding    | 응답 헤더 Content-Encoding을 설정합니다                                | string | 아니요   |
| Range                      | 다운로드할 파일의 범위를 설정하며, 형식은 bytes=first-last입니다                  | string | 아니요   |
| IfModifiedSince            | 지정된 시간 이후에 수정되면 반환됩니다                                     | string | 아니요   |

#### 반환 결과 설명

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

| 매개변수 이름 | 매개변수 설명 | 유형 |
| ---------- | ------------------------------------------------------------ | ---------- |
| Body       | 다운로드 파일의 콘텐츠                                               | StreamBody |
| 파일 메타 정보 | 다운로드 파일의 메타 정보, Etag 및 X-Cos-Request-Id 등의 정보가 포함되며, 설정된 파일 메타 정보도 반환할 수 있습니다 | string     |

### 단일 객체 삭제

#### 기능 설명

버킷의 해당 파일을 삭제합니다.

#### 방식 프로토타입

```go
func (s *ObjectService) Delete(ctx context.Context, key string) (*Response, error)
```

#### 요청 예시

```go
key := "test/objectPut.go"
resp, err := client.Object.Delete(context.Background(), name)
```

#### 매개변수 설명

| 매개변수 이름             | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| -------- | ------------------------------------------------------------ | ------ | ---- |
| key      | 객체 키(Key)이며, 버킷에서 객체의 유일한 식별자입니다. 예를 들어, 객체의 액세스 도메인 이름 ` bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg ` 중, 객체 키는 doc1/pic1.jpg입니다 | string | 예   |

### 여러 객체 삭제

#### 기능 설명

지정 버킷의 파일을 일괄 삭제합니다.

#### 방식 프로토타입

```go
func (s *ObjectService) DeleteMulti(ctx context.Context, opt *ObjectDeleteMultiOptions) (*ObjectDeleteMultiResult, *Response, error)
```

#### 요청 예시

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

#### 매개변수 설명

```go
type ObjectDeleteMultiOptions struct {
	Quiet   bool     
	Objects []Object
}
type Object struct {
	Key		string
}
```

| 매개변수 이름             | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| -------- | ------------------------------------------------------------ | ------ | ---- |
| Objects  | 삭제할 각 목표 객체의 정보를 설명합니다                           | List   | 예   |
| Key                  | 객체 키(Key)이며, 버킷에서 객체의 유일한 식별자입니다. 예를 들어, 객체의 액세스 도메인 이름 ` bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg ` 중, 객체 키는 doc1/pic1.jpg입니다 | string      | 아니요   |
| Quiet    | 삭제의 결과 반환 방식을 표시하며, 선택 가능 값은 true, false이고, 기본 설정은 false입니다. true로 설정하면 실패의 오류 정보만 반환하며, false로 설정하면 성공과 실패의 모든 정보를 반환합니다. | bool   | 아니요   |

#### 반환 결과 설명

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

| 매개변수 이름 | 매개변수 설명 | 유형 |
| -------------- | -------------------------------- | -------- |
| DeletedObjects | 삭제 성공한 객체 정보           | []struct |
| Errors         | 삭제 실패한 객체 정보           | string   |
| Key            | 삭제 실패한 객체 경로         | string   |
| Code           | 삭제 실패한 객체의 해당 오류 코드   | string   |
| Message        | 삭제 실패한 객체의 해당 오류 정보 | string   |

### 객체 메타데이터 획득

#### 기능 설명

지정 파일의 메타 정보를 획득합니다.

#### 방식 프로토타입

```go
func (s *ObjectService) Head(ctx context.Context, key string, opt *ObjectHeadOptions) (*Response, error)
```

#### 요청 예시

```go
key := "test/hello.txt"
resp, err := client.Object.Head(context.Background(), key, nil)
```

#### 매개변수 설명

```go
type ObjectHeadOptions struct {
	IfModifiedSince string
}
```

| 매개변수 이름             | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| --------------- | ------------------------------------------------------------ | ------ | ---- |
| key             | 객체 키(Key)이며, 버킷에서 객체의 유일한 식별자입니다. 예를 들어, 객체의 액세스 도메인 이름 ` bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg ` 중, 객체 키는 doc1/pic1.jpg입니다 | string | 예   |
| IfModifiedSince | 지정된 시간 이후에 수정되면 반환됩니다                                     | string | 아니요   |

#### 반환 결과 설명

```go
{
    'Content-Type': 'application/octet-stream',
    'Content-Length': '16807',
    'ETag': '"9a4802d5c99dafe1c04da0a8e7e166bf"',
    'Last-Modified': 'Wed, 28 Oct 2014 20:30:00 GMT',
    'X-Cos-Request-Id': 'NTg3NzQ3ZmVfYmRjMzVfMzE5N182NzczMQ=='
}
```

| 매개변수 이름 | 매개변수 설명 | 유형 |
| ---------- | ------------------------------------------------------------ | ------ |
| 파일 메타 정보 | 파일의 메타 정보를 획득합니다. Etag 및 X-Cos-Request-Id 등의 정보가 포함되며, 설정된 파일 메타 정보도 포함됩니다 | string     |

### 멀티파트 업로드 초기화

#### 기능 설명

새로운 멀티파트 업로드 태스크를 만들고, UploadId를 반환합니다.

#### 방식 프로토타입

```go
func (s *ObjectService) InitiateMultipartUpload(ctx context.Context, name string, opt *InitiateMultipartUploadOptions) (*InitiateMultipartUploadResult, *Response, error)
```

#### 요청 예시

```go
name := "test_multipart"
//opt 선택 가능
v, resp, err := client.Object.InitiateMultipartUpload(context.Background(), name, nil）
```

#### 매개변수 설명

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
	// 사용자 지정 x-cos-meta-* header
	XCosMetaXXX        *http.Header
	XCosStorageClass   string      
}
```

| 매개변수 이름             | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| -------------------- | ------------------------------------------------------------ | ----------- | ---- |
| r                    | 업로드 파일의 콘텐츠, 파일 스트림이나 바이트 스트림이 될 수 있습니다. r이 bytes.Buffer/bytes.Reader/strings.Reader가 아닐 경우, opt.ObjectPutHeaderOptions.ContentLength를 지정해야 합니다 | io.Reader   | 예   |
| key                  | 객체 키(Key)이며, 버킷에서 객체의 유일한 식별자입니다. 예를 들어, 객체의 액세스 도메인 이름 ` bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg ` 중, 객체 키는 doc1/pic1.jpg입니다 | string      | 예   |
| XCosACL              | 파일의 ACL 설정, 예: private, public-read, public-read-write    | string      | 아니요   |
| XCosGrantFullControl | 지정 계정에 파일에 대한 읽기/쓰기 권한을 부여합니다. 형식은 `id=" ",id=" "` 서브 계정에 권한을 부여해야 할 경우, 형식은 `id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"` 루트 계정에 권한을 부여해야 할 경우, 형식은 `id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"` 예: `id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"` | string      | 아니요   |
| XCosGrantRead        | 지정 계정에 파일에 대한 읽기 권한을 부여합니다. 형식은 `id=" ",id=" "` 서브 계정에 권한을 부여해야 할 경우, 형식은 `id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"` 루트 계정에 권한을 부여해야 할 경우, 형식은 `id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"` 예: `id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"` | string      | 아니요   |
| XCosGrantWrite       | 지정 계정에 파일에 대한 쓰기 권한을 부여합니다. 형식은 `id=" ",id=" "` 서브 계정에 권한을 부여해야 할 경우, 형식은 `id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"` 루트 계정에 권한을 부여해야 할 경우, 형식은 `id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"` 예: `id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"` | string | 아니요   |
| XCosStorageClass     | 파일의 스토리지 클래스를 설정하며, 가능한 값은 STANDARD, STANDARD_IA입니다. 기본값은 STANDARD   | string      | 아니요   |
| Expires              | Content-Expires를 설정합니다                                         | string      | 아니요   |
| CacheControl         | 캐시 정책, Cache-Control을 설정합니다                                 | string      | 아니요   |
| ContentType          | 콘텐츠 유형, Content-Type을 설정합니다                                  | string      | 아니요   |
| ContentDisposition   | 파일 이름, Content-Disposition을 설정합니다                           | string      | 아니요   |
| ContentEncoding      | 인코딩 형식, Content-Encoding을 설정합니다                              | string      | 아니요   |
| ContentLength        | 전송 길이 설정                                                 | string      | 아니요   |
| XCosMetaXXX          | 사용자 지정의 파일 메타 정보, x-cos-meta로 시작해야 하며, 그렇지 않으면 무시됩니다 | http.Header | 아니요   |

#### 반환 결과 설명

```go
type InitiateMultipartUploadResult struct {
	Bucket   string
	Key      string
	UploadID string                   
}
```

| 매개변수 이름 | 매개변수 설명 | 유형 |
| -------- | ------------------------------------------------------------ | ------ |
| UploadId | 멀티파트 업로드의 ID 표시                                            | string |
| Bucket             | 버킷 이름, bucket-appid으로 구성                        | string   |
| Key      | 객체 키(Key)이며, 버킷에서 객체의 유일한 식별자입니다. 예를 들어, 객체의 액세스 도메인 이름 ` bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg ` 중, 객체 키는 doc1/pic1.jpg입니다 | string |

### 멀티파트 업로드 정지

#### 기능 설명

멀티파트 업로드 태스크를 취소하고, 이미 업로드된 파트를 삭제합니다.

#### 방식 프로토타입

```go
func (s *ObjectService) AbortMultipartUpload(ctx context.Context, key, uploadID string) (*Response, error)
```

#### 요청 예시

```go
key := "test_multipart.txt"
v, _, err := client.Object.InitiateMultipartUpload(context.Background(), key, nil)
// Abort
resp, err := client.Object.AbortMultipartUpload(context.Background(), key, v.UploadID)
```

#### 매개변수 설명

| 매개변수 이름             | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| -------- | ------------------------------------------------------------ | ------ | ---- |
| key      | 객체 키(Key)이며, 버킷에서 객체의 유일한 식별자입니다. 예를 들어, 객체의 액세스 도메인 이름 ` bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg ` 중, 객체 키는 doc1/pic1.jpg입니다 | string | 예   |
| UploadId | 멀티파트 업로드의 ID 표시                                            | string | 예   |

### 파트 업로드

#### 기능 설명

하나의 파트를 지정된 UploadId에 업로드하며, 단일 파트 크기는 5GB를 초과할 수 없습니다.

#### 방식 프로토타입

```go
func (s *ObjectService) UploadPart(ctx context.Context, key, uploadID string, partNumber int, r io.Reader, opt *ObjectUploadPartOptions) (*Response, error)
```

#### 요청 예시

```go
// 주의: 멀티파트 업로드의 최대 파트 수량은 10000입니다
key := "test/test_multi_upload.go"
f := strings.NewReader("test heoo")
// opt 선택 가능
_, err := client.Object.UploadPart(
    context.Background(), key, uploadID, 1, f, nil,
)
```

#### 매개변수 설명

```go
type ObjectUploadPartOptions struct {
    ContentLength   int                                      
}
```

| 매개변수 이름             | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| ------------- | ------------------------------------------------------------ | --------- | ---- |
| key           | 객체 키(Key)이며, 버킷에서 객체의 유일한 식별자입니다. 예를 들어, 객체의 액세스 도메인 이름 ` bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg ` 중, 객체 키는 doc1/pic1.jpg입니다 | string    | 예   |
| UploadId      | 멀티파트 업로드의 ID 표시, InitiateMultipartUpload에서 생성합니다                                            | string | 예   |
| PartNumber    | 멀티파트 업로드의 번호 표시                                           | int       | 예   |
| r                    | 멀티파트 업로드의 콘텐츠, 로컬 파일 스트림이나 바이트 스트림이 될 수 있습니다. r이 bytes.Buffer/bytes.Reader/strings.Reader가 아닐 경우, opt.ContentLength를 지정해야 합니다 | io.Reader   | 예   |
| ContentLength | 전송 길이 설정                                                 | int       | 아니요   |

#### 반환 결과 설명

```go
{
    'ETag': 'string'
}
```

| 매개변수 이름 | 매개변수 설명 | 유형 |
| -------- | ------------------- | ------ |
| ETag             | 업로드된 파트의 MD5 값                | string |

### 파트 나열

#### 기능 설명

지정 UploadId에 이미 업로드된 파트의 정보를 나열합니다.

#### 방식 프로토타입

```go
func (s *ObjectService) ListParts(ctx context.Context, name, uploadID string) (*ObjectListPartsResult, *Response, error)
```

#### 요청 예시

```go
key := "test/test_list_parts.go"
v, resp, err := client.Object.ListParts(context.Background(), key, uploadID)
```

#### 매개변수 설명

| 매개변수 이름             | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| -------- | ------------------------------------------------------------ | ------ | ---- |
| key      | 객체 키(Key)이며, 버킷에서 객체의 유일한 식별자입니다. 예를 들어, 객체의 액세스 도메인 이름 ` bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg ` 중, 객체 키는 doc1/pic1.jpg입니다 | string | 예   |
| UploadId | 멀티파트 업로드의 ID 표시, InitiateMultipartUpload에서 생성합니다             | string | 예   |

#### 반환 결과 설명

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

| 매개변수 이름 | 매개변수 설명 | 유형 |
| -------------------- | ------------------------------------------------------------ | ------ |
| Bucket               | 버킷 이름, bucketname-appid으로 구성                        | string |
| EncodingType         | 기본으로 인코딩하지 않음, 반환값의 인코딩 방식을 지정합니다. 선택 가능값: url                | String |
| Key                  | 객체 키(Key)이며, 버킷에서 객체의 유일한 식별자입니다. 예를 들어, 객체의 액세스 도메인 이름 ` bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg ` 중, 객체 키는 doc1/pic1.jpg입니다 | string |
| UploadId             | 멀티파트 업로드의 ID 표시, InitiateMultipartUpload에서 생성합니다                                            | string |
| Initiator            | 멀티파트 업로드의 생성자, DisplayName, UIN 및 ID가 포함됩니다                | struct |
| Owner             | 파일 소유자의 정보, DisplayName, UIN 및 ID가 포함됩니다                  | struct |
| StorageClass         | 파일의 스토리지 클래스이며, STANDARD, STANDARD_IA가 포함됩니다. 기본값은 STANDARD   | string      |
| PartNumberMarker     | PartNumberMarker의 다음 파트부터 나열하기 시작함을 표시합니다. 기본값은 0이고, 첫번째 파트부터 나열을 의미합니다. | int    |
| NextPartNumberMarker | 다음 나열될 멀티파트의 시작 위치를 표시합니다 | int    |
| MaxParts             | 파트의 최대 반환 수량, 기본값은 최대 1000                   | int    |
| IsTruncated          | 반환된 멀티파트가 잘렸는지를 표시합니다                                  | bool     |
| Part                 | 업로드된 파트 관련 정보, ETag, PartNumber, Size, LastModified 등이 포함됩니다 | struct |

### 멀티파트 업로드 완료

#### 기능 설명

지정된 UploadId의 모든 파트를 한 개의 파일로 모읍니다. 파일의 최종 크기는 1MB보다 커야 하며 그렇지 않으면 오류가 반환됩니다.

#### 방식 프로토타입

```go
func (s *ObjectService) CompleteMultipartUpload(ctx context.Context, key, uploadID string, opt *CompleteMultipartUploadOptions) (*CompleteMultipartUploadResult, *Response, error)
```

#### 요청 예시

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

#### 매개변수 설명

```go
type CompleteMultipartUploadOptions struct {
	Parts   []Object
}
type Object struct {
	ETag         string
	PartNumber   int     
}
```

| 매개변수 이름             | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| ------------------------------ | ------------------------------------------------------------ | ------ | ---- |
| key                            | 객체 키(Key)이며, 버킷에서 객체의 유일한 식별자입니다. 예를 들어, 객체의 액세스 도메인 이름 ` bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg ` 중, 객체 키는 doc1/pic1.jpg입니다 | string | 예   |
| UploadId                       | 멀티파트 업로드의 ID 표시, InitiateMultipartUpload에서 생성합니다             | string | 예   |
| CompleteMultipartUploadOptions | 모든 파트의 ETag 및 PartNumber 정보                           | struct | 예   |

#### 반환 결과 설명

```go
type CompleteMultipartUploadResult struct {
	Location string
	Bucket   string
	Key      string
	ETag     string
}
```

| 매개변수 이름 | 매개변수 설명 | 유형 |
| -------- | ------------------------------------------------------------ | ------ |
| Location | URL 주소                                                     | string |
| Bucket   | 버킷 이름, bucketname-appid으로 구성                        | string |
| Key      | 객체 키(Key)이며, 버킷에서 객체의 유일한 식별자입니다. 예를 들어, 객체의 액세스 도메인 이름 ` bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg ` 중, 객체 키는 doc1/pic1.jpg입니다 | string |
| ETag     | 병합 후 객체의 고유한 태그 값입니다. 해당 값은 객체 콘텐츠의 MD5 검증값이 아니며, 대상의 고유성을 검사하는 데만 사용할 수 있습니다. 파일 내용을 검사해야 할 경우, 업로드 과정에 단일 파트의 ETag 값을 검증할 수 있습니다. | string |

### 객체 ACL 설정

#### 기능 설명

파일의 ACL 정보를 설정하고, XCosACL, XCosGrantFullControl, XCosGrantRead, XCosGrantWrite를 통해 헤더를 입력하는 방식으로 ACL을 설정하거나 ACLXML을 통해 본문을 입력하여 ACL을 설정할 수 있습니다. 두 방식 중 하나만 선택할 수 있으며 그렇지 않으면 충돌이 반환됩니다.

> !현재 액세스 정책 항목은 1000으로 제한되어 있습니다. 객체에 대해 ACL 제어가 필요하지 않은 경우 설정하지 마십시오. 기본으로 버킷 권한은 계승됩니다.

#### 방식 프로토타입

```go
func (s *ObjectService) PutACL(ctx context.Context, key string, opt *ObjectPutACLOptions) (*Response, error)
```

#### 요청 예시

헤더를 통한 객체 ACL 설정

```go
opt := &cos.ObjectPutACLOptions{
    Header: &cos.ACLHeaderOptions{
        XCosACL: "private",
    },
}
key := "test/hello.txt"
resp, err := client.Object.PutACL(context.Background(), key, opt)
```

본문을 통한 객체 ACL 설정

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

#### 매개변수 설명

```go
type ACLHeaderOptions struct {
	XCosACL              string
	XCosGrantRead        string
	XCosGrantWrite       string
	XCosGrantFullControl string
}
```

| 매개변수 이름             | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| -------------------- | ------------------------------------------------------------ | ------ | ---- |
| key                  | 객체 키(Key)이며, 버킷에서 객체의 유일한 식별자입니다. 예를 들어, 객체의 액세스 도메인 이름 ` bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg ` 중, 객체 키는 doc1/pic1.jpg입니다 | string | 예   |
| XCosACL              | 버킷의 ACL 설정, 예: private, public-read, public-read-write | string | 아니요   |
| XCosGrantFullControl | 지정 계정에 버킷에 대한 읽기/쓰기 권한을 부여합니다. 형식은 `id=" ",id=" "` 서브 계정에 권한을 부여해야 할 경우, 형식은 `id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"` 루트 계정에 권한을 부여해야 할 경우, 형식은 `id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"` 예: `id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"` | string | 아니요   |
| XCosGrantRead        | 지정 계정에 버킷에 대한 읽기 권한을 부여합니다. 형식은 `id=" ",id=" "` 서브 계정에 권한을 부여해야 할 경우, 형식은 `id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"` 루트 계정에 권한을 부여해야 할 경우, 형식은 `id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"` 예: `id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"` | string | 아니요   |
| XCosGrantWrite       | 지정 계정에 버킷에 대한 쓰기 권한을 부여합니다. 형식은 `id=" ",id=" "` 서브 계정에 권한을 부여해야 할 경우, 형식은 `id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"` 루트 계정에 권한을 부여해야 할 경우, 형식은 `id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"` 예: `id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"` | string | 아니요   |
| ACLXML               | 지정 계정에 버킷에 대한 액세스 권한을 부여하며, 구체적인 형식은 get object acl 반환 결과 설명을 참조하십시오 | struct | 아니요   |

### 객체 ACL 획득

#### 기능 설명

지정 파일의 ACL 정보를 획득합니다.

#### 방식 프로토타입

```go
func (s *ObjectService) GetACL(ctx context.Context, key string) (*ObjectGetACLResult, *Response, error)
```

#### 요청 예시

```go
key := "test/hello.txt"
v, resp, err := client.Object.GetACL(context.Background(), key)
```

#### 매개변수 설명

| 매개변수 이름             | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| -------- | ------------------------------------------------------------ | ------ | ---- |
| key      | 객체 키(Key)이며, 버킷에서 객체의 유일한 식별자입니다. 예를 들어, 객체의 액세스 도메인 이름 ` bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg ` 중, 객체 키는 doc1/pic1.jpg입니다 | string | 예   |

#### 반환 결과 설명

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

| 매개변수 이름 | 매개변수 설명 | 유형 |
| ----------------- | ------------------------------------------------------------ | ------ |
| Owner             | 버킷 소유자의 정보, DisplayName 및 ID가 포함됩니다                  | struct |
| AccessControlList | 버킷 권한 부여자의 정보, Grantee 및 Permission이 포함됩니다           | struct |
| Grantee           | 권한 부여자의 정보, DisplayName, Type, ID 및 UIN이 포함됩니다          | struct |
| Type              | 권한 부여자의 종류, 유형은 CanonicalUser 또는 Group입니다            | string |
| ID                | 유형이 CanonicalUser일 경우, 해당 권한 부여자의 ID                | string |
| DisplayName       | 권한 부여자의 이름                                             | string |
| UIN               | 유형이 Group일 때, 해당 권한 부여자의 UIN                       | string |
| Permission        | 부여자가 소유한 버킷의 권한, 선택 가능 값은 FULL_CONTROL, WRITE, READ이며, 각각 읽기/쓰기 권한, 쓰기 권한, 읽기 권한에 대응합니다 | string |

### 객체 복사 설정

#### 기능 설명

소스 경로에서 대상 경로로 파일을 복사합니다. 파일 크기는 1M ~ 5G가 권장되며, 5G를 초과하는 파일의 경우 멀티파트 업로드(Upload-Copy)를 사용하십시오. 파일 메타 속성 및 ACL은 복사 과정에서 수정할 수 있습니다. 사용자는 이 API를 사용하여 파일 이동, 파일 이름 바꾸기, 파일 속성 수정 및 사본 생성 등을 할 수 있습니다.
>!계정 간 복사의 경우, 먼저 복사할 파일의 권한을 공개 읽기로 하거나 대상 계정에 대한 권한을 부여해야 합니다. 다만, 같은 계정일 경우는 권한 부여할 필요가 없습니다.

#### 방식 프로토타입

```go
func (s *ObjectService) Copy(ctx context.Context, key, sourceURL string, opt *ObjectCopyOptions) (*ObjectCopyResult, *Response, error)
```

#### 요청 예시

```go
u, _ := url.Parse("http://test-1253846586.cos.ap-guangzhou.myqcloud.com")
source := "test/objectMove_src"
soruceURL := fmt.Sprintf("%s/%s", u.Host, source)
dest := "test/objectMove_dest"
//opt := &cos.ObjectCopyOptions{}
r, resp, err := client.Object.Copy(context.Background(), dest, soruceURL, nil)
```

#### 매개변수 설명

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
	// 사용자 지정 x-cos-meta-* header
	XCosMetaXXX    				    *http.Header
	XCosCopySource 					string      
}
```

| 매개변수 이름             | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| ------------------------------- | ------------------------------------------------------------ | ----------- | ---- |
| key                             | 객체 키(Key)이며, 버킷에서 객체의 유일한 식별자입니다. 예를 들어, 객체의 액세스 도메인 이름 ` bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg ` 중, 객체 키는 doc1/pic1.jpg입니다 | string      | 예   |
| sourceURL                       | 복사할 소스 파일의 URL                                          | string      | 예   |
| XCosACL                         | 파일의 ACL 설정, 예: private, public-read, public-read-write    | string      | 아니요   |
| XCosGrantFullControl            | 지정 계정에 파일에 대한 읽기/쓰기 권한을 부여합니다. 형식은 `id=" ",id=" "` 서브 계정에 권한을 부여해야 할 경우, 형식은 `id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"` 루트 계정에 권한을 부여해야 할 경우, 형식은 `id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"` 예: `id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"` | string      | 아니요   |
| XCosGrantRead                   | 지정 계정에 파일에 대한 읽기 권한을 부여합니다. 형식은 `id=" ",id=" "` 서브 계정에 권한을 부여해야 할 경우, 형식은 `id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"` 루트 계정에 권한을 부여해야 할 경우, 형식은 `id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"` 예: `id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"` | string      | 아니요   |
| XCosGrantWrite                  | 지정 계정에 파일에 대한 쓰기 권한을 부여합니다. 형식은 `id=" ",id=" "` 서브 계정에 권한을 부여해야 할 경우, 형식은 `id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"` 루트 계정에 권한을 부여해야 할 경우, 형식은 `id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"` 예: `id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"` | string      | 아니요   |
| XCosMetadataDirective           | 선택 가능한 값은 Copy, Replaced입니다. Copy로 설정하면, 설정한 사용자의 메타데이터 정보를 무시하여 바로 복사합니다. Replaced로 설정하면, 설정한 메타 정보에 따라 메타 데이터를 수정합니다. 대상 경로가 소스 경로와 같으면 반드시 Replaced로 설정해야 합니다 | string      | 예   |
| XCosCopySourceIfModifiedSince   | 객체가 지정된 시간 이후 수정되면 조작이 실행되고 그렇지 않으면 412가 반환됩니다. XCosCopySourceIfNoneMatch와 함께 사용할 수 있으며, 다른 조건과 함께 사용하면 충돌이 반환됩니다. | string      | 아니요   |
| XCosCopySourceIfUnmodifiedSince | 객체가 지정된 시간 후에 수정되지 않으면 조작이 실행되고 그렇지 않으면 412가 반환됩니다. XCosCopySourceIfMatch와 함께 사용할 수 있으며, 다른 조건과 함께 사용하면 충돌이 반환됩니다. | string      | 아니요   |
| XCosCopySourceIfMatch           | 객체의 Etag가 지정한 것과 일치하면 조작을 실행하고 그렇지 않으면 412가 반환됩니다. XCosCopySourceIfUnmodifiedSince와 함께 사용할 수 있으며, 다른 조건과 함께 사용하면 충돌이 반환됩니다. | string      | 아니요   |
| XCosCopySourceIfNoneMatch       | 객체의 Etag가 지정한 것과 일치하지 않으면 조작을 실행하고 그렇지 않으면 412가 반환됩니다. XCosCopySourceIfModifiedSince와 함께 사용할 수 있으며, 다른 조건과 함께 사용하면 충돌이 반환됩니다. | string      | 아니요   |
| XCosStorageClass                | 파일의 스토리지 클래스를 설정하며, 가능한 값은 STANDARD, STANDARD_IA입니다. 기본값은 STANDARD   | string      | 아니요   |
| XCosMetaXXX                     | 사용자 지정의 파일 메타 정보                                       | http.Header | 아니요   |
| XCosCopySource                  | 소스 파일 URL 경로, versionid 하위 리소스를 통해 히스토리 버전을 지정할 수 있습니다       | string      | 아니요   |

#### 반환 결과 설명

업로드 파일의 속성:

```go
type ObjectCopyResult struct {
    ETag         string
    LastModified string
}
```

| 매개변수 이름 | 매개변수 설명 | 유형 |
| ------------ | -------------------------- | ------ |
| ETag             | 복사 파일의 MD5 값                | string |
| LastModified | 복사 파일의 마지막 수정 시간 | string |

## 비정상 설명

API가 반환한 응답은 Golang http 표준 라이브러리 [Response](https://golang.org/pkg/net/http/#Response) 유형입니다.
err.Error()를 통해 오류 메시지, 서버가 반환한 구체 정보를 획득할 수 있습니다. 오류 코드에 대한 더 자세한 정보는 [COS 오류 코드](https://cloud.tencent.com/document/product/436/7730)를 참조하십시오.
