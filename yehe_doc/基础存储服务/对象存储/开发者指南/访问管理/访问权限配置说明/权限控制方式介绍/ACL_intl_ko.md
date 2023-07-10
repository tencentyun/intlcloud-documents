## 기본 개념

액세스 제어 리스트(ACL)는 XML 언어를 사용하며, 리소스와 관련된 권한 부여자 및 권한 수여자 리스트입니다. 각각의 버킷과 객체에는 모두 이와 관련된 ACL이 있으며, 익명 사용자나 다른 Tencent Cloud의 루트 계정에 기본적인 읽기 및 쓰기 권한을 부여합니다.

>! 리소스와 관련된 ACL 관리에는 다음과 같은 제한이 있습니다.
>- 리소스 소유자는 항상 리소스에 대해 FULL_CONTROL 권한을 가지며, 권한을 철회 또는 수정할 수 없습니다.
>- 익명 사용자는 리소스 소유자가 될 수 없으며, 이때 객체 리소스의 소유자는 버킷의 생성자(Tencent Cloud 루트 계정)에 속합니다.
>- Tencent Cloud CAM(Cloud Access Management) 루트 계정 또는 사전 설정 사용자 그룹에만 권한을 부여할 수 있으며 사용자 정의 사용자 그룹에는 권한을 부여할 수 없으므로 서브 계정에게 권한을 부여하지 않는 것이 좋습니다.
>- 권한에 대한 추가 조건은 지원하지 않습니다.
>- 거부 표시 권한은 지원하지 않습니다.
>- 하나의 리소스는 최대 100개의 ACL 정책을 가질 수 있습니다.
>

## 적용 시나리오

