## ACL 개요
액세스 제어 리스트(ACL)는 리소스의 액세스 정책 옵션으로, 버킷 및 객체의 액세스를 관리할 수 있으며 다른 루트 계정 및 서브 계정, 사용자 그룹에 기본적인 읽기, 쓰기 권한을 부여할 수 있습니다.

**액세스 정책과의 차이점은 ACL은 관리 권한에 다음과 같은 제한이 존재한다는 것입니다.**
- Tencent Cloud 계정에만 권한 부여 가능
- 객체 읽기, 객체 쓰기, ACL 읽기, ACL 쓰기, 모든 권한 등 다섯 개 작업 그룹만 지원
- 효력 발생 조건 부여 지원하지 않음
- 명시적 거부 효과 지원하지 않음

**ACL이 지원하는 제어 단위:**
- 버킷(Bucket)
- 객체 키 접두사(Prefix)
- 객체(Object)

## ACL의 제어 요소
버킷 또는 객체 생성 시, 해당 리소스가 소속된 루트 계정이 리소스에 대한 모든 권한을 가지며 수정 또는 삭제할 수 없습니다. ACL을 통해 다른 Tencent Cloud 계정에 액세스 권한을 부여할 수 있습니다.
버킷의 ACL 예시는 다음과 같습니다. 여기에서 100000000001은 루트 계정, 100000000011은 루트 계정 아래의 서브 계정, 100000000002는 다른 루트 계정을 나타냅니다. ACL에는 해당 버킷의 소유자인 Owner를 식별할 수 있는 요소가 포함되어 있으며, 해당 버킷의 소유자는 버킷의 모든 권한을 가지고 있습니다. 또한 Grant 요소에서 익명 읽기 권한을 부여하며, `http://cam.qcloud.com/groups/global/AllUsers`의 READ 권한 형식으로 표시합니다.

```shell
<AccessControlPolicy>
  <Owner>
    <ID>qcs::cam::uin/100000000001:uin/100000000001</ID>
    <DisplayName>qcs::cam::uin/100000000001:uin/100000000001</DisplayName>
  </Owner>
  <AccessControlList>
    <Grant>
      <Grantee xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="RootAccount">
        <ID>qcs::cam::uin/100000000001:uin/100000000001</ID>
        <DisplayName>qcs::cam::uin/100000000001:uin/100000000001</DisplayName>
      </Grantee>
      <Permission>FULL_CONTROL</Permission>
    </Grant>
    <Grant>
      <Grantee xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="Group">
        <URI>http://cam.qcloud.com/groups/global/AllUsers</URI>
      </Grantee>
      <Permission>READ</Permission>
    </Grant>
  </AccessControlList>
</AccessControlPolicy>
```



#### 권한 부여자
**루트 계정**
다른 루트 계정에 사용자 액세스 권한을 부여할 수 있으며, CAM의 위탁인(principal) 정의를 이용해 권한을 부여할 수 있습니다. 예시는 다음과 같습니다.
```bash
qcs::cam::uin/100000000002:uin/100000000002
```

**서브 계정**
사용자의 루트 계정 아래의 서브 계정(예: 100000000011) 또는 다른 루트 계정 아래의 서브 계정에 권한을 부여할 수 있으며, CAM의 위탁인(principal) 정의를 이용해 권한을 부여할 수 있습니다. 예시는 다음과 같습니다.
```bash
qcs::cam::uin/100000000001:uin/100000000011
```

- **익명 사용자**
익명 사용자에게 액세스 권한을 부여할 수 있으며, CAM의 위탁인(principal) 정의를 이용해 권한을 부여할 수 있습니다. 예시는 다음과 같습니다.
```bash
http://cam.qcloud.com/groups/global/AllUsers
```

#### 권한 작업 그룹
 ACL이 지원하는 권한 작업 그룹은 다음 표와 같습니다.

