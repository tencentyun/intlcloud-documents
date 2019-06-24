## 서명 생성

### Sign 기능 설명

서명 생성

### 방법 프로토타입 1

```
static std::string Sign(const std::string& secret_id,
                        const std::string& secret_key,
                        const std::string& http_method,
                        const std::string& in_uri,
                        const std::map<std::string, std::string>& headers,
                        const std::map<std::string, std::string>& params);
```

#### 매개변수 설명

| 매개변수 이름 | 매개변수 설명 | 유형 |
| ----------- | ----------------------------------------------------- | ------------------------ |
| secret_id   | 개발자가 소유한 프로젝트 신분 식별 ID, 신분 검증에 사용합니다             | String                   |
| secret_key  | 개발자가 소유한 프로젝트 ID 키                              | String                   |
| http_method | HTTP 방법, POST/GET/HEAD/PUT 등, 대소문자를 구분하지 않습니다 | String                   |
| in_uri      | HTTP uri                                              | String                   |
| headers     | HTTP header의 키 값 쌍                                  | map&lt;string,string&gt; |
| params      | HTTP params의 키 값 쌍                                  | map&lt;string,string&gt; |

#### 반환 결과 설명

서명 반환, 지정한 유효 기간 내에 (CosSysConfig 설정 사용, 기본값 60s) 사용할 수 있으며, 빈 열이 반환되면 서명이 실패했음을 나타냅니다.

##### 방법 프로토타입 2

```
static std::string Sign(const std::string& secret_id,
                        const std::string& secret_key,
                        const std::string& http_method,
                        const std::string& in_uri,
                        const std::map<std::string, std::string>& headers,
                        const std::map<std::string, std::string>& params,
                        uint64_t start_time_in_s,
                        uint64_t end_time_in_s);
```

#### 매개변수 설명

| 매개변수 이름 | 매개변수 설명 | 유형 |
| --------------- | ---------------------------------------------------- | ------------------------- |
| secret_id       | 개발자가 소유한 프로젝트 신분 식별 ID, 신분 검증에 사용합니다            | String                    |
| secret_key      | 개발자가 소유한 프로젝트 ID 키                             | String                    |
| http_method     | HTTP 방법, POST/GET/HEAD/PUT 등, 대소문자를 구분하지 않습니다 | String                    |
| in_uri          | HTTP uri                                             | String                    |
| headers         | HTTP header의 키 값 쌍                                 | map&lt;string,string&gt; |
| params          | HTTP params의 키 값 쌍                                 | map&lt;string,string&gt; |
| start_time_in_s | 서명 적용 시작 시간                                   | uint64_t                  |
| end_time_in_s   | 서명 적용 종료 시간                                   | uint64_t                  |

#### 반환 결과 설명

String, 서명 반환은 지정한 유효 기간 내에 사용할 수 있으며, 빈 열이 반환되면 서명이 실패했음을 나타냅니다.

## Service/Bucket/Object 작업

Service/Bucket/Object와 관련된 모든 방법 프로토타입은 모두 다음과 같이 표시됩니다.

```
CosResult Operator(BaseReq, BaseResp)
```

### CosResult

CosResult는 요청에 오류가 발생할 때 반환된 오류 코드와 해당 오류 정보를 캡슐화합니다. 자세한 정보는 [오류 코드](/document/product/436/7730 "오류 코드")를 참조하십시오.

>!SDK 내부에 캡슐화된 요청은 모두 CosResult 객체를 반환할 수 있고, 매번 호출이 완료된 후, IsSucc() 멤버 함수를 사용하여 호출이 성공했는지 여부를 확인합니다.

#### 멤버 함수

| 함수                      | 함수 설명                                                     |
| ------------------------- | ------------------------------------------------------------ |
| bool isSucc()             | 이번 호출의 성공 또는 실패를 반환합니다.<br>false 반환 시: 후속 CosResult 멤버 함수는 의미가 있습니다. <br>True 반환 시: OperatorResp에서 특정 반환 콘텐츠를 획득할 수 있습니다. |
| string GetErrorCode()     | COS가 반환한 오류 코드를 획득하여, 오류 코드 시나리오를 확인합니다.                    |
| string GetErrorMsg()      | 특정 오류 정보를 포함합니다.                                         |
| string GetResourceAddr()  | 리소스 주소, 버킷 주소 또는 객체 주소입니다.                        |
| string GetXCosRequestId() | 요청 발송 시, 서버가 자동으로 요청에 대한 고유 ID를 생성합니다.<br>문제가 발생할 때 request-id는 COS가 문제를 더 빨리 찾을 수 있도록 도와줍니다. |
| string GetXCosTraceId() | 요청에 오류가 발생하면 서버는 이 오류에 대해 고유한 ID를 자동으로 생성합니다.<br>사용 시 문제가 발생하면, trace-id는 COS가 문제를 더 빨리 찾을 수 있도록 도와줍니다.<br>요청 시 문제가 발생하면, trace-id와 request-id는 일대일로 대응합니다.
| string GetErrorInfo() | SDK 내부 오류 정보를 획득합니다.|
| int GetHttpStatus() | HTTP 상태 코드를 획득합니다.|

#### BaseReq/BaseResp

BaseReq, BaseResp는 요청 및 반환을 캡슐화합니다. 호출자는 다른 작업 유형에 따라 다른 OperatorReq(예: 나중에 설명할 GetBucketReq)를 생성하고 OperatorReq의 내용을 기입하면 됩니다.
함수가 반환된 후, BaseResp에 해당하는 멤버 함수를 호출하여 요청 결과를 얻습니다.

- Request의 경우 특별한 설명이 없으면 Request의 생성자만 주의하면 됩니다.
- Response의 경우, 모든 방법의 Response는 모두 공통 반환 헤더를 획득하는 멤버 함수가 있습니다.
  Response의 멤버 함수는 다음과 같으며, 구체 필드 의미는 [공통 응답 헤더](/document/product/436/7729 "공통 응답 헤더")를 참조하십시오. 여기서는 자세히 설명하지 않습니다.

```
uint64_t GetContentLength();
std::string GetContentType();
std::string GetEtag();
std::string GetConnection();
std::string GetDate();
std::string GetServer();
std::string GetXCosRequestId();
std::string GetXCosTraceId();
```

## Bucket 작업

### Get Bucket

#### 기능 설명

Get Bucket 요청은 List Object 요청과 동일하며, 해당 버킷 아래의 부분 또는 모든 객체를 나열할 수 있습니다. 해당 요청을 시작하려면 읽기 권한이 있어야 합니다. 관련 API 문서는 [Get Bucket](/document/product/436/7734)을 참조하십시오.

#### 방식 프로토타입

```cpp
CosResult GetBucket(const GetBucketReq& req, GetBucketResp* resp);
```

#### 매개변수 설명

| 매개변수 | 매개변수                                |
| ---- | --------------------------------------- |
| req  | GetBucketReq , GetBucket 작업의 요청입니다.   |
| resp | GetBucketResp , GetBucket 작업의 반환입니다. |

GetBucketResp는 다음 멤버 함수를 제공하며, Get Bucket으로 반환된 XML 형식의 구체 내용을 획득하는 데 사용됩니다.

```C++
std::vector<Content> GetContents();
std::string GetName();
std::string GetPrefix();
std::string GetMarker();
uint64_t GetMaxKeys();
bool IsTruncated();
std::vector<std::string> GetCommonPrefixes();
```

그 중 Content의 의미는 다음과 같습니다.

```
struct Content {
    std::string m_key; // 객체의 Key
    std::string m_last_modified; // 객체 마지막 수정 시간
    std::string m_etag; // 파일의 MD-5 알고리즘 검증값
    std::string m_size; // 파일 크기, 단위는 Byte
    std::vector<std::string> m_owner_ids; // 버킷 소유자 정보
    std::string m_storage_class; // 객체의 저장 유형, 열거 값: STANDARD, STANDARD_IA
};
```

#### 예시

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "cpp_sdk_v5-123456789";

// GetBucketReq의 생성자는 bucket_name을 입력해야 합니다
qcloud_cos::GetBucketReq req(bucket_name);
qcloud_cos::GetBucketResp resp;
qcloud_cos::CosResult result = cos.GetBucket(req, &resp);

// 호출에 성공할 경우 resp의 멤버 함수를 호출하여 반환 내용을 획득합니다
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

### Put Bucket

#### 기능 설명

Put Bucket API 요청은 지정된 계정 아래에 버킷을 생성할 수 있습니다. 해당 API는 익명 요청을 지원하지 않으므로 Authorization 서명 인증이 있는 요청을 사용해야 새 버킷을 생성할 수 있습니다. 버킷을 생성한 사용자는 기본으로 버킷의 소유자입니다. 관련 API 문서는 [Put Bucket](/document/product/436/7738)을 참조하십시오.

#### 방식 프로토타입

```cpp
CosResult PutBucket(const PutBucketReq& req, PutBucketResp* resp);
```

#### 매개변수 설명

| 매개변수 | 매개변수 설명                              |
| ---- | ------------------------------------- |
| req  | PutBucketReq, PutBucket 작업의 요청입니다.  |
| resp | PutBucketResp, PutBucket 작업의 반환입니다. |

PutBucketReq는 다음과 같은 멤버 함수를 제공합니다.

```C++
// Bucket의 ACL 속성 정의, 유효 값: private,public-read-write,public-read
// 기본값: private
void SetXCosAcl(const std::string& str);

// 관한 부여받은 자에게 읽기 권한을 부여합니다. 형식: x-cos-grant-read: id=" ",id=" ".
// 서브 계정에 권한을 부여해야 할 경우, id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"
// 루트 계정에 권한을 부여해야 할 경우, id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"
void SetXCosGrantRead(const std::string& str);

// 권한 부여받은 자에게 쓰기 권한을 부여합니다. 형식: x-cos-grant-write: id=" ",id=" "./
// 서브 계정에 권한을 부여해야 할 경우, id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>",
// 루트 계정에 권한을 부여해야 할 경우, id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"
void SetXCosGrantWrite(const std::string& str);

// 권한 부여받은 자에게 쓰기 권한을 부여합니다. 형식: x-cos-grant-full-control: id=" ",id=" ".
// 서브 계정에 권한을 부여해야 할 경우, id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>",
// 루트 계정에 권한을 부여해야 할 경우, id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"
void SetXCosGrantFullControl(const std::string& str);
```

#### 예시

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "cpp_sdk_v5-123456789";

qcloud_cos::PutBucketReq req(bucket_name);
qcloud_cos::PutBucketResp resp;
qcloud_cos::CosResult result = cos.PutBucket(req, &resp);

