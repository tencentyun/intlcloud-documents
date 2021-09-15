## 소개

본 문서에서는 버킷의 기본 작업에 대한 API 개요 및 SDK 예시 코드를 제공합니다.


| API                                                          | 작업명             | 작업 설명                           |
| ------------------------------------------------------------ | ------------------ | ---------------------------------- |
| [GET Service](https://intl.cloud.tencent.com/document/product/436/8291) |버킷 리스트 조회     | 지정 계정의 모든 버킷 리스트 조회   |
| [PUT Bucket](https://intl.cloud.tencent.com/document/product/436/7738) | 버킷 생성         | 지정 계정에서 버킷 생성         |
| [HEAD Bucket](https://intl.cloud.tencent.com/document/product/436/7735) | 버킷 및 해당 권한 인덱스 | 버킷 존재 여부 및 액세스 권한 보유 여부 인덱스 |
| [DELETE Bucket](https://intl.cloud.tencent.com/document/product/436/7732) | 버킷 삭제         | 지정 계정의 빈 버킷 삭제           |




## 버킷 리스트 조회

#### 기능 설명

지정 계정의 모든 버킷 리스트를 조회합니다.

#### 메소드 프로토타입

```go
func (s *ServiceService) Get(ctx context.Context) (*ServiceGetResult, *Response, error)
```

#### 요청 예시

[//]: # (.cssg-snippet-get-service)
```go
_, _, err := client.Service.Get(context.Background())
if err != nil {
    panic(err)
}
```


#### 반환 결과 설명

GetServiceResult를 통해 요청 결과 반환.

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

| 매개변수 이름     | 매개변수 설명                                                     | 유형   |
| ------------ | ------------------------------------------------------------ | ------ |
| ID           | Bucket 소유자의 ID                                           | string |
| DisplayName  | Bucket 소유자 이름 정보                                      | string |
| Name         | Bucket 이름                                                | string |
| Region       | Bucket 소재 리전                                              | string |
| CreationDate | Bucket 생성 시간. ISO8601 형식. 예시: 2016-11-09T08:46:32.000Z | string |

## 버킷 생성

#### 기능 설명

지정된 계정에 버킷을 생성합니다.

#### 메소드 프로토타입

```go
func (s *BucketService) Put(ctx context.Context, opt *BucketPutOptions) (*Response, error)
```

#### 요청 예시

[//]: # (.cssg-snippet-put-bucket)
```go
opt := &cos.BucketPutOptions{
    XCosACL: "private",
}
_, err := client.Bucket.Put(context.Background(), opt)
if err != nil {
    panic(err)
}


// MAZ 버킷 생성
opt.CreateBucketConfiguration = &cos.CreateBucketConfiguration{
    BucketAZConfig: "MAZ",
}
_, err := client.Bucket.Put(context.Background(), opt)
if err != nil {
    panic(err)
}

```

#### 매개변수 설명
```go
type BucketPutOptions struct {
	XCosACL              string 
	XCosGrantRead        string  
	XCosGrantWrite       string  
	XCosGrantFullControl string 
    CreateBucketConfiguration *CreateBucketConfiguration
}
type CreateBucketConfiguration struct {
    BucketAZConfig string
}
```

| 매개변수 이름             | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| -------------------- | ------------------------------------------------------------ | ------ | ---- |
| XCosACL              | Bucket의 ACL 설정. 예: private, public-read, public-read-write | string | 아니요   |
| XCosGrantFullControl | 지정 계정에 Bucket에 대한 읽기/쓰기 권한 부여. 형식: `id=" ",id=" "`, 서브 계정에 권한을 부여해야 하는 경우의 형식: `id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`, 루트 계정에 권한을 부여해야 하는 경우의 형식: `id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`. 예: `id="qcs::cam::uin/100000000001:uin/100000000011",id="qcs::cam::uin/100000000001:uin/100000000001"` | string | 아니요   |
| XCosGrantRead        | 지정 계정에 Bucket에 대한 읽기 권한 부여. 형식: `id=" ",id=" "`, 서브 계정에 권한을 부여해야 하는 경우의 형식: `id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`, 루트 계정에 권한을 부여해야 하는 경우의 형식: `id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`. 예: `id="qcs::cam::uin/100000000001:uin/100000000011",id="qcs::cam::uin/100000000001:uin/100000000001"` | string | 아니요   |
| XCosGrantWrite       | 지정 계정에 Bucket에 대한 쓰기 권한 부여. 형식: `id=" ",id=" "`, 서브 계정에 권한을 부여해야 하는 경우의 형식: `id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`, 루트 계정에 권한을 부여해야 하는 경우의 형식: `id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`. 예: `id="qcs::cam::uin/100000000001:uin/100000000011",id="qcs::cam::uin/100000000001:uin/100000000001"` | string | 아니요   |
| BucketAZConfig | 버킷 AZ 구성. MAZ로 지정하여 다중 AZ 버킷을 생성합니다. 다중 AZ 스토리지 유형은 현재 베이징 및 광저우 리전만 지원됩니다. | Struct  | 아니요 |

## 버킷 및 해당 권한 인덱스

#### 기능 설명

버킷의 존재 여부 및 액세스 권한 보유 여부를 인덱스합니다.

#### 메소드 프로토타입

```go
func (s *BucketService) Head(ctx context.Context) (*Response, error)
```

#### 요청 예시

[//]: # (.cssg-snippet-head-bucket)
```go
_, err := client.Bucket.Head(context.Background())
if err != nil {
    panic(err)
}
```


## 버킷 삭제

#### 기능 설명

지정 계정의 빈 버킷을 삭제합니다.

#### 메소드 프로토타입

```go
func (s *BucketService) Delete(ctx context.Context) (*Response, error)
```

#### 요청 예시

[//]: # (.cssg-snippet-delete-bucket)
```go
_, err := client.Bucket.Delete(context.Background())
if err != nil {
    panic(err)
}
```
