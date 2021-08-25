## 소개

본 문서는 객체의 간단한 작업, 멀티파트 작업 등 기타 관련 API 개요 및 SDK 예시 코드를 제공합니다.

### 간단한 작업

| API                                                          | 작업명         | 작업 설명                       |
| ------------------------------------------------------------ | -------------- | ------------------------------ |
| [GET Bucket(List Objects)](https://intl.cloud.tencent.com/document/product/436/30614) | 객체 리스트 조회   | 버킷의 일부 또는 모든 객체 조회           |
| [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) | 간편 객체 업로드   | 버킷에 단일 객체 업로드           |
| [HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745) | 객체 메타데이터 조회 | 객체 메타데이터 정보 조회             |
| [GET Object](https://intl.cloud.tencent.com/document/product/436/7753) | 객체 다운로드       | 로컬에 객체 다운로드             |
| [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881) | 객체 복사 설정   | 타깃 경로에 파일 복사             |
| [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743) | 단일 객체 삭제   | 버킷에서 지정 객체 삭제         |
| [DELETE Multiple Objects](https://intl.cloud.tencent.com/document/product/436/8289) | 다수의 객체 삭제   | 버킷에서 객체 일괄 삭제         |
| [POST Object restore](https://intl.cloud.tencent.com/document/product/436/12633) | 보관된 객체 복구 | 아카이브 유형의 객체 검색 및 액세스           |
| GET Object URL | 객체 URL 가져오기 | 객체의 서명없는 URL 가져오기 |

### 멀티파트 작업

| API                                                          | 작업명         | 작업 설명                             |
| ------------------------------------------------------------ | -------------- | ------------------------------------ |
| [List Multipart Uploads](https://intl.cloud.tencent.com/document/product/436/7736) | 멀티파트 업로드 조회   | 현재 진행 중인 멀티파트 업로드 정보 조회         |
| [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746) | 멀티파트 업로드 초기화 | 	멀티파트 업로드 작업 초기화     |
| [Upload Part](https://intl.cloud.tencent.com/document/product/436/7750) | 파트 업로드       | 파일 멀티파트 업로드                         |
| [Upload Part - Copy](https://intl.cloud.tencent.com/document/product/436/8287) | 멀티파트 복사       | 다른 객체를 한 파트로 복사             |
| [List Parts](https://intl.cloud.tencent.com/document/product/436/7747) | 업로드된 파트 조회   | 특정 멀티파트 업로드 작업에서 업로드된 파트 조회   |
| [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742) | 멀티파트 업로드 완료   | 전체 파일의 멀티파트 업로드 완료               |
| [Abort Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7740) | 멀티파트 업로드 중지   | 멀티파트 업로드 작업 중지 및 업로드된 파트 삭제 |

## 간단한 작업

### 객체 리스트 조회

#### 기능 설명

버킷의 일부 또는 모든 객체를 조회합니다.

#### 메소드 프로토타입

```cpp
CosResult GetBucket(const GetBucketReq& req, GetBucketResp* resp)
```

#### 요청 예시

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "examplebucket-1250000000";

// GetBucketReq의 생성자에 bucket_name 전달 필요
qcloud_cos::GetBucketReq req(bucket_name);
qcloud_cos::GetBucketResp resp;
qcloud_cos::CosResult result = cos.GetBucket(req, &resp);

// 호출 성공. resp의 멤버 함수를 호출하여 반환 내용 획득
if (result.IsSucc()) {
    std::cout << "Name=" << resp.GetName() << std::endl;
    std::cout << "Prefix=" << resp.GetPrefix() << std::endl;
    std::cout << "Marker=" << resp.GetMarker() << std::endl;
    std::cout << "MaxKeys=" << resp.GetMaxKeys() << std::endl;
} else {
    std::cout << "ErrorInfo=" << result.GetErrorInfo() << std::endl;
    std::cout << "HttpStatus=" << result.GetHttpStatus() << std::endl;
    std::cout << "ErrorCode=" << result.GetErrorCode() << std::endl;
    std::cout << "ErrorMsg=" << result.GetErrorMsg() << std::endl;
    std::cout << "ResourceAddr=" << result.GetResourceAddr() << std::endl;
    std::cout << "XCosRequestId=" << result.GetXCosRequestId() << std::endl;
    std::cout << "XCosTraceId=" << result.GetXCosTraceId() << std::endl;
} 
```

#### 매개변수 설명

| 매개변수 | 매개변수 설명            |  유형         | 필수 입력 여부  |
| ---- | --------------------| --------------| ------|
| req  | GetBucket 작업의 요청 | GetBucketReq  | 예    |
| resp | GetBucket 작업의 응답 | GetBucketResp | 예    |


GetBucketResp는 다음의 멤버 함수를 제공하며, Get Bucket이 반환하는 XML 형식의 상세 내용을 획득하는 데 사용합니다. 

```cpp
std::vector<Content> GetContents();
std::string GetName();
std::string GetPrefix();
std::string GetMarker();
uint64_t GetMaxKeys();
bool IsTruncated();
std::vector<std::string> GetCommonPrefixes();
```

여기서 Content의 정의는 다음과 같습니다.

```
struct Content {
    std::string m_key; // Object의 Key
    std::string m_last_modified; // Object의 최종 수정 시간
    std::string m_etag; // 파일의 MD-5 알고리즘 검증 값
    std::string m_size; // 파일 크기, 단위: Byte
    std::vector<std::string> m_owner_ids; // Bucket 소유자 정보
    std::string m_storage_class; // Object 스토리지 유형. 열거 값: STANDARD, STANDARD_IA
};
```

### 간편한 객체 업로드

#### 기능 설명

지정한 버킷에 객체를 업로드합니다.

#### 메소드 프로토타입

```cpp
/// Stream으로 업로드
CosResult PutObject(const PutObjectByStreamReq& req, PutObjectByStreamResp* resp)

/// 로컬 파일 업로드
CosResult PutObject(const PutObjectByFileReq& req, PutObjectByFileResp* resp)
```

#### 요청 예시

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "examplebucket-1250000000";
std::string object_name = "object_name";

// 간편 업로드(스트림)
{
    std::istringstream iss("put object");
    // request의 생성자에 istream 입력 필요
    qcloud_cos::PutObjectByStreamReq req(bucket_name, object_name, iss);
    // Set 메소드를 호출하여 메타데이터 또는 ACL 등 설정
    req.SetXCosStorageClass("STANDARD_IA");
    // MD5 검증을 비활성화. req.TurnOnComputeConentMd5() 사용 활성화. 기본적으로 활성화되어 있음
    req.TurnOffComputeConentMd5();
    qcloud_cos::PutObjectByStreamResp resp;
    qcloud_cos::CosResult result = cos.PutObject(req, &resp);
    
    if (result.IsSucc()) {
        // 호출 성공 시 resp의 멤버 함수를 호출하여 반환 내용 획득
        do sth
    } else {
        // 호출 실패 시 result의 멤버 함수를 호출하여 오류 정보 획득
        std::cout << "ErrorInfo=" << result.GetErrorInfo() << std::endl;
        std::cout << "HttpStatus=" << result.GetHttpStatus() << std::endl;
        std::cout << "ErrorCode=" << result.GetErrorCode() << std::endl;
        std::cout << "ErrorMsg=" << result.GetErrorMsg() << std::endl;
        std::cout << "ResourceAddr=" << result.GetResourceAddr() << std::endl;
        std::cout << "XCosRequestId=" << result.GetXCosRequestId() << std::endl;
        std::cout << "XCosTraceId=" << result.GetXCosTraceId() << std::endl;
     }
}

// 간편 업로드(파일)
{
    // request의 생성자에 로컬 파일 경로 전달 필요
    qcloud_cos::PutObjectByFileReq req(bucket_name, object_name, "/path/to/local/file");
    // Set 메소드를 호출하여 메타데이터 또는 ACL 등 설정
    req.SetXCosStorageClass("STANDARD_IA");
    // MD5 검증을 비활성화하고 req.TurnOnComputeConentMd5() 사용 활성화. 기본적으로 활성화되어 있음
    req.TurnOffComputeConentMd5();
    qcloud_cos::PutObjectByFileResp resp;
    qcloud_cos::CosResult result = cos.PutObject(req, &resp);
        if (result.IsSucc()) {
        // 호출 성공 시 resp의 멤버 함수를 호출하여 반환 내용 획득
        do sth
    } else {
        // 호출 실패 시 result의 멤버 함수를 호출하여 오류 정보 획득
        std::cout << "ErrorInfo=" << result.GetErrorInfo() << std::endl;
        std::cout << "HttpStatus=" << result.GetHttpStatus() << std::endl;
        std::cout << "ErrorCode=" << result.GetErrorCode() << std::endl;
        std::cout << "ErrorMsg=" << result.GetErrorMsg() << std::endl;
        std::cout << "ResourceAddr=" << result.GetResourceAddr() << std::endl;
        std::cout << "XCosRequestId=" << result.GetXCosRequestId() << std::endl;
        std::cout << "XCosTraceId=" << result.GetXCosTraceId() << std::endl;
     }
}
```

#### 매개변수 설명

| 매개변수 | 매개변수 설명            |  유형                                    | 필수 입력 여부  |
| ---- | --------------------| -----------------------------------------| ------|
| req  | PutObject 작업의 요청 | PutObjectByStreamReq/PutObjectByFileReq  | 예    |
| resp | PutObject 작업의 응답 | PutObjectByStreamResp/PutObjectByFileResp| 예    |


매개변수 Req에는 다음의 멤버 함수가 포함되어 있습니다.

```cpp
// Cache-Control RFC 2616에서 정의한 캐시 정책. Object의 메타데이터로 저장
void SetCacheControl(const std::string& str);

// Content-Disposition RFC 2616에서 정의한 파일 이름. Object의 메타데이터로 저장
void SetContentDisposition(const std::string& str);

// Content-Encoding    RFC 2616에서 정의한 인코딩 형식. Object의 메타데이터로 저장-
void SetContentEncoding(const std::string& str);

// Content-Type    RFC 2616에서 정의한 콘텐츠 유형(MIME). Object의 메타데이터로 저장
void SetContentType(const std::string& str);

// Expect에서 Expect: 100-continue 사용 시, 서버의 확인을 받아야만 요청 콘텐츠 발송 가능
void SetExpect(const std::string& str);

// Expires RFC 2616에서 정의한 만료시간. Object의 메타데이터로 저장
void SetExpires(const std::string& str);

// 사용자 정의한 헤더 정보 허용. Object의 메타데이터로 반환. 용량 제한: 2KB
void SetXCosMeta(const std::string& key, const std::string& value);

// x-cos-storage-class로 Object의 스토리지 등급 설정. 열거 값: STANDARD, STANDARD_IA, ARCHIVE
// 기본값: STANDARD
void SetXCosStorageClass(const std::string& storage_class);

// Object의 ACL 속성 정의. 유효 값: private, public-read
// 기본값: private
void SetXcosAcl(const std::string& str);

// 권한이 부여된 사용자에게 읽기 권한 부여. 형식: x-cos-grant-read: id=" ",id=" ".
// 서브 계정에 권한을 부여할 경우, id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"
// 루트 계정에 권한을 부여할 경우, id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"
void SetXcosGrantRead(const std::string& str);

// 권한이 부여된 사용자에게 읽기/쓰기 권한 부여. 형식: x-cos-grant-full-control: id=" ",id=" ".
// 서브 계정에 권한을 부여할 경우, id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>",
// 루트 계정에 권한을 부여할 경우, id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"
void SetXcosGrantFullControl(const std::string& str);

/// Server 측 암호화에 사용할 알고리즘 설정. 현재 AES256 지원
void SetXCosServerSideEncryption(const std::string& str);
```

매개변수 Resp에는 다음의 멤버 함수가 포함되어 있습니다.

```C++
/// Object 버전 넘버 획득. Bucket에 멀티 버전이 활성화되지 않은 경우 공백 문자열 반환
std::string GetVersionId();

/// Server 측 암호화 시 사용하는 알고리즘
std::string GetXCosServerSideEncryption();
```

### 객체 메타데이터 조회

#### 기능 설명

객체 메타데이터 정보를 조회합니다.

#### 메소드 프로토타입

```cpp
CosResult HeadObject(const HeadObjectReq& req, HeadObjectResp* resp)
```


#### 요청 예시

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "examplebucket-1250000000";
std::string object_name = "object_name";
qcloud_cos::HeadObjectReq req(bucket_name, object_name);
qcloud_cos::HeadObjectResp resp;
qcloud_cos::CosResult result = cos.HeadObject(req, &resp);
if (result.IsSucc()) {
    // 다운로드 완료 시, HeadObjectResp의 멤버 함수 호출 가능
} else {
    // 다운로드 실패 시, CosResult의 멤버 함수를 호출하여 requestID 등의 오류 정보 출력 가능
}
```

#### 매개변수 설명

| 매개변수 | 매개변수 설명             |  유형         | 필수 입력 여부  |
| ---- | ---------------------| --------------| ------|
| req  | HeadObject 작업의 요청 | HeadObjectReq | 예    |
| resp | HeadObject 작업의 응답 | HeadObjectResp| 예    |


HeadObjectResp는 공용 헤더의 멤버 함수를 읽어오는 것 외에도, 다음의 멤버 함수를 제공합니다.

```cpp
std::string GetXCosObjectType();

std::string GetXCosStorageClass();

// 사용자 정의한 meta 획득. 매개변수는 x-cos-meta-* 중에서 * 설정
std::string GetXCosMeta(const std::string& key);

// map 형식으로 사용자 정의한 모든 meta 반환. map의 key에는 "x-cos-meta-" 접두사가 포함되지 않음
std::map<std::string, std::string> GetXCosMetas();

// Server 측 암호화 시 사용하는 알고리즘 획득
std::string GetXCosServerSideEncryption(); 
```

### 객체 다운로드

#### 기능 설명

객체를 로컬에 다운로드합니다(Get Object).

#### 메소드 프로토타입

```cpp
// Object를 로컬 파일에 다운로드
CosResult GetObject(const GetObjectByFileReq& req, GetObjectByFileResp* resp)

// Object를 스트림에 다운로드
CosResult GetObject(const GetObjectByStreamReq& req, GetObjectByStreamResp* resp)

// Object를 로컬 파일에 다운로드(멀티 스레드)
CosResult GetObject(const MultiGetObjectReq& req, MultiGetObjectResp* resp)
```

#### 요청 예시

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "examplebucket-1250000000";
std::string object_name = "object_name";
std::string local_path = "/tmp/object_name";

// 로컬 파일에 다운로드
{
    // request는 appid, bucketname, object, 로컬 경로를 제공해야 함(파일 이름 포함)
    qcloud_cos::GetObjectByFileReq req(bucket_name, object_name, local_path);
    qcloud_cos::GetObjectByFileResp resp;
    qcloud_cos::CosResult result = cos.GetObject(req, &resp);
    if (result.IsSucc()) {
        // 다운로드 완료 시, GetObjectByFileResp의 멤버 함수 호출 가능
    } else {
        // CosResult의 멤버 함수를 호출하여 requestID 등의 오류 정보 출력 가능
    }
}

// 스트림에 다운로드
{
    // request는 appid, bucketname, object, 출력 스트림을 제공해야 함
    std::ostringstream os;
    qcloud_cos::GetObjectByStreamReq req(bucket_name, object_name, os);
    qcloud_cos::GetObjectByStreamResp resp;
    qcloud_cos::CosResult result = cos.GetObject(req, &resp);
    if (result.IsSucc()) {
        // 다운로드 완료 시, GetObjectByStreamResp의 멤버 함수 호출 가능
    } else {
        // 다운로드 실패 시, CosResult의 멤버 함수를 호출하여 requestID 등의 오류 정보 출력 가능
    }
}

// 멀티 스레드로 로컬에 파일 다운로드
{
    // request는 appid, bucketname, object, 로컬 경로를 제공해야 함(파일 이름 포함)
    qcloud_cos::MultiGetObjectReq req(bucket_name, object_name, local_path);
    qcloud_cos::MultiGetObjectResp resp;
    qcloud_cos::CosResult result = cos.GetObject(req, &resp);
    if (result.IsSucc()) {
        // 다운로드 완료 시, MultiGetObjectResp의 멤버 함수 호출 가능
    } else {
        // 다운로드 실패 시, CosResult의 멤버 함수를 호출하여 requestID 등의 오류 정보 출력 가능
    }
}
```

#### 매개변수 설명

| 매개변수 | 매개변수 설명            |  유형                                                        | 필수 입력 여부  |
| ---- | --------------------| -------------------------------------------------------------| ------|
| req  | GetObject 작업의 요청 | GetObjectByFileReq/GetObjectByStreamReq/MultiGetObjectReq    | 예    |
| resp | GetObject 작업의 응답 | GetObjectByFileResp/GetObjectByStreamResp/MultiGetObjectResp | 예    |



멤버 함수는 다음과 같습니다.

```
// 응답 헤더의 Content-Type 매개변수 설정
void SetResponseContentType(const std::string& str);

// 응답 헤더의 Content-Language 매개변수 설정
void SetResponseContentLang(const std::string& str);

// 응답 헤더의 Content-Expires 매개변수 설정
void SetResponseExpires(const std::string& str);

// 응답 헤더의 Cache-Control 매개변수 설정
void SetResponseCacheControl(const std::string& str);

// 응답 헤더의 Content-Disposition 매개변수 설정
void SetResponseContentDisposition(const std::string& str);

// 응답 헤더의 Content-Encoding 매개변수 설정
void SetResponseContentEncoding(const std::string& str);

```

GetObjectResp는 공용 헤더의 멤버 함수를 읽어오는 것 외에도, 다음의 멤버 함수를 제공합니다.

```cpp
// Object의 마지막 수정 시간 획득. 문자열 형식은 Date이며, "Wed, 28 Oct 2014 20:30:00 GMT"와 유사
std::string GetLastModified();

// Object type 획득. Object의 추가 업로드 가능 여부를 표시합니다. 열거 값: normal 또는 appendable
std::string GetXCosObjectType();

// Object의 스토리지 유형 획득. 열거 값: STANDARD, STANDARD_IA
std::string GetXCosStorageClass();

// map 형식으로 사용자 정의한 모든 meta 반환. map의 key에는 "x-cos-meta-" 접두사가 포함되지 않음
std::map<std::string, std::string> GetXCosMetas();

// 사용자 정의한 meta 획득. 매개변수는 x-cos-meta-*중에서* 설정
std::string GetXCosMeta(const std::string& key);

// Server 측 암호화 시 사용하는 알고리즘 획득
std::string GetXCosServerSideEncryption(); 
```

### 객체 복사 설정

타깃 경로에 파일을 복사합니다.

#### 메소드 프로토타입

```cpp
CosResult PutObjectCopy(const PutObjectCopyReq& req, PutObjectCopyResp* resp)
```

#### 요청 예시

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "examplebucket-1250000000";
std::string object_name = "sevenyou";

qcloud_cos::PutObjectCopyReq req(bucket_name, object_name);                                                                                                                       
req.SetXCosCopySource("sevenyousouthtest-12345656.cn-south.myqcloud.com/sevenyou_source_obj");
qcloud_cos::PutObjectCopyResp resp;
qcloud_cos::CosResult result = cos.PutObjectCopy(req, &resp);
```

#### 매개변수 설명

| 매개변수 | 매개변수 설명                |  유형             | 필수 입력 여부  |
| ---- | ------------------------| ------------------| ------|
| req  | PutObjectCopy 작업의 요청 | PutObjectCopyReq  | 예    |
| resp | PutObjectCopy 작업의 응답 | PutObjectCopyResp | 예    |


PutObjectCopyReq에는 다음의 멤버 함수가 포함되어 있습니다.

```
// 원본 파일 URL 경로. versionid 하위 리소스로 이전 버전을 지정할 수 있습니다.
void SetXCosCopySource(const std::string& str);

// 메타데이터 복사 여부. 열거 값: Copy, Replaced. 기본값: Copy
// Copy로 표기할 경우 Header의 사용자 메타데이터 정보를 무시하고 복사
// Replaced로 표기할 경우 Header 정보에 따라 메타데이터 수정
// 타깃 경로와 원본 경로가 동일한 경우, 즉 사용자가 메타데이터 수정을 시도할 경우 반드시 Replaced로 표기
void SetXCosMetadataDirective(const std::string& str);

// Object가 지정된 시간 이후에 수정될 경우 작업을 수행하고, 그렇지 않을 경우 412 반환
// x-cos-copy-source-If-None-Match와 함께 사용할 수 있으며, 다른 조건과 함께 사용할 경우 충돌 반환
void SetXCosCopySourceIfModifiedSince(const std::string& str);

// Object가 지정된 시간 이후에 수정되지 않는 경우 작업을 수행하고, 그렇지 않을 경우 412 반환
// x-cos-copy-source-If-Match와 함께 사용할 수 있으며, 다른 조건과 함께 사용할 경우 충돌 반환
void SetXCosCopySourceIfUnmodifiedSince(const std::string& str);

// Object의 Etag가 사전 설정과 동일한 경우 작업을 수행하고, 그렇지 않을 경우 412 반환
// x-cos-copy-source-If-Unmodified-Since와 함께 사용할 수 있으며, 다른 조건과 함께 사용할 경우 충돌 반환
void SetXCosCopySourceIfMatch(const std::string& str);

// Object의 Etag가 사전 설정과 동일하지 않은 경우 작업을 수행하고, 그렇지 않을 경우 412 반환
// x-cos-copy-source-If-Modified-Since와 함께 사용할 수 있으며, 다른 조건과 함께 사용할 경우 충돌 반환
void SetXCosCopySourceIfNoneMatch(const std::string& str);

// x-cos-storage-class로 Object의 스토리지 등급 설정. 열거 값: STANDARD, STANDARD_IA
// 기본값: STANDARD
void SetXCosStorageClass(const std::string& storage_class);

// Object의 ACL 속성 정의. 유효 값: private, public-read
// 기본값: private
void SetXCosAcl(const std::string& str);

// 권한이 부여된 사용자에게 읽기 권한 부여. 형식: id="[OwnerUin]"  
void SetXCosGrantRead(const std::string& str);

// 권한이 부여된 사용자에게 모든 권한 부여. 형식: id="[OwnerUin]"
void SetXCosGrantFullControl(const std::string& str);

// 사용자 정의한 헤더 정보 허용. Object의 메타데이터로 반환. 용량 제한: 2KB
void SetXCosMeta(const std::string& key, const std::string& value);

/// Server 측 암호화에 사용할 알고리즘 설정. 현재 AES256 지원
void SetXCosServerSideEncryption(const std::string& str);

```

PutObjectCopyResp에는 다음의 멤버 함수가 포함되어 있습니다.

```
// 파일의 MD5 알고리즘 검증 값 반환. ETag 값으로 Object 내용에 변경 발생 여부 검사 가능
std::string GetEtag();

// 반환된 파일의 최종 수정 시간. 형식: GMT
std::string GetLastModified();

// 버전 넘버 반환
std::string GetVersionId();

/// Server 측 암호화 시 사용하는 알고리즘
std::string GetXCosServerSideEncryption();

```

### 단일 객체 삭제

#### 기능 설명

버킷에서 지정 객체를 삭제합니다.

#### 메소드 프로토타입

```cpp
CosResult DeleteObject(const DeleteObjectReq& req, DeleteObjectResp* resp)
```

#### 요청 예시

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "examplebucket-1250000000";
std::string object_name = "test_object";

qcloud_cos::DeleteObjectReq req(bucket_name, object_name);
qcloud_cos::DeleteObjectResp resp;
qcloud_cos::CosResult result = cos.DeleteObject(req, &resp);

// 호출 성공 시 resp의 멤버 함수를 호출하여 반환 내용 획득
if (result.IsSucc()) {
    // ...
} else {
    // CosResult의 멤버 함수를 호출하여 requestID 등의 오류 정보 출력 가능
} 
```

#### 매개변수 설명

| 매개변수 | 매개변수 설명               |  유형             | 필수 입력 여부  |
| ---- | -------------------- --| ------------------| ------|
| req  | DeleteObject 작업의 요청 | DeleteObjectReq   | 예    |
| resp | DeleteObject 작업의 응답 | DeletObjectResp   | 예    |


### 다수의 객체 삭제

#### 기능 설명

버킷에서 다수의 객체를 일괄 삭제합니다.

#### 메소드 프로토타입

```cpp
CosResult DeleteObjects(const DeleteObjectsReq& req, DeleteObjectsResp* resp)
```

#### 요청 예시

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "examplebucket-1250000000";

std::vector<std::string> objects;
std::vector<ObjectVersionPair> to_be_deleted;
objects.push_back("batch_delete_test_00");
objects.push_back("batch_delete_test_01");
objects.push_back("batch_delete_test_02");
objects.push_back("batch_delete_test_03");
for (size_t idx = 0; idx < objects.size(); ++idx) {
    ObjectVersionPair pair;
    pair.m_object_name = objects[idx];
    to_be_deleted.push_back(pair);
}
qcloud_cos::DeleteObjectsReq req(bucket_name, to_be_deleted);  
qcloud_cos::DeleteObjectsResp resp;                 
qcloud_cos::CosResult result = cos.DeleteObjects(req, &resp);
// 호출 성공 시 resp의 멤버 함수를 호출하여 반환 내용 획득
if (result.IsSucc()) {
    // ...
} else {
    // CosResult의 멤버 함수를 호출하여 requestID 등의 오류 정보 출력 가능
} 

```

#### 매개변수 설명

| 매개변수 | 매개변수 설명                |  유형             | 필수 입력 여부  |
| ---- | ------------------------| ------------------| ------|
| req  | DeleteObjects 작업의 요청 | DeleteObjectsReq  | 예    |
| resp | DeleteObjects 작업의 응답 | DeletObjectsResp  | 예    |


DeleteObjectsReq에는 다음의 멤버 함수가 포함되어 있습니다.

```cpp
// 객체 추가 및 버전 지정
void AddObjectVersion(const std::string& object, const std::string& version)
// 객체 추가, 멀티 버전 아님
void AddObject(const std::string& object)
```

DeleteObjectsResp에는 다음의 멤버 함수가 포함되어 있습니다.

```cpp
// 삭제 완료한 objects 정보 획득
std::vector<DeletedInfo> GetDeletedInfos() const

// 삭제 실패한 objects 정보 획득
std::vector<ErrorInfo> GetErrorinfos() const
```

해당 DeletedInfo 및 ErrorInfo의 구조는 다음과 같습니다.

```
struct DeletedInfo{
    std::string m_key; // object key
}
struct ErrorInfo{
    std::string m_key; // object key
    std::string m_code; // error code
    std::string m_message; // error message
}
```

### 보관된 객체 복구 

#### 기능 설명

아카이브 유형의 객체를 검색 및 액세스합니다.

#### 메소드 프로토타입

```cpp
CosResult PostObjectRestore(const PostObjectRestoreReq& req, PostObjectRestoreResp* resp)
```

#### 요청 예시

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "examplebucket-1250000000";
std::string object_name = "sevenyou";

{   
    qcloud_cos::PostObjectRestoreReq req(bucket_name, object_name);
    req.SetExiryDays(30);
    req.SetTier("Standard");
    qcloud_cos::PostObjectRestoreResp resp;
    qcloud_cos::CosResult result = cos.PostObjectRestore(req, &resp);
    // 호출 성공 시 resp의 멤버 함수를 호출하여 반환 내용 획득
    if (result.IsSucc()) {
        // ...
    } else {
        // CosResult의 멤버 함수를 호출하여 requestID 등의 오류 정보 출력 가능
    } 
}   
```

#### 매개변수 설명

| 매개변수 | 매개변수 설명                    |  유형                | 필수 입력 여부  |
| ---- | ----------------------------| ---------------------| ------|
| req  | PostObjectRestore 작업의 요청 | PostObjectRestoreReq | 예    |
| resp | PostObjectRestore 작업의 응답 | PostObjectRestoreResp| 예    |


PostObjectRestoreReq에는 다음의 멤버 함수가 포함되어 있습니다.

```
// 임시 사본의 만료 시간 설정
void SetExiryDays(uint64_t days);

// 열거 값: Expedited, Standard, Bulk. 기본값: Standard
void SetTier(const std::string& tier);
```

### 객체 URL 획득

#### 기능 설명

객체의 서명이 포함되지 않은 URL을 획득합니다.

#### 메소드 프로토타입

```cpp
std::string GetObjectUrl(const std::string& bucket, const std::string& object, bool https = true, const std::string& region = "");
```

#### 요청 예시

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "examplebucket-1250000000";
std::string object_name = "sevenyou";
//객체 https url을 획득합니다. region은 config.json에 설정된 리전입니다.
cos.GetObjectUrl(bucket_name, object_name);
//객체 http url을 획득합니다. region은 config.json에 설정된 리전입니다.
cos.GetObjectUrl(bucket_name, object_name, false);
//객체 https url을 획득합니다. region은 ap-shanghai입니다.
cos.GetObjectUrl(bucket_name, object_name, true, "ap-shanghai");  
```

#### 매개변수 설명

| 매개변수 | 매개변수 설명                 |  유형              | 필수 입력 여부  |
| ------ | ------------- | ------ | -------- |
| bucket | 버킷 이름      | string | 예       |
| object | 객체 이름        | string | 예       |
| https  | https 사용 여부 | bool   | 아니오       |
| region | 리전 이름        | string | 아니오       |



## 멀티파트 작업

다음은 객체의 멀티파트 업로드 작업 내용입니다.

- 객체 멀티파트 업로드: 멀티파트 업로드를 초기화하고 파트를 업로드하면 완료됩니다.
- 업로드된 멀티파트를 삭제합니다.


### 멀티파트 업로드 조회

#### 기능 설명

지정 버킷에서 진행 중인 멀티파트 업로드를 조회합니다(List Multipart Uploads).

#### 메소드 프로토타입

```cpp
CosResult CosAPI::ListMultipartUpload(const ListMultipartUploadReq& request, ListMultipartUploadResp* response)
```

#### 요청 예시

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "examplebucket-1250000000";
std::string object_name = "test_object";

qcloud_cos::ListMultipartUploadReq req(bucket_name, object_name);
qcloud_cos::ListMultipartUploadResp resp;
qcloud_cos::CosResult result = cos.ListMultipartUpload(req, &resp);

for (std::vector<qcloud_cos::Upload>::const_iterator itr = rst.begin(); itr != rst.end(); ++itr) {
    const qcloud_cos::Upload& upload = *itr;
    std::cout << "key = " << upload.m_key << ", uploadid= " << upload.m_uploadid << ", storagen class = " << upload.m_storage_class << ", m_initiated= " << upload.m_initiated << std::endl;
}   

// 호출 성공 시 resp의 멤버 함수를 호출하여 반환 내용 획득
if (result.IsSucc()) {
    // ...
} else {
    // CosResult의 멤버 함수를 호출하여 requestID 등의 오류 정보 출력 가능
} 
```

#### 매개변수 설명

| 매개변수 | 매개변수 설명                      |  유형                  | 필수 입력 여부  |
| ---- | ------------------------------| -----------------------| ------|
| req  | ListMultipartUpload 작업의 요청 | ListMultipartUploadReq | 예    |
| resp | ListMultipartUpload 작업의 응답 | ListMultipartUploadResp| 예    |


ListMultipartUploadReq 멤버 함수:

```
// 접두사가 Prefix인 Object key에 한정하여 반환합니다. Prefix를 사용하여 조회할 경우 반환되는 key에는 Prefix가 포함되어 있으므로 주의해야 합니다.
void SetPrefix(const std::string& prefix);

// 구분 문자는 하나의 부호로, Object 이름에 지정한 접두사가 포함되어 있으며 첫 번째로 출현한 delimiter 문자 사이의 Object가 하나의 그룹 요소인 common prefix가 됩니다. prefix가 없는 경우 경로의 시작점부터 시작됩니다.
void SetDelimiter(const std::string& delimiter);

// 규정된 반환 값의 인코딩 형식. 유효 값: url
void SetEncodingType(const std::string& encoding_type);

// upload-id-marker와 함께 사용합니다. upload-id-marker가 지정되지 않은 경우 ObjectName은 알파벳 순서가 key-marker보다 큰 항목이 열거되며, upload-id-marker가 지정된 경우 ObjectName은 알파벳 순서가 key-marker보다 큰 항목이 열거됩니다. ObjectName은 알파벳 순서가 key-marker와 동일하고 UploadID는 upload-id-marker보다 큰 항목이 열거됩니다.
void SetKeyMarker(const std::string& marker);

// 반환되는 최대 multipart 수량 설정. 유효한 값 범위: 1~1000, 기본값: 1000
void SetMaxUploads(const std::string& max_uploads);

// key-marker와 함께 사용합니다. key-marker가 지정되지 않은 경우 upload-id-marker가 생략되며, key-marker가 지정된 경우 ObjectName은 알파벳 순서가 key-marker보다 큰 항목이 열거됩니다. ObjectName은 알파벳 순서가 key-marker와 동일하고 UploadID는 upload-id-marker보다 큰 항목이 열거됩니다.
void SetUploadIdMarker(const std::string& upload_id_marker);
```

ListMultipartUploadResp 멤버 함수:

```
// Bucket에 있는 Object의 해당 메타 정보 획득
std::vector<Upload> GetUpload()；
// Bucket 이름
std::string GetName()；
// 인코딩 형식
std::string GetEncodingType() const；
// 기본적으로 UTF-8 이진법 순서로 열거되며, marker부터 시작해 모든 항목을 나열
std::string GetMarker() const；
// 해당 UploadId 값부터 시작해 항목을 나열
std::string GetUploadIdMarker() const；
// 반환 항목이 잘린 경우, 반환된 NextKeyMarker가 다음 항목의 시작점
std::string GetNextKeyMarker() const；
// 반환 항목이 잘린 경우, 반환된 UploadId가 다음 항목의 시작점
std::string GetNextUploadIdMarker() const；
// 반환되는 최대 multipart 수량. 유효한 값 범위: 0~1000
std::string GetMaxUploads () const；
// 응답 요청 항목이 잘렸는지 여부. Boolean 값: true, false
bool IsTruncated()；
// 반환되는 파일 접두사
std::string GetPrefix() const；
// 구분 문자 획득 
std::string GetDelimiter() const；
// Prefix부터 delimiter 사이의 동일 경로를 같은 종류로 분류하여 Common Prefix로 정의
std::vector<std::string> GetCommonPrefixes() const
```



### 멀티파트 업로드 초기화

#### 기능 설명

멀티파트 업로드를 초기화하고 해당하는 uploadId를 가져옵니다(Initiate Multipart Upload).

#### 메소드 프로토타입

```cpp
CosResult InitMultiUpload(const InitMultiUploadReq& req, InitMultiUploadResp* resp)
```

#### 요청 예시

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);
std::string bucket_name = "examplebucket-1250000000";
std::string object_name = "object_name";

qcloud_cos::InitMultiUploadReq req(bucket_name, object_name);
qcloud_cos::InitMultiUploadResp resp;
qcloud_cos::CosResult result = cos.InitMultiUpload(req, &resp);

std::string upload_id = "";
if (result.IsSucc()) {
    upload_id = resp.GetUploadId();
}
```

#### 매개변수 설명


| 매개변수 | 매개변수 설명                  |  유형              | 필수 입력 여부  |
| ---- | --------------------------| -------------------| ------|
| req  | InitMultiUpload 작업의 요청 | InitMultiUploadReq | 예    |
| resp | InitMultiUpload 작업의 응답 | InitMultiUploadResp | 예    |


InitMultiUploadReq의 멤버 함수는 다음과 같습니다.

```
// Cache-Control RFC 2616에서 정의한 캐시 정책. Object의 메타데이터로 저장
void SetCacheControl(const std::string& str);

// Content-Disposition RFC 2616에서 정의한 파일 이름. Object의 메타데이터로 저장
void SetContentDisposition(const std::string& str);

// Content-Encoding    RFC 2616에서 정의한 인코딩 형식. Object의 메타데이터로 저장-
void SetContentEncoding(const std::string& str);

// Content-Type    RFC 2616에서 정의한 콘텐츠 유형(MIME). Object의 메타데이터로 저장
void SetContentType(const std::string& str);

// Expires RFC 2616에서 정의한 만료시간. Object의 메타데이터로 저장
void SetExpires(const std::string& str);

// 사용자 정의한 헤더 정보 허용. Object의 메타데이터로 반환. 용량 제한: 2KB
void SetXCosMeta(const std::string& key, const std::string& value);

// x-cos-storage-class로 Object의 스토리지 등급 설정. 열거 값: STANDARD, STANDARD_IA, ARCHIVE
// 기본값: STANDARD
void SetXCosStorageClass(const std::string& storage_class);

// Object의 ACL 속성 정의. 유효 값: private, public-read
// 기본값: private
void SetXcosAcl(const std::string& str);

// 권한이 부여된 사용자에게 읽기 권한 부여. 형식: x-cos-grant-read: id=" ",id=" ".
// 서브 계정에 권한을 부여할 경우, id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"
// 루트 계정에 권한을 부여할 경우, id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"
void SetXcosGrantRead(const std::string& str);

// 권한이 부여된 사용자에게 읽기/쓰기 권한 부여. 형식: x-cos-grant-full-control: id=" ",id=" ".
// 서브 계정에 권한을 부여할 경우, id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>",
// 루트 계정에 권한을 부여할 경우, id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"
void SetXcosGrantFullControl(const std::string& str);

/// Server 측 암호화에 사용할 알고리즘 설정. 현재 AES256 지원
void SetXCosServerSideEncryption(const std::string& str);

```

해당 요청 실행을 완료한 뒤 반환되는 response에는 bucket, key, uploadId가 포함됩니다. 이는 멀티파트 업로드의 타깃 Bucket, Object 이름, 이후 멀티파트 업로드에 필요한 번호를 의미합니다.

InitMultiUploadResp의 멤버 함수는 다음과 같습니다.

```cpp
std::string GetBucket();
std::string GetKey();
std::string GetUploadId();

// Server 측 암호화 시 사용하는 알고리즘
std::string GetXCosServerSideEncryption();
```

<span id ="MULIT_UPLOAD_PART"></span>
###  멀티파트 업로드 

멀티파트 업로드합니다(Upload Part).

#### 메소드 프로토타입

```cpp
CosResult UploadPartData(const UploadPartDataReq& request, UploadPartDataResp* response)
```

#### 요청 예시

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "examplebucket-1250000000";
std::string object_name = "test_object";

// 첫 번째 파트 업로드
{
    std::fstream is("demo_5M.part1");
    qcloud_cos::UploadPartDataReq req(bucket_name, object_name, upload_id, is);
    req.SetPartNumber(1);
    // MD5 검증을 비활성화하고 req.TurnOnComputeConentMd5() 사용 활성화. 기본적으로 활성화되어 있음
    req.TurnOffComputeConentMd5();
    qcloud_cos::UploadPartDataResp resp;
    qcloud_cos::CosResult result = cos.UploadPartData(req, &resp);

    // 업로드 완료 시 멀티파트 번호와 반환되는 ETag를 기록해야 합니다.
    if (result.IsSucc()) {
        etags.push_back(resp.GetEtag());
        part_numbers.push_back(1);
    }
    is.close();
}

// 두 번째 파트 업로드
{
    std::fstream is("demo_5M.part2");
    qcloud_cos::UploadPartDataReq req(bucket_name, object_name,
                                      upload_id, is);
    req.SetPartNumber(2);
    qcloud_cos::UploadPartDataResp resp;
    qcloud_cos::CosResult result = cos.UploadPartData(req, &resp);

    // 업로드 완료 시 멀티파트 번호와 반환되는 ETag를 기록해야 합니다. 
    if (result.IsSucc()) {
        etags.push_back(resp.GetEtag());
        part_numbers.push_back(2);
    }
    is.close();
}
```

#### 매개변수 설명

| 매개변수 | 매개변수 설명                 |  유형             | 필수 입력 여부  |
| ---- | -------------------------| ------------------| ------|
| req  | UploadPartData 작업의 요청 | UploadPartDataReq | 예    |
| resp | UploadPartData 작업의 응답 | UploadPartDataResp| 예    |


UploadPartDataReq 구성 시, 요청의 APPID, Bucket, Object, 초기화 완료 후 획득하는 UploadId, 업로드 데이터 스트림을 지정해야 하며, 호출이 완료되면 스트림은 호출한 쪽에서 자체적으로 비활성화합니다.

```
UploadPartDataReq(const std::string& bucket_name,
                    const std::string& object_name, const std::string& upload_id,
                    std::istream& in_stream);

```

또한 요청에는 파트 번호가 필요하며, 해당 파트는 멀티파트 업로드 완료 시에도 사용됩니다.

```
void SetPartNumber(uint64_t part_number);

```

UploadPartDataResp의 멤버 함수는 다음과 같습니다.

```
/// Server 측 암호화 시 사용하는 알고리즘
std::string GetXCosServerSideEncryption();

```

### 멀티파트 복사

다른 객체를 한 파트로 복사합니다.

#### 메소드 프로토타입

```cpp
CosResult UploadPartCopyData(const UploadPartCopyDataReq& request,UploadPartCopyDataResp* response)
```

#### 요청 예시

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "examplebucket-1250000000";
std::string object_name = "test_object";

std::string upload_id;
std::vector<uint64_t> numbers;
std::vector<std::string> etags;
std::string etag1 = "", etag2 = "";
InitMultiUpload(cos, bucket_name, object_name, &upload_id);

// First part
qcloud_cos::UploadPartCopyDataReq req(bucket_name, object_name, upload_id, 1);
req.SetXCosCopySource("sevenyousouth-1251668577.cos.ap-guangzhou.myqcloud.com/seven_10G.tmp");
req.SetXCosCopySourceRange("bytes=0-1048576000");
qcloud_cos::UploadPartCopyDataResp resp;
qcloud_cos::CosResult result = cos.UploadPartCopyData(req, &resp);
if（result.IsSucc()) {
    etag1 = resp.GetEtag();
}
numbers.push_back(1);
etags.push_back(etag1);

// Second part
qcloud_cos::UploadPartCopyDataReq req2(bucket_name, object_name, upload_id, 2);                                                       
req2.SetXCosCopySource("sevenyoutest-7319456.cos.cn-north.myqcloud.com/sevenyou_2G_part");
req2.SetXCosCopySourceRange("bytes=1048576000-2097152000");
qcloud_cos::UploadPartCopyDataResp resp2;
qcloud_cos::CosResult result = cos.UploadPartCopyData(req2, &resp2);
if（result.IsSucc()) {
    etag2 = resp2.GetEtag();
}
numbers.push_back(2)；
etags.push_back(etag2);

CompleteMultiUpload(cos, bucket_name, object_name, upload_id, etags, numbers);
```

#### 매개변수 설명

| 매개변수 | 매개변수 설명                     |  유형                 | 필수 입력 여부  |
| ---- | -----------------------------| ----------------------| ------|
| req  | UploadPartCopyData 작업의 요청 | UploadPartCopyDataReq | 예    |
| resp | UploadPartCopyData 작업의 응답 | UploadPartCopyDataResp| 예    |


```cpp
/// 이번 멀티파트 복사의 ID 설정
void SetUploadId(const std::string& upload_id)
/// 이번 멀티파트 복사의 번호 설정
void SetPartNumber(uint64_t part_number)
/// 이번 멀티파트 복사의 원본 파일 URL 경로 설정. versionid 하위 리소스로 이전 버전 지정 가능
void SetXCosCopySource(const std::string& src)
/// 원본 파일의 바이트 범위 설정. 범위 값은 반드시 bytes=first-last 형식 사용
void SetXCosCopySourceRange(const std::string& range)
 /// Object가 지정된 시간 이후에 수정될 경우 작업을 수행하고, 그렇지 않을 경우 412 반환
void SetXCosCopySourceIfModifiedSince(const std::string& date)
/// Object가 지정된 시간 이후에 수정되지 않는 경우 작업을 수행하고, 그렇지 않을 경우 412 반환
void SetXCosCopySourceIfUnmodifiedSince(const std::string& date)
/// Object의 Etag가 사전 설정과 동일한 경우 작업을 수행하고, 그렇지 않을 경우 412 반환 
void SetXCosCopySourceIfMatch(const std::string& etag)
/// Object의 Etag가 사전 설정과 동일하지 않은 경우 작업을 수행하고, 그렇지 않을 경우 412 반환
void SetXCosCopySourceIfNoneMatch(const std::string& etag)
```

```
/// 반환되는 파일의 MD5 알고리즘 검증 값 획득
std::string GetEtag() const
/// 반환된 파일의 최종 수정 시간. 형식: GMT
std::string GetLastModified() const
/// Server 측 암호화 시 사용하는 알고리즘
std::string GetXCosServerSideEncryption() const
```

### 업로드된 파트 조회

#### 기능 설명

특정 멀티파트 업로드 작업에서 업로드된 파트를 조회합니다.

#### 메소드 프로토타입

```cpp
CosResult ListParts(const ListPartsReq& req, ListPartsResp* resp)
```

#### 요청 예시

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "examplebucket-1250000000";
std::string object_name = "test_object";

// uploadId는 InitMultiUpload 호출 후 획득
qcloud_cos::ListPartsReq req(bucket_name, object_name, upload_id);
req.SetMaxParts(1);                                                                                                                                                               
req.SetPartNumberMarker("1");
qcloud_cos::ListPartsResp resp;
qcloud_cos::CosResult result = cos.ListParts(req, &resp);

// 호출 성공 시 resp의 멤버 함수를 호출하여 반환 내용 획득
if (result.IsSucc()) {
    // ...
} else {
    // CosResult의 멤버 함수를 호출하여 requestID 등의 오류 정보 출력 가능
} 
```

#### 매개변수 설명

| 매개변수 | 매개변수 설명            |  유형        | 필수 입력 여부  |
| ---- | --------------------| -------------| ------|
| req  | ListParts 작업의 요청 | ListPartsReq | 예    |
| resp | ListParts 작업의 응답 | ListPartsResp| 예    |



ListPartsReq에는 다음의 멤버 함수가 포함되어 있습니다.

```
// 생성자, Bucket 이름, Object 이름, 멀티파트 업로드 ID
ListPartsReq(const std::string& bucket_name,                                                                                                                                      
             const std::string& object_name,
             const std::string& upload_id); 

// \brief 반환 값의 인코딩 방식 규정
void SetEncodingType(const std::string& encoding_type);

// \brief 한 번에 반환 가능한 최대 항목 수량. 설정하지 않을 경우 기본값: 1000
void SetMaxParts(uint64_t max_parts);

// \brief 기본적으로 UTF-8 이진법 순서로 열거되며, marker부터 시작해 모든 항목을 나열
void SetPartNumberMarker(const std::string& part_number_marker);

```

ListPartsResp에는 다음의 멤버 함수가 포함되어 있습니다.

```
// 멀티파트 업로드의 타깃 Bucket
std::string GetBucket();

// 반환 값의 인코딩 방식 규정
std::string GetEncodingType();

// Object 이름
std::string GetKey();

// 이번 멀티파트 업로드의 ID 표시
std::string GetUploadId();

// 이번 업로드 담당자의 정보 표시
Initiator GetInitiator();

// 해당 파트 소유자의 정보 표시
Owner GetOwner();

// 기본적으로 UTF-8 이진법 순서로 열거되며, marker부터 시작해 모든 항목을 나열
uint64_t GetPartNumberMarker();

// 파트별 정보 반환
std::vector<Part> GetParts();

// 반환 항목이 잘린 경우, 반환된 NextMarker가 다음 항목의 시작점
uint64_t GetNextPartNumberMarker();

// 해당 멀티파트의 스토리지 등급 표시. 열거 값: Standard, Standard_IA, ARCHIVE
std::string GetStorageClass();

// 한 번에 반환 가능한 최대 항목 수량
uint64_t GetMaxParts();

// 반환 항목이 잘렸는지 여부. Boolean 값: true, false
bool IsTruncated();

```

여기서 Part, Owner, Initiator의 정의는 다음과 같습니다.

```cpp
struct Initiator {
    std::string m_id; // 생성자의 고유 ID
    std::string m_display_name; // 생성자의 사용자 이름 설명
};

struct Owner {
    std::string m_id; // 사용자의 고유 ID
    std::string m_display_name; // 사용자 이름 설명
};

struct Part {
    uint64_t m_part_num; // 파트 번호
    uint64_t m_size; // 파트 크기, 단위: Byte
    std::string m_etag; // Object 파트의 MD5 알고리즘 검증 값
    std::string m_last_modified; // 파트의 최종 수정 시간
};

```

### 멀티파트 업로드 완료

#### 기능 설명

전체 파일의 멀티파트 업로드를 완료합니다.

#### 메소드 프로토타입

```cpp
CosResult CompleteMultiUpload(const CompleteMultiUploadReq& request, CompleteMultiUploadResp* response)
```

#### 요청 예시

```cpp
qcloud_cos::CompleteMultiUploadReq req(bucket_name, object_name, upload_id);
qcloud_cos::CompleteMultiUploadResp resp;
req.SetEtags(etags);
req.SetPartNumbers(part_numbers);

qcloud_cos::CosResult result = cos.CompleteMultiUpload(req, &resp);
```

#### 매개변수 설명

| 매개변수 | 매개변수 설명                     |  유형                  | 필수 입력 여부  |
| ---- | -----------------------------|------------------------| ------|
| req  | CompleteMultiUpload 작업의 요청 | CompleteMultiUploadReq | 예    |
| resp | CompleteMultiUpload 작업의 응답 | CompleteMultiUploadResp| 예    |


CompleteMultiUploadReq 구성 시, 요청의 APPID, Bucket, Object, 초기화 완료 후 획득하는 UploadId를 지정해야 합니다.

```
CompleteMultiUploadReq(const std::string& bucket_name,
                       const std::string& object_name, const std::string& upload_id)

```

또한, request에는 업로드하는 모든 파트의 번호와 ETag를 설정해야 합니다.

```
// 다음 방법을 호출할 때에는 번호와 ETag의 순서가 일대일로 대응되어야 함
void SetPartNumbers(const std::vector<uint64_t>& part_numbers);
void SetEtags(const std::vector<std::string>& etags) ;

// part_number와 ETag 조합 추가
void AddPartEtagPair(uint64_t part_number, const std::string& etag);

/// Server 측 암호화에 사용할 알고리즘 설정. 현재 AES256 지원
void SetXCosServerSideEncryption(const std::string& str);
```

CompleteMultiUploadResp의 반환 내용에는 Location, Bucket, Key, ETag가 포함됩니다. 이는 생성하는 Object의 공인 네트워크 액세스 도메인, 멀티파트 업로드의 타깃 Bucket, Object 이름, 병합 후 파일의 MD5 알고리즘 검증 값을 의미합니다. 다음의 멤버 함수를 호출하여 response 내용에 액세스할 수 있습니다.

```
std::string GetLocation();
std::string GetKey();
std::string GetBucket();
std::string GetEtag();

// Server 측 암호화 시 사용하는 알고리즘
std::string GetXCosServerSideEncryption();

```

### 멀티파트 업로드 중지

#### 기능 설명

멀티파트 업로드 작업을 중지하고 업로드된 파트를 삭제합니다.

#### 메소드 프로토타입

```cpp
CosResult AbortMultiUpload(const AbortMultiUploadReq& request, AbortMultiUploadResp* response)
```

#### 요청 예시

```cpp
qcloud_cos::AbortMultiUploadReq req(bucket_name, object_name, upload_id);
qcloud_cos::AbortMultiUploadResp resp;
qcloud_cos::CosResult result = cos.AbortMultiUpload(req, &resp);
```

#### 매개변수 설명

| 매개변수 | 매개변수 설명                   |  유형                | 필수 입력 여부  |
| ---- | ---------------------------|----------------------| ------|
| req  | AbortMultiUpload 작업의 요청 | AbortMultiUploadReq  | 예    |
| resp | AbortMultiUpload 작업의 응답 | AbortMultiUploadResp | 예    |


AbortMultiUploadReq는 구성 시 Bucket, Object, Upload_id를 지정해야 합니다.

```cpp
AbortMultiUploadReq(const std::string& bucket_name,
                    const std::string& object_name, const std::string& upload_id);
```

특별한 방법은 없으며, BaseResp의 멤버 함수를 호출하여 공용 헤더 내용을 획득할 수 있습니다.



## 고급 인터페이스(권장)

### 복합 업로드

#### 기능 설명

멀티파트 업로드의 각 인터페이스를 캡슐화해 동시에 업로드합니다.

#### 메소드 프로토타입

```cpp
CosResult MultiUploadObject(const MultiUploadObjectReq& request, MultiUploadObjectResp* response)
```

#### 요청 예시

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "examplebucket-1250000000";
std::string object_name = "exampleobject";
std::string local_file = "./test"

qcloud_cos::MultiUploadObjectReq req(bucket_name, object_name, local_file);
// Complete 인터페이스의 내부 chunk 액티브 보장. timeout 시간을 비교적 길게 설정하는 것을 권장
req.SetRecvTimeoutInms(1000 * 60);
qcloud_cos::MultiUploadObjectResp resp;
qcloud_cos::CosResult result = cos.MultiUploadObject(req, &resp);

// 호출 성공 시 resp의 멤버 함수를 호출하여 반환 내용 획득
if (result.IsSucc()) {
    // ...
} else {
    // CosResult의 멤버 함수를 호출하여 requestID 등의 오류 정보 출력 가능
} 
```

#### 매개변수 설명

| 매개변수 | 매개변수 설명                    |  유형                 | 필수 입력 여부  |
| ---- | ----------------------------|-----------------------| ------|
| req  | MultiUploadObject 작업의 요청 | MultiUploadObjectReq  | 예    |
| resp | MultiUploadObject 작업의 응답 | MultiUploadObjectResp | 예    |


MultiUploadObjectReq에는 다음의 멤버 함수가 포함되어 있습니다.

```cpp
// 파트 크기 설정. 1M 이하인 경우 1M로 계산되며, 5G 이상인 경우 5G로 계산됨
void SetPartSize(uint64_t bytes)
// 사용자 정의한 헤더 정보 허용. Object의 메타데이터로 반환. 용량 제한: 2KB 
void SetXCosMeta(const std::string& key, const std::string& value)
// Server 측 암호화에 사용할 알고리즘 설정. 현재 AES256 지원
void SetXCosServerSideEncryption(const std::string& str)
// 내부 스레드 풀 크기 설정
void SetThreadPoolSize(int size)
```

MultiUploadObjectResp에는 다음의 멤버 함수가 포함되어 있습니다.

```
std::string GetRespTag()
/// Server 측 암호화 시 사용하는 알고리즘 
std::string GetXCosServerSideEncryption() const
```

### 복합 다운로드

#### 기능 설명

동시에 Range로 다운로드합니다.

#### 메소드 프로토타입

```cpp
CosResult GetObject(const MultiGetObjectReq& request, 
MultiGetObjectResp* response)
```

#### 요청 예시

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "examplebucket-1250000000";
std::string object_name = "exampleobject";
std::string file_path = "./test";

qcloud_cos::MultiGetObjectReq req(bucket_name, object_name, file_path);  
qcloud_cos::MultiGetObjectResp resp;                                    
qcloud_cos::CosResult result = cos.GetObject(req, &resp); 

// 호출 성공 시 resp의 멤버 함수를 호출하여 반환 내용 획득
if (result.IsSucc()) {
    // ...
} else {
    // CosResult의 멤버 함수를 호출하여 requestID 등의 오류 정보 출력 가능
} 
```

#### 매개변수 설명

| 매개변수 | 매개변수 설명                 |  유형              | 필수 입력 여부  |
| ---- | -------------------------|--------------------| ------|
| req  | MultiGetObject 작업의 요청 | MultiGetObjectReq  | 예    |
| resp | MultiGetObject 작업의 응답 | MultiGetObjectResp | 예    |


MultiGetObjectReq에는 다음의 멤버 함수가 포함되어 있습니다.

```cpp
// 파트 크기 설정
void SetSliceSize(uint64_t bytes)
// 스레드 풀 크기 설정
void SetThreadPoolSize(int size)
```

MultiGetObjectResp에는 다음의 멤버 함수가 포함되어 있습니다.

```cpp
/// Server 측 암호화 시 사용하는 알고리즘
std::string GetXCosServerSideEncryption() const
```
