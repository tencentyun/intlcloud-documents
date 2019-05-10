## 기본 개념

ACL은 XML 언어를 사용하여 설명하며 리소스와 연결된 권한 부여자 지정 및 권한 부여 리스트입니다. 매개 버킷과 객체는 모두 이에 연결되는 ACL은 익명 사용자 또는 기타 Tencent Cloud 루트 계정에 기본 읽기/쓰기 권한 부여를 지원합니다.

>! 리소스에 연결된 ACL 관리 사용에는 몇 가지 제한이 있습니다.
>- 리소스 소유자는 리소스에 대한 FULL_CONTROL 권한을 항상 갖고 있으며 취소 또는 수정할 수 없습니다.
>- 익명 사용자는 리소스 소유자가 될 수 없으며 이때 객체 리소스의 소유자는 버킷 생성자(Tencent Cloud 루트 계정)에 속합니다.
>- 오직 Tencent Cloud의 CAM 루트 계정 또는 익명 사용자에게만 권한을 부여할 수 있으며 서브 사용자 또는 사용자 그룹에는 권한을 부여할 수 없습니다.
>- 권한 조건 추가를 지원하지 않습니다.
>- 명시적 거절 권한을 지원하지 않습니다.
>- 하나의 리소스는 최대 100개의 ACL 정책을 가질 수 있습니다.

## ACL 요소

### 피부여자

지원하는 권한 피부여자는 CAM 루트 계정 또는 사전 정의 CAM 사용자 그룹일 수 있습니다.

>!
>- 다른 Tencent Cloud 루트 계정에 접근 권한을 부여했을 경우, 권한을 부여받은 해당 루트 계정은 이 계정의 서브 사용자, 사용자 그룹 또는 역할의 접근 권한을 부여할 수 있습니다.
>- COS는 익명 사용자 또는 CAM 사용자 그룹에 WRITE, WRITE_ACP 또는 FULL_CONTROL 권한을 부여하는 것을 절대 권장하지 않습니다. 일단 권한 부여가 허용되면 사용자 그룹은 리소스에 업로드, 다운로드, 삭제 등 행위가 진행될 수 있으므로 데이터 유실, 비용 차감 등의 위험이 따릅니다.


버킷 또는 객체의 ACL에서 권한 부여를 지원하는 피부여자는 다음을 포함합니다.

