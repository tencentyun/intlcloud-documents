## 소개

본 문서는 버킷, 객체의 액세스 제어 리스트(ACL) 관련 API 개요 및 SDK 예시 코드를 제공합니다.


**버킷 ACL**

| API                                                          | 작업명         | 작업 설명                                |
| :----------------------------------------------------------- | :------------- | :-------------------------------------- |
| [PUT Bucket acl](https://intl.cloud.tencent.com/document/product/436/7737) | 버킷 ACL 설정 | 지정 버킷의 액세스 권한 제어 리스트(ACL) 설정 |
| [GET Bucket acl](https://intl.cloud.tencent.com/document/product/436/7733) |버킷 ACL 조회 | 지정 버킷의 액세스 권한 제어 리스트(ACL) 조회 |


**객체 ACL**

| API                                                          | 작업명       | 작업 설명                                      |
| ------------------------------------------------------------ | ------------ | --------------------------------------------- |
| [PUT Object acl](https://intl.cloud.tencent.com/document/product/436/7748) | 객체 ACL 설정 | Bucket의 특정 Object(파일/객체)의 ACL 설정 |
| [GET Object acl](https://intl.cloud.tencent.com/document/product/436/7744) | 객체 ACL 조회 | Object(파일/객체)의 ACL 조회                |


## 버킷 ACL

### 버킷 ACL 설정

#### 기능 설명

지정 버킷의 액세스 권한 제어 리스트를 설정합니다(PUT Bucket acl).

#### 방법 모델

```go
func (s *BucketService) PutACL(ctx context.Context, opt *BucketPutACLOptions) (*Response, error)
```

#### 요청 예시

[//]: # (.cssg-snippet-put-bucket-acl)
```go
// 1. 요청 헤더를 통해 Bucket ACL 설정
opt := &cos.BucketPutACLOptions{
    Header: &cos.ACLHeaderOptions{
        //private, public-read, public-read-write
        XCosACL: "private",
    },
}
_, err := client.Bucket.PutACL(context.Background(), opt)
if err != nil {
    panic(err)
}

// 2. 요청 본문을 통해 Bucket ACL 설정
opt = &cos.BucketPutACLOptions{
    Body: &cos.ACLXml{
        Owner: &cos.Owner{
            ID: "qcs::cam::uin/100000000001:uin/100000000001",
        },
        AccessControlList: []cos.ACLGrant{
            {
                Grantee: &cos.ACLGrantee{
                    // Type의 옵션: "Group", "CanonicalUser"
                    Type: "RootAccount",
                    ID:   "qcs::cam::uin/100000760461:uin/100000760461",
                },
                // Permission의 옵션: "WRITE", "FULL_CONTROL"
                Permission: "FULL_CONTROL",
            },
        },
    },
}
_, err = client.Bucket.PutACL(context.Background(), opt)
if err != nil {
    panic(err)
}
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
| XCosACL              | Bucket의 ACL 설정. 예: private, public-read, public-read-write | string | 아니요   |
| XCosGrantFullControl | 지정 계정에 Bucket에 대한 읽기/쓰기 권한 부여. 포맷: `id=" ",id=" "`, 서브 계정에 권한을 부여해야 하는 경우의 포맷: `id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`, 루트 계정에 권한을 부여해야 하는 경우의 포맷: `id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`. 예: `id="qcs::cam::uin/100000000001:uin/100000000011",id="qcs::cam::uin/100000000001:uin/100000000001"` | string | 아니요   |
| XCosGrantRead        | 지정 계정에 Bucket에 대한 읽기 권한 부여. 포맷: `id=" ",id=" "`, 서브 계정에 권한을 부여해야 하는 경우의 포맷: `id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`, 루트 계정에 권한을 부여해야 하는 경우의 포맷: `id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`. 예: `id="qcs::cam::uin/100000000001:uin/100000000011",id="qcs::cam::uin/100000000001:uin/100000000001"` | string | 아니요   |
| XCosGrantWrite       | 지정 계정에 Bucket에 대한 쓰기 권한 부여. 포맷: `id=" ",id=" "`, 서브 계정에 권한을 부여해야 하는 경우의 포맷: `id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`, 루트 계정에 권한을 부여해야 하는 경우의 포맷: `id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`. 예: `id="qcs::cam::uin/100000000001:uin/100000000011",id="qcs::cam::uin/100000000001:uin/100000000001"` | string | 아니요   |
| ACLXML               | 지정 계정에 Bucket에 대한 액세스 권한 부여. 자세한 포맷은 GET Bucket acl 반환 결과 설명 참조 | struct | 아니요   |

### 버킷 ACL 조회

#### 기능 설명

지정 버킷의 액세스 권한 제어 리스트를 조회합니다(GET Bucket acl).

#### 방법 모델

```go
func (s *BucketService) GetACL(ctx context.Context) (*BucketGetACLResult, *Response, error)
```

#### 요청 예시

[//]: # (.cssg-snippet-get-bucket-acl)
```go
_, _, err := client.Bucket.GetACL(context.Background())
if err != nil {
    panic(err)
}
```

#### 반환 결과 설명

GetBucketACLResult를 통해 요청 결과를 반환합니다.

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

| 매개변수 이름          | 매개변수 설명                                                     | 유형   |
| ----------------- | ------------------------------------------------------------ | ------ |
| Owner             | DisplayName, ID를 포함한 Bucket 소유자 정보                  | struct |
| AccessControlList | Grantee, Permission을 포함한 Bucket 권한 부여자 정보           | struct |
| Grantee           | DisplayName, Type, ID, UIN을 포함한 권한 부여자 정보          | struct |
| Type              | 권한 부여자 유형. CanonicalUser 또는 Group            | string |
| ID                | Type이 CanonicalUser인 경우 해당 권한 부여자의 ID                | string |
| DisplayName       | 권한 부여자의 이름                                             | string |
| UIN               | Type이 Group인 경우 해당 권한 부여자의 UIN                       | string |
| Permission        | 부여자가 가지고 있는 Bucket의 권한. 옵션값: FULL_CONTROL(읽기/쓰기 권한), WRITE(쓰기 권한), READ(읽기 권한) | string |



## 객체 ACL

### 객체 ACL 설정

#### 기능 설명

객체의 액세스 권한 제어 리스트를 설정합니다(PUT Object acl).

#### 방법 모델

```go
func (s *ObjectService) PutACL(ctx context.Context, key string, opt *ObjectPutACLOptions) (*Response, error)
```

#### 요청 예시

[//]: # (.cssg-snippet-put-object-acl)
```go
// 1. 요청 헤더를 통해 설정
opt := &cos.ObjectPutACLOptions{
    Header: &cos.ACLHeaderOptions{
        XCosACL: "private",
    },
}
key := "exampleobject"
_, err := client.Object.PutACL(context.Background(), key, opt)
if err != nil {
    panic(err)
}
// 2. 요청 본문을 통해 설정
opt = &cos.ObjectPutACLOptions{
    Body: &cos.ACLXml{
        Owner: &cos.Owner{
            ID: "qcs::cam::uin/100000000001:uin/100000000001",
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

_, err = client.Object.PutACL(context.Background(), key, opt)
if err != nil {
    panic(err)
}
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
| key                  | 객체 키(Key)는 객체의 버킷 내 고유 식별자. 예: 객체의 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`에서 객체 키는 doc/pic.jpg임 | string | 예   |
| XCosACL              | Object의 ACL 설정. 예: private, public-read                  | string | 아니요   |
| XCosGrantFullControl | 권한을 부여받은 계정에 모든 권한 부여. 포맷: id="[OwnerUin]"                | string | 아니요   |
| XCosGrantRead        | 권한을 부여받은 계정에 읽기 권한 부여. 포맷: id="[OwnerUin]"                  | string | 아니요   |
| ACLXML               | 지정 계정에 Bucket 액세스 권한 부여. 자세한 포맷은 get object acl 반환 결과 설명 참조 | struct | 아니요   |

### 객체 ACL 조회

#### 기능 설명

Object(파일/객체)의 ACL을 조회합니다(GET Object acl).

#### 방법 모델

```go
func (s *ObjectService) GetACL(ctx context.Context, key string) (*ObjectGetACLResult, *Response, error)
```

#### 요청 예시

[//]: # (.cssg-snippet-get-object-acl)
```go
key := "exampleobject"
_, _, err := client.Object.GetACL(context.Background(), key)
if err != nil {
    panic(err)
}
```

#### 매개변수 설명

| 매개변수 이름 | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| -------- | ------------------------------------------------------------ | ------ | ---- |
| key      | 객체 키(Key)는 객체의 버킷 내 고유 식별자. 예: 객체의 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`에서 객체 키는 doc/pic.jpg임 | string | 예   |

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

| 매개변수 이름          | 매개변수 설명                                                     | 유형   |
| ----------------- | ------------------------------------------------------------ | ------ |
| Owner             | DisplayName, ID를 포함한 Bucket 소유자 정보                  | struct |
| AccessControlList | Grantee, Permission을 포함한 Bucket 권한 부여자 정보          | struct |
| Grantee           | DisplayName, Type, ID, UIN을 포함한 권한 부여자 정보          | struct |
| Type              | 권한 부여자 유형. CanonicalUser 또는 Group            | string |
| ID                | Type이 CanonicalUser인 경우 해당 권한 부여자의 ID                | string |
| DisplayName       | 권한 부여자의 이름                                             | string |
| UIN               | Type이 Group인 경우 해당 권한 부여자의 UIN                       | string |
| Permission        | 부여자가 가지고 있는 Bucket의 권한. 옵션값: FULL_CONTROL(읽기/쓰기 권한), WRITE(쓰기 권한), READ(읽기 권한) | string |
