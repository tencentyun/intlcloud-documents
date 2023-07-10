## 소개

본 문서는 버킷의 기본 작업에 대한 관련 API 개요 및 SDK 예시 코드를 제공합니다.


| API                                                          | 작업명             | 작업 설명                           |
| ------------------------------------------------------------ | ------------------ | ---------------------------------- |
| [GET Service(List Buckets)](https://intl.cloud.tencent.com/document/product/436/8291) | 버킷 리스트 조회     | 특정 계정의 모든 버킷 리스트 조회     |
| [PUT Bucket](https://intl.cloud.tencent.com/document/product/436/7738) | 버킷 생성         | 특정 계정에서 버킷 생성         |
| [HEAD Bucket](https://intl.cloud.tencent.com/document/product/436/7735) | 버킷 및 해당 권한 인덱스 | 버킷 존재 여부 및 액세스 권한 보유 여부 인덱스 |
| [DELETE Bucket](https://intl.cloud.tencent.com/document/product/436/7732) | 버킷 삭제         | 특정 계정의 빈 버킷 삭제           |


## 버킷 리스트 조회

#### 기능 설명

특정 계정의 모든 버킷 리스트를 조회하는 데 사용합니다.

#### 방법 모델

```cpp
CosResult GetService(const GetServiceReq& request, GetServiceResp* response)
```

#### 요청 예시

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "examplebucket-1250000000";

qcloud_cos::GetServiceReq req;
qcloud_cos::GetServiceResp resp;
qcloud_cos::CosResult result = cos.GetService(req, &resp);

// 호출 성공 시 resp의 멤버 함수를 호출하여 반환 내용 획득
if (result.IsSucc()) {
    const qcloud_cos::Owner& owner = resp.GetOwner();
    const std::vector<qcloud_cos::Bucket>& buckets = resp.GetBuckets();
    std::cout << "owner.m_id=" << owner.m_id << ", owner.display_name=" << owner.m_display_name << std::endl;               
     for (std::vector<qcloud_cos::Bucket>::const_iterator itr = buckets.begin(); itr != buckets.end(); ++itr) {
         const qcloud_cos::Bucket& bucket = *itr;
         std::cout << "Bucket name=" << bucket.m_name << ", location=" 
         << bucket.m_location << ", create_date=" << bucket.m_create_date << std::endl;                                  
     } 
} else {
    // CosResult의 멤버 함수를 호출하여 requestID 등의 오류 정보 출력 가능
} 
```

#### 매개변수 설명

| 매개변수 | 매개변수 설명             | 유형          | 필수 입력 여부  |
| ---- | ---------------------|---------------| ------|
| req  | GetService 작업 요청 | GetServiceReq | 예    |
| resp | GetService 작업 응답 | GetServiceResp| 예    |


GetServiceResp는 다음의 멤버 함수를 제공하며, Get Service가 반환하는 XML 포맷 상의 상세 내용을 획득하는 데 사용합니다. 

```C++
// Bucket 소유자 정보 획득
Owner GetOwner() const;
// 모든 Bucket 리스트 정보 획득
std::vector<Bucket> GetBuckets() const
```

여기서 Owner의 정의는 다음과 같습니다.

```cpp
struct Owner {
    std::string m_id;    // 버킷 소유자의 ID
    std::string m_display_name; // 버킷 소유자의 이름 정보
}; 
```

여기서 Bucket의 정의는 다음과 같습니다.

```cpp
// 단일 Bucket의 정보 설명                                                                                                                                                                    
struct Bucket {
    std::string m_name; // Bucket 이름
    std::string m_location; // Bucket이 속한 리전
    std::string m_create_date; // Bucket 생성 시간으로, ISO8601 포맷을 사용합니다. 예시: 2016-11-09T08:46:32.000Z
};
```



## 버킷 생성

#### 기능 설명

하나의 버킷을 생성합니다(PUT Bucket).

#### 방법 모델

```cpp
CosResult PutBucket(const PutBucketReq& req, PutBucketResp* resp)
```

#### 요청 예시

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "examplebucket-1250000000";

qcloud_cos::PutBucketReq req(bucket_name);
qcloud_cos::PutBucketResp resp;
qcloud_cos::CosResult result = cos.PutBucket(req, &resp);

// 호출 성공 시 resp의 멤버 함수를 호출하여 반환 내용 획득
if (result.IsSucc()) {
    // ...
} else {
    // CosResult의 멤버 함수를 호출하여 requestID 등의 오류 정보 출력 가능
} 
```

#### 매개변수 설명

| 매개변수 | 매개변수 설명            | 유형         | 필수 입력 여부  |
| ---- | --------------------|--------------| ------|
| req  | PutBucket 작업 요청 | PutBucketReq | 예    |
| resp | PutBucket 작업 응답 | PutBucketResp| 예    |


PutBucketReq는 다음의 멤버 함수를 제공합니다.

```C++
// Bucket의 ACL 속성 정의. 유효 값: private, public-read-write, public-read
// 기본값: private
void SetXCosAcl(const std::string& str);

// 권한이 부여된 사용자에게 읽기 권한 부여. 포맷: x-cos-grant-read: id=" ",id=" ".
// 서브 계정에 권한을 부여할 경우, id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"
// 루트 계정에 권한을 부여할 경우, id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"
void SetXCosGrantRead(const std::string& str);

// 권한이 부여된 사용자에게 쓰기 권한 부여. 포맷: x-cos-grant-write: id=" ",id=" "./
// 서브 계정에 권한을 부여할 경우, id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>",
// 루트 계정에 권한을 부여할 경우, id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"
void SetXCosGrantWrite(const std::string& str);
    
// 권한이 부여된 사용자에게 읽기/쓰기 권한 부여. 포맷: x-cos-grant-full-control: id=" ",id=" ".
// 서브 계정에 권한을 부여할 경우, id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>",
// 루트 계정에 권한을 부여할 경우, id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"
void SetXCosGrantFullControl(const std::string& str);
```

## 버킷 및 해당 권한 인덱스

#### 기능 설명

버킷의 존재 여부 및 액세스 권한 보유 여부를 인덱스합니다.

#### 방법 모델

```C++
CosResult HeadBucket(const HeadBucketReq& req, HeadBucketResp* resp)
```

#### 요청 예시

```C++
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "examplebucket-1250000000";

qcloud_cos::HeadBucketReq req(bucket_name);
qcloud_cos::HeadBucketResp resp;
qcloud_cos::CosResult result = cos.HeadBucket(req, &resp);

// 호출 성공 시 resp의 멤버 함수를 호출하여 반환 내용 획득
if (result.IsSucc()) {
    // ...
} else {
    // CosResult의 멤버 함수를 호출하여 requestID 등의 오류 정보 출력 가능
} 
```

#### 매개변수 설명

| 매개변수 | 매개변수 설명             |  유형         | 필수 입력 여부  |
| ---- | ---------------------| --------------| ------|
| req  | HeadBucket 작업 요청 | HeadBucketReq | 예    |
| resp | HeadBucket 작업 응답 | HeadBucketResp| 예    |


## 버킷 삭제

#### 기능 설명

특정 계정의 빈 버킷을 삭제합니다.

#### 방법 모델

```cpp
CosResult DeleteBucket(const DeleteBucketReq& req, DeleteBucketResp* resp)
```

#### 요청 예시

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "examplebucket-1250000000";

// DeleteBucketReq의 구조 함수에 bucket_name 입력 필요
qcloud_cos::DeleteBucketReq req(bucket_name);
qcloud_cos::DeleteBucketResp resp;
qcloud_cos::CosResult result = cos.DeleteBucket(req, &resp);

// 호출 성공 시 resp의 멤버 함수를 호출하여 반환 내용 획득
if (result.IsSucc()) {
    // ...
} else {
    // CosResult의 멤버 함수를 호출하여 requestID 등의 오류 정보 출력 가능
} 
```

#### 매개변수 설명

| 매개변수 | 매개변수 설명               |  유형           | 필수 입력 여부  |
| ---- | -----------------------| ----------------| ------|
| req  | DeleteBucket 작업 요청 | DeleteBucketReq | 예    |
| resp | DeleteBucket 작업 응답 | DeleteBucketResp| 예    |