- 계정 간: 루트 계정 ID를 사용하여 [계정 센터]의 [계정 정보](https://console.cloud.tencent.com/developer)에서 [계정 ID]를 획득하십시오. 예: `398626565`.
- 사전 정의된 사용자 그룹: URI 태그를 사용하여 사전 정의된 사용자 그룹을 플래그하십시오. 지원하는 사용자 그룹은 다음을 포함합니다.
  - 익명 사용자 그룹 - `http://cam.qcloud.com/groups/global/AllUsers`, 이 그룹은 세계적으로 모든 사람이 권한 부여를 받을 필요가 없으며, 요청 서명 여부에 상관없이 리소스에 접근 가능함을 의미합니다.
  - 인증된 사용자 그룹 -`http://cam.qcloud.com/groups/global/AuthenticatedUsers`. 이 그룹은 Tencent Cloud CAM 계정 인증을 거친 모든 사용자가 모두 리소스 접근이 가능함을 의미합니다.


### 작업 권한

Tencent Cloud COS가 리소스 ACL 에서 지원하는 작업은 실질적으로 일련의의 작업 집합입니다. 버킷과 객체 ACL에 있어서 각각 다른 함의를 의미합니다.

**버킷의 작업**

다음은 버킷 ACL에서 지원하는 설정 작업 리스트입니다.

| 작업 집합       | 설명                 | 허용하는 행위                                                   |
| ------------ | -------------------- | ------------------------------------------------------------ |
| READ         | 객체 나열             | GetBucket, HeadBucket, GetBucketObjectVersions, ListMultipartUploads |
| WRITE        | 객체 업로드, 덮어쓰기 및 삭제 | PutObject, PutObjectCopy, PostObject, InitiateMultipartUpload, UploadPart, UploadPartCopy, CompleteMultipartUpload, DeleteObject |
| READ_ACP     | 버킷의 ACL 읽기     | GetBucketAcl                                                 |
| WRITE_ACP    | 버킷의 ACL 쓰기     | PutBucketAcl                                                 |
| FULL_CONTROL | 상기 4가지 권한의 집합   | 상기 모든 행위의 집합                                           |

>!버킷의 WRITE, WRITE_ACP 또는 FULL_CONTROL 권한을 신중히 부여하십시오. 버킷의 WRITE 권한을 부여하면 권한을 부여받은 자가 기존의 모든 객체를 덮어쓰기하거나 삭제하는 것을 허용합니다.

** 객체 작업**

다음은 객체 ACL 에서 지원하는 설정 리스트입니다.

| 작업 집합       | 설명             | 허용하는 행위                        |
| ------------ | ------------------ | --------------------------------------- |
| READ         | 객체 읽기           | GetObject, GetObjectVersion, HeadObject |
| READ_ACP     | 객체의 ACL 읽기     | GetObjectAcl, GetObjectVersionAcl       |
| WRITE_ACP    | 객체의 ACL 쓰기    | PutObjectAcl, PutObjectVersionAcl       |
| FULL_CONTROL | 상기 4가지 권한의 집합 | 상기 모든 행위의 집합                      |

>! 객체는 작업 집합의 WRITE 부여를 지원하지 않습니다.

### 사전 정의된 ACL

Tencent Cloud COS는 일련의 사전 정의된 ACL의 권한 부여를 지원하며 이는 간단한 권한의 설명에 큰 편리를 제공합니다. 사전 정의된 ACL을 설명할 때, PUT Bucket/Object 또는 PUT Bucket/Object ACL에 `x-cos-acl` 헤더가 있어야 하며 필요한 권한을 설명해야 합니다. 만약 동시에 요청 본문이 XML의 서술 내용이 가질 경우, 헤더의 서술을 우선 선택하고 요청 본문의 XML 설명은 무시합니다.

**버킷의 사전 정의된 ACL**

| 사전 정의 이름           | 설명                                                         |
| ------------------ | ------------------------------------------------------------ |
| private                   | 생성자(루트 계정)가 FULL_CONTROL 권한을 가지며 다른 사용자는 권한이 없습니다(기본) |
| public-read               | 생성자가 FULL_CONTROL 권한을 가지며 익명 사용자 그룹은 READ 권한을 가집니다.     |
| public-read-write  | 생성자와 익명 사용자 그룹은 모두 FULL_CONTROL 권한을 가지며 일반적으로 이 권한의 부여를 권장하지 않습니다. |
| authenticated-read             | 생성자가 FULL_CONTROL 권한을 가지며 인증 사용자 그룹은 READ 권한을 가집니다.     |

**객체의 사전 정의된 ACL**

| 사전 설정 이름           | 설명                                                         |
| ------------------------- | ------------------------------------------------------------ |
| default                   | 설명이 비어 있음. 이때, 요청은 허용된 버킷 또는 서브 사용자 정책에 따르며 선언이 없으면 거부합니다. |
| private                   | 생성자(루트 계정)가 FULL_CONTROL 권한을 가지며며 다른 사용자는 권한이 없습니다.  |
| public-read               | 생성자가 FULL_CONTROL 권한을 가지며 익명 사용자 그룹은 READ 권한을 가집니다.     |
|  authenticated-read             | 생성자가 FULL_CONTROL 권한을 가지며 인증 사용자 그룹이 READ 권한을 가집니다.     |
|  bucket-owner-read            | 생성자가 FULL_CONTROL 권한을 가지며 버킷 소유자가 READ 권한을 가집니다.     |
| bucket-owner-full-control | 생성자와 버킷 소유자가 모두 FULL_CONTROL 권한을 가집니다.             |

>!객체는 public-read-write의 권한 부여를 지원하지 않습니다.

## 예시
### 버킷의 ACL
버킷 생성 시, COS는 하나의 기본 ACL을 생성하여 리소스 소유자에게 리소스의 완전 제어 권한(FULL_CONTROL)을 부여합니다. 예시는 다음과 같습니다.

```xml
<AccessControlPolicy>
  <Owner>
    <ID>Owner-Cononical-CAM-User-Id</ID>
  </Owner>
  <AccessControlList>
    <Grant>
      <Grantee>
        <ID>Owner-Cononical-CAM-User-Id</ID>
      </Grantee>
      <Permission>FULL_CONTROL</Permission>
    </Grant>
  </AccessControlList>
</AccessControlPolicy>
```

### 객체의 ACL

** 객체 생성 시, COS는 기본으로 ACL을 생성하지 않으며 이때 객체의 소유자는 버킷 소유자입니다. **객체가 버킷의 권한을 계승하며 버킷의 접근 권한과 일치합니다. 객체는 기본 ACL이 없기 때문에 버킷 정책(Bucket Policy)중 접근자와 그 행위에 대한 정의에 따라 요청의 허용 여부를 판단합니다. 자세한 내용은 [접근 정책 언어 개요](https://cloud.tencent.com/document/product/436/18023) 문서를 참조하십시오.

객체에 다른 접근 권한을 부여할 경우, 이를 기반하여 더 많은 ACL을 추가하여 객체의 접근 권한을 설명할 수 있습니다. 예: 익명 사용자의 단일 객체 읽기 전용 권한 부여. 예시는 다음과 같습니다.

```xml
<AccessControlPolicy>
  <Owner>
    <ID>Owner-Cononical-CAM-User-Id</ID>
  </Owner>
  <AccessControlList>
    <Grant>
      <Grantee>
        <ID>Owner-Cononical-CAM-User-Id</ID>
      </Grantee>
      <Permission>FULL_CONTROL</Permission>
    </Grant>
    <Grant>
      <Grantee>
        <URI>http://cam.qcloud.com/groups/global/AllUsers</URI>
      </Grantee>
      <Permission>READ</Permission>
    </Grant>
  </AccessControlList>
</AccessControlPolicy>
```


