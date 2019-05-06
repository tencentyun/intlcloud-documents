## ACL 개요
접근 제어 리스트(ACL)는 리소스를 기반으로 한 접근 정책 옵션 중 하나로 버킷 및 객체의 접근 관리에 사용됩니다. ACL을 사용하면 다른 루트 계정, 서브 계정과 사용자 그룹에 기본적인 읽기, 쓰기 권한을 부여합니다.

#### 접근 정책과 달리 ACL로 권한을 관리하는 데 몇 가지 제한이 있습니다.
- Tencent Cloud 계정에만 권한을 부여할 수 있습니다.
- 객체 읽기, 객체 쓰기, ACL 읽기, ACL 쓰기 및 전체 권한 등 5가지 작업 그룹만 지원합니다.
- 효력 조건을 부여하지 못합니다.
- 거부 효력 표시는 지원하지 않습니다.

#### ACL에서 지원하는 제어 단위:
- 버킷(Bucket)
- 접두사(Prefix)
- 객체(Object)

## ACL의 제어 요소
버킷 또는 객체 생성 시, 리소스가 소속된 루트 계정은 리소스에 대한 전체 권한을 가지지만, 수정이나 삭제할 수는 없습니다. ACL을 사용하여 다른 Tencent Cloud 계정에 접근 권한을 부여할 수 있습니다. 다음은 버킷 ACL의 예시입니다.
```xml
<AccessControlPolicy>
  <Owner>
    <ID>qcs::cam::uin/12345:uin/12345</ID>
    <DisplayName>qcs::cam::uin/12345:uin/12345</DisplayName>
  </Owner>
  <AccessControlList>
    <Grant>
      <Grantee xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="RootAccount">
        <ID>qcs::cam::uin/12345:uin/12345</ID>
        <DisplayName>qcs::cam::uin/12345:uin/12345</DisplayName>
      </Grantee>
      <Permission>FULL_CONTROL</Permission>
    </Grant>
    <Grant>
      <Grantee xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="RootAccount">
        <ID>qcs::cam::uin/54321:uin/54321</ID>
        <DisplayName>qcs::cam::anyone:anyone</DisplayName>
      </Grantee>
      <Permission>READ</Permission>
    </Grant>
  </AccessControlList>
</AccessControlPolicy>
```
ACL에는 버킷에 대한 전체 권한을 가지고 있는 버킷 소유자를 식별할 수 있는 Owner 요소가 포함되어 있고, 동시에 Grant 요소는 `qcs::cam::anyone:anyone`의 READ 권한 형식으로 표시되는 익명의 읽기 권한을 부여합니다.

### 권한 부여받은 자
#### 루트 계정
다른 루트 계정에 사용자 접근 권한을 부여할 수 있으며, CAM에서 의뢰인(principal)의 정의를 사용하여 권한을 부여할 수 있습니다. 다음과 같습니다.
```
qcs::cam::uin/1238423:uin/1238423
```

#### 서브 계정
사용자 루트 계정에 속한 서브 계정 또는 다른 루트 계정에 속한 서브 계정에 권한을 부여할 수 있으며, CAM에서 의뢰인(principal)의 정의를 사용하여 권한을 부여할 수 있습니다. 다음과 같습니다.
```
qcs::cam::uin/1238423:uin/3232
```

#### 익명 사용자
익명 사용자에게 접근 권한을 부여할 수 있으며, CAM에서 의뢰인(principal)의 정의를 사용하여 권한을 부여할 수 있습니다. 다음과 같습니다.
```
qcs::cam::anyone:anyone
```

### 권한 작업 그룹
다음 표는 ACL에서 지원하는 권한 작업 그룹입니다.

| 작업 그룹         | 버킷             | 접두사           | 객체  |
| ------------ | ----------------- | ---------------- | --------- |
| READ         | 버킷의 객체 나열 및 읽기      | 디렉터리의 객체 나열 및 읽기  | 객체 읽기    |
| WRITE        | 버킷의 객체 생성, 덮어쓰기 및 삭제하기 | 디렉터리의 임의 객체 생성, 덮어쓰기 및 삭제하기 | 객체 덮어쓰기 및 삭제   |
| READ_ACP     | 버킷의 ACL 읽기        | 디렉터리의 ACL 읽기       | 객체의 ACL 읽기 |
| WRITE_ACP    | 버킷의 ACL 수정        | 디렉터리의 ACL 수정       | 객체의 ACL 수정 |
| FULL_CONTROL | 버킷 및 객체에 대한 임의 조작      | 디렉터리의 객체에 대한 임의 조작     | 객체에 대해 임의 조작 실행 |

### 표준 ACL 설명
COS는 사전 정의된 일련의 라이센싱을 지원하며, 표준 ACL이라 부릅니다. 다음 표는 표준 ACL 라이센싱 정의에 대해 나열하였습니다.
> **주의:**
> 루트 계정은 항상 FULL_CONTROL 권한이 있으므로 이에 대해 특별히 설명하지 않습니다.

| 표준 ACL            | 의미                                      |
| ----------------- | --------------------------------------- |
|(공백)               | 기본 정책으로 다른 사람은 권한이 없고, 리소스는 상위 권한을 계승합니다.                 |
| private           | 다른 사람은 권한이 없습니다.  |
| public-read       | 익명 사용자 그룹은 READ 권한을 가집니다. |
| public-read-write | 익명 사용자 그룹은 READ와 WRITE 권한을 가집니다. 일반적으로 버킷에 이 권한을 부여하는 것은 권장하지 않습니다. |

## ACL 예시
### 버킷에 대한 ACL 설정
다음 예시는 다른 루트 계정이 버킷에 대한 읽기 권한을 가질 수 있다는 것을 보여줍니다:
![버킷에 대한 ACL 설정](//(//mc.qcloudimg.com/static/img/7088f7b6c3336668b4b04f63392e069d/image.png)

### 객체에 대한 ACL 설정
다음 예시는 다른 루트 계정이 객체에 대한 읽기 권한을 가질 수 있다는 것을 보여줍니다:
![객체에 대한 ACL 설정](//(//mc.qcloudimg.com/static/img/9ed379e66236d84bdd3c070e99f95e7d/image.png)
