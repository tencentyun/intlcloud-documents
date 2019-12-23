## 기본 개념
접근 권한 부여는 사용자가 접근자가 어떤 사람이고 어떤 조건에서 어떤 리소스에 대해 구체적인 작업을 실행하는 제어 능력 조합입니다. 따라서 하나의 접근 권한 행위를 설명할 때, 일반적으로 **신분, 리소스, 작업, 조건(옵션)**이 4가지의 요소를 포함합니다.

## 접근 권한 요소

### Tencent Cloud의 ID

사용자가 Tencent Cloud 계정을 등록할 때, 시스템은 Tencent Cloud 서비스에 로그인하는 루트 계정 신분 하나를 생성합니다. Tencent Cloud 루트 계정은 사용자 관리 기능을 통해 다른 역할을 맡은 분류 사용자를 관리합니다. 사용자 유형은 **협력자, 메시지 수신자, 서브 계정과 역할** 등을 포함합니다. 자세한 정의는 CAM의 [신분 관리](https://intl.cloud.tencent.com/document/product/598/13665)와 [용어집](https://intl.cloud.tencent.com/document/product/598/18564) 문서를 참조하십시오.

### COS의 리소스

 버킷과 객체는 COS의 기본 리소스입니다. 그 중 그들은 모두 관련 서브 리소스를 갖고 있습니다.

버킷의 서브 리소스를 다음을 포함합니다.

- acl과 policy: 버킷의 접근 제어 정보
- website: 버킷의 정적 웹사이트 호스팅 구성
- tagging: 버킷의 태그 정보
- cors: 버킷의 크로스 도메인 구성 정보
- lifecycle: 버킷의 수명 주기 구성 정보

객체의 서브 리소스는 다음을 포함합니다.

- acl: 객체의 접근 제어 정보
- restore: 보관 유형 객체의 복원 구성

### COS의 작업

COS는 일련의 리소스에 대상한 API 작업을 제공합니다. 자세한 내용은 [작업 리스트](https://cloud.tencent.com/document/product/436/10111) 문서를 참조하십시오.

## CAM 개요

### 비공개 원칙

**기본 상황에서 Tencent Cloud COS의 리소스는 모두 비공개입니다.**

리소스 소유자(버킷 리소스를 생성하는 Tencent Cloud 루트 계정)는 해당 리소스의 최고 권한을 갖고 있으며 리소스 소유자는 접근 정책을 편집하거나 수정하여 다른 사람 또는 익명 사용자에게 접근 권한을 부여할 수 있습니다.

Tencent Cloud CAM 계정에 버킷을 생성하거나 객체를 업로드할 경우 그 상위 루트 계정이 리소스 소유자입니다.

버킷 소유자의 루트 계정은 다른 Tencent Cloud 루트 계정에게 객체 업로드 권한(즉, 계정 간 업로드)을 부여할 수 있습니다. 이 상황에서 객체 소유자는 여전히 버킷 소유자의 루트 계정입니다.

## 접근 제어 정책

#### 리소스 기반 정책

COS는 **버킷**과 **객체** 차원에서 각각 접근 제어를 지원합니다. 구체적인 내용은 다음 표를 참조하십시오.

| 차원   | 유형                   | 설명 방식 | 지원하는 ID                                       | 지원 리소스 세분화       | 지원 작업         | 지원 효력    |
| ------ | ---------------------- | -------- | ------------------------------------------------ | -------------------- | ------------------ | ------------- |
| Bucket | 접근 정책 언어 | JSON     | 서브 계정, 역할, Tencent Cloud 서비스, 기타 루트 계정, 익명 사용자 등 | 버킷, 객체, 접두사 등 | 각 구체적 작업   | 허용/거부 명시 |
| Bucket | ACL   | XML      | 다른 루트 계정, 익명 사용자                             | 버킷               | 작업한 읽기/쓰기 권한 | 허용만        |
| Object | ACL     | XML      |  다른 루트 계정, 익명 사용자                             | 객체                 | 작업한 읽기/쓰기 권한 | 허용만        |

**버킷 정책**

버킷 정책은 JSON 언어를 사용하여 설명하며 익명 ID 또는 Tencent Cloud의 모든 CAM 계정에 버킷 및 버킷 작업, 객체 및 객체 작업에 대한 권한 부여를 지원합니다. Tencent Cloud COS의 버킷 정책은 해당 버킷의 거의 모든 작업을 관리할 수 있기 때문에 ACL로 불가능한 접근 정책을 관리할 때 버킷 정책을 사용하는 것을 권장합니다.

>! Tencent Cloud 루트 계정은 계정에 포함된 리소스(버킷 포함)의 최대 권한을 갖고 있습니다. 버킷 정책에서 거의 모든 작업을 제한할 수 있지만 루트 계정은 항상 PUT Bucket Policy 작업 권한을 갖고 있습니다. 루트 계정이 이 작업을 호출하면 버킷 정책을 검사하지 않습니다.

다음은 익명 사용자에게 광저우에 위치한 버킷 `examplebucket-1250000000`의 모든 객체에 대한 접근을 허용한 정책으로서 서명을 인증할 필요없이 버킷의 모든 객체(GetObject)를 다운로드할 수 있습니다. 즉, URL을 아는 익명 사용자는 모두 객체(공인 읽기 방식과 비슷함)를 다운로드할 수 있습니다.

```json
{
  "Statement": [
    {
      "Principal": "*",
      "Effect": "Allow",
      "Action": ["cos:GetObject"],
      "Resource": ["qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/*"]
    }
  ],
  "Version": "2.0"
}
```

**ACL**

ACL은 XML 언어를 사용하여 설명하며 리소스와 연결된 권한 부여자 지정 및 권한 부여 리스트입니다. 매개 버킷과 객체는 모두 이에 연결되는 ACL은 익명 사용자 또는 기타 Tencent Cloud 루트 계정에 기본 읽기/쓰기 권한 부여를 지원합니다.

>! 리소스 소유자는 발행한 ACL의 이 항목 설명 여부와 상관없이 리소스에 대한 FULL_CONTROL 권한을 항상 갖고 있습니다.

다음은 한 버킷의 ACL 예시로서. 버킷 소유자(사용자 UIN: 1250000000)의 완전 제어 권한을 설명하였습니다.

```xml
<AccessControlPolicy>
  <Owner>
    <ID>qcs::cam::uin/1250000000:uin/1250000000</ID>
  </Owner>
  <AccessControlList>
    <Grant>
      <Grantee xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="RootAccount">
        <ID>qcs::cam::uin/1250000000:uin/1250000000</ID>
      </Grantee>
      <Permission>FULL_CONTROL</Permission>
    </Grant>
  </AccessControlList>
</AccessControlPolicy>
```

다음은 한 버킷의 ACL 예시입니다. 객체 소유자(사용자 UIN: 1250000000)의 완전 제어 권한을 설명하였으며 모든 사람에게 읽기(익명 사용자의 공개 읽기) 권한을 부여하였습니다.

```xml
<AccessControlPolicy>
  <Owner>
    <ID>qcs::cam::uin/1250000000:uin/1250000000</ID>
  </Owner>
  <AccessControlList>
    <Grant>
      <Grantee>
        <ID>qcs::cam::uin/1250000000:uin/1250000000</ID>
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

#### 사용자 기반 정책

사용자는 CAM 에서 루트 계정에 포함된 다른 유형의 사용자에게 다른 권한을 부여할 수 있습니다.

사용자 정책과 버킷 정책의 가장 큰 차이는 사용자 정책은 효력, 작업, 리소스와 조건(옵션)만 설명하고 의뢰인을 설명하지 않습니다. 그렇기 때문에 사용자 정책은 작성 완료 후, 서브 계정, 사용자 그룹 또는 역할에 연결 작업을 해야 하고 사용자 정책에서 작업과 리소스 권한을 익명 사용자에게 부여하는 것을 지원하지 않습니다.

[사전 정의된 정책으로 연결 권한 부여](https://intl.cloud.tencent.com/document/product/598/10602)하거나 [사용자 정책 자체 작성](https://intl.cloud.tencent.com/document/product/598/10603)한 후, 지정 의뢰인에 연결하면 하위 계정의 접근 제어를 구현할 수 있습니다.

다음은 광저우에 위치한 버킷 `examplebucket-1250000000`의 모든 COS 작업 권한 부여 정책입니다. 정책을 저장한 후 다시 CAM 서브 계정, 사용자 그룹 또는 역할에 연결해야 적용합니다.

```json
{
  "Statement": [
    {
      "Effect": "Allow",
      "Action": ["cos:*"],
      "Resource": [
          "qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/*",
          "qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/"
      ]
    }
  ],
  "Version": "2.0"
}
```