// 호출에 성공할 경우 resp의 멤버 함수를 호출하여 반환 내용을 획득합니다
if (result.IsSucc()) {
    // ...
} else {
    // 버킷 생성에 실패하면, CosResult의 멤버 함수를 호출하여 requestID 등의 오류 정보를 출력할 수 있습니다.
}
```

### Delete Bucket

#### 기능 설명

Delete Bucket API 요청은 지정된 계정에서 버킷을 삭제할 수 있습니다. 삭제하기 전에 요청 버킷의 콘텐츠는 비어 있어야 합니다. 버킷 내의 정보를 삭제해야만 버킷 자체를 삭제할 수 있습니다. 관련 API 문서는 [Delete Bucket](/document/product/436/7732)을 참조하십시오.

#### 방식 프로토타입

```cpp
CosResult DeleteBucket(const DeleteBucketReq& req, DeleteBucketResp* resp);
```

#### 매개변수 설명

| 매개변수 | 매개변수 설명                                   |
| ---- | ------------------------------------------ |
| req  | DeleteBucketReq, DeleteBucket 작업의 요청입니다.   |
| resp | DeletBucketResp, DeletBucket 작업의 반환입니다. |

#### 예시

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "cpp_sdk_v5-123456789";

// DeleteBucketReq의 생성자는 bucket_name을 입력해야 합니다
qcloud_cos::DeleteBucketReq req(bucket_name);
qcloud_cos::DeleteBucketResp resp;
qcloud_cos::CosResult result = cos.DeleteBucket(req, &resp);

// 호출에 성공할 경우 resp의 멤버 함수를 호출하여 반환 내용을 획득합니다
if (result.IsSucc()) {
    // ...
} else {
    // 버킷 삭제에 실패하면, CosResult의 멤버 함수를 호출하여 requestID 등의 오류 정보를 출력할 수 있습니다.
}
```

### Put Bucket Replication

#### 기능 설명

Put Bucket Replication 요청은 버전 관리가 활성화된 버킷에 replication 구성을 추가하는 데 사용됩니다. 만일 버킷에 이미 복제 구성이 있는 경우, 해당 요청은 기존의 구성을 대체합니다.

#### 방식 프로토타입

```cpp
CosResult PutBucketReplication(const DPutBucketReplicationReq& req, PutBucketReplicationResp* resp);
```

#### 매개변수 설명

| 매개변수 | 매개변수 설명                                                    |
| ---- | ----------------------------------------------------------- |
| req  | PutBucketReplicationReq, PutBucketReplication 작업의 요청입니다.  |
| resp | PutBucketReplicationResp, PutBucketReplication 작업의 반환입니다. |

```
// Replication을 시작한 사람의 ID를 설정합니다. role 형식: qcs::cam::uin/[UIN]:uin/[Subaccount]
void SetRole(const std::string& role);

// ReplicationRule 추가
void AddReplicationRule(const ReplicationRule& rule);

// ReplicationRules 설정
void SetReplicationRule(const std::vector<ReplicationRule>& rules);
```

그 중 ReplicationRule의 정의는 다음과 같습니다.

```
struct ReplicationRule {
    bool m_is_enable; // 해당 Rule의 적용 여부
    std::string m_id; // 비필수 선택 필드, 구체 Rule의 이름 표시에 사용합니다
    std::string m_prefix; // 접두사 매칭 정책, 중첩할 수 없으며 중첩 시 오류가 반환됩니다. 접두사 매칭 루트 디렉터리는 비어 있습니다.
    std::string m_dest_bucket; // 대상 버킷 표시, 리소스 식별자: qcs:id/0:cos:[region]:appid/[AppId]:[bucketname]
    std::string m_dest_storage_class; // 비필수 선택 필드, 스토리지 클래스, 열거형 값: Standard, Standard_IA; 비어 있으면 원래 버킷 레벨을 유지하는 것을 의미합니다

    ReplicationRule();
    ReplicationRule(const std::string& prefix,
                    const std::string& dest_bucket,
                    const std::string& storage_class = "",
                    const std::string& id = "",
                    bool is_enable = true);
};
```

#### 예시

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "cpp_sdk_v5-123456789";

// PutBucketReplicationReq의 생성자는 bucket_name을 입력해야 합니다
qcloud_cos::PutBucketReplicationReq req(bucket_name);
req.SetRole("qcs::cam::uin/***:uin/****");
qcloud_cos::ReplicationRule rule("sevenyou_10m", "qcs:id/0:cos:cn-south:appid/***:sevenyousouthtest", "", "RuleId_01", true);
req.AddReplicationRule(rule)

qcloud_cos::PutBucketReplicationResp resp;
qcloud_cos::CosResult result = cos.PutBucketReplication(req, &resp);

// 호출에 성공할 경우 resp의 멤버 함수를 호출하여 반환 내용을 획득합니다
if (result.IsSucc()) {
    // ...
} else {
    // 크로스 지역 복제 설정에 실패하면, CosResult의 멤버 함수를 호출하여 requestID 등의 오류 정보를 출력할 수 있습니다.
}
```

### Get Bucket Replication

#### 기능 설명

Get Bucket Replication API 요청은 읽기 버킷에서 사용자의 도메인 간 구성 정보 복제를 구현합니다.

#### 방식 프로토타입

```cpp
CosResult GetBucketReplication(const DGetBucketReplicationReq& req, GetBucketReplicationResp* resp);
```

#### 매개변수 설명

| 매개변수 | 매개변수 설명                                                    |
| ---- | ----------------------------------------------------------- |
| req  | GetBucketReplicationReq, GetBucketReplication 작업의 요청입니다.  |
| resp | GetBucketReplicationResp, GetBucketReplication 작업의 반환입니다. |

```
// Replication를 시작한 사람의 ID를 획득합니다
std::string GetRole();

// ReplicationRules를 획득합니다. ReplicationRule 정의는 Put Bucket Replication을 참조하십시오
std::vector<ReplicationRule> GetRules();
```

#### 예시

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "cpp_sdk_v5-123456789";

// GetBucketReplicationReq의 생성자는 bucket_name을 입력해야 합니다
qcloud_cos::GetBucketReplicationReq req(bucket_name);
qcloud_cos::GetBucketReplicationResp resp;
qcloud_cos::CosResult result = cos.GetBucketReplication(req, &resp);

// 호출에 성공할 경우 resp의 멤버 함수를 호출하여 반환 내용을 획득합니다
if (result.IsSucc()) {
    // ...
} else {
    // 크로스 지역 복제 설정 획득에 실패하면, CosResult의 멤버 함수를 호출하여 requestI 등의 오류 정보를 출력할 수 있습니다.
}
```

### Delete Bucket Replication

#### 기능 설명

Delete Bucket Replication API 요청은 버킷의 사용자에서 크로스 지역 복제 구성 삭제를 실시합니다.

#### 방식 프로토타입

```cpp
CosResult DeleteBucketReplication(const DDeleteBucketReplicationReq& req, DeleteBucketReplicationResp* resp);
```

#### 매개변수 설명

| 매개변수 | 매개변수 설명                                                     |
| ---- | ------------------------------------------------------------ |
| req  | DeleteBucketReplicationReq, DeleteBucketReplication 작업의 요청입니다.  |
| resp | DeleteBucketReplicationResp, DeleteBucketReplication 작업의 반환입니다. |

#### 예시

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "cpp_sdk_v5-123456789";

// DeleteBucketReplicationReq의 생성자는 bucket_name을 입력해야 합니다
qcloud_cos::DeleteBucketReplicationReq req(bucket_name);
qcloud_cos::DeleteBucketReplicationResp resp;
qcloud_cos::CosResult result = cos.DeleteBucketReplication(req, &resp);

// 호출에 성공할 경우 resp의 멤버 함수를 호출하여 반환 내용을 획득합니다
if (result.IsSucc()) {
    // ...
} else {
    // 크로스 지역 복제 설정 삭제가 실패하면, CosResult의 멤버 함수를 호출하여 requestID 등의 오류 정보를 출력할 수 있습니다.
}
```

### Put Bucket Lifecycle

#### 기능 설명

COS는 사용자가 수명 주기 구성의 방식으로 버킷의 객체 수명 주기를 관리할 수 있도록 지원합니다. 수명 주기 구성에는 한 세트의 객체 규칙에 적용될 한 개 또는 여러 개의 규칙 그룹이 포함됩니다(그 중 각 규칙은 COS에 대한 작업을 정의).
이러한 작업은 다음 두 가지 유형으로 구분됩니다.

- 전환 작업: 객체를 다른 스토리지 클래스로 전환할 시간을 정의합니다. 예를 들어, 객체 생성 30일 후에 STANDARD_IA(IA, 액세스 빈도가 낮을 경우 적용) 소토리지 클래스로 전환하도록 선택할 수 있습니다.
- 만료 작업: 객체의 만료 시간을 지정합니다. COS는 자동으로 사용자 대신 만료된 객체를 삭제합니다.
  Put Bucket Lifecycle은 버킷에 대한 새로운 수명 주기 구성을 작성하는 데 사용됩니다. 해당 버킷에 수명 주기가 이미 설정되었으며, 해당 API를 사용하여 새 구성을 작성하는 동시에 원래 구성을 겹쳐 쓰게 됩니다. 관련 API 문서는 [Put Bucket Lifecycle](/document/product/436/8280)을 참조하십시오.

#### 방식 프로토타입

```cpp
CosResult PutBucketLifecycle(const DPutBucketLifecycleReq& req, PutBucketLifecycleResp* resp);
```

#### 매개변수 설명

| 매개변수 | 매개변수 설명                                                |
| ---- | ------------------------------------------------------- |
| req  | PutBucketLifecycleReq, PutBucketLifecycle 작업의 요청입니다.  |
| resp | PutBucketLifecycleResp, PutBucketLifecycle 작업의 반환입니다. |

```
// LifecycleRule 추가
void AddRule(const LifecycleRule& rule)

// LifecycleRule 설정
void SetRule(const std::vector<LifecycleRule>& rules)
```

LifecycleRule의 정의는 다음과 같이 비교적 복잡합니다.

```
struct LifecycleTag {
    std::string key;
    std::string value;
};

class LifecycleFilter {
public:
    LifecycleFilter();

    std::string GetPrefix();
    std::vector<LifecycleTag> GetTags();

    void SetPrefix(const std::string& prefix);
    void SetTags(const std::vector<LifecycleTag>& tags);
    void AddTag(const LifecycleTag& tag);

    bool HasPrefix();
    bool HasTags();

private:
    std::string m_prefix; // 규칙이 적용되는 접두사를 지정합니다. 접두사에 매칭되는 객체는 해당 규칙의 영향을 받습니다. Prefix는 최대 1개만 있을 수 있습니다
    std::vector<LifecycleTag> m_tags; // 태그, Tag는 0개 또는 여러 개가 있을 수 있습니다
};

class LifecycleTransition {
public:
    LifecycleTransition();

    uint64_t GetDays();
    std::string GetDate();
    std::string GetStorageClass();

    void SetDays(uint64_t days);
    void SetDate(const std::string& date);
    void SetStorageClass(const std::string& storage_class);

    bool HasDays();
    bool HasDate();
    bool HasStorageClass();

private:
    // 같은 규칙에 동시에 Days 및 Date를 함께 사용할 수 없습니다
    uint64_t m_days; // 규칙에 대응하는 동작의 객체의 마지막 수정일 만료 후 며칠 동안 작업되는지를 표시합니다. 유효값은 음수가 아닌 정수입니다
    std::string m_date; // 규칙에 대응하는 동작이 언제 작업되는지를 표시합니다
    std::string m_storage_class; // 객체가 전환 저장될 대상 스토리지 클래스 지정, 열거형 값: Standard_IA
};

class LifecycleExpiration {
public:
    LifecycleExpiration();

    uint64_t GetDays();
    std::string GetDate();
    bool IsExpiredObjDelMarker();

    void SetDays(uint64_t days);
    void SetDate(const std::string& date);
    void SetExpiredObjDelMarker(bool marker);

    bool HasDays();
    bool HasDate();
    bool HasExpiredObjDelMarker();

private:
    // 같은 규칙에 동시에 Days 및 Date를 함께 사용할 수 없습니다
    uint64_t m_days; // 규칙에 대응하는 동작의 객체의 마지막 수정일 만료 후 작업 일수를 표시합니다. 유효값은 양의 정수입니다
    std::string m_date; // 규칙에 대응하는 동작이 언제 작업되는지를 표시합니다
    bool m_expired_obj_del_marker; // 만료 객체 삭제 여부 표시, 열거혀 값 true, false
};

