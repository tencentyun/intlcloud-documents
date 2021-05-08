## 소개

본 문서는 버전 제어에 대한 API 개요 및 SDK 예시 코드를 제공합니다.

| API                                                          | 작업명       | 작업 설명                 |
| ------------------------------------------------------------ | ------------ | ------------------------ |
| [PUT Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19889) | 버전 제어 설정 | 버킷의 버전 제어 기능 설정 |
| [GET Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19888) | 버전 제어 확인 | 버킷의 버전 제어 정보 조회 |

## 버전 제어 설정

#### 기능 설명

특정 버킷의 버전 제어 기능(PUT Bucket versioning)을 설정합니다.

#### 방법 모델
```go
func (s *BucketService) PutVersioning(ctx context.Context, opt *BucketPutVersionOptions) (*Response, error)
```

#### 요청 예시
[//]: # ".cssg-snippet-put-bucket-versioning"
```go
opt := &cos.BucketPutVersionOptions{
    // Enabled 또는 Suspended. 버전 제어 설정은 일단 활성화되면 제거할 수 없으며, 일시 중지만 가능
    Status: "Enabled",
}
_, err := client.Bucket.PutVersioning(context.Background(), opt)
if err != nil {
    panic(err)
}
```

#### 매개변수 설명
```go
type BucketPutVersionOptions struct {
	Status  string
}
```
| 매개변수 이름| 설명  | 유형  |
| ----| ---- | ---- |
| BucketPutVersionOptions | 버전 제어 정책  | struct |
| Status | 버전 제어가 활성화되어 있는지 설명. 열거 값: Suspended(버전 제어 일시 중지), Enabled(버전 제어 활성화)  | string |

## 버전 제어 조회

#### 기능 설명

특정 버킷의 버전 제어 정보(GET Bucket versioning)를 조회합니다.

#### 방법 모델
```go
func (s *BucketService) GetVersioning(ctx context.Context) (*BucketGetVersionResult, *Response, error)
```

#### 요청 예시
[//]: # ".cssg-snippet-get-bucket-versioning"
```go
_, _, err := client.Bucket.GetVersioning(context.Background())
if err != nil {
    panic(err)
}
```

#### 반환 결과 설명
```go
type BucketGetVersionResult struct {
	Status  string
}
```
| 매개변수 이름| 설명  | 유형  |
| ----| ---- | ---- |
| BucketGetVersionResult | 버전 제어 정책  | struct |
| Status | 버전 제어가 활성화되어 있는지 설명. 열거 값: Suspended(버전 제어 일시 중지), Enabled(버전 제어 활성화)  | string |

