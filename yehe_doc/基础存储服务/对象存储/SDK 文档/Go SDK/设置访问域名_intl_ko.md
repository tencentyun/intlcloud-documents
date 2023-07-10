## 소개

본문은 기본 도메인이 아닌 도메인으로 Cloud Object Storage(COS) 서비스를 요청하는 방법을 제공합니다.

### 기본 COS 도메인 이름 설정

#### 요청 예시
```go
// examplebucket-1250000000과 COS_REGION을 실제 정보로 수정합니다.
u, _ := url.Parse("https://examplebucket-1250000000.cos.COS_REGION.myqcloud.com")
// Get Service 쿼리에 사용, 모든 리전 기본값: service.cos.myqcloud.com
su, _ := url.Parse("https://cos.COS_REGION.myqcloud.com")
b := &cos.BaseURL{BucketURL: u, ServiceURL: su}
// 1. 영구 키
client := cos.NewClient(b, &http.Client{
   Transport: &cos.AuthorizationTransport{
       SecretID:  "SECRETID",
       SecretKey: "SECRETKEY",
   },
})
```

### 기본 CDN 가속 도메인

#### 기능 설명

COS 콘솔에서 버킷에 기본 CDN 가속 도메인을 활성화한 후 SDK 코드에 해당 도메인을 설정해 편리하게 기본 가속 도메인을 구현할 수 있습니다.
기본 가속 도메인 활성화 방법은 [기본 CDN 가속 도메인 활성화](https://intl.cloud.tencent.com/document/product/436/31505)를 참고하십시오.

#### 요청 예시

```go
// examplebucket-1250000000을 실제 정보로 수정.
u, _ := url.Parse("https://examplebucket-1250000000.file.myqcloud.com")
b := &cos.BaseURL{BucketURL: u}
// CDN 가속 도메인 사용. COS의 인증 정보 재발송 불필요.
client := cos.NewClient(b, &http.Client{})
```

### 사용자 정의 CDN 가속 도메인

#### 기능 설명

COS 콘솔에서 버킷에 사용자 정의 CDN 가속 도메인을 설정한 후 SDK 코드에 해당 도메인을 설정해 편리하게 사용자 정의 도메인에 가속 기능을 구현할 수 있습니다. 사용자 정의 CDN 가속 도메인 활성화 방법은 [사용자 정의 CDN 가속 도메인 활성화](https://intl.cloud.tencent.com/document/product/436/31506)를 참고하십시오.

#### 요청 예시

```go
// 사용자 정의 cdn 가속 도메인 이름 설정
u, _ := url.Parse("https://xxx.xxx.com")
b := &cos.BaseURL{BucketURL: u}
// CDN 가속 도메인 사용. COS의 인증 정보 재발송 불필요.
client := cos.NewClient(b, &http.Client{})
```

### 사용자 정의 원본 서버 도메인

#### 요청 예시

```go
// 사용자 정의 원본 서버 도메인
u, _ := url.Parse("https://xxx.xxx.com")
b := &cos.BaseURL{BucketURL: u}
client := cos.NewClient(b, &http.Client{
   Transport: &cos.AuthorizationTransport{
       SecretID:  "SECRETID",
       SecretKey: "SECRETKEY",
   },
})
```

### 글로벌 가속 도메인

#### 요청 예시

```go
// 글로벌 가속 도메인
// examplebucket-1250000000을 실제 정보로 수정.
u, _ := url.Parse("https://examplebucket-1250000000.cos.accelerate.myqcloud.com")
b := &cos.BaseURL{BucketURL: u}
client := cos.NewClient(b, &http.Client{
   Transport: &cos.AuthorizationTransport{
       SecretID:  "SECRETID",
       SecretKey: "SECRETKEY",
   },
})
```
