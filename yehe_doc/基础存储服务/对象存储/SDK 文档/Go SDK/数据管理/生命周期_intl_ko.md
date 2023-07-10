## 소개

본 문서는 라이프사이클에 대한 API 개요 및 SDK 예시 코드를 제공합니다.

| API                                                          | 작업 이름       | 작업 설명                     |
| ------------------------------------------------------------ | ------------ | ------------------------------ |
| [PUT Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8280) | 라이프사이클 설정 | 버킷의 라이프사이클 관리 구성 설정 |
| [GET Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8278) | 라이프사이클 쿼리| 버킷 라이프사이클 관리 설정 쿼리   |
| [DELETE Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8284) | 라이프사이클 삭제 | 버킷 라이프사이클 관리 구성 삭제   |

## 라이프사이클 설정

#### 기능 설명

지정된 버킷의 라이프사이클 구성 정보 설정(PUT Bucket lifecycle).

#### 메소드 프로토타입
```go
func (s *BucketService) PutLifecycle(ctx context.Context, opt *BucketPutLifecycleOptions) (*Response, error)
```

#### 요청 예시
[//]: # (.cssg-snippet-put-bucket-lifecycle)
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
_, err := client.Bucket.PutLifecycle(context.Background(), lc)
if err != nil {
    panic(err)
}
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
	Days    int    
}
type BucketLifecycleAbortIncompleteMultipartUpload struct {
	DaysAfterInitiation string 
}
```

| 매개변수 이름                       | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| ------------------------------ | ------------------------------------------------------------ | ------ | ---- |
| BucketLifecycleRule            | ID, Filter, Status, Expiration, Transition, AbortIncompleteMultipartUpload를 포함한 규칙 설정. | List   | Yes   |
| ID                             | 규칙 ID 설정. 라이프 사이클 규칙의 고유 식별자.   | String | No   |
| Status                         | Rule 활성화 여부 설정, 선택 옵션: Enabled 또는 Disabled           | String | Yes   |
| Filter                         | 규칙의 영향을 받는 Object 배열 설명.  Bucket에 있는 모든 objects를 설정하려면 Prefix를 비워두십시오. | Struct | Yes   |
| Transition                     | Object 스토리지 유형 전환 규칙 설정. Days 및 Date 지정 가능. Date의 형식은 GMT ISO 8601이어야 합니다. StorageClass는 Standard_IA, Archive 선택 가능. 복수 규칙 동시 설정 가능. | Struct | No   |
| Expiration                     | Object 만료 규칙 설정. Days 및 Date 지정 가능. Date의 형식은 GMT ISO 8601이어야 합니다. | Struct | No   |
| AbortIncompleteMultipartUpload | 멀티파트 업로드 완료 기한 지정                       | Struct | No   |

## 라이프사이클 쿼리

#### 기능 설명

버킷의 라이프사이클 관리 설정을 쿼리합니다(GET Bucket lifecycle).

#### 메소드 프로토타입
```go
func (s *BucketService) GetLifecycle(ctx context.Context) (*BucketGetLifecycleResult, *Response, error)
```

#### 요청 예시

[//]: # (.cssg-snippet-get-bucket-lifecycle)
```go
_, _, err := client.Bucket.GetLifecycle(context.Background())
if err != nil {
    panic(err)
}
```

#### 반환 결과 설명

GetBucketLifecycleResult를 통해 요청 결과를 반환합니다.

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
	Days    int    
}
type BucketLifecycleAbortIncompleteMultipartUpload struct {
	DaysAfterInitiation string 
}
```

| 매개변수 이름                       | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| ------------------------------ | ------------------------------------------------------------ | ------ | ---- |
| BucketLifecycleRule            | ID, Filter, Status, Expiration, Transition, AbortIncompleteMultipartUpload를 포함한 해당 규칙 설정 | List   | Yes   |
| ID                             | 규칙의 고유 ID                                                | String | No   |
| Status                         | Rule 활성화 여부 설정, 선택 옵션: Enabled 또는 Disabled           | String | Yes   |
| Filter                         | 규칙의 영향을 받는 Object 배열을 설명하는 데 사용됩니다.  Bucket에 있는 모든 objects를 설정하려면 Prefix를 비워두십시오. | Struct | Yes   |
| Transition                     | Object 스토리지 유형 전환 규칙 설정. Days 및 Date를 지정할 수 있습니다. Date의 형식은 GMT ISO 8601이어야 합니다. StorageClass는 Standard_IA, Archive 선택 가능. 복수 규칙 동시 설정 가능. | Struct | No   |
| Expiration                     | Object 만료 규칙 설정. Days 및 Date를 지정할 수 있습니다. Date 의 형식은 GMT ISO 8601이어야 합니다. | Struct | No   |
| AbortIncompleteMultipartUpload | 멀티파트 업로드 완료 기한 지정                       | Struct | No   |


## 라이프사이클 삭제

#### 기능 설명

버킷의 라이프사이클 관리 구성을 삭제합니다(DELETE Bucket lifecycle).

#### 메소드 프로토타입

```go
func (s *BucketService) DeleteLifecycle(ctx context.Context) (*Response, error)
```

#### 요청 예시

[//]: # (.cssg-snippet-delete-bucket-lifecycle)
```go
_, err := client.Bucket.DeleteLifecycle(context.Background())
if err != nil {
    panic(err)
}
```