class LifecycleNonCurrTransition {
public:
    LifecycleNonCurrTransition();

    uint64_t GetDays();
    std::string GetStorageClass();

    void SetDays(uint64_t days);  
    void SetStorageClass(const std::string& storage_class);

    bool HasDays();
    bool HasStorageClass();

private:
    uint64_t m_days; // 규칙에 대응하는 동작의 객체의 마지막 수정일 만료 후 며칠 동안 작업되는지를 표시합니다. 유효값은 음수가 아닌 정수입니다
    std::string m_storage_class; // 객체가 전환 저장될 대상 스토리지 클래스 지정, 열거형 값: Standard_IA
};

class LifecycleNonCurrExpiration {
public:
    LifecycleNonCurrExpiration();

    uint64_t GetDays();

    void SetDays(uint64_t days);

    bool HasDays();

private:
    uint64_t m_days; // 규칙에 대응하는 동작의 객체의 마지막 수정일 만료 후 작업 일수를 표시합니다. 유효값은 양의 정수입니다
};

struct AbortIncompleteMultipartUpload {
    uint64_t m_days_after_init; // 멀티파트 업로드 시작 후 며칠 내에 업로드를 완료해야 하는지 표시합니다
};

class LifecycleRule {
public:
    LifecycleRule();

    void SetIsEnable(bool is_enable);
    void SetId(const std::string& id);
    void SetFilter(const LifecycleFilter& filter);
    void AddTransition(const LifecycleTransition& rh);
    void SetExpiration(const LifecycleExpiration& rh);
    void SetNonCurrTransition(const LifecycleNonCurrTransition& rh);
    void SetNonCurrExpiration(const LifecycleNonCurrExpiration& rh);
    void SetAbortIncompleteMultiUpload(const AbortIncompleteMultipartUpload& rh);

    bool IsEnable();
    std::string GetId();
    LifecycleFilter GetFilter();
    std::vector<LifecycleTransition> GetTransitions();
    LifecycleExpiration GetExpiration();
    LifecycleNonCurrTransition GetNonCurrTransition();
    LifecycleNonCurrExpiration GetNonCurrExpiration();
    AbortIncompleteMultipartUpload GetAbortIncompleteMultiUpload();

    bool HasIsEnable();
    bool HasId();
    bool HasFilter();
    bool HasExpiration();
    bool HasNonCurrTransition();
    bool HasNonCurrExpiration();
    bool HasAbortIncomMultiUpload();

private:
    bool m_is_enable; // 규칙 적용 여부
    std::string m_id; // 규칙 ID
    LifecycleFilter m_filter; // 필터, 규칙 적용의 객체 범위를 지정하는 데 사용합니다
    std::vector<LifecycleTransition> m_transitions; // 전환 작업
    LifecycleExpiration m_expiration; // 만료 작업
    LifecycleNonCurrTransition m_non_curr_transition; // 현재 버전이 아닌 전환 작업
    LifecycleNonCurrExpiration m_non_curr_expiration; // 현재 버전이 아닌 만료 작업
    AbortIncompleteMultipartUpload m_abort_multi_upload; // 멀티파트 업로드 실행의 최장 허용 시간을 설정합니다
}
```

#### 예시

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "cpp_sdk_v5-123456789";

// PutBucketLifecycleReq의 생성자는 bucket_name을 입력해야 합니다
qcloud_cos::PutBucketLifecycleReq req(bucket_name);
// 규칙 1 설정
{
    qcloud_cos::LifecycleRule rule;
    rule.SetIsEnable(true);
    rule.SetId("lifecycle_rule00");
    qcloud_cos::LifecycleFilter filter;
    filter.SetPrefix("sevenyou_e1");
    rule.SetFilter(filter);
    qcloud_cos::LifecycleExpiration expiration;
    expiration.SetDays(1);
    rule.SetExpiration(expiration);
    req.AddRule(rule);
}

// 규칙 2 설정
{
    qcloud_cos::LifecycleRule rule;
    rule.SetIsEnable(true);
    rule.SetId("lifecycle_rule01");
    qcloud_cos::LifecycleFilter filter;
    filter.SetPrefix("sevenyou_e2");
    rule.SetFilter(filter);
    qcloud_cos::LifecycleExpiration expiration;
    expiration.SetDays(3);
    rule.SetExpiration(expiration);
    req.AddRule(rule);
}

qcloud_cos::PutBucketLifecycleResp resp;
qcloud_cos::CosResult result = cos.PutBucketLifecycle(req, &resp);

// 호출에 성공할 경우 resp의 멤버 함수를 호출하여 반환 내용을 획득합니다
if (result.IsSucc()) {
    // ...
} else {
    // 수명 주기 설정에 실패하면, CosResult의 멤버 함수를 호출하여 requestID 등의 오류 정보를 출력할 수 있습니다.
}
```

### Get Bucket Lifecycle

#### 기능 설명

Get Bucket Lifecycle은 버킷에 대한 수명 주기 구성을 조회하는 데 사용됩니다. 해당 버킷에 설정된 수명 주기가 없으면, NoSuchLifecycleConfiguration을 반환합니다. 관련 API 문서는 [Get Bucket Lifecycle](/document/product/436/8278)을 참조하십시오.

#### 방식 프로토타입

```cpp
CosResult GetBucketLifecycle(const GetBucketLifecycleReq& req, GetBucketLifecycleResp* resp);
```

#### 매개변수 설명

| 매개변수 | 매개변수 설명                                                |
| ---- | ------------------------------------------------------- |
|  req  | GetBucketLifecycleReq, GetBucketLifecycle 작업의 요청입니다.  |
| resp | GetBucketLifecycleResp, GetBucketLifecycle 작업의 반환입니다. |

```
// LifecycleRules 획득
std::vector<LifecycleRule> GetRules()
```

그 중, LifecycleRule 정의는 Put Bucket Lifecycle을 참조하십시오.

#### 예시

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "cpp_sdk_v5-123456789";

// GetBucketLifecycleReq의 구조 함수에 bucket_name을 입력해야 합니다
qcloud_cos::GetBucketLifecycleReq req(bucket_name);
qcloud_cos::GetBucketLifecycleResp resp;
qcloud_cos::CosResult result = cos.GetBucketLifecycle(req, &resp);

// 호출에 성공할 경우 resp의 멤버 함수를 호출하여 반환 내용을 획득합니다
if (result.IsSucc()) {
    // ...
} else {
    // 수명 주기 구성 획득에 실패하면, CosResult의 멤버 함수를 호출하여 requestID 등의 오류 정보를 출력할 수 있습니다.
}
```

### Delete Bucket Lifecycle

#### 기능 설명

Delete Bucket Lifecycle은 버킷에 대한 수명 주기 구성을 삭제하는 데 사용됩니다. 해당 버킷에 설정된 수명 주기가 없으면, NoSuchLifecycleConfiguration을 반환합니다. 관련 API 문서는 [Delete Bucket Lifecycle](/document/product/436/8284)을 참조하십시오.

#### 방식 프로토타입

```cpp
CosResult DeleteBucketLifecycle(const DeleteBucketLifecycleReq& req, DeleteBucketLifecycleResp* resp);
```

#### 매개변수 설명

| 매개변수 | 매개변수 설명                                                     |
| ---- | ------------------------------------------------------------ |
| req  | DeleteBucketLifecycleReq, DeleteBucketLifecycle 작업의 요청입니다. |
| req  | DeleteBucketLifecycleResp, DeleteBucketLifecycle 작업의 반환입니다. |

#### 예시

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "cpp_sdk_v5-123456789";

// DeleteBucketLifecycleReq의 생성자는 bucket_name을 입력해야 합니다
qcloud_cos::DeleteBucketLifecycleReq req(bucket_name);
qcloud_cos::DeleteBucketLifecycleResp resp;
qcloud_cos::CosResult result = cos.DeleteBucketLifecycle(req, &resp);

// 호출에 성공할 경우 resp의 멤버 함수를 호출하여 반환 내용을 획득합니다
if (result.IsSucc()) {
    // ...
} else {
    // 수명 주기 구성 삭제에 실패하면, CosResult의 멤버 함수를 호출하여 requestID 등의 오류 정보를 출력할 수 있습니다.
}
```

### Put Bucket CORS

#### 기능 설명

CPut Bucket CORS API는 버킷에 대한 CORS 권한을 요청하는 데 사용되며, XML 형식의 구성 파일을 가져와서 구성할 수 있습니다. 파일 크기 제한은 64KB입니다. 기본으로 버킷의 소유자는 직접 해당 API를 사용할 권한이 있으며, 버킷 소유자는 해당 권한을 기타 사용자에게 부여할 수도 있습니다. 관련 API 문서는 [Put Bucket CORS](/document/product/436/8279)를 참조하십시오.

#### 방식 프로토타입

```cpp
CosResult PutBucketCORS(const DPutBucketCORSReq& req, PutBucketCORSResp* resp);
```

#### 매개변수 설명

| 매개변수 | 매개변수 설명                                      |
| ---- | --------------------------------------------- |
| req  | PutBucketCORSReq, PutBucketCORS 작업의 요청입니다.  |
| req  | PutBucketCORSResp, PutBucketCORS 작업의 반환입니다. |

```
// CORSRule 추가
void AddRule(const CORSRule& rule);

// CORSRule 설정
void SetRules(const std::vector<CORSRule>& rules)


```

CORSRule 정의는 다음과 같습니다.

```
struct CORSRule {
    std::string m_id; // 구성 규칙의 ID, 선택 가능
    std::string m_max_age_secs; // OPTIONS 요청이 얻은 결과의 유효기간 설정
    std::vector<std::string> m_allowed_headers; // OPTIONS 요청 발송 시 서버에 다음 요청은 어떠한 사용자 지정 HTTP 요청 헤더도 사용할 수 있는지 알리며, 와일드카드 *를 지원합니다
    std::vector<std::string> m_allowed_methods; // 허용된 HTTP 작업, 열거형 값: GET, PUT, HEAD, POST, DELETE
    std::vector<std::string> m_allowed_origins; // 허용된 액세스 소스, 와일드카드 * 지원, 형식: 프로토콜://도메인[:포트] 예: http://www.qq.com
    std::vector<std::string> m_expose_headers;  // 브라우저가 수신 할 수 있는 서버의 사용자 지정 헤더 정보 설정
};


```

#### 예시

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "cpp_sdk_v5-123456789";

// PutBucketCORSReq 생성자는 bucket_name을 입력해야 합니다
qcloud_cos::PutBucketCORSReq req(bucket_name);
qcloud_cos::CORSRule rule;
rule.m_id = "123";
rule.m_allowed_headers.push_back("x-cos-meta-test");
rule.m_allowed_origins.push_back("http://www.qq.com");
rule.m_allowed_origins.push_back("http://cloud.tentent.com");
rule.m_allowed_methods.push_back("PUT");
rule.m_allowed_methods.push_back("GET");
rule.m_max_age_secs = "600";
rule.m_expose_headers.push_back("x-cos-expose");
req.AddRule(rule);

qcloud_cos::PutBucketCORSResp resp;
qcloud_cos::CosResult result = cos.PutBucketCORS(req, &resp);