| 작업 그룹          | 버킷 액세스 권한             | 접두사 액세스 권한             | 객체 액세스 권한      |
| ------------ | ----------------- | ---------------- | --------- |
| READ         | 버킷의 객체 조회 및 읽기      | 디렉터리 아래의 객체 조회 및 읽기      | 객체 읽기      |
| WRITE        | 버킷의 모든 객체 생성, 덮어쓰기, 삭제 | 디렉터리 아래의 모든 객체 생성, 덮어쓰기, 삭제 | 지원하지 않음  |
| READ_ACP     | 버킷의 ACL 읽기        | 디렉터리 아래의 ACL 읽기       | 객체의 ACL 읽기 |
| WRITE_ACP    | 버킷의 ACL 수정        | 디렉터리 아래의 ACL 수정       | 객체의 ACL 수정 |
| FULL_CONTROL | 버킷 및 객체에 대한 모든 작업      | 디렉터리 아래의 객체에 대한 모든 작업     | 객체에 대해 실행하는 모든 작업 |

#### 표준 ACL 설명
COS는 일련의 사전 설정 권한을 지원합니다. 이를 표준 ACL이라 부르며, 표준 ACL의 권한 부여에 대한 의미는 다음 표와 같습니다.

>!루트 계정은 항상 FULL_CONTROL 권한을 가지므로 이에 대한 설명은 다음 표에 포함되어 있지 않습니다.

| 표준 ACL            | 의미                                      |
| ----------------- | --------------------------------------- |
| (비어 있음)               | 기본 정책. 다른 사용자에게 권한이 없으며, 리소스는 상위 권한 상속                 |
| private           | 다른 사용자에게 권한 없음                               |
| public-read       | 익명의 사용자 그룹에게 READ 권한이 부여됨                        |
| public-read-write | 익명의 사용자 그룹에게 READ 및 WRITE 권한이 부여됨. 버킷에 해당 권한 부여는 권장하지 않음 |

## 사용 방법

### 콘솔을 이용한 CAL 작업

**버킷에 ACL 설정**
다음은 다른 루트 계정에 특정 **버킷**의 읽기 권한을 부여하는 예시입니다.
![](https://main.qcloudimg.com/raw/d7fdfdcf75abd5b34fa3fc704f134ed1.png)

**객체에 ACL 설정**
다음은 다른 루트 계정에 특정 **객체**의 읽기 권한을 부여하는 예시입니다.
![](https://main.qcloudimg.com/raw/436257b395fd84afe85a5448d9b3280c.png)

>!- 서브 계정을 사용해 버킷 또는 객체에 액세스할 때 **액세스 권한 없음** 안내가 표시되는 경우, 먼저 루트 계정에서 서브 계정에 버킷에 정상적으로 액세스할 수 있는 권한을 부여해야 합니다. 이에 대한 자세한 작업 방법은 [서브 계정으로 버킷 리스트에 액세스](https://intl.cloud.tencent.com/document/product/436/17061)를 참조하십시오.

### API를 이용한 ACL 작업

**버킷 ACL**

| API                                                          | 작업명         | 설명                                |
| :----------------------------------------------------------- | :------------- | :-------------------------------------- |
| [PUT Bucket acl](https://intl.cloud.tencent.com/document/product/436/7737) |   버킷 ACL 설정 | 지정 버킷 액세스 권한 제어 리스트 설정  |
| [GET Bucket acl](https://intl.cloud.tencent.com/document/product/436/7733) | 버킷 ACL 조회  | 	버킷 액세스 제어 리스트 조회 |

**객체 ACL**

| API                                                          | 작업명       | 설명                                      |
| :----------------------------------------------------------- | :----------- | :-------------------------------------------- |
| [PUT Object acl](https://intl.cloud.tencent.com/document/product/436/7748) | 객체 ACL 설정| 버킷의 한 객체의 액세스 제어 리스트 설정  |
| [GET Object acl](https://intl.cloud.tencent.com/document/product/436/7744) | 객체 ACL 조회 | 객체 액세스 제어 리스트 조회                |

