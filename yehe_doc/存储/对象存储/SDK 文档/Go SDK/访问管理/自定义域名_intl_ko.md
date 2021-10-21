

## 소개

본문은 사용자 정의 도메인에 대한 API 개요 및 SDK 예시 코드를 제공합니다.

| API                                                          | 작업명         | 작업 설명                             |
| ----------------- | -------------- | -------------------------- |
| PUT Bucket domain | 사용자 정의 도메인 설정 | 버킷 사용자 정의 도메인 정보 설정 |
| GET Bucket domain | 사용자 정의 도메인 쿼리 | 버킷 사용자 정의 도메인 정보 쿼리 |
| DELETE Bucket domain | 사용자 정의 도메인 삭제 |버킷 사용자 정의 도메인 정보 삭제|

## 사용자 정의 도메인 설정

#### 기능 설명

PUT Bucket domain은 버킷 사용자 정의 도메인 설정에 사용됩니다.

#### 메소드 프로토타입

```go
func (s *BucketService) PutDomain(ctx context.Context, opt *BucketPutDomainOptions) (*Response, error)
```

#### 요청 예시

[//]: # (.cssg-snippet-put-bucket-domain)
```go
opt := &cos.BucketPutDomainOptions{
    Rules: []cos.BucketDomainRule{
    {
        Status:            "ENABLED",
        Name:              "www.example.com",
        Type:              "REST",
        ForcedReplacement: "CNAME",
    },
    },
}   
resp, err := c.Bucket.PutDomain(context.Background(), opt)
```

#### 매개변수 설명

```go
type BucketDomainRule struct {
    Status            string
    Name           string
    Type              string
    ForcedReplacement string
}

type BucketPutDomainOptions struct {
    XMLName xml.Name
    Rules   []BucketDomainRule
}
```

| 매개변수 이름         | 설명                                                         | 유형             |
| ---------------------- | ------------------------------------------------------------ | ------ |
| BucketPutDomainOptions | 사용자 정의 도메인 설정                                               | Struct |
| Rules                  | 도메인 설정 규칙                                                 | Array  |
| Status                 | 도메인 활성화/비활성화 상태. 유효값: ENABLED/DISABLED                   | String |
| Name                   | 사용자 정의 도메인. 유효값: 문자, 숫자, 점                     | String |
| Type                   | 바인딩된 원본 서버 유형. 유효값: REST/WEBSITE                          | String |
| ForcedReplacement      | 기존 설정 교체. 유효값: CNAME/TXT. 입력하면 도메인 이름의 소유권을 강제 인증한 후 구성을 전송합니다. | String |

#### 오류 코드 설명

이 요청에서 발생할 수 있는 몇 가지 특수 오류는 다음과 같습니다.

| 상태 코드                                 | 설명                                                         |
| -------------------------------------- | ------------------------------------------------------------ |
| HTTP 409 Conflict                      | 도메인 이름 레코드가 이미 존재하며 요청에 강제 덮어쓰기가 설정되어 있지 않습니다. 또는 도메인 이름 레코드가 없고 요청에 강제 덮어쓰기가 설정되어 있습니다. |
| HTTP 451 Unavailable For Legal Reasons | 도메인 이름이 중국 내 도메인 이름이며 ICP비안이 완료되지 않았습니다. |

## 사용자 정의 도메인 쿼리

#### 기능 설명

GET Bucket domain은 버킷의 사용자 지정 도메인 이름 정보를 쿼리하는 데 사용됩니다.

#### 메소드 프로토타입

```go
func (s *BucketService) GetDomain(ctx context.Context) (*BucketGetDomainResult, *Response, error)
```

#### 요청 예시

[//]: # (.cssg-snippet-get-bucket-domain)
```go
v, resp, err := c.Bucket.GetDomain(context.Background())
```

#### 반환 결과 설명

```go
type BucketGetDomainResult BucketPutDomainOptions
```

| 매개변수 이름              | 설명                                                         | 유형   |
| --------------------- | ------------------------------------------------------------ | ------ |
| BucketGetDomainResult | 사용자 정의 도메인 설정                                               | Struct |
| Rules                 | 도메인 설정 규칙                                                 | Array  |
| Status                 | 도메인 활성화/비활성화 상태. 유효값: ENABLED/DISABLED                   | String |
| Name                   | 사용자 정의 도메인. 유효값: 문자, 숫자, 점                     | String |
| Type                   | 바인딩된 원본 서버 유형. 유효값: REST/WEBSITE                          | String |
| ForcedReplacement      | 기존 설정 교체. 유효값: CNAME/TXT. 입력하면 도메인 이름의 소유권을 강제 인증한 후 구성을 전송합니다. | String |

## 사용자 정의 도메인 삭제

DELETE  Bucket domain은 버킷의 모든 사용자 정의 도메인 정보 삭제에 사용됩니다.

#### 메소드 프로토타입

```go
func (s *BucketService) DeleteDomain(ctx context.Context) (*Response, error)
```

#### 요청 예시

[//]: # (.cssg-snippet-delete-bucket-domain)
```go
_, err := c.Bucket.DeleteDomain(context.Background())
```