// 호출에 성공할 경우 resp의 멤버 함수를 호출하여 반환 내용을 획득합니다
if (result.IsSucc()) {
    // ...
} else {
    // 수명 주기 설정에 실패하면, CosResult의 멤버 함수를 호출하여 requestID 등의 오류 정보를 출력할 수 있습니다.
}
```

### Get Bucket CORS

#### 기능 설명

Get Bucket CORS API는 버킷 소유자가 버킷에서 CORS의 정보 구성 획득을 구현합니다. 풀 네임은 Cross-Origin Resource Sharing이며, W3C 표준입니다. 기본으로 버킷의 소유자는 직접 해당 API를 사용할 권한이 있으며, 버킷 소유자는 해당 권한을 기타 사용자에게 부여할 수도 있습니다. 관련 API 문서는 [Get Bucket CORS](/document/product/436/8274)을 참조하십시오.

#### 방식 프로토타입

```cpp
CosResult GetBucketCORS(const DGetBucketCORSReq& req, GetBucketCORSResp* resp);
```

#### 매개변수 설명

| 매개변수 | 매개변수 설명                                      |
| ---- | --------------------------------------------- |
| req  | GetBucketCORSReq, GetBucketCORS 작업의 요청입니다.  |
| req  | GetBucketCORSResp, GetBucketCORS 작업의 반환입니다. |

```
// CORSRules, CORSRule 정의 참조 Put Bucket CORS 획득
std::vector<CORSRule> GetCORSRules();

```

#### 예시

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "cpp_sdk_v5-123456789";

// GetBucketCORSReq 생성자는 bucket_name을 입력해야 합니다
qcloud_cos::GetBucketCORSReq req(bucket_name);
qcloud_cos::GetBucketCORSResp resp;
qcloud_cos::CosResult result = cos.GetBucketCORS(req, &resp);

// 호출에 성공할 경우 resp의 멤버 함수를 호출하여 반환 내용을 획득합니다
if (result.IsSucc()) {
    // ...
} else {
    // 수명 주기 구성 획득에 실패하면, CosResult의 멤버 함수를 호출하여 requestID 등의 오류 정보를 출력할 수 있습니다.
}
```

### Delete Bucket CORS

#### 기능 설명

Delete Bucket CORS는 버킷에 대한 수명 주기 구성을 삭제하는 데 사용됩니다. 해당 버킷에 설정된 수명 주기가 없으면, NoSuchCORSConfiguration을 반환합니다. 관련 API 문서는 [Delete Bucket CORS](/document/product/436/8283)을 참조하십시오.

#### 방식 프로토타입

```cpp
CosResult DeleteBucketCORS(const DDeleteBucketCORSReq& req, DeleteBucketCORSResp* resp);
```

#### 매개변수 설명

| 매개변수 | 매개변수 설명                                            |
| ---- | --------------------------------------------------- |
| req  | DeleteBucketCORSReq, DeleteBucketCORS 작업의 요청입니다.   |
| req  | DeleteBucketCORSResp, DeleteBucketCORS 작업의 반환입니다. |

#### 예시

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "cpp_sdk_v5-123456789";

// DeleteBucketCORSReq 생성자는 bucket_name을 입력해야 합니다
qcloud_cos::DeleteBucketCORSReq req(bucket_name);
qcloud_cos::DeleteBucketCORSResp resp;
qcloud_cos::CosResult result = cos.DeleteBucketCORS(req, &resp);

// 호출에 성공할 경우 resp의 멤버 함수를 호출하여 반환 내용을 획득합니다
if (result.IsSucc()) {
    // ...
} else {
    // 수명 주기 구성 삭제에 실패하면, CosResult의 멤버 함수를 호출하여 requestID 등의 오류 정보를 출력할 수 있습니다.
}
```

###  Put Bucket ACL

#### 기능 설명

Put Bucket ACL API는 버킷의 ACL(Access Control List) 테이블을 작성하는 데 사용되며, 헤더: "x-cos-acl", "x-cos-grant-read", "x-cos-grant-write", "x-cos-grant-full-control"을 통하여 ACL 정보를 입력하거나 또는 본문을 통하여 XML 형식으로 ACL 정보를 입력할 수 있습니다. 관련 API 문서는 [Put Bucket ACL](/document/product/436/7737)을 참조하십시오.

#### 방식 프로토타입

```cpp
CosResult PutBucketACL(const DPutBucketACLReq& req, PutBucketACLResp* resp);
```

#### 매개변수 설명

| 매개변수 | 매개변수 설명                                    |
| ---- | ------------------------------------------- |
| req  | PutBucketACLReq, PutBucketACL 작업의 요청입니다.  |
| req  | PutBucketACLResp, PutBucketACL 작업의 반환입니다. |

```
// Bucket의 ACL 속성 정의, 유효 값: private,public-read-write,public-read
// 기본값: private
void SetXCosAcl(const std::string& str);

// 관한 부여받은 자에게 읽기 권한을 부여합니다. 형식: x-cos-grant-read: id=" ",id=" ".
// 서브 계정에 권한을 부여해야 할 경우, id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"
// 루트 계정에 권한을 부여해야 할 경우, id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"
void SetXCosGrantRead(const std::string& str);

// 권한 부여받은 자에게 쓰기 권한을 부여합니다. 형식: x-cos-grant-write: id=" ",id=" "./
// 서브 계정에 권한을 부여해야 할 경우, id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>",
// 루트 계정에 권한을 부여해야 할 경우, id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"
void SetXCosGrantWrite(const std::string& str);

// 권한 부여받은 자에게 쓰기 권한을 부여합니다. 형식: x-cos-grant-full-control: id=" ",id=" ".
// 서브 계정에 권한을 부여해야 할 경우, id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>",
// 루트 계정에 권한을 부여해야 할 경우, id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"
void SetXCosGrantFullControl(const std::string& str);

// 버킷 소유자 ID
void SetOwner(const Owner& owner);

// 권한 정보와 권한 정보 설정
void SetAccessControlList(const std::vector<Grant>& grants);

// 단일 버킷의 권한 정보 추가
void AddAccessControlList(const Grant& grant);


```

>!SetXCosAcl/SetXCosGrantRead/SetXCosGrantWrite/SetXCosGrantFullControl 이 인터페이스는 SetAccessControlList/AddAccessControlList와 동시에 사용할 수 없습니다. 전자는 HTTP Header를 설정하여 구현되고, 후자는 XML 형식의 내용을 본문에 추가하기 때문에 둘 중 하나만 선택할 수 있습니다. SDK 내부에서는 첫 번째 유형이 우선합니다.

ACLRule 정의는 다음과 같습니다.

```
struct Grantee {
    // type 유형은 RootAccount, SubAccount일 수 있습니다
    // type 유형이 RootAccount인 경우, id의 uin에 계정 ID를 입력하고, id의 uin에 계정 ID를 입력하고, anyone(모든 유형의 사용자로 대체)을 사용하여 uin/<OwnerUin> 및 uin/<SubUin>으로 대체할 수도 있습니다
    // type 유형이 RootAccount인 경우, uin은 루트 계정을 나타내고, Subaccount는 서브 계정을 나타냅니다
    std::string m_type;
    std::string m_id; // qcs::cam::uin/<OwnerUin>:uin/<SubUin>
    std::string m_display_name; // 비필수 옵션
    std::string m_uri;
};

struct Grant {
    Grantee m_grantee; // 권한 부여받은 자 리소스 정보
    std::string m_perm; // 권한 부여된 사람의 권한 정보 표시, 열거형 값: READ, WRITE, FULL_CONTROL
};


```

#### 예시

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "cpp_sdk_v5-123456789";

// PutBucketACLReq 생성자는 bucket_name을 입력해야 합니다
qcloud_cos::PutBucketACLReq req(bucket_name);
qcloud_cos::ACLRule rule;
rule.m_id = "123";
rule.m_allowed_headers.push_back("x-cos-meta-test");
rule.m_allowed_origins.push_back("http://www.qq.com");
rule.m_allowed_origins.push_back("http://cloud.tentent.com");
rule.m_allowed_methods.push_back("PUT");
rule.m_allowed_methods.push_back("GET");
rule.m_max_age_secs = "600";
rule.m_expose_headers.push_back("x-cos-expose");
req.AddRule(rule);

qcloud_cos::PutBucketACLResp resp;
qcloud_cos::CosResult result = cos.PutBucketACL(req, &resp);

// 호출에 성공할 경우 resp의 멤버 함수를 호출하여 반환 내용을 획득합니다
if (result.IsSucc()) {
    // ...
} else {
    // ACL을 설정하면, CosResult의 멤버 함수를 호출하여 requestID 등의 오류 정보를 출력할 수 있습니다.
}
```

###  Get Bucket ACL

#### 기능 설명

Get Bucket ACL API는 Bucket의 ACL, 즉, 버킷(Bucket)의 액세스 권한 제어 목록을 가져오는 데 사용됩니다. 이 API는 버킷의 소유자만 작업 권한이 있습니다. 관련 API 문서는 [Get Bucket ACL](/document/product/436/7733)을 참조하십시오.

#### 방식 프로토타입

```cpp
CosResult GetBucketACL(const DGetBucketACLReq& req, GetBucketACLResp* resp);
```

#### 매개변수 설명

| 매개변수 | 매개변수 설명                                    |
| ---- | ------------------------------------------- |
| req  | GetBucketACLReq, GetBucketACL 작업의 요청입니다.   |
| req  | GetBucketACLResp, GetBucketACL 작업의 반환입니다. |

```
std::string GetOwnerID();
std::string GetOwnerDisplayName();
std::vector<Grant> GetAccessControlList();

```

#### 예시

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "cpp_sdk_v5-123456789";

// GetBucketACLReq 생성자는 bucket_name을 입력해야 합니다
qcloud_cos::GetBucketACLReq req(bucket_name);
qcloud_cos::GetBucketACLResp resp;
qcloud_cos::CosResult result = cos.GetBucketACL(req, &resp);

// 호출에 성공할 경우 resp의 멤버 함수를 호출하여 반환 내용을 획득합니다
if (result.IsSucc()) {
    // ...
} else {
    // ACL 획득에 실패하면, CosResult의 멤버 함수를 호출하여 requestID 등의 오류 정보를 출력할 수 있습니다.
}
```

## Object 조작

object_name은 객체 키(Key)이며, 버킷에서 객체의 유일한 식별자입니다. 예를 들어, 객체의 액세스 도메인 이름 bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg 중, 객체 키는 doc1/pic1.jpg입니다.

“객체 키”에 관한 자세한 정보는 [객체 개요](https://cloud.tencent.com/document/product/436/13324)를 참조하십시오.

### Get Object

#### 기능 설명

Get Object 요청은 파일(Object)을 로컬이나 지정 스트림으로 다운로드할 수 있습니다. 해당 작업은 대상 객체에 대한 읽기 권한이 있거나 또는 대상 개체가 모든 사람에 대해 읽기 권한을 개방해야 합니다(공개 읽기).

#### 방식 프로토타입

```cpp
// 객체를 로컬 파일에 다운로드합니다
CosResult GetObject(const GetObjectByFileReq& req, GetObjectByFileResp* resp);

// 객체를 스트림에 다운로드합니다
CosResult GetObject(const GetObjectByStreamReq& req, GetObjectByStreamResp* resp);

