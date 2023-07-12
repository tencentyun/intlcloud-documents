## 개요

본 문서는 버킷, 객체의 액세스 제어에 대한 리스트(ACL) 관련 API 개요 및 SDK 샘플 코드를 제공합니다.

**버킷ACL**

| API                                                          | 작업명         | 작업 설명                                |
| ------------------------------------------------------------ | -------------- | --------------------------------------- |
| [PUT Bucket acl](https://intl.cloud.tencent.com/document/product/436/7737) | 버킷 ACL 설정 | 지정 버킷의 액세스 권한 제어 리스트(ACL) 설정 |
| [GET Bucket acl](https://intl.cloud.tencent.com/document/product/436/7733) |버킷 ACL 조회 | 지정 버킷의 액세스 권한 제어 리스트(ACL) 조회 |

**객체 ACL**

| API                                                          | 작업명       | 설명                                      |
| ------------------------------------------------------------ | ------------ | --------------------------------------------- |
| [PUT Object acl](https://intl.cloud.tencent.com/document/product/436/7748) | 객체 ACL 설정| 버킷의 한 객체의 액세스 제어 리스트 설정  |
| [GET Object acl](https://intl.cloud.tencent.com/document/product/436/7744) | 객체 ACL 조회 | 객체 액세스 제어 리스트 조회                |

## 버킷 ACL
### 버킷 ACL 설정

#### 기능 설명

지정 버킷의 액세스 권한 제어 리스트(PUT Bucket acl)를 설정합니다. 이 작업은 덮어쓰기 작업으로, 기존의 권한 설정을 덮어쓰기 합니다. ACL은 사전 정의된 권한 정책(CannedAccessControlList) 혹은 사용자 정의된 권한 제어(AccessControlList)를 포함합니다. 두 권한을 동시에 설정할 경우, 사전 정의된 정책을 무시하고 사용자 정의 정책을 메인으로 합니다.

#### 메소드 프로토타입 

```cpp
CosResult PutBucketACL(const PutBucketACLReq& request, PutBucketACLResp* response);
```

#### 요청 예시

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);
std::string bucket_name = "examplebucket-1250000000";

// PutBucketACLReq의 구조 함수에 bucket_name 입력 필요
qcloud_cos::PutBucketACLReq req(bucket_name);
qcloud_cos::PutBucketACLResp resp;

// ACL 구성을 설정합니다(충돌 방지를 위해 Body, Header 두 가지 방식 중 한 가지 선택)
// 1. header를 통해 ACL 설정
req.SetXCosAcl("public-read-write");

// 2. body를 통해 ACL 설정
qcloud_cos::Owner owner = {"qcs::cam::uin/00000000001:uin/00000000001", "qcs::cam::uin/00000000001:uin/00000000001" };
qcloud_cos::Grant grant;
req.SetOwner(owner);
grant.m_grantee.m_type = "Group";
grant.m_grantee.m_uri = "http://cam.qcloud.com/groups/global/AllUsers";
grant.m_perm = "READ";
req.AddAccessControlList(grant);

qcloud_cos::PutBucketACLResp resp;
qcloud_cos::CosResult result = cos.PutBucketACL(req, &resp);

if (result.IsSucc()) {
    // 요청 성공
} else {
    // 요청 실패 시, CosResult의 멤버 함수를 호출하여 오류 정보 출력. 예: requestID 등
} 
```

#### 매개변수 설명

| 매개변수 | 매개변수 설명            |  유형                                                        | 필수 입력 여부  |
| ---- | ------------------------| ----------------| ------|
| req  | PutBucketACL 작업의 요청  | PutBucketACLReq | 예    |
| resp | PutBucketACL 작업의 응답  | PutBucketACLResp| 예    |

PutBucketACLReq는 다음의 멤버 함수를 제공합니다.

```
// Bucket의 ACL 속성 정의. 유효 값: private, public-read-write, public-read
// 기본값: private
void SetXCosAcl(const std::string& str);

// 수여자에게 읽기 권한 부여. 형식: x-cos-grant-read: id=" ",id=" ".
// 서브 계정에 권한을 부여해야 하는 경우, id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"
// 루트 계정에 권한을 부여해야 하는 경우, id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"
void SetXCosGrantRead(const std::string& str);

// 수여자에게 쓰기 권한 부여. 형식: x-cos-grant-write: id=" ",id=" "./
// 서브 계정에 권한을 부여해야 하는 경우, id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>",
// 루트 계정에 권한을 부여해야 하는 경우, id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"
void SetXCosGrantWrite(const std::string& str);

// 수여자에게 읽기/쓰기 권한 부여. 형식: x-cos-grant-full-control: id=" ",id=" ".
// 서브 계정에 권한을 부여해야 하는 경우, id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>",
// 루트 계정에 권한을 부여해야 하는 경우, id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"
void SetXCosGrantFullControl(const std::string& str);

// Bucket 소유자 ID
void SetOwner(const Owner& owner);

// 수여자 정보 및 권한 정보 설정
void SetAccessControlList(const std::vector<Grant>& grants);

// 단일 Bucket의 인증 정보 추가
void AddAccessControlList(const Grant& grant);

```

>!SetXCosAcl, SetXCosGrantRead, SetXCosGrantWrite, SetXCosGrantFullControl과 같은 인터페이스와 SetAccessControlList 및 AddAccessControlList는 동시에 사용할 수 없습니다. 전자는 실제로 HTTP Header 설정을 통해 구현되고 후자는 Body에 XML 형식의 내용을 추가한 것이기 때문에 때문에 둘 중 하나만 선택할 수 있습니다. SDK 내부에서는 첫번째 종류를 우선 사용합니다.

해당 요청과 관련된 클래스 정의는 다음과 같습니다.

```
struct Owner {
    // 버킷 소유자 정보
    std::string m_id; // owner의 완전한 ID, 형식: qcs::cam::uin/<OwnerUin>:uin/<SubUin>
    std::string m_display_name;  // owner의 설명
};

struct Grantee {
    // type 유형: RootAccount, SubAccount
    // type 유형이 RootAccount인 경우 id의 uin에 계정 ID를 입력하거나 anyone(모든 유형의 사용자)으로 uin/<OwnerUin>, uin/<SubUin>을 대체할 수 있습니다.
    // type 유형이 RootAccount인 경우, uin은 루트 계정을 나타내고 Subaccount는 서브 계정을 나타냅니다.
    std::string m_type; 
    std::string m_id; // qcs::cam::uin/<OwnerUin>:uin/<SubUin>
    std::string m_display_name; // 선택사항
    std::string m_uri;
};

struct Grant {
    Grantee m_grantee; // 권한 수여자 리소스 정보
    std::string m_perm; // 수여자에게 부여된 권한 정보. 선택 가능한 값: ‘READ’, ‘WRITE’, ‘FULL_CONTROL’.
};

```

### 버킷 ACL 조회

#### 기능 설명

지정 버킷의 액세스 권한 리스트를 조회합니다.

#### 메소드 프로토타입

```cpp
CosResult GetBucketACL(const GetBucketACLReq& req, GetBucketACLResp* resp)
```

#### 요청 예시

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);
std::string bucket_name = "examplebucket-1250000000";

qcloud_cos::GetBucketACLReq req(bucket_name);
qcloud_cos::GetBucketACLResp resp;
qcloud_cos::CosResult result = cos.GetBucketACL(req, &resp);

if (result.IsSucc()) {
    // 요청 성공 시 resp의 멤버 함수를 호출하여 반환 내용 획득
} else {
    // 요청 실패 시, CosResult의 멤버 함수를 호출하여 오류 정보를 출력할 수 있음. 예: requestID 등
} 

```

#### 매개변수 설명

| 매개변수 | 매개변수 설명            |  유형                                                        | 필수 입력 여부  |
| ---- | ------------------------| ----------------| ------|
| req  | GetBucketACL 작업의 요청  | GetBucketACLReq | 예    |
| resp | GetBucketACL 작업의 응답  | GetBucketACLResp| 예    |


GetBucketACLResp 다음 멤버 함수를 제공합니다.

```
std::string GetOwnerID();
std::string GetOwnerDisplayName();
std::vector<Grant> GetAccessControlList();
```

## 객체 ACL


### 객체 ACL 설정

#### 기능 설명

버킷 내 객체의 액세스 제어 리스트 설정

>!현재 액세스 정책 항목은 1000개로 제한되어 있습니다. 객체 ACL 제어를 진행할 필요가 없으면 설정하지 마십시오. 기본적으로 Bucket 권한이 상속됩니다.

ACL은 사전 정의된 권한 정책(CannedAccessControlList) 혹은 사용자 정의된 권한 제어(AccessControlList)를 포함합니다. 두 권한이 동시에 설정될 경우, 사전 정의 정책은 무시되고 사용자 정의 정책이 메인이 됩니다.

#### 메소드 프로토타입

```cpp
CosResult PutObjectACL(const PutObjectACLReq& req, PutObjectACLResp* resp)
```

#### 요청 예시

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "examplebucket-1250000000";
std::string object_name = "test";

// 1 ACL 구성 설정(Body를 통해 Body와 Header의 두 가지 방식으로 ACL을 설정할 수 있지만 둘 중 하나만 선택할 수 있습니다. 그렇지 않으면 충돌이 발생합니다.)
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
    if (result.IsSucc()) {
        // 요청 성공
    } else {
        // 요청 실패 시, CosResult의 멤버 함수를 호출하여 오류 정보를 출력할 수 있음. 예: requestID 등
    } 
}   

// 2 ACL 구성 설정(Header를 통해 Body와 Header의 두 가지 방식으로 ACL을 설정할 수 있지만 둘 중 하나만 선택할 수 있습니다. 그렇지 않으면 충돌이 발생합니다.)
{   
    qcloud_cos::PutObjectACLReq req(bucket_name, object_name);                                                                                                                    
    req.SetXCosAcl("public-read-write");

    qcloud_cos::PutObjectACLResp resp;
    qcloud_cos::CosResult result = cos.PutObjectACL(req, &resp);
    if (result.IsSucc()) {
        // 요청 성공
    } else {
        // 요청 실패 시, CosResult의 멤버 함수를 호출하여 오류 정보를 출력할 수 있음. 예: requestID 등
    } 
}   
```


#### 매개변수 설명

| 매개변수 | 매개변수 설명                |  유형             | 필수 입력 여부  |
| ---- | ------------------------| -----------------| ------|
| req  | PutObjectACL 작업의 요청  | PuttObjectACLReq | 예    |
| resp | PutObjectACL 작업의 응답  | PutObjectACLResp | 예    |


PutObjectACLReq는 다음의 멤버 함수를 포함합니다.

```
// Object의 ACL 속성 정의. 유효 값: private, public-read
// 기본값: private
void SetXCosAcl(const std::string& str);

// 수여자에게 읽기 권한 부여. 형식: id="[OwnerUin]" 
void SetXCosGrantRead(const std::string& str);

// 수여자에게 모든 권한 부여. 형식: id="[OwnerUin]"
void SetXCosGrantFullControl(const std::string& str);

// Object 소유자 ID
void SetOwner(const Owner& owner);

// 권한 수여자 정보 및 권한 정보 설정
void SetAccessControlList(const std::vector<Grant>& grants);

// 단일 Object 의 권한 부여 정보 추가
void AddAccessControlList(const Grant& grant);

```

>!SetXCosAcl/SetXCosGrantRead/SetXCosGrantWrite/SetXCosGrantFullControl과 같은 인터페이스와 SetAccessControlList/AddAccessControlList는 동시에 사용할 수 없습니다. 전자는 실제로 HTTP Header 설정을 통해 구현되고 후자는 Body에 XML 형식의 내용을 추가한 것이기 때문에 때문에 둘 중 하나만 선택할 수 있습니다. SDK 내부에서는 첫번째 종류를 우선 사용합니다.

ACLRule 정의는 다음과 같습니다.

```
struct Grantee {
    // type 유형: RootAccount, SubAccount
    // type 유형이 RootAccount인 경우 id의 uin에 계정 ID를 입력하거나 anyone(모든 유형의 사용자)으로 uin/<OwnerUin>, uin/<SubUin>을 대체할 수 있습니다.
    // type 유형이 RootAccount인 경우, uin은 루트 계정을 나타내고 Subaccount는 서브 계정을 나타냅니다.
    std::string m_type; 
    std::string m_id; // qcs::cam::uin/<OwnerUin>:uin/<SubUin>
    std::string m_display_name; // 선택사항
    std::string m_uri;
};

struct Grant {
    Grantee m_grantee; // 권한 수여자 리소스 정보
    std::string m_perm; // 수여자에게 부여된 권한 정보. 선택 가능한 값: ‘READ’, ‘WRITE’, ‘FULL_CONTROL’.
};

```

### 객체 ACL 조회

#### 기능 설명

객체 액세스 제어 리스트 조회

#### 메소드 프로토타입

```cpp
CosResult GetObjectACL(const GetObjectACLReq& req, GetObjectACLResp* resp)
```

#### 요청 예시

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "examplebucket-1250000000";
std::string object_name = "exampleobject";

// GetObjectACLReq의 구조 함수는 Object_name을 전달해야 합니다.
qcloud_cos::GetObjectACLReq req(bucket_name, object_name);
qcloud_cos::GetObjectACLResp resp;
qcloud_cos::CosResult result = cos.GetObjectACL(req, &resp);

if (result.IsSucc()) {
    // 요청 성공 시 resp의 멤버 함수를 호출하여 반환 내용 획득
} else {
    // 요청 실패 시, CosResult의 멤버 함수를 호출하여 오류 정보를 출력할 수 있음. 예: requestID 등
} 
```

#### 매개변수 설명

| 매개변수 | 매개변수 설명            |  유형                                                        | 필수 입력 여부  |
| ---- | ------------------------| ----------------| ------|
| req  | GetObjectACL 작업의 요청  | GetObjectACLReq | 예    |
| resp | GetObjectACL 작업의 응답  | GetObjectACLResp| 예    |


GetObjectACLResp는 다음의 멤버 함수를 포함합니다.

```
std::string GetOwnerID();
std::string GetOwnerDisplayName();
std::vector<Grant> GetAccessControlList();
```
