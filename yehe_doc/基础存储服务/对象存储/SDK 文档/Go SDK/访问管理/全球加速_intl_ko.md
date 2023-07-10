
## 소개

본 문서는 글로벌 가속에 대한 API 개요 및 SDK 예시 코드를 제공합니다.

| API                                                          | 작업명       | 작업 설명                         |
| :----------------------------------------------------------- | :----------- | :------------------------------- |
| [PUT Bucket Accelerate](https://intl.cloud.tencent.com/document/product/436/33411) | 글로벌 가속 설정 | 버킷의 글로벌 가속 기능 활성화 또는 일시 중지   |
| [GET Bucket Accelerate](https://intl.cloud.tencent.com/document/product/436/33412) | 글로벌 가속 조회 | 버킷의 글로벌 가속 기능 설정 정보 조회 |


## 글로벌 가속 설정

#### 기능 설명

버킷의 글로벌 가속 기능을 활성화하거나 일시 중지합니다.

#### 방법 모델

```go
func (s *BucketService) PutAccelerate(ctx context.Context, opt *BucketPutAccelerateOptions) (*Response, error)
```

#### 요청 예시

[//]: # ".cssg-snippet-put-accelerate"
```go
opt := &cos.BucketPutAccelerateOptions{
    Status: "Enabled",
    Type:   "COS",
}
_, err = c.Bucket.PutAccelerate(context.Background(), opt)
if err != nil {
    // ERROR
}
```
#### 매개변수 설명

```go
type BucketPutAccelerateOptions struct {
    Status  string
}
```
| 매개변수 이름 | 매개변수 설명                                             | 유형   | 필수 입력 여부 |
| -------- | ---------------------------------------------------- | ------ | ---- |
| Status   | 글로벌 가속 기능 활성화 여부 표시. 열거 값: Suspended, Enabled | string | 예   |

### 글로벌 가속 조회

#### 기능 설명

버킷의 글로벌 가속 기능 설정을 조회합니다.

#### 방법 모델

```go
func (s *BucketService) GetAccelerate(ctx context.Context) (*BucketGetAccelerateResult, *Response, error)
```

#### 요청 예시

[//]: # ".cssg-snippet-get-accelerate"
```go
res, _, err = c.Bucket.GetAccelerate(context.Background())
if err != nil {
    // ERROR
}
```
#### 반환 결과 설명

```go
type BucketGetAccelerateResult struct {
    Status  string
}
```
| 매개변수 이름 | 매개변수 설명                                             | 유형   | 필수 입력 여부 |
| -------- | ---------------------------------------------------- | ------ | ---- |
| Status   | 글로벌 가속 기능 활성화 여부 표시. 열거 값: Suspended, Enabled | string | 예   |