// 객체를 로컬 파일에 다운로드합니다(멀티 스레드)
CosResult GetObject(const MultiGetObjectReq& req, MultiGetObjectResp* resp);
```

#### 매개변수 설명

| 매개변수 | 매개변수 설명                                                     |
| ---- | ------------------------------------------------------------ |
| req  | GetObjectByFileReq/GetObjectByStreamReq/MultiGetObjectReq, GetObject 작업의 요청입니다. |
| resp | GetObjectByFileResp/GetObjectByStreamResp/MultiGetObjectResp, GetObject 작업의 반환입니다. |

멤버 함수는 다음과 같습니다.

```
// 응답 헤더에 Content-Type 매개변수를 설정합니다.
void SetResponseContentType(const std::string& str);

// 응답 헤더에 Content-Language 매개변수를 설정합니다.
void SetResponseContentLang(const std::string& str);

// 응답 헤더에 Content-Expires 매개변수를 설정합니다.
void SetResponseExpires(const std::string& str);

// 응답 헤더에 Cache-Control 매개변수를 설정합니다.
void SetResponseCacheControl(const std::string& str);

// 응답 헤더에 Content-Disposition 매개변수를 설정합니다.
void SetResponseContentDisposition(const std::string& str);

// 응답 헤더에 Content-Encoding 매개변수를 설정합니다.
void SetResponseContentEncoding(const std::string& str);

```

GetObjectResp는 공통 헤더의 멤버 함수를 읽는 것 이외에도 다음과 같은 멤버 함수를 제공합니다.

```C++
// 객체가 마지막으로 수정된 시간을 획득합니다. 문자열 형식 Date는 "Wed, 28 Oct 2014 20:30:00 GMT"와 유사합니다.
std::string GetLastModified();

// 객체 유형 획득, 객체가 추가로 업로드할 수 있는지 여부 표시, 열거형 값: normal 또는 appendable
std::string GetXCosObjectType();

// 객체의 스토리지 클래스 획득, 열거형 값: STANDARD, STANDARD_IA
std::string GetXCosStorageClass();

// map 형식으로 모든 사용자 지정의 meta를 반환합니다. map의 key는 모두 "x-cos-meta-" 접두사를 포함하지 않습니다
std::map<std::string, std::string> GetXCosMetas();

// 사용자 지정 meta 획득, 매개변수는 x-cos-meta-*중의 *일 수 있습니다
std::string GetXCosMeta(const std::string& key);

// 서버 측 암호화에 사용되는 알고리즘 획득
std::string GetXCosServerSideEncryption();
```

#### 예시

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "cpp_sdk_v5-123456789";
std::string object_name = "object_name";
std::string local_path = "/tmp/object_name";

// 로컬로 다운로드
{
    // request는 appid, bucketname, object 및 로컬 경로(파일 이름 포함)를 제공해야 합니다
    qcloud_cos::GetObjectByFileReq req(bucket_name, object_name, local_path);
    qcloud_cos::GetObjectByFileResp resp;
    qcloud_cos::CosResult result = cos.GetObject(req, &resp);
    if (result.IsSucc()) {
        // 다운로드가 성공하면 GetObjectByFileResp의 멤버 함수를 호출할 수 있습니다
    } else {
        // 다운로드에 실패하면, CosResult의 멤버 함수를 호출하여 requestID 등의 오류 정보를 출력할 수 있습니다
    }
}

// 스트림으로 다운로드
{
    // request는 appid, bucketname, object 및 출력 스트림을 제공해야 합니다
    std::ostringstream os;
    qcloud_cos::GetObjectByStreamReq req(bucket_name, object_name, os);
    qcloud_cos::GetObjectByStreamResp resp;
    qcloud_cos::CosResult result = cos.GetObject(req, &resp);
    if (result.IsSucc()) {
        // 다운로드가 성공하면 GetObjectByStreamResp 멤버 함수를 호출할 수 있습니다
    } else {
        // 다운로드에 실패하면, CosResult의 멤버 함수를 호출하여 requestID 등의 오류 정보를 출력할 수 있습니다
    }
}

// 여러 스레드로 로컬에 다운로드
{
    // 매개변수 appid, bucketname, object 및 로컬 경로(파일 이름 포함)가 요청에 필요해야 합니다.
    qcloud_cos::MultiGetObjectReq req(bucket_name, object_name, local_path);
    qcloud_cos::MultiGetObjectResp resp;
    qcloud_cos::CosResult result = cos.GetObject(req, &resp);
    if (result.IsSucc()) {
        // 다운로드가 성공하면 MultiGetObjectResp 멤버 함수를 호출 할 수 있습니다
    } else {
        // 다운로드에 실패하면, CosResult의 멤버 함수를 호출하여 requestID 등의 오류 정보를 출력할 수 있습니다
    }
}
```

### Head Object

#### 기능 설명

Head Object 요청은 해당하는 객체의 메타데이터를 검색할 수 있으며 Head의 권한은 Get의 권한과 일치합니다.

#### 방식 프로토타입

```cpp
CosResult HeadObject(const HeadObjectReq& req, HeadObjectResp* resp);
```

#### 매개변수 설명

| 매개변수 | 매개변수                                |
| ---- | --------------------------------------- |
| req  | HeadObjectReq, HeadObject 작업의 요청입니다.  |
| resp | HeadObjectResp, HeadObject 작업의 반환입니다. |

HeadObjectResp는 공통 헤더의 멤버 함수를 읽는 것 이외에도 다음과 같은 멤버 함수를 제공합니다.

```C++
std::string GetXCosObjectType();

std::string GetXCosStorageClass();

// 사용자 지정 meta 획득, 매개변수는 x-cos-meta-*중의 *일 수 있습니다
std::string GetXCosMeta(const std::string& key);

// map 형식으로 모든 사용자 지정의 meta를 반환합니다. map의 key는 모두 "x-cos-meta-" 접두사를 포함하지 않습니다
std::map<std::string, std::string> GetXCosMetas();

// 서버 측 암호화에 사용되는 알고리즘 획득
std::string GetXCosServerSideEncryption();
```

#### 예시

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "cpp_sdk_v5-123456789";
std::string object_name = "object_name";
qcloud_cos::HeadObjectReq req(bucket_name, object_name);
qcloud_cos::HeadObjectResp resp;
qcloud_cos::CosResult result = cos.HeadObject(req, &resp);
if (result.IsSucc()) {
    // 다운로드가 성공하면 HeadObjectResp 멤버 함수를 호출할 수 있습니다
} else {
    // 다운로드에 실패하면, CosResult의 멤버 함수를 호출하여 requestID 등의 오류 정보를 출력할 수 있습니다
}
```

### Put Object

#### 기능 설명

Put Object 요청은 한 개의 파일(Object)을 지정 버킷으로 업로드할 수 있습니다.

- 업로드 프로세스 중에 기본으로 파일에 대해 MD5 검증이 수행됩니다(업로드 MD5 검증 비활성화는 예제 코드 참조)
-  현재 액세스 정책 항목은 1000으로 제한되어 있습니다. 객체에 대해 ACL 제어가 필요하지 않은 경우 업로드 시 설정하지 마십시오. 기본으로 버킷 권한은 계승됩니다.

#### 방식 프로토타입

```cpp
/// 스트림을 통한 업로드 진행
CosResult PutObject(const PutObjectByStreamReq& req, PutObjectByStreamResp* resp);

/// 로컬 파일 업로드
CosResult PutObject(const PutObjectByFileReq& req, PutObjectByFileResp* resp);
```

#### 매개변수 설명

| 매개변수 | 매개변수 설명                                                     |
| ---- | ------------------------------------------------------------ |
| req  | PutObjectByStreamReq/PutObjectByFileReq, PutObject 작업의 요청입니다. |
| resp | PutObjectByStreamResp/PutObjectByFileResp, PutObject 작업의 반환입니다. |

매개변수 Req는 다음의 멤버 함수를 포함합니다.

```C++
// Cache-Control RFC 2616에 정의된 캐시 정책, 객체 메타데이터로 저장됩니다
void SetCacheControl(const std::string& str);

// Content-Disposition RFC 2616에 정의된 파일 이름, 객체 메타데이터로 저장됩니다
void SetContentDisposition(const std::string& str);

// Content-Encoding    RFC 2616에 정의된 인코딩 형식, 객체 메타데이터로 저장됩니다
void SetContentEncoding(const std::string& str);

// Content-Type    RFC 2616에 정의된 내용 유형(MIME), 객체 메타데이터로 저장됩니다
void SetContentType(const std::string& str);

// Expect  Expect 사용 시: 100-continue 시, 서버측에서 확인을 받기 전까지 요청 내용이 전송되지 않습니다
void SetExpect(const std::string& str);

// Expires RFC 2616에 정의된 만료 시간, 객체 메타데이터로 저장됩니다
void SetExpires(const std::string& str);

// 사용자 지정의 헤더 정보를 허용하며, 객체 메타데이터로 반환됩니다. 크기 제한은 2K입니다
void SetXCosMeta(const std::string& key, const std::string& value);

// x-cos-storage-class를 통해 객체의 스토리지 클래스 설정, 열거형 값: STANDARD, STANDARD_IA
// 기본값: STANDARD(현재는 화남 지역만 지원됨)
void SetXCosStorageClass(const std::string& storage_class);

// 객체 정의의 ACL 속서, 유효 값: private,public-read-write,public-read
// 기본값: private
void SetXcosAcl(const std::string& str);

// 관한 부여받은 자에게 읽기 권한을 부여합니다. 형식: x-cos-grant-read: id=" ",id=" ".
// 서브 계정에 권한을 부여해야 할 경우, id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"
// 루트 계정에 권한을 부여해야 할 경우, id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"
void SetXcosGrantRead(const std::string& str);

// 권한 부여받은 자에게 쓰기 권한을 부여합니다. 형식: x-cos-grant-write: id=" ",id=" "./
// 서브 계정에 권한을 부여해야 할 경우, id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>",
// 루트 계정에 권한을 부여해야 할 경우, id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"
void SetXcosGrantWrite(const std::string& str);

// 권한 부여받은 자에게 쓰기 권한을 부여합니다. 형식: x-cos-grant-full-control: id=" ",id=" ".
// 서브 계정에 권한을 부여해야 할 경우, id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>",
// 루트 계정에 권한을 부여해야 할 경우, id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"
void SetXcosGrantFullControl(const std::string& str);

/// 서버 측 암호화에 사용되는 알고리즘 설정, 현재 AES256 지원
void SetXCosServerSideEncryption(const std::string& str);
```

매개변수 Resp는 다음의 멤버 함수를 포함합니다.

```C++
/// 버전 번호를 획득합니다. 버킷이 여러 버전을 시작하지 않으면 빈 문자열이 반환됩니다
std::string GetVersionId();

