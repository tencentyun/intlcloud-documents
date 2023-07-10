## 소개

본문은 버킷 Referer 에 대한 화이트/블랙리스트의 API 개요 및 SDK 예시 코드를 제공합니다.

| API                                                          | 작업 이름         | 작업 설명                   |
| ------------------------------------------------------------ | -------------- | -------------------------- |
| [PUT Bucket referer](https://intl.cloud.tencent.com/document/product/436/31423) | 버킷 Referer 설정 | 버킷 Referer 화이트 또는 블랙리스트 설정 |
| [GET Bucket referer](https://intl.cloud.tencent.com/document/product/436/30615) | 버킷 Referer 쿼리| 버킷 Referer 화이트 또는 블랙리스트 쿼리 |

## 버킷 Referer 설정

#### 기능 설명

버킷의 Referer의 화이트 또는 블랙리스트를 설정합니다(PUT Bucket referer).

#### 메소드 프로토타입

```go
func (s *BucketService) PutReferer(ctx context.Context, opt *BucketPutRefererOptions) (*Response, error)
```

#### 요청 예시

```go
opt := &cos.BucketPutRefererOptions{
	Status:      "Enabled",
	RefererType: "White-List",
	DomainList: []string{
		"*.qq.com",
		"*.qcloud.com",
	},
	EmptyReferConfiguration: "Allow",
}
  
_, err := c.Bucket.PutReferer(context.Background(), opt)
```

#### 매개변수 설명

```go
type BucketPutRefererOptions struct {
    Status                  string 
    RefererType             string 
    DomainList              []string 
    EmptyReferConfiguration string
}
```

| 매개변수 이름                                   | 매개변수 설명                                                     | 유형                                     |
| ---------------------------------------- | ------------------------------------------------------------ | ---------------------------------------- |
| Status         | 링크 도용 방지 활성화 여부. 열거 값: Enabled, Disabled.           | String |
| RefererType    | 링크 도용 방지 유형 열거 값: Black-List, White-List          | String |
| DomainList         | 적용 도메인. 포트, IP, 와일드 카드\* 지원, 복수 지원.        | Array |
| EmptyReferConfiguration | 빈 Refer 액세스 허용 여부, 열거 값: Allow, Deny | String |

## 버킷 Referer 쿼리

#### 기능 설명

버킷의 Referer의 화이트 또는 블랙리스트를 쿼리합니다(PUT Bucket referer).

#### 메소드 프로토타입

```go
func (s *BucketService) GetReferer(ctx context.Context) (*BucketGetRefererResult, *Response, error)
```

#### 요청 예시

```go
res, _, err := c.Bucket.GetReferer(context.Background())
```

#### 반환 결과 설명

```go
type BucketGetRefererResult struct {
    Status                  string 
    RefererType             string 
    DomainList              []string 
    EmptyReferConfiguration string
}
```

| 매개변수 이름                                   | 매개변수 설명                                                     | 유형                                     |
| ---------------------------------------- | ------------------------------------------------------------ | ---------------------------------------- |
| Status         | 링크 도용 방지 활성화 여부. 열거 값: Enabled, Disabled.           | String |
| RefererType    | 링크 도용 방지 유형 열거 값: Black-List, White-List          | String |
| DomainList         | 적용 도메인. 포트, IP, 와일드 카드\* 지원, 복수 지원.        | Array |
| EmptyReferConfiguration | 빈 Refer 액세스 허용 여부, 열거 값: Allow, Deny | String |
