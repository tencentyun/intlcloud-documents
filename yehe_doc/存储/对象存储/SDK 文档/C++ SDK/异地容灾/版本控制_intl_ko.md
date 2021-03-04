## 소개

본 문서에서는 버전 제어에 대한 API 개요 및 SDK 예시 코드를 제공합니다.

| API                                                          | 작업명       | 작업 설명                 |
| ------------------------------------------------------------ | ------------ | ------------------------ |
| [PUT Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19889) | 버전 제어 설정 | 버킷의 버전 제어 기능 설정 |
| [GET Bucket versioning](https://intl.cloud.tencent.com/zh/document/product/436/19888) | 버전 제어 확인 | 버킷의 버전 제어 정보 조회 |

## 버전 제어 설정

#### 기능 설명

특정 버킷의 버전 제어 기능(PUT Bucket versioning)을 설정합니다.

#### 프로토타입 메소드
```cpp
CosResult BucketOp::PutBucketVersioning(const PutBucketVersioningReq& req, PutBucketVersioningResp* resp);
```

#### 요청 예시

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);
std::string bucket_name = "examplebucket-1250000000";
qcloud_cos::PutBucketVersioningReq req(bucket_name);
qcloud_cos::PutBucketVersioningResp resp;

// 버전 제어 활성화
req.SetStatus(true);

qcloud_cos::CosResult result = cos.PutBucketVersioning(req, &resp);

if (result.IsSucc()) {
    // 요청 성공
} else {
    // 요청 실패 시, CosResult의 멤버 함수를 호출하여 오류 정보를 출력할 수 있음. 예: requestID 등
} 
```

#### 매개변수 설명

| 매개변수 | 매개변수 설명                      | 유형                   | 필수 입력 여부  |
| ---- | ------------------------------|------------------------| ------|
| req  | PutBucketVersioning 작업의 요청 | PutBucketVersioningReq | 예    |
| resp | PutBucketVersioning 작업의 응답  | PutBucketVersioningResp| 예    |


PutBucketVersioningReq는 다음과 같은 메소드를 제공하여 버전 제어를 활성화하거나 일시 중지할 수 있습니다.

```cpp
void SetStatus(bool is_enable);
```


## 버전 제어 조회

#### 기능 설명

특정 버킷의 버전 제어 정보(GET Bucket versioning)를 조회합니다.

#### 프로토타입 메소드
```cpp
CosResult CosAPI::GetBucketVersioning(const GetBucketVersioningReq& request, GetBucketVersioningResp* response);
```

#### 요청 예시

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);
std::string bucket_name = "examplebucket-1250000000";
qcloud_cos::GetBucketVersioningReq req(bucket_name);
qcloud_cos::GetBucketVersioningResp resp;

qcloud_cos::CosResult result = cos.GetBucketVersioning(req, &resp);

if (result.IsSucc()) {
    // 요청 성공 시, resp 메소드를 통해 버전 제어 상태를 획득
} else {
    // 요청 실패 시, CosResult의 멤버 함수를 호출하여 오류 정보를 출력할 수 있음. 예: requestID 등
} 
```

#### 매개변수 설명

| 매개변수 | 매개변수 설명                      | 유형                   | 필수 입력 여부  |
| ---- | ------------------------------|------------------------| ------|
| req  | GetBucketVersioning 작업의 요청 | GetBucketVersioningReq | 예    |
| resp | GetBucketVersioning 작업의 요청  | GetBucketVersioningResp| 예    |


GetBucketVersioningResp는 다음과 같은 메소드를 제공하여 버전 제어 상태를 획득합니다.

```cpp
int GetStatus() const;
```