/// 서버 측 암호화에 사용되는 알고리즘
std::string GetXCosServerSideEncryption();
```

#### 예시

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "cpp_sdk_v5-123456789";
std::string object_name = "object_name";

//### 간편 업로드(스트림)
{
    std::istringstream iss("put object");
    // request의 생성자에서 istream을 입력해야 합니다.
    qcloud_cos::PutObjectByStreamReq req(bucket_name, object_name, iss);
    // Set 방법 구성 메타데이터 또는 ACL 등을 호출
    req.SetXCosStorageClass("STANDARD_IA");
    // MD5 확인을 닫고, req.TurnOnComputeConentMd5() 사용을 시작합니다. 기본값이 시작됩니다
    req.TurnOffComputeConentMd5();
    qcloud_cos::PutObjectByStreamResp resp;
    qcloud_cos::CosResult result = cos.PutObject(req, &resp);

    if (result.IsSucc()) {
        // 호출에 성공할 경우 resp의 멤버 함수를 호출하여 반환 내용을 획득합니다
        do sth
    } else {
        // 호출에 실패하면, result의 멤버 함수를 호출하여 오류 정보를 획득합니다
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
    // request의 생성자에서 로컬 파일 경로를 입력해야 합니다
    qcloud_cos::PutObjectByFileReq req(bucket_name, object_name, "/path/to/local/file");
    // Set 방법 구성 메타데이터 또는 ACL 등을 호출
    req.SetXCosStorageClass("STANDARD_IA");
    // MD5 확인을 닫고, req.TurnOnComputeConentMd5() 사용을 시작합니다. 기본값이 시작됩니다
    req.TurnOffComputeConentMd5();
    qcloud_cos::PutObjectByFileResp resp;
    qcloud_cos::CosResult result = cos.PutObject(req, &resp);
        if (result.IsSucc()) {
        // 호출에 성공할 경우 resp의 멤버 함수를 호출하여 반환 내용을 획득합니다
        do sth
    } else {
        // 호출에 실패하면, result의 멤버 함수를 호출하여 오류 정보를 획득합니다
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

### Delete Object

#### 기능 설명

Delete Object API 요청은 COS의 버킷에서 파일(Object)를 삭제할 수 있습니다. 해당 작업은 요청자가 버킷에 대한 쓰기 권한이 있어야 합니다. 관련 API 문서는 [Delete Object](/document/product/436/7743)를 참조하십시오.

#### 방식 프로토타입

```cpp
CosResult DeleteObject(const DeleteObjectReq& req, DeleteObjectResp* resp);
```

#### 매개변수 설명

| 매개변수 | 매개변수 설명                                   |
| ---- | ------------------------------------------ |
| req  | DeleteObjectReq, DeleteObject 작업의 요청입니다. |
| resp | DeletObjectResp, DeletObject 작업의 반환입니다.  |

#### 예시

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "cpp_sdk_v5-123456789";
std::string object_name = "test_object";

qcloud_cos::DeleteObjectReq req(bucket_name, object_name);
qcloud_cos::DeleteObjectResp resp;
qcloud_cos::CosResult result = cos.DeleteObject(req, &resp);

// 호출에 성공할 경우 resp의 멤버 함수를 호출하여 반환 내용을 획득합니다
if (result.IsSucc()) {
    // ...
} else {
    // 객체 삭제에 실패하면, CosResult의 멤버 함수를 호출하여 requestID 등의 오류 정보를 출력할 수 있습니다
}
```

## 멀티파트 업로드 작업

### Initiate Multipart Upload

#### 기능 설명

Initiate Multipart Upload 요청은 멀티파트 업로드를 초기화합니다. 해당 요청을 성공적으로 실행하면 후속 Upload Part 요청에 사용되는 Upload ID가 반환됩니다.

#### 방식 프로토타입

```cpp
CosResult InitMultiUpload(const InitMultiUploadReq& req, InitMultiUploadResp* resp);
```

#### 매개변수 설명

| 매개변수 | 매개변수 설명                                          |
| ---- | ------------------------------------------------- |
| req  | InitMultiUploadReq, InitMultiUpload 작업의 요청입니다.  |
| resp | InitMultiUploadResp, InitMultiUpload 작업의 반환입니다. |

InitMultiUploadReq의 멤버 함수는 다음과 같습니다.

```
// Cache-Control RFC 2616 에 정의된 캐시 정책, 객체 메타데이터로 저장됩니다
void SetCacheControl(const std::string& str);

// Content-Disposition RFC 2616 에 정의된 파일 이름, 객체 메타데이터로 저장됩니다
void SetContentDisposition(const std::string& str);

// Content-Encoding    RFC 2616 에 정의된 인코딩 형식, 객체 메타데이터로 저장됩니다
void SetContentEncoding(const std::string& str);

// Content-Type    RFC 2616 에 정의된 내용 유형(MIME), 객체 메타데이터로 저장됩니다
void SetContentType(const std::string& str);

// Expires RFC 2616 에 정의된 만료 시간, 객체 메타데이터로 저장됩니다
void SetExpires(const std::string& str);

// 사용자 지정의 헤더 정보를 허용하며, 객체 메타데이터로 반환됩니다. 크기 제한은 2K입니다
void SetXCosMeta(const std::string& key, const std::string& value);

// x-cos-storage-class를 통해 객체의 스토리지 클래스 설정, 열거형 값: STANDARD, STANDARD_IA
// 기본값: STANDARD
void SetXCosStorageClass(const std::string& storage_class);

// 객체 정의의 ACL 속서, 유효 값: private,public-read-write,public-read
// 기본값: private
void SetXcosAcl(const std::string& str);

// 관한 부여받은 자에게 읽기 권한을 부여합니다. 형식: x-cos-grant-read: id=" ",id=" ".
// 서브 계정에 권한을 부여해야 할 경우, id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"
// 루트 계정에 권한을 부여해야 할 경우, id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"
void SetXcosGrantRead(const std::string& str);

// 권한 부여받은 자에게 쓰기 권한을 부여합니다. 형식: x-cos-grant-write: id=" ",id=" "./
// 서브 계정에 권한을 부여해야 할 경우, id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>",
// 루트 계정에 권한을 부여해야 할 경우, id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"
void SetXcosGrantWrite(const std::string& str);

// 권한 부여받은 자에게 쓰기 권한을 부여합니다. 형식: x-cos-grant-full-control: id=" ",id=" ".
// 서브 계정에 권한을 부여해야 할 경우, id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>",
// 루트 계정에 권한을 부여해야 할 경우, id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"
void SetXcosGrantFullControl(const std::string& str);

/// 서버 측 암호화에 사용되는 알고리즘 설정, 현재 AES256 지원
void SetXCosServerSideEncryption(const std::string& str);

```

해당 요청을 성공적으로 실행한 후, 반환된 응답에는 bucket, key, uploadId가 포함될 수 있으며, 각각 멀티파트 업로드의 대상 버킷, 객체 이름 및 이어지는 멀티파트 업로드에 필요한 번호를 나타냅니다.

InitMultiUploadResp의 멤버 함수는 다음과 같습니다.

```C++
std::string GetBucket();
std::string GetKey();
std::string GetUploadId();

// 서버 측 암호화에 사용되는 알고리즘
std::string GetXCosServerSideEncryption();
```

#### 예시

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);
std::string bucket_name = "cpp_sdk_v5-123456789";
std::string object_name = "object_name";

qcloud_cos::InitMultiUploadReq req(bucket_name, object_name);
qcloud_cos::InitMultiUploadResp resp;
qcloud_cos::CosResult result = cos.InitMultiUpload(req, &resp);

std::string upload_id = "";
if (result.IsSucc()) {
    upload_id = resp.GetUploadId();
}
```

### Upload Part

#### 기능 설명

Upload Part 요청은 초기화 후 멀티파트 업로드를 구현하며, 지원되는 파트 수량은 1에서 10000까지이고, 파트의 크기는 1MB~5GB입니다. 각 Upload Part 요청 시 partNumber 및 uploadID가 있어야 하며, partNumber는 파트의 번호로서 비순차적 업로드를 지원합니다.

> 팁: 업로드 프로세스 중에 기본으로 파일에 대해 MD5 검증이 수행됩니다(업로드 MD5 검증 비활성화는 예제 코드 참조)

#### 방식 프로토타입

```cpp
CosResult UploadPartData(const UploadPartDataReq& request, UploadPartDataResp* response);
```

#### 매개변수 설명

| 매개변수 | 매개변수 설명                                        |
| ---- | ----------------------------------------------- |
| req  | UploadPartDataReq, UploadPartData 작업의 요청입니다.  |
| resp | UploadPartDataResp, UploadPartData 작업의 반환입니다. |

UploadPartDataReq가 생성될 때, 요청의 APPID, Bucket, Object, 초기화 성공 후 획득한 UploadId 및 업로드된 데이터 스트림을 지정해야 합니다(호출 완료 후 스트림이 호출자 자신에 의해 닫힘).

```
UploadPartDataReq(const std::string& bucket_name,
                    const std::string& object_name, const std::string& upload_id,
                    std::istream& in_stream);

```

또한, 요청은 파트 번호를 지정해야 하며, 이 파트는 멀티파트 업로드 시에 사용되기도 합니다.

```
void SetPartNumber(uint64_t part_number);

```

UploadPartDataResp의 멤버 함수는 다음과 같습니다.

```
/// 서버 측 암호화에 사용되는 알고리즘
std::string GetXCosServerSideEncryption();

```

#### 예시

```cpp
// 첫번째 파트 업로드
{
    std::fstream is("demo_5M.part1");
    qcloud_cos::UploadPartDataReq req(bucket_name, object_name,
                                      upload_id, is);
    req.SetPartNumber(1);
    // MD5 확인을 닫고, req.TurnOnComputeConentMd5() 사용을 시작합니다. 기본값이 시작됩니다
    req.TurnOffComputeConentMd5();
    qcloud_cos::UploadPartDataResp resp;
    qcloud_cos::CosResult result = cos.UploadPartData(req, &resp);

    // 업로드 성공 시 파트 번호 및 반환된 ETag를 기록해야 합니다
    if (result.IsSucc()) {
        etags.push_back(resp.GetEtag());
        part_numbers.push_back(1);
    }
    is.close();
}

// 두번째 파트 업로드
{
    std::fstream is("demo_5M.part2");
    qcloud_cos::UploadPartDataReq req(bucket_name, object_name,
                                      upload_id, is);
    req.SetPartNumber(2);
    qcloud_cos::UploadPartDataResp resp;
    qcloud_cos::CosResult result = cos.UploadPartData(req, &resp);

    // 업로드 성공 시 파트 번호 및 반환된 ETag를 기록해야 합니다
    if (result.IsSucc()) {
        etags.push_back(resp.GetEtag());
        part_numbers.push_back(2);
    }
    is.close();
}
```

### Complete Multipart Upload

#### 기능 설명

Complete Multipart Upload는 전체 멀티파트 업로드를 구현할 수 있습니다. Upload Parts를 사용하여 모든 파트를 업로드한 후, 이 API를 사용하여 업로드를 완료할 수 있습니다. 이 API 사용 시 본문에 각 파트의 PartNumber 및 ETag를 제공하여 파트의 정확성을 인증해야 합니다.

#### 방식 프로토타입

```cpp
CosResult CompleteMultiUpload(const CompleteMultiUploadReq& request, CompleteMultiUploadResp* response);
```

#### 매개변수 설명

| 매개변수 | 매개변수 설명                                                  |
| ---- | --------------------------------------------------------- |
| req  | CompleteMultiUploadReq, CompleteMultiUpload 작업의 요청입니다.  |
| resp | CompleteMultiUploadResp, CompleteMultiUpload 작업의 반환입니다. |

CompleteMultiUploadReq가 구성될 때, 요청의 APPID, Bucket, Object, 초기화 성공 후 획득한 UploadId를 지정해야 합니다.

```
CompleteMultiUploadReq(const std::string& bucket_name,
                       const std::string& object_name, const std::string& upload_id)

```

또한, request는 모든 업로드된 멀티파트 번호 및 ETag를 설정해야 합니다.

```
// 다음 방법을 호출할 때, 번호 및 ETag의 순서는 일대일로 대응해야 한다는 데 주의하십시오.
void SetPartNumbers(const std::vector<uint64_t>& part_numbers);
void SetEtags(const std::vector<std::string>& etags) ;

// part_number 및 ETag 쌍 추가
void AddPartEtagPair(uint64_t part_number, const std::string& etag);

