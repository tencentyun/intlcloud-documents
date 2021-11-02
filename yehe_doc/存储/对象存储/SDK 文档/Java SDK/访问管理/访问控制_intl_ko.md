## 소개

본 문서는 버킷, 객체의 액세스 제어에 대한 리스트(ACL) 관련 API 개요 및 SDK 샘플 코드를 제공합니다.

**버킷 ACL**

| API                                                          | 작업 이름         | 작업 설명                   |
| :----------------------------------------------------------- | :------------- | :----------------------------- |
| [PUT Bucket acl](https://intl.cloud.tencent.com/document/product/436/7737) | 버킷ACL 설정 | 지정 버킷 액세스 권한 제어 리스트 설정 |
| [GET Bucket acl](https://intl.cloud.tencent.com/document/product/436/7733) | 버킷 ACL 조회 | 버킷 액세스 제어 리스트 조회       |

**객체 ACL**

| API                                                          | 작업명       | 작업 설명                                      |
| ------------------------------------------------------------ | ------------ | --------------------------------------------- |
| [PUT Object acl](https://intl.cloud.tencent.com/document/product/436/7748) | 객체 ACL 설정| 버킷의 특정 객체의 액세스 제어 리스트 설정 |
| [GET Object acl](https://intl.cloud.tencent.com/document/product/436/7744) | 객체 ACL 조회 | 객체 액세스 제어 리스트 조회             |

## 버킷 ACL
### 버킷 ACL 설정

#### 기능 설명

지정 버킷의 액세스 권한 제어 리스트(PUT Bucket acl)를 설정합니다. 이 작업은 덮어쓰기 작업으로, 기존의 권한 설정을 덮어쓰기 합니다. ACL은 사전 정의된 권한 정책(CannedAccessControlList) 혹은 사용자 정의된 권한 제어(AccessControlList)를 포함합니다. 두 권한을 동시에 설정할 경우, 사전 정의된 정책을 무시하고 사용자 정의 정책을 메인으로 합니다.

#### 메소드 프로토타입

```java
// 방법 1 (사용자 정의 정책 설정)
public void setBucketAcl(String bucketName, AccessControlList acl)
  throws CosClientException, CosServiceException;
// 방법 2 (사전 정의된 정책 설정)
public void setBucketAcl(String bucketName, CannedAccessControlList acl) throws CosClientException, CosServiceException;
// 방법 3 (위의 두 가지 방법의 캡슐화는 두 가지 정책 설정이 포함되어 있습니다. 동시 설정 시 사용자 정의 정책이 메인으로 설정됩니다.)
public void setBucketAcl(SetBucketAclRequest setBucketAclRequest) 
  throws CosClientException, CosServiceException;
```

#### 요청 예시

[//]: # (.cssg-snippet-put-bucket-acl)
```java
// bucket의 이름 생성 규칙은 BucketName-APPID입니다. 여기에 입력되는 버킷 이름은 반드시 해당 형식을 따라야 합니다.
String bucketName = "examplebucket-1250000000";
// 사용자 정의 ACL 설정
AccessControlList acl = new AccessControlList();
Owner owner = new Owner();
// uin 콘솔에서 확인 가능: https://console.cloud.tencent.com/developer
owner.setId("qcs::cam::uin/100000000001:uin/100000000001");
acl.setOwner(owner);
String id = "qcs::cam::uin/100000000001:uin/100000000001";
UinGrantee uinGrantee = new UinGrantee("qcs::cam::uin/100000000001:uin/100000000001");
uinGrantee.setIdentifier(id);
acl.grantPermission(uinGrantee, Permission.FullControl);
cosClient.setBucketAcl(bucketName, acl);

// 사전 정의된 ACL 설정
// 개인 읽기/쓰기 설정(새로 생성된 bucket은 개인 읽기/쓰기 설정이 기본값)
cosClient.setBucketAcl(bucketName, CannedAccessControlList.Private);
// 공개 읽기 및 개인 쓰기 설정
cosClient.setBucketAcl(bucketName, CannedAccessControlList.PublicRead);
// 공개 읽기/쓰기 설정
cosClient.setBucketAcl(bucketName, CannedAccessControlList.PublicReadWrite);
```


#### 매개변수 설명

방법3 매개변수는 1과 2를 포함하므로 방법3을 예로 들어 소개하겠습니다.

| 매개변수 이름            | 설명           | 유형                |
| ------------------- | -------------- | ------------------- |
| setBucketAclRequest | 권한 설정 요청 | SetBucketAclRequest |

Request 멤버 설명:

| Request 멤버 | 설정 방법            | 설명                                                         | 유형                    |
| ------------ | ------------------- | ------------------------------------------------------------ | ----------------------- |
| bucketName   | 구조 함수 혹은 set 메소드 | Bucket의 이름 생성 규칙은 BucketName-APPID이며 자세한 내용은 [버킷 개요](https://intl.cloud.tencent.com/document/product/436/13312) 참고 | String                  |
| acl          | 구조 함수 혹은 set 메소드 | 사용자 정의 권한 정책                                               | AccessControlList       |
| cannedAcl    | 구조 함수 혹은 set 메소드 | 공개 읽기, 공개 읽기/쓰기, 개인 읽기 등 사전 정의된 정책                         | CannedAccessControlList |

| 구성원 이름         | 설명                            | 유형     |
| -------------- | ------------------------------- | -------- |
| List&lt;Grant> | 모든 권한 부여 정보 포함            | 배열     |
| owner          | Object 혹은 Owner 의 소유자 표시 | Owner 클래스 |

Grant 클래스의 구성원 설명:

| 구성원 이름     | 설명                                       | 유형       |
| ---------- | ------------------------------------------ | ---------- |
| grantee    | 권한 수여자의 개인 정보                         | Grantee    |
| permission | 권한 수여자의 권한 정보(읽기 가능, 쓰기 가능, 읽기/쓰기 가능 등) | Permission |

Owner 클래스의 구성원 설명:

| 구성원 이름      | 설명                           | 유형   |
| ----------- | ------------------------------ | ------ |
| id          | 소유자의 개인 정보               | String |
| displayname | 소유자의 이름(지금의 id와 동일) | String |

CannedAccessControlList는 사전 설정한 정책을 모든 사람에게 공개합니다. 열거 유형이며, 열거 값은 다음과 같습니다.

| 열거 값          | 설명                                             |
| --------------- | ------------------------------------------------ |
| Private         | 개인 읽기/쓰기(owner만 읽기/쓰기 가능)                  |
| PublicRead      | 공개 읽기 및 개인 쓰기(owner는 읽기와 쓰기 가능, 다른 클라이언트는 읽기만 가능) |
| PublicReadWrite | 공개 읽기/쓰기(누구나 읽기/쓰기 가능)                   |

#### 반환 결과 설명

- 성공: 반환값 없음.
- 실패: 오류 발생(예: 실명 인증 실패), CosClientException 또는 CosServiceException 오류 발생. 자세한 내용은 [오류 해결](https://intl.cloud.tencent.com/document/product/436/31537)을 참고하십시오.


### 버킷 ACL 조회

#### 기능 설명

지정 버킷의 액세스 권한 리스트를 조회합니다.

#### 메소드 프로토타입

```plaintext
public AccessControlList getBucketAcl(String bucketName)
       throws CosClientException, CosServiceException
```

#### 요청 예시

[//]: # (.cssg-snippet-get-bucket-acl)
```java
// bucket의 이름 생성 규칙은 BucketName-APPID입니다. 여기에 입력되는 버킷 이름은 반드시 해당 형식을 따라야 합니다.
String bucketName = "examplebucket-1250000000";
AccessControlList accessControlList = cosClient.getBucketAcl(bucketName);
//버킷 권한을 사전 설정 ACL로 전환하면 다음과 같은 선택지를 얻을 수 있습니다: Private, PublicRead, PublicReadWrite
CannedAccessControlList cannedAccessControlList = accessControlList.getCannedAccessControl();
```


#### 매개변수 설명

| 매개변수 이름   | 설명                                                         | 유형   |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | Bucket의 이름 생성 형식은 BucketName-APPID이며, 자세한 내용은 [버킷 이름 생성 규칙](https://intl.cloud.tencent.com/document/product/436/13312#.E5.AD.98.E5.82.A8.E6.A1.B6.E5.91.BD.E5.90.8D.E8.A7.84.E8.8C.83) 참고 | String |

#### 반환 결과 설명

- 성공: 하나의 Bucket ACL 반환. 
- 실패: 오류 발생(예: 실명 인증 실패), CosClientException 또는 CosServiceException 오류 발생. 자세한 내용은 [오류 해결](https://intl.cloud.tencent.com/document/product/436/31537)을 참고하십시오.

## 객체 ACL


### 객체 ACL 설정

#### 기능 설명

버킷 내 객체의 액세스 제어 리스트를 설정합니다.

ACL은 사전 정의된 권한 정책(CannedAccessControlList) 혹은 사용자 정의된 권한 제어(AccessControlList)를 포함합니다. 두 권한이 동시에 설정될 경우, 사전 정의 정책은 무시되고 사용자 정의 정책이 메인이 됩니다.

#### 메소드 프로토타입

```java
// 방법 1 (사용자 정의 정책 설정)
public void setObjectAcl(String bucketName, String key, AccessControlList acl)
       throws CosClientException, CosServiceException
// 방법 2 (사전 정의된 정책 설정)
public void setObjectAcl(String bucketName, String key, CannedAccessControlList acl)
       throws CosClientException, CosServiceException
// 방법 3 (위의 두 가지 방법의 캡슐화는 두 가지 정책 설정이 포함되어 있습니다. 동시 설정 시 사용자 정의 정책이 메인으로 설정됩니다.)
public void setObjectAcl(SetObjectAclRequest setObjectAclRequest)
  throws CosClientException, CosServiceException;
```

#### 요청 예시

[//]: # (.cssg-snippet-put-object-acl)
```java
// 권한 정보 중 개인 정보 형식에 대한 요구가 있을 경우, 루트 계정과 서브 계정에 대한 표준은 다음과 같습니다.
// uin 콘솔에서 확인 가능: https://console.cloud.tencent.com/developer
// 아래의 root_uin과 sub_uin은 반드시 유효한 UIN 계정이어야 합니다.
// 루트 계정 qcs::cam::uin/<root_uin>:uin/<root_uin>는 루트 계정 root_uin의 사용자를 표시합니다(앞뒤의 uin도 동일).
//  예시: qcs::cam::uin/100000000001:uin/100000000001
// 서브 계정 qcs::cam::uin/<root_uin>:uin/<sub_uin>는 root_uin의 서브 계정 sub_uin 클라이언트를 표시합니다.
//  예시: qcs::cam::uin/100000000001:uin/100000000011 
// 버킷의 이름 생성 형식: BucketName-APPID
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";
// 사용자 정의 ACL 설정
AccessControlList acl = new AccessControlList();
Owner owner = new Owner();
// owner의 정보를 설정합니다. owner는 루트 계정만 할 수 있습니다.
owner.setId("qcs::cam::uin/100000000001:uin/100000000001");
acl.setOwner(owner);

// 루트 계정 100000000001에 읽고 쓰는 권한을 부여할 수 있습니다.
UinGrantee uinGrantee1 = new UinGrantee("qcs::cam::uin/100000000001:uin/100000000001");
acl.grantPermission(uinGrantee1, Permission.FullControl);
cosClient.setObjectAcl(bucketName, key, acl);

// 사전 정의된 ACL 설정
// 개인 읽기/쓰기 설정(Object의 권한으로 Bucket 통합 묵인)
cosClient.setObjectAcl(bucketName, key, CannedAccessControlList.Private);
// 공개 읽기 및 개인 쓰기 설정
cosClient.setObjectAcl(bucketName, key, CannedAccessControlList.PublicRead);
// 공개 읽기/쓰기 설정
cosClient.setObjectAcl(bucketName, key, CannedAccessControlList.PublicReadWrite);
```


#### 매개변수 설명

- **방법3** 매개변수는 1과 2를 포함하므로 방법3을 예로 들어 소개하겠습니다.

| 매개변수 이름            | 설명   | 유형                |
| ------------------- | ------ | ------------------- |
| SetObjectAclRequest | 요청 | setObjectAclRequest |

Request 멤버 설명:

| Request 멤버 | 설정 방법          | 설명                                                         | 유형           |
| ------------ | ------------------- | ------------------------------------------------------------ | ----------------------- |
| bucketName   | 구조 함수 혹은 set 메소드 | 버킷의 이름 생성 형식은 BucketName-APPID이며, 자세한 내용은 [버킷 이름 생성 규칙](https://intl.cloud.tencent.com/document/product/436/13312#.E5.AD.98.E5.82.A8.E6.A1.B6.E5.91.BD.E5.90.8D.E8.A7.84.E8.8C.83) 참고 | String                  |
| key          | 구조 함수 혹은 set 메소드 | 객체 키(Key)는 버킷에 있는 객체의 고유 표식입니다. 예를 들어, 객체의 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg` 에서, 객체 키는 doc/picture.jpg입니다. 자세한 내용은 [객체 키](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오. | String                  |
| acl          | 구조 함수 혹은 set 메소드 | 사용자 정의 권한 정책                                               | AccessControlList       |
| cannedAcl    | 구조 함수 혹은 set 메소드 | 공개 읽기, 공개 읽기/쓰기, 개인 읽기 등 사전 정의된 정책                         | CannedAccessControlList |

| 구성원 이름         | 설명                            | 유형     |
| -------------- | ------------------------------- | -------- |
| List&lt;Grant> | 모든 권한 부여 정보 포함            | 배열     |
| owner          | Object 또는 Owner 의 소유자 표시 | Owner 클래스 |

Grant 클래스의 구성원 설명:

| 구성원 이름     | 설명                                         | 유형       |
| ---------- | -------------------------------------------- | ---------- |
| grantee    | 권한 수여자의 개인 정보                         | Grantee    |
| permission | 권한 수여자의 권한 정보(읽기 가능, 쓰기 가능, 읽기/쓰기 가능 등) | Permission |

Owner 클래스의 구성원 설명:

| 구성원 이름      | 설명                           | 유형   |
| ----------- | ------------------------------ | ------ |
| id          | 소유자의 개인 정보               | String |
| displayname | 소유자의 이름(지금의 id와 동일) | String |

CannedAccessControlList는 사전 설정한 정책을 모든 사람에게 공개합니다. 열거 유형이며, 열거 값은 다음과 같습니다.

| 열거 값          | 설명                                             |
| --------------- | ------------------------------------------------ |
| Private         | 개인 읽기/쓰기(owner만 읽기/쓰기 가능)                  |
| PublicRead      | 공개 읽기 및 개인 쓰기(owner는 읽기와 쓰기 가능, 다른 클라이언트는 읽기만 가능) |
| PublicReadWrite | 공개 읽기/쓰기(누구나 읽기/쓰기 가능)                   |

#### 반환 결과 설명

- 성공: 반환값 없음.
- 실패: 오류 발생(예: 실명 인증 실패). CosClientException 또는 CosServiceException 오류 발생. 자세한 내용은 [오류 해결](https://intl.cloud.tencent.com/document/product/436/31537)을 참고하십시오.

### 객체 ACL 조회

#### 기능 설명

객체의 액세스 제어 리스트를 조회합니다.

#### 메소드 프로토타입

```java
public AccessControlList getObjectAcl(String bucketName, String key)
  throws CosClientException, CosServiceException;
```

#### 요청 예시

[//]: # (.cssg-snippet-get-object-acl)
```java
// 버킷의 이름 생성 형식: BucketName-APPID
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";
AccessControlList accessControlList = cosClient.getObjectAcl(bucketName, key);
//파일 권한을 사전 설정 ACL로 전환하면 Private, PublicRead, Default와 같은 선택값을 얻을 수 있습니다.
CannedAccessControlList cannedAccessControlList = accessControlList.getCannedAccessControl();
```


#### 매개변수 설명

| 매개변수 이름   | 설명                                                         | 유형   |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | Bucket의 이름 생성 형식은 BucketName-APPID이며, 자세한 내용은 [버킷 이름 생성 규칙](https://intl.cloud.tencent.com/document/product/436/13312#.E5.AD.98.E5.82.A8.E6.A1.B6.E5.91.BD.E5.90.8D.E8.A7.84.E8.8C.83) 참고 | String |
| key        | 객체 키(Key)는 버킷에 있는 객체의 고유 표식입니다. 예를 들어, 객체의 액세스 도메인`examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`에서, 객체 키는 doc/picture.jpg입니다. 자세한 내용은 [객체 키](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오. | String |

#### 반환 결과 설명

- 성공: 하나의 Object가 있는 ACL 반환.
- 실패: 오류 발생(예: 실명 인증 실패), CosClientException 또는 CosServiceException 오류 발생. 자세한 내용은 [오류 해결](https://intl.cloud.tencent.com/document/product/436/31537)을 참고하십시오.