>! 공개 익명 사용자 액세스(공개 읽기)는 매우 위험한 작업으로 트래픽 도용의 리스크가 있으므로 공개 읽기를 사용해야 하는 경우 보안을 위해 [링크 도용 방지 설정](https://intl.cloud.tencent.com/document/product/436/13319)을 할 수 있습니다.
>

간단한 액세스 권한을 설정하거나 또는 버킷 및 객체에 대한 익명 액세스를 개방해야 하는 경우 ACL을 선택하십시오. 그러나 더 많은 경우에는 더 유연한 버킷 정책 또는 사용자 정책을 먼저 사용하는 것이 좋습니다. ACL에 적용 가능한 시나리오는 다음과 같습니다.

- 단순 액세스 권한만 설정합니다.
- 콘솔에서 액세스 권한을 빠르게 설정합니다.
- 모든 익명의 인터넷 사용자에게 객체, 디렉터리 또는 버킷을 개방하며 ACL 작업이 더 편리합니다.


## ACL의 요소

### 자격 Grantee

CAM의 루트 계정 또는 사전 설정된 CAM 사용자 그룹은 권한을 수여할 수 있습니다.

>!
>- 기타 Tencent Cloud 루트 계정에 액세스 권한을 부여했을 때, 이 권한을 받은 루트 계정은 해당 루트 계정에 속해 있는 서브 계정, 사용자 그룹 또는 역할에 액세스 권한을 부여할 수 있습니다.
>- COS(Cloud Object Storage)는 익명 사용자 또는 CAM 사용 그룹에 WRITE, WRITE_ACP 또는 FULL_CONTROL 권한 부여를 권장하지 않습니다. 권한 부여를 허용하면 사용자 그룹이 귀하의 리소스를 업로드/다운로드/삭제할 수 있고 이로 인해 데이터 손실, 비용 차감 등 리스크가 발생할 수 있습니다.
>


버킷 또는 객체의 ACL에서 권한을 수여할 수 있는 자격은 다음을 포함합니다.

- 계정 간: 루트 계정의 ID를 사용하고, **계정 센터**의 [계정 정보](https://console.cloud.tencent.com/developer)를 통해 계정 ID를 받으십시오. (예시: 100000000001)
- 사전 설정 사용자 그룹: URI 태그를 사용해 사전 설정된 사용자 그룹을 표기하십시오. 지원되는 사용자 그룹은 다음을 포함합니다.
  - 익명 사용자 그룹 - `http://cam.qcloud.com/groups/global/AllUsers` 해당 그룹은 요청에 서명을 했든지 안 했든지, 누구나 권한 부여 없이 리소스에 액세스할 수 있다는 의미입니다.
  - 인증 사용자 그룹 - `http://cam.qcloud.com/groups/global/AuthenticatedUsers` 해당 그룹은 Tencent Cloud CAM 계정의 인증을 거친 사용자는 모두 리소스에 액세스할 수 있다는 의미입니다.


### 작업 Permission

Tencent Cloud COS가 리소스 ACL에서 지원하는 작업은 사실상 일련의 작업 그룹으로, 버킷 및 객체 ACL에는 각각 다른 의미를 갖습니다.

**버킷의 작업**

아래 표는 버킷 ACL에서 설정을 지원하는 작업 리스트입니다.

| 작업 그룹       | 설명            | 허용된 동작                                                   |
| ------------ | -------------------- | ------------------------------------------------------------ |
| READ         | 객체 나열         |  HeadBucket, GetBucketObjectVersions, ListMultipartUploads |
| WRITE        | 객체 업로드, 덮어쓰기 및 삭제 | PutObject, PutObjectCopy, PostObject, InitiateMultipartUpload, UploadPart, UploadPartCopy, CompleteMultipartUpload, DeleteObject |
| READ_ACP     | 버킷의 ACL 읽기     | GetBucketAcl                                                 |
| WRITE_ACP    | 버킷의 ACL 쓰기     | PutBucketAcl                                                 |
| FULL_CONTROL | 이상 네 가지 권한의 집합   | 이상 모든 동작의 집합                                           |

>! 버킷의 WRITE, WRITE_ACP 또는 FULL_CONTROL 권한 부여에 신중하시기 바랍니다. 버킷에 부여된 WRITE 권한은 권한 수여자 모든 객체를 덮어쓰기 또는 삭제할 수 있도록 허용합니다.
>

**객체의 작업**

아래 표는 객체 ACL에서 설정을 지원하는 작업 리스트입니다.

| 작업 그룹       | 설명               | 허용된 동작                              |
| ------------ | ------------------ | --------------------------------------- |
| READ         | 객체 읽기         | GetObject, GetObjectVersion, HeadObject |
| READ_ACP     | 객체의 ACL 읽기     | GetObjectAcl, GetObjectVersionAcl       |
| WRITE_ACP    | 객체의 ACL 쓰기     | PutObjectAcl, PutObjectVersionAcl       |
| FULL_CONTROL | 이상 세 가지 권한의 집합 | 이상 모든 동작의 집합                      |

>?객체는 WRITE 작업 그룹 권한 부여를 지원하지 않습니다.

### 사전 설정한 ACL

COS는 일련의 사전 설정된 ACL에 대한 권한 부여를 지원하며 간단한 권한을 쉽게 설명할 수 있습니다. ACL 사전 설정을 사용할 때, PUT Bucket/Object 또는 PUT Bucket/Object acl에서 x-cos-acl 헤더를 가져옴과 동시에 필요한 권한을 설명합니다. 만약 동시에 본문 요청 중 XML의 설명 콘텐츠를 가져왔을 경우, 헤더 설명을 먼저 선택하고 본문 요청 중의 XML 설명은 무시합니다.

**버킷의 사전 설정 ACL**

| 사전 설정 명칭           | 설명                                                               |
| ------------------ | ------------------------------------------------------------------ |
| private            | 생성자(루트 계정)는 FULL_CONTROL 권한을 가지며, 다른 사람은 권한이 없습니다.(기본값)   |
| public-read        | 생성자는 FULL_CONTROL 권한을 가지며, 익명 사용자 그룹은 READ 권한을 갖습니다.           |
| public-read-write  | 생성자와 익명 사용자 그룹이 모두 FULL_CONTROL 권한을 가지며, 이 권한을 부여하는 것은 권장하지 않습니다. |
| authenticated-read | 생성자는 FULL_CONTROL 권한을 가지며, 인증 사용자 그룹은 READ 권한을 갖습니다.           |

**객체의 사전 설정 ACL**

| 사전 설정 명칭                  | 설명                                                                         |
| ------------------------- | ---------------------------------------------------------------------------- |
| default                   | 설명이 비어 있을 때, 각 레벨 디렉터리의 명시적 설정 및 버킷의 설정에 따라 요청이 허용됐는지 확인합니다.(기본값) |
| private                   | 생성자(루트 계정)는 FULL_CONTROL 권한을 가지며, 다른 사람은 권한이 없습니다.                     |
| public-read               | 생성자는 FULL_CONTROL 권한을 가지며, 익명 사용자 그룹은 READ 권한을 갖습니다.                     |
| authenticated-read | 생성자는 FULL_CONTROL 권한을 가지며, 인증 사용자 그룹은 READ 권한을 갖습니다.           |
| bucket-owner-read         | 생성자는 FULL_CONTROL 권한을 가지며, 버킷 소유자는 READ 권한을 갖습니다.                   |
| bucket-owner-full-control | 생성자와 버킷 소유자가 FULL_CONTROL 권한을 갖습니다.                             |

>? 객체는 public-read-write 권한 부여를 지원하지 않습니다.
>

## 예시
### 버킷의 ACL
버킷 생성 시 COS는 기본 ACL을 생성하여, 리소스 소유자가 리소스에 대한 전체 제어 권한을 부여 받도록 합니다. 예시는 다음과 같습니다.

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

**객체 생성 시, COS는 기본적으로 ACL을 생성하지 않으며, 이때 객체의 소유자는 버킷 소유자입니다**. 객체 상속 버킷의 권한은 버킷의 액세스 권한과 일치합니다. 객체는 기본적으로 ACL을 가지지 않으므로 버킷 정책(Bucket Policy) 중 방문자와 그의 동작의 정의에 따라 요청이 허용 여부를 판단합니다. 자세한 내용은 [액세스 정책 언어 개요](https://intl.cloud.tencent.com/document/product/436/18023) 문서를 참고하십시오.

객체에 기타 액세스 권한을 부여해야 할 경우, 이를 기초로 더 많은 ACL을 추가해 객체의 액세스 권한을 설명할 수 있습니다. 예를 들어 익명 사용자에게 단일 객체에 대한 읽기 전용 권한을 부여하는 방법은 다음과 같습니다.

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