/// 서버 측 암호화에 사용되는 알고리즘 설정, 현재 AES256 지원
void SetXCosServerSideEncryption(const std::string& str);

```

CompleteMultiUploadResp의 반환 내용에는 Location, Bucket, Key, ETag가 포함되며, 각각 생성된 객체의 외부 네트워크 액세스 도메인 이름, 멀티파트 업로드의 대상 버킷, 객체 이름 및 병합 후 파일의 MD5 알고리즘 검증값을 나타냅니다. 아래 나온 멤버 함수를 호출하여 응답의 내용에 대해 액세스할 수 있습니다.

```
std::string GetLocation();
std::string GetKey();
std::string GetBucket();
std::string GetEtag();

/// 서버 측 암호화에 사용되는 알고리즘
std::string GetXCosServerSideEncryption();

```

#### 예시

```cpp
qcloud_cos::CompleteMultiUploadReq req(bucket_name, object_name, upload_id);
qcloud_cos::CompleteMultiUploadResp resp;
req.SetEtags(etags);
req.SetPartNumbers(part_numbers);

qcloud_cos::CosResult result = cos.CompleteMultiUpload(req, &resp);
```

### Multipart Upload

#### 기능 설명

멀티파트 업로드는 멀티파트 업로드 초기화, 멀티파트 업로드, 멀티파트 업로드 완료의 세 단계를 캡슐화하고, 요청 중에만 업로드 파일을 지정하면 됩니다.

#### 방식 프로토타입

```cpp
CosResult MultiUploadObject(const MultiUploadObjectReq& request,        MultiUploadObjectResp* response);
```

#### 매개변수 설명

| 매개변수 | 매개변수 설명                                             |
| ---- | ----------------------------------------------------- |
| req  | MultiUploadObjectReq, MultiUploadObject 작업의 요청입니다.  |
| resp | MultiUploadObjectResp, MultiUploadObject 작업의 반환입니다. |

MultiUploadObjectReq는 생성할 때 버킷, 객체 및 업로드 대기 중인 로컬 경로를 지정해야 합니다. 로컬 경로를 지정하지 않으면 기본값은 현재 작업 경로에서 객체와 이름이 같은 파일입니다.

```
MultiUploadObjectReq(const std::string& bucket_name,
                     const std::string& object_name, const std::string& local_file_path = "");

/// 서버 측 암호화에 사용되는 알고리즘 설정, 현재 AES256 지원
void SetXCosServerSideEncryption(const std::string& str);

```

- 멀티파드 업로드가 성공한 경우, 해당 응답의 반환 내용은 CompleteMultiUploadResp와 일치합니다.
- 멀티파드 업로드가 실패한 경우, 해당 response는 여러 실패 조건에 따라 반환 내용이 InitMultiUploadResp, UploadPartDataResp, CompleteMultiUploadResp와 일치합니다. `GetRespTag()`를 호출하여 어느 단계에서 특정 실패를 했는지 알 수 있습니다.

```
// Init, Upload, Complete 반환
std::string GetRespTag();

/// 서버 측 암호화에 사용되는 알고리즘
std::string GetXCosServerSideEncryption();

```

#### 예시

```cpp
qcloud_cos::MultiUploadObjectReq req( bucket_name, object_name, "/temp/demo_6G.tmp");
qcloud_cos::MultiUploadObjectResp resp;
qcloud_cos::CosResult result = cos.MultiUploadObject(req, &resp);

if (result.IsSucc()) {
    std::cout << resp.GetLocation() << std::endl;
    std::cout << resp.GetKey() << std::endl;
    std::cout << resp.GetBucket() << std::endl;
    std::cout << resp.GetEtag() << std::endl;
} else {
    // 어느 단계에서 특정 실패 정보 획득
    std::string resp_tag = resp.GetRespTag();
    if ("Init" == resp_tag) {
        // print result
    } else if ("Upload" == resp_tag) {
        // print result
    } else if ("Complete" == resp_tag) {
        // print result
    }
}
```

### Abort Multipart Upload

#### 기능 설명

Abort Multipart Upload는 멀티파트 업로드를 취소하고 이미 업로드된 파트를 삭제하는 데 사용됩니다. Abort Multipart Upload 호출 시, 이 Upload Parts 업로드 파트를 사용 중일 때 요청이 있으면 Upload Parts는 실패를 반환합니다.

#### 방식 프로토타입

```cpp
CosResult AbortMultiUpload(const AbortMultiUploadReq& request, AbortMultiUploadResp* response);
```

#### 매개변수 설명

| 매개변수 | 매개변수 설명                                            |
| ---- | --------------------------------------------------- |
| req  | AbortMultiUploadReq, AbortMultiUpload 작업의 요청입니다.  |
| resp | AbortMultiUploadResp, AbortMultiUpload 작업의 반환입니다. |

AbortMultiUploadReq는 생성 시 Bucket, Object 및 Upload_id를 지정해야 합니다.

```C++
AbortMultiUploadReq(const std::string& bucket_name,
                    const std::string& object_name, const std::string& upload_id);
```

특수 방법이 없으면, BaseResp에 해당하는 멤버 함수를 호출하여 공통 헤더 내용을 획득할 수 있습니다.

#### 예시

```cpp
qcloud_cos::AbortMultiUploadReq req(bucket_name, object_name,
                                                    upload_id);
qcloud_cos::AbortMultiUploadResp resp;
qcloud_cos::CosResult result = cos.AbortMultiUpload(req, &resp);
```

### List Parts

#### 기능 설명

List Parts는 특정 멀티파트 업로드의 업로드된 파트를 조회하는 데 사용됩니다. 즉, 지정된 UploadId가 속한 성공적으로 업로드된 모든 파트를 나열하는 데 사용됩니다. 관련 API 문서는 [List Parts](/document/product/436/7747)를 참조하십시오.

#### 방식 프로토타입

```cpp
CosResult ListParts(const ListPartsReq& req, ListPartsResp* resp);
```

#### 매개변수 설명

| 매개변수 | 매개변수 설명                              |
| ---- | ------------------------------------- |
| req  | ListPartsReq, ListParts 작업의 요청입니다.  |
| resp | ListPartsResp, ListParts 작업의 반환입니다. |

```
// 생성자, 버킷 이름, 객체 이름, 멀티파트 업로드 ID
ListPartsReq(const std::string& bucket_name,                                                                                                                                      
             const std::string& object_name,
             const std::string& upload_id);

// \brief 반환값의 인코딩 방식 규정
void SetEncodingType(const std::string& encoding_type);

// \brief 1회 반환의 최대 항목 수를 반환하며, 설정되지 않으면 기본값은 1000입니다
void SetMaxParts(uint64_t max_parts);

// \brief 기본 설정으로 UTF-8 이진 순서로 항목이 나열되며, 모든 나열 항목은 marker에서 시작합니다
void SetPartNumberMarker(const std::string& part_number_marker);

```

```
// 멀티파트 업로드 대상 버킷
std::string GetBucket();

// 반환값의 인코딩 방식 규정
std::string GetEncodingType();

// 객체 이름
std::string GetKey();

// 해당 멀티파트 업로드의 ID
std::string GetUploadId();

// 해당 업로드 개시자 정보
Initiator GetInitiator();

// 해당 파트의 소유자 정보
Owner GetOwner();

// 기본 설정으로 UTF-8 이진 순서로 항목이 나열되며, 모든 나열 항목은 marker에서 시작합니다
uint64_t GetPartNumberMarker();

// 각 파트의 정보 반환
std::vector<Part> GetParts();

// 반환 항목 잘리면, 반환되는 NextMarker는 다음 항목의 시작점입니다
uint64_t GetNextPartNumberMarker();

// 해당 멀티파트의 스토리지 클래스를 나타냅니다. 열거형 값: Standard, Standard_IA
std::string GetStorageClass();

// 1회 반환하는 최대 항목 수입니다
uint64_t GetMaxParts();

// 반환 항목이 잘라내기 되었는지 여부, 부울값: TRUE, FALSE
bool IsTruncated();

```

그 중 Part, Owner, Initiator의 정의는 다음과 같습니다.

```
struct Initiator {
    std::string m_id; // 생성자의 고유한 식별자
    std::string m_display_name; // 생성자의 사용자 이름 설명
};

struct Owner {
    std::string m_id; // 사용자의 고유한 식별자
    std::string m_display_name; // 사용자 이름 설명
};

struct Part {
    uint64_t m_part_num; // 파트 번호
    uint64_t m_size; // 파트의 크기, 단위는 Byte
    std::string m_etag; // 객체 파트의 MD5 알고리즘 검증값
    std::string m_last_modified; // 파트의 마지막 수정 시간
};

```

#### 예시

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "cpp_sdk_v5-123456789";
std::string object_name = "test_object";

// uploadId는 InitMultiUpload를 호출한 후에 얻어집니다
qcloud_cos::ListPartsReq req(bucket_name, object_name, upload_id);
req.SetMaxParts(1);                                                                                                                                                               
req.SetPartNumberMarker("1");
qcloud_cos::ListPartsResp resp;
qcloud_cos::CosResult result = cos.ListParts(req, &resp);

// 호출에 성공할 경우 resp의 멤버 함수를 호출하여 반환 내용을 획득합니다
if (result.IsSucc()) {
    // ...
} else {
    // 객체 삭제에 실패하면, CosResult의 멤버 함수를 호출하여 requestID 등의 오류 정보를 출력할 수 있습니다
}
```

### Put Object ACL

#### 기능 설명

Put Object ACL API는 객체의 ACL 테이블을 작성하는 데 사용되며, 헤더: "x-cos-acl", "x-cos-grant-read", "x-cos-grant-write", "x-cos-grant-full-control"을 통하여 ACL 정보를 입력하거나 또는 본문을 통하여 XML 형식으로 ACL 정보를 입력할 수 있습니다. 관련 API 문서는 [Put Object ACL](/document/product/436/7748)을 참조하십시오.

>!현재 액세스 정책 항목은 1000으로 제한되어 있습니다. 객체에 대해 ACL 제어가 필요하지 않은 경우 설정하지 마십시오. 기본으로 버킷 권한은 계승됩니다.

#### 방식 프로토타입

```cpp
CosResult PutObjectACL(const PutObjectACLReq& req, PutObjectACLResp* resp);
```

#### 매개변수 설명

| 매개변수 | 매개변수 설명                                    |
| ---- | ------------------------------------------- |
| req  | PutObjectACLReq, PutObjectACL 작업의 요청입니다.  |
| resp | PutObjectACLResp, PutObjectACL 작업의 반환입니다. |

```
// 객체 정의의 ACL 속서, 유효 값: private,public-read-write,public-read
// 기본값: private
void SetXCosAcl(const std::string& str);

// 관한 부여받은 자에게 읽기 권한을 부여합니다. 형식: x-cos-grant-read: id=" ",id=" ".
// 서브 계정에 권한을 부여해야 할 경우, id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"
// 루트 계정에 권한을 부여해야 할 경우, id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"
void SetXCosGrantRead(const std::string& str);

// 권한 부여받은 자에게 쓰기 권한을 부여합니다. 형식: x-cos-grant-write: id=" ",id=" "./
// 서브 계정에 권한을 부여해야 할 경우, id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>",
// 루트 계정에 권한을 부여해야 할 경우, id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"
void SetXCosGrantWrite(const std::string& str);

// 권한 부여받은 자에게 쓰기 권한을 부여합니다. 형식: x-cos-grant-full-control: id=" ",id=" ".
// 서브 계정에 권한을 부여해야 할 경우, id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>",
// 루트 계정에 권한을 부여해야 할 경우, id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"
void SetXCosGrantFullControl(const std::string& str);

// 객체 소유자 ID
void SetOwner(const Owner& owner);

// 권한 정보와 권한 정보 설정
void SetAccessControlList(const std::vector<Grant>& grants);

// 단일 객체 권한 정보 추가
void AddAccessControlList(const Grant& grant);


```

>!SetXCosAcl/SetXCosGrantRead/SetXCosGrantWrite/SetXCosGrantFullControl 등 이러한 API는 SetAccessControlList/AddAccessControlList와 동시에 사용할 수 없습니다. 전자는 HTTP Header를 설정하여 구현되고, 후자는 XML 형식의 내용을 본문에 추가하기 때문에 둘 중 하나만 선택할 수 있습니다. SDK 내부에서는 첫 번째 유형이 우선합니다.

ACLRule 정의는 다음과 같습니다.

```
struct Grantee {
    // type 유형은 RootAccount, SubAccount일 수 있습니다
    // type 유형이 RootAccount인 경우, id의 uin에 계정 ID를 입력하고, id의 uin에 계정 ID를 입력하고, anyone(모든 유형의 사용자로 대체)을 사용하여 uin/<OwnerUin> 및 uin/<SubUin>으로 대체할 수도 있습니다
    // type 유형이 RootAccount인 경우, uin은 루트 계정을 나타내고, Subaccount는 서브 계정을 나타냅니다
    std::string m_type;
    std::string m_id; // qcs::cam::uin/<OwnerUin>:uin/<SubUin>
    std::string m_display_name; // 비필수 옵션
    std::string m_uri;
};

struct Grant {
    Grantee m_grantee; // 권한 부여받은 자 리소스 정보
    std::string m_perm; // 권한 부여된 사람의 권한 정보 표시, 열거형 값: READ, WRITE, FULL_CONTROL
};


```

#### 예시

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "cpp_sdk_v5-123456789";
std::string object_name = "sevenyou";

// 1 ACL 구성 설정(본문을 통함. ACL 설정은 본문, 헤더 두 가지 방식을 통해 설정할 수 있지만 그 중 하나만 선택할 수 있습니다. 그렇지 않으면 충돌이 발생합니다)
{   
    qcloud_cos::PutObjectACLReq req(bucket_name, object_name);
    qcloud_cos::Owner owner = {"qcs::cam::uin/xxxxx:uin/xxx", "qcs::cam::uin/xxxxxx:uin/xxxxx" };
    qcloud_cos::Grant grant;
    req.SetOwner(owner);
    grant.m_grantee.m_type = "Group";
    grant.m_grantee.m_uri = "http://cam.qcloud.com/groups/global/AllUsers";
    grant.m_perm = "READ";
    req.AddAccessControlList(grant);

    qcloud_cos::PutObjectACLResp resp;
    qcloud_cos::CosResult result = cos.PutObjectACL(req, &resp);
    // 호출에 성공할 경우 resp의 멤버 함수를 호출하여 반환 내용을 획득합니다
    if (result.IsSucc()) {
        // ...
    } else {
        // ACL을 설정하면, CosResult의 멤버 함수를 호출하여 requestID 등의 오류 정보를 출력할 수 있습니다.
    }
}   

// 2 ACL 구성 설정(헤더를 통함, ACL 설정은 본문, 헤더 두 가지 방식을 통해 설정할 수 있지만 그 중 하나만 선택할 수 있습니다. 그렇지 않으면 충돌이 발생합니다)
{   
    qcloud_cos::PutObjectACLReq req(bucket_name, object_name);                                                                                                                    
    req.SetXCosAcl("public-read-write");

    qcloud_cos::PutObjectACLResp resp;
    qcloud_cos::CosResult result = cos.PutObjectACL(req, &resp);
    // 호출에 성공할 경우 resp의 멤버 함수를 호출하여 반환 내용을 획득합니다
    if (result.IsSucc()) {
        // ...
    } else {
        // ACL을 설정하면, CosResult의 멤버 함수를 호출하여 requestID 등의 오류 정보를 출력할 수 있습니다.
    }
}   
```

### Get Object ACL

#### 기능 설명

Get Object ACL API는 Object의 ACL, 즉 객체(파일, Object)의 액세스 권한 제어 리스트를 가져오는 데 사용됩니다. 이 API는 Object의 소유자만 작업 권한이 있습니다. 관련 API 문서는 [Get Object ACL](/document/product/436/7744)을 참조하십시오.

#### 방식 프로토타입

```cpp
CosResult GetObjectACL(const DGetObjectACLReq& req, GetObjectACLResp* resp);
```

#### 매개변수 설명

| 매개변수 | 매개변수 설명                                    |
| ---- | ------------------------------------------- |
| req  | GetObjectACLReq, GetObjectACL 작업의 요청입니다.  |
| resp | GetObjectACLResp, GetObjectACL 작업의 반환입니다. |

```
std::string GetOwnerID();
std::string GetOwnerDisplayName();
std::vector<Grant> GetAccessControlList();

```

#### 예시

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string Object_name = "cpp_sdk_v5-123456789";

// GetObjectACLReq 생성자는 Object_name을 입력해야 합니다
qcloud_cos::GetObjectACLReq req(Object_name);
qcloud_cos::GetObjectACLResp resp;
qcloud_cos::CosResult result = cos.GetObjectACL(req, &resp);

// 호출에 성공할 경우 resp의 멤버 함수를 호출하여 반환 내용을 획득합니다
if (result.IsSucc()) {
    // ...
} else {
    // ACL 획득에 실패하면, CosResult의 멤버 함수를 호출하여 requestID 등의 오류 정보를 출력할 수 있습니다.
}
```

### Put Object Copy

#### 기능 설명

Put Object Copy 요청은 파일을 소스 경로에서 대상 경로로 복사하는 것을 구현합니다. 복사 과정에서 파일 기존 속성 및 ACL은 수정할 수 있습니다. 사용자는 이 API를 사용하여 파일 이동, 파일 이름 바꾸기, 파일 속성 수정 및 복사본 생성 등을 할 수 있습니다. 파일 크기는 1MB~5GB이 권장되며, 5GB를 초과하는 파일의 경우 멀티파트 업로드 Upload - Copy를 사용하십시오. 관련 API 문서는 [Put Object Copy](/document/product/436/10881)를 참조하십시오.

#### 방식 프로토타입

```cpp
CosResult PutObjectCopy(const PutObjectCopyReq& req, PutObjectCopyResp* resp);
```

#### 매개변수 설명

| 매개변수 | 매개변수 설명                                      |
| ---- | --------------------------------------------- |
| req  | PutObjectCopyReq, PutObjectCopy 작업의 요청입니다.  |
| resp | PutObjectCopyResp, PutObjectCopy 작업의 반환입니다. |

```
// 소스 파일 URL 경로, versionid 하위 리소스를 통해 이전 버전을 지정할 수 있습니다
void SetXCosCopySource(const std::string& str);

// 메타데이터 복사 여부, 열거형 값: Copy, Replaced, 기본값은 Copy입니다.
// 식별자가 Copy인 경우, Header의 사용자 메타데이터 정보를 무시하고 직접 복사합니다.
// 식별자가 Replaced인 경우, Header 정보에 따라 메타데이터를 수정합니다.
// 대상 경로와 기존 경로가 일치하고, 즉 사용자가 메타데이터를 수정하려면, Replaced여야 합니다
void SetXCosMetadataDirective(const std::string& str);

// Object가 지정된 시간 이후 수정될 때, 작업이 실행되고 그렇지 않으면 412가 반환됩니다.
// x-cos-copy-source-If-None-Match와 함께 사용할 수 있고, 다른 조건과 통합 사용하면 충돌이 반환됩니다.
void SetXCosCopySourceIfModifiedSince(const std::string& str);

// Object가 지정된 시간 후에 수정되지 않으면 작업이 실행되고, 그렇지 않으면 412가 반환됩니다.
// x-cos-copy-source-If-Match와 함께 사용할 수 있고, 다른 조건과 통합 사용하면 충돌이 반환됩니다.
void SetXCosCopySourceIfUnmodifiedSince(const std::string& str);

// Object의 Etag와 지정이 일치할 때, 작업을 실행하고 그렇지 않으면 412가 반환됩니다.
// x-cos-copy-source-If-Unmodified-Since와 함께 사용할 수 있고, 다른 조건과 통합 사용하면 충돌이 반환됩니다
void SetXCosCopySourceIfMatch(const std::string& str);

// Object의 Etag와 지정이 불일치할 때, 작업이 실행되고 그렇지 않으면 412가 반환됩니다.
// x-cos-copy-source-If-Modified-Since와 함께 사용할 수 있고, 다른 조건과 통합 사용하면 충돌이 반환됩니다.
void SetXCosCopySourceIfNoneMatch(const std::string& str);

// x-cos-storage-class를 통해 객체의 스토리지 클래스 설정, 열거형 값: STANDARD, STANDARD_IA
// 기본값: STANDARD(현재는 화남 지역만 지원됨)
void SetXCosStorageClass(const std::string& storage_class);

// Object 정의의 ACL 속성, 유효값: private, public-read-write, public-read
// 기본값: private
void SetXCosAcl(const std::string& str);

// 관한 부여받은 자에게 읽기 권한을 부여합니다. 형식: x-cos-grant-read: id=" ",id=" ".
// 서브 계정에 권한을 부여해야 할 경우, id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"
// 루트 계정에 권한을 부여해야 할 경우, id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"
void SetXCosGrantRead(const std::string& str);

// 권한 부여받은 자에게 쓰기 권한을 부여합니다. 형식: x-cos-grant-write: id=" ",id=" "./
// 서브 계정에 권한을 부여해야 할 경우, id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>",
// 루트 계정에 권한을 부여해야 할 경우, id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"
void SetXCosGrantWrite(const std::string& str);

// 권한 부여받은 자에게 쓰기 권한을 부여합니다. 형식: x-cos-grant-full-control: id=" ",id=" ".
// 서브 계정에 권한을 부여해야 할 경우, id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>",
// 루트 계정에 권한을 부여해야 할 경우, id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"
void SetXCosGrantFullControl(const std::string& str);

// 사용자 지정의 헤더 정보를 허용하며, 객체 메타데이터로 반환됩니다. 크기 제한은 2K입니다
void SetXCosMeta(const std::string& key, const std::string& value);

/// 서버 측 암호화에 사용되는 알고리즘 설정, 현재 AES256 지원
void SetXCosServerSideEncryption(const std::string& str);

```

```
// 파일의 MD5 알고리즘 검증값을 반환합니다. ETag의 값은 Object의 내용이 변경되었는지 확인하는 데 사용할 수 있습니다.
std::string GetEtag();

// 반환 파일의 마지막 수정 시간, GMT 형식
std::string GetLastModified();

// 버전 번호 반환
std::string GetVersionId();

/// 서버 측 암호화에 사용되는 알고리즘
std::string GetXCosServerSideEncryption();

```

#### 예시

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "cpp_sdk_v5-123456789";
std::string object_name = "sevenyou";

qcloud_cos::PutObjectCopyReq req(bucket_name, object_name);                                                                                                                       
req.SetXCosCopySource("sevenyousouthtest-12345656.cn-south.myqcloud.com/sevenyou_source_obj");
qcloud_cos::PutObjectCopyResp resp;
qcloud_cos::CosResult result = cos.PutObjectCopy(req, &resp);
```
